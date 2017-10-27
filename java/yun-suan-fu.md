# 运算符

## 算术运算符

```
+ - \* / % ++ --
```

* 运算符除了进行数学运算的加法之外，还可以做字符串的拼接。  
  ++ 自增  
  -- 自减

实例：

```java
int m = 10;
System.out.println(m++); // 10
System.out.println(m); // 11
System.out.println(++m); // 12
System.out.println(-m); // -12
```

## 赋值运算符

= += -+ \*= /= %=

实例

```java
m += 1; // m = m + 1
System.out.println(m); // 13
m -= 1; // m = m - 1
System.out.println(m); // 12
```

## 比较运算符

用于判断两个变量或者常量的大小，返回结果为 true/false。

`&gt; &lt; &gt;= &lt;= == !=`

> 左右两边的操作数只能是数值

## 逻辑运算符

运算符两边必须是 boolean 类型的变量、常量、表达式

与 && 或者 \|\| 非 !

与：只要有一个假就是假

或者：只要有一个真就是真

## 三目运算符

expression ? if-true-statement : if-false-statement

实例：

```java
int age = 16;
String ageStr = age > 18 ? "成年" : "未成年";
System.out.println(ageStr); // 未成年
```

## 结合性和优先级

应该尽量在比较复杂的表达式中使用圆括号，明确的标注计算的优先级。

---

**自学部分：**

关于运算符优先级表

## 



