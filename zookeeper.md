# Zookeeper
设置一个单独的zookeeper
1. 解压下载的文件，进入解压的根目录
2. 在conf目录下配置zoo.cfg文件

```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181

```
- tickTime zookeeper的最小时间单位（毫秒），心跳时间和session超时最小时间是2倍的tickTime
- dataDir 内存中存放数据快照的路径，除非申明，否则数据库更新的事务日志。
- clientPort 客户端连接的端口

## 客户端连接

```
zkCli.sh -server 127.0.0.1:2181

# 查看路径下
[zk: localhost:2181(CONNECTED) 2] ls /
[motan, zookeeper]

[zkshell: 9] create /zk_test my_data
Created /zk_test

[zkshell: 12] get /zk_test
my_data
cZxid = 5
ctime = Fri Jun 05 13:57:06 PDT 2009
mZxid = 5
mtime = Fri Jun 05 13:57:06 PDT 2009
pZxid = 5
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0
dataLength = 7
numChildren = 0

[zkshell: 14] set /zk_test junk
cZxid = 5
ctime = Fri Jun 05 13:57:06 PDT 2009
mZxid = 6
mtime = Fri Jun 05 14:01:52 PDT 2009
pZxid = 5
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0
dataLength = 4
numChildren = 0
[zkshell: 15] get /zk_test
junk
cZxid = 5
ctime = Fri Jun 05 13:57:06 PDT 2009
mZxid = 6
mtime = Fri Jun 05 14:01:52 PDT 2009
pZxid = 5
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0
dataLength = 4
numChildren = 0

[zkshell: 16] delete /zk_test
[zkshell: 17] ls /
[zookeeper]
[zkshell: 18]

```
## 集群配置

```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
initLimit=5
syncLimit=2
server.1=zoo1:2888:3888
server.2=zoo2:2888:3888
server.3=zoo3:2888:3888

```

[文档地址](https://zookeeper.apache.org/doc/r3.4.6/zookeeperProgrammers.html)

