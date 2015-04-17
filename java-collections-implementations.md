###Java Collections Framework implementations.
---

**Set Implementations**

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

  | HashSet | LinkedHashSet | TreeSet |
:--- |:---:|:---:|:---:
Insertion (add) | O(1) | O(1) | O(log n)
Deletion (remove) | O(1) | O(1) | O(log n)
Search (contains) | O(1) | O(1) | O(log n)
Iteration (next) | O(h/n) | O(1) | O(log n)
Positional Access (get) | no | no | no
Order | no guarantee | insertion-order | sorted | 
Interfaces | Set | Set | Set, SortedSet
Implementation | HashMap | LinkedHashMap | Red-Black Tree

Note: h is the HashSet capacity (number of buckets in a HashMap that's backing it up)

---

**List Implementations**

There are 2 general-purpose `List` implementations: 

- **ArrayList**
	- implemented as a resizable array
	- fast constant-time positional access
- **LinkedList**
	- implemented as a doubly-linked list
	- allocates a node object for each element in the list
	- also implements the `Queue` interface
	- has 7 options operations(`clone`, `addFirst`, `getFirst`, `removeFirst`, `addLast`, `getLast`, `removeLast`)
	- main benefits: Iterator.remove() and ListIterator.add(E element) are constant runtime (O(1))


**List Implementations Time Complexity:**

  | ArrayList | LinkedList
:--- |:---:|:---:
Positional Access (get) | **O(1)**  | O(n)
Insertion (add) | O(1) | O(1)
ListIterator.add | O(n) | **O(1)**
Deletion (remove) | O(n) | O(n)
Iterator.remove | O(n) | **O(1)**
Search (contains) | O(n) | O(n)
Iteration (next) | O(n) | O(1)
Interface | List | List, Queue
Implementation | resizable array | doubly-linked list 


---

**Map Implementations Time Complexity:**

  | HashMap | LinkedHashMap | TreeMap |
:--- |:---:|:---:|:---:
Positional Access (get) | O(1)  | O(1)  | O(log n)
Insertion (put) | O(1) | O(1) | O(log n)
Deletion (remove) | O(1) | O(1) | O(log n)
Search (containsKey) | O(1) | O(1) | O(log n)
Iteration (next) | O(h/n) | O(1) | O(log n)
Order | no guarantee | insertion-order | sorted | 
Null values/keys | allowed | allowed | only values 
Interfaces | Map | Map | Map, SortedMap
Implementation | buckets | double-linked buckets | Red-Black Tree


