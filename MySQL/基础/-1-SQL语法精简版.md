**1、查看所有的数据库**

```sql
show databases;
```

**2、创建自己的数据库**

```sql
create database 数据库名;

#创建 atguigudb 数据库，该名称不能与已经存在的数据库重名。
create database atguigudb;
```

**3、使用自己的数据库**

```sql
use 数据库名;

#使用atguigudb数据库
use atguigudb;
```

说明：如果没有使用use语句，后面针对数据库的操作也没有加“数据名”的限定，那么会报“ERROR 1046(3D000): No database selected”（没有选择数据库）

使用完 use 语句之后，如果接下来的 SQL 都是针对一个数据库操作的，那就不用重复 use 了，如果要针对另一个数据库操作，那么要重新 use。

**4、查看某个库的所有表格**

```sql
show tables;  #要求前面有use语句

show tables from 数据库名;
```

**5、创建新的表格**

```sql
create table 表名称(
    字段名 数据类型,
    字段名 数据类型
);
```

说明：如果是最后一个字段，后面就不用加逗号，因为逗号的作用是分割每个字段。

```sql
#创建学生表
create table student(
	id int,
	name varchar(20)  #说名字最长不超过20个字符
);
```

**6、查看一个表的数据**

```sql
select * from 数据库表名称;
```

```sql
#查看学生表的数据
select * from student;
```

**7、添加一条记录**

```sql
insert into 表名称 values(值列表);

#添加两条记录到student表中
insert into student values(1,'张三');
insert into student values(2,'李四');
```

报错：

```sql
mysql\> insert into student values(1,'张三');

ERROR 1366 (HY000): Incorrect string value: '\xD5\xC5\xC8\xFD' for column 'name' at row 1

mysql\> insert into student values(2,'李四');

ERROR 1366 (HY000): Incorrect string value: '\xC0\xEE\xCB\xC4' for column 'name' at row 1

mysql\> show create table student;
```

字符集的问题。

**8、查看表的创建信息**

```sql
show create table 表名称\G

#查看student表的详细创建信息
show create table student\G
```

```sql
#结果如下
*************************** 1. row ***************************
   Table: student
Create Table: CREATE TABLE `student` (
 `id` int(11) DEFAULT NULL,
 `name` varchar(20) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1
1 row in set (0.00 sec)
```

上面的结果显示student的表格的默认字符集是“latin1”不支持中文。

**9、查看数据库的创建信息**

```sql
show create database 数据库名\G

#查看 atguigudb 数据库的详细创建信息
show create database atguigudb\G
```

```sql
#结果如下
*************************** 1. row ***************************
   Database: atguigudb
Create Database: CREATE DATABASE `atguigudb` /*!40100 DEFAULT CHARACTER SET latin1 */
1 row in set (0.00 sec)
```

上面的结果显示 atguigudb 数据库也不支持中文，字符集默认是latin1。

**10、删除表格**

```sql
drop table 表名称;
```

```sql
#删除学生表
drop table student;
```

**11、删除数据库**

```sql
drop database 数据库名;
```

```sql
#删除atguigudb数据库
drop database atguigudb;
```

