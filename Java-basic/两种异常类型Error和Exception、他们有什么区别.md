### 两种异常类型**Error**和**Exception**、他们有什么区别

**Error**

​	含义：描述了Java运行时系统的内部错误和资源耗尽错误（程序不应该抛出这种类型的对象）

**Exception**

- RuntimeException

  含义：程序错误导致的异常属于RunTimeException

  - 错误的类型转换
  - 数组访问越界
  - 访问空指针

- 其他异常

  程序本生没有问题，但由于向IO错误这类问题导致的异常

  - 试图在文件尾部后面读取数据
  - 试图打开 一个不存在的文件
  - 试图根据给定的字符串查找Class对象，而这个字符串表示的类并不存在。

补充：

如果出现RuntimeException异常，那么一定是你的问题