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

- ## 🏗 Designing Real-World Systems

  _This section covers common system design interview questions that require
  end-to-end architecture thinking. Each example highlights critical components,
  trade-offs, and justifications._

  - ### URL Shortener (e.g., bit.ly)

    **What is it?** _A service that takes a long URL and returns a shortened
    version._

    **Key Requirements:**

    - _Short unique ID generation_
    - _Fast redirection (low latency)_
    - _Analytics (click count, geo info)_

    **Components:**

    - _Hashing or Base62 ID generator_
    - _Database to store mappings (URL ↔ ID)_
    - _Caching for hot links_
    - _Load balancer, API gateway_

    **Challenges:**

    - _Collision handling_
    - _Database scalability (partitioning by hash)_

  - ### Rate Limiter

    **What is it?** _A system to limit how frequently a user can make requests._

    **Use Cases:**

    - _Prevent abuse (login attempts, API usage)_
    - _Ensure fairness in multi-tenant systems_

    **Techniques:**

    - _Token Bucket, Leaky Bucket, Fixed Window, Sliding Log_
    - _Redis or in-memory store for counters_

    **Key Design Points:**

    - _Per-user/IP throttling_
    - _Global vs per-endpoint limits_

  - ### Messaging/Chat System (e.g., WhatsApp)

    **What is it?** _Real-time or asynchronous message exchange between users._

    **Core Features:**

    - _Message queues (Kafka, RabbitMQ)_
    - _Delivery receipts, read status_
    - _User presence tracking_

    **Challenges:**

    - _Message ordering & consistency_
    - _Offline message delivery_
    - _Scalability under high fan-out (group chats)_

  - ### Social Feed (e.g., Twitter, Instagram)

    **What is it?** _A personalized feed of posts/tweets/images based on follows
    or interests._

    **Feed Generation Models:**

    - _Pull-based (on read)_
    - _Push-based (on write)_
    - _Hybrid (pre-generate feed for active users)_

    **Scalability Considerations:**

    - _Fan-out writes vs reads_
    - _Use of queues, denormalized storage_
    - _Caching & timeline sharding_

  - ### File Storage System (e.g., Dropbox, Google Drive)

    **What is it?** _A system to upload, store, and retrieve user files with
    metadata._

    **Core Components:**

    - _Distributed storage (S3, HDFS, GCS)_
    - _Metadata service (file names, structure)_
    - _Chunking large files_
    - _Versioning & access control_

    **Challenges:**

    - _Data deduplication_
    - _Secure sharing and permissions_

  - ### Video Streaming Platform (e.g., YouTube, Netflix)

    **What is it?** _A platform that allows users to stream video content._

    **Design Focus:**

    - _Upload pipeline: transcoding, chunking, storage_
    - _CDN distribution for low latency_
    - _Playback buffering, adaptive bitrate (ABR)_

    **Scaling Challenges:**

    - _Storage costs for replicas_
    - _Live streaming vs on-demand differences_

  - ### Notification System (e.g., push/email/SMS alerts)

    **What is it?** _System to send time-sensitive messages across multiple
    channels._

    **Key Features:**

    - _Multi-channel dispatch (email, push, SMS)_
    - _User preferences & retries_
    - _Asynchronous processing via queues_

    **Challenges:**

    - _Idempotency for retries_
    - _Rate limiting for third-party APIs_

  - ### Ride-Sharing Platform (e.g., Uber, Lyft)

    **What is it?** _A platform to connect drivers and riders in real time._

    **Core Components:**

    - _Real-time location tracking_
    - _Matching engine (drivers ↔ riders)_
    - _Pricing algorithm (surge, distance)_
    - _Trip lifecycle management_

    **Scaling Challenges:**

    - _Geospatial indexing (e.g., Uber's H3)_
    - _Low-latency event systems_

  - ### E-commerce Platform (e.g., Amazon)

    **What is it?** _Online system to display, sell, and manage products._

    **Key Subsystems:**

    - _Product catalog (search, filter)_
    - _Shopping cart_
    - _Checkout flow & payment_
    - _Order fulfillment, warehouse updates_

    **Tech Concerns:**

    - _Inventory consistency_
    - _User personalization_
    - _Search scalability (Typesense, Elasticsearch)_

  - ### Analytics System (e.g., Google Analytics, Amplitude)

    **What is it?** _Tracks user behavior and aggregates it for reporting._

    **Key Features:**

    - _Real-time event ingestion (Kafka, Flink)_
    - _Data pipeline (ETL → Data Warehouse)_
    - _User-level metrics, dashboards_

    **Storage Options:**

    - _ClickHouse, BigQuery, Redshift_

    **Challenges:**

    - _Data volume and deduplication_
    - _Event schema evolution_

  - ### Payment System (e.g., Stripe, PayPal)

    **What is it?** _Handles transactions, fraud detection, and payment
    processing._

    **Components:**

    - _PCI-compliant storage_
    - _Idempotent transaction creation_
    - _Webhook system for external notification_

    **Concerns:**

    - _Atomicity (debit one account, credit another)_
    - _Rollbacks and reconciliation_
    - _Third-party API errors_

- ## 📝 Interview Strategy & Frameworks

  _This section provides a structured approach to cracking system design
  interviews, including preparation strategies, frameworks, and evaluation
  criteria._

  - ### Understanding the Interview Format

    **What is it?** _System design interviews assess your ability to design
    large-scale, distributed systems under constraints._

    **Common Settings:**

    - _45–60 minute sessions_
    - _Whiteboard or virtual design tools_
    - _Focus on trade-offs, scalability, and clarity_

    **What Interviewers Look For:**

    - _Communication & structure_
    - _Technical depth & breadth_
    - _Handling edge cases & trade-offs_

  - ### The 4-Step Design Process

    **What is it?** _A consistent method to approach any system design problem._

    **Steps:**

    1. **Clarify Requirements** _Ask questions to define core vs. optional
       features._
    2. **High-Level Design** _Draw components: clients, services, databases,
       queues, etc._
    3. **Deep Dive** _Zoom into a few components (e.g., DB schema, cache
       logic)._
    4. **Bottlenecks & Trade-offs** _Discuss scaling, failure handling,
       consistency, etc._

  - ### Common Frameworks

    **What is it?** _Mental models that help you structure design questions._

    **1. RISE (Requirements, Interfaces, Storage, Estimate):**

    - _Start with user goals and system constraints_
    - _Define APIs and user interactions_
    - _Design data storage and structure_
    - _Estimate usage, traffic, and scale_

    **2. SCALE (Storage, Cache, Availability, Load balancing, Elasticity):**

    - _Focus on scaling a known system_
    - _Drives discussion on performance bottlenecks_

    **3. SPACE (Security, Performance, Availability, Cost, Experience):**

    - _Balance system goals beyond just scalability_
    - _Great for open-ended or product-oriented systems_

  - ### Estimation Questions

    **What is it?** _Quick back-of-the-envelope calculations to ground your
    assumptions._

    **Common Examples:**

    - _How many requests/sec will the system serve?_
    - _How much storage per user per day?_
    - _Data retention costs over 1 year?_

    **Why It Matters:**

    - _Justifies architecture choices_
    - _Shows realism and engineering maturity_

  - ### Handling Trade-offs

    **What is it?** _All real-world systems involve compromises. Interviewers
    want to see you reason through them._

    **Typical Trade-offs:**

    - _Consistency vs Availability (CAP) and Latency_
    - _Read vs Write optimization_
    - _Cost vs Performance_
    - _Speed to build vs Long-term scalability_

    **Best Practices:**

    - _Be explicit when choosing one side_
    - _Mention fallback strategies_

- ## 🧪 Self-Preparation & Practice

  _This section offers practical tips, study resources, and exercises to help
  you master system design through consistent and focused practice._

  - ### How to Structure Your Preparation

    **Why It Matters:** _System design is a skill best built over time through
    repetition and exposure to real-world problems._

    **Preparation Strategy:**

    - _Start with fundamentals (latency, throughput, CAP theorem, caching,
      etc.)_
    - _Learn key components (load balancers, databases, queues, etc.)_
    - _Study real-world systems (Twitter, Dropbox, Uber, etc.)_
    - _Practice designing systems on paper/whiteboard_
    - _Get feedback from peers or mentors_
    - _Reflect and improve from mock interviews_

  - ### Must-Read Resources

    **1. System Design Primer (GitHub)** _One of the most comprehensive
    resources with explanations, strategies, and practice problems._
    [System Design Primer Github](https://github.com/donnemartin/system-design-primer)

    **2. System Design Handbook** _Step-by-step guides, questions, and
    architecture walkthroughs._
    [System Design Handbook](https://www.systemdesignhandbook.com/guides/system-design-interview)

    **3. Interviewing.io System Design Guide** _Clear breakdown of design
    concepts and interview approach._
    [Interviewing.io System Design Guide](https://interviewing.io/guides/system-design-interview/part-two)

    **4. High Scalability Blog (Archive)** _Chronological lessons learned from
    real-world architecture._
    [High Scalability Blog (Archive)](https://web.archive.org/web/20221030091841/http://www.lecloud.net/tagged/scalability/chrono)

    **5. System Design Interview Questions (Handbook)** _Curated list of
    open-ended design questions and variations._
    [System Design Interview Questions (Handbook)](https://www.systemdesignhandbook.com/blog/system-design-interview-questions/)

    **6. Useful You Tube Videos**

    - **[Google SWE System Design](https://www.youtube.com/playlist?list=PLjTveVh7FakKjb4UYzUazqBNNF-WGurXp)**
    - **[System Design by Gaurav Sen](https://youtube.com/playlist?list=PLMCXHnjXnTnvo6alSjVkgxV-VH6EPyvoX&feature=shared)**
    - **[Harvard Lecture](https://www.youtube.com/watch?v=-W9F__D3oY4)**

  - ### Practice Techniques

    **1. Paper & Whiteboard Practice** _Draw architecture diagrams by hand to
    simulate interview conditions._

    **2. Timed Mock Sessions** _Limit yourself to 45–60 minutes per problem._

    **3. Peer Reviews & Feedback** _Explain your designs to others and get
    critical feedback._

    **4. Flashcards for Concepts** _Use flashcards to memorize latency numbers,
    protocols, consistency models._

    **5. Reverse Engineering** _Pick any popular product and try to imagine how
    it’s built._

  - ### Systems to Try Designing (Sorted by Complexity)

    **Beginner:**

    - _URL shortener_
    - _Rate limiter_
    - _Image upload service_

    **Intermediate:**

    - _Chat/messaging app_
    - _Feed system (Instagram, Twitter)_
    - _Video streaming platform_

    **Advanced:**

    - _Distributed file storage (Dropbox)_
    - _Ride-sharing app (Uber)_
    - _E-commerce marketplace_
    - _Analytics pipeline_

  - ### Tracking Progress

    **What to Track:**

    - _Number of designs practiced_
    - _Feedback and mistakes_
    - _Knowledge gaps (e.g., protocols, algorithms)_

    **How to Stay Consistent:**

    - _Use Notion, Obsidian, or a simple doc to journal lessons_
    - _Build a “System Design Portfolio” with your drawings_
    - _Revisit hard problems monthly to reinforce learning_
