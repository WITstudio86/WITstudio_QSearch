结构体等涉及泛型的类型无法通过`print!("{}",vec)` 这种利用 Display 进行打印的 , 需要手动实现

```rust
use std::fmt;

#[derive(Debug)]
struct Complex {
    real: f64,
    imag: f64,
}

// 手动实现 fmt::Display
impl fmt::Display for Complex {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{} + {}i", self.real, self.imag)
    }
}

fn main(){
    let complex = Complex {
        real: 3.3,
        imag: 7.2,
    };
    println!("Debug: {:?}", complex);
    println!("Display: {}", complex);
}
```

`write!` 本身会返回一个`fmt::Result` , 如果多次使用  , 可以利用`?` 简化操作 , 避免对期间多个 `write!` 的处理

```rust
use std::fmt;

struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "[")?;
        for (count , v) in self.0.iter().enumerate() {
            if count!= 0 {
                write!(f, ", {} : {}", count,v)?;
            }else{
                write!(f, "{} : {}", count,v)?;
            }
        }
        write!(f, "]") // 注意 此处可以直接作为表达式使用
    }
}
    


fn main() {
    let list = List(vec![1, 2, 3]);
    println!("{}", list);
}
```