# mongodb


### 进入容器
```shell
$ docker exec -it mongodb bash
```


### 登录MongoDB
```shell
$ mongo -u admin -p admin123 --authenticationDatabase yapidb
$ mongo -u admin --authenticationDatabase yapidb
$ mongo mongodb://admin:admin123@127.0.0.1:27017/yapidb
```


### 创建用户
```shell
# 不受限
db.createUser({user:"root", pwd:"root123", roles:["root"]})
# 超级管理员
db.createUser({ user: "sa", pwd: "admin123", roles: [ { role: "dbAdminAnyDatabase", db: "admin" } ]})
db.createUser({ user: "test", pwd: "qwe168", roles: [ { role: "readWrite", db: "yapidb" } ]})  
db.getSiblingDB('yapidb').createUser({user: 'test', pwd: 'qwe168', roles: [{role: 'readWrite', db: 'yapidb'}]});
```


### 删除用户
```shell
db.dropUser('test')
```


### 数据库链接
```shell
mongodb://admin:admin123@127.0.0.1:27017/admin
```







