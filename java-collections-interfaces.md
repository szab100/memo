###Java Collections Framework interfaces.
---

**Collection** is the root interface in the collection hierarchy (package java.util).

```Java
public interface Collection<E> extends Iterable<E> {

    // Query Operations:
    int size();
    boolean isEmpty();
    boolean contains(Object o);
    Iterator<E> iterator();

    // Modification Operations:
    boolean add(E e);
    boolean remove(Object o);

    // Array Operations:
    Object[] toArray();
    <T> T[] toArray(T[] a);

    // Bulk Operations:
    boolean containsAll(Collection<?> c);
    boolean addAll(Collection<? extends E> c);
    boolean removeAll(Collection<?> c);
    boolean retainAll(Collection<?> c);
    void clear();

    // Comparison and hashing:
    boolean equals(Object o);
    int hashCode();
}
```
---

**Iterator** points at the next unseen element in a collection.

```Java
public interface Iterator<E> {
 
    boolean hasNext();
    E next();
    void remove();
}
```

---

**Set** is a collection that contains **no duplicate** elements. The `Set` interface contains *only* methods inherited from `Collection` and adds the restriction that duplicate elements are prohibited. A set uses the `equals` method of its elements to determine if two elements are the same (logical equality).


```Java
public interface Set<E> extends Collection<E> { }
```
---

**SortedSet** is a `Set` that maintains its elements in ascending order, sorted according to the elements' natural ordering or according to a `Comparator` provided at `SortedSet` creation time.

```Java
public interface SortedSet<E> extends Set<E> {

    // Comparator access:
    Comparator<? super E> comparator();

    // Range-view operations:
    SortedSet<E> subSet(E fromElement, E toElement);
    SortedSet<E> headSet(E toElement);
    SortedSet<E> tailSet(E fromElement);

    // Endpoints:
    E first();
    E last();
}
```
---

The **List** is an ordered `Collection` (a sequence). You can retrieve elements from a `List` by their exact position. 

```java
interface List extends Collection {

    // Positional Access Operations:
    E get(int index);
    E set(int index, E element);
    void add(int index, E element);
    E remove(int index);

    // Search Operations:
    int indexOf(Object o);
    int lastIndexOf(Object o);

    // List Iterators:
    ListIterator<E> listIterator();
    ListIterator<E> listIterator(int index);

    // View:
    List<E> subList(int fromIndex, int toIndex);
}
```
---

**ListIterator** allows to traverse the list in either direction, modify the list during iteration, and obtain the current position of the iterator.

```java
public interface ListIterator<E> extends Iterator<E> {

    // Query Operations:
    boolean hasNext();
    E next();
    boolean hasPrevious();
    E previous();
    int nextIndex();
    int previousIndex();

    // Modification Operations:
    void remove();
    void set(E e);
    void add(E e);
}
```
---

**List Algorithms**

Most polymorphic algorithms in the `Collections` class apply specifically to `List`. 

- `sort` — sorts a List using a merge sort algorithm, which provides a fast, stable sort. (A stable sort is one that does not reorder equal elements.)
- `shuffle` — randomly permutes the elements in a List.
- `reverse` — reverses the order of the elements in a List.
- `rotate` — rotates all the elements in a List by a specified distance.
- `swap` — swaps the elements at specified positions in a List.
- `replaceAll` — replaces all occurrences of one specified value with another.
- `fill` — overwrites every element in a List with the specified value.
- `copy` — copies the source List into the destination List.
- `binarySearch` — searches for an element in an ordered List using the binary search algorithm.
- `indexOfSubList` — returns the index of the first sublist of one List that is equal to another.
- `lastIndexOfSubList` — returns the index of the last sublist of one List that is equal to another.

---

**Map Interface**

A **Map** is an object that maps keys to values. It models the mathematical function abstraction:  
1. A map cannot contain duplicate keys.  
2. Each key can map to at most one value. 

```java
public interface Map<K,V> {

    // Query Operations:
    int size();
    boolean isEmpty();
    boolean containsKey(Object key);
    boolean containsValue(Object value);
    V get(Object key);

    // Modification Operations:
    V put(K key, V value);
    V remove(Object key);

    // Bulk Operations:
    void putAll(Map<? extends K, ? extends V> m);
    void clear();

    // Views:
    Set<K> keySet();
    Collection<V> values();
    Set<Map.Entry<K, V>> entrySet();

    interface Entry<K,V> {

        K getKey();
        V getValue();
        V setValue(V value);
        boolean equals(Object o);
        int hashCode();
    }

    // Comparison and hashing:
    boolean equals(Object o);
    int hashCode();
}
```

---

**SortedMap Interface**

A **SortedMap** is a `Map` that provides a total ordering on its keys. The map is sorted according to the keys' natural ordering, or according to a `Comparator` provided at the time of the `SortedMap` creation.

```java
public interface SortedMap<K,V> extends Map<K,V> {

    // Comparator access:
    Comparator<? super K> comparator();

    // Range-view operations:    
    SortedMap<K,V> subMap(K fromKey, K toKey);
    SortedMap<K,V> headMap(K toKey);
    SortedMap<K,V> tailMap(K fromKey);

    // Endpoints:
    K firstKey();
    K lastKey();

    // The Iterator of the collection views traverse the collections in order:
    Set<K> keySet();
    Collection<V> values();
    Set<Map.Entry<K, V>> entrySet();
}
```

---

**Object Ordering**:
- Comparable Interface
- Comparator

The **Comparable Interface** consists of one `compareTo` method that returns a negative integer, 0, or a positive integer depending on whether the receiving object is less than, equal to, or greater than the specified object. 

```java
public interface Comparable<T> {

    public int compareTo(T o);
}
```

A **Comparator** is an object that encapsulates an ordering. To order a sorted collection, such as `TreeSet`, use a `Comparator` that is compatible with `equals`, i.e. the only elements seen as equal when using `compare` are those that are also seen as equal when compared using `equals`.


```java
public interface Comparator<T> {

    int compare(T o1, T o2);
}
```

---

**Queue Interface**

A **Queue** is a collection for holding elements prior to processing. 

`Queue` ordering:
- FIFO (first-in-first-out) - typical implementations (`LinkedList`)
- Comparator or the elements' natural ordering - *priority queues* 

`Queue` methods:

Type of Operation | Throws exception | Returns `null` or `false`
:--:|:--:|:--:
Insert | add(e) | offer(e)
Remove | remove() | poll()
Examine | element() | peek()

```java
public interface Queue<E> extends Collection<E> {

    boolean add(E e);
    boolean offer(E e);

    E remove();
    E poll();

    E element();
    E peek();
}
```

---

**Deque Interface**

- Deque is short for "double ended queue" (pronounced "deck").  
- A linear collection with element insertion and removal at *both* ends.  
- `Deque` can be used as both FIFO (First-In-First-Out) queue and LIFO (Last-In-First-Out) stack.


Summary of `Deque` methods:

Type of Operation | Throws exception | Returns `null` or `false` | Throws exception | Returns `null` or `false`
:-:|:-:|:-:|:-:|:-:
Insert | addFirst(e) | offerFirst(e) | addLast(e) | offerLast(e)
Remove | removeFirst() | pollFirst() | removeLast() |  pollLast()
Examine | getFirst() | peekFirst() | getLast() |  peekLast()


- FIFO: `Deque` extends the `Queue` interface.  
Comparison of `Queue` and `Deque` methods:

Queue Method  |  Equivalent Deque Method
:-:|:-:
add(e) | addLast(e)
offer(e)  |  offerLast(e)
remove()  |  removeFirst()
poll() | pollFirst()
element() |  getFirst()
peek() | peekFirst()


- LIFO: `Deque` can also be used as a stack.  
Comparison of legacy `Stack` and `Deque` methods:

Legacy Stack Method | Equivalent Deque Method
:-:|:-:
push(e) | addFirst(e)
pop() | removeFirst()
peek() | peekFirst()


```java
public interface Deque<E> extends Queue<E> {

    // Deque methods:
    void addFirst(E e);
    void addLast(E e);
    boolean offerFirst(E e);
    boolean offerLast(E e);

    E removeFirst();
    E removeLast();
    E pollFirst();
    E pollLast();

    E getFirst();
    E getLast();
    E peekFirst();
    E peekLast();

    boolean removeFirstOccurrence(Object o);
    boolean removeLastOccurrence(Object o);

    // Queue methods:
    boolean add(E e);
    boolean offer(E e);
    E remove();
    E poll();
    E element();
    E peek();

    // Legacy Stack methods:
    void push(E e);
    E pop();

    // Collection methods:
    boolean remove(Object o);
    boolean contains(Object o);
    public int size();
    Iterator<E> iterator();
    Iterator<E> descendingIterator();
}
```


