title: Linux学习记录（五）：Manjaro + i3安装和配置流程
author: ddhsa
tags:
  - linux
  - Manjaro
  - i3wm
  - 安装配置
categories:
  - linux学习
date: 2019-07-08 14:41:00
---
# 安装

## U盘烧录
  * 使用sufus烧录镜像
  * 选择DD模式

## boot设置
  * 使用EIFI模式选择U盘启动
  * 将secure boot模式为常规模式None

## 安装Manjaro到硬盘
  * 分区
  * 安装

# 设置

## 常规设置
将软件源切换到国内
修改配置文件`/etc/pacman.conf`
添加
```
[archlinuxcn]
SigLevel = Never
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

将源全部改到国内
```
sudo pacman-mirrors -c China
```

软件更新`sudo pacman -Syyu`

simplescreenrecorder
screenkey

选择编辑器vim

高亮pacman`/etc/pacman.conf`中#36中的color

改shell，使用fish
chsh -s /usr/bin/fish
curl -L https://get.oh-my.fish | fish
drau

使用alias自定义快捷键
eg:alias c clear
funcsave c
alias s screenfetch
funcsave s


## 提高效率使用i3
sudo pacman -S i3
vim ~/.Xresoures
Xft.dpi: 200
screenkey

修改终端alacritty
dmenu
exec_always alacritty
size: 18

改键位
sudo pacman -S xorg
xmodmap -pke > ~/.xmodmap
xev

xmodmap ~/.xmodmap生效

vim ~/.config/i3/config

new_window 1pixel

sudo pacman -S lxappearance
azut、papirus、brzze

壁纸管理器
sudo pacman -S feh
variety

alacritty》》opacity

compton

安装输入法
sudo pacman -S fcitx fcitx-im fcitx-configtool
sudo pacman -S fcitx-sogoupinyin

vim ~/.xprofile

export GTK IM MODULE=fcitx
export QT IM MODULE=fcitx
export XMODIFIERS="@im=fcitx"

安装Chrome浏览器
sudo pacman -S chromium

剪辑视频
sudo pacman -S kdenlive

修图gimp

邮件thunderbird

office安装libreoffice

vlc

虚拟机virtualbox

deepin.com.qq.im

electronic-wechat

transmission

abittorrent

文件管理文件sudo pacman -S range

steam

sudo pacman -S polybar
