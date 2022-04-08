## 下载安装

Centos系列输入以下命令：

```
yum -y install nginx
```

Ubuntu系列输入以下命令：

```
apt -y install nginx
```

## 查看80端口是否占用

```
netstat -ntlp
```

## 运行nginx

```
nginx
```

## 网页更改

首先在home文件夹下创建文件夹比如test，用来放置页面代码

在test文件夹下创建html格式的文件并写入代码，比如test.html

在etc文件夹下找到nginx，然后在conf.d文件夹下创建.conf格式的文件，比如test.conf

在这个文件夹下写入server代码

```
server {
  server_name 47.93.222.12; // 你的域名或者 ip
  root /home/test; // 你的克隆到的项目路径
  index test.html; // 显示首页
  location ~* ^.+\.(jpg|jpeg|gif|png|ico|css|js|pdf|txt){
    root /home/test;
  } // 静态文件访问
}
```

