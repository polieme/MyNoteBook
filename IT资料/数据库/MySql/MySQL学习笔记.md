## MySQL 插入数据
MySQL使用INSERT INTO 语句插入数据
### 语法
```sql
INSERT INTO table_name (filed1, field2, field3) VALUES (value1, value2, value3);
```
例子：
```sql
INSERT INTO tt_area (id, name, pid) VALUES ('1', '北京', '0');
```

## MySQL 查询数据
```sql
SELECT * FROM TABLE LIMIT 10; #查询前10条数据
SELECT * FROM TABLE LIMIT 5,10;#查询6-15条数据，第一个参数是从那条数据开始，第二个参数是指查询多少条
SELECT * FROM tt_users A ORDER BY reg_time DESC,reco_name ASC #按照多个字段进行排序，DESC是倒序，ASC是正序，其中
```

## MySQL Update更新数据
```SQL
/*通过查询一个表里面的数据更新另一个表中的数据*/
UPDATE tableA,
 tableB
SET tableA.columnA = tableB.columnB
WHERE
	tableA.clumnC = tableB.columnD
```





## 数据库层面的操作

* 常规的update
```sql
mysql -u root -p password #登录mysql数据库
use database name #使用哪个数据库实例
drop database #删除某个数据库实例
mysqldump -u root -p database_name> /usr/data/mysqldata_bak_20171110.db #数据泵导出
mysqldump -u root -p database_name< /usr/data/mysqldata_bak_20171011.db #数据泵导入

```

* 非常规update(通过子查询更新主表，子查询中牵扯GROUP BY 和 查询条件)
  首先在数据库创建表，并插入数据，具体的sql如下：
```sql
DROP TABLE IF EXISTS `demo_value`;
CREATE TABLE `demo_value` (
  `id` int(5) NOT NULL,
  `user_id` int(5) DEFAULT NULL,
  `value` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of demo_value
-- ----------------------------
INSERT INTO `demo_value` VALUES ('1', '1', '20');
INSERT INTO `demo_value` VALUES ('2', '1', '30');
INSERT INTO `demo_value` VALUES ('3', '1', '20');
INSERT INTO `demo_value` VALUES ('4', '1', '20');
INSERT INTO `demo_value` VALUES ('5', '2', '30');
INSERT INTO `demo_value` VALUES ('6', '2', '20');
INSERT INTO `demo_value` VALUES ('7', '2', '20');
INSERT INTO `demo_value` VALUES ('8', '3', '20');
INSERT INTO `demo_value` VALUES ('9', '4', '20');
INSERT INTO `demo_value` VALUES ('10', '4', '30');
INSERT INTO `demo_value` VALUES ('11', '5', '40');
INSERT INTO `demo_value` VALUES ('12', '6', '20');

DROP TABLE IF EXISTS `demo_value`;
CREATE TABLE `demo_value` (
  `id` int(5) NOT NULL,
  `user_id` int(5) DEFAULT NULL,
  `value` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

-- ----------------------------
-- Records of demo_value
-- ----------------------------
INSERT INTO `demo_value` VALUES ('1', '1', '20');
INSERT INTO `demo_value` VALUES ('2', '1', '30');
INSERT INTO `demo_value` VALUES ('3', '1', '20');
INSERT INTO `demo_value` VALUES ('4', '1', '20');
INSERT INTO `demo_value` VALUES ('5', '2', '30');
INSERT INTO `demo_value` VALUES ('6', '2', '20');
INSERT INTO `demo_value` VALUES ('7', '2', '20');
INSERT INTO `demo_value` VALUES ('8', '3', '20');
INSERT INTO `demo_value` VALUES ('9', '4', '20');
INSERT INTO `demo_value` VALUES ('10', '4', '30');
INSERT INTO `demo_value` VALUES ('11', '5', '40');
INSERT INTO `demo_value` VALUES ('12', '6', '20');
```

```sql
UPDATE demo_name
SET sum_value = (
	SELECT
		SUM(`value`)
	FROM
		demo_value
	WHERE
		demo_value.user_id = demo_name.id
	GROUP BY
		user_id
)
```


## 其他
- 在Navicat中，Ctrl+Q是创建一个查询界面
- MySQL底层实现是从右往左进行解析执行，因此把