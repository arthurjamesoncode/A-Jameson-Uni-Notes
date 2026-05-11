## Writing Custom Exceptions
All exceptions are objects of type `java.lang.Exception` which means that we can create our own custom exceptions by extending this class, or one of it's subclasses (e.g. `RuntimeException`).

When creating our own exceptions, we need to think about a few things:
- Is there a built in exception which works for our purposes?
- Is it an exception that can be recovered from, and so the compiler should check for it (**checked exception**)?
- Is it an exception which should stop the program in most cases (**unchecked exception**)?

In the first case, we don't need to make a custom exception at all. We should always consider this before we write a new exception. Slightly further down is a list of a bunch of useful exceptions that already exist within Java.

In the second case we need to extend `Exception`, and therefore create a **checked exception**. In the third case, we want to extend `RuntimeException` and therefore create an **unchecked exception**.

There are a number of useful exceptions that Java comes with, including:
- `ArithmeticException` - Invalid arithmetic operations such as dividing by 0
- `ArrayIndexOutOfBoundsException` - Trying to access an index that is negative or larger than or equal to the length of the array
- `FileNotFoundException` - Trying to access a file which doesn't exist or isn't accessible
- `NullPointerException` - Referring to methods or attributes of a null object
- `RuntimeException` - Any exception that can occur during runtime (not checked for at compile time)
- `StringIndexOutOfBoundsException` - Using an index that is negative or larger than or equal the length of the `String` object
## Example
How about if we wanted to create an custom exception called `NegativeNumberException` which could be thrown when:
- A method which can only take **positive number values** is passed a **negative number**
- A user inputs a negative number when they should input a positive
- etc.

We could do so like this
```
/** An exception for complaining abut negative integers */
public class NegativeNumberException extends Exception {

	public NegativeNumberException () {}
	
	public NegativeNumberException (String message) { 
		super(message)
	}
	
	public NegativeNumberException (Throwable cause) {
		super(cause)
	}
	
	public NegativeNumberException (String message, Throwable cause) {
		super(message, cause);
	}
}
```

We define the exception, and give it four constructors. The arguments of these match a constructor that the superclass `Exception` has, and so in every case (except default) we call `super` with the arguments.

This functionally just adds a label via the name of the exception. There is no real other point of using this custom exception over just a standard `Exception`, although saying that like this undersells just how important it can be to provide these labels.

Note that since we extended `Exception` and not `RuntimeException` this is a **checked exception**,  meaning that we must declare our methods to throw it or define a handler for it.
## Using Custom Exceptions
We use custom exceptions the same way we use normal exceptions. The main difference is there is no situation when a custom exception will be thrown automatically, we must always decide to throw them.

Imagine we wanted to make a class which reads an integer from the user, and prints it. It only wants to take positive integers so we need to check for negative numbers and throw this exception if so.

```
import java.util.Scanner;
import java.util.InputMismatchException;

public class ReadNonNegLong {
	
	public static void main (String args []) throws NegativeNumberException {
	// Create a Scanner object to read from "standard input"
	Scanner scan = new Scanner(System.in);
	// Try to get a long as input. This can throw a RuntimeException 
	try {
		System.out.print ("Enter an integer (or long ): "); 
		long l = scan.nextLong();
		if (l < 0) {
			throw new NegativeNumberException ("Sorry, your input is negative!")
		} 
		System.out.println(l);
	} catch (InputMismatchException e) 
		System.out.println("Oops! That input wasn’t an integer");
	}
}
```

Note that since we created a checked exception, and it isn't handled by the try-catch statement, we **must declare** that our `main` methods `throws NegativeNumberException`.

If we were to try and use this program now we can see
```
$ java ReadNonNegLong 
Enter an integer (or long ): -12 
NegativeNumberException: Sorry, your input is negative! 

$ java ReadNonNegLong 
Enter an integer (or long): five 
Oops! That input wasn’t an integer 

$ java ReadNonNegLong Enter an integer (or long): 343 
343
```

Notice how for both of the first two cases our program complains. Since we "handle" `InputMismatchException` it simply prints the defined message but since we just "throw" the `NegativeNumberException` it shows us the exception name and also the message we passed into it.

