# TIDB

### Mac 部署
```shell
# 安装 TIUP
curl --proto '=https' --tlsv1.2 -sSf https://tiup-mirrors.pingcap.com/install.sh | sh
# 配置 .zshrc
export PATH=/Users/vjudge/.tiup/bin:$PATH
# 启动服务
tiup playground v4.0.16 --db 2 --pd 3 --kv 3 --monitor

# 访问 tidb
tiup client
mysql --comments --host 127.0.0.1 --port 4001 -u root -p

# 一些监控
dashboard: http://127.0.0.1:2379/dashboard (root + 空)
Prometheus: http://127.0.0.1:9090
Grafana: http://127.0.0.1:3000 (admin + admin)

# 清理集群
tiup clean --all
```