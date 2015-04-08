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

**An Iterator** points at the next unseen element in a collection.

```java
public interface Iterator<E> {
 
    boolean hasNext();
    E next();
    void remove();
}
```

---

**Set** is a collection that contains **no duplicate** elements. Adds no new methods. A set uses the equals method of its elements to determine if two elements are the same (logical equality).


```Java
public interface Set<E> extends Collection<E> { }
```
---

**SortedSet** 

```java
public interface SortedSet<E> extends Set<E> {

    Comparator<? super E> comparator();

    SortedSet<E> subSet(E fromElement, E toElement);
    SortedSet<E> headSet(E toElement);
    SortedSet<E> tailSet(E fromElement);

    E first();
    E last();
}
```









