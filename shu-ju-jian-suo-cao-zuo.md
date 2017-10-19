# 数据检索操作

## 简单的数据检索

* **指定字段的数据记录查询**

如果某张表的字段较多，但是在具体的某个场景中，只需要用到部分字段的信息，使用该查询。

语法：

```sql
SELECT field1, field2,... FROM table_name [WHERE condition]
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



