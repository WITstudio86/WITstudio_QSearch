# 在不使用 expect 等解包的情况下操作值的方法

## Option

### map

- 如果是 none 返回 none , 如果是 Some 将值代入闭包参数中 , 用闭包的返回值代替原值
```rust
fn main() {
    // Some 时进行操作
    let fuc = |a| a*10;
    let opt = Option::Some(18);
    assert_eq!(opt.map(fuc), Option::Some(180));
    
    // none 忽略
    let opt = Option::None;
    assert_eq!(opt.map(fuc), Option::None);
}
```

### cloned

- 将`Option(&T)` 转换为 `Option(T)`
	- 注意不是 `&Option(T)`
```rust

fn main() {
    let opt = Option::Some(&18);
    let opt = opt.cloned();
}
```

### is_some和is_none
- `is_some` 在Option 的结果是 Some 值的时候返回`true` 
- `is_none` 在 option 的结果是 None 的时候返回 `true`
```rust
fn main() {
    let opt = Option::Some(&18);
    assert_eq!(opt.is_some(), true);
    let opt = Option::None;
    assert_eq!(opt.is_some(), false);
}
```
### as_ref 和 as_mut

- `as_ref` 
	- 将`Option<T>` 或 `&Option<T>` 转换为 `Option<&T>`
- `as_mut` 
	- 将`Option<T>` 或 `&mut Option<T>` 转换为 `Option<&mut T>`

```rust
fn main() {
    let s: String = String::from("Hello World");
    let mut opt: Option<String> = Option::Some(s);

    let ref_opt: Option<&String> = opt.as_ref();

    let mut_ref_opt: Option<&mut String> = opt.as_mut();
}
```

### take
- 将`Option::Some()` 的值拿出来 , 原地留取一个`None` 
- 会发生移权

```rust

fn main() {
    let s: String = String::from("Hello World");
    let mut opt: Option<String> = Option::Some(s);

    let s: Option<String> = opt.take();// 发生移权

    println!("{:?}", opt);// None
}
```

### replace
- 将 some 中的值抛出并替换
	- 闭包不可用
```rust

fn main() {
    let mut opt = Option::Some(32);

    let old = opt.replace(64);
    println!("old: {:?}, opt: {:?}", old, opt);

    // let old = opt.replace(|x| x * 2);
    // println!("old: {:?}, opt: {:?}", old, opt);
}
```
### and_then

- 在 Option 的结果为`Some` 的时候执行闭包参数返回闭包执行的结果
	- 注意返回的结果需要是`Option<T>` 

```rust
fn main() {
    let opt = Option::Some(32);
    let result = opt.and_then(|x| Some(x * 2));

    println!("opt:{:?}, Result:{:?}", opt,result);
    // opt:Some(32), Result:Some(64)

    let result = opt.and_then(|x| Option::<i32>::None);
    println!("opt:{:?}, Result:{:?}", opt,result);
    // opt:Some(32), Result:None
}
```

## Result

- `map , is_ok , is_err , as_ref , as_mut ,and_then` 等与 Option 相同

### map_err
- 在 err 的时候, 返回包裹闭包参数返回值信息的新 Err


```rust
fn main() {
    let mut rus = Result::<i32,String>::Err("Error".to_owned());

    let new_err = rus.as_mut().map_err(|x| format!("new error message: {x}"));
    assert_eq!(new_err,Err("new error message: Error".to_owned()));

    assert_eq!(&rus,&Err("Error".to_owned()));
}
```

