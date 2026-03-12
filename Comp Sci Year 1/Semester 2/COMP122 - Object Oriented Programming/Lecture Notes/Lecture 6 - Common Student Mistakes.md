## Compiler Errors
When submitting code to CodeGrade, the first check is that the code compiles and runs without error. 

This is incredibly important, and should be checked locally before uploaded. When submitting labs and exercises this doesn't matter, as you have time to recognise that it won't compile before the deadline. During your exam, however, you are on a much stricter deadline and, especially if you make your submission close to the end of the exam time, the tests may not have time to complete before your submission.

In general, we can solve these errors by simply reading the error and then editing the file in some way.
### Missed Declarations

For example consider the `Declarations.java` file from the week 2 labs. When trying to compile this code we get the following error:
```shell
$ javac Declarations.java 
Declarations.java:7: error: cannot find symbol
        double weightDifference = newWeight - currentWeight;
                                              ^
  symbol:   variable currentWeight
  location: class Declarations
1 error
```

Here you can see the location of the error the compiler raises
```shell
Declarations.java:7
```
in the form `File.java:line`, followed by the error itself
```shell
error: cannot find symbol
```
the text of the line causing the error
```shell
        double weightDifference = newWeight - currentWeight;
```
and some extra information about the error
```shell
  symbol:   variable currentWeight
  location: class Declarations
1 error
```

The `cannot find symbol` error means that the identifier being provided, `currentWeight`, has not been declared. This tells us that, if we want our code to compile, then we must go back into our code and declare `currentWeight` somewhere.
### Incorrect Declarations
Consider the following code snippet from the `CShanty.java` file from the week 3 labs.
```java
for(i = 0; i < n; i++) {
	System.out.println("Soon may the compiler come,");
	System.out.println("To bring class files and exceptions");
}
```

If we try to compile this code we get the following errors:
```shell
$ javac CShanty.java
CShanty.java:7: error: cannot find symbol
        for(i = 0; i < n; i++) {
            ^
  symbol:   variable i
  location: class CShanty
CShanty.java:7: error: cannot find symbol
        for(i = 0; i < n; i++) {
                   ^
  symbol:   variable i
  location: class CShanty
CShanty.java:7: error: cannot find symbol
        for(i = 0; i < n; i++) {
                          ^
  symbol:   variable i
  location: class CShanty
3 errors
```

You can see this code gives us 3 `cannot find symbol` errors. This tells us that our variable `i` was never actually declared.

This is because the `i = 0` segment from the first part of the for loop is meant to be the declaration, but the `int` has been omitted. This causes java to not recognise the declaration as a declaration, and as such means that it can't recognise `i` as a variable.
## Other Errors
The rest of this lecture keeps going over common errors and I can't bring myself to write about them in the same level of detail. So instead I'm listing the rest of the errors here quickly.

This module is 100% graded by actual programming, the only real way to get good at that is by practice.
### Taking Input
Be careful of taking input in the correct way. In particular in the Newton's Method lab, you are asked to take input through the command line arguments not the scanner.

The scanner is the normal way to take keyboard input while the program is running, while command line arguments are passed to the program as it is executed.

If a lab asks you to take input in one way and you write your program to process a different kind of input then your program will fail the CodeGrade tests.
### Main Method Signature
The main method always has the signature:
```java
public static void main(String[] args)
```

If you do not include any part of that, whether it be `public`, `static`, `void`, `main`(all in lower case), or `String[] args` then the main method won't be recognised as the main method by Java.

>The name of the identifier `args` is the only customisable part of the statement as method signatures only care about the type and number of arguments, not their name.

Also, if you do not take in a `String[]` as a parameter of this method you wouldn't be able to access any of the command line arguments anyway.
### Case Sensitive Identifiers
Identifiers in Java are case sensitive. You must be careful to use the correct names.

`LeapYear` is not the same as `leapYear` and if you mix them you will get `cannot find symbol` errors.




