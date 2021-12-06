# Docker常用命令

#### 基础

##### 验证是否安装成功

```bash
$ docker version
# 或者
$ docker info
```

##### 启动Docker服务

```bash
# service 命令的用法
$ sudo service docker start

# systemctl 命令的用法
$ sudo systemctl start docker
```

#### Image相关

```bash
# 列出本机的所有 image 文件。
$ docker image ls

# 删除 image 文件
$ docker image rm [imageName]
```



##### 抓取 image 文件

```bash
# library是默认组
docker image pull hello-world
```







#### Container相关



##### 运行 image 文件

```bash
从 image 文件，生成一个正在运行的容器实例。
docker container run hello-world
```

命令是新建容器，每运行一次，就会新建一个容器。同样的命令运行两次，就会生成两个一模一样的容器文件。

```bash
$ docker container run \
  -d \
  --rm \
  --name wordpressdb \
  --env MYSQL_ROOT_PASSWORD=123456 \
  --env MYSQL_DATABASE=wordpress \
  mysql:5.7
```

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

- `-d`：容器启动后，在后台运行。
- `--rm`：容器终止运行后，自动删除容器文件。
- `--name wordpressdb`：容器的名字叫做`wordpressdb`
- `--env MYSQL_ROOT_PASSWORD=123456`：向容器进程传入一个环境变量`MYSQL_ROOT_PASSWORD`，该变量会被用作 MySQL 的根密码。
- `--env MYSQL_DATABASE=wordpress`：向容器进程传入一个环境变量`MYSQL_DATABASE`，容器里面的 MySQL 会根据该变量创建一个同名数据库（本例是`WordPress`）。
- `--rm`：停止运行后，自动删除容器文件。
- `--name wordpress`：容器的名字叫做`wordpress`。
- `--volume "$PWD/":/var/www/html`：将当前目录（`$PWD`）映射到容器的`/var/www/html`（Apache 对外访问的默认目录）。因此，当前目录的任何修改，都会反映到容器里面，进而被外部访问到。
- `--link wordpressdb:mysql`，表示 WordPress 容器要连到`wordpressdb`容器，冒号表示该容器的别名是`mysql`。
- `-p 127.0.0.2:8080:80`：将容器的 80 端口映射到`127.0.0.2`的`8080`端口。
- `--volume "$PWD/wordpress":/var/www/html`：将容器的`/var/www/html`目录映射到当前目录的`wordpress`子目录。

重复使用容器

##### **docker container start**  

重复使用容器文件



##### 

##### 

```bash
# 列出本机正在运行的容器
$ docker container ls

# 列出本机所有容器，包括终止运行的容器
$ docker container ls --all


$ docker container kill [containID]

$ docker container stop [containID]
# 删除容器文件
$ docker container rm [containerID]

docker container logs

docker container exec

docker container cp

$ docker container exec -it [containerID] /bin/bash

```





##### 