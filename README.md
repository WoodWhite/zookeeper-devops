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

##### 4、安装

##### 5、配置

##### 6、启动

##### 7、工具

##### 8、运维
* 清理数据

```
场景
zookeeper 的log、 snapshot数据太多，需要清理，保留最新的10个log、snapshot。 
工具
zookeeper-server-cleanup 或 zkCleanup.sh 
命令
zookeeper-server-cleanup /var/lib/zookeeper/version-2/ 10
```

