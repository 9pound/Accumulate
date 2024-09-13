# String、StringBuilder、StringBuffer的区别？

### 概括

String：适用于少量的字符串操作的情况

StringBuilder：适用于单线程下在字符缓冲区进行大量操作的情况

StringBuffer：适用多线程下在字符缓冲区进行大量操作的情况	



### 细节

**都是final类**

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence
    
public final class StringBuilder  extends AbstractStringBuilder
    implements java.io.Serializable, CharSequence    
    
public final class StringBuffer extends AbstractStringBuilder 
     implements java.io.Serializable, CharSequence    
```



String的数组一定会存满

而另外两个不会有count变量记录字符串长度

```java
// String
private final char value[];
/** Cache the hash code for the string */
private int hash; // Default to 0


//AbstractStringBuilder
/**
 * The value is used for character storage.
 */
char[] value;

/**
 * The count is the number of characters used.
 */
int count;
```

StringBuilder、StringBuffer、数组不够的时候会进行扩容

```
private void ensureCapacityInternal(int minimumCapacity) {
    // overflow-conscious code
    if (minimumCapacity - value.length > 0) {
        value = Arrays.copyOf(value,
                newCapacity(minimumCapacity));
    }
}
```

StringBuffer 大部分方法都加了synchronized关键字