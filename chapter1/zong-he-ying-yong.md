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

```sql
-- ----------------------------
-- Table structure for t_base_customer
-- ----------------------------
DROP TABLE IF EXISTS `t_base_customer`;
CREATE TABLE `t_base_customer` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `sex` int(11) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `tel` varchar(255) DEFAULT NULL,
  `wechat` varchar(255) DEFAULT NULL,
  `address` varchar(255) DEFAULT NULL,
  `birthday` date DEFAULT NULL,
  `profession` varchar(255) DEFAULT NULL,
  `image` varchar(255) DEFAULT NULL,
  `vip_code` varchar(255) DEFAULT NULL,
  `is_vip` int(255) DEFAULT NULL,
  `favorite` varchar(255) DEFAULT NULL,
  `dislike` varchar(255) DEFAULT NULL,
  `con_count` int(11) DEFAULT NULL,
  `con_able` varchar(255) DEFAULT NULL,
  `con_time` time DEFAULT NULL,
  `con_closest` datetime DEFAULT NULL,
  `con_sum` decimal(10,2) DEFAULT NULL,
  `con_style` varchar(255) DEFAULT NULL,
  `have_car` int(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8 COMMENT='会员表';

-- ----------------------------
-- Table structure for t_base_employee
-- ----------------------------
DROP TABLE IF EXISTS `t_base_employee`;
CREATE TABLE `t_base_employee` (
  `id` int(11) NOT NULL,
  `restaurant_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `position_id` int(11) DEFAULT NULL,
  `tel` varchar(255) DEFAULT NULL,
  `sex` varchar(255) DEFAULT NULL,
  `address` varchar(255) DEFAULT NULL,
  `id_number` varchar(255) DEFAULT NULL,
  `id_image` varchar(255) DEFAULT NULL,
  `entry_time` date DEFAULT NULL,
  `marry` varchar(255) DEFAULT NULL,
  `wechat` varchar(255) DEFAULT NULL,
  `email` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_employee_restaurant` (`restaurant_id`),
  KEY `FK_fk_employee_type` (`position_id`),
  CONSTRAINT `FK_fk_employee_restaurant` FOREIGN KEY (`restaurant_id`) REFERENCES `t_base_restaurant` (`id`),
  CONSTRAINT `FK_fk_employee_type` FOREIGN KEY (`position_id`) REFERENCES `t_base_position_type` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_menu
-- ----------------------------
DROP TABLE IF EXISTS `t_base_menu`;
CREATE TABLE `t_base_menu` (
  `id` int(11) NOT NULL,
  `type_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `standard_price` decimal(10,2) DEFAULT NULL,
  `specification` varchar(255) DEFAULT NULL,
  `special` varchar(255) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  `praise` varchar(255) DEFAULT NULL,
  `image` varchar(255) DEFAULT NULL,
  `restaurant_id` int(11) DEFAULT NULL,
  `window_id` int(11) DEFAULT NULL,
  `cost` decimal(10,2) DEFAULT NULL,
  `finish_time` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_menue_restaurant` (`restaurant_id`),
  KEY `FK_fk_menue_type` (`type_id`),
  KEY `FK_fk_menue_window` (`window_id`),
  CONSTRAINT `FK_fk_menue_restaurant` FOREIGN KEY (`restaurant_id`) REFERENCES `t_base_restaurant` (`id`),
  CONSTRAINT `FK_fk_menue_type` FOREIGN KEY (`type_id`) REFERENCES `t_base_menu_type` (`id`),
  CONSTRAINT `FK_fk_menue_window` FOREIGN KEY (`window_id`) REFERENCES `t_base_window` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_menu_stand
-- ----------------------------
DROP TABLE IF EXISTS `t_base_menu_stand`;
CREATE TABLE `t_base_menu_stand` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `specification` varchar(255) DEFAULT NULL,
  `specification_price` decimal(10,2) DEFAULT NULL,
  `specification_cost` decimal(10,2) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  `menu_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_STAND_MENU` (`menu_id`),
  CONSTRAINT `FK_STAND_MENU` FOREIGN KEY (`menu_id`) REFERENCES `t_base_menu` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=9 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_menu_type
-- ----------------------------
DROP TABLE IF EXISTS `t_base_menu_type`;
CREATE TABLE `t_base_menu_type` (
  `id` int(11) NOT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_position_type
-- ----------------------------
DROP TABLE IF EXISTS `t_base_position_type`;
CREATE TABLE `t_base_position_type` (
  `id` int(11) NOT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `salary` decimal(10,2) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_restaurant
-- ----------------------------
DROP TABLE IF EXISTS `t_base_restaurant`;
CREATE TABLE `t_base_restaurant` (
  `id` int(11) NOT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `address` varchar(255) DEFAULT NULL,
  `scale` varchar(255) DEFAULT NULL,
  `tel` varchar(255) DEFAULT NULL,
  `type` varchar(255) DEFAULT NULL,
  `manager_id` int(11) DEFAULT NULL,
  `m_tel` varchar(255) DEFAULT NULL,
  `legal_per` varchar(255) DEFAULT NULL,
  `license_code` varchar(255) DEFAULT NULL,
  `open_time` time DEFAULT NULL,
  `avg_customer` int(11) DEFAULT NULL,
  `official_account` varchar(255) DEFAULT NULL,
  `avg_day_turnover` decimal(10,2) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  `table_turnover_rate` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_restaurant_employee` (`manager_id`),
  CONSTRAINT `FK_fk_restaurant_employee` FOREIGN KEY (`manager_id`) REFERENCES `t_base_employee` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_table
-- ----------------------------
DROP TABLE IF EXISTS `t_base_table`;
CREATE TABLE `t_base_table` (
  `id` int(11) NOT NULL,
  `restaurant_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `people_num` int(11) DEFAULT NULL,
  `position` varchar(255) DEFAULT NULL,
  `kind` varchar(255) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_table_restaurant` (`restaurant_id`),
  CONSTRAINT `FK_fk_table_restaurant` FOREIGN KEY (`restaurant_id`) REFERENCES `t_base_restaurant` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_base_window
-- ----------------------------
DROP TABLE IF EXISTS `t_base_window`;
CREATE TABLE `t_base_window` (
  `id` int(11) NOT NULL,
  `restaurant_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `machine_code` varchar(255) DEFAULT NULL,
  `manager_id` int(11) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_window_employee` (`manager_id`),
  CONSTRAINT `FK_fk_window_employee` FOREIGN KEY (`manager_id`) REFERENCES `t_base_employee` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_busi_order_detail
-- ----------------------------
DROP TABLE IF EXISTS `t_busi_order_detail`;
CREATE TABLE `t_busi_order_detail` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `order_head_id` int(11) DEFAULT NULL,
  `menu_id` int(11) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `fode_code_id` int(11) DEFAULT NULL,
  `cost` decimal(10,2) DEFAULT NULL,
  `price` decimal(10,2) DEFAULT NULL,
  `amount` int(11) DEFAULT NULL,
  `specification` varchar(255) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_detail_fode_code` (`fode_code_id`),
  KEY `FK_fk_detail_head` (`order_head_id`),
  KEY `FK_fk_detail_menue` (`menu_id`),
  CONSTRAINT `FK_DETAIL_MENU` FOREIGN KEY (`menu_id`) REFERENCES `t_base_menu` (`id`),
  CONSTRAINT `FK_fk_detail_fode_code` FOREIGN KEY (`fode_code_id`) REFERENCES `t_base_menu_stand` (`id`),
  CONSTRAINT `FK_fk_detail_head` FOREIGN KEY (`order_head_id`) REFERENCES `t_busi_order_head` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=21 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_busi_order_head
-- ----------------------------
DROP TABLE IF EXISTS `t_busi_order_head`;
CREATE TABLE `t_busi_order_head` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `restaurant_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `member` varchar(255) DEFAULT NULL,
  `reservation_code` varchar(255) DEFAULT NULL,
  `reservation_tel` varchar(255) DEFAULT NULL,
  `reservation_name` varchar(255) DEFAULT NULL,
  `reservation_num` int(11) DEFAULT NULL,
  `reservation_comment` varchar(255) DEFAULT NULL,
  `table_id` int(11) DEFAULT NULL,
  `amount` int(11) DEFAULT NULL,
  `enter_time` datetime DEFAULT NULL,
  `confirm_time` datetime DEFAULT NULL,
  `check_out_time` datetime DEFAULT NULL,
  `employee_id` int(11) DEFAULT NULL,
  `customer_id` int(11) DEFAULT NULL,
  `total` decimal(10,2) DEFAULT NULL,
  `discount` decimal(10,2) DEFAULT NULL,
  `actual_amount` decimal(10,2) DEFAULT NULL,
  `pay_type` varchar(255) DEFAULT NULL,
  `comment` varchar(255) DEFAULT NULL,
  `state` int(11) DEFAULT NULL,
  `cashier_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_order_customer` (`customer_id`) USING BTREE,
  KEY `FK_fk_order_employee` (`employee_id`) USING BTREE,
  KEY `FK_fk_order_restaurant` (`restaurant_id`) USING BTREE,
  KEY `FK_fk_order_table` (`table_id`) USING BTREE,
  CONSTRAINT `FK_fk_order_customer` FOREIGN KEY (`customer_id`) REFERENCES `t_base_customer` (`id`),
  CONSTRAINT `FK_fk_order_employee` FOREIGN KEY (`employee_id`) REFERENCES `t_base_employee` (`id`),
  CONSTRAINT `FK_fk_order_restaurant` FOREIGN KEY (`restaurant_id`) REFERENCES `t_base_restaurant` (`id`),
  CONSTRAINT `FK_fk_order_table` FOREIGN KEY (`table_id`) REFERENCES `t_base_table` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_busi_window_detail
-- ----------------------------
DROP TABLE IF EXISTS `t_busi_window_detail`;
CREATE TABLE `t_busi_window_detail` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `p_id` int(11) DEFAULT NULL,
  `order_detail_id` int(11) DEFAULT NULL,
  `finish_time` datetime DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_windowdetail_detail` (`order_detail_id`),
  KEY `FK_fk_windowdetail_windoworder` (`p_id`),
  CONSTRAINT `FK_P_ID` FOREIGN KEY (`p_id`) REFERENCES `t_busi_window_order_head` (`id`),
  CONSTRAINT `FK_fk_windowdetail_detail` FOREIGN KEY (`order_detail_id`) REFERENCES `t_busi_order_detail` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=40 DEFAULT CHARSET=utf8;

-- ----------------------------
-- Table structure for t_busi_window_order_head
-- ----------------------------
DROP TABLE IF EXISTS `t_busi_window_order_head`;
CREATE TABLE `t_busi_window_order_head` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `order_head_id` int(11) DEFAULT NULL,
  `code` varchar(255) DEFAULT NULL,
  `window_id` int(11) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  `amount` int(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `FK_fk_windoworder_order_` (`order_head_id`),
  CONSTRAINT `FK_fk_windoworder_order_` FOREIGN KEY (`order_head_id`) REFERENCES `t_busi_order_head` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8;
```

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

