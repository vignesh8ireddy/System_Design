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
        ```
        * Requests are distributed evenly across the servers in a sequential or rotational manner one after another.
        * First request to goes to server 1, next goes to server 2, and so on. So treats all of the servers equally
        * Doesn't consider the load already on a server or it's capacity (different servers may have different capacities) so risk of uneven distribution

        class LoadBalancer {
            private List<String> servers;
            private int currentIndex;

            public LoadBalancer(List<String> servers) {
                this.servers = new ArrayList<>(servers);
                this.currentIndex = 0;
            }

            public String getNextServer() {
                String nextServer = servers.get(currentIndex);
                currentIndex = (currentIndex + 1) % servers.size();
                return nextServer;
            }
        }

        public class RoundRobinExample {
            public static void main(String[] args) {
            
                // Sample list of servers
                List<String> serverList = new ArrayList<>();
                serverList.add("Server1");
                serverList.add("Server2");
                serverList.add("Server3");

                // Create a load balancer with the server list
                LoadBalancer loadBalancer = new LoadBalancer(serverList);

                // Simulate requests to the load balancer
                for (int i = 0; i < 10; i++) {
                    String nextServer = loadBalancer.getNextServer();
                    System.out.println("Request " + (i + 1) + ": Routed to " + nextServer);
                }
            }
        }
        ```
        2. Weighted Round Robin
        ```
        * Servers with high capacities are given a larger portion of the requests.
        * Distribution is cyclic like before but server receiving number of requests proportional to its capacity
        * Server 1 (0.3) => load balancer always makes sure it has 3 requests at a time, Server 2 => gets assigned only one request and until its done no other requests are assigned to it.

        class WeightedRoundRobinBalancer {
            private List<Server> servers;
            private int[] cumulativeWeights;
            private int totalWeight;
            private int currentIndex;
            private Random random;

            public WeightedRoundRobinBalancer(List<Server> servers) {
                this.servers = new ArrayList<>(servers);
                this.totalWeight = calculateTotalWeight(servers);
                this.cumulativeWeights = calculateCumulativeWeights(servers);
                this.currentIndex = 0;
                this.random = new Random();
            }

            private int calculateTotalWeight(List<Server> servers) {
                int totalWeight = 0;
                for (Server server : servers) {
                    totalWeight += server.getWeight();
                }
                return totalWeight;
            }

            private int[] calculateCumulativeWeights(List<Server> servers) {
                int[] cumulativeWeights = new int[servers.size()];
                cumulativeWeights[0] = servers.get(0).getWeight();
                for (int i = 1; i < servers.size(); i++) {
                    cumulativeWeights[i] = cumulativeWeights[i - 1] + servers.get(i).getWeight();
                }
                return cumulativeWeights;
            }

            public Server getNextServer() {
                int randomValue = random.nextInt(totalWeight);
                for (int i = 0; i < cumulativeWeights.length; i++) {
                    if (randomValue < cumulativeWeights[i]) {
                        currentIndex = i;
                        break;
                    }
                }
                return servers.get(currentIndex);
            }

            // Inner class representing a server with a weight
            static class Server {
                private String name;
                private int weight;

                public Server(String name, int weight) {
                    this.name = name;
                    this.weight = weight;
                }

                public String getName() {
                    return name;
                }

                public int getWeight() {
                    return weight;
                }
            }
        }

        public class WeightedRoundRobinExample {
            public static void main(String[] args) {
                // Sample list of servers with weights
                List<WeightedRoundRobinBalancer.Server> serverList = new ArrayList<>();
                serverList.add(new WeightedRoundRobinBalancer.Server("Server1", 3));
                serverList.add(new WeightedRoundRobinBalancer.Server("Server2", 2));
                serverList.add(new WeightedRoundRobinBalancer.Server("Server3", 1));

                // Create a weighted round-robin load balancer with the server list
                WeightedRoundRobinBalancer balancer = new WeightedRoundRobinBalancer(serverList);

                // Simulate requests to the load balancer
                for (int i = 0; i < 10; i++) {
                    WeightedRoundRobinBalancer.Server nextServer = balancer.getNextServer();
                    System.out.println("Request " + (i + 1) + ": Routed to " + nextServer.getName());
                }
            }
        }

        Drawback: Requires adjusting weighs as server capacities change
        ```

        3. Source IP hash
        ```
        * Distributing incoming requests among a set of servers based on the hash value of the source IP address, aiming to ensure that requests originating from the same source IP address are consistently directed to the same server.

        class SourceIpHashLoadBalancer {
            private Map<String, String> ipToServerMap;

            public SourceIpHashLoadBalancer() {
                this.ipToServerMap = new HashMap<>();
            }

            public void addServer(String serverName) {
                // Add server to the mapping
                ipToServerMap.put(serverName, serverName);
            }

            public String getServerForIp(String sourceIp) {
                // Calculate hash of the source IP
                int hash = sourceIp.hashCode();

                // Get the list of available servers
                String[] servers = ipToServerMap.keySet().toArray(new String[0]);

                // Map the hash value to a server index
                int serverIndex = Math.abs(hash) % servers.length;

                // Return the selected server
                return servers[serverIndex];
            }
        }

        public class SourceIpHashLoadBalancerExample {
            public static void main(String[] args) {
                // Create a source IP hash load balancer
                SourceIpHashLoadBalancer loadBalancer = new SourceIpHashLoadBalancer();

                // Add servers to the load balancer
                loadBalancer.addServer("Server1");
                loadBalancer.addServer("Server2");
                loadBalancer.addServer("Server3");

                // Simulate requests with different source IPs
                String[] sourceIps = {"192.168.1.1", "10.0.0.1", "172.16.0.1"};

                for (String sourceIp : sourceIps) {
                    String selectedServer = loadBalancer.getServerForIp(sourceIp);
                    System.out.println("Request from " + sourceIp + " routed to " + selectedServer);
                }
            }
        }

        * If certain source IPs are more active, then it may lead to uneven load distribution
        * Adding or removing Servers may disrupt session persistence (solution: Consistent Source IP Hashing)
        ```

        4. Consistent Hashing
        ```
        * To minimize the need for rehashing when the number of nodes in a system changes.
        * Represents the requests by the clients and the server nodes in a virtual ring structure called hashring.
        * Number of locations in the ring is not fixed, but it is considered to have an infinite number of points.
        * Both the server nodes and requests are placed in the ring using the same hash functions
        * Each request is served by the server node that first appears while traversing clockwise from the request.
        * Uniform Distribution of Data
        * Handles Load balancing flexibly while scaling the server nodes, when a new node is added to the network only small number of keys are remapped to the new node, which helps to reduce the overhead associated and similarly when a node removed.
        * Handles Node failures
        * No overhead of rehashing
        * Handles DUPLICATE requests

        Working of Consistent Hashing
        Phase 1: Hash Function Selection
        Phase 2: Server Node assignment based on the hash function.
        Phase 3: Key replication, i.e keys are copied across a number of network nodes to make sure that data is accessible in a distributed system even in the case of node failures.
        Phase 4: Node addition/removal, requires to remap the keys to new nodes in order to maintain system balance
        Phase 5: Load Balancing, to keep the system balanced when a node is overloaded, portions of its keys can be remapped to others.
        Phase 6: Failure Recovery, when a node fails remapping happens

        Implementation

        Step 1: Choose a Hash Function
                Common choices: MD5, SHA-1, or SHA-256
        Step 2: Define Hash Ring
                Represent the range of hash values as a ring and distribute them evenly.
        Step 3: Assign Nodes to the Ring
                Assign each node a position on the ring by hashing node's id
        Step 4: Key Mapping
                Map request keys with the same hash function and find position on the ring where the values fall.
                Walk clockwise from that position on the ring to find the first node encountered which becomes owner of the key.
        Step 5: Node Additions
                When a new node is added, compute its position on the hash ring using the hash function
                Identify the range of keys that will be owned by the new node by finding the predecessor node on the ring
                Update the ring to include new node and remap the affected keys
        Step 6: Node Deletions
                Identify the range of keys that will be affected by finding the successor node on the ring and update to remap affected keys to the successor
        Step 7: Load Balancing
                Periodically check the load on each node by monitoring the number of keys it owns.
                Consider redistribution some keys when there is an imbalance.

        Disadvantages
        1. Hash Function Complexity, overall efficiency is affected by how complicated the hash function is.
        2. Performace Cost, computing resources needed to map keys to nodes, replicate keys, and remap keys can result in some performance overhead.
        3. Lack of Flexibility, ability to adapt to changing requirements or shifting network conditions may be constrained by the rigid limits of consistent hashing.
        4. High Resource Use, for remapping, hashing, assigning keys
        5. Complexity of Management

        ```


    * Dynamic Load Balancing Algorithms: These algorithms adapts to the changing conditions of the system, such as variations in server load, network traffic, or resource availability.
        1. Least Connection Method
        ```
        * Distributes incoming workloads in a way that minimizes the current load on each server, aiming for a balanced distribution
        * Assigns new request to the server with fewest active connections.

        class LeastConnectionLoadBalancer {
            private Map<String, Integer> serverConnections;

            public LeastConnectionLoadBalancer() {
                this.serverConnections = new HashMap<>();
            }

            public void addServer(String serverName) {
                // Add a server to the load balancer with 0 initial connections
                serverConnections.put(serverName, 0);
            }

            public String getServerWithLeastConnections() {
                // Find the server with the least active connections
                int minConnections = Integer.MAX_VALUE;
                String selectedServer = null;

                for (Map.Entry<String, Integer> entry : serverConnections.entrySet()) {
                    if (entry.getValue() < minConnections) {
                        minConnections = entry.getValue();
                        selectedServer = entry.getKey();
                    }
                }

                // Increment the connection count for the selected server
                if (selectedServer != null) {
                    serverConnections.put(selectedServer, minConnections + 1);
                }

                return selectedServer;
            }
        }

        public class LeastConnectionLoadBalancerExample {
            public static void main(String[] args) {
                // Create a Least Connection load balancer
                LeastConnectionLoadBalancer loadBalancer = new LeastConnectionLoadBalancer();

                // Add servers to the load balancer
                loadBalancer.addServer("Server1");
                loadBalancer.addServer("Server2");
                loadBalancer.addServer("Server3");

                // Simulate requests and print the server to which each request is routed
                for (int i = 0; i < 10; i++) {
                    String selectedServer = loadBalancer.getServerWithLeastConnections();
                    System.out.println("Request " + (i + 1) + ": Routed to " + selectedServer);
                }
            }
        }

        * Additional computing needed for every new request
        * Ignores server capacities; a server with fewer connections may still have less capacity
        * Sticky sessions i.e no session persistence

        ```
        
        2. Least Response Time Method
        ```
        * Considers the historical performance of the servers to make decisions about routing incoming requests.
        ```
        
        3. Resource Based Load balancing algorithm
        ```
        * Distributes requests based on the current resource availability of each server (i.e resource health), such as CPU usage, memory or network bandwidth.
        * Requires continous monitoring of server resources, which can add complexity.
        * Real-time tracking of resources may consume additional system resources.
        ```

* Challenges of using Load Balancers
    1. Single Point of Failure: Issues with load balancer itself could cause traffic distribution to be disrupted.
    2. Complexity and Cost: Implementation and management can be complicated
    3. Configuration Challenges: especially when dealing with complex application architectures or diverse server environments.
    4. Potential for Overhead: there may be additional overhead in the form of delay and processing time, even though modern load balancers are designed to lessen this effect.
    5. SSL Inspection Challengers: When SSL termination is performed at the load balancer, it may introduce challenges related to SSL inspection and handling end-to-end encryption.

