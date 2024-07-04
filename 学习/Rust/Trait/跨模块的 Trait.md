- 如果再模块 A 中一个类型实现了某个 Trait
- 即使这个类型和 Trait 都是 pub 状态 , 在另一个模块中使用的时候也会报错
- 需要在使用这个类型的同时将 Trait 也 use 到当前的 scope

```rust

```