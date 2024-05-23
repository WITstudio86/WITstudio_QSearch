[010-字符串](../../阅读学习/Rust%20程序设计第二版/002-基本类型/010-字符串.md)

```rust
fn main() {
	let a = String::from("hello");
	// println!("{}",a[2]);
	println!("{:?}", a.chars().nth(2).unwrap());
}
```