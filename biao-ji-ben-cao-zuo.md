# 表基本操作

## MySQL的存储引擎

在较为大型的应用系统中，我们一般为将数据库做**读写分离**操作。

MySQL的主要存储引擎：

* **InnoDB：**支持事务

> 事务：多条指令原子性的执行。

* MyISAM：不支持事务，但是它的数据访问效率较高

## 表操作

**创建表**

> 表的元素有：表名、表的字段
>
> 表字段的元素有：字段名、**数据类型**、字段长度、**约束**

```sql
CREATE TABLE table_name (
    字段名称 字段数据类型 [字段约束],
    字段名称 字段数据类型 [字段约束] 
)
```

示例：

```sql
-- 创建表的语句
CREATE TABLE student_info (
    code VARCHAR(50),
    name VARCHAR(50)
)
```

**SQL语言的注释**

用`--`表示注释部分的内容

**MySQL 字段数据类型**

> 主要分为：数值、日期、字符串三种类型。

数值类型：MySQL 是支持所有标准 SQL 中的数值类型。在绝大多数的应用程序中，我们使用 INT 和 DECIMAL 类型就可以了。

* INT：整型
* DECIMAL：浮点类型
* 其他数值类型：SMALLINT、NUMBERIC

日期类型：一般使用 DATETIME （用日期和时间构成）、DATE（只是表示日期），其他不常用的还有 TIME 、YEAR等等。

字符串类型：一般最常使用 VARCHAR（可变长度）、CHAR（定长）、TEXT（长文本类型，例如博客文章等数据），其他不常用的还有 LONGTEXT、TINYTEXT等等。

> VARCHAR 和 CHAR 的区别：例如 VARCHAR 定义的长度为 200，在使用的时候是存储了 4 个字符长度的字符串，那么在数据库中只会占用 4 个字符的数据空间，CHAR 是定长，无论存储多少数据，在数据空间中都会占用到定义的长度。

在数据中，我们一般不会去存储类似照片、视频这样的二进制文件，而是把这些文件在服务器中的访问地址用字符串类型的数据进行存储。

> 在定义数据库字段名称时，由于数据库不区分大小写，所以，一般碰到了多个单词，我们用`_`分隔

示例：

```sql
-- 创建表的语句
CREATE TABLE student_info (
    code CHAR(2),
    name VARCHAR(50),
    age INT(12),
    weight DECIMAL(10, 2),
    birthday DATE,
    in_school DATETIME,
    description TEXT
)
```

**表的约束**

在一个完整的表中，是需要对表中的字段进行相关约束的。

> 使用约束主要是为了保证数据表中数据的合法性以及相对完整性。

约束类型包括：

* 主键约束（PRIMARY KEY:PK）：唯一的确定在数据表中的记录，而且主键约束是不能为空的，我们一般使用没有业务含义的字段去进行主键定义，在MySQL中可以使用自增长类型的主键或者可以使用 UUID 。
* 非空约束（NOT NULL）
* 默认值（DEFAULT）
* 唯一约束（UNIQUE KEY:UK）
* 外键约束（FOREIGN KEY:FK）

语法：

```sql
CONSTRAINT 外键名称 FOREIGN KEY 外键字段 REFERENCES 外键关联表(关联表的字段)
```

* 自动增长（AUTO\_INCREMENT）、

综合示例：

```sql
-- 创建表的语句
CREATE TABLE student_info1 (
    id INT AUTO_INCREMENT PRIMARY KEY,
    -- 建立非空和唯一性约束
    code CHAR(2) NOT NULL UNIQUE,
    name VARCHAR(50) NOT NULL DEFAULT 'zhangsan',
    age INT(12) NOT NULL,
    weight DECIMAL(10, 2),
    birthday DATE NOT NULL,
    in_school DATETIME NOT NULL,
    description TEXT
)

CREATE TABLE student_account1 (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    account VARCHAR(20),
    password VARCHAR(20),
    CONSTRAINT FK_SI_SA_01 FOREIGN KEY (student_id) REFERENCES student_info1(id)
)
```

> 主键是用来定义一条记录的唯一性的，在应用程序中，一般通过 ID 找到某条记录，主键是不会用过更新的。
>
> 在建立了外键关系的两个表中，一般是子表通过某个字段引用主表的**主键**数据，如果要去对外键数据进行处理，一般我们会先解除外键关系，然后对数据处理后再加上。

删除表：自学完成

修改表：自学完成

XMind

