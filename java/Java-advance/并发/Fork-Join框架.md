# Fork-Join框架

- 本质：多线程递归操作
- Fork就是把大任务切分为若干子任务并行的执行，
- Join就是合并这些子任务的执行结果



- 有些应用使用了大量线程，但其中大多数都是空闲的，
- 有些应用可能对每个处理器内核分别使用一个线程来完成计算密集型任务如图像或视频处理，fork-join框架专门来支持这一类应用

fork-join框架使用了一种有效的智能方法来平衡可用线程的工作负载，这种方法称为工作密取，每个线程都有一个双端队列来完成任务。一个工作线程将子任务压入其双端队列的对头（只有一个线程可以访问对头，所以不需要加锁），一个工作线程空闲时，他会从另一个双端队列的队尾密取一个任务，由于大的子 任务都在队尾，这种密取很少出现 



**工作窃取算法**：某个线程从其他队列里窃取任务来执行

线程与队列一一对应



API

ForkJoinTask:

 RecursiveAction

 RecursiveTask:

ForkJoinPool:



问题

假设想统计一个数组中有多少个元素满足某个特定的属性，可以将这个数组一分为二，分别对这两部分进行统计，再将结果相加。

#### 如何使用

- 扩展RecursiveTask<T>,如果计算会生成一个为类型为T结果
- 扩展RecursiveAction<T>，如果不生成任何结果



异常处理：

isCompletedAbnormally() :检测任务是否已经抛出异常或已经被取消了

getException():获取异常



实现原理：











参考：https://www.jianshu.com/p/484d9e2a470e

参考：http://ifeve.com/fork-join-1/

参考：https://blog.csdn.net/tyrroo/article/details/81390202

参考：https://blog.csdn.net/codingtu/article/details/88729498?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.edu_weight