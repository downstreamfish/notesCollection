---
style: candy
---
Java核心技术
===

## 面向对象
	面向对象设计是一种程序设计技术。它将重点放在数据(即对象)和对象的接口上。

## 数组拷贝
	在Java中，允许将一个数组变量拷贝给另一个数组变量，这时，两个变量将引用同一个数组：
```Java
	int[] luckyNumber = smallPrimes;
	luckyNumber[5] = 12;  //now smallPrimes[5] is also 12
```

如果希望将一个数组的所有值拷贝到一个新的数组中去，就要使用Arrays类的copyOf方法：


```java
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
```

## 注释
  + 方法注释：
  	@param variable description
	@return descreiption
	@throws class description
  + 通用注释
	@author name
	@version text
	@since text
	@deprecated text
	@see reference <a href="..."></a>  {@link package.class#feature label}
* overloading
	返回值不同的函数不能构成重载。如一个类可以有多个构造方法，而构造方法没有返回值。
* 反射(reflection)
	反射是指在程序运行期间发现更多的类及其属性的能力。
	一个对象可以引用多种实际类型的现象被称为多态(polymorphism).在运行时能够自动地选择调用哪个方法的现象称为动态绑定(dynamic binding)。

## JVM
  * JVM内存组成：新域(Young Generation)、旧域(Tenured Generation)和永久域(Perm Generation)，新域由Eden   和两个救助空间Survivor组成。永久域(Perm Generation)保存那些在虚拟机的整个生存期都生存的对象，因此，该域不需要被垃圾收集程序清空。
  * Java虚拟机配置选项有`-X`选项和`-XX`选项，可设置3种类型的值：Boolean、Numeric、String.
  * 垃圾收集器的7种类型：`标记-清除收集器、标记-压缩收集器、复制收集器、增量收集器、分代收集器、并发收集器、并行收集器`。
  * 设置JVM内存域的方法：
	+ `-Xms`：设置堆初始大小
	+ `-Xmx`: 设置堆最大大小
	+ `-Xmn`：设置新域大小
	+ `-XX:NewSize`：设置新域的初始值
	+ `-XX:MaxNewsize`: 设置新域的最大值
	+ `-XX:NewRatio`：设置新域与旧域比例
	+ `-XX:MaxPerSize`：设置永久域最大大小
	+ `-XX:PerSize`：设置永久域初始值
	+ `-XX:SurvivorRation`：设置救助域与Eden空间的比值

##  完美的equals方法的建议：
  1. 显式参数命名为otherObject， 稍后需要将它转换成另一个叫做other的变量。
  2. 检测this与otherObject是否引用同一个对象。

    if(this == otherObject) return true;
    
  这条语句只是一个优化，实际上，这是一种经常采用的形式。因为计算这个等式要比一个一个地比较类中的域所付出的代价小得多。
  3. 检测otherObject是否为null，如果为null，返回false。这项检测是很必要的。

    if(otherObject == null) return false;
  4. 比较this与otherObject是否属于同一个类。如果equals的语义在每个类中有所改变，就使用getClass()检测：

    if(getClass() != otherObject.getClass()) return false;
  如果所有的子类都拥有统一的语义，就使用instanceof检测：

    if(!(otherObject instanceof ClassName)) return true;
  5. 将otherObject转换为相应的类类型变量：

    ClassName other = (ClassName) otherObject;
  6. 现在开始对所有需要比较的域进行比较了。使用==比较基本类型域，使用equals比较对象域。如果所有的域都匹配，就返回true，否则返回false。

    return field1 == other.field1 && field2 == other.field2 && ...;
##  HashCode方法
  * 散列码(hash code) 是由对象导出的一个整型值。散列码是没有规律的。如果x和y是两个不同的对象，`x.hashCode()`与`y.hashCode()`基本不会相同。

  * 由于hashCode方法定义在Object类中，因此每个对象都有一个默认的散列码，其值为对象的存储地址。

  * 如果重新定义equals方法，就必须重新定义hashCode方法，以便用户可以将对象插入到散列表中。
  * HashCode方法应该返回一个整型数值(也可以是负数)，并合理第组合实例域的散列码，以便能够让各个不同的对象产生的散列码更加均匀。
  * Equals与hashCode的定义必须一致，如果`x.equals(y)` 返回true，那么`x.hashCode()`就必须与`y.hashCode（）` 具有相同的值。

##  ToString方法
  * toString()方法用于返回表示对象值的字符串。
  * toString()方法遵循这样的格式：类的名字，随后是一对方括号括起来的域值。
  * 只要对象与一个字符串通过操作符“+”连接起来，Java编译就会自动地调用toSting()方法。
  * 数组继承了object类的toSting方法，数组类型将按照旧的格式打印。即是会显示数组的类型名和内存地址。如果要打印数组内容，方式是调用静态方法`Arrays.toString(arrayName);`。如果是多维数组，需要调用`Arrays.deepToString(arrayName);`方法。
  * toString方法是一种非常有用的调试工具。强烈建议为自定义的每个类增加toSting方法。

##  反射(reflective)
  * 功能：

    * 在运行中分析类的能力
    * 在运行中查看对象。
    * 实现数组的操作代码。
    * 利用Method对象，这个对象很像C++中的函数指针
  * Class类
	+ 在程序运行期间，Java运行时系统始终为所有的对象维护一个被称为运行时的类型标识。这个信息保存着每个对象所属的类足迹。虚拟机利用运行时信息选择相应的方法执行。
  * 检查类的结构

## 继承设计的技巧
  * 将公共操作和域放在超类
  * 不要使用受保护(protected)的域
	1. 子类集合是无限制的，任何一个人都能够由某个类派生一个子类，并编写代码以直接访问protected的实例域，从而破坏了封装性。
	2. 在Java程序设计语言中，在同一个包中的所有类都可以访问protected域，而不管它是否为这个类的子类。
  
  * 使用继承实现"is-a"关系
  * 除非所有继承的方法都有意义，否则不要使用继承。
  * 在覆盖方法时，不要改变预期的行为。
  * 使用多态，而非类型信息。
  * 不要过多地使用反射。
  反射机制使得人们可以通过在运行时查看域和方法，让人们编写出更具有通用性的程序。这种功能对于编写系统程序来说极其实用，但是通常不适于编写应用程序。反射是很脆弱的，即编译器很难帮助人们发现程序中的错误。任何错误只能在运行时才被发现，并导致异常。

	


