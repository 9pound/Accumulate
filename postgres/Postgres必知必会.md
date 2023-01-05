# Postgres 必知必会





### 约束

#### 主键

#### 外键

#### 唯一约束

#### 非空约束

#### 检查约束

#### 排他约束

### 修改表

#### 添加列

```sql
ALTER TABLE tab_name  ADD COLUMN  column_name  cloumn_type;
```

#### 删除列

```SQL
ALTER TABLE tab_name DROP COLUMN column_name;
#CASCADE移除任何依赖于被删除列的所有东西
ALTER TABLE tab_name DROP COLUMN column_name CASCADE;
```

#### 修改列类型

```postgresql
#最好在修改类型之前先删除该列上所有的约束，然后在修改完类型后重新加上相应修改过的约束
ALTER TABLE tab_name ALTER COLUMN col_name TYPE col_type;
```

#### 重命名列

```postgresql
ALTER TABLE tab_name RENAME COLUMN old_name TO new_name;
```

#### 增加约束

```postgresql
#唯一约束
ALTER TABLE tab_name ADD CONSTRAINT cons_name

#检查约束
ALTER TABLE tab_name ADD CHECK;

#外键约束
ALTER TABLE tab_name ADD FOREIGN KEY() REFERENCES 

#非空约束
ALTER TABLE tab_name ALTER COLUMN col_name SET NOT NULL
```

#### 删除约束

#### 修改列默认值

```postgresql
ALTER TABLE tab_name ALTER COLUMN col_name SET DEFAULT def_value;
```



#### 重命名表

```postgresql
ALTER TABLE old_tab_name TO new_tab_name;
```



### 函数

#### 序列函数

#### 条件函数



#### 格式化函数

##### to_char()

```postgresql
select to_char(now(),'yyyymmdd');
select to_char(now(),'yyyymmdd hh:mi:ss');
```

##### to_date()

##### to_number()

##### to_timestamp()

#### 字符串函数

##### ||

##### length()

##### reverse()

##### lower()

##### upper()

##### position()

##### substring()

##### substr

##### left()

##### right()

##### trim()

##### concat()

##### repeat()

##### replace()



最



## 可重复执行脚本示例





