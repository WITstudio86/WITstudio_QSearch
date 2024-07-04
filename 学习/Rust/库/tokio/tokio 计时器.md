
```rust
use std::time::Duration;

use anyhow::{Ok, Result};
use tokio::time;

async fn doit() -> Result<()> {
    // 定义时间间隔
    let mut interval = time::interval(Duration::from_millis(2000));
    // 2秒
    interval.tick().await;
    println!("2 秒过去了");
    // 又 2 秒 
    interval.tick().await;
    println!("4 秒过去了");
    Ok(())
}

#[tokio::main]
async fn main() {
    println!("starting");
    doit().await.unwrap();
    println!("code end")
}
```