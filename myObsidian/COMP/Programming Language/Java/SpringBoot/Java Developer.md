---
aliases: [springboot]

---
# Java Basics
## Java Refresher Course
[[StringBuffer && StringBuilder]]
[[ArrayList & LinkList]]
[[Stack & Queue]]
[[Map]] [[HashSet]]
Exercise
1. Complete the “String reverse” coding problem.
```java
// wrong answer
public static String reverseString(String s) {
   ArrayList<Character> array  = Arrays.asList(s.toCharArray());
   array.reverse();
   String res = array.toArray();
   return res;
}    
public static String reverseString(String s) {
        StringBuffer sb = new StringBuffer(s);
        sb.reverse();
        return sb.toString();
    }
```
Takeaways:
	1. toArray() <<>> java.utils.Arrays: Arrays.asList();
	2. List do not support reverse operation >>> Use Stringbuffer. reverse()

2. findDuplicate
```java
public static int findDuplicate(String input){
   HashSet<Character> set = new HashSet<Character>();
   int res = 0;
   while(set.size() == res&& set.size()< input.length()){
	  set.add(input.charAt(res));
	  res++;
   }
   return (res == set.size()) ? -1 : res-1; 
}
public static int findDulicate(String input){
	Set<Character> set = new HashSet<Character>();
	for(int i=0;i<input.length();i++){
		if(set.contains(input.charAt(i)) return i;
		else set.add(input.charAt(i));
	}
	return -1;
}
```
3. TopK largest
```java
public static List<int> topLargest(int[]arr,int k){
	TreeSet<Integer> set = new TreeSet<Integer>();
	for(int num: arr){
		set.add(num);
		if(set.size()>k) set.pollFirst();
	}
	return set.steam().collect(Collecter.toList())// check this out
}

```
Takeaways
1. for 的写法
2. data structure is quite important about sloving the problem.
3. steam()

# Intro to Spring Boot
### Microservice vs Monolithic
Microservices - also known as the microservice architecture - is an architectural style that structures an application as a collection of services that are
-   Highly maintainable and testable
-   Loosely coupled
-   Independently deployable
-   Organized around business capabilities
-   Owned by a small team
The microservice architecture enables the rapid, frequent and reliable delivery of large, complex applications. It also enables an organization to evolve its technology stack.
### MVC(Model View Controller)
### Spring and SpringBoot

## Spring boot Exception
There are five types of situations we can handle Spring Boot exceptions rather than showing error pages like 404 or 500.
Let’s recap these spring boot exception handling.

1.  Create custom error page. -> create a error.html page, when errors happen, customer will be redirected to this page.
2.  [@ExceptionHandler](https://github.com/ExceptionHandler). -> handle exceptions inside each controller.
3.  [@ControllerAdvice](https://github.com/ControllerAdvice) + [@ExceptionHandler](https://github.com/ExceptionHandler)  
    Create a separate class and write all exceptions based on their types.
4.  Configure SimpleMappingExceptionResolver class ->  
    Rather than adding one method per exception, create a key-value pair class, and let system look for the error
5.  Custom HandlerExceptionResolver class -> use reflection to find what type of exception it’s
## WebSocket 
Websocket is a low-level protocol. It defines how a stream of bytes is transformed into frames, which contains a text or binary message. A WebSocket message itself does not have instructions about how to route or process it. Therefore, we need additional support to achieve two-way communication. With Spring Boot, we have STOPM.
### STOMP( Simple Text Oriented Message Protocol)
STOMP is a simple text-based message protocol. With it, clients can send and receive messages to and from each other. STOMP is called HTTP for Web. It defines a handful of frame types that are mapped onto WebSockets frames, e.g., `CONNECT, SUBSCRIBE, UNSUBSCRIBE, ACK, or SEND`.
STOMP Frame Object
- command -> string
- Header -> JavaScript Object
- Body -> String








