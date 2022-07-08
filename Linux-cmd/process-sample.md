# 进程相关


### 根据进程名查看进程
```shell
ps aux | grep [process_name]
ps -ef | grep [process_name]
```


### 通过进程 id 查看占用端口
```shell
netstat -nap | grep [process_id]
```


### 通过端口号查看占用的进程 id
```shell
netstat -nap | grep [port]
```


















