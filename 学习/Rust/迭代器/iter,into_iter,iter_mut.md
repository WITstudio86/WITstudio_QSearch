- `iter()` 获取由元素的不可变引用组成的迭代器
- `iter_mut()` 获取由元素的可变引用组成的迭代器
- `into_iter()` 获取元素所有权组成的迭代器

```rust
fn main() {
    let mut arr = [1,2,3,4];
    let mut i_arr = arr.iter();
    assert_eq!(&1 , i_arr.next().unwrap());
    assert_eq!(&2 , i_arr.next().unwrap());
    assert_eq!(&3 , i_arr.next().unwrap());
    assert_eq!(&4 , i_arr.next().unwrap());

    let mut i_mut_arr = arr.iter_mut();
    assert_eq!(&mut 1 , i_mut_arr.next().unwrap());
    assert_eq!(&mut 2 , i_mut_arr.next().unwrap());
    assert_eq!(&mut 3 , i_mut_arr.next().unwrap());
    assert_eq!(&mut 4 , i_mut_arr.next().unwrap());

    let mut i_i_arr = arr.into_iter();
    assert_eq!(1 , i_i_arr.next().unwrap());
    assert_eq!(2 , i_i_arr.next().unwrap());
    assert_eq!(3 , i_i_arr.next().unwrap());
    assert_eq!(4 , i_i_arr.next().unwrap());
}
```