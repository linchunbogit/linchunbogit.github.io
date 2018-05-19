---
layout:     post
title:      "mysql-基础"
subtitle:   " "
date:       2018-05-09 11:10:00
author:     "Popo"
header-img: "img/bg/bg_xingkong5.jpg"
tags:
    - 数据库
---

### 概述
#### SHOW STATUS说明
```
Aborted_clients 由于客户没有正确关闭连接已经死掉，已经放弃的连接数量。
Aborted_connects 尝试已经失败的MySQL服务器的连接的次数。
Connections 试图连接MySQL服务器的次数。
Created_tmp_tables 当执行语句时，已经被创造了的隐含临时表的数量。
Delayed_insert_threads 正在使用的延迟插入处理器线程的数量。
Delayed_writes 用INSERT DELAYED写入的行数。
Delayed_errors 用INSERT DELAYED写入的发生某些错误(可能重复键值)的行数。
Flush_commands 执行FLUSH命令的次数。
Handler_delete 请求从一张表中删除行的次数。
Handler_read_first 请求读入表中第一行的次数。
Handler_read_key 请求数字基于键读行。
Handler_read_next 请求读入基于一个键的一行的次数。
Handler_read_rnd 请求读入基于一个固定位置的一行的次数。
Handler_update 请求更新表中一行的次数。
Handler_write 请求向表中插入一行的次数。
Key_blocks_used 用于关键字缓存的块的数量。
Key_read_requests 请求从缓存读入一个键值的次数。
Key_reads 从磁盘物理读入一个键值的次数。
Key_write_requests 请求将一个关键字块写入缓存次数。
Key_writes 将一个键值块物理写入磁盘的次数。
Max_used_connections 同时使用的连接的最大数目。
Not_flushed_key_blocks 在键缓存中已经改变但是还没被清空到磁盘上的键块。
Not_flushed_delayed_rows 在INSERT DELAY队列中等待写入的行的数量。
Open_tables 打开表的数量。
Open_files 打开文件的数量。
Open_streams 打开流的数量(主要用于日志记载）
Opened_tables 已经打开的表的数量。
Questions 发往服务器的查询的数量。
Slow_queries 要花超过long_query_time时间的查询数量。
Threads_connected 当前打开的连接的数量。
Threads_running 不在睡眠的线程数量。
Uptime 服务器工作了多少秒。
```

#### My.ini配置 虚拟内存
```
innodb_buffer_pool_size=576M ->128M InnoDB引擎缓冲区
query_cache_size=100M ->32 查询缓存
tmp_table_size=102M ->32M 临时表大小
key_buffer_size=16m ->8M
```

#### mysql权限大全
|权限|描述|
|--|--|
|ALL PRIVILEGES|影响除WITH GRANT OPTION之外的所有权限|
|ALTER|影响ALTER TABLE命令的使用|
|ALTER ROUTINE|影响创建存储例程的能力|
|CREATE|影响CREATE TABLE命令的使用|
|CREATE ROUTINE|影响更改和弃用存储例程的能力|
|CREATE TEMPORARY TABLES|影响CREATE TEMPORARY TABLE命令的使用|
|CREATE USER|影响创建、弃用；重命名和撤销用户权限的能力|
|CREATE VIEW|影响CREATE VIEW命令的使用|
|DELETE|影响DELETE命令的使用|
|DROP|影响DROP TABLE命令的使用|
|EXECUTE|影响用户运行存储过程的能力|
|EVENT|影响执行事件的能力（从MySQL5.1.6开始）|
|FILE|影响SELECT INTO OUTFILE和LOAD DATA INFILE的使用|
|GRANT OPTION|影响用户委派权限的能力|
|INDEX|影响CREATE INDEX和DROP INDEX命令的使用|
|INSERT|影响INSERT命令的使用|
|LOCK TABLES|影响LOCK TABLES命令的使用|
|PROCESS|影响SHOW PROCESSLIST命令的使用|
|REFERENCES|未来MySQL特性的占位符|
|RELOAD|影响FLUSH命令集的使用|
|REPLICATION CLIENT|影响用户查询从服务器和主服务器位置的能力|
|REPLICATION SLAVE|复制从服务器所需的权限|
|SELECT|影响SELECT命令的使用|
|SHOW DATABASES|影响SHOW DATABASES命令的使用|
|SHOW VIEW|影响SHOW CREATE VIEW命令的使用|
|SHUTDOWN|影响SHUTDOWN命令的使用|
|SUPER|影响管理员级命令的使用，如CHANGE、MASTER、KILL thread、mysqladmindebug、PURGE MASTER LOGS和SET GLOBAL|
|TRIGGER|影响执行触发器的能力（从MySQL5.1.6开始）|
|UPDATE|影响UPDATE命令的使用|
|USAGE|只连接，不授予权限|

### 命令
#### 注意
window环境需要cd到 mysql.exe目录或者配置环境变量

#### 连接mysql

* **本地连接**

```
// mysql -u 用户名 -p(密码不需要填，回车后会要求输入密码)
mysql -u root -p
```

* **远程连接**

```
// mysql -h地址 -u 用户 -p
mysql -h112.74.171.53 -u root -p
```

#### 基本操作
* **查看数据库版本**

```
SELECT DATABASE();
```

* **显示当前时间**

```
SELECT NOW();
```

* **显示当前年月日**

```
SELECT DAYOFMONTH(CURRENT_DATE);
SELECT MONTH(CURRENT_DATE);
SELECT YEAR(CURRENT_DATE);
```

* **计算器**

```
// SELECT 算术
SELECT 1+1;
```


#### 数据库操作
* **连接数据库**

```
// USE 数据库名
// 例子：连接TEST数据库
USE TEST;
```

* **查看所有的数据库**

```
SHOW DATABASES;
```

* **查看当前连接的数据库**

```
SELECT DATABASE();
```

#### 表操作
* **查看所有表**

```
SHOW TABLES;
```

* **创建表**

```
// CREATE TABLE 表名 (字段 字段类型,...)
// 例子：创建TEST_TABLE
CREATE TABLE TEST_TABLE(
  id int(4) not null primary key auto_increment,
  name char(20) not null,
  sex int(4) not null default '0',
  degree double(16,2));
```

* **查看表结构**

```
// DESC 表名
// 例子：查看test_table的表结构
DESC test_table;
```

* **删除表**

```
// DROP TABLE 表名
// 例子：删除TEST_TABLE
DROP TABLE TEST_TABLE;
```

* **表插入数据**

```
// INSERT INTO 表名 [(字段名,...)] VALUES （值,...）
// 例子：像TEST1插入全部数据
INSERT INTO test_table VALUES(3, 'Tom', 1, 96.45);
// 例子：向test_table表插入名字
INSERT INTO test_table(name) VALUES('Tom');
```

* **删除表数据**

```
// DELETE FROM 表名 WHERE 表达式
// 例子：删除test_table表id为3的数据
DELETE FROM test_table WHERE id=3;
```

* **查询表数据**

```
// SELECT 字段,.. FROM 表名 WHERE 表达式
// 例子：查看test_table数据
SELECT * FROM test_table;
```

* **更新表数据**

```
// UPDATE 表名 set 字段=新值, ... WHERE 条件
// 例子：更新test_table表id为1的名字
UPDATE test_table SET name="Join" WHERE id=1;
```

* **处理表字段**

```
// 加字段：ALTER TABLE 表名 ADD 字段 类型 其他
// 例子：给test_table加一列age，类型是int(4)，默认值是0
ALTER TABLE test_table ADD age int(4) default '0';

// 加索引：ALTER TABLE 表名 ADD INDEX 索引名 (字段名,....)
// 例子：
ALTER TABLE test_table ADD INDEX Tindex(age);

// 加关键字：ALTER TABLE 表名 ADD PRIMARY KEY (字段名)
// 例子:
ALTER TABLE test_table add PRIMARY KEY (id);

// 移除自增关键字：ALTER TABLE 表名 MODIFY 字段名称 字段类型 DROP PRIMARY KEY
// 例子：
ALTER TABLE test_table MODIFY id int, DROP PRIMARY KEY;

// 移除非自增关键字：ALTER TABLE 表名 DROP PRIMAY KEY；
// 例子：
ALTER TABLE test_table DROP PRIMAY KEY;

// 加唯一限制条件的索引：ALTER TABLE 表名 ADD UNIQUE 索引名 (字段名)
// 例子：
ALTER TABLE test_table ADD UNIQUE Tindex(age);

// 删除某个索引：ALTER TABLE 表名 DROP INDEX 索引名
// 例子：
ALTER TABLE test_table DROP INDEX Tindex;

// 修改原字段名称及类型：ALTER TABLE 表名 CHANGE 旧字段名称 新字段名称 新字段类型
// 例子：
ALTER TABLE test_table CHANGE name cname char(22);

// 删除字段：ALTER TABLE 表名 DROP 字段名
// 例子：
ALTER TABLE test_table DROP age;
```

* **修改表名**

```
// RENAME TABLE 旧表名 TO 新表名
// 例子：
RENAME TABLE test_table TO test_table2;
```

#### 用户操作

* **添加新用户**

```
// CREATE USER '用户名'@'地址' IDENTIFIED BY '密码'
// 例子：创建只可以在本地登录的TEST1,密码为123456
CREATE USER 'TEST1'@'localhost' IDENTIFIED BY '123456';
// 例子：创建只可以在192.168.1.101登录的TEST2,密码为123456
CREATE USER 'TEST2'@'192.168.1.101' IDENTIFIED BY '123456';
// 例子：创建可以在任何地方登录且没密码的TEST3
CREATE USER 'TEST3'@'%' IDENTIFIED BY '123456';
```

* **删除用户**

```
// DROP USER '用户名'@'地址'
// 例子：删除TEST1用户
DROP USER 'TEST1'@'localhost';
```

* **修改密码**

```
// SET PASSWORD FOR '用户名'@'地址' = PASSWORD('新密码')
// 修改TEST1的密码为654321
SET PASSWORD FOR 'TEST1'@'localhost' = PASSWORD('654321');
// 修改当前登录用户TEST1密码为123456
SET PASSWORD = PASSWORD('123456');

// MYSQLADMIN -u root [-p旧密码] PASSWORD 新密码 (没有旧密码可以不写-p)，注：不是所有版本都有效？
mysqladmin -u root password '654321';
mysqladmin -u root password '654321' "123456";
```

* **查看用户权限**

```
// 查看当前用户权限
SHOW GRANTS;
// 查看指定用户的权限
// SHOW GRANTS FOR 用户@地址;
// 例如：查看TEST1权限
SHOW GRANTS FOR TEST1@localhost;
```

* **用户授权**

```
// GRANT 权限,.. ON 数据库.表 TO '用户名'@'登录主机'
// 例子1：给TEST1授予select和insert的所有表的权限
GRANT SELECT,INSERT ON *.* TO 'TEST1'@'localhost';
// 例子2：给TEST1授予操作所有数据库表的所有任意权限，但不包括授权权限
GRANT ALL ON *.* TO 'TEST1'@'localhost';
// 例子3：给TEST1授予操作所有数据库表的所有任意权限，包括授权权限
GRANT ALL ON *.* TO 'TEST1'@'localhost' WITH GRANT OPTION;

// 更新授权表
FLUSH PRIVILEGES;
```

* **撤销用户权限**

```
// REVOKE 权限,... ON 数据库.表 FROM '用户名'@'登录主机'
// 例子1：撤销TEST1的select权限
REVOKE SELECT ON *.* FROM 'TEST1'@'localhost';
// 例子2：撤销TEST1的授权权限
REVOKE GRANT OPTION ON *.* FROM 'TEST1'@'localhost';

// 更新授权表
FLUSH PRIVILEGES;
```

* **当前用户信息**

```
// 查看当前用户
SELECT USER();
// 查看当前用户详情
STATUS;
```

* **查看mysql所有用户**

```
// user表在mysql数据库里面，使用mysql表
USE MYSQL;
// 查询和显示
SELECT HOST, USER FROM USER;
```

#### 数据库信息
```
// 查看当前数据库的连接数，其他变量的查看类似
SHOW STATUS LIKE 'Thread%';
// 查看当前数据库的最大连接数(可以在/etc/my.cnf里面设置 max_connections = 1000)
SHOW VARIABLES LIKE '%max_connections%';
// 设置数据库的最大连接数，其他变量的设置类似
SET GLOBAL max_connections=200;
```


















