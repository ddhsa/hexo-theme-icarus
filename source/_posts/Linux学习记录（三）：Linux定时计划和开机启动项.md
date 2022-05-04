title: Linux学习记录（三）：Linux定时计划和开机启动项
author: ddhsa
tags:
  - linux
  - 定时计划
  - 开机启动
categories:
  - linux学习
date: 2019-05-20 09:34:00
---

# crontab定时计划
>定时计划我们采用`crontab`指令即可，下面给大家讲解下用法

*crontab [-u username] [-l|-e|-r]*

参数：

* `-u`: 只有root才能进行这个任务，也即帮其他用户新建/删除crontab工作调度;

* `-e`: 编辑crontab 的工作内容;

* `-l`: 查阅crontab的工作内容;

* `-r`: 删除所有的crontab的工作内容，若仅要删除一项，请用-e去编辑。

范例一：用`dmtsai`的身份在每天的`12：00`发信给自己
```
crontab -e
```
建立任务
```
0 12 * * * mail dmtsai -s "at 12:00" < /home/dmtsai/.bashrc
```

代表意义|分钟|小时|日期|月份|周|命令
-|-|-|-|-|-|-
数字范围|0~59|0~23|1~31|1~12|0~7|就命令啊

周的数字为0或7时，都代表“星期天”的意思。另外，还有一些辅助的字符，大概有下面这些：

特殊字符|代表意义
-|-
`*(星号)`|代表任何时刻都接受的意思。举例来说，范例一内那个日、月、周都是`*`，就代表着不论何月、何日的礼拜几的12：00都执行后续命令的意思。
`,(逗号)`|代表分隔时段的意思。举例来说，如果要执行的工作是3：00与6：00时，就会是：`0 3,6 * * * command`时间还是有五列，不过第二列是 3,6 ，代表3与6都适用
`-(减号)`|代表一段时间范围内，举例来说，8点到12点之间的每小时的20分都进行一项工作：`20 8-12 * * * command`仔细看到第二列变成`8-12`代表8,9,10,11,12 都适用的意思
`/n(斜线)`|那个n代表数字，即是每隔n单位间隔的意思，例如每五分钟进行一次，则：`*/5 * * * * command`用`*`与`/5`来搭配，也可以写成0-59/5，意思相同为当前用户创建cron服务

## 1.键入 crontab  -e 编辑crontab服务文件

例如文件内容如下：
```
*/2 * * * * /bin/sh /home/admin/jiaoben/buy/deleteFile.sh
```
保存文件并并退出
```
 */2 * * * * /bin/sh /home/admin/jiaoben/buy/deleteFile.sh
 ```
 `*/2 * * * * `通过这段字段可以设定什么时候执行脚本
`/bin/sh /home/admin/jiaoben/buy/deleteFile.sh` 这一字段可以设定你要执行的脚本，这里要注意一下`bin/sh` 是指运行  脚本的命令  后面一段时指脚本存放的路径

## 2.查看该用户下的crontab服务是否创建成功
 用 `crontab  -l` 命令  

## 3.启动crontab服务 
一般启动服务用  `/sbin/service crond start` 若是根用户的`cron`服务可以用 `sudo service crond start`， 这里还是要注意下不同版本**linux**系统启动的服务的命令也不同 ，像我的虚拟机里只需用 `sudo service cron restart` 即可，若是在根用下直接键入`service cron start`就能启动服务

## 4.查看服务是否已经运行
用 `ps -ax | grep cron` 

## 5.开启/关闭定时任务

fileclear.sh

```
tamcdir=${HOME}/ora/user_projects/domains/tamc
cd ${tamcdir}
echo rm -f `ls heapdump*.phd`
rm -f heapdump*.phd
echo rm -f `ls javacore*.txt`
rm -f javacore*.txt
echo rm -f `ls Snap*.trc`
rm -f Snap*.trc
cd bin
echo cp /dev/null nuhup.out
cp /dev/null nuhup.out
cd ${tamcdir}/pxbak
echo rm -rf `ls 20*`
rm -rf 20*
cd ${tamcdir}/webapps/tamcx/fileLoad
echo rm -f `find /weblogic/ora/user_projects/domains/tamc/webapps/tamcx/fileLoad/ -mtime +1`
find /weblogic/ora/user_projects/domains/tamc/webapps/tamcx/fileLoad/ -mtime +1 -exec rm -f {} \;
```

task.crontab

```
#web服务端日志、临时文件清理
10 1 * * * ksh $HOME/tools/clearweblogic.sh >>/weblogic/ora/user_projects/domains/tamc/webapps/tamcx/log/crontab.log 2>>/weblogic/ora/user_projects/domains/tamc/webapps/tamcx/log/crontab.log
```

`task.null.crontab`是一个没有内容的空文件

开启定时任务 
```
crontab /weblogic/tools/task.crontab
```
停止定时任务
```
crontab /weblogic/tools/task.null.crontab
```
