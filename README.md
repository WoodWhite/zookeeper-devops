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

```
yum install zookeeper zookeeper-server
```

##### 5、配置

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
# the directory where the translog is stored.
dataLogDir=/var/lib/zookeeper/log
# the port at which the clients will connect
clientPort=2181
server.2=4.8.1.2:2888:3888
server.8=4.8.1.8:2888:3888
server.10=4.8.1.10:2888:3888
```

##### 6、启动

```
单机单服务
命令：systemctl start zookeeper-server

单机多服务
命令：zookeeper-server start etc/zookeeper/z1/z1.cfg
     zookeeper-server start etc/zookeeper/z2/z2.cfg
     zookeeper-server start etc/zookeeper/z3/z3.cfg
```

##### 7、端口

```
clientPort # 客户端连接的端口，默认2181
xxxx:xxxx # follower连接leader的端口（前），默认2888；leader选举的端口（后），默认3888
```

##### 8、工具
* zookeeper-client 或 zkCli.sh
* zookeeper-server-cleanup 或 zkCleanup.sh
* zookeeper-server 或 zkServer.sh

##### 9、运维

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

