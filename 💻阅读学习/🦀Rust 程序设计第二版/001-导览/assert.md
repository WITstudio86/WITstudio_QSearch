## assert 是不可跳过的
- 不论是`--release` 还是默认编译的结果都是不会跳过`assert!` 宏的
- `debug_assert!` 在编译模式下会忽略来增加运行速度

例如下面程序:

```rust
fn main() {
    println!("{}", gcd(0, 6));
}

fn gcd(mut m: u64, mut n: u64) -> u64 {
    debug_assert!(m != 0 && n != 0);
    if m < n {
        let t = m;
        m = n;
        n = t;
    }
    while m != 0 {
        m = m % n;
    }
    n
}
```
在默认编译下会执行 `debug_assert!` 宏 , 直接在第 6 行处 panic , 但是如果通过 `--release` 编译则不会执行第六行的 `debug_assert!` 所以在 m 接收的参数为 `0` 的时候会报处除零错误

## assert_eq

