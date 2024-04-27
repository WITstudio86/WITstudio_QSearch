## assert 是不可跳过的
- 不论是`--release` 还是默认编译的结果都是不会跳过`assert!` 宏的
- `debug_assert!` 在编译模式下会忽略来增加运行速度

