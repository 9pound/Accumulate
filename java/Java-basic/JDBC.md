## JDBC 

###  72.什么是 JDBC？ 

JDBC：java数据库连接，编程人员可以通过这个API接口连接到数据库，并使用Sql语句完成对数据库的查找与更新，简单说就是jdbc负责在中间层和后台数据库之间进行通信

### 73.解释下驱动(Driver)在 JDBC 中的角色。 

JDBC 驱动提供了特定厂商对 JDBC API 接口类的实现，驱动必须要提供 java.sql 包下面这些类 的实现：Connection, Statement, PreparedStatement,CallableStatement, ResultSet 和 Driver。 

### 74.Class.forName()方法有什么作用？ 

这个方法用来载入跟数据库建立连接的驱动。 

### 75.PreparedStatement 比 Statement 有什么优势？ 

PreparedStatements 是预编译的，因此，性能会更好。同时，不同的查询参数值， PreparedStatement 可以重用。 

76.什么时候使用 CallableStatement？用来准备 CallableStatement 的方法是什么？ 

CallableStatement 用来执行存储过程。存储过程是由数据库存储和提供的。存储过程可以接 受输入参数，也可以有返回结果。非常鼓励使用存储过程，因为它提供了安全性和模块化。 准备一个 CallableStatement 的方法是： CallableStament.prepareCall(); 


### 77.数据库连接池是什么意思？ 

像打开关闭数据库连接这种和数据库的交互可能是很费时的，尤其是当客户端数量增加的时 候，会消耗大量的资源，成本是非常高的。可以在应用服务器启动的时候建立很多个数据库 连接并维护在一个池中。连接请求由池中的连接提供。在连接使用完毕以后，把连接归还到 池中，以用于满足将来更多的请求。 