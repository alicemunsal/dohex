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
[1] Hexagonal Architecture https://alistair.cockburn.us/hexagonal-architecture/  
[2] Onion Architecture https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/  
[3] Clean Architecture https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html  
[] Enterprise Integration Patterns https://camel.apache.org/components/3.18.x/eips/enterprise-integration-patterns.html  

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYzMjg1MTg3MiwtNzc3NzIzNzUxLC0xMT
I4NjA3MTUzLDQxMDAzMDYwOSwtMTM1NjMxNzI0NywtNzg2Mjgy
NzksMTY5MDY1MDU0OCwtMzUyODgyODM3LC0xNjU3MjA1NTUsLT
Y3MjIyMjcwNCwzNjI5MDQ2OTYsNDgyMzIwMTQ2LC05MjQ3MzM0
NjAsOTU3MjQzMzEzLDUxMDgwODM0LC00NDI3MzQ0NzYsLTEwMT
U2OTk0OTUsODQ5MjA3NDE5LC0xNDI0NjEyODk4LDIxMTA3MTc4
MzRdfQ==
-->