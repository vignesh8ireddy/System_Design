# System Design

> Designing the architecture, components, and interfaces for a system so that it meets the end-user requirements.

* Robust, Scalable, efficient applications
* architect solutions to handle real world complexities
* scalable: grow and handle increased demand without failure, shrink increasing resource utilization and efficiency
* Efficient resource management
* Adaptability: systems evolve with changing business needs and reduce long term costs
* micro services X monolithic

* System Design in SDLC, analyze -> plan -> DESIGN -> implement -> develop -> release
* LLD: class & module design, logics, data structures, maintainability (for developers and engineers); OOPS & Design Patterns
* HLD: Architecture of entire system, system components and interactions, scalability, performance, reliability (for architects & stakeholders like managers)
* Redis cache, memcached, CDNs, apis
* Functional Requirements: what system must do like user registration, streaming, texting messages, media...
* Non Functional Requirements: scalability, latency, availability, security, etc
* Networking and Security fundamentals like DNS, protocols(TCP/UDP, HTTP, WebSockets), OAuth, JWT, TLS/SSL, rate-limiting, API security and basic DDOS protection
* Message Queues and steaming tools like Kafka and RabbitMQ
* Fault tolerance, fallback strategies, redundancy, Load Balancer types & algorithms.
* Observability tools like Prometheus, Grafana, ELK Stack(Elasticsearch, Logstash, Kibana), Alerting systems like PagerDuty
* Design Trade-offs: performance considerations, scalability, security, cost,...


### Software Testing

* Manual X Automation Testing

1. White Box X Black Box X Grey Box
2. Functional Testing, Non-Functional Testing
3. Unit Testing, Integration Testing, System Testing
4. Performance Testing (Load testing, Stress testing, scalability testing, stability testing, spike testing)

### Characteristics of System Design
* Features of the System
* Define APIs
* Availability
* Latency & Performance
* Scalability
* Durability
* Class Diagrams
* Security and Privacy
* Cost Efficiency

### Building Blocks
* Client-Server Architecture
* IP Address, Domain Names, DNS server & Lookup
* IPV4 X IPV6
* Proxy Server / Reverse Proxy Server
* Latency, Caching, CDN, Edge
* HTTP(S), HTTP2, SSL, TLS
* Public Key Infrastructure & Certificate Authority
* TCP X UDP (for video streaming)
* API (REST X GraphQL)
* Database Servers (SQL - ACID X NoSQL - BASE)
* Scaling (Vertical X Horizontal)
* Load Balancers (L4, L7)
* Distributed Systems, CAP theorem
* Database Servers and Scaling
* Database Indexing
* Replication
* Sharding, Vertical Partitioning
* Normalization, DeNormalization
* BLOB Storage
* Content Delivery Network
* Web Sockets
* Webhooks
* Microservices, Message Queues
* API Gateway, Rate Limiting
* Idempotency Technique
* Optimistic locking X Pessimistic locking of transactions
* Strong Consistency X Eventual Consistency
* CPU/RAM/Storage/Network Bandwidth
* Bloom Filters & Count-Min sketch
* Paxos - Consensus over distributed hosts
* Design Patterns & Object Oriented Design
* Virtual Machines & Containers
* PUB-SUB over Queue
* Map-Reduce
* Multi-threading, Concurrency, locks, synchronization, CAS

### Tools

* Database
  * Apache Cassandra
  * MongoDB / CouchBase
  * MySQL
* Distributed Cache
  * Memcached
  * Redis

* Zookeeper
* 
* 
* Apache Kafka
* 
* NGINX
* HAProxy
* 
* Solr, ElasticSearch
* BLOB store Amazon S3
* Docker
  * Kubernetes
  * Mesos
* Hadoop/Spark
  * HDFS



Non Functional Requirements:
Scalability 
Performance 
Reliability 
Security 
Maintainability 
Interoperability 
Usability 
Availability
Cost effectiveness 



### System Architectural Styles

* Monilithic Architecture
  * Under this architecture, the UI, business logic, and data access layers are all created, put into use, and maintained as one unified unit (a single codebase).
  * Preferred for its simplicity and ease of initial setup, cost-effectiveness(economical for startups or small projects), Security (reduced attack surface), legacy support (many systems still rely on monolithic architectures).
  * Highly rigid, so it is difficult to scale, maintain,and adjust to changing needs.
  ```
    Characteristics:
    1. Single Codebase
    2. Tight Coupling
    3. Shared Memory
    4. Centralized Database
    5. Layered Structure: separate layers for data access, business logic and presentation (like mvc, model, view and controller)
    6. Limited Scalability: achievable with ineffiencies and high resource usage (because entire application must be scaled instead of a particular component or service).

    Key Components of Monolithic Architecture:
    1. User Interface (UI)
    2. Application Logic
    3. Data Access Layer
    4. Database
    5. External Dependencies: third party APIs, authentication providers, or messaging queues, external systems or services.
    6. Middleware: components that manage cross-cutting issues like logging, security or performace monitoring et cetera.

    Design Principles of Monolithic Systems
    1. Modularity: It is essential to structure the code in modules
    2. Separation of Concerns: According to the separation of concerns principles, several application components should be responsible for separate tasks.
    3. Scalability: Scalable design is when system supports horizontal scaling whenever necessary. This might involve asynchronous processing for resource intensive operations, employing caching methods, optimizing performance critical components.
    4. Encapsulation: Revealing only the interfaces required for communication while hiding the core operations of a component. Used for reducing dependencies and make code maintainence and evolution easier.
    5. Consistency: Consistent coding styles, architectural patterns, and design principles across the entire codebase for clarity and predictability.

    Deploying Challenges:
    1. Long Deployment Cycles: complete codebase is deployed as a sigle unit. Every component must be packed, tested and deployed every time.
    2. Risk of Downtime: instead of a service, entire system has to be re-deployed which leads to downtime.
    3. Limited Scalability: replicating the complete application stack can result in inefficiencies and higher infrastructure expenses.
    4. Resource Consumption: More memory and CPU compared to lightweight architectures like microservices.
    5. Limited flexibility: Difficult to make modifications

    Scaling Monolithic Systems:
    1. Vertical Scaling (also called, Scale-up): increasing virtual machine resources such as CPU, memory or storage. Provides immediate relief but has limitations beyond which it is prohibitively expensive or potentially impractical.

    2. Performance Optimization: Optimizing operational bottlenecks in sigle-function operations by finding areas of inefficiency, database query optimization, improving algorithmic complexity, reducing resource usage, etc
    
    3. Caching: for reducing the load on external services. But storage methods must be carefully configured to ensure accuracy and up-to-date information

    4. Load Balancing: for distributing traffic across multiple instances of a monolithic application.

    5. Database sharding: Each shard stores a small portion of the data, allowing for horizontal scaling of the database. However, database sharding add complexity to the application and requires careful planning and maintainence.

    Strategies for migrating from Monolithic Architecture to Microservices Architecture

    1. Strangle Fig Pattern
    2. Decomposition by Business Capability
    3. Database Decoupling
    4. Event-Driven Architecture
  ```
* Microservices Architecture


### Scalability

* Horizontal scaling (add more instances) and vertical scaling (increase size of instance like, RAM, CPU, etc.) are two different aproached to improve the performance and capacity of the system.
* Scaling ensures high availability and reliability, maintains performance and response time, supports growing data and storage needs.

```
1. Vertical Scaling (Scaling-in)
> Upgrading the same system rather than increasing number of systems.
> Simple to implement and useful for monolithic and small scale applications.
> No changes to application code, less complex network, less complicated maintenance.
Examples:
i. Upgrading a MySQL server from 16GB RAM to 64GB to handle more queries.
ii. Moving a webiste hosted on a 2-core VM to an 8-core, higher-RAM VM to improve performance.
Disadvantages:
i. Limited scalability: Unlike horizontal scaling, vertical scaling is constrained by the hardware's physical limitations.
ii. One server still receives all the incoming requests thus increasing the possibility of downtime in the event of server failure.
iii. requires restarting or replacing the machine => Downtime!
iv. expensive comparatively because updrading the hardware 
```

```
2. Horizontal Scaling (Scaling-out)
> Adding more machines or servers to distribute the workload across a larger number of individual units.
> No downtime while horizontal scaling
> Increased fault tolerance
> cheaper compared to vertical in long run.
Disadvantages:
i. Requires complex architecture (load balancers, distributed databases, etc.)
ii. Difficult to maintain strong consistency across distributed nodes.
iii. More machines => more networking, power, and maintainence.
iv. Needs orchestration tools like Kubernetes, Ansible etc.
v. Issues can be spread across nodes, making root-cause analysis tricky.
vi. Communication between nodes adds latency and complexity.
```

```
Horizontal X Vertical

i. Cost Effectiveness: Horizontal for large systems, Vertical becomes costlier long-term.
ii. Flexibility: Horizontal
iii. Fault Tolerance: Horizontal
iv. Performance: Horizontal (improves as workload is distributed), Vertical (improves but can hit hardware limits)
v. Complexity: Vertical less complex
vi. Applicability: Horizontal for massive scalability needs, vertical for moderate requirements
vii. vertical is high secure because more control over a single server.
viii. horizontal is super fast when compared to vertical

> Follow hybrid approach of combining the speed and consistency of vertical scaling, with the resilience and infinite scalability of horizontal scaling.
```

```
Achieving Scalability

> Vertical scaling for an app like a big building with everything inside, horizontal it it's more like a city with many differenct parts.

> NoSQL for lots of data and users at once, SQL for smaller apps

> Serverless can be an excellent choice for applications with unpredictable traffic patterns or occasional spikes in activity because:

i. it automatically cotrols resource scalability depending on demand.
ii. pay only for the actual resources used.
iii. AWS lambda or azure functions reduce operational overhead by handling underlying infrastructure.
```

```
Bottlenecks that hurt the Scalability

1. Database bottlenecks
> Slow queries, ineffective indexing, insufficient hardware resources, or inadequate indexing cause the database to become a performance bottleneck.

2. Network bottlenecks in a distributed system
> network bandwidth or latency becomes a limiting factor
> content delivery infrastructure
> too many requests straining the network

3. Server bottlenexks
> server resources like CPU, RAM or disk I/O

4. Authentication bottlenecks
> When the process of confirming user identities and allowing access to resources becomes a limiting element in a system's overall performance and usability.
> ineffective authentication procedures, a high volume of user authentication requests, or insufficient infrastructure for authentication.

5. Third-party services bottlenecks
> modern apps frequently rely on third-party services like cloud storage, geolocation, and payment processing whcih may limit a system's overall performance, dependability and scalability.

6. Code Execution bottlenecks
> The design, writing, or execution of software code affects a computer system's performance and efficiency.

7. Data Storage Bottlenecks
> slow access to file storage systems or inefficient utilization of disk space, leading to issues such as slow data access, data loss, or scalability problems.

```
