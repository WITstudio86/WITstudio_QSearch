```rust
use anyhow::Result;
use tokio::{fs::File, io::AsyncWriteExt};

async fn write_file() -> Result<()> {
    // 异步创建文件
    let mut file = File::create(
        "hello.txt"
    ).await.unwrap();

    // 异步写入
    AsyncWriteExt::write_all(
        &mut file, 
        b"Hello, world!\nHello Rust!"
    ).await.unwrap();

    Ok(())
}


#[tokio::main]
async fn main() {
    write_file().await.unwrap();
}
```