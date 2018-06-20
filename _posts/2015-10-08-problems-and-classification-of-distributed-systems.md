---
layout: post
title: A Primer on Distributed Systems
---

Days of Moore’s law, that number of transistors in an integrated circuit double every two years, are arguably numbered. Our modern world grows and demands computing needs faster than Moore’s law. We have complex applications and big data which simply can not be processed and stored by a single computer, no matter if that’s the fastest computer in world or has maximum possible hard drives attached. A modern *scalable application* consists of several processes. A process, as I use here, may represent a physical computer, a virtual machine, a container, or a thread in a concurrent system. A fundamental problem in such a hybrid architecture is that each process needs to communicate and coordinate with other processes to work on some task. Such processes may be distributed as containers or virtual machines on same server or be on separate server nodes in same datacenter or even distributed to separate distant datacenters connected with secure networks. We call such systems by names such as Distributed Software Systems, Distributed Architecture and Microservices etc.

## Challenges for Distributed Algorithms

Distributed environments pose additional challenges in comparison to traditional monolithic application architectures: How to continue operations in presences of failures? Failures in network connectivity, hardware, single process, data integrity or security of some processes or data center should not take down entire application. *Distributed algorithms* help us ensuring services coordinate reliably and continue operations even if some of them fail. Distributed algorithms need to be reliable, secure and tolerant to faults caused by environment.

Distributed computing involves study and implementation of algorithms that help processes in achieving coordination with each other. In addition of running concurrently or in parallel, some processes in such a system may fail and others may continue operations. These failures are characteristics of a distributed system. A distributed system is different than concurrent system because a distributed system expects failures while concurrent systems rely on all processes completing without failures.

When some processes in distributed system fails, it must be made sure that other services synchronize their activities correctly and consistently. It must be fault tolerant and robust. This challenge makes distributed software engineering a very hard but very interesting problem.

As an example, if some web server crashes, action should be to switch website to a new server immediately without having any downtime or making users notice the failure. Even more reliable system would continue processing client requests even if one or few of the requests fail or take an unusual amount of time. In addition to client-server interaction between users of a web application and application server, distributed systems may consist of several processes which coordinate with each other to perform some common task. Both, the client server and multiple processes architecture coexist in modern micro services architectures. An example implementation would be such that, a client connects to a server via a *gateway api* and gateway api service makes requests to and coordinates with several services to complete the client request.

To coordinate, processes need to exchange messages with each other. Such message passing introduces a new problem we call distributed agreement problem. Processes need to agree on what to do, what happened, what needs to be done and who does what and in what order. As an example consider following situations:
- For processes to communicate with each other, they must agree on who they are (IP address, ssh keys). They also need to agree on what format to pass messages in (RPC, SOAP, REST or other) and how to pass those messages (Message queues, TCP/UDP)
These processes may sometimes need to make sure what they are about to do is agreed upon by all other processes and if anyone disagrees such a task must be aborted. Such situations are called *distributed transactions* and this problem is called *atomic commitment* problem.
- Agreeing on what to do is just one of the problems, in addition to what to do, processes may need to agree on in what order to perform the given task. Performing tasks in order is crucial for distributed databases. This problem is called *total order broadcasting* problem.

## Types of Distributed Applications

We attempt to classify distributed systems based on nature of distribution of their processes. Note that, these categories aren’t the only ones and some applications may even fall in multiple categories. Distributed systems often rely in one of following categories:

### Publish-Subscribe Applications

In applications that fall in this category, processes may fall in one of following conditions: produces of information who publish and consumers of information who subscribe to information. This paradigm is often called *publish-subscribe* and is most common type of distributed architecture. Examples of such applications may be Stock exchange application, Sound and video streaming services and Bittorrent.

### Process Control

In process control applications several processes control a single physical activity. Most common example of this kind of applications is Aircraft or Train control in which data from multiple sensors controls the flight. Monitoring of nuclear power plant or car manufacturing assembly automated by several robotic arms.

Every process in such a system is connected to a sensor, the goal is to perform a single task such as mapping aircraft on radar or control speed of train despite the possibility of failure in one of sensors.

### Cooperative Work

Sometimes people connected with network from different nodes may want to collaborate on same task such as editing a document, a software or a video conference or group chat etc. Shared workspace is shown as single storage for all collaborators. Such operations can be achieved by getting different nodes to agree on order of reads and writes on the workspace.

### Distributed Databases

Databases need to agree on whether to commit or discard a particular transaction. In a setup where there are multiple instances of databases in master/slave or master/master replication mode, in case of a transaction all nodes must detect if data is available to every other node and then commit. If failure such as error in data integrity, network or hardware failute is detected in any one node is detected, all nodes may abort the transaction. This problem is called *atomic commitment* problem.

### Distributed Storage

A system where large amount of data is to be stored, it may not be sufficient to use a single system. Data is distributed among several nodes and presented to application is single large storage. In such systems, data is distributed among several nodes and copies of data are made on different nodes in case one of nodes fails. A single file may also be stored in parts on several nodes. Read and write operations are distributed on different nodes to load balance IO and increase throughput.

## References and Further Reading

This article is a dumbed down version of chapter one in [Introduction to reliable secure distributed programming](http://www.amazon.com/Introduction-Reliable-Secure-Distributed-Programming/dp/3642152597/ref=sr_1_3?ie=UTF8&qid=1444293858&sr=8-3&keywords=reliable+distributed+systems) book. I recommend studying whole book as it will help in clarifying theoratical concepts of distributed systems. 

[ETH Zurich's course](http://dcg.ethz.ch/lectures/podc_allstars/index.html) on Distributed Systems is also a great resource. Chapter 0 is good resource to reflect on concepts described in this article. 

Expect more posts on distributed systems from me in future.