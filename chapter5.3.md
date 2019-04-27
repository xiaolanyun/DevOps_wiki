### 5.3、配置服务

1、将redis配置成服务

按上面的操作步骤，Redis的启动脚本为

```
/usr/local/redis-3.0.3/utils/redis_init_script

将脚本复制到/etc/rc.d/init.d/目录下，并命名为redis

cp /usr/local/redis-3.0.3/utils/redis_init_script /etc/rc.d/init.d/redis
```

***

编辑/etc/rc.d/init.d/redis，修改相应配置，使之能注册为服务

```
vi /etc/rc.d/init.d/redis
查看以上redis服务脚本，作如下几个修改的准备；

(1)在脚本第一行后面添加内容如下：

#chkconfig:2345 80 90

(如果不添加上面内容，在注册服务时会提示：service redis does not support chkconfig)

------

(2)REDISPORT端口修改为各节点对应的端口：（注意：端口名将与下面配置文件名有关）

------

(3)EXEC=/usr/local/bin/redis-server改为EXEC=/usr/local/redis-3.0.3/bin/redis-server

------

(4)CLIEXEC=/usr/local/bin/redis-cli改为CLIEXEC=/usr/local/redis-3.0.3/bin/redis-cli

------

(5)配置文件设置，对CONF属性作如下调整

CONF=”/etc/redis/${REDISPORT}.conf”

改为

CONF=”/usr/local/redis-3.0.3/cluster/${REDISPORT}/redis-${REDISPORT}.conf”

------

(6)更改redis开启的命令，以后台运行的方式执行；

$EXEC $CONF&#”&”作用是将服务转到后面运行

修改后的/etc/rc.d/init.d/redis服务脚本内容为（注意各节点的端口不同）:
#!/bin/sh
#chkconfig:2345 80 90
#Simple Redis init.d script conceived to work on Linux systems

#as it does use of the /proc filesystem.

REDISPORT=7113
EXEC=/usr/local/redis-3.0.3/bin/redis-server
CLIEXEC=/usr/local/redis-3.0.3/bin/redis-cli

PIDFILE=/var/run/redis_${REDISPORT}.pid
CONF="/usr/local/redis-3.0.3/cluster/${REDISPORT}/redis-${REDISPORT}.conf"

case "$1" in
    start)
        if [ -f $PIDFILE ]
        then
                echo "$PIDFILE exists, process is already running or crashed"
        else
                echo "Starting Redis server..."
                $EXEC $CONF&#"&"
        fi
        ;;
    stop)
        if [ ! -f $PIDFILE ]
        then
                echo "$PIDFILE does not exist, process is not running"
        else
                PID=$(cat $PIDFILE)
                echo "Stopping ..."
                $CLIEXEC -p $REDISPORT shutdown
                while [ -x /proc/${PID} ]
                do
                    echo "Waiting for Redis to shutdown ..."
                    sleep 1
                done
                echo "Redis stopped"
        fi
        ;;
    *)
        echo "Please use start or stop as first argument"
        ;;
esac
```



***

以上配置操作完成后，便可将Redis注册为服务；

```
chkconfig --add redis 

将Redis添加到环境变量中：

vi /etc/profile

export PATH=$PATH:/usr/local/redis-3.0.3/bin

使配置生效：

source /etc/profile
```