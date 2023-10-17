# What is Maintainability?
- Modularity
	- Change to a component has minimal impact to others
- Reusability
	- Can be used in more than one system
- Analysability
	- Assess the impact on a product or system of an intended change
- Modifiability
	- Modified without introducing defects or degrading existing product quality
- Testability
	- Determine whether those criteria been met
## Considerations
- Software Coding
	- Coding Guidelines
- Software Design and Development
	- Object-oriented Design
	- Design Principles and Patterns
	- Development Strategy
- Solution Architecture
	- Integration patterns
	- Architecture Styles
# S.O.L.I.D Design Principles
- Single Responsibility
	- A class should have one, and only one, reason to change
- Open Closed 
	- You should be able to extend a class's behaviour, without modifying it
- Liskov Substitution
	- Derived classes must be substitutable for their base classes
- Interface Segregation
	- Make fine-grained interfaces that are client specific
- Dependency Inversion
	- Depend on abstractions and not on concrete implementations
# Design Patterns
## What are they?
- A solution to a common software problem
- Patterns are a common design vocabulary, improve documentation and understandability
## When not to use them
- Possibly make code harder to understand
- Increases code size
- Increase performance latency
## Gang of Four (GoF) patterns
![[week10_gof_01.png]]
### Singleton
We might sometimes need only 1 instance of a particular class and thus make it illegal to have more. Creating many objects can also take a lot of time and memory. Especially so if the objects are essentially the same.
#### Intent
Ensure a class only has one instance with a global point of access to it
![[week10_singleton_01.png]]
#### Example Claims System
![[week10_singleton_02.png]]
![[week10_singleton_03.png]]
To implement a singleton,
1) _Make constructor(s) private_ so that there are no outside calls
2) Declare a _single static private instance_ of the class
3) Write a public _getInstance()_ or similar method that allows access to the single instance
![[week10_singleton_04.png]]
### Builder
Imagine a complex object that requires step-by-step initialisation of many fields and nested objects. Often, these are buried inside a large constructor with many parameters or even scattered across client code.
#### Intent
Separate the construction of a complex object step by step which allows for different representations using the same construction process.
![[week10_builder_01.png]]
#### Example Claims System
Using the same example,
![[week10_builder_02.png]]
To make a builder,
1) Encapsulate, create and assemble the parts of a complex object in a separate Builder object
2) Delegate the object creation to a builder object instead of directly
3) (Optional) Extract a series of calls to the builder steps to construct a product into a separate class called Director
![[week10_builder_03.png]]
### Factory
There exist a class to return a specific product. This class then needs to be extended to return other products in the same family. You then have to create more and more classes. This will result in the caller having to write specific codes to instantiate the required products. This will tightly couple code with its callers.
#### Intent
- Define an interface for creating an object, but let subclasses decide which class to instantiate
- Lets a class defer instantiation to subclasses
![[week10_factory_01.png]]
#### Example Claims System
Using the same example,
![[CS301/images/week10_factory_02.png]]
To implement a factory,
1) Create an interface of the product
2) Create concrete classes implementing the interface
3) Create an interface of the creator(factory) class
4) Create a concrete class implementing the creator interface
![[week10_facatory_03.png]]