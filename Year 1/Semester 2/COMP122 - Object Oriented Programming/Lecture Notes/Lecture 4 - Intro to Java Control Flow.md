## Different Types of Variable
There are a few different types of variable in Java. 
### Class Variables
Class variables are declared inside of a class, but outside of any method or block. They must be declared using the  `static` keyword, type, and identifier. They are also called `static` variables.

Class variables are accessible inside every method of a class, and can also be accessed without even initialising the class. They are the same for every instance of a given class.

If a class variable is not initialised they will use the default value from the table under [[#Default Variables]]. 
### Instance Variables
Instance variables are declared inside of a class but outside of any method or block.  They declared simply using the type and identifier.

Instance variables are accessible inside every method of an instance, and are different for every instance. 

If an instance variable is not initialised they will use the default value from the table under [[#Default Variables]]. 
### Local Variables
Local variables are declared inside of a method. They are declared simply using their type and identifier.

Local variables are only accessible inside of the method they are declared in and will be have a value determined every time the method is called.

Local variables must be initialised. If you don't initialise a local variable, you will get an error.
### Default Variables
Below you can see a table giving the default values for every primitive data type in Java.

| Type    | Default | Size    | Range                           |
| ------- | ------- | ------- | ------------------------------- |
| byte    | 0       | 1 byte  | -128 to 127                     |
| short   | 0       | 2 bytes | -32,768 to 32,767               |
| char    | u0000   | 2 bytes | 0 to 65,535                     |
| int     | 0       | 4 bytes | -2,146,483,648 to 2,146,483,647 |
| long    | 0L      | 8 bytes | $\pm9.22e^8$                    |
| float   | 0.0f    | 4 bytes | 6-7 digits precision            |
| double  | 0.0d    | 8 bytes | 15-16 digits precision          |
| boolean | false   | 1 bit*  | true or false                   |
>\*boolean represents 1 bit of information but doesn't have a defined size. It depends on the virtual machine that runs the byte code
## Common Mistakes
When writing Java code, there a number of simple syntax mistakes that are easy to make.

Every statement, or (informally) line, in Java must end with a semi-colon. Ending a line without a semi colon will cause an error at compile time.

When writing multi-line comments, it is very easy to accidentally end the comment too early. If you do this the compiler may complain as code that should be written in a comment may not have a valid syntax when taken out of the comment. Similarly if you start writing a multi-line comment, you must close them or all of your code may be commented out.

You must also be careful to close brackets and quotes. Double quotes are called **string literals**, and single quotes indicate characters. Any kind of unclosed quotes and brackets will cause errors at compile time.

You must also be careful when writing out method names and identifiers, as Java is case sensitive. So `num` and `Num` are different.

Finally you must be careful to name your **main** method and **classes** correctly. The name of the class should be the same as the name of the file and start with a capital letter. The name of your main method should always be **main** in all lower case.

Below you can some code with some of these common mistakes in in:
```java
/*
	* Author : Patrick Totzke
	* The Welcome class implements an application */
	* that prints out a welcome message .

public class Welcome {
	// --------------- METHODS - - - - - - - - - - - - -
	/* Main Method */
	public static void mian (String [] args) {
		System.out.println("Welcome to COMP122")
		System.out.println("This is going to be easy!);
}
```

If we fix these errors we get code that looks like:
```java
/*
	* Author : Patrick Totzke
	* The Welcome class implements an application
	* that prints out a welcome message .
*/

public class Welcome {
	// --------------- METHODS - - - - - - - - - - - - -
	/* Main Method */
	public static void main (String [] args ) {
		System.out.println("Welcome to COMP122");
		System.out.Println("This is going to be easy!");
	}
}
```

If you struggle learning syntax, don't worry. Just attempt some coding exercises and, when you mess up, your IDE or your compiler will let you know. Eventually, you will become proficient in syntax just through practice.
## Control Flow
Control flow is when you use conditions to determine which parts of your code get executed.

We will look at what some valid conditions are as well as 2 methods of control flow today, `if-else` statements and `switch` statements.
### Conditions
Conditions are any expression that evaluates to a boolean. 

Some of the most common conditions will look like:
- `a == b` to check equality
- `a != b` to check inequality
- `a < b` or `a > b` to check order
- `a <= b` or `a >= b` to check both order and equality
- `A && B` to check if conditions `A` and `B` are both true
- `A || B` to check if either condition `A` or condition `B` are true
- `!A` to check if condition `A` is not true
### If-Else Statements
If-Else statements check a condition and then, if the condition is true, execute some code within the `if` block. If the condition is not true the code in the `else` block is executed instead. You can chain together if-else statements. The `else` block is optional, and is not required to have a valid if statement.

The syntax for it looks like this:
```
if (condition) {
	<statements>
}
```
OR
```
if (condition) {
	<statements1>
} else {
	<statements2>
}
```
OR
```
if (condition1) {
	<statements1>
} else if (condition2) {
	<statements2>
} else {
	<statements3>
}
```
And so on.

Consider the following problem: 

"Write a Java program that takes a single integer as input. 

If the input is less than 50, add 10 and return the result raised to the power of 4. 

Otherwise, simply return the input raised to the power of 4"

We can solve this problem using an if statement.

You can see a sample solution below:
```java
public class Power4 {

	public static void main (String[] args) {
		int input = 101;
		
		if (input < 50) input = input + 10;

		int result = (int) Math.pow(input , 4.0);
		System.out.println(result);
	}
}
```

Notice how, since this program doesn't need an else block and the code inside the `if` block is only one line, we don't actually need curly brackets to indicate the `if` block. Instead a semi-colon is sufficient.
### Switch Statement
The switch statement is used for making a choice between several possible outcomes. You need a variable to compare with a collection of “cases”. You can include a “default” case at the end, that will be executed if none of the cases match.

You can handle situations like these using only a chain of if-else statements, but sometimes it may be clearer or more readable to use a switch statement.

The general structure of a switch statement below:
```
switch (variable){
	case case_1 : 
		// code
		break;
	case case_2 : 
		// code
		break;
	...
	case case_n : 
		// code
		break;
	default: 
		// code
		break;
}
```
A switch statement looks at every "case" statement and checks if it is equal to the variable. So the first block of code would execute if `variable == case_1` and so on. 

After it encounters a case that equals `variable` it will then execute every statement written within the switch statement until it hits a `break` statement, including statements written under. If you place a `break` statement after each case this functions the same as a chain of `if-else` statements.

You can see an example switch statement below:
```
int x = <some number>

switch (x) {
	case 1:
	case 2:
		break;
    case 3:
        System.out.println(x);
        System.out.println("Blah");
    case 4:
        System.out.println(x);
        System.out.println("Bglah");
    case 5:
        System.out.println(x);
        System.out.println("Nyah");
        break;
    default:
	    System.out.println(x);
        System.out.println("Guah");
}
```

If `x` is 1, this statement will execute everything after the `case 1` line until the first `break` statement it encounters. In this case it would execute nothing as the first `break` statement comes before any lines of code are executed. This is the same for if `x` is 2.

If `x` is 3, it will execute the code under `case 3:`, `case 4:`, and `case 5:` as the first `break` statement comes at the end of `case 5:`, and so the output is
```
3
Blah
3
Bglah
3
Nyah
```

If `x` is 4, it will execute the code under `case 4:`, and `case 5:` as the first `break` statement comes at the end of `case 5:`, and so the output is
```
4
Bglah
4
Nyah
```

If `x` is 5 it will only execute the code under `case 5:`, as the first `break` statement comes at the end of `case 5:`, and so the output is
```
5
Nyah
```

If `x` is 6 (or any number greater), the only code executed will be the code under `default:`, as none of the other cases are a match, and so this would output
```
6
Guah
```

