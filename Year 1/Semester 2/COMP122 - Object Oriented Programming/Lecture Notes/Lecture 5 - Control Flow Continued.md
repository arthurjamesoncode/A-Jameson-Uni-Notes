## If-Else Example
We learned about if-else statements [[Lecture 4 - Intro to Java Control Flow#If-Else Statements|last lecture]], but lets now run through an example.

Consider the java code below, what do you think it will do?

```java
if (myValue > 0)
	if (myValue % 2 == 0)
		System.out.println("positive and even");
else 
	System.out.println("not positive");
```

On a first glance, this code seems to check if the code is positive, then check if it's also even. 

So if the value is both positive and even then it will print "positive and even" otherwise if it is not positive it will print not positive.

However the actual output looks like this
![[if-else-table.png]]

So why is it not doing what we think it should? The reason is that we haven't used curly braces to enforce which code should go inside the `if` block and the `else` block.

If you are familiar with Python, you may expect your programming languages to care about indentation. This is not the case with Java.

When Java is compiled, all of the white space is removed. So how does java determine what should be in the `if` block and the `else` block? The answer is that the **next** statement to follow the `if (<condition>)` line is placed inside the `if` block, and the next statement to follow the `else` line is placed inside the else block.

Curly braces collect a whole group of statements into 1 statement (or block), which can then all be placed inside of the relevant block. If curly braces are not used, it runs through the next sequentially until it sees a complete statement.

Usually it would determine that it has seen a full statement when it comes across `;` which indicates the end of a statement. However, in the case of an if statement, if will continue to look for an `else` statement, and the block of code it should execute. 

What this means for this code block is that the `else` block is actually an alternative for the inner `if` statement, not the outer one.

Indentation is useful for making your code easy to read, but it does not enforce any kind of control flow. With some exceptions, it is pretty much always a good idea to use curly brackets to ensure your code does what is expected.

## Loops
### For-Loop
A for-loop is used to repeat a block of code for a fixed number of times. The syntax for a for loop is as follows:
```java
for (<initialisation>; <condition>; <update>;) {
	<statements>
}
```
- `<initialisation>` is a statement which is executed before the first time the loop runs. This usually initialises a iterator, for example `int i=0`
- `<condition>` is a statement which evaluates to a boolean. Before each iteration, the loop checks if `<condition>` evaluates to true, and stops execution if it evaluates to false.
- `<update>` is a statement which is executed at the end of each iteration, before the `<condition>` is evaluated.

For example consider the following example loop which prints out all numbers from 1 to 10:
```java
for (int i = 1; i <= 10; i++){
	System.out.println(i)
}
```

It is important to make sure that the `<update>` statement moves us closer to the end condition, in order to avoid an infinite loop.
### While-Loop
A while loop repeats some code while a condition is true. The syntax for a while-loop is as follows:
```java
while (<condition>) {
	<statements>
}
```
`<condition>` is a statement which evaluates to a boolean.

The while loop will first check that `<condition>` is true. If it is true, it will then execute the condition, and if false it will stop execution. It will check the same thing before every iteration.

A **do-while** loop is a variation on the while loop which will always run the code once, and then repeat it while the condition is true. It looks like the following:
```java
do {
	<statements>
} while (<condition>)
```

Again you must be careful that your code moves you closer to terminating your loop, otherwise you could end up in an infinite loop.
## Methods
In many of the code snippets so far we have used the line of code
```java
System.out.println("Hello!");
```
What exactly is this line of code?

This is a statement in which we **call a method** named `System.out.println` which takes a single `String` parameter.

Here's another example:
```java
double twoSquared = Math.pow(2.0, 2.0)
```
This statement calls a method called `Math.pow` that has two parameters of type `double` and returns a `double`.

So what are methods? They:
- Are defined inside of a class definition;
- Can have arguments and a return value, but don't have to have either;
- Correspond to "functions" or "procedures" in other languages;

Methods **belong** to the class they are defined within. Some methods are **static** and don't require an instance of a class.

In the previous examples `Math.pow` is not actually the method. `pow` is the method and `Math` is the class that it belongs to. This is an example of a **static** method, meaning that we can call it by referencing the `Math` class, not an instance of it. We will go into more detail about this later.

The syntax for defining a method is like so:
```java
<modifiers> <returnType> methodName (<parameter1>, <parameter2>, ...) {
	<statements>
}
```
- `<modifiers>` determine how the method can be accessed
- `<returnType>` is the type of the value that the method returns
- `methodName` is an identifier.
- `<parameter1>` and the following parameters are a comma separated list of arguments, each given in the format `<type> identifier`.
- `<statements>` is the body of the method that it will execute if called. If the return type is anything other than void the last line of statements must be `return <value>` where `<value>` is the same type as `<returnType>`

For an example class with some methods look below:
```java
public class MaximumDemo {
	
	public static int maximum(int a, int b) {
		if (a >= b) {
			return a;
		} else {
			return b;
		}
	}
	
	public static void main(String[], args) {
		int x - 27
		int y = 13
		System.out.print("The maximum of " + x + " and " + y + 
						 " is " + maximum(x,y))
	}
}
```
### Method Signatures
The modifiers, type of the method, spelling of the identifier, and types and orderings of the parameters together all form the **signature** of the method. 

This signature is what java uses to uniquely identify the method.

Consider the following class:
```java
public class Test {

  public static int max (int a, int b) {return a;}
  public static int maX (int a, int b) {return a;}
  public static int max (int a, double b) {return a;}
  public static int max (double b, int a) {return a;}

  public static void main (String[] args) {
    System.out.println(max(1, 1));
    System.out.println(maX(2, 1));
    System.out.println(max(3, 1.0));
    System.out.println(max(1.0, 4));
  }
}
```
Java sees no problem with this, as all of these methods are distinguished by different things. As a result, if we were to run this code it would output
```
1
2
3
4
```
As each method is called. It can differentiate all of these by the types that are passed to them or by the identifier.
## Random Walk Example
Now that we've seen the basics of how to put together programs in Java let's try our hand at solving a problem.

Consider the following problem: "A person, having had several drinks at one of their local pubs, starts to walk home. At each step, he is equally likely to walk one street to/away from their home. How long (on average) does it take to reach his home if he starts n streets away from home?"

We could use maths to try and determine an average number of steps dependent on $n$, but instead lets use Java to model this situation, and run it thousands of times to get an average.

As all we are concerned about is whether he gets closer to, or further from, his home we can just use a single number to measure the distance. As he is equally likely to move away from his house as he is to move towards it, we can say that 50% of the time we need to increase the distance, and 50% of the time we need to decrease it.

Then we simply run the program in a while loop until distance hits 0, measuring the number of steps it takes.

Further than this we can run a for loop testing this program for various different values of $n$.

First lets set up our class with the following skeleton code:
```java
public class Drunk {
  public static void main (String[] args) {

  }
  
  static int getSteps (int pos) {

  } 
}
```
This is just our class, main method, and the method we will be writing our first code in `steps`. The purpose of the `steps` method is to check how many steps it takes the drunk in one simulation, starting `pos` streets away.

In order to do this we will need to use `Math.random` this is a method that gives us a random number between 1 and 0. We can combine this with `Math.floor`, which rounds down to the nearest integer, in order to get a random whole number from a selection. We can then use this random whole number to determine if the drunk gets closer to or further from his house.

The full code for this method looks like this:
```java
public class Drunk {
  public static void main (String[] args) {
    System.out.println(getSteps(5));
  }

  static int getSteps (int pos) {
    int steps = 0;
    
    while (pos > 0) {
      int direction = (int) Math.floor(2*Math.random()); //gives direction a value of either 1 or 0 with equal probability
      
      if (direction == 1) pos++;
      else pos--;
      
      steps++;
    }
    
    return steps;
  }
}
```

So now if we run the code we will get the number of steps it takes the drunk to walk home in a given simulation. This could be 25, it could be 8, it could be 857. But how about we try to find the number of steps on average over a number of iterations for a given $n$. 

Lets start with defining the number of simulations to run as a constant, as well as our starting steps. Then we just need to use a for loop to run the correct number of simulations, adding the steps of each one to a total, and then output this total divided by the number of simulations.

The full code is below:
```java
public class Drunk {
  public static void main (String[] args) {
    final int SIMULATIONS = 100;
    final int START = 5;

    int total = 0;
    for (int i = 0; i < SIMULATIONS; i++) {
      total += getSteps(START);
    }
    System.out.println(total/SIMULATIONS);
  }

  static int getSteps (int pos) {
    int steps = 0;
    
    while (pos > 0) {
      int direction = (int) Math.floor(2*Math.random()); //gives direction a value of either 1 or 0 with equal probability
      
      if (direction == 1) pos++;
      else pos--;
      
      steps++;
    }
    
    return steps;
  }
}
```

If we run our code now, it will print the average of running 100 simulations, but what if we wanted to test our code for different values of $n$. Well we can do so by changing `START` from a constant to a variable and running another for loop, which changes the value of start.

You can see the full code below:
```java
public class Drunk {
  public static void main (String[] args) {
    final int SIMULATIONS = 100;
    
    for (int start = 1; start <= 20; start++) {
      int total = 0;
      for (int i = 0; i < SIMULATIONS; i++) {
        total += getSteps(start);
      }
      
      System.out.println(start + ": " + total/SIMULATIONS);
    }
  }

  static int getSteps (int pos) {
    int steps = 0;
    
    while (pos > 0) {
      int direction = (int) Math.floor(2*Math.random()); //gives direction a value of either 1 or 0 with equal probability
      
      if (direction == 1) pos++;
      else pos--;
      
      steps++;
    }
    
    return steps;
  }
}
```
Now when we run our code it will give us some output in the form:
```
1: 97
2: 77
3: 315
4: 46370
5: 4680
6: 91310
7: 4448
8: 6345
9: 4398
10: 2638
11: 2552
12: 5295
13: 41806
14: 54807
15: 193676
16: 10406
17: 360348
18: 241686
19: 53707
20: 61111
```
Where each line is the starting distance and the average number of steps it takes to reach home.