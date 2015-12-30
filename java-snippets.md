#### Java class file disassembler:

`javap -c Foo.class` will show the disassembly of Foo.class.

---

#### java.io

- IO Stream is a conceptually endless flow of data.   
- Streams in java.io are either byte based (reading and writing bytes) or character based (reading and writing characters).
- Summary of main java.io classes:

&nbsp; | Byte Based </br> Input | Byte Based </br> Output | Character Based </br> Input | Character Based </br> Output
:---: | :---:| :---: | :---: | :---:
Abstract | InputStream | OutputStream | Reader | Writer
Byte/Character bridge |  |  | InputStreamReader | OutputStreamWriter
Arrays | ByteArrayInputStream | ByteArrayOutputStream | CharArrayReader | CharArrayWriter
Files | FileInputStream </br> RandomAccessFile | FileOutputStream </br> RandomAccessFile | FileReader | FileWriter
Pipes | PipedInputStream | PipedOutputStream | PipedReader | PipedWriter
Buffering | BufferedInputStream | BufferedOutputStream | BufferedReader | BufferedWriter
Filtering | FilterInputStream | FilterOutputStream | FilterReader | FilterWriter
Parsing | PushbackInputStream </br> StreamTokenizer |  | PushbackReader </br> LineNumberReader |
Strings |  |  | StringReader | StringWriter
Data | DataInputStream | DataOutputStream |  |
Formatted Data |  | PrintStream |  | PrintWriter
Objects | ObjectInputStream | ObjectOutputStream |  |
Utilities | SequenceInputStream |  |  |

---

#### Bitwise and Bit Shift operators

Operator | Bitwise Operation
:--- | :---
~      | Unary bitwise complement
<<     | Signed left shift
>>     | Signed right shift
>>>    | Unsigned right shift
&      | Bitwise AND
&#124;      | Bitwise inclusive OR
^      | Bitwise exclusive OR


& | &#124; | ^
:---: | :---: | :---:
0 & 0 = 0 | 0 &#124; 0 = 0 | 0 ^ 0 = 0
1 & 0 = 0 | 1 &#124; 0 = 1 | 1 ^ 0 = 1
0 & 1 = 0 | 0 &#124; 1 = 1 | 0 ^ 1 = 1
1 & 1 = 1 | 1 &#124; 1 = 1 | 1 ^ 1 = 0


& | &#124; | ^
:---: | :---: | :---:
x & 0 = 0 | x &#124; 0 = x | x ^ 0 = x
x & (-1) = x | x &#124; (-1) = -1 | x ^ (-1) = ~x
x & x = x | x &#124; x = x | x ^ x = 0


- Left shift:  
  `(n << s) == n * Math.pow(2, s)`

- Right shifts:
	- the __unsigned__ (or logical) right shift operator `>>>` inserts a 0 into the leftmost bit (most significant bit):  
	`-1 >>> 31 == 1`
	- the leftmost bit inserted by the __signed__ right shift operator `>>` depends on sign extension (0 for positive n and 1 for negative n):  
	`-1 >> 1 == -1`
	- the __signed__ right shift operator `>>` for negative integers is NOT equal to division by 2:  
	`-3 / 2 = -1`, whereas `-3 >> 1 = -2`
	- if n >= 0:  
    `(n >> s) == (int)(n / Math.pow(2, s))`  
    `(n >>> s) == (n >> s)`
	- if n < 0:  
    `(n >> s) == Math.floor(n / Math.pow(2, s))`  
    `(n >>> s) == (n >> s) + (2 << ~s)`

---

#### The 2's Complement

The 2's complement of an N-bit number is the complement with respect to 2<sup>N</sup>, i.e. the result of subtracting the number from 2<sup>N</sup>. The 2's complement of a number behaves like the arithmetic negative of the original number.

To calculate the 2's complement of a binary number:

1. invert the bits by flipping 1s to 0s and 0s to 1s (the unary bitwise complement operation (~), also called 1's complement)
2. then add 1 (ignoring the overflow)

For example, using 1 byte (8 bits), the 2's complement of 5<sub>10</sub> = 0000 0101<sub>2</sub> is 1111 1011<sub>2</sub> = -5<sub>10</sub>:

1. ~(0000 0101) = 1111 1010
2. 1111 1010 + 1 = 1111 1011

The 2's complement of 0 is 0: inverting gives all 1s, and adding 1 changes the 1s back to 0s (since the overflow is ignored).

---

#### Method Overloading vs. Overriding  

- Method **Overloading**:
	- Method with same name co-exists in same class, but they must have different method signatures.
	- Resolved using static binding at compile time.

- Method **Overriding**:
	- Method with same name and same signature is declared in derived class or sub-class.
	- Resolved using dynamic binding at runtime.
	- Examples: `equals(), hashCode(), compareTo()`.
	- Cannot override static methods (`main()`, for example) because they are associated with Class rather than Object, and resolved and bonded during compile time. Also, private and final methods cannot be overridden.
	- Good practice is to use `@Override` annotation.

---

#### Implementing `equals()` and `hashCode()` override:

```java
public class Person implements Comparable<Person> {

	private String name;
	private int age;

	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}

	@Override
	public boolean equals(Object y) {
		if (y == this) return true;
		if (y == null) return false;
		if (y.getClass() != this.getClass()) return false;
		Person that = (Person) y;
		return this.name.equals(that.name) && this.age == that.age;
	}

	// satisfies the hashCode contract
	@Override
	public int hashCode() {
		return (31 * name.hashCode() + age);
	}

	@Override
	public String toString() {
		return name + " " + age;
	}

	// impose total ordering, i.e. ordering that is compatible with equals:
	// (a.compareTo(b) == 0) => a.equals(b)
	@Override
	public int compareTo(Person other) {

		// lexicographic ordering:
		int nameComp = name.compareTo(other.name);

		// if names are the same, return in seniority order:
		return (nameComp != 0 ? nameComp
				: (age < other.age ? -1 : (age == other.age ? 0 : 1)));
	}
}
```

---

#### IntegerCache, ShortCache, ByteCache, CharacterCache

The `Integer` class has a static cache, that stores 256 `Integer` objects.  

Two autoboxing conversions of a primitive value p will yield an identical reference (that is, the == comparison will return true) if p is:

- `Short` and `Integer` from -128 to 127
- `Byte`
- `Boolean`
- `Character` from \u0000 to \u007f (7f is 127 in decimal)

---

#### String concatenation:

```java
	a += b
```

is the equivalent of

```java
	a = new StringBuilder().append(a).append(b).toString();
```

---

#### String's natural ordering:

The successor of a string s in String's natural ordering is `s + "\0"`, which is `s` with a null character appended.

```java
	String[] wordArray = {"included", "j", "aaa"};
	SortedSet<String> dictionary = new TreeSet<String>(Arrays.asList(wordArray));
	System.out.println(dictionary.subSet("a", "included\0"));
```
The code above will output: `[aaa, included]`

---

#### Parity test

- Warning: for negative odd integers `(x % 2) == 1` will return false,  
since the remainder will be -1, not 1: `(-3 % 2) == -1`.  
- Test for "not equal to zero" instead:

```java
	public static boolean isOdd(int x) {
		return (x % 2) != 0;
	}
```

