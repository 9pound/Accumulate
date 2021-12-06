# Docker概述

It works on my machine



Linux 容器不是模拟一个完整的操作系统，而是对进程进行隔离

容器有点像轻量级的虚拟机，能够提供虚拟化的环境，但是成本开销小得多。





Docker 是什么？

Docker 属于 Linux 容器的一种封装，提供简单易用的容器使用接口。

Docker 将应用程序与该程序的依赖，打包在一个文件里面。

运行这个文件，就会生成一个虚拟容器。程序在这个虚拟容器里运行，就好像在真实的物理机上运行一样。有了 Docker，就不用担心环境问题。



基本概念:

- **镜像（Image）**：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
- **容器（Container）**：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
- **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。



常用命令：

验证docker 是否安装成功

- docker version
- docker info

启动docker

```# service 命令的用法
# service 命令的用法
$ sudo service docker start

# systemctl 命令的用法
$ sudo systemctl start docker
```

拉取镜像

docker image pull hello-world

查看镜像

docker image  ls

删除镜像

docker image rm



运行

```bash
docker container run hello-world

docker container kill [containID]

# 列出本机正在运行的容器
$ docker container ls

# 列出本机所有容器，包括终止运行的容器
$ docker container ls --all


# 删除指定的容器文件
$ docker container rm [containerID]
```









退出容器

 exit 命令

使用 CTRL+D 



参考：[Docker 入门教程 - 阮一峰的网络日志 (ruanyifeng.com)](https://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)