# 下载安装压缩包

在自己要安装的目录下执行

```
wget https://github.com/cdr/code-server/releases/download/3.4.1/code-server-3.4.1-linux-x86_64.tar.gz
```

# 查看压缩包

```
ls -ash
```

# 解压

```
tar -zxvf 压缩包名字
```

# 进入解压后的文件中

```
cd 文件名
```

# 运行命令

```
export PASSWORD="你的密码" && ./code-server --host 0.0.0.0 --port 8080
```

# 更改默认密码，ip和端口

在root文件夹下找到.config文件夹进入，里面找到code-server文件夹进入，找到config.yaml进入配置

# 后台运行

```
sudo apt install screen  //下载screen
screen -S mycodeserevr  //其中mycodeserver是自己起的名字，这样就创建了一个新的screen对话
跳出一个screen，在这里执行启动code-server的命令
这样code-server就在后台运行起来，这时要退出screen，指令是:ctrl+a+d，即可返回原页面，输入指令：screen -ls，即可查看所有的screen
想要恢复某个screen，指令为screen -r screen名
删除screen的指令为：screen -X -S 25149 quit，再次screen -ls，就发现screen被删除了。
```

