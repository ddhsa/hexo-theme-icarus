title: Linux学习记录（一）：Linux 中各个文件夹的作用
author: ddhsa
cover: https://ddhsa126.stdcdn.com/blog/Linux-Wallpaper-15.jpg
thumbnail: https://ddhsa126.stdcdn.com/blog/Linux-Wallpaper-15.jpg
toc: true
tags:
  - linux
  - 文件
categories:
  - linux学习
date: 2019-05-07 18:24:00
---
Linux 中各个文件夹的作用，包含了/、/boot、/sbin、/bin、/lib、/dev、/home、/root、/etc、/usr、/proc、/opt、/mnt、/media、/var、/tmp、/lost+found等各种路径，可以了解各个文件夹内存放的文件的作用。

<!-- more -->


**/  根目录**

　　包含了几乎所的文件目录。相当于中央系统。进入的最简单方法是：cd /。

**/boot  引导程序，内核等存放的目录**

这个目录，包括了在引导过程中所必需的文件。在最开始的启动阶段，通过引导程序将内核加载到内存，完成内核的启动（这个时候，[虚拟文件系统](https://www.baidu.com/s?wd=%E8%99%9A%E6%8B%9F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)还不存在，加载的内核虽然是从硬盘读取的，但是没经过Linux的[虚拟文件系统](https://www.baidu.com/s?wd=%E8%99%9A%E6%8B%9F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)，这是比较底层的东西来实现的。然后内核自己创建好[虚拟文件系统](https://www.baidu.com/s?wd=%E8%99%9A%E6%8B%9F%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)，并且从虚拟文件系统的其他子目录中（例如/sbin 和 /etc加载需要在开机启动的其他程序或者服务或者特定的动作（部分可以由用户自己在相应的目录中修改相应的文件来配制。如果我们的机器中包含多个操作系统，那么可以通过修改这个目录中的某个配置文件（例如grub.conf来调整启动的默认操作系统，系统启动的择菜单，以及启动延迟等参数。  

**/sbin  [超级用户](https://www.baidu.com/s?wd=%E8%B6%85%E7%BA%A7%E7%94%A8%E6%88%B7&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)可以使用的命令的存放目录**

存放大多涉及[系统管理](https://www.baidu.com/s?wd=%E7%B3%BB%E7%BB%9F%E7%AE%A1%E7%90%86&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)的命令（例如引导系统的init程序，是超级权限用户root的可执行命令存放地，普通用户无权限执行这个目录下的命令（但是有时普通用户也可能会用到。）我们要记住，凡是目录sbin中包含的都是[root权限](https://www.baidu.com/s?wd=root%E6%9D%83%E9%99%90&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Yvn1-WuymsPHw-m1DdP1ck0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EP1f4P1RLPWc)才能执行的。

**/bin  普通用户可以使用的命令的存放目录**  
系统所需要的那些命令位于此目录，比如ls、cp、mkdir等命令；类似的目录还/usr/bin，/usr/local/bin等等。这个目录中的文件都是可执行的、普通用户都可以使用的命令。作为基础系统所需要的最基础的命令就是放在这里。


**/lib  根目录下的所程序的共享库目录**  
此目录下包含系统引导和在根用户执行命令时候所必需用到的共享库。做个不太好但是比较形象的比喻，点类似于Windows上面的system32目录。理说，这里存放的文件应该是/bin目录下程序所需要的库文件的存放地，也不排除一些例外的情况。类似的目录还/usr/lib，/usr/local/lib等等。

**/dev 设备文件目录**  
在Linux中设备都是以文件形式出现，这里的设备可以是硬盘，键盘，鼠标，网卡，终端，等设备，通过访问这些文件可以访问到相应的设备。设备文件可以使用mknod命令来创建；而为了将对这些设备文件的访问转化为对设备的访问，需要向相应的设备提供设备驱动模块（一般将设备驱动编译之后，生成的结果是一个*.ko类型的二进制文件，在内核启动之后，再通过insmod等命令加载相应的设备驱动之后，我们就可以通过设备文件来访问设备了。一般来说，想要Linux系统支持某个设备，需要 相应的硬件设备，支持硬件的驱动模块，以及相应的设备文件。

**/home  普通用户的家目录**  
在Linux机器上，用户主目录通常直接或间接地置在此目录下。其结构通常由本地机的管理员来决定。通常而言，系统的每个用户都自己的家目录，目录以用户名作为名字存放在/home下面（例如quietheart用户，其家目录的名字为/home/quietheart。该目录中保存了绝大多数的用户文件(用户自己的配置文件，定制文件，文档，数据等)，  

**/root  用户root的$HOME目录**  
系统管理员(就是root用户或超级用户)的主目录比较特殊，不存放在/home中，而是直接放在/root目录下了。

**/etc 全局的配置文件存放目录。**  
系统和程序一般都可以通过修改相应的配置文件，来进行配置。例如，要配置系统开机的时候启动那些程序，配置某个程序启动的时候显示什么样的风格等等。通常这些配置文件都集中存放在/etc目录中，所以想要配置什么东西的话，可以在/etc下面寻找我们可能需要修改的文件。

**1\. /etc/rc或/etc/rc.d或/etc/rc?.d**  
启动、或改变运行级时运行的脚本或脚本的目录。  
**2\. /etc/passwd**  
用户数据库，其中的域给出了用户名、真实姓名、用户起始目录、加密口令和用户的其  
他信息。  
**3\. /etc/fdprm**  
软盘参数表，用以说明不同的软盘格式。可用setfdprm 进行设置。更多的信息见setfdprm  
的帮助页。  
**4\. /etc/fstab**  
指定启动时需要自动安装的文件系统列表。也包括用swapon -a启用的s w a p区的信息。  
**5\. /etc/group**  
类似/etc/passwd ，但说明的不是用户信息而是组的信息。包括组的各种数据。  
**6\. /etc/inittab**  
init 的配置文件。  
**7\. /etc/issue**  
包括用户在登录提示符前的输出信息。通常包括系统的一段短说明或欢迎信息。具体内  
容由系统管理员确定。  
**8\. /etc/magic**  
“file”的配置文件。包含不同文件格式的说明，“file”基于它猜测文件类型。  
**9\. /etc/motd**  
motd是message of the day的缩写，用户成功登录后自动输出。内容由系统管理员确定。  
常用于通告信息，如计划关机时间的警告等。  
**10\. /etc/mtab**  
当前安装的文件系统列表。由脚本(scritp)初始化，并由mount 命令自动更新。当需要一  
个当前安装的文件系统的列表时使用(例如df 命令)。  
**11\. /etc/shadow**  
在安装了影子(shadow)口令软件的系统上的影子口令文件。影子口令文件将/etc/passwd  
文件中的加密口令移动到/etc/shadow中，而后者只对超级用户(root)可读。这使破译口令更困  
难，以此增加系统的安全性。  
**12\. /etc/login.defs**  
login命令的配置文件。  
**13\. /etc/printcap**  
类似/etc/termcap ，但针对打印机。语法不同。  
**14\. /etc/profile/etc/csh.login、/etc/csh.cshrc**  
登录或启动时bourne或c shells执行的文件。这允许系统管理员为所有用户建立全局缺省环境。  
**15\. /etc/securetty**  
确认安全终端，即哪个终端允许超级用户(root)登录。一般只列出虚拟控制台，这样就不  
可能(至少很困难)通过调制解调器(modem)或网络闯入系统并得到超级用户特权。  
**16\. /etc/shells**  
列出可以使用的shell。chsh 命令允许用户在本文件指定范围内改变登录的shell。提供一  
台机器f t p服务的服务进程ftpd 检查用户s h e l l是否列在/etc/shells 文件中，如果不是，将不允  
许该用户登录。  
**17\. /etc/termcap**  
终端性能数据库。说明不同的终端用什么“转义序列”控制。写程序时不直接输出转义  
序列(这样只能工作于特定品牌的终端)，而是从/etc/termcap 中查找要做的工作的正确序列。  
这样，多数的程序可以在多数终端上运行。


**/usr  这个目录中包含了命令库文件和在通常操作中不会修改的文件。**  
这个目录对于系统来说也是一个非常重要的目录，其地位类似Windows上面的”Program Files”目录（安装程序的时候，默认就是安装在此文件内部某个子文件夹内。输入命令后系统默认执行/usr/bin下的程序（当然，前提是这个目录的路径已经被添加到了系统的环境变量中。此目录通常也会挂载一个独立的磁盘分区，它应保存共享只读类文件，这样它可以被运行Linux的不同主机挂载。

**/usr/lib**  
目标库文件，包括动态连接库加上一些通常不是直接调用的可执行文件的存放位置。  
这个目录功能类似/lib目录，理说，这里存放的文件应该是/bin目录下程序所需要的库文件的存放地，也不排除一些例外的情况。

**/usr/bin**  
一般使用者使用并且不是系统自检等所必需可执行文件的目录。  
此目录相当于根文件系统下的对应目录（/bin，非启动系统，非修复系统以及非本地安装的程序一般都放在此目录下。

**/usr/sbin**  
管理员使用的非系统必须的可执行文件存放目录。  
此目录相当于根文件系统下的对应目录（/sbin，保存系统管理程序的二进制文件，并且这些文件不是系统启动或文件系统挂载 /usr 目录或修复系统所必需的。

**/usr/share**  
存放共享文件的目录。  
在此目录下不同的子目录中保存了同一个操作系统在不同构架下工作时特定应用程序的共享数据(例如程序文档信息)。使用者可以找到通常放在 /usr/doc 或 /usr/lib 或 /usr/man 目录下的这些类似数据。

**/usr/include**  
C程序语言编译使用的头文件。  
linux下开发和编译应用程序所需要的头文件一般都存放在这里，通过头文件来使用某些库函数。默认来说这个路径被添加到了环境变量中，这样编译开发程序的时候编译器会自动搜索这个路径，从中找到你的程序中可能包含的头文件。

**/usr/local**  
安装本地程序的一般默认路径。  
当我们下载一个程序源代码，编译并且安装的时候，如果不特别指定安装的程序路径，那么默认会将程序相关的文件安装到这个目录的对应目录下。也就是说，这个目录存放的内容，一般都是我们后来自己安装的软件的默认路径，如果择了这个默认路径作为软件的安装路径，被安装的软件的所文件都限制在这个目录中，其中的子目录就相应于根目录的子目录。

**/proc  特殊文件目录**  
这个目录采用一种特殊的文件系统格式（proc格式，内核支持这种格式。其中包含了全部虚拟文件。它们并不保存在磁盘中，也不占据磁盘空间(尽管命令ls -c会显示它们的大小)。当您查看它们时，您实际上看到的是内存里的信息，这些文件助于我们了解系统内部信息。例如：


1/ 关于进程1的信息目录。每个进程在/proc 下一个名为其进程号的目录。  
cpuinfo 处理器信息，如类型、制造商、型号和性能。  
devices 当前运行的核心配置的设备驱动的列表。  
dma 显示当前使用的DMA通道。  
filesystems 核心配置的文件系统。  
interrupts 显示使用的中断，and how many of each there have been.  
ioports 当前使用的I/O端口。  
kcore 系统物理内存映象。与物理内存大小一样，但实际不占这么多内存；  
kmsg 核心输出的消息。也被送到syslog 。  
ksyms 核心符号表。  
loadavg 系统”平均负载”；3个没意义的指示器指出系统当前的工作量。  
meminfo 存储器使用信息，包括物理内存和swap。  
modules 当前加载了哪些核心模块。  
net 网络协议状态信息。  
self 到查看/proc 的程序的进程目录的符号连接。  
stat 系统的不同状态  
uptime 系统启动的时间长度。  
version 核心版本。


**/opt  可择的文件目录**  
这个目录表示的是可择的意思，些自定义软件包或者第方工具，就可以安装在这里。

**/mnt  临时挂载目录**  
这个目录一般是用于存放挂载储存设备的挂载目录的，比如磁盘，光驱，网络文件系统等，当我们需要挂载某个磁盘设备的时候，可以把磁盘设备挂载到这个目录上去，这样我们可以直接通过访问这个目录来访问那个磁盘了。一般来说，我们最好在/mnt目录下面多建立几个子目录，挂载的时候挂载到这些子目录上面，因为通常我们可能不仅仅是挂载一个设备吧?

**/media  挂载的媒体设备目录**  
挂载的媒体设备目录，一般外部设备挂载到这里，例如cdrom等。比如我们插入一个U盘，我们一般会发现，Linux自动在这个目录下建立一个disk目录，然后把U盘挂载到这个disk目录上，通过访问这个disk来访问U盘。

**/var  内容经常变化的目录**  
此目录下文件的大小可能会改变，如缓冲文件，日志文件，缓存文件，等一般都存放在这里。

**/tmp  临时文件目录**  
该目录存放系统中的一些临时文件，文件可能会被系统自动清空。

**/lost+found   恢复文件存放的位置**  
当系统崩溃的时候，在系统修复过程中需要恢复的文件，可能就会在这里被找到了，这个目录一般为空。

**另外，有些目录容易混淆，这里简单区分一下：**  
/bin,/sbin与/usr/bin,/usr/sbin:  
/bin一般存放对于用户和系统来说“必须”的程序（二进制文件）。  
/sbin一般存放用于系统管理的“必需”的程序（二进制文件），一般普通用户不会使用，根用户使用。  
/usr/bin一般存放的只是对用户和系统来说“不是必需的”程序（二进制文件）。  
/usr/sbin一般存放用于系统管理的系统管理的不是必需的程序（二进制文件）。

/lib与/usr/lib:  
/lib和/usr/lib的区别类似/bin,/sbin与/usr/bin,/usr/sbin。  
/lib一般存放对于用户和系统来说“必须”的库（二进制文件）。  
/usr/lib一般存放的只是对用户和系统来说“不是必需的”库（二进制文件）。
