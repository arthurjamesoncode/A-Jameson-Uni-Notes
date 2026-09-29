If you've ever visited any official java documentation, on , you might've wondered how it was made. Did someone write this all out?

The answer is that it was generated with using Javadoc.
## Javadoc
Javadoc is a command line tool to generate API docs (as seen on [oracle](https://docs.oracle.com/)) directly from your source code.

It requires using special "Javadoc comments", which take the form `/** comment */`. This is the same as the multi line comment syntax, meaning that it will be completely ignored by the compiler like any other comments.

Each comment documents the class, interface, or method that appears directly after it. 

They can contain special markup tags which Javadoc can interpret. For example:
- `@author`
- `@param`
- etc.

The class hierarchy of the source code is automatically extracted.

Below you can see an example Javadoc comment for the method `String.charAt()`:
```
/** 
* Returns the {@code char} value at the 
* specified index. An index ranges from {@code 0} to
* {@code length() - 1}. The first {@code char} value of the sequence 
* is at index {@code 0}, the next at index {@code 1},
* and so on, as for array indexing. 
*
* <p>If the {@code char} value specified by the index is a 
* <a href="Character.html#unicode">surrogate</a>, the surrogate
* value is returned. 
* 
* @param       index    the index of the {@code char} value.
* @return      the {@code char} value at the specified index of this string. 
*              The first {@code char} value is at index {@code 0}. 
* @throws      IndexOutOfBoundsException if the {@code index} 
*              argument is negative or not less than the length of this 
*              string 
*/
```

You can invoke Javadoc using the command line. It is part of the JavaSE, so it should be installed on whichever PC you use for Java programming.

If you wanted to use Javadoc to generate docs for all files in a directory called `src` and output them to a directory called `docs` then you could do that with the command below:
```shell
$> javadoc -d docs -author src/*.java
```

`-d` is an option that allows us to provide a directory to store the generated documentation (`docs`).

`-author` is an option that causes it to not drop the `@author` tag.

For more documentation on Javadoc you can view:
- [Oracle Docs](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/javadoc.html)
- [Wikipedia](https://en.wikipedia.org/wiki/Javadoc)
## Version Control
When we program we often might want to:
- Quickly reload code back to an old state;
- Save older versions for safety;
- Collaborate with others;
- Work on independent features simultaneously;
- Find out when and why a code change was needed.

**Version control** is our answer to this problem.

**Version Control Systems (VCS)** can also be called **Source Code Management (SCM)** tools or **Revision Control Systems (RCS)**.

They usually provide:
- A long-term history of every file
- Branching and merging of code
- Traceability, meaning you can annotate code changes
- Rich tool support, such as IDE integration, command line tools, GUIs and dedicated websites.

**Local** version control only takes place on 1 machine. This can be useful for keeping track of your own projects but is not enough if you start to collaborate with other people.

**Centralised** version control systems usually have one central repository which provides the developers working on it with a working copy. They can then make changes to this working copy and merge back into the central repository. Examples include:
- CVS
- SVN

**Distributed** version control systems are when everyone on the system has access to a clone of the full repository. There will often still be a remote repository that functions as the central one, for collaboration purposes, but everyone has access to the full repository and can make full changes on it. Examples include:
- git
- mercurial
- bazaar

I recommend you learn git, and start using it for all your code.

GitHub and GitLab are popular hosting services for git repositories.
