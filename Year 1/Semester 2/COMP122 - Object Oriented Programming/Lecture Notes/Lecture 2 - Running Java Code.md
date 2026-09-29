## Compilers vs Interpreters
There are 2 main ways of turning source code written in a high level language into machine readable code. These 2 ways are **compilers** and **interpreters**.

**Compiler:**
- Translates source code into executable binary code all at once.
- The full code is analysed and checked for errors before the code can be executed.
- Compiled binary code is specific to each architecture and operating system.
- Many different languages are compiled: Cobol, Fortran, C, Haskell

**Interpreters:**
- Interpreters translate and execute source code a single line at a time.
- This is slower than a compiler but doesn't require the whole code to be compiled before it can be executed.
- Source code is run directly on the system using an interpreter.
- Many languages use an interpreter: Perl, Bash, Python, JavaScript
## Running Java Code
Java uses a combination of a compiler and interpreter. 

First you must install Java. For windows or mac you can visit [Adoptium](https://adoptium.net/temurin/releases) and install java for your machine. You can check that you have installed it correctly by running `java -version` in your terminal. If it shows something, like below you have installed it correctly.
```
openjdk 13.0.1 2019-10-15
OpenJDK Runtime Environment (build 13.0.1+9)
OpenJDK 64-Bit Server VM (build 13.0.1+9, mixed mode, sharing)
```

If you are running Linux you can just install it with your package manager.

When you first write code in java, you write it inside of a `.java` file. 

Below is the code from the first lab exercise.

`Hello.java`
```java
public class Hello {
	public static void main(String[] args) {
		System.out.println("Please enter your name:");
		
		java.util.Scanner scanner = new java.util.Scanner(System.in);
		String name = scanner.nextLine();
		
		System.out.println("Hello " + name + "!");
	}
}
```

Do not worry about what the specific code is doing, you simply need be concerned with running it at the moment.

Once we have our code written we can go into our terminal, and run this command, making sure we are in the same directory 
```
>javac Hello.java
```
This will generate a new file in the same directory called `Hello.class`. This file contains, Java byte code. Which is then interpreted by the java virtual machine (JVM) at run time before being run on your PC.

To run your code you do
```
>java Hello
```
>Note that you don't need to write `Hello.class` or `Hello.java`

If you change anything inside the `Hello.java` file, you must recompile it before those changes are reflected in the `Hello.class` file.

You can also specify a directory for your byte code to compile in, like so
```
>javac -d build Hello.java
```

If you run the above command in your terminal, instead of generating the `Hello.class` file inside the same directory, it will generate the `Hello.class` file inside a folder called build. 

This is because the `-d` tells the command line to place the compiled code inside the chosen directory (that's what the d stands for). If you are on a Unix based system or using git bash on windows then this will create a new folder. On windows you may need to run 
```
mkdir build
```
to create a folder called build before you run the code.

To run java code from a different folder, you need to use the `-cp` flag (which stands for class path). 

So to run the code in the build folder we use
```
>java -cp build Hello
```
