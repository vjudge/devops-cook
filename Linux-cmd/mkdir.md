# mkdir
创建目录。


### 语法
```
mkdir [参数] [目录]
```

### 常用参数
* -p : 递归创建多级目录
* -m : 建立目录的同时设置目录的权限
* -z : 设置安全上下文
* -v : 显示目录的创建过程


### sample
```
# 当前目录下创建目录
mkdir ./vjudge/linux/test
# 创建目录的同时设置目录权限
mkdir -m 700 ./vjudge/linux/test
# 同时创建多个目录
mkdir test1 test2 test3
```




