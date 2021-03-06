---
title: 消息队列
categories: Java
tags: 面试
description: RabbitMQ系列
abbrlink: fec99276
date: 2019-07-30 09:33:26
keywords:
---

## 1.RabbitMQ使用场景

1. 跨系统的**异步通信**。所有需要异步交互的地方都可以使用消息队列。

2. **多个应用之间的耦合**。由于消息是平台无关和语言无关的，而且语义上也不再是函数调用，因此更适合作为多个应用之间的松耦合的接口。基于消息队列的耦合，不需要发送方和接收方同时在线。在企业应用集成（EAI）、文件传输、共享数据库、消息队列、远程过程调用都可以作为集成的方法。

3. **应用内的同步变异步**。比如订单处理，就可以由前端应用将订单信息放到队列，后端应用从队列里依次获得消息处理，高峰时的大量订单可以积压在队列里慢慢处理掉。由于同步通常意味着阻塞，而大量线程的阻塞会降低计算机的性能。

4. **消息驱动的架构（EDA）**，系统分解为消息队列、消息制造者和消息消费者，一个处理流程可以根据需要拆成多个阶段（Stage），阶段之间用队列连接起来，前一个阶段处理的结果放入队列，后一个阶段从队列中获取消息继续处理。

5. **应用需要更灵活的耦合方式**。如发布订阅，比如可以指定路由规则。

6. **跨局域网，甚至跨城市的通讯（CDN行业）**。比如北京机房与广州机房的应用程序的通信。

## 2.RabbitMQ重要角色

RabbitMQ 中重要的角色有：生产者、消费者和代理：

- 生产者：消息的创建者，负责创建和推送数据到消息服务器；
- 消费者：消息的接收方，用于处理数据和确认消息；
- 代理：就是 RabbitMQ 本身，用于扮演“快递”的角色，本身不生产消息，只是扮演“快递”的角色。

## 3.RabbitMQ的重要组件

- ConnectionFactory（连接管理器）：应用程序与Rabbit之间建立连接的管理器，程序代码中使用。
- Channel（信道）：消息推送使用的通道。
- Exchange（交换器）：用于接受、分配消息。
- Queue（队列）：用于存储生产者的消息。
- RoutingKey（路由键）：用于把生成者的数据分配到交换器上。
- BindingKey（绑定键）：用于把交换器的消息绑定到队列上。

## 4.RabbitMQ中vhost的作用

　　vhost 可以理解为**虚拟broker** ，即 mini-RabbitMQ  server。其内部均含有独立的 queue、exchange 和 binding 等。但最重要的是其拥有**独立的权限系统**，可以做到 vhost 范围的用户控制。当然，从 RabbitMQ 的全局角度，vhost 可以作为不同权限隔离的手段（一个典型的例子就是不同的应用可以跑在不同的 vhost 中）。 

## 5.RabbitMQ的消息发送原理

　　首先客户端必须连接到 RabbitMQ服务器才能发布和消费消息。客户端和 rabbit server 之间会创建一个 tcp 连接，一旦 tcp 打开并通过了认证（用户名和密码匹配），客户端和 RabbitMQ就创建了一条 amqp 信道（channel）。信道是创建在“真实” tcp 上的虚拟连接，amqp 命令都是通过信道发送出去的，每个信道都会有一个唯一的 id，不论是发布消息，订阅队列都是通过这个信道完成的。

## 6.RabbitMQ如何保证消息的稳定性

- 提供了事务的功能。
- 通过将 channel 设置为 confirm（确认）模式。

## 7.RabbitMQ如何避免消息丢失

1. 消息持久化
2. ACK确认机制
3. 设置集群镜像模式
4. 消息补偿机制

　　其实个人感觉，RabbitMQ就是通信协议的翻版，可能这样子说有点过了，但是不得不说的是，RabbitMQ里面的很多东西借鉴了通信协议的思想、也用了数据结构、数据库的一些技术，所以再一次证明了学习底层原理有多么重要！

## 8.保证消息持久化成功的条件

1. 声明队列必须设置持久化， durable 设置为 true。
2. 消息推送投递模式必须设置持久化，deliveryMode 设置为 2（持久）。
3. 消息已经到达持久化交换器。
4. 消息已经到达持久化队列。

以上四个条件都满足才能保证消息持久化成功。

## 9.RabbitMQ持久化缺点

　　持久化的缺点就是降低了服务器的吞吐量。因为使用的是磁盘而非内存存储，从而降低了吞吐量。可尽量使用 ssd 硬盘来缓解吞吐量的问题。

## 10.RabbitMQ的广播类型

三种广播模式：


1. fanout：所有bind到此exchange的queue都可以接收消息（纯广播，绑定到RabbitMQ的接受者都能收到消息）；
2. direct：通过routingKey和exchange决定的那个唯一的queue可以接收消息；
3. topic：所有符合routingKey(此时可以是一个表达式)的routingKey所bind的queue可以接收消息；

## 11.RabbitMQ如何实现延迟消息队列

1. 通过消息过期后进入死信交换器，再由交换器转发到延迟消费队列，实现延迟功能；
2. 使用 RabbitMQ-delayed-message-exchange 插件实现延迟功能。

## 12.RabbitMQ集群作用

集群主要有以下两个用途：

1. 高可用：某个服务器出现问题，整个 RabbitMQ还可以继续使用；

2. 高容量：集群可以承载更多的消息量。

## 13.RabbitMQ节点的类型

1. 磁盘节点：消息会存储到磁盘。

2. 内存节点：消息都存储在内存中，重启服务器消息丢失，性能高于磁盘类型。

## 14.RabbitMQ每个节点是否是其他节点的完整拷贝

不是，原因有以下两个：

1. 存储空间的考虑：如果每个节点都拥有所有队列的完全拷贝，这样新增节点不但没有新增存储空间，反而增加了更多的冗余数据；
2. 性能的考虑：如果每条消息都需要完整拷贝到每一个集群节点，那新增节点并没有提升处理消息的能力，最多是保持和单节点相同的性能甚至是更糟。

## 15.RabbitMQ集群中唯一一个磁盘节点崩溃了会发生什么情况

如果唯一磁盘的磁盘节点崩溃了，不能进行以下操作：

- 不能创建队列
- 不能创建交换器
- 不能创建绑定
- 不能添加用户
- 不能更改权限
- 不能添加和删除集群节点

唯一磁盘节点崩溃了，集群是可以保持运行的，但你不能更改任何东西。

## 16.RabbitMQ对集群节点停止顺序有要求吗

　　RabbitMQ对集群的停止的顺序是有要求的，应该先关闭内存节点，最后再关闭磁盘节点。如果顺序恰好相反的话，可能会造成消息的丢失。

