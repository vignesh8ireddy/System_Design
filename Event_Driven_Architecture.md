EDA is a software design paradigm where system components communicate by producing and responding to events. These events can be important happenings, like user actions or changes in the system's state.

* This approach enables real-time responsiveness, scalability, and modularity.
* Components are independent, meaning they can function without being tightly linked to one another
* This structure enhances flexibility, scalability, and real-time responsiveness in systems.

> At a big party where everyone is doing their own thing. Instead of constantly checking on each other, they use a bell to signal important things, like "cake's ready" or "dance party starting." That bell is like an event in event-driven architecture. 

1. Representation: Events are expressed as messages or signals that communicate specific information.
2. Triggering: Various sources, such as user actions or data changes, can trigger events.
3. Asynchronicity: EDA often uses asynchronous communication, allowing components to work independently and in parallel.
4. Publish-Subscribe Model: A pub/sub model is used to manage events, with individuals who produce them publishing them and interested parties subscribing to them.
5. Event Types: By pupose, events are grouped together, such as "UserLoggedIn" or "OrderPlaced."
6. Payload: Events often include extra information, or payload, that provides context (e.g. a "PaymentReceived" event might detail the payment amount.)
7. Event Handling: Components have specific handlers that dictate their response to events.
8. Real-time Processing: Events allow immediate reactions to changes, making EDA ideal for scenarios requiring quick responsiveness.

* Components of EDA
    1. Event Source: initiates flow of information that drives the entire architecture, can be user interfaces, sensors, databases, and external systems.
    2. Event: emitted by sources and can encapsulate various types of information, serving as the primary means through which different components communicate.
    3. Event Broker/Event Bus: A central hub, facilitates communication between various components by handling event distribution, filtering, and routing. It ensures events reach the right subscribers, promoting efficient interaction within the system.
    4. Publisher: Generates events when specific conditions or actions occur
    5. Subscriber: shows interest in particular event types and subscribes to them.
    6. Event Handler: A piece of code linked to a subscriber that defines how to process received events.
    7. Dispatcher: sometimes, a dispatcher is used to route events to the appropriate event handlers for processing.
    8. Aggregator: Several related events are combined by an aggregator to create a single, more significant event, reducing complexity by simplifying the management of numerous individual events, making it easier for subscribers to process relevant information.
    9. Listener: A component that actively monitors the event bus for events and reacts to them. Often they are tailored to specific event types, ensuring that they respond promptly to changes that are relevant to their function.

* Usecases
    1. Real-time processing: if application needs to react instantly to the changes.
    2. Scalability: when system is expected to grow and handle an increasing number of events.
    3. Decoupling/Modularity: promote a modular design
    4. Complex Event Processing: handling multiple events and derive insights from them
    5. Integration of Diverse Systems: various systems or services that need to communicate, enabling flexible communication between different technologies.

    Examples:
    * IoT applications: for processing sensor data, monitor remotely, react quickly to shifting changes.
    * Financial Services: for real-time processing of transactions, fraud detection, and market data updates. Events like, trade executions, payment authorizations, and market fluctuations can trigger immediate responses.
    * E-commerce: for order placing, inventory changes, and payment processing.
    * Telecommunications: for managing dynamic network circumstances and load adaption.
    * Online Gaming: handling interactions between players, in-game events, and updating game state.


* Challenges of EDA
    1. Increased Complexity: As more events and components are added, it can be tough to manage how events flow and to keep everything coordinated.
    2. Event Order and Consistency: Keeping events in the right order and making sure the system remains consistent can be tricky, especially when handling events that come in out of sequence or ensuring that actions are completed as a group.
    3. Debugging and Tracing: Finding and fixing issues in a distributed and asyncronous setup can be harder than in traditional systems.
    4. Event Latency: Because events are processed individually, there can be delays between when an event occurs and when it gets responded to.

* Event Driven Architecture vs. Message Driven Architecture
    1. Definition
        * EDA focuses on events that represent significant state changes.
        * MDA centers around exchange of messages between components, often using a message broker
    2. Communication
        * EDA uses events
        * MDA uses messages which may have a broader scope than events.
    3. Triggering Mechanism
        * Events are often triggered by changes in the system's state
        * Messages are sent and received based on the needs of the communicating components.
    4. Handling
        * Event Handlers
        * Message Handlers/Listeners
    5. Examples
        * Order placement, sensor data updates triggering actions
        * Message Queues, Pub/Sub systems, request-response patterns