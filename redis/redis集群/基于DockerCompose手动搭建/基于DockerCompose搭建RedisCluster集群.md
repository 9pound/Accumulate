# DockerCompose构建Redis集群

##### 1、新建配置模板文件

- redis-cluster-conf.tmpl

```shell
port ${PORT}
requirepass 1234
masterauth 1234
protected-mode no
daemonize no
appendonly yes
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 15000
cluster-announce-ip 192.168.10.10
cluster-announce-port ${PORT}
cluster-announce-bus-port 1${PORT}
```

- `port`：[节点端口](https://www.zhihu.com/search?q=节点端口&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A229103533})；
- `requirepass`：添加访问认证；
- `masterauth`：如果主节点开启了访问认证，从节点访问主节点需要认证；
- `protected-mode`：保护模式，默认值 yes，即开启。开启保护模式以后，需配置 `bind ip` 或者设置访问密码；关闭保护模式，外部网络可以直接访问；
- `daemonize`：是否以守护线程的方式启动（后台启动），默认 no；
- `appendonly`：是否开启 AOF 持久化模式，默认 no；
- `cluster-enabled`：是否开启[集群模式](https://www.zhihu.com/search?q=集群模式&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A229103533})，默认 no；
- `cluster-config-file`：[集群节点](https://www.zhihu.com/search?q=集群节点&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A229103533})信息文件；
- `cluster-node-timeout`：集群节点连接超时时间；
- `cluster-announce-ip`：集群节点 IP，填写宿主机的 IP；
- `cluster-announce-port`：集群节点映射端口；
- `cluster-announce-bus-port`：集群节点总线端口。

##### 2、初始化节点目录以及配置信息

```shell
for port in `seq 6371 6378`; \
do \
  mkdir -p redis-${port}/conf \
  && PORT=${port} envsubst < redis-cluster-conf.tmpl > redis-${port}/conf/redis.conf \
  && mkdir -p redis-${port}/data;\
done

```

##### 3、编写Docker Compose ymal 配置文件

- docker-compose.yml

```
# 描述 Compose 文件的版本信息
version: "3"

# 定义服务，可以多个
services:
  redis-6371: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6371 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6371/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6371/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
  redis-6372: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6372 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6372/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6372/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令    
  redis-6373: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6373 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6373/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6373/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
  redis-6374: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6374 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6374/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6374/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
  redis-6375: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6375 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6375/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6375/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
  redis-6376: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6376 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6376/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6376/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令    
  redis-6377: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6377 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6377/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6377/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
  redis-6378: # 服务名称
    image: redis:5.0.0 # 创建容器时所需的镜像
    container_name: redis-6378 # 容器名称
    restart: always # 容器总是重新启动
    network_mode: "host" # host 网络模式
    volumes: # 数据卷，目录挂载
      - ~/redis-cluster-compose/redis-6378/conf/redis.conf:/usr/local/etc/redis/redis.conf
      - ~/redis-cluster-compose/redis-6378/data:/data
    command: redis-server /usr/local/etc/redis/redis.conf # 覆盖容器启动后默认执行的命令
```

##### 4、启动所有redis容器

```shell
$ docker-compose up -d
```

##### 5、连接redis任一实例，创建集群

```shell
$ docker container exec -it redis-6371 /bin/bash



redis-cli -a 1234 --cluster create 172.16.0.11:6371 172.16.0.11:6372 172.16.0.11:6373 172.16.0.11:6374 172.16.0.11:6375 172.16.0.11:6376 172.16.0.11:6377 172.16.0.11:6378 --cluster-replicas 1
```

##### 6、连接redis，验证

```shell
#检查集群状态
redis-cli -a 1234 --cluster check 192.168.10.11:6375

# 连接至集群某个节点
redis-cli -c -a 1234 -h 192.168.10.11 -p 6376
# 查看集群信息
cluster info
# 查看集群结点信息
cluster nodes
```

参考
https://zhuanlan.zhihu.com/p/229103533