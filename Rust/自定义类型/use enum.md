use 还可以用来简化枚举的书写

```rust
enum Ip{
    v4,
    v6
}

fn main() {
    use Ip::*;
    let ipv4 = v4;
    // let ipv6 = v6;
    match ipv4 {
        v4 => println!("ipv4"),
        v6 => println!("ipv6"),        
    }
}
```