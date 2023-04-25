# javap



一般常用的是-v -l -c三个选项。

javap -l ：会输出行号和本地变量表信息；
javap -c ：会对当前class字节码进行反编译生成汇编代码；
javap -v： class字节码文件中除了包-c参数包含的内容外，还会输出行号、局部变量表信息、常量池等信息；





  -c           输出类中各方法的未解析的代码，即构成java字节码的指令

  -classpath <pathlist>    指定javap用来查找类的路径。目录用：分隔

  -extdirs <dirs>       覆盖搜索安装方式扩展的位置，扩展的缺省位置为jre/lib/ext

  -help          输出帮助信息

  -J<flag>         直接将flag传给运行时系统

  -l            输出行及局部变量表

  -public          只显示public类及成员

  -protected        只显示protected和public类及成员。

  -package         只显示包、protected和public类及成员，，这是缺省设置

  -private          显示所有的类和成员

  -s            输出内部类型签名

  -bootclasspath <pathlist>   指定加载自举类所用的路径，如jre/lib/rt.jar或i18n.jar

  -verbose         打印堆栈大小、各方法的locals及args参数，以及class文件的编译版本



## javap -v

```shell
$ javap -v Synchronized.class
Classfile /E:/in-action/concurrency-in-action/out/production/concurrency-in-action/the_art_of_java_concurrency_programming/chapter4/Synchronized.class
  Last modified 2023▒▒4▒▒14▒▒; size 716 bytes
  SHA-256 checksum ea6522859977d11d2cf036ac95eaae3601af55021f0197c531e0cb2506c7c4b8
  Compiled from "Synchronized.java"
public class the_art_of_java_concurrency_programming.chapter4.Synchronized
  minor version: 0
  major version: 61
  flags: (0x0021) ACC_PUBLIC, ACC_SUPER
  this_class: #7                          // the_art_of_java_concurrency_programming/chapter4/Synchronized
  super_class: #2                         // java/lang/Object
  interfaces: 0, fields: 0, methods: 4, attributes: 1
Constant pool:
   #1 = Methodref          #2.#3          // java/lang/Object."<init>":()V
   #2 = Class              #4             // java/lang/Object
   #3 = NameAndType        #5:#6          // "<init>":()V
   #4 = Utf8               java/lang/Object
   #5 = Utf8               <init>
   #6 = Utf8               ()V
   #7 = Class              #8             // the_art_of_java_concurrency_programming/chapter4/Synchronized
   #8 = Utf8               the_art_of_java_concurrency_programming/chapter4/Synchronized
   #9 = Methodref          #7.#10         // the_art_of_java_concurrency_programming/chapter4/Synchronized.func1:()V
  #10 = NameAndType        #11:#6         // func1:()V
  #11 = Utf8               func1
  #12 = Utf8               Code
  #13 = Utf8               LineNumberTable
  #14 = Utf8               LocalVariableTable
  #15 = Utf8               this
  #16 = Utf8               Lthe_art_of_java_concurrency_programming/chapter4/Synchronized;
  #17 = Utf8               main
  #18 = Utf8               ([Ljava/lang/String;)V
  #19 = Utf8               args
  #20 = Utf8               [Ljava/lang/String;
  #21 = Utf8               StackMapTable
  #22 = Class              #20            // "[Ljava/lang/String;"
  #23 = Class              #24            // java/lang/Throwable
  #24 = Utf8               java/lang/Throwable
  #25 = Utf8               func2
  #26 = Utf8               SourceFile
  #27 = Utf8               Synchronized.java
{
  public the_art_of_java_concurrency_programming.chapter4.Synchronized();
    descriptor: ()V
    flags: (0x0001) ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 3: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       5     0  this   Lthe_art_of_java_concurrency_programming/chapter4/Synchronized;

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: (0x0009) ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=3, args_size=1
         0: ldc           #7                  // class the_art_of_java_concurrency_programming/chapter4/Synchronized
         2: dup
         3: astore_1
         4: monitorenter
         5: aload_1
         6: monitorexit
         7: goto          15
        10: astore_2
        11: aload_1
        12: monitorexit
        13: aload_2
        14: athrow
        15: invokestatic  #9                  // Method func1:()V
        18: return
      Exception table:
         from    to  target type
             5     7    10   any
            10    13    10   any
      LineNumberTable:
        line 5: 0
        line 7: 5
        line 8: 15
        line 9: 18
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0      19     0  args   [Ljava/lang/String;
      StackMapTable: number_of_entries = 2
        frame_type = 255 /* full_frame */
          offset_delta = 10
          locals = [ class "[Ljava/lang/String;", class java/lang/Object ]
          stack = [ class java/lang/Throwable ]
        frame_type = 250 /* chop */
          offset_delta = 4

  public static synchronized void func1();
    descriptor: ()V
    flags: (0x0029) ACC_PUBLIC, ACC_STATIC, ACC_SYNCHRONIZED
    Code:
      stack=0, locals=0, args_size=0
         0: return
      LineNumberTable:
        line 13: 0

  public synchronized void func2();
    descriptor: ()V
    flags: (0x0021) ACC_PUBLIC, ACC_SYNCHRONIZED
    Code:
      stack=0, locals=1, args_size=1
         0: return
      LineNumberTable:
        line 17: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       1     0  this   Lthe_art_of_java_concurrency_programming/chapter4/Synchronized;
}
SourceFile: "Synchronized.java"

```

