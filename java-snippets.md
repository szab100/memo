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

#### :floppy_disk: Memory Usage in Java (on a 64-bit machine).

- Primitive types:

type  | bytes
:---: | :---:
boolean | 1
byte | 1
char | 2
int | 4
long | 8
float | 4
double | 8

- References:  
8 bytes for a memory address (on a 64-bit machine)

- Objects:  
16 bytes overhead +
memory used by each instance variable, padded to a multiple of 8 bytes

	For example, Integer wrapper object:  
	24 bytes = 16 bytes overheard + 4 bytes int + padding to a multiple of 8

- Arrays:  
24 bytes header (16 bytes object overhead + 4 bytes for the length + 4 bytes padding) + memory needed to store the values

type  | bytes
:---: | :---:
boolean[] | ~N
int[] | ~4N
double[] | ~8N

- Strings:  
56 + 2N bytes = 32 bytes (for the String object) + (24 + 2N) bytes (for the char[] array in a string of length N)

- Linked List node object (inner class):  
48 bytes = 16 bytes object overhead + 8 bytes extra overhead for a reference to the enclosing instance + 2 * 8 bytes for references to next/previous node + 8 bytes reference to a node data

---

#### Precedence and associativity of Java operators

Java operators, from highest to lowest precedence, along with their associativity:

<table cellspacing="1" cellpadding="5" border="0">
<tbody><tr align="center">
<th>Operator</th>
<th>Description</th>
<th>Level</th>
<th>Associativity</th>
</tr>

<tr align="center">
<td>
<code>[]</code><br>
<code>.</code><br>
<code>()</code><br>
<code>++</code><br>
<code>--</code>
</td>
<td>
access array element<br>
access object member<br>
invoke a method<br>
post-increment<br>
post-decrement
</td>
<td>1</td>
<td>left to right</td>
</tr>

<tr align="center">
<td>
<code>++</code><br>
<code>--</code><br>
<code>+</code><br>
<code>-</code><br>
<code>!</code><br>
<code>~</code>
</td>
<td>
pre-increment<br>
pre-decrement<br>
unary plus<br>
unary minus<br>
logical NOT<br>
bitwise NOT
</td>
<td>2</td>
<td>right to left</td>
</tr>

<tr align="center">
<td>
<code>()</code><br>
<code>new</code>
</td>
<td>
cast<br>
object creation
</td>
<td>3</td>
<td>right to left</td>
</tr>

<tr align="center">
<td>
<code>*</code><br>
<code>/</code><br>
<code>%</code>
</td>
<td>
multiplicative
</td>
<td>4</td>
<td>left to right</td>
</tr>


<tr align="center">
<td>
<code>+</code> <code>-</code><br>
<code>+</code>
</td>
<td>
additive<br>
string concatenation
</td>
<td>5</td>
<td>left to right</td>
</tr>

<tr align="center">
<td>
<code>&lt;&lt;</code> <code>&gt;&gt;</code><br>
<code>&gt;&gt;&gt;</code>
</td>
<td>
shift
</td>
<td>6</td>
<td>left to right</td>
</tr>

<tr align="center">
<td>
<code>&lt;</code> <code>&lt;=</code><br>
<code>&gt;</code> <code>&gt;=</code><br>
<code>instanceof</code>
</td>
<td>
relational<br>
type comparison
</td>
<td>7</td>
<td>left to right</td>
</tr>


<tr align="center">
<td>
<code>==</code><br>
<code>!=</code>
</td>
<td>
equality
</td>
<td>8</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>&amp;</code></td>
<td>bitwise AND</td>
<td>9</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>^</code></td>
<td>bitwise XOR</td>
<td>10</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>|</code></td>
<td>bitwise OR</td>
<td>11</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>&amp;&amp;</code></td>
<td>conditional AND</td>
<td>12</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>||</code></td>
<td>conditional OR</td>
<td>13</td>
<td>left to right</td>
</tr>

<tr align="center">
<td><code>?:</code></td>
<td>conditional</td>
<td>14</td>
<td>right to left</td>
</tr>

<tr align="center">
<td>
<code> =</code> <code>+=</code> <code>-=</code><br>
<code>*=</code> <code>/=</code> <code>%=</code><br>
<code>&amp;=</code> <code>^=</code> <code>|=</code><br>
<code>&lt;&lt;=</code> <code>&gt;&gt;=</code> <code>&gt;&gt;&gt;=</code>
</td>
<td align="">
assignment
</td>
<td>15</td>
<td>right to left</td>
</tr>

</tbody></table>

Associativity:
- `x = y = z = 17` is treated as `x = (y = (z = 17))`, since the `=` operator has right-to-left associativity.  
- `72 / 2 / 3` is treated as `(72 / 2) / 3`, since the `/` operator has left-to-right associativity.

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
