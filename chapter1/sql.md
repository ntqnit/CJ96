# MySQL标准SQL

应用程序对数据库的访问是通过SQL语句完成的，在SQL中，可以分为
- 数据定义语句
- 数据操作语句
    - 修改数据的语句
    - **查询数据的语句**（重点）
    
## 修改数据语句

新增数据、修改数据、删除数据

> 在书写 SQL 语句时我们一般遵循关键字是大写，虽然在SQL中是不区分大小写的，但是对于关键字建议是用大写，自己定义的表、视图、函数这类使用小写。

**新增数据**

_指定字段插入语法：_

```sql
INSERT INTO table_name(field1, field2,...) VALUES(value1, value2, value3)
```
- field1可以省略不写，但是如果不写，后面VALUES的顺序是要和你定义时的顺序保持一致的；
- field1如果写了，那么fields里面的顺序要和VALUES后面的数值保持一致。

> 在实际的开发中，一般都要给定字段进行插入，不建议省略fields的定义。

_批量插入查询结果_

```sql
INSERT INTO table_name(field1, field2,...) SELECT field1, field2, ... FROM new_talbe
```
实例

```sql
INSERT INTO s_v1(code, name, birthday)
SELECT code, name, birthday FROM s
```

**修改数据**

> 在程序开发中，修改数据一般是非常关键的操作，所以，只要是写更新数据的语句的时候，一定要想好**条件**。

语法：

```sql
UPDATE table_name SET field1=value1, field2=value2, ... WHERE condition
```






    
