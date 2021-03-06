# 修改数据语句

新增数据、修改数据、删除数据

> 在书写 SQL 语句时我们一般遵循关键字是大写，虽然在SQL中是不区分大小写的，但是对于关键字建议是用大写，自己定义的表、视图、函数这类使用小写。

## 新增数据

* 指定字段插入语法：

```sql
INSERT INTO table_name(field1, field2,...) VALUES(value1, value2, value3)
```

1. field1可以省略不写，但是如果不写，后面VALUES的顺序是要和你定义时的顺序保持一致的；
2. field1如果写了，那么fields里面的顺序要和VALUES后面的数值保持一致。

> 在实际的开发中，一般都要给定字段进行插入，不建议省略fields的定义。

* 批量插入查询结果

```sql
INSERT INTO table_name(field1, field2,...) SELECT field1, field2, ... FROM new_talbe
```

示例：

```sql
INSERT INTO s_v1(code, name, birthday)
SELECT code, name, birthday FROM s
```

## 修改数据

> 在程序开发中，修改数据一般是非常关键的操作，所以，只要是写更新数据的语句的时候，一定要想好**条件**。

语法：

```sql
UPDATE table_name SET field1=value1, field2=value2, ... WHERE condition
```

示例：

```sql
UPDATE s SET code='ss6',birthday='1990-10-10' WHERE name='zhangsan'
```

## 删除数据

> 同样的和修改数据操作一样，在删除数据的时候，一定要加上删除数据的**条件**。

语法：

```sql
DELETE FROM table_name WHERE condition
```

示例：

```sql
DELETE FROM s WHERE name='zhangsan'
```



