# 数据检索操作

## 简单的数据检索

* **指定字段的数据记录查询**

如果某张表的字段较多，但是在具体的某个场景中，只需要用到部分字段的信息，使用该查询。

语法：

```sql
SELECT field1, field2,... FROM table_name [WHERE condition] [ORDER BY field1 ASC/DESC, field2 ASC/DESC,...]
```

示例：

```sql
SELECT 
course.name AS '名称',
course.code AS '编码' 
FROM c AS course
```

> 我们习惯的会在查询中指定表的别名，同样在字段上写可以定义别名。

* **查询所有数据**

使用通配符`*`查询

语法：

```sql
SELECT * FROM table_name [WHERE condition]
```

> 此处遍历出来的数据的顺序是创建表中字段的顺序。

* **避免重复数据的查询**

使用关键字：DISTINCT

> 例如要查询有在校生的班级编号，就可以使用 DISTINCT 关键字，查询 stu\_info 表。
>
> 在使用 DISTINCT 查询时要注意：其效率较低的。

```sql
SELECT DISTINCT clazz FROM stu_info
```

* **查询数据处理**
  * 数学运算的数据结果处理：+ - \* / %
    ```sql
    SELECT name, price AS '人民币', price/6 AS '美元' FROM t_menu
    ```
  * 格式化的数据处理
    使用CONCAT\(STR1, STR2, ...\)进行字符串拼接是最常用的。
    ```sql
    SELECT name, CONCAT('¥',price) AS '人民币', CONCAT('$',price/6) AS '美元' FROM t_menu
    ```

## 条件查询

* 带关系运算符和逻辑运算符的表达式；
* 带 BETWEEN AND 关键字的条件查询；
* 带 IS NULL 关键字的条件查询；
* 带 IN 关键字的条件查询；
* 带 LIKE 关键字的条件查询。

**关系运算符和逻辑运算符**

关系运算符：&gt;、 &gt;=、 &lt;、 &lt;=、 !=\(&lt;&gt;\)、 =；

逻辑运算符：AND\(&&\)、OR\(\|\|\)、NOT\(!\)、XOR。

示例：

```sql
SELECT * FROM stu_info WHERE age >= 18 AND clazz = 'C1' AND code = '01'
```

**BETWEEN ADN**

> 一般用在对数值或者日期的区间判断条件中，而且是可以被替代的。

```sql
SELECT * FROM stu_info WHERE age BETWEEN 16 AND 20
SELECT * FROM stu_info WHERE age >= 16 AND age <=20
-- 使用 NOT 取反
SELECT * FROM stu_info WHERE NOT (age >= 16 AND age <=20)
```

**IS NULL**

> 判断数据结果集中非空元素，要注意的是：NULL 和 空字符串是两个概念，使用的查询条件不尽相同

```sql
SELECT * FROM stu_info WHERE name IS NULL;
SELECT * FROM stu_info WHERE name = ''; -- 判断空字符串
```

使用非空判断是要注意

```sql
SELECT * FROM stu_info WHERE name IS NOT NULL
```

**IN**

> 条件在某些离散的数据范围内

```sql
SELECT * FROM stu_info WHERE clazz IN ('C1', 'C2');
-- 替代方案
SELECT * FROM stu_info WHERE clazz = 'C1' OR clazz = 'C2'
```

LIKE

> 模糊查询：用的较多，一般用到的是全匹配 `%搜索字%`，尾部匹配 `搜索字%`
>
> 其他还有单个字匹配 `_` 和首部匹配 `%搜索字`

```sql
SELECT * FROM stu_info WHERE name LIKE '李_强';
SELECT * FROM stu_info WHERE name LIKE '李%';
SELECT * FROM stu_info WHERE name LIKE '%李%';
```

## 数据排序

> 数据的排序方式：顺序 ASC、逆序 DESC。
>
> 在排序中是可以多字段排序的，即会有第一排序条件和第二、三...次排序条件

```sql
SELECT * FROM stu_info ORDER BY clazz ASC, code DESC
```

## 限制数据记录数量

使用 LIMIT 关键字，后面跟两个参数，第一个参数是从第几条开始，第二个是一共显示多少条记录

```sql
SELECT * FROM stu_info ORDER BY clazz ASC, code DESC LIMIT 9, 3

-- 显示 page 页，每页显示 num 条记录
-- page = 2; num = 3;
-- x = (page - 1) * num
-- y = num
```

## 统计函数和分组查询

例如要查询：

* 每个班级有多少学生；
* 每个班级中年龄最大的学生是谁；

> 对于一个较完整的 SQL 语句执行的解释

```sql
SELECT 
clazz,MAX(age) AS '最大年龄',
COUNT(*) AS '多少人' 
FROM stu_info 
WHERE id > 2
GROUP BY clazz HAVING count(*) > 1
ORDER BY MAX(age) DESC
```

执行顺序

1. 筛选整个表找那个`id > 2` 的数据；
2. 把筛选出的记录按照 `clazz` 字段进行分组；
3. 把分组完的结果，筛选出每组数据总数量 &gt; 1的数据 `count(*) > 1`；
4. 按照分组后的字段进行排序 `MAX(age) DESC`；
5. 按照 SELECT 中要求显示的字段输出结果集。

**常用的统计函数**

COUNT：在实际开发中，会使用 COUNT 函数计算条件查询后的总数据量，用于计算总页数。另外用在分组聚合函数中求分组单元中的数据量。

SUM/AVG/MAX/MIN：自学。

分组查询语法：

```
SELECT
分组完的字段1,
分组完的字段2,
...
FROM 表名 
[WHERE 全局表的过滤条件] 
[GROUP BY 表字段1, 表字段2
 HAVING 分组完成后的过滤条件（可以加聚合）
]
[ORDER BY 分组完的字段1 ASC/DESC, 分组完的字段2 ASC/DESC,...]
```



