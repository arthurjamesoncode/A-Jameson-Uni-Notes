## Private & Protected Attributes and Methods
If we specify an attribute or method to be **private** or **protected** it means they cannot be accessed directly by other objects.

To interact with an object, we must use its **interface**, which is its **public** methods or attributes.

For example if we were to instantiate some instances of the `Square` class from [[Lecture 8 - Objects & Classes|last lecture]], we would not be able to access their size or colour directly since they are **private** attributes.

```java
Square blueSquare = new Square(5, blue)

System.out.println(blueSquare.size) 
//gives an error since size is a private attribute
```

It is good practice to declare attributes as private or protected.

If you look below you can see a table of the accessibility of variables declared with different keywords.

|              | Class | Package | Subclass (same pkg) | Subclass (diff pkg) | World |
| ------------ | ----- | ------- | ------------------- | ------------------- | ----- |
| `public`     | +     | +       | +                   | +                   | +     |
| `protected`  | +     | +       | +                   | +                   |       |
| *no modifer* | +     | +       | +                   |                     |       |
| `private`    | +     |         |                     |                     |       |

## Accessors/Mutators
As we said, it's good practice for our attributes to be private.

If private attributes need to be obtained by another class, the programmer can provide public **accessor** functions (**get methods**) that will return the values. These only show the current value of the attribute so there is no risk of them being changed unfairly.

If another object needs to be able to change the value of private or protected attribute we can add **mutator** functions (**set methods**) which can change the value.

It's good practice to provide as few accessors and mutators as needed. It is up to the designer of the class to decide which private attributes need accessor and mutator methods.

