# 基于消息传递机制的并发方式

计算机的并发模型有很多，其中一种是基于消息传递机制的并发方式。这种并发方式的特点是，不同的并发执行体之间通过消息传递来进行通信，而不是通过共享内存。
这其中有两个著名的并发模型，分别是Actor模型和CSP模型。
但是我先讨论一下消息传递机制的一些基本组成，然后我们就可以看到Actor模型和CSP模型的异同了。

## 消息传递机制的基本组成

消息传递机制的需要有两种实体，一种是发送或接收信息的process，另一种是存储消息的message queue。
这两种实体之间的关系是，process可以向message queue发送消息，也可以从message queue接收消息。

message queue的实现也有两种，一种是blocking的，一种是non-blocking的。

于是process和message queue的组合关系就有下表：

| 特征                                     |   |   |
|:---------------------------------------|:-:|:-:|
| 1个 process 可以 send to 几个 queue      | n | 1 |
| 1个 process 可以 receive from 几个 queue | n | 1 |
| 1个 queue 可以 sent from 几个 process    | n | 1 |
| 1个 queue 可以 received to 几个 process  | n | 1 |
| send 操作是否阻塞                        | ✓ | x |
| receive 操作是否阻塞                     | ✓ | x |

## 几种并发模型的异同

对于上表，Actor模型是(n, 1, n, 1, x, x)，CSP模型是(n, n, n, n, ✓, ✓)。

于是，理论上应该还存在一种模型的特征组合是(n, n, n, n, x, x)。
这种模型的特征是，process可以向多个message queue发送消息，也可以从多个message queue接收消息。
一个message queue可以被多个process发送消息，也可以被多个process接收消息。
而且send和receive操作都是non-blocking的。
