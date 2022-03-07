# redis














### redis.config
```shell
# 远程连接
# bind 127.0.0.1 -::1
protected-mode no
# 后台启动
daemonize yes
# 设置连接密码
requirepass my-password
```


### 关闭
```shell
redis-cli shutdown
```


### 启动
```shell
redis-server ./redis.config
```


### 远程连接 redis
```shell
redis-cli -h 127.0.0.1 -p 6379 -a password
```