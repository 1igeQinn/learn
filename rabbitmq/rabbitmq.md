rabbitmq

work queue  多个消费队列，来处理发过来的消息。
Round-robin dispatching[循环分发，平均分配到每个worker？]
message acknowledgment 即消息消费者在接收处理完消息之后会返回一个消息告知可以删除消息，如果消费者在处理过程

                                        
rabbitmq 不允许重新定义一个已经存在的队列【具有不同的属性】 如：
原来建立了一个叫 hello[不持久化]的队列 就不能在建立一个hello【持久化的】队列

## publish subscribe 订阅发布
 exchange 的类型 有direct topic header fanout