```rust
use std::str::from_utf8;

use anyhow::{Ok, Result};
use tokio::{fs::File, io::AsyncReadExt};

// 异步读取文件内容
async fn read_file() -> Result<Vec<u8>> {
    let mut content = Vec::new();
    let mut file = File::open("hello.txt").await?;
    file.read_to_end(&mut content).await?;
    Ok(content)
}

#[tokio::main]
// Tokio 运行异步任务
async fn main() {
    let content = read_file().await.unwrap();
    println!("content: {:?}", from_utf8(&content).unwrap());
}
```