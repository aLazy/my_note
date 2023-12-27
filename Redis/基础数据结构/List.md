## 内部实现
List底层数据结构是由双向链表或者压缩列表实现的。
<font color=blue>在redis3.2之后，List数据结构底层只由quicklist实现，替代了双向链表和压缩列表</font>在redis7.0之后底层数据结构为listpack。

## 常用命令
```
//将一个或多个value插入到key列表的表头
LPUSH key value [value ...]
//将一个或多个value插入到key列表的表尾
RPUSH key value [value ...]

//弹出表头元素，并返回该元素
LPOP key
//弹出表尾元素并返回该元素
RPOP key

//返回指定区间的元素
LRANGE key start stop

//阻塞式  弹出元素，timeout=0表示一致阻塞
BLPOP key [key ...] timeout
BRPOP key [key ...] timeout
```

## 应用场景
1. 消息队列
    1. 消息保序
    生产者使用lpush向队列中增加消息，消费者使用rpop主动从队列中获取消息。
    **性能风险点**：消费者需要使用一个循环，不断读取消息，会带来cpu的消耗。可以使用brpop进行阻塞式读取，节省cpu开销
    2. 处理重复消息：
    生产者在发送消息时给消息生成一个全局唯一的id。消费需要在接收消息时将id号保留，并查询，以保证消息的不重复
    3. 消息的可靠性
    消费者在读取消息后，消息队列将删除该消息。当消费者读取后出现了故障或者宕机，将会导致该条未处理完成的消息丢失。
    因此需要使用BRPOPLPUSH命令，在读取消息时对消息进行备份。
## List的缺陷
1. List不支持多个消费者消费同一条消息。不支持消费组