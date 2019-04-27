### 8.1、git

1、下载git

<https://www.cnblogs.com/mrjade/p/9299064.html>

Git下载网址

https://mirrors.edge.kernel.org/pub/software/scm/git/

注释：prefix=/usr/local 是把prefix这个变量的赋值传到make脚本，也就是makefile里。
 all是makefile中指定的一个编译目标，如果make没有加all，那么默认会执行makefile中的第一个编译目标，这是两者的不同之处。但是，在大多数的makefile中，会将all作为第一个编译目标，如果是这样，那么all加不加都是一样的，因此，真实的执行结果依赖于makefile的写法，是否把all作为第一个编译目标

***

2、安装

2.1、卸载Centos自带的git1.7.1:
通过git –version查看系统带的版本，Centos应该自带的是git版本是1.7.1

终端输入：

```
yum remove git
```

2.2、安装所需软件包

终端输入：

```
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidoc

yum install gcc perl-ExtUtils-MakeMaker
```

2.3、下载git2.2.1并将git添加到环境变量中

（1）终端输入：

```
wget https://github.com/git/git/archive/v2.2.1.tar.gz
```

（2）解压：

```
tar zxvf v2.2.1.tar.gz
```

（3）终端输入：

```
　　cd git-2.7.0
　　make prefix=/usr/local/git all
　　make prefix=/usr/local/git install
```

（4）配置环境变量

```
sudo vim /etc/profile

export PATH=$PATH:/usr/local/git/bin
```

　　保存并退出

（5）终端输入：

```
source /etc/profile
```

***

3、配置

3.1、windows下生成ssh

```
cd ~/.ssh             #可以进入目录表示以前生成过ssh                                 

ll                    #列出文件,下面命令生成ssh,pub文件内容即ssh                                  

ssh-keygen -t rsa -C "2407512504@qq.com" 
```

***

3.2、linux下生成ssh

终端输入

```
ssh-keygen -t rsa
```

一路回车

生成位置：/root/.ssh

***

3.3、配置github的ssh

打开github-右上角头像-setting-左边列出有ssh配置,将pub文件内容复制到ssh公钥配置

***

3.4、测试ssh

```
ssh -T git@github.com
```

***

3.5、配置全局用户名

查看当前配置

```
git config --global  --list
```

配置

```
git config --global user.name "xiaolanyun"

git config --global user.email "2407512504@qq.com"
```

