## Docker Compose





管理多个容器的联动，让多个 Docker 容器组成一个应用

需要定义一个 [YAML](https://www.ruanyifeng.com/blog/2016/07/yaml.html) 格式的配置文件`docker-compose.yml`，写好多个容器之间的调用关系。然后，只要一个命令，就能同时启动/关闭这些容器。

```bash
# 启动所有服务
$ docker-compose up
# 关闭所有服务
$ docker-compose stop
```