# Database Choices

Atomicity - Each transaction is all or nothing  
Consistency - Any transaction will bring the database from one valid state to another  
Isolation - Executing transactions concurrently has the same results as if the transactions were executed serially  
Durability - Once a transaction has been committed, it will remain so  

3 Main Questions:
- How is data represented?
- How is data stored?
- How is data transported?

## How is Data Represented?
## How is Data Transported?
## How is Data Stored?
### Vertical vs. Horizontal Scaling
**Vertical Scaling** = This is equivalent to scaling up by improving RAM, CPU, and Disk Space. 
Pros:  
- It is very easy to implement and is convenient to use
- Good for latency sensitive systems as there is no need for communication between machines
- Very consistent. No need to apply distributed algorithms to ensure ACID compliance
- Lots of joins are better on vertical scaled database
Cons:
- Expensive
- Physical limit to how much hardware you can scale to
- While system is upgraded there is downtime
- Single point of failure
- Bad for parallel work
<br>

**Horizontal Scaling** = Scale outwards by distributing the load between multiple machines. This can be done via Replication or Partitioning (Sharding).
Replication = Copying the same data to multiple servers. Most of the time one machine handles writes and a lot of machines handle reads. When the writing database fails then the read database promotes up. There is slight delay between syncing the read and write machines.
Sharding = Split data across servers via partitioning key. This is very useful if users are coming from different parts of the world as the shards can be closer to those users. The # of shards depends on what queries are being used, the growth rate of incoming data, and etc. Sharding is traditionally much easier for NoSQL DBs than SQL DBs.

Pros:
- Cheaper than vertical scaling
- Unlimited Growth
- Fault Tolerance
- Great for Parallel Work
- Lower DB downtime
Cons:
- Harder to Implement
- By CAP theorem, hard to guarantee consistency
- Bad for joining data across machines
- Has slight inconsistency when syncing databases for replication
- Multi Shard Transactions are very difficult to handle

### Relational vs NoSQL Database vs. Others
**Relational** = stores data in tables with columns and rows
<br>
Pros:
- Structured Schema
- ACID transactions
- SQL as a language already mature and refined
- Foreign keys and constraints prevent schema from not being followed
- Query Planner and Indexing help queries be very fast
Cons:
- Hard to scale horizontally
- Rigid Schema
- Hard to handle unstructured data like BLOBs, JSON, logs, images
- Expensive at scale
- Transactions are hard on distributed scale

**NoSQL** = stores data in various formats: key-value, document(JSON), and graph
- Key-Value = can support storing varying objects like images, videos, etc. There is no need for table joins, and keys can be sorted.
<br>
Pros:
- Structu
Cons:
-
- Document = Collections of documents act as tables and documents become rows. Each document has an ID, and it is easy to access a field as it is a tree structure. The schemas are also very flexible and Document databases are designed to scale horizontally as collections can be sharded on hashed, range, compound keys. Document sits as a midpoint between the speed of Key-Value but still offering richer queries and strict schema of relational DBs.
Pros:
- Flexible Schema
- Scales well horizontally
- Easy to work with
Cons:
- 
- Graph = stores data as nodes and relationships as edges, and each node/edge can have properties. These are great for queries that require traversing through a graph like friends of a friends of a friend. Typically these are good for applications like recommendation systems and fraud detection where you are attempting to use existing entities to find nearby entities with similar thiings
Pros:
- Relationship Friendly and Driven
- Flexible Schema
Cons:
- Not optimized for heavy aggregation
- Struggles with large datasets and fields
- Not mature as a concept

**Overall**
Pros:
- Designed for horizontal scalability 
- Handles large datasets and high throughput workloads well
- Flexible Schema
- Optimized for writes
- Replication easier than relational
Cons:
- Not fully ACID compliant. Not strongly consistent
- Limited Querying and Transaction
- Data is duplicated often as join's do not really exist

### Caches
**Caching** = a technique used to store frequently accessed data in memory, making subsequent access to that data faster

