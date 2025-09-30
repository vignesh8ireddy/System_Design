### Proxies in System Design

* An intermediary between client devices and servers, intercepts traffic facilitating communication through forwarding requests and responses.

* Purpose of proxy servers
    1. Content Filtering: filtering content based on different policies, blockading access to particular websites or content categories. Prevents access to malicious content material.

    2. Privacy and Anonymity: Forward proxies masks the IP addresses of client devices, provides a degree of anonymity all throughout web surfing. Useful for users who wanna be anonymous.

    3. Security and Accesss Control: Network security by examining and filtering incoming traffic. Block malicious content, filter out dangerous websites, prevent unauthorized access to sensitive resources.

    4. Load Balancing: Reverse proxies distribute incoming traffic across more than one servers to optimize resource utilization.

    5. Caching: Proxies, in particular caching proxies, keep copies of frequently accessed resources locally.

* Types of Proxy Servers
    1. Forward Proxy: sits between client and internet, used to send data to user groups within the internal network. evaluates the information given with the request to determine if it should proceed with establishing a connection.
        * Enhancing client anonymity
        * Accessing geo-blocked or restricited content
        * Content filtering and monitoring in organizations
        * Reducing bandwidth consumption through caching
        * Logging and tracking user activity for compliance

    2. Reverse Proxy Server: sits between internet and server, listens to the requests made by the client and redirect to the particular web server which is present on different servers
        * Load balancing accross multiple servers
        * Caching content to improve server performance
        * Protecting backend servers from direct exposure to the internet
        * SSL/TLS offloading to improve server efficiency
        * Mitigating DDoS attacks and enhancing security

    3. Web Proxy Server: When an HTTP request is forwarded via a web proxy, only the URL is sent instead of its path. A particular proxy server receives the request and responds. Examples: HAP Proxy and Apache Proxy.

    4. Public Proxy: Hides users IP addresses in order to hide their identity.

* Disadvantages of Proxy Servers: Latency and Configuration complexity