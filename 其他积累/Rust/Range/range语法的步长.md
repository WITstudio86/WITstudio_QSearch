
使用 `.step_by(步长)` 的方式设置步长

```rust
for i in (2..=n as usize).step_by(2) {
	if arr[i] {
		print!("{} ", i);
	}
}
```