### Rate Limiting

A technique of controlling the rate of traffic or requests to a system to regulate how quickly it processes and serves incoming requests. It prevents overload, and ensure fair resource distribution.

* Reduces the possibility fo resource abuse and denial-of-service (DoS) attacks and hence the best possible performance, dependability, and security of systems.

* Usecases of Rate Limiting:
    1. API Rate Limiting: to control the volume of client requests, ensure fair access and prevent abuse.
    2. Web Server Rate Limiting: as a defense against denial-of-service attacks and to prevent server overload.
    3. Database Rate limitation: preventing from undue strain and to preserve database performance.
    4. Login Rate restriction: To stop password guessing and brute-force assaults, login systems employ rate restriction.

* Types of Rate Limiting
    1. IP-based Rate Limiting: restricting the amount of traffic that can originate from a single IP address, frequently used to stop abuses like bots and DoS attacks.
        * Limitation 1: using techniques like VPNs, proxy servers, or even botnets to spoof different IPs and get around the limit.
        * Limitation 2: If multiple users share same IP address like in a corporate network, a legitimate user could get blocked.

    2. Server-based Rate Limiting: number of requests that can be sent to a particular server in a predetermined period of time (e.g 100 requests per second)
        * Limitation 1: If attackers send requests across different servers, they might avoid hitting the rate limit on any single one.
        * Limitation 2: If the limit is too low or the server is under heavy load, even legitimate users might face blocks, and if the limit is too high, attackers may get around the limit.
    
    3. Geography-based Rate Limiting: restricting traffic based on the geographic location of IP address. mostly used for complying with regional laws and regulations.
        * Limitation 1: could get around using VPNs or proxy servers

* Rate Limiting Algorithms
    1. Token Bucket Algorithm
    2. Leaky Bucket Algorithm
    3. Fixed Window Counting Algorithm
    4. Sliding Window Log Algorithm

* Client-side vs. Server-side Rate Limiting
    1. Request Control
        * client-side: requests are throttled/delayes before reaching the server.
        * server-side: requests are processed by server then decides to accept, reject or delay
    2. Flexibility
        * client-side: Limited flexibility as it relies on client-side configurations
        * server-side: Great flexibility
    3. Security
        * client-side: less secure as it can be bypassed or manipulated by clients
        * server-side: more secure

* Rate Limiting in different layers of the system
    1. Application layer: Implementing rate limitation code inside the application code, it is applicable to all requests the application is processing irrespective of where they come from or end up.
    2. API Gateway layer: Implementing rate limitation rules inside the API gateway, it covers incoming requests and applies rate limiting before they reach application.
    3. Service Layer: Implementing rate limiting logic within individual services or microservices, applies to requests processed by each service independently allowing fine-grained control.
    4. Database layer: Rate limiting controls the rate of database queries, or transactions i.e read and write operations.

* Challenges of Rate Limiting
    1. Latency
    2. False Positives causing legite users frustrated
    3. Configuration Complexity particulary in systems with a variety of traffic patterns and use cases
    4. Scalability Challenges, if not appropriately scaled, rate limiting methods themselves may create a bottleneck under excessive load. One of the biggest challenges is making sure rate-limiting systems can manage growing traffic levels without seeing any degradation in performance.