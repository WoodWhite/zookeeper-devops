# zookeeper
版本号：3.4.5

操作系统：Centos 7

##### 1、简介
* 作用
* 概念

##### 2、架构
* 单机
* 集群

##### 3、安装

##### 4、配置

##### 5、启动

##### 6、工具

##### 7、运维
* 清理数据

```
场景
zookeeper 的log、 snapshot数据太多，需要清理，保留最新的10个log、snapshot。 
工具
zookeeper-server-cleanup zkCleanup.sh 
命令
zookeeper-server-cleanup /var/lib/zookeeper/version-2/ 10
```

