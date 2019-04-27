### 3.3、mysql5.7&8.0开启远程登录权限

1、mysql5.7开启远程登录权限

```
GRANT ALL PRIVILEGES
ON *.* TO 'root'@'%' IDENTIFIED BY 'Admin123*' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

2、mysql8.0开启远程登陆权限

```
mysql> show databases;

+--------------------+

| Database           |

+--------------------+

| information_schema |

| mysql              |【这个数据库含有usr表】

| performance_schema |

| sys                |

+--------------------+

4 rows in set (0.01 sec
```

***

```
mysql> use mysql

Reading table information for completion of table and column names

You can turn off this feature to get a quicker startup with -A

Database changed
```

***

```
mysql> show tables

    -> ;

+---------------------------+

| Tables_in_mysql           |

+---------------------------+

| columns_priv              |

| component                 |

| db                        |

| default_roles             |

| engine_cost               |

| func                      |

| general_log               |

| global_grants             |

| gtid_executed             |

| help_category             |

| help_keyword              |

| help_relation             |

| help_topic                |

| innodb_index_stats        |

| innodb_table_stats        |

| password_history          |

| plugin                    |

| procs_priv                |

| proxies_priv              |

| role_edges                |

| server_cost               |

| servers                   |

| slave_master_info         |

| slave_relay_log_info      |

| slave_worker_info         |

| slow_log                  |

| tables_priv               |

| time_zone                 |

| time_zone_leap_second     |

| time_zone_name            |

| time_zone_transition      |

| time_zone_transition_type |

| user                      |【找到user表】

+---------------------------+

33 rows in set (0.00 sec)
```

***

```
mysql> update user set host = "%" where user='root';【设置root用户远程连接】

Query OK, 1 row affected (0.03 sec)

Rows matched: 1  Changed: 1  Warnings: 0
```

***

```
mysql> select host, user, authentication_string, plugin from user;【查看用户权限，root的host为%,表示可以进行远程连接】

+-----------+------------------+------------------------------------------------------------------------+-----------------------+

| host      | user             | authentication_string                                                  | plugin                |

+-----------+------------------+------------------------------------------------------------------------+-----------------------+| %         | root             | $A$005$1pg#)80Qbb.*0(  ~F1iXY3XZdgigIERqgyo/8rRlwEiW/gN00A0zVF2llP5 | caching_sha2_password || localhost | mysql.infoschema | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | caching_sha2_password || localhost | mysql.session    | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | caching_sha2_password || localhost | mysql.sys        | $A$005$THISISACOMBINATIONOFINVALIDSALTANDPASSWORDTHATMUSTNEVERBRBEUSED | caching_sha2_password |

+-----------+------------------+------------------------------------------------------------------------+-----------------------+

4 rows in set (0.00 sec)

------


```



