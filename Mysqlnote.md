#MySQL 基础
###MySQL常见命令
	启动MySQL:net start MySQL
	停止MySQL:net stop MySQL
	进入MySQL: mysql -h localhost -P3306 -u root -p
			或 mysql -u root -p

	1.查看当前所有的数据库
		show databases;
	2.打开指定的库
		use 库名
	3.查看当前库的所有表
		show tables;
	4.查看其他库的所有表
		show table from 库名;
	5.创建表
		create table 表名(
			列名 列类型；
			列名 列类型；
			...
			）
	6.查看表的结构
		desc 表名；
	7.查看服务器的版本
		方式一：登录mysql服务端
		select version()
		方式二：没登陆mysql服务端
		mysql --version
		或 mysql --V
###MySQL的语法规范
	1. 不区分大小写，但是建议关键字大写，表名、列名小写
	2. 每条命名最好用分号结尾
	3. 每条命名根据需求，可以进行缩进或换行
	4. 注释
		单行注释：#注释文字
		单行注释：-- 注释文字
		多行注释：/* 注释文字 */

###DQL语言的学习
	1. 基础查询
		1. use myemployees; #先打开库	
		2. 格式：select 查询列表(表中字段、常量值、表达式、函数) from 表名: 
		3. 查询：select last_name,salary,email from employees;
				select * from employees;
		4. 起别名：select last_name as 名 from employees;
		5. 去重:select distinct department_id from employees;
		6. +号的作用:运算符功能，会把字符串转成数值型
		7. concat():字符串、字符段等进行拼接——>select concat('a','b','c') as 结果:
		8. 按条件表达式筛选
			select * from employees where salary>12000;
		9. 逻辑运算符: and、or、not
			select last_name,salary from employees where salary>=10000 and salary<=20000;
		10. 模糊查询: like 
			% 任意多个字符，包括0个字符
			_ 任意单个字符
			/ 转义字符
			eg:
			select * from employees where last_name like '%a%';
			select * from employees where last_name like '___a___';
			select * from employees where last_name like'_/_a%';
		11. 模糊查询 between and  ——> 10000<=salary<=12000
			select * from employees where salary between 10000 and 12000;
		12. 模糊查询 in
			select last_name,job_id from employees where job_id in('IT_PROT','AD_VP','AD_PRES');
		13. is null、is not null
			select * from employees where salary is null;
		14. 安全等于 <=>
			select * from employees where salary <=> 12000;
		15. ifnull
			ifnull(expr1,expr1)

	2. 条件查询
	3. 排序查询
	4. 常用函数
	5. 分组函数
	6. 分组查询
	7. 连接查询
	8. 子查询
	9. 分页查询
	10. union联合查询