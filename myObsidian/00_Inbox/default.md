1. `default`关键字指定在没有`case` 匹配的情况下要运行的一些代码：
2. 总所周知在使用接口的时候，很多人都会遇到一个很尴尬的事情，在实现某个接口的时候，需要实现该接口所有的方法。这个时候default关键字就派上用场了。通过default关键字定义的方法，集成该接口的方法不需要去实现该方法。

```java
int day = 8; 
String dayString; 
switch (day) { 
	case 1: dayString = "Monday"; break; 
	case 2: dayString = "Tuesday"; break; 
	case 3: dayString = "Wednesday"; break; 
	case 4: dayString = "Thursday"; break; 
	case 5: dayString = "Friday"; break; 
	case 6: dayString = "Saturday"; break; 
	//如果case没有匹配的值，那么肯定是星期日 
	default: dayString = "Sunday"; break; 
} 
System.out.println(dayString);
```
```java
interface IntefercaeDemo { 
	//具体方法 
	default void showDefault(){ 
		System.out.println("this is showDefault method"); 
	} 
	//具体方法 
	static void showStatic(){ 
		System.out.println("this is showStatic method"); 
	} 
	//没有实现的抽象方法 
	void sayHi(); 
	} 
class LearnDefault implements IntefercaeDemo{ 
	//实现抽象方法 
	@Override public void sayHi() { 
		System.out.println("this is sayHi mehtod"); 
	} 
	public static void main(String[] args) { 
		//接口中被static所修饰的具体方法 
		IntefercaeDemo.showStatic(); 
		//将实现了IntefercaeDemo的类实例化
		LearnDefault learnDefault = new LearnDefault(); 
		//被Default所修饰的具体方法可以通过引用变量来调用 
		learnDefault.showDefault(); 
	} 
}
```
What is the difference between `static` and `defult`？
~~接口中方法都为抽象方法。~~： **这句话在JAVA8之前是对的，在JAVA8之后就错了**
1.  实现类可以重写default方法，不能重写static方法
2. 如果一个类同时继承了一个类和实现了一个或多个接口，而父类中拥有和接口中default方法相同的签名、返回值的方法时，当该类未重写该方法，直接调用时，将会调用父类中的方法。
3. 如果一个类实现了两个接口，而这两个接口拥有相同方法签名（相同的方法名、参数）、返回类型的default方法时，实现类就必须重写该default方法
