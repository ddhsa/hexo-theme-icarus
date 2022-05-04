title: 'Linux学习记录（四）：Linux中各种安装软件tar.gz,rpm,deb'
author: ddhsa
tags:
  - 软件安装
  - 安装包
categories:
  - linux学习
date: 2019-06-16 23:11:00
---
本篇文章主要介绍了linux 下安装软件tar.gz, rpm,deb的方法 ，具有一定的参考价值，感兴趣的小伙伴们可以参考一下。

在Linux系统中，软件安装程序比较纷繁复杂，不过最常见的有两种：

1）一种是软件的源代码，您需要自己动手编译它。这种软件安装包通常是用gzip压缩过的tar包（后缀为.tar.gz）。  

2）另一种是软件的可执行程序，你只要安装它就可以了。这种软件安装包通常被是一个RPM包（Redhat Linux Packet Manager，就是Redhat的包管理器），后缀是.rpm。

当然，也有用rpm格式打包的源代码，用gzip压缩过的可执行程序包。只要您理解了以下的思路，这两种形式的安装包也不在话下了。

下面，我们就分成两个部分来说明软件安装思路：

**第一部分：搞定.tar.gz**

1.首先，使用tar -xzvf来解开这个包，如：  

[?](#)

1

`#tar -xzvf apache_1_3_6_tar.gz`

这样就会在当前目录中创建了一个新目录(目录名与.tat.gz包的文件名类似），用来存放解压了的内容。如本例中就是apache_1.3.6

2.进入这个目录，再用ls命令查看一下所包含的文件，如：  

[?](#)

1

2

`#拟定cd apache_1.3.6`

`#ls`

你观察一下这个目录中包含了以下哪一个文件：configure、Makefile还是Imake。  

1）如果是configure文件,就执行：  

[?](#)

1

2

3

`#./configure`

`#make`

`#make install`

2）如果是Makefile文件,就执行：  

[?](#)

1

2

`#make`

`#make install`

3）如果是Imake文件,就执行：  

[?](#)

1

2

3

`#xmkmf`

`#make`

`#make install`

3.如果没有出现什么错误提示的话，就搞定了。至于软件安装到什么地方，通常会在安装时出现。否则就只能查阅一下README，或者问问我，:-)

如果遇到错误提示，也别急，通常是十分简单的问题：  

**1）没有安装C或C++编译器；**  

确诊方法：执行命令gcc（C++则为g++），提示找不到这个命令。  

解决方法：将Linux安装光盘mount上来，然后进入RPMS目录，执行命令：  

#rpm -ivh gcc* （哈哈，我们用到了第二种安装方式）  

**2）没有安装make工具；**  

确诊方法：执行命令make，提示找不到这个命令。  

解决方法：将Linux安装光盘mount上来，然后进入RPMS目录，执行命令：  

[?](#)

1

`#rpm -ivh make*`

**3）没有安装autoconf工具；  
**

确诊方法：执行命令make，提示找不到这个命令。  

解决方法：将Linux安装光盘mount上来，然后进入RPMS目录，执行命令：  

[?](#)

1

`#rpm -ivh autoconf*`

**4）缺少某些链接库；**  

确诊方法：在make时，提示需要某些文件。  

解决方法：安装包含这个文件的包，这就需要积累了。

**第二部分：搞定.rpm**

RPM是Red Hat公司随Redhat Linux推出了一个软件包管理器，通过它能够更加轻松容易地实现软件的安装。

1.安装软件：执行rpm -ivh rpm包名，如：  

[?](#)

1

`#rpm -ivh apache-1.3.6.i386.rpm`

2.升级软件：执行rpm -Uvh rpm包名。  

3.反安装：执行rpm -e rpm包名。  

4.查询软件包的详细信息：执行rpm -qpi rpm包名  

5.查询某个文件是属于那个rpm包的：执行rpm -qf rpm包名  

6.查该软件包会向系统里面写入哪些文件：执行 rpm -qpl rpm包名

**第三部分：搞定.deb**  

deb 是 ubuntu 、debian 的格式。  

rpm 是 redhat 、fedora 、suse 的格式。

他们不通用（虽然可以转换一下）。

deb是debian发行版的软件包  

ubuntu是基于debian 发行的 所有可以用

.deb是solaris系统下的安装包后缀名。安装方法如下

cd 到安装包的目录

dpkg -i 安装包名字

如果你使用的是red hat linux，然后运行以下命令安装

cd 到安装包的目录  

rpm -ivh 安装包名字  

以上就是本文的全部内容，希望对大家的学习有所帮助，也希望大家多多支持脚本之家。

#### 您可能感兴趣的文章:

*   [CentOS 安装软件出现错误：/lib/ld-linux.so.2: bad ELF interpreter 解决](/article/108495.htm "CentOS 安装软件出现错误：/lib/ld-linux.so.2: bad ELF interpreter 解决")
*   [linux下查看yum/rpm/dpkg某软件是否已安装的方法](/article/107877.htm "linux下查看yum/rpm/dpkg某软件是否已安装的方法")
*   [Linux上安装和卸载rpm软件包的方法](/article/97053.htm "Linux上安装和卸载rpm软件包的方法")
*   [Linux中Python 环境软件包安装步骤](/article/81780.htm "Linux中Python 环境软件包安装步骤")
*   [在Debian系的Linux中检查软件包是否被安装的方法](/article/63134.htm "在Debian系的Linux中检查软件包是否被安装的方法")
*   [Linux中服务器软件为什么需要编译安装](/article/47457.htm "Linux中服务器软件为什么需要编译安装")
*   [服务器安全狗Linux版软件安装使用说明](/article/28544.htm "服务器安全狗Linux版软件安装使用说明")
*   [Linux rpm tar 操作系统下软件的安装与卸载方法](/article/12938.htm "Linux rpm tar 操作系统下软件的安装与卸载方法")
*   [LINUX通用的软件安装方法](/article/3449.htm "LINUX通用的软件安装方法")
*   [详解linux安装软件的几种方法](/article/159155.htm "详解linux安装软件的几种方法")

[![](//files.jb51.net/image/linux_tb.gif?0404)](http://www.xiaziyuan8.com/v/linux/)

原文链接：http://blog.chinaunix.net/uid-23781137-id-3455554.html

![](//files.jb51.net/skin/2018/images/jb51ewm.png)

微信公众号搜索 “ 脚本之家 ” ，选择关注

程序猿的那些事、送书等活动等着你

*   [linux](http://common.jb51.net/tag/linux/1.htm "搜索关于linux的文章")
*   [rpm](http://common.jb51.net/tag/rpm/1.htm "搜索关于rpm的文章")
*   [tar.gz](http://common.jb51.net/tag/tar%2Egz/1.htm "搜索关于tar.gz的文章")
