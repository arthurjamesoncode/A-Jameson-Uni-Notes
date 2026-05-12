## Model-View-Controller (MVC) Pattern
The "Model-View-Controller" pattern is a commonly used way to break down applications with a user interface.

It breaks the application into 3 parts:
- The internal representation of the the information (**Model**)
- The presentation of the information to the user (**View**)
- How the application responds to user input (**Controller**)

We've covered classes and general programming concepts during this course, so in terms of representing information internally (the model), we should be pretty good at that by now.

In terms of view and controller though, we have been restricted to just text input in a terminal until now. This lecture is going to be spent going over graphical ways to present information (**view**), and the ways we can allow users to interact with these GUIs (**controller**).
## View
Graphical ways to interact with computers have been around for a long time. They were conceptualised in the 60s, commercialised near the end of the 70s and widely used in the 80s.

Pretty much any graphical user interface uses:
- Windows
- Icons
- Menus
- Pointer
although these are not requirements.

When we make GUIs we usually use pre-defined packages (or toolkits) which come with a lot of components (also called widgets). Widgets could be things like:
- Buttons
- Sliders
- Menus
- Containers (used to structure the layout of the GUI)

A GUI for a specific application is built out of these components.

For example take the following low res image off the lecture slides.
![[gui_example.png]]

This is an application GUI consisting of:
- A frame (top level container widget)
- A panel inside the frame
- A grid layout inside the panel
- Radio buttons inside the grid layout
Along with a number of other containers and widgets.

In OOP languages, every widget is an instance of a widget class which extend more general container classes.
## Java GUI Toolkits
Java's GUI framework is mostly based in the "Swing" library. The original GUI framework is called the "Abstract Windowing Toolkit" (AWT).

Swing isn't completely different from AWT since Swing components inherit from the core AWT components. The newer Swing components typically have names that being with `J` to help distinguish them from AWT components.

For example AWT has a `Frame` class and a `Button` class while Swing has a `JFrame` class and a `JButton` class.

If we wanted to build a GUI using Swing, we would first need to create a main window frame for our application. Pretty much all GUI applications will have this.

We need to import the components from the `javax.swing` library in order to use them. We can also import all the swing components with `import javax.swing.*`.

Once we have access to the `JFrame` class we can create a frame like so, passing in a string for the title of the window.
```java
JFrame frame = new JFrame("Main Title")
```

If we want to change the title of the window we can do so with 
```java
frame.setTitle("new title")
```

Inside of this frame we can continue to add components to match the functionality that we want.
### Rest of Lecture
The rest of this lecture goes a bit more into Java GUI toolkits, including how to handle user input in the form of events.

This might be really valuable for you, but I personally cannot be bothered to write a detailed guide on this like much of the other content given that it will not show up in our exam.

If you want to get good at GUIs in Java, the best way is to just build some simple GUI apps. 

You can then just get the required information about specific components from [here](https://docs.oracle.com/javase/8/docs/api/javax/swing/package-summary.html) or any number YouTube tutorials such as [this one](https://www.youtube.com/watch?v=Kmgo00avvEw) by Bro Code.

I personally don't recommend following YouTube tutorials unless you get entirely stuck, or just want an introduction to the topic. There's an all too common experience of finishing a YouTube tutorial and going to start an actual project but then realising that you still don't really know where to start. 

They can be useful to get you started but I find there is no better way to learn how to code something than a blank file and a willingness to read docs. 