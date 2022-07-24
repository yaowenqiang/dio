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
