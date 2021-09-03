# HashMap与HashSet的区别？

| HashMap                                                | HashSet                                                      |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| 实现了Map接口                                          | 实现Set接口                                                  |
| 存储键值对                                             | 仅存储对象                                                   |
| 调用put（）向map中添加元素                             | 调用add（）方法向Set中添加元素                               |
| HashMap使用键（Key）计算Hashcode                       | HashSet使用成员对象来计算hashcode值， 对于两个对象来说hashcode可能相同， 所以equals()方法用来判断对象的相等性， 如果两个对象不同的话，那么返回false |
| HashMap相对于HashSet较快，因为它是使用唯一的键获取对象 | HashSet较HashMap来说比较慢                                   |