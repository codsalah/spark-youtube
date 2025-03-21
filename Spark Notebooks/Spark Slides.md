
Up: [[Spark the Definitive guide Book]]
Tags: #literature 
Topics:
prerequisites:
Teacher/Author:
Link: [[Spark Slides low level]]
- [[Spark Article]]
A-N-K-I: 
17-03-25
04:27

-----

### **What is Apache Spark?** (Claims)
- Unified.
- Computing Engine.
- Libraries.
- For Parallel data processing. 
- On Cluster of computers.

![[Pasted image 20250317042924.png]]

#### **Unified** 
- Unified Platform
- Offer various APIs
	- SQL
	- ML
	- RDDs
	- Stream processing
- High Performance
- Structured APIs

### **Computing Engine**
- Computation Focus
- In-memory Computation
- Storage Compatibility
- Non-Hadoop Flexibility

### **Libraries**
- Built-in
- External

### **Evolution of The Big Data Problem**
- Parallel Shift
- Data Cost Decline
- New Model Need

### **History of Spark**
- Origins - UC Berkeley’s AMPlab (2009)
- Evolution Milestones
	- 2010 paper by Matei Zaharia and team
		- MapReduce Problem.
		- Memory engine
![[Pasted image 20250317051652.png]]
- Scala for SQL in **2011**
- Apache Spark in **2013** with 100+ contributors (2100+ now in 2025)
- Spark 2.0 in **2016** with structured APIs like Data Frames.
- Spark 3.0 (**2020**) with adaptive query execution
- Spark 3.5 (**2023**) for tighter cloud integration.


#### **Introduction to Spark**
- **Spark’s Basic Architecture**: 
	- Think beyond your solo PC
- **Spark Applications**: 
	- Every Spark job has a driver and executors.
- **Spark Session** -  **main entry point** for interacting with Spark.
	-  interactive mode (pyspark or spark shell).
	- In a **standalone application**.
	- Provides some functions.
	- Think of it like an interaction between two or more entities

#### **Spark Distributed Execution** (Architecture Overview)
- **Spark Application**
- **Spark Driver**
- **Spark Session**
- **Cluster Manager**
- **Spark Executors**

#### **Spark Deployment Modes**
- Spark can be deployed in different environments.
	- Deployment options:
- Choice trade-off:

### **Lazy Evaluation**
- What is Lazy Evaluation
- What are actions ?
- Types of an action
- Why ?

### **Dags (Directed Acyclic Graph)**
Drawings and Drawings... (Spark Application model, Job Dag)
- **Application**
- **Job**
- **Stage**
- **Task**

[Link Article](https://medium.com/plumbersofdatascience/understanding-spark-dags-b82020503444)


## Structured APIs Overview
**Structured API Overview**
- Core Types
	- Datasets, DataFrames, and SQL tables/views
- Batch & Streaming
	- APIs work for both batch jobs and streaming
- Execution Basics
	- Hit an action, and Spark breaks it into stages and tasks, running it across the cluster as a job.
	- DataFrames and Datasets are what you tweak with transformations; actions kick off the compute or pull results back.

## Transformation
Apache Spark, **RDDs** (Resilient Distributed Datasets), **DataFrames**, and **Datasets** are <mark style="background: #FF8888;">immutable</mark>.
- Spark do the transformation to the immutable files as python do it.
	- They create new object and return a reference to it.

**Types of transformation**
- Narrow transformation
	- What is it ?
	- Examples of it ?
- Wide transformation
	- What is it ?
	- Examples of It ?

#### **RDDs**
- What are Resilient Distributed Datasets (<mark style="background: #8fcf85;">RDDs</mark>)
	- Low Level
- Situations where <mark style="background: #FF8888;">RDDs</mark> are necessary

##### Lab


# What is next ?
## Data Frames, Datasets, SQL
## Spark Streaming