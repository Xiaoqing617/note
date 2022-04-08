# Ubuntu安装

```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

# fastos安装

```
docker run --restart always -p 8081:8081 -d -v /var/run/docker.sock:/var/run/docker.sock -v /etc/docker/:/etc/docker/ wangbinxingkong/fast:latest
```

# 安装nginx

```
拉取官方的最新版本的镜像：docker pull nginx:latest
```

## 查看本地镜像看看是否安装成功

```
docker images
```

## 运行容器

```
docker run --name nginx-test -p 8080:80 -d nginx
--name nginx-test：容器名称。
-p 8080:80： 端口进行映射，将本地 8080 端口映射到容器内部的 80 端口。然后就可以通过IP+8080进入网页
-d nginx： 设置容器在在后台一直运行。
```

# 安装php

```
拉取官方的镜像：docker pull php
```

# 安装MySQL

```
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
-p 3306:3306 ：映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机ip:3306 访问到 MySQL 的服务。
MYSQL_ROOT_PASSWORD=123456：设置 MySQL 服务 root 用户的密码。
```

### 进入MySQL

```
#先进入容器
docker exec -it mysql bash
#登录mysql
mysql -h localhost -u root -p
```