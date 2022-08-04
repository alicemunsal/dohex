# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD)[^4] is mainly used in video game development. Some of its fundamental principles can be applicable to other areas of software development such as Frontend, Backend and Embedded. 

By bringing these two paradigms together, we can create testable, scalable, modular architecture to handle complexity and consistent project structure to reduce the model-code gap[^5] .

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

> Programmer's job is not the write code; Programmer's job is to solve (data transformation) problems  

## DoHex  
we can start with mon
programming is organizing thinking with diagrams, bunch of boxes and lines.
If we use Hexagonal Architecture and Data Oriented Design principles together with  
encourage programmers 
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

### References
[^1]: Hexagonal architecture https://alistair.cockburn.us/hexagonal-architecture/
[^2]: Onion architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
[^3]: Clean architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[^4]: Data Oriented Design https://www.dataorienteddesign.com/dodmain/
[^5]: Model-code gap https://www.georgefairbanks.com/software-architecture/model-code-gap/
[^6]: Open-Closed Principle https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[^7]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc
[^8]: Out of the Tar Pit http://curtclifton.net/papers/MoseleyMarks06a.pdf
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MzQ4NjA1OSwtMjQ4MzE3NDU5LC0xNT
M5MjQ0MjI3LDE3MzU3NDgyNzIsLTExMzA5NDQxODIsLTE4MTMz
NDMzNzQsLTE4NjczNzc1MjksNDMwNjAyMDI5LDcwNzE3OTE1MC
wtMTEzNDI5NDAxMiw1ODg4MDA0NTYsLTExNjc2MDU0ODUsLTQ1
NDU1NjY4NSwtODQzNzc5MjMwLDE0MzEyMTU4NjgsLTExNjQxMj
Y2MzYsLTkwODIxNTEwLC05MDAwNDE3NTEsMTY5MTg3NzQ4Niw5
MzAyMDY0NDhdfQ==
-->