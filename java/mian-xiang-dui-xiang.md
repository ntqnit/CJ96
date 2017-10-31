# 面向对象编程

## 面向过程和面向对象编程

例如 C 语言、VB 语言都是面向过程的编程语言。通过一个函数（方法）解决一件事情，「就事论事」。事情处理完成后，是不会留下任何的「遗产」的。

一件事情：

例如 「南通青鸟 IT 教育 96 班同学在 3 教室上陆老师的 Java 课」。

用面向对象的思维逻辑去分析，抽象实体：

* 班级
* 学生
* 教室
* 老师
* 课程
* 学校

## 类和对象

**类：** 是一种自定义的数据类型。有时把这种数据类型也叫做「类类型」或者「引用数据类型」。「引用」就是内存地址的意思。

**对象：**通过类创建的变量。

> 类是一群对象的特征母版，对象是类的具体实例。
>
> 类是一群对象的抽象。

### 类的定义

> 类所具备的最基本要素：（静态）属性、（动态）方法。

语法：

```java
[修饰符] class 类名 {
    // 成员变量
    [修饰符] 数据类型 成员变量1;
    [修饰符] 数据类型 成员变量2;
    ...

    // 方法
    [修饰符] 返回值 方法名1([参数列表]) {
        方法体语句;
    }
    [修饰符] 返回值 方法名2([参数列表]) {
        方法体语句;
    }
    ...

    // 构造器：创建对象用的方法
    [修饰符] 类名([参数列表1]) {
        方法语句;
    }
    [修饰符] 类名([参数列表2]) {
        方法语句;
    }

}
```

类的三大部件：成员变量、方法、构造器。

实例：

```java
public class Student1 {
    // 构造器
    Student1(String name, int age, String code) {
        this.name = name;
        this.age = age;
        this.code = code;
    }

    // 成员变量
    String name;
    int age;
    String code;

    // 方法
    String intro() {
        return "我叫"+this.name+"，我的学号是"+this.code+"，我今年"+this.age+"岁了。";
    }

    void listen() {
        System.out.println(this.name + "在上课。");
    }

}
```

使用类构建对象

```java
public static void main(String[] args) {
    // 构建一个对象：调用类的构造器
    Student1 hehao = new Student1("何浩", 20, "C25");

    // 用对象：给属性赋值
    hehao.birthday = new Date(); // 赋值
    System.out.println(hehao.code); // 获取属性值

    // 用对象：调用对象的方法
    System.out.println(hehao.intro());
    hehao.listen();

}
```

> 类名的定义要符合 Java 的标识符命名规范，类名首字母大写，如果多个单词，使用驼峰命名法则（每个独立单词首字母大写），**在 Java 中，只要看到首字母大写，你就是一个类。**
>
> 类中三大部件的定义是没有严格的顺序的，但是，我们一般遵循，构造器、成员编程、方法这样的定义顺序。

**构造器**

语法：

```
[修饰符] 类名([参数列表]) {}
```

* 构造器是一个特殊的方法，方法名就是类名，没有返回值（和 void 是有区别的），构造器是类创建对象的唯一途径。如果一个类没有显式的定义一个构造器，那么**编译器会给这个类默认的定义一个没有参数的构造器**。
* 如果显式的定义了一个构造器，那么编译器就不会给类定义默认的空参数构造器。

**成员变量**

语法：

```
[修饰符] 数据类型 成员变量名 [= 默认值];
```

* 修饰符：可以省略，也可以是 public protected private static final，其中 public protected private 只允许出现。
* 数据类型：可以是任意的数据类型（包含基本数据类型、类类型、数组类型）
* 默认值：如果是类类型的，没有定义默认值，那么成员变量的值为 null，如果是基本数据，没有定义默认值，那么成员变量的值是有意义的，比如 int 就是 0，boolean 就是 false。

**方法**

语法：

```
[修饰符] 方法的返回值数据类型 方法名(形参列表) {
    方法体语句;
}
```

* 修饰符：可以省略，也可以是 public protected private static final abstract，其中 public protected private 只允许出现
* 返回值：可以是数据类型（不要忘了自定义的数据类型），也可以是 void，如果定义了返回值，那么就必须在 return 后面跟随该类型的值或者对象。
* 方法名：一般首字母小写，也适用驼峰命名法则，一般是动词在前，名词在后，不易过长
* 形参列表：定义方法可以接受的参数，由 0-N 个 「数据类型 参数名」通过 「,」 组合的。一旦方法指定了形参，那么在调用的时候就必须一一对应的传入实参。

**static 关键字**

用于修饰成员变量和方法，用 static 修饰的成员变量后者方法是属于 **类** 的，而不属于该类的实例（对象）。通常把 static 修饰的成员变量称为「类变量、静态变量」，方法称为「类方法、静态方法」

> 静态的成员是不能访问非静态成员的；
>
> 静态成员之间是可以互相访问的。

```java
static String teacher = "陆老师";

// 方法

static String fun2() {
    System.out.println(this.name); // 错误代码
    System.out.println(teacher);
    return "";
}
```

**使用一个对象的过程**

* 定义类
* 构建和使用对象

语法：

```
类类型 对象名 = new 构造器方法();
```

实例：

```java
Student1 hehao = new Student1("何浩", 20, "C25");
```

在内存中的执行过程：

1、在栈内存中，会存储对象名，在没有执行构造器创建对象并赋值时，此时对象名对应的值为 null；

2、通过 new 关键字调用类的构造器在堆内存中分配了一块对象区域；

3、通过赋值运算符 = ，将堆内存中的对象地址赋给栈内存中的变量名；

4、例如再次给对象的属性赋值：通过栈内存定位到对象在堆内存中的地址，找到相应的成员变量，进行赋值操作。

> 引用，还可以称为「地址」、「指针」，特指类类型，因为只有类类型才会在堆内存中分配对象空间，并将地址（指针）在栈内存中用于对象变量名的引用。

**this 关键字**

Java 中使用 this 关键字，指向调用该方法的对象。根据 this 所在的位置，大致分为两种：

* 出现在构造器中：引用该构造器正在初始化的对象；
* 普通方法中：调用该方法的对象。

this 用于在类定义中，获取当前对象的属性，或者调用当前对象的方法。

> 在类定义中，可以省略 this 关键字去调用属性或者方法，但是在类被编译的时候，编译器还是会加上 this 关键字。所以强烈建议在类定义时如果要调用该类中的普通成员变量后者方法，还是要把 this 加上去。
>
> 用 static 修饰的方法中是不能使用 this 关键字的。

```java
Student1(String name, int age, String code) {
    this.name = name;
    this.age = age;
    this.code = code;
}

String intro() {
    return "我叫" + this.name + "，我的学号是" + this.code + "，我今年" + this.age + "岁了。";
}

void listen() {
    System.out.println("自我介绍：" + this.intro() + "  " + this.name + "在上课。");
    return;
}

static String fun2() {
    return this.intro(); // 错误代码
}
```

### 方法的详解

**所属性：**

要么属于类（用 static 修饰的方法）、要么属于对象。

```java
public class Demo6 {
	public static void main(String[] xxx) {
		// 获取用户输入的信息
		int age = Integer.valueOf(xxx[0]);
		String sex = xxx[1];
		
		// 构建封装对象
		Student1 stu = new Student1();
		stu.age = age;
		stu.sex = sex;

		// 执行业务逻辑
		System.out.println(stu.fun1() ? "合法" : "非法");

		
	}
}

class Student1 {
	int age;
	String sex;

	// 用于判断年龄和性别是否是合法结婚年龄的方法
	boolean fun1() {
		if (this.sex.equals("男")) {
			if (this.age >= 25) {
				return true;
			} else {
				return false;
			}
		} else {
			if (this.age >= 23) {
				return true;
			} else {
				return false;
			}
		}
	}
}

```

> 程序的设计：
>
> * 用户的输入
> * 输入内容进行封装
> * **调用业务逻辑方法**
> * 输出结果

**方法关心的要素**

* 方法属于谁
* 方法的参数
* 方法的返回值



