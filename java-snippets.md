
__The Java Class File Disassembler:__

`javap -c Foo.class` will show the disassembly of Foo.class.

---

__String concatenation:__

```java
	a += b
```

is the equivalent of
	
```java
	a = new StringBuilder().append(a).append(b).toString();
```

---

__String's natural ordering:__

The successor of a string s in String's natural ordering is `s + "\0"`, which is `s` with a null character appended.

```java
	String[] wordArray = {"included", "j", "aaa"};
	SortedSet<String> dictionary = new TreeSet<String>(Arrays.asList(wordArray));
	System.out.println(dictionary.subSet("a", "included\0"));
```
The code above will output: `[aaa, included]`

---

__Method Overloading vs. Overriding:__  

	- Method **Overloading**: method with same name co-exists in same class, but they must have different method signatures. Resolved using static binding at compile time.
	
	- Method **Overriding**: method with same name and same signature is declared in derived class or sub-class. Resolved using dynamic binding at runtime. 
	
		Examples: `equals(), hashCode(), compareTo()`. 
		Cannot override static methods (`main()`, for example) because they are associated with Class rather than Object, and resolved and bonded during compile time. Also, private and final methods cannot be overridden. Good practice is to use `@Override` annotation.

---

__Implementing `equals()` and `hashCode()` override:__

```java
public class Person {

	private String name;
	private int age;
	
	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	public boolean equals (Object y) {
		if (y == this) return true;
		if (y == null) return false;
		if (y.getClass() != this.getClass()) return false;
		Person that = (Person) y;
		return this.name.equals(that.name) && this.age == that.age;
	}

	// satisfies the hashCode contract
	@Override
    public int hashCode() {		
        return 31 * name.hashCode() + age;
    }

	@Override    
	public String toString () {
		return name + " " + age;
	}
}
```

---

__IntegerCache, ShortCache, ByteCache, CharacterCache__

The `Integer` class has a static cache, that stores 256 `Integer` objects.  

Two autoboxing conversions of a primitive value p will yield an identical reference (that is, the == comparison will return true) if p is:

- `Short` and `Integer` from -128 to 127
- `Byte`
- `Boolean`
- `Character` from \u0000 to \u007f (7f is 127 in decimal)

---


 	