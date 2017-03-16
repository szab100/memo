### Java Collections Framework implementations
---

#### Set Implementations

There are 3 general-purpose `Set` implementations:

- **HashSet**
	- stores its elements in `HashMap<E, Object>`
	- the best-performing implementation
	- however it makes no guarantees about the order of iteration
- **LinkedHashSet**
	- implemented as a hash map with a linked list running through it (LinkedHashMap)
	- orders its elements based on the order in which they were inserted into the set (*insertion-order*)
	- runs nearly as fast as HashSet (except iteration time is not affected by capacity)
- **TreeSet**
	- stores its elements in a red-black tree
	- orders its elements based on their values
	- substantially slower than `HashSet` (log-time versus constant-time for most operations)


**Set Implementations Time Complexity:**

&nbsp; | HashSet | LinkedHashSet | TreeSet |
:--- |:---:|:---:|:---:
Insertion (add) | O(1) | O(1) | O(log n)
Deletion (remove) | O(1) | O(1) | O(log n)
Search (contains) | O(1) | O(1) | O(log n)
Iteration (next) | O(h/n) | O(1) | O(log n)
Positional Access (get) | no | no | no
Order | no guarantee | insertion-order | sorted
Interfaces | Set | Set | Set, SortedSet
Implementation | HashMap | LinkedHashMap | Red-Black Tree

Note: h is the HashSet capacity (number of buckets in a HashMap that's backing it up)

---

#### List Implementations

There are 2 general-purpose `List` implementations:

- **ArrayList**
	- implemented as a resizable array
	- fast constant-time positional access `get(int index)`, whereas `LinkedList` requires iterating through the nodes in O(n)
	- if more elements than the capacity of the underlying array are added, a new array (1.5 times the size) is allocated, and the old array is copied to the new one, resulting in O(n)
- **LinkedList**
	- implemented as a doubly-linked list
	- allocates a node object for each element in the list, thus uses more memory
	- also implements the `Deque` interface
	- has 7 optional operations(`clone`, `addFirst`, `getFirst`, `removeFirst`, `addLast`, `getLast`, `removeLast`)
	- main benefits: `LinkedList` allows for constant-time insertions or removals *using iterators*: `Iterator.remove()` and `ListIterator.add(E element)`, whereas `ArrayList` requires shifting the remainder of the array over, resulting in O(n) in the worst case


**List Implementations Time Complexity:**

&nbsp; | ArrayList | LinkedList
:--- |:---:|:---:
Positional Access: `get(int index)` | **O(1)**  | O(n)
Insertion: `add(E element)` | O(1) | O(1)
Insertion: `add(int index, E element)` | O(n) | O(n)
Insertion: `ListIterator.add(E element)` | O(n) | **O(1)**
Deletion: `remove(int index)` | O(n) | O(n)
Deletion: `Iterator.remove()` | O(n) | **O(1)**
Search: `contains(E element)` | O(n) | O(n)
Iteration: `ListIterator.next()` | O(1) | O(1)
Order | insertion-order | insertion-order
Interface | List | List, Deque
Implementation | resizable array | doubly-linked list


---

#### Map Implementations

There are 3 general-purpose `Map` implementations:

- **HashMap** : fast
- **LinkedHashMap**: insertion-order iteration, near-HashMap performance
- **TreeMap**: slow (O(log n)), SortedMap operations and key-ordered Collection-view iteration

**Map Implementations Time Complexity:**

&nbsp; | HashMap | LinkedHashMap | TreeMap |
:--- |:---:|:---:|:---:
Positional Access (get) | O(1)  | O(1)  | O(log n)
Insertion (put) | O(1) | O(1) | O(log n)
Deletion (remove) | O(1) | O(1) | O(log n)
Search (containsKey) | O(1) | O(1) | O(log n)
Iteration (next) | O(h/n) | O(1) | O(log n)
Order | no guarantee | insertion-order | sorted
Null values/keys | allowed | allowed | only values
Interfaces | Map | Map | Map, SortedMap
Implementation | buckets | double-linked buckets | Red-Black Tree


---

#### Queue Implementations

There are 2 general-purpose `Queue` implementations:

- **LinkedList**: provides first in, first out (FIFO) queue operations
- **PriorityQueue**:
	- based on the heap data structure
	- orders elements according to the order specified at construction time (natural ordering or an explicit `Comparator`)
	- the *head* of the queue is the least element with respect to the specified ordering
	- `iterator` is not guaranteed to traverse the elements of the `PriorityQueue` in any particular order. For ordered traversal, use `Arrays.sort(pq.toArray())`.

---

#### Deque Implementations

There are 2 general-purpose `Deque` implementations:

- **LinkedList**:
	- more flexible
	- implements all optional `List` operations
	- `null` elements are allowed
	- consumes more memory
	- not ideal to iterate
- **ArrayDeque**:
	- the resizable array implementation
	- more efficient than the `LinkedList` for add and remove operation at both ends
	- to iterate use:
		- the `foreach` loop
		- the `Iterator` (for the forward traversal)

**Queue and Deque Implementations Time Complexity:**

&nbsp; | offer/add | peek/element | poll/remove
:-:|:-:|:-:|:-:
LinkedList | O(1) | O(1) | O(1)
PriorityQueue | O(log n) | O(1) | O(log n)
ArrayDeque | O(1) | O(1) | O(1)

---

#### Bridge between array-based and collection-based APIs

- `Arrays.asList()`
	- `Arrays.asList(a)` method returns a `List` view of its array argument.
	- Changes to the list write through to the array and vice versa.
	- The size of the collection is the size of the array and cannot be changed (cannot call `add` or `remove` methods).
	- A reference to the backing array is not retained.
- `Collection.toArray()`
	- The `Collection` interface `toArray` method with no arguments creates a new array of `Object` whose length is identical to the number of elements in a `Collection` c:  
	`Object[] a = c.toArray();`

---
