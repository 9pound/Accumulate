###### SQL奇淫巧技

列转行

group_concat

行转列

某个聚合函数配合case when 使用





**HAVING**

不结合GROUP BY 使用 HAVING语句

能写在 WHERE 子句里的条件不要写在 HAVING 子句里



**自连接**

查看编号是否连续？

```
select '存在缺失的编号' as gap
	from SeqTbl 
having count(*) <> MAX(seq);
```

实现排序



**CASE WHEN**

1. 对当前工资为 1 万以上的员工，降薪 10%。
2. 对当前工资低于 1 万的员工，加薪 20%。

```text
一般的写法，会有问题
--条件1
UPDATE Salaries
SET salary = salary * 0.9 WHERE salary >= 10000;
--条件2
UPDATE Salaries
SET salary = salary * 1.2
WHERE salary < 10000;

特殊的写法
UPDATE salaries 
SET salary = CASE WHEN salary >= 10000 THEN salray*0.9 WHEN  salary < 10000 THEN salary * 1.2
ELSE salary END;
```

**IN**

需要对多个字段使用 IN 谓词时，将它们汇总到一处

某些情况下使用EXISTS 代替IN操作







**不命中索引的情况**



如果发生了隐式类型转换可能不会命中索引

如下的几种否定形式不能用到索引：

- != & <>
- NOT IN
- NOT LIKE
- NOT EXTSTS

```text
SELECT *
  FROM SomeTable
 WHERE col_1 <> 100;
```

可以改成以下形式

```text
SELECT *
  FROM SomeTable
 WHERE col_1 > 100 or col_1 < 100;
```