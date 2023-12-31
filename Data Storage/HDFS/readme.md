# HDFS (Hadoop Distributed File System) Overview

## Motivation:

The motivation behind HDFS arises from the limitations of traditional file systems when dealing with large datasets. Key motivations include:

1. **Single Drive Read Limitations:**
   - Reading all data from a single drive takes a long time.

2. **Parallel Reading from Multiple Disks:**
   - The solution is to read from multiple disks concurrently to improve data access speed.

3. **Data Scaling Across Multiple Machines:**
   - When a dataset exceeds the storage capacity of a single machine, it becomes necessary to distribute and partition the data across multiple machines.
  
     - 네트워크 베이스로 이루어진 파일 시스템을 통해서 큰 파일들을 저장할 수 있고 읽을 수 있도록 처리한게 HDFS
     - 따라서 네트워크 복잡한 문제들이 발견될수 있지만 그래도 큰 목적은 파일 시스템을 만들 때 데이터의 로스 없이 노드들이 장애가 일어나도 잘 견딜수 있게 만드는 목적


## HDFS Overview:

Hadoop Distributed File System (HDFS) is designed to address the challenges of storing and processing large-scale data. It is a network-based file system that enables the storage and retrieval of massive files across a distributed cluster of machines. The primary goals of HDFS include fault tolerance, scalability, and efficient data processing.

### Data Types Supported:

- Structured Data
- Semi-structured Data (XML, HTML, JSON)
- Unstructured Data

## Design and Concepts of HDFS:

### Very Large Files:

- HDFS is optimized for handling very large files, ranging from hundreds of megabytes to petabytes in size.

### Streaming Data Access Patterns:

- Efficient data processing patterns involve writing data once and reading it multiple times.

### Commodity Hardware:

- Designed to run on clusters of commodity hardware to achieve cost-effective and scalable computation.

## Tradeoff Considerations:

- **Low-latency Data Access:**
  - HDFS prioritizes high throughput over low-latency access.

- **Handling of Lots of Small Files:**
  - HDFS is not suitable for managing a large number of small files in one Namenode due to inefficiencies in storing metadata.
  - 파일들을 위치들을 저장해야하고 이런 메타 데이터들을 다 기억해야하는데 여러 개의 메타데이터들이 생겨나기 때문에 비효울적 

- **Multiple Writers and Arbitrary File Modifications:**
  - HDFS does not support multiple writers or arbitrary file modifications, emphasizing a write-once, read-many processing pattern.

## Blocks:

- **Definition:**
  - A minimum amount of data that a disk can read or write (default size is 128MB).

- **File Organization:**
  - Files in HDFS are broken into block-sized chunks called data blocks.

- **Benefits:**
  - Large block sizes optimize data retrieval speed.
  - Blocks fit well with replication for fault tolerance and availability.
- HDFS에 있는 Block이 큰 이유는 나중에 데이터를 읽을 때 빠르게 읽기 위해
- 작은 단위로 있으면 더 많이 읽어와야 하기 때문

# Name Node & Data Node

An HDFS cluster operates with two types of nodes in a master-worker pattern: a name node (the master) and multiple data nodes (workers).

## Name Node:

The namenode manages the filesystem namespace, maintaining the filesystem tree and metadata for all files and directories. It also possesses information about the datanodes where blocks for a given file are located.

- **FSImage:**
  - Stores the entire namespace information, including the mapping of files to blocks.
  - 파일에 매핑된 블록 등을 포함한 전체 네임스페이스 정보를 저장

- **EditLog:**
  - Records metadata changes in the filesystem. If metadata changes occur in the FSImage, specific file modifications are logged as transaction logs.
  - : FSImage 정보에서 metatdata 정보가 만약 변경된다면, 특정 파일에 변경사항 Transaction 로그들 기록

Without the namenode, the filesystem becomes unusable, leading to a Single Point of Failure (SPOF). It is crucial to make the namenode resilient to failure.

## Data Node:

Datanodes are the workhorses of the filesystem, storing and retrieving blocks as instructed. They periodically report their status information back to the namenode.

- Datanodes send periodic signals, known as "Heartbeats," to inform the namenode about their status (every 3 seconds).

- In the absence of the namenode, the filesystem cannot be used, and all files may be lost since there is no way to reconstruct files from the blocks on the datanodes.
  - 이거를 SPOF 라고 불림
    - All the files on the filesystem would be lost since there would be not way of knowing how to reconstruct the files from the blocks on the datanodes
    - It is important to make the namenode resilient to failture
 

### Single Point of Failure (SPOF):

A situation where the failure of a single component disrupts the entire system. In the case of HDFS, the namenode is a SPOF, and ensuring its resilience is important.
- 어떤 시스템에서 하나의 구성 요소가 동작하지 않으면 시스템 전체가 중단되는 상황. 장애가 발생한 구성 요소에 대한 여분 혹은 대체 가능한 요소가 구비되어 있지 않아서, 장애 복구가 완료될 때까지 운영이 불가능한 상황 직면

### High Availability:

Refers to a system's ability to operate continuously for an extended period. High availability aims to minimize downtime even in the presence of component failures.

## Checksums in HDFS:

HDFS transparently checksums all data written to it and verifies checksums by default when reading data.

- Datanodes are responsible for verifying the data they receive before storing the data and its checksum(if it detects an error, the client receives a ChecksumException)

- When Clients read data from data-nodes, they verify checksum as well, comparing them with the ones stored at the datanode

- HDFS can heal corrupted blocks by copying one of the good replicas.

### Checksum:

Checksums are computed and stored values for a portion or the entire data block. When reading data, HDFS compares stored checksum values with the computed checksum to verify data integrity.

# Fault Tolerance in Hadoop HDFS

Fault tolerance in Hadoop HDFS refers to the system's ability to handle adverse conditions and work intensively under challenging situations. In Hadoop 2.x, fault tolerance is achieved through the process of replica creation. HDFS creates copies of data blocks and stores them on multiple machines. If any machine fails, the data block can be accessed from another computer containing a copy of the same data, ensuring no data loss.

HDFS's replica placement policy involves:

1. One replica in the local rack.
2. On a node in a remote rack.
3. On a different node in the same remote rack.

**Rack:** In the context of computer clusters, a "rack" refers to a set of several servers or data storage devices associated from both a network and physical perspective.

## Hadoop Ecosystem Components

### MapReduce (Data Processing)

### YARN (Cluster Resource Management)

1. **Scalability:**
   - Ability to scale horizontally by adding more nodes to the cluster.

2. **High Availability:**
   - Ensuring continuous operation over an extended period, even in the face of component failures.

3. **Unity:**
   - Providing a unified platform for various data processing tools and frameworks.

4. **Multi-Tenancy:**
   - Supporting the concurrent use of the system by multiple users or applications.

Hadoop Ecosystem, including HDFS, facilitates the operation of various tools like Spark, Flink, Impala, Hive, ensuring they run effectively on the Hadoop cluster.

**Cluster:** A "cluster" denotes a computing environment where multiple computers or servers are interconnected through a network to distribute processing tasks and utilize shared resources. Clusters act as a single system, collaborating to enhance performance and provide high availability.

## Column-Oriented Databases

Column-oriented databases store data in columns rather than rows, grouping similar attributes into column families. This is in contrast to row-oriented databases (e.g., MySQL, Oracle RDBS) where rows are grouped together.

### Row-Oriented Database:

- **Example:**
1. Paul Walker, US, 231, Gallardo
2. Vin Disel, Brazil, 520, Mustang

- Row Oriented Case: Paul Walker, US, 231, Gallardo,   2. Vin Disel, Brazil, 520, Mustang
- Column Oriented Case: 1, 2 | Paul Walker, Vin Disel | US, Brazil | 231, 520 | Gallardo, Mustang
- Column oriented 가 빠른 이유는 query를 했을 때 불필요한 column 에 access를 안해도된다
-  select name, address from example 을 보면 row-oriented들은 불필요한 다른 column도 읽어아햠






