###Java Collections Framework implementations.
---

**Set Implementations**

There are 3 general-purpose `Set` implementations: 

- **HashSet** 
	- stores its elements in `HashMap<E, Object>`
	- the best-performing implementation
	- however it makes no guarantees about the order of iteration
- **LinkedHashSet**
	- implemented as a hash table with a linked list running through it (LinkedHashMap)
	- orders its elements based on the order in which they were inserted into the set (*insertion-order*)
	- runs nearly as fast as HashSet
- **TreeSet**
	- stores its elements in a red-black tree
	- orders its elements based on their values
	- substantially slower than `HashSet` (log-time versus constant-time for most operations)


**Time Complexity**:

  | HashSet | LinkedHashSet | TreeSet |
:--- |:---:|:---:|:---:
Insertion (add) | O(1) | O(1) | O(log n)
Deletion (remove) | O(1) | O(1) | O(log n)
Search (contains) | O(1) | O(1) | O(log n)
Iteration (next) | O(h/n) | O(1) | O(log n)
Positional Access (get) | no | no | no
Order | no guarantee | insertion-order | sorted | 
Interfaces | Set | Set | Set, SortedSet
Implementation | HashMap (buckets) | LinkedHashMap (double-linked buckets) | Red-Black Tree

Note: h is the HashSet capacity (number of buckets in a HashMap that's backing it up)

---

**Map Implementations**

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


