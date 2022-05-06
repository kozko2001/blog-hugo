
---
title: CCDAK (Confluente Certified Developer for Apache Kafka) Notes -- Cloud.Guru
date: 2022-06-05 00:00:00
---
---

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

### 1.5 Kafka Architecture

