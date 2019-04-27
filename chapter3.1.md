### 3.1、初始化登录

***

1、安装mysql之后初始登陆问题

```
[root@localhost bin]#mysql -u root -p

Enter password: 

ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)
```

解决：

```
vi /etc/my.cnf

最后一行添加配置参数

skip-grant-tables

重启mysql服务

service mysqld restart

正常进入mysql
```

***

