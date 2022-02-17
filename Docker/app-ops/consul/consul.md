# docker 部署 consul

### 拉取镜像
```shell
docker pull consul
```


### 查询容器 ip
```shell
docker inspect --format '{{ .NetworkSettings.IPAddress }}' consul1
```


### 启动前准备
```shell
# 保存 consul 数据
mkdir ~/_data/consul
```


### 启动server
* agent: 表示启动 agent 进程
* server: 表示 consul 为 server 模式
* client: 表示 consul 为 client 模式
* bootstrap: 表示这个节点是 Server-Leader
* ui: 启动 Web UI, 默认端口 8500
* node: 指定节点名称, 集群中节点名称唯一
* client: 绑定客户端接口地址, 0.0.0.0 表示所有地址都可以访问
```shell
docker run -d -p 8500:8500 -v /tmp/_docker/consul:/consul/data -e CONSUL_BIND_INTERFACE='eth0' --name=consul1 consul agent -server -bootstrap -ui -client='0.0.0.0'
```


### 加入其他节点
* join：表示加入到指定节点
```shell
docker run -d --name=consul2 -e CONSUL_BIND_INTERFACE=eth0 consul agent --server=true --client=0.0.0.0 --join 172.17.0.2
docker run -d --name=consul3 -e CONSUL_BIND_INTERFACE=eth0 consul agent --server=true --client=0.0.0.0 --join 172.17.0.2
docker run -d --name=consul4 -e CONSUL_BIND_INTERFACE=eth0 consul agent --server=false --client=0.0.0.0 --join 172.17.0.2
```


### 搭建 dc2
```shell
docker run -d --name=consul5 -e CONSUL_BIND_INTERFACE='eth0' consul agent -server -bootstrap-expect 3 -datacenter=dc2
docker run -d --name=consul6 -e CONSUL_BIND_INTERFACE=eth0 consul agent --datacenter=dc2 --server=true --client=0.0.0.0 --join 172.17.0.6
docker run -d --name=consul7 -e CONSUL_BIND_INTERFACE=eth0 consul agent --datacenter=dc2 --server=true --client=0.0.0.0 --join 172.17.0.6
docker run -d --name=consul8 -e CONSUL_BIND_INTERFACE=eth0 consul agent --datacenter=dc2 --server=false --client=0.0.0.0 --join 172.17.0.6
```


### 关联 dc1 和 dc2
```shell
docker exec -it consul6 consul join -wan 172.17.0.2  
```


### 查看集群下的节点
```shell
docker exec -it consul1 consul members
```


### 存储 K/V
```shell
docker exec -t node1 consul kv put user/config/connections 5
```


### 获取 K/V
```shell
docker exec -t node1 consul kv get -detailed user/config/connections
```


### 进入容器
```shell
docker exec -it consul1 /bin/sh
```





