title: ProXmoX VE搭建家庭多媒体服务器（二）：Frp内网穿透实现外网访问
author: ddhsa
tags:
  - frp
  - 内网穿透
  - pve
categories:
  - 个人兴趣
date: 2019-05-17 14:30:00
---

# 一、为什么要内网穿透

当然是为了方便管理啦，最好是只要在有公网的地方就可以访问家里的服务器！

其实之前用过`ZeroTier one`觉得已经很强大了，基本满足了日常应用场景，优势显而易见：

  * 简单，搭建成本低，一条指令就可以搭建起来；
  * 全平台支持，什么`Linux`、`Android`、`Windows`、`MAC OS`等等都能很好的支持；
  * 稳定性可观，`UDP`打洞成功的话基本能实现P2P连接，速度仅由双方带宽决定，很不错；
  * 操作简单，管理界面友好，`zerotier central`接管所有用户；

当然缺陷也是有的，不然我也不会放弃ta是吧：

  * UDP打洞不成功的话就基本不可用了，其实`zerotier`也是有代理的（打洞失败就启用），只是在国外而已，慢，你懂的；
  * 官方在1.10版本之后其实推出了自建代理，称之为`moon`，但是搭建起来复杂不说，成功率不高，摔；（可能是我愚笨，如果有高人成功了可以指点下）
  * 很多情况下无法打洞成功，非同城网络、多级路由、复杂网络、移动热点貌似这些都可能会导致无法连通。

总之公司网络和我的移动手机热点都不行，果断放弃。

后来又考察了市面上简单的内网穿透方案，`花生壳`、`蒲公英`，这些商业公司做的限制太多，被限制了就很蛋疼了，不爽，免费的东西也要吃了不拉肚子啊，果断找自己搭建的，即使麻烦点，用着爽才是硬道理，生命在于折腾。

比较火的几个方案`Ngrok`、`Natapp`、`Lanproxy`、`Frp`，最终选择了`Frp`，觉得最适合也是最好用，还开源，这里都给大家简单介绍下：

## Ngrok

*   项目主页：[https://ngrok.com/](https://ngrok.com/)
*   项目介绍： 一个通过任何`NAT`或防火墙为您的本地主机服务器提供即时访问、安全的URL的命令。类似花生壳，分为服务端和客户端，也可以自己搭建服务端。
*   使用教程：[点击跳转](https://yangqiang.im/?p=750)

## Ssh

_配合autossh工具使用，因为autossh会容错_

*   项目主页：[http://www.harding.motd.ca/autossh/](http://www.harding.motd.ca/autossh/)
*   项目介绍：自动重新启动`SSH`会话和隧道。autossh是一个程序，用于启动ssh的副本并进行监控，在死亡或停止传输流量时根据需要重新启动它。 这个想法来自`rstunnel（Reliable SSH Tunnel）`，但是在C中实现。作者的观点是，它不像匆匆忙忙的工作那么容易。使用端口转发环路或远程回显服务进行连接监视。在遇到连接拒绝等快速故障时，关闭连接尝试的速度。在OpenBSD，Linux，Solaris，Mac OS X，Cygwin和AIX上编译和测试; 应该在其他BSD上工作。免费软件。
*   使用教程：[点击跳转](http://www.yangqiang.im/?p=698)

## Natapp

*   项目主页：[https://natapp.cn/](https://natapp.cn/)
*   项目介绍：基于ngrok的国内收费内网穿透工具，类似花生壳，有免费版本，比花生壳好。免费版本：提供http,https,tcp全隧道穿透，随机域名/TCP端口，不定时强制更换域名/端口，自定义本地端口

## Frp

*   项目主页：[https://github.com/fatedier/frp](https://github.com/fatedier/frp)
*   项目介绍：frp 是一个可用于内网穿透的高性能的反向代理应用，支持 `tcp`, `udp`, `http`, `https` 协议。利用处于内网或防火墙后的机器，对外网环境提供 http 或 https 服务。对于 http, https 服务支持基于域名的虚拟主机，支持自定义域名绑定，使多个域名可以共用一个80端口。利用处于内网或防火墙后的机器，对外网环境提供 tcp 和 udp 服务，例如在家里通过 ssh 访问处于公司内网环境内的主机。

## Lanproxy

*   项目主页：[https://github.com/ffay/lanproxy](https://github.com/ffay/lanproxy)
*   项目介绍：lanproxy是一个将局域网个人电脑、服务器代理到公网的内网穿透工具，目前仅支持tcp流量转发，可支持任何tcp上层协议（访问内网网站、本地支付接口调试、ssh访问、远程桌面...）。目前市面上提供类似服务的有花生壳、TeamView、GoToMyCloud等等，但要使用第三方的公网服务器就必须为第三方付费，并且这些服务都有各种各样的限制，此外，由于数据包会流经第三方，因此对数据安全也是一大隐患。

## Spike

*   项目主页：[https://github.com/slince/spike](https://github.com/slince/spike)
*   项目介绍：Spike是一个可以用来将你的内网服务暴露在公网的快速的反向代理，基于`ReactPHP`，采用IO多路复用模型。采用Php实现。

## 花生壳

*   项目主页：[https://hsk.oray.com/](https://hsk.oray.com/)
*   项目介绍：商业化比较成功的内网穿透。个人开发很不推荐，收费贵，企业可以考虑使用。

`frp`内网穿透比`ngrok`要简单的多，无需多复杂的配置就可以达到比较好的穿透效果，扩展性也很强。

注意：用国内服务器搭建，需要域名备案才能使用`（划重点）`


# 二、Frp配置说明

前面说了这么多理由，话不说，现在我们来操作吧

## 1、实现功能

（1）外网通过ssh访问内网机器  
（2）自定义绑定域名访问内网web服务
（3）外网访问PVE建的交接系统的服务

## 2、配置前准备

（1）公网服务器1台（我这里用的阿里云ECS）
（2）内网服务器1台（我的就是PVE服务器啦）
（3）公网服务器绑定域名1个（方便访问搞个域名）
（4）内网服务器部署一个web服务（测试用，我这就是PVE的https界面）

# 三、安装Frp


## 下载文件
1、公网服务器与内网服务器都需要下载frp进行安装

2、下载地址是[https://github.com/fatedier/frp/releases](https://github.com/fatedier/frp/releases)

也可以通过命令下载：

```
wget https://github.com/fatedier/frp/releases/download/v0.16.1/frp_0.16.1_linux_amd64.tar.gz
```

3.在WINDOWS下用`winscp`软件登录，上传`frp_0.16.1_linux_amd64.tar.gz`至`root`目录

4.解压文件：
```
tar -zxvf frp_0.16.1_linux_amd64.tar.gz
```
>注：`frps`、`frps.ini`这个两个是服务端文件，`frpc`、`frpc.ini`这两个是客户端文件

## 配置服务端
>非常重要——由于公网服务端作为中转，千万记得端口放行和防火墙关闭，千万记得端口放行和防火墙关闭，千万记得端口放行和防火墙关闭，重要的事情说三遍，`划重点`！

1.进入解压目录：
```
cd frp_0.16.1_linux_amd64
```
frps、frps.ini这个两个是服务端文件，frpc、frpc.ini这两个是客户端文件

2.修改参数：

`vi ./frps.ini`

```
[common]
bind_port = 7000
vhost_http_port = 8090
vhost_https_port = 4430
```
`bind_port`为客户端与服务端进行通信的端口，`vhost_http_port`为服务端http服务的端口。其它更丰富的配置可参考`frps_full.ini`和项目帮助文档。

按”i”键进行编辑，按`“esc”`退出编辑状态，输入`“:wq”`退出

## 启动服务端

***临时启动***
```
./frps -c ./frps.ini
```
![手把手教你用frp实现内网穿透，进行远程桌面和http访问 - 简书](http://cdn.pidaye.top/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E4%BD%A0%E7%94%A8frp%E5%AE%9E%E7%8E%B0%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F%EF%BC%8C%E8%BF%9B%E8%A1%8C%E8%BF%9C%E7%A8%8B%E6%A1%8C%E9%9D%A2%E5%92%8Chttp%E8%AE%BF%E9%97%AE%20-%20%E7%AE%80%E4%B9%A6.webp)

公网服务端搭建成功

***设置开机启动和后台运行***

上一步中的frps占据了整个命令窗口，所以接下来要考虑如何让它在后台运行并且开机自启：
首先通过`vi /etc/systemd/system/frps.service`命令新建文件并写入以下内容:

```
[Unit]
Description=frps daemon
After=syslog.target  network.target
Wants=network.target

[Service]
Type=simple
ExecStart=/usr/frp/frp_0.16.0_linux_386/frps -c /usr/frp/frp_0.16.0_linux_386/frps.ini
Restart= always
RestartSec=1min

[Install]
WantedBy=multi-user.target
```
注意`ExecStart`中要配置成自己的路径。

然后使用`systemctl start frps`即可启动`frps`, 用`systemctl enable frps`即可将`frps`设置为开机启动。

## 配置客户端

`vi ./frpc.ini`

```
[common]  
server_addr = 120.56.37.48      #公网服务器ip  
server_port = 7000              #与服务端bind_port一致  

#公网通过ssh访问内部服务器  
[ssh]  
type = tcp                      #连接协议  
local_ip = 127.0.0.1            #内网服务器ip  
local_port = 22                 #ssh默认端口号  
remote_port = 6022              #自定义的访问内部ssh端口号  

#公网访问内部web服务器以http方式  
[web]  
type = https                     #访问协议
local_ip = 127.0.0.1            #内网服务器ip
local_port = 8006                 #内网web服务的端口号  
custom_domains = www.veelove.cn,veelove.cn   

[nasweb]
type = http                     
local_ip = 192.168.10.215       #内网桥接nas web的IP
local_port = 5000               #群晖NAS登陆地址端口是5000
custom_domains = nas.veelove.cn

[nasphoto]
type = tcp                      #协议为TCP协议
local_ip = 192.168.10.216
local_port = 80
remote_port = 8000              #需要做一个端口转发才可以实现APP登陆，端口自定义
custom_domains = photo.veelove.cn

[lede]
type = http                     #协议为http
local_ip = 192.168.10.254       #保持不变，如果您更换过lede后台地址，请自行修改
local_port = 80
custom_domains = lede.veelove.cn #更换为自己的域名

[esxi]
type = https #协议为https
local_ip = 192.168.1.101 #更换为自己esxi后台管理地址
local_port = 443
custom_domains = esxi.veelove.cn #更换为自己的域名

[dsphoto]
type = tcp #协议为tcp
local_ip = 127.0.0.1
local_port = 80
remote_port = 8000 #转发端口可以自己设定
custom_domains = photo.veelove.cn #更换为自己的域名

```

>注：所绑定的公网服务器域名，一级、二级域名都可以，绑定多个域名时用英文`“,”`分开

## 启动客户端

***临时启动***

`./frps -c ./frps.ini`

![手把手教你用frp实现内网穿透，进行远程桌面和http访问 - 简书](http://cdn.pidaye.top/%E6%89%8B%E6%8A%8A%E6%89%8B%E6%95%99%E4%BD%A0%E7%94%A8frp%E5%AE%9E%E7%8E%B0%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F%EF%BC%8C%E8%BF%9B%E8%A1%8C%E8%BF%9C%E7%A8%8B%E6%A1%8C%E9%9D%A2%E5%92%8Chttp%E8%AE%BF%E9%97%AE%20-%20%E7%AE%80%E4%B9%A6.webp)

公网服务端搭建成功

***设置开机启动和后台运行***

上一步中的frps占据了整个命令窗口，所以接下来要考虑如何让它在后台运行并且开机自启：
首先通过`vi /etc/systemd/system/frpc.service`命令新建文件并写入以下内容:

```
[Unit]
Description=frpc daemon
After=syslog.target  network.target
Wants=network.target

[Service]
Type=simple
ExecStart=/usr/frp/frp_0.16.0_linux_386/frpc -c /usr/frp/frp_0.16.0_linux_386/frpc.ini
Restart= always
RestartSec=1min

[Install]
WantedBy=multi-user.target
```
注意`ExecStart`中要配置成自己的路径。

然后使用`systemctl start frpc`即可启动`frpc`, 用`systemctl enable frpc`即可将`frpc`设置为开机启动。

# 四、穿透公司代理内网(有需要时使用)

## 1.修改服务端配置文件

`vi ./frps.ini`
```
[common]
bind_port = 443        #端口号修改为443
vhost_http_port = 80    #访问客户端web服务自定义的端口号
```
## 2.修改客户端配置文件
```
vi ./frpc.ini
```
```
[common]
server_addr = 118.24.127.138
server_port = 443                            #端口号修改为443
http_proxy = http://10.168.57.241:8088       #加入公司代理地址

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[web]
type = http
local_ip = 127.0.0.1
local_port = 80
custom_domains = www.veelove.cn
```

服务端与客户端启动方式不变


# 五、进阶设置（P2P）

## 点对点内网穿透

>这里可以使用zerotier的方案，搭建更简单一些效果差不多，下面是frp的点对点方案

`frp` 提供了一种新的代理类型 `xtcp` 用于应对在希望传输大量数据且流量不经过服务器的场景。

使用方式同 `stcp` 类似，需要在两边都部署上 `frpc` 用于建立直接的连接。

目前处于开发的初级阶段，并不能穿透所有类型的 `NAT` 设备，所以穿透成功率较低。穿透失败时可以尝试 `stcp` 的方式。

`frps` 除正常配置外需要额外配置一个 `udp` 端口用于支持该类型的客户端:
```
bind_udp_port = 7001
```
启动 frpc，转发内网的 `ssh` 服务，配置如下，不需要指定远程端口:
```
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000

[p2p_ssh]
type = xtcp
# 只有 sk 一致的用户才能访问到此服务
sk = abcdefg
local_ip = 127.0.0.1
local_port = 22
```

在要访问这个服务的机器上启动另外一个 frpc，配置如下:
```
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000

[p2p_ssh_visitor]
type = xtcp
# xtcp 的访问者
role = visitor
# 要访问的 xtcp 代理的名字
server_name = p2p_ssh
sk = abcdefg
# 绑定本地端口用于访问 ssh 服务
bind_addr = 127.0.0.1
bind_port = 6000
```

通过 ssh 访问内网机器，假设用户名为 test:
```
ssh -oPort=6000 test@127.0.0.1
```

# 附加文档：群晖NAS使用frp穿透服务

>（针对单独开穿透的群辉系统，如果前面都是桥接可以直接在PVE客户端加上所有服务即可）

## 设置ROOT密码，获取群晖的ROOT权限

1.打开控制面板,开启SSH功能


![FE841EBA-76C5-48E7-B063-351ECE53453F 1133×725](http://cdn.pidaye.top/FE841EBA-76C5-48E7-B063-351ECE53453F%201133%C3%97725.jpg)

2.终端输入命令ssh admin@192.168.1.201登录，密码为群辉NAS的用户密码（地址修改为自己的NAS地址，win用户用Putty这个软件登录）


![屏幕快照-2018-03-28-下午3.30.17 1142×732](http://cdn.pidaye.top/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-03-28-%E4%B8%8B%E5%8D%883.30.17%201142%C3%97732.png)

3.输入命令

```
sudo -i
```

4.设置root密码

```
synouser --setpw root XXX
```

【XXX便是你要修改的密码】

## 客户端调试

### 1.使用root用户登录群晖6.1
```
ssh root@192.168.1.201
```
(地址修改为自己的群晖NAS地址)

### 2.群晖NAS登陆后台配置文件
```
[common]
server_addr = 118.24.127.138
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[nasweb]  
type = http                   
local_ip = 127.0.0.1           
local_port = 5000                     #群晖NAS登陆地址端口是5000
custom_domains = nas.veelove.cn
```

### 2.使用群晖NAS手机APP的DS photo软件在外网访问配置文件
```
[common]
server_addr = 118.24.127.138
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[nasweb]  
type = http                   
local_ip = 127.0.0.1           
local_port = 5000                     #群晖NAS登陆地址端口是5000
custom_domains = nas.veelove.cn

[nasphoto]  
type = tcp                             #协议为TCP协议
local_ip = 127.0.0.1           
local_port = 80
remote_port = 8000                    #需要做一个端口转发才可以实现APP登陆，端口自定义
custom_domains = photo.veelove.cn
```
## 外网访问esxi后台管理、群晖NAS、群晖NAS客户端DS Photo、LEDE软路由后台

```
[common]
server_addr = 118.24.127.138             #更换为自己服务器IP地址
server_port = 7000

[lede]
type = http                              #协议为http
local_ip = 192.168.1.1                   #保持不变，如果您更换过lede后台地址，请自行修改
local_port = 80
custom_domains = lede.veelove.cn         #更换为自己的域名

[esxi]
type = https                             #协议为https
local_ip = 192.168.1.101                 #更换为自己esxi后台管理地址
local_port = 443
custom_domains = esxi.veelove.cn         #更换为自己的域名

[dsphoto]
type = tcp                               #协议为tcp
local_ip = 127.0.0.1
local_port = 80
remote_port = 8000                       #转发端口可以自己设定
custom_domains = photo.veelove.cn        #更换为自己的域名

[dsm]
type = http                              #协议为http
local_ip = 127.0.0.1
local_port = 5000
custom_domains = nas.veelove.cn          #更换为自己的域名
```

## 如何让Frp在群晖中自动开机运行


### 1.进入群晖控制面板》任务计划》新增》触发任务》用户定义的脚本

![屏幕快照-2018-04-23-上午7.58.15 998×568](http://cdn.pidaye.top/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%887.58.15%20998%C3%97568.png)

### 2.添加脚本
```
/root/frp/frpc -c /root/frp/frpc.ini
```
上面的frp修改为你frp目录的文件名称，我在视频里面建议是修改为frp方便记忆

![屏幕快照-2018-04-23-上午8.11.45 1005×574](http://cdn.pidaye.top/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%888.11.45%201005%C3%97574.png)

### 3.按照下图的序号号顺序操作，重启群晖NAS即可

![屏幕快照-2018-04-23-上午7.59.51 996×568](http://cdn.pidaye.top/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7-2018-04-23-%E4%B8%8A%E5%8D%887.59.51%20996%C3%97568.png)
