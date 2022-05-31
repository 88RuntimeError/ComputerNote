# 一、基础篇
## 1. MySQL启动与连接

### 1.1 MySQL启动
| 操作                                      | 说明            |
| ----------------------------------------- | --------------- |
| net start mysql80                         | 启动MySQL服务   |
| mysql [-h127.0.0.1] [-p3306] -uroot-proot | 登录MySQL服务器 |
| mysql -u root -p                          | 登录MySQL服务器 |
| net stop mysql80                          | 关闭MySQL服务   |

### 1.2 MySQL客户端连接Navicate

- 修改密码编码方式(Windows)

  - 执行命令

    ```mysql
    use mysql
    select user,host from user;
    ```

  - 找到用户名和host

    ```mysql
    alter user 'root'@'localhost' identified by 'root' password expire never;
    
    alter user 'root'@'localhost' identified with mysql_native_password by 'root';
    
    # root是user localhost是host
    ```




## 2. SQL
### 2.1 SQL基础语法
>1.SQL语句可以单行或多行书写，以分号结尾。
>2.SQL语句可以使用空格/缩进来增强语句的可读性
>3.MySQL数据库的SQL语句不区分大小写，关键字建议使用大写
>4.注释：
>
>- 单行注释：- - 注释内容 或 # 注释内容(MySQL特有)
>- 多行注释：/* 注释内容 */
- **SQL分类**

| 分类 | 全称                       | 说明                                                   |
| ---- | -------------------------- | ------------------------------------------------------ |
| DDL  | Data Definition Language   | 数据定义语言，用来定义数据库对象(数据库，表，字段)     |
| DML  | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改         |
| DQL  | Data Query Language        | 数据查询语言，同来查询数据库中表的记录                 |
| DCL  | Data Control Language      | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |
- **数值类型**

| 类型         | 大小    | 有符号(SIGNED)范围                                    | 无符号(UNSIGNED)范围                                    |
| ------------ | ------- | ----------------------------------------------------- | ------------------------------------------------------- |
| tinyint      | 1 byte  | (-128, 127)                                           | （0, 255）                                              |
| smallint     | 2 bytes | (-32768, 32767)                                       | (0, 65535)                                              |
| mediumint    | 3 bytes | (-8388608, 8388607)                                   | (0, 16777215)                                           |
| int或integer | 4 bytes | (-2147483648, 2147483647)                             | (0, 4294967295)                                         |
| bigint       | 8 bytes | $$ (-2^{63}, 2^{63}-1) $$                             | $$ (0, 2^{64}-1) $$                                     |
| float        | 4 bytes | (-3.402823466 E+38, 3.402823466351 E+38)              | 0和(1.175494351 E-38, 3.402823466 E+38)                 |
| double       | 8 bytes | (-1.7976931348623157 E+308, 1.7976931348623157 E+308) | 0和(2.2250738585072014 E-308, 1.7976931348623157 E+308) |
| decimal      |         | 依赖于M(精度)和D(标度)的值                            | 依赖于M(精度)和D(标度)的值                              |

- **字符串类型**

| 类型       | 大小               | 描述                         |
| ---------- | ------------------ | ---------------------------- |
| char       | 0-255 bytes        | 定长字符串                   |
| varchar    | 0-65535 bytes      | 变长字符串                   |
| tinyblob   | 0-255 bytes        | 不超过255个字符的二进制数据  |
| tinytext   | 0-255 bytes        | 短文本字符串                 |
| blob       | 0-65535 bytes      | 二进制形式的长文本数据       |
| text       | 0-65535 bytes      | 长文本数据                   |
| mediumblob | 0-16777215 bytes   | 二进制形式的中等长度文本数据 |
| mediumtext | 0-16777215 bytes   | 中等长度文本数据             |
| longblob   | 0-4294967295 bytes | 二进制形式的极大文本数据     |
| longtext   | 0-4294967295 bytes | 极大文本数据                 |

- **日期时间类型**

| 类型      | 大小 | 范围                                       | 格式                | 描述                     |
| --------- | ---- | ------------------------------------------ | ------------------- | ------------------------ |
| date      | 3    | 1000-01-01 至 9999-12-31                   | YYYY-MM-DD          | 日期值                   |
| time      | 3    | -838:59:59 至 838:59:59                    | HH:MM:SS            | 时间值或持续时间         |
| year      | 1    | 1901 至 2155                               | YYYY                | 年份值                   |
| datetime  | 8    | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| timestamp | 4    | 1970-01-01 00:00:00 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |





### 2.2 DDL：数据定义语言

#### 2.2.1 数据库操作

##### 查询

- **查询所有数据库：**`show databases;`
- **查看当前所在数据库：**`select database();`

##### 创建

- **创建数据库：**`create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则];`
- **创建数据库案例：**`creat database test default charset utf8mb4;`

##### 删除

- **删除指定数据库：**`drop database [if exists] 数据库名;`

##### 使用

- **选择指定数据库：**`use 数据库名`

  

#### 2.2.2 表操作

##### 查询

- **查询当前数据库中所有的表：**`show tables;`
- **查询表的结构：**`desc 表名;`
- **查询指定表的建表语句：**`show create table 表名;`

##### 创建

- 语法

```mysql
create table 表名(
    字段1  字段1类型[comment 字段1注释],
    字段2  字段2类型[comment 字段2注释],
    字段3  字段3类型[comment 字段3注释],
    ······
    字段n  字段n类型[comment 字段n注释]
)[comment 表注释];
```

- 举例

```mysql
create table emp(
	id int comment '编号',
    workno varchar(10) comment '工号',
    name varchar(10) comment '姓名',
    gender char(1) comment '性别',
    age tinyint unsigned comment '年龄',
    idcard char(18) comment '身份证号',
    entrydate date comment '入职时间'
) comment '员工信息表';
```

##### 修改

```
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| id        | int              | YES  |     | NULL    |       |
| workno    | varchar(10)      | YES  |     | NULL    |       |
| name      | varchar(10)      | YES  |     | NULL    |       |
| gender    | char(1)          | YES  |     | NULL    |       |
| age       | tinyint unsigned | YES  |     | NULL    |       |
| idcard    | char(18)         | YES  |     | NULL    |       |
| entrydate | date             | YES  |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+
```

- **添加字段：**`alter table 表名 add 字段名 类型(长度) [comment 注释] [约束];`
  - 案例：` alter table emp add nickname varchar(20);`
- **修改数据类型：**`alter table 表名 modify 字段名 新数据类型(长度)`
  - 案例：`alter table emp modify name varchar(20);`
- **修改字段名和字段类型：**`alter table 表名 change 旧字段名 新字段名 类型(长度) [comment 注释] [约束]`
  - 案例：`alter table emp change nickname username varchar(30) comment '用户名';`
- **删除字段：**`alter table 表名 drop 字段名;`
  - 案例：`alter table emp drop entrydate;`
- **修改表名：**`alter table 旧表名 rename to 新表名;`
  - 案例：`alter table emp rename to employee;`

```
+----------+------------------+------+-----+---------+-------+
| Field    | Type             | Null | Key | Default | Extra |
+----------+------------------+------+-----+---------+-------+
| id       | int              | YES  |     | NULL    |       |
| workno   | varchar(10)      | YES  |     | NULL    |       |
| name     | varchar(20)      | YES  |     | NULL    |       |
| gender   | char(1)          | YES  |     | NULL    |       |
| age      | tinyint unsigned | YES  |     | NULL    |       |
| idcard   | char(18)         | YES  |     | NULL    |       |
| username | varchar(30)      | YES  |     | NULL    |       |
+----------+------------------+------+-----+---------+-------+
```

##### 删除

- **删除表：**`drop table [if exists] 表名;`
  - 案例：`drop table if exists emp;`
- **删除指定表，并重新创建该表：**`truncate table 表名;`
  - 案例：`truncate table employee;`



### 2.3 DML：数据操作语言

#### 添加

- **给指定字段添加数据：**

  - **插入一条数据：**`insert into 表名(字段名1, 字段名2, ...) values(值1, 值2, ...);`

    - 案例：![image-20220519162350580](MySQL.assets/image-20220519162350580.png)

    

- **给全部字段添加数据：**

  - **插入一条数据：**`insert into 表名 values(值1, 值2, ...);`

    - 案例：![image-20220519162332859](MySQL.assets/image-20220519162332859.png)

      

- **批量添加数据：**

  - `insert into 表名(字段名1, 字段名2, ...) values(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...);`
    - 案例：![image-20220519163738939](MySQL.assets/image-20220519163738939.png)

  - `insert 表名 values(值1, 值2, ...),(值1, 值2, ...),(值1, 值2, ...);`
    - 案例：![image-20220519162728383](MySQL.assets/image-20220519162728383.png)

  

- **注意：**

  - 插入数据时，指定的字段顺序需要与值的顺序是一一对应的
  - 字符串和日期型数据赢包含在引号中
  - 插入的数据大小，应该在字段的规定范围内

#### 更新

- **修改数据：**`update 表名 set 字段名1=值1, 字段名2=值2, [WHERE 条件];`
  - 案例1：`update employee set name='张三三' where id=1;`
  - 案例2：`update employee set name='小昭', gender='女' where id=2;`
  - 案例3：`update employee set workno='1';`
- **注意：**修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据

#### 删除

- **删除数据：**`delete from 表名 [where 条件];`

  - 案例1：`delete from employee where gender='女';`
  - 案例2：`delete from employee;`

  

- **注意：**
  - delete语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据
  - delete语句不能删除某一个字段的值(可以使用update)

### 2.4 DQL：数据查询语言

#### 2.4.1 基础查询

##### 查询多个字段

- `select 字段1,字段2,字段3,... from 表名;`
  - `selcet id,name,workaddress,age,gender from emp;`
- `select * from 表名;`

##### 设置别名

- `select 字段1 as 别名1, 字段2 as 别名2, ... from 表名;`
  - `select workaddress as '工作地址' from emp;`
  - `select workaddress '工作地址' from emp;`

##### 去除重复记录

- `select distinct 字段列表 from 表名;`
  - `select distinct workaddress '工作地址' from emp;`

#### 2.4.2 条件查询



#### 2.4.3 聚合函数

#### 2.4.4 分组查询

#### 2.4.5 排序查询

#### 2.4.6 分页查询

#### 2.4.7 案例练习



### 2.5 DCL：数据控制语言

## 3.函数
## 4.约束
## 5.多表查询
## 6.事物
# 二、进阶篇
## 1.存储引擎
## 2.索引
## 3.SQL优化
## 4.视图/存储过程/触发器
## 5.锁
## 6.InnoDB核心
## 7.MySQL管理
# 三、运维篇
## 1.日志
## 2.主从复制
## 3.分库分表
## 4.读写分离
