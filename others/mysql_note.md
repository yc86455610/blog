
   * [MySQL约束](#mysql约束)
      * [主键约束](#主键约束)
      * [自增约束](#自增约束)
      * [唯一约束](#唯一约束)
      * [非空约束](#非空约束)
      * [默认约束](#默认约束)
      * [外键约束](#外键约束)
   * [数据库三大设计范式](#数据库三大设计范式)
      * [第一范式](#第一范式)
      * [第二范式](#第二范式)
      * [第三范式](#第三范式)
   * [MySql查询练习](#mysql查询练习)
      * [1、查询student表的所有记录](#1查询student表的所有记录)
      * [2、查询student表中的所有记录的sname，ssex和class列](#2查询student表中的所有记录的snamessex和class列)
      * [3、查询教师所有单位即不重复的department列](#3查询教师所有单位即不重复的department列)
      * [4、查询score表中成绩在60到80之间的所有记录](#4查询score表中成绩在60到80之间的所有记录)
      * [5、查询score表中成绩为85，86或88的记录](#5查询score表中成绩为8586或88的记录)
      * [6、查询student表中“95031”班或性别为“女”的同学记录](#6查询student表中95031班或性别为女的同学记录)
      * [7、以class降序查询student表中的所有记录](#7以class降序查询student表中的所有记录)
      * [8、以cno升序、degree降序查询score表中的所有记录](#8以cno升序degree降序查询score表中的所有记录)
      * [9、查询“95031”班的学生人数](#9查询95031班的学生人数)
      * [10、查询score表中的最高分的学生学号和课程号（子查询或者排序）](#10查询score表中的最高分的学生学号和课程号子查询或者排序)
      * [11、查询每门课的平均成绩](#11查询每门课的平均成绩)
      * [12、查询score表中至少有2名学生选修的并以3开头的课程的平均分数](#12查询score表中至少有2名学生选修的并以3开头的课程的平均分数)
      * [13、查询分数大于70，小于90的 sno 列](#13查询分数大于70小于90的-sno-列)
      * [14、查询所有学生的 sname，cno 和 degree 列](#14查询所有学生的-snamecno-和-degree-列)
      * [15、查询所有学生的 sno，cname 和 degree 列](#15查询所有学生的-snocname-和-degree-列)
      * [16、查询所有学生的sname， cname， degree 列](#16查询所有学生的sname-cname-degree-列)
      * [17、查询'95031'班学生每门课的平均分](#17查询95031班学生每门课的平均分)
      * [18、查询选修'3-105课程的成绩高于‘109’号同学‘3-105’成绩的所有同学的记录](#18查询选修3-105课程的成绩高于109号同学3-105成绩的所有同学的记录)
      * [19、查询成绩高于学号为‘109’、课程号为‘3-105’的成绩的所有记录](#19查询成绩高于学号为109课程号为3-105的成绩的所有记录)
      * [20、查询和学号为108、101的同学同年出生的所有学生的sno、sname和sbirthday列](#20查询和学号为108101的同学同年出生的所有学生的snosname和sbirthday列)
      * [21、查询“张旭”教师任课的学生成绩](#21查询张旭教师任课的学生成绩)
      * [22、查询选修某课程的同学人数多于5人的教师姓名](#22查询选修某课程的同学人数多于5人的教师姓名)
      * [23、查询95033和95031班全体学生的记录](#23查询95033和95031班全体学生的记录)
      * [24、查询存在有85分以上成绩的课程cno](#24查询存在有85分以上成绩的课程cno)
      * [25、查询出‘计算机系’教师所教课程的成绩表](#25查询出计算机系教师所教课程的成绩表)
      * [26、查询‘计算机系’和‘电子工程系’不同职称的教师的tname和prof](#26查询计算机系和电子工程系不同职称的教师的tname和prof)
      * [27、查询选修编号为‘3-105’课程且成绩至少高于选修编号为‘3-245’的同学的cno，sno和degree，并按degree从高到低次序排列](#27查询选修编号为3-105课程且成绩至少高于选修编号为3-245的同学的cnosno和degree并按degree从高到低次序排列)

# MySQL约束

## 主键约束
他能够唯一确定一直表中的一条记录。也就是通过给某个字段添加约束，就可以使得该字段不重复且不为空。

```sql

create table user (
    id int primary key,
    name varchar(20)
);

insert into user values(1, '张三');

mysql> insert into user values(1, '张三');
ERROR 1062 (23000): Duplicate entry '1' for key 'PRIMARY'


insert into user values(2, '张三');


mysql> select * from user;
+----+--------+
| id | name   |
+----+--------+
|  1 | 张三   |
|  2 | 张三   |
+----+--------+
2 rows in set (0.01 sec)


insert into user values(null, '张三');

mysql> insert into user values(null, '张三');
ERROR 1048 (23000): Column 'id' cannot be null

# 不能重复也不能为空



# 联合主键,只要加起来不重复就可以
create table user2(
    id int,
    name varchar(20),
    passwd varchar(20),
    primary key(id, name)
);


insert into user2 values(1, '张三', 123);
insert into user2 values(2, '张三', 123);
insert into user2 values(2, '李四', 123);


mysql> select * from user2;
+----+--------+--------+
| id | name   | passwd |
+----+--------+--------+
|  1 | 张三   | 123    |
|  2 | 张三   | 123    |
|  2 | 李四   | 123    |
+----+--------+--------+
3 rows in set (0.00 sec)

insert into user2 values(null, '张三', 123);

mysql> insert into user2 values(null, '张三', 123);
ERROR 1048 (23000): Column 'id' cannot be null

# 联合主键任意一个都不能为空

```

## 自增约束

```sql
create table user3(
    id int key auto_increment,
    name varchar(20)
);

insert into user3 (name) values('张三');

mysql> select * from user3;
+----+--------+
| id | name   |
+----+--------+
|  1 | 张三   |
+----+--------+
1 row in set (0.00 sec)

mysql> insert into user3 (name) values('张三');
Query OK, 1 row affected (0.01 sec)

mysql> select * from user3;
+----+--------+
| id | name   |
+----+--------+
|  1 | 张三   |
|  2 | 张三   |
+----+--------+
2 rows in set (0.00 sec)


# 如果创建表的时候，忘记创建主键约束了，该怎么办？

create table user4(
    id int, 
    name varchar(20)
);

# 修改表结构，添加主键约束
alter table user4 add primary key(id);

mysql> desc user4;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

# 删除？
alter table user4 drop primary key;

mysql> alter table user4 drop primary key;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc user4;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)


# 使用modify修改字段来添加主键
alter table user4 modify id int primary key;

mysql> alter table user4 modify id int primary key;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc user4;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)


```

## 唯一约束

约束修饰的字段的值不可以重复

```
create table user5(
    id int, 
    name varchar(20)
);

alter table user5 add unique(name);

mysql> desc user5;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.01 sec)

insert into user5 value(1, '张三');
insert into user5 value(1, '张三');

mysql> insert into user5 value(1, '张三');
Query OK, 1 row affected (0.00 sec)

mysql> insert into user5 value(1, '张三');
ERROR 1062 (23000): Duplicate entry '张三' for key 'name'

mysql> select * from user5;
+------+--------+
| id   | name   |
+------+--------+
|    1 | 张三   |
|    1 | 李四   |
+------+--------+
2 rows in set (0.00 sec)

create table user6(
    id int, 
    name varchar(20),
    unique(name)
);



create table user7(
    id int, 
    name varchar(20) unique
);

create table user8(
    id int, 
    name varchar(20),
    unique(id, name)
);


mysql> desc user8;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  | MUL | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)


insert into user8 values(1,'张三');
insert into user8 values(1,'张三');

#组合在一起不重复就可以
unique(id, name) 

mysql> insert into user8 values(2,'李四');
Query OK, 1 row affected (0.00 sec)

mysql> select * from user8;
+------+--------+
| id   | name   |
+------+--------+
|    1 | 张三   |
|    2 | 张三   |
|    2 | 李四   |
+------+--------+
3 rows in set (0.00 sec)


# 删除唯一约束
alter table user7 drop index name;

mysql> alter table user7 drop index name;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc user7;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

modify 添加

alter table user7 modify name varchar(20) unique;


总结:
1、建表的时候就添加约束
2、使用alter 。。。 add。。。
3、使用alter 。。。 modify。。。去添加
4、使用alter 。。。 drop 。。。 去删除



```
## 非空约束

修饰的字段不能为null
```
create table user9 (
    id int,
    name varchar(20) not null
);


mysql> desc user9;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

insert into user9 values(1, '张三');

insert into user9 (name) values('李四');

mysql> select * from user9;
+------+--------+
| id   | name   |
+------+--------+
|    1 | 张三   |
| NULL | 李四   |
+------+--------+
2 rows in set (0.00 sec)



```


## 默认约束

```
就是当插入字段值的时候如果没有传值，就会使用默认值

create table user10(
    id int, 
    name varchar(20),
    age int default 10
);

mysql> desc user10;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | 10      |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

insert into user10 (id, name) values(1,'张三');

mysql> select * from user10;
+------+--------+------+
| id   | name   | age  |
+------+--------+------+
|    1 | 张三   |   10 |
+------+--------+------+
1 row in set (0.01 sec)

insert into user10 values(1,'张三',19);

mysql> insert into user10 values(1,'张三',19);
Query OK, 1 row affected (0.01 sec)

mysql> select * from user10;
+------+--------+------+
| id   | name   | age  |
+------+--------+------+
|    1 | 张三   |   10 |
|    1 | 张三   |   19 |
+------+--------+------+
2 rows in set (0.00 sec)


传了值就不会使用默认值

```

##  外键约束
```
设计到两个表：主表，副表

班级表
create table classes (
    id int primary key,
    name varchar(20)
);


学生表
create table students(
    id int primary key,
    name varchar(20),
    class_id int,
    foreign key(class_id) references classes(id) 
);

insert into classes values(1,'1班');
insert into classes values(2,'2班');
insert into classes values(3,'3班');
insert into classes values(4,'4班');

mysql> select * from classes;
+----+------+
| id | name |
+----+------+
|  1 | 1班  |
|  2 | 2班  |
|  3 | 3班  |
|  4 | 4班  |
+----+------+
4 rows in set (0.00 sec)

insert into students values(1001,'张三',1);
insert into students values(1002,'张三',2);
insert into students values(1003,'张三',3);
insert into students values(1004,'张三',4);

insert into students values(1005,'李四',5);

mysql> insert into students values(1005,'李四',5);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`test`.`students`, CONSTRAINT `students_ibfk_1` FOREIGN KEY (`class_id`) REFERENCES `classes` (`id`))

1、主表 classes 中没有的数据值在副表中不可以使用
2、主表中的记录被副表引用，是不可以被删除

delete from classes where id = 4;

mysql> delete from classes where id = 4;
ERROR 1451 (23000): Cannot delete or update a parent row: a foreign key constraint fails (`test`.`students`, CONSTRAINT `students_ibfk_1` FOREIGN KEY (`class_id`) REFERENCES `classes` (`id`))     //4班被引用了

```






# 数据库三大设计范式

## 第一范式 

```
数据表中的所有字段都是不可分割的原子值

create table student2(
    id int primary key,
    name varchar(20),
    address varchar(30)
);

insert into student2 values(1,'张三','江苏苏州');
insert into student2 values(2,'李四','江苏南京');
insert into student2 values(3,'王五','江苏无锡');

mysql> select * from student2;
+----+--------+--------------+
| id | name   | address      |
+----+--------+--------------+
|  1 | 张三   | 江苏苏州     |
|  2 | 李四   | 江苏南京     |
|  3 | 王五   | 江苏无锡     |
+----+--------+--------------+
3 rows in set (0.00 sec)

字段值还可以继续拆分，不满足1NF

create table student3(
    id int primary key,
    name varchar(20),
    country varchar(30),
    privince varchar(30),
    city varchar(30),
    details varchar(30)
);


insert into student3 values(1,'张三','中国','江苏省','苏州市','干将路333号');
insert into student3 values(2,'李四','中国','江苏省','苏州市','人民路100号');
insert into student3 values(3,'王五','中国','江苏省','苏州市','十全街300号');

mysql> select * from student3;
+----+--------+---------+-----------+-----------+-----------------+
| id | name   | country | privince  | city      | details         |
+----+--------+---------+-----------+-----------+-----------------+
|  1 | 张三   | 中国    | 江苏省    | 苏州市    | 干将路333号     |
|  2 | 李四   | 中国    | 江苏省    | 苏州市    | 人民路100号     |
|  3 | 王五   | 中国    | 江苏省    | 苏州市    | 十全街300号     |
+----+--------+---------+-----------+-----------+-----------------+
3 rows in set (0.00 sec)

范式，设计的越详细，对于某些实际操作可能更好，但不一定都是好处。
拆字段，字段不可以再拆分，满足第一范式


```

## 第二范式
```
前提：必须满足第一范式
除主键外的每一列都必须完全依赖于主键，才能满足第二范式
如果要出现不完全依赖，只看发生在联合主键的情况下

订单表

create table myOrder(
    product_id int, 
    customer_id int, 
    product_name varchar(20),
    customer_name varchar(20),
    primary key(product_id, customer_id)
);

问题：
除主键以外的其他列，只依赖于主键的部分字段（不完全依赖于主键），不满足第二范式

拆表

create table myOrder(
    order_id primary key;
    product_id int, 
    customer_id int
);

create table product(
    id int primary key,
    name varchar(20)
);

create table customer(
    id int primary key,
    name varchar(20)
);

分成三个表，满足了第二范式的设计！！

```


## 第三范式
```
必须先满足第二范式
除了主键列的其他列，不能有传递依赖

create table myOrder(
    order_id primary key;
    product_id int, 
    customer_id int,
    customer_phone varchar(15)
);


改成以下:

create table myOrder(
    order_id primary key;
    product_id int, 
    customer_id int,
);

create table customer(
    id int primary key;
    name varchar(20),
    phone varchar(15)
);

满足第三范式：不能有传递依赖

```

# MySql查询练习

```
> 学生表
Student
学号
姓名
出生年月日
所在班级

create table student(
    sno varchar(20) primary key,
    sname varchar(20) not null,
    ssex varchar(10) not null,
    sbirthday datetime,
    class varchar(20)
);




> 课程表
Course
课程号
课程名称
教师编号

create table course(
    cno varchar(20) primary key,
    cname varchar(20) not null,
    tno varchar(20) not null,
    foreign key(tno) references teacher(tno)
);

> 教师表
Teacher
教师编号
教师名字
教师性别
出生年月日
职称
所在部门

create table teacher(
    tno varchar(20) primary key,
    tname varchar(20) not null,
    tsex varchar(10) not null,
    tbirthday datetime,
    prof varchar(20) not null,
    dapartment varchar(20) not null
);

> 成绩表
Score
学号
课程号
成绩

create table score(
    sno varchar(20) not null,
    cno varchar(20) not null,
    degree decimal,
    foreign key(sno) references student(sno),
    foreign key(cno) references course(cno),
    primary key(sno, cno)
);



往数据表中添加数据

添加学生信息
insert into student values('101','曾华','男','1977-09-01','95033');
insert into student values('102','匡明','男','1975-10-02','95031');
insert into student values('103','王丽','女','1976-01-23','95033');
insert into student values('104','李军','男','1976-02-20','95033');
insert into student values('105','王芳','女','1975-02-10','95031');
insert into student values('106','陆君','男','1974-06-03','95031');
insert into student values('107','王尼玛','男','1977-09-01','95033');
insert into student values('108','张全蛋','男','1975-10-02','95031');
insert into student values('109','赵铁柱','女','1976-01-23','95033');

添加教师表
insert into teacher values('804','李诚','男','1958-12-02','副教授','计算机系');
insert into teacher values('856','张旭','男','1969-03-12','讲师','电子工程系');
insert into teacher values('825','王萍','女','1972-05-05','助教','计算机系');
insert into teacher values('831','刘冰','女','1977-08-14','助教','电子工程系');

添加课程表
insert into course values('3-105','计算机导论','825');
insert into course values('3-245','操作系统','804');
insert into course values('6-166','数字电路','856');
insert into course values('9-888','高等数学','831');

添加成绩表
insert into score values('103','3-105','92');
insert into score values('103','3-245','86');
insert into score values('103','6-166','85');
insert into score values('105','3-105','88');
insert into score values('105','3-245','75');
insert into score values('105','6-166','79');
insert into score values('109','3-105','76');
insert into score values('109','3-245','68');
insert into score values('109','6-166','81');

```

查询练习

## 1、查询student表的所有记录

```
mysql> select * from student;
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 101 | 曾华      | 男   | 1977-09-01 00:00:00 | 95033 |
| 102 | 匡明      | 男   | 1975-10-02 00:00:00 | 95031 |
| 103 | 王丽      | 女   | 1976-01-23 00:00:00 | 95033 |
| 104 | 李军      | 男   | 1976-02-20 00:00:00 | 95033 |
| 105 | 王芳      | 女   | 1975-02-10 00:00:00 | 95031 |
| 106 | 陆君      | 男   | 1974-06-03 00:00:00 | 95031 |
| 107 | 王尼玛    | 男   | 1977-09-01 00:00:00 | 95033 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
| 109 | 赵铁柱    | 女   | 1976-01-23 00:00:00 | 95033 |
+-----+-----------+------+---------------------+-------+
9 rows in set (0.00 sec)

```

## 2、查询student表中的所有记录的sname，ssex和class列

```

select sname, ssex, class from student;

mysql> select sname, ssex, class from student;
+-----------+------+-------+
| sname     | ssex | class |
+-----------+------+-------+
| 曾华      | 男   | 95033 |
| 匡明      | 男   | 95031 |
| 王丽      | 女   | 95033 |
| 李军      | 男   | 95033 |
| 王芳      | 女   | 95031 |
| 陆君      | 男   | 95031 |
| 王尼玛    | 男   | 95033 |
| 张全蛋    | 男   | 95031 |
| 赵铁柱    | 女   | 95033 |
+-----------+------+-------+
9 rows in set (0.00 sec)

```

## 3、查询教师所有单位即不重复的department列

```

select distinct department from teacher;

mysql> select distinct department from teacher;
+-----------------+
| department      |
+-----------------+
| 计算机系        |
| 电子工程系      |
+-----------------+
2 rows in set (0.00 sec)

```

## 4、查询score表中成绩在60到80之间的所有记录

```
查询区间  between 。。。 and 。。。

select * from score where degree between 60 and 80;

mysql> select * from score where degree between 60 and 80;
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 105 | 3-245 |     75 |
| 105 | 6-166 |     79 |
| 109 | 3-105 |     76 |
| 109 | 3-245 |     68 |
+-----+-------+--------+
4 rows in set (0.01 sec)

select * from score where degree > 60 and degree < 80;

```
## 5、查询score表中成绩为85，86或88的记录

```
表示或者关系的查询  in

select * from score where degree in (85, 86, 88);

mysql> select * from score where degree in (85, 86, 88);
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 103 | 3-245 |     86 |
| 103 | 6-166 |     85 |
| 105 | 3-105 |     88 |
+-----+-------+--------+
3 rows in set (0.00 sec)
```
## 6、查询student表中“95031”班或性别为“女”的同学记录
```sql
select * from student where class='95031' or ssex='女';

mysql> select * from student where class='95031' or ssex='女';
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 102 | 匡明      | 男   | 1975-10-02 00:00:00 | 95031 |
| 103 | 王丽      | 女   | 1976-01-23 00:00:00 | 95033 |
| 105 | 王芳      | 女   | 1975-02-10 00:00:00 | 95031 |
| 106 | 陆君      | 男   | 1974-06-03 00:00:00 | 95031 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
| 109 | 赵铁柱    | 女   | 1976-01-23 00:00:00 | 95033 |
+-----+-----------+------+---------------------+-------+
6 rows in set (0.00 sec)
```
## 7、以class降序查询student表中的所有记录

升序降序 asc desc

select * from student order by class desc;

mysql> select * from student order by class desc;
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 101 | 曾华      | 男   | 1977-09-01 00:00:00 | 95033 |
| 103 | 王丽      | 女   | 1976-01-23 00:00:00 | 95033 |
| 104 | 李军      | 男   | 1976-02-20 00:00:00 | 95033 |
| 107 | 王尼玛    | 男   | 1977-09-01 00:00:00 | 95033 |
| 109 | 赵铁柱    | 女   | 1976-01-23 00:00:00 | 95033 |
| 102 | 匡明      | 男   | 1975-10-02 00:00:00 | 95031 |
| 105 | 王芳      | 女   | 1975-02-10 00:00:00 | 95031 |
| 106 | 陆君      | 男   | 1974-06-03 00:00:00 | 95031 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
+-----+-----------+------+---------------------+-------+
9 rows in set (0.00 sec)

select * from student order by class asc;


## 8、以cno升序、degree降序查询score表中的所有记录
```sql
select * from score order by cno asc, degree desc;

mysql> select * from score order by cno asc, degree desc;
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 103 | 3-105 |     92 |
| 105 | 3-105 |     88 |
| 109 | 3-105 |     76 |
| 103 | 3-245 |     86 |
| 105 | 3-245 |     75 |
| 109 | 3-245 |     68 |
| 103 | 6-166 |     85 |
| 109 | 6-166 |     81 |
| 105 | 6-166 |     79 |
+-----+-------+--------+
9 rows in set (0.00 sec)
```
## 9、查询“95031”班的学生人数
```
统计 count

select count(*) from student where class='95031';

mysql> select count(*) from student where class='95031';
+----------+
| count(*) |
+----------+
|        4 |
+----------+
1 row in set (0.01 sec)

```
## 10、查询score表中的最高分的学生学号和课程号（子查询或者排序）
```sql
select sno, cno from score where degree=(select max(degree) from score);

mysql> select sno, cno from score where degree=(select max(degree) from score);
+-----+-------+
| sno | cno   |
+-----+-------+
| 103 | 3-105 |
+-----+-------+
1 row in set (0.00 sec)


1、找到最高分
select max(degree) from score

+-------------+
| max(degree) |
+-------------+
|          92 |
+-------------+
1 row in set (0.00 sec)

2、找到最高分的sno和cno

select sno, cno from score where degree=(select max(degree) from score);

排序的做法：

select sno, cno, degree from score order by degree;

mysql> select sno, cno, degree from score order by degree;
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 109 | 3-245 |     68 |
| 105 | 3-245 |     75 |
| 109 | 3-105 |     76 |
| 105 | 6-166 |     79 |
| 109 | 6-166 |     81 |
| 103 | 6-166 |     85 |
| 103 | 3-245 |     86 |
| 105 | 3-105 |     88 |
| 103 | 3-105 |     92 |
+-----+-------+--------+
9 rows in set (0.00 sec)

select sno, cno, degree from score order by degree limit 0,1;

mysql> select sno, cno, degree from score order by degree limit 0,1;
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 109 | 3-245 |     68 |
+-----+-------+--------+
1 row in set (0.00 sec)

select sno, cno, degree from score order by degree desc limit 0,1;

mysql> select sno, cno, degree from score order by degree desc limit 0,1;
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 103 | 3-105 |     92 |
+-----+-------+--------+
1 row in set (0.00 sec)

select sno, cno, degree from score order by degree desc limit 0,2;

limit作用： 从多少开始查，查多少条

```

## 11、查询每门课的平均成绩

```sql
select * from course;


avg()

select avg(degree) from score where cno='3-105'; 

mysql> select avg(degree) from score where cno='3-105';
+-------------+
| avg(degree) |
+-------------+
|     85.3333 |
+-------------+
1 row in set (0.00 sec)

select degree from score where cno='3-105';

查询每门课的平均成绩

select cno, avg(degree) from score group by cno;

mysql> select cno, avg(degree) from score group by cno;
+-------+-------------+
| cno   | avg(degree) |
+-------+-------------+
| 3-105 |     85.3333 |
| 3-245 |     76.3333 |
| 6-166 |     81.6667 |
+-------+-------------+
3 rows in set (0.00 sec)


```

## 12、查询score表中至少有2名学生选修的并以3开头的课程的平均分数

```sql
分组条件与模糊查询

select cno, avg(degree), count(*) from score group by cno
having count(cno)>=2 and cno like '3%';

mysql> select cno, avg(degree), count(*) from score group by cno
    -> having count(cno)>=2 and cno like '3%';
+-------+-------------+
| cno   | avg(degree) |
+-------+-------------+
| 3-105 |     85.3333 |
| 3-245 |     76.3333 |
+-------+-------------+
2 rows in set (0.01 sec)

mysql> select cno, avg(degree), count(*) from score group by cno
    -> having count(cno)>=2 and cno like '3%';
+-------+-------------+----------+
| cno   | avg(degree) | count(*) |
+-------+-------------+----------+
| 3-105 |     85.3333 |        3 |
| 3-245 |     76.3333 |        3 |
+-------+-------------+----------+
2 rows in set (0.00 sec)

分组  group by
分组后带条件  having 不是 where
模糊查询 like 

```

## 13、查询分数大于70，小于90的 sno 列

```sql
select sno, degree from score
where degree>70 and degree<90;

select sno, degree from score
where degree between 70 and 90;

mysql> select sno, degree from score
    -> where degree>70 and degree<90;
+-----+--------+
| sno | degree |
+-----+--------+
| 103 |     86 |
| 103 |     85 |
| 105 |     88 |
| 105 |     75 |
| 105 |     79 |
| 109 |     76 |
| 109 |     81 |
+-----+--------+
7 rows in set (0.00 sec)

```

## 14、查询所有学生的 sname，cno 和 degree 列

```sql
多表查询  

select sname from student;

select cno, degree from score;

添加sno，多表查询

select sno, sname from student;

select sno, cno, degree from score;

select sname, cno, degree from student, score
where student.sno=score.sno;

mysql> select sname, cno, degree from student, score
    -> where student.sno=score.sno;
+-----------+-------+--------+
| sname     | cno   | degree |
+-----------+-------+--------+
| 王丽      | 3-105 |     92 |
| 王丽      | 3-245 |     86 |
| 王丽      | 6-166 |     85 |
| 王芳      | 3-105 |     88 |
| 王芳      | 3-245 |     75 |
| 王芳      | 6-166 |     79 |
| 赵铁柱    | 3-105 |     76 |
| 赵铁柱    | 3-245 |     68 |
| 赵铁柱    | 6-166 |     81 |
+-----------+-------+--------+
9 rows in set (0.00 sec)

```

## 15、查询所有学生的 sno，cname 和 degree 列

```sql
select cno, cname from course;

mysql> select cno, cname from course;
+-------+-----------------+
| cno   | cname           |
+-------+-----------------+
| 3-105 | 计算机导论      |
| 3-245 | 操作系统        |
| 6-166 | 数字电路        |
| 9-888 | 高等数学        |
+-------+-----------------+
4 rows in set (0.00 sec)

select cno, sno, degree from score;

mysql> select cno, sno, degree from score;
+-------+-----+--------+
| cno   | sno | degree |
+-------+-----+--------+
| 3-105 | 103 |     92 |
| 3-245 | 103 |     86 |
| 6-166 | 103 |     85 |
| 3-105 | 105 |     88 |
| 3-245 | 105 |     75 |
| 6-166 | 105 |     79 |
| 3-105 | 109 |     76 |
| 3-245 | 109 |     68 |
| 6-166 | 109 |     81 |
+-------+-----+--------+
9 rows in set (0.00 sec)


select sno, cname, degree from score, course 
where score.cno=course.cno;


mysql> select sno, cname, degree from score, course 
    -> where score.cno=course.cno;
+-----+-----------------+--------+
| sno | cname           | degree |
+-----+-----------------+--------+
| 103 | 计算机导论      |     92 |
| 103 | 操作系统        |     86 |
| 103 | 数字电路        |     85 |
| 105 | 计算机导论      |     88 |
| 105 | 操作系统        |     75 |
| 105 | 数字电路        |     79 |
| 109 | 计算机导论      |     76 |
| 109 | 操作系统        |     68 |
| 109 | 数字电路        |     81 |
+-----+-----------------+--------+
9 rows in set (0.01 sec)


```

## 16、查询所有学生的sname， cname， degree 列

```sql
要查询的字段分别来自三张表

sname-->student
cname-->course
degree-->score

select sname, cname, degree from student, course, score
where student.sno=score.sno and course.cno=score.cno;


mysql> select sname, cname, degree from student, course, score
    -> where student.sno=score.sno and course.cno=score.cno;
+-----------+-----------------+--------+
| sname     | cname           | degree |
+-----------+-----------------+--------+
| 王丽      | 计算机导论      |     92 |
| 王丽      | 操作系统        |     86 |
| 王丽      | 数字电路        |     85 |
| 王芳      | 计算机导论      |     88 |
| 王芳      | 操作系统        |     75 |
| 王芳      | 数字电路        |     79 |
| 赵铁柱    | 计算机导论      |     76 |
| 赵铁柱    | 操作系统        |     68 |
| 赵铁柱    | 数字电路        |     81 |
+-----------+-----------------+--------+
9 rows in set (0.00 sec)

select sname, cname, degree, student.sno, course.cno from student, course, score
where student.sno=score.sno 
and course.cno=score.cno;

mysql> select sname, cname, degree, student.sno, course.cno from student, course, score
    -> where student.sno=score.sno 
    -> and course.cno=score.cno;
+-----------+-----------------+--------+-----+-------+
| sname     | cname           | degree | sno | cno   |
+-----------+-----------------+--------+-----+-------+
| 王丽      | 计算机导论      |     92 | 103 | 3-105 |
| 王丽      | 操作系统        |     86 | 103 | 3-245 |
| 王丽      | 数字电路        |     85 | 103 | 6-166 |
| 王芳      | 计算机导论      |     88 | 105 | 3-105 |
| 王芳      | 操作系统        |     75 | 105 | 3-245 |
| 王芳      | 数字电路        |     79 | 105 | 6-166 |
| 赵铁柱    | 计算机导论      |     76 | 109 | 3-105 |
| 赵铁柱    | 操作系统        |     68 | 109 | 3-245 |
| 赵铁柱    | 数字电路        |     81 | 109 | 6-166 |
+-----------+-----------------+--------+-----+-------+
9 rows in set (0.00 sec)

select sname, cname, degree, student.sno as stu_sno, score.sno, course.cno as cou_cno, score.cno from student, course, score
where student.sno=score.sno 
and course.cno=score.cno;

mysql> select sname, cname, degree, student.sno as stu_sno, score.sno, course.cno as cou_cno, score.cno from student, course, score
    -> where student.sno=score.sno 
    -> and course.cno=score.cno;
+-----------+-----------------+--------+---------+-----+---------+-------+
| sname     | cname           | degree | stu_sno | sno | cou_cno | cno   |
+-----------+-----------------+--------+---------+-----+---------+-------+
| 王丽      | 计算机导论      |     92 | 103     | 103 | 3-105   | 3-105 |
| 王丽      | 操作系统        |     86 | 103     | 103 | 3-245   | 3-245 |
| 王丽      | 数字电路        |     85 | 103     | 103 | 6-166   | 6-166 |
| 王芳      | 计算机导论      |     88 | 105     | 105 | 3-105   | 3-105 |
| 王芳      | 操作系统        |     75 | 105     | 105 | 3-245   | 3-245 |
| 王芳      | 数字电路        |     79 | 105     | 105 | 6-166   | 6-166 |
| 赵铁柱    | 计算机导论      |     76 | 109     | 109 | 3-105   | 3-105 |
| 赵铁柱    | 操作系统        |     68 | 109     | 109 | 3-245   | 3-245 |
| 赵铁柱    | 数字电路        |     81 | 109     | 109 | 6-166   | 6-166 |
+-----------+-----------------+--------+---------+-----+---------+-------+
9 rows in set (0.00 sec)

```

## 17、查询'95031'班学生每门课的平均分

```sql
select * from student where class='95031';
select sno from student where class='95031';


select * from score where sno in (select sno from student where class='95031');

select cno, avg(degree) 
from score 
where sno in (select sno from student where class='95031') 
group by cno;

mysql> select cno, avg(degree) 
    -> from score 
    -> where sno in (select sno from student where class='95031') 
    -> group by cno;
+-------+-------------+
| cno   | avg(degree) |
+-------+-------------+
| 3-105 |     88.0000 |
| 3-245 |     75.0000 |
| 6-166 |     79.0000 |
+-------+-------------+
3 rows in set (0.00 sec)

```

## 18、查询选修'3-105课程的成绩高于‘109’号同学‘3-105’成绩的所有同学的记录

```sql

select degree from score where sno='109' and cno='3-105';

select * from score where cno='105' and  degree>(select degree from score where sno='109' and cno='3-105');

```

## 19、查询成绩高于学号为‘109’、课程号为‘3-105’的成绩的所有记录

```sql

select * from score where degree>(select degree from score where sno='109' and cno='3-105');

mysql> select * from score where degree>(select degree from score where sno='109' and cno='3-105');
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 103 | 3-105 |     92 |
| 103 | 3-245 |     86 |
| 103 | 6-166 |     85 |
| 105 | 3-105 |     88 |
| 105 | 6-166 |     79 |
| 109 | 6-166 |     81 |
+-----+-------+--------+
6 rows in set (0.00 sec)

```

## 20、查询和学号为108、101的同学同年出生的所有学生的sno、sname和sbirthday列

```sql

select * from student where sno in (108,101);

mysql> select * from student where sno in (108,101);
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 101 | 曾华      | 男   | 1977-09-01 00:00:00 | 95033 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
+-----+-----------+------+---------------------+-------+
2 rows in set (0.00 sec)

select year(sbirthday) from student where sno in (108,101);

mysql> select year(sbirthday) from student where sno in (108,101);
+-----------------+
| year(sbirthday) |
+-----------------+
|            1977 |
|            1975 |
+-----------------+
2 rows in set (0.00 sec)

select * from student where year(sbirthday) in (select year(sbirthday) from student where sno in (108,101));

mysql> select * from student where year(sbirthday) in (select year(sbirthday) from student where sno in (108,101));
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 101 | 曾华      | 男   | 1977-09-01 00:00:00 | 95033 |
| 107 | 王尼玛    | 男   | 1977-09-01 00:00:00 | 95033 |
| 102 | 匡明      | 男   | 1975-10-02 00:00:00 | 95031 |
| 105 | 王芳      | 女   | 1975-02-10 00:00:00 | 95031 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
+-----+-----------+------+---------------------+-------+
5 rows in set (0.01 sec)

```

## 21、查询“张旭”教师任课的学生成绩

```sql

多层嵌套子查询

select tno from teacher where tname='张旭';

select cno from course where tno = (select tno from teacher where tname='张旭');

select * from score where cno = (select cno from course where tno = (select tno from teacher where tname='张旭'));

mysql> select * from score where cno = (select cno from course where tno = (select tno from teacher where tname='张旭'));
+-----+-------+--------+
| sno | cno   | degree |
+-----+-------+--------+
| 103 | 6-166 |     85 |
| 105 | 6-166 |     79 |
| 109 | 6-166 |     81 |
+-----+-------+--------+
3 rows in set (0.01 sec)

```

## 22、查询选修某课程的同学人数多于5人的教师姓名

```sql
insert into score values('101','3-105','90');
insert into score values('102','3-105','91');
insert into score values('104','3-105','89');

insert into score values('103','3-105','92');
insert into score values('103','3-245','86');
insert into score values('103','6-166','85');
insert into score values('105','3-105','88');
insert into score values('105','3-245','75');
insert into score values('105','6-166','79');
insert into score values('109','3-105','76');
insert into score values('109','3-245','68');
insert into score values('109','6-166','81');

select cno from score group by cno having count(*)>5;

select tname from teacher where tno=(select tno from course where cno=(select cno from score group by cno having count(*)>5));

mysql> select tname from teacher where tno=(select tno from course where cno=(select cno from score group by cno having count(*)>5));
+--------+
| tname  |
+--------+
| 王萍   |
+--------+
1 row in set (0.00 sec)

```

## 23、查询95033和95031班全体学生的记录
```sql
in表示或者关系

select * from student where class in(95033, 95031);

mysql> select * from student where class in(95033, 95031);
+-----+-----------+------+---------------------+-------+
| sno | sname     | ssex | sbirthday           | class |
+-----+-----------+------+---------------------+-------+
| 101 | 曾华      | 男   | 1977-09-01 00:00:00 | 95033 |
| 102 | 匡明      | 男   | 1975-10-02 00:00:00 | 95031 |
| 103 | 王丽      | 女   | 1976-01-23 00:00:00 | 95033 |
| 104 | 李军      | 男   | 1976-02-20 00:00:00 | 95033 |
| 105 | 王芳      | 女   | 1975-02-10 00:00:00 | 95031 |
| 106 | 陆君      | 男   | 1974-06-03 00:00:00 | 95031 |
| 107 | 王尼玛    | 男   | 1977-09-01 00:00:00 | 95033 |
| 108 | 张全蛋    | 男   | 1975-10-02 00:00:00 | 95031 |
| 109 | 赵铁柱    | 女   | 1976-01-23 00:00:00 | 95033 |
+-----+-----------+------+---------------------+-------+
9 rows in set (0.00 sec)

```

## 24、查询存在有85分以上成绩的课程cno

```sql
select cno, degree from score where degree>85;
```

## 25、查询出‘计算机系’教师所教课程的成绩表

```sql
//先查询出出计算机系的老师
select tno from teacher where department='计算机系';

//根据查找到的老师查询到所教的课程
select cno from course where tno in (select tno from teacher where department='计算机系');

//再根据课程查询成绩表
select * from score where cno in (select cno from course where tno in (select tno from teacher where department='计算机系'));


```

## 26、查询‘计算机系’和‘电子工程系’不同职称的教师的tname和prof

```sql

union 求并集
select prof from teacher where department='电子工程系'

select * from teacher where department='计算机系' and prof not in (select prof from teacher where department='电子工程系')
union
select * from teacher where department='电子工程系' and prof not in (select prof from teacher where department='计算机系');

mysql> select * from teacher where department='计算机系' and prof not in (select prof from teacher where department='电子工程系')
    -> union
    -> select * from teacher where department='电子工程系' and prof not in (select prof from teacher where department='计算机系');
+-----+--------+------+---------------------+-----------+-----------------+
| tno | tname  | tsex | tbirthday           | prof      | department      |
+-----+--------+------+---------------------+-----------+-----------------+
| 804 | 李诚   | 男   | 1958-12-02 00:00:00 | 副教授    | 计算机系        |
| 856 | 张旭   | 男   | 1969-03-12 00:00:00 | 讲师      | 电子工程系      |
+-----+--------+------+---------------------+-----------+-----------------+
```

## 27、查询选修编号为‘3-105’课程且成绩至少高于选修编号为‘3-245’的同学的cno，sno和degree，并按degree从高到低次序排列

```sql

```