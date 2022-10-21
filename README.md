# Apache-Kafka-for-absolute-beginners

# For windows - Install Single Node Cluster

```sh
E:\confluent-7.2.2>bin\windows\zookeeper-server-start.bat etc\kafka\zookeeper.properties
Classpath is empty. Please build the project first e.g. by running 'gradlew jarAll'
```

If you get the above error, add above `rem Classpath addition for core` in E:\confluent-7.2.2\bin\windows

```sh
rem classpath addition for LSB style path
if exist %BASE_DIR%\share\java\kafka\* (
	call:concat %BASE_DIR%\share\java\kafka\*
)
```

- Start Zookeeper and Kafka

```sh
E:\confluent-7.2.2>bin\windows\zookeeper-server-start.bat etc\kafka\zookeeper.properties

E:\confluent-7.2.2>bin\windows\kafka-server-start.bat etc\kafka\server.properties
```

- Load and read data

```
E:\confluent-7.2.2>bin\windows\kafka-topics.bat --create --topic test --partitions 1 --replication-factor 1 --bootstrap-server localhost:9092
Created topic test.

E:\confluent-7.2.2>bin\windows\kafka-console-producer.bat --topic test --broker-list localhost:9092 < E:\confluent-7.2.2\data\sample1.csv

E:\confluent-7.2.2>bin\windows\kafka-console-consumer.bat --topic test --bootstrap-server localhost:9092 --from-beginning
```
------------------

# Install Multi Node Cluster

rename server.properties to `server-0.properties`, also copy and create `server-1.properties` nd `erver-2.properties`. Change below 3 parameters

```
broker.id=0
listeners=PLAINTEXT://:9092
log.dirs=/tmp/kafka-logs-0
```


```sh
E:\confluent-7.2.2>bin\windows\zookeeper-server-start.bat etc\kafka\zookeeper.properties

E:\confluent-7.2.2>bin\windows\kafka-server-start.bat etc\kafka\server-0.properties

E:\confluent-7.2.2>bin\windows\kafka-server-start.bat etc\kafka\server-1.properties

E:\confluent-7.2.2>bin\windows\kafka-server-start.bat etc\kafka\server-2.properties
```

```sh
E:\confluent-7.2.2>bin\windows\kafka-topics.bat --create --topic stock-ticks --partitions 3 --replication-factor 1 --bootstrap-server localhost:9092
Created topic stock-ticks.

E:\confluent-7.2.2>bin\windows\kafka-console-producer.bat --topic stock-tics --broker-list localhost:9092 < E:\confluent-7.2.2\data\sample1.csv

E:\confluent-7.2.2>bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic stock-ticks --from-beginning --group group1

E:\confluent-7.2.2>bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic stock-ticks --from-beginning --group group1
```

![image](https://user-images.githubusercontent.com/54174687/197177834-4fa3999d-6bb2-4e88-948f-37e78c2645e0.png)

Like this we can see all partition data

```
E:\confluent-7.2.2>bin\windows\kafka-dump-log.bat --files E:\tmp\kafka-logs-0\stock-ticks-1\00000000000000000000.log
Dumping E:\tmp\kafka-logs-0\stock-ticks-1\00000000000000000000.log
Starting offset: 0
baseOffset: 0 lastOffset: 162 count: 163 baseSequence: 0 lastSequence: 162 producerId: 1001 producerEpoch: 0 partitionLeaderEpoch: 0 isTransactional: false isControl: false deleteHorizonMs: OptionalLong.empty position: 0 CreateTime: 1666348931639 size: 16339 magic: 2 compresscodec: none crc: 1974167200 isvalid: true
baseOffset: 163 lastOffset: 325 count: 163 baseSequence: 163 lastSequence: 325 producerId: 1001 producerEpoch: 0 partitionLeaderEpoch: 0 isTransactional: false isControl: false deleteHorizonMs: OptionalLong.empty position: 16339 CreateTime: 1666348931654 size: 16325 magic: 2 compresscodec: none crc: 3506398774 isvalid: true
baseOffset: 326 lastOffset: 489 count: 164 baseSequence: 326 lastSequence: 489 producerId: 1001 producerEpoch: 0 partitionLeaderEpoch: 0 isTransactional: false isControl: false deleteHorizonMs: OptionalLong.empty position: 32664 CreateTime: 1666348931686 size: 16303 magic: 2 compresscodec: none crc: 3361958651 isvalid: true
baseOffset: 490 lastOffset: 657 count: 168 baseSequence: 490 lastSequence: 657 producerId: 1001 producerEpoch: 0 partitionLeaderEpoch: 0 isTransactional: false isControl: false deleteHorizonMs: OptionalLong.empty position: 48967 CreateTime: 1666348931723 size: 16360 magic: 2 compresscodec: none crc: 3342591433 isvalid: true
baseOffset: 658 lastOffset: 820 count: 163 baseSequence: 658 lastSequence: 820 producerId: 1001 producerEpoch: 0 partitionLeaderEpoch: 0 isTransactional: false isControl: false deleteHorizonMs: OptionalLong.empty position: 65327 CreateTime: 1666348931726 size: 16381 magic: 2 compresscodec: none crc: 1583871579 isvalid: true

E:\confluent-7.2.2>
```

----------------------------------
# For MAC

```sh
@Prateeks-MacBook-Pro ~ % confluent local services start
The local commands are intended for a single-node development environment only,
NOT for production usage. https://docs.confluent.io/current/cli/index.html

Using CONFLUENT_CURRENT: /var/folders/kn/4wr9__651l37hckxvnnwt4hh0000gn/T/confluent.793004
Starting ZooKeeper
ZooKeeper is [UP]
Starting Kafka
Kafka is [UP]
Starting Schema Registry
Schema Registry is [UP]
Starting Kafka REST
Kafka REST is [UP]
Starting Connect
Connect is [UP]
Starting ksqlDB Server
ksqlDB Server is [UP]
Starting Control Center
Control Center is [UP]
```

# Create Topic

```
@Prateeks-MacBook-Pro ~ % kafka-topics --create --topic test --partitions 1 --replication-factor 1 --bootstrap-server localhost:9092
Created topic test.
```

# Load Data Through CSV file

```
@Prateeks-MacBook-Pro ~ % kafka-console-producer --topic test --broker-list localhost:9092 < /Users/prats/Downloads/Apache-Kafka-For-Absolute-Beginners-master/00-data/data/sample1.csv 
@Prateeks-MacBook-Pro ~ % 
```

# To see all messages

```sh
kafka-console-consumer --topic test --bootstrap-server localhost:9092 --from-beginning
```

