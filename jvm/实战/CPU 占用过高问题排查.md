# CPU 占用过高问题排查

系统可生成最大线程数+

```shell
cat /proc/sys/kernel/threads-max
```

进程最大线程数:

    cat /proc/sys/vm/max map count+，

用户最大进程数:

    执行ulimit -u+，结果为1024

jps

查看pid进程内的线程

ps -T -p //

ps -T -p pid | wc -l

实时显示PID进程内的各个线程情况

top -H -p PID
