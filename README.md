# Learn Kafka

Kafka is a distributed system consisting of servers and clients that communicate via a high-performance TCP network protocol. It can be deployed on bare-metal hardware, virtual machines, and containers in on-premise as well as cloud environments.

source - https://kafka.apache.org/

### Important Note: If you use higher version of Kafka v2.2+, We highly recommend you to use --bootstrap-server option wherever zookeeper comes in kafka because zookeeper depedency will be removed soon from Kafka version 3.

## Kafka Commands 

<details>

  <summary> 1. How to create a topics in kafka ? </summary>
  <p>
    
 Creating the Kafka topic with 3 partitions and 3 replications. Please make sure you have adequate amount of brokers especially when you specify replication factor is 3 (you must have 3 brokers added in the cluster).
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
    
    To list all the topics in a cluster including (system genarated topics)

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
<details>

  <summary> 3. How to describe a topics in kafka ? </summary>
  <p>
    
    To describe a topic and get information about partition,replication factor 

```console
kafka-topics.sh --zookeeper localhost:2181 --describe --topic first_topic
```
  </p>
</details>   

---
<details>

  <summary> 4. How to increase the number of partitions of a Kafka topic? </summary>
  <p>
    
   Increasing the no of partitions in a Kafka is not a recommended approach to run when your consumers are relying on key-based ordering as changing the number of partitions changes the key-hashing technique.
   If data is partitioned by hash(key) % number_of_partitions then this partitioning will potentially be shuffled by adding partitions but Kafka will not attempt to automatically redistribute data in any way.
   
```console
kafka-topics.sh --zookeeper localhost:2181 --alter --topic first_topic --partitions 7
```
  </p>
</details>   

---
<details>

  <summary> 5. How to Delete a Kafka Topic </summary>
  <p>
    
    Deleting a kafka topic is fairly an easy task. You will need to set one property (delete.topic.enable=true) in broker configuration to 'true', and just issue a command to delete to topic. In case 
    if this property is not included then the topics will be 'marked for deletion' but actually it will not be deleted. Sometimes topic deletion does not happen, if you face this problem, you can use 
    a zookeeper to delete a topic.

Delete topcis from Kafka client:

```console
kafka-topics.sh --zookeeper localhost:2181 --delete --topic first_topic
```

Delete topics from ZK Client. Login to the Zookeeper CLI, and ensure the topic is not deleted by running the below command. If you dont get any error, it means topic is not yet deleted and run the rest of the commands.

```console
get /brokers/topics/<topic_name>
rmr /brokers/topics/<topic_name>
rmr /admin/delete_topics/<topic_name>
```
  </p>
</details>   

---
