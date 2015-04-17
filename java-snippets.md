- To remove all null's from a collection:

```java
 	c.removeAll(Collections.singleton(null));
```

- To add multiple values to already initialized list:

```java
 	list.addAll(Arrays.asList(a, b, c, d, e, f, g));
```

- To add multiple values to a not yet initialized list:

```java 	
	List<E> list = new ArrayList<E>(Arrays.asList(a, b, c, d, e, f, g));
```

- To modify a List during iteration with ListIterator (unlike ListIterator, Iterator allows you to delete elements, but not to replace an existing element or to add a new one):

```
	List<String> list = Arrays.asList(" a ", " b ", " c ");
	ListIterator<String> it = list.listIterator();
	while (it.hasNext()) {
		it.set(it.next().trim());
	}
```

- To iterate over the keys in a Map:

```java
	for (KeyType key: map.keySet()){
		System.out.println(key);
	}
```

- To iterate over the keys in a Map with an iterator:

```java
	Iterator<KeyType> it = map.keySet().iterator();
	while (it.hasNext()) {
		System.out.println(it.next());
	}
```

- To iterate over key-value pairs in a Map:

```java
	for (Map.Entry<KeyType, ValueType> el: map.entrySet()) {
		System.out.println(el.getKey() + ": " + el.getValue());
	}
```

- To sort Map by Keys (using TreeMap, which is slower than HashMap because it runs sorting operation with each insertion, update and removal):

```java
	Map<K,V> sortedMap = new TreeMap<K,V>(map);
```

- To sort Map by Keys (LinkedHashMap will keep the keys in the order they are inserted):

```java
	List<K> keys = new ArrayList<K>(map.keySet());
	Collections.sort(keys);
	Map<K,V> sortedMap = new LinkedHashMap<K,V>();
	for(K key: keys){
		sortedMap.put(key, map.get(key));
	}
```

- To sort Map by Values:

```java
	List<Map.Entry<K,V>> entries = new LinkedList<Map.Entry<K,V>>(map.entrySet());
	Collections.sort(entries, new Comparator<Map.Entry<K,V>>() {
		@Override
		public int compare(Entry<K, V> o1, Entry<K, V> o2) {
			return o1.getValue().compareTo(o2.getValue());
		}
	});
	Map<K,V> sortedMap = new LinkedHashMap<K,V>();
	for(Map.Entry<K,V> entry: entries){
		sortedMap.put(entry.getKey(), entry.getValue());
	}
```

- String concatenation:

```java
	a += b is the equivalent of
	a = new StringBuilder().append(a).append(b).toString();
```

- String's natural ordering:

The successor of a string s in String's natural ordering is `s + "\0"`, which is `s` with a null character appended.

```java
	String[] wordArray = {"included", "j", "aaa"};
	SortedSet<String> dictionary = new TreeSet<String>(Arrays.asList(wordArray));
	System.out.println(dictionary.subSet("a", "included\0"));
```
The code above will output: [aaa, included]

- SortedSet Endpoint Operations:

To go one element backward from a specified interior object `obj` in a sorted set:

```java
Object predecessor = sortedSet.headSet(obj).last();
```

- Method Overloading vs. Overriding:
	- Method **Overloading**: method with same name co-exists in same class, but they must have different method signatures. Resolved using static binding at compile time.
	
	- Method **Overriding**: method with same name and same signature is declared in derived class or sub-class. Resolved using dynamic binding at runtime. 
	
		Examples: `equals(), hashCode(), compareTo()`. 
		Cannot override static methods (`main()`, for example) because they are associated with Class rather than Object, and resolved and bonded during compile time. Also, private and final methods cannot be overridden. Good practice is to use `@Override` annotation.




 	