# mongodb


### 进入容器
```shell
$ docker exec -it mongodb bash
```


### 登录MongoDB
```shell
$ mongo -u admin -p admin@123 --authenticationDatabase vjudgedb
$ mongo -u admin --authenticationDatabase vjudgedb
$ mongo mongodb://admin:admin@123@127.0.0.1:6030/yapidb
```


### 创建用户
```shell
db.getSiblingDB('admin')
    .createUser({
        user: 'test',
        pwd: 'qwe@168',
        roles: ['readWrite']
});
```


### 数据库链接
```shell
mongodb://test:qwe@168@127.0.0.1:6030/vjudgedb
```







