---
style: candy
---
## Java

#### Java运行环境(JRE)
  * JRE = JVM + API(Lib)
  * JRE运行程序时的三项主要功能
    1. 加载代码：由class loader完成。
    2. 校验代码：由bytecode verifier完成。
    3. 执行代码：由runtime interpreter完成。
#### JDK提供的工具
  * Java编译器：javac.exe
  * Java执行器：java.exe
  * 文档生成器：javadoc.exe
  * Java打包器：jar.exe
  * Java调试器：jdb.exe
  * 运行图形界面程序：javaw
  * 查看类信息及反汇编：javap
#### 面向对象设计思想的要点：认为客观世界由各种对象组成
  * 程序的分析和设计都围绕着：
    + 有哪些对象类
    + 每个类有哪些属性，哪些方法
    + 类之间的关系(继承、关联等)
    + 对象之间发送消息(调用方法)
#### Java程序的基本构成：
  * package语句

  * import语句

  * 类定义--class：一个文件只能有一个public类（且与文件同名）

  * 类 = 类头 + 类体

  * 类成员 = 字段(field) + 方法(method)
    + 字段（field，属性、变量)
    + 方法（method， 函数）

  * 方法 = 方法头 + 方法体

#### 使用jar打包
  1. 编译：`javac A.java`
  2. 打包：`jar cvfm A.jar A.man A.class`

   + `c`表示创建(create)
   + `v`表示显示详情(verbose)
   + `f`表示指定文件名
   + `m`表示清单文件
  3. 运行：`java -jar A.jar`
   + A.man是清单文件(manifest)，内容如：
```
   Manifest-Version:1.0
   Class-Path:
   Main-class:A
```

+ 清单文件文件可以任意命名，常见的是MINIFEST.MF
+ 使用javap查看类的信息: `javap classname`
+ 使用javap反汇编：`javap -c classname`

#### 使用JavaDoc生成文档
  * `javadoc -d 目录名 xxx.java`
  * /**  */这其中可以使用以下标记
	+ `@author`对类的说明--标明开发该类模块的作者
	+ `@version`对雷达说明--标明该类模块的版本
	+ `@see`对类、属性、方法的说明，参考转向，就是相关主题
	+ `@param` 对方法的说明--对方法中某参数的说明
	+ `@return`对方法的说明--对方法返回值的说明
	+ `@exception`对方法的说明--对方法可能抛出的异常进行说明

#### 基本类型与引用类型：
  * 基本类型：变量在栈中，在“这里”
  * 引用类型：变量引用到堆， 在“那里”
  * 赋值时：基本类型复制的是值，引用类型复制的是引用。

#### Java数据类型划分

* 数据类型决定数据的存储方式和运算方式
* Java中的数据类型分为两大类
  + 基本数据类型(primitive types)
	- 数值型
	  * 整数类型(byte, short, int, long)
	  * 浮点类型(float, double)
	- 字符型(char)
	  * 字符常量是用单引号括起来的单个字符
	  * Java字符采用Unicode编码，每个字符占两个字节。
	  * Java语言还允许使用转义字符`\`来将其后的字符转变为其它的含义。
	- 布尔型(boolean)--逻辑型
	  * boolean类型适于逻辑运算，一般用于流程控制
	  * boolean类型数据只允许取值`true`或`false`，不可以用`0`或`非0`的整数替代`true`和`false`。
>  Java各整数类型有固定的表数范围和字段长度，而不受具体操作系统的影响，以保证Java程序的可一致性

| 类 型 | 占用存储空间 | 表数范围 |
|---|---|---|
| byte | 1字节 | -128~127 |
| short | 2字节 | -2^15~2^15-1 |
| int | 4字节 | -2^31~2^31-1 |
| long | 8字节 | -2^63~2^63-1 |
| float| 4字节 | -3.403E38~3.403E38|
| double | 8字节 | -1.798E308~1.798E308|

> 注意：Java中没有“无符号数”，可以用long来处理无符号整数(`uint`)

  + 引用类型(reference types)
	- 类(class)
	- 接口(interface)
	- 数组

#### 标识符(Identifier)
  * 名字就是标识符：任何一个变量、常量、方法、对象和类都需要有名字。
  * 标识符要满足如下的规定：
	1. 标识符可以由字母、数字和下划线(`_`)、美元符号(`$`)组合而成。
	2. 标识符必须以字母、下划线或美元符号开头，不能以数字开头。
  * 标识符最好与其意义相符，以增加程序的可读性
  * Java是大小写敏感的语言
	+ 按Java惯例，类名首字母用大写
	+ 其余(包名、方法名、变量名)首字母都小写
	+ 少用下划线
	+ 常量随使用随定义

#### 表达式
  * 表达式是符合一定语法规则的运算符和操作数的序列
  * 表达式的类型和值
	+ 对表达式中操作数进行运算得到的结果称为表达式的值
	+ 表达式的值的数据类型即为表达式的类型
  * 表达式的运算顺序
	+ 首先应按照运算符的优先级从高到低的顺序进行
	+ 优先级相同的运算符按照事先约定的结合方向进行
	+ 对于运算符的优先级和结合性，适当使用括号`()`
  * 表达式中的类型转换
	+ int->long->float->double
	+ **整型提升**，所有的byte, short, char参与算术运算都转为int

#### Java程序的注释
  * `//`用于单行注释。注释从`//`开始，终止于行尾
  * `/*...*/`用于多行注释。注释从`/*`开始，到`*/`结束，且这种注释不能互相嵌套。
  * `/**...*/`是Java所特有的doc注释，它以`/**`, 到`*/`结束
#### 数组
  * Java语言中声明数组时不能指定其长度(数组中元素的个数)，数组是引用类型，数组名只是一个引用。
  * 数组复制
	1. for循环，效率最低
	2. System.arraycopy()效率最高
	3. Arrays.copyOf()效率低于第2个
	4. Object.clone()效率低于第2和3种
  * 数组一经分配空间，其中的每个元素也被按照成员变量的类型被隐式初始化。
  * 数组元素的引用方式，
	+ index为数组元素下标，可以是整型常量或整型表达式
	+ 数组元素下标从0开始，长度为n的数组合法下标取值范围：`0 ~ n-1`
  * 每个数组都有一个属性length指明它的长度。

#### 类
  * 类是组成Java程序的基本要素
  * 是一类对象的原型
  * 它封装了一类对象的状态和方法
	+ 它将变量与函数封装到一个类中
  * 构造方法
	+ 构造方法(constructor)是一种特殊的方法
	+ 用来初始化(new)该类的一个新的对象
	+ 构造方法和类名同名，而且不写返回数据类型。
	+ 一般情况，类都有一个至多个构造方法
	+ 如果没有定义任何构造方法，系统会自动产生一个构造方法，称为默认构造方法(default constructor)
	+ 默认构造方法不带参数，并且方法体为空。

#### 方法重载(overload)
  * 方法重载(overloading): 多个方法有相同的名字，编译时能识别出来。
  * 这些方法的**签名**(signature)不同，或者是参数个数不同，或者是参数类型不同。
  * 通过方法重载可以实现多态(polymorphism)
#### this的使用
  1. 在方法及构造方法中，使用this来访问字段及方法
  2. 使用this解决局部变量(方法中的变量)或参数变量与域变量同名的问题。
  3. 构造方法中，用this调用另一构造方法，在构造方法中调用另一个构造方法，则这条调用语句必须放在第一句。
#### 继承
  * 继承(inheritance)是面向对象的程序设计中最为重要的特征之一
  * 子类(subclass), 父类或超类(superclass)
 	+ 父类包括所有直接或间接被继承的类。
  * Java支持单继承：**一个类只能有一个直接父类**
  * 继承的优点：
	+ 子类可以继承父类的状态和行为
	  - 可以修改父类的状态或重载父类的行为
	  - 可以添加型的状态和行为
	+ 可以提高程序的抽象程度
	+ 实现代码重用，提高开发效率和可维护性
  * Java中的继承是通过`extends`关键字来实现的，如果没有`extends`，则该类默认为`java.lang.Object`的子类
> 所有的类都是通过直接或间接地继承`java.lang.Object`得到的。
  * 字段
	1.字段的继承
	  + 子类可以继承父类的所有字段
	2. 字段的隐藏
	  + 子类重新定义一个与父类那里继承来的域变量完全相同的变量，称为域的隐藏。
	3. 字段的添加
	  + 在定义子类时，加上新的域变量，就可以使子类比父类多一些属性。
  * 方法
	1. 方法的继承
	  + 父类的非私有方法也可以被子类字段继承
	2. 方法的覆盖(Override)（修改）
	  + 子类也可以重新定义与父类同名的方法， 实现对父类方法的覆盖(Override)
  	  + `@Override` JDK1.5以后可以使用这个注记来表示(不用也是可以的)
	  + 通过方法的覆盖，能够修改对象的同名方法的具体实现方法。
	3. 方法的重载
	  + 一个类中可以有几个同名的方法，这称为方法的重载(Overload)。同时，还可以重载父类中的同名方法。与方法覆盖不同的是，重载不要求参数类型列表相同。**重载的方法实际是新添加的方法。**
  * 使用super访问父类的域和方法
	+ 由于继承，使用this可以访问父类的域和方法，但有时为了明确地指明父类的域和方法，就要使用关键字`super`
	+ 使用super不能访问在子类中添加的域和方法。
	+ 使用super可以访问被子类所隐藏了的同名变量。
	+ 当覆盖父类的同名方法的同时，又要调用父类的方法，就必须使用super。
  * 使用父类的构造方法
	+ 构造方法是不能继承的，在子类构造方法中，可以使用`super`来调用父类的构造方法，**super()必须放在第一句**
  * 父类对象与子类对象的转换
	1. 子类对象可以被视为其父类的一个对象
	2. 父类对象不能被当做其某一个子类的对象
	3. 如果一个方法的形式参数定义的是父类对象，那么调用这个方法时，可以使用子类对象作为实际参数。
	4. 如果父类对象引用指向的实际是一个子类对象，那么这个父类对象的引用可以用强制类型转换成子类对象的引用

#### package
  * 用法：`package pkg1[.pkg2[.pkg3]...];`
  * 包及子包的定义，实际上是为了解决名字空间、名字冲突
	+ 它与类的继承没有关系。事实上，一个子类与其父类可以位于不同的包中。
  * 包有两方面的含义
	+ 一是名字空间、存储路径(文件夹)
	+ 一是可访问性(同一包中的各个类，默认情况下可以互相访问)
#### import
  * 用法：`import package1[.pkg2...].(classname | *)`
  * Java编译器自动导入包`java.lang.*`;