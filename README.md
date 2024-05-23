# ApacheSpark

HDFS, Map Reduce, Hive

**HDFS** - store large datasets across a distributed environment(storage of data by breaking it into large blocks and distributing them across multiple nodes for fault tolerance)

**Map Reduce** - programming model and processing framework for distributed data processing(divides a task into two phases: the Map phase, which processes and filters data, and the Reduce phase, which aggregates the results, enabling efficient large-scale data analysis across a cluster.)

Data storage
Data process 
Data pipeline
Data visualization
Data testing
Data lake
Data scheduler

Hadoop framework has tool for data storage, data process, data pipeline and data scheduler.

Two types of data process 
Batch process(Already stored data needs any processing)
Stream process(Streaming data need to processed)
*(Hadoop has only a batch process)

Before spark, they used Hadoop for batch processing and Storm for stream processing.

============================================================

**Spark is for Data processing(Distributed processing).**

**Data Storage**- Spark Integrate with : 
     NO SQL : Hbase, Cassandra, MongoDB  
     RDBMS : Oracle, Mysql, Postgres …(any rdbms) 
     Distributed File System : HDFS, s3 ….(any distributed file system)  
     Standalone File System : ntfs(windows), ext(linux)


Spark supports all the tools from Hadoop except Map Reduce.

Spark supports Languages : Java, Scala, Python, R

SparkFramework has modules namely
**Spark sql, 
Spark streaming, 
Spark MLlib, 
GraphX**
     
Spark executes demon process
Master  
Worker

Deployment modes
Standalone (using only spark for the distributed execution)
Yet Another Resource Negotiator YARN (spark with Hadoop)

Cluster manager

YARN provides a more advanced and flexible resource management system, allowing multiple applications (e.g., Spark, MapReduce, Tez) to share cluster resources dynamically.
   

Scenario :
**Standalone Mode**:You have a small cluster dedicated to running Spark jobs only. You set up a Spark standalone cluster with a master node and worker nodes. Spark manages the resources within this cluster, but if you need to run another type of job (e.g., a Hadoop MapReduce job), you'll need a separate cluster or have to manage the resources manually.

**YARN Mode**:You have a large cluster running a mix of Spark, Hadoop MapReduce, and Apache Flink jobs. YARN manages the overall cluster resources. When you submit a Spark job, YARN negotiates and allocates the necessary resources. If the cluster is busy, YARN ensures fair allocation based on priority and capacity, allowing all jobs to run efficiently side-by-side without manual intervention.

**Mesos Mode**:You have a large cluster running a mix of Spark, Docker containers, and other distributed applications. Mesos acts as a distributed kernel, abstracting the entire data center's resources into a single pool. When you submit a Spark job, Mesos negotiates and allocates resources from this pool based on resource constraints and isolation requirements. If the cluster is busy, Mesos dynamically reallocates resources to prioritize high-priority tasks, ensuring optimal resource utilization across the cluster.

Spark repl (Read-Evaluate-Print-Loop) / spark-shell 
Spark-shell (scala)
Pyspark (python)  
Has only for two languages (scala and python)

Transformation(group, sort, Reduce,Filter) and Actions(collect, show, count, save as text ..)
(For instance, function parameters might go unused, so we don't need to evaluate them. In the example above there is no point in evaluating 3 + 2 , because it's not used. The style of only evaluating what's needed is called lazy evaluation.)
Lazy evaluation in Spark refers to the optimization technique where transformations on distributed datasets (RDDs, DataFrames, or Datasets) are not immediately executed when they are called, but instead, Spark builds up a directed acyclic graph (DAG) of the transformations applied to the data(in which it search for actions which is implemented or not), because without any actions for the result only doing transformation is no use.

Spark API 
**RDD
Dataframes
Datasets**

Ref : https://www.youtube.com/watch?v=71ntq5LImRc&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=8



**PYSPARK vs PANDAS**

Ref : https://www.youtube.com/watch?v=YEGnTKRHpu8&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=3


**Spark Standalone Architecture** 

(https://www.youtube.com/watch?v=ja07Pa8NAt0)


**Data Locality** - data locality refers to the concept of processing data close to its physical location
                      within the cluster to minimize data movement, thereby improving performance and
                      reducing latency(delay).

**Types of persist** (where can we all store the data)

   - disk 
   - memory
   - disk and memory
   
**Fault tolerance**

**Data Replication:**

In some configurations, such as when using Apache Hadoop's HDFS, Spark can leverage data replication to access alternative copies of the data if one replica becomes unavailable.

**Task Re-execution:**

When a worker node fails, Spark reschedules and re-executes the tasks assigned to that node on another available node using the lineage information to regenerate the lost data.

Need to store data(replica) for activating fault tolerance.
(When executor fails, attempts to relaunch the executor in the same machine)
(When machine fails, it search for the replica(data) to launch the node)

Using the ‘supervise’ command to restart the driver program in the master node, when it gets kill (all the executors on the worker node get terminated).

In the early stage of Spark there is only one master node(no HA for master node) when master node fails then the entire job needs to be restarted.

High Availability(HA) for master nodes(has one active master and one passive master).Can able to add multiple master nodes but it all will be in passive only(listens to the executors).

While a passive master is able to listen to the executors, it continues the tasks(when active master fails).

This active to passive assigning is done by Zookeeper.(need to install zookeeper and integrate with the spark). Zookeeper monitors the master node.

**Zookeeper(cluster coordinator)**  - used in Distributed Systems to coordinate distributed process and services.
          - Zookeeper service provides configuration and state management and distributed coordination services.



**Master - Slave , Peer to peer and Leader Follower**

In Master-Slave communication, every command is passed over the master node, no slave will communicate with another slave directly.
In Peer to Peer communication, there is no master and slave. Can communicate one to one without any intermediate.
In Leader Follower, there will be leader and more follower, when leader fails the next follower will be the leader. 

Zookeeper comes under the Leader Follower category.


**Need to go through** 

**Apache Hadoop YARN (Yet Another Resource Negotiator):**

A resource management layer for Hadoop clusters that allows Spark to share resources and run alongside other Hadoop applications.

**Apache Mesos:**

A general-purpose cluster manager that can run various distributed applications, including Spark, providing fine-grained resource sharing and isolation.

**Kubernetes:**

An open-source container orchestration platform that allows Spark to run in a Kubernetes cluster using containers, offering robust scaling and resource management.
