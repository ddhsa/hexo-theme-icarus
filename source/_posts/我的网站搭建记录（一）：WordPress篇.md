title: 我的网站搭建记录（一）：WordPress篇
tags:
  - 网站
categories:
  - 网站搭建
date: 2019-02-05 07:44:00
---
![blob.jpg](http://cdn.pidaye.top/wangzhandajian.jpg)
## 1、准备工作
### 购买域名（然而并没有卵用）
我是在`西部数码`购买的，大家可以随便买，哪个便宜用哪个吧！
说没有用是因为最开始建站初期你有很长时间都用不到域名，等你真正调试完准备上线了之后再买域名也不迟！
### 购买云服务器
你如果跟我一样是个穷屌丝的话，也可以先不买云服务器，可以先在本机上搞个环境测试下，不过早晚都是买，可以先从便宜的云虚拟主机或者空间买，等你觉得你够牛逼了再买ECS；
另外可以在网上多关注一下优惠活动，有时候服务器包年啥的很便宜，白菜可以看情况屯；
给大家推荐几个网站吧：

- [海会主机](http://www.haihuizhuji.com "海会主机")（网站不大初级用户可以看看便宜的云主机）
- [阿里云](https://cn.aliyun.com "阿里云")（比较好用吧，我用的这个）
- [野草云](http://www.yecaoyun.com "野草云")（这个很小众但是便宜啊）
- [小夜博客](https://www.vpsmm.com "小夜博客")（可以看看这里的优惠）

### 搭建环境/调试
**环境准备：**
可以使用[XAMPP](https://www.apachefriends.org/zh_cn/index.html "XAMPP")搭建，也可以用国内比较火的[宝塔面板](https://www.bt.cn "宝塔面板")搭建，这个就不给大家演示了，比较简单都是一键式的；
**整体调试**
调试前先要搞一个[wordpress](https://cn.wordpress.org "wordpress")安装包，可以直接在[wordpress官网](https://cn.wordpress.org "wordpress官网")上下载，然后按照说明操作即完成了站点的搭建。
> *注：以下是快速安装说明*
1、 下载并解压缩`WordPress`程序安装包, 如果你还没的话.
2、在你的网页服务器上为WordPress创建一个数据库, 并且也创建一个`MySQL` 拥有所有权限可以进入和修改的用户.
3、重命名` wp-config-sample.php `文件为 `wp-config.php`.
4、用你最喜欢的 文本编辑器 打开 `wp-config.php` ，填上你的数据库信息。
5、把WordPress文件夹放在你服务器上想要放的地方:

> - 如果你想把通过顶级域名来访问你的WordPress博客 (例如 http://example.com/),移动或上传所有解压后的WordPress文件夹里面的文件(但不包括WordPress文件夹本身) 到你服务器的根目录下.
- 如果你想通过子域名来访问你的博客(例如 http://example.com/blog/), 将wordpress 重命名为你想要的子目录名称， 接着上传至你的网站服务器。 例如，你想让WordPress 安装在子目录"blog"中，你就应该将"wordpress"这个文件夹重命名为"blog"，接着上传至你的网站服务器的根目录中。

> 6、在你喜欢的浏览器中访问wp-admin/install.php 以便启动安装程序.

> - 如果你在根目录下安装WordPress,，你应该访问: http://example.com/wp-admin/install.php
- 如果你将WordPress安装在子目录blog下，你应该访问: http://example.com/blog/wp-admin/install.php

## 2、搭建操作
### 下载工具织梦源码--》wordpress下载工具织梦源码--》wordpress
### 学习了markdown语言
### 观看教学视频
### 定位网站内容，决定尝试
### 下载yusi主题
## 3、优化美化
### 调整主体样式（发现了很多坑）
表格样式、缩进、换行
### 添加音乐播放器（代码实现）

https://github.com/MoePlayer/APlayer
https://github.com/metowolf/MetingJS
https://aplayer.js.org/#/zh-Hans/


>给大家看看效果

<style>
    li {margin: 0em 0;}
    button {min-height: 0px;}
    .aplayer {margin: 0 0 1.75em 0 !important;}
</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.js"></script>
<!-- 加在页眉 -->

<div class="aplayer" data-id="2067465886" data-server="netease" data-volume="0.4"data-type="playlist" data-mode="random"></div>
<!-- 播放网易云音乐歌单 -->

<div id="aplayer">
  <pre class="aplayer-lrc-content">
        [by:呆唯yuki]
		[00:00.000] 作曲 : 関取花
		[00:01.000] 作词 : 関取花
		[00:11.35]街のおきては厳しくて
		[00:27.56]僕はいつもひとりぼっち
		[00:32.89]何にも知らない君のこと
		[00:38.20]一度愛しただけなのに
		[00:54.78]街のみんなは冷たくて
		[00:59.93]君はいつもひとりぼっち
		[01:05.26]何にも知らない僕のこと
		[01:10.78]一度愛しただけなのに
		[01:15.55]とんでもない 出来事が起きた
		[01:20.82]街中の灯が消えてった
		[01:26.21]僕以外誰が灯すのだ
		[01:31.68]君の事を誰が守るのだ
		[01:37.34]ラッターネラッターネ タバコの火を消して
		[01:42.91]ラッターネラッターネ ほら灯を灯せ
		[01:59.59]君の作ったろうそくに
		[02:04.62]僕が小さな灯を灯す
		[02:10.10]僕がラッターネを作るから
		[02:15.49]君は明かりを灯してよ
		[02:20.16]とんでもないことを起こすのだ
		[02:25.61]街中が目を覚ますまで
		[02:30.97]これ以上 大切な事は 他にはない もう他には無い
		[02:41.95]ラッターネラッターネ 暖炉の火を消して
		[02:47.74]ラッターネラッターネ ほら灯を灯せ
		[02:52.84]ラッターネラッターネ タバコの火を消して
		[02:58.00]ラッターネラッターネ ほら灯を灯せ
		[03:04.22]大停電の夜に ほら君と僕とでラッターネ
		[03:14.80]せめてものおわびに 街中に灯を灯す
		[03:25.47]ラッターネラッターネ タバコの火を消して
		[03:30.84]ラッターネラッターネ ほら灯を灯せ
		[03:36.23]ラッタ一ネラッターネ
		[03:39.02]この街の誰も僕を一人にできやしないさ
		[03:46.90]ラッターネラッターネ 踊りましょう
		[03:52.11]ラッターネラッターネ 歌いましょう
		[03:57.44]ラッターネラッターネ 目が覚めて
		[04:03.09]ラッターネラッターネ 朝が来る
    </pre>
</div>
<script>
const ap = new APlayer({
    container: document.getElementById('aplayer'),
    lrcType: 2,
    audio: [{
        name: 'ラッターネ',
        artist: ' 関取花',
        url: 'http://pan.pidaye.top/?/02音乐/関取花%20-%20ラッターネ.mp3',
        cover: 'http://pan.pidaye.top/?/02音乐/関取花%20-%20ラッターネ.jpg',
      lrc: 'http://pan.yangkai126.club/?/02%E9%9F%B3%E4%B9%90/%E9%96%A2%E5%8F%96%E8%8A%B1%20-%20%E3%83%A9%E3%83%83%E3%82%BF%E3%83%BC%E3%83%8D.lrc'
            }]
});
</script>
<!-- 播放个人歌单 -->

<script src="https://cdn.jsdelivr.net/npm/meting@2.0.1/dist/Meting.min.js"></script>
<!-- meting网易接口 -->

>实现代码

```html
<style>
    li {margin: 0em 0;}
    button {min-height: 0px;}
    .aplayer {margin: 0 0 1.75em 0 !important;}
</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/aplayer/1.10.1/APlayer.min.js"></script>
<!-- 加在页眉 -->

<div class="aplayer" data-id="2067465886" data-server="netease" data-volume="0.4"data-type="playlist" data-mode="random"></div>
<!-- 播放网易云音乐歌单 -->

<div id="aplayer">
  <pre class="aplayer-lrc-content">
        [by:呆唯yuki]
		[00:00.000] 作曲 : 関取花
		[00:01.000] 作词 : 関取花
		[00:11.35]街のおきては厳しくて
		[00:27.56]僕はいつもひとりぼっち
		[00:32.89]何にも知らない君のこと
		[00:38.20]一度愛しただけなのに
		[00:54.78]街のみんなは冷たくて
		[00:59.93]君はいつもひとりぼっち
		[01:05.26]何にも知らない僕のこと
		[01:10.78]一度愛しただけなのに
		[01:15.55]とんでもない 出来事が起きた
		[01:20.82]街中の灯が消えてった
		[01:26.21]僕以外誰が灯すのだ
		[01:31.68]君の事を誰が守るのだ
		[01:37.34]ラッターネラッターネ タバコの火を消して
		[01:42.91]ラッターネラッターネ ほら灯を灯せ
		[01:59.59]君の作ったろうそくに
		[02:04.62]僕が小さな灯を灯す
		[02:10.10]僕がラッターネを作るから
		[02:15.49]君は明かりを灯してよ
		[02:20.16]とんでもないことを起こすのだ
		[02:25.61]街中が目を覚ますまで
		[02:30.97]これ以上 大切な事は 他にはない もう他には無い
		[02:41.95]ラッターネラッターネ 暖炉の火を消して
		[02:47.74]ラッターネラッターネ ほら灯を灯せ
		[02:52.84]ラッターネラッターネ タバコの火を消して
		[02:58.00]ラッターネラッターネ ほら灯を灯せ
		[03:04.22]大停電の夜に ほら君と僕とでラッターネ
		[03:14.80]せめてものおわびに 街中に灯を灯す
		[03:25.47]ラッターネラッターネ タバコの火を消して
		[03:30.84]ラッターネラッターネ ほら灯を灯せ
		[03:36.23]ラッタ一ネラッターネ
		[03:39.02]この街の誰も僕を一人にできやしないさ
		[03:46.90]ラッターネラッターネ 踊りましょう
		[03:52.11]ラッターネラッターネ 歌いましょう
		[03:57.44]ラッターネラッターネ 目が覚めて
		[04:03.09]ラッターネラッターネ 朝が来る
    </pre>
</div>
<script>
const ap = new APlayer({
    container: document.getElementById('aplayer'),
    lrcType: 2,
    audio: [{
        name: 'ラッターネ',
        artist: ' 関取花',
        url: 'http://pan.yangkai126.club/?/02%E9%9F%B3%E4%B9%90/%E9%96%A2%E5%8F%96%E8%8A%B1%20-%20%E3%83%A9%E3%83%83%E3%82%BF%E3%83%BC%E3%83%8D.mp3',
        cover: 'http://pan.yangkai126.club/?/02%E9%9F%B3%E4%B9%90/%E9%96%A2%E5%8F%96%E8%8A%B1%20-%20%E3%83%A9%E3%83%83%E3%82%BF%E3%83%BC%E3%83%8D.jpg',
      lrc: 'http://pan.yangkai126.club/?/02%E9%9F%B3%E4%B9%90/%E9%96%A2%E5%8F%96%E8%8A%B1%20-%20%E3%83%A9%E3%83%83%E3%82%BF%E3%83%BC%E3%83%8D.lrc'
            }]
});
</script>
<!-- 播放个人歌单 -->

<script src="https://cdn.jsdelivr.net/npm/meting@2.0.1/dist/Meting.min.js"></script>
<!-- meting网易接口 -->
```

**添加视频播放器**

https://github.com/MoePlayer/DPlayer

>给大家看看效果

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.25.0/DPlayer.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.25.0/DPlayer.min.js"></script>
<!-- 在页眉引入css和js文件 -->

<div id="dplayer-427-1"></div>
<script>
(function(){
    var player = new DPlayer({
        "container":document.getElementById("dplayer-427-1"),
        "preload":"no",
        "video":{
            "url":"http://pan.pidaye.top/?/01电影/微创光电iVsom智慧运维管理平台介绍.mp4"
        },
        danmaku:{
            id:"lumo-1903-021",
            api:"https://api.diygod.me/dplayer/"
        }
    });
    window.dplayers||(window.dplayers=[]);
    window.dplayers.push(player);
})()
</script>

>实现代码

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.25.0/DPlayer.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.25.0/DPlayer.min.js"></script>
<!-- 在页眉引入css和js文件 -->

<div id="dplayer-427-1"></div>
<script>
(function(){
    var player = new DPlayer({
        "container":document.getElementById("dplayer-427-1"),
        "preload":"no",
        "video":{
            "url":"http://pan.yangkai126.club/?/01%E7%94%B5%E5%BD%B1/%E5%BE%AE%E5%88%9B%E5%85%89%E7%94%B5iVsom%E6%99%BA%E6%85%A7%E8%BF%90%E7%BB%B4%E7%AE%A1%E7%90%86%E5%B9%B3%E5%8F%B0%E4%BB%8B%E7%BB%8D.mp4"
        },
        danmaku:{
            id:"lumo-1903-021",
            api:"https://api.diygod.me/dplayer/"
        }
    });
    window.dplayers||(window.dplayers=[]);
    window.dplayers.push(player);
})()
</script>
<!-- 显示效果插入到文章正文 -->
```

**缩略图**
**字体**
**代码修改**
**新评论添加微信提醒功能**
