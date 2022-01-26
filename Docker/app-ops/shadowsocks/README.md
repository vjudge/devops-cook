# Shadowsocks




### docker 部署
```shell
docker run -e PASSWORD=test2021 -p 9102:8388 -p 9102:8388/udp -m aes-256-cfb -s 0.0.0.0 -d shadowsocks/shadowsocks-libev
```




