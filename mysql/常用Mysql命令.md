# 常用Mysql命令

1、查看当前数据库

```
select database();
```

2、查看数据库版本

```
select version();
```

3、显示广泛的服务器状态信息

```
show status;
```

4、查看当前登入用户

```
select user();
show grants; 显示用户权限
```

5、显示数据库列表

```
show databases
```

6、选择数据库

```
use school；
```

7、显示建库语句

```
show create database school;
```

8、显示数据库中的表

```
show tables;
```

9、显示建表语句

```
show create table student;
```

10、显示表中的字段

```
show columns from students;
```

## DDL

创建数据库

create database school；

删除数据库

delete database school；

创建表

create table school（

）

查看表定义

DESC school；

删除表

drop table school；

更改表名

**alter table** school  **rename** high_school

增加字段

**alter table** student **add column** age int(3);

删除字段

alter table student drop column age;

修改列类型

alter table student modify name varchar(30);

重命名字段

alter table student change age age_1 int(4);

## DML

插入记录

insert into student(id，name) values('1','张三')；

更新记录

update student set id='2',name='李四' where id = '1'；

删除记录

delete from student where name = '李四'；



### 视图

创建视图

create or replace view student_list_view as

select * from student

删除视图

drop view student_list_view

