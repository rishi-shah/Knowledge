## Domain Driven Design
### Basics

- Domain Driven design requires a deep understanding of domain. What is the domain, what are the objects in the domains,
  how does this object communicate with each other, what are the properties of each domains, what is the importance of each 
  properties. What is the function of each object in the domain. And so on.
    - For example, if we were to design and application for air traffic control. We need to sit with the experts and get all the knowledge related to the air traffic control. What are the objects in air traffic control. Objects can be as below
    1. Airplane
    1. Route/Fix Points (lat, long, altitude.)
    
    - Then we can  further go and divide the functionality and so on.

### Choosing language
- When we have gathered enough of the domain level knowledge we can further go and decide on the best language or technology suitable or particular domain.
- There are many different language that suits and solves different sets of problem. But we can divide further in to Object oriented language or Function/Procedural language. 
- If we are more in scientific domain or mathematical domain, since many theories are simply addressed using function calls and data structures because it is mostly about computations.
- But if we have a domain/problem statement dealing with real life problems and object, we can go for object oriented programming.
- Once we have decided on the Language, we can now start mapping domain to models. 
- Model are nothing but representation of each object with its properties and functionlities, along with the relationships and interaction with other objects.
- In general Object oriented programming language is more suited to model driven implimentation as the both are based on same paradigm.

### Finding patterns.
- Each domain has a problem set, that we are trying to solve by designing a program. 
- And generally each set of problem has some patterns in it, and which can be further solved by identifying those pattern and finding a simple solution to solve all the problems within that pattern range.


### Layered Architecture.
- In Object oriented programming, UI, database and other support code often gets written directly into business objects. Additional business logic is embedded in the behavior of UI and db scripts. This happens mostly as it's the quickest way of development and getting things working.
- When domain related code gets mixed with UI or DB or any other layers, it becomes extremely difficult to see and think about changes, as change in UI or DB might actually end up changing the business logic.
- Vice versa, to change business logic, we might need to meticulously trace and change UI, DB and code. This is extremely time consuming and error prone process.
- We must always break down our applications into layers. We must strive to make each layers cohesive and complete on it own.
- We must follow architectural and design patterns to maintain loose coupling between each layer.
- When this is achieved, domain model are free of any UI, DB or processing information, thus allowing them to truely evolve into rich representation of business knowledge.

### Architectural solution for domain driven design.

Common architectural solution for domain driven design is divided into 4 layers.
1. User interface/Presentation layer: responsible for presenting information to users.
1. Application Layer: This is a thin layer which coordinates the application
activity. It does not contain business logic. It does not
hold the state of the business objects, but it can hold
the state of an application task progress. 
1. Domain Layer: This layer contains information about the domain. This
is the heart of the business software. The state of
business objects is held here. Persistence of the
business objects and possibly their state is delegated to
the infrastructure layer.
1. This layer acts as a supporting library for all the other
layers. It provides communication between layers,
implements persistence for business objects, contains
supporting libraries for the user interface layer, etc. 

### Entities

There is a category of object which seems to have an identity, which remains the same thorughout the state of the software. For these objects, its not the attributes that matter, but a thread of continuity and identity, which spans the life of a system and can extend beyond it. This objects are called entities.

Consider a bank accounting system. Each account has its own number. An account can be precisly identified by the number. This number remains unchanged throughout the life of the program. This is known as entity. By implimenting entity we are creating identity.

Entites are important objects of domain model, and they should be considered from the beginning of the modelling process.

We can be tempted to make all the objects entity. But we should refrain from doing so at creating and keeping a trace on identity is a costly operaiont and can lead to further degradation. Moreover entites are unique and cannot be reused for anything else. In case if we just need to represent some attribute of a domain, like lat long of the fixed point in airplane example, we can just create an object that represents this points, It's ok if it doesn't have any identity, Such types of objects are known as Value objects and this can be composite part of an identity object such as plane. Airplane can be a unique identity object, having a specific identity making it different from the rest of te planes. But Airplane can have a list of cordinates in correct order that it can follow associated with it, it doesn't really matter if this fixed points have any identity or not.

It is also important to have object entity made immutable or static, since it doesn't have any identity and is whole in it's value alone, this can be reused by another entity, instead of creating redundancy in the system. Like Lat long combination, we can have an value object for each lat lang combination which can be static in memory and can be reused by different (flight) identity object accross system. 

### Services

When analysing a domain, we come accross some actions that are not part of behavior of any objects of the domain. They are just action accross multiple objects of domain, but not part of any. But since we are using object oriented language, which objects behavior should this action be?

For example, when transferring money between 2 accounts, whose behvaior should it be, sending account or receiving account? Whenever such behaviors are encountered in an domain, it's best to declare them as a service. Such objects do not have it's own internal state, but it provides and important function accross domain.

There are 3 major characteristics that set services aside 
1. The operation performed by the Service refers to a domain
concept which does not naturally belong to an Entity or Value
Object. 
1. The operation performed refers to other objects in the domain. 
1. The operation is stateless. 

Services are defined by interfaces, thus keeping it loosely coupled.

### Modules

For large organisations and applications models tends to grow bigger and bigger. Therefore it is crucial to organize models into a set of modules before it reaches the point complexity, where it becomes too large to understand. Modules is nothing but logical grouping of interrelated models and functionality into one.

It is widely accepted that code should have high cohesion and low coupling. It is recommended to group highly related classes into modules to provide highest possible cohesion. There are several types of cohesions, but 2 major are communicational and functional. 

- Communicational cohesion - When parts of module operate on same data.
- Functional cohesion - When parts of module come together to perform a well-defined task.

Each module should have logical grouping of classes and objects. Each module should also have a well defined interface, so that it can be used by other modules. Instead of calling 3 objects of a module, we can call one interface method of module, thus reducing coupling.

Choose Modules that tell the story of the system and contain a
cohesive set of concepts. This often yields low coupling between
modules, but if it doesn’t look for a way to change the model to
disentangle the concepts, or an overlooked concept that might be
the basis of a Module that would bring the elements together in a
meaningful way.


### Aggregates

An Aggregate is a group of associated objects which are considered as one unit with regards to data changes. The Aggregate is demarcated by a boundary which seperates the objects inside from the outside. Each aggregate has a root. The root is an entity, and it is the only object that is accessible to outside world. The root can hold reference to any of the aggregate objects and any of the aggregate objects can hold reference to other aggregate objects but outside objects can only hold reference of the root. This design ensures the data integrity, as outside objects cannot change the aggregate objects, and if they do want to change the aggregate object, they need to ask root to make the change.

### Factories

An Aggregate objects and entities in a vast domain, often become to complex and huge. When we lay the responsibility of object creation on root constructor, often things become complex and slow. This is where factories come in to picture. The only task/objective of roots constructor is that of assembly. The creation of its internal objects is task of respective factories. 

For example we have a class printer, the class constructors only objective is to assemble printer. It's like If we give plastic, metal, silica and rubber to printer class and ask it to create a printer. It's not job or printer class to create plastic body, silica and metal chips and rubber linning, It's the job or respective objects factory to create the plastic body and other parts of printer, Printer constructors only job is to assembly the objects created by factories and present and object of printer.


### Context Maps

An enterprise application has multiple models, and each model has its own Bounded Context. It is advisable to use the context as the basis for team organization. People in the same team can
communicate more easily, and they can do a better job integrating the model and the implementation. While every team works on its model, it is good for everyone to have an idea of the overall picture. A Context Map is a document which outlines the different Bounded Contexts and the relationships between them.


## Note : - This is are notes I took down while studying Domain driven design quickly http://www.carfield.com.hk/document/software+design/dddquickly.pdf