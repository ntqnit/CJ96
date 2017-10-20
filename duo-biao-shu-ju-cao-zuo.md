# 多表数据操作

## 表之间的关系

* 一对多（多对一）

> 在多的一方加入一的一方的外键

* 多对多

> 通过一个中间表将两个表之间建立关系

* 一对一

> 在所谓的子表中加入所谓主表的外键，并加上唯一性约束

## 表关联查询

**自然连接查询**

> 使用 WHERE 条件将两个表之间进行关联查询

```sql
-- 查询学员的学号、姓名、所在班级名称
SELECT s.clazz_id,s.code,s.`name`,c.id,c.`name`
FROM student as s, clazz as c
WHERE S.clazz_id = C.id
```

要注意的是，如果不加条件，直接查询，会把两个表进行笛卡尔积的操作，查询出来的数据是有问题。

**内连接查询**

> 内连接查询是可以使用自然连接查询替代的，但是效率方面，内连接会高

```sql
-- 内连接查询
SELECT s.`code`, s.`name`, c.`name` FROM student s 
INNER JOIN clazz c ON s.clazz_id = c.id
```

**左外连接查询**

> 以左表为主表，左表中的数据都会被显示出来，关联的右表中，如果存在符合条件的数据，那么会被关联出并显示，如果没有，则会显示 NULL。

```sql
-- 左外连接
SELECT s.`code`, s.`name`, c.`name` FROM student s 
LEFT JOIN clazz c ON s.clazz_id = c.id
```

自学内容：右外连接、全连接

