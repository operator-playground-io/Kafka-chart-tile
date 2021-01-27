<h1 align="center">Kafka</h1>

![Logo](_images/logo.png)

[Kafka](https://kafka.apache.org/) is a distributed streaming platform used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, wicked fast, and runs in production in thousands of companies. It was developed by LinkedIn first, and is used by technology leaders such as Uber, Netflix, Slack, Coursera, Spotify and others.

# Introduction
Kafka Bitnami Chart  bootstraps a [Kafka](https://github.com/bitnami/bitnami-docker-kafka) deployment on a [Kubernetes](http://kubernetes.io/) cluster using the [Helm](https://helm.sh/) package manager.
It also packages Zookeeper to manage and coordinate the Kafka cluster.

In this tutorial, we’ll use Helm for setting up Kafka on top of a Kubernetes cluster, in order to create a highly-available streaming platform.
In addition to leveraging the intrinsic scalability and high availability aspects of Kubernetes, this setup will help keeping Kafka secure by providing simplified upgrade and rollback workflows via Helm.

# Prerequisites

- Kubernetes 1.12+
- Helm 3.0-beta3+
- PV provisioner support in the underlying infrastructure

# Kafka Architecture
First let’s take a closer look at the Kafka basic architecture. Kafka architecture is made up of topics, producers, consumers, clusters, brokers, partitions, replicas, leaders, and followers.


A high level Kafka Architectural flow is as shown below :

![](_images/kafka-architecture.png)

**Kafka Brokers :**

A Kafka broker is a server running in a Kafka cluster (or, a Kafka cluster is made up of a number of brokers). Typically, multiple brokers work in concert to form the Kafka cluster and achieve load balancing and reliable redundancy and failover. Brokers utilize Apache ZooKeeper for management and coordination of the cluster. Each broker instance is capable of handling read and write quantities reaching to the hundreds of thousands each second (and terabytes of messages) without any impact on performance. Each broker has a unique ID, and can be responsible for partitions of one or more topic logs. Connecting to any broker will bootstrap a client to the full Kafka cluster. To achieve reliable failover, a minimum of three brokers should be utilized —with greater numbers of brokers comes increased reliability.

**Kafka Producers :**

A Kafka producer serves as a data source that optimizes, writes, and publishes messages to one or more Kafka topics. Kafka producers also serialize, compress, and load balance data among brokers through partitioning.

**Kafka Consumers :**

Consumers read data by reading messages from the topics to which they subscribe. Consumers will belong to a consumer group. Each consumer within a particular consumer group will have responsibility for reading a subset of the partitions of each topic that it is subscribed to. 

**Zookeeper :**

Kafka uses zookeeper to manage service discovery for kafka brokers that form the cluster. Zookeeper sends changes of the topology to kafka, so each node in the cluster knows when a new broker joins, a broker dies, a topic was removed or a topic was added, etc. Zookeeper provides an in-sync view of kafka cluster configuration.

**Kafka Topics :**

A Kafka topic defines a channel through which data is streamed. Producers publish messages to topics, and consumers read messages from the topic they subscribe to. Topics organize and structure messages, with particular types of messages published to particular topics. Topics are identified by unique names within a Kafka cluster, and there is no limit on the number of topics that can be created. 

**Kafka Partitions :**

Within the Kafka cluster, topics are divided into partitions, and the partitions are replicated across brokers. From each partition, multiple consumers can read from a topic in parallel. It’s also possible to have producers add a key to a message—all messages with the same key will go to the same partition. While messages are added and stored within partitions in sequence, messages without keys are written to partitions in a round robin fashion. There is no limit on the number of Kafka partitions that can be created.

# Objective of tutorial

In this tutorial,we are going to cover following topics:

- How to Install Kafka Bitnami Helm Chart and verify its successful installation.
- Verify status of pods and services. 
- Deploy a test client that will execute scripts against the Kafka cluster.
- Uninstall Kafka Helm Chart and release resources.





