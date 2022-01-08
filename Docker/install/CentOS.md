# 安装 Docker


### 卸载旧版本
```shell
sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux docker-engine-selinux docker-engine
```


### 预安装
```shell
sudo yum install -y yum-utils
```


### 添加 yum 软件源
```shell
sudo yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sudo sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

# 官方源
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```


### 安装 Docker
```shell
sudo yum install docker-ce docker-ce-cli containerd.io
```


### 启动 docker
```shell
sudo systemctl enable docker
sudo systemctl start docker
```


### 建立用户组
```shell
sudo groupadd docker
sudo usermod -aG docker $USER
```


### 测试 docker 安装是否正确
```shell
docker run --rm hello-world
```




