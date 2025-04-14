### Steps:
    - Functional Requirements
    
    - Non-functional Requirements (scaling + special cases)
    
    - Apis/Data-Flow
    
    - High Level Design ( serves Function requirements)
    
    - Deep Dive ( serves Non-Function requirements)


How to Approach System Design Question in an Interview:
Templates:

![image](https://github.com/user-attachments/assets/5a27be94-49da-4f2d-ae8c-107f7c50e8ca) 
https://www.hellointerview.com/learn/system-design/in-a-hurry/delivery
https://leetcode.com/discuss/interview-question/system-design/5073436/System-Design-Template


### Functional Requirement: [ pick 2 or 3 most important features]
    - What part of the system to design?
    - What are the steps of the Request flow from user to the db and Respose from the DB to the user.
    - User related: who are the users/ how they will be served
    - User Scale: Daily Actiuve User (DAU), Lar sclae Data reaqd/write?
    - basic algorithm to serve the problem

    -- [ Out of Scope ]
  
### Non-functional Requirements (scaling + special cases): [ pick 2 or 3 cases]
    - Microservice Architecture to handle scaling in different traffic, read, writes, logic, etc. 
    - CAP Theorem : Strong Consistency vs (Availability and Eventual Consistency)  *** Different parts of the system might have different Consistency and Availability 
    - Read/ Write Ratio: read heavy or write heavy system. Must choose different components -database/caching layer/broker/sharding based on that
    - Low Latecy: low latency for real time updates - messaging app, uber driver location updates, search through Database, etc
    - Popular Event/ Peak hour/ Celebrity user/ Hot server/ Hot shard/ etc
    - Idempotency (Consider single event when multiple events are requested: multiple clicks to do transaction, ad-click, checkout button click, etc)
    - estimation:
        1) read throughput, write throughput (incoming read/write request per second)
        2) number of backend servers needed to handle requests request
        3) storage needed to write all data


    - Fault Tolerance( if server, database shard, network goes down)
    - if user goes offline


    - push vs pull mechanism to fan-out data
    - Polling, Long Lolling (not-persistent)
    - Websocket (persistent connections, bi-directional)
    - Server Sent Event (persistent connections)
    - WebRtc (peer to peer connections)


    - Message Queue to receive messages asynchronosly: kafka, amazon SQS, rabbit MQ
    - Event Streaming for logging system, event stream handling, etc: Kafka, Kinesis, etc
    - pub/sub
    - CDC (Change Data Capture) to forward the event of any change of data in the DB. (primary DB -> Elastic Search)


    - Analytics aggregator to aggregate data in real-time: apache Spark, Flink (this system receives data from brokers-Kafka )
    - Batch processing to aggregate data, process writes in batch using chron job or scheduler in every n (5, 10, 15, 60 minutes, 1 day, 1 week, etc) minutes (needs input file to batch process and generates output file)
    - Loggin, Monitoring, health check

    
    - System Security / DDoS attack / running user code, query in secured environment
    - Rate limiting to save servers, databases, detect spammers, etc: fixed time window (minute 1, minute 2, etc), sliding window, etc
    - Encryption of user personal data/location/credit card info etc.

    
    - Concurrency in request handling to maintain Consistency:
        1) in server level(consistency to handle to book a ticket by servers)
        2) in each device level (issue in multithreading operation in same exact time ex: unique key generations by same device)
    - Locking Meckanism
        1) redis Lock with TTL
        2) SQL DB row lock during read-write
        3) Dynamoc DB TTL for rows


    - SQL/ No-SQL/ ACID property/ Availability vs Consistency / Read Heavy system/ write heavy system/ What kind of indexing needed (geo hash, full text inverted index)/ Row Locking
    - Data Partitioning/ Sharding and replication.
    - Caching for best user experience: if data is static then caching is always helpful (LRU)
    - CDN
    - Encoding/decoding data
    - compress files specially media files(images, videos)
    - upload huge files by chunking (resumeable uploads)
    - create file with different resolution to serve users in different scenarios(poor network, mobile network, low bandwith, etc)
    - deduplication of data
    

    - Load balancing: Zoo Keeper - smart load balancer, uses heart bit mechanism to check if the machines are running fine, etc
    - Consistent Hashing (best in any situation: stateful, stateless, adding/removing servers, etc)
    - Round Robin (Stateless system)
    - Hash Based (Stateful): poor in handling changes (add/remove servers)
    

    -- [ Out of Scope ]
    

            
[Designing Data Intensive Application](http://xfido.com/pdf/designing-data-intensive-applications.pdf)       
[mit course link](http://nil.csail.mit.edu/6.824/2018/schedule.html?fbclid=IwAR2R-VKSo2hGhDqVE7veo7SWoRK62h3eKrOxliz6yRgSSrhbsuBzA1bYn7o)       
[DDIA youtube](https://www.youtube.com/watch?v=PdtlXdse7pw&list=PL4KdJM8LzAMecwInbBK5GJ3Anz-ts75RQ)         
[martin kleppmann series](https://www.youtube.com/playlist?list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB)             
[hbase table desing choices](https://github.com/siam1251/cmds/blob/master/.images/hbase_design.pdf)        
[hbase design examples](https://dzone.com/articles/understanding-hbase-and-bigtab)           

idempotent             
[security](#security)      

<a name="security">   
 
### Conversion
  |number| memory| unit|
  |------|-------|------|
  |1 Million |  1 MegaByte | 10^6|
  |1 Billion |  1 GigaByte | 10^9|
  |1 Trillion| 1 Terabyte| 10^12|
  |1 Quadrillion| 1 Petabyte| 10^15|
### Security   
 TLS handshake [link](https://www.cloudflare.com/en-ca/learning/ssl/what-happens-in-a-tls-handshake/#:~:text=A%20TLS%20handshake%20is%20the,and%20agree%20on%20session%20keys.)

Different no-sql database
|database type| example|
|-------|-----|
|Time series| influxDB, prometheus, graphite|
|graph based|Neo4j|
|spatial|quadtree, R tree|
|blob stroe|amazon s3, gcs|
|Document Databases|CouchDB and MongoDB|

Availability

|Avialability| Downtime per year|
|-------|-----|
|90%(one nine)|36 days|
|99%(two nine)|3.6 days|
|99.9%(3 nine)|8.7 hours|
|**99.99% ("four nines")**|	52.60 minutes	|
|**99.999% ("five nines")	|5.26 minutes**|
|99.9999% ("six nines")	|31.56 seconds|
|99.99999% ("seven nines")|	3.16 seconds|

ACID properties
 
|Property| Definition|
|-------|-----|
|Atomicity| either all succeed or all fail|
|Consistency|none of balances go zero;cannot have duplicates ...|
|Isolation| serialization; thread safe; each of the transactions will happen like one by one|
|Durability| guarantees that transactions that have committed will survive permanentl|
 
### Scaling your design (swiss army knife)
 * sharding
 * cacheing
 * indexing columns
 * CDN
 * Geolocation
 * offloading to job queue-cpu/time intensive
 * prefetching-keep reads sequentially
 * batch your writes
 * Reading/writing from workers, replicas
 * blocking as less as possible-consitency
### Scaling your algorithm 


### There are four conditions that are necessary to achieve deadlock:
* Mutual Exclusion - At least one resource must be held in a non-sharable mode; If any other process requests this resource, then that process must wait for the resource to be released.       
* Hold and Wait - A process must be simultaneously holding at least one resource and waiting for at least one resource that is currently being held by some other process.
* No preemption - Once a process is holding a resource ( i.e. once its request has been granted ), then that resource cannot be taken away from that process until the process voluntarily releases it.
* Circular Wait - A set of processes { P0, P1, P2, . . ., PN } must exist such that every P[ i ] is waiting for P[ ( i + 1 ) % ( N + 1 ) ]. ( Note that this condition implies the hold-and-wait condition, but it is easier to deal with the conditions if the four are considered separately. )

|storage| lookup time|
|-------|-----|
|RAM    |100x faster than disk|
|Reading 1 MB from RAM| 250 μs .25 ms|
|Reading 1 MB from SSD| 1,000 μs (1 ms)|
|Transfer 1 MB over Network| 10,000 μs (10 ms)|
|Reading 1MB from HDD|20,000 μs (20 ms)|
|Inter-Continental Round Trip|150,000 μs (150 ms)|

### Capacity estimation   
youtube
|storage| Reads/sec| Writes/sec|Bandwidth|
|-------|----------|------------|--------|
| 1M users| | ||
| 1M users| | ||
| 1M users| | ||
| 1M users| | ||
| 1M users| | ||

### Read/Write Ratio of Different Databases:
https://chatgpt.com/canvas/shared/67b77b9987d88191b49b0fc54c185608
### **Overview**
---
### **Summary Table**

| Database                   | Max Writes/sec          | Max Reads/sec            | Scaling Model                   |
| -------------------------- | ----------------------- | ------------------------ | ------------------------------- |
| **DynamoDB**               | \~1MB/s per partition   | \~3MB/s per partition    | Auto-sharding                   |
| **MySQL/PostgreSQL (RDS)** | 3K-5K (single instance) | 10K+ (single instance)   | Read replicas                   |
| **Aurora (AWS)**           | \~200K                  | Millions (with replicas) | Read replicas                   |
| **MongoDB**                | 10K-50K (single node)   | \~100K+                  | Sharding                        |
| **Cassandra**              | 100K+ per node          | 50K+ per node            | Linear scalability              |
| **Redis**                  | 500K+                   | 1M-2M+                   | In-memory, clustered            |
| **Spanner**                | 10K per node            | 100K per node            | Strongly consistent, horizontal |

---
This report provides a comparative analysis of the read and write performance of various databases, including SQL and NoSQL solutions. It highlights their capabilities in handling transactions, scalability, and real-time processing.

### **1. Amazon DynamoDB (NoSQL)**

**Write Performance:**

- Provisioned mode: Up to 1,000 WCU per partition (\~1MB/s)
- On-demand mode: Scales automatically but limited to 1MB/s per partition

**Read Performance:**

- Strongly consistent: 1 RCU = 4KB read
- Eventually consistent: 1 RCU = 8KB read
- Max per partition: \~3,000 RCU (\~3MB/s)

**Scaling:** Horizontal, adds partitions dynamically

---

### **2. Amazon RDS (SQL - MySQL/PostgreSQL)**

**Write Performance:**

- Single-instance: 3,000-5,000 writes/sec (depends on IOPS & instance size)
- Aurora (AWS scalable SQL DB): Up to 200,000 writes/sec

**Read Performance:**

- Single-instance: \~10,000 reads/sec
- Aurora Read Replicas: Scale to millions of reads/sec

**Scaling:** Read replicas for read scaling, limited write scalability

---

### **3. MongoDB (NoSQL - Document DB)**

**Write Performance:**

- Single node: 10,000-50,000 writes/sec (depends on indexing and hardware)
- Sharded cluster: Scales to millions of writes/sec

**Read Performance:**

- Single node: \~100,000 reads/sec
- Read replicas: Scale reads horizontally to millions/sec

**Scaling:** Horizontal via sharding and replication

---

### **4. Apache Cassandra (NoSQL - Wide Column Store)**

**Write Performance:**

- Designed for high writes (\~100,000+ writes/sec per node)
- Scales linearly with more nodes (e.g., 10 nodes → 1M+ writes/sec)

**Read Performance:**

- Single node: \~50,000+ reads/sec
- Requires tuning for read-heavy workloads

**Scaling:** Fully distributed, linear scalability (optimized for write-heavy applications)

---

### **5. Redis (In-Memory Key-Value Store)**

**Write Performance:**

- Single instance: \~500,000+ writes/sec
- Cluster mode: Scales to millions of writes/sec

**Read Performance:**

- Single instance: \~1-2 million reads/sec
- Read replicas enhance scalability

**Scaling:** Horizontal scaling via sharding & clustering

---

### **6. Google Spanner (Distributed SQL)**

**Write Performance:**

- \~10,000 writes/sec per node
- Strong consistency with horizontal scaling

**Read Performance:**

- \~100,000 reads/sec per node
- Multi-region replication ensures strong consistency

**Scaling:** True horizontal scaling while maintaining ACID compliance

### **Conclusion**

The choice of database depends on the specific use case:

- **For high write workloads**, **Cassandra** or **DynamoDB** are ideal.
- **For high read performance**, **Redis** or **MongoDB** provide excellent scalability.
- **For SQL workloads requiring strong consistency**, **Google Spanner** or **Aurora** are top choices.

Proper database selection ensures optimal application performance, cost efficiency, and reliability.

---

**Prepared by:** Wali Bhuiyan




### BASE (nosql database)     
* Basically available
* Soft state
* eventually consistent

[Cassandra and mongoDB & CAP theorem](https://www.ibm.com/cloud/learn/cap-theorem)    
* Cassandra uses masterless architecture (partition in a ring, consistent hashing) and use gossip protocol to communicate 
* 
ACL  (authorized client list)  
[JWT (JSON Web Token) and OpenID Connect (OIDC, based auth2)](https://www.youtube.com/watch?v=ZjPF8yZ83Wo)       
* openID activates authn
  
| Databases | features |consistency|    example       |
| ------ | ------ |-----|------|         
|DynamoDB, amazon| kv store, key–value and document data structures, OLTP (Online Transactional Processing) | typically used as eventually consistent|  The partition key + the optional sort key form the primary key of the table, so they must be unique.  let's say I'm storing logging data for several applications. My partition key could be the Application Name, and the sort key the timestamp of the log. This allows me to query all logs of a particular application of the last hour in 1 query, using the BEGINS WITH operator, or even all the logs of last Wednesday for an application, by using the BETWEEN operator| 
|amazon s3| large object store database, key-value base|--|  |
|cassandra,hbase, big table| wide column store, key-value, use row key, Online analytical processing (OLAP)| typically used as eventually consistent| [hbase](https://hbase.apache.org/book.html#datamodel) has column family then colum name, usually one hfile per column family, row_key, column-family[c1, c2] are sorted based on row_key. searching based on row_key is fast (get operation) [link](https://www.linkedin.com/pulse/secondary-indexing-hbase-tale-how-screw-up-simple-idea-michael-segel/) but with other keys it's slow (scan operation), you may create another  table with another row_key for faster search|
|sql| structured storage, used in any transaction| consistent, ACID| |
|Document Databases,CouchDB and MongoDB  | data is stored in documents (instead of rows and columns in a table)| and these documents are grouped together in collections Each document can have an entirely different structure | Document databases include the CouchDB and MongoDB|
* Transaction Model [stack overflow](https://stackoverflow.com/a/29381684)
```
Neither Amazon DynamoDB nor Apache HBase support multi-item/cross-row or crosstable transactions due to performance considerations.
However, both databases provide batch operations for reading and writing 
multiple items/rows across multiple tables with no transaction guarantees.
```
```
For workloads that need high update rates to perform data aggregations or maintain counters, Apache HBase is a good choice.
This is because Apache HBase supports a multi-version concurrency control mechanism, which contributes to its strongly consistent reads and writes.
Amazon DynamoDB gives you the flexibility to specify whether you want your read request to be eventually consistent or strongly
consistent depending on your specific workload. reached within a second.
```
### spark vs hadoop   
Hadoop uses persistent data storage for map/reduce operation while spark use in memory (RDD-resilient distributed datasets)
* spark is super fast (realtime) vs map/reduce was never meant for realtime
* hadoop uses yarn (resource manager), pig, hive, sqoop
* both are fault tolerant 
* For realtime use spark otherwise hadoop 
### CAP theorem       
Consistency: Every read receives the most recent write or an error           
Availability: Every request receives a (non-error) response, without the guarantee that it contains the most recent write            
Partition tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes           

http long polling vs web sockets          

[system desing primer](https://github.com/donnemartin/system-design-primer#content-delivery-network)                
[comparison](https://www.prisma.io/dataguide/intro/comparing-database-types)           
[column family vs row](https://dataschool.com/data-modeling-101/row-vs-column-oriented-databases/)                   
[ovserable pattern vs pub-sub pattern](https://medium.com/easyread/difference-between-pub-sub-pattern-and-observable-pattern-d5ae3d81e6ce)           

### What’s the Difference Between Columnar Database (redshift) vs. Wide-column Database (hbase, cassandra)?          
A Columnar data store will store each column separately on disk. A Wide-column database is a type of columnar database that supports a column family stored together on disk, not just a single column.

[kabir vai](https://docs.google.com/document/d/1-Fv2nih7LZ9EJC-E_f_vMvkOsaAiadXWPXP--7EEd-s/edit)       
### Sabir vai links   
http://highscalability.com/amazon-architecture?fbclid=IwAR3oPXtzLW7mVDkHly6sAeGFSOTNb1RN43c8KL3H83XjJ2b459D4TnX5T_U                 
http://highscalability.com/google-architecture?fbclid=IwAR2mT91b27hE7xEug6x5b3KAathp8YQQhEMwmghhBapTnk5kDiJpPwYDhjY              
http://highscalability.com/youtube-architecture?fbclid=IwAR3CGL4dxgtRCmusUiipUZGqgKrFVs1JROJBbwV3xiQYpnEe0x-CTBURiMU                     
http://highscalability.com/blog/2016/6/27/how-facebook-live-streams-to-800000-simultaneous-viewers.html                              
http://highscalability.com/scaling-twitter-making-twitter-10000-percent-faster                             
http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html                             
http://highscalability.com/blog/2015/9/14/how-uber-scales-their-real-time-market-platform.html
http://highscalability.com/blog/2011/12/19/how-twitter-stores-250-million-tweets-a-day-using-mysql.html
https://instagram-engineering.com/what-powers-instagram-hundreds-of-instances-dozens-of-technologies-adf2e22da2ad
https://www.youtube.com/watch?v=PE4gwstWhmc

##### column family is not column oriented database(hbase is column family where redshift is column oriented, redshift is RDMS database but column oriented)

### Which part I should focus to implement?

### Requirement 
  * What does the system do? (web crawler)
  * I want to make sure that we are at the same page. Can you please give me an example?
  * Which part I should focus to implement?
  * which parts should I implement, newsfeed generation or user posts?
  * Decide whether it's a algorithmic question or system design? If you are still confused ask interviewer.
  * Who are the users of this system? (important!)
  * Will this system server globally? (cluster)
  * what will be the number of users at a time? 5B, dayily 2B, 
  * capacity estimation: Vehicle travel time from source to destination is latency.       
       Types of Roadways are bandwidth.
       Number of Vehicles traveling is throughput.        
       Latency (difference between post and response in seconds)            
  * what many users will post at a second?
  * what will be post size? 100 KByte * 5 Posts * 2B = 1000 Billon KB = 10^9*10^3
  * make your system latency p99.99 ? how?
#### Calculation:
 
  * convert 2B/(24*60*60) per second
  * Data incoming and data outgoint ?
  * characters
  * How many servers do I need, one server can serve 1 Million uses so ....

### Federation (or functional partitioning [link](https://github.com/donnemartin/system-design-primer#reverse-proxy-web-server))          
splits up databases by function. For example, instead of a single, monolithic database, you could have three databases: forums, users, and products, resulting in less read and write traffic to each database and therefore less replication lag
### Database Scaling 
  * sharding or partition
  * sharding is need when lots of write otherwise Replication would work  
  * vertical sharding, many tables, tweet tabe, user table
  * horizontal sharding, tweet table will be sharded into multiple machines
  * horizontal sharding, based on user id (mod id by total number of machines to redirect multiple machines) 
  * replication (no single point of failure)
  
Client  -> Gateway server -> load balancer --> clusters --> database

### Message Brokers / asynchronous communication / (pub/sub pattern)       
   * RabbitMQ (default point to point channel/ but can be configured as pub/sub)
   * Redis
   * Kafka (pub/sub)

### Batch Processing
    * Apache Hadoop (uses MapReduce to split large datasets across distributed clusters, process data in parallel and aggregate the results)
    * AWS Batch

### Batch vs Stream Processing - What's the Difference? When to use what?
[Batch vs Stream Processing](https://www.neovasolutions.com/2020/07/20/apache-kafka-a-quick-overview/)
    
    

### Bloom Filters      
 * n hash functions map to k positions             
 * each hash will give one value from between 0.. k value and we will set that position to 1            
 #### Write-ahead logging       
* write-ahead logging (WAL) is a family of techniques for providing atomicity and durability (two of the ACID properties) in database systems.
* The changes are first recorded in the log, which must be written to stable storage, before the changes are written to the database.       
 
### Caching software (CDN for video cache, asset server )           
* Redis (S3 for object or video cache, asset server)  
* Memcache
* Casandra
### apache kafka (data driven architecture)  must visit [link](https://www.youtube.com/watch?v=06iRM1Ghr1k)     
   * kafka topics are same as a database (using ksql)  

### Write-ahead logging         
### Seperating metadata and data         
### Cassandra (low latency circular database)              
### stream api using kafka                     
### lambda architecture uses kafka (for analyzing data) [link](https://www.youtube.com/watch?v=BO761Fj6HH8)           
### kafka messaging (broker/topic)    
### Elasticsearch 
   * Application search —- For applications that rely heavily on a search platform for the access, retrieval, and reporting of data.
   * Website search —- Websites which store a lot of content find Elasticsearch a very useful tool for effective and accurate searches. It’s no surprise that Elasticsearch is steadily gaining ground in the site search domain sphere.
## Terms   

### relational vs nosql [link](https://integrant.com/blog/when-to-use-sql-vs-nosql)  
   #### SQL      
   * Scaling out with SQL is possible, but requires extensive effort (partitioning, sharding, clustering, etc.) and cost. 
   *  You can run SQL on Azure, for example, but you will be limited in your ability to scale.
   *  If you’re working with a multi-tenant application, you will need sharding and partitioning (separating very large databases into smaller, faster, more easily managed parts). To achieve this with SQL databases requires additional coding. NoSQL databases (such as CosmosDB) includes these features out-of-box.
   #### NoSQL  
   *  NoSQL engines are designed to scale out and leverage cloud computing. When scaling out or horizontally we are adding resources to a single node (a computer or server). We can have one database working on multiple nodes. Scaling out (or back in) means we can easily add and remove nodes. This makes NoSQL a perfect match for the cloud. Because it can scale out, you will be maximizing the scalability benefits of the cloud. 
   *  NoSQL vs. SQL Speed (of your team) The ability to store huge amounts of data in a flexible way makes NoSQL faster to develop.
   *
  #### SQL vs NOSQL
| SQL | NOSQL |
| ------ | ------ |
|   Data uses schema     |     Schema-less    |
|   Relations     |    No (very few) relations     |
|   Data is distributed across multiple table and normalized     |     Data is typicall merged/ nested in a few collections, no join operation is needed as data is self sufficient    |
|  Horizontal scaling is difficult/impossible; vertical scaling is possible      |  Both horizontal and vertical scaling is easy to implement       |
|    Limitations for lots of (thousands) read and write queries per second    |     Great performance for mass(simple) read & write |

### Data denormalization    
   * Denormalization is a strategy used on a previously-normalized database to increase performance. [link](https://en.wikipedia.org/wiki/Denormalization)     
### Kafka           
   * [link](https://www.neovasolutions.com/2020/07/20/apache-kafka-a-quick-overview/)
   * kafka clusters
   * zookeaper is used for monitoring kafka clusters 
   * Kafka is used for data streaming (pub/sub pattern)
   
   ```
       producer1 producer2 producer3
        |            |         |
    -----------kafka clusters------------------
       topic1            topic2           topic3
       ------            ------           ------
       partition1       partition1
       partition2       partition2
       partition3
    --------------------------------------------
        |                 |                 |
     consumer1         consumer2        consummer3
   ```
   
### Zookeeper
   * heartbeat to check if other servers are alive
   * Zookeeper replicates all your data to every node and lets clients watch the data for changes. Changes are sent very quickly (within a bounded amount of time) to clients. You can also create "ephemeral nodes", which are deleted within a specified time if a client disconnects.
   * cluster-wide locks for your services  
   * Finally, the maximum size of a "file" (znode) in Zookeeper is 1MB, but typically they'll be single strings.
   * Basically, ZooKeeper (and Curator, which is built on it) helps in handling the mechanics of clustering -- heartbeats, distributing updates/configuration, distributed locks, etc

### Redis [link](https://redis.io/topics/introduction)   
  * Transactions
  * Pub/Sub
  * Lua scripting
  * Keys with a limited time-to-live
  * LRU eviction of keys
  * Automatic failover
### Fanout/Fanin
### NGINX (en·juh-neks)    
Load balancing software  
### Clusters vs bucket
### lazy vs eager
### persistent data storage
### indexing sql table column
### S3 vs GCS (google cloud storage)  
### Load Balancer  
### Microservice   
### Peer to Peer connection  or download for machines in a same cluster  
### HFDS ( Hadoop Distributed File System)
### apache kafka vs apache spark 

![alt text](./.images/system_diagram.png "System Diagram Template")
  <br/><br/>
![alt text](./.images/system_codingcamp.png "System Diagram Template2")
   <br/><br/>
![alt text](./.images/system_primer2.png "System Diagram Template2")
   <br/><br/>
![alt text](./.images/system_primer1.png "System Diagram Template2")
  
  
