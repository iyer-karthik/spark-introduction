# Conceptual introduction to Spark

### Preliminaries
Spark is a popular tool for big data processing and analytics. Spark is a newer framework compared to tools such as Hadoop. Spark is generally faster than Hadoop. 

#### Outline

***What is Big Data?***

For starters, Big Data is an overloaded term with no single definition. A good mental heuristic is this - we know we are working with Big Data when instead of using a single machine, it's easier to use a distributed system of multiple computers. To understand when data becomes big data we need to be familiar with the capabilities of modern hardware. We must be aware of what Peter Norvig calls 'Numbers everyone must know'. We will explore these numbers now to get some context on Big Data. 

***Review of the hardware behing big data***

Here are some key hardware components. 

* **CPU (Central Processing Unit)** Every process on the computer is handled by the CPU. This includes calculations and also instructions for the other components of the compute.

The CPU can also store small amounts of data inside itself in what are called registers. These registers hold data that the CPU is working with at the moment. For example, say you write a program that reads in a 40 MB data file and then analyzes the file. When you execute the code, the instructions are loaded into the CPU. The CPU then instructs the computer to take the 40 MB from disk and store the data in memory (RAM). The registers make computations more efficient: the registers avoid having to send data unnecessarily back and forth between memory (RAM) and the CPU.

It takes ~250 times longer to find and load a random byte from memory into the CPU than to process the same byte with CPU. 

* **Memory (RAM)** When your program runs, data gets temporarily stored in memory before getting sent to the CPU. Memory is ephemeral storage - when your computer shuts down, the data in the memory is lost.

Memory is also expensive. Beyond the fact that memory is expensive and ephemeral, for most use cases in the industry, memory and CPU aren't the bottleneck. Instead the storage and network slow down many tasks. 

As an aside, a distributed system or a cluster is just a bunch of connected machines and these machines are usually called nodes. 

* **Storage (SSD or Magnetic Disk)** Storage is used for keeping data over long periods of time. When a program runs, the CPU will direct the memory to temporarily load data from long-term storage.

Loading data from long-term storage like SSD or Magnetic Disk can be 15-200 times slower. 

* **Network (LAN or the Internet)** Network is the gateway for anything that you need that isn't stored on your computer. The network could connect to other computers in the same room (a Local Area Network) or to a computer on the other side of the world, connected over the internet.

Transferring data across a network is the biggest bottleneck when working with Big Data. For this reason distributed systems
try to minimize shuffling data back and forth between different computers. 

Here are the hardware components from fastest to slowest: 

CPU (200 times faster than) > Memory (15 times faster than) > Storage (20 times faster than) > Network

Note that if the size of your dataset is larger than your RAM, you might still be able to analyze the data on a single computer. By default, the Python pandas library will read in an entire dataset from disk into memory. If the dataset is larger than your computer's memory, the program won't work.

However, the Python pandas library can read in a file in smaller chunks. Thus, if you were going to calculate summary statistics about the dataset such as a sum or count, you could read in a part of the dataset at a time and accumulate the sum or count.


***Introduction to distributed systems***
* With distributed computing each CPU in the cluster has its own memory. 

* In distributed computing, each computer/ machine is connected to other machines across the netowrk. 

* In general parallel computing implies multiple machines share the same memory


***Hadoop Ecosystem***

Here is a list of some terms associated with Hadoop.

* **Hadoop**  - an ecosystem of tools for big data storage and data analysis. Hadoop is an older system than Spark but is still used by many companies. The major difference between Spark and Hadoop is how they use memory. ***Hadoop writes intermediate results to disk whereas Spark tries to keep data in memory whenever possible. This makes Spark faster for many use cases.***

* **Hadoop MapReduce** - a system for processing and analyzing large data sets in parallel.

* **Hadoop YARN** - a resource manager that schedules jobs across a cluster. The manager keeps track of what computer resources are available and then assigns those resources to specific tasks.

* **Hadoop YARN** - a resource manager that schedules jobs across a cluster. The manager keeps track of what computer resources are available and then assigns those resources to specific tasks.

As Hadoop matured, other tools were developed to make Hadoop easier to work with. These tools included:

**Apache Pig** - a SQL-like language that runs on top of Hadoop MapReduce i.e run ad-hoc MapReduce jobs using a SQL-like language

**Apache Hive** - another SQL-like interface that runs on top of Hadoop MapReduce

### How is Spark related to Hadoop? 

Spark is another big data framework. Spark contains libraries for data analysis, machine learning, graph analysis, and streaming live data. Spark is generally faster than Hadoop. ***This is because Hadoop writes intermediate results to disk whereas Spark tries to keep intermediate results in memory whenever possible.***

The Hadoop ecosystem includes a distributed file storage system called HDFS (Hadoop Distributed File System). Spark, on the other hand, does not include a file storage system. You can use Spark on top of HDFS but you do not have to. Spark can read in data from other sources as well such as Amazon S3.

### What is MapReduce?

MapReduce is a programming technique for manipulating large data sets. "Hadoop MapReduce" is a specific implementation of this programming technique. There are 3 steps involved in this technique - map, shuffle and reduce. 

The technique works by first dividing up a large dataset and distributing the data across a cluster. In the map step, each data is analyzed and converted into a (key, value) pair. 

In the shuffle step Data points with the same key get moved to the same cluster node. 

In the reduce step, the values with the same keys are combined together.

While Spark doesn't implement MapReduce, you can write Spark programs that behave in a similar way to the map-reduce paradigm. 

## Disclaimer: Notes scribed from Udacity's course on Introduction to Spark
