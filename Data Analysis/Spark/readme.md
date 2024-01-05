
# MapReduce Disadvantages and Spark Advantages

## MapReduce Disadvantages
- **More complex, multi-pass analytics**
- **More interactive ad-hoc queries**
- **More real-time streaming processing**
- **Problems in MapReduce**
  - Slow due to replication, serialization on disk I/O

## Complement in Spark
- **10-100x faster than network and disk due to in-memory systems**
- **Memory access is much faster than disk**
- **Well suited to iterative and machine learning algorithms**
- **Spark is also able to make use of HDFS**
  - Spark runs on HDFS through YARN, combining the benefits of both HDFS and Spark.

## Spark RDD (Resilient Distributed Datasets)
- Distributed collections of objects that can be cached in memory across the cluster.
- Manipulated through parallel operators.
- Automatically recomputed on failure.
- Immutable (read-only).
- Partitioned collections of records.
- Can contain any type of Python, Java, or Scala.
  - Note: When running RDD with Python, it may be slower compared to other languages. Hence, Dataset or Dataframe is recommended.

## Spark Functions
- **Transformations:** Operations on RDDs that return a new RDD.
  - Map, filter, sort, join, distinct
- **Actions:** Return a final value or write data to an external storage system.
  - Count, reduce, collect

## Lazy Evaluation
- Means when calling a transformation on an RDD, the operation is not immediately performed.
- Directed Acyclic Graph (DAG) is utilized for optimized execution.

## Spark Components
- Spark depends on a cluster manager to launch executors and the driver.
- The manager is a pluggable component in Spark.

