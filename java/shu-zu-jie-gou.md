# 数组结构

数组是编程语言中最常用的一种**数据类型**。可以存储多个数据。

**数组的要点**

* 存放的数据是相同的数据类型
* 数组的长度在定义时就确定了大小，数组是不可变长度的，或者说叫定长
* 数组中可以存放任意的数据类型（包含基本数据类型、引用数据类型、数组）
* 数组本身是引用数据类型（在栈内存中会存储其在堆内存中的引用地址）

**定义语法**

```
type[] 变量名; // 强烈建议用这种命名
type 变量名[]; // 只要知道就可以
```

**数组的初始化**

在 Java 语言中，数组必须先被初始化，才能被使用。所谓的初始化，就是在内存中为数组元素分配空间，并未每个元素赋予初始值。

* 静态初始化：显式的指定每个数组元素的值，由系统来决定数组的大小；
* 动态初始化：只需要指定数组的长度，通过程序动态的给每个元素赋值。

静态初始化

语法：

```
type[] arrayName = {element1, element2,....}; // 比较常见
type[] arrayName = new type[]{element1, element2,...};
```

```java
int[] arrs2;
arrs2 = new int[]{1, 2 ,3 ,4};

int[] arrs = {1, 2, 3, 4}; // 简写
```

动态初始化

语法：

```
type[] arrayName = new type[length];
```

> 数组中的索引，通过 arrayName\[index\] 获取指定位置的数据，index 从 0 开始，最大值为 length-1

* 通过数组索引方式对数组元素进行赋值时，使用数组.length属性作为 for 循环的条件。
* 在对数组元素进行操作时，一般使用 for 循环结构。

```java
for (int i = 0; i < arrs3.length; i++) {
    arrs3[i] = (i+1) * 10;
}

for (int i = 0; i < arrs3.length; i++) {
    System.out.println(arrs3[i]);
}
```

foreach 遍历数组

```
for (type element : array | collections) {
    element...
}
```

实例：

```java
for(int a : arrs3) {
    System.out.println(a);
}
```

> 使用 foreach 一般情况下，值用作**遍历数据**，如果要对数组中元素进行修改，还是需要使用 for 循环带索引的方式进行，因为在上述的代码中，a 只是循环元素的一个副本。



