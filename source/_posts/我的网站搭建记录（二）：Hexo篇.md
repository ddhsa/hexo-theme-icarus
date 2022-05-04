title: 我的网站搭建记录（二）：Hexo篇
author: ddhsa
tags:
  - hexo
  - 静态网站
categories:
  - 网站搭建
date: 2019-05-07 18:26:00
---
>其实之前用过`wordpress`部署自己的博客系统，也一直觉得wp还是很适合我这种小白使用的，得益于丰富的插件，强大的后台管理，数不胜数的主题，wp深受大家的喜欢。
但是wp的臃肿让我在后期使用中愈发觉得难以接受，而且完全依赖后台的写作方式也让我很是不爽，总觉得这种写博客的方式不是最佳的、可靠的。

想了解`WordPress`的可以看这篇{% post_link 我的网站搭建记录（一）：WordPress篇 %}

一次翻阅docker文章的过程发现了`hexo`这个神物，当时没太留意，以为静态网页这种东西很麻烦，后来闲来无事决定体验以下`hexo`，一用果然升天了。本地部署写好了文章后`git`到任何地方这才是我要的体验啊，而且由于hexo生成的是全静态网站，托管和呈现就更加简单了，如果你想搭建一个自己的博客，强烈推荐`hexo`。

***什么是Hexo***
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 `Markdown`（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。并且有很多人为其制作了很多优秀的主题（`theme`）。我选择Hexo主要有以下五点:

  * 主题选择多而且美
  * 一键部署
  * 编译文章速度极快
  * 丰富的插件
  * 支持MarkDown
话不多说，直接进入主题．

# 一、基础篇
## Hexo的安装

因为我用的`debian9`的系统，安装这部分的内容，适合`linux`用户．`Windows`安装可以参考下面这二篇文章

[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249 "https://zhuanlan.zhihu.com/p/26625249")

[手把手教你用Hexo+Github 搭建属于自己的博客](https://blog.csdn.net/gdutxiaoxu/article/details/53576018 "https://blog.csdn.net/gdutxiaoxu/article/details/53576018")

*PS：如果安装的`git`是绿色便携版请将目录添加到系统环境变量`path`中*

### 安装准备
安装 Hexo 相当简单。最主要就是需要下面这二个软件

  * Node.js
  * Git

### 安装Hexo
Debian下要先把`sh`改成`bash`,运行下面的命令，选择否。(Centos可以跳过这一步!)
```
dpkg-reconfigure dash
```
![Hexo+Github搭建自己的博客 --- 心得汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.png)
下载安装脚本并执行。
```
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
source /root/.bashrc
nvm install stable
```

测试安装环境是否准备好了

```
npm -v
node -v
```

运行安装命令

```
mkdir /mnt/blog
cd /mnt/blog
npm install -g hexo-cli
hexo init
```

这样就安装好了。简单吧！接下来就是把hexo运行起来。

*备注：`/mnt/blog`这个目录，你可以改成你自己要安装的目录。*

### 运行hexo
注意：所有hexo命令都要在自己建的这个`blog`这个主目录来执行。

`hexo g && hexo s`
这里说明一下hexo 的几个常用命令

命令简写
```
hexo init #初始化博客
hexo g == hexo generate #生成博客
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署
```

常用命令：
```
hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
```

测试
![Hexo+Github搭建自己的博客 --- 心得汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)
*注意：不要按`Ctrl+C` 关掉了*

然后在浏览器出输入你的`IP`地址加`4000`端口号就可以正常看到了hexo了,如果端口号显示占用，请在`hexo s`后面加`-p 5000`或者其他端口．


*备注：用Centos的同学记得要先把防火墙给关了。如何关闭Centos防火墙?百度一下吧*

## 主题（以`Next`为例）
Hexo主题是他的强项，网上有非常多的主题支持。都非常好看。想具体了解的话，可以看看这篇Hexo有哪些好看的主题?

### 安装主题
Hexo 安装主题的方式非常简单，只需要将主题文件拷贝至站点目录的 `themes` 目录下， 然后修改下配置文件即可
在这我们使用git克隆最新版
```
cd /mnt/blog
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### 启用主题
将Next主题下载到blog目录的themes主题下的next文件夹中。打开站点的`_config.yml`配置文件，修改主题为next

然后打开主题的_config.yml配置文件，不是站点配置文件，找到Scheme Settings
![Hexo+Github搭建自己的博客 --- 心得汇总2018版安装篇  思想就是武器12](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A812.jpg)

next主题有三个样式，我用的是`Gemini`，你们可以自己试试看，选择你自己喜欢的样式(只需要把行首的#去除，#是注释)。然后执行
```
hexo clean && hexo s
```
再在浏览器输入IP地址，就可以看到效果了。

>备注：这里需要注意一下_config.yml这个文件有二个。一个是站点根目录下有一个_config.yml，叫站点配置文件。另外一个是主题next目录下也有一个_config.yml，叫主题配置文件，不要搞错了。

---

# 二、优化篇(next主题)

## 改语言

## 改首页描述

## 添加标签分类界面（！）

## 设置侧边栏设置圆形可旋转头像（设置头像）

## 点击出现桃心效果
![Hexo-Github搭建自己的博客 --- 心得汇总2018版（主题配置篇）  思想就是武器](http://cdn.pidaye.top/Hexo-Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%EF%BC%88%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E7%AF%87%EF%BC%89%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.gif)
设置方法：

```
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
```

然后将里面的代码copy一下，新建`love.js`文件并且将代码复制进去，然后保存。

将`love.js`文件放到路径`themes/next/source/js/src`里面，然后打开`themes/next/layout/_layout.swig`文件,在末尾（在前面引用会出现找不到的bug）

添加以下代码：

```
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
```

## 添加RSS
![Hexo-Github搭建自己的博客 --- 心得汇总2018版（主题配置篇）  思想就是武器](http://cdn.pidaye.top/Hexo-Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%EF%BC%88%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E7%AF%87%EF%BC%89%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)
设置方法：
执行以下命令安装`RSS插件`

```
npm install hexo-generator-feed --save
```

编辑网站根目录下的`_config.yml`，添加以下代码开启

```
plugin:
- hexo-generator-feed
feed:
type: atom
path: atom.xml
limit: 20
```

## 结尾添加“文本结束”
设置效果：
![Hexo-Github搭建自己的博客 -23231-- 心得汇总2018版（主题配置篇）  思想就是武器](http://cdn.pidaye.top/Hexo-Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20-23231--%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%EF%BC%88%E4%B8%BB%E9%A2%98%E9%85%8D%E7%BD%AE%E7%AF%87%EF%BC%89%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)

设置方法：
在路径`themes/next/layout/_macro`中新建`passage-end-tag.swig`文件,并添加以下内容：

```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">
            -------------本文结束
            <i class="fa fa-paw"></i>
            感谢您的阅读-------------
        </div>
    {% endif %}
</div>
```

接着打开`themes/next/layout/_macro/post.swig`文件，在`post-body`之后，`post-footer`之前添加如下代码,(大概在350行左右的位置)：

```
<div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```

然后打开主题配置文件`_config.yml`,在末尾添加：
```
passage_end_tag:
  enabled: true
```
>备注：如果文字显示乱码，请将文件编码改成utf-8格式；

## 修改结尾#标签
## 首页不显示全文(只显示预览)
## 添加顶部加载条
## 侧边栏推荐阅读
## 添加联系方式
## 添加打赏功能
## 显示阅读百分比
## 加入valine在线评论
## 显示文章热度（？）
## 增加搜索侧边栏
### 1.在hexo的根目录下执行命令：
```
npm install hexo-generator-searchdb --save
```

### 2.在根目录下的/theme/next/_config.yml文件中添加配置:
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

### 3.在根目录下的/theme/next/_config.yml文件中搜索`local_search`，将`enable`改为`true`：

```
local_search:
  enable: true
```

---
# 三、高阶尝试
## 将hexo部署到Github
### 去github网站去注册一个帐号
创建账号这个我就不说了吧，自行百度。

### 创建一个`xxx.github.io`的public仓库
![Hexo+Github搭建自己的博客 --- 心得汇总2018版安装篇  思想就是武器2](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A82.jpg)
![Hexo+Github搭建自己的博客 1221](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%201221.jpg)

### 安装 `hexo-deployer-git`
```
npm install hexo-deployer-git --save
```

网站配置git
把网站的`_config.yml`配置文件拉到最后配置`deploy`

![Hexo+Github搭建自己的博客 --汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20--%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)

![Hexo+Github搭建自己的博32432客 --- 心得汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A32432%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)

然后在电脑上配置`git`
```
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

生成ssh密钥文件：运行之后什么都不用输入，直接按三次回车。

```
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```
最终会生成一个文件在用户目录下，打开用户目录，找到`.ssh\id_rsa.pub`文件，

```
cat ~/.ssh/id_rsa.pub
```
复制里面的内容，
![Hexo+Github搭建32234自己的博客 --- 心得汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA32234%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)

打开你的github主页，进入`个人设置` -> S`SH and GPG keys` -> `New SSH key`：
![Hexo+Github搭建自己的博423432客 --- 心得汇总2018版安装篇  思想就是武器](http://cdn.pidaye.top/Hexo+Github%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A423432%E5%AE%A2%20---%20%E5%BF%83%E5%BE%97%E6%B1%87%E6%80%BB2018%E7%89%88%E5%AE%89%E8%A3%85%E7%AF%87%20%20%E6%80%9D%E6%83%B3%E5%B0%B1%E6%98%AF%E6%AD%A6%E5%99%A8.jpg)

大功告成
输入这条命令将hexo部署到github

```
hexo clean && hexo g && hexo d
```

最后在浏览器中输入xxxx.github.io这个网址就可以享受自己的劳动果实了。

>技巧： 在命令行输入alias up='hexo clean && hexo g && hexo d' 这样以后直接输入up。就可以把hexo部署到github上了。


## 将hexo静态网站部署到七牛云
> 一直有关注过七牛云。它的访问统计分析和CND加速功能让我很心动。正好之前用的服务器也快到期了。所以尝试着把博客部署到七牛云上。下面介绍一下将Hexo生成的页面部署到七牛云

### 准备

[七牛云](https://www.qiniu.com/)：

*   七牛云是云服务商，为用户提供免费的存储空间，CND加速，图片处理等功能。
*   注册七牛云，实名认证，创建储存空间，绑定域名，融合CDN，缓存设置等这里就不赘述了。

[qshell](https://developer.qiniu.com/kodo/tools/1302/qshell)：

*   shell是七牛提供的命令行上传工具，可以将本地的文件快速上传到七牛云

[Hexo](https://hexo.io/zh-cn/)：

*   这个不用多说大家都知道是博客框架

### 安装使用qshell

[qshell下载](http://devtools.qiniu.com/qshell-v2.3.6.zip)

下面介绍`Mac`系统下的安装和使用方法，其它系统可以参考[文档](https://github.com/qiniu/qshell#%E5%AE%89%E8%A3%85)

### 安装

该工具由于是命令行工具，所以只需要从上面的下载之后即可使用。其中文件名和对应系统关系如下：

文件名|描述
-|-
qshell_linux_x86|Linux 32位系统
qshell_linux_x64|Linux 64位系统
qshell_windows_x86.exe|Windows 32位系统
qshell_windows_x64.exe|Windows 64位系统
qshell_darwin_x64|Mac 64位系统，主流的系统

1）权限： 如果在Linux或者Mac系统上遇到`Permission Denied`的错误，请使用命令 `chmod +x qshell_darwin_x64` 来为文件添加可执行权限。`qshell_darwin_x64` 是上面的文件名，各个系统不一样

2）任何位置运行 对于Linux或者Mac，如果希望能够在任何位置都可以执行，那么可以把qshell所在的目录加入到环境变量`$PATH`中去。假设qshell命令被解压到路径`/Users/coder/Downloads`目录下面，那么我们可以把如下的命令写入到你所使用的bash所对应的配置文件中，如果是`/bin/bash`，那么就是`<sub>/.bashrc`文件，如果是`/bin/zsh`，那么就是`</sub>/.zshrc`文件中。写入的内容为：

```
export PATH=$PATH:/Users/coder/Downloads
```
保存完毕之后，可以通过两种方式立即生效，其一为输入`source ~/.zshrc`或者`source ~/.bashrc`来使配置立即生效，或者完全关闭命令行，然后重新打开一个即可，接下来就可以在任何位置使用`qshell`命令了。

### 使用

添加密钥和账户名称

该工具有两类命令，一类需要鉴权，另一类不需要。
需要鉴权的命令都需要依赖七牛账号下的 `AccessKey`, `SecretKey`和 `Name`。所以这类命令运行之前，需要使用 `account` 命令来添加 `AccessKey` ，`SecretKey`和`Name` 。 `Name`是用户可以自定义的字符串，用来唯一表示`AccessKey/SecretKey`账户，qshell会对添加的每一个账户信息加密保存，可以使用自命令user进行切换，切换账户的时候，需要使用账户唯一标识 Name。

```
$ qshell account <Your AccessKey> <Your SecretKey> <Your Name>
```

其中name表示该账号的名称, 如果`ak`, `sk`, `name`首字母是`"-"`, 需要使用如下的方式添加账号, 这样避免把该项识别成命令行选项:

```
$ qshell account -- <Your AccessKey> <Your SecretKey> <Your Name>
```

添加完账户后，就可以使用qshell上传，下载文件了

更详细的信息也可以参考文档[传送门](https://github.com/qiniu/qshell)

### Hexo配置

现在我们可以在Hexo项目的根目录下创建`upload.conf`文件

```
{
  // 这个地址是根目录地址，不可使用相对路径
  "src_dir": "/Users/coder/7coder/7coder-blog/public",
  // 储存空间名称
  "bucket": "7coder",
  // 是否覆盖
  "overwrite" : true,
  // 检查新增文件
  "rescan_local" : true
}
```
*如果是windows系统请使用以下指令*

```
{
  "src_dir": "D:\\Users\\coder\\7coder\\7coder-blog\\public",
  "bucket": "7coder",
  "overwrite" : true,
  "rescan_local" : true
}
```

Hexo生成的静态页面全部放在public文件夹下，所以`src_dir`应当是要以`/public`结尾的。

接下来可以使用`qshell`来上传文件了
```
qshell qupload upload.conf
```

执行后就会打印出同步的文件，然后访问你的空间域名就可以了。

关于qupload命令可以阅读详细文档[传送门](https://github.com/qiniu/qshell/blob/master/docs/qupload.md)

今后写完博客只需下面两条命令就可以完成部署了

```
hexo generate
qshell qupload upload.conf
```
windows下直接双击脚本即可

### 一键部署

我们的目的是实现一键部署，但是上面使用了两条命令才搞定。

打开Hexo下的package.json，填入以下代码

```
"scripts":{
    "publish": "hexo generate && qshell qupload upload.conf"
  }
```

今后只需要 `npm run publish` 就可实现一键打包部署到七牛云啦~

### 附

*   如果上传成功但是访问无变化，可能是七牛的缓存原因。可以前往`域名管理`修改缓存配置
*   七牛云的默认访问会在域名后拼上`/index.html`,可以前往空间设置开启默认首页
*   在写文章的过程中，有时候需要引用站内的其他文章。可以通过内置的标签插件的语法`post_link`来实现引用。
    ```
    {% post_link 文章文件名（不要后缀） 文章标题（可选） %}
    ```
    举例 引用 Hello.md
    ```
    {% post_link Hello %}
    ```
    或者
    ```
    {% post_link Hello 你好 %}
    ```
## hexo图片编辑自动上传七牛图库

>此应用方式是将七牛静态网站和图片分别保存，方便管理，因此图片存储我专门又建了一个公开空间，然后用另外的二级域名实现cdn加速

众所周知hexo文章支持markdown编辑，大大方便了文章的编写，但是图片存储的问题是我们比较棘手的，我这里给大家推荐下我目前在用的方式，仅供参考，基本实现了自动上传，还是十分方便的；

### 使用hexo-admin管理网站
hexo没有图形化的后台管理界面，这个是大家不太习惯的地方，好在hexo插件丰富，这里推荐hexo-admin来实现图形化后台，主要用于建立post，好像其他的功能也都容易抽猝：

>注：如果你跟我一样嫌(tai)麻(lan)烦(le)的话，那么利用Hexo-admin插件，加上自己部分diy，也许一个自己比较满意的Hexo博客发布方式就到手了，岂不是一大爽事。

> 就是这个feel~倍儿爽

反正我就是懒，不要拉我，让我懒。其实有时候这种“懒”往往能促使人进步，如果不嫌麻烦甘于重复劳动，虽然会少掉很多折腾，但也会少掉很多发现和进步。  
好了，鸡汤喝完，该说正事儿了。

**hexo-admin官网**  
[https://jaredforsyth.com/hexo-admin/](https://link.jianshu.com?t=https://jaredforsyth.com/hexo-admin/)

#### step 1

安装必要环境：`NodeJs`、`Hexo-cli`、`Hexo`等

#### step 2

初始化博客，一般到这里你应该是已经初始化自己的博客了，如果还没有的话，请看下面

````
cd /usr/local/
hexo init yourblog
cd yourblog
npm install
````

#### step 3

安装hexo-admin插件，并且启动hexo服务，打开浏览器访问能看到基本的界面

```
npm install --save hexo-admin
hexo server -d
open http://localhost:4000/admin/
```

**登录界面**  

![5548926-76381c3b23a04058.png 1000×323](http://cdn.pidaye.top/5548926-76381c3b23a04058.png%201000%C3%97323.webp)


到这里，没进行配置的小伙伴可能还无法登录，请接着往下看。

#### step 4

在hexo的_config.yml配置hexo-admin
```
admin:
   username: zoro
   password_hash:be121740bf988b2225a313fa1f107ca1
   secret: hey hexo
   deployCommand: './admin_script/hexo-generate.sh'
```

>注
1、password_hash就是密码，通过bcrypt hash，你可以用尽你一切手段对自己的密码做一个bcrypt加密，C/Java/Python都可以，做人嘛，重要的是嗨森；  
2、secret用以cookies安全；  
3、deployCommand就是一个关键点，不要着急，下面给出说明；

**主页**  

![](//upload-images.jianshu.io/upload_images/5548926-cfba47671e9c6e9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

*   Post：博客文章列表，包括已经发布的和还在草稿箱等待宠幸的；
*   Pages：就是诸如标签云之类的页面管理；
*   About：关于admin插件的说明
*   hexo-gen：这个原来是Deploy，被我修改了，关键节点；
*   Settings:配置；

#### step 5

先解释一下上面配置的那个`deployCommand`的用处，目的在于页面上你点击了Deploy页面下面的Deploy按钮的时候，所执行的脚本，这里格子拿它来作为执行`hexo g`的载体。  
说到这里，可能有些人不是很理解为什么要这么做，看官莫急，听我细细道来。  
其实，当你以`hexo server -d`启动了hexo服务的时候，hexo-admin插件在你修改了 某篇博已发布博客，或者新发布博客的时候，会在后台帮你执行一系列操作，所以这个时候，你可以通过`http://localhost:4000`访问就可以看到刚才发布到博客了，看到这里，有读者应该就要心里问候：那你是不是傻，为什么还要折腾？容我说一句，原因只有一点：以`hexo server`启动的hexo对外提供的服务，并不是特别稳定，访问略慢，毕竟不是专门的web服务容器，而且如果你不以`nohup`方式启动的话，一旦关掉Xshell等操作界面的时候，就会被迫关掉，所以带来了一系列令人不喜的体验，这就是我折腾的唯一原因。  
因此，其实格子是以Nginx为web服务容器对外提供博客服务，每次将新博客生成静态Html放到Nginx配置的目录下，速度不要太快；格子的云主机只有`1G内存 单核CPU`,还是能有不俗的访问体验，所以觉得还算没白折腾。  


所以，**重点**
来了，在_config.yml里面填写好deployCommand的存储路径之后，在该路径下生成脚本；

```
touch hexo-generate.sh;
vim hexo-generate.sh;
```

输入以下内容
```
    #!/usr/bin/env sh
    hexo g
```

保存退出，并赋予执行权限

执行Shift+:，输入q，如下
```
    :q
    chmod +x hexo-generate.sh
```

#### step 6

验证效果，可以先行验证是否有效果  
1、启动hexo server  
2、访问`http://localhost:4000/admin`并登陆  
3、进入`Posts`页面，新建博客并编写发布；  
4、进入`Deploy`页面（如果你还没改掉改名称的话），点击下面的Deploy按钮  
5、进入博客目录`->public`，查看相应的html是否有生成，如果有，那么恭喜你成功了。

### 使用atom编写markdown文章

上一个步骤实现了后台管理，虽然hexo-admin可以发布和编辑文章，但是为了更加专注写作和保障稳定性，现在给大家介绍一个编辑工具`Atom`，这个工具不仅解决了编辑，同时也解决了图片上传的问题，这个才是我们重点要解决的问题：

#### step 1
准备一个七牛空间，专门用于图片存储的，详细步骤可参考`七牛cdn`，这里给大家看看效果吧：
![Clipboard - 2019-05-20 16.41.09](http://cdn.pidaye.top/Clipboard%20-%202019-05-20%2016.41.09.png)
这一步是建立一个cdn对象存储空间，用于存放图片和cdn加速,这里需要记住你的空间名称如：`blog`和域名如：`XXX.XXX.com`；
![Clipboard - 2019-05-20 16.42.14](http://cdn.pidaye.top/Clipboard%20-%202019-05-20%2016.42.14.png)
如上图得到我们的秘钥，即`AK`、`SK`，这里后面需要用到；

#### step 2
下载`atom`，官网地址(可能需要出国)：
[Atom官网](https://atom.io)

#### step 3
下载安装后这里要安装一个扩展插件，`Markdown Preview Enhanced`
![Clipboard - 2019-05-20 16.51.53](http://cdn.pidaye.top/Clipboard%20-%202019-05-20%2016.51.53.png)

这个插件的功能就是实现将本地图片文件自动`upload`到七牛空间中，而且是拖动文件就能实现哦，是不是很方便；

![Clipboard - 2019-05-20 16.49.49](http://cdn.pidaye.top/Clipboard%20-%202019-05-20%2016.49.49.png)

>注：
*   在Image Upload这一项选择qiniu
*   Qiniu AccessKey填上你的AK
*   Qiniu SecretKey填上你的SK
*   Qiniu Bucket填上你的空间名称
*   Qiniu Domain填上你的cdn域名

ok，enjoy it！

## hexo开机启动

> Hexo安装hexo-admin组件以后，所有的操作都可以在浏览器中轻松完成了，但是有一个问题就是每次开机都需要运行一次`hexo s`

### windows下配置开机启动

为了更方便的使用，寻找一种可以开机启动`hexo server`的方法，通过脚本实现。  
需要创建2个脚本，一个为`vbs`脚本，一个为`bat`脚本。

vbs脚本放到启动文件夹，用于运行bat脚本，而bat脚本用于启动`hexo server`

#### 创建vbs脚本
```
    set ws=WScript.CreateObject("WScript.Shell")
    ws.Run "E:\\WorkSpace\\webProject\\Hexo-blog\\hexo-server.bat /start",0
```
#### 创建bat脚本
```
    E:
    cd E:/WorkSpace/webProject/Hexo-Blog
    hexo s -d
```
#### 将vbs脚本放到启动文件夹

win10 启动文件夹目录为  
`C:\Users\你的用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`

这样就能实现开机启动hexo server了，剩下的一切都可以交给`浏览器`和`hexo-admin`了。如果使用七牛，则可以使用[hexo-admin with qiniu](https://github.com/xbotao/hexo-admin)

## 电脑重装后如何恢复hexo
电脑重装系统后需要恢复hexo的安装状态，这就需要重新配置环境和安装hexo了；
### 安装基础环境
1、重新安装配置Node.js环境
*   下载node
*   查看node和npm版本

2、git环境安装确认
*   下载安装git
*   关联GitHub
### 安装hexo
```
npm install hexo-cli -g
npm install hexo --save
hexo -v
```
安装相应的依赖
```
npm install
```
