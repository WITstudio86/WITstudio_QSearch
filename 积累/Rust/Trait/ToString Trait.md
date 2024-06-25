要把任何类型转换成 `String`，只需要实现那个类型的 [`ToString`](https://rustwiki.org/zh-CN/std/string/trait.ToString.html) trait。然而不要直接这么做，您应该实现[`fmt::Display`](https://rustwiki.org/zh-CN/std/fmt/trait.Display.html) trait，它会自动提供 [`ToString`](https://rustwiki.org/zh-CN/std/string/trait.ToString.html)，并且还可以用来打印类型，

[实现Display](../输入输出/实现Display.md)

## 使用 string::ToString Trait

```rust
use std::string::ToString;

struct Circle {
    radius: i32
}

impl ToString for Circle {
    fn to_string(&self) -> String {
        format!("Circle of radius {:?}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```