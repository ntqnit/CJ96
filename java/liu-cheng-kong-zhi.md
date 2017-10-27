# 流程控制

* 顺序结构
* 判断（分支选择）结构
* 循环结构

## 顺序结构

程序是一个自上而下运行的过程。

## 分支选择结构

Java 中的分支选择结构有 if 结构、switch 结构

### if 结构

具备三种类型的结构表现形式

* 形式一：

```java
if (logic expression) {
    statement;
}
```

```java
int age = 20;
if (age > 18) {
    String name = "Tom";
    System.out.println("我叫" + name + "，已经" + age + "岁了，我成年了！");
}
```

* 形式二：

```java
if (logic expression) {
    statement;
} else {
    statement;
}
```

```java
int age = 16;
if (age > 18) {
    String name = "Tom";
    System.out.println("我叫" + name + "，已经" + age + "岁了，我成年了！");
} else {
    System.out.println("我还未成年！");
}
```

* 形式三：

```java
if (logic expression) {
    statement;
} else if (logic expression) {
    statement;
} else {
    statement;
}
```

```java
if (age >= 0 && age <= 10) {
    System.out.println("少年");
} else if (age <= 18) {
    System.out.println("青少年");
} else if (age <= 30) {
    System.out.println("青年");
} else if (age <= 50) {
    System.out.println("中年");
} else {
    System.out.println("老年");
}
```

### switch 结构

swtich 语句是有控制表达式和多个 case 标签块组成。在控制表达式中，只允许出现 byte、short、int、char四种基础数据类型，在JDK1.7以后，支持 String 类型的控制表达式。

```java
switch (expression) {
    case condition1 : {
        statement;
        break;
    }
    case condition2 : {
        statement;
        break;
    }
    default : {
        statement;
        break;
    }

}
```

```java
String color = "red";
switch (color) {
case "red": {
    System.out.println("红色");
    break;
}
case "blue": {
    System.out.println("蓝色");
    break;
}
case "green": {
    System.out.println("绿色");
    break;
}
default: {
    System.out.println("没有找到");
    break;
}
}
```

> 在 case 中要加入 break 关键字跳出；
>
> 在实际的开发中，我们一般使用 if - else 结构替代 switch。swtich 结构应用的较少。

## 循环结构

循环语句可以在满足循环条件的情况下，反复执行某一段代码。

被重复执行的代码叫做循环体。

循环语句可能包含的部分有：

* 初始化语句（init\_statement）：一条或多条语句，这些语句用于完成一些初始化的工作。
* 循环条件（test\_expression）：是一个 boolean 类型的表达式，这个表达式决定是否继续执行循环体。
* 循环体（body\_statement）：如果条件允许，循环体会被反复执行。
* 迭代语句（iteration\_statement）：在一次循环体执行结束后，对循环体条件进行求值，通常用于控制循环条件中的变量，使得循环在合适的时候结束。

### while 结构

```java
(init_statement);
while (test_expression) {
    body_statement;
    [iteration_statement];
}
```

```java
int sum = 0;
int i = 1;

while (i <= 10) {
    sum = sum + i;
    i++;
}

System.out.println(sum); // 55
```

### do-while 结构

```
(init_statement);
do {
    body_statement;
    [iteration_statement];
} while (test_expression)
```

> 无论如何都会执行一次循环体内容





