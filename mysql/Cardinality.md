# Cardinality

Cardinality表示索引中不重复记录的预估值，它不是一个准确值



**低选择性**：字段的取值范围小，如性别，地区字段

**高选择性**：字段的取值范围大，几乎没有重复



## 如何查看索引是否高选择性

```
show index
```

在实际应用中，Cardinality/n_rows_in_table应尽可能地接近1。如果非常小，那么用户需要考虑是否还有必要创建这个索引。故在访问高选择性属性的字段并从表中取出很少一部分数据时，对这个字段添加B+树索引是非常有必要的



## 数据库如何统计Cardinality信息呢？存储引擎中进行

- 通过采样方法来完成

- 在InnoDB存储引擎中，Cardinality统计信息的更新发生在两个操作中:INSERT和UPDATE。

## InnoDB存储引擎内部对更新Cardinality信息的策略

根据前面的叙述，不可能在每次发生INSERT和UPDATE时就去更新Cardinality信息，这样会增加数据库系统的负荷，同时对于大表的统计，时间上也不允许数据库这样去操作。

- 表中1/16的数据已发生过变化。
  - 第一种策略为自从上次统计Cardinality信息后，表中1/16的数据已经发生过变化，这时需要更新Cardinality信息。
- stat_modified_counter>2 000 000 000。
  - 第二种情况考虑的是，如果对表中某一行数据频繁地进行更新操作，这时表中的数据实际并没有增加，实际发生变化的还是这一行数据，则第一种更新策略就无法适用这这种情况。故在InnoDB存储引擎内部有一个计数器stat_modified_counter，用来表示发生变化的次数，当stat_modified_counter大于2 000 000000时，则同样需要更新Cardinality信息。

## 采样的方法采样的过程如下:

- 默认InnoDB存储引擎对8个叶子节点（LeafPage）进行采样取得B+树索引中叶子节点的数量，记为A。
- 随机取得B+树索引中的8个叶子节点。统计每个页不同记录的个数，即为P1，P2，…，P8。
- 根据采样信息给出Cardinality 的预估值:Cardinality=(P1+P2+…+P8)）*A/8。

