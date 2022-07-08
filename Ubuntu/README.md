# 常用命令


### 查看系统版本
```shell
cat /etc/issue
cat /proc/version
lsb_release -a
uname -a
```


### 查看 CPU
```shell
# 查看物理CPU个数
cat /proc/cpuinfo| grep "physical id"| sort| uniq| wc -l

# 查看每个物理CPU中core的个数(即核数)
cat /proc/cpuinfo| grep "cpu cores"| uniq

# 查看逻辑CPU的个数
cat /proc/cpuinfo| grep "processor"| wc -l

# 查看CPU信息（型号）
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
```


### 查看内存
```shell
cat /proc/meminfo
```


### 查看内核
```shell
uname -a
cat /proc/version
```


### 查看机器型号
```shell
dmidecode | grep "Product Name"
dmidecode
```















