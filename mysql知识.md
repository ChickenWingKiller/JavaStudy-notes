# DDL--操作数据库，表，列等
1. 查询：show databases;
2. 创建 
创建数据库：create database 数据库名称;
创建数据库（判断，如果不存在则创建）：create database if not exists 数据库名称;
3. 删除
删除数据库：drop database 数据库名称;
删除数据库（判断，如果存在则删除）：drop databse if exists 数据库名称;
4. 使用数据库
查看当前使用的数据库：select database();
使用数据库（进入数据库）：use 数据库名称;

# DDL--操作表
1. 查询表
查询当前数据库下所有表名称：show tables;
查询表结构：desc 表名称;
2. 创建表：
create table 表名(
	字段名1 数据类型1，
	字段名2 数据类型2，
	...
	字段名n 数据类型n
);
注意：最后一行末尾，不能加逗号。
3. 删除表
drop table 表名;
删除表时判断表是否存在：drop table if exists 表名;
4. 修改表
	* 修改表名：alter table 表名 rename to 新的表名;
	* 添加一列：alter table 表名 add 列名 数据类型;
	* 修改数据类型：alter table 表名 modify 列名 新数据类型;
	* 修改列名和数据类型：alter table 表名 change 列名 新列名 新数据类型;
	* 删除列：alter table 表名 drop 列名;

# DML--对表中的数据进行增删改
1. 添加数据
	* 给指定列添加数据：insert into 表名（列名1，列名2，...) values (值1，值2，...);
	* 给全部列添加数据：insert into 表名 values (值1，值2，...);
	* 批量添加数据：insert into 表名 (列名1，列名2，...) values (值1，值2，...),(值1，值2，...)...;
insert into 表名 values (值1，值2，...),(值1，值2，...)...;
2. 修改数据
修改表数据：update 表名 set 列名1=值1, 列名2=值2,...[where 条件];
3. 删除数据
delete from 表名 [where 条件];

# DQL--对表中的数据进行查询
查询语法：
select
	字段列表
from
	表名列表
where
	条件列表
group by
	分组字段
having
	分组后条件
order by
	排序字段
limit
	分页限定
## 1.基础查询
查询多个字段：select 字段列表 from 表名;
select * from 表名; --查询所有数据
去除重复记录：select distinct 字段列表 from 表名;
起别名：as : as也可以省略，写在列名后面
## 2.条件查询：
select 字段列表 from 表名 where 条件列表;
不等于号： ！=,<>
null值的比较不能使用 =,!=。需要使用 is,is not。
age=1 or age=2 or age=3, in (1,2,3)
like占位符：模糊查询，_单个任意字符，%多个任意字符。 (查询姓'马'的学员信息：select * from stu where name like '马%';)

## 3.排序查询
select 字段列表 from 表名 order by 排序字段名1 排序方式1,排序字段名2 排序方式2 ...;
排序方式：ASC 升序排列（默认值），DESC 降序排列
如果有多个排序条件，当前面的条件值一样时，才会根据第二条件进行排序
## 4.聚合函数（将一列数据作为一个整体，进行纵向计算）
select 聚合函数名(列名) from 表名;
count(列名):统计数量
	取值：1.主键；2，*
max(列名)
min(列名)
sum(列名)
avg(列名)
注意：null值不参与所有聚合函数运算
## 5.分组查询
select 字段列表 from 表名 [where 分组前条件限定] group by 分组字段名 [having 分组后条件过滤];
注意：分组之后，查询的字段为聚合函数和分组字段，查询其他字段无任何意义。
(查询男同学和女同学各自的数学平均分，以及各自人数，要求：分数低于70分的不参与分组，分组之后人数大于2个的：select sex, avg(math), count(\*) from stu where math>70 group by sex having count(\*)>2;)
where和having的区别：1.执行时机不一样，where是分组之前进行限定，不满与where条件，则不参与分组，而having是分组之后对结果进行过滤。
					2.可判断的条件不一样，where不能对聚合函数进行判断，having可以。(执行顺序：where>聚合函数>having)
## 6.分页查询
select 字段列表 from 表名 limit 起始索引, 查询条目数;
起始索引：从0开始
计算公式：起始索引=(当前页码-1)*每页显示的条目数
tips：1，分页查询limit是MySQL数据库的方言，Oracle用rownumber，SQL Server用top

# 约束
- 约束的概念：约束是作用于表中列上的规则，用于限制加入表的数据。约束的存在保证了数据库中数据的正确性、有效性和完整性。
- 约束的分类：
	1. 非空约束。保证列中所有数据不能有null值，not null
	2. 唯一约束。保证列中所有数据各不相同，unique
	3. 主键约束。主键是一行数据的唯一标识，要求非空且唯一，primary key,(auto_increment,自增长,当列是数字类型并且唯一约束	)
	4. 检查约束。保证列中的值满足某一条件，check
	5. 默认约束。保存数据时，未指定值则采用默认值，default
	6. 外键约束。外键用来让两个表的数据之间建立连接，保证数据的一致性和完整性，foreign key
		   (tips：MySQL不支持检查约束)

在创建表时，字段的数据类型后面，添加约束。或者建完表通过alter table添加约束。
创建外键：建表时添加约束：constraint 外键名称 FOREIGN key (外键列名) REFERENCES 主表(主表列名);
建完表后，添加外键：alter table emp(表名) add CONSTRAINT fk_emp_dept(外键名称) Foreign key(dep_id(外键字段名称)) REFERENCES dept(主表名称)(id(主表列名称));
删除外键：alter table emp(表名) drop FOREIGN key fk_emp_dept(外键名称);

# 数据库设计
- 概念：建立数据库中的表结构以及表与表之间的关联关系的过程。设计有哪些表，表里有哪些字段，表和表之间是什么关系。
- 表之间的关系：
	1. 一对一：用户和用户详情，一对一关系多用于表拆分，将一个实体中经常使用的字段放一张表，不经常使用的字段放另一张表，用于提升查询性能。
				实现方式：在任意一方加入外键，关联另一方主键，并且设置外键为唯一(unique)
	2. 一对多（多对一）：员工和部内。
			 	实现方式：在多的一方建立外键，指向一的一方的主键。
	3. 多对多：商品和订单。
			 	实现方式：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键。

# 多表查询 （从多张表查询数据）
- 笛卡尔积：取A，B集合所有组合的情况
- 连接查询：
	1. 内连接：相当于A，B交集数据。(select * from emp, dept where emp.dep_id=dept.did)
		- 隐式内连接：select 字段列表 from 表1，表2... where 条件;(select t1.name,t1.gender,t2.dname from emp t1,dept t2 where t1.dep_id=t2.did;)
		- 显示内连接：select 字段列表 from 表1 [inner] join 表2 on 条件;(select * from emp inner join dept on emp.dep_id=dept.did),inner可以省略。
	2. 外连接：
		- 左外连接：相当于查询A表所有数据和交集部分数据。select 字段列表 from 表1 left [outer] join 表2 on 条件;
		- 右外连接：相当于查询B表所有数据和交集部分数据。select 字段列表 from 表1 right [outer] join 表2 on 条件;
		- 子查询：查询中嵌套查询，称嵌套查询为子查询。（查询工资高于猪八戒的员工信息：select * from emp where salary > (select salary from emp where name='猪八戒';)
		 	1. 子查询根据查询结果不同，作用不同：
		 		单行单列：作为条件值，使用=,!=,<,>等进行条件判断。 select 字段列表 from 表 where 字段名=(子查询);
		 		多行单列：作为条件值，使用in等关键字进行条件判断。 select 字段列表 from 表 where 字段名 in (子查询);
		 		多行多列：作为虚拟表。select 字段列表 from (子查询) where 条件;

# 事务
- 简介：数据库的事务(Transaction)是一种机制，一个操作序列，包含了一组数据库操作命令。这一组数据库命令要么同时成功，要么同时失败。事务是一个不可分割的工作逻辑单元。
- 开启事务：start transaction;、begin;
- 提交事务：commit;
- 回滚事务：rollback;
- 事务四大特征：A(原子性),C(一致性),I(隔离性),D(持久性)
- 查询事务的默认提交方式：select @@autocommit; 1为自动提交
- 修改事务的提交方式，手动提交：set @@autocommit = 0;
- oracle为默认手动提交