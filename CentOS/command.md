# 常用命令

### 查看系统版本
```
cat /etc/redhat-release
# CentOS Linux release 8.4.2105
```


### 查看内核版本等信息
```
uname -a
# Linux vjudge 4.18.0-305.3.1.el8.x86_64 #1 SMP Tue Jun 1 16:14:33 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```


### 查看cpu个数
```
cat /proc/cpuinfo | grep "physical id" | uniq | wc -l
# 1
```


### 查看cpu核数
```
cat /proc/cpuinfo | grep "cpu cores" | uniq
# cpu cores	: 1
```


### 查看cpu型号
```
cat /proc/cpuinfo | grep 'model name' |uniq
# model name	: Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
```







###
