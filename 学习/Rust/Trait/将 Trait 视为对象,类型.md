# 将 Trait 视为对象,类型

- 想要实现一个函数可能会返回多种类型的值
	- 使用枚举
		- 写死的类型 , 修改成员就要修改整个枚举
	- 使用 Trait 对象
		- 开放的类型 , 只要实现了某个 Trait 就会自动成为一部分

```rust
struct TypeA;
struct TypeB;
struct TypeC;

trait TraitFlag {}

impl TraitFlag for TypeA {}
impl TraitFlag for TypeB {}
impl TraitFlag for TypeC {}

fn func()->impl TraitFlag{
    TypeA
}

fn main() {
    func();
}
```
==但是这种写法不能用在 if 语句上 , 因为这种写法在编译的时候其实会自动展开为 3 个返回不动类型的函数 , 进行自动调用 , 但是if语句的不同分支是 3 种类型 , 所以会报错== 

## 需要 Trait 作为一个整体而不是展开

- 将`impl` 修改为`dync` 即可不展开的, 把实现 Trait 的所有类型视为一种类型的使用了
- 但是此时的返回值所占用尺寸在编译器是无法确定的 , 所以需要使用Box 将其移动到堆上

```rust
struct TypeA;
struct TypeB;
struct TypeC;

trait TraitFlag {}

impl TraitFlag for TypeA {}
impl TraitFlag for TypeB {}
impl TraitFlag for TypeC {}

fn func(n:u8) -> Box<dyn TraitFlag> {
    if n == 1{
        Box::new(TypeA)
    }else if n == 2{
        Box::new(TypeB)
    }else{
        Box::new(TypeC)
    }
}

fn main() {
    func(1);
    func(2);
    func(3);
}
```

```rust

```