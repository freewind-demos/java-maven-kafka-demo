Java Maven Kafka Demo
=====================

Kafka是一种订阅消费服务，适用于不同系统间的数据集成。可以让人以“事件驱动”的方式来思考程序设计。

与我们自己随便手写的Observer/Listener不同，kafka在保证数据的完整性、可用性、性能各方面很好，所以被采用：
- 分布式存储
- 多机
- 数据可持久化
- 各种connector，比如直接监听文件

Kafka通常需要下载二进制边，解压并通过命令行启动。

详情参见： https://kafka.apache.org/quickstart

1. 启动环境
------

-. `bin/zookeeper-server-start.sh config/zookeeper.properties`
-. `bin/kafka-server-start.sh config/server.properties`
-. `KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"`
-. `bin/kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c config/kraft/server.properties`
-. `bin/kafka-server-start.sh config/kraft/server.properties`

2. 创建主题
-------

- `bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092`
- `bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092`

可以通过命令行写入和读取事件
-----------------------

```
$ bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
> hello
> world
```

```
$ bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
hello
world
```

我们这个例子主要是用java来实现前面用命令行写入和读取事件

Run:
1. 首先运行前面1和2中的命令，在命令行下启动kafka环境和server，并建立好`quickstart-events`主题
2. 在编辑器中依次运动 `Consumer` 和 `Producer`，并查看结果
