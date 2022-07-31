# DoHex - Data Oriented Hexagonal Architecture 

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same concept.  
 
I will present ...simplified thinking... practical variations of this concept
Consistent and simple design and development strategy for 
 

## Hexagonal Architecture 

### Philosophy  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control)  

![App and oursite world](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)

*App and outside world (IO Devices)*  

### Implementation   

> Hexagonal Architecture, allows an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
> -- Alistair Cockburn  

![Application](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hex.png)

This is our application written in TypeScript and driven by a test. It uses in memory repository to save users.  

![code](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Code.png)

"addUser" is the only **Use Case** of our application. The use case has a **Business Logic** that checks whether name is empty and save this user to the repository.   

We can build our entire use cases with all business logic inside, using only unit tests. We don't need databases or external interfaces or UI. We can then add the infrastructure elements and other things necessary to make it a functional application.  

Our test, the **Driving Adapter** calls our application use cases. We can swap it with a CLI application or  a REST service.  Similarly we can swap our **Driven Adapter** with the MongoDB, PostgreSQL or a Web Service call. We can do that without modifying application's source code. This is an example for the Open-Closed Principle[^4] of the SOLID acronym; "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification". 

## Component Based Architecture

### Component  

Component is over saturated terminology in the software industry. In the context of this post: A component is a group of related functionality that resides behind a nice and clean interface.  

A component can represent a part of our domain (user, invoice, order, shipping, etc.), or be part of our infrastructure ( authentication, log, email etc.), or be an integration point to a third-party system, (payment api, crm api etc).

### Package By Component  

Software architecture is often expressed as a set of diagrams. In the design phase, we draw bunch of boxes and lines to create architectural view of our software. But in the end we structure our code based on **Layered Architecture**.  
 
![Layered Architecture](https://martinfowler.com/bliki/images/presentationDomainDataLayering/all_basic.png)
  
Therefore software architecture don’t reflect the reality of what’s happening in the code. George Fairbanks calls this concept **Model-Code Gap**[^5]. Robert Martin has addressed this issue with his **Screaming Architecture**[^6] concept. 

We can solve this problem with vertical slicing instead of horizontal slicing. This is often referred to as **Package by Component** or “Package by future" as opposed to”Package by layer“, and it’s quite well explained by Simon Brown in his blog post[^7]. Martin Fowler has also written about this and I borrowed these drawings from his post: "Presentation Domain Data Layering"[^8] 

![enter image description here](https://martinfowler.com/bliki/images/presentationDomainDataLayering/all_top.png)

Now, we aligned the architecture view of the software and the code view. It makes the code easy to understand and discuss. And end of each discussion, we can reflect back to the code.

### Hexagonal Architecture for Components  

Component can be developed separately using Hexagonal architecture. Each component is encapsulated in its own package and has its own ports, adapters and all the implementation details inside. Component functionalities can only be used through its own ports.

### Component Communication  

Components can talk to each other in various ways. They can communicate to each other directly through their ports, or they can expose service interfaces (REST, gRPC, etc), or we can use event-driven architecture, etc. This is a big topic, so I will write about it in a latter post.  

![Direct](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Event%20Bus.png)
*Component Communication through Event Bus*

## Data Oriented Programming


#### Adapter Organization

![Adapters](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Adapter%20Organization.png)

### Project Structure
How can we organize our code to reflect architecture
There is no such thing as complex project in this perspective. S
Components
Lib: 
Acl: Anti-Corruption Layer 

### Libraries  
A library is a **Side Effect** free functionality 

![Libraries](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Lib.png)

### Web Applications

Nowadays we are developing web interfaces mostly as a Single Page Applications(SPA) using React, Vue, Svelte,... This is a different application connected to the our backend services (or maybe we are using GraphQL or Firebase as a backend). Nonetheless we have a separate application running in the browser. We can use the same architecture in javascript and we can connect our UI components through adapters.




### Object Oriented Programming
![OO Programmer](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/ooprogrammer.png)
Give this a chance.
Alan Kay 


### Test Driven Development

### Deployment


### Threading
Single Thread Per Request
Non-Blocking or Asynchronous  --> Actor style, Akka, go goroutines, kotlin corutines

### Scaling

## References
[^1]: Hexagonal architecture https://alistair.cockburn.us/hexagonal-architecture/
[^2]: Onion architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
[^3]: Clean architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
[^4]: Open-Closed Principle https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[^5]: Model-code gap https://www.georgefairbanks.com/software-architecture/model-code-gap/
[^6]: Screaming Architecture http://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html
[^7]: Package by component http://www.codingthearchitecture.com/2015/03/08/package_by_component_and_architecturally_aligned_testing.html
[^8]: Presentation Domain Data Layering https://martinfowler.com/bliki/PresentationDomainDataLayering.html
[^9]: Shared-nothing architecture https://en.wikipedia.org/wiki/Shared-nothing_architecture
[^10]: Event-Driven Architecture https://en.wikipedia.org/wiki/Event-driven_architecture
[^11]: What do you mean by “Event-Driven”? https://martinfowler.com/articles/201701-event-driven.html

[^21]: Divide and conquer algorithm https://en.wikipedia.org/wiki/Divide-and-conquer_algorithm
[^22]: Enterprise Integration Patterns (EIP) https://camel.apache.org/components/3.18.x/eips/enterprise-integration-patterns.html
[^23]: C4 Model https://c4model.com/
[^24]: Anti-corruption Layer (ACL) https://deviq.com/domain-driven-design/anti-corruption-layer
[^25]: The Origin of Complexity https://itnext.io/the-origin-of-complexity-8ecb39130fc
[^26]: Package by component http://www.codingthearchitecture.com/2015/03/08/package_by_component_and_architecturally_aligned_testing.html
[^27]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc

[^28]: Entity Component System (ECS) https://en.wikipedia.org/wiki/Entity_component_system
[^29]: Share nothing architecture https://en.wikipedia.org/wiki/Shared-nothing_architecture
[^30]: Domain Driven Design (DDD) https://en.wikipedia.org/wiki/Domain-driven_design


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTQ3NTQ4NzIsLTExNTI2NzgwNzksOT
A1MjExMzk0LC0yMDk5ODgxNDAxLDc3MzAyMzQzMiw1NzQ5NTEy
MzIsMTM5NTY3NjI1OSwtNTAyOTA1MDgyLDE5MTIzMTg5MzgsNT
AyOTYzMTcsNDI5ODM3ODc1LDYzNDcyMzA1LDE4NjAzMjQwOTYs
LTEzNTMzNTYyNjIsNTY0MzIyNjQxLC05MjQ4Mjk4OCwtNjQxOD
c5MjI3LDE4MjMzNTEyMzksLTIxMjI1ODc1MzUsMTk1NzczMjUw
M119
-->