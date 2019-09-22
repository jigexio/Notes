# MySQL

## [SQL](https://www.bilibili.com/video/av49005203/?p=1)
1. ### 什么是SQL？

   Structured Query Language(结构化查询语言)

   就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。

2. ### SQL通用语法
   
    SQL 语句可以单行或多行书写，以分号结尾
      	MySQL数据库的 SQL 语句不区分大小写，关键字建议使用大写
      	3种注释：
      		#单行注释：-- （有空格）或 #
    		  #多行注释：/* */
   
3. ### SQL分类

   ​	SQL语言按照实现的功能不同，主要分为3类：数据操纵语言（DML），数据定义语言（DDL）,数据控制语言（DCL）

   * ### 数据定义语言（DDL）:是一组SQL命令，用于创建和定义数据库对象，并且将对这些对象的定义保存到数据字典中。通过DDL语句可以创建数据库对象，修改数据库对象和删除数据库对象等。
   
   ####  1.==操作数据库==

常用的DDL语句及其功能：

 	***(Create)创建：**

​		创建数据库：		 

```SQL
  create database +数据库名称;
```



​	   创建数据库，判断不存在，再创建:		

```SQL
 create database if not exists +数据库名称;
```



​	   创建数据库，并指定字符集： 

```SQL
 create database +数据库名称 character set +字符集名称;
```

   

   练习：创建db4数据库，判断是否存在，并指定字符集为gbk

```SQL
 create database if not exists db4 character set gbk;
```



   

​		***(Retrieve)查询**

   		查询所有数据库的名称：

```SQL
	show databases;
```



  		 查询某个数据库的字符集：查询某个数据库的创建语句

```SQL
	  show create database +数据库名称;
```

   

   ​	***(Update)修改：**

​		   修改数据库的字符集:

```SQL
alter database +数据库名称 character set 字符集名称;
```

   

   ​	***(Delete)删除：**

  		 删除数据库：			  

```SQL
 drop database +数据库名称;
```



​		   判断数据库存在，存在再删除：	 

```SQL
  drop database if exists +数据库名称;
```

   

   ​	***使用数据库：**

​		   查询当前正在使用的数据库名称：	 

```SQL
 select database();
```



​		   使用数据库：

```SQL
use +数据库名称;
```





#### 			2.==操作表==



   ​	***(Retrieve)查询：**

​			查询某个数据库中所有的表名称：	

```SQL
	show tables;
```

​		  

​			 查询表结构：

```SQL
  	 desc +表名;
```



​		***(Create)创建：**

​			创建表：

```SQL
	create table +表名(

	 		   列名1 数据类型1，

			   列名2 数据类型2,

			   <u>*......*</u>

			   列名n 数据类型n

			   );
```

   数据库类型：

​		   1.int: 整数类型

​				   <u>age int</u>

  		 2.double:小数类型

   				<u>score double(5,2)</u> :总共有5位数，两位是小数，所以最大是999.99

  		 3.date:日期，只包含年月日，yyyy-MM-dd

​		   4.datetime:日期，包含年月日，时分秒，yyyy-MM-dd  HH-mm-ss

​		   5.timestamp:时间错类型，包含年月日，时分秒，yyyy-MM-dd  HH-mm-ss  (注：如果不给这个字段赋值，或赋值为NULL，则默认使用当前的系统时间，来自动赋值)

​		   6.varchar: 字符串

```SQL
 name vaechar(20):最大为20个字符

 zhangsan :8个字符  张三：2个字符
```



​		*例子：创建表：

```SQL
	create table student(

				id int,

				name varchar,

				age int,

				score double,

				birthday date,

				insert_time timestamp

				);
```

 		 ***复制表：**

```SQL
	create table +表名 like 被复制的表名
```



​	***修改表：**

​			修改表名：

```SQL
	alter table +表名 rename to 新表名;
```

​			修改表的字符集：			

```SQL
	alter table 表名 character set 字符集名称;
```

​			添加一列：

```SQL
	alter table +表名 add 数据类型;
```

​			修改列名称和数据类型：				

```SQL
	alter table 表名 change 列名 数据类型;

	alter table 表名 modify 列名 新数据类型;
```

​			删除列：

```SQL
	alter table 表名 drop 列名;
```



​		***删除表：**	

```SQL
	drop table +表名;

	drop table if exists +表名;
```



------



   * ### 数据操纵语言（DML）：主要用来处理数据库中的数据内容。允许用户对数据库中的数据进行查询 ，插入，更新和删除等操作。

   常用的DML语句及其功能：

​     **1.添加数据**：

​			*语法：

```SQL
	insert into 表名(列名1，列名2，...，列名n) values (值1，值2，...，值n)
```

​			*注意：

​		1.列名和值要一一对应

​		2.如果在表名后名没有添加列名的话，则默认给所有列添加值:	

```SQL
	insert into 表名 values (值1，值2，...，值n);
```

​		3.除了数字类型，其他类型需要使用引号(单双都可以)

​     **2.删除数据：**

​			*语法：

```SQL
	delete from 表名 [where +条件]
```

​			*注意:

​				1.如果不加条件，则会删除表中所有记录

​				2.如果要删除所有记录：			

```SQL
		1.delete from 表名;(不推荐，有多少条记录就会执行多少次删除记录操作，效率低)

		2.truncate table 表名;(推荐使用，效率更高，先删除表，再创建一个同名无记录的新表)
```

​	 **3.修改数据：**

​			*语法：	

```SQL
	update 表名 set 列名1=值1，列名2=值2，...[where 条件]；
```

​			*注意：

​				1.如果不加任何条件，则会将表中相应的所有记录全部修改。

- ### 数据查询语句(DQL):用来查询数据，不会对数据造成变化。把查询的结果发送到客户端进行显示。查询的结果为一个虚拟表。

  ​	具体请转：[MySQL之DQL](https://blog.csdn.net/qq_33248299/article/details/54881598)

  ​	1.**基础查询**

  ​			1.查询所有列：

  ```SQL
  select * from 表名;
  ```

  ​			2.查询指定列：

  ```SQL
  select 列名1,列名2,.. from 表名;
  ```

  

  ​	**2.排序查询**

  ​			*语法：
  
  ```SQL
order by 排序字段1 排序方式1，排序字段1 排序方式2，...
  ```

  ​			*排序方式：
  
  ```SQL
  ASC：升序 (默认)
  
  DESC：降序
  ```


  ​		*注意：

  ​				如果有多个排序条件，则当前边的条件值一样时，才会去判断第二条件。

  

  ​	**3.聚合函数**：将一列数据作为一个整体，进行纵向计算

  ​			1.count：计算个数

  ​					1.一般选择非空的列：主键

  ​					2.count(*)

  ​			2.max：计算最大值

  ​			3.min：计算最小值

  ​			4.sum：计算和

  ​			5.avg：计算平均值

  ​		

  ​		*注意：聚合函数的计算排除null值

  ​				解决方案：

  ​						1.选择不包含null的项

  ​						2.利用IFNULL函数，如：

  ```SQL
  select count(IFNULL(列名,0)) from 表名;
  ```

  

  **4.分组查询**

  ​		1.语法：

  ```SQL
  	group by 分组字段;
  	
  	having 聚合函数;
  ```

  ​		2.注意：

  ​			1.分组之后查询的字段：分组字段，聚合函数

  ​			2.where和having的区别：

  ​					1.where在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来。

  ​					2.where后不可以跟聚合函数，而having可以进行聚合函数的判断。

  ​		3.例子	

  ```SQL
  --在学生student表中，按照性别sex分，分别查询男，女同学的平均分，人数
  	select sex, count(id) from student group by sex;
  
  --在前一个要求下再加一个：数学math分数低于70分的人不参与分组
  	select sex,count(id) from student where math<70 group by sex;
  
  --再在上一个的基础上再加一个：人数要大于两人
  	select sex,count(id) from student where math<70 group by sex having count(id)>2;
  或
  	select sex,count(id) 人数 from student where math<70 group by sex having 人数>2;
  ```

  

  **5.分页查询**

  ​		1.语法：

  ```SQL
  limit 开始的索引 每页查询的条数;
  ```

  ​		2.公式：

  ​				开始的索引 = (当前页码 -1)*每页查询的条数

  

  ```SQL
  --每页显示3条
  	select * from student limit 0,3 ;--第一页
  
  	select * from student limit 3,3 ;--第二页
  
  	select * from student limit 6,3; --第三页
  ```

  ​		3.limit 是一个“方言”，只用于SQL语句中

  

  **6.条件查询**

  ​		1.语法：

  ```SQL
  where子句后跟条件
  ```

  ​		2.运算符：

  ```SQL
  * < , > , <= , >= , = , <>
  * between...and
  * in(集合)
  * like：模糊查询
  	*占位符：
  		*_ :单个任意字符
  		*% :多个任意字符
  * is null
  * and 或 &&
  * or 或 ||
  * not 或 |
  ```

  

  ```SQL
  --查询年龄大于17岁的
  	select * from student where age>17;
  
  --查询年龄再17岁到30岁的
  	select * from student where age between 17 and 30;
  
  --查询年龄为19，22，25的
  	select * from student where age in(19,22,25);
  
  --查询英语成绩(不)为null的人
  	select * from student where English is (not) null;
  ```

  

  ​		like 模糊查询

  ```SQL
  --查询姓陈的有哪些
  	select * from student where name like '陈%';
  
  --查询姓名中第二个字是浩的人
  	select * from student where name like '_浩%';
  
  --查询名字是三个字的人
  	select * from student where name like '___';
  
  --查询名字中包含浩的人
  	select * from student where name like '%浩%';
  ```

  

------

  

  #### 约束

  ​		*概念：对表中的数据进行限定，保证数据的正确性、有效性和完整性

  ​		*分类：

  ​				1.主键约束：primary key

  ​				2.非空约束：not null

  ​				3.唯一约束：unique

  ​				4.外键约束：foreign key

  

  ​		*非空约束：not null

  ```SQL
  --1.创建表，添加非空约束
  	create table stu{
  		id int,
  		name varchar(20) not null --添加了非空约束;
  	}
  
  --2.创建表完后，添加非空约束
  	alter table stu modify name varchar(20) not null;
  
  --3.删除name的非空约束
  	alter table stu modify name varchar(20);
  ```



  ​		*唯一约束：unique

  ```SQL
  --1.创建表，添加唯一约束
  	create table stu{
  		id int,
  		phone_number varchar(20) unique --添加了唯一约束;
  	}
  --注意：MySQL中，唯一约束的限定值可以存在多个null
  
  --2.创建表完后，添加唯一约束
  	alter table stu modify phone_number varchar(20) unique;
  
  --3.删除唯一约束
  	alter table stu drop index phone_number;
  ```



  ​		*主键约束：primary key

​					1.含义：非空且唯一

​					2.一张表只能有一个字段为主键

​					3.主键：一张表中记录的唯一标识

  ​				*注意：

  ```SQL
  --1.创建表，添加主键约束
  	create table stu{
  		id int primary key,
  		name varchar(20);
  	}
  	
  --2.创建完表后，添加主键约束
  	alter table stu modify id int primary key;
  	
  --3.删除主键约束
  	alter tabel stu drop primary key;
  ```

  				4.自动增长

```SQL
		语法：auto_increment
```

​					*注意：

​							1.一般和主键一起使用

​							2.如果某一列值为int型的，可以用auto_increment来完成值的自动增长

```SQL
	--在创建表时，添加主键约束，并完成	主键自动增长
		create table stu{
  		id int primary key auto_increment,
  		name varchar(20);
  	}
  	
  	--添加自动增长
  		alter table stu modify id int;
  	--删除自动增长
  		alter table stu modify id int auto_increment;
```

