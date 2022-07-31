### Component Communication

#### Direct Communication  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Direct.png)

Components can only talk to each other through their ports. Nothing wrong with this design if you are developing simple application. But we coupled our components to each other. 

#### Event Bus 

The Electronic industry designed different standards to allow micro-controllers and devices to communicate each other: I2C, Modbus, CAN Bus, etc.  

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/modbus.jpg)

These standards are similar to our good old friend **Pub-Sub Design Pattern**. Our components can talk to each other through event bus. Components do not share (independently access) the same memory or storage: **Shared-nothing architecture**[^9].

![Event bus](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Event%20Bus.png)

This is the most preferable communication in general. It allows loosely coupled and asynchronous communication. 
This is classified as the **Event-Driven Architecture**[^10]. it needs different thinking and has its own disadvantages.  

Event-Driven Architecture has 4 common patterns according to Martin Fowler:  What do you mean by “Event-Driven”?[^11]

1. Event Notification
2. Event-Carried State Transfer
3. Event Sourcing
4. CQRS 

When we need out-process robust communication for our components, **Event Sourcing** can be used. We can directly connect necessary components to event streaming platform through its adapters, or we can connect our event bus to event streaming platform.

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Deployment.png)   

#### Shared Data

Our components can be logically connected through shared data such as PostgreSQL or MongoDB.

![Shared Data](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Shared%20Data.png)

#### Service Interface

We can connect our components synchronously through service call.

![Service Communication](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Service.png)

#### Hybrid  

Direct communication, shared data and service interface communication less preferable. But we are not living in a perfect world and we can pragmatically use mix of them. Also you can change your decision later with a reasonable effort.   

![enter image description here](https://raw.githubusercontent.com/alicemunsal/dohex/master/diagrams/1-Hybrid.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1OTkyMDA3NF19
-->