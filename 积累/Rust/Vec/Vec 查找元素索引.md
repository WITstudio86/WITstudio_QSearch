```rust
// 找到第一次出现的 2 的索引
println!("{}", arr.iter().position(|&x| x == 2).unwrap());
```

> `.position()` 返回一个 Option , 找到的话返回`Some(索引)` , 否则返回`None` 

