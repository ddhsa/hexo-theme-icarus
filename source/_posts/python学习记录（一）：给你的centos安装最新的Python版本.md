title: python学习记录（一）：给你的centos安装最新的Python版本
author: ddhsa
tags:
  - centos
  - python
categories:
  - python学习
date: 2019-06-03 17:35:00
---
# 下载最新的python
1、可利用linux自带下载工具wget下载，如下所示：

```
yum install wget
```

我安装的是最小`centos`系统，所以使用编译命令前，必须安装`wget`服务，读者如果安装的是界面centos系统，或者使用过编译工具则可跳过安装wget，直接进行下边的编译步骤 ）

```
wget http://www.python.org/ftp/python/3.7.3/Python-3.7.3.tgz
```

2、下载完成后到下载目录下，解压
```
tar -xzvf Python-3.7.3.tgz
```

3、进入解压缩后的文件夹
```
cd Python-3.7.3　　
```
![1240839-20180206154135810-550114657 473×169](http://cdn.pidaye.top/1240839-20180206154135810-550114657%20473%C3%97169.png)


# 编译python安装包
1、在编译前先在`/usr/local`建一个文件夹`python3`（作为python的安装路径，以免覆盖老的版本）
```
mkdir /usr/local/python3
```
（此处新建文件夹用`mkdir`，如果是新建文件则用`touch`）


2、开始编译安装（开始前先安装gcc `yum install gcc`我安装的是最小centos系统，所以使用编译命令前，必须安装编译套件gcc，读者如果安装的是界面centos系统，或者使用过编译工具则可跳过安装gcc，直接进行下边的编译步骤）
依次执行下面3条指令完成编译和安装
```
./configure --prefix=/usr/local/python3
```

```
make
```

```
make install
```

# 替代老版本
1、此时已经安装好新版本，但并没有覆盖老版本，再将原来`/usr/bin/python`链接改为别的名字（我保留了两个版本的，一个python，一个python3）

```
mv /usr/bin/python /usr/bin/python_old2
```
2、再建立新版本python的链接
```
ln -s /usr/local/python3/bin/python3  /usr/bin/python
```
3、这个时候输入
```
python -V
```
大功告成，enjoy it！


*PS：如果不建立新安装路径python3，而是直接默认安装，则安装后的新python应该会覆盖linux下自带的老版本，也有可能不覆盖，具体看安装过程了，这个大家可以自己试验下，当然如果还想保留原来的版本，那么这种方法最好不过了。*

# 问题汇总
## gcc编译报错
```
cannot find -lc
```
这问题一般是由于ld在进行库连接时找不到相应的库文件导致的
但是这个问题主要是少安装了两个软件包：
 `glibc-static`    `glibc-utils`
 使用指令安装确实的依赖即可
```
yum install glibc* -y
```
