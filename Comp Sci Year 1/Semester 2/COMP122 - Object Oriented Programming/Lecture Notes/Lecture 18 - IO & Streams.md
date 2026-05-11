## I/O in Java
Input and output are very important parts of writing programs in any programming languages.

The types of I/O in Java include:
- Command-line arguments
- `System.in` and `System.out`
- Reading from and writing to files
- Graphical User Interfaces (GUIs)

A lot of I/O in java is handled in the form of **streams**. This note will be spent going over streams and simple I/O.
## Stream
A stream is an endless flow of data. You can read from a stream or write to a stream, and each stream must be connected to either a **data source** or **destinations**.

In Java, streams are objects. They have different sources/destinations as well as different basic units (bits/bytes/characters/object).

The two basic kinds of steams in Java are:
- `InputStream`/`OutputStream` - Which are **bytes-based** streams.
- `Reader`/`Writer` - Which are **character-based** streams.

These are abstract classes, meaning they define functionality but not a strict implementation. You can view the docs for these abstract classes, as well as their solid implementations [here](https://docs.oracle.com/javase/8/docs/api/java/io/package-summary.html).
## Bit/Byte Streams
Bits and bytes are low-level and uninterpreted representations of information. A bit is a single 1 or 0, and a byte is 8 bits.

Bits are too small to really be used much in a high level programming language like Java, so instead we use **bytes**. Java has two data types to represent a single byte:
- `byte` - a primitive type representing the numbers 0-255
- `Byte` - an object wrapper for the `byte` data type

Below you can see an example of a byte-based input stream in Java
```java
InputStream inStream = new FileInputStream("textfile.txt");

int data = inStream.read();

while (data != -1) {
	char c = (char) data; //converts integer to character
	System.out.print(c); // prints character 
	data = inStream.read();
}

inStream.close();
```

This program reads every byte in a file, prints each character and then closes the open input stream.

The first line opens a stream called `inStream` with source `textfile.txt`. 

`inStream.read()` returns an `int` which is either a number between 0 and 255 inclusive (the value of the byte) or -1 which represents the end of the file. It must use an `int` because if it was a byte it would not have a spare value to indicate end of file.

The last line closes `inStream`.

The way this is done is somewhat problematic. Specifically there are exceptions that can occur when reading from a file, and if any of these exceptions occur while reading from `inStream` then `inStream` will not be closed. 

This isn't a serious problem for little problems like the ones we will complete for the 122 labs/exam but can matter a lot if there was sensitive data in that file that we don't want to expose outside of this method.

The safer way to do this is to wrap this in a try catch statement and use the `finally` block to close the file, like so
```java
try {
	InputStream inStream = new FileInputStream("textfile.txt");
	
	int data = inStream.read();
	
	while (data != -1) {
		char c = (char) data; //converts integer to character
		System.out.print(c); // prints character 
		data = inStream.read();
	}
} catch (IOException e) {
	e.printStackTrace()
} finally {
	inStream.close();
}
```
Now we ensure that `inStream` closes no matter what happens.

Java 7 introduced a **try-with-resource** construct which automatically closes the stream. You simply need to declare the input stream in the beginning of the try block like so
```java
try (InputStream inStream = new FileInputStream("textfile.txt")) {
	int data = inStream.read();
	
	while (data != -1) {
		char c = (char) data; //converts integer to character
		System.out.print(c); // prints character 
		data = inStream.read();
	}
} catch (IOException e) {
	e.printStackTrace()
}
```

This works because `InputStream` implements the `AutoCloseable` interface.

Each instance of an `InputStream` has the method `available()`, this returns the estimated number of bytes which can be read from this stream before it blocks (can not give us anything). If the end of the stream is detected, then `inStream.available()` will be 0. This means we can also use `inStream.available()` to check whether we can read from `inStream`.
## Character Streams
Characters are higher level (compared to byte) representations of single symbols.

Characters, unlike bytes, require interpretations. There are a number of different encodings into bits/bytes available including:
- ASCII-code to translate between bytes and symbols commonly used in the west. It uses 8-bits and therefore 1 character is 1 byte.
- Unicode to translate between many more symbols. Popular encodings are UTF-8 and UTF-16. You can read more about this [here](https://en.wikipedia.org/wiki/Unicode).

In the language of `java.io`, `Streams` are byte based and `Reader`/`Writer`s are character based.

Below you can see an example of a character based input stream, used similarly to how we used a byte based input stream
```java
try (FileReader fr = new FileReader("textfile.txt")) {
	int data = inStream.read();
	
	while (data != -1) {
		char c = (char) data; //converts integer to character
		System.out.print(c); // prints character 
		data = inStream.read();
	}
} catch (IOException e) {
	e.printStackTrace()
}
```

You can see that the way we use it is identical to the `InputStream`. The main difference is that `Reader`s can be passed a `Charset` which indicates how to map sequences of bytes to sixteen bit Unicode code units.

If not passed a charset, the reader will use the platforms default charset.
## Nested Streams
A powerful feature of Java's streams is the ability to be nested. You can create a type of stream which internally uses another, lower-level stream for the plumbing.

Examples of this are:
- Adding write/read buffers to increase efficiency
- Filtering the stream contents
- Object based streams

For example let's look at the `BufferedWriter` class in action. Take the following code snippet.
```java
FileWriter fw = null;
BufferedWriter writer = null;

try (fw = new FileWriter (args[0])) {
	try (writer = new BufferedWriter (fw)) {
		writer.write("The quick brown fox jumped over the lazy dogs.");
		writer.newLine();
		writer.write("" + 200);
		writer.newLine();
	}
} catch (IOException err) {
	err.printStackTrace();
}
```

The `BufferedWriter` (called `writer`) defined in the inner try block uses the `FileWriter` (called `fw`) internally.

The "buffer" allows writing to the actual file to be delayed at first and then written in bulk. This is often faster than writing to the file multiple times successively. 

You need to make sure to **flush the buffer** (or close it) to ensure that all the information in the buffer is written to the file. In the code snippet given this is done by using the try with resources pattern.

The `newLine()` method writes a platform specific newline character.

>Note that the `FileWriter` constructor will create (or **overwrite**) the file provided. If you want to add to the end of a file, then you must use an alternate constructor. You can read about this in the `java.io` docs ([here](https://docs.oracle.com/javase/8/docs/api/java/io/package-summary.html))

## `System.in`, `System.out`, `System.err`
There are a number of "sinks" which hold the I/O and error information for a command line program.

These are:
- Standard Input (`stdin`) - The source of input data for command line programs (defaults to the keyboard). This is accessible in Java as `System.in`
- Standard Output (`stdout`) - The output sink for command line programs, by default this prints on the terminal. This is accessible in Java as `System.out`
- Standard Error (`stderr`) - The destination for error messages, by default also the console. This is accessible in Java as `System.err`

In Java, these are all `Stream` objects and offer `write`, `read`, and other convenience methods. You can read more about these [here](https://docs.oracle.com/javase/7/docs/api/java/lang/System.html).
## Scanners
Javas standard library has a class that allows you to read a bunch of different types of data: `java.util.Scanner`.

It offers the following methods:
- `next()`
- `nextBoolean()`
- `nextByte()`
- `nextDouble()`
- `nextFloat()`
- `nextInt()`
- `nextLine()`
- `nextLong()`
- `nextShort()`
Which allow it to grab the next instance of a given data type in a stream, or just the next value.

If the next thing to be read doesn't match (can't be converted to) the data type given then it will cause an error. Scanners have a number of methods of the form `hasNext()` or `hasNextType()` to determine if there is more to read, and what types it can be read as.

Scanner also has a number of constructors, that allow to read directly from files, paths, or any `InputStream`. For instance, `new Scanner(System.in)` will read from standard input, whereas `new Scanner("somefile.txt")` will read from a text file. 

You can read more about scanners [here](https://docs.oracle.com/javase/7/docs/api/java/util/Scanner.html)