# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD)[^4] is gaining traction mainly in video game development. Some of its fundamental principles can be applicable to other areas of software development. 

By bringing these two paradigms together, we can create testable, scalable, modular architecture to handle complexity better and consistent project structure to reduce the model-code gap[^5] .

## Hexagonal Architecture 

### Philosophy  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> 
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control).   

![App and oursite world](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)
 

Our application does not know anything about IO devices and should not depend on them. But an IO device must implement an adapter for connecting to our application through its ports. 

### Implementation   

> Hexagonal Architecture, allows an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
> 
> -- Alistair Cockburn  

![Application](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hex.png)

This is our application written in TypeScript and driven by a test. It uses in memory repository to save users.  

![code](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Code.png)

"addUser" is the only **Use Case** of our application. The use case has a **Business Logic** that checks whether name is empty and save this user to the repository.   

We can build our entire use cases with all business logic inside, using only unit tests. We don't need databases or external interfaces or UI. We can then add the infrastructure elements and other things necessary to make it a functional application.  

Our test, the **Driving Adapter** calls our application use cases. We can swap it with a CLI application or  a REST service.  Similarly we can swap the **Driven Adapter** with the MongoDB, PostgreSQL or a Web Service call. We can do that without modifying application's original source code, we only need to add new adapters. (a.k.a. Open-Closed Principle[^6])

## Data Oriented Design

>  The purpose of all programs, and all parts of those programs, is to transform data from one form to another.  
>  
>  -- Mike Acton  

In his famous [talk](https://www.youtube.com/watch?v=rX0ItVEVjHc)[^7] at CppCon, Mike Acton describes data oriented design principles. Data Oriented Design (DOD) approach is to focus on the data and to think about transformation of data.  
  
### Transformation

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-DOD.png)


We are developing software systems with logical parts (or layers). Each part may need different data models and/or transformation functions.     

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Transformer.png)

For the perspective of the DOD; repositories, gateways or UI patterns like MVC, MVVM or MVP; all the patterns are transformation mechanisms.  

### Solving Problems

> - If you don't understand the data you don't understand the problem.  
> - Understand the problem by understanding the data.  
> - Different problems require different solutions.  
> - If you have different data, you have different problem.  
> - If you don't understand the cost of solving the problem, you don't understand the problem.
> - Solving problems you probably don't have creates more problems.
> - There is no ideal, abstract solution to the problem.  
>
> -- Mike Acton

Today, Software developers try to create abstract model of the problem domain by focusing on classes and their relationships as taught in school. Hence, they tend to neglect to understand the properties of data. 

Data-oriented design forces you to think about your data first and foremost: what it is, what is its shape and size, how it is processed and how it flows between the different stages of your program. 

DOD's standpoint is to separate data and behavior. Thus we can achieve; simplified thinking, better performance, better testability. 

> Programmer's job is not the write code; Programmer's job is to solve (data transformation) problems.  
> 
> -- Mike Acton

## DoHex  

 DoHex is yet another Hexagonal Architecture that **Component based**[^8], **Event Driven**[^9] and Data Oriented. 

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Architecture.png)

The architecture is made up of components that communicate with each other. Each component is developed separately; is encapsulated in its own package and has its own ports, adapters and all the implementation details inside. Component functionalities can only be used through its own ports. We can think components like in memory **Microservices**.  

### Component

A component can contain 1 App, 1 Core and many Adapters as needed.

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-component.png)

* **App**: It's the essential part of the component. Other parts are optional but all components must have one app. This is the application logic of the component. It coordinates other parts and contains automation functionalities. App also contains Ports. **Ports** are interfaces that define contracts between app and adapters.  Use cases of the component are exposed to driving adapters as a function in this part.  

* **Core**: This is the business logic or domain logic part of the component. It contains real world business rules. If domain logic of the component is very simple, we can omit this part and combine application and business logic into use cases of the app part. You may still want to use **Object Oriented Design** for some of your components business logic. In this case, change this part's name to **Domain** and put your domain entities here.     

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-OO.png)

* **Adapters**: Adapters are the connection point of the IO devices. Driving adapters call app use cases and Driven adapter functionalities are called by use cases of the app based on the application logic of the component.  

* **Lib**: Library is the transformation unit of the containing part of the component. The purpose of all parts of a program is to transform data. Therefore, all parts (adapter, app, core) may need this transformation unit. A library consist of data models and/or transformation functions. Transformation functions are stateless and deterministic. Libraries can be put into any part of the program and do exactly the same thing, transform data: JSON to an object, an object to another type of object (mapping), an object to a boolean (validation), an object to a SQL string, etc.  

Each component can have a different complexity, we can omit unnecessary parts and libraries. Also we don't need to pass data to deepest part of the component if it is not necessary. A part might decides to directly return its response to the caller part but we should try to be consistent for part responsibilities. 

Component parts and libraries provide facade interfaces as a service for usability and testability. Except adapters, component parts are **Side Effects**[^10] free. Thus we can develop internal functionalities of these services by test driven development(TDD) techniques. In this way, we can decouple unit tests and internal implementations of the component for easier refactoring and we make deeper classes[^11] as a bonus.

### Event Bus And Scheduler

Event bus and scheduler are the essential concepts for this architecture. Event bus is the implementation of the **Pub-Sub Design Pattern**[^12] and it is the way to enable efficient communication between different components without them being aware of one another. Scheduler let you run functions periodically at pre-determined intervals and incentives developers to think asynchronously.

Event bus and scheduler should be directly injected to the app constructor instead of an adapter. This will create path of least resistance for developers and encourage them to write loosely coupled, asynchronous components and **Reactive**[^13] systems with less effort. 


## Project Structure

Well organized and consistent project structure reduces developer cognitive load and development time, increases readability and maintainability. Also it reflects your architectural decisions and designs. Therefore it can help you to reduce the model-code gap[^5]


![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-structure.png)

```
acl					--> anti corruption layer for external dependencies (implement facade or adapter)
components
    customer
    notification
    orders
    payment
    product
    shipping
libs				--> shared libraries
```
**acl:** Anti corruption layer[^14] for external dependencies and legacy applications. Instead of directly using them, we should implement facade or adapter pattern for these dependencies.  
**components:** This is where we put each component as a folder.  
**libs:**  It contains shared libraries. In case of we need shared model and/or transformation functions among the components. However you should be cautious about using shared libraries, because they create coupling.
```
acl	
components
    customer
	    adapters
	    app
	    core
    notification
	    adapters
	    app
    orders
    payment
    product
    shipping
libs
```
```
	customer
        adapters
	        InMemoryCustomerRepository.java
	        SqliteCustomerRepository
		        SqliteCustomerRepository.java
		        lib
        app
            CustomerAppService.java 						--> Test
            lib
	            CustomerAppLibService.java					--> Test
	            models
	                AddCustomerRequest.java
	                AddCustomerResponse.java
	            transformers
            ports
                ICustomerRepository.java
        core
	        CustomerCoreService.java						--> Test
	        lib
		        CustomerCoreLibService.java					--> Test
	            models
		            Customer.java
```
This is the expanded view of the customer component. Structuring and naming conventions are visible. "Service" keyword is added at the end of the each facade classes that you should write unit tests. 

## Notes

* Event bus is the preferred communication type for components but there are others. Design of your system might look like this:

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hybrid.png)     

* DoHex only expects polymorphic behavior from a programming language. Hence we can use Java, JavaScript, C++, C#, Python; or modern languages that are not considered as OO like Rust and Go or old structural programming languages like C (by vtable[^15]).

* Hexagonal Architecture is already used in embedded systems.[^16] DoHex architecture can be used for frontend, backend and embedded applications. 

* DoHex is quite suitable for organization-wide usage. It enables technical ubiquitous language among teams and projects although these projects have been developed in different languages and platforms. Furthermore, it enables those projects to communicate with each other easier.

* DoHex allows us to develop and test our application as a monolith and if it is needed, deploy it also as a microservices application with reasonable effort. 

* When out-process robust communication is needed, **Event Sourcing** can be used. We can directly connect necessary components to a event streaming platform through its adapters, or we can connect our event bus to a event streaming platform.  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Deployment.png)

## Conclusion

In summary; DoHex changes developer's focus to components and component communication, data and data transformation instead of layers, entities. 

DoHex provides simple and consistent way to structure your components in 3 parts: **app** handles application logic and provides ports for adapters, **core** handles business logic, **adapters** handles side effects; connects IO devices and manages states, and **lib** provides data transformation functionalities for these parts.  
 
I believe, there are no silver bullets. Every project is different and we always need to evaluate the context before implementing any ideas. Take this post as an inspiration for your future projects.

This is my second attempt to write about DoHex Architecture. The first one was getting too long and complicated. I decided  to split into multiple post.  Concurrency and thread models, transactions, component communications, adapter organization, scaling, testing, refactoring, deployment are the remaining topics.


### References
[^1]: Hexagonal architecture https://alistair.cockburn.us/hexagonal-architecture/
[^2]: Onion architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
[^3]: Clean architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[^4]: Data Oriented Design https://www.dataorienteddesign.com/dodmain/
[^5]: Model-code gap https://www.georgefairbanks.com/software-architecture/model-code-gap/
[^6]: Open-Closed Principle https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[^7]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc
[^8]: Package by component http://www.codingthearchitecture.com/2015/03/08/package_by_component_and_architecturally_aligned_testing.html
[^9]: Event driven architecture https://en.wikipedia.org/wiki/Event-driven_architecture
[^10]: Side effects https://en.wikipedia.org/wiki/Side_effect_(computer_science)
[^11]: Classes should be deep https://akshaykhot.com/classes-should-be-deep/
[^12]: Pub-Sub Design Pattern https://www.enjoyalgorithms.com/blog/publisher-subscriber-pattern
[^13]: Reactive Manifesto https://www.reactivemanifesto.org/
[^14]: Anti-corruption Layer (ACL) https://deviq.com/domain-driven-design/anti-corruption-layer
[^15]: Virtual method table https://en.wikipedia.org/wiki/Virtual_method_table
[^16]: Hexagonal Architecture for Qt Embedded Applications https://embeddeduse.com/2021/11/07/my-talk-hexagonal-architecture-the-standard-for-qt-embedded-applications-at-meeting-embedded-2021/


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDIzODEyOCwtMTUxNTkzMTEzOCwtMT
M4MTI2MzMyNiwzMDE2Nzk1MjksODg2MzA5OTc1LC0xNTM1NDc1
NjY3LC00NzAzNjg0ODIsLTQzNzY1NzU0NywtMTY5NTIxMjY1Ni
wxMTI5MjEyNTcsLTY5MzE4MDg3NCwtOTYyNzE5NjgxLC0xNTMz
OTg2NDI5LC0xNDkyMTAyNTAzLDEwNjI1NzkyNDMsNjYzMzg1OT
g1LDExOTY3NjI2MTgsLTExNzc5NDMyMjMsOTkzMzgzMzMxLC0y
MDc0NDI1MjIxXX0=
-->