---
title: redis使用
date: 2021-12-02 10:46:24
tags: redis
comments: true
categories: redis使用

---
# redis使用
<!--more-->
### 持久化 : redis是内存数据库，断电既失去数据所以需要持久化

> redis持久化的两种方式：
>
> - RDB (redis database) : 生成快照，指定时间间隔内将内存中数据生成快照 snakeshot , 默认文件名称是dump.rbd
> - AOF (append  only file)：记录所有操作，启动时恢复  默认文件是 appendonly.aof

{% codeblock %}
主从复制
主机负责写入，从机负责读 一主二从
从机连接主机后，会立马复制主机的数据过来
宕机问题：一个主机多个从机，主机宕机后，从机无法写入数据，这时候可以手动的 指定其余从机的里面的一个为主机
哨兵模式：就是解决redis集群中出现了主机宕机的情况，其会根据用户指定的配置文件，自己动从 从机里面投票选举一个主机，就不用手动配置了
{% endcodeblock %}



### 乐观锁、悲观锁

概念？

 自己的理解：

- 乐观锁：很乐观，认为每次拿数据的时候别人不会修改
- 悲观锁：很悲观，认为每次拿数据的时候，别人都会吸怪

{% codeblock  lang:html %}

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=26305536&auto=1&height=66"></iframe>

{% endcodeblock %}




> redis 发布订阅	
>
> 可以用来做消息通知，即时聊天
>
> | 序号 | 命令及描述                                                   |
> | :--- | :----------------------------------------------------------- |
> | 1    | [PSUBSCRIBE pattern [pattern ...\]](https://m.runoob.com/redis/pub-sub-psubscribe.html) 订阅一个或多个符合给定模式的频道。 |
> | 2    | [PUBSUB subcommand [argument [argument ...\]]](https://m.runoob.com/redis/pub-sub-pubsub.html) 查看订阅与发布系统状态。 |
> | 3    | [PUBLISH channel message](https://m.runoob.com/redis/pub-sub-publish.html) 将信息发送到指定的频道。 |
> | 4    | [PUNSUBSCRIBE [pattern [pattern ...\]]](https://m.runoob.com/redis/pub-sub-punsubscribe.html) 退订所有给定模式的频道。 |
> | 5    | [SUBSCRIBE channel [channel ...\]](https://m.runoob.com/redis/pub-sub-subscribe.html) 订阅给定的一个或多个频道的信息。 |
> | 6    | [UNSUBSCRIBE [channel [channel ...\]]](https://m.runoob.com/redis/pub-sub-unsubscribe.html) 指退订给定的频道。 |
