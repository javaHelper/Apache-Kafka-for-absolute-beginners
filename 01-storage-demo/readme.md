E:\Books\Apache-Kafka-for-absolute-beginners\01-storage-demo>%KAFKA_HOME%\bin\windows\zookeeper-shell.bat localhost:2181
Connecting to localhost:2181
Welcome to ZooKeeper!
JLine support is disabled

WATCHER::

WatchedEvent state:SyncConnected type:None path:null

ls /
[admin, brokers, cluster, config, consumers, controller, controller_epoch, feature, isr_change_notification, latest_producer_id_block, leadership_priority, log_dir_ev
ent_notification, zookeeper]
ls /brokers
[ids, seqid, topics]
ls /brokers/topics
[_confluent-command, invoice]
ls /brokers/ids
[0, 1, 2]

# Down the two brokers
ls /brokers/ids
[2]

# Up all brokers

