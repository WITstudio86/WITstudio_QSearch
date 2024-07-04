# Option 和 Result 之间的转换

## Option 到 Result

- 使用 `.ok_or` 方法
	- 如果 Option 的结果是 Some, 那么就转换为 `Ok(Some 的值)`
	- 如果 Option 的结果是 None , 那么就转换为 `Err(携带参数值)`

```rust
fn main() {
    assert_eq!(Some(123).ok_or("错误") , Ok(123));
    assert_eq!(None::<i32>.ok_or("错误") , Err("错误"));
}
```

## Result 到 Option

> 这中转换需要考虑保留什么数据到 Option 中


### ok()

- 如果是 Ok 就将值放入 `Some()`中
- 如果是 Err 就转换为 `None`

```rust
assert_eq!(Ok::<i32,()>(4).ok(), Some(4));
```

### err()

- 如果是 err , 将 err 携带的信息放入 `some()` 
- 如果是 Ok , 返回 None

```rust
assert_eq!(Err::<i32,&str>("error").err() , Some("Error"));
```