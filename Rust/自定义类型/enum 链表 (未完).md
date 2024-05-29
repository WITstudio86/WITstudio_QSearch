```rust
// 定义一个枚举类型 List
#[derive(Clone)]
enum List{
    Item(u32 , Box<List>),
    Nil
}

// 实现 List 枚举类型的相关方法
impl List{
    // 创建一个新的空列表
    fn new() -> List{
        Self::Nil
    }

    // 将列表转换为字符串
    fn to_string(&self) -> String{
        match *self {
            Self::Item(val , ref other) => {
                format!("[{} {}" , val , other.to_string_method())
            }
            Self::Nil => format!("[]")
        }
    }
    // 将列表中的每个元素转换为字符串，并拼接起来
    fn to_string_method(&self) -> String{
        match *self{
            Self::Item(val , ref other) => {
                format!(", {} {}" , val , other.to_string_method())
            },
            Self::Nil => format!("]")
        }
    }

    // 在列表的第一个位置添加一个新元素
    fn shift(&mut self , value:u32){
        *self = Self::Item(value, Box::new(self.clone()));
    }

    // 在列表的末尾添加一个新元素
    fn push(&mut self , value:u32){
        match *self {
            Self::Item(_, ref mut others) =>{
                others.push(value)
            },
            Self::Nil =>{
                self.shift(value)
            }
            
        }
    }

    // 在指定索引处插入一个新元素
    fn insert(&mut self , index : usize , value:u32){
        match *self {
            Self::Item(_ , ref mut others) =>{
                if index == 0{
                    self.shift(value);
                }else{
                    others.insert(index - 1 , value);
                }
            },
            Self::Nil =>{
                panic!("the index is out of range")
            }
        }
    }

    // 获取列表的长度
    fn len(&self) -> usize{
        match *self {
            Self::Item(_, ref others) => {
                1 + others.len()
            },
            Self::Nil => 0
        }
    }

}

// 主函数
fn main() {
    let mut list = List::new();
    list.shift(1);
    list.push(2);
    list.insert(1 , 100);
    println!("{}", list.to_string());
    println!("{}", list.len());
}
```