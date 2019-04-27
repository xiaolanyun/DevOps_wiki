### 4.1、安装部署

1、选择三台服务器：10.211.55.7（主节点）   10.211.55.8（副本节点）  10.211.55.9（副本节点）

下载mongodb：

```
wget <https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz>

解压到：/root/data/program/software

文件夹重命名为mongodb
```

***

```
进入mongodb目录：cd /root/data/program/software/mongodb

新建两个文件夹：

mkdir db

mkdir logs
```

***

```
进入bin目录cd /root/data/program/software/mongodb/bin

新建配置文件：

touch mongodb.conf

内容：

              dbpath=/root/data/program/software/mongodb/db

              logpath=/root/data/program/software/mongodb/logs/mongodb.log

              port=27017

              fork=true

	      	  nohttpinterface=true
```

命令解释：mongod --dbpath=/data/db前台启动Mongodb进程，如果Session窗口关闭，Mongodb进程也随之停止，不过Mongodb同时还提供了一种后台Daemon方式启动，只需要加上一个"--fork"参数即可，值得注意的是，用到了"--fork"参数就必须启用"--logpath"参数。

***

分别三台服务器上启动mongodb：

```
/root/data/program/software/mongodb/bin/mongod --replSet repset -f /root/data/program/software/mongodb/bin/mongodb.conf
```

命令解释：

启动配置文件

各个服务器查看，都已经启动：

```
[root@bigdata3 bin]# ps -ef|grep mongodb

root      2574     1  1 22:09 ?        00:00:00 /data/program/software/mongodb/bin/mongod --replSet repset -f /root/data/program/software/mongodb/bin/mongodb.conf
```

***

在三台机器上任意一台机器登陆mongodb：

```
/root/data/program/software/mongodb/bin/mongo

使用admin数据库

use admin

定义副本集配置变量，这里的_id:”repset”和上面命令参数--replSet repset保持一致

config = { _id:"repset", members:[{_id:0,host:"192.168.222.128:27017"},{_id:1,host:"192.168.222.129:27017"},{_id:2,host:"192.168.222.130:27017"}]}
```

***

初始化副本集群：

rs.initiate(config);

![img](image/4.1.0.png)表示成功

查看集群节点的状态：

```
 rs.status();

如下结果：

{

 "set" : "repset",

 "date" : ISODate("2017-09-21T14:30:17.190Z"),

 "myState" : 1,

 "term" : NumberLong(1),

 "heartbeatIntervalMillis" : NumberLong(2000),

 "optimes" : {

  "lastCommittedOpTime" : {

   "ts" : Timestamp(1506004207, 1),

   "t" : NumberLong(1)

  },

  "appliedOpTime" : {

   "ts" : Timestamp(1506004207, 1),

   "t" : NumberLong(1)

  },

  "durableOpTime" : {

   "ts" : Timestamp(1506004207, 1),

   "t" : NumberLong(1)

  }

 },

 "members" : [

  {

   "_id" : 0,

   "name" : "10.211.55.7:27017",

   "health" : 1,

   "state" : 2,

   "stateStr" : "SECONDARY",

   "uptime" : 111,

   "optime" : {

​    "ts" : Timestamp(1506004207, 1),

​    "t" : NumberLong(1)

   },

   "optimeDurable" : {

​    "ts" : Timestamp(1506004207, 1),

​    "t" : NumberLong(1)

   },

   "optimeDate" : ISODate("2017-09-21T14:30:07Z"),

   "optimeDurableDate" : ISODate("2017-09-21T14:30:07Z"),

   "lastHeartbeat" : ISODate("2017-09-21T14:30:16.070Z"),

   "lastHeartbeatRecv" : ISODate("2017-09-21T14:30:16.887Z"),

   "pingMs" : NumberLong(0),

   "syncingTo" : "10.211.55.9:27017",

   "configVersion" : 1

  },

  {

   "_id" : 1,

   "name" : "10.211.55.8:27017",

   "health" : 1,

   "state" : 2,

   "stateStr" : "SECONDARY",

   "uptime" : 111,

   "optime" : {

​    "ts" : Timestamp(1506004207, 1),

​    "t" : NumberLong(1)

   },

   "optimeDurable" : {

​    "ts" : Timestamp(1506004207, 1),

​    "t" : NumberLong(1)

   },

   "optimeDate" : ISODate("2017-09-21T14:30:07Z"),

   "optimeDurableDate" : ISODate("2017-09-21T14:30:07Z"),

   "lastHeartbeat" : ISODate("2017-09-21T14:30:16.070Z"),

   "lastHeartbeatRecv" : ISODate("2017-09-21T14:30:16.877Z"),

   "pingMs" : NumberLong(0),

   "syncingTo" : "10.211.55.9:27017",

   "configVersion" : 1

  },

  {

   "_id" : 2,

   "name" : "10.211.55.9:27017",

   "health" : 1,

   "state" : 1,

   "stateStr" : "PRIMARY",

   "uptime" : 163,

   "optime" : {

​    "ts" : Timestamp(1506004207, 1),

​    "t" : NumberLong(1)

   },

   "optimeDate" : ISODate("2017-09-21T14:30:07Z"),

   "infoMessage" : "could not find member to sync from",

   "electionTime" : Timestamp(1506004115, 1),

   "electionDate" : ISODate("2017-09-21T14:28:35Z"),

   "configVersion" : 1,

   "self" : true

  }

 ],

 "ok" : 1

}




```











































