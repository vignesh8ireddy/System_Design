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


#### Database Sharding

* A technique for horizontal scaling of databases, where the data is split across multiple databases instances, or shards, to improve performance and reduce the impact of large amounts of data on a single database.
* It is a web server working with multiple data servers instead of working with only one server.

1. Key Based Sharding (hash-based sharding): we take the value of an entity such as ID, IP address of a client, zip code, etc and use this value as an input of the hash function. and the generated hash value is used to determine which shard we need to use to store the data.

Advantages:
* Predictable Data Distribution: Every key is associated with a particular shard, guaranteeing a uniform and consistent distribution of data
* Optimized Range Queries: key based sharding can be optimized to handle these range queries efficiently.
Disadvantages:
* Chances of Uneven Data Distribution: IF the sharding key is not well-distributed it may result in uneven data distribution across shards.
* Limited scalability with specific keys: If certain keys experience high traffic or if the dataset is heavily skewed toward specific key ranges.
* Complex Key Selection: Selecting an approriate sharding key is crucial for effective sharding.

2. Horizontal or Range Based Sharding: We divide the data by separating it into different parts based on the range of a specific value within each record. (let's say based on last name, A-P goes to one shard or rest goes to another shard or ID values, 100000-200000 goes to one shard and rest goes to other)

Advantages:
* Scalability using multiple shards
* Improved Performance through parallelization
Disadvantages:
* Complex querying across shards: Coordinating queries involving multiple shards can be challenging.
* Uneven Data Distribution as a result uneven workloads among shards

3. Vertical Sharding: we split the entire columns from the table and put them into new distict tables (shards). Data is totally independent of one partition to the other ones, and also each partition holds both distinct rows and columns. (for example, twitter users might have a profile, number of followers and some tweets posted by his/her own. We can place the user profiles on one shard, followers in the second shard, and tweets on a third shard.)

Advantages:
* Query Performance: by allowing each shard to focus on a specific subset of columns query performance is improved.
* Simplified Queries: Queries that require a specific set of columns can be simplified, as they only need to interact with the shard containing the relevant columns.
Disadvantages:
* Potential for Hotspots: Certain shards may become hotspots if they contain highly accessed columns
* Challenges in Scheman changes: making changes to the original schema (i.e adding or removing columns) may be more challenging, impacting multiple shards and require careful coordination.

4. Directory-Based Sharding: we create and maintain a lookup table or lookup service for the original database. Basically we use a shard key for lookup table and we do mapping for each entity that exists in the database. (client application -> lookup table -> shard)

Advantages:
* Flexible data distribution: the central directory (lookup table) can dynamically be managed and update the mapping of data to shard locations.
* Efficient Query Routing using the lookup tables
* Dynamic Scalability: adding or removing shards without requiring changes to the application logic.
Disadvatages:
* Centralized point of failure: If lookup table is unavailable or experience issues, it can disrupt the entire system.
* Increased latency: introducing additional layer, potentially leads to increased latency compared to other sharding techniques.

#### Ways to Optimize database sharding for even data distribution
1. Use consistent Hashing: for uniform distribution
2. Choose a good sharding key: making sure no hotspots
3. Range-based sharding with caution:  shard doesn't get overloaded with more data than others
4. Regularly monitor and rebalance whenever necessary to avoid uneven loads as data grows
5. Automate sharding logic: for automatically distributing data and maintaining balance across shards.

#### Alternatives to Database Sharding
1. Vertical Scaling: Instead of splitting the database, you can upgrade your existing server by adding more CPU, RAM, or storage to handle more load. (but has limitations)
2. Replication: Creating copies of the database on multiple servers. Ensures availability but can lead to synchronization issues.
3. Partitioning: Instead of sharding acroos multiple servers, partitioning splits data within the same server into smaller sections, improving query performance for large datasets
4. Caching: Storing frequently accessed data in a cache, you reduce the load on your main database, improving performance.
5. CDNs: For read-heavy workloads, using a Content Delivery Network can offload some of the data access from your primary database.)

#### Disadvatages of Sharding
1. Increased Complexity: when compared to single database
2. Rebalancing Challenges: re-distributing uneven shards can be difficult and time consuming
3. Cross-Shard Queries can be slower and more complicated to handle
4. Operational Overhead: more monitoring, backups and maintenance
5. Potential Data Loss: If a shard fails and isn't properly backed up, there's a higher risk of losing the data.

