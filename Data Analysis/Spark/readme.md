
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

# Spark DataFrame Motivation

Spark DataFrames serve as a powerful abstraction for simplifying distributed big data processing. The motivation behind using Spark DataFrames includes:

- **Intuitive Coding:** Spark DataFrames allow for intuitive coding, making it easier for developers to write efficient code.
- **Extension of Spark RDD API:** An extension of the Spark Resilient Distributed Dataset (RDD) API, Spark DataFrames are optimized for writing code more efficiently while retaining power.
- **Spark SQL Module:** Programming abstraction is provided in the Spark SQL module, offering additional capabilities for structured data processing.

## RDD (Resilient Distributed Dataset)

**Characteristics:**
- RDD is a collection of distributed and immutable data elements.
- Developers have low-level API control for explicit distribution and manipulation of data.
- Lack of type safety, with errors discovered at runtime.

**Use Cases:**
- When low-level control is required.
- Processing unstructured or undefined-structure data.
- Handling complex data processing and transformations where user control is necessary.

## DataFrame

**Characteristics:**
- DataFrame is a logical distributed collection for processing structured data.
- Utilizes Catalyst optimizer to optimize physical execution plans efficiently.
- Provides a query language similar to SQL for easy data manipulation.

**Use Cases:**
- Processing structured data effectively.
- When performance optimization and efficient execution plans are required.
- When dealing with data using SQL-like syntax.

## Dataset

**Characteristics:**
- Dataset is a distributed collection with type safety for processing structured data.
- Limited functionality in Python, primarily available in Java and Scala.
- Extends DataFrame features to provide type safety.

**Use Cases:**
- When type safety is crucial, and development is in Java or Scala.
- Extending DataFrame functionality while ensuring type safety.



