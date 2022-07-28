## DoHex - Data Oriented Hexagonal Architecture 

### Intro

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [1], Onion Architecture [2], Clean Architecture[3] all circle around the same concept.  
 
I will present ...simplified thinking... practical variations of this concept
Consistent and simple design and development strategy for 
 
### Hexagonal Architecture
![Hex1](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1.drawio.png)
*App and outside world (IO Devices)*

#### Dichotomy of Control

> *The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.*  
> — Epictetus. Discourses. II.5  

This concept within Stoic philosophy is referred to as the Dichotomy of Control (“DOC”), the understanding of what is and what is not within our control, and it is one of the most important tenets of the philosophy. 

### Component Diagram 

What is a component anyway. 
Famous blue book, Bounded Context

### Component Communication

### Adapter Organization

### Web Applications

Nowadays we are developing web interfaces mostly as a Single Page Applications(SPA) using React, Vue, Svelte,... This is a different application connected to the our backend services or maybe we are using GraphQL as a backend. Nonetheless we have a separate application running in the browser. We can use the same architecture in javascript and we can connect our UI components 

### Project Structure
There is no such thing as complex project in this perspective. S

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
[1] Hexagonal Architecture https://alistair.cockburn.us/hexagonal-architecture/  
[2] Onion Architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/  
[3] Clean Architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html  
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMjcyMDg2OSw0MTAwMzA2MDksLTEzNT
YzMTcyNDcsLTc4NjI4Mjc5LDE2OTA2NTA1NDgsLTM1Mjg4Mjgz
NywtMTY1NzIwNTU1LC02NzIyMjI3MDQsMzYyOTA0Njk2LDQ4Mj
MyMDE0NiwtOTI0NzMzNDYwLDk1NzI0MzMxMyw1MTA4MDgzNCwt
NDQyNzM0NDc2LC0xMDE1Njk5NDk1LDg0OTIwNzQxOSwtMTQyND
YxMjg5OCwyMTEwNzE3ODM0LDY2Njc0Mzk0OCwzMzcxMzk0NzVd
fQ==
-->