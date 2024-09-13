# Runnable&Callable

### Runnable

- 函数式接口

```
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```



### **Callable**

- 函数式接口
- Callable与Runnable类似，但是有返回值。Runnable是一个没有参数和返回值得异步方法


```java
@FunctionalInterface
public interface Callable<V> {
    /**
     * Computes a result, or throws an exception if unable to do so.
     *
     * @return computed result
     * @throws Exception if unable to compute a result
     */
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





