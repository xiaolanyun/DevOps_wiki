### 3、Mysql

***

1、说明：bigdata2安装mysql8，bigdata3安装mysql5.7。因为版本有差异，根据需要选择使用，双版本选择增强平台的服务能力。

***

2、安装mysql

2.1、mysql8:

yum默认直接安装最新版本。

```
yum -y install mysql-server
```

2.2、mysql5.7:

```
wget http://dev.mysql.com/get/mysql57-community-release-el7-7.noarch.rpm
```

查看mysql157的rpm包文件

```
rpm -qpl mysql57-community-release-el7-7.noarch.rpm

警告：mysql57-community-release-el7-7.noarch.rpm: 头V3 DSA/SHA1 Signature, 密钥 ID 5072e1f5: NOKEY

/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

/etc/yum.repos.d/mysql-community-source.repo

/etc/yum.repos.d/mysql-community.repo
```

***

安装rpm包

```
rpm -ivh mysql57-community-release-el7-7.noarch.rpm
```

***

查看yum库

```
yum list Mysql*
```

会自动生成以下包

```
已加载插件：fastestmirror, langpacks

Loading mirror speeds from cached hostfile

epel/x86_64/metalink                            | 6.2 kB     00:00     

 \* epel: mirrors.tuna.tsinghua.edu.cn

base                                            | 3.6 kB     00:00     

extras                                          | 3.4 kB     00:00     

jenkins                                         | 2.9 kB     00:00     

mysql-connectors-community                      | 2.5 kB     00:00     

mysql-tools-community                           | 2.5 kB     00:00     

mysql57-community                               | 2.5 kB     00:00     

updates                                         | 3.4 kB     00:00     

(1/3): mysql-connectors-community/x86_64/primary_ |  37 kB   00:00     

(2/3): mysql-tools-community/x86_64/primary_db    |  54 kB   00:00     

(3/3): mysql57-community/x86_64/primary_db        | 170 kB   00:02     

已安装的软件包

mysql57-community-release.noarch     el7-7        installed            

可安装的软件包

MySQL-python.x86_64                  1.2.5-1.el7  base                 

MySQL-zrm.noarch                     3.0-17.el7   epel                 

mysql++.x86_64                       3.1.0-12.el7 epel                 

mysql++-devel.x86_64                 3.1.0-12.el7 epel                 

mysql++-manuals.x86_64               3.1.0-12.el7 epel                 

mysql-community-client.i686          5.7.25-1.el7 mysql57-community    

mysql-community-client.x86_64        5.7.25-1.el7 mysql57-community    

mysql-community-common.i686          5.7.25-1.el7 mysql57-community    

mysql-community-common.x86_64        5.7.25-1.el7 mysql57-community    

mysql-community-devel.i686           5.7.25-1.el7 mysql57-community    

mysql-community-devel.x86_64         5.7.25-1.el7 mysql57-community    

mysql-community-embedded.i686        5.7.25-1.el7 mysql57-community    

mysql-community-embedded.x86_64      5.7.25-1.el7 mysql57-community    

mysql-community-embedded-compat.i686 5.7.25-1.el7 mysql57-community    

mysql-community-embedded-compat.x86_64

                                     5.7.25-1.el7 mysql57-community    

mysql-community-embedded-devel.i686  5.7.25-1.el7 mysql57-community    

mysql-community-embedded-devel.x86_64

                                     5.7.25-1.el7 mysql57-community    

mysql-community-libs.i686            5.7.25-1.el7 mysql57-community    

mysql-community-libs.x86_64          5.7.25-1.el7 mysql57-community    

mysql-community-libs-compat.i686     5.7.25-1.el7 mysql57-community    

mysql-community-libs-compat.x86_64   5.7.25-1.el7 mysql57-community    

mysql-community-release.noarch       el7-7        mysql57-community    

mysql-community-server.x86_64        5.7.25-1.el7 mysql57-community 【这个是重点】   

mysql-community-test.x86_64          5.7.25-1.el7 mysql57-community    

mysql-connector-c++.x86_64           8.0.15-1.el7 mysql-connectors-community

mysql-connector-c++-devel.x86_64     8.0.15-1.el7 mysql-connectors-community

mysql-connector-c++-jdbc.x86_64      8.0.15-1.el7 mysql-connectors-community

mysql-connector-java.noarch          1:5.1.25-3.el7

                                                  base                 

mysql-connector-odbc.x86_64          8.0.15-1.el7 mysql-connectors-community

mysql-connector-odbc-debuginfo.x86_64

                                     8.0.15-1.el7 mysql-connectors-community

mysql-connector-odbc-setup.x86_64    8.0.15-1.el7 mysql-connectors-community

mysql-connector-python.noarch        2.0.4-1.el7  mysql-connectors-community

mysql-connector-python.x86_64        8.0.15-1.el7 mysql-connectors-community

mysql-connector-python-cext.x86_64   8.0.15-1.el7 mysql-connectors-community

mysql-connector-python-debuginfo.x86_64

                                     2.1.7-1.el7  mysql-connectors-community

mysql-mmm.noarch                     2.2.1-15.el7 epel                 

mysql-mmm-agent.noarch               2.2.1-15.el7 epel                 

mysql-mmm-monitor.noarch             2.2.1-15.el7 epel                 

mysql-mmm-tools.noarch               2.2.1-15.el7 epel                 

mysql-proxy.x86_64                   0.8.5-2.el7  epel                 

mysql-proxy-devel.x86_64             0.8.5-2.el7  epel                 

mysql-ref-manual-5.5-en-html-chapter.noarch

                                     1-20170320   mysql57-community    

mysql-ref-manual-5.5-en-pdf.noarch   1-20170320   mysql57-community    

mysql-ref-manual-5.7-en-html-chapter.noarch

                                     1-20181224   mysql57-community    

mysql-ref-manual-5.7-en-pdf.noarch   1-20181224   mysql57-community    

mysql-router.x86_64                  8.0.12-1.el7 mysql-tools-community

mysql-router-community.x86_64        8.0.15-1.el7 mysql-tools-community

mysql-router-debuginfo.x86_64        8.0.12-1.el7 mysql-tools-community

mysql-shell.x86_64                   8.0.15-1.el7 mysql-tools-community

mysql-shell-debuginfo.x86_64         8.0.15-1.el7 mysql-tools-community

mysql-utilities.noarch               1.6.5-1.el7  mysql-tools-community

mysql-utilities-extra.noarch         1.5.6-1.el7  mysql-tools-community

mysql-workbench-community.x86_64     8.0.15-1.el7 mysql-tools-community

mysql-workbench-community-debuginfo.x86_64

                                     8.0.15-1.el7 mysql-tools-community

mysql57-community-release.noarch     el7-10       mysql57-community    

mysqlreport.noarch                   3.5-11.el7   epel                 

mysqltuner.noarch                    1.7.13-1.git.59e5f40.el7

                                                  epel 
```

***

安装mysql

```
yum install mysql-community-server
```

查看mysql版本

```
mysql -V

mysql  Ver 14.14 Distrib 5.7.25, for Linux (x86_64) using  EditLine wrapper
```

***

3、启动mysql服务

启动mysql：

```
service mysqld start
```

查看mysql的状态：

```
service mysqld status
```

关闭mysql:

```
service mysqld stop
```

























