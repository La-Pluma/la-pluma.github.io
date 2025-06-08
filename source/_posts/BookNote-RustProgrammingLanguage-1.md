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

<p><font size = 5><b>目录</b></font></p>

- [书籍基本信息](#书籍基本信息)
- [Chapter1 Rust部署](#chapter1-rust部署)
  - [安装](#安装)
  - [使用Cargo管理Rust项目](#使用cargo管理rust项目)
- [Chapter2 快速入门](#chapter2-快速入门)
- [Chapter3 编程概念](#chapter3-编程概念)
  - [3.1 变量和可变性](#31-变量和可变性)
    - [3.1.1 变量](#311-变量)
    - [3.1.2 常量](#312-常量)
    - [3.1.3 遮蔽](#313-遮蔽)
  - [3.2 数据类型](#32-数据类型)

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
