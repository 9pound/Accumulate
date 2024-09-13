# HashMap与HashTable的区别？

**HashMap**

数据结构

- 数组+链表+红黑树

初始容量

- 初始化大小为16。之后每次扩充，容量变为原来的2倍。

父类

- AbstractMap

hash方法

- 

线程安全

- 线程不安全

对空键和空值得支持

- Null可以作为键，但是这样的键只有一个
- 可以有一个或多个键所对应的值为空



遍历方式



**Hashtable**

数据结构

- 数组+链表

初始容量

- 默认的初始大小为11，之后每次扩充，容量变为原来的2n+1

父类

- Dictionary

hash方法

- Object.hashCode();

线程安全

- 线程安全，效率低

对空键和空值得支持

- 既不支持Null key也不支持Null value。

遍历方式

参考

https://blog.csdn.net/wangxing233/article/details/79452946

