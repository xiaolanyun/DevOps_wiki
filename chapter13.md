### 13、postman&newman

设计思路

![](image/13.0.PNG)

介绍

1、接口测试用于检测外部系统与系统之间以及内部各个子系统之间的交互点。

接口测试需要接口文档，包括：URL，请求方式，请求参数，返回参数，请求示例，状态码说明。

http请求包含请求头和请求体。

get请求：没有请求体，只有请求头，请求参数只能下写在URL里面或者cookie里面。cookie可以理解为存在本地的键值对。

post请求：有请求头和请求体。请求参数放到请求题里面。

2、postman是一款接口测试工具。Newman是为Postman而生，专门用来运行Postman编写好的脚

本，及生成相关的测试报告的命令。


