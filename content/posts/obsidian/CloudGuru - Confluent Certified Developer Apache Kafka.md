
---
title: CCDAK (Confluente Certified Developer for Apache Kafka) Notes  == Cloud.Guru
date: 2022-06-05 00:00:00
---
---
t
# CCDAK (Confluente Certified Developer for Apache Kafka)

## 1  Introduction
### 1.1 Installation
- Kafka need around 6Gb of JVM Heap Space

```bash
kafka-topics --list --bootstrap-server localhost:9092 # get the list of topics
```

### 1.2 What is Kafka
What is:
- publish and subscribe to streams of data records
- store the records in a fault-tolerant and scalable fashion
- Process streams of records in real-team

Kafka can be used to:
- messaging
- streaming

Strong points:
- very reliable (not losing data)
- Fault tolerance
- robust API

### 1.3 Kafka from the CLI

### 1.4 Publisher/Subscriber

**Topics** are datafeed (log) that help us to have the data organized in our kafka cluster.

**Topic Log**: is an order, inmutable list of data records. when we publish a record, it's added at the end of the log.

**Partition**: the topic log is divided in partitions, which may reside in different broker. For scalability.

**Offsets**: is the index of a record (in the partition).

**Producers**: is an external service adding data to a topic. Producers can decide to which partition they want to write. The default strategy is round-robin.

**Consumers**: services that receive the data, consumer controls it own offset for the partition. They can actually read in any order. You can have as many consumers as you want subscribed to a topic. The record data is not deleted after being consumed.

**Consumer Group**: To scale horizontal, we need a consumer group, where the consumers inside the consumer group, will process different partitions.

### 1.5 Kafka Cluster Architecture

**Brokers**: nodes in the kafka cluster (a server running kafka). One of them is the controller. uses TCP protocol to handle network.

**ZooKeeper**: Is another project, but it's used by managing the server, making sure that the cluster is stable. (adding brokers, removing brokers). Could be installed in a different server than the brokers.

**Controller**: There is 1 controller at any giving time (one of the brokers). Coordinates decisions on where to place partitions and data replicas.

### 1.6 Partitions and Replications

**Problem**: What happen when a server crashes with the partitions. what happens to that data.

**Replication** => storing multiple copies of each topic partition to different brokers. setting `replication_factor` by topic. Each replica will be in different broker.

**Leader**: Each replication has a **leader**, that means is the source of truth. Specially important for the order, so all writing/reading will be done at the leader replica. If a leader goes down, another replica will become the leader -> **Leader election**

**In-Sync Replicas**: replicas that are sync with the leader replica. You can turn on `unclean leader election` . Will allow to be elected as a leader when the leader goes down. By default only, will only consider **In-Sync replicas**

What if there is only non-sync replicas? kafka will wait until there is a new in-sync replica... thus not allowing to add new messages to the log or read.

`kafka-topics --bootstrap-server localhost:9092 --create --topic my-topic --partitions 3 --replication-factor 2` 

`kafka-topics --bootstrap-server localhost:9092 --describe --topic my-topic`

`kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 6 --topic inventory_purchases`

``kafka-console-producer --broker-list localhost:9092 --topic inventory_purchases`

``kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --from-beginning

Add a consumer to a specific group, execute in multiple terminals to have multiplce consumers in the same consumer group.
`kafka-console-consumer --bootstrap-server localhost:9092 --topic inventory_purchases --group 2`

## Kafka Java APIs
Shared java libraries that help to operate with kafka.
- `Producer API`
- `Consumer API`
- `Streams API`: Consumes data from a topic, transforms it, and write it into a new topic
- `Connect API`: Pull/Push data from external services
- `AdminClient API`

props that use in the video or creating a producer `bootstrap.servers` `key.serializer` `value.serializer`

`Producer<String, String> producer = new KafkaProducer<>(props)`

`producer.send(new ProducerRecord<String, String>("count-topic", "count", ))`