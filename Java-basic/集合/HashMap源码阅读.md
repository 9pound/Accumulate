# HashMap源码阅读

**类声明**

```java
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable
```

**成员变量**

```java
private static final long serialVersionUID = 362498820763181265L;

static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

static final int MAXIMUM_CAPACITY = 1 << 30;

static final float DEFAULT_LOAD_FACTOR = 0.75f;

static final int TREEIFY_THRESHOLD = 8;

static final int UNTREEIFY_THRESHOLD = 6;

static final int MIN_TREEIFY_CAPACITY = 64;

transient Node<K,V>[] table;

transient Set<Map.Entry<K,V>> entrySet;

transient int size;

transient int modCount;

int threshold;

final float loadFactor;

```

**构造方法**

```

```

**内部数据结构**

数组 + 链表红黑树

数组节点

```java
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        V value;
        Node<K,V> next;

        Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }

        public final K getKey()        { return key; }
        public final V getValue()      { return value; }
        public final String toString() { return key + "=" + value; }

        public final int hashCode() {
            return Objects.hashCode(key) ^ Objects.hashCode(value);
        }

        public final V setValue(V newValue) {
            V oldValue = value;
            value = newValue;
            return oldValue;
        }

        public final boolean equals(Object o) {
            if (o == this)
                return true;
            if (o instanceof Map.Entry) {
                Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                if (Objects.equals(key, e.getKey()) &&
                    Objects.equals(value, e.getValue()))
                    return true;
            }
            return false;
        }
    }
```

**树节点**

```
 static final class TreeNode<K,V> extends LinkedHashMap.Entry<K,V> {
        TreeNode<K,V> parent;  // red-black tree links
        TreeNode<K,V> left;
        TreeNode<K,V> right;
        TreeNode<K,V> prev;    // needed to unlink next upon deletion
        boolean red;
        TreeNode(int hash, K key, V val, Node<K,V> next) {
            super(hash, key, val, next);
        }
}
```



**Hash函数**

```java
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

**HashMap的数据插入原理**

```java
 final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; 
     	Node<K,V> p; 
     	int n, i;
     	// 1、判断数组是不是空的，是空的就扩容
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;
     	// 2、判断要插入元素的位置有没有元素，没有直接新建
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            Node<K,V> e; K k;
            //3、如果插入的位置有元素要考虑三种情况，链表，树
            if (p.hash == hash &&
                 // 3.1 如果要插入的元素元当前节点元素hash码和键值key完全相同，直接覆盖
                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            else if (p instanceof TreeNode)
                // 3.2 如果是树节点，则插入新的树节点
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {
                // 3.3 如果是链表节点
                for (int binCount = 0; ; ++binCount) {
                    // 3.3.4 如果找不到相同的，在链表尾插入新节点。并且如果插入新节点后链表长度大于等于7 将链表转换为红黑树
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    // 3.3.3 如果在链表中找到一个节点它的hash和key与要插入的节点完全一样，覆盖
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            // 4、插入元素之后保存新Value、返回旧Value
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
     	// 5、如果超出HashMap中元素的个数大于threshold、扩容
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
```

**HashMap的get方法**

```java
   public V get(Object key) {
        Node<K,V> e;
        return (e = getNode(hash(key), key)) == null ? null : e.value;
    }

    final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; 
        Node<K,V> first, e; 
        int n; K k;
        // table不为空，且table中有只、对应key的Hash码的位置有值
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            // hash码相同，且可以相同直接返回
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            // hash码不同，或者hash码相同但是key不同
            if ((e = first.next) != null) {
                // 遍历树或者链表，直到找到hash吗和key同时相同的Node节点，返回
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                   
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        // 没找到就返回空2
        return null;
    }

// 不同的key可能会有相同的hash码
// 不同的hash码可能会被散列到同一个位置
```



**HashMap的扩容的原理**

```java
// 主要是干两件事
计算新数组的长度，和threshold
把以前表的内容搬过来


final Node<K,V>[] resize() {
    	// 保存老表的引用、大小、threshold
        Node<K,V>[] oldTab = table;
        int oldCap = (oldTab == null) ? 0 : oldTab.length;
        int oldThr = threshold;
        int newCap, newThr = 0;
    	// 1、如果旧数组的长度大于零
        if (oldCap > 0) {
            // 1.1 如果超过最大容量不在扩容
            if (oldCap >= MAXIMUM_CAPACITY) {
                threshold = Integer.MAX_VALUE;
                return oldTab;
            }
            // 1.2 否则扩大为原来的两倍
            else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                     oldCap >= DEFAULT_INITIAL_CAPACITY)
                newThr = oldThr << 1; // double threshold
        }
    	// 2、如果旧数组的长度小于或等于零，threshold大于零，那么新数组的大小为就的Threshold
        else if (oldThr > 0) // initial capacity was placed in threshold
            // 新数组的大小
            newCap = oldThr;
        else {               // zero initial threshold signifies using defaults
            //3、旧数组的长度小于等于零，且threshold也小于等于零，初始化
            newCap = DEFAULT_INITIAL_CAPACITY;
            newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
        }
    		// 如果数组的长度小于等于零，和thrhold==0 直接初始化
        if (newThr == 0) {
            float ft = (float)newCap * loadFactor;
            newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                      (int)ft : Integer.MAX_VALUE);
        }
        threshold = newThr;
        @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
        table = newTab;
        if (oldTab != null) {
            for (int j = 0; j < oldCap; ++j) {
                Node<K,V> e;
                if ((e = oldTab[j]) != null) {
                    oldTab[j] = null;
                    if (e.next == null)
                        newTab[e.hash & (newCap - 1)] = e;
                    else if (e instanceof TreeNode)
                        ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                    else { // preserve order
                        Node<K,V> loHead = null, loTail = null;
                        Node<K,V> hiHead = null, hiTail = null;
                        Node<K,V> next;
                        do {
                            next = e.next;
                            if ((e.hash & oldCap) == 0) {
                                if (loTail == null)
                                    loHead = e;
                                else
                                    loTail.next = e;
                                loTail = e;
                            }
                            else {
                                if (hiTail == null)
                                    hiHead = e;
                                else
                                    hiTail.next = e;
                                hiTail = e;
                            }
                        } while ((e = next) != null);
                        if (loTail != null) {
                            loTail.next = null;
                            newTab[j] = loHead;
                        }
                        if (hiTail != null) {
                            hiTail.next = null;
                            newTab[j + oldCap] = hiHead;
                        }
                    }
                }
            }
        }
        return newTab;
    }
```



# FAQ

1. 数据结构
2. 为什么 loadFactor 是 0.75？
3. 为什么默认是 16？为什么它的 size 是 2 的 n 次方？
4. hash函数（扰动函数）怎么设计的，为什么要高位参与与运算？与操作
5. 你说泊松分布，什么是泊松分布？
6. 讲下它的扩容机制。
7. 什么时候转红黑树，为什么要转红黑树？，阈值为什么是8
8. 为什么它是线程不安全的，它的哪些方法是线程不安全的？
9. 为什么会造成死循环？1.8 是如何解决这个问题的？
10. 1.8还有三点主要的优化
    1. 数组+链表改成了数组+链表或红黑树；
    2. 链表的插入方式从头插法改成了尾插法，简单说就是插入时，如果数组位置上已经有元素，1.7将新元素放到数组中，原始节点作为新节点的后继节点，1.8遍历链表，将元素放置到链表的最后；
    3. 扩容的时候1.7需要对原数组中的元素进行重新hash定位在新数组的位置，1.8采用更简单的判断逻辑，位置不变或索引+旧容量大小；
    4. 在插入时，1.7先判断是否需要扩容，再插入，1.8先进行插入，插入完成再判断是否需要扩容；
    
11. 为什么重写equals时也要同时覆盖hashcode？
12. 那HashMap是线程安全的吗，怎么解决这个线程不安全的问题？
13. HashTable、Collections.synchronizedMap、以及ConcurrentHashMap
14. HashMap内部节点是有序的吗？
15. 遍历方式keySet()、values()、entirySet()
16. 为什么它是线程不安全的，它的哪些方法是线程不安全的？
17. 为什么会造成死循环？
18. 1.8 是如何解决这个问题的？



https://blog.csdn.net/zhengwangzw/article/details/104889549?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight