# PL/SQL(Procedural Language/SQL)

1、什么是PL/SQL

Oracle引入的一种过程化编程语言构建于sql之上，用来编写包含sql的语句的程序，

2、与普通sql的区别？

sql：是一次只向服务器发一条语句。

PL/SQL：一次向服务器发送送多条语句，减少系统开销，提高系统性能。

3、plsql的



4、PL/SQL的语句块的基本结构

- 块头区
- 声明区
- 执行区
- 异常区

### **块头区**  PL/SQL程序块的类型、名称、参数、返回值

语法：

```
Pragram_type program_name ([parameter_name in/out/in out type specs]...)

[return datatye]
```

示例：

```
create or replace function fun_test(f float)
return float

create or replace procedure pro_test(name in varchar2)
```

参数的类型 IN,OUT,IN OUT

程序类型 ：FUNCTION,PROCEDURE,PACKAGE(FUNCTION函数必须有返回值，可以在任意位置使用RETURN来返回)

```
//定义function
create or replace function fun_test(f float)
return float
//定义过程
create or replace procedure pro_test(name IN varchar2)
```

### **声明区** ：用来声明变量

**：=** 赋值运算符

**default** 为变量或常量赋值

**CONSTANT**：表示一个变量一旦赋值，在程序运行期间将保持不变 

**语法：**

```plsql
--声明区在块头区的后面，可以使用is关键字说明后面的是声明区，也可以使用DECLARE关键字
--在任意位置声明变量
declare
	var_name [constrant] datatype [(constraint)] [;=value];

--在块头区后面声明变量	
is
	var_name [constrant] datatype [(constraint)] [;=value];
```

**示例**

```pLsql
声明一个字符变量
var_name varchar2(20);
声明一个带约束的字符前两
var_name varchar2(20) not null;
声明一个常量且赋初值
var_name constant varchar2(20) := 'china';
声明一个变量且使用DEFAULT关键字
var_name integer default 3.1415926;
```

### **执行区**

语法

```plsql
begin --标识执行区开始
	--logic statements
end;  --标识执行区结束
```

### **异常区**

语法

```PLSQL
EXCEPTION
	WHEN exception_name1
	THEN
		handl error1
	WHEN exception_name2
	THEN	
		handl error2
	WHEN other_exception
		default error handling;
```

**例子**

```plsql
create or replace procedure pro_test (f float)
is
	var_name varchar2(20);
	exception1 EXCEPTION; --自定义异常
BEGIN 
	statement1;
    BEGING
            statement2;
            raise exception1
        EXCEPTION	-- statement2 抛出的异常在这里处理 注意这里有一个begin end 区块
            WHEN exception1
        Handling errors;
     END;
     statement3;
     EXCETION --statement1和statement2 抛出的异常在这里处理
     	WHEN OTHERS
     		handling errors;
END;
	
```

**具体的例子**

1. 让SQLplus显示输出；(数据缓存并显示)

   ```plsql
   set serveroutput on --把服务器返回的数据缓存到内存，PL/SQL语句块执行结束后显示在屏幕上
   set serveroutput on size 4000;
   set serveroutput on off;
   ```

2. 编写PL/SQL程序

```plsql
DECLARE	
	var_first_name varchar2(30);
	var_last_name  varchar2(30);
BEGIN	
	select first_name,last_name 
		into var_first_name,var_last_name	
	from employees
	where employee_id = 168;

	dbms_output.put_line('var_first_name is : '||var_first_name);
	dbms_output.put_line('var_last_name is : '||var_last_name);

	EXCEPTION 
			WHEN NO_DATA_FOUND THEN
			dbms_output.put_line('no data found');
END;
.		--表示语句块的结束
/		--表示执行PL/SQL语句块
```

PL/SQL 语句块执行过程

语法检查->替代->生成伪代码

PL/SQL 与 SQL 的区别

### 替代变量的使用



```plsql
替代变量是干嘛的？
	替代变量用来接收用户的输入信息
替代变量可以以&开头，也可以使用&&开头，有什么区别？
	&对于名称相同的替代变量要求输入两次
	&&对于名称相同的替代变量

declare 	
	var_first_name varchar2(30);
	var_last_name varchar2(30);
	var_employee_id number := &b_employee_id;
BEGIN	
	select first_name,last_name
	into var_first_name,var_last_name
	from employees 
	where employee_id = var_employee_id;
	dbms_output.put_line('var_first_name is :'||var_first_name);
	dbms_output.put_line('var_last_name is : '||var_last_name);
end;

```

```
set varify off；
```

替代变量以&开头或者使用“&&”开头，区别是“&&”开头的替代变量表示：只要在当前PL/SQL块中定义相同的替代变量，执行PL/SQL 块时，只需要输入一次该替代变量的值。

```plsql
begin  
	dbms_output.put_line('Tom is from : '||'&country');
	dbms_output.put_line('Jerry is from : '||'&country');
end;
.
/

begin  
	dbms_output.put_line('Tom is from : '||'&&country');
	dbms_output.put_line('Jerry is from : '||'&&country');
end;
.
/
```



