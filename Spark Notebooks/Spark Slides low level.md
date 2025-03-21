
Up: [[Spark Slides]]
Tags: #literature 
Topics:
prerequisites:
Teacher/Author:
Link:
A-N-K-I: 
17-03-25
04:35

-----

###  **What Is Apache Spark?**

##### **Definition** with some claims
Apache Spark is a <mark style="background: #8fcf85;">unified</mark> <mark style="background: #CCCC33;">computing engine</mark> for <mark style="background: #FFAA55;">parallel data processing</mark> on  <mark style="background: #F5aee5;">computer clusters</mark>.
- Spark scales from a single laptop to thousands of servers, making it ideal for big data processing.
##### **Unified (say)**
- Spark’s a unified platform for big data apps—one tool for all your needs.
    - Handles diverse analytics tasks like SQL and machine learning on a single engine with consistent APIs.
    - Makes real-world analytics—interactive or production—easier and faster.
- Offers flexible, composable APIs.
    - Build apps from small pieces or existing libraries, and add your own if needed.
- Designed for **high performance** with optimization.
    - Combines tasks like SQL and machine learning into one quick data scan.
- **Structured APIs**
	- Became the standard by solving the mix-and-match problem, evolving with structured APIs like DataFrames in Spark 2.0 for smarter optimization.

##### **Computing Engine (say)**
- **Computation Focus**
	- Is not like like <mark style="background: #8fcf85;">hadoop</mark> (Computing and storage together), making it tricky to use one without the other
		- Map Reduce for computation
		- HDFS for storage

- Spark’s all about being a computing engine, not a storage system.
    - It loads data from wherever it’s stored and runs computations on it.
        - Works with tons of storage options like Amazon S3, Hadoop, Cassandra, or Kafka, without caring where the data lives.
- Doesn’t store data itself or pick favorites among storage systems.
    - Since data’s costly to move, 
        - Spark <mark style="background: #CCCC33;">focuses on in place Computation</mark> 
- **In-Place Memory**
	- Process the data right in RAM, avoiding slow disk reads
		- Ram --> (random access memory)
			- Temporary (volatile)
			- Limited storage
			- very Fast
		- HDD (hard disk driver)- SSD (Solid-State Drive)
	- **RAM** is 3,000x faster than **SSDs** and 1,500,000 times faster than **HDDs**.
- [Link](https://colin-scott.github.io/personal_website/research/interactive_latency.html)


#### **Parallel Processing** (say)
- Distributes computations across multiple nodes in a cluster for efficiency.
- Executes tasks concurrently, leveraging distributed memory and reducing bottlenecks.

#### **Libraries (say)**
- Built on its unified engine to give you a single API for all kinds of data tasks.
    - Like Spark SQL for structured data, 
    - MLlib for machine learning, 
    - Structured Streaming for real-time processing
    - GraphX for graphs.
- External third-party libraries (open-source) world.
    - Hundreds of third-party packages, 
        - Such as storage connectors to new tools.  

### **The Big Data Problem (say)**
- Why do we even need Spark? It’s all about shifts in computing economics.
    - Processors got faster yearly, so apps scaled up without changes—until 2005, 
    - when heat limits stopped that, pushing us to parallel cores.
        - Suddenly, apps needed parallelism to speed up, setting the stage for Spark.
- Meanwhile, <mark style="background: #8fcf85;">data storage and collection kept getting cheaper</mark> and better.
    - Storage Is now cheap

Scaling Up --> From one single core to multiple cores (on the same device)
Scaling Out --> From one single device to multiple connected devices through the network. 

<mark style="background: #CCCC33;">Computation Shift</mark>: Single-core ended up; now we need parallel cores, so apps must adapt for speed, sparking tools like Apache Spark.

<mark style="background: #CCCC33;">Storage Shift</mark>: Cheap, and More IOT Sensor devices , better quality, more data collected.


#### **History of Spark (say)**
- Spark kicked off in <mark style="background: #8fcf85;">2009 at UC Berkeley’s</mark> AMPlab, born from a research project to fix Hadoop MapReduce’s inefficiencies.
    - Started with a 2010 paper by Matei Zaharia and team, tackling issues like slow, multi-pass machine learning jobs.
        - MapReduce forced separate jobs per data pass; 
        - Spark built a functional API and in-memory engine to make it fast and simple.
- Evolution Milestones
	- 2010 paper by Matei Zaharia and team
		- MapReduce Problem.
			- Frequent **disk I/O** slowed down iterative and complex workloads.
			- Lack of **in-memory computation** for efficient data reuse.
		- Memory engine
			- Introduced **Resilient Distributed Datasets (RDDs)**.
			- Allowed **caching data in memory**, making iterative jobs (ML, graph processing) much faster.
![[Pasted image 20250317051652.png]]
- Scala and Shark for SQL in **2011**
- went Apache in **2013** with 100+ contributors
- Spark 2.0 in **2016** with structured APIs like Data Frames.
- Spark 3.0 (**2020**) with adaptive query execution
- Spark 3.5 (**2023**) for tighter cloud integration.


### Introduction to Spark
**Spark’s Basic Architecture**: Think beyond your solo PC
- Spark uses a cluster, a bunch of machines pooling power like one big computer.
	- Single machines can’t handle big data fast enough; a cluster fixes that.
	- Spark coordinates tasks across this cluster, managed by something like its standalone manager, YARN, 
		- you submit your app, and it gets the resources to roll.


**Spark Applications**: Every Spark job has a driver and executors.
- The <mark style="background: #8fcf85;">driver</mark>’s the boss—runs your main code, tracks the app, and splits work to executors.
- <mark style="background: #CCCC33;">Executors</mark> are the workers, spread across the cluster, doing the heavy lifting under the driver’s orders. 
	- It’s the heartbeat of how Spark gets stuff done!
Think of a **Spark application** as a **container** running Spark jobs

Something like name node and data node in hadoop
- name node is like the driver
- data node is like the executer

**Spark Session** -  **main entry point** for interacting with Spark.
-  interactive mode (pyspark or spark shell)
- In a **standalone application**
- Provides functions to 
	- create DataFrames, 
	- run SQL queries
	- manage Spark configurations.


#### **Spark Distributed Execution**
###### **Spark Architecture Overview**
![[Pasted image 20250317052547.png]]

- **Spark Driver**
	- Instantiates SparkSession (entry point).
	- Communicates with Cluster Manager to request resources.
	- Schedules DAG computations (Directed Acyclic Graph).
	- Distributes tasks across executors and collects results.
Runs on the **master node** in a cluster.

- **Spark Session**
	- Introduced in **Spark 2.0** as a **unified API** for all operations.
		- Replaces <mark style="background: #8fcf85;">SparkContext</mark>, <mark style="background: #8fcf85;">SQLContext</mark>, <mark style="background: #8fcf85;">HiveContext</mark>, <mark style="background: #8fcf85;">StreamingContext</mark>

- **Cluster Manager**
	- Standalone Mode: Built-in, easy setup.
	- Apache Hadoop YARN: Runs within Hadoop ecosystem.

- **Spark Executors**
	- Executors are **worker processes** that perform actual computation.
Responsibilities:
- <mark style="background: #CCCC33;">Execute tasks</mark> assigned by the driver.
- <mark style="background: #FFAA55;">Store intermediate data in memory</mark> (for performance).
- <mark style="background: #8fcf85;">Communicate results back to the driver</mark>.
Each Spark application gets dedicated executors.
Executors shut down when the application finishes.

### **Spark Deployment Modes**
- Spark can be deployed in different environments.
- Deployment options:
1. **Local Mode**: Single-machine execution (for testing).
2. **Standalone Mode**: Spark’s built-in cluster manager.
3. **YARN Cluster Mode**: Runs within Hadoop’s YARN.
4. **Mesos Cluster Mode**: Multi-framework resource sharing.
5. **Kubernetes Mode**: Cloud-native containerized execution.

- Choice of mode depends on:
    - **Scalability needs** (single node vs. distributed cluster).
    - **Integration with existing infrastructure**.
    - **Cloud vs. on-premises deployment**.

![[Pasted image 20250317060720.png]]

More details on Chapter 15 Spark Definitive guide Book


### **Lazy Evaluation**
Processing does not execute each operation right away
- that means it does not start until we trigger any <mark style="background: #CCCC33;">action</mark>.

All transformations can be combined together into a single transformation and executed together.
- This happen with RDDs, Dataframes.

**_Actions_**:  
Actions are operations that trigger the actual computation
- Return results to driver program or write data to an external storage system.

**Action types**
- Actions to **view data in the console**
- Actions to **collect data** to native objects in the respective language
- Actions to **write to output data sources**

**Why Lazy Evaluation?**
- Efficiency
	- Execution is delayed until needed, allowing Spark to optimize the execution plan.
	- Reduces unnecessary data shuffling and minimizes data transfer across the cluster.
	- Ensures only the required data is processed, leading to efficient resource utilization.
- Optimization
	- Enables Spark’s **Catalyst Optimizer** to evaluate the entire **DAG** (Directed Acyclic Graph) before execution.
- Fault Tolerance
	- Stores **lineage information** (a record of all transformations) instead of intermediate results.
	- If a node fails, Spark can **recompute only the lost data** instead of rerunning all transformations.
[Lazy Evaluation](https://www.ishandeshpande.com/post/the-art-of-efficiency-understanding-lazy-evaluation-in-apache-spark)


#### **Dag** (Directed Acyclic Graph)
DAG in Apache Spark in similar terms is a set of **Vertices** and **Edges**

Spark Application model Drawing.
![[Pasted image 20250317070421.png]]
- **Application**
    - A user program built on Spark using its APIs.
    - Consists of a **driver program** and **executors** on the cluster.

- **Job**
    - A parallel computation consisting of multiple **tasks**.
    - Triggered by a **Spark action** (e.g., `save()`, `collect()`).
    - The driver converts the application into one or more **jobs**.
    - <mark style="background: #F5aee5;">Each job is transformed into</mark> a **DAG**, defining execution flow.

- **Stage**
    - Each job is divided into **stages**, which contain multiple tasks.
    - Stages are created based on operations that can run **serially or in parallel**.
    - Some operations require **data transfer**, splitting execution into multiple stages.

- **Task**
    - The smallest unit of execution within a stage.
    - Each task is assigned to a Spark **executor**.
    - Tasks correspond to a **single partition** of data.

### **RDDs**
**Resilient Distributed Datasets (RDDs)**
- Low-level API in Spark for distributed data processing
- Used when Structured APIs (DataFrames/Datasets) are insufficient
- Immutable, partitioned collection of objects.
- Supports parallel computation

**Differences from DataFrames/Datasets:**
- No predefined schema (raw Java/Scala/Python objects)
- Requires manual optimizations (e.g., filtering, aggregations)
- More control over storage & computation

**When to use RDDs**
- Functionality not available in Structured APIs (e.g., fine-grained control over data placement)
- Maintaining legacy Spark 1.x code-bases.
- Custom shared variable manipulation
- General <mark style="background: #CCCC33;">Advice</mark>:
    - Use Structured APIs when possible for better performance & ease of use
    - Understand <mark style="background: #FFAA55;">RDDs</mark> for debugging & optimization
#### Lab


### **Structured API Overview**
- Core Types
	- <mark style="background: #FFAA55;">Datasets</mark>, <mark style="background: #CCCC33;">DataFrames</mark>, and <mark style="background: #FF8888;">SQL</mark> tables/views
- Batch & Streaming
	- APIs work for both batch jobs and streaming
- Execution Basics
	- Hit an action, and Spark breaks it into stages and tasks, running it across the cluster as a job.
	- <mark style="background: #8fcf85;">DataFrames</mark> and <mark style="background: #8fcf85;">Datasets</mark> are what you tweak with transformations; actions kick off the compute or pull results back.

## Transformation
Python immutable change
Immutable objects (like **integers, strings, tuples, frozensets**) are stored in memory
- Just like how python change in the immutable objects
	- Leave the Object as it is and create another object then point to that new one 
![[Pasted image 20250320072223.png]]

- In spark the core data structure are immutable, meaning they can not be changed after the creation,
-  To change a `DataFrame` ==transformation== 
	- transformation is the core of how you express your business logic using spark

There are two types of transformations: 
- those that specify narrow dependencies
![[Pasted image 20240622063103.png]]
- **Narrow Transformations**: Operations where each input partition contributes to only one output partition, e.g., `map`, `filter`. These are fault-tolerant and performed in parallel.

- those that specify wide dependencies.
![[Pasted image 20240622063127.png]]
- **Wide Transformations**: Operations requiring data shuffling across partitions, e.g., `groupByKey`, `join`. These are more resource-intensive but essential for certain computations.



### **DataFrames**

### **DataSets**

#### Lab




































