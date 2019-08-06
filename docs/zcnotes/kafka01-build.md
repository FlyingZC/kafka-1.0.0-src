# kafka idea 源码阅读环境搭建

选择 kafka-1.0 版本

## 安装 Gradle
https://gradle.org/releases/

配置环境变量
E:\soft\gradle-5.5\bin

配置 GRADLE_HOME

不要使用最新的 gradle5,gradle idea 执行时会不兼容报错.用 4 即可.

## 安装scala
- 下载scala
http://downloads.typesafe.com/scala/2.11.8/scala-2.11.8.msi

- idea安装scala插件

## gradle idea
kafka项目导入idea,gradle可能会失败.

在 build.gradle 中配置
```
repositories {
    maven {
        url "https://maven.aliyun.com/nexus/content/groups/public"
    }
```

执行`gradle idea`.

若 build 失败,通过 `gradle idea --debug --stacktrace`具体解决.

## 验证
- 启动zk

- 启动 kafka.Kafka
``` 
name: kafka-standalone
Main class: kafka.Kafka
vm options : -Dlog4j.configuration=file:config/log4j.properties
program arguments : config/server.properties
module : core 或 core-main.
控制台打日志,配置 VM options : -Dlog4j.configuration=file:config/log4j.properties
```

- 启动 kafka.tools.ConsoleProducer
```
Program arguments : --topic zp --broker-list localhost:9092
指定 topic 和 broker
module : core_test
```

- 启动 kafka.tools.ConsoleConsumer
```
Program arguments : --topic zp --zookeeper localhost:2181
module : core_test
```