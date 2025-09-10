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



