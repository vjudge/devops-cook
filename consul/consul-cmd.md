# consul 命令


### consul agent
```shell
# 开发模式下启动代理 (单节点)
$ consul agent -dev
# 持久化启动
# -server: 以 server 模式启动代理。如果没加，默认启动 client
# -client: 提供 HTTP、DNS、RPC 等服务，默认是127.0.0.1，不对外提供服务，如果需要则改成 0.0.0.0
# -node: 节点在集群中的名称，在一个集群中必须是唯一的，默认是该节点的主机名
# -bootstrap-expect=1: 期望的 server 节点数目，consul 一直等到指定sever数目的时候才会引导整个集群。如果没加，表明集群没有 leader
# -bind: 绑定的 IP 地址。默认0.0.0.0，将绑定到本地计算机上的所有地址，并将第一个可用的私有 IPv4 地址通告给群集的其余部分
# -data-dir: 配置数据持久化目录
# -config-dir：配置文件目录，所有以 .json 结尾的文件都会被加载，可以是服务或 Consul 自身的配置
# -join: 加入一个已经启动的 agent 的 ip 地址，可以指定多个
# -retry-join: 允许你在第一次失败后进行尝试
# -retry-interval: 两次 join 之间的时间间隔，默认是30s
# -retry-max: 尝试重复 join 的次数，默认是0，即无限次尝试
# -log-level: 日志信息级别，默认是info，还可以选择：trace、debug、info、warn、err
# -ui: 开启 web 管理界面
$ consul agent -server -bootstrap-expect=1 -data-dir=/tmp/consul -bind=127.0.0.1
```
配置文件: consul agent -config-dir $PWD/config
```json
{
  "bind_addr": "127.0.0.1",
  "datacenter": "dc1",
  "data_dir": "/tmp/consul",
  "encrypt": "7Y61t8M",
  "log_level": "INFO",
  "enable_debug": true,
  "node_name": "consul1",
  "server": true,
  "ui": true,
  "bootstrap_expect": 1,
  "leave_on_terminate": false,
  "skip_leave_on_interrupt": true,
  "rejoin_after_leave": true,
  "acl": {
    "enabled": true,
    "default_policy": "deny",
    "down_policy": "extend-cache"
  }
}
```


### consul members
查看集群成员
```shell
$ consul members
# 查看集群成员更多元数据
$ consul members -detailed
```
输出基于gossip协议，并最终一致


### consul catalog
```shell
# 查询所有注册服务
$ consul catalog services
# 显示包含的节点信息以及 TaggedAddresses 节点信息
$ consul catalog nodes --detailed
```


### consul acl
```shell
# 重新运行ACL启动命令，确认索引号
# AccessorID 相当于账号，SecretID 相当于密码，后续命令都要带上 SecretID
# 例如 consul members -token <SecretID>
# 例如 curl --location --request GET 'http://localhost:8500/v1/catalog/nodes' --header 'X-Consul-Token: <SecretID>'
$ consul acl bootstrap
# 输出全部可用的策略
$ consul acl policy list
# 查看指定策略
$ consul acl policy read -id <policy_id>
# 查看token (令牌)列表
$ consul acl token list
# 查看指定的 token 信息
$ consul acl token read -id <token_id>
```


### consul watch
watch 的类型有
* key: 监听键值对变化
* keyprefix: 监听指定前缀键值对变化
* services: 监听服务列表
* nodes: 监听节点列表
* service: 监听服务实例
* checks: 监听健康检查
* event: 监听用户事件
```shell
$ consul watch -type key -key hello echo 'hello change'
```


### consul kv put
```shell
# 添加 key-value
# 要更新现有key的值，请在相同路径上put一个值
$ consul kv put redis/config/minconns 1
$ consul kv put redis/config/maxconns 10
$ consul kv put -flags=42 redis/config/users/admin 123456

# CAS 操作提供原子键更新，需指定 -cas 选项
$ consul kv put -cas -modify-index=716 foo bar
```


### consul kv get
```shell
# 查看 key 的 value 值
$ consul kv get redis/config/minconns
# 获取更多元数据
$ consul kv get -detailed redis/config/minconns
# 递归列出所有 key 和 value，结果以字典序返回
$ consul kv get -recurse
```


### consul kv delete
```shell
# 删除某个 key 值
$ consul kv delete redis/config/minconns
# 递归删除某个前缀的 key
$ consul kv delete -recurse redis
```


### consul kv export
导出键值到本地
```shell
$ consul kv export  '' > consul.d/consul_data.json
```


### consul kv import
导入键值到 consul
```shell
$ consul kv import consul_data.json
```


### consul snapshot
快照
```shell
# 生成快照
$ consul snapshot save consul_data.snap
# 还原快照
$ consul snapshot restore consul_data.snap
```












