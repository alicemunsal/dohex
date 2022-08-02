# DoHex - Data Oriented Hexagonal Architecture  

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same simple but efficient concept.

Data Oriented Design (DOD) is mainly used in video game development. We can apply some of its principles to other areas of software development such as Frontend, Backend and Embedded.
I will propose testable, scalable, modular architecture for using 
Project structure consistent 
model-code gap
It will simplify designing and developing highly maintainable , testable, scalable 

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

Our test, the **Driving Adapter** calls our application use cases. We can swap it with a CLI application or  a REST service.  Similarly we can swap the **Driven Adapter** with the MongoDB, PostgreSQL or a Web Service call. We can do that without modifying application's original source code, we only need to add new adapters. (aka Open-Closed Principle[^4])

## Data Oriented Design

Data Oriented Design (DOD) is mainly used in video game development. DOD approach is to focus on the data and to think about transformation of data.  In his famous [talk](https://www.youtube.com/watch?v=rX0ItVEVjHc)[^5] at CppCon, Mike Acton describes data oriented design principles. 

> The purpose of all programs, and all parts of those programs, is to transform data from one form to another.
> -- Mike Acton  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-DOD.png)


We are developing software systems with logical parts (or layers). Each parts may need different data models and/or transformation functions.

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Transformer.png)

Repositories, gateways, boundery objects or UI patterns like MVC, MVVM or Prensenters; all the patterns are transformation mechanisms.

## DoHex  

If we use Hexagonal Architecture and Data Oriented Design principles together with  

> There are only two hard things in Computer Science: cache invalidation and naming things. 
> --Phil Karlton

we can add lib if we need model or transformation
sample app design, folder structure graphs and model code gap  

### References
[^1]: Hexagonal architecture https://alistair.cockburn.us/hexagonal-architecture/
[^2]: Onion architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
[^3]: Clean architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[^4]: Open-Closed Principle https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[^5]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTE3MTkwNzYxLC04NTIxMzUzODgsLTc4NT
E4NDUyNCwtMTkzMTA5ODYyOCwtNTI5MTI5NDQ5LC0yMDc5MTgw
MzA3LC0yNDkzNzAzNjAsMTkxNTcxNTk3NCwtMTUzOTYwOTY4NS
wxNjYwMDcwNDkyLC03NDQ2Mzk4MjEsMTczMzU1ODQ1NCwtMTUw
MDE5Nzg1MiwtMTYwMzg0OTgyNiwxNjEwNzYwNDI3LC0yMTM5MT
c5NTY5LDEzMDExOTA1NzIsLTIxMTExNDExODgsMTUzNTMxNjUw
NCwxNjAyNDA4ODczXX0=
-->