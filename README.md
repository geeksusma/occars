# Vehicle Bookings for OC's Cars

Our Company is a small one which is becoming so popular after publishing some adverts on TV. The business is runned up by and old retired race car driver called Ortega Cano,
 who needs a solution now the booking requests are growing.

The business has a small flote of vehicles, some big bikes, small vans (they can be adapted for camping) and cars (they can be small, medium or big)
 The cost per day it depends on the vehicle and the season (Spring and Summer are considered the most expensive seasons so the price is increased a 15% per day)

Customers can book only a vehicle at a time (because, basically, he can't drive two vehicles at same time) but they can change his vehicle along the journey.
 The price of the journey is calculated once the journey is over.

Customers must have a license-id, and they must have more than two years driving.

Obviously, a vehicle can't be booked if it is already booked for the same period of time, or it can't be booked if it is already in a journey.

We provide to our customers the vehicles with their tank full, if they don't return the vehicle in same conditions, a penalty is included as part of 
the final price (it depends on how big is the tank for the vehicle, 30$ for bikes, 80$ for vans, and 40$, 50$, 60$ for S, M and XL cars).

So, please provide to Ortega Cano a nice solution to run his job, otherwise he will back to the road again.

#DDD design
The aim of the project is to give a solution to the problem introducing both strategic and tactical patterns linked with domain 
driven design architecture.

## Strategic pattern
Consists in defining:
 - A common language between technical and business (called Ubiquitous Language) so we avoid misunderstandings when defining
actions, use cases, etc.
 - Business rules applied to solve the current problem (this is called the Domain)
 - Bounded Contexts: it's a logical limit defining an independent part of the domain. A BC has its own rules, entities, actions... 
 - Context map, to define the relationships between the different bounded contexts 

##Tactical
Tactical DDD is when you define your domain models with more precision. The tactical patterns are applied within a single bounded context. For example, in a microservices architecture, we are particularly interested in the entity and aggregate patterns.
- Entities
    - They are mutable
    - The way of checking his uniqueness is through an Id field
    - They have no logic
    - Example: A database entity
- Value Objects
    - They are in-mutable
    - The way of checking his uniqueness is through the whole object structure
    - They have logic (with no side effects)
    - They expose an "API" beyond getters
    - All those properties build a non anemic Object
    - Example: A Currency class
- Aggregates
    - Define a limit in one or more entities, but the basic rule is one entity per aggregate
    - The purpose of an aggregate is to model transactional invariants.
    - The aggregate is created, retrieved and stored as a whole.
    - The aggregate is always in a consistent state.
    - The aggregate is owned by an entity called the aggregate root, whose ID is used to identify the aggregate itself.
    - Example: Customers create orders, orders contain products, products have suppliers, and so on
    
- Repositories
    - Domain oriented interfaces to retrieve/persist data
    - Mostly they are commonly used as an abstraction layer over a database
    - In fact also a client which is retrieving info from disk or an external API, also can follow this pattern
    
- Domain services
    - They are stateless
    - They are highly cohesive (meaning they are specialized in doing one thing and one thing only)
    - They contain business logic that does not naturally fit elsewhere
    - They can interact with other domain services and to some extent with repositories
    - They can publish domain events
    - An example of Domain service would implement the logic of checking if the costumer is able to request a car / journey

- Application Services
    - Don´t have any business logic, acts as a proxy between the domain model and the "rest of the world"
    - The application service is responsible for handling transactions, ensuring system security, looking up the proper aggregates, invoking methods on them and saving the changes back to the database
    - An example of application service could be a REST controller that links to our domain logic

- Domain Events


## Resources
- https://docs.microsoft.com/en-us/azure/architecture/microservices/model/tactical-ddd#:~:text=Tactical%20DDD%20is%20when%20you,the%20entity%20and%20aggregate%20patterns.
- https://vaadin.com/learn/tutorials/ddd/tactical_domain_driven_design