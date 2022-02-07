# consul 原理

### consul 内部原理
consul 官网图
![consul](https://github.com/vjudge/devops-cook/blob/master/consul/consul-theory.png)

* 工作架构通过 using raft 算法工作
* Consul 支持多数据中心，通过 Internet 互联。为了提高通信效率，只有 server 节点加入跨数据中心通信
* Consul 分为 Client 和 Server 两种节点，所有节点也被称为 Agent
  * Server 节点保存数据
    * Server 的数量推荐是 3 个或者 5 个，在 Leader 挂掉的时候会启动选举机制产生一个新的 Leader
    * Server 节点有一个 Leader 和多个 Follower，Leader 节点会将数据同步到Follower 
  * Client负责健康检查及转发数据请求到 Server
  * 集群内数据的读写请求既可以直接发到Server，也可以通过Client使用RPC转发到Server，请求最终会到达Leader节点
    * 集群内数据的读写和复制都是通过TCP的8300端口完成
* 集群内的 Consul 节点通过 gossip 协议（流言协议）维护成员关系
  * 单个数据中心的流言协议同时使用 TCP 和 UDP 通信，并且都使用 8301 端口
  * 跨数据中心的流言协议也同时使用 TCP 和 UDP 通信，端口使用 8302


### 协议类型
Consul 有两种协议类型
* Consensus Protocol (共识协议)
  * 提供 CAP 定理所描述的一致性。该协议基于 Raft 算法
  * 在实现共识协议时，使用 Raft 算法，其中 raft 节点始终处于以下三种状态中的任何一种：Follower、Candidate 或 Leader
* Gossip Protocol (八卦协议)
  * 用于管理成员资格、跨集群发送和接收消息
  * gossip 协议的使用有两种方式 : WAN(无线局域网)和 LAN(局域网)



### Raft 算法
Raft 是一种用于管理复制日志的共识算法。它依赖于 CAP 定理 的原理，该定理指出，在存在网络分区的情况下，必须在一致性和可用性之间做出选择

Raft Cluster 包含多个服务器，通常为奇数























