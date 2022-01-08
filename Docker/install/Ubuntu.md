# 安装 Docker


### 卸载旧版本
```shell
sudo apt-get remove docker docker-engine docker.io
```


### 使用 apt 预安装
```shell
sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```


### 添加软件源的 GPG 密钥
```shell
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# 官方源
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```


### 向 sources.list 中添加 Docker 软件源
```shell
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 官方源
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


### 安装 Docker
```shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
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




