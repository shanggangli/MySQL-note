# MySQL 基础
	数据库的好处
		1. 可以持久化数据到本地
		2. 结构化查询
### MySQL常见命令
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
### MySQL的语法规范
	1. 不区分大小写，但是建议关键字大写，表名、列名小写
	2. 每条命名最好用分号结尾
	3. 每条命名根据需求，可以进行缩进或换行
	4. 注释
		单行注释：#注释文字
		单行注释：-- 注释文字
		多行注释：/* 注释文字 */

### DQL语言的学习
	1. 基础查询、条件查询
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
		13. is null、is not null   判断某字段或表达式是否为null
			select * from employees where salary is null;
		14. 安全等于 <=>
			select * from employees where salary <=> 12000;
		15. 不等于 <>
		16. ifnull
			ifnull(expr1,expr1)
	2. 排序查询
		select 查询列表 
		from 表 
		【where 筛选条件】 
		order by 排序列表 【asc|desc】	#默认是升序
		order by 子句中可以支持单个字段、多个字段、表达式、函数、别名
		
		案例：
		1. select * from employees order by salary desc; #降序
		2. select * from employees where department id>=90 order salary;
		3. select * from employees order by salary asc,employee_id desc;
	3. 常用函数
		select 函数名(实参列表) 【from 表】;
		字符函数：concat、lenght、ifnull、upper、lower、substr、substring、instr、trim、lpad、rpad、replace等等
		数学函数: round() 四舍五入、ceil() 向上取整、floor() 向下取整、truncate() 截断、mod() 取余
		日期函数： now()、curdate()、curtime()、year()、month()
				str_to_date('9-13-1999','%m-%d-%Y') 1999-9-13 将字符转化成日期
				date_format('2020/6/6','%Y年%m月%d日') 2020年6月6日 将日期转化成字符
				datediff:返回两个日期相差的天数
		if、if else函数：if(X,X,X)
		case函数:case 要判断的字段或表达式 when 常量 then 要显示的值或语句 end；
	4. 分组函数(统计函数)
		sum、avg一般处理数值型
		max、min、count可以处理任何类型
		以上的函数都忽略null值
		1. sum(): select sum(salary) from employees;
		2. avg(): select avg(salary) from employees;
		3. max(): select max(salary) from employees;
		4. min(): select min(salary) from employees;
		5. count(): select count(salary) from employees;
		6. 合在一起用： select sum(salary) as 求和 avg(salary) as 平均from employees;
		7. count(*) 查询列数
	5. 分组查询
		select column,group_funntion(colums)
		from	table
		[where condition]
		[group by group_by_expression]
		[order by column];
		where 一定要放在from后面
		案例：
		select max(salary),job_id 
		from employees 
		where commission_pct is not null 
		group by job_id 
		having max(salary)>12000;
	6. 连接查询(多表查询)
		内连接:等值连接、非等值连接、自连接
		外连接:左外、右外、全连
		交叉连接

		sql99语法：
			select 查询列表
			from 表1 别名 【连接类型】
			join 表2 别名
			on 连接条件
			【where 筛选条件】
			【group by 分组】
			【having 筛选条件】
			【order by 排序列表】
		分类：
			内连接：inner
			外连接：      应用于一张表有，另一张无
				左外：left  【outer】
				右外：right	【outer】
				全外：full	【outer】
			交叉连接：cross
		
		案例：
			1. 查询哪个城市没有部门
			2. 查询部门名为SAL或IT的员工信息
			
	7. 子查询   可以理解成英语里的从句！ (禁止套娃！)
	
	8. 分页查询
	9. union联合查询
		用于多表，并且多个表并没有直接连接关系
		语法：
			查询语句1
			union
			查询语句1
			union
		特点：
			1. 要求多条查询语句的列数是一致的
			2. 查询语句的顺序要一致
			3. union关键字会去重，union all 可以包含重复部分
### DML语言
	1. 插入语句(insert)
		1. insert into 表名(列...) values (值1...);
		
	2. 修改语句(undate)
		单表查询：
		1. updata 表名 set 列=新值,... where 筛选条件;
		多表查询：
		2. update 表1 别名 inner|left|right join 表2 别名 on 连接条件 set 列=值,... where 筛选条件;
		
	3. 删除语句(delete)
		1. delete from 表名 where 筛选条件
		2. truncate table 表名
