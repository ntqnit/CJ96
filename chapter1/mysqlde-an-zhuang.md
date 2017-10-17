# MySQL的下载和安装

## 下载

[下载地址](https://dev.mysql.com/downloads/mysql/)

> 要注意的问题：选择你所用的操作系统和操作系统的位数

选择安装版本 MSI Installer

![](/assets/001.png)

## 安装

> 如果已安装要卸载重新安装，需要把`C:\ProgramData\MySQL` 目录删除，否则在安装的最后一步会出现问题。

**安装需要注意的几个问题**

- 在配置步骤中，字符编码选择UTF8；
- 端口默认是3306，可以修改，但是不建议；
- 创建root账号的密码；

![](/assets/002.png)

![](/assets/003.png)

![](/assets/004.png)

## 使用默认的MySQL客户端管理

> 关于环境变量的Path的解释：.exe .bat 是Windows平台的可执行文件，为了方便，我们把MySQL的安装目录下的bin目录追加到Path中（**在Windows10以下的系统中要特别注意不要把Path的变量值全部都替换掉，要在后面追加，加上;**）

**关于DOS命令的简单说明**

- 进入命令提示符控制台CMD，命令：打了一个字符串通过回车让计算机去执行一定的操作；
- 进入盘符，`D:` `C：`
- 进入到目录 `cd` ，跟的目录名称是可以使用通配符*，比如要进入 d:/mydocument ，可以通过命令 `cd mydoc*`
- 返回上级目录 `cd..`
- 列式目录 `dir`
- 树状列式目录内的所有文件 `tree`

例如通过tree打印MySQL安装目录的全部文件结构


    ├─bin
    ├─data
    │  ├─mysql
    │  └─performance_schema
    ├─docs
    ├─include
    │  └─mysql
    │      └─psi
    ├─lib
    │  ├─debug
    │  └─plugin
    └─share
        ├─charsets
        ├─czech
        ├─danish
        ├─dutch
        ├─english
        ├─estonian
        ├─french
        ├─german
        ├─greek
        ├─hungarian
        ├─italian
        ├─japanese
        ├─korean
        ├─norwegian
        ├─norwegian-ny
        ├─polish
        ├─portuguese
        ├─romanian
        ├─russian
        ├─serbian
        ├─slovak
        ├─spanish
        ├─swedish
        └─ukrainian


## 使用Navicat管理工具

**建立数据库连接**

文件-新建连接-MySQL

输入包括：IP地址、端口号、用户名、密码

**完成数据表的创建和使用**

> 在MySQL中可以建立多个库，每个库由多个表构成。






