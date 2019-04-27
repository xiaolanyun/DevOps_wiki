### 2、服务器基础配置

------

1、windows下虚拟机选择VM workstation 14pro。linux选择Centos7版本。

***

2、具体配置

前提：

目前准备了三台centos7的虚拟机：

10.211.55.7bigdata1

10.211.55.8bigdata2 

10.211.55.9bigdata3

***

安装过程：

网络选择：NAT

主机名：bigdata1

全名,用户名：xiaolanyun1

root密码：xiaolanyun

如下是一些基础配置，之后的开源工具的安装，另行在服务器上安排。

（1）、 服务器jdk版本1.8

配置：/etc/profile

```
export JAVA_HOME=/data/program/software/java8

export JRE_HOME=/data/program/software/java8/jre

export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib

export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

验证：java -version

source /etc/profile 使配置立刻生效
```

（2）、 统一host

```
vi /etc/hosts

192.168.222.128 bigdata1

192.168.222.129 bigdata2

192.168.222.130 bigdata3
```

（3）、 防火墙

对于centos6：

```
查看状态：service iptables status

关闭：service iptables stop
```

对于centos7:

```
查看状态：firewall-cmd --state

关闭：systemctl stop firewalld.service

关闭开机启动：systemctl disable firewalld.service
```