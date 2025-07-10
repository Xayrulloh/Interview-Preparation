# System Design Interview Preparation

- ## 🧠 Core Concepts in System Design

  _This step covers foundational system design concepts that are essential for
  technical interviews, designing scalable systems, and making architectural
  decisions_

  - ### Scalability

    **What is it?** _Scalability is the system's ability to handle increased
    load without degrading performance._

    **Types:**

    - **Vertical Scaling (Scale-Up):** _Add more resources (CPU, RAM) to a
      single machine._
    - **Horizontal Scaling (Scale-Out):** _Add more machines to distribute the
      load._

    **When to Use:**

    - _When your user base or data volume is growing._
    - _When performance bottlenecks arise due to limited hardware._

    **Trade-offs:**

    - _Vertical scaling is simple but has limits._
    - _Horizontal scaling requires distributed coordination (e.g., sharding,
      replication)._

    **Examples:**

    - _Adding more web servers behind a load balancer._
    - _Splitting a monolithic database by user ID._

  - ### Latency vs Throughput

    **What is it?**

    - **Latency:** _Time it takes to process a single request._
    - **Throughput:** _Number of requests processed per unit time._

    **When to Focus On:**

    - **Latency:** _Real-time applications like chat, video calls._
    - **Throughput:** _Background processing, analytics systems._

    **Trade-off:** _Batching requests increases throughput but adds latency._

    **Examples:**

    - **Kafka:** _Streams can process millions of events per second (high
      throughput)._
    - **REST APIs** _Should respond within 200ms for good user experience (low
      latency)._

  - ### CAP Theorem (Availability vs Consistency)

    **What is it?** _In distributed systems, you can only have two out of
    three:_

    - **Consistency:** _All nodes see the same data._
    - **Availability:** _Every request gets a response (even during failures)._
    - **Partition Tolerance:** _System continues working even with network
      splits._

    **When to Use:**

    - **Consistency:** _Banking, inventory systems._
    - **Availability:** _Social networks, logging systems._

    **Examples:**

    - **CP:** _HBase, MongoDB (strong consistency mode)._
    - **AP:** _DynamoDB, CouchDB._

  - ### Load Balancing

    **What is it?** _A method of distributing requests across multiple servers
    to ensure reliability and responsiveness._

    **When to Use:**

    - _Any multi-server system._
    - _To prevent bottlenecks or server crashes._

    **Common Strategies:**

    - _Round Robin_
    - _Least Connections_
    - _Weighted Routing_
    - _IP Hashing_

    **Benefits:**

    - _Fault tolerance_
    - _Better resource utilization_
    - _Zero-downtime deployments_

  - ### Caching

    **What is it?** _Storing frequently accessed data in fast storage (e.g.,
    memory)._

    **When to Use:**

    - _Repeated queries with same response._
    - _Reduce database or API load._

    **Types:**

    - _In-memory (Redis, Memcached)_
    - _CDN (Cloudflare, Akamai)_
    - _Browser caching_

    **Challenges:**

    - _Cache invalidation_
    - _Stale data_
    - _Cache stampedes_

  - ### Data Partitioning (Sharding)

    **What is it?** _Splitting large datasets across smaller, more manageable
    pieces (shards)._

    **When to Use:**

    - _Single DB can't handle the volume._
    - _Faster access to subsets of data._

    **Partitioning Strategies:**

    - _Hash-based (e.g., user ID)_
    - _Range-based (e.g., date ranges)_
    - _Directory-based (lookup table)_

    **Challenges:**

    - _Cross-shard queries_
    - _Re-sharding_
    - _Hot partitions_

  - ### Replication

    **What is it?** _Creating copies of data to increase availability and fault
    tolerance._

    **When to Use:**

    - _To serve more read traffic._
    - _For disaster recovery._

    **Types:**

    - _Master-Slave (Primary-Replica)_
    - _Multi-Master_

    **Challenges:**

    - _Replication lag_
    - _Write conflicts in multi-master_

  - ### Consistency Models

    **What is it?** _Defines how consistent the data appears to users across a
    distributed system._

    **Models:**

    - **Strong Consistency:** _All users see the same data._
    - **Eventual Consistency:** _Data becomes consistent over time._
    - **Causal Consistency, Read-Your-Writes, Monotonic Reads:** _Middle-ground
      models._

    **When to Use:**

    - _Strong: Financial systems_
    - _Eventual: Social media feeds_

  - ### Message Queues & Asynchronous Communication

    **What is it?** _Producers publish messages to a queue, and consumers
    process them asynchronously._

    **When to Use:**

    - _Background tasks (e.g., sending emails)_
    - _Buffering burst traffic_
    - _Decoupling services_

    **Examples:**

    - _Kafka, RabbitMQ, Amazon SQS_

    **Challenges:**

    - _Message ordering_
    - _Retry and duplication_
    - _Dead-letter queues_

  - ### Rate Limiting & Throttling

    **What is it?** _Restricting how often a client can make a request._

    **When to Use:**

    - _Preventing abuse (e.g., login brute force)_
    - _Protecting services from overload_

    **Techniques:**

    - _Token Bucket_
    - _Leaky Bucket_
    - _Fixed/Sliding Window Counters_

  - ### Failover & Redundancy

    **What is it?** _Backup systems that take over when a primary system fails._

    **When to Use:**

    - _Mission-critical applications_
    - _Disaster recovery setups_

    **Examples:**

    - _Active-passive database setup_
    - _Load balancers with multiple backends_

  - ### Monitoring & Observability

    **What is it?** _Tracking the health, performance, and behavior of systems
    in real-time._

    **When to Use:**

    - _Always, especially in production_

    **Tools:**

    - _Prometheus, Grafana, Datadog_
    - _ELK Stack (Elasticsearch, Logstash, Kibana)_
    - _OpenTelemetry_

    **Components:**

    - _Metrics (CPU, memory, requests/sec)_
    - _Logs (structured, error logs)_
    - _Traces (request flows across services)_

  - ### Idempotency

    **What is it?** _An operation that can be safely repeated without changing
    the result._

    **When to Use:**

    - _Payment systems_
    - _Account creation APIs_
    - _Retry logic_

    **Techniques:**

    - _Use unique request IDs or tokens_
    - _Store operation history_

  - ### Back-pressure

    **What is it?** _Controlling the flow of data to prevent systems from being
    overwhelmed._

    **When to Use:**

    - _High-throughput stream processing_
    - _Queued systems_

    **Strategies:**

    - _Drop or delay messages_
    - _Pause upstream producers_

  - ### Service Discovery

    **What is it?** _Mechanism to automatically detect service instances in
    dynamic environments._

    **When to Use:**

    - _Microservice architecture_
    - _Container orchestration (e.g., Kubernetes)_

    **Tools:**

    - _DNS-based discovery_
    - _etcd, Consul, Eureka_
