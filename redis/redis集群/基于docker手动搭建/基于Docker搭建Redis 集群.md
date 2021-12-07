# 基于Docker的Redis 集群搭建 

### 1、创建网卡

```
docker network create redis --subnet 172.28.0.0/16
```

### 2、创建节点目录及配置文件

```
for port in $(seq 1 6); 
do 
mkdir -p ~/redis-cluster/node-${port}/conf
touch ~/redis-cluster/node-${port}/conf/redis.conf
cat << EOF > ~/redis-cluster/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.28.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done
```

windows上编辑文件后上传Linux 后需要 执行如下命令  解决Linux和windows下的回车换行符不兼容的问题

```
sed 's/\r//g' redis-cluster-init.sh > redis-cluster-init2.sh 
```

### 3、启动docker容器

参数说明

- -p 参数 容器6379端口映射到本地端口 6371
- -name ： 容器的名字叫做 redis-1
- -v : 将当前目录 ~/redis/node-1/data 映射到容器的
- -d : 容器启动后在后台运行
- --net ： 
- --ip ：
- redis:5.0.9-alpine3.11 ： 使用哪一个镜像

```
# 容器1

docker run -p 6371:6379 -p 16371:16379 --name redis-1 \
-v ~/redis-cluster/node-1/data:/data \
-v ~/redis-cluster/node-1/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.11 redis:5.0.5 redis-server /etc/redis/redis.conf

# 容器2

docker run -p 6372:6379 -p 16372:16379 --name redis-2 \
-v ~/redis-cluster/node-2/data:/data \
-v ~/redis-cluster/node-2/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.12 redis:5.0.5 redis-server /etc/redis/redis.conf

# 容器3

docker run -p 6373:6379 -p 16373:16379 --name redis-3 \
-v ~/redis-cluster/node-3/data:/data \
-v ~/redis-cluster/node-3/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.13 redis:5.0.5 redis-server /etc/redis/redis.conf

# 容器4

docker run -p 6374:6379 -p 16374:16379 --name redis-4 \
-v ~/redis-cluster/node-4/data:/data \
-v ~/redis-cluster/node-4/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.14 redis:5.0.5 redis-server /etc/redis/redis.conf

# 容器5

docker run -p 6375:6379 -p 16375:16379 --name redis-5 \
-v ~/redis-cluster/node-5/data:/data \
-v ~/redis-cluster/node-5/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.15 redis:5.0.5 redis-server /etc/redis/redis.conf

# 容器6

docker run -p 6376:6379 -p 16376:16379 --name redis-6 \
-v ~/redis-cluster/node-6/data:/data \
-v ~/redis-cluster/node-6/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.28.0.16 redis:5.0.5 redis-server /etc/redis/redis.conf
```

### 4、创建集群

```
# 进入容器

docker container exec -it redis-1 /bin/bash

# 创建 集群

redis-cli --cluster create 172.28.0.11:6379 172.28.0.12:6379 172.28.0.13:6379 172.28.0.14:6379 172.28.0.15:6379 172.28.0.16:6379 --cluster-replicas 1

# 启动redis集群客户端（-c表示集群）

> redis-cli -c

# 查看集群信息

> cluster info 

# 查看集群节点

> cluster nodes


```

ipv4 转发被禁用问题

```
# 向配置文件中追加如下内容 /etc/sysctl.conf

net.ipv4.ip_forward=1

# 重启网络

systemctl restart network

# 验证

sysctl net.ipv4.ip_forward
```





参考地址：
https://cloud.tencent.com/developer/article/1838120





