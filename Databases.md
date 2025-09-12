## Databases in System Design

* One of the most critical system design choices is among SQL Vs NoSQL databases can drastically impact your system's overall performance and scalibility.

```
SQL Database
1. Tabular Data Model
2. Fixed and Pre-defined Schema
3. ACID Compliance: Atomicity, Consistency, Integrity and Durability
4. Structured Query Language: makes it suitable for applicaitions requiring statistical analytics and reporting.
5. Strong Relationships: SQL databases excel in coping with complex relationships between facts tables.

> Popular SQL databases: MySQL and PostgreSQL
> Usecases: Financial Systems, CMS, banking & Inventory Management, E-commerce
> Choosing SQL Database
1. Complex and Advanced Queries and reporting
2. Data Integrity: When facts consistency and integrity are paramount, particularly in financial or regulatory applications, ACID compliance best preference.
3. Transactions: A go-to option for packages that require support for multi-step, ACID compliant transactions, like e-commerce systems.
```

```
NoSQL Database
1. Flexible Data Model: key-cost pairs, document stores, huge-column shops and graph databases.
2. Schema-less: statistics can be inserted without a predefined scheman.
3. BASE: Basically Available, Soft State, Eventually Consistent i.e prioritizes excessive availability and performance over strict consistency.
4. Proprietary Query Language

> Popular NoSQL databases: MongoDB and Cassandra
> Usecases: Social Media or Big data Platforms, Real time analytics, IoT applications
> Choosing NoSQL database
1. High Scalability: handling a large amount of records and visitors, provides a good horizontal scalability opportunities.
2. Flexible Schema: Information structure is dynamic and may evolve through years.
3. Real time analytics: for processing streaming facts because of their pace and versatility.
```

#### Scalibility and Performance

1. Vertical Scaling in SQL (with limitations)
2. Horizontal Scaling in NoSQL

#### Query Language and Transactions
1. NoSQL databases vary in their query languages, with some using traditional SQL and others adopting unique approaches.
2. The choice between strong ACID transactions (SQL) and eventual consistency (NoSQL) depends on the importance of data integrity in your application.

#### Flexibility and Schema Evolution
1. Adapting a SQL database to evolving data requirements may involve complex schema changes and potential downtime.
2. Dynamic Schema evolution is supported by NoSQL databases, enabling developers to adjust to shifting requirements with no difficulty.

#### Importance of Database replication
1. High Availability: in the event of one or more servers fail.
2. Disaster Recovery
3. Load Balancing: for distributing read queries across multiple servers, reducing load on any single server and improving performance.
4. Fault tolerance
5. Scalability: distribution of write operations across multiple servers, reducing the load on any single server.
6. Data locality: reduces latency by bringing data closer to users.

#### Working of Database of Replication
1. Identify the primary database (Source)
2. Set Up Replica Databases (Targets)
3. Data Changes Captured: through a transaction log or change data capture mechanism
4. Transmit Changes to Replicas: captured changes are sent to replica databases over the network in real-time or at scheduled intervals.
5. Apply Changes on Replicas: apply changes and sync with primary database
6. Monitor and Maintain Synchroization: handling issues like delays or conflicts during synchronization
7. Read or Write Operations: Applications can read data from replicas (to reduce load on the primary) and may write to the primary, depending on the replication model.

#### Database Replication Models

1. Master-Slave Replication
All write operations, including inserts, updates, and deletions, must be received by the master database. and slave databases keep a duplicate of the data and replicate the modifications made to the master database.

2. Master-Master Replication/Multi-Master Replication
t is also known as bidirectional replication, is a setup in which two or more databases are configured as master databases, and each master can accept write operations. and changes made to any master database are replicated to all other master databases.

3. Snapshot Replication
Creating a copy of the whole database at a certain moment in time and then replicating that snapshot to one or more destination servers.

4. Transactional Replication
Any modifications made to a particular table in one database (publisher) are instantly copied to other databases (subscribers)

5. Merge Replication
It is a database synchronizaton method allowing both the central server (publisher) and its connected devices (subscribers) to make changes to the data, resolving conflicts when necessary.

#### Strategies for Database Replication

* These strategies determine how to select data, copy and distribute it between databases to gain specific goals such as scalability, availibility, and efficiency.

1. Full Database Replication
2. Partial Database Replication: Subset of database is replicated
3. Selective Database Replication: More granular control over which part of database is replicated.
4. Sharding: A database scaling technique that involves partitioning data across multiple database instances (shards) based on a key. This approach allows for distributing the workload and data storage acorss multiple servers, imporoving scalability and performance.
5. Hybrid Replication: combining multiple replication techniques to achieve specific goals.

#### Configurations of Database replication
1. Synchronous Replication Configuration: replicates changes in real-time to one or more replicas. Until atleast one copy acknowledges receiving the changes, the transaction isn't considered committed. Offers high data consistency

2. Asynchronous Replication Configuration: Primary database won't wait for the clones to acknowledge the replication. Faster transaction processing is possible but there may be small lag in consistency between primary and replica(s)

3. Semi-synchronous replication configuration: ensures improved performace and excellent data consistency for essential data by replicating changes to at least oen replica synchronously.

#### Challenges with Database Replication
1. Data Consistency
2. Complexity
3. Cost
4. Conflict Resolution
5. Latency