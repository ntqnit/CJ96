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



