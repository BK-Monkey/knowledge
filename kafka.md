# KAFKA 常用命令
## 启动
```
bin/zookeeper-server-start.sh -daemon config/zookeeper.properties 
bin/kafka-server-start.sh -daemon config/server.properties 

bin/zookeeper-server-start.sh -daemon config/zookeeper.properties 
bin/kafka-server-start.sh -daemon config/server.properties 
```
***

## 停止
```
bin/kafka-server-stop.sh 
bin/zookeeper-server-stop.sh 
```

***
## 创建主题
```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 8 --topic {topic name}
```
***
## 列出主题
```
bin/kafka-topics.sh --list --zookeeper ${ZK_BIND}
```
***
## 快速生产消息
```
bin/kafka-console-producer.sh --topic {topic} --bootstrap-server localhost:9092
```
***
## 查看消费消息
```
bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list
bin/kafka-consumer-groups.sh --describe --bootstrap-server 127.0.0.1:9092 --group quickstart-events
```
***
## 查看消费者列表
```

```
***
## 消费数据
```
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
```
***

