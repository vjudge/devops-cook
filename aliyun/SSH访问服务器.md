# 访问服务器

### 创建SSH密钥对
1. 在左侧导航栏，选择网络与安全 > 密钥对。
2. 单击创建密钥对。
3. 填入必填信息，注意资源组需要关联服务器实例。
4. 重启关联的服务器实例。


### 密钥对保存
创建密钥对成功之后，会自动下载 **.pem文件。将其移动到 ~/.ssh 目录下，并修改文件权限。
```
# chmod 400 [.pem私钥文件在本地机上的存储路径]
chmod 400 ~/.ssh/vjudge.pem
```


### 直接访问服务器
```
# ssh -i [.pem私钥文件在本地机上的存储路径] root@[公网IP地址]
ssh -i ~/.ssh/vjudge.pem root@10.10.xx.xxx
```


### 配置SSH访问服务器
#### 配置SSH
在 ~/.ssh/config 文件内配置如下
```
# 输入ECS实例的别名，用户SSH远程连接。
Host ecs
# 输入ECS实例的公网IP地址。
HostName 121.196.**.**
# 输入端口号，默认为22。
Port 22
# 输入登录账号。
User root
# 输入.pem私钥文件在本机的地址。
IdentityFile ~/.ssh/ecs.pem
```

#### 访问服务器
```
ssh [ECS实例的别名]
```




















