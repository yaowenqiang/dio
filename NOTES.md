## Distributed Consensus: Paxos

+ Paxos
+ Raft: like Paxos, but understandable
+ Blockchain: like Paxos, but when people are lying to you

Paxos Uses:

+ Lightweight transactions in cassandra
  + INSERT  ... IF NOT EXISTS
+ Clustrix transactions (commercial product)
+ BigTable's Chubby lock manager
+ Master election

## Distributed Transactions

> starbucks does not use two-phase commit

ACID Transactions

+ Atomic
+ Consistent
+ Isolated
+ Durable

> write-off(注销)
> compensate(补偿)

# Consistent Hashing


> R + W > N

> N is the number of replicas
> R is the number of replicas agree to read
> W is the number of replicas success to write


## When to use Cassandra?

+ Scale
+ Transactional data
+ Always On


## Hadoop

+ MapReduce API
+ MapReduce job management
+ Distributed Filesystem(HDFS)
+ Enormous ecosystem

### HDFS

+ Files and directories
+ Metadata managed by a replicated master
+ Files stored in large, immutable, replicated blocks


### Real-World Hadoop

+ Cloudera, Hortonworks, MapR
+ Nobody write map, reduce functions
+ Hive(SQL-Like interface)
+ Intergration with BI front-ends

### When to Use Hadoop?

+ Data volume is large
+ Data velocity is low
+ Lagency SLAs are not aggressive

## Spark

+ Scatter/gather paradigm(similar to MapReduce)
+ More general data models(RDDs)
+ More general programming model(transform/action)
+ Storage agnostic

### What's an RDD?

+ Bigger than a computer
+ Rea from an input source
+ Output of a pure function
+ Immutable
+ Typed
+ Ordered
+ Lazily e evaluated
+ Partitioned
+ Collection of things

## Storm

> designed at twitter

### Storm Goals

+ Stream data processing
+ Friendlier programming model than message-passing
+ At-least-once processing semantics
+ Horizontal scalability, fault tolerance
+ Fast answers on massive scale data

### Programming Model

+ Stream: a sequence of tuples(probably lots)
+ Spout(水龙头): a source of streams
+ Bolt(螺栓,处理单元): applies a function an input stream, produce one ore more output streams
+ Topology: a graph of spouts, and bolts, a "Job" that runs indefinitely


### Architecture

+ Nimbus - central coordinator of jobs
+ zookeeper
+ Supervisor - a node that performs processing
+ Task: a thread of bolt or sprout execution
+ Worker: a JVM process where a topology executes

### Stream Grouping(Partition)

+ Assign tuples to tasks through a consistent-hashing-like mechanism
+ Configurable
  + Shuffle Grouping: random assignment
  + Fields Grouping: mod hash of subset of tuple fields
  + All Grouping: send to every tasks


## Synchronization

## Lambda architecture


+ System input is an event stream
+ Events are immutable!
+ Batch and stream processing are functional

> http://nathanmarz.com/blog/how-to-beat-the-cap-theorem.html


## Sharding


## Messaging introduction

+ Means of loosely coupling subsystems
+ messages are consumed by subscribers
+ Created by one ore more producers
+ Organized into topics
+ Processed by brokers
+ Usually persistent over the short term

### Messaging Problems

+ What if a topic get too big for one computer?
+ What if one computer is not reliable enough?
+ How strongly can be guarantee delivery?

## Kafka

+ Distributed messagequeue
+ Horizontally scalable, fault-tolerant
+ Durable
+ Fast
  + 100s MB reads and writes/second
  + Thousands of clients
  + per broker!
+ Widely deployed
+ JVM based(written in Scala)
+ Native Java and Scala APIs(Akka option)
+ Binary wire protocol
+ Start at three nodes and grow!


### Definitions

+ Message: an immutable  array of bytes
+ Topic: a feed of feeds
+ Producer: a process that publishes messages to a topic
+ Consumer: a single-threaded process that subscribes to a topic
+ Broker: one of the servers that comprises a cluster


### Partitioning

+ A scaling strategy
+ Done in teh Producer by a pluggable class and a message key
+ Order is maintained in-partition only

### ZooKeeper

+ Required part of Kafka architecture
+ Producers use it to find partitions and replication information
+ Consumers use it to track current index

### Replication

+ Brokers can fail
+ Configurable in-sync replica sets
+ One leader, n-1 followers
+ Only the leader communicates with clients
+ When the leader failed, a new leader is elected


## Vector Clocks

+ A means of proving sequence
+ Not a means of telling the time
+ We are concurrently modifying one value
+ Every actor has an ID
+ Every actor tracks a sequence number
+ Consider Basho's famous example
+ Can not be wrong(LWW(Last Write Win) can)
+ Push complexity into the client

> [why vector clocks are easy](http://basho.com/why-vector-clocks-are-easy/)
> [why cassandra doesn't need vector clocks](http://www.datastax.com/dev/blog/why-cassandra-doesn't-need-vector-clocks)




