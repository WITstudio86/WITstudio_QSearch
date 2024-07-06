- `tokio::task::spawn` 已经废弃现在使用`tokio::spawn` 等价的
	- 创建的时候就已经开始执行
	- 通过 joinHandle`.await` 只是为了等待结果避免主进程在线程未结束的时候就结束了 , 看不到结果

通过通道实现的[锁](锁.md)中的多线程操作同一片数据问题的另一种解法
```rust
use tokio::{spawn, sync::mpsc};

#[tokio::main]
async fn main() {
    let mut vec = vec![1, 2, 3, 4, 5];
    // tx可以认为是生产者 , rx 是消费者 , 只有 rs 可以操作数据
    // 100 是通道容量
    let (tx , mut rx) = mpsc::channel::<u32>(100);

    let channel1 = tx.clone();
    let channel2 = tx.clone();

    // creat two spwan
    let a = spawn(async move {
        // 操作的时候发送消息
        // 校准发送写法
        if let Err(_) = channel1.send(50).await{
            println!("spawn1 send error");
        }else {
            println!("spawn1 send success");
        }
    });

    let b = spawn(async move {
        if let Err(_) = channel2.send(100).await{
            println!("spawn2 send error");
        }else {
            println!("spawn2 send success");
        }
    });

    let c = spawn(async move{
        // 常见接收操作
        while let Some(v) = rx.recv().await {
            println!("recv value is {}", v);
            vec[2] = v;
            println!("vec = {:?}" , vec);
        }
    });
 
    _ = a.await;
    _ = b.await;
    _ = c.await;

    println!("code end");
}
```