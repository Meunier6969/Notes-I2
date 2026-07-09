# Software Design and Modeling
**Teacher** : Ilyes JENHANI (?)
**Moodle Link** : https://moodle.myefrei.fr/course/view.php?id=20412

# Design Principles
## SOLID
- S: **Single Responsibility Principle**

Every class has one, and only one, reason to change. 

- O: **Open/Closed Principle**

The system is open for extension and closed for modification.

- L: **Liskov Substitution Principle**

Any implementation can substitute its abstraction without breaking the consuming code.

- I: **Interface Segregation Principle**

Interfaces are kept narrow and role-specific.

- D: **Dependency Inversion Principle**

High-level services depend on abstractions injected at construction time.

## GRASP
- **Creator**

Object creation is assigned to the class that aggregates or closely uses the object being created.

- **Controller**

The system uses dedicated use-case controllers rather than a single monolithic façade.

- **Low Coupling**

All services communicate through interfaces, never through concrete classes.

- **High Cohesion**

Each class has a single, well-defined set of responsibilities.

- **Information expert**

Responsibilities are assigned to the class that holds the information needed to fulfil them.

## Design patterns
- **Strategy Pattern**

The Strategy pattern is applied in two distinct areas of the system: payment processing and pricing computation. Rather than encoding conditional branches directly inside a processor class, each variant of behaviour is extracted into its own class behind a stable interface, making the family of algorithms fully interchangeable at runtime.

- **Observer Pattern**

The Observer pattern governs how appointment lifecycle changes propagate into notifications. The Appointment class acts as the subject: it maintains a list of registered AppointmentObserver instances and calls notifyObservers whenever a significant state transition occurs. NotificationDispatcher is the primary concrete observer; AppointmentAuditLogger is provided as an extensibility example for audit trails.

- **Factory Pattern**

The Factory pattern centralises the construction of Notification objects inside NotificationFactory, shielding the rest of the system from the details of how notifications are assembled.

- **Singleton Pattern**

The Singleton pattern is applied to SystemConfigurationManager, which holds the system-wide settings that must remain consistent across the entire application lifecycle: default appointment duration, notification retry policy, supported payment methods, and
feature flags. Allowing more than one instance of this class would risk inconsistent configuration state across different parts of the application.

- **State Method Pattern**

The State pattern manages the appointment lifecycle, encoding valid and invalid transitions directly into each state class rather than into a tangle of conditionals inside Appointment. An appointment can occupy one of four states, ScheduledState, ConfirmedState, CompletedState, and CancelledState , each implementing the AppointmentState interface, which exposes confirm, cancel, complete, and getStateName.

## UML Diagrams
- **Use Case**

Describes what the system does from the point of view of the users, without going into the implementation. Used to describe functional needs.

- **Class Diagram**

Describe the structure of the system (each classe, interface, attributes, ...)

- **Sequence Diagram**

Describes the behavior of the system, and the messages that are transmitted between actors/objects to achieve certain tasks.

