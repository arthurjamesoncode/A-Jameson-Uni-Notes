## `File` Objects
We have seen how we can read from and to files using **streams** & **readers/writers**.

Java also provides us with class, `java.io.File`, which is used to represent files in the OS. This class provides methods to interact with the file system including:
- deleting/renaming files;
- creating new directories;
- listing the files in a given directory;
- etc.

If you want detailed in depth information you can look to the oracle docs [here](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)

The objects themselves actually represent abstract pathnames, rather than full files. You can think of the objects themselves as "File handlers". Their main benefit is to provide ways to interact with the file system which don't depend on the system your program is running on.

For example, Windows uses the backslash `\` as the separator between directory names, but Linux and MacOS use the forward slash `/` instead. The installation of the java runtime environment (JRE) knows which separator the system it is installed on needs, and as a result `File` offers a `separator` attribute which can be used and works regardless of the system you are on.

The other methods provided by the `File` class similarly abstract the specific details of what reading/writing/etc needs to look like on your system.

So
```java
File fn = new File ("data/output.txt");
```
works on Linux and MacOS systems but won't work if run on a windows system.

However
```java
File fn = new File ("data" + File.separator + "output.txt");
```
will work regardless of which system it is run on.
## Example
Imagine we want to create a class which counts the total number of lines in a text file.

We need some way of accessing this file, and then reading the contents of this file line by line in order to count it.

We can create a file handler for the file (we'll assume we have the directory hard-coded), and then we can pass this into a scanner which we can use to read the file line by line.

When working with files we need to be careful. File handling methods often throw exceptions since we can never be sure what a user will have on their machine. This means they will often throw exceptions that we must handle. You can see how we handle the `FileNotFoundException` below.

```java
import java.io.File; // import the File object 
import java.io.FileNotFoundException; // import the Exception
import java.util.Scanner;

/** 
  * A class that demonstrates how to check for a "file not found" error. 
  * @author Patrick Totzke 
  * @version 1 
*/ 
public class CountLinesInFile {
	public static void main (String[] args) {
		File fileHandler; // object representing the file
		Scanner scanner; // object to read from a file 
		int counter = 0; // counts the lines of text
		
		String fileName = "text-file.txt";
		fileHandler = new File (fileName); // create File object
		try { 
			// Attempt to open the file. May throw FileNotFoundException 
			scanner = new Scanner (fileHandler); 
			//file was opened successfully. Iterate through it 
			while (scanner.hasNextLine()) {
				scanner.nextLine();
				counter ++;
			} 
			System.out.println (fileName + " has " + counter + " lines.");
		} catch (FileNotFoundException fnfe) {
			System.out.println(fnfe); // Oops , print out the error!
		}
	} // end of " main " method
}
```

But what about if we wanted to be able to pass the name of the file we want to count into our program. To do this is simple we must just use the `String[] args` argument. This contains the arguments passed to a Java program when run from the console.

So we could do so like this
```java
import java.io.File; // import the File object 
import java.io.FileNotFoundException; // import the Exception
import java.util.Scanner;

/** 
  * A class that demonstrates how to check for a "file not found" error. 
  * @author Patrick Totzke 
  * @version 1 
*/ 
public class CountLinesInFile {
	public static void main (String[] args) {
		File fileHandler; // object representing the file
		Scanner scanner; // object to read from a file 
		int counter = 0; // counts the lines of text
		
		String fileName = args[0]; //gets filename from arguments
		fileHandler = new File (fileName); // create File object
		try { 
			// Attempt to open the file. May throw FileNotFoundException 
			scanner = new Scanner (fileHandler); 
			//file was opened successfully. Iterate through it 
			while (scanner.hasNextLine()) {
				scanner.nextLine();
				counter ++;
			} 
			System.out.println (fileName + " has " + counter + " lines.");
		} catch (FileNotFoundException fnfe) {
			System.out.println(fnfe); // Oops , print out the error!
		}
	} // end of " main " method
}
```

>Note that if we call this with no arguments we will get an error. You can handle these cases by checking the number of arguments using `args.length`.
