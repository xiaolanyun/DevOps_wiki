### 9.2、配置服务

1、配置脚本，实现开机自启

```
ln -s /usr/local/sonarqube-6.7.6/bin/linux-x86-64 /usr/bin/sonar

cd /etc/init.d/

vi sonar

#!/bin/sh

# chkconfig:2345 10 90

# rc file for SonarQube

#

# description: SonarQube system (www.sonarsource.org)

#

### BEGIN INIT INFO

# Provides: sonar

# Required-Start: $network

# Required-Stop: $network

# Default-Start: 3 4 5

# Default-Stop: 0 1 2 6

# Short-Description: SonarQube system (www.sonarsource.org)

# Description: SonarQube system (www.sonarsource.org)

### END INIT INFO

/usr/bin/sonar $*
```

***

2、添加服务

```
sudo chmod 755 /etc/init.d/sonar

sudo chkconfig --add sonar
```

***

3、配置服务启动时依赖的jdk，配置为jdk中java命令的绝对路径

```
vi /usr/local/sonarqube-6.7.6/conf/wrapper.conf

wrapper.java.command=/usr/local/java8/jdk1.8.0_191/bin/java
```



***

4、测试状态

```
[sonar@xxxxxx ~]$ service sonar status

SonarQube is running (31746)
```

用户名：admin

密码：admin