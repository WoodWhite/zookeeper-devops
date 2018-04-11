# zookeeper
版本号：3.4.5

操作系统：Centos 7

##### 1、简介
* 功能
* 概念

##### 2、架构
* 单机
* 集群

##### 3、机制
* 事务日志（log）

```
每提交一个事务都保存在日志中。
```

* 快照 (snapshot)

```
每提交一定数量（5000或10000，可配置）的事务，做一次快照。
```

* 存储结构

```
以类似目录树数据结构存储数据
```

##### 4、安装

##### 5、配置

##### 6、启动

##### 7、工具
* zookeeper-client 或 zkCli.sh
* zookeeper-server-cleanup 或 zkCleanup.sh
* zookeeper-server 或 zkServer.sh

##### 8、运维

* 连接服务端

```
本机
命令：zookeeper-client 或 zkCli.sh

远端
命令：zookeeper-client -server ip:port 或 zkCli.sh -server ip:port # 默认端口2181
```

---

* 帮助

```
help
```

* 查看

```
查看目录结构
命令：ls /xxx

查看文件内容
命令：get /xxx/xxx/xxx
```

* 删除

```
删除非空目录
命令： rmr /xxx

删除文件
命令：delete /xxx/xxx/xxx

```

* 退出

```
quit
```

---
* 查看服务状态

```
场景
集群方式，确定哪一台是leade 或 查看配置文件路径。 
工具
zookeeper-server 或 zkServer.sh 
命令
zookeeper-server status
```


* 清理

```
场景
zookeeper 的log、 snapshot数据太多，需要清理，保留最新的10个log、snapshot。 
工具
zookeeper-server-cleanup 或 zkCleanup.sh 
命令
zookeeper-server-cleanup /var/lib/zookeeper/version-2/ 10
```

