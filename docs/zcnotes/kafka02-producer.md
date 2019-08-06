## 生产者发送消息逻辑
1.KafkaProducer.send() 中

1.1.拦截器拦截 interceptors.onSend(record)

1.2.1.确保 metadata 可用,即在数据发送前确保该 topic 可用.

1.2.2.序列化 key, value

1.2.3.返回分区号

1.2.4.向消息累加器 RecordAccumulator 中 追加数据

1.2.4.1.一个 TopicPartition 对应一个 Deque,没有则创建.Deque 里 放的是 ProducerBatch.

1.2.4.2.若 Deque 里有 ProducerBatch,取出最后一个 ProducerBatch 追加数据后返回.若没有 ProducerBatch, 则新建 ProducerBatch 并使用 BufferPool 分配缓冲区 再追加数据.

1.2.5.若 batch 满了,唤醒 sender 线程发送数据
