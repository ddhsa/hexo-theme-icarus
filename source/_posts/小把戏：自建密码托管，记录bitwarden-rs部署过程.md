title: 小把戏：自建密码托管，记录bitwarden_rs部署过程
author: ddhsa
tags:
  - docker
  - bitwarden
categories:
  - docker学习
date: 2019-03-27 16:18:00
---
> 声明：本次部署参考了[my nook](https://blog.mynook.info/post/selfhost-bitwarden/ "my nook")大神的部署方式，由于我是个小白，原文的部署方式的我来说还是不够细节，故重新整理了此文章部署过程，方便各位小伙伴参考，如有疑问欢迎各位在评论中提出。

# 缘起

之所以用自建的密码托管服务器，还是因为我一直在用的密码管理lastpassword主密码忘记了，搞得我不得不找一个**全平台、开源、好用、私有**的密码管理方式，而且刚好同事也在研究自建密码托管，说有几种很好的部署方式，综合网上的资料，偶然发现了`mynook`大神写的教程，发现大神的需求与我十分吻合，就是部署比较复杂，思前想后还是决定尝试下。

当然部署过程发现很多问题，查阅了一些资料总算是部署好了，本文应该用到的方式还是比较简单的，需要敲代码的地方也很少，得益于宝塔便捷的管理功能，很多都是图形化，简单方便！

如下便是整个部署流程：

部署项目介绍：
> 在 GitHub 上搜索时发现有人用 [Rust](https://www.rust-lang.org/en-US/) 实现了 Bitwarden 服务器，项目叫做 [bitwarden_rs](https://github.com/dani-garcia/bitwarden_rs)，并且提供了 Docker 镜像。这个实现更进一步降低了对机器配置的要求，并且 Docker 镜像体积很小，部署非常方便。此外，官方服务器中需要付费订阅的一些功能，在这个实现中是免费的。

------------


要求
==

你需要有一个域名。 机器上需要有 Docker 环境。具体参考 [Docker 官方文档](https://docs.docker-cn.com/engine/installation/linux/docker-ce/centos/#使用镜像仓库进行安装)来安装 Docker-CE。
以下是简单的部署方式:

```shell
sudo yum install /path/to/package.rpm
sudo systemctl start docker
sudo docker run hello-world
```

此外，本文使用 docker-compose 来管理服务，参考 [docker-compose 的官方文档](https://docs.docker.com/compose/install/)来安装。在 Linux 上可以一行命令安装：

```shell
sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
```


如果要更新 docker-compose，也可以直接使用这条命令，只需要修改版本号为最新的 docker-compose 版本号。

最后就是安装bitwarden_rs：
可参考[bitwarden_rs](https://github.com/dani-garcia/bitwarden_rs "bitwarden_rs")中的文档

```shell
docker pull mprasil/bitwarden:latest
```

配置文件
====

假设你准备在主目录中存放数据，新建一个目录：

```shell
cd ~ && mkdir bitwarden && cd bitwarden
pwd
# 应当输出 /home/username/bitwarden
```

准备一个配置文件：

```shell
cat >> config.env <<EOF
SIGNUPS_ALLOWED=true
DOMAIN=https://example.com
DATABASE_URL=/data/bitwarden.db
ROCKET_WORKERS=10
WEB_VAULT_ENABLED=true
EOF
```

以上配置文件的说明：

*   `SIGNUPS_ALLOWED` 控制是否开放用户注册，因为你必须先注册才能存储数据，所以暂且先打开；
*   `DOMAIN` 填入你准备分配给 Bitwarden 服务使用的域名；
*   `DATABASE_URL` 设置数据库在容器内的路径，你可以不设置，默认位于 `/data/db.sqlite3`；
*   `ROCKET_WORKERS` 设置服务器使用几个线程。10 是默认值，你可以根据机器性能和个人需求适当调整；
*   `WEB_VAULT_ENABLED` 设置是否开启 Web 客户端。如果开启，可以通过访问你的域名来打开 Web 客户端，用户登录后即可通过网页管理密码。因为注册用户需要，所以也暂且先打开；

准备服务描述文件：

```shell
cat >> docker-compose.yml <<EOF
version: '3'

services:
  bitwarden:
    image: mprasil/bitwarden:latest
    container_name: bitwarden
    restart: always
    volumes:
      - ./data:/data
    env_file:
      - config.env
    ports:
      - "6666:80"
EOF
```

这个文件主要描述了这些内容：

*   `bitwarden` 现在是唯一一个服务；
*   `image: mprasil/bitwarden:latest` 指定使用 Docker Hub 的 `mprasil/bitwarden` 最新镜像；
*   `volumes` 中指定将容器内的 `/data` 目录挂载到宿主机的当前目录下的 `data` 目录，这样你可以在宿主机上执行数据库的备份操作；
*   `ports` 指定将容器内的 80 端口映射到了宿主机的 6666 端口；

以后对 bitwarden 服务做的所有操作，都需要预先进入这两个配置文件所在的目录内。

反向代理和 HTTPS、启动服务
================

> 因为服务描述文件中将 bitwarden 服务的 80 端口映射到了宿主机的 6666 端口，你可以在宿主机上使用 nginx 或其他反向代理，为你的域名配置对应的代理规则，使得访问域名时，流量可以经由 bitwarden 服务来处理。使用 nginx 的配置文件部分内容如下：

```shell
location / {
    proxy_pass http://127.0.0.1:6666;
    proxy_set_header Host $http_host;
     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

注：以上是大佬的原文，实际操作还是很复杂的，在这里可以用宝塔自带的配置下我们的域名网站：
1、建立网站，用你准备的那个域名常规建站（我这里用的WEB服务器是Nginx）
2、设置反向代理，即将自己的域名代理到内部127.0.0.1:6666上（注意在防火墙中开放你的端口）
3、最后配置HTTPS，可直接在网站设置里面导入证书，证书可以免费在阿里云上获取

> **此外，现在是 2018 年，还请为域名配置 HTTPS 证书，并将 HTTP 流量阻挡或重定向到 HTTPS。这是对数据安全的基本尊重。**这方面的配置可以参考[《快速配置 HTTPS》](https://blog.mynook.info/post/fast-way-to-configure-a-https-site/)。

如果你使用 traefik 或其他反代方案，请自行参考工具各自的官方文档完成配置。

最后启动服务：

```shell
docker-compose up -d
```


用户注册和数据导入
=========

启动服务后，通过浏览器访问你配置好的域名，应当看到下图所示的登录界面。

![](http://cdn.pidaye.top/wp-content/uploads/2019/03/bitwarden-web-vault-login-856%C3%97754.png)

点击下方链接进入注册页面。

![](http://cdn.pidaye.top/wp-content/uploads/2019/03/bitwarden-web-vault-register-824%C3%971158.png)

注册完毕之后不需要验证邮箱（bitwarden_rs 目前没有实现邮件相关的功能），直接登录。登录之后在左侧栏的「工具」菜单中找到数据导入页面，如图。

![](http://cdn.pidaye.top/wp-content/uploads/2019/03/bitwarden-import-940%C3%97584.png)

在这里进行数据导入就可以啦。

关闭用户注册、关闭 web vault
===================

现在你的 Bitwarden 服务器允许任何人注册帐号使用，你可能希望关闭这个功能。在前面生成的 `config.env` 中，调整以下两项值：

    SIGNUPS_ALLOWED=false
    WEB_VAULT_ENABLED=false


修改之后，需要重启 bitwarden 服务才生效。运行以下命令来删除并重新创建容器。不必担心，因为指定了 `volume` 映射，你的数据不会被删除。

    docker-compose down && docker-compose up -d


这样就关闭了用户注册功能，并禁用了 web vault 的访问。密码数据之后还是可以在客户端中进行编辑的。

客户端的使用
======

安装配置好服务端后，还需要在客户端上登录，将数据同步过来，才能使用自动填充等功能。Bitwarden 的客户端界面都大同小异，这里以 Firefox 扩展为例。

首先在登录界面，点击左上角齿轮图标的设置按钮。

![](http://cdn.pidaye.top/wp-content/uploads/2019/03/bitwarden-client-login-748%C3%97754.png)

在设置界面，只需要在最上面的服务器地址栏中，填写你的 Bitwarden 服务器地址即可。然后点击设置界面右上角的「保存」。接下来使用你的邮箱和主密码登录即可同步数据。

![](http://cdn.pidaye.top/wp-content/uploads/2019/03/bitwarden-client-settings-login-748%C3%97608.png)

注意事项
====

对于使用任何密码管理工具的人来说，主密码的重要性不言而喻。一旦主密码泄漏，相当于将所有帐号密码拱手相让；一旦主密码丢失，所有数据也都化作随机噪音，变得一文不值。所以，请时常审视、改进你的安全策略，定期对帐号做安全审查，不定期修改并牢记主密码。

*   [安全](https://blog.mynook.info/tags/%E5%AE%89%E5%85%A8)
*   [SafeInCloud](https://blog.mynook.info/tags/safeincloud)
*   [Enpass](https://blog.mynook.info/tags/enpass)
*   [Bitwarden](https://blog.mynook.info/tags/bitwarden)
*   [密码](https://blog.mynook.info/tags/%E5%AF%86%E7%A0%81)
*   [密码管理](https://blog.mynook.info/tags/%E5%AF%86%E7%A0%81%E7%AE%A1%E7%90%86)
*   [工具](https://blog.mynook.info/tags/%E5%B7%A5%E5%85%B7)
*   [Docker](https://blog.mynook.info/tags/docker)
