# ArrayList和LinkedList和Vector的区别？

## **1、ArrayList**

### 签名

```java
public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

### 数据结构：数组（Object数组）

```java
 /**
     * The array buffer into which the elements of the ArrayList are stored.
     * The capacity of the ArrayList is the length of this array buffer. Any
     * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
     * will be expanded to DEFAULT_CAPACITY when the first element is added.
     */
    transient Object[] elementData; // non-private to simplify nested class access
```

### 初始大小：10


```java
 private static final int DEFAULT_CAPACITY = 10;
```

### 特点：

（1）查询快,增删慢   

（2）允许重复元素，允许null值

（3）按照插入的顺序保存元素，容量是自动增加

（4）擅长随机访问元素，但是在ArrayList中间插入和移除元素时比LinkedList慢

（5）线程不安全的

缺点：

应用：

（1）如果要进行大量的随机访问，就是用ArrayList

## **2、LinkedList**

### 签名

```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```

### 数据结构：双向链表

(java1.6z之前为循环链表，1.7之后取消循环)

```java
 private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```

初始大小：0

```java
transient int size = 0;
```

特点：

（1）查询慢,增删快 （随机访问时较慢）

（2）允许重复元素，允许null值

（3）按照插入的顺序保存元素，容量无限大（只要内存够 ）

（4）拥有使其用做栈，队列，双端队列的方法

缺点：（1）线程不安全

用途：

（1）需要队列，栈的行为

（2）如果经常需要从表中间插入或删除元素，应该使用LInkedList

## **Vector**

### 数据结构（Object数组）

```java
protected Object[] elementData;
```

### 初始大小：10

```java
 public Vector() {
        this(10);
    }
```

### 特点：

（1）因为是数组，特与ArrayList相同

（2）Vector是线程安全的，它的所有方法都是同步的。