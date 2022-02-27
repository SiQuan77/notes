# 前言

​	最近参加了一个项目组，开发语言用的是php，本来想的是进去写前端的，后来进组之后发现目前的工作主要还是围绕着修复旧nexsus php的bug为主，于是按照组里leader的建议安装了fedora。本来是用liunx环境就ok，自己安装了centos后被leader建议使用fedora，于是开始接触了fedora。

​	后来又在fedora里安装php，podman，git，jdk还有phpstorm等等。由于podman是类似于docker的容器，会单独开篇幅进行总结。

​	在这里我会写一些我在安装fedora时遇到的问题和学习到的小知识，持续更新..

## 介绍fedora

> ​	Fedora Linux（第七版以前为Fedora Core）是由Fedora项目社区开发、红帽公司赞助，目标是创建一套新颖、多功能并且自由（开放源代码）的操作系统。Fedora是商业化的Red Hat Enterprise Linux发行版的**上游**源码。
>
> ​	Fedora对于用户而言，是一套功能完备、更新快速的免费操作系统；而对赞助者Red Hat公司而言，它是许多新技术的测试平台，被认为可用的技术最终会加入到Red Hat Enterprise Linux中。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220227221019.png)

关于这里的上游源码我做个解释：上游和下游实际上只是数据流的方向。这个数据在上游或下游流动的方式取决于最终需要谁来处理它。基本上，**程序员是上游，用户是下游**。

# 遇到的问题

​	本次安装的fedora版本是Fedora-Workstation-Live-x86_64-35-1.2.iso，leader建议选择Workstation版本因为带有**图形化界面**，而server没有。

## 安装后没网络



> 本部分参考[centos7连接网络不可达的解决方法 - yongfengnice - 博客园 (cnblogs.com)](https://www.cnblogs.com/yongfengnice/p/8808893.html)，感谢yongfengnice！

 

 ​	在fedora下载镜像后，通过VMware安装。进去之后还要记得install to hard drive，在安装向导里选择中文语言。之后通过ifconfig查不到本机的ip，一直是**网络不可达状态**。

 ​	查阅网络后，通过编辑/etc/sysconfig/network-scripts/ifcfg-xxx（这个xxx取决于你的以太网卡）解决，我安装之后/etc/sysconfig/network-scripts这个文件夹是存在的，但是ifcfg-xxx不存在，我自己创建并且编辑，具体步骤在下图：

 ![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/202202272127176.png)



 

 # 学到的知识

## 在fedora安装php环境

> 安装参考[(81条消息) linux搭建初始php环境（极简！）_954L-CSDN博客_linux安装php环境](https://blog.csdn.net/wkh___/article/details/83183621)，感谢954L！

### 安装

1.安装apache

```bash
yum -y install httpd
```

2.安装php

```bash
yum -y install php
```

3.安装php-fpm

```bash
yum -y install php-fpm
```

4.安装php-mysql

```bash
yum -y install php-mysql
```

5.安装apache拓展

```bash
yum -y install httpd-manual mod_ssl mod_perl mod_auth_mysql
```

6.安装php拓展

```bash
yum -y install php-gd php-xml php-mbstring php-ldap php-pear php-xmlrpc
```

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220227214643.png)

### 测试环境

1.启动apache

```bash
service httpd start
```

之后在fedora自带的火狐浏览器里输入http://localhost/来测试是否开启。如果出现如下图所示，则证明开启成功。如果80端口被占用（比如nginx），则有可能开启不成功。

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/20220227215003.png)

2.测试php

进入apache的web根目录：/var/www/html记住此路径地址，FTP或SSH上传时把项目上传到此地址，当然也可以自己重新配置或host文件。

这里先写个测试php校验是否可用，注意在/var/www/html下创建test.php。

```bash
vi test.php
```

插入如下内容：

```php
<?php
 
phpinfo();
 
?>
```

![](https://cdn.jsdelivr.net/gh/SiQuan77/img_bed/2018101916061821)

## 安装git

> 参考[在Linux系统上安装Git - 在树上唱歌w - 博客园 (cnblogs.com)](https://www.cnblogs.com/wulixia/p/11016684.html)，该文有从github上下载源包安装的步骤。

一句搞定，参考

```bash
yum -y install git
```

## jdk安装

> 参考[fedora安装jdk - wujinfeng - 博客园 (cnblogs.com)](https://www.cnblogs.com/w-jinfeng/articles/5736159.html)，感谢wujinfeng！

这里我个人觉得把自带的卸载了使用oracle的安装！

fedora24自带**openjdk**，所以如果安装oracle的jdk的话要先删除openjdk，步骤如下：

### 卸载openjdk

0：进入管理员命令行。

1：rpm -qa|grep jdk 查看当前的jdk情况。 

2：dnf remove java java-1.8.0-openjdk* 卸载openjdk，这个过程中因为依赖原因可能会卸载一些额外的软件。 

### 使用解压方式安装

1：去oracle官网下载官方jdk，我下载的是tar.gz格式的。 

2 ：解压jdk安装包tar -zxvf jdk-****-linux-x64.tar.gz  复制到自己的软件文件夹，我的软件一般放到opt下，所以 mv jdk***/  /opt/  

3：配置环境变量vi /etc/profile 后在倒数第三行处输入下面的内容 

  export JAVA_HOME=/opt/jdk1***

  export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib

  export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HOME/bin

4：让环境变量生效 source  /etc/profile 

5：验证：输入java或者java -version

### 使用rpm包安装

这种方式快一点，但是会默认安装在/usr/java路径下！不过两种方式本质上是相同的！

1.去官网下载对应的rpm包，比如jdk-8u25-linux-x64.rpm

2.使用命令

```bash
rpm -ivh jdk-8u321-linux-x64.rpm
```

3.向/etc/profile文件追加以下内容：

```
JAVA_HOME=/usr/java/jdk1.8.0_321-amd64
JRE_HOME=/usr/java/jdk1.8.0_321-amd/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
```

这部分要随机应变，因为有可能解压出来的文件夹名称有略微不同，**切忌机械复制**！
