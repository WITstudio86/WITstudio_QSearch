要把任何类型转换成 `String`，只需要实现那个类型的 [`ToString`](https://rustwiki.org/zh-CN/std/string/trait.ToString.html) trait。然而不要直接这么做，您应该实现[`fmt::Display`](https://rustwiki.org/zh-CN/std/fmt/trait.Display.html) trait，它会自动提供 [`ToString`](https://rustwiki.org/zh-CN/std/string/trait.ToString.html)，并且还可以用来打印类型，

[实现Display](../输入输出/实现Display.md)

## 使用 string::ToString Trait

