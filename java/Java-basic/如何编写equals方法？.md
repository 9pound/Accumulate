# 如何编写equals方法？

### java规范要求equals方法具有下面特性：

**自反性**：对任何非空引用x，x.equals(x)应该返回true。
**对称性**：对于任何应用x，y，当且仅当y.equals(x)返回true，x.equals(y)也应该返回true。
**传递性**：对于任何x，y和z，如果x.equals(y)返回true，y.equals(z)返回true，x.equals(z)也应该返回true。
**一致性**：如果x和y应用大的对象没有发生变化，反复调用x.equals(y)应该返回同样的结果。

对于任意非空引用x，x.equals(null)返回false。

### 编写一个完美的equals方法的建议

​	(1)显示参数命名为otherObject。

```java 
public boolean equals(Object otherObject)
```

​	(2)检测this与otherObject是否引用同一对象。

```java
if(this == otherObject)	return true;
```

​	(3)检测otherObject是否为空，如果为null，返回false。

```java
if(otherObject  == null) return false;
```

​	(4)比较this与otherObject是否是同一个类。

```java
// 如果equals的语义在每个子类中有所改变，使用getClass()检测
if(getClass() != otherObject.getClass()) return false;
// 如果所有的子类都拥有统一的语义，就使用instanceof检测
if(!(otherObject instanceof ClassName)) return false;
```

​	(5)将otherObject转化为相应的类型变量。

```
ClassName other = (ClassName) otherObject;
```

​	(6)对所有需要比较的域进行比较，==比较基本类型的域，使用equals比较对象域。如果所有的域都匹配，就返回true，否则返回false。

```
return field1 == other.field1
	&&Objects.equals(field2,other.field2)
	&&...
```

