### Pub/Sub Architecture

Consider a scenario of synchronous message passing. You have two components in your system that commnunicate with each other. The receiver asks for a service from the sender and the sender serves the request and waits for an acknowledgement from the receiver.

* There is another receiver that requests a service from the sender. The sender is blocked since it hasn't yet received any acknowledgement from the first receiver.
* The sender isn't able to serve the second receiver which can create problems.

To solve this kinda scenarios and drawbacks, the Pub-Sub model was introduced.

The Publisher/Subscriber model is a messaging pattern used in software architecture to facilitate asynchronous communication between different components or systems.

* Components of Pub/Sub Architecute
    * Publisher: Creates and sends messages to topics without knowing anything about subscribers
    * Subscriber: Receives messages from subscribed topics without knowing publishers
    * Topic: A named channel that categorizes messages.
    * Message Broker: Routes messages from publishers to subscribers based on subscriptions, ensuring delivery, persistence, and scalability.
    * Message: The data unit exchanged, which can be text, JSON, or binary.
    * Subscription: Links subscribers to topics, defining which messages are received and delivery guarantees (e.g, at-most-once, at-least-once).

> Twitter, Instagram are a real-life example of Pub/Sub architecture.

* Use-cases of Pub/Sub
    * Real-time data streaming: used in applications that deal with real-time data, like IoT devices and sensor networks, allowing multiple subscibers to get data streams right away.
    * Event-driven Architecute: This setup works well for systems that react to events instead of constantly checking for updates, making applications more responsive
    * Message Queues: Pub/Sub can act as a message queue, temporarily holding messages until subscribers can process them.
    * Notifications and Alerts: Lets publishers send important updates that subscribers can receive instantly
    * Microservices Communication: Helps microservices talk to each other, allowing them to communicate without being tightly connected, which improves scalability and reliability.
    * Scalable Web Applications: supports features like real-time updates and chat, so many users can join and leave, receive information at the same time without overloading the server.

* Types of Pub/Sub Services
    1. Pub/Sub Service: Main messaging service that most users and applications choose.
        * Highly reliable
        * Integrations: supports a wide range of integrations with other services.
        * Automatic Capacity Management: Handles scaling automatically based on demand.
        * Data Replication: Synchronously replicates all data to at least two zones and offers best-effort replication to a third zone for added reliability.

    2. Pub/Sub Lite Service: Messaging service designed to be more cost-effective but comes with some trade-offs
        * Lower Reliability
        * Zonal or Regional Storage: Zonal Lite topics are stored in one zone, while Regional Lite topics replicate data to a second zone asynchronously.
        * Pre-provisioning Required: need to manage and provide your own storage and throughtput capacity.
        * Cost-Effective

* Pub/Sub vs. Message Queues: MQs deliver messages to one consumer at a time (point-to-point), ensuring order and delivery. Pub/Sub broadcasts messages to multiple subscribers simultaneously, ideal for event driven systems.
* Pub/Sub vs. Steaming Platforms: Steaming platforms like Apache Kafka handle continous data streams with long-term retention and complex processing. Pub/Sub focuses on simpler, real-time message delivery.
* Pub/Sub vs. WebSockets: WebSockets enable real-time, bidirectional client-server communication (e.g. chat). Pub/Sub decouples publishers and subscribers, supporting multiple subscribers wihtout direct connections.
* Pub/Sub vs. HTTP APIs: HTTP APIs use synchronous request-response communication. Pub/Sub supports asynchronous messaging, allowing publishers to send without waiting for subscribers responses.

* Do NOT use Pub/Sub architecture when:
    1. you need very quick communication between parts of your system, Pub/Sub might not be the best option, the process of routing messages and managing subscriptions can slow things down.
    2. you need simple architecture, using Pub/Sub can make your system more complicated, especially when it comes to routing messages and handling subscriptions.
    3. you need order of delivery, Pub/Sub doesn't guarantee that messages will be delivered in the order they were sent.
    4. application is small with few components communicate directly, Pub/Sub could add unnecessary complexity that isn't needed.

* Challenges of Pub/Sub
    * Messaging Order
    * Exactly one delivery: Ensuring no duplicates despite failures is difficult and complex.
    * Latency: routing introduces delays, hard to balance with scalability and reliability.
    * Complexity: managing subscriptions, routing, and consistency needs careful planning.

> Apache Kafka, Google Cloud Pub/Sub, Amazon SNS/SQS are examples of Pub/Sub messaging, and JMS, RabbitMQ, AMQP are examples of point-to-point messaging.