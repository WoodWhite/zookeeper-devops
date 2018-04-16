# zookeeper
[官网](https://zookeeper.apache.org)

版本号：3.4.5

操作系统：Centos 7

##### 1、简介
* 功能

```
分布式应用协调服务中间件
i 命名服务
ii 配置管理
iii 同步
iiii 组服务
```

* 概念

```
leader/follower
server/client
znode
log/snapshot
ensemble
nodes and ephemeral znodes
conditional updates and watches
```

* 组成要素

![](https://zookeeper.apache.org/doc/current/images/zkcomponents.jpg)

* 同功能、同类型服务软件

```
Etcd
```

##### 2、模式
* 单机
* 集群

##### 3、算法

```
基于 Paxos 的 Zab 算法。
```

* [Paxos](http://lamport.azurewebsites.net/pubs/paxos-simple.pdf)
* [Zab](https://pdfs.semanticscholar.org/b02c/6b00bd5dbdbd951fddb00b906c82fa80f0b3.pdf)

##### 4、机制
* 事务日志（log）

```
每一个更新操作都分配一个唯一、有序的数，每一个提交的事务都保存在事务日志中，以便数据恢复。
```

* 快照 (snapshot)

```
提交一定数量（5000或10000，可配置）的事务，做一次快照。
```

* 数据模型、等级命名空间

```
类似 Linux 目录树的数据结构，不同的是zookeeper将数据存在内存中。
```

* 服务可用性

```
大多数可用，整个服务就是可用的。
如集群中有3个 zookeeper 服务节点，其中2个服务正常，那么这个 zookeeper 服务就是可用的。
```

* 写请求

```
所有的写请求都会打到leader上，由leader完成写操作。
```

##### 5、安装

```
yum install zookeeper zookeeper-server
```

##### 6、配置

```
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

maxClientCnxns=50
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
dataDir=/var/lib/zookeeper/snapshot
# the directory where the transaction log is stored.
dataLogDir=/var/lib/zookeeper/log
# the port at which the clients will connect
clientPort=2181
server.2=4.8.1.2:2888:3888
server.8=4.8.1.8:2888:3888
server.10=4.8.1.10:2888:3888
```

##### 7、启动

```
单机单服务
命令：systemctl start zookeeper-server

单机多服务
命令：zookeeper-server start etc/zookeeper/z1/z1.cfg
     zookeeper-server start etc/zookeeper/z2/z2.cfg
     zookeeper-server start etc/zookeeper/z3/z3.cfg
```

##### 8、端口

```
clientPort # 客户端连接的端口，默认2181
xxxx:xxxx # follower连接leader的端口（前），默认2888；leader选举的端口（后），默认3888
```

##### 9、工具
* zookeeper-client 或 zkCli.sh
* zookeeper-server-cleanup 或 zkCleanup.sh
* zookeeper-server 或 zkServer.sh

##### 10、运维

* 连接服务端

```
本机
命令：zookeeper-client 或 zkCli.sh

远端
命令：zookeeper-client -server ip:port 或 zkCli.sh -server ip:port # 默认端口2181

集群
命令：zookeeper-client -server ip1:port,ip2:port,ip3:port 或 zkCli.sh -server ip1:port,ip2:port,ip3:port
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

