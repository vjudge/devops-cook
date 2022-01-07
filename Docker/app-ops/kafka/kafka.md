# 部署 kafka

# 启动服务
```shell
docker-compose -f multi-zk-multi-kafka.yml up -d
```


### 停止服务
```shell
docker-compose -f multi-zk-multi-kafka.yml stop
```


### 停止并删除服务
```shell
docker-compose -f multi-zk-multi-kafka.yml down
```



### 其他项目
```
https://github.com/conduktor/kafka-stack-docker-compose
```



### 进入 kafka 容器
```shell
docker exec -it kafka1 /bin/bash
```


### 进入操作目录
```shell
cd opt/kafka/
```


### 查看 topic 列表
```shell
bin/kafka-topics.sh --list --zookeeper 110.42.242.203:2181
```


### 查看 topic
```shell
bin/kafka-topics.sh --describe --zookeeper 110.42.242.203:2181 --topic test 
```


### 创建 topic
```shell
bin/kafka-topics.sh --create --zookeeper 110.42.242.203:2181 --replication-factor 3 --partitions 3 --topic test
```


### 删除 topic
```shell
bin/kafka-topics.sh --zookeeper 110.42.242.203:2181 --topic test-vj --delete 
```


### 创建生产者
```shell
# bin/kafka-console-producer.sh --broker-list 110.42.242.203:9092 --topic test-producer
```


### 创建消费者
```shell
# bin/kafka-console-consumer.sh --bootstrap-server 110.42.242.203:9092 --topic test-consumer --from-beginning
```


### 查看所有的组
```shell
bin/kafka-consumer-groups.sh --bootstrap-server 110.42.242.203:9092 --list

bin/kafka-consumer-groups.sh --command-config config/consumer.properties  --bootstrap-server 110.42.242.203:9092 --list
```


### 查看消费情况
```shell
bin/kafka-consumer-groups.sh --describe --bootstrap-server 110.42.242.203:9092 --group test-grp

bin/kafka-consumer-groups.sh --command-config config/consumer.properties  --describe --bootstrap-server 110.42.242.203:9092 --group test-grp
```



