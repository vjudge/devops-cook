# 部署 rabbitmq

### 获取镜像
```shell
docker pull rabbitmq:management
```

### 启动
```shell
docker run -d -p 5672:5672 -p 15672:15672 --name rabbitmq rabbitmq:management
```




