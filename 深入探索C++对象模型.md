# 深入探索C++对象模型
-------------------
# 第0章 导读
## C++编译器作者的话
当初在设计C++编译器时，设计了一个名为Simpler的组件来转换内部的程序的表现。其中有三种转换时任何对象模型都需要的：

> * 1.与编译器相关的转换（Implementation-dependent transformations）

> 例如，当parser看到这个表达式：
> > fct()
> 它并不知道这是一个
> > * (a)这是一个函数调用。
> > * (b)这是overloaded call operator在class object fct上的一种应用。
> 默认情况下，这是一个函数调用，但是当(b)的情况出现时，Simplifer就要重写并调换call subtree。
>
> * 2.语言语境转换(Language sematics transformations)

> 这包括constructor/destructor的合成和扩展、memberwise初始化、对与memberwise copy的支持、在代码中安插conversion operators、临时性对象以及对constructor/destructor的调用
> * 3.程序代码和对象模型的转换(Code and object model transformations)

> 这包括对virtual functions、virtual base class和inheritance和一般支持、new和delete运算操作符、class objects所组成的数组、local static class instances、带有非常量表达式(nonconstant expression)之global object的静态初始化操作。


## 译者的话
### 什么是C++模型
p9.
### 本书组织
p13.
**建议先阅读第1,3,4章。**

### 名词对照
p20.

|英文名词|中文名词及其意义|
|-|-|
|access level|访问级别：public、private、protected|
|access section|访问区段：public、private、protected三种段落|
|alignment|边界调整：调整至默写bytes的倍数。其结果视不同的机器而定。例如32位机器通常调整至4的倍数|
|bind|绑定：将程序中的某个符号真正附着(决议)至一块实体上|
|class|类|
|class hierarchy|class体系，class 层次结构|
|composition|组合：通常与继承(inheritance)一同讨论|
|concrete inheritance|具体继承(相对于抽象继承)|
|constructor|构造函数|
|data member|数据成员(亦或被称为member variable)|
|declaration,delcare|声明|
|definition, define|定义(通常附带“在一块内存中挖一块空间”的行为)|
|derived|派生|
|destructor|解构造函数|
|encapsulation|封装|
|explicit|明确的(通常指C++代码中明确出现的)|
|hierarchy|体系、层次结构|
|implement|实现(动词)|
|implementation|实现品、实现物：本书有时指C++编译器。大部分时候指class member function的内容|
|implicit|隐含的、暗喻的(通常指未出现在C++代码中的)|
|inheritance|继承|
|inline|内联(C++关键词)|
|instance|实体|
|layout|布局：指object在内存中的数据分布情况|
|mangle|名称切割重组(C++对于函数名称的一种处理方式)|
|member function|成员函数。亦或被称为function member|
|members|成员，泛指data members和function members|
|object|对象：根据class的声明而完成的一份占有内存的实体|
|offset|偏移位置|
|operand|操作数|
|operator|运算符|
|overhead|额外负担(因为某种设计而导致的额外成本)|
|overload|重载|
|overloaded fuction|重载函数|
|override|改写(对virtual function的重新设计)|
|paradigm|典范(*参考#22页*)|
|pointer|指针|
|polymorphism|多态|
|programming|程序设计、程序化|
|reference|参考(动词)|
|reference|引用：C++的&运算符|
|resolve|决议：函数调用时链接器所进行的一种操作，将符号与函数实体产生关联。如果你调用func()而链接时找不到func()实体，就会出现"unresolved exterals"链接错误|
|slot|表格中的一格(一个元素)；条孔；条目；条格|
|subtype|子类型|
|type|类型，类别：指的是int、float等内建类型，或C++ classes等自定类型|
|virtual|虚拟|
|virtual function|虚拟函数|
|virtual inheritance|虚拟继承|
|virtual table|虚拟表格：为实现虚拟机制而设计的一种表格，内放virtual functions的地址|

### 其他重要名词
|名词|解释|其他|
|-|-|-|
|COM|Component Object Module|《Essential COM》《COM本质论》|
|CORBA|Common Object Request Broker Architecture|一种标准的面向对象应用程序体系规范|
|SOM|-|-|

## 目录
> 本立道生 001

> 目录 005

> 前言 013

> 第0章 导读（译者的话） 025

> 第1章 关于对象(Object Lessons) 001
> > 加上封装后的布局成本(Layout Costs for Adding encapsulation) 005
>
> > 1.1 C++对象模式(The C++ Object Model) 006
> > > * 简单对象模型(A Simple Object Model) 007
> > > * 表格驱动对象模型(A Table-driven Object Model) 008
> > > * C++对象模型(The C++ Object Model) 009
> > > * 对象模型如何影响程序(How the Object Model Effects Programs) 013

> > 1.2 关键词带来的差异(A Keyword Distinciton) 015
> > > * 关键词的困扰 016
> > > * 策略性正确的struct(The politically correct  struct) 019
> > 1.3 对象的差异(An Object Distinction) 022
> > > * 指针的类型(The Type of a Pointer) 028
> > > * 加上多态之后(Adding polymorphism) 0029

> 第2章 构造函数语意学(The Semantics of Constructors) 037
> > 2.1 Default Constructor的构建操作
> > > * "带有Default Constructors"的Members Class Object 041
