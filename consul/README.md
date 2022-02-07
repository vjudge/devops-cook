# [Consul](https://www.consul.io)
Consul 是 HashiCorp 公司推出的一个用于实现分布式系统的服务发现与配置工具。Consul 使用 Go 语言编写，具有天然可移植性，支持多平台部署

Consul 内置了服务注册与发现、分布一致性协议实现、dns 解析、健康检查、Key/Value 存储、多数据中心方案

Consul 是分布式的、高可用的、横向扩展的。consul 特性
* 服务发现: 通过 DNS 或者 HTTP 接口使服务注册和服务发现变的很容易
* 健康检查: Consul 提供了健康检查的机制，从简单的服务端是否返回 200 的响应代码到较为复杂的内存使用率是否低于 90%
* key/value 存储: 一个用来存储动态配置的系统。提供简单的HTTP接口，可以在任何地方操作
* 多数据中心: 无需复杂的配置，即可支持任意数量的区域
* Web UI : Consul 提供了一个漂亮的 Web 界面，可以轻松使用和管理 consul 中的所有功能


### client 模式
客户端模式。是consul节点的一种模式，所有注册到当前节点的服务会被转发到SERVER，本身是不持久化这些信息


### server 模式
服务端模式。表明是个 server，功能和 client 一样，但它会把所有的信息持久化的本地，这样遇到故障，信息是可以被保留的
* server-leader: 负责同步注册的信息给其它的SERVER，同时也要负责各个节点的健康监测


### Consul agent
Consul安装之后，代理必须运行。 代理可以在服务器或客户端模式下运行


### Consul 命令
members命令的输出基于gossip协议，并最终一致
```shell
# 开发模式下启动代理
consul agent -dev
# 退出代理: 节点上的服务和健康检查全部注销
# 在当前节点执行
consul leave
# 可在其他任意节点执行
consul force-leave [node-id]
# 持续打印当前 Consul 的日志信息
consul monitor

# 查看集群成员
consul members
# 查看集群成员更多元数据
consul members -detailed

# 查询所有注册服务
consul catalog services

# 反注册: 删除注册的服务
consul services deregister -id=app-serv
```

在任何时候，当地代理所看到的可能与服务器上的状态不完全一致。要获得完全一致，可以使用 HTTP API 将 HTTP 请求转发给 Consul 服务器
```shell
curl http://localhost:8500/v1/catalog/nodes
```


### 注册服务
服务可以通过提供服务定义或通过对 HTTP API 进行适当的调用来注册

服务定义是注册服务最常用的方式
```shell
# PUT
curl http://127.0.0.1:8500/v1/agent/service/register -X PUT -i -H "Content-Type:application/json" -d '{
  "ID": "userServiceId",  
  "Name": "userService",
  "Tags": [
    "primary",
    "v1"
  ],
  "Address": "127.0.0.1",
  "Port": 9000,
  "EnableTagOverride": false,
  "Check": {
    "DeregisterCriticalServiceAfter": "90m",
    "HTTP": "http://www.baidu.com",
    "Interval": "10s"
  }
}'
```
```json
// 参数说明
{
  "ID": "userServiceId", //服务id
  "Name": "userService", //服务名
  "Tags": [              //服务的tag，自定义，可以根据这个tag来区分同一个服务名的服务
    "primary",
    "v1"
  ],
  "Address": "127.0.0.1",//服务注册到consul的IP，服务发现，发现的就是这个IP
  "Port": 8000,          //服务注册consul的PORT，发现的就是这个PORT
  "EnableTagOverride": false,
  "Check": {             //健康检查部分
    "DeregisterCriticalServiceAfter": "90m",
    "HTTP": "http://www.baidu.com", //指定健康检查的URL，调用后只要返回20X，consul都认为是健康的
    "Interval": "10s"   //健康检查间隔时间，每隔10s，调用一次上面的URL
  }
}
```


### 服务发现
```shell
# 查询注册的服务
curl http://localhost:8500/v1/catalog/services
# passing=false，会自动过滤掉不健康的服务，包括本身不健康的服务和不健康的Consul节点上的服务
curl http://127.0.0.1:8500/v1/catalog/service/app-serv?passing=false
```


### Consul 集群
当一个Consul代理启动时，它不知道任何其他节点：它是一个孤立的集群

要加入现有的集群，只需要知道一个现有的成员。 代理加入后，会与该成员通讯，并迅速发现集群中的其他成员。 Consul 代理可以加入任何其他代理，而不仅仅是服务器模式下的代理

集群中的每个节点都必须具有唯一的名称。 默认情况下，Consul使用机器的主机名


#### 启动代理
* -node: 指定节点名称，默认使用机器的主机名
* -bind: 侦听地址，必须可以被集群中的所有其他节点访问。虽然绑定地址不是绝对必要的，但最好提供一个
* -server: 作为集群中的服务器
* -bootstrap-expect: 向服务器提示期望加入的其他服务器节点的数量。此选项可以延迟复制日志的引导，直到预期数量的服务器成功加入
* -enable_script_checks: 是否可以启用可以执行外部脚本的运行状况检查
* -config-dir: 标记可以找到服务和检查定义的位置
* -join: 启动的时候，要加入到哪个集群内
* -ui: 设置自带的UI
```shell
consul agent -server -bootstrap-expect=1 -data-dir=/tmp/consul -node=agent-one -bind=192.168.100.101 -enable-script-checks=true -config-dir=/etc/consul.d
```


### 健康检查
健康检查是服务发现的关键组件，可以防止使用不健康的服务

#### 查找失败的检查
```shell
curl http://localhost:8500/v1/health/state/critical
# DNS 查询
dig @127.0.0.1 -p 8600 web.service.consul
```


### KV Data
```shell
# 添加 key-value
# 要更新现有key的值，请在相同路径上put一个值
consul kv put redis/config/minconns 1
consul kv put redis/config/maxconns 10
consul kv put -flags=42 redis/config/users/admin 123456

# 查看 key 的 value 值
consul kv get redis/config/minconns
# 获取更多元数据
consul kv get -detailed redis/config/minconns

# 递归列出所有 key 和 value，结果以字典序返回
consul kv get -recurse

# 删除某个 key 值
consul kv delete redis/config/minconns
# 递归删除某个前缀的 key
consul kv delete -recurse redis

# CAS 操作提供原子键更新，需指定 -cas 选项
consul kv put -cas -modify-index=716 foo bar
```






















