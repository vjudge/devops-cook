# tmux


### 安装
```shell
# Ubuntu 或 Debian
$ sudo apt-get install tmux

# CentOS 或 Fedora
$ sudo yum install tmux

# Mac
$ brew install tmux
```


### 列出所有快捷键，及其对应的 Tmux 命令
```shell
tmux list-keys
```


### 列出所有 Tmux 命令及其参数
```shell
tmux list-commands
```


### 查看所有会话
```shell
tmux ls
# or
tmux list-session
```


### 列出当前所有 Tmux 会话的信息
```shell
tmux info
```


### 新建会话
```shell
tmux new -s <session-name>
```


### 接入某个会话
```shell
# 使用会话编号
tmux attach -t 0

# 使用会话名称
tmux attach -t <session-name>
```


### 重命名某个会话
```shell
tmux rename-session -t 0 <new-name>
```


### 切换会话
```shell
# 使用会话编号
tmux switch -t 0

# 使用会话名称
tmux switch -t <session-name>
```


### 退出
按下 Ctrl+d 或者显式输入 exit 命令，就可以退出 Tmux 窗口



### 杀死某个会话 
```shell
# 使用会话编号
tmux kill-session -t 0

# 使用会话名称
tmux kill-session -t <session-name>
```


### 快捷键
* Ctrl+b d : 分离当前会话
* Ctrl+b s : 列出所有会话
* Ctrl+b $ : 重命名当前会话



### 分离会话
在 Tmux 窗口中，按下 Ctrl+b d 或者输入 tmux detach 命令，就会将当前会话与窗口分离
```shell
tmux detach
```


### 划分窗口
```shell
# 划分上下两个窗格
$ tmux split-window

# 划分左右两个窗格
$ tmux split-window -h
```


### 交换窗格位置
```shell
# 当前窗格上移
$ tmux swap-pane -U

# 当前窗格下移
$ tmux swap-pane -D
```


### 窗格快捷键
* Ctrl+b % : 划分左右两个窗格
* Ctrl+b " : 划分上下两个窗格
* Ctrl+b <arrow key> : 光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓
* Ctrl+b ; : 光标切换到上一个窗格
* Ctrl+b o : 光标切换到下一个窗格
* Ctrl+b { : 当前窗格与上一个窗格交换位置
* Ctrl+b } : 当前窗格与下一个窗格交换位置
* Ctrl+b Ctrl+o : 所有窗格向前移动一个位置，第一个窗格变成最后一个窗格
* Ctrl+b Alt+o : 所有窗格向后移动一个位置，最后一个窗格变成第一个窗格
* Ctrl+b x : 关闭当前窗格
* Ctrl+b ! : 将当前窗格拆分为一个独立窗口
* Ctrl+b z : 当前窗格全屏显示，再使用一次会变回原来大小
* Ctrl+b Ctrl+<arrow key> : 按箭头方向调整窗格大小
* Ctrl+b q : 显示窗格编号



### 新建窗口
```shell
tmux new-window

# 新建一个指定名称的窗口
tmux new-window -n <window-name>
```


### 切换窗口
```shell
# 切换到指定编号的窗口
tmux select-window -t <window-number>

# 切换到指定名称的窗口
tmux select-window -t <window-name>
```


### 重命名窗口
```shell
tmux rename-window <new-name>
```


### 重命名窗口
* Ctrl+b c : 创建一个新窗口，状态栏会显示多个窗口的信息
* Ctrl+b p : 切换到上一个窗口（按照状态栏上的顺序）
* Ctrl+b n : 切换到下一个窗口
* Ctrl+b <number> : 切换到指定编号的窗口，其中的<number>是状态栏上的窗口编号
* Ctrl+b w : 从列表中选择窗口
* Ctrl+b , : 窗口重命名










