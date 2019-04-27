### 9.3、SonarQubeScanner

```
官网下载地址：https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner
选择linux 64 bit，进行下载

sudo unzip -d /usr/local sonar-scanner-cli-3.3.0.1492-linux.zip

配置环境变量
vi /etc/profile
export SONAR_SCANNER_HOME=/usr/local/sonar-scanner-3.3.0.1492-linux
PATH=$PATH:${SONAR_SCANNER_HOME}/bin

配置sonar-scanner
cd /usr/local/sonar-scanner-3.3.0.1492-linux/conf
sudo vi sonar-scanner.properties

#----- Default SonarQube server
sonar.host.url=http://192.168.222.130:9000

#----- Default source code encoding
#sonar.sourceEncoding=UTF-8
#----- Security (When 'sonar.forceAuthentication' is set to 'true')
sonar.login=admin
sonar.password=admin

验证是否成功
sonar-scanner -h
```



