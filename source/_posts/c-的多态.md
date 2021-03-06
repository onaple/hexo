---
title: c++ 多态
comments: true
tags:
  - 多态
  - C++
  - 面向对象
categories:
  - C++
date: 2017-03-05 16:34:59
update: 2017-03-05 16:34:59
---
## C和C++的区别：1. C是一个结构化语言，它的重点在于算法和数据结构。C程序的设计首要考虑的是如何通过一个过程，对输入（或环境条件）进行运算处理得到输出（或实现过程（事务）控制）。C的优势在于编写的程序更接近于硬件，仅次于汇编语言，所以他相对其他编程语言高效的多，但同时程序员负责一切不安全，如内存泄露等。但正是由于这样的风险的存在，对程序员的紧密思维要求更高。2. C++是有C，面向对象，泛型编程，stl组成。用面向对象来编程首要考虑的是如何构造一个对象模型，让这个模型能够契合与之对应的问题域，这样就可以通过获取对象的状态信息得到输出或实现过程（事务）控制。 所以C与C++的最大区别在于它们的用于解决问题的思想方法不一样。之所以说C++比C更先进，是因为“ 设计这个概念已经被融入到C++之中 ”。

	## 面向对象的三大特性：
封装，继承，多态
1. 	封装：将对象的属性和方法封装在对象内部，形成一个个独立的单元模块，对外通访问权限控制管理对象数据的交互。(访问权限：（private，protected,public) 保证封装性的关键)目的：增强代码的安全性和简化编程，让使用者不必了解类具体的实现细节，只要通过外部接口，以特定的权限来使用类的方法即可。2.	继承：一个对象获得另一对象的特性的过程。是将一群类组织起来，定义了父子关系，实现了代码的重用，父类定义了所有子类的的共有借口和私有实现，同时子类都可以增加或覆盖继承来的东西，以实现独有的行为。3. 	多态：它是建立在了继承的基础上；简单来说，就是一个接口，多个方法.具体来说：它是指不同子类在继承父类后分别覆盖了父类的方法多态性使得同一属性或者行为在基类及其子类间有不同的语义；多态性丰富了对象的内容，增强了软件的灵活性和可重用性；C++的多态性有两种：编译时的多态（函数重载），运行时多态（虚函数）（联编（binding)或称为绑定:是指计算机程序自身彼此关联的过程联编工作在编译连接阶段完成的情况称为：静态联编联编在程序运行阶段完成的情况称为：动态联编。）
##	c++ 重载 覆盖 隐藏的区别和执行方式 :
1. 成员函数被重载的特征:相同的范围（在同一个类中）；函数名字相同；参数不同； virtual 关键字可有可无。2. 覆盖是指派生类函数覆盖基类函数，特征是:不同的范围（分别位于派生类与基类）； 函数名字相同； 参数相同； 基类函数必须有virtual 关键字。 3. “隐藏”是指派生类的函数屏蔽了与其同名的基类函数，规则如下:如果派生类的函数与基类的函数同名，但是参数不同。此时，不论有无virtual关键字，基类的函数将被隐藏（注意别与重载混淆）。 （2）如果派生类的函数与基类的函数同名，并且参数也相同，但是基类函数没有virtual 关键字。此时，基类的函数被隐藏（注意别与覆盖混淆）4. 3种情况怎么执行：
重载：看参数;隐藏：用什么就调用什么;覆盖：调用派生类;
## 虚函数的工作原理：
编译器处理虚函数的方法是.给每个对象添加一个隐藏成员。隐藏成员中保存了一个指向函数地址数组的指针。而这个数组称为虚函数表，虚函数表中存储了为类对象进行声明的虚函数的地址。
1. 单继承时	-	虚函数指针在对象的最前面的位置；	-	虚函数地址按照声明的顺序存放于虚表中；	-	父类虚函数地址在子类虚函数地址的前面；	-	子类如果覆盖父类的虚函数，则被放到虚表中原父类虚函数的位置	-	没有被覆盖的函数依旧在原位。2. 	多重继承的特殊地方：	-	每个父类都有自己的虚表时，子类的虚函数成员只被放到第一个父类中。	-	子类有多个虚表指针，位于类的最前面，分别指向不同的父类的虚表，（按继承的顺序）。	-	如果有覆盖情况，则替换所有被覆盖的父类虚函数地址。3. 父类访问子类中成员函数只能通过虚函数，覆盖的方法。否则无法访问。但我们可以通过函数指针强行访问虚表里的函数。本人就是通过此方法的出的以上结论。4. 虚函数特性：	- 虚函数是动态联编的基础。	- 是非静态的成员函数。	-	在类的声明中，在函数原型之前写virtual。	-	virtual 只用来说明类声明中的原型，不能用在函数实现时。	-	具有继承性，基类中声明了虚函数，派生类中无论是否说明，同原型函数都自动为虚函数。	-	本质：不是重载声明而是覆盖。	-	调用方式：通过基类指针或引用，执行时会根据指针指向的对象的类，决定调用哪个函数。5.	虚函数的限制	- 只有类的成员函数才能说明为虚函数，因为虚函数仅适用于继承关系的 类对象，所以普通函数不能说明为虚函数。	- 内联函数不能是虚函数，因为内联函数是在编译时决	定其位置。	- 构造函数不能是虚函数，因为构造时对象还是一片未	定型的空间，就没有虚指针，虚表。。	- 	析构函数可以是虚函数，而且通常声明为虚函数。##	纯虚函数与抽象类1.	带有纯虚函数的类称为抽象类:

```
class  类名 {     virtual 类型 函数名(参数表)=0;  //纯虚函 	 ...};
```
2.	作用：	- 抽象类为抽象和设计的目的而建立，将有关的数据和行为组织在一个继承层次结构中，保证派生类具有要求的行为。	- 对于暂时无法实现的函数，可以声明为纯虚函数，留给派生类去实现。主要作用是通过它为一个类族建立一个公共的接口，使它们能够更有效地发挥多态特性。3. 	注意：抽象类只能作为基类来使用;不能声明抽象类的对象;但可以声明一个指针