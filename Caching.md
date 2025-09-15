### Caching

* Storing frequently accessed data in a location that is easily and quickly accessible. The purpose of caching is to improve the performance and efficiency of a system by reducing the amount of time it takes to access frequently accessed data.

* Caching acts as the local store for the data and retrieving the data from this local or temporary storage is easier and faster than retrieving it from the database.

* In a typical web application, we can add an application server cache, and an in-memory store like Redis alongside our application server.

* Cache Working
    * When the first time a request is made a call will have to be made to the database to process the query. This is known as a cache miss.
    * Before giving back the result to the user, the result will be saved in the cache.
    * When the second time a user makes the same request, the application will check your cache first to see if the result for that request is cached or not.
    * If it is then the result will be returned from the cache. This is known as a cache hit.
    * The response time for the second time request will be a lot less than the first time. 

* Why you cannot store all the data in cache?
    *  Hardware of the cache which is much more expensive than a normal database.
    * Also, the search time will increase if you store tons of data in your cache.
    * Cache is typically a volatile storage, meaning data is lost if the system crashes or restarts. For critical and long-term data, storing it only in cache would risk data loss.

* Types of Cache
    1. Application Server Cache: a storage layer within an application server that temporarily holds frequently accessed data, so it can be quickly retrieved without needing to go back to the main database each time. </br>
    Drawback: When you add multiple servers to handle a high volume of requests. With several servers, a load balancer sends requests to different nodes, but each node only has its own cache and doesn’t know about the cached data on other nodes.
    To fix this, there are two main options: Distributed Cache and Global Cache.

    2. Distributed Cache: In the distributed cache, each node will have a part of the whole cache space, and then using the consistent hashing function each request can be routed to where the cache request could be found.
    <br/> Let's suppose we have 10 nodes in a distributed system, and we are using a load balancer to route the request then.
    <br/> Each of its nodes will have a small part of the cached data.
    <br/> To identify which node has which request the cache is divided up using a consistent hashing function, so that each request can be routed to where the cached request could be found.
    <br/> If a requesting node is looking for a certain piece of data, it can quickly know where to look within the distributed cache to check if the data is available.

    3. Global Cache: you will have a single cache space and all the nodes use this single space. Every request will go to this single cache space. There are two kinds of the global cache
    <br/> First, when a cache request is not found in the global cache, it's the responsibility of the cache to find out the missing piece of data from anywhere underlying the store (database, disk, etc).
    <br/> Second, if the request comes and the cache doesn't find the data then the requesting node will directly communicate with the DB or the server to fetch the requested data.

    4. CDN (Content Distribution Network): It is essentially a group of servers that are strategically placed across the globe with the purpose of accelerating the delivery of web content.
        * It manages servers that are geographically distributed over different locations.
        * Stores the web content in its servers.
        * Attempts to direct each user to a server that is part of the CDN and close to the user so as to deliver content quickly.
    <br/>
    <br/> CDN is used where a large amount of static content is served by the website.
    <br/> First, request ask the CDN for data, if it exists then the data will be returned. If not, the CDN will query the backend servers and then cache it locally.

* Applications of Caching
    * Web Page Caching
    * Database Caching
    * CDNs: they use caching to keep copies of data in several places throughout the globe.
    * Session Caching: Applications store session data in a cache to remember user info between visits, making experience seamless
    * API Response Caching: Frequently requested API data, like stock prices or weather data, can be cached so responses are faster.

* Advantages of using Caching
    * Improved performance
    * Reduced load on the original source (application server/database)
    * Cost savings
* Disadvantages of using Caching
    * Data inconsistency
    * Cache eviction issues if policies are not designed properly
    * Additional complexity

* Cache Invalidation Strategies
* Eviction Policies
