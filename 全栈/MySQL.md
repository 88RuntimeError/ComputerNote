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



# 四、Python与MySQL交互

## 4.1 Python操作MySQL步骤

**在pymysql中提供了Connection和Cursor对象来管理操作MySQL**

![image-20220607112709202](MySQL.assets/image-20220607112709202.png)

### **1. 引入pymysql模块**

```python
from pymysql import *
```



### **2. 构造Connection对象**

代表一个与MySQL Server的socket连接，使用connect方法来创建一个连接实例。

创建对象，调用connect()方法:

```python
conn = connect(参数列表)
```

- 参数host：连接的mysql主机，如果本机是'localhost'
- 参数port：连接的mysql主机的端口，默认是3306
- 参数database(db)：数据库的名称
- 参数user：连接的用户名
- 参数password(passwd)：连接的密码
- 参数charset：通信采用的编码方式，推荐使用utf8

**Connection对象常用的API:**

| API             | 说明                         |
| --------------- | ---------------------------- |
| connect()       | 创建一个数据库连接实例       |
| close()         | 发送一个退出消息，并关闭连接 |
| commit()        | 提交修改至数据库             |
| cursor()        | 创建一个cursor(游标)实例     |
| ping()          | 检测服务器是否在运行         |
| rollback()      | 回滚当前事务                 |
| select_db(db)   | 设置当前db                   |
| show_warnings() | 显示警告信息                 |

### 3. 构造Cursor对象

代表一个与MySQL数据库交互对象，使用Connection.Cursor()在当前socket连接上的交互对象。

游标（Cursor）是处理数据的一种方法，为了查看或者处理结果集中的数据，游标提供了在结果集中一次一行或者多行前进或向后浏览数据的能力。可以把游标当作一个指针，它可以指定结果中的任何位置，然后允许用户对指定位置的数据进行处理
通俗来说就是，操作数据和获取数据库结果都要通过游标来操作。

![image-20220607113024342](MySQL.assets/image-20220607113024342.png)



**Cursor对象常用API：**

| API           | 说明                       |
| ------------- | -------------------------- |
| close()       | 关闭当前cursor             |
| execute()     | 执行一个sql语句            |
| executemany() | 执行批量sql语句            |
| fetchall()    | 取所有数据                 |
| fetchmany()   | 取多条数据，指定取数据条数 |
| fetchone()    | 取一条数据                 |

### 4. Python操作MySQL步骤代码

```python
#1 导入pymysql库
from pymysql import *

#2 创建数据库连接
conn = Connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')

print(conn)

#3 创建游标
cur = conn.cursor()

#4 执行sql语句和数据处理
pass

#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```

- 执行结果

  ![image-20220607113206285](MySQL.assets/image-20220607113206285.png)

  看到以上运行结果，说明Connection对象创建成功，数据库已经连接成功！

## 4.2 sql语句注入

**什么是sql注入**

用户提交带有恶意的数据与SQL语句进行字符串方式的拼接，从而影响了SQL语句的语义，最终产生数据泄露或数据的篡改的现象。



**如何防止sql注入-sql语句参数化**

参数化查询是指在设计与数据库链接并访问数据时，在需要填入数值或数据的地方，使用参数 (Parameter) 来给值，这个方法目前已被视为最有效可预防SQL注入攻击的防御方式。



```python
#1 导入pymysql包
from pymysql import *

#2 创建数据连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')

#3 打开游标
cur = conn.cursor()

#4 执行sql语句和数据处理
sname = input('请输入用户名：')
passwd = input('请输入密码：')
#有sql注入漏洞的sql语句
#sql = "select * from t_student where sname='%s' and passwd='%s'"%(sname,passwd)
#print(sql)
#select * from t_student where sname='test' or 1=1 #' and passwd='dsafdsa'
#为防止sql注入，我们对sql语句进行参数化
sql = "select * from t_student where sname=%s and passwd=%s"
params = (sname,passwd)

rowcount = cur.execute(sql,params)

if rowcount != 0:
    print("登录成功！")
else:
    print("登录失败！")

#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```



## 4.3 增加数据

### 4.3.1 增加单条数据

```python
#1  导入pymsql包
from pymysql import *

#2 创建数据库连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')

#3 打开游标
cur = conn.cursor()

#4 执行 sql语句
#编写sql语句
try:
    sql = "insert into t_student values (%s,%s,%s,%s,%s,%s,%s,%s)"
    params = (7,"肖小军","123456",'男',21,"2020-07-15","大数据班","123456@126.com")
    #执行sql语句
    cur.execute(sql,params)
    conn.commit()
except:
    conn.rollback()

print("数据增加成功!")
#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```

运行结果

![image-20220607113419982](MySQL.assets/image-20220607113419982.png)



### 4.3.2 增加多条数据

```python
#1  导入pymsql包
from pymysql import *

#2 创建数据库连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')

#3 打开游标
cur = conn.cursor()

#4 执行 sql语句
#编写sql语句
try:
    sql = "insert into t_student values (%s,%s,%s,%s,%s,%s,%s,%s)"
    params = [(7,"王辉1","123456",'男',24,"2020-09-15","Python全栈班","123456@126.com"),
              (7, "王辉2", "123456", '男', 24, "2020-09-15", "Python全栈班", "123456@126.com"),
              (7, "王辉3", "123456", '男', 24, "2020-09-15", "Python全栈班", "123456@126.com")
              ]
    #执行sql语句
    cur.executemany(sql,params)
    conn.commit()
except:
    conn.rollback()

print("数据增加成功!")
#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```

运行结果

![image-20220607113512768](MySQL.assets/image-20220607113512768.png)



## 4.4 删除数据

```python
#1  导入pymsql包
from pymysql import *

#2 创建数据库连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')
print(conn)
#3 打开游标
cur = conn.cursor()

#4 执行 sql语句
#编写sql语句
try:
    sql = "delete from t_student where sno=%s"
    params = (7)
    #执行sql语句
    rowcount = cur.execute(sql,params)
    conn.commit()
except:
    conn.rollback()

print("已删除"+str(rowcount)+"条数据!")
#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```

运行结果

![image-20220607113546063](MySQL.assets/image-20220607113546063.png)



## 4.5 修改数据

```python
#1  导入pymsql包
from pymysql import *

#2 创建数据库连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')
print(conn)
#3 打开游标
cur = conn.cursor()

#4 执行 sql语句
#编写sql语句
try:
    # 删除和修改操作一定要限定条件，不然将影响其他数据，甚至误删或修改整个数据库
    sql = "update t_student set sname=%s where sno=%s"
    params = ('李敏',8)
    #执行sql语句
    rowcount = cur.execute(sql,params)
    conn.commit()
except:
    conn.rollback()

print("已修改"+str(rowcount)+"条数据!")
#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```

运行结果

![image-20220607113620572](MySQL.assets/image-20220607113620572.png)



## 4.6 查询数据

```python
#1  导入pymsql包
from pymysql import *

#2 创建数据库连接
conn = connect(host='localhost',port=3306,user='root',password='root',db='mytestdb',charset='utf8')

#3 打开游标
cur = conn.cursor()

#4 执行 sql语句
#编写sql语句
# 查询数据时，为了节约内存，不要用*,而应该指定具体要取的字段，另外要指定查询条件
sql = "select sno,sname,sex,age,classname from t_student where age>%s"
params = (20)
#执行sql语句
cur.execute(sql,params)

# result=cur.fetchone()  #取一条数据
# print(result)

#result=cur.fetchmany(3)  #取指定多条数据
result=cur.fetchall()  #取所有数据
#打印输出执行结果
for row in result:
    print(row)

#5 关闭游标
cur.close()

#6 关闭连接
conn.close()
```



### 4.7 数据库封装操作

观察前面的文件发现，除了sql语句及参数不同，其它语句都是一样的

这样造成了很多重复代码，我们可以把数据库常用操作封装为一个类，以便代码可以重复使用

- **创建MysqlHelper.py文件，定义类**

  ```python
  from pymysql import *
  
  class MysqlHelper(object):
      #数据库连接参数，可以定义多个，比如conn_params1，conn_params2，用于连接多个数据库，在类实例化时指定
      conn_params1 = {'host': 'localhost', 'port': 3306, 'user': 'root', 'passwd': 'root', 'db': 'mytestdb',
                      'charset': 'utf8'}
  
      #类的构造函数，主要用于类的初始化
      def __init__(self, conn_params):
          self.__host = conn_params['host']
          self.__port = conn_params['port']
          self.__db = conn_params['db']
          self.__user = conn_params['user']
          self.__passwd = conn_params['passwd']
          self.__charset = conn_params['charset']
  
      #建立数据库连接和打开游标
      def __connect(self):
          self.__conn = connect(host=self.__host, port=self.__port, db=self.__db, user=self.__user, passwd=self.__passwd,
                              charset=self.__charset)
          self.__cursor = self.__conn.cursor()
  
      #关闭游标和关闭连接
      def __close(self):
          self.__cursor.close()
          self.__conn.close()
  
      #取一条数据
      def get_one(self, sql, params):
          result = None
          try:
              self.__connect()
              self.__cursor.execute(sql, params)
              result = self.__cursor.fetchone()
              self.__close()
          except Exception as e:
              print(e)
          return result
  
      #取所有数据
      def get_all(self, sql, params):
          lst = ()
          try:
              self.__connect()
              self.__cursor.execute(sql, params)
              lst = self.__cursor.fetchall()
              self.__close()
          except Exception as e:
              print(e)
          return lst
  
      #增加数据
      def insert(self, sql, params):
          return self.__edit(sql, params)
  
      #修改数据
      def update(self, sql, params):
          return self.__edit(sql, params)
  
      #删除数据
      def delete(self, sql, params):
          return self.__edit(sql, params)
  
      #写数据操作具体实现，增删改操作都是调用这个方法来实现，这是个私有方法，不允许类外部调用
      def __edit(self, sql, params):
          count = 0
          try:
              self.__connect()
              count = self.__cursor.execute(sql, params)
              self.__conn.commit()
              self.__close()
          except Exception as e:
              print(e)
          return count
  ```

  

- **MysqlHelper类的调用**

  ```python
  from MysqlHelper import *
  
  # 数据库查询
  '''
  mysqlhelper = MysqlHelper(MysqlHelper.conn_params1)
  sql = "select sno,sname,sex,age,classname from t_student where age>%s"
  params = (20)
  result = mysqlhelper.get_all(sql, params)
  
  # 打印输出执行结果
  for row in result:
      print(row)'''
  
  
  #增加数据
  '''
  mysqlhelper = MysqlHelper(MysqlHelper.conn_params1)
  sql = "insert into t_student values (%s,%s,%s,%s,%s,%s,%s,%s)"
  params = (11,"王五","123456",'男',24,"2020-09-15","python全栈班","123456@126.com")
  rowcount = mysqlhelper.insert(sql, params)
  print("已增加"+str(rowcount)+"条数据")'''
  
  
  #删除数据
  '''
  mysqlhelper = MysqlHelper(MysqlHelper.conn_params1)
  sql = "delete from t_student where sno=%s"
  params = (11)
  rowcount = mysqlhelper.delete(sql, params)
  print("已删除"+str(rowcount)+"条数据")'''
  
  #修改数据
  '''
  mysqlhelper = MysqlHelper(MysqlHelper.conn_params1)
  sql = "update t_student set classname=%s where sno=%s"
  params = ('大数据班',9)
  rowcount = mysqlhelper.update(sql, params)
  print("已修改"+str(rowcount)+"条数据")'''
  ```

  
