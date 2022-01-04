# Redis-Sentinel

可以监视指定的Redis主服务器以及下属服务器，并在主服务器下线时自动进行故障转移

### 哨兵进程的工作方式

1. 每个Sentinel（哨兵）进程以每秒钟一次的频率向整个集群中的Master主服务器，Slave从服务器以及其他Sentinel（哨兵）进程发送一个 PING 命令。
2. 如果一个实例（instance）距离最后一次有效回复 PING 命令的时间超过 down-after-milliseconds 选项所指定的值，则这个实例会被 Sentinel（哨兵）进程标记为主观下线（SDOWN）。
3. 如果一个Master主服务器被标记为主观下线（SDOWN），则正在监视这个Master主服务器的所有Sentinel（哨兵）进程要以每秒一次的频率确认Master主服务器的确进入了主观下线状态。
4. 当有足够数量的 Sentinel（哨兵）进程（大于等于配置文件指定的值）在指定的时间范围内确认Master主服务器进入了主观下线状态（SDOWN）， 则Master主服务器会被标记为客观下线（ODOWN）。
5. 在一般情况下， 每个Sentinel（哨兵）进程会以每 10 秒一次的频率向集群中的所有Master主服务器、Slave从服务器发送 INFO 命令。
6. 当Master主服务器被 Sentinel（哨兵）进程标记为客观下线（ODOWN）时，Sentinel（哨兵）进程向下线的 Master主服务器的所有 Slave从服务器发送 INFO 命令的频率会从 10 秒一次改为每秒一次。
7. 若没有足够数量的 Sentinel（哨兵）进程同意 Master主服务器下线， Master主服务器的客观下线状态就会被移除。若 Master主服务器重新向 Sentinel（哨兵）进程发送 PING 命令返回有效回复，Master主服务器的主观下线状态就会被移除。
   



redis哨兵至少需要部署三个实例以满足健壮性要求

