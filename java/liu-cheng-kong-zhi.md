```
流程控制
```

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
> 在实际的开发中，我们一般使用 if - else 结构替代 switch.



