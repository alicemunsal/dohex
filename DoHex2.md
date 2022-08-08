# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD)[^4] is gaining traction mainly in video game development. Some of its fundamental principles can be applicable to other areas of software development such as Frontend, Backend and Embedded. 

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

Our test, the **Driving Adapter** calls our application use cases. We can swap it with a CLI application or  a REST service.  Similarly we can swap the **Driven Adapter** with the MongoDB, PostgreSQL or a Web Service call. We can do that without modifying application's original source code, we only need to add new adapters. (aka Open-Closed Principle[^6])

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

* **Adapters**: Adapters are the connection point of the IO devices. Driving adapters call app use cases and Driven adapter functionalities are called by use cases of the app based on the application logic of the component.  

* **Lib**: Library is the transformation unit of the containing part of the component. The purpose of all parts of a program is to transform data. Therefore, all parts (adapter, app, core) may need this transformation unit. A library consist of data models and/or transformation functions. Libraries can be put into any part of the program and do exactly the same thing; transform data: JSON to an object, an object to a another type of object (mapping), an object to a boolean (validation), an object to a SQL string, etc.  

Each component can have a different complexity, we can omit unnecessary parts and libraries. Also we don't need to pass data to deepest part of the component if it is not necessary. A part might decides to directly return its response to the caller part but we should try to be consistent for part responsibilities. 

Component parts and libraries provide facade interfaces as a service for usability and testability. Only adapters have **Side Effects**[^10]; app, core, lib does not. Thus we can develop internal functionalities of these services by test driven development(TDD) techniques. In this way, we can decouple unit tests and internal implementations of the component for easier refactoring and we make deeper classes[^11] as a bonus.

### Messaging And Scheduling

Messaging and scheduling are essential concepts for this architecture. Therefore we may want to inject them directly to the **app** constructor instead of an adapter. 


## Project Structure

Well organized and consistent project structure reduces developer cognitive load and development time, increases readability and maintainability. Also it reflects your architectural decisions and designs. Thus it can help you to reduce the model-code gap[^5]


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
**components:** This is where we put each component as a folder.  
**libs:**  It contains shared libraries. In case of we need shared model and/or transformation functions among the components. However you should be cautious about using shared libraries, because they create coupling.
**acl:** Anti corruption layer[^12] for external dependencies and legacy applications. Instead of directly using them, we should implement facade or adapter pattern for these dependencies.  
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

* DoHex is not depended on any programming language.
* Messaging and scheduling are essential for this architecture. Therefore   




CQRS is natural
freedom 
High level project structure is the way to connect your software architecture to your source code.
Developers dont much to learn about

Reflecting this selections and drawings into code is considered as the part of the design process

Direct writing instead of thinking about structring your classes and naming

we can start with monolith and split them into microservices
programming is organizing thinking with diagrams, bunch of boxes and lines.
If we use Hexagonal Architecture and Data Oriented Design principles together with  
encourage programmers
encourage reactivity 
lib incentives developers to think for data and transformation
Messaging and scheduling incentives and directing developers to think async and create loosely coupled system. 
we can still use oop in core. 
cognitive load
least resistance path
least effort
organizational project structure
portable code
u can use go, rust, c, c++, java with the same structure

component oriented is natural fit for hexagonal architecture

Immutable data types
side effect free
data behavior 
DTOs, CQRS
Different langs. and Modern langs.
Threading

testing is easier, changing is easier

We don't need a library, if implicit transformation provided by the external frameworks or data is passed directly to the inner layers or our data model is a simple data type like int, double, string.  

> There are only two hard things in Computer Science: cache invalidation and naming things. 
> --Phil Karlton

we can add lib if we need model or transformation
sample app design, folder structure graphs and model code gap  

Software Architecture is the blueprint of the software system. It is about making fundamental choices that are hard to change. Selecting languages, paradigms, tools, frameworks, methodologies and drawing large number of boxes and lines at the board are the parts of the architectural process.  

One of the reason of the invention of the CQRS Pattern[^13] is, domain entities are not suitable for complex queries. So we decided to separate queries from the domain. Query part of this pattern is not obey the Object Oriented Design, it's Data Driven.

lib may have models and/or transformers folder. models folder contains data models named DTOs, POCOs, POJOs, Records or Structs depends on what language you are using. transformers folder contains transformation functions for these data models.    


## Conclusion
 
I am a software architect actively developing softwares. I believe, there are no silver bullets. Every project is different and we always need to evaluate the context before implementing any ideas. Take this post as an inspiration for your future projects.

This is my second attempt to write about DoHex Architecture. The first one was getting too long and complicated. I decided  to split into multiple post.  Thread models, transactions, component communications, adapter organization, scaling, testing, refactoring, deployment are the remaining topics.

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
[^12]: Anti-corruption Layer (ACL) https://deviq.com/domain-driven-design/anti-corruption-layer
[^13]: CQRS https://martinfowler.com/bliki/CQRS.html
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTQwMzM5NiwxNTgwMTYwMzg5LDE2MT
U5MzAwOCwtMTgxNzEwNTk5MywtMTgwODc1NzM1MSwtMTg3OTMx
ODAxMywxOTE1NDYyODg2LDEwOTU2OTIwODUsMTIzOTY2NDQyOC
wtMjY5NTE0Njg0LC0xMjM2NDE3NTU1LC01NzAxMDQyLDEyNTky
NTQzNTgsMTkyMjM5NzgzMiwyMDE1ODM1NTI2LC0xODkwMjI1OT
MwLDE5ODQ5NjkxMzcsOTYwODAxNDIsLTEwMTQ0NTI3MCwxNDAz
MDUyMzgyXX0=
-->