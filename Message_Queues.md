### Message Queues

* Enable Asynchronous communication between system components, acting as buffer that decouple producers from consumers.
* Allows systems to operate even when components are delayed or unavailable

* A typical message structure consists of two main parts:
    1. Headers: contains metadata such as unique identifier, timestamp, message type and routing information.
    2. Body: contains the actual message payload in any format, including text, binary data, or structured data like JSON, XML

* Key Components of a Message Queue System
    1. Message Producer
    2. Message Queue
    3. Message Consumer
    4. Message Broker (Optional): provides additional functionality like message routing, filtering, and message transformation.

* Working
    1. Sending Messages: producer creates and sends messages to the message queue.
    2. Queuing Messages: message queue stores the message temporarily, making available for one or more consumers, typically in FIFO order.
    3. Consuming Messages: when consumers are ready, they retrieve messages from queue, and process them at their own pace, enabling asynchronous communication
    4. Acknowledgement (Optional): In some cases, consumers send acknowledgements back to the queue, indicating that they have successfully processed a message.

* Need of Message Queue
    1. Asynchronous Communication
    2. Decoupling
    3. Workflow Management

* Types of Message Queues
    1. Point-to-Point Message Queues
        * Once consumer retrieves the message, it is removed from the queue.
        * Request-Response implementation
        * Work Queue: queue is used to store to all the work/tasks to be completed by the consumer
        * Guaranteed Delivery: Consumers can be configured retry retrieving messages until they are successfully processed.
    2. Publish-Subscribe Message Queues
        * When a producer publishes a message to publish/subscribe queue, the message is routed to all consumers that are subscribed to the queue.
        * Consumers can subscribe to multiple queues, and also unsubscribe.
        * More complex than point-to-point queue
        * Used to implement real-time streaming applications, social media, stock market tickets, etc.
        * Used to implement event-driven architecture, where components of a system communicate with each other by publishing and subscribing to events.

* Message Routing
    1. Topic-Based Routing: Messages are sent to topics/channels, and subscribers express interest in specific topics.
    2. Direct Routing: Messages are sent directly to specific queues or consumers based their addresses or routing keys.
    3. Content-Based Routing: Filters or rules are defined to route messages that meet specific criteria based on the content of the message.

* Scalability of Message Queues
    1. Distributed Queues: Implement the message queue as a distributed system with multiple nodes, enabling horizontal scaling.
    2. Partitioning: Split queues into partitions to distribute message processing across different nodes or clusters
    3. Use load balancers to evenly distribute incoming messages to queue consumers.

* Dead letter queues and message prioritization in Message Queues

    1. Dead Letter Queues: Mechanism for handling messages that cannot be processed successfully, by providing way to investigate and potentially reprocess them while preventing them from blocking the system.
        * Messages with errors in their content or format
        * Messages with exceeded TTL or delivery attempts
        * Messages that cannot be delivered to any consumer
    
    2. Message Prioritization: for controlling their processing order.
        * Handles urgency, message content order, business rules, etc

> RabbitMQ, Apache Kafka are popular message queues for distributed systems.