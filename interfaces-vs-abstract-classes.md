# interfaces-vs-abstract-classes

A common interview question for Java Developer positions asks for the
difference between abstract classes and interfaces.

You should be able to clearly explain the difference between the two.

Below is a list of some differences between the two:

    - A class can extend only one class (abstract or not) but can implement
      multiple interfaces
    - Interface variables are implicitly `public static final`. Abstract classes
      can declare any modifiers on instance variables.
    - Interfaces can (as of Java 8) provide default methods, but all others are
      public abstract. Abstract classes can declare any modifiers on their
      methods.

Another type of question relates to why you would use one approach over the
other.

In general, if you wanted to develop and enforce a certain hierarchy of
functionality where state and behavior was tracked, then you would use an
abstract class.

If you want a class to be free to implement functionality without constrained
to a hierarchy, then an interface is a better approach.

