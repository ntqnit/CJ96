# 综合应用

> 结合之前所学知识，运用 SQL 语言完成一个实例应用的数据操作，重点是了解在应用程序中，如何构建数据查询语句。  
> 任何基于数据库的应用程序类型，包括 B/S 架构、 C/S 架构、APP 应用，其实归根结底都是用不同的界面或者形式完成对数据库中数据的操作，所以，了解数据中应用的处理过程很重要。

一个典型的应用程序，包含的功能有：

* 基础数据维护：一般通过初始化完成部分数据，后续再次维护；
* 业务流程处理：一般通过具体的功能模块完成；
* 数据分析和报表：通过相关复杂的查询完成，使用视图，或者缓存统计报表。

下面，我们从上一章节中的订餐系统进行延伸，模拟系统的数据操作过程等。

## 表结构

以下为表的物理结构脚本

**基础数据表：**

## 数据处理

**1、注册会员**

> 输入项：曹敏、女、1380000000，作为一个完整的记录，还需要默认值

```sql
INSERT INTO t_base_customer(name, sex, tel, vip_code, is_vip)
VALUES('曹敏', 1, '138000000', CONCAT('V',unix_timestamp(now())) ,1);
```

**2、会员信息完善**

> 输入项：用户ID、微信账号、地址、生日

```sql
UPDATE t_base_customer SET wechat='123456', address='南通', birthday='1995-10-10' WHERE id=4;
```

**3、客户点餐**

> 输入项：餐厅、服务员、餐桌、时间、会员、就餐人数

```sql
INSERT INTO t_busi_order_head(code, member, restaurant_id, employee_id, table_id, enter_time, customer_id, amount, state)
VALUES(CONCAT('PO',unix_timestamp(now())),'是', 1, 4, 1, now(), 4, 8, 1);
```

**4、确认订单菜品**

4.1、插入订单明细数据

> 输入性：关联订单、规格ID、数量、非价格属性规格、备注

```sql
INSERT INTO t_busi_order_detail(order_head_id, menu_id, name, fode_code_id, cost, price, amount, specification, comment)
SELECT 5, m.id, m.name, s.id, s.specification_price, s.specification_cost, 1, '微辣', '少油'
FROM t_base_menu_stand s
LEFT JOIN t_base_menu m ON s.menu_id = m.id
WHERE s.id = 1;

INSERT INTO t_busi_order_detail(order_head_id, menu_id, name, fode_code_id, cost, price, amount, specification, comment)
SELECT 5, m.id, m.name, s.id, s.specification_price, s.specification_cost, 1, '', ''
FROM t_base_menu_stand s
LEFT JOIN t_base_menu m ON s.menu_id = m.id
WHERE s.id = 3;

INSERT INTO t_busi_order_detail(order_head_id, menu_id, name, fode_code_id, cost, price, amount, specification, comment)
SELECT 5, m.id, m.name, s.id, s.specification_price, s.specification_cost, 1, '中辣', '不要香菜'
FROM t_base_menu_stand s
LEFT JOIN t_base_menu m ON s.menu_id = m.id
WHERE s.id = 6;

INSERT INTO t_busi_order_detail(order_head_id, menu_id, name, fode_code_id, cost, price, amount, specification, comment)
SELECT 5, m.id, m.name, s.id, s.specification_price, s.specification_cost, 1, '中辣', '不要香菜'
FROM t_base_menu_stand s
LEFT JOIN t_base_menu m ON s.menu_id = m.id
WHERE s.id = 7;
```

4.2、 确认订单：修改订单头

> 输入项：订单编号，默认操作：确认时间、修改订单状态

```sql
UPDATE t_busi_order_head SET confirm_time = now(), state = 2 WHERE id = 5;
```

4.3、分配档口订单

> 输入项：订单编号,创建档口订单头表

```sql
INSERT INTO t_busi_window_order_head(amount, order_head_id, code, window_id, create_time)
SELECT count(*), 5, CONCAT('D',unix_timestamp(now())),m.window_id , now()
FROM t_busi_order_detail d
LEFT JOIN t_busi_order_head h ON d.order_head_id = h.id
LEFT JOIN t_base_menu m ON d.menu_id = m.id
WHERE h.id = 5
GROUP BY m.window_id;
```

4.4、档口订单明细

> 输入项：档口订单，档口ID，订单ID

```sql
INSERT INTO t_busi_window_detail(p_id, order_detail_id, finish_time)
SELECT 9, d.id, DATE_ADD(h.confirm_time,INTERVAL m.finish_time*d.amount MINUTE)
FROM t_busi_order_detail d 
LEFT JOIN t_busi_order_head h ON d.order_head_id = h.id
LEFT JOIN t_base_menu m ON d.menu_id = m.id
WHERE m.window_id = 1 AND h.id = 5;

INSERT INTO t_busi_window_detail(p_id, order_detail_id, finish_time)
SELECT 10, d.id, DATE_ADD(h.confirm_time,INTERVAL m.finish_time*d.amount MINUTE)
FROM t_busi_order_detail d 
LEFT JOIN t_busi_order_head h ON d.order_head_id = h.id
LEFT JOIN t_base_menu m ON d.menu_id = m.id
WHERE m.window_id = 3 AND h.id = 5;

INSERT INTO t_busi_window_detail(p_id, order_detail_id, finish_time)
SELECT 11, d.id, DATE_ADD(h.confirm_time,INTERVAL m.finish_time*d.amount MINUTE)
FROM t_busi_order_detail d 
LEFT JOIN t_busi_order_head h ON d.order_head_id = h.id
LEFT JOIN t_base_menu m ON d.menu_id = m.id
WHERE m.window_id = 4 AND h.id = 5;
```

**5、埋单**

5.1、修改订单数据

> 输入项：关联订单、收银员、优惠金额、支付方式

```sql
UPDATE t_busi_order_head h
INNER JOIN (SELECT SUM(d.price * d.amount) as psum, d.order_head_id as order_id FROM t_busi_order_detail d GROUP BY d.order_head_id) AS t ON h.id = t.order_id
SET h.cashier_id = 2, h.state = 3, h.total = t.psum, h.discount = 10, h.actual_amount = total - discount, h.check_out_time = now(), pay_type = '现金'
WHERE h.id = 5;
```

5.2、修改会员消费数据：增加消费数量、修改最近消费时间、增加消费总额，注意判断字段是否为空

> 输入项：关联订单

```sql
UPDATE t_base_customer c
INNER JOIN t_busi_order_head h ON h.customer_id = c.id AND h.id = 5
SET c.con_closest = h.confirm_time, c.con_count =  IFNULL(c.con_count,0) + 1, c.con_sum = IFNULL(c.con_sum,0) + h.actual_amount
```

**6、统计分析**

各自整理。

