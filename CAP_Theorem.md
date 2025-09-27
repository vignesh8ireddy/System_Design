* According to the CAP theorem, only two of the three desirable characteristics - Consistency, Availability and Partition tolerance can be shared or present in a networked shared data system or distributed system.
    * Provides a way of thinking about the trade-offs involved in designing and building distributed systems.
    * helps to explain why certain types of systems may be more appropriate for certain use cases.

* Properties of CAP theorem
    * Consistency: all clients see the same data simultaneously, no matter which node they connect to in a distributed system.
    * Availability: all non-failing nodes in a distributed system return a response for all read and write requests in a bounded amount of time, even if one or more other nodes are down. (Every request receives a response, whether successful or not.)
    * Partition Tolerance: the system continues to operate despite arbitrary message loss or failure in parts of the system.

* Trade-Offs in the CAP theorem
    1. CA System: A CA System delivers consistency and availiability across all the nodes. It can't do this if there is a partition between any two nodes in the system and therefore does't support partition tolerance.

    2. CP System: A CP System delivers consistency and partition tolerance at the expense of availability. When a partition occurs between two nodes, the systems shuts down the non-available node until the partition is resolved. Some of the examples of the databases are MongoDB, Redis, and HBase.

    3. AP System: An AP System availabiiity and partition tolerance at the expense of consistency. When a partition occurs, all nodes remains available, but those at the wrong end of a partition might return an older version of data than others. Example: CouchDB, Cassandra and Dyanmo DB, etc.

    Example:
    * We have a simple distributed system where S1 and S2 are two server. The two server can talk to each other. Here, System is partition tolerant. Here We will prove that system can be either consistent or available.
    * Suppose there is a network failure and S1 and S2 cannot talk to each other. Now assume that the client makes a write to S1. The client then send a read to S2.
    * Given S1 and S2 cannot talk, they have different view of the data. If the system has to remain consistent, it must deny the request and thus give up on availability.
    * If the system is available, then the system has to give up on consistency. This proves the CAP Theorem.

* Use Cases of the CAP Theorem
    1. Banking Transactions (CP System)
    2. Social Media Newsfeed (AP System)
    3. Online Shopping Cart (Hybrid CAP System): Adding items to the card could be AP, but when confirming the order and processing payment, the system might switch to a CP mode, ensuring consistency across all servers before finalizing the transaction.

