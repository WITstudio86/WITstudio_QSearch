## 来自2015的方法版的组织方法

```
├── Cargo.lock
├── Cargo.toml
├── outputmd.md
└── src
    ├── getsum
    │   ├── getsum1.rs
    │   ├── getsum2.rs
    │   └── mod.rs
    └── main.rs
```
> getsum 可以理解为拆分出来的一个模块 , 其中的 mod.rs 中通过`mod` 关键字导入当前模块中的其他文件 , 通过`pub` 可以选择公开出来的的内容
> 在 main 中可以通过 mod 导入需要的模块

> - num模块中的PrimInt 用于限制整数[限制数字](../Trait/限制数字.md)

==main.rs==
```rust
use getsum::{getsum1, getsum2};

mod getsum;

fn main() {
    let result1 = getsum1::get_sum(1, 2);
    let result2 = getsum2::get_sum(vec![1,2]);
}
```

==getsum/mod.rs==
```rust
pub mod getsum1;
pub mod getsum2;
```

==getsum/getsum1.rs==
```rust
use num::PrimInt;

pub fn get_sum<T:PrimInt>(a:T,b:T)->T{
    a + b
}
```

==getsum/getsum2.rs==
```rust
use num::PrimInt;

pub fn get_sum<T:PrimInt>(arr:Vec<T>)->T{
    arr.iter().fold(T::zero(),|acc,x| acc + *x)
}
```

## 其他方式

- 将 mod.rs 移出所在文件夹并将其重命名为文件夹的名字即可 , 其他内容不变
