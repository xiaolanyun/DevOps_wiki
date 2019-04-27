### 13.2、newman

1、环境

node.js

安装cnpm,国内镜像快。

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```



2、bigdata3安装newman

安装：

```
cnpm install -g newman

cnpm install -g newman-reporter-html【其余报告自行安装】
```

3、newman执行脚本并生成报告

输入newman查看可使用命令参数。

可生成测试报告类型：json,junit的xml，html.

```
newman run phonecheck.json
–reporterscli,html,json,junit --reporter-json-export poptestjsonOut.json
--reporter-junit-export poptestxmlOut.xml --reporter-html-export poptesthtmlOut.html
```









