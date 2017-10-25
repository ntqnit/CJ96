# JAVA

## 什么是Java

Java可以理解为编程语言或者开发工具。

**目的**

Java 最终的目的是用于编写直接在机器上运行的程序。

与 HTML 运行与浏览器，SQL 运行与数据库系统对比，Java 能做的事情更多，更加的普遍。

**对于跨平台的理解**

为了让平台对编程人员透明，写出可以在不同平台运行的相同源代码，Java 开发除了 JVM （Java 虚拟机）。

> 一次编译，到处运行。

## Java 的发展史

* Java 创始人
* Java 的演化步骤
* SUN 公司
* Oracle 公司 09 年收购 SUN 公司

## JDK

Java开发工具包（Java Development Kit），是一套用户给 Java 编程人员的开发套件，其中包含了：

* JRE （Java Runtime Envoirment）：Java 运行时环境，其中最重要的部件是 JVM；
* Java 开发工具：编译工具 javac、API 生成工具 javadoc......；
* 核心类库 （Java API）

**下载 JDK 并安装**

目录说明

```
├─bin 存放一系列的命令和工具
├─db
├─include
├─jre Java运行时环境
└─lib 核心类库
```

## **通过配置方式部署 JDK**

**关于命令提示符的基本操作**

打开命令提示符：`cmd`

进入相应的盘符：`c: d: e:` 回车

列式某个目录下的所有文件：`dir`

```
2017/09/14  13:56    <DIR>          env
2017/10/25  10:17               110 Hello.java
2017/10/22  09:21               113 index.html
2017/09/25  09:16             3,961 logo.png
2017/10/15  22:56    <DIR>          My Training
2017/10/01  19:20    <DIR>          MySQL Datafiles
2017/10/23  14:22    <DIR>          Pic
2017/10/19  17:22    <DIR>          Program Files
2017/10/18  08:57    <DIR>          QMDownload
2017/10/25  10:45    <DIR>          temp
2017/10/04  23:21    <DIR>          Virtual Machines
2017/10/12  12:55    <DIR>          Work
2017/10/22  09:15                 0 新建文本文档.txt
```

> 在资源管理器中，文件夹和文件我们要相同对待，即是同一类型的。

进入某个目录：`cd` 目录名（目录名的通配使用\*）

```
D:\>cd my*

D:\My Training>
```

返回到上一层目录：`cd..`

**什么是环境变量**

进入环境变量：「我的电脑-右键」-&gt; 「属性」-&gt; 「高级系统设置」-&gt; 「环境变量」

定义变量：

引用变量：

Path 变量的用途：系统的全局的路径，我们在任意位置可以访问在 Path 定义的文件夹（目录）中的可执行程序或者批处理文件，在Windows 系统中，可以直接执行的文件有 exe/bat。

> 在 Path 变量中，可以定义多个文件目录，之间用`;`号隔开

**配置 JDK**

前提条件：需要包含完整 JDK 文件的文件夹。

1、 JAVA\_HOME = `d:\xx\xx\jdk1.8`

2、在 Path 中**追加目录** `%JAVA_HOME%\bin`

3、CLASSPATH = `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`

这样就完成了 JDK 的部署。

## 第一个 JAVA 程序

Hello,World 程序的意图：验证你配置的开发环境是否是正确有效的。

在某个目录中新建一个名叫 Hello.java 的文件（注意把文件后缀隐藏选项去掉），文件内容如下

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

1、使用 javac 命令将 Hello.java 文件编译成 Hello.class 字节码文件

```
javac Hello.java
```

2、使用 java 命令，调用本机的 JVM 执行字节码文件

```
D:\>java Hello
Hello, World!
```

另一个程序案例

使用 Java 编写乘法口诀表

```java
public class Hello {
    public static void main(String[] args) {

        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print("" + i + " * " + j + " = " + (i*j) + "\t");
            }
            System.out.println();
        }
    }
}
```

运行结果

```
1 * 1 = 1
2 * 1 = 2       2 * 2 = 4
3 * 1 = 3       3 * 2 = 6       3 * 3 = 9
4 * 1 = 4       4 * 2 = 8       4 * 3 = 12      4 * 4 = 16
5 * 1 = 5       5 * 2 = 10      5 * 3 = 15      5 * 4 = 20      5 * 5 = 25
6 * 1 = 6       6 * 2 = 12      6 * 3 = 18      6 * 4 = 24      6 * 5 = 30      6 * 6 = 36
7 * 1 = 7       7 * 2 = 14      7 * 3 = 21      7 * 4 = 28      7 * 5 = 35      7 * 6 = 42      7 * 7 = 49
8 * 1 = 8       8 * 2 = 16      8 * 3 = 24      8 * 4 = 32      8 * 5 = 40      8 * 6 = 48      8 * 7 = 56      8 * 8 = 64
9 * 1 = 9       9 * 2 = 18      9 * 3 = 27      9 * 4 = 36      9 * 5 = 45      9 * 6 = 54      9 * 7 = 63      9 * 8 = 72      9 * 9 = 81
```



