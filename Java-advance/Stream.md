# Stream

特点

允许你以声明式的方式处理数据集合（遍历数据集的高级迭代器），还可以进行并行处理。

声明式：说明想要完成什么，而不是说明如何实现

本质：



特点

- 流水线
- 内部迭代



流与集合的区别



什么时候进行计算

流按需计算。

集合是急切创建





只能遍历一次，当一个流遍历完后，我们就说这个流被消费掉了



内部迭代和外部迭代

区别在于，是有用户做循环，还是API帮你做循环。



流操作的分类

- 中间操作：
- 终端操作：从流的流水线中产生结果

短路技巧

循环合并





## StreamAPI

### 筛选

### 切片

### 截断

### 跳过

映射

扁平化

查找

匹配

归约

### 数值流

求和

最大最小值

## 构建流

分组

分区

收集器



