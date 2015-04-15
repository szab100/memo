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

The **List** is an ordered `Collection` (a sequence). The `List` interface adds random access methods:

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

