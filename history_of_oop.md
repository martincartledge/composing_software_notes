> “OOP to me means only messaging, local retention and protection and hiding of state- process, and extreme late-binding of all things.” ∼ Alan Kay

In other words, according to Alan Kay, the essential ingredients of OOP are:

- Message passing
- Encapsulation
- Dynamic binding

- Encapsulating state by isolating other objects from local state changes. The only way to affect another object’s state is to ask (not command) that object to change it by sending a message. State changes are controlled at a local, cellular level rather than exposed to shared access.
- Decoupling objects from each other — the message sender is only loosely coupled to the message receiver, through the messaging API.
- Runtime adaptability via late binding. Runtime adaptability provides many great benefits that Alan Kay considered essential to OOP.

> In programmer lingo, algebras are like abstractions made up of functions (operations) accompanied by specific laws enforced by unit tests those functions must pass (axioms/equations).

What is essential to OOP?

- Encapsulation
- Message passing
- Dynamic binding (the ability for the program to evolve/adapt at runtime)

What is non-essential?

- Classes
- Class inheritance
- Special treatment for objects/functions/data
- The `new` keyword
- Polymorphism
- Static types
- Recognizing a class as a “type”

> Functor is math jargon that essentially means “supporting the map operation”

> Types don’t matter to .map() because it doesn’t try to manipulate them directly, instead applying a function that expects and returns the correct types for the application.

> Components (Objects) can reuse behaviors from shared functions and modular imports without sharing their data
