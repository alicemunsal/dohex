## DoHex - Data Oriented Hexagonal Architecture 

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [^1], Onion Architecture [^2], Clean Architecture[^3] all circle around the same concept.  
 
I will present ...simplified thinking... practical variations of this concept
Consistent and simple design and development strategy for 
 
### Philosophy  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control)  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)

*App and outside world (IO Devices)*  

  ### Hexagonal Architecture  
> Hexagonal Architecture, allows an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
> -- Alistair Cockburn  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hex.png)

This is our application written in TypeScript and driven by a test. It uses in memory repository to save users.  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Code.png)

"addUser" is the only usecase of our application. The usecase has a business rule to check whether name is empty and save this user to the repository.   

We can build our entire usecases with all business logic inside, using only unit tests. We don't need databases or external interfaces or UI. We can then add the infrastructure elements and other things necessary to make it a functional application.  

We can swap "Driving Adapter" which is calling our application, with CLI application or REST service. Also we can swap our "Driven Adapter" which is used by our application with MongoDB, PostgreSQL or a Web Service. 

### Component 

Component is overly used terminology in the software industry. In the context of this post:  
A component is a group of related functionality that resides behind a nice and clean interface. 



### Component Communication

### Adapter Organization

### Web Applications

Nowadays we are developing web interfaces mostly as a Single Page Applications(SPA) using React, Vue, Svelte,... This is a different application connected to the our backend services (or maybe we are using GraphQL or Firebase as a backend). Nonetheless we have a separate application running in the browser. We can use the same architecture in javascript and we can connect our UI components through adapters.

### Project Structure
There is no such thing as complex project in this perspective. S
Components
Lib: 
Acl: Anti-Corruption Layer 

### Object Oriented Programming
![OO Programmer](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/ooprogrammer.png)
Give this a chance.
Alan Kay 

### Data Oriented Programming

### Test Driven Development

### Deployment


### Threading
Single Thread Per Request
Non-Blocking or Asynchronous  --> Actor style, Akka, go goroutines, kotlin corutines

### Scaling

### References
[^1]: Hexagonal Architecture https://alistair.cockburn.us/hexagonal-architecture/  
[^2]: Onion Architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/  
[^3]: Clean Architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html  
[]: Enterprise Integration Patterns https://camel.apache.org/components/3.18.x/eips/enterprise-integration-patterns.html  
[]: Screaming Architecture http://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html  
[]: C4 Model https://c4model.com/  
[]: Anti-corruption Layer https://deviq.com/domain-driven-design/anti-corruption-layer  
[]: The Origin of Complexity https://itnext.io/the-origin-of-complexity-8ecb39130fc  
[]: Package by component http://www.codingthearchitecture.com/2015/03/08/package_by_component_and_architecturally_aligned_testing.html  
[]: Data-Oriented Design and C++ https://www.youtube.com/watch?v=rX0ItVEVjHc  
[]: The Many Meanings of Event-Driven Architecture https://www.youtube.com/watch?v=STKCRSUsyP0  


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwMjI4Nzk2MSwtNjIxMzg0NTUwLDUyMz
YyNzE2NCwtMjY2MTk4OTA2LC02ODUwNDY0OTAsLTEwNTc5MDg2
ODksLTE5NTA3MDYzODEsMjEzMTQ5ODYyOSwtNTg2NzI1NzksNz
A2ODQzNjg3LDE4MDMyNjQ3NTksMTU3MDc5MTgxMSwtMTc0MDAy
MDQ4NywtMTE0MjM2NzczMiwxOTMxNDI1OTk0LDY3NTYwMTI3MS
wxNTQ2NTQzMDExLDkwNTcyMTcwOCw1OTYxNTM3NDksMTI3NjM0
NTg2XX0=
-->