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

- ## 🧱 Technical Building Blocks in System Design

  _This section explores the essential components used to build scalable,
  reliable, and efficient systems. These concepts are the "building materials"
  of modern architecture._

  - ### APIs and API Gateway

    **What is it?** _An API (Application Programming Interface) defines how
    components interact. An API Gateway is a single entry point that routes
    client requests to different backend services._

    **When to Use:**

    - _To decouple frontend and backend._
    - _To manage microservices._
    - _To apply rate-limiting, authentication, and logging in one place._

    **Common Patterns:**

    - _REST_
    - _GraphQL_
    - _gRPC_

    **Tools:**

    - _Kong, NGINX, AWS API Gateway, Apigee_

  - ### Databases

    **What is it?** _A database stores, organizes, and retrieves data
    efficiently._

    **Types:**

    - **Relational (SQL):** _PostgreSQL, MySQL_
    - **Non-Relational (NoSQL):** _MongoDB, DynamoDB, Cassandra_

    **When to Use:**

    - **SQL:** _Structured, transactional data (e.g., user records)_
    - **NoSQL:** _Flexible, large-scale data (e.g., user activity logs)_

    **Design Concepts:**

    - _Indexing_
    - _Joins_
    - _Transactions (ACID vs BASE)_
    - _Data modeling_

  - ### Caching Systems

    **What is it?** _Fast-access storage layer to reduce database or computation
    load._

    **When to Use:**

    - _Frequently accessed or expensive-to-calculate data_

    **Types:**

    - **In-memory:** _Redis, Memcached_
    - **Distributed caches:** _Hazelcast, Couchbase_

    **Challenges:**

    - _Cache invalidation_
    - _Eviction strategies (LRU, LFU, TTL)_
    - _Write-through vs write-back vs write-around_

  - ### Content Delivery Networks (CDNs)

    **What is it?** _A CDN delivers static content (e.g., images, JS, CSS) from
    geographically distributed edge servers._

    **When to Use:**

    - _Global apps with heavy media_
    - _To reduce latency and origin load_

    **Providers:**

    - _Cloudflare, Akamai, Fastly, Amazon CloudFront_

  - ### Load Balancers

    **What is it?** _A system that evenly distributes incoming network traffic
    across backend servers._

    **When to Use:**

    - _Scale horizontally_
    - _Ensure high availability and failover_

    **Types:**

    - _Layer 4 (Transport) vs Layer 7 (Application)_
    - _Active-Passive vs Active-Active_

    **Examples:**

    - _NGINX, HAProxy, AWS ELB_

  - ### Message Brokers / Queues

    **What is it?** _Tools that enable asynchronous communication by queuing
    messages between components._

    **When to Use:**

    - _Decouple producers and consumers_
    - _Buffer high-load tasks (e.g., notifications, processing)_

    **Types:**

    - _Kafka (stream), RabbitMQ, SQS, NATS_

    **Considerations:**

    - _Message ordering_
    - _Durability_
    - _Delivery guarantees (at-most-once, at-least-once, exactly-once)_

  - ### Distributed Storage Systems

    **What is it?** _Storage systems that span across multiple machines or data
    centers._

    **When to Use:**

    - _Large-scale data (e.g., videos, backups, logs)_
    - _High availability_

    **Examples:**

    - _Amazon S3, Google Cloud Storage, HDFS, Ceph_

    **Features:**

    - _Replication_
    - _Erasure coding_
    - _Tiered storage_

  - ### Configuration Management

    **What is it?** _Tools and techniques to manage software configuration
    across environments._

    **When to Use:**

    - _Multi-env deployments (dev/stage/prod)_
    - _Infrastructure as Code (IaC)_

    **Tools:**

    - _Ansible, Terraform, Chef, Puppet_

  - ### Service Mesh

    **What is it?** _A layer to handle service-to-service communication,
    observability, and security in microservices._

    **When to Use:**

    - _Kubernetes or microservices architectures_
    - _Need for tracing, retries, mTLS, policies_

    **Examples:**

    - _Istio, Linkerd, Consul Connect_

  - ### Observability Stack

    **What is it?** _Collecting and analyzing logs, metrics, and traces to
    understand system behavior._

    **When to Use:**

    - _Always (especially in prod)_
    - _Debugging or performance optimization_

    **Tools:**

    - _Prometheus + Grafana_
    - _ELK stack (Elasticsearch, Logstash, Kibana)_
    - _Jaeger, OpenTelemetry, Datadog_
