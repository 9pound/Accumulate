# Statement与PrepareStatement语句的区别

1、Statement用于执行静态SQL语句，在执行时，必须指定一个事先准备好的SQL语句。
2、PrepareStatement是预编译的SQL语句对象，sql语句被预编译并保存在对象中。被封装的sql语句代表某一类操作，语句中可以包含动态参数“?”，在执行时可以为“?”动态设置参数值。
3、使用PrepareStatement对象执行sql时，sql被数据库进行解析和编译，然后被放到命令缓冲区，每当执行同一个PrepareStatement对象时，它就会被解析一次，但不会被再次编译。在缓冲区可以发现预编译的命令，并且可以重用。
4、PrepareStatement可以减少编译次数提高数据库性能。