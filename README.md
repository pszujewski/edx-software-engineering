### Software Contruction

5th course in EDX micro-masters

#### What is Software Engineering?

In building large software systems, software engineers must consider the following axes of development:

- Requirements
- Design
- Build
- Validate
- Deploy
- Maintain
- Improve
- Research

#### Choice of programming language

A language's syntax defines its grammar, which is the permissible ordering of tokens by which a computer can make sense of what the programmer wants the program to execute.

One common language feature is whether the language is interpreted or compiled. Interpreted languages are read and executed from the top down. So if you declare a function, you can only invoke that function below the declaration.

In contrast compiled languages are typically analyzed and transformed by a compiler program before they are executed. The compiler generates an 'executable' from the source code. The compiler will compile the source code into machine code (or come machine code representation), bytecode, or another programming language. The compilation process also provides source code analysis on performance, etc. The compiler can check the syntax of a language to make sure it's syntatically valid. Comilers can also optimize while compiling. Ordering method declarations is also not a problem in compiled languages.

#### On JavaScript, compilation and TypeScript

Javascript is a compiled language because it uses JIT (just-in-time) compilation to compile JS source code in bytecode so it can be executed by the browser's JavaScript Engine. JIT compilation is when a program is compiled at runtime of a program rather than compiling prior to execution. JS is dynamically typed, so the developer does not need to declare each variable as a specific type. Instead dynamically-typed languages associate variable types with values rather than declared types.

TypeScript is a language that extends JavaScript with tpe annotations so the developer can have the benefists of static typing. TS compiles to JavaScript using the TypeScript compiler.

```typescript
var age: number;
age = 10;
age = 100;
// age = 'Peter' // will not compile
```

Static typeing is actually optional is TS because the developer can assign variables as being of type 'any' as well. This allows you to take advantage of both static and dynamic typing.

```typescript
var age: any;
age = 10;
age = 100;
age = "Peter"; // will compile
```

#### Concurrency and Asynchronous Programming

These are two techniques for increasing the performace of our systems that are widely used today.

Concurrant programs are able to execute multiple parts (i.e functions/methods...) of a program simultaneously on the same hardware. However, the difficulty is that all of these simultaneous procedures will be accessing the same memory (or same pool of objects) and variables at the same time. Writing concurrent programs is difficlt because all of tehse functions are accessing teh same pool of memory at the same time. As they are accessing teh same shared memory they are reading and writing from the shared variables. However the advantage of concurrency is greater performance. Moder computer architecture has been adding more 'cores' to computer processors. As more cores are added, we can run more concurrent code.

Java provides a full concurrency model using Threads. A thread is like a process within a process. Recall that "In computing, a process is an instance of a computer program that is being executed. It contains the program code and its current activity. Depending on the operating system, a process may be made up of multiple threads of execution that execute instructions concurrently" [http://learn-gevent-socketio.readthedocs.io/en/latest/general_concepts.html].

A process is an executing instance of an application, and it contains the following resources:

- an image of the executable machine code associated with the program
- memory, which includes: executable code, process-specific data (input and output), call stack that keeps track of active subroutines and/or other events, the heap which holds intermediate computation data during run time
- operating system descriptors of resources that are allocated to the process such as file descriptors (unix/linux) and handles (windows), dat sources and sinks
- security attributes (process owner and set of permissions, e.g. allowable operations)
- processor state (context) such as registers and physical memory addressing

The operating system keeps its processes separated and allocates the resources they need, so that they are less likely to interfere with each other and cause system failures (e.g. deadlock or thrasing).

"A thread is simply a path of execution within a process and in the case of python programs, our (python) process can contain multiple threads - implemented via the python threading module for example."

For more on threads and proccesses, visit the link above.

#### Concurrency and async in the real world

Concurrency is concerned with managing access to shared state from different threads.

Java implements concurrency using threads, but TypeScript and JavaScript do not. Instead these use asynchronous programming. TS and JS are single-threaded, non-blocking, asynchronous programming languages. The single-threaded aspect means only one statement at a time can be executed in a process. Blocking means that if the process encounters a slow statement, the rest of the program must wait until that statement finishes. TS and JS both provide behaviors that are Non-Blocking.

Non-blocking behavior is great in the context of network requests, for example. A round-trip network request can take as long as the equivalent of 100 million other statements executing. So while that process is waiting for that network request to complete, the rest of the system is sitting idle when it could be getting other things done.

Async behavior (particularly for network or file I/O operations) gives JS its non-blocking qualities. Even though this non-blocking behavior is single-threaded, JS provides an asynchronous function callback pattern to offload blocking operations.

There are 4 main parts to the platform that actually executes TS and JS code:

- The call stack: This is an ordered set of statements. As functions execute, they are placed on the call stack. When they return (to physical memory address), these functions are popped off the stack, passing the execution back to the caller (function below).
- Web APIs: This is the browser engine running the code or Nodejs if you are running a node process. In this space, asynchronous code is handled instead of in the call stack. So it runs in parallel with the functions on the call stack. When the asyc request is done executing, it passes the callback to the queue and invokes the callback.
- Callback Queue: This is also an ordered set of statements that contains all callbacs assigned to async functions
- The Event Loop: is in charge of checking the callback queue and if there is something on it, passing that statement (in the queue) to the call stack so it can execute.

insert js platform image

#### Processes of software development

Waterfall Process: a classic methodology developed from traditional engineering fields.

- Requirements phase: collect all the requirements for the system. This includes the specification document
- Design: documentation that lays out the architecture of the project at a higher level, for example the classes, methods and functions needed for the system.
- Implementation phase: consumes the design documentation to put the plan in place.
- Verification team will come up with a set of test plans for testing the system.
- Maintenance

The one downfall of this process is that the is no feedback loop through the process.

#### Agile Development

is all about tightening the feedback loop between developers and customers/stakeholders. Bring the cutomer into the development team.

- Favor agility over planning
- Favor buildable software over extensive documentation
- decrease the amount of time that development teams spend building the wrong thing

Extreme programming (xp) is all about having a buildable system at all times. Always favor the simplest solution.

#### Scrum Process

There is a running list of features to develop in what's known as the product backlog. For an individual 'sprint', the scrum master and development team create a sprint backlog during a planning process, and set a specific timeline by which that sprint will be completed. By the end of the sprint, you have a shippable product. The project owner then can evaluate output. The standup meeting is an important part of the process and ensures that everyone on the team is on track.

### Module 2: Specifications

Definition: Document that details what properties should the system we are going to build have? What behaviors do all stakeholders want the system to have? The engineering team must interpret this document to implement a design based on the spcifications developed in tandem with the product owner.

A key part of developing a product specification is identifying the product requirements, which include concrete functional requirements and non-functional properties/requirements of the system. So for example, "user can log out" is a functional requirement, whereas "system should be intuitive and simple" is a non-functional property. Requirements themselves have properties and expectations attached to them: they should be complete, concise, precise and consistent. We wamt them to be consistent in that we don't want requirements to contradict each other.

The cycle for specifying requirements includes: Elicitation, Analysis, Reification, Validation, and then back to Elicitation. Reification refers to making abstract concepts real or concrete. So once a tentative model is elucidated from the requirements process, it can be mocked up for further verification: we can then examine the model to see if it's viable.

Other than functional and non-functional requirements, there are also design contstraints: for example budgetary contraints or regulatory constraints. There are environmental constraints: software doesn't run in isolation, for example cloud service provider, etc. Finally we have preferences, which are an ordered list of the product owners/customers' preferred features.

#### User Stories

help capture cohesion between customer, product and dev team. User stories have 5 main parts:

- role-goal-benefit: who is going to benefit from this feature and what is it going to achieve? describe a specific role, an achievable goal, and the value that this goal might hold
- Limitations
- Definition of done: is the feature done, complete, and correct
- engineering tasks: keep track of how this feature interacts with other systems. We want our definition of done to be easily verifiable so the client knows what the expect, and the person fulfilling the user story can be validated that they've completed the task. Therefore, we want this to be as clear as possible, without ambiguities.
- effort estimate: overall cost of a feature

#### Invest - for creating user stories

Independence: User stories should be independent from each other wherever they are all consolidated.
Negotiable: If we can't negotiate a story, we can't effectively choose if we work on addressing the pains expressed in the story
Value: Provides meaningful value for the product.
Estimable: Effective costing for the development of a feature
Small: small features are easier to estimate, etc. user stories should be as small as possible
Testability: Ensure it is testable

Example of 5 main parts that build up a single user story:

1. As a prof, I want to create repositories so that my students can do their work
2. Need: Repo names, student Ids
3. Definition of done: I want to be able to run this using a single command, automated test cases
4. Engineering note: use Github manager
5. Cost estimate: 1.5 units/ days

#### Decomposing user stories - mario game example

Role: Player
Goal: Move mario
Benefit: Dodge or attack the enemy
Limitations: Just getting keyboard input
Engineering notes: Will need to use the Level class in the project
Cost: 3 units
Definition of Done: Key input controls Mario's movement, who is able to move through the current level. When Mario collides with the enemy, one of them should be hit.

This user story violates the INVEST principles. It is not independent because the notion of movement, key control and collision are all combined in this one user story. It is however, negotiable since the developer has a lot of development options for implementing the story, and it's clearly valuable because the game isn't very interesting without the ability to move Mario.

### Testing

Easy to take shortcuts on testing. But don't!

Black-box testing only gives you documentation to guide your tests. White-box testing also gives you the code written there.

White box testing - when you test the internals (the pieces that compose the system). We look at the internals to see how it's working. Based on internal implementation, we write tests

Block box testing - when you use the specification for a feature in order to write tests. You use the API signature and the specification for the feature to design test cases. You do not concern yourself with the source code or internal implementation.

A test case evaluates a single executable test in your program.

Unit tests check simple properties of a system. So unit tests focus on specific units of a software system, such as a self contained method. This is primary form of tests. It is good at isolating behavior/properties of the system. Big downfall is they don't tell you if the whole program work together. The main difficulty with unit tests is that they are not very good at simulating users.

An integration test is about tying things together. Integration tests are less isolated than a unit test because they're implementing multiple parts of the system at once. They are broader than unit tests. Smoke tests are a subset of integration tests, and just a basic running of part of the system. They are a sanity check. (tests if units work together)

System tests test the whole system.

Key goals of testing:

1. Does the code implement the specification for the feature?
2. Are there any defects in the implementation?
3. Can we understand where we expect to find the defects?
   Non-goal: Ensure that the system is bug-free.

Coverage is a software-development metric for measuring how much of a system is 'covered' by tests. It is usually represented by a percentage.

Flow independent coverage:

- block (coverage based on arbitrarily defined blocks of code)
- line (coverage baseed on lines of code)
- statement (breaking up individual statements)

Flow dependent coverage

- Branch (e.g for an if statement, are both true and false branches tested? Must test all branches)
- Path (first you define all possible paths in a function, and then test each path. one path is arbitrarily designed)

It is generally best-paractice to start with focusing on simple line-coverage, then move to statement, branch, and finally path coverage (the most complicated).

#### Equivalence class partitioning

An approach used to make a very large 'state space' more tractable that still ensures effective testing. You could also say this is input partitioning.

For example, imagine you had a function called isGreater that received two TS numbers as inputs. These numbers could be positive or negative, and could be between -50 and 50. This is a large state space because there are a lot of possible different inputs that could be received here. Implementing equivalence class partitioning here would mean effectively choosing inputs for testing this large state space. So a good idea would be to definitely test the function if it received a positive number and a negative number, for example. One such test case is representative of the state space.

In other words, "While we cannot test all possible inputs and outputs (which would create a huge state space), our goal is to choose a selection from each region to ascertain whether our system can handle many types of inputs. This narrows the scope of testing."

Boundary value analysis is about testing edge cases: When we want to increase robustness, we want to look at how our system can handle unexpected inputs or circumstances. When we do boundary value analysis, we ensure that our system can graceflly handle input values that may have ambiguous effects (such as edge cases). We want to test values that are around the boundaries mentioned in the specification, as those detail different behaviours of our function.

#### Assertionas

Popular organizational methods for test suites popularized by Java's JUnit

Four-phase test: in which a test suite has a before, beforeEach, series of tests that test behavior (assertions on execution) and then an after phase for clean-up.

Given-when-then: popularized by BDD (Behavior driven development) approaches to testing. This approach favors readability and asserts that given a certain program state, then we expect a certain outcome. "Given" should explain the context around the situation. "When" should describe what triggers the situation, with some specificity. "Then" states the consequences of "when".

It is important to note that no testing can ensure that code has no bugs. Assertions are mainly useful to check that the state or output of functions is what you expect it to be. You can find exceptions usually be simply running code - but you can't always easily check the result of a function by running it.

A note on TS testing with chai

`expect().to.equal()` uses strict equality, which means that for non-primitive values, it checks that the two parameters refer to the same place in memory. `expect().to.deep.equal()` uses deep equality, which means that it recursively checks that the two parameters' key-value pairs contain the same contents. You can also chain onto a function call with `.deep()` to ensure deep checking.

Goals in testing: 1) Reach the code we are trying to test 2) Trigger a defect 3) Propagate the result to make it -> 4) Observe the defect 5) Interpret the result and determine the defect and its root cause.

Testability is the practice of building your system and modifying your source code so that the above goals can be met in your test suite. In Test-Driven Development (TDD) this is natural because we are writing the tests first.

Testable code qualities: Controlability, Isolatability, Observability, Automatability

Controlability is about ensuring that the code in question is testable in that is short and succint and does not require a lot of lines of code to test. The key in non-controllable code in the object-oriented world is too many 'new' statements in the constructor of a given class. Controllability is also about being able to invoke code witha mock state. Can you pass in mock parameters given the source code, or is the source code written in such a way as to make that very difficult? for exmaple, does the code use external libraries within it's constructor function, such as jQuery querying the DOM, which is hard to mock.

Observability requires that the code under test produces an observable state that we can assert against. For example, if the internal state of an object is modified by the function under test, and that state is a private field, does the class under test include a 'getField' method that would allow us to observe the state of that field?

Isolatability is about the ability to observe a defect and isolate/identify that defect's root cause. Methods that are too large make isolating defects within them very difficult. Isolateability focuses on being able to test the behaviour of a specific method or function in isolation. This means that we want all other factors to be controlled or predictable

Automatability: Are the tests written in such a way that it is possible to automate them. Automatability is concerned with being able to programmatically invoke both tests suites and code so that it is easy to run a test suite. If a set of tests can be invoked with minimal human intervention, they are easier to run, and can be run more often.

### High-Level Design

A note on abstraction: Too much abstraction makes understanding and reading the system very difficult. Too little makes it unmanageable and unflexible.

- Language Constructs: Enable developers to focus on task intent instead of execution context. Examples include: methods, function, Promises.
- High-level top-down decomposition: We start with a high-level abstract description and add more and more details to it over time.
- Encapsulation: separate the data from the implementation that operates on that data.
- Diagrams: an example of a structural diagram would be a Class diagram, and an example of a behavioral diagram would be a sequence diagram. Structural diagrams highlight the structural composition of a system, and behavioral diagrams highlight the dynamic flow of a system.
- Deploymnt diagrams are structural diagrams that overlay class diagrams to provide information about where specific classes or modules exist at runtime.
- State Machine diagrams help us reason about how our application state can transition from one state to another.

#### APIs and design

Refers to Application Programming Interface(s), or interfaces for source code elements. As developer it is the interface with which you work with a module, library, or external source code. API is the prgrammatic surface of our applications.

**High-level API design principles**

- Do one thing: APIs should be focused on performing one task well.
- Never expose internal implementation details
- APIs should be as small as possible. It should be focused and only do what is most necessary
- API usability: It should be easy to read and undestand API documentation

**Low-Level API design principles**

- Avoid long parameter lists, and avoid two parameters of the same type being sequential in the list. It would be easy for the API consumer to accidentally mix up these two parameters.
- APIs should return really descriptive objects when consumed.
- Avoid exceptional returns. If an API consumer expects an API to return a User object, that API should always return an Object, even if the user is not found. For example, we don't want to return null and lead to a null pointer exception.
- Handle exceptional circumstances and user mistakes.
- Favor immutability: When we return an object to a client of an API, we don't want the client of our API to be able to alter the interal state of an object.
- Favor private code (private class, fields, etc.): unless there is a thought-out reason for making something public, keep it private.

Steps for designing an API: Start with a short spec, solicit feedback, create concrete prototypes (at least 3 different usages of the API), develop documentation with usage examples.

Properties of API usability is determined by its visibility, model, mapping, feedback (regarding, for ex, when an API is used incorrectly). Visibility can be measured by asking the question, how long does it take a developer to learn how to use an API. How visibile are the important methods? If actions are well mapped within your API, then error rates should be lower since developers will be more likely to take the actions that help them complete their desired task.

#### Remote Procedure Call (RPC)

It's often the case that we want to execute some code that isn't going to run on our local machine, so instead in a cloud-based service or maybe another machine in our local network. In other words, we want to call some remote code and get a response back. We want our local machine to request something from a remote service, and then get a response back.

REST stands for Representation State Transfer and is a software architecture for distributed hypermedia applications. This works well when the web is thought of as a collection of independent and remote services. This architecture allows for these services to not have to hold any state regarding their clients. The core design decisions are based on these pillars: simple, reliable, scalable, extensible. Statelessness is a core architectural constraint for REST services. It makes REST based services much easier to scale. We are talking about application state here, and not resource state. Resource state is obviously important here.

#### Uniform Resource Identifiers

URLs (web browser/ web pages access) are a subset of all possible URIs (URLs are in fact URIs). URIs provide a simple and transparent mechanism for naming remote resources. REST-based services all use standard access methods for parameterizing requests being made from the client to the remote service (get, post, put, delete...).

REST-based services also generate intermediate representations of their internal data in a format that is consumable by the client. So for JavaScript applications in the web, that means JSON. This in essence enforces information-hiding from the client.

The nouns in a REST-based system correspond to the reources that your system allows you to access and manipulate. We define theses using URIs. So for example: `/users/alice` corresponds to a single user Alice in our system. Other than passing data in the URI itself, the request headers also can pass parameters. Responses from REST service contains a header and a body.

Headers typically contain metadata about the request itself, such as the status code, which indicates success, failure, or other conditions. Most common formats for the response body include JSON, HTML, or XML. These formats are used instead of plain text because plain text isn't self-descriptive or useful programmatically.

#### Versioning an API

There are several ways to do this. PATH: One is to build it into the URIs explicitly. QUERY: Put it in a query string. HEADER: or you could put it the request headers.

#### Coupling

Captures how closely related or connected two program classes are. It can be problematic and is closely related to how evolvable and maintainable our codebase is. You do not usually want classes that are tightly coupled. It adds particular challenges around re-usability of classes. We do not want classes that are too closely bound. It is also easier to understand and reason about a system that is made up of independent classes.

Does the coupling arise because of similar data being stored and manipulated by different classes? Stamp coupling occurs when two classes are coupled through data structures, meaning they depend on the same data structures (publicly defined types). Global coupling occurs when global variables are used. Content coupling occurs when the internal state is modified by another unit. Content coupling represents a break down in information hiding and encapsulation.

Stamp coupling is coupling that involves reliance on data structures, as described here. In this case, since you are dealing with small, well-defined interfaces, this type of coupling is not problematic.

Coupling is however a natural part of building software and is even required to some degree for performing complex tasks. Cohesion is a key measure for evaluating how focused a unit of execution is in our system. Cohesion ultimately measures how well units of our system interact together. In the Object-oriented world

#### Cohesion

How well do the fields and methods in a class go together/ work together to perform a single task? Classes that have low cohesion are too large and are responsible for too many actions. It impedes software evolution. Cohesive classes generally have a small set of cohesive fields. This drives us to having larger number of smaller classes, which helps to isolate changes.

Cohesion is about ensuring our abstractions and program design is good. You must ask, does the class do one thing? It is important to know that coupling to a degree is unavoidable and you will have some coupling within a cohesive class. Three main types of cohesion: functional cohesion, sequential cohesion, communication cohesion, and proceduarl cohesion (when it must follow a specific order. Procedural cohesion is less desirable.

Example of sequential cohesion: the sequence of operations is important. Without being assigned a price, an item cannot be assigned a price category. Without a price category, an item cannot be added to the correct collection of items. This kind of Sequential Cohesion is not problematic in this case, because it is necessary for the system to perform the desired task.

Coincidental cohesion is not really cohesion, and is basically a lack of 'good' cohesion. In general, system design should be highly cohesive and loosely coupled.

Example of temporal cohesion, which is when code is only related by timing:

You examine a method named prepareLocationForClosure that is designed to be invoked in the case where a department store location needs to prepare to permanently close down. Within this method, there are many calls to other methods such as cancelAllRestockingOrders, activateSalePricesOnAllItems, transferAllWarehouseEmployees, etc.

The methods invoked by transferWareHouseItems are all diverse in their responsibilities. The only thing that these methods have in common is that they need to be invoked around the same time of execution, so they are an example of Temporal Cohesion. This is a problematic type of cohesion.

#### Design guidance

Goals: system should be easy to understand, amenable to new features, and easy to diagnose when there are issues. Utlimately what we want to do is adhere to a set of design principles that help us make good design decisions.

The SOLID Principles give a useful lens for reasoning about decision decisions:

- Single-responsability principle: a module should do one thing. See strategy pattern (small and independent algorithms), command pattern (abstract actions an object takes), and state pattern (abstract away how an object behaves given different states at runtime). This dirves us to have large numbers of classes, but each class is easier to understand and repair.

- The Open/Closed principle says our systems should be open to extension but closed to modification. This means that the system can get new features with modifying existing features. We don't want to accidentally modify existing classes just while adding new features or classes.

- Liskov Substitution principle: Any Object in a program should be interchangeable with any other object in the same program that has the exact same parent type. The parent being the type that is the super class to the objects in question.

- Interface Segregation principle: Clients should not be forced to rely on interfaces that they do not use. So instances of the interface should always use or need all the present methods and field for their interface.

- Dependency Inversion: classes should depend on abstractions, and NOT on implementations. This principle makes classes much more reusable. So methods should take interfaces in their parameters and always return interfaces.

### Low-Level Design

High-level design is about thinking about the intent of the design, low-level design is about thinking of the more mechanical details.

#### Design Patters

The patterns all have pros and cons to them. There are down-sides to every pattern.

- Creational: these patterns help us build objects in an extensible way.
- Structural: these help us structure our systems in ways that help us avoid future evolutionary patterns
- Behavioral: these make it so we can more easily add new behaviors to our systems at runtime.

Main pillars:

- Encapsulate What Varies: design a system in such a way that it is easily extendable. This is also about building the appropriate abstractions. This makes it easier for future developers to add new functionality. Often it can be really challenging to anticipate future needs. Avoid unnecessary abstractions however.
  Benefits:

1. Makes it easier to extend systems
2. it helps future bug fixes to be more localized

- Designing to interfaces helps to decouple our implementation from our design. The interface definitions define the system's high-level vocabulary.
  Benefits:

1. it improves the reusability of code in a system
2. Decouples implementation from design

- Favor composition over inheritance: this makes your code more dynamic at runtime, and makes it easier to add new features moving forward. This design guideline is somewhat at odds with other patterns because the others stress inheritance. Code that is inheritance-based is much more brittle than code that is composition-based. Code that is coupled based on composition benefits from seeing changes in parent-types to children percolate down. Composition drives you to have much smaller classes. This gives you a lot of flexibility.
  Benefits:

1. Makes it easier to add new features (open/closed)
2. it makes systems more dynamic at runtime

#### Singleton design pattern:

A creational pattern to use when you have a single object that needs to be used throughout the whoel system. It is often the case that you need to always pass/use a single instance of that object. In the Singleton pattern usually the Singleton object has a private label for the constructor and a getInstance method that returns the Singleton instance. This method would include a call to the constructor and then a setter to set the instance field (storing a reference to the instance of the singleton object) if the oject has not yet been instantiated. In effect however, this makes a Singleton a global variable.

#### Strategy design pattern:

Designed explicitly for varying the behavior of an application based on new requirements. We want to be able to capture future algorithms to allow future extension. It is open to extension but closed to modification. It provides a strategy interface that new concrete classes can implement to add functionality to the system. This is a way to vary behavior of our programs in a very static way.

This is a classic example of using polymorphism to hide concrete types behind abstract interfaces. So in this way we are really hiding information about the concrete implementations of theses concrete algorithms. The startegy interface declares the structure of all the algorithms we might want to encapsulate within the one strategy instance. For example, you might have a strategy factory class that manages getting the correct strategy given a context.

#### State design pattern

Gives us a way to vary the behavior of our programs in a very dynamic way. Used when you want to vary the state of your program to generate different behaviors. The way to do this is to encapsulate state in explicit state objects, and to also allow these objects to manage state transitions. This removes responsibility on clients to manage state. The states themselves are responsible for their own transitions. State decisions are localized in state classes, which makes reasoning about state transitions much more manageable.

In the object oriented world, the whole program state is associated with and composed of smaller states. Each state object implements a state interface. The state object holds a context field that is an association with the object for which the state in question has an effect.

The State pattern features a context field that allows transition back to a previous state. It also includes a setState() method that allows for these kinds of transitions between States at runtime. At run time, a concrete state invokes the setState method on the context object. That is how state transitions occur.

In this pattern, there is a Context Object with a `setState` method and a field called `state` that holds the State object that is the current state of teh system. Each given state object holds a reference (association) to the Context object so the state manages any calls to setState and transitions to different states. Therefore, each individual state class knows to which other possible state it can transition at all times. The burden of actually setting the state is maintained in each state class available. These state classes all implement a `State` object interface that includes an `action` method. Thus, the `Context` object is incharge of centralizing the current state of the system, defining the `setState()` method, and is composed of `State.` (hence the diamon in the diagram).

**Example of the State pattern**

The state pattern relies on composition. Using the mario game example, imagine we have a `Mario` object. Calling `Mario.hit()` calls `this.state.hit()` and `this.state` holds one of the possible `MarioState` objects. Each `MarioState` implements the `MarioState` interface which includes a `hit` method. The `hit` method is implemented in each state class that implements the `MarioState` object. So if the state of mario is small, large, or invincible (if he has gotten a star), then the actual `hit` implementation varies because each instance of the `MarioState` implements it. Thus the functionality is delegated to the State objects

#### State and strategy: conclusion

They are very similar. Both use inheritance to enable extension and 'openness' to extension. Both aim to isolate clients from future changes and keep the clients un-modified when adding additional functionality. Such that all you need to do is add a new state class that implements the state interface.

However their intent is entirely different, the state pattern is all about enabling state transition dynamically at runtime, whereas the strategy pattern is not as dynamic. The algorithm is set at the beginning of executing and it stays the same. The strategy pattern allows you to easily add new algorithms to your system without having to change the client classes that implement those strategies.

#### Façade design pattern

This structural pattern aims to make subsystems in a program easier for a client to use. It uses composition and encourages weak coupling between the types in its subsystems. It aims to reduce the subsystem's apparent complexity by reviewing the client's use of the system, thinking about the high-level tasks the client is trying to achieve, and then aiming to support these tasks directly within the facade interface.

For example, imagine you have client 1 and client 2. Client 1 needs to know about types A, B, and C. Client 2 needs to know about types A, B, C and E. But learning how to use all these different types in complicated. Introducing a Facade types in front of these other types wwould simplify client-subsystem interaction.

Facade uses composition to hide internal types unless they need to. It's important that the Facade not block a client from doing some task. The ultimate goal of Facade is to simplify a system. It provides a simplified view on an internal implementation. Recall that a client can still depend on parts of the sub-system that are not included in Facade by accessing them directly (in addition to having access to all components that are already included in the Facade).

Facade should implement **dependency inversion** such that it's methods take interface parameters and always return interface types in their returns. So back to the example, if A, B, and C all implement the same interface type, then the Facade methods can work with this type in its method parameters and return types. This makes it a lot easier to reuse that code in the future.

The Facade pattern does come in conflict a bit with the Single-Responsability principle.

#### Decorator design pattern

The decorator pattern allows us to add arbitrary combinations of behaviors to individual instances of objects. Rather than adding them to every instance of a class. It allows instances of objects to be wrapped with additional behavioral responsability. The decorator pattern is very good at Single-responsability.

Recall that the Decorator allows us to augment an object's responsibilities dynamically at runtime. Recall that a decorated object is oblivious to the kinds of wrappers/decorators that it has. Each decorator is dealt with one layer at a time during execution.

This is a classic example of composition over inheritance. While the pattern does use inheritance, the power of the pattern comes from inheritance. It's structure is very similar to the composit pattern. The intent of the decorator pattern is to wrap new behavors on instances of an object. Each Component has a wrap field, which allows the behaviors to be forwarded onto the encapsulated objects. DEcorators should never be aware of their context.

```javascript
// Component is an interface with an action() method

class ConcreteObject implements Component {
  action() {...}
}

class Decorator implements Component {
  constructor(WrappedComponent) {
    this.wrap = WrappedComponent;
  }
  action() {
    // do something more specific than this.wrap.action and then
    // compose on action()
    this.wrap.action();
  }
}

let c = new ConcreteObject(); // implements 'action' method
    c = new Decorator(c); // implements 'action' method and calls wrap.action(): the action() implemented in ConcreteObject
    c.action();
```

`action` might also be `render`. Imagine you have a GameFrame for Mario and then a Lava level and an Underwater level that both extend GameFrame. If you want to decorate that GameFrame with background images, like lightning flashes, and rain storms and optional mixes of the two. Lightning, Storm, and GameFrame all must implement the same Component interface with one key cascading, composed method i.e `render`. you might see:

```javascript
let gf = new GameFrame();
gf = new Lightning(new Storm(gf)); // where Lightning and Storm are decoraters
gf.render(); // calls lightning's render, which calls its wrapped render, and so forth.
```

#### Model View Controller (MVC)

Seperates the view/UI from the business logic. The model is a data-centric representation of an application's data. The Model's objects are often subjects within the observer pattern. Models force developers to step back and think about how to properly encapsulate the data in within our systems in objects.

The Views know how to render the model. If the Model is the subject in the observer pattern, the view is the observer. View retrieves state and Model notifies the view observers. One view is typically composed of many views (view are composites).

The Controller is tightly bound to the view. The controller contains all the business logic for updating the view given new state from the model. The Controller can also make useof the Strategy pattern. Updates to the Model should lead to `notify()` being called to pass on those updates to the view observers.

#### Model-View-Presenter (MVP)

Aims to decrease the tempatation to add functionality to the views. The presenter should not have any dependency on UI components. The view should not be coupled to the Model at all. It never receives any model objects. Instead the presenter sends only primitive types to the view. The presenter is responsible for updating the model and retrieving state that is then passed on to the view layer.

By not passing model objects up into the view, it ensures that the view cannot grow too large. This forces teh view to pass data to the presenter in a more simplified format. The views are the things most likely to change, so we want it to be as simple as possible. The views pass `actions` to the presenter that is then used to update the model state.

The steps in interacting with the MVP pattern from the User's perspective: 1) User initiates some event. This dispatches an action to the Presenter to modify some Model state. 2) The Presenter forwards requests to the Model to update that state and it then retrieves relevant state. 3) The Model notifies relevant Presenter methods that are observing it of any state changes 4) The Presenter receives these state changes and invokes some `update()` method and updates the View layer to reflect the new state, only passing primitive types to the view.

#### Conclusion: MVP and MVC

Both aim to decouple the View layer from the business logic of the application. One problem with MVP potentially is that the Presenter can become very very large, so it's important to properly manage the Presenter. There is also MVVVM, Model-View-View-Model. These designs are very much driven by decoupling. These models force developers to think about the data and views completely separetly.

### Construction

#### Non-Structural Properties

When we think of properties our system should have, we most often think of complexity and performance.
You could also think about security, scalability, etc. Readability is also incredibly important so others can unerstand the intent in original code.

**Properties of code that make it hard to read/understand**

1. Deep nesting via conditions, loops, etc. Instead large nested functions should be broken into many functions
2. Poor naming and poor naming conventions
3. Individual code writing style: developers on a team should all conform to a similar style of writing code.
4. No comments: comments can help with understandin what is going on but should not be abused.
5. Not broken down into digestible pieces: Should be broken into individual steps

#### Code Analysis

Static analysis: for example a compiler ingests source code and outputs any errors.
Linters give semantic warnings to help avoid common mistakes and can be used to adhere team members to style guide.

#### Automation

Automation is crucial to modern software development because of team size, complexity and pace of development. Allows for building software in a reliable, repeatable and revertible way. When we don't introduce automation where it is possible to do so, we introduce the chance of some important failure happening.

#### Code Smells and Maintenance

A mojority of software development is performed on existing systems. Software maintenance is a crucial component of a system's overall budget. There are 4 primary categories of software maintenance: Corrective (fix defects), Adaptive (help system with external changes), Perfective (add or modify functionality), Preventative (improve structure). Perfective is the most common. Preventative is the least common but can have an outsized effect on enabling other kinds of changes to be successful.

Code can easily become unstructured due to increasing complexity or poor design choices, or to a lack of preventitive maintenance. Time pressure can degrade the quality of a system. As code evolves, fixing bugs and adding features can become more difficult. Code smells are negative traits that long-lived systems often exhibit.

**Categories of code smells**

Bloaters: Size of program elements make them hard to change or work with. Examples include: long methods, large classes, methods with long parameter lists.
OO Abusers: Failure to leverage OO design.
Change preventers: Make it harder to evolve code. Shotgun surgery is when you have change across the system.
Dispensibles: Pre-mature optimization. This also includes when you have speculative generality and dead code, or duplicate code.
Couplers: Code changes that exhibit unnecessary coupling.

#### Refactoring

Designs downgrade as software evolves. Developers often find solutions that work but aren't optimal. Technical debt refers to the cost of these quick fixes. Thinking about technical debt encourages long-term planning.
Reckless and deliberate technical debt is irresponsable. Deliberate and prudent technical debt is intentional. Inadvertant and Reckless technical debt is incompetent, and prudent and inadvertant technical debt is accidental.

Refactoring is the most common way to repay technical debt. Refactoring aims to improve code design while preserving semantics. Code smells are often used as indicators for design improvements. Other improvements, such as reduced coupling, improved cohesion, increased reusability can also be achieved in refactoring.

Refactoring rule of threes: 1) code the feature, 2) code it but take note, 3) Refactor code first. Remember that pre-mature refactoring is not good. Program behavior should be unchanged after refactoring. It's also difficult to do without a good test suites.
