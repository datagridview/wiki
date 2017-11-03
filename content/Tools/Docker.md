---
title: "Docker"
date: 2017-08-12 11:36
updated: 2017-08-12 11:36
tag: Tools
collection: 虚拟化
log: "html中的JavaScript"
---

[TOC]

以下命令以shell为平台。

## 参考网站

* [docker官网](https://docs.docker.com/)
* [runoob手册](http://www.runoob.com/docker/docker-command-manual.html)
* [docker样例教学](https://docs.docker.com/samples/)

## Docker容器生命周期

### docker run操作

```shell
docker run [option] image [command] [arg]

-a stdin/stdout/stderr		#标准输入输出类型
-d							#后台守护进程
-i							#交互，与-t连用
-t							#分配伪终端
--name						#命名
--dns						#指定域名解析器
-h							#指定hostname
-m							#容器使用内存最大值
```

### docker其他生命周期操作

```shell
docker start/stop/restart [option] container	#开始/停止/重启容器
docker kill [option] container					#杀死容器
docker rm [option] container					#移除容器
docker pause/unpause [option] container			#挂起/就绪
docker exec -i -t myngix /bin/sh /root/myexec.sh#执行操作（例）
```

## 对于容器宏观操作

```shell
docker ps [option] 
-a		#列出所有
--format#模板文件
-f		#过滤
-l		#最近

docker inspect [option] container/image	#返回容器/镜像元数据
docker top [option] container			#正在运行的进程
docker attach [option] container		#链接正在运行的容器
docker events [option]					#获取实时事件
docker logs [option] container			#日志
docker export [option] container -o		#输出到文件
docker port [option] container			#端口映射
```

`3306/TCP->0.0.0.0:3306`意指docker 开放了3306端口映射到了主机的3306端口上。

## 容器rootfs操作

```shell
docker commit [option] container [name:tag]
-a		#作者
-c		#dockfile指令
-m		#说明
-p		#commit时，containers暂停

docker cp X Y
docker diff container	#文件更改
```

## 仓库交互

```shell
docker login -u xx -p xx	#登陆
docker logout				#登出
docker push [name:tag]		#推送
docker pull [name:tag]		#拉回本地
docker search [image]		#搜索镜像
```

## 本地镜像管理

### 查看本地镜像
```shell
docker images [options] [repo[]]
-a			#本地所有
-f			#满足条件
--no-trunc	#完整镜像信息
```
### 删除镜像
```shell
docker rmi [options] image [image..]
-f			#强制删除
```
### 打标签
```shell
docker tag image[:tag] repo/tag
#ex.docker tag ubuntu:15.10 he/ubuntu:v3
```

### 创建镜像
```shell
docker build [OPTIONS] PATH | URL | -
#ex.docker build -t runoob/ubuntu:v1
#ex.docker build github.com/creack/docker-firefox
-f 			#指定要使用的Dockerfile路径
```
`docker build`命令具体细节[runoob](http://www.runoob.com/docker/docker-build-command.html)
### 镜像操作历史记录
```shell
docker history [OPTIONS] IMAGE
#docker history he/ubuntu:v3
```

### 其他

```shell
docker save [options] IMAGE [IMAGE..]	#归档文件
# docker save -o my_ubuntu_v3.tar he/ubuntu:v3
docker import [options] file|URL|- [repo[:tag]]#从归档创建镜像
# docker import  my_ubuntu_v3.tar he/ubuntu:v4 
docker info
docker version
```

## TODO

* dockefile语法和实践
* docker集群实践问题