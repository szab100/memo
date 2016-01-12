- __To remove all `null`'s from a collection:__

```java
 	c.removeAll(Collections.singleton(null));
```

- __To remove all elements that map to a specified value from a `Map`:__

	If you have a `Map` that maps people to their occupation and you want to eliminate all the lawyers: 

```java
map.values().removeAll(Collections.singleton(LAWYER));
```

- __To add multiple values to already initialized `List`:__

```java
 	list.addAll(Arrays.asList(a, b, c, d, e, f, g));
```

- __To add multiple values to a not yet initialized `List`:__

```java 	
	List<E> list = new ArrayList<E>(Arrays.asList(a, b, c, d, e, f, g));
```

- __To modify a `List` during iteration with `ListIterator`:__  

Unlike `ListIterator`, `Iterator` allows you to delete elements, but not to replace an existing element or to add a new one.

```java
	List<String> list = Arrays.asList(" a ", " b ", " c ");
	ListIterator<String> it = list.listIterator();
	while (it.hasNext()) {
		it.set(it.next().trim());
	}
```

- __To iterate over the keys in a `Map`:__

```java
	for (K key: map.keySet()){
		System.out.println(key);
	}
```

- __To iterate over the keys in a `Map` with an `Iterator`:__

```java
	Iterator<K> it = map.keySet().iterator();
	while (it.hasNext()) {
		System.out.println(it.next());
	}
```

- __To iterate over key-value pairs in a `Map`:__

```java
	for (Map.Entry<K, V> el: map.entrySet()) {
		System.out.println(el.getKey() + ": " + el.getValue());
	}
```

- __To sort `Map` by keys using `TreeMap`:__

`TreeMap` is slower than `HashMap` because it runs sorting operation with each insertion, update and removal in O(log n).

```java
	Map<K,V> sortedMap = new TreeMap<K,V>(map);
```

- __To sort `Map` by keys:__  

`LinkedHashMap` will keep the keys in the order they are inserted.

```java
	List<K> keys = new ArrayList<K>(map.keySet());
	Collections.sort(keys);
	Map<K,V> sortedMap = new LinkedHashMap<K,V>();
	for(K key: keys){
		sortedMap.put(key, map.get(key));
	}
```

- __To sort `Map` by values:__

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

- __`SortedSet` endpoint operations:__

To go one element backward from a specified interior object `obj` in a sorted set:

```java
Object predecessor = sortedSet.headSet(obj).last();
```

- __Reverse Order Comparator:__

```java
public class ReverseOrderComparator {
	
	public static final Comparator<Integer> REVERSE_ORDER = new Comparator<Integer>() {
		public int compare(Integer e1, Integer e2) {
			return (e1 < e2 ? 1 : (e1 == e2 ? 0 : -1));
		}
	};

	public static void main(String[] args) {
		Integer[] array = { Integer.MIN_VALUE, Integer.MAX_VALUE, 0 };
		Arrays.sort(array, REVERSE_ORDER);
		System.out.println(Arrays.toString(array));
	}
}
```

 	