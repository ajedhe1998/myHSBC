# Day 18
### Local Class
* We can define class inside scope of another method. It is called local class/method local class.
```java
class Program{  //Program.class
    public static void main(String[] args) {
        //Method Local Class
        class Complex{  //Program$1Complex.class

        }
    }
}
```
* We can not use reference/instance of method local class outside method.
* Types of Local class:
    1. Method Local Inner class
    2. Method Local Anonymous Inner class
#### Method Local Inner class
* In Java, we can not declare local variable/class static.
* Non static, method local class is also called as method local inner class.
```java
public class Program {
	public static void main(String[] args) {
		class Complex{	
			private int real = 10, imag = 20;
			@Override
			public String toString() {
				return "Complex [real=" + real + ", imag=" + imag + "]";
			}
		}
		Complex c1 = null;
		c1 = new Complex();
		System.out.println(c1.toString());
	}
}
```
#### Method Local Anonymous Inner class
* In Java, we can define class without name. It is called annonymous class.
* In Java, we can create annonymous class inside method only hence it is called as method local annonymous class.
* In Java, we can not declare local class static. Hence annonymous class is also called as metod local annonymous inner class.
* Consider following syntax:
```java
Object obj = null;  //object reference / reference
```
```java
new Object( );  //Anonymous instance of class java.lang.Object
```
```java
Object obj = new Object( );  //Instance with reference
```
* Anonymous inner class using concrete class
```java
public class Program {	//Program.class
	public static void main(String[] args) {
		Object obj = new Object() {	//Program$1.class
			private String message = "Hello";
			@Override
			public String toString() {
				return this.message;
			}
		};		
		System.out.println(obj.toString());
	}
}
```
* Anonymous inner class using abstract class:
```java
abstract class Shape{
	protected double area;
	public abstract void calcuateArea( );
	public double getArea() {
		return area;
	}
}
public class Program {	//Program.class
	public static void main(String[] args) {
		Shape sh = new Shape() {
			private double radius = 10;
			@Override
			public void calcuateArea() {
				this.area = Math.PI * Math.pow(this.radius, 2);
			}
		};
		
		sh.calcuateArea();
		System.out.println("Area	:	"+sh.getArea());
	}
}
```
* Anonymous inner class using interface:
```java
interface Printable{
	void print( );
}
public class Program {	//Program.class
	public static void main(String[] args) {
		Printable p = new Printable() {
			private String message = "Good Morning";
			@Override
			public void print() {
				System.out.println(message);
			}
		};
		p.print();
	}
}
```
### Functional Programming
* Book : Java 8 In Action.
* POP : It is programming methodology in which we can solve real world problems using global function and structure.
* OOP : It is programming methodology in which we can solve real world problems using class and object.
* Funtional Programming : It is programming methodology in which we can solve real world problems by chaining/linking functions( pipeline of function ).
* Key features in Java 8 Functinoal Programming:
    1. Interface Default Method
    2. Static interface method
    3. Functional Interface
    4. Lambda expression
    5. Method reference
    6. Java 8 streams.
### Lambda Expression
* Expression is a statement which may contain:
    1. Literals / constants
    2. Variables
    3. Operators
* Example:
```java
    int num1 = 10, num2 = 20;
    int result = num1 + num2;   //Arithmetic Expression 
```
* "->" operator is called lambda operator. Its meaning is "goes to".
* If expression contains lambda operator then such expression is called lambda expression.
* Syntax:
    - FunctionalInterface ref = ( Input params )-> { Lambda Body };
    - Input parameters goes to lambda body.
    - If lambda body contains single statement then use of  { } is optional.
* Lambda expresion is also called as Anonymous method.
* Abstract method of Functinoal interface is called Functinoal method / method descriptor.
* To implement functional interface we should define lambda expression
* If interface contains single abstrasct method then it is called functional interface.
```java
@FunctionalInterface
interface Printable{
	void print( );	//Functional method / Method descriptor
}
```
```java
Printable p = ( )-> System.out.println("Inside Lambda Expresion");
p.print();
```
* Consider another example:
```java
@FunctionalInterface
interface Printable{
	void print( String message );	//Functional method / Method descriptor
}
public class Program {	//Program.class
	public static void main(String[] args) {
		//Printable p = ( String msg )-> System.out.print(msg);
		//Printable p = ( String message )-> System.out.print(message);
		//Printable p = ( message )-> System.out.print(message);
		Printable p = message -> System.out.print(message);
		p.print( "Have a nice day." );
	}
}
```
* Consider another example
```java
@FunctionalInterface
interface IMath{
	int sum( int num1, int num2 );
}
public class Program {	//Program.class
	public static void main(String[] args) {
		IMath m = ( num1, num2 )-> num1 + num2;
		int result = m.sum(10, 20);
		System.out.println("Result	:	"+result);
	}
}
```
* Consider another example:
```java
@FunctionalInterface
interface IMath{
	int factorial( int number );
}
public class Program {	//Program.class
	public static void main(String[] args) {
		IMath m = number ->{
			int fact = 1;
			for( int count = 1; count <= number; ++ count ) {
				fact = fact * count;
			}
			return fact;
		};
		
		int result = m.factorial(5);
		System.out.println("Result	:	"+result);
	}
}
```
* Consider example
```java
public class Program {	
	public static void main(String[] args) {
		List<Integer> list = new ArrayList<>( );
		list.add(10);
		list.add(20);
		list.add(30);
		
		//Consumer<Integer> action = ( Integer number)-> System.out.println(number);
		//list.forEach(action);
		
		list.forEach( ( Integer number)-> System.out.println(number) );
	}
}
```
### Method reference
```java
@FunctionalInterface
interface Printable{
	void print( );
}
public class Program {	
	public static void showRecord( ) {
		System.out.println("Inside showRecord() method");
	}
	public void displayRecord( ) {
		System.out.println("Inside displayRecord() method");
	}
	public static void main(String[] args) {
		Printable p1 = Program::showRecord;
		p1.print();
		
		Program prog = new Program(); 
		Printable p2 = prog::displayRecord;
		p2.print();
		
		Printable p3 = System.out::println;  
		p3.print();
		
	}
}
```
* Consider Example:
```java
public static void main(String[] args) {
    List<Integer> list = new ArrayList<>( );
    list.add(10);
    list.add(20);
    list.add(30);
    
    list.forEach( System.out::println );
}
```
### String Handling
* In Java, string is a collection of character object.
* If we want to manipulate String then we can use:
    1. java.lang.String
    2. java.lang.StringBuffer
    3. java.lang.StringBuilder
    4. java.util.StringTokenizer
#### String
* It is a final class declared in java.lang package.
* It implements Serializable, Comparable<String>, CharSequence interface.
* String is not buit-in / primitive type in Java. It is a class hence it is considered as reference type.
* We can create String instance with and without new operator.
* Consider example:
```java
String s1 = new String("SunBeam");  //OK : String Instance => Heap
```
```java
String s2 = "SunBeam";  //OK : String Literal => String Literal Pool
```
* String s2 = "SunBeam" is equivalent to
```java
char[] data = {'S','u','n','B','e','a','m'};
String str = new String( data );
```
* String objects are constant. If we try to modify its state then new string instane gets created. In other words, String objects are immutable objects.
* If we want to concatenate strings then we should use "concat()" method.
* If we want to concatenate string and variable of primitive/non primitive type then we should use operator.

### StringBuffer and StringBuilder
* Both are final classes declared in java.lang package.
* Both are used to create mutable String object.
* It is mandatory to use new operator to create their instance.
* Even though both are final, equals and hashCode() method is not overriden inside it.
* StringBuffer is thread-safe/synchronized whereas StringBuilder is unsynchronized.
* StringBuilder is introduced in JDK 1.0 and StringBuffer is introduced on JDK 1.

### Reflection
