* Concurrency: Dealing with multiple tasks at once, but not necessarily executing them simultaneously. Instead, tasks make progress by sharing time on the same processing resource. It creates the illusion of parallelism.
    * Tasks start, run and complete in overlapping time periods.
    * A single processor may switch between tasks quickly (context switching), giving the illusion of simultaneous execution.
    * Common in environments where responsiveness is important (e.g., handling multiple user requests).

> Concurrency: A single cashier serving multiple customers by switching between them very quickly.

* Parallelism: Executing multiple tasks at the same time on multiple processing units. Here  tasks are divided into smaller sub-tasks that are processed seemingly simultaneously or parallel. It is used to increase the throughput and computational speed of the system by using multiple processors. 
    * Tasks are divided into subtasks that run simultaneously on separate cores or processors.
    * Mainly focuses on performance improvements via true simultaneous execution.
    * Often used for data processing, scientific computation and high-performance applications.

> Parallelism: Multiple cashiers serving multiple customers at the same time.

* Load Balancer: A networking device or software application that distributes and balances the incoming traffic among the servers to provide high availability, efficient utilization of servers, and high performance.

* Without Load Balancer:
    1. Single Point of Failure
    2. Overloaded Servers
    3. Limited Scalability

* Key characteristics of a Load Balancer
    1. Traffic Distribution
    2. High Availability
    3. Scalability
    4. Optimization: optimizes resource utilization preventing bottlenecks.
    5. Health Monitoring
    6. SSL Termination: Some load balancers can handle SSL/TLS encryption and decryption, offloading this resource-intensive task from servers.
    7. Maintaining User Sessions

* Working of a Load Balancer
    1. Receives Incoming requests
    2. Checks Server Health
    3. Distributes Traffic
    4. Handles Server Failures
    5. Optimizes Performance

* Types of Load Balancers
    1. Hardware Load Balancers
        * These are real devices that are set up within a data center to control how traffic is distributed among servers. 
        * They are highly reliable and work well since they are specialized devices, but they are costly to purchase, scale, and maintain. 
        * They're often used by large companies with consistent, high traffic volumes.
    2. Software Load Balancers
        * These are software programs that divide up traffic among servers. They operate on pre-existing infrastructure (on-premises or in the cloud), in contrast to hardware load balancers.
        * Because software load balancers make it simple to modify resources as needed, they are more scalable and less expensive.
        * They are adaptable and appropriate for a range of businesses, including ones that use the cloud.
    3. Cloud Load Balancers
        * Cloud load balancers, which are offered as a service by cloud providers like AWS, Google Cloud, and Azure, automatically distribute traffic without requiring physical hardware. 
        * Users just pay for the resources they use, and they are very scalable. They are perfect for dynamic workloads since they can readily interface with cloud-based apps and adjust to traffic spikes.
    4. Layer 4 (Transport Layer) Load Balancers
        * Uses IP addresses and port numbers (TCP/UDP) to distribute traffic while operating at the OSI model's transport layer. 
        * Because Layer 4 load balancers do not examine the data being sent, they are quicker and better suited for easier routing jobs. They effectively manage high traffic volumes with little overhead.
    5. Layer 5 (Application Layer) Load Balancers
        * These load balancers function at the OSI model's application layer, so they can route traffic according to specific application data, such as HTTP headers, URLs, cookies, or user sessions. 
        * They are able to make more complex routing choices, like sending traffic to various servers according on user preferences or the type of content. Web applications that need content-based routing frequently use them.
    6. Global Server Load Balancer (GSLB)
        * These distribute traffic across servers located in different geographical regions, improving user experience by routing requests to the closest or most responsive server.
        * They help reduce latency and provide disaster recovery by ensuring service availability across multiple data centers in case of server or region failures.

* Load Balancing Algorithms
    * Static Load Balancing Algorithms
        1. Round Robin
        2. Weighted Round Robin
        3. Source IP hash
    * Dynamic Load Balancing Algorithms
        1. Least Connection Method
        2. Least Response Time Method

* Challenges of using Load Balancers
    1. Single Point of Failure: Issues with load balancer itself could cause traffic distribution to be disrupted.
    2. Complexity and Cost: Implementation and management can be complicated
    3. Configuration Challenges: especially when dealing with complex application architectures or diverse server environments.
    4. Potential for Overhead: there may be additional overhead in the form of delay and processing time, even though modern load balancers are designed to lessen this effect.
    5. SSL Inspection Challengers: When SSL termination is performed at the load balancer, it may introduce challenges related to SSL inspection and handling end-to-end encryption.