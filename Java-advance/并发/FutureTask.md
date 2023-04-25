# FutureTask

#### 类签名

```java
public class FutureTask<V> implements RunnableFuture<V>
    
public interface RunnableFuture<V> extends Runnable, Future<V> {
/**
 * Sets this Future to the result of its computation
 * unless it has been cancelled.
 */
void run();
}
```

#### 成员变量

```
   /**
     * The run state of this task, initially NEW.  The run state
     * transitions to a terminal state only in methods set,
     * setException, and cancel.  During completion, state may take on
     * transient values of COMPLETING (while outcome is being set) or
     * INTERRUPTING (only while interrupting the runner to satisfy a
     * cancel(true)). Transitions from these intermediate to final
     * states use cheaper ordered/lazy writes because values are unique
     * and cannot be further modified.
     *
     * Possible state transitions:
     * NEW -> COMPLETING -> NORMAL
     * NEW -> COMPLETING -> EXCEPTIONAL
     * NEW -> CANCELLED
     * NEW -> INTERRUPTING -> INTERRUPTED
     */
    
    
    private volatile int state;
    private static final int NEW          = 0;
    private static final int COMPLETING   = 1;
    private static final int NORMAL       = 2;
    private static final int EXCEPTIONAL  = 3;
    private static final int CANCELLED    = 4;
    private static final int INTERRUPTING = 5;
    private static final int INTERRUPTED  = 6;

    /** The underlying callable; nulled out after running */
    private Callable<V> callable;
    /** The result to return or exception to throw from get() */
    private Object outcome; // non-volatile, protected by state reads/writes
    /** The thread running the callable; CASed during run() */
    private volatile Thread runner;
    /** Treiber stack of waiting threads */
    private volatile WaitNode waiters;
```

#### 构造方法

```
public FutureTask(Callable<V> callable) {
    if (callable == null)
        throw new NullPointerException();
    this.callable = callable;
    this.state = NEW;       // ensure visibility of callable
}

/**
 * Creates a {@code FutureTask} that will, upon running, execute the
 * given {@code Runnable}, and arrange that {@code get} will return the
 * given result on successful completion.
 *
 * @param runnable the runnable task
 * @param result the result to return on successful completion. If
 * you don't need a particular result, consider using
 * constructions of the form:
 * {@code Future<?> f = new FutureTask<Void>(runnable, null)}
 * @throws NullPointerException if the runnable is null
 */
public FutureTask(Runnable runnable, V result) {
    this.callable = Executors.callable(runnable, result);
    this.state = NEW;       // ensure visibility of callable
}
```



