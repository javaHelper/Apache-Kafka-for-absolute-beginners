# Apache-Kafka-for-absolute-beginners

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

@Prateeks-MacBook-Pro ~ % kafka-topics --create --topic test --partitions 1 --replication-factor 1 --bootstrap-server localhost:9092
Created topic test.

@Prateeks-MacBook-Pro ~ % kafka-console-producer --topic test --broker-list localhost:9092 < /Users/prats/Downloads/Apache-Kafka-For-Absolute-Beginners-master/00-data/data/sample1.csv 
@Prateeks-MacBook-Pro ~ % 

```
