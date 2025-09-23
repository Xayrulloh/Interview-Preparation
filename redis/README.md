# Redis Interview Questions

1. ## **What is Redis and why is it used**

   - **Type:** _In-memory data structure store_
   - **Key Features:**
     - Supports strings, hashes, lists, sets, sorted sets
     - Sub-millisecond latency
     - Atomic operations
   - **Primary Use Cases:**
     - Caching layer
     - Session storage
     - Real-time analytics
     - Message broker (Pub/Sub)

2. ## **Redis vs Traditional Databases**

   | Aspect        | Redis              | MySQL/MongoDB      |
   | ------------- | ------------------ | ------------------ |
   | **Storage**   | In-memory          | Disk-based         |
   | **Speed**     | Microsecond reads  | Millisecond reads  |
   | **Data Size** | Limited by RAM     | Limited by disk    |
   | **Use Case**  | Caching, real-time | Persistent storage |

3. ## **Redis Concurrency Handling**

   - **Single-threaded:** _by design (avoids locks)_
   - **Non-blocking I/O:**
     - Uses multiplexing (epoll/kqueue)
     - Processes commands one-by-one
   - **Atomic operations:** _INCR, SETNX, etc._

4. ## **Redis Pub/Sub**

   - **Publish-Subscribe:** _messaging pattern_
   - **Channels:** _Categories for messages_
   - **Example Flow:**
     1. SUBSCRIBE news_channel
     2. PUBLISH news_channel "Hello Redis"
     3. All subscribers receive message

5. ## **Redis Persistence**

   1. ### **(Snapshotting)**

      - Periodic binary snapshots
      - Configurable intervals (save 900 1)
      - Pros: Compact, faster restarts
      - Cons: Potential data loss

   2. ### **(Append-Only File)**

   - Logs every write operation
   - Configurable sync options:
     - always: safest
     - everysec: balanced
     - no: fastest
   - Pros: Durability
   - Cons: Larger files

6. ## **Redis Keys**

   - **Format:** _Any binary sequence (max 512MB)_
   - **Best Practices:**
     - Use namespaces (user:1000:profile)
     - SET/GET/DEL commands
     - TTL for expiration
   - **Pattern Matching:**
     - KEYS user:\* (avoid in production)
     - SCAN for safe iteration

7. ## **When NOT to Use Redis**

   - **Large datasets** exceeding server RAM
   - **Complex transactions** requiring ACID
   - **Permanent storage** as sole database
   - **Heavy writes** with low-latency reads
   - **Relational data** needing joins
