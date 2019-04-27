### 5.2、集群测试

1、bigdata3中

```
/usr/local/redis-3.0.3/bin/redis-cli -c -p 7111

127.0.0.1:7111> set zy zhangyong

OK
```



bigdata2中

```
/usr/local/redis-3.0.3/bin/redis-cli -c -p 7112

127.0.0.1:7112> get zy

-> Redirected to slot [2092] located at 192.168.222.130:7111

"zhangyong"


```



bigdata1同理查看