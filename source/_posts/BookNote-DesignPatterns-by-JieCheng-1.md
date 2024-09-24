---
title: 读书笔记-大话设计模式 Ch0
date: 2024-09-10 19:45:47
hidden: false
tags:
- 读书笔记
- 设计模式
categories:
- 读书笔记
---

**精彩的代码是如何想出来的, 要比看到精彩的代码更加令人期待.**

<!-- more -->

<p><font size = 5><b>目录</b></font></p>

- [书籍基本信息](#书籍基本信息)
- [Chapter 0: Preview 面向对象基础](#chapter-0-preview-面向对象基础)

---

## 书籍基本信息

《大话设计模式》程杰 2007.

本文***不提供***书籍的电子版文件, 请有需要的读者移步至**Z-library**或其他渠道获得.

本书以情景对话形式, 辅以故事或例子介绍设计模式, 以C#语言书写代码, 适合有面向过程编程基础但面向对象编程能力弱的初学者.

## Chapter 0: Preview 面向对象基础

> 附录A 培训实习生——面向对象基础
>
> **Tips:** 本部分不设计具体的语法细节, 特性和原理, 仅作示例, 如有需去可移步至专业书籍文献寻求细节, 如[**微软官方**](https://learn.microsoft.com/en-us/dotnet/csharp/)或书籍[**C#图解教程**](https://book.douban.com/subject/34894447/).

- **对象(Object):** 对象是一个自包含的实体, 用一组可识别的特性和行为来标识.

    > **Tips:** 定义比较拗口, 通俗来说, 对象是对事物的抽象, 一切事物都可以称为对象.

- **面向对象编程(Object-Oriented Programming):** 面向对象的编程.

    > **Tips:** 简称OOP, 区别于面向过程编程, 面向过程需要分析得出步骤, 按序实现程序功能. OOP首先对事物抽象为"对象", 用对象的属性和行为解决问题.

- **类(Class):** 具有相同属性和功能对象的抽象集合.

``` C#
class Cat {
    public string shout() {
        return "mew";
    }
}
```

- **实例(Instance) & 实例化:** 实例是真实的对象, new得到实例的过程称为实例化.

    > **Tips:** 类就像是工厂的蓝图, 实例就是生产出来的产品, 一个类只有实例化后才可以调用(可能不严谨, 存疑), 和蓝图与产品一样, 一个类可以实例化出多个不同的实例(**学生类**可以实例化为**学生李华**, **学生张三**等).

``` C#
Cat cat = new Cat();
```

- **修饰符:**
  - **public:** 修饰的类成员允许被任何类访问
  - **protected:** 修饰的类成员仅允许该类和其子类访问
  - **private:** 修饰的类成员仅允许该类访问

    > **Tips:** 程序设计是一门权衡和妥协的艺术, 对OOP为何如此设计的读者可自行查阅OOP发展的历史.

- **属性:** 属性是一个方法或一对方法, 在调用它的代码看来, 它是一个字段, 即属性适合于以字段的方法使用方法调用的场合.

- **字段:** 储存类设计所需的数据, 形式上是与类相关的变量.

``` C#
class Example{
    private int num; //声明一个私有内部字段, 修饰符private
    public int Num { //Num公有外部属性, 修饰符public
        get { //外部读取方法
            return Num;
        }
        set { //外部修改方法, 删去此方法时表示Num是只读的.
            Num = value; // set含有隐式参数, 由关键字value表示, 用于赋值
        }
    }
}
```

> **Tips:** 属性和字段的描述比较抽象, 推荐直接结合代码理解. 笔者认为是一种语法糖上的tricky, 在其他语言OOP也有相似的写法. 这种写法的好处是隔离内部与外部, 仅允许类提供的公共方法访问类内成员变量.

- **构造方法/构造函数:** 对类进行初始化的方法. 与类同名, 无返回值, 不需要void, 在new中调用.

    > **Tips:** 以上语法细节适用于C#, 非C#可能会有差别, 类中不显示写明构造函数时由编译器默认构造(更多语法细节和原理请移步至讨论C#的相关文献).

``` C#
class Cat {
    private string name;
    public Cat(string name){ //这是构造函数
        this.name = name;
    }
}
```

- **重载(overload):** 提供了创建多个同名方法(Function)的功能, 重载方法的参数类型不同. 重载可以在不改变原方法基础上添加新功能.

    > **Tips:** 这里**参数类型的不同**指的是参数个数不同或参数类型的不同(详见代码示例)

``` C#
class Example{
    //不仅构造函数, 普通函数也可以重载
    public function(){};
    public function(int arg_1){};
    public function(float arg_1){};
    public function(int arg_1, float arg_2){};
    public function(float arg_1, int arg_2){};//类型顺序不同也会被认为是重载
}
```

- **封装:** 每个对象包含该对象操作所需的所有信息, 不必依赖其他对象来完成自己的操作, 该特性称为封装.

    > **Addtional:** 良好的封装可以减少耦合, 类内部实现可以自由修改, 具有清晰的对外接口

- **继承:** 对象的继承代表了一种"**is-a**"关系, 若描述为"B是A", 则认为B可以继承A. 又可以理解为B是A的一种特殊化, B拥有A的特性之外, 还拥有自己独特的特性. 即继承代表了一种包含关系, A包含B.

    > **Addtional:**
    > - 继承的双方称为**子类/派生类&父类/基类**.
    > - 子类继承父类的成员有方法, 域, 属性, 事件, 索引指示器
    > - 构造方法**无法**继承, 只能调用, 可以使用**base**关键字(C#语法特性)

``` C#
class Animal { //父类
    protected string name = "";
    public Animal() { //构造函数
        this.name = "unamed";
    }
    public Animal(string name) {
        this.name = name;
    }
    protected int shoutNum = 3;
    public int ShoutNum { //属性
        get {
            return shoutNum;
        }
        set {
            shoutNum = value;
        }
    }
}

class Cat : Animal { //继承父类Animal的子类Cat
    public Cat() : base() {}
    public Cat(string name) : base(name) {}

    public string Shout() {
        string result = "";
        for(int i = 0; i < shoutNum; i++){
            result += "mew ";
        }
        return result;
    }
}

class Dog : Animal { //继承父类Animal的子类Dog
    public Dog() : base() {}
    public Dog(string name) : base(name) {}

    public string Shout() {
        string result = "";
        for(int i = 0; i < shoutNum; i++){
            result += "woof ";
        }
        return result;
    }
}
```

> **Tips:** 继承的**优点**是使子类公共部分放在了父类, 代码得到了共享, 减少了代码重复, 修改和扩展都变得相对容易. 但**缺点**也是显而易见的, 继承会破坏封装, 父类实现的细节暴露给子类, 父类和子类间是强耦合的.

- **多态:** 多态表示不同的对象可以执行相同的动作, 但通过自己的代码执行.

    > **Additional:**
    > - 子类以父类身份出现
    > - 子类工作时以自己的方式实现
    > - 子类以父类身份出现时, 无法使用子类特有的属性和方法
    >
    > **Tips:** 在父类中, 该动作需要声明为虚拟的, 用关键字**virtual**标识.

- **重写/覆写(override):** 子类使用关键字**override**将父类实现替换为自己的实现.

``` C#
class Animal{
    ......
    public virtual string Shout(){ //声明为虚方法
        return "";
    }
}
class Cat : Animal{
    ......
    public override string Shout(){ //覆写
        ....... //略, 代码见上文
    }
}
class Dog : Animal{
    ......
    public override string Shout(){ //覆写
        ....... //略, 代码见上文
    }
}

/*-----------------------------------------------------*/
/*执行环境*/

arrayAnimal = new Animal[5];
arrayAnimal[0] = new Cat();
arrayAnimal[1] = new Dog();
foreach(Animal item in arrayAnimal){
    MessageBox.Show(item.Shout()); //Cat为"mew", Dog为"woof".
}

```

> **Tips1:** C#的多态性分为静态多态性和动态多态性. 静态多态性即为前文提到的overload重载, 在编译时确定; 动态多态性为override覆写, 在运行时确定, 通过抽象类(见下文)和虚方法实现.
>
> **Tips2:** 笔者在翻阅相关资料时, 在C++语言中发现了更为复杂的机制, overwrite重写和override覆写存在区别, 详见[**博客园|C++中的Overload、Override和Overwrite**](https://www.cnblogs.com/kuliuheng/p/4107012.html)
>
> **Addtional:** 原书对上述实现Animal Shout的代码进行重构, 具体方法为将Shout()声明为父类公共方法(去掉virtual), 声明新的虚方法getSound(), 在Shout()中调用, 在子类中覆写(override), 从而避免了代码重复, 此处笔者不再浪费篇幅详细赘述.

- **抽象类&抽象方法:** C#允许将类和方法用关键字**abstract**声明, 即抽象类, 抽象方法.

    > **Addtional:**
    > - 抽象类不能被实例化
    > - 抽象方法必须被子类覆写(override)
    > - 含有抽象方法的类必须声明为抽象类, 不论是否具有一般方法
    > - 使用时考虑让抽象类拥有尽可能多的共同代码, 拥有尽可能少的数据
    >
    > **Tips:** 抽象类通常代表一种抽象概念, 提供了一个继承的出发点, 当设计一个新的抽象类时, 一定是用来继承的. 因此在继承结构中, 叶节点应当是具体类, 非叶节点应当是抽象类.

- **接口(Interface):** 接口是把隐式公共方法和属性组合起来, 以封装特定功能的一个集合. 类实现了接口就可以支持接口所指定的所有属性和成员. 接口不允许提供任何成员的执行方法(因此接口不能实例化, 没有构造方法, 字段和修饰符, 不能声明静态或虚拟等).

    > **Addtionnal:**
    > - 实现接口的类必须实现接口中所有方法和属性.
    > - 一个类可以支持多个接口, 不同类也可以支持相同接口.
    >
    > **Tips:** [菜鸟教程|C# Interface](https://www.runoob.com/csharp/csharp-interface.html)将接口表述为:
    >
    >接口定义了所有类继承接口时应遵循的语法合同. 接口定义了语法合同"是什么"部分, 派生类定义了语法合同"怎么做"部分. 接口定义了属性, 方法和事件, 这些都是接口的成员. 接口只包含了成员的声明. 成员的定义是派生类的责任. 接口提供了派生类应遵循的标准结构.
    >
    > **书写规范:** 接口的命名需要在前面加一个大写"I".

``` C#
// 笔者在此化简了书目中提供的例子, 能理解即可.
// 叮当猫继承自上文出现的Cat类, 内部需要实现变东西的接口

interface IChange {
    string ChangeThing(string thing);
}

class MachineCat : Cat, IChange {
    public MachineCat() : base(){}
    public MachineCat() : base(name){}

    public string ChangeThing(string thing){ //实现接口, 不需要使用override修饰
        return base.Shout() + "我有万能口袋, 可以变出: " + thing;
    }
}
```

> **Additional:**
> 笔者在此补充一点C#的语法特性, 接口也可以继承接口, 假设IB继承IA, 在IB中不需要声明IA中的声明, 但实现IB的类需要实现IA和IB中的所有声明.
>
> **Compare: Class v.s. Interface**
>
> - **语法上:** 抽象类可以给出一些成员的实现, 接口不能包含成员的实现, 抽象类的抽象成员可被子类部分实现, 但接口的成员需要类全部实现, 一个类只能继承**一个**抽象类, 但可以实现**多个**接口.
> - **含义上:** 类是对象的抽象, 抽象类是对类的抽象, 接口是对**行为**的抽象.
> - **使用上:** 如果行为跨越不同类的对象, 可使用接口; 对于一些相似的类对象, 用继承抽象类. 需要注意的是, 实现接口和继承抽象类并不冲突.
> - **设计角度上:** 抽象类是从子类中发现了公共的东西, 泛化出父类, 然后子类继承父类, 而接口根本不知道子类的存在, 方法如何实现不明确, 预先定义.

- **泛型(Generic):** 泛型是具有占位符(类型参数)的类, 结构, 接口和方法, 这些占位符是类, 结构, 接口和方法所储存域或使用的一个或多个类型的占位符. 泛型集合类可以将类型参数用作它所存储的对象的类型的占位符: 类型参数作为其字段的类型和其方法的参数类型出现.

    > **Additional:** 通常情况下, 都建议使用泛型集合, 因为这样可以获得类型安全的直接优点而不需要从基集合类型派生并实现类型特定成员. 此外, 如果集合元素为值类型, 泛型集合类型的性能通常优于对应的非泛型集合类型, 因为使用泛型时不必对元素进行装箱.
    >
    > **Tips:** [菜鸟教程|C# Generic](https://www.runoob.com/csharp/csharp-generic.html)将泛型表述为:
    >
    > 泛型(Generic)允许您延迟编写类或方法中的编程元素的数据类型的规范, 直到实际在程序中使用它的时候. 换句话说, 泛型允许您编写一个可以与任何数据类型一起工作的类或方法.
    >
    > 泛型的定义较为晦涩, 建议结合代码理解. 笔者在此强烈建议阅读更多的资料来学习泛型.

``` C#
using System.Collections.Generic; //增加泛型集合命名空间

public partial class Forml : Form{
    IList<Animal> arrayAnimal; // 声明泛型集合变量, 表示只接受Animal类型
    //List<Animal> arrayAnimal; 两种写法是等价的

    private Event(){
        arrayAnimal = new List<Animal>();

        arrayAnimal.Add(new Cat());
        arrayAnimal.Add(new Dog());
        arrayAnimal.Add(123); // Error! Invalid Type 
    }
}
```

- **委托:** 委托是对函数的封装, 可以当作给方法的特征指定一个名称. 委托对象用关键字**delegate**声明.

- **事件:** 事件时委托的一种特殊形式, 当发生有意义的事情时, 事件对象处理通知过程. 事件对象用关键字**event**声明.

> **Additional:** 委托是一种引用方法的类型, 一旦为委托分配了方法, 委托将与该方法具有完全相同的行为. 事件则是在发生其他类或对象关注的事情时, 类或对象可通过事件通知它们.

``` C#
//情境: 猫Tom叫的时候两只老鼠Jerry和Jack要跑.

class Cat{
    private string name;
    public Cat(string name){
        this.name = name;
    }

    public delegate void CatShoutEventHandler(); // 声明委托
    public event CatShoutEventHandler CatShout; //声明事件

    public void Shout(){
        Console.WriteLine("喵, 我是{0}.", name);
        if (CatShout != null){ // 如果声明了事件CatShout
            CatShout();
        }
    }
}

class Mouse{
    private string name;
    public Mouse(string name){
        this.name = name;
    }

    public void Run(){
        Console.WriteLine("老猫来了, {0}快跑", name);
    }
}

static void Main(string[] args){
    Cat cat = new Cat("Tom");
    Mouse mouse1 = new Mouse("Jerry");
    Mouse mouse2 = new Mouse("Jack");

    cat.CatShout += new Cat.CatShoutEventHandler(mouse1.Run);
    cat.CatShout += new Cat.CatShoutEventHandler(mouse2.Run); 
    // "+=" 表示 "add_CatShout" 的意思; 与之相反 "-=" 表示 "remove_CatShout()"

    cat.Shout();
    Console.Read();
}
```

运行结果:

``` Shell
喵, 我是Tom.
老猫来了, Jerry快跑!
老猫来了, Jack快跑!
```

- **EventArgs:** EventArgs是包含事件数据的类的基类.

``` C#
public class CatShoutEventArgs : EventArgs{
    private string name;
    public string Name{
        get {return name; }
        set {name = value; }
    }
}

class Cat{
    private string name;
    public Cat(string name){
        this.name = name;
    }

    public delegate void CatShoutEventHandler(object sender, CatShoutEventArgs args);
    public event CatShoutEventHandler CatShout;

    public void Shout(){
        Console.WriteLine("喵, 我是{0}.", name);
        if(CatShout != null){
            CatShoutEventArgs e = new CatShoutEventArgs();
            e.Name = this.name;
            CatShout(this, e);
        }
    }
}

class Mouse{
    private string name;
    public Mouse(string name){
        this.name = name;
    }

    public void Run(object sender, CatShoutEventArgs args){
        Console.WriteLine("老猫{0}来了, {1}快跑!", args.Name, name);
    }
}
```

Main执行结果:

``` Shell
喵, 我是Tom.
老猫Tom来了, Jerry快跑!
老猫Tom来了, Jack快跑!
```
