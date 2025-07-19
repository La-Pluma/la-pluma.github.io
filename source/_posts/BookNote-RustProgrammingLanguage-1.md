---
title: 读书笔记-Rust程序设计语言
date: 2025-06-08 20:14:31
hidden: true
tags:
- 读书笔记
- Rust
categories:
- 读书笔记-Rust程序设计语言
---

**The Rust programming language is fundamentally about empowerment.**

<!--more-->

## 书籍基本信息

英文版: <https://doc.rust-lang.org/stable/book/>

中文版: <https://kaisery.github.io/trpl-zh-cn/>

## Chapter1 Rust部署

### 安装

见原文<https://kaisery.github.io/trpl-zh-cn/ch01-01-installation.html>

笔者使用的IDE为vscode, 推荐配置rust-analyzer插件

### 使用Cargo管理Rust项目

- `cargo new [proj_name]`, 创建一个新的Rust项目
- `cargo init`, 将当前目录初始化为一个Rust项目
  - 需要注意的是, 需要手动创建src目录并转移项目文件
  - 因此更建议从一开始就采用cargo进行项目管理
- `cargo build`, 进行编译, 生成build
  - `cargo build --release`, 花费更长的时间在编译时进行优化, 适用于release版本构建
- `cargo run`, 运行可执行文件, 默认以main作为入口
- `cargo check`, 在不生成可执行文件的情况下检验代码是否可编译

## Chapter2 快速入门

跟着书中教程走即可

## Chapter3 编程概念

**关键字(Keywords):** 由语言保留使用而不允许变量或函数定义的名称, 对于Rust, 请参见[**附录A**](https://kaisery.github.io/trpl-zh-cn/appendix-01-keywords.html)

### 3.1 变量和可变性

#### 3.1.1 变量

- 使用关键字`let`声明**变量(Variable)**
- 变量默认是**不可改变的(Immutable)**
  - 直观上来说, 这样的变量不允许**二次赋值**
- 使用`mut`关键字修饰变量使其可变

```rust
let a = 5;
a = 6; //error!

let mut b = 6;
b = 7; //pass
```

#### 3.1.2 常量

- 使用关键字`const`声明**常量(Constant)**
- 常量无法被`mut`修饰
- 常量**必须**在声明时指定类型
- 常量**只能**被常量表达式赋值
  - 与常量相比, 不可变变量允许使用一个不确定值(运行前)进行赋值; 二者的共同点是均不允许二次赋值.

```rust
let HOURS_IN_SECONDS: u32 = 60 * 60;
```

> **Additional:** Rust中的常量求值
>
> <https://doc.rust-lang.org/reference/const_eval.html#constant-evaluation>

#### 3.1.3 遮蔽

**遮蔽(Shadowing):** 定义一个与之前变量同名的新变量, 在作用域范围内, 此时的变量均视为后定义的变量

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {x}");
    let x = x + 1;
    println!("The value of x is: {x}");
    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }
    println!("The value of x is: {x}");
}
-----------------------------------------------------------------
The value of x is: 5
The value of x is: 6
The value of x in the inner scope is: 12
The value of x is: 6
```

> **Compare: shadowing & mut**
>
> 遮蔽从原来上是新建了一个变量, 因此允许覆盖定义的变量类型不同; 而可变变量从始至终都是对同一个变量操作, 因此不允许赋值不同的变量类型.
>
> ```rust
> //pass
> let spaces = "   "; // Type: String
> let spaces = spaces.len(); // Type: Integer
> //error
> let mut spaces = "   ";
> let spaces = spaces.len(); // mismatched types
> ```

### 3.2 数据类型

**数据类型(Data Type):** 包括**标量(scalar)**和**复合(compound)**

> **Tips:** Rust是**静态类型(statically typed)**语言, 在编译时就必须知道所有变量的类型; 当有多种类型可能时, 需要**显式**指定变量类型.

#### 3.2.1 标量类型

包括整型, 浮点型, 布尔类型和字符类型

##### 整型

|长度|有符号|无符号|
|:---:|:---:|:---:|
|8|i8|u8|
|16|i16|u16|
|32|i32|u32|
|64|i64|u64|
|128|i128|u128|
|32/64|isize|usize|

对于`iszie`/`usize`, 在32位机器上是32位, 在64位机器上是64位

**数字字面值:**

|数字字面值|例子|
|:---:|:---:|
|Decimal|98_222(允许使用'_'作为分隔符)|
|Hex|0xff|
|Octal|0o77|
|Binary|0b1111_0000|
|Byte(仅用于u8)|b'A'|

> **Additional: Rust中的整型溢出**
>
> - debug模式下Rust面对整型溢出的情况会使程序panic
> - `--release`模式下Rust默认采用和C++相同的处理方式(补码溢出)
>
> Rust标准库提供了处理溢出的方法
>
> ```Rust
> //wrapping_*: 正常溢出
> let a: u8 = 255;
> assert_eq!(a.wrapping_add(1), 0); // a = 0
> //checked_*: 返回None
> let b: u8 = 200;
> assert_eq!(b.checked_mul(2), None); // 200*2=400 > u8::MAX(255)
> assert_eq!(b.checked_div(0), None); // 除零错误
> //overflowing_*: 返回布尔值表示是否溢出
> let (result, overflowed) = 255u8.overflowing_add(1);
> assert_eq!(result, 0);     // 环绕结果
> assert_eq!(overflowed, true); // 标记溢出
> //saturating_*: 最大/最小值处做饱和处理
> assert_eq!(255u8.saturating_add(1), 255); // 上饱和到 u8::MAX
> assert_eq!((-128i8).saturating_sub(1), -128); // 下饱和到 i8::MIN
> assert_eq!(100u8.saturating_mul(3), 255); // 300 > 255 → 255
> ```

##### 浮点型

遵循IEEE-754标准, 包括`f32`和`f64`两种类型

##### 布尔类型

包括`ture`和`false`, 允许使用`bool`关键字标识布尔类型

##### 字符类型

使用关键字`char`标识字符类型

Rust中字符类型长度为4Bytes(32bits), 表示**Unicode标量值(Unicode Scalar Value)**, 有效值为`U+0000 ~ U+D7FF, U+E000 ~ U+10FFFF`

#### 3.2.2 复合类型

包括**元组(tuple)**和**数组(array)**

##### 元组

元组的长度在声明后**不会变化**, 元组中元素类型允许不同

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
//元组元素的访问
//方法1: 模式匹配(pattern matching)进行解构(destructure)
let (x, y, z) = tup;
println!("y: {y}");
//方法2: 索引
let five_hundred = tup.0;
let six_point_four = tup.1;
let one = tup.2;

//单元(unit): 不包含值的元组
let empty = ()
```

##### 数组

```rust
// 数组的声明
let a = [1, 2, 3, 4, 5];
let b: [i32; 5] = [1, 2, 3, 4, 5]; // 声明一个类型为i32, 长度为5的数组
let c: [3; 5]; // 等价于 let c = [3, 3, 3, 3, 3];
// 数组元素的访问
let first = a[0]; //下标从0开始
```

> **Tips:** Rust中的数组越界访问
>
> rust中面临数组的越界访问, 程序会panic而非继续执行, 这避免了某些可能会出现在c/c++中的非预期结果(例如在linux下越界访问可能会引起`segmentation fault`)

### 3.3 函数

使用关键字`fn`定义函数.

与C/C++不同, rust不关注函数定义的位置, 因此也不需要进行函数声明

```rust
fn main(){
    let ret = foo(42, 'c');
    println!("ret = {ret}")
}

fn foo(x: i32, y: char) -> i32{
    println!("x = {x}, y = {y}");
    return 5;
    // 5
    // 上述两行代码的作用完全是等价的, 但是笔者是C/C++系受众, 
    // 因此更习惯return的表达方式
}
--------------
Output
--------------
x = 42, y = c
ret = 5
```

> **Additional: 语句(Statement)和表达式(Expression)**
>
> 简单来说, 语句执行动作但无返回值, 表达式执行计算产生值
>
> 例如: `x + y`是一个表达式, 但`let z = x + y`是一个语句
>
> 在Rust中, 语句不允许作为右值出现(`let a = (let b = 3)`是非法的)

### 3.4 注释

- 用`//`标识的内容会被注释, 这与C/C++的用法是一致的
- 用`/*`和`*/`包围的内容会被注释, 同样与C/C++一致
- 用`///`标识的内容称为文档注释, 此处暂且不做展开

### 3.5 控制流

#### 3.5.1 条件控制

包括`if`, `else`, `if else`

需要注意的是, 与C/C++不同, rust的布尔表达式不会做整型到布尔类型的自动转化, 需要显式给出`number != 0`作为判断条件

```rust
if number > 0{
    println!("positive number")
} else if number == 0 {
    println!("zero")
} else {
    println!("negtive number")
}
-------
// 允许左值为表达式
if number % 2 == 0 {
    println!("even number")
} else {
    println!("odd number")
}
-------
// 允许使用if作为表达式
let condition = true;
let number = if condition { 5 } else { 6 }; // number = 5
// 需要注意的是, if表达式的所有分支必须返回相同类型的值, 否则会报错
let number = if condition { 5 } else { "6" }; //error!
```

#### 3.5.2 循环控制

```rust
------
loop
------
// 直到手动中断或执行到循环体分支中的break
loop {
    println!("again!");
}
// loop允许作为表达式返回值
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter * 2; // 返回20
    }
};
// 标签机制
// rust提供了标签机制标识嵌套的循环, 部分替代了goto的用法
let mut count = 0;
'outer: loop {
    println!("count = {count}");
    let mut remaining = 10;
    loop {
        if remaining == 9 {
            break; // 仅跳出内层循环
        }
        if count == 2 {
            break 'outer; // 跳出外层循环
        }
        remaining -= 1;
    }
    count += 1;
}
------
while
------
while condition {
    // 循环体
}
------
for
------
let a = [10, 20, 30, 40, 50];
for element in a {
    println!("the value is: {element}");
}
for number in (0..5) { // 0..5表示0,1,2,3,4
    println!("{a[number]}");
}
```

## Chapter4 所有权