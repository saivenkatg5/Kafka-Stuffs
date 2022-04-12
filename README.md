# Learn Kafka

Kafka is a distributed system consisting of servers and clients that communicate via a high-performance TCP network protocol. It can be deployed on bare-metal hardware, virtual machines, and containers in on-premise as well as cloud environments.

source - https://kafka.apache.org/

### Important Note: If you use higher version of Kafka v2.2+, We highly recommend you to use --bootstrap-server option wherever zookeeper comes in kafka because zookeeper depedency will be removed soon from Kafka version 3.

## Kafka Commands 

<details>

  <summary> 1. How to create a topics in kafka ? </summary>
  <p>
    
 Creating the Kafka topic with 3 partitions and 3 replications. Please make sure you have adequate amount of brokers especially when you specify replication facotr is 3 (you must have 3 brokers added in the cluster).
    To know the number of brokers in the kafka cluster, Login to Ambari/CM and navigate to kafka service where you will find the running brokers listed and another way is to check the broker znode in zookeeper.

```console
Kafka v2.2+:

kafka-topics.sh --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 

Kafka v2.1 or less:

kafka-topics.sh --zookeeper localhost:2181 --topic first_topic --create --partitions 3 --replication-factor 3
```
  </p>
</details>   

---
<details>

  <summary> 2. How to list a topics in kafka ? </summary>
  <p>
    
    To list all the topics in a cluster including (system genrated topics)

```console
kafka-topics.sh --zookeeper localhost:2181 --list

__consumer_offsets
first_topic
second_topic
test
```
  </p>
</details>   

---
