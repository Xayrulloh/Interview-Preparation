# MongoDB Interview Questions

1. ## **What's MongoDB**  
    *MongoDB is a popular, open-source NoSQL database that uses a document-oriented data model. Instead of tables and rows like traditional relational databases, MongoDB stores data in flexible, JSON-like documents organized into collections. This flexibility allows it to handle structured, semi-structured, and unstructured data, making it well-suited for modern applications*

2. ## **Advantages of MongoDB**
    - **Flexible Schema:** *Dynamic schema (BSON documents)*
    - **Indexing:** *Primary/secondary indexes on any field*
    - **Scalability:** *Horizontal scaling via sharding*
    - **High Performance:** *In-memory processing*
    - **Query Capabilities:** *Rich query language with:*
        - Pattern matching
        - Geospatial queries
        - Text search
    - **Agile Development:** *JSON-like documents map to objects*

3. ## **When to Use MongoDB**
    - **Modern Applications:**
        - Rapid iteration
        - Flexible data models
    - **Use Cases:**
        - Content management
        - Real-time analytics
        - IoT applications
        - Mobile apps
        - Catalogs with variable attributes

4. ## **MongoDB Data Types**
    | Type | Description | Example |
    |------|-------------|---------|
    | String | UTF-8 text | "hello" |
    | Number | Integers/doubles | 42, 3.14 |
    | Boolean | true/false | true |
    | Null | Empty value | null |
    | Date | Timestamp | ISODate(...) |
    | Array | Ordered lists | [1,2,3] |
    | Object | Embedded documents | {x:1} |
    | Binary | Non-text data | BinData(...) |
    | ObjectId | Unique ID | ObjectId(...) |

5. ## **CRUD Operations**
    ### **Create**
    - insertOne({name:"John"})
    - insertMany([{...}, {...}])

    ### **Read** 
    - find({status:"active"})
    - find().limit(10).sort({date:-1})

    ### **Update**
    - updateOne({_id:1}, {$set:{status:"inactive"}})
    - updateMany({age:{$lt:18}}, {$inc:{score:5}})

    ### **Delete**
    - deleteOne({_id:123})
    - deleteMany({expired:true})

6. ## **Key Features**
    - **Indexing:** *15+ index types (TTL, geospatial, etc.)*
    - **Aggregation:** *Pipeline for complex analytics*
    - **Replication:** *High availability via replica sets*
    - **Sharding:** *Automatic data partitioning*
    - **GridFS:** *Large file storage system*

7. ## **Mongo Shell**
    - Interactive JavaScript interface
    - Supports all MongoDB commands
    - Access via `mongo` command
    - Features:
        - Tab completion
        - Command history
        - JS expression evaluation

8. ## **MongoDB Structure**
    ### **Databases**
    - Logical containers for collections
    - Special databases:
        - admin: Authentication
        - local: Replica set data
        - config: Sharding metadata

    ### **Collections**
    - Group of documents
    - No schema enforcement
    - Maximum size: 64TB (with WiredTiger)

    ### **Documents**
    - BSON format (Binary JSON)
    - Max size: 16MB
    - Field ordering preserved
    - _id field always required

9. ## **$set Modifier**
    - Updates fields if they exist
    - Creates fields if they don't
    - Example:
        ```mongo
        updateOne(
            {_id:1}, 
            {$set:{last_login: new Date()}}
        )
        ```

10. ## **Sharding Process**
    1. **Shard Key** *selection (e.g., user_id)*
    2. **Chunks** *creation (64MB default)*
    3. **Balancer** *redistributes chunks*
    4. **Query Router** *(mongos) directs requests*

11. ## **Indexing**
    - **Types:**
        - Single field
        - Compound
        - Multikey (arrays)
        - Hashed
        - Text
    - **Properties:**
        - Unique
        - Sparse
        - TTL
        - Partial

12. ## **Transactions**
    - Multi-document ACID compliance
    - Sessions:
        ```ts
        const session = db.getMongo().startSession()
        session.startTransaction()
        try {
            // operations
            session.commitTransaction()
        } catch {
            session.abortTransaction()
        }
        ```

13. ## **Backup Utilities**
    | Tool | Purpose |
    |------|---------|
    | mongodump | Binary backup |
    | mongorestore | Binary restore |
    | mongoexport | JSON/CSV export |
    | mongoimport | JSON/CSV import |
    | bsondump | BSON to JSON |

14. ## **MongoDB: BASE vs ACID**
    *MongoDB follows **BASE** principles rather than strict ACID (except for multi-document transactions)*

    **BASE Characteristics:**
    - **Basically Available:** *System guarantees availability even during failures*
    - **Soft State:** *Database state may change over time (eventual consistency)*
    - **Eventual Consistency:** *Data will become consistent over time*

    **ACID Support in MongoDB:**
    - **Single-Document Operations:** *Always ACID compliant*
    - **Multi-Document Transactions:** *ACID compliant (v4.0+)*
        - Requires replica sets
        - Maximum transaction runtime: 60s default

    **When MongoDB Chooses BASE:**
    - Horizontal scaling (sharding)
    - High write throughput
    - Distributed systems where immediate consistency isn't critical