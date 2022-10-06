## Resource
1.  Core Java Volume I -Fundamentals[[Core Java Volume I -Fundamentals|核心技术卷]]
2. Core Java Volume II - Advance Features
3. 并发编成的艺术
4. Udacity
5. 程序员鱼皮 java路线图


## Java Keywords	
abstract	continue	for	new	super assert [[default]]	 goto null	switch boolean	do	if	package	synchronized break	double	implements	private	this byte	else	import	protected	throw case	enum	instanceof	public	throws catch	extends	int	return	[[transient]] char	final	interface	short	try class	finally	long	static	void const	float	native	[[strictfp]]	volatile while	

## Variable type
-   A **primitive value** is simply a value, by itself, with no additional data.
Data Type	Size
byte	1 byte
short	2 bytes
int	4 bytes
long	8 bytes
float	4 bytes
double	8 bytes
boolean	1 byte
char	2 bytes
-   A **reference value** is a value that refers to an object stored in another location in memory.

## Java memory (Stack vs Heap)
Java uses two different memory regions when running an application: The **stack** and the **heap**.
-   The stack is used to store primitives and object references, while the heap is used to store the objects themselves.
-   Items in the stack get added and removed as a given method executes, while objects in the heap stay until the application is done (or at least, until there are no object references using them from anywhere in the program, at which point they are removed by the garbage collector).
-   Items are removed from the stack in a [**Last-In-First-Out (LIFO) **](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))order, meaning that the last element you added to the stack is the first that gets popped off the stack. 
-   Remember that the items in a stack are only maintained as long as the related method is running. By the time a given method has finished running, all of the items on the stack for that method will have been removed.
-   Objects in the heap are accessible from anywhere in the program, while items on a given stack can only be accessed by the related method.
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209051741278.png)

## Types of Access Modifiers
There are four types of access modifiers in Java:
-   **Public** means the class can be accessed from everywhere. If you have a method on a class that you want to expose to all other classes, then use this access modifier.
-   **Private** means only the defining class can access the data. This provides security, by not allowing other classes to change the data directly. Instead, they must make changes to the data via the provided methods only.
-   **Protected** means that access is restricted to the defining class, package, or subclass. This will be useful when we get into subclasses and inheritance in a later lesson, as it will allow our subclasses to use variables and methods from the parent class.
-   **Default** means access is restricted to the defining class or the package. This can be used when we have classes inside the same package that we may want to expose data and methods too.
| ------- | ------------ | -------------- | --------------------------- | --------------- |
| ------- | ------------ | -------------- | --------------------------- | --------------- |
| Access  | Inside class | inside package | outside package by subclass | outside package |
| Private | Yes          | No             | No                          | NO              |
| Defult  | Yes          | Yes            | No                          | NO              |
| Protect | Yes          | Yes            | Yes                         | No              |
| Publuic | Yes          | Yes            | Yes                         | Yes             |

## Erro and Exception 
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209051825754.png)
### Unchecked Exceptions
-   **Unchecked** exceptions are exceptions that are unknown to the compiler.
-   Because these exceptions are only known at runtime, they are also referred to as _runtime exceptions_.
-   They are a result of a programming error, typically arithmetic errors (such as division by 0).
-   Unchecked exceptions are used when when we expect that the caller of the method cannot recover from the exception.
### Checked Exceptions
-   **Checked** exceptions are known to the compiler.
-   If we are calling a method that potentially throws a checked exception, it _must_ be handled (or we will get an error from the compiler).
-   Checked exceptions are used when we expect that the caller of the method _can_ recover from the exception.

## Date and Calendar
Date类（官方不再推荐使用,官方解释Date类不利于国际化，推荐使用Calendar类）
Date 表示特定的瞬间，精确到毫秒。
在 JDK 1.1 之前，类 Date 有两个其他的函数。它允许把日期解释为年、月、日、小时、分钟和秒值。它也允许格式化和解析日期字符串。不过，这些函数的 API 不易于实现国际化。从 JDK 1.1 开始，应该使用 Calendar 类实现日期和时间字段之间转换，使用 DateFormat 类来格式化和解析日期字符串。Date 中的相应方法已废弃（查阅自API文档）

Calendar类
Calendar 类是一个抽象类，它为特定瞬间与一组诸如 YEAR、MONTH、DAY_OF_MONTH、HOUR 等 日历字段之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法。瞬间可用毫秒值来表示，它是距历元（即格林威治标准时间 1970 年 1 月 1 日的 00:00:00.000，格里高利历）的偏移量。
该类还为实现包范围外的具体日历系统提供了其他字段和方法。这些字段和方法被定义为 protected。
与其他语言环境敏感类一样，Calendar 提供了一个类方法 getInstance，以获得此类型的一个通用的对象。Calendar 的 getInstance 方法返回一个 Calendar 对象，其日历字段已由当前日期和时间初始化：


## Generics
Generics are a way to parameterize class types into classes, methods and variables so that we eliminate the need for casting, have stronger type checks at compile time, and develop generic algorithms.
```java
List strings = new List();
//to
List<String> strings = new <String>ArrayList();

import java.util.ArrayList;
import java.util.List;

public class GenericsExcercise {

    public static void main(String[] args) {
        ArrayList<Object> variables = new ArrayList<Object>();
        Double doubleNumber = 1.5;
        String name = "Sally";
        int intNumber = 1;
        char letter = 'a';

        variables.add(doubleNumber);
        variables.add(name);
        variables.add(intNumber);
        variables.add(letter);

        for (Object variable : variables) {
            GenericsExcercise.displayClassName(variable);
        }

    }
    static <T> void displayClassName(T variable) {
        System.out.println(variable.getClass().getName());
    }

}

```


## Collections
Collections are data structures that were created to provide improved interoperability and performance. Collections provides a more effective framework and architecture for storing, retrieving, and processing data.

## Functional programming
#### Lambda Expression
 lambdas usually result in much cleaner and easier to understand code(Since Java 8)
 > Java Predicate接口，用户希望使用 `java.util.function.Predicate` 接口筛选数据，可以使用 lambda 表达式或方法引用来实现 `boolean test(T t)` 方法。`Predicate` 接口主要用于流的筛选。给定一个包含若干项的流，`Stream` 接口的 `filter` 方法传入 `Predicate` 并返回一个新的流，它仅包含满足给定谓词的项。
```java
//Example of Functional code
int getTopScore(List<Student> students) {
 return students.stream()//
     .filter(Objects::nonNull)
     .mapToInt(Student::getScore)
     .max()
     .orElse(0);
}
// Change imperiative to Functional
public static void main(String[]args){
	List<String> = List.of("Hello","\t   ","world","    \t","goodbye");
	long numberofWhiteSpace= countMatchingStrings(
		input,
		new Predicate<String>{
			@Override 
			public boolean test(String s){return s.trim().isEmpty()}
		});
	)
	long numberofWhiteSpace= countMatchingStrings(
		input,s->s.trim().isEmpty());
	)
	
}

```

> (parameters) -> expression 或 (parameters) ->{ statements; }
> () -> 5 // 1. 不需要参数,返回值为 5
> () -> () -> 10 // ??

#### Functional Interfaces
A **functional interface** is a Java interface with exactly one abstract method, called the **functional method**, which is designed for Lambda expression  
```java
@FunctionalInterface// 1. added to any interface that is not a valid functional interface compile error if not functional 2. tell others 
public interface Predicate<T> {
  boolean test(T t);
  default Predicate<T> negate() { return (t) -> !test(t); }

  // Other methods left out of this example
}
```
When you're designing a Java interface, you should consider making it a functional interface **if it describes a single operation.**
- A **functional interface** is an interface with exactly **one** abstract method.? why
- A functional interface can have any number of default methods. _**Runnable**_, _**ActionListener**_, _**Comparable**_ are some of the examples of functional interfaces.
- they can include any quantity of default and static methods.

**Java SE 8 included four main kinds of functional interfaces** which can be applied in multiple situations. These are: `Consumer`  `Predicate` `Function`  `Supplier`


#### Lambdas vs Anonymous Class
| Anonymous Class                    | Lambda                   | 
| ---------------------------------- | ------------------------ |
| Generated at compile-time          | Generated at runtime     |
| Can @Override `equals()`/`hashCode(0)` | cannot                   |
| `this` refer to anonymous class      | refer to enclosing class |
```java
public static void main(String[]args){  
    Runnable r = () -> System.out.println(this.getClass());// static method: do something with class itself not its instance.  
	r.run();  
}
```
#### Limitations of Lambda
-   They can only be used to implement _functional interfaces_, not classes.
-   Lambdas cannot implement any interface that has multiple abstract methods.
-   Lambdas cannot throw checked exceptions (any subclass of `Exception`, such as `IOException`).
**Solutions to this problem** try-catch(with lambda) for-loop(without lambda)
#### Captured Variables
Lambdas can _capture_ variables from the surrounding code. If a lambda uses any variables from the surrounding code, those variables are _captured_. Variables can only be captured if they are **effectively final**(is a variable whose value does not change after it is initialized.)
A good test is add final keywords to it.
objects are passed by reference. Even though the `HashMap`changes, the variable's value is the `HashMap`'s location in memory, and that location never changes.

### Method Reference
A **method reference** is a short lambda expression that refers to a method that is already named.
```java
long numberOfWhitespaceStrings = countMatchingStrings(input, String::isBlank);
```
However, if it cannot capture variables you should use lambda

### [[Stream]]
A stream pipeline consists of creating a stream, calling intermediate operations on the stream,
- single-use
- lazily evaluated
>  peek(Consumer< super > action) : used for debug, without termination operation do nothing

```java
Stream.of(1, 2, 3)
    .sorted(Comparator.reverseOrder())
    .peek(System.out::print); // no output
```

### Collector
A `Collector` is a terminal stream operation that accumulates stream elements into a container.
```java
Map<Year, Long> graduatingClassSizes = studentList.stream()
    .collect(Collectors.groupingBy(
        Student::getGraduationYear, Collectors.counting());
```

### Optional
-   `java.util.Optional` is a container object that may or may not contain a single, non-null value.
-   Optional is an **alternative to using `null`** to represent the absence of a value.
-  Consider using Optional instead fo null (avoid error) 
-  can sometimes lead to more verbose code by forcing you to call `.get()` whenever you want the value
```java
int getTopScore(List<Student> students) {
 return students.stream()
     .filter(Objects::nonNull)
     .mapToInt(Student::getScore)
     .max() // OptionalInt return 
     .orElse(0); //`orElse()` makes sure that a default value of `0` will be returned.
}
```
How does the `Optional` class help you avoid `NullPointerException`: Signals that the API caller should check if there is a value before using it.

if steam 中 .get method 出来了一个list `flatMap()` + `.stream()`

!!! date 的处理


### Files and I/O
-   Read and write binary and text files in Java.
-   Prevent resource leaks using the `try-with-resources` idiom.
-   Compare several different serialization formats: JSON, XML, and Java Object Serialization.
-   Serialize and deserialize JSON in Java.
#### Files
```java
BufferedReader reader =
   Files.newBufferedReader(Path.of("test"), StandardCharsets.UTF_8);
String line;
while ((line = reader.readLine()) != null) {
 useString(line);
}
reader.close();
```
#### Path

### Preventing Resource Leaks
Closeable
 `try-with-resources`
```java
try (Writer writer = Files.newBufferedWriter(Path.of("test"))) {
  writer.write("Hello, world!");
} catch (IOException e) {
  e.printStackTrace();
}
try (InputStream in   = Files.newInputStream(Path.of("foo"));
     OutputStream out = Files.newOutputStream(Path.of("bar"))) {
  out.write(in.readAllBytes());
}


```
**only close the resorce  you creat**
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209092318941.png)

### Serialization
```java
Path path = Path.of("list.bin");
    try (var out = new ObjectOutputStream(Files.newOutputStream(path))) {
      out.writeObject(List.of("Hello", " ", "World!"));
    }
    try (var in = new ObjectInputStream(Files.newInputStream(path))) {
      List<String> deserialized = (List<String>) in.readObject();
      System.out.println(deserialized);
    }
```

