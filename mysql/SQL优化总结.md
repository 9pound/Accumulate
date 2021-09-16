# SQL优化总结

## 查询优化

### SELECT 

1. 任何地方都不要使用 select * from t 
2. 可以把子查询优化为 join 操作

### JOIN

1. join表建议不超过 5 个

### WHERE

1. 应尽量避免在 where 子句中使用!=或<>操作符
2. 应尽量避免在 where 子句中对字段进行 null 值判断
3. 避免隐式转换
4.  or 使用union all 代替
5. in 和 not in  使用between代替或者exists 
6. 应尽量避免在 where 子句中对字段进行表达式或者函数操作



## 索引优化

- 首先应考虑在 where 及 ORDER BY、GROUP BY、DISTINCT涉及的列上建立索引







## Explain

![image-20210917014641675](E:\Accumulate\mysql\SQL优化总结.assets\image-20210917014641675.png)



**id：**查询的执行循序

**table** 查询了那些表

**select_type：**查询类型

- SIMPLE:简单SELECT查询，查询中不包含子查询或者UNION
- PRIMARY:查询中包含任何复杂的子部分，最外层的查询
- SUBQUERY：SELECT或WHERE中包含的子查询部分
- DERIVED：在FROM中包含的子查询被标记为DERIVER(衍生)， MySQL会递归执行这些子查询，把结果放到临时表中
- UNION：若第二个SELECT出现UNION，则被标记为UNION, 若UNION包含在FROM子句的子查询中，外层子查询将被标记为DERIVED
- UNION RESULT：从UNION表获取结果的SELECT

**type：**访问类型

system>const>eq_ref>ref>fulltext>ref_or_null>index_merge>unique_subquery>index_subquery>range>index>ALL

- system：表只有一行记录（等于系统表），这是const类型的特例，平时不会出现
- const：如果通过索引依次就找到了，const用于比较主键索引或者unique索引。 因为只能匹配一行数据，所以很快。如果将主键置于where列表中，MySQL就能将该查询转换为一个常量
- eq_ref：唯一性索引扫描，对于每个索引键，表中只有一条记录与之匹配。常见于主键或唯一索引扫描
- ref：非唯一性索引扫描，返回匹配某个单独值的所有行。本质上也是一种索引访问，它返回所有匹配 某个单独值的行，然而它可能会找到多个符合条件的行，所以它应该属于查找和扫描的混合体
- range：只检索给定范围的行，使用一个索引来选择行。key列显示使用了哪个索引，一般就是在你的where语句中出现between、<、>、in等的查询，这种范围扫描索引比全表扫描要好，因为只需要开始于缩印的某一点，而结束于另一点，不用扫描全部索引
- index：Full Index Scan ，index与ALL的区别为index类型只遍历索引树，这通常比ALL快，因为索引文件通常比数据文件小。 （也就是说虽然ALL和index都是读全表， 但index是从索引中读取的，而ALL是从硬盘读取的）
- all：Full Table Scan，遍历全表获得匹配的行

**possible_keys：**可能用到的索引

**key：**实际用到的索引

**rows：**查询了多少行

**Extra：**包含不适合在其他列中显示但十分重要的额外信息：
Using filesort： 说明MySQL会对数据使用一个外部的索引排序，而不是按照表内的索引顺序进行读取。MySQL中无法利用索引完成的排序操作称为“文件排序”

- Using temporary： 使用了临时表保存中间结果，MySQL在对查询结果排序时使用临时表。常见于排序order by和分组查询group by
- Using index： 表示相应的SELECT操作中使用了覆盖索引（Covering Index），避免访问了表的数据行，效率不错。 如果同时出现using where，表明索引被用来执行索引键值的查找； 如果没有同时出现using where，表明索引用来读取数据而非执行查找动作 覆盖索引（Covering Index）： 理解方式1：SELECT的数据列只需要从索引中就能读取到，不需要读取数据行，MySQL可以利用索引返回SELECT列表中 的字段，而不必根据索引再次读取数据文件，换句话说查询列要被所建的索引覆盖 理解方式2：索引是高效找到行的一个方法，但是一般数据库也能使用索引找到一个列的数据，因此他不必读取整个行。 毕竟索引叶子节点存储了他们索引的数据；当能通过读取索引就可以得到想要的数据，那就不需要读取行了，一个索引 包含了（覆盖）满足查询结果的数据就叫做覆盖索引 注意： 如果要使用覆盖索引，一定要注意SELECT列表中只取出需要的列，不可SELECT *, 因为如果所有字段一起做索引会导致索引文件过大查询性能下降
  impossible where： WHERE子句的值总是false，不能用来获取任何元组*
- 
  select tables optimized away： 在没有GROUP BY子句的情况下基于索引优化MIN/MAX操作或者对于MyISAM存储引擎优化COUNT(*)操作， 不必等到执行阶段再进行计算，查询执行计划生成的阶段即完成优化
- distinct： 优化distinct操作，在找到第一匹配的元祖后即停止找同样值的操作

