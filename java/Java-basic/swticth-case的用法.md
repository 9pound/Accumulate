# swticth-case

switch-case语句格式如下：

```
switch(变量){
case 变量值1:
    //;
    break;
case 变量值2:
    //...;
    break;
  ...
case default:
    //...;
    break;
}
```

swtich()变量类型只能是**int、short、char、byte和enum**类型（**JDK 1.7 之后，类型也可以是String了**）。当进行case判断时，JVM会自动从上到小扫描，寻找匹配的case，可能存在以下情况：

**情况一：若未找到，则执行默认的case。**

```
        int i = 5;
        switch(i){
        case 0:
            System.out.println("0");break;
        case 1:
            System.out.println("1");break;
        case 2:
            System.out.println("2");break;
        default:
            System.out.println("default");break;
        }

输出：default
```

**情况二：当每一个case都不存在break时，JVM并不会顺序输出每一个case对应的返回值，而是继续匹配，匹配不成功则返回默认case。**

```
        int i = 5;
        switch(i){
        case 0:
            System.out.println("0");
        case 1:
            System.out.println("1");
	case 2:
            System.out.println("2");
        default:
            System.out.println("default");
        }
输出：default
```

**情况三：当每一个case都不存在break时，匹配成功后，从当前case开始，依次返回后续所有case的返回值。**

```
        int i = 2;
        switch(i){
        case 0:
            System.out.println("0");
        case 1:
            System.out.println("1");
        case 2:
            System.out.println("2");
        default:
            System.out.println("default");
        }

输出：2
     default
```

**情况四：若当前匹配成功的case不存在break，则从当前case开始，依次返回后续case的返回值，直到遇到break，跳出判断。**

```
        int i = 2;
        switch(i){
        case 0:
            System.out.println("0");
        case 1:
            System.out.println("1");
        case 2:
            System.out.println("2");
        case 3:
            System.out.println("3");break;
        default:
            System.out.println("default");
        }


输出：2
     3
```

### 因此switch case执行时，一定会先进行匹配，匹配成功返回当前case的值，再根据是否有break，判断是否继续输出，或是跳出判断。

还需注意的是case后面只能是常量，可以是运算表达式，但一定要符合正确的类型。不能是变量，即便变量在之前进行了赋值，JVM依然会报错。



A man must be on his own！





[参考](https://www.cnblogs.com/yjd_hycf_space/p/8039379.html)

