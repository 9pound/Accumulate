# Oracle—惊天为人的骚操作

## 表复制

### **复制表结构和数据**

CREATE TABLE table_name AS SELECT * FROM old_table_name;

### **只复制表结构**

CREATE TABLE table_name AS SELECT * FROM old_table_name  WHERE 1=2

### **只复制表数据**

两个表结构一毛一样：

INSERT INTO  table_name select * from old_table_name;

结构不完全一致：

Insert into table_name(column1,column2...) select column1,column2 from old_table_name;