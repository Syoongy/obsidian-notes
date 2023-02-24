## Building Object-Oriented Software
An app may consist of many objects with dependencies between themselves.
This prompted the need for software containers like Spring or PicoContainer to assemble these objects/components into apps. AKA Dependency Injection(DI).

## Software Components and Services
### Component
A piece of software that can be used without change in its code by other apps. The application can then extend the component's behaviour.
It can be used locally from Classes, Jar files, DLL, etc.
### Service
Similar to a component in the sense that it can be used by other apps.
Used through HTTP, Remote Procedure Call (RPC), Sockets or Messaging.

----
## Dependency Management
```Java
public class Car {  
	private Driver driver;  
	public Car() {  
		this.driver = new Driver();  
	}  
	public void drive () {...}  
}
```
```Java
// code changed in the Driver class  
public class Driver() {...public Driver(License l) ...}  
// unit testing with a mock driver  
createMock(Driver.class)  
// how to give this mock driver to the Car object?
```
The Car class is dependant on Driver while also being responsible for creating a Driver.
If for example, the Driver class now needs a license, there will be many changes required to accommodate this change. This leads to tightly coupled code.
To combat this, we can use Injection
```Java
public class Driver {  
	private License license;  
	public Driver(License license) {  
		this.license = license;  
	}  
}  
// We want Driver to be injected into Car  
// Car does not care where Driver is from, as long as it gets a working one  
public class Car {  
	private Driver driver;  
	public Car(Driver injectedDriver) {  
		this.driver = injectedDriver;  
	}  
	public void drive () {...}  
}
```
Thus, the DI container is responsible for its own object, making unit testing easier.
```Java
@Test  
public void driveMethodTest() {  
	//Create our mock depedencies  
	Driver mockedDriver = createMock(Driver.class);  
	//Inject our mocked classes into the Car  
	Car testCar = new Car(mockedDriver);  
	testCar.drive();  
	...  
}
```
----
## Dependency Injection
This technique is used extensively in Java. Objects define their dependencies through Constructor arguments and properties that are set on object instance.

The DI container injects these dependencies when creating the object
### Inversion of Control (IoC)
The reverse of an object controlling the instantiation/location of its dependencies via construction of classes.
### Characteristics
- Loose coupling is better
- Easier to test
- Java standard
- May be difficult to read and debug
- Dependence on a DI framework

----
## The Spring Framework
- Component-based software development framework
- Spring Core: DI (IOC) container
- DI Configuration
	- XML files or JAVA annotations
	- Auto-config is usually used

`@Inject` tells Spring where injection needs to be applied. It is the standard JSR-330 annotation.
`@Autowired` is specific to Spring and can be used in place of `@Inject`
`@Component` is a simple bean
`@Controller` is a servlet controller
`@Repository` is for data access
Spring searches for these beans and perform injections

----
## Dependency Injection Variants
### Constructor-based
Required dependencies are passed as arguments into the constructor. This also allows for multiple constructors with the need to add `@Autowired` to each constructor.
- This is used for required dependencies as they are passed when instantiating.
- The fields could be final and allows immutable objects.
- Can identify code smell easily
	- Large number of constructor arguments indicates too many responsibilities for the class
```Java
private DependencyA depA;  
private DependencyB depB;  
@Autowired  
public DI(DependencyA depA, DependencyB depB) {  
	this.dependencyA = depA;  
	this.dependencyB = depB;  
}
```
### Setter-based
Required dependencies are declared as fields and the values are set with the setter methods requiring `@Autowired` for each method.
This variant allows for optional dependencies with no immutability.
The drawback is verbose code.
```Java
private DependencyA depA;  
private DependencyB depB;  
@Autowired  
public void setDependencyA(DependencyA depA) {  
	this.depA = depA;  
}  
@Autowired  
public void setDependencyB(DependencyB depB) {  
	this.depB = depB;  
}
```
### Field injection
This requires an `@Autowired` annotation above the respective field resulting in less code to write. This however makes it too easy to add dependencies with no immutability.
This variant also has no way of instantiating the class without all of the required dependencies.
```Java
@Autowired  
private DependencyA dependencyA;  
@Autowired  
private DependencyB dependencyB;
```
## Circular Dependency
For constructor injection only. May have problems of unresolvable dependency where one of the beans has to be injected into the other. This can be resolved through setter injection.
```Java
public class A {  
	private B b;  
	@ Inject  
	public A(B b){...};  
	...  
}  
public class B {  
	private  
	@ Inject  
	public B(A a){...};  
	...  
}
```
Can be converted into
```Java
public class A {  
	private B b;  
	public A(){...};  
	@ Inject  
	public void setB(B b){  
		this.b = b;  
	}  
	...  
}  
public class B {  
	private A a;  
	public B(){...};  
	@ Inject  
	public void setA(A a){  
		this.a = a;  
	}  
...  
}
```

----
## Software Architectures
### Monolithic
This uses a single codebase to implement all functions.
- Easy, fast to develop
- Difficult to maintain over time
- Hard to deploy part of the app
- Not possible to scale a single function
It also promotes one language and one platform. This allows for better compatibility between app components at the cost of flexibility.
The typical components are
- User Interface
- Business Logic
- Database

### Microservices
This allows for a single unit to implement on functionality to support the business requirements. They can be invoked by other apps or services vie a standard interface, independent of language and platform.

Microservices are also loosely coupled where individual services can be implemented, changed, deployed and scaled.

----
## REST: Representational State Transfer
Proposed by R. Fielding in 2000- why do I need to know this.
An architectural style that includes a set of principles, properties and constraints for HTTP-based applications. It utilises web standards such as HTTP, URL, JSON, HTML, etc.
### Application Programming Interfaces (APIs)
This is what enables REST services. They are exposed from the server side.
### HTTP methods
There are 4 main methods that can be safe/unsafe and idempotent/not idempotent
Safe: A method should not change the resource
Idempotent: A method call can be made once or several times in a row with the same result.
- POST
	- Unsafe
	- Not idempotent
- GET
	- Safe
	- Idempotent
- PUT
	- Unsafe
	- Idempotent
- Delete
	- Unsafe
	- Idempotent
### HTTP Text Messages
This is made up of 2 parts, Request and Response.
#### Request
- Method name URI
- Headers
- Body (optional)
#### Response
- Status line (HTTP version status-code status-text)
- Headers
- Body (optional)
These messages can also be returned in JSON format. This is a simple data-interchange format which is human-readable along with also being easy for machines to parse/generate.