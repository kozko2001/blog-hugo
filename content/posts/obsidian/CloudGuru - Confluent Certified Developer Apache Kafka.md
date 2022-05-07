
---
title: CCDAK (Confluente Certified Developer for Apache Kafka) Notes  == Cloud.Guru
date: 2022-05-06 00:00:00
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

## 2. Kafka Java APIs
Shared java libraries that help to operate with kafka.
- `Producer API`
- `Consumer API`
- `Streams API`: Consumes data from a topic, transforms it, and write it into a new topic
- `Connect API`: Pull/Push data from external services
- `AdminClient API`

props that use in the video or creating a producer `bootstrap.servers` `key.serializer` `value.serializer`

`Producer<String, String> producer = new KafkaProducer<>(props)`

`producer.send(new ProducerRecord<String, String>("count-topic", "count", "value"))`

`producer.close()`

## 3. Kafka Streams

### Stateless transformations
- **branch**: splits a stream into multiple streams based on predicated
- **filter**: removes messages from the input stream based on a condition
- **flatMap**: maps records to new set of logs (0, 1, or n) and flats them back to a stream
- **Foreach**:
- **GroupBy/GroupByKey**: Group records by their keys.
- **Map**: transforms each stream record to a new one
- **Merge**: merge two streams into a new one

### 3.2 Aggregations
Functions that you can execute to get calculations after doing **groupBy**

- **Aggregate**: generates a new row based on a calculation from the values in the same key/aggregation
- **Count**: Count values with the same agg
- **Reduce**:

### 3.3 Joins
Combine streams into one stream.

**Co-Partitioning**: for merging, topics need to have the same number of partitions, and the same partitioning strategy. That's because each stream application (consumer in a consumer group), only have a subset of the partitions

You can use `GlobalKTable` this way, the streams application will have the data from all partitions, but you loss performance.

**Inner Join**

**Left Join**

**Outter Join**

### 3.4 Windowing

Allow to divide the aggregate groups, not only on keys, but now also on the time the record was produced

### 3.5 Streams vs Tables
**Streams**: new records do NOT replace previous data. Examples: credit card transactions

**Tables**: represents the current state, example: a users current balance in the bank account


## 4. Advanced Application Design Concepts

### 4.1 Kafka Configuration
All configurations are done by key-value pairs.

**broker configuration**:  you can use `server.properties`, the command line or the `AdminClient API`

**topic configuration**: you can configure `kafka-topics` to set properties at creation time or `kafka-configs` (a default AdminClient API tool). All topics config have a broker default value

### 4.2 Topics design
number of partitions, replication factor.

- What is your need for fault tolerance?
- How many consumers are going to be in each consumer group? => each consumer will get at least 1 partition
- How  much memory available on each broker? `replica.fetch.max.bytes` => around 1Mb

### 4.3 Metrics and monitoring
Kafka + Zookeeper expose metrics through JMX.

## 5. Kafka in Java
### 5.1 Java producers
`acks=all` => makes the producers to receive the ACK when all in-sync replicas acknowledged the record.
We can have a callback when the record is actually acknowledged.

### 5.2 Java Consumers
`enable.auto.commit` <- if true, the API send a notification to the kafka cluster saying until which part has been consumed in a scheduled base (every some seconds)
`consumer.Poll(Duration.ofMillis(100)`

`consumer.commitSync()` <-- to manually commit

What if you consumed some messages, but didn't commit the new offset, and the consumer process crash? => kafka has no way to know that this messages were already processed... so you will process them again.

## 6. Confluent Rest API proxy

a only confluent service, that allows to consume/produce from this REST Api proxy

### 6.1 Producing messages with REST Proxy

we make a `POST` request to `/topics/topic-name` with the payload 
```json
{
  "records": [
	  {
		  "key": "key":
		  "value": "value"
	  }
  ]
}
```

### 6.2 Consume messages with REST Proxy

We need more steps...

1. Create a consumer and consumer instance
`POST` to `/consumers/consumer-name`
```
{
  "name": "consumer_instance_name",
  "format": "json",
  "auto.offset.reset": "earliest"
}
```
2. Subscribe the consumer to a topic
`POST` to `/consumers/consumer_name/instances/consimer_instance/subscription`
```
{
	"topics": [
	  "topic_name"
	]
}
```

3. consuming messages
`GET` `/consumers/consumer_name/instances/consumer_instance_name/records`

## 7. Schema registry
Until now, we were storing strings. How we can use better (more complex and efficient formats) formats. and How we can make sure all clients can process the data.

**Schema registry** => is a central place of schemas, also versioned.

### 7.1 Creating Avro schema
Not in the video (from my memory) Avro is a binary packing protocol, one interesting thing is that also had versioning, and prevent new versions of an avro schema that is not backward compatible.

Avro schemas are represented as JSON
```
{
  "namespace": "<namespace>",
  "type": "record"
  "name": "<schema name>",
  "fields": [
	  {
		  "name": "<fieldname>",
		  "type": "<field_type>"
	  }
  ]
}
```

### 7.2 Using Avro schema in a producer

```
props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, KafkaAvroSerializer.class)
props.put(AbstractKafkaAvroSerDeConfig.SCHEMA_REGISTRY_URL_CONFIG, "http://localhost:8081")
```

Avro is able to autogenerate value classes from the avro json schema -> via avro plugin.

### 7.3 Using Avro schema in a consumer

