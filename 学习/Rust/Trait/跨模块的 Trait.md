- 如果再模块 A 中一个类型实现了某个 Trait
- 即使这个类型和 Trait 都是 pub 状态 , 在另一个模块中使用的时候也会报错
- 需要在使用这个类型的同时将 Trait 也 use 到当前的 scope

```rust
use mode_b::fun;

fn main() {
    fun()
}

mod mode_a{
    pub trait ATrait {
        fn play(&self){
            println!("play");
        }
    }
    pub struct AStruct;
    impl ATrait for AStruct {}
}

mod mode_b{
    // 下满这行注释了的话会报错
    use super::mode_a::ATrait;
    use super::mode_a::AStruct;
    
    pub fn fun(){
        let a = AStruct;
        a.play();
    }
}
```