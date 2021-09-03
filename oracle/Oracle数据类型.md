Oracle数据类型

提示：允许为空的列定义在后面。

![1554104936339](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\1554104936339.png)

varchar2：变长字符类型，最长32767，最大列宽4000；

char：定长字符类型，如果赋予该变量的字面值较小，则使用空格填充。不给参数默认为一个字节，最大为2000个字节

number：存储任何大小的整数和浮点数。可以限制长度和精度。

long : 用于存储变长字符串，最大长度为2GB，通常用来存储文本，字符数组，以及各种文档。

- 限制：不能在表达式、函数以及where、group by 等特定语句中引用 LONG类型的数据列。

long raw: 用于存储原始的二进制变量数据，最大值为2GB。

- 不能使用DML语句来直接查询或进行其他操作

boolean : 只有三个值true、false、null。

pls_integer(plsql环境中与类型binary_integer相同)：带符号的整数数据类型

- 特点：直接使用硬件存储和计算，相对于number具有存储空间小、计算速度快的优势。



date：日期类型，存储定长的日期值

timestamp：相对于date，timestamp更精确。

anchored: 随着对象中数据的变化而作相应的变化。

- 特点：anchored会随着表中列类型的变化而变化。
- 语法：

```plsql
变量名 对象类型属性%type

var_name employees.first_name%type;
var_salary enployees.salary%type;、

declare
	var_name employees.first_name%type;
	var_salary employees.salary%type;
begin 
	select first_name,salary into var_name,var_salary
	from employees where employee_id = 206;
	dbms_output.put_line('var_name is '||var_name);
	dbms_output.put_line('var_salary  is '||var_salary);
end;
.
```

### 自定义数据类型

无约束的自定义子类型

语法

```plsql
subtype 子类型名称 is 基类型

declare 
	subtype mynumber is number;
	var_num1 mynumber(6,2):=100;
	var_num2 mynumber(8,2):=200;
	var_num3 mynumber(8,2):=300;
	var_max_num constant mynumber(8,2) := 300000.00;
	subtype mynatural is natural;
	var_nat1 mynatural := 1;
	var_nat2 mynatural := 2;
	var_nat3 mynatural := 3;
begin
	var_num1 := var_num1 + var_nat1;
	var_num2 := var_num2 + var_nat2;
	var_num3 := var_num3 + var_nat3;
	
	dbms_output.put_line('var_num1 is : '||to_char(var_num1));
	dbms_output.put_line('var_num2 is : '||to_char(var_num2));
	dbms_output.put_line('var_num3 is : '||to_char(var_num3));
end;
.
/
	
```

有约束的自定义子类型

语法

```plsql
subtype 子类型 is 基类型
{precision [,scale] | range low_value..high_value}[not null]

declare
	subtype balance is number(8,2);
	checking_account balance;
	savings_account balance;
begin 
	checking_account := 2000.00;
	savings_account := 1000000.00; --不满足类型条件，报错
end;
	
	
declare 
	subtype under10 is pls_integer range 0..9;
	subtype between1099 is pls_integer range 10..99;
	subtype under100 is pls_integer range 0..99;
	d10 under10 := 10;
	d1099 between1099 := 35;
	u100 under100;]
begin
	u100 := d10;
	u100 := d1099;
	d199 := d10; --不满足条件，报错
end;
```

