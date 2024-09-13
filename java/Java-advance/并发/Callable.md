# Callable和Future

#### **Callable**

Callable与Runnable类似，但是有返回值。Runnable是一个没有参数和返回值得异步方法

```java
public interface Callable<V>
{
V call() throws Exception;
}
```

#### Future

用来保存异步计算的结果

**FutureTask**

​	包装器类是一种非常便利的机制，可将Callable转换成Future和Runnable，它同时实现二者的接口。

```java
Callable<Integer> myComputation = ....
FutureTask<Integer> task = new FutureTask<Integer>(myComputation );
Thread t = new Thread(task);
t.start();
Ingeger result = task.get();
```

