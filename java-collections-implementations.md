###Java Collections Framework implementations.
---

**Set Implementations**

There are 3 general-purpose `Set` implementations: 
- **HashSet** 
	- stores its elements in `HashMap<E, Object>`
	- the best-performing implementation
	- however it makes no guarantees about the order of iteration
- **TreeSet**
	- stores its elements in a red-black tree
	- orders its elements based on their values
	- substantially slower than `HashSet` (log-time versus constant-time for most operations)
- **LinkedHashSet**
	- implemented as a hash table with a linked list running through it
	- orders its elements based on the order in which they were inserted into the set (*insertion-order*)
	- runs nearly as fast as HashSet

