## DoHex - Data Oriented Hexagonal Architecture 

### Intro

Over a decade, we are continuously reviving a particular style of software architecture with different names ,interpretations and nuances. Ports And Adapters, Hexagonal Architecture [1], Onion Architecture [2], Clean Architecture[3] all circle around the same concept.  
 
I will present ...simplified thinking... practical variations of this concept
Consistent and simple design and development strategy for 
 
### Hexagonal Architecture  

> The chief task in life is simply this: to identify and separate matters so that I can say clearly to myself which are externals not under my control, and which have to do with the choices I actually control.  
> -- Epictetus

This is one of the most important and profound concepts in Stoicism. The dichotomy of control is the Stoic idea of separating things that are within our control, and things that are outside of our control.   

Hexagonal Architecture has the same idea, we must separate our application code (within our control), and IO Devices (outside of our control)  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-App.png)
*App and outside world (IO Devices)*  
  
> Hexagonal Architecture, allows an application to equally be driven by users, programs, automated test or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.
> -- Alistair Cockburn  

Simplest code

### Component 

What is a component anyway. 
Famous blue book, Bounded Context
* ~~**Simple Function:** Email Sender, Message logger.~~  
* ~~**Group of Functionalities:** Notification service (sends Email, SMS, Mobile notifications),  CRUD interface for school assets.~~
* ~~**Bounded Context in DDD:** Support Context, Sales Context~~
* ~~**Whole Application:** Embedded software that reads data from sensors and sends to MQTT Broker.~~ 


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
[] Screaming Architecture http://blog.cleancoder.com/uncle-bob/2011/09/30/Screaming-Architecture.html  
[] Anti-corruption Layer https://deviq.com/domain-driven-design/anti-corruption-layer  
[] The Origin of Complexity https://itnext.io/the-origin-of-complexity-8ecb39130fc  

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjc1NjAxMjcxLDE1NDY1NDMwMTEsOTA1Nz
IxNzA4LDU5NjE1Mzc0OSwxMjc2MzQ1ODYsLTE2MDQ1NTc2NTks
MjA5OTQ1MTE5NiwxNjQ3MjA3Mzg0LC03MDM0MjE2MzUsMTYzMj
g1MTg3MiwtNzc3NzIzNzUxLC0xMTI4NjA3MTUzLDQxMDAzMDYw
OSwtMTM1NjMxNzI0NywtNzg2MjgyNzksMTY5MDY1MDU0OCwtMz
UyODgyODM3LC0xNjU3MjA1NTUsLTY3MjIyMjcwNCwzNjI5MDQ2
OTZdfQ==
-->