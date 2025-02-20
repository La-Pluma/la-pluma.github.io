---
title: 读书笔记-大话设计模式 Ch1-
date: 2024-09-24 23:12:19
hidden: true
tags:
- 读书笔记
- 设计模式
categories:
- 读书笔记-设计模式
---

**好的代码可维护, 可复用, 可扩展, 灵活性强.**

<!--more-->

<p><font size = 5><b>目录</b></font></p>

- [Additional : UML类图](#additional--uml类图)
  - [什么是UML](#什么是uml)
  - [UML类图的示例](#uml类图的示例)
- [Chapter 1: 简单工厂模式(Simple Factory)](#chapter-1-简单工厂模式simple-factory)
- [Chapter2 : 策略模式(Strategy)](#chapter2--策略模式strategy)

## Additional : UML类图

**在线UML工具:** <https://www.plantuml.com/plantuml/uml>

### 什么是UML

**统一建模语言UML(Unified Modeling Language)** 是一种脚本语言, 是一种开放的方法, 用于说明, 可视化, 构建和编写一个正在开发的, 面向对象的, 软件密集系统的产品的开放方法.

简单来说, 对于应用的人, 可以通过简单的语言来生成描述的图像(包括类图, 时序图等).

### UML类图的示例

![pic2-2](BookNote-DesignPatterns-by-JieCheng-2/pic2-2.png)

关于UML类图的介绍在Internet中有充足的资料和手册, 书中也有简单的规约介绍, 笔者在此不详细介绍UML图的语法和规约.(或者待专门出一期整理UML用法的栏目)

## Chapter 1: 简单工厂模式(Simple Factory)

先来看看书中给的例子:

```C#
//简单工厂类
public class OperationFactory{
    public static Operation createOperate(string operate){
        Operation oper = null;
        switch (operate){
            case "+":
                oper = new OperationAdd();
                break;
            case "-":
                oper = new OperationSub();
                break;
            case ...
            ...
        }
        return oper;
    }
}

//应用端
Operation oper;
oper = OperationFactory.createOperate("+");
oper.NumberA = 1;
oper.NumberB = 2;
double result = oper.GetResult();
```

UML图如下:

![pic2-1](BookNote-DesignPatterns-by-JieCheng-2/pic2-1.png)

简单来说, 就是通过一个简单工厂类`XXXFactory`生产"产品"(实例化类),即**有一个专门的类负责创建实例的过程**. 这样修改后端的功能时(比如说添加新的运算类), 前端的逻辑不需要重构(以上述例子中只需要修改`createOperate("+")->createOperate("-")`); 同时后端的具体实现细节没有暴露给前端, 降低了耦合度.

## Chapter2 : 策略模式(Strategy)

- 面向对象的编程, 并不是类越多越好, 类的划分是为了封装, 但分类的基础是抽象, 具有相同属性和功能的对象的抽象集合才是类.

**策略模式(Strategy)** 定义了算法家族, 分别封装起来, 让它们之间相互替换, 此模式让算法的变化不会影响到使用算法的客户.

![pic2-3](BookNote-DesignPatterns-by-JieCheng-2/pic2-3.png)