title: ProXmoX VE搭建家庭多媒体服务器（一）：ProXmoX VE 安装及基础配置
author: ddhsa
tags:
  - pve
  - 家庭服务器
categories:
  - 个人兴趣
date: 2019-05-15 10:22:00
---

>原文链接[基于ProXmoX VE的虚拟化家庭服务器（篇一）—ProXmoX VE 安装及基础配置](https://post.smzdm.com/p/768830/)
修改了中间的代码错误和格式调整

# 为什么用ProXmoX VE

主要还是一个朋友推荐，他自己用的是`ESXI`，觉得限制还是有的，况且`proxmox ve`兼容性好啊，我家买了一个`SYS E300-8D`买来当然不能荒废，果断选一个好用不费劲的方案

下面列一下主流的几个虚拟化方案的优缺点

  * `ESXI`-比较热门的GEN8全虚拟化系统，然而在GEN8上一直存在一些小问题，安装使用一个月，6.0以上系统的磁盘问题通过换驱动解决了，但是出现虚拟机偶尔卡住无法关机等情况，而且开关机引导时间很长

  * `UNRAID`，非常厉害的一个半虚拟化系统，配置简单，傻瓜直通，然而界面英文，我这种外文渣用起来非常难受，授权收费`basic`$59，`plus`$89，`pro`$129，存储数量依次为Basic：6个存储介质，Plus：12个存储介质，Pro：不限，申请了一个30天的试用KEY，用了2天就没用下去了，英文太难受。


最后定下来使用ProXmoX VE

# ProXmoX VE 介绍

`Proxmox VE`是一款套开源的虚拟化管理软件，用户可通过网页的方式来管理[服务器](https://www.smzdm.com/fenlei/fuwuqi/)上使用 `kvm` 以及 `lxc` 技术运行的虚拟机。同时提供了一些先进功能的支持，如`集群`、`HA`等。

`PVE`虽然是开源，却是由一个商业公司在运营、更新以及维护。

# ProXmoX VE 安装

## 基础准备

16G以上U盘一个(非必须，这个U盘是用来安装PROXMOX的，也可以直接装[硬盘](https://www.smzdm.com/fenlei/yingpan/)上，GEN8比较特殊，使用U盘引导比较方便，所以我安装在U盘上)；4G以上U盘一个；

支持虚拟化技术的CPU；

如果要虚拟软路由，需要有2个网口以上，最好千兆;

## 安装过程

首先去proxmox下载安装包，目前最新版本是5.4-1，推荐使用[种子](https://www.proxmox.com/en/downloads)下载，速度会比较快，下载完成后务必使用使用工具进行SHA256校验，防止下载错误;


### 方法一：使用U盘做启动盘安装系统

>如果你有`IPMI`那更好了直接可以用虚拟磁盘，具体方式可以跳到下一个

然后使用软碟通把下载的ISO文件刻录进4G的U盘（本人使用GEN8的ILO4远程安装，有GEN8的朋友应该知道咋弄）。

接着把4GU盘和16GU盘插入电脑，BIOS中开启虚拟化支持（具体方法百度，BIOS太多，我就不放图了），一个网口接入路由，使用4GU盘引导启动很快就会进入安装界面。

### 方法二：使用IPMI虚拟磁盘安装系统

### 安装使用

![5b9f4976ed9f19895_e600.jpg 600×375](http://cdn.pidaye.top/5b9f4976ed9f19895_e600.jpg%20600%C3%97375.png)

此处选择第一项回车，稍微等待一会，进入下图界面

![5b9f4977217c69276_e600.jpg 600×450](http://cdn.pidaye.top/5b9f4977217c69276_e600.jpg%20600%C3%97450.png)

选择 `I agree`

这里选择你要安装的的硬盘或者U盘，选定后点击`Next`

![5b9f4977859ad8338_e600.jpg 600×450](http://cdn.pidaye.top/5b9f4977859ad8338_e600.jpg%20600%C3%97450.png)

这里一般会默认`China`，如果没有那就输入china，其他默认，点击`Next`

然后输入两遍`管理密码和邮箱`，点击`Next`

![5b9f4977dc3429854_e600.jpg 600×450](http://cdn.pidaye.top/5b9f4977dc3429854_e600.jpg%20600%C3%97450.png)

这里注意，查看一下是不是你局域网的网段，如果不是，很可能和路由之间网络不通，另外，`Hostname`这项的格式需为`*.*`，默认的是无法下一步的，我这里使用PVE.LEN，点击`next`，等待安装完成，出现如下界面时，说明安装已经完成，点击`reboot`，

等待重启完成，拔掉U盘或者退出，虚拟磁盘如果顺利，会出现如下界面

![5b9f497816c518309_e600.jpg 600×361](http://cdn.pidaye.top/5b9f497816c518309_e600.jpg%20600%C3%97361.png)

# ProXmoX VE 初始配置

## 使用浏览器登录

用另外一台电脑在浏览器中输入上面的地址进行访问

![5b9f49784e6f89797_e600.jpg 600×316](http://cdn.pidaye.top/5b9f49784e6f89797_e600.jpg%20600%C3%97316.png)

`language`选择`chinese`就可以中文访问啦，用户名输入`root`，密码为刚才安装时候输的两遍管理密码

![5b9f49787f9326583_e600.jpg 600×236](http://cdn.pidaye.top/5b9f49787f9326583_e600.jpg%20600%C3%97236.png)

## 去掉订阅弹窗
由于proxmox一些功能是需要付费订阅的，虽然可以免费使用，但是每次登陆时候都会弹出如上让你订阅的通知，比较烦，我们这里通过技术手段把它屏蔽掉。

首先点击确定把它关掉，然后通过winscp打开以下文件`/usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js`，或者直接在

![5b9f49789dc6b2067_e600.jpg 600×337](http://cdn.pidaye.top/5b9f49789dc6b2067_e600.jpg%20600%C3%97337.png)

shell中使用VI等工具编辑，找到
```
if(data.status!=='Active'){
```

替换为

```
if(false){
```
这条位置比较靠后，大约在800行，替换完成后保存文件，注销登陆，清理浏览器缓存，再次登陆，发现已经不再弹窗让你订阅啦。

接下来下来我们更新一下proxomx的软件，proxmox的底层毕竟是个debian系统，刚安装还是要更新一下的，在shell中输入`apt update && apt dist-upgrade`，回车，发现报错无法更新，查看官方文档发现需要更改一些设置，在`shell`输入

```
rm -f /etc/apt/sources.list.d/pve-enterprise.list
```

添加新的

```
echo "deb http://download.proxmox.com/debian/pve stretch pve-no-subscription" > /etc/apt/sources.list.d/pve-install-repo.list
```

下载秘钥
```
wget http://download.proxmox.com/debian/proxmox-ve-release-5.x.gpg-O /etc/apt/trusted.gpg.d/proxmox-ve-release-5.x.gpg
```

再次输入
```
apt update && apt dist-upgrade
```

已经可以正常更新，等待更新完成，更新完成后重启一下虚拟机

# ProXmoX VE 磁盘映射

如果你的proxmox是直接安装在硬盘上的，那已经可以正常使用了，如果你和我一样是安装在U盘的，因为U盘空间比较小，需要弄个硬盘用来安装虚拟机

![5b9f4978cca96571_e600.jpg 600×547](http://cdn.pidaye.top/5b9f4978cca96571_e600.jpg%20600%C3%97547.png)

在磁盘中看下哪个是你要挂载的硬盘，一般推荐SSD，我这里需要挂载的设备目录为`/dev/sdb`，  


在shell中输入`mkdir /mnt/sdb`创建sdb[文件夹](https://www.smzdm.com/fenlei/wenjianjia/)用来给磁盘挂载

输入`fdisk /dev/sdb`管理这个硬盘，给它分区

输入`n`新建分区

![5b9f4978be99b1781_e600.jpg 478×108](http://cdn.pidaye.top/5b9f4978be99b1781_e600.jpg%20478%C3%97108.png)

输入`p`建立主分区，

![5b9f49791b0d89311_e600.jpg 466×120](http://cdn.pidaye.top/5b9f49791b0d89311_e600.jpg%20466%C3%97120.png)

输入`1`创建一个分区，

![5b9f49790c5c72082_e600.jpg 472×92](http://cdn.pidaye.top/5b9f49790c5c72082_e600.jpg%20472%C3%9792.png)


这里是让输入这个分区的扇区起始位置，我们选择默认，直接`回车`

![5b9f497931d597756_e600.jpg 600×40](http://cdn.pidaye.top/5b9f497931d597756_e600.jpg%20600%C3%9740.png)

分区的扇区结束位置，默认，`直接回车`，到此就分区完成了，我们输入`p`查看一下  

![5b9f4979617127416_e600.jpg 600×186](http://cdn.pidaye.top/5b9f4979617127416_e600.jpg%20600%C3%97186.png)

分区已经完成，目录为`/dev/sdb1`

输入`w`，保存并退出`fdisk`工具

输入`mkfs -t ext4/dev/sdb1`格式化一下

输入`mount/dev/sdb1 /mnt/sdb`进行挂载

输入`vim /etc/fstab`编辑一下这个文件，在最后追加

```
/dev/sdb1 /mnt/sdbext4 defaults 0 0
```
`ctrl+x`退出保存 按`Y` 是否保存 `Enter` 退出
`cat /etc/fstab` 看最后一行是否加入成功

使proxmox可以开机自动挂载.

然后依次点击数据`中心`-`存储`-`添加`-`目录`

![5b9f497979a976234_e600.jpg 600×423](http://cdn.pidaye.top/5b9f497979a976234_e600.jpg%20600%C3%97423.png)

![5b9f4979909b93240_e600.jpg 600×247](http://cdn.pidaye.top/5b9f4979909b93240_e600.jpg%20600%C3%97247.png)


`ID`随意，目录输入刚才挂载的目录，内容都选上，点添加，

最后点OS查看一下是否正常识别

![5b9f4979cb1bf7047_e600.jpg 600×131](http://cdn.pidaye.top/5b9f4979cb1bf7047_e600.jpg%20600%C3%97131.png)

----
顺便推荐下这位老哥写的其他教程
> 网络速度慢，我该怎么办？关注[**#家庭Wi-Fi布网#**](https://post.smzdm.com/p/a25rk48n/)话题，参加有奖实战征稿！关注[**#如何玩转NAS#**](https://www.smzdm.com/tag/%E5%A6%82%E4%BD%95%E7%8E%A9%E8%BD%ACNAS/post/)话题，与其用一个朝开夕倒的免费云，不如自己动手搭建一个私有云，没那么难(＾Ｕ＾)ノ~
