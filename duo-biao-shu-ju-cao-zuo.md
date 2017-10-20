# 多表数据操作

## 表之间的关系

* 一对多（多对一）

> 在多的一方加入一的一方的外键

* 多对多

> 通过一个中间表将两个表之间建立关系

* 一对一

> 在所谓的子表中加入所谓主表的外键，并加上唯一性约束

## 表关联查询

自然连接查询

> 使用 WHERE 条件将两个表之间进行关联查询

```sql
SELECT s.clazz_id,s.code,s.`name`,c.id,c.`name`
FROM student as s, clazz as c
WHERE S.clazz_id = C.id
```



