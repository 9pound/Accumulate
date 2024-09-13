# LinkedList源码阅读

### 类签名

```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```

有两个特殊的接口、LinkedList可以作为队列使用。

- AbstractSequentialList （AbstractSequentialList<E> extends AbstractList<E>）
- Deque 

### 成员变量

```java
// 1、初始化容量0
transient int size = 0;
/**
 * Pointer to first node.
 * Invariant: (first == null && last == null) ||
 *            (first.prev == null && first.item != null)
 */
transient Node<E> first;
/**
 * Pointer to last node.
 * Invariant: (first == null && last == null) ||
 *            (last.next == null && last.item != null)
 */
transient Node<E> last;


/**
 * Returns the (non-null) Node at the specified element index.
 */
Node<E> node(int index) {
    // assert isElementIndex(index);

    if (index < (size >> 1)) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

### 构造函数

```java
public LinkedList() {
}
/**
 * Constructs a list containing the elements of the specified
 * collection, in the order they are returned by the collection's
 * iterator.
 *
 * @param  c the collection whose elements are to be placed into this list
 * @throws NullPointerException if the specified collection is null
 */
public LinkedList(Collection<? extends E> c) {
    this();
    addAll(c);
}
```

### 增删改查实现

#### size方法

```java
/**
 * Returns the number of elements in this list.
 *
 * @return the number of elements in this list
 */
public int size() {
    return size;
}


```

#### add方法

```java
public boolean add(E e) {
    linkLast(e);
    return true;
}
/**
 * Links e as last element.
 */
void linkLast(E e) {
    // 1、创建临时指针、记录尾指针的位置
    final Node<E> l = last;
    final Node<E> newNode = new Node<>(l, e, null);
    // 2、将尾指针指向新增节点
    last = newNode;
    // 3、将新节点连接到，旧链表上
    if (l == null)
        first = newNode;
    else
        l.next = newNode;
    size++;
    modCount++;
}
```

#### get方法

```java
// Positional Access Operations

/**
     * Returns the element at the specified position in this list.
     *
     * @param index index of the element to return
     * @return the element at the specified position in this list
     * @throws IndexOutOfBoundsException {@inheritDoc}
     */
public E get(int index) {
    // 1、检查索引是否越界
    checkElementIndex(index);
    // 2、没越界，遍历，找到索引处的元素，返回
    return node(index).item;
}
private void checkElementIndex(int index) {
    if (!isElementIndex(index))
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}
/**
     * Tells if the argument is the index of an existing element.
     */
private boolean isElementIndex(int index) {
    return index >= 0 && index < size;
}

/**
     * Returns the (non-null) Node at the specified element index.
     */
Node<E> node(int index) {
    // assert isElementIndex(index);
    // 有意思、判断索引是在链表的左半边还是右半边。如果是左半边从前往后遍历。如果是右半边，从后往前遍历
    if (index < (size >> 1)) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

### 队列方法

#### remove 方法

```java
/**
 * Retrieves and removes the head (first element) of this list.
 *
 * @return the head of this list
 * @throws NoSuchElementException if this list is empty
 * @since 1.5
 */
public E remove() {
    return removeFirst();
}
    /**
     * Removes and returns the first element from this list.
     *
     * @return the first element from this list
     * @throws NoSuchElementException if this list is empty
     */
    public E removeFirst() {
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return unlinkFirst(f);
    }

```

### 栈方法

#### push方法

```java
/**
 * Pushes an element onto the stack represented by this list.  In other
 * words, inserts the element at the front of this list.
 *
 * <p>This method is equivalent to {@link #addFirst}.
 *
 * @param e th
 e element to push
 * @since 1.6
 */
public void push(E e) {
    addFirst(e);
}
/**
* Inserts the specified element at the beginning of this list.
*
* @param e the element to add
*/
public void addFirst(E e) {
	linkFirst(e);
}
/**
 * Links e as first element.
 */
private void linkFirst(E e) {
    final Node<E> f = first;
    final Node<E> newNode = new Node<>(null, e, f);
    first = newNode;
    if (f == null)
        last = newNode;
    else
        f.prev = newNode;
    size++;
    modCount++;
}

```

#### pop方法

```java
    /**
     * Pops an element from the stack represented by this list.  In other
     * words, removes and returns the first element of this list.
     *
     * <p>This method is equivalent to {@link #removeFirst()}.
     *
     * @return the element at the front of this list (which is the top
     *         of the stack represented by this list)
     * @throws NoSuchElementException if this list is empty
     * @since 1.6
     */
    public E pop() {
        return removeFirst();
    }
        /**
     * Removes and returns the first element from this list.
     *
     * @return the first element from this list
     * @throws NoSuchElementException if this list is empty
     */
    public E removeFirst() {
        final Node<E> f = first;
        if (f == null)
            throw new NoSuchElementException();
        return unlinkFirst(f);
    }
        /**
     * Unlinks non-null first node f.
     */
    private E unlinkFirst(Node<E> f) {
        // assert f == first && f != null;
        final E element = f.item;
        final Node<E> next = f.next;
        f.item = null;
        f.next = null; // help GC
        first = next;
        if (next == null)
            last = null;
        else
            next.prev = null;
        size--;
        modCount++;
        return element;
    }
```

### 扩容方法