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
### Adapter
You need to integrate an external code base to your existing code base. The interfaces however, are not compatible and you cannot change the external codes. This will get extremely messy if we used only conditionals.
#### Intent
- Convert the interface of a class into another interface clients expect
- Adapter lets classes work together that couldn't otherwise due to incompatible interfaces.
![[wk11_adapter_01.png]]
#### Example Claims System
Using the same example,
![[wk11_adapter_02.png]]
To implement an adapter,
1) Create an interface of the adapter
2) Create concrete(adapter) class implementing the adapter interface
3) Let the adapter compose the adaptee
4) Implement the logic to adapt the adaptee
![[wk11_adapter_03.png]]
![[wk11_adapter_04.png]]
### Facade
You must make your objects work with external objects (e.g. third party code). We would need to encapsulate some objects from external, keep track of dependencies, execute methods in the correct order, etc. Thus, the business logic of our classes would become tightly coupled to the implementation details of 3rd party classes, making it hard to comprehend and maintain.
#### Intent
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use
![[wk11_facade_01.png]]
#### Example Claims System
![[wk11_facade_02.png]]
To implement a facade,
1) Create an interface and methods for the set of services behind the facade
2) Create concrete (service) class implementing the service interface
3) Create concrete (facade) class to hide these services
4) Implement the logic for client to call through the facade
![[wk11_facade_03.png]]
![[wk11_facade_04.png]]
### Observer
You have a popular class whose state is wanted by many other classes. Those classes can keep checking the popular class but it would be inefficient
#### Intent
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically
![[wk11_observer_01.png]]
#### Example Claims System
![[wk11_observer_02.png]]
To implement an observer,
1) Create an interface of the subject with methods to register, notify and unregister
2) Create concrete (subject) class implementing the subject interface
3) Create interface with methods for the observer
4) Update concrete (observer) to implement the interface
5) Register observers to the subject

![[wk11_observer_03.png]]
![[wk11_observer_04.png]]
### Chain of Responsibility
You are tasked to perform a series of checks sequentially before returning the result. These checks depend on the input value and can vary (optional checks). Writing these checks in a conditional manner creates messy and unmaintainable code.
#### Intent
Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it
![[wk11_cor_01.png]]
#### Example Claims System
![[wk11_cor_02.png]]
To implement a chain of responsibility,
1) Create an interface of the handler
2) Create concrete (approver) class implementing the handler interface
3) Chain up the handlers (approvers)
![[wk11_cor_03.png]]
![[wk11_cor_04.png]]
