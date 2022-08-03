# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD)[^4] is mainly used in video game development. Some of its fundamental principles can be applicable to other areas of software development such as Frontend, Backend and Embedded. 

By bringing these two concepts together, we can create testable, scalable, modular architecture to handle complexity and consistent project structure to reduce the model-code gap[^5] .

## Hexagonal Architecture 

### Philosophy  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control).   

![App and oursite world](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)

*App and outside world (IO Devices)*  

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

Data Oriented Design (DOD) approach is to focus on the data and to think about transformation of data.  In his famous [talk](https://www.youtube.com/watch?v=rX0ItVEVjHc)[^7] at CppCon, Mike Acton describes data oriented design principles. 

### Transformation

>  The purpose of all programs, and all parts of those programs, is to transform data from one form to another.  
>  -- Mike Acton

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-DOD.png)


We are developing software systems with logical parts (or layers). Each parts may need different data models and/or transformation functions.     

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Transformer.png)

For the perspective of the DOD; repositories, gateways or UI patterns like MVC, MVVM or MVP; all the patterns are transformation mechanisms.  

### Solving Problems

> - If you don't understand the data you don't understand the problem.  
> - Understand the problem by understanding the data.  
> - Different problems require different solutions.  
> - If you have different data, you have different problem.  
> - If you don't understand the cost of solving the problem, you don't understand the problem.
> - Solving problems you probably don't have creates more problems you definitely do.
> - There is no ideal, abstract solution to the problem.  

Software developers try to create abstract model of the problem domain by focusing on entities and their relationships as taught in school and tend to ignore data. If we want to create meaningful solutions, we need to understand problem first,   


Immutable data types
side effect free
data behavior 
DTOs, CQRS
Different langs. and Modern langs.
Threading


## DoHex  

If we use Hexagonal Architecture and Data Oriented Design principles together with  
lib incentives developers to think for data and transformation
Messaging and scheduling incentives and directing developers to think async and create loosely coupled system. 
cognitive load
least resistance path
least effort

> There are only two hard things in Computer Science: cache invalidation and naming things. 
> --Phil Karlton

we can add lib if we need model or transformation
sample app design, folder structure graphs and model code gap  

### References
[^1]: Hexagonal architecture https://alistair.cockburn.us/hexagonal-architecture/
[^2]: Onion architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
[^3]: Clean architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[^4]: Data Oriented Design https://www.dataorienteddesign.com/dodmain/
[^5]: Model-code gap https://www.georgefairbanks.com/software-architecture/model-code-gap/
[^6]: Open-Closed Principle https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[^7]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzcxMzA4MjMsLTIwNTQ0ODQ2MDEsMTYxMT
U0ODQ1MywtMjA2ODQwNzQyOSwyMTQ1OTc3NTY1LC0zMTEyNDUx
ODAsMTY0ODY0MTEyOCwxNjg2ODQzMjAsMTA4MDk0Nzc1OCwxMD
UxOTAxODYzLDEzMDc3MjY3MiwxMjE2MTYwMDA3LC0xMjQ5ODg3
NzE3LDkwNzQ4NTUyMiwtMTQwOTg3MDU2MCwxODUzMjA3MTU0LC
0xNzQyNzk5NzIzLC0xNzQyNzk5NzIzLDE1OTY3MDUyNDMsLTIw
OTU4MDMwNTJdfQ==
-->