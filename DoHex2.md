# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD)[^4] is gaining traction mainly in video game development. Some of its fundamental principles can be applicable to other areas of software development such as Frontend, Backend and Embedded. 

By bringing these two paradigms together, we can create testable, scalable, modular architecture to handle complexity and consistent project structure to reduce the model-code gap[^5] .

## Hexagonal Architecture 

### Philosophy  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control).   

![App and oursite world](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)
 

Our application does not know anything about IO devices and should not depend on them. But an IO device must implement an adapter for connecting to our application through its ports. 

### Implementation   

> Hexagonal Architecture, allows an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
> -- Alistair Cockburn  

![Application](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hex.png)

This is our application written in TypeScript and driven by a test. It uses in memory repository to save users.  

![code](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Code.png)

"addUser" is the only **Use Case** of our application. The use case has a **Business Logic** that checks whether name is empty and save this user to the repository.   

We can build our entire use cases with all business logic inside, using only unit tests. We don't need databases or external interfaces or UI. We can then add the infrastructure elements and other things necessary to make it a functional application.  

Our test, the **Driving Adapter** calls our application use cases. We can swap it with a CLI application or  a REST service.  Similarly we can swap the **Driven Adapter** with the MongoDB, PostgreSQL or a Web Service call. We can do that without modifying application's original source code, we only need to add new adapters. (aka Open-Closed Principle[^6])

## Data Oriented Design

>  The purpose of all programs, and all parts of those programs, is to transform data from one form to another.  
>  -- Mike Acton  

In his famous [talk](https://www.youtube.com/watch?v=rX0ItVEVjHc)[^7] at CppCon, Mike Acton describes data oriented design principles. Data Oriented Design (DOD) approach is to focus on the data and to think about transformation of data.  
  
### Transformation

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-DOD.png)


We are developing software systems with logical stages (or layers). Each stage may need different data models and/or transformation functions.     

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

Today, Software developers try to create abstract model of the problem domain by focusing on classes and their relationships as taught in school. Hence, they tend to neglect to understand the properties of data. 

Data-oriented design forces you to think about your data first and foremost: what it is, what is its shape and size, how it is processed and how it flows between the different stages of your program. 

DOD's standpoint is to separate data from behavior. Thus we can achieve; simplified thinking, better performance, better testability. 

> Programmer's job is not the write code; Programmer's job is to solve (data transformation) problems.  

## DoHex  

 DoHex is yet another Hexagonal Architecture that **Component based**[^8], **Event Driven**[^9] and Data Oriented. 

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Architecture.png)

Each component is developed separately; is encapsulated in its own package and has its own ports, adapters and all the implementation details inside. Component functionalities can only be used through its own ports. We can think components like in memory **Microservices**.  

Component part definitions:
* **lib**: Libraries are used when different data model and/or transformation functions are necessary at that part. Each layer gets data from outside layer and transform that data to inner layer data models. We don't need a library, if implicit transformation provided by the external frameworks or data is passed directly to the inner layers without need for transformation or data model is   
* **app:** This is the application logic part of the component. It's about automation. This part contains usecases and if necessary request and response models for the usecases in its lib. If business logic is trivial, we can include in this part.
* **core**: Business logic part of the component. 

Each component can have a different complexity, we can omit unnecessary parts.

Key points of the DoHex:
* 

CQRS is natural
freedom 
High level project structure is the way to connect your software architecture to your source code.


Reflecting this selections and drawings into code is considered as the part of the design process

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

> There are only two hard things in Computer Science: cache invalidation and naming things. 
> --Phil Karlton

we can add lib if we need model or transformation
sample app design, folder structure graphs and model code gap  

Software Architecture is the blueprint of the software system. It is about making fundamental choices that are hard to change. Selecting languages, paradigms, tools, frameworks, methodologies and drawing large number of boxes and lines at the board are the parts of the architectural process.  

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
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjE1ODkyMDYzLDE3NDM2ODA2ODAsMTY0MD
M5NzA2Niw3MTE4Mjg3MzYsMTkzMTI1MDE3NiwtNDY1NTE0Njg2
LC0yMDQyODg5MjE0LC02NjkyMTE0MDgsNDc1NzI0ODgsNTc3Nj
g4OCwtMTA5NDMxODU4NCwtMTA5NDMxODU4NCwtMTQ3ODY1NzM2
OSwxNDU1OTMyODE3LC03NDUzNDgxNjYsLTE2NTAyNjYxMzMsLT
E2NTAyNjYxMzMsMTYzNTE5OTI3LDEwNzkyNjc3NSwtMTIxOTc4
NzA2XX0=
-->