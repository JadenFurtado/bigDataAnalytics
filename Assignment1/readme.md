# Explain Hadoop Architecture
Hadoop is a framework permitting the storage of large volumes of data on node systems. The Hadoop architecture  allows parallel processing of data using several components:

    Hadoop HDFS to store data across slave machines
    Hadoop YARN for resource management in the Hadoop cluster
    Hadoop MapReduce to process data in a distributed fashion
    Zookeeper to ensure synchronization across a cluster

This article lets you understand the various Hadoop components that make the Hadoop architecture.
Hadoop HDFS

The Hadoop Distributed File System (HDFS) is Hadoop’s storage layer. Housed on multiple servers, data is divided into blocks based on file size. These blocks are then randomly distributed and stored across slave machines.

HDFS in Hadoop Architecture divides large data into different blocks. Replicated three times by default, each block contains 128 MB of data. Replications operate under two rules:

    Two identical blocks cannot be placed on the same DataNode
    When a cluster is rack aware, all the replicas of a block cannot be placed on the same rack

 datanode

In this example, blocks A, B, C, and D are replicated three times and placed on different racks. If DataNode 7 crashes, we still have two copies of block C data on DataNode 4 of Rack 1 and DataNode 9 of Rack 3.

There are three components of the Hadoop Distributed File System:  

    NameNode (a.k.a. masternode): Contains metadata in RAM and disk
    Secondary NameNode: Contains a copy of NameNode’s metadata on disk
    Slave Node: Contains the actual data in the form of blocks

## NameNode

NameNode is the master server. In a non-high availability cluster, there can be only one NameNode. In a high availability cluster, there is a possibility of two NameNodes, and if there are two NameNodes there is no need for a secondary NameNode. 

NameNode holds metadata information on the various DataNodes, their locations, the size of each block, etc. It also helps to execute file system namespace operations, such as opening, closing, renaming files and directories.
Secondary NameNode

The secondary NameNode server is responsible for maintaining a copy of the metadata in the disk. The main purpose of the secondary NameNode is to create a new NameNode in case of failure.

In a high availability cluster, there are two NameNodes: active and standby. The secondary NameNode performs a similar function to the standby NameNode.
Hadoop Cluster - Rack Based Architecture

We know that in a rack-aware cluster, nodes are placed in racks and each rack has its own rack switch. Rack switches are connected to a core switch, which ensures a switch failure will not render a rack unavailable.
HDFS Read and Write Mechanism

HDFS Read and Write mechanisms are parallel activities. To read or write a file in HDFS, a client must interact with the namenode. The namenode checks the privileges of the client and gives permission to read or write on the data blocks.
Datanodes

Datanodes store and maintain the blocks. While there is only one namenode, there can be multiple datanodes, which are responsible for retrieving the blocks when requested by the namenode. Datanodes send the block reports to the namenode every 10 seconds; in this way, the namenode receives information about the datanodes stored in its RAM and disk.

Let us now discuss the next component of the Hadoop architecture - Hadoop YARN.
Hadoop YARN

Hadoop YARN (Yet Another Resource Negotiator) is the cluster resource management layer of Hadoop and is responsible for resource allocation and job scheduling. Introduced in the Hadoop 2.0 version, YARN is the middle layer between HDFS and MapReduce in the Hadoop architecture. 

The elements of YARN include:

*   ResourceManager (one per cluster)
*   ApplicationMaster (one per application)
*   NodeManagers (one per node)

## Resource Manager

Resource Manager manages the resource allocation in the cluster and is responsible for tracking how many resources are available in the cluster and each node manager’s contribution. It has two main components:

    Scheduler: Allocating resources to various running applications and scheduling resources based on the requirements of the application; it doesn’t monitor or track the status of the applications
    Application Manager: Accepting job submissions from the client or monitoring and restarting application masters in case of failure

## Application Master

Application Master manages the resource needs of individual applications and interacts with the scheduler to acquire the required resources. It connects with the node manager to execute and monitor tasks.
Node Manager

Node Manager tracks running jobs and sends signals (or heartbeats) to the resource manager to relay the status of a node. It also monitors each container’s resource utilization.
Container

Container houses a collection of resources like RAM, CPU, and network bandwidth. Allocations are based on what YARN has calculated for the resources. The container provides the rights to an application to use specific resource amounts.
Steps to Running an application in YARN

    Client submits an application to the ResourceManager
    ResourceManager allocates a container
    ApplicationMaster contacts the related NodeManager because it needs to use the containers
    NodeManager launches the container 
    Container executes the ApplicationMaster

Now that you know about YARN, let us continue with the next important component of Hadoop architecture called MapReduce. 

Free Course: Getting Started with Hadoop
Learn the Fundamentals of HadoopEnroll Now
Free Course: Getting Started with Hadoop

## MapReduce

MapReduce is a framework conducting distributed and parallel processing of large volumes of data. Written using a number of programming languages, it has two main phases: Map Phase and Reduce Phase.
Map Phase 

Map Phase stores data in the form of blocks. Data is read, processed and given a key-value pair in this phase. It is responsible for running a particular task on one or multiple splits or inputs.
Reduce Phase

The reduce Phase receives the key-value pair from the map phase. The key-value pair is then aggregated into smaller sets and an output is produced. Processes such as shuffling and sorting occur in the reduce phase.

The mapper function handles the input data and runs a function on every input split (known as map tasks). There can be one or multiple map tasks based on the size of the file and the configuration setup. Data is then sorted, shuffled, and moved to the reduce phase, where a reduce function aggregates the data and provides the output.
MapReduce Job Execution

    The input data is stored in the HDFS and read using an input format. 
    The file is split into multiple chunks based on the size of the file and the input format. 
    The default chunk size is 128 MB but can be customized. 
    The record reader reads the data from the input splits and forwards this information to the mapper. 
    The mapper breaks the records in every chunk into a list of data elements (or key-value pairs). 
    The combiner works on the intermediate data created by the map tasks and acts as a mini reducer to reduce the data. 
    The partitioner decides how many reduce tasks will be required to aggregate the data. 
    The data is then sorted and shuffled based on their key-value pairs and sent to the reduce function. 
    Based on the output format decided by the reduce function, the output data is then stored on the HDFS.

# Explain Hadoop ecosystem

Overview: Apache Hadoop is an open source framework intended to make interaction with big data easier, However, for those who are not acquainted with this technology, one question arises that what is big data ? Big data is a term given to the data sets which can’t be processed in an efficient manner with the help of traditional methodology such as RDBMS. Hadoop has made its place in the industries and companies that need to work on large data sets which are sensitive and needs efficient handling. Hadoop is a framework that enables processing of large data sets which reside in the form of clusters. Being a framework, Hadoop is made up of several modules that are supported by a large ecosystem of technologies. 

Introduction: Hadoop Ecosystem is a platform or a suite which provides various services to solve the big data problems. It includes Apache projects and various commercial tools and solutions. There are four major elements of Hadoop i.e. HDFS, MapReduce, YARN, and Hadoop Common. Most of the tools or solutions are used to supplement or support these major elements. All these tools work collectively to provide services such as absorption, analysis, storage and maintenance of data etc. 

Following are the components that collectively form a Hadoop ecosystem: 
 

    HDFS: Hadoop Distributed File System
    YARN: Yet Another Resource Negotiator
    MapReduce: Programming based Data Processing
    Spark: In-Memory data processing
    PIG, HIVE: Query based processing of data services
    HBase: NoSQL Database
    Mahout, Spark MLLib: Machine Learning algorithm libraries
    Solar, Lucene: Searching and Indexing
    Zookeeper: Managing cluster
    Oozie: Job Scheduling

Note: Apart from the above-mentioned components, there are many other components too that are part of the Hadoop ecosystem. 

All these toolkits or components revolve around one term i.e. Data. That’s the beauty of Hadoop that it revolves around data and hence making its synthesis easier. 

## HDFS: 
 

    HDFS is the primary or major component of Hadoop ecosystem and is responsible for storing large data sets of structured or unstructured data across various nodes and thereby maintaining the metadata in the form of log files.
    HDFS consists of two core components i.e. 
        Name node
        Data Node
    Name Node is the prime node which contains metadata (data about data) requiring comparatively fewer resources than the data nodes that stores the actual data. These data nodes are commodity hardware in the distributed environment. Undoubtedly, making Hadoop cost effective.
    HDFS maintains all the coordination between the clusters and hardware, thus working at the heart of the system.

## YARN: 
 

    Yet Another Resource Negotiator, as the name implies, YARN is the one who helps to manage the resources across the clusters. In short, it performs scheduling and resource allocation for the Hadoop System.
    Consists of three major components i.e. 
        Resource Manager
        Nodes Manager
        Application Manager
    Resource manager has the privilege of allocating resources for the applications in a system whereas Node managers work on the allocation of resources such as CPU, memory, bandwidth per machine and later on acknowledges the resource manager. Application manager works as an interface between the resource manager and node manager and performs negotiations as per the requirement of the two.

## MapReduce: 
 

    By making the use of distributed and parallel algorithms, MapReduce makes it possible to carry over the processing’s logic and helps to write applications which transform big data sets into a manageable one.
    MapReduce makes the use of two functions i.e. Map() and Reduce() whose task is: 
        Map() performs sorting and filtering of data and thereby organizing them in the form of group. Map generates a key-value pair based result which is later on processed by the Reduce() method.
        Reduce(), as the name suggests does the summarization by aggregating the mapped data. In simple, Reduce() takes the output generated by Map() as input and combines those tuples into smaller set of tuples.

## PIG: 

 Pig was basically developed by Yahoo which works on a pig Latin language, which is Query based language similar to SQL.

    It is a platform for structuring the data flow, processing and analyzing huge data sets.
    Pig does the work of executing commands and in the background, all the activities of MapReduce are taken care of. After the processing, pig stores the result in HDFS.
    Pig Latin language is specially designed for this framework which runs on Pig Runtime. Just the way Java runs on the JVM.
    Pig helps to achieve ease of programming and optimization and hence is a major segment of the Hadoop Ecosystem.

## HIVE: 
 

    With the help of SQL methodology and interface, HIVE performs reading and writing of large data sets. However, its query language is called as HQL (Hive Query Language).
    It is highly scalable as it allows real-time processing and batch processing both. Also, all the SQL datatypes are supported by Hive thus, making the query processing easier.
    Similar to the Query Processing frameworks, HIVE too comes with two components: JDBC Drivers and HIVE Command Line.
    JDBC, along with ODBC drivers work on establishing the data storage permissions and connection whereas HIVE Command line helps in the processing of queries.

## Mahout: 
 

    Mahout, allows Machine Learnability to a system or application. Machine Learning, as the name suggests helps the system to develop itself based on some patterns, user/environmental interaction or on the basis of algorithms.
    It provides various libraries or functionalities such as collaborative filtering, clustering, and classification which are nothing but concepts of Machine learning. It allows invoking algorithms as per our need with the help of its own libraries.

## Apache Spark: 
 

    It’s a platform that handles all the process consumptive tasks like batch processing, interactive or iterative real-time processing, graph conversions, and visualization, etc.
    It consumes in memory resources hence, thus being faster than the prior in terms of optimization.
    Spark is best suited for real-time data whereas Hadoop is best suited for structured data or batch processing, hence both are used in most of the companies interchangeably.

## Apache HBase: 
 

    It’s a NoSQL database which supports all kinds of data and thus capable of handling anything of Hadoop Database. It provides capabilities of Google’s BigTable, thus able to work on Big Data sets effectively.
    At times where we need to search or retrieve the occurrences of something small in a huge database, the request must be processed within a short quick span of time. At such times, HBase comes handy as it gives us a tolerant way of storing limited data

Other Components: Apart from all of these, there are some other components too that carry out a huge task in order to make Hadoop capable of processing large datasets. They are as follows: 

 

    Solr, Lucene: These are the two services that perform the task of searching and indexing with the help of some java libraries, especially Lucene is based on Java which allows spell check mechanism, as well. However, Lucene is driven by Solr.
    Zookeeper: There was a huge issue of management of coordination and synchronization among the resources or the components of Hadoop which resulted in inconsistency, often. Zookeeper overcame all the problems by performing synchronization, inter-component based communication, grouping, and maintenance.
    Oozie: Oozie simply performs the task of a scheduler, thus scheduling jobs and binding them together as a single unit. There is two kinds of jobs .i.e Oozie workflow and Oozie coordinator jobs. Oozie workflow is the jobs that need to be executed in a sequentially ordered manner whereas Oozie Coordinator jobs are those that are triggered when some data or external stimulus is given to it.


# Big Data Characteristics

Big Data contains a large amount of data that is not being processed by traditional data storage or the processing unit. It is used by many multinational companies to process the data and business of many organizations. The data flow would exceed 150 exabytes per day before replication.

There are five v's of Big Data that explains the characteristics.
5 V's of Big Data

*    Volume
*    Veracity
*    Variety
*    Value
*    Velocity

## Volume

The name Big Data itself is related to an enormous size. Big Data is a vast 'volumes' of data generated from many sources daily, such as business processes, machines, social media platforms, networks, human interactions, and many more.

Facebook can generate approximately a billion messages, 4.5 billion times that the "Like" button is recorded, and more than 350 million new posts are uploaded each day. Big data technologies can handle large amounts of data.

## Variety

Big Data can be structured, unstructured, and semi-structured that are being collected from different sources. Data will only be collected from databases and sheets in the past, But these days the data will comes in array forms, that are PDFs, Emails, audios, SM posts, photos, videos, etc.

The data is categorized as below:

    Structured data: In Structured schema, along with all the required columns. It is in a tabular form. Structured Data is stored in the relational database management system.
    Semi-structured: In Semi-structured, the schema is not appropriately defined, e.g., JSON, XML, CSV, TSV, and email. OLTP (Online Transaction Processing) systems are built to work with semi-structured data. It is stored in relations, i.e., tables.
    Unstructured Data: All the unstructured files, log files, audio files, and image files are included in the unstructured data. Some organizations have much data available, but they did not know how to derive the value of data since the data is raw.
    Quasi-structured Data:The data format contains textual data with inconsistent data formats that are formatted with effort and time with some tools.

Example: Web server logs, i.e., the log file is created and maintained by some server that contains a list of activities.
## Veracity

Veracity means how much the data is reliable. It has many ways to filter or translate the data. Veracity is the process of being able to handle and manage data efficiently. Big Data is also essential in business development.

For example, Facebook posts with hashtags.
## Value

Value is an essential characteristic of big data. It is not the data that we process or store. It is valuable and reliable data that we store, process, and also analyze.

## Velocity

Velocity plays an important role compared to others. Velocity creates the speed by which the data is created in real-time. It contains the linking of incoming data sets speeds, rate of change, and activity bursts. The primary aspect of Big Data is to provide demanding data rapidly.

Big data velocity deals with the speed at the data flows from sources like application logs, business processes, networks, and social media sites, sensors, mobile devices, etc.
