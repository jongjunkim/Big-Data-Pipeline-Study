
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

# Thoughts on Implementing Spark RDD

When implementing Spark RDD, several considerations come to mind:

- **Less Intuitive than Spark SQL or DataFrame:**
  - RDDs are less intuitive compared to Spark SQL or DataFrame, making them less straightforward to work with.

- **Low-level and Some Drawbacks:**
  - RDDs are low-level and suffer from certain issues.
  - They express "how" a solution is achieved rather than "what."

- **Lack of Optimization:**
  - RDDs cannot be optimized as effectively as Spark DataFrames, especially due to the absence of the Catalyst optimizer.

- **Performance in Non-JVM Languages:**
  - RDDs may perform slowly in non-JVM languages like Python.

## Abstraction Level

- **Managing Complexity:**
  - Abstraction levels help manage complexity in programming.
  - Higher abstraction levels allow simpler commands to perform more tasks.

## High-level Interface vs Low-level Interface

- **Low-level API:**
  - Provides more detailed and less abstract functions, offering greater control to manipulate functions.

- **High-level API:**
  - Is more generic and simpler.

## Type Safety

- **Type Safety:**
  - RDDs and Datasets provide type safety, validating types during compilation and throwing errors for incorrect assignments.

## Spark SQL

- **Beyond SQL:**
  - Spark SQL is not limited to SQL; it goes beyond handling structured data.

- **Performance Advantage:**
  - Spark SQL outperforms traditional SQL as it leverages multiple nodes for processing compared to the single-core execution of SQL.

- **Benefits:**
  - Writing less code.
  - Reading less data (fetching only necessary data).
  - Leveraging its own optimizer to handle complex tasks.

# RDD vs DataFrame Code

## RDD:

```python
Data = sc.textFile(…).split(“\t”)
Data.map(lambda x: (x[0], [int(x[1]), 1])) \
    .reduceByKey(lambda x, y: [x[0] + y[0], x[1] + y[1]]) \
    .map(lambda x: [x[0], x[1][0] / x[1][1]]) \
    .collect()
```
## Dataframe:
```python
sqlCtx.table(“people”).groupby(“name”).agg(“name, avg(“age)).collect()
```
- **따라서 RDD보다 DataFrame을 쓰는 이유는 Python으로 코딩했을 때 성능이 떨어지지 않고 코드도 좀더 간결해지고 직관적이게 되어서**

 ## Read Less Data**
- **Spark SQL can help you read less data automatically**
    -	Converting to more efficient formats
    -	Using partitioning 
    -	Partitioning 을 통해서 필요한 데이터만 가져오는거
      - 예를들어 년도별로 parition하면 필요한 연도만 가져오는거
    -	Pushing predicts into storage systems
## DataFrame Queries
  -	Catalyst Optimizer
    - Constant Folding (Complier 최적화)
      -	Runtime에서 처리하지 않고 Complier에서 상수값들을 미리 처리
  -	Predicate Pushdown
    -	(조건절을 미리 계산, 필요한 데이터만 가져오는거)
    -	Select col from data where ~~ 했을때 select col을 먼저하는게 아니라 where 절을 통해서 데이터를 골라내고 select을 하기 때문에 더 빠르다  
  -	Column Pruning 
    -	연산에 필요한  column만 읽는거


 
