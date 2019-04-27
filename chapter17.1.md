### 17.1、服务器相关配置

centos中的环境变量文件是 /etc/profile
bash目录~/.bash_profile

***

bigdata1   192.168.222.128         20G  12.1G  8G
nexus：
/root/data/program/software/Nexus/nexus-3.14.0-04/bin
启动
./nexus run &
http://192.168.222.128:8081/

mongodb:
启动进程：/root/data/program/software/mongodb/bin/mongod --replSet repset -f /root/data/program/software/mongodb/bin/mongodb.conf
进入mongodb
/root/data/program/software/mongodb/bin/mongo
端口27017

jdk
/root/data/program/software/java8/jdk1.8.0_191



***

bigdata2    192.168.222.129          20G  12.7G  8G
mysql8.0          3306
禅道      8088



***

bigdata3     192.168.222.130         40G   23.1G  17G
mysql5.7     3306

sonar-scanner
/usr/local/sonar-scanner-3.3.0.1492-linux/bin
sonar
/usr/local/sonarqube-6.7.6/bin/linux-x86-64
192.168.222.130:9000

jenkins：
/etc/sysconfig/jenkins

http://192.168.222.130:8099/


gitbook


git
/usr/local/git/bin

gradle
/usr/local/gradle-4.6

sdk
/root/data/program/software/android-sdk-linux

java
/usr/local/java8/jdk1.8.0_191

maven3.3.9
/usr/local/apache-maven-3.3.9-bin/apache-maven-3.3.9
/usr/local/apache-maven-3.3.9-bin/apache-maven-3.3.9/conf/settings.xml

jdk
/usr/local/java8/jdk1.8.0_191

***

windows
前端网站
http://localhost:8088/#/login