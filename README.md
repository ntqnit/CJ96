![](/assets/005.png)# 计算机软件概论

## 计算机学科分类

    计算机硬件、计算机网络、计算机软件
    
### 计算机硬件

**认识的计算机的组成**

CPU、显卡、主板、显示器、内存、硬盘、电源、键盘鼠标

**计算机组成**

控制器、运算器、存储器、输入设备、输出设备

- 存储器：硬盘、内存、U盘、光盘、软盘
- 内存：一般指运行中的程序进行数据存储的介质，是在学习软件开发中，硬件部分要着重理解的概念。
- CPU：控制器和运算器
- 输入设备：键盘、鼠标、写字板、话筒
- 输出设备：打印机、显示器

### 计算机网络

> "信息高速公路"：要致富，先修路

网络的发展孕育了开源、分享（OpenSource/Share）的精神。

**IP 地址**

计算机在网络中的唯一标识（网络的概念：包含了广域网和局域网）

如果一台计算机在局域网中，并且该局域网连接了互联网，则该机器会有两种身份，一个在是局域网中的IP地址，还有一个对外的IP地址。

IP 地址的格式：192.168.1.154（4个分隔，每个数字从0-254）

**如何查看IP地址**

进入命令提示符CMD中

输入命令 ``` ipconfig ```

## 软件的分类

### 系统软件
> 系统软件就是一个国家

- Windows
- iOS
- Linux

### 应用软件
> 应用程序就是具备特定功能的实体，比如医院、警察局、体育馆等

**下载类型的软件**

> 这类软件我们也成为**客户端软件**，或者叫 **C/S 架构**的软件（Customer/Server）,主程序是在客户端机器的。

有新的内容需要下载插件或者重新下载整个安装包去更新。但是，可以获取到本地的资源，让应用程序能够运行的更加流畅。

**基于浏览器访问的应用**

> 浏览器本身就是一个客户端软件，网站、Web信息管理系统很多都采用 B/S 架构进行设计（Browser/Server）,主程序放在服务器中，核心的业务逻辑也是在服务器中运行的。

浏览器有IE/Chorme/Firefox等

*优势与劣势*

- B/S 架构程序的更新对终端用户来讲，是完全透明的。
- 但是，在客户端浏览器中每一个资源（文字、图片、视频、样式）都要全部从服务器中请求到，服务器的压力比较大，而且不同的网络环境，对于终端来讲，请求的时间也不是不尽相同的。
- B/S 架构的软件能够不断发展和兴起的主要原因是“信息高速公路”

## 学习的重点

**我们的课程是学习基于B/S架构的Web应用**

在 B/S 架构的应用中，主要是做网站类应用、信息化系统类应用（CRM客户关系系统、HIS医疗信息系统、OA办公系统、ERP企业信息化系统、MES......） 

## B/S 架构的应用程序原理

### 访问地址的说明

**服务器**

> 服务器的概念：全天候，对外有固定的 IP 地址，而且配置较高的计算机。

**域名**

> 域名：唯一的，格式一般为 xx.xx，一般的域名的后缀有 .com .cn .net .edu .org .com.cn .tt .xyz等，域名的用途很简单，就是解析到某个具体的IP地址服务器上

**关于访问地址的解释**

浏览器访问的完整的路径名：

如：``` http://www.qq.com:80/news/1016/1.html``` 

- 协议：http
- 主机：www
- 域名：qq.com
- 端口：80
- 资源：news/1016/1.html

**原理图**

![](/assets/005.png)



