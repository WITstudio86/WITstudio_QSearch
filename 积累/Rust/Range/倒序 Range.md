```rust
for i in (1..100).rev(){
	print!("{i} ");// 1 2 3 3 .. 99
}
```

```rust
fn main() {
    for n in (1..10).step_by(2).rev() {
        print!("{n} "); // 9 7 5 3 1
    }
}
```