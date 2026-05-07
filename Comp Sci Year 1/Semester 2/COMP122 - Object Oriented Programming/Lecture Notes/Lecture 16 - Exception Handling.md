An Exception is an anomalous situation that requires special processing:
- The contents of a file doesn't match the specification
- A user passes in an argument that breaks the program, such as `arg=0` to a function which divides by `arg`
- etc.

The concept of these comes from before OOP or Java, and most languages have some kind of standardised way to manage error handling, separating it from normal code.

The general pattern in software is the "Try-Catch" pattern. This means that:
- Code is run while the computer is aware that something can go wrong (**Try**)
- If something goes wrong, there is a handler which can deal with the exception (**Catch**)

In pseudocode this pattern is
```
try 
	do stuff // dangerous code .. errors may happen
catch exception 
	deal with it // handler 
```

You may hear people talk about exceptions being **raised** or **thrown**. This usually depends on the programming language they are used to. In **Java** we say **thrown**.
## Exceptions In Java
In OOP languages like Java, exceptions are **objects**. When an anomalous situation occurs:
- An Exception object is created and "thrown". This contains information about the error case.
- The JVM looks for and calls a matching handler.
- If no handler is found (the exceptions occurs outside of a try-catch statement), the program will terminate and the exception is shown with the error message.

**Importantly**, in Java, Exceptions are **NOT** Errors:
- An error is a serious problem usually caused by the environment. An application can't (or at least shouldn't) be dealing with these issues. For example, running out of memory.
- An exception is caused by the application itself and can often be recovered from. For example, a user gives invalid input.

Every exception in Java fits into one of two categories:
- **Checked Exceptions** 
- **Unchecked Exceptions**

**Checked Exceptions** are exceptions that the compiler forces us to deal with. 

If a method you write contains code which can throw a checked exception, Java will not let you compile unless you either:
- Catch and handle it;
- Declare in the method declaration that it can throw this type of exception.

**Unchecked exceptions** can still be thrown or handled, just like checked exceptions, but the compiler doesn't enforce it. All the exceptions which extend `RuntimeException` are **unchecked exceptions**.

Below you can see the hierarchy tree for Errors and Exceptions.
![[exception-hierarchy.png]]
### Checked Exception Example
Look at the code snippet below
```java
public class ReadFromKeyboard { 
	public static void main (String args[]) { 
	// System .in. read () reads one byte from stdin
	int myChar = System.in.read();
	System.out.println((char) myChar);
	}
}
```

If we were to try and compile this we would see
```bash
$ javac ReadFromKeyboard.java 
ReadFromKeyboard.java:18: error: unreported exception IOException; 
	must be caught or declared to be thrown 
		int myChar = System.in.read(); 
		                         ^ 
1 error
$
```

This doesn't compile because `System.in.read()` can throw the **checked exception** `IOException`. In order for our code to compile, we must either **handle** this exception, or not handle it but declare that `main` may throw `IOException`.

The easier (but not always best) method is to **rethrow** the exception. This is done by using the `throws` keyword in the method declaration like so
```java
public class ReadFromKeyboard { 
	public static void main (String args[]) throws IOException { 
	// System .in. read () reads one byte from stdin
	int myChar = System.in.read();
	System.out.println((char) myChar);
	}
}
```

An alternative is to surround the "dangerous" code in a try-catch statement, which provides a handler to deal with the exception like so
```java
public class ReadFromKeyboard { 
	public static void main (String args[]) throws IOException { 
		try {
			// System .in. read () reads one byte from stdin
			int myChar = System.in.read();
			System.out.println((char) myChar);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
### Try-Catch Blocks
Java uses the `try` keyword to introduce potentially dangerous code, and the `catch` keyword for introducing exception handlers.

A `catch` block must follow a `try` block and there can be multiple exception handlers for one `try` block. Every `catch` block must declare which type of exception it handles. This is how the interpreter searches for an appropriate handler.

The catch block is then handed an **Exception object**, which we can give any valid identifier to. In the example above we chose `e` as the identifier. This object contains information about the exception that we have caught, such as an error message and the stack trace.

Try-Catch statements can also include a `finally` block. This is code that will be executed in any case, so either after the `try` block is successfully completed or an error is caught and handled.

The general syntax for a try-catch block is
```java
try { 
	// dangerous code that may throw XException , YException, ZException
} catch (XException e) {
	//handle XExceptions
catch (YException e) { 
	// handle YExceptions
} catch (ZException steve) {
	// handle ZException
} finally { 
	// will eventually get executed in any case
}
```

Notice how the identifier can be anything we choose, and you don't need to select unique identifiers for the objects passed to different catch blocks.

>Note if `RuntimeException`, `Exception`, or any general exception class are caught in a catch block, they will also catch all of their child objects. This can lead to bugs if you forget that a specific exception can occur and needs to be handled different.
>
>As a result, you should try and make the exceptions that you catch as specific as possible.
### Unchecked Exception Example
The example given above uses `System.in.read()`. This is a method can throw the checked exception `IOException`.

Alternatively you can use `java.io.Scanner` to collect input using the methods:
- `int nextInt()`
- `long nextLong()`
- `double nextDouble()`

These methods **do not** throw **checked exceptions**, but they may throw subclasses of `RuntimeException` (unchecked exceptions) if they are trying to pass the "wrong kind" of input.

Take the program below
```
import java.util.Scanner;

public class ReadLong {
	public static void main (String args []) {
		// Create a Scanner instance
		Scanner scan = new Scanner (System.in); 
		System.out.print("Enter an integer (or long): "); 
		
		// Try to get a long as input. This can create an exception if something
		// other than numbers are entered, or if a number with a decimal
		// point is input , etc. 
		long l = scan.nextLong(); 
		System.out.println(l);
	}
}
```

This program will compile, and on a lot of "nice" inputs it will be behave as expected. 
```
$ java ReadLong 
Enter an integer (or long ): 43234
43234
```

If the user gives an input which doesn't work however, this will throw a runtime exception.
```
$ java ReadLong 
Enter an integer (or long ): fdafdas 
Exception in thread "main" java.util.InputMismatchException 
	at java.util.Scanner.throwFor(Scanner.java:864) 
	at java.util.Scanner.next(Scanner.java:1485) 
	at java.util.Scanner.nextLong(Scanner.java:2222) 
	at java.util.Scanner.nextLong(Scanner.java:2182) 
	at ReadLong.main(ReadLong.java:19) 
$
```

In order to stop this so that our program works we need to check for this `InputMismatchException` using a try-catch block.

```
import java.util.Scanner;

public class ReadLong {
	public static void main (String args []) {
		// Create a Scanner instance
		Scanner scan = new Scanner (System.in); 
		System.out.print("Enter an integer (or long): "); 
		
		try {
			long l = scan.nextLong();
			System.out.println(l);
		} catch (InputMismatchException e) {
			System.out.prinln("Give me an invalid input again, and I will personally ensure we come for you first when AI takes over.)
		}
	}
}
```

So now our program works just like it did before, but also gives a much needed warning to any meat sacks who haven't learnt their place.