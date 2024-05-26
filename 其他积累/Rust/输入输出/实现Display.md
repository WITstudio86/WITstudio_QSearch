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

多次