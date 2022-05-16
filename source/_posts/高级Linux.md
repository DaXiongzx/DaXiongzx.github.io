---
title: 高级Linux
description: Nju高级Linux期末复习大全
---

# 高级linux

# 第一章 发行版、组成、内核版本

---

## Linux概念

Linux是一个免费的多用户、多任务的操作系统，其运行方式、功能和Unix系统很相似，但Linux系统的稳定性、安全性与网络功能是许多商业操作系统所无法比拟的。Linux系统最大的特色是源代码完全公开，在符合GNU/GPL（通用公共许可证）的原则下，任何人都可以自由取得、散布甚至修改源代码

## Linux应用领域（简答1-1）

1、linux服务器 2、嵌入式linux系统  3、软件开发平台  3、桌面应用

## Linux系统特点（简答1-2）

1．开放性 2．多用户 3．多任务 4．良好的用户界面 5．设备独立性 6．丰富的网络功能 7．可靠的系统安全 8．良好的可移植性

## Linux系统组成（简答1-3）

1．内核 2、shell  3、文件系统（xfs、ext4) 4、应用程序（软件）

### 内核

内核是操作系统的核心，具有很多最基本的功能，如虚拟内存、多任务、共享库、需求加载、可执行程序和TCP/IP网络功能。

内核是一个用来和硬件打交道并为用户程序提供有限服务集的支撑软件，是操作系统中最核心的功能框架部分。

### Shell

Shell是系统的用户界面,是一个命令解释器,具有普通编程语言的很多特点.

### 文件系统

文件系统是文件存放在磁盘等存储设备上的组织方法

### 应用程序

程序集，包括：文本编辑器、编程语言、X Window、办公软件

## 版本：发行版本+内核版本

### 内核版本：是Linux内核在历次修改或增加相应的功能后的版本编号。

内核版本号是由点分隔的3段数字组成：r.x.y ，比如3.10.0-327。
r：目前发布的内核主版本。 x：偶数表示稳定版本；奇数表示开发版本。 y：错误修补的次数。

### 发行版本：组织和公司，将Linux系统的内核、应用软件和文档包装起来，提供一些系统安装界面，就构成了Linux发行版本。（简答1-4）

发行版本和内核版本相对独立，各个发行版本在内核层是兼容的。

发行版本：（1）Red Hat （2）CentOS （3）Ubuntu （4）Debian （5）Fedora （6）kali

## 1.4Red Hat Linux系统概述

### Red Hat系统优点：

1．支持和硬件平台多 2．优秀的安装界面 3．独特的RPM升级方式 4．丰富的软件包 5．安全性能好
6．方便的系统管理界面 7．详细而完整的在线文档

### redhat7 新特性：多了些软件支持（python2.7 java7),引入了docker(1-7)

# 第二章 安装分区方案

首先考虑硬件兼容性

### 安装linux硬件要求：CPU  内存（1G以上）  硬盘（10G以上）  显卡  显示器  光驱（简答题2-1）

## 交换分区：用作虚拟内存的磁盘空间被称为交换分区（swap分区)

物理内存是有限的，这样就使用到了虚拟内存。它是利用磁盘空间虚拟出的一块逻辑内存

Linux的内存管理采取的是分页存取机制（最近最常使用机制），内核会在适当的时候将物理内存中不经常使用的数据块自动交换到虚拟内存中，而将经常使用的信息保存在物理内存。

## 分区命名方案（简答题2-3）

文件名的格式为/dev/xxyN（比如/dev/sda1分区）。

/dev：这是Linux系统中所有设备文件所在的目录名。因为    分区位于硬盘上，而硬盘是设备。

xx：表示分区所在设备的类型，通常是hd（IDE硬盘）或sd（SCSI硬盘）。

y：这个字母表示分区所在的设备。/dev/hda（第1个IDE 硬盘）或/dev/sdb（第2个SCSI硬盘）；

N：最后的数字N代表分区。前4个分区（主分区或扩展分区）用数字1～4表示，逻辑驱动器从5开始。例如，/dev/hda3是第1个IDE 硬盘上的第3个主分区或扩展分区；/dev/sdb6是第2个SCSI硬盘上的第2个逻辑驱动器。

## 磁盘分区和挂在目录

Linux系统中的每一个分区都是构成支持一组文件和目录所必需的存储区的一部分。挂载是将分区关联到某一目录的过程，挂载分区使起始于这个指定目录（称为挂载目录）的存储区能够被使用。

分区/dev/sda5被挂载在目录/usr上，这意味着所有在/usr下的文件和目录在物理上位于/dev/sda5。因此文件/usr/bin/cal被保存在分区/dev/sda5上，而文件/etc/passwd却不是。

/usr目录下的目录还有可能是其它分区的挂载目录。例如，某个分区（如/dev/sda7）可以被挂载到/usr/local目录下，这意味着文件/usr/local/man/whatis将位于分区/dev/sda7上，而不是分区/dev/sda5上。

### 分区规则：（简答2-2）

swap分区则无需挂载点。

（1）最简单的分区规划  （swap /boot  /)
•swap分区：即交换分区，实现虚拟内存，建议大小是物理内存的1～2倍；
•/boot分区：用来存放与Linux系统启动有关的程序，比如引导装载程序等，最少200MB；
•/分区：建议大小至少在10GB以上。

（2）合理的分区规划(swap boot / /var /home /usr)
•swap分区：实现虚拟内存，建议大小是物理内存的1～2倍；
•/boot分区：建议大小最少为200MB；
•/usr分区：用来存放Linux系统中的应用程序，其相关数据较多，建议大小最少为8GB；
•/var分区：用来存放Linux系统中经常变化的数据以及日志文件，建议大小最少为1GB；
•/分区：Linux系统的根目录，所有的目录都挂在这个目录下面，建议大小最少为1GB；
•/home分区：存放普通用户的数据，是普通用户的宿主目录，建议大小为剩下的空间。

在RHEL 7系统中默认使用FirewallD防火墙

默认情况下，FirewallD防火墙的连接区域为public(2-5)

# 第三章 Linux字符界面   字符界面的终端窗口切换、启动级别、终端的名称pds-0 pds-1、关机重启、man、shell（通配符）、TAB、管道、重定向、vi模式（移动命令再看下）

进入linux系统字符界面方式：1、通过字符界面。2、图形界面下的终端。3、虚拟控制台（简答题3-1）

系统启动默认进入的是图形化界面 

command: systemctl get-default 获取启动方式  

graphical.target表示图形化界面 |     systemctl set-default multi-user.target设置为字符界面

root登录后提示符是“#"   而其他用户登录后提示符是“$”

虚拟控制台：使得linux可以同时多用户登录

### 关闭和重启Linux系统：shutdown （-h -r)、halt、reboot（简答题3-2）

shutdown -h now  ：立即关闭计算机系统。 

shutdown -h +45  ： 定时45分钟后关闭计算机系统。

shutdown -r now "system will be reboot now  ：立即重新启动计算机系统，并发出警告信息。

shutdown -r 01:38  ：定时在1点38分重新启动计算机系统。

halt命令就是调用 shutdown –h

halt：使用halt命令关闭系统。

### 目标（简答题3-3）.target

使用目标替换运行级别（multi-user.target  graphical.target),每个目标都有名字和独特的功能。

### Linux下获取帮助（3-4）

man ls             ls —help

### Shell

Shell接收用户命令，然后调用相应的应用程序，同时它还是一种程序设计语言

目前流行的Shell有sh、csh 、ksh、tcsh和bash等,默认类型为bash.

普通用户zhangsan,他的工作目录是/home/zhangsan

### 通配符

? 代表任何单一字符    *代表任何字符

### 管道

ls /etc|more    命令more是分页显示内容

rpm -qa|grep a|more  命令rpm -qa显示已经安装在系统上的RPM包，命令grep a是过滤软件包，命令more是分页显示这些信息

## Linux重定向有哪些（3-5）

输出重定向、输入重定向、错误重定向、同时实现错误和输出重定向

### 输出重定向

输出重定向，即将某一命令执行的输出保存到文件中，如果已经存在相同的文件，那么覆盖源文件中的内容。

ls/boot > /root/abc 使用输出重定向将/boot目录的内容保存到/root/abc文件中

echo Hello > /root/mm  使用echo命令和输出重定向创建/root/mm文件，文件内容是hello

cat /root/mm   显示文件/root/mm

### 输出追加重定向

将某一命令执行的输出添加到已经存在的文件中。

echo Hello > /root/ao    echo Linux >> /root/ao

cat /root/ao   

Hello
Linux

### 输入重定向

即将某一文件的内容作为命令的输入。

cat < /root/mm    将文件/root/mm的内容作为输入让cat命令执行

### 输入追加重定向

这种输入重定向告诉Shell，当前标准输入来自命令行的一对分隔符之间的内容

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled.png)

### 错误重定向（错误追加重定向与输出追加重定向类似）

即将某一命令执行的出错信息输出到指定文件中。 命令语法：[命令] 2> [文件]

cat /root/kk 2> /root/b      /root/kk文件不存在。  出现报错信息，将其保存到文件/root/b中

### 同时实现输出和错误重定向

[命令] &> [文件]

ls /boot &> /root/kk    

## Vi编辑器

vi编辑器是Linux系统字符界面下最常使用的文本编辑器，用于编辑任何ASCII文本。

vi编辑器有3种基本工作模式，分别是命令模式、插入模式和末行模式。（简答3-6）进入vi编辑器之后，系统默认处于命令模式。在命令模式下，按冒号键“:”可以进入末行模式。按字母键“a”（光标当前位置后插入，i是光标位置前插入）就可以进入插入模式。只有在插入模式下，才可以进行文本编辑。在插入模式下按“Esc”键可回到命令模式。

# 第四章  （rm、wc、软硬连接）

Linux 系统与 Windows 系统有很大的不同，它以目录的形式挂载文件系统，其目录结构是一个分层的树形结构。linux分硬链接和软链接。

## Linux文件类型

在 Linux 系统中除了一般文件之外，所有的目录和设备都是以文件的形式存在的。

常见文件类型：普通文件、目录文件、设备文件、管道文件和符号链接文件（简答4-1）

普通文件：ls -lh可以查看某个文件的属性 ”-rw - - - - - - -"  第一个“-”表示该文件是普通文件

目录文件：ls -lh可以查看某个文件的属性 ”drwxr - xr - x "  第一个“d”表示该文件是目录文件

设备文件：存在于/dev目录中，分为块设备文件和字符设备文件

块设备文件：主要特点是可以随机读写，最常见的是磁盘，如/dev/hda1 、/dev/sda1  ls -l ”brwxr - xr - x "  第一个“b”表示该文件是块设备文件

字符设备文件：最常见的是打印机和终端，如/dev/null,  ls -l ”crwxr - xr - x "  第一个“c”表示该文件是字符设备文件

管道文件（FIFO文件）：ls -l  ”prwxr - xr - x "  第一个“p”表示该文件是管道文件

链接文件 ：两者区别（4-2）  

软链接：软链接文件又叫符号链接文件，这个文件包含了另一个文件的路径名。 ls -l ”lrwxr - xr - x "  第一个“l”表示该文件是软链接文件

硬链接：硬链接是已存在文件的另一个文件，若删除硬链接源文件，硬链接文件依然存在，而且保留了原有内容。ls -l ”lrwxr - xr - x "  第二列文件硬链接数大于1，那么就是硬链接文件。

## Linux文件目录结构 （home:主目录）

Linux系统都有根文件系统，Linux系统的目录结构是分层的树型结构，都是挂载在'/‘下（4-3）

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 1.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 2.png)

## 常见文件和目录操作

cd ~:跳转到用户主目录  cd ~zhangsan:跳转到用户zhangsan的主目录 （/home ==~)

ls -al /root   （文件的链接数）

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 3.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 4.png)

touch可以创建文件，也可以更改文件的时间：touch -c -t 06071930 file1

mkdir创建目录

rmdir：删除空目录

cp:复制文件和目录，也可以将复制后的文件改名     cp [选项 ] [源文件 目录 ] [目标文件 目录 ]

cp /etc/grub2.cfg   /root/grub  将 /etc/grub2.cfg 文件复制到 /root 目录下，并改名为 grub

cp -r /boot   /root   将 /boot 目录中的所有文件及其子目录复制到目录 /root 中。

mv移动文件和目录，也可以更改其名称。   mv [选项 ] 源文件 目录 ] [目标文件 目录 ]

移动： mv-f /root/picture/*.png  /usr/local/share/picture  将 /root/picture 目录下所有的后缀名为 ““.png的文件移到 /usr/local/share/picture 目录下。

改名：mv /root/picture/kdepic/png  /root/picture/life.png   把 /root/picture 目录下的文件 kdepic.png 改名为 life.png

rm:删除文件或目录：rm -rf /root/ab  （4-5）

wc:统计文件行数、单词数、字节数和字符数     wc [选项 ] 文件    wc /root/aa   结果： 3 8 22 /root/aa

内核为每一个新创建的文件分配一个 inode （索引节点）号，文件属性保存在索引节点里，在访问文件时，索引节点被复制到内存里，从而实现文件的快速访问。

ln:创建链接文件（包括软链接和硬链接）   ln [选项 ] [源文件名] [链接文件名]

软链接：也叫符号链接，这个文件包含了另一个文件的路径名。类似于windows的快捷方式。

硬链接：硬链接记录的是目标的inode,软链接记录的是目标的路径。软链接就像是快捷方式，而硬链接就像是备份。 软链接可以跨分区做链接，而硬链接由于inde的缘故，只能在本分区中做链接。（4-2）

硬链接文件的使用：[root@rhel ~]#echo hello > a   [root@rhel ~]#ln a b

软连接文件的使用 [root@rhel ~]#echo hello > a   [root@rhel ~]#ln s a b

# 第五章  tail -f 看日志、查找命令

## 文本内容显示：cat 、more 、less  、head、 tail (5-1)

cat: 把 t  后输入到 textfile2 文件中:cat -n textfile1>textfile2

使用cat命令创建mm.txt: cat>mm.txt<<EOF>Hello>Linux>EOF

more:分页显示文本信息 。按空格显示下一页，按[b]返回显示上一页内容。

 逐页显示信息，如有两行以上的空白行则以一行空白行显示：more -s testfile

从第二十行开始显示：more +20 testfile

一次两行显示：more -2 testfile

less:回卷显示文本文件。Less与more较为相似，less允许使用者往回卷动

回卷显示/etc/services文件的内容： less /etc/services

head:显示指定文件前若干行，默认为10行

head [选项］ 文件   [root@rhel ~]# head -c 100 /etc/passwd 显示前100个字节数据内容

[root@rhel ~]# head -3 /etc/passwd 显示前三行数据

tail:查看文件末尾数据

末尾三行： tail -3 /etc/passwd               末尾100字节：tail -c 100 /etc/passwd

## 文本内容处理 ：sort 、uniq 、cut、 comm 、diff  (5-2)

sort:对文件中的数据进行排序。 正序：sort textfile  逆序：sort -r textfile （5-5）   

uniq:将重复行从输出文件中删除。查看重复的数据：uniq -d file 查看不重复的数据：uniq -u file

cut:从文件每行中显示出选定的字节、字符或字段   cut [选项] 文件  [root@rhel ~]# cut -f 1,5 -d: /etc/passwd

comm:逐行比较两个已排序的文件   comm [选项 ] [文件 1] [ 文件 2] 选项-1含义：不输出文件1持有的行 。-2：不输出文件2持有的行。 -3：不输出两个文件共有的行。  

如果没有指定任何参数，comm 命令读取这两个文件，然后输出三列：第1 列输出 file1 中特有的行；第 2 列输出 file2 中特有的行；第 3 列输出两个文件中共有的行。

comm -12 file1 file2:只显示file1和file2中相同行的数据

diff:逐行比较两个文本文件，列出其不同之处。与comm不同，不需要事先排序好。diff file1 file2

uname -r（显示内核版本）（5-3）

## 文件和命令查找 grep find locate

grep：查找文件中符合条件的字符串

在文件kkk中搜索匹配字符串“test file"  :grep 'text file' kkk 

显示所有以d开头的文件中包含”test"的行数据内容 ：grep 'test' d*

在文件/root/aa中找出以b开头的行内容： grep ^b /root/aa

不是以b开头的行内容：grep -v ^b /root/aa

找出以le结尾的行内容：grep le$ /root/aa

查找sshd进程信息：ps -ef |grep sshd

find:找出文件系统内符合条件的文件

查找/boot目录下的启动菜单配置文件grub.cfg:   find /boot -name grub.cfg

查找/目录下所有以“.conf”为扩展名的文件： find / -name '*.conf'

列出当前目录及其子目录下所有最近 20 天内更改过的文件。 find. -ctime -20

locate:在数据库中查找文件，该数据库每天由cron来建立，比find速度快。

locate httpd.conf       

显示找到几个httpd.conf文件： locate -c httpd.conf

## 系统信息显示（uname、hostname、free、du)

uname:显示计算机及操作系统相关信息   -r（5-3）：内核发行号    -m：硬件架构 -a:全部信息

hostname:显示或修改计算机主机名  显示主机名：hostname  修改主机名：hostname Linux

free查看内存信息 :-m :以mb为单位查看  -t:显示系统物理内存加上交换分区总的容量

du：显示目录或文件的磁盘占用量

显示/root目录磁盘占用量：du -s /root   以mb为单位显示：du -sh /root

## 日期和时间 cal、date、hwclock

cal：显示日历信息

显示本月日历：cal

显示2001年年历：cal 2001

显示2007年9月的月历：cal 9 2007

以星期一为每周的第一天的方式来显示本月的日历：cal -m

以1月一号起，显示今年的年里：cal -jy

date:显示和设置系统日期和时间

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 5.png)

hwclock:查看和设置硬件时钟

查看硬件时间：hwclock

以系统时间更新硬件时间。hwclock -w

以硬件时间更新系统时间。hwclock -s

## 信息交流 echo、mesg、wall、write

echo:

将文本“ Hello Linux ”添加到新文件 notes 中:echo hello linux >notes

显示$HOME变量的值：echo $HOME

mesg: 允许或拒绝写消息

显示当前消息许可设置：mesg

只允许root用户发送消息到自己主机：mesg n

wall:对全部已登录用户发送信息：wall “下班以后请关闭计算机”
write：向用户发送消息    write [用户 ] [终端名称]  write root tty3 hello 

clear:清除计算机屏幕上显示的信息。(5-4)

uptime：显示系统已经运行的时间

# 第六章：shell语法、变量定义、文件目录测试、位置参数（$...）

## Shell程序

### 基本语法：开头部分+注释部分+语句执行部分（6-1shell程序的创建过程）

要使用脚本文件，需要赋予该文件可执行的权限 chmod u+x [文件名]

     开头： #!/bin/bash（放在文件的第一行） #! /bin/bash

#表示注释

在shell中输入多行命令可以得到命令的结果信息

输入shell脚本文件的完整路径就可以执行shell程序  /root/date (6-2)

如果没有将脚本文件设置为可执行文件(chmod u+x file)，则需要 bash /root/date来执行shell文件 (6-2)

## 变量

对 Shell 来讲，所有变量的取值都是一个字符， Shell 程序采用$var 的形式来引用名为 var 的变量的值。

查看一些环境变量的值：echo $HOME  显示用户主目录的完全路径名

### 常见环境变量（6-3）

HOME       用于保存用户主目录的完全路径名
PATH         用于保存用冒号分隔的目录路径名，Shell 将按 PATH 变量中给出的顺序搜索这些目录，找到的第一个与命令名称一致的可执行文件将被执行
TERM        终端的类型
UID          当前用户的UID ，由数字构成PWD当前工作目录的绝对路径名，该变量的取值随cd 命令的使用而变化
PS1    主提示符，在root 用户下，默认的主提示符是 “#”，在普通用户下，默认的主提示符是"$"

PS2  在Shell 接收用户输入命令的过程中，如果用户在输入行的末尾输入然后按回车键，或者当用户按回车键时Shell 判断出用户输入的命令没有结束时，就显示这个辅助提示符，提示用户继续输入命令的其余部分，默认的辅助提示符是“>"

### 用户定义的变量：

      变量名=变量值   在定义变量时，变量名前不应该加符号”$"   变量名尽量用大写字母

AS = 120   echo $AS

设置变量只读： readonly 变量名

export 命令可以将一个局部变量提供给Shell命令使用 export 变量名=变量值

### 位置参数（类似与python format)

位置参数之间用空格分隔， Shell 取第一个位置参数替换程序文件中的 $1 ，第二个替换 $2 ，依次类推。 $0不是位置参数，其内容是当前这个shell程序的文件名。

### 预定义变量

与环境变量类似，也是shell一开始就定义的变量，预定义变量由符号 $和另一个符号组成，如：$#、$*

[https://www.notion.so](https://www.notion.so)

### 参数位置的变量（没怎么看，也不重要，zs没讲）

参数置换功能以便用户根据不同的条件来给变量赋不同的值。

### 变量表达式（test，这里zs也没细讲)

test [表达式] 

字符串比较

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 6.png)

### 字符串比较符号（6-4）

= 比较两个字符串是否相同，相同则为”是“

！= 比较两个字符串是否相同，不同则为”是“

-n  比较字符串的长度是否大于0 ，如果大于 0 则为"是"

-z   比较是否等于0

$?:表示的是上一个命令的执行结果，结果为0表示没有错误。

[root@rhel ~]# echo $?   ：显示上次命令的执行结果

数字比较：

test $int1 -eq $int2         -eq:等于   -ge:大于等于  -le:小于等于  -ne:不等于  -gt:大于  -lt:小于

逻辑测试：（没怎么看  ！  -a(and）  -o (or)) if条件中会用到

文件操作测试：测试文件的文件操作逻辑（也许会考）

test -r file

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 7.png)

## 条件判断语句（这里留意下数比较和字符串比较）

### if 和case的区别 ：if是2选1  而case是多个中选1个。

if then fi 语句和 if then else fi    （if [    ]间内的内容要有空格）

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 8.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 9.png)

case语句：

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 10.png)

循环：

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 11.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 12.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 13.png)

while是在循环条件为真时继续执行循环，而until是在条件为假时继续执行循环。

# 第七章 用户和组群账户管理  /etc/skel目录、 /etc/login.defs文件

root是系统最高管理者  UID=0

与用户和组账户相关的配置文件有 /etc/passwd 、/etc/shadow 、 /etc/group 和 /etc/gshadow 。

### 新建用户的UID默认从1000开始（7-4）

### 设置密码和不设置密码的区别：能否登录到 Linux上（7-5）

## 用户账户

用户通过UID来标识，每个用户拥有的权限不一样。

### 三大类用户：root用户、系统用户、普通用户（7-1）

## 系统用户

即系统自身所拥有的账户，但是无法登录Linux，系统用户的UID为1~999

## 普通用户

这类用户能登录系统，但是权限有一定的限制。 UID:1000~60000

/etc/group   /etc/gshadow

### /etc/group   /etc/gshadow字段含义（7-3）

zhangsan（组群名）:x（组群密码）:1000（GID）:  (组群成员）

### /etc/passwd文件字段含义 /etc/shadow（7-2）

zhangsan（用户名）:x（密码）:1000（uid):1000(gid）:张三 （用户名全称）:/ zhangsan （主目录）:/bin/bash（登录shell）  passwd

/etc/shadow 文件内容包括用户及被加密的密码以及其它

用户以zhangsan登录系统，首先会检查/etc/passwd文件，查看是否有zhansgan用户，之后确定uid，通过uid来确定用户身份，若存在则读取相应的密码。/etc/passwd中密码是加密后的，真实密码被映射到/etc/shadow文件

### 用户账户设置（创建 修改 删除）

useradd zhangsan   passwd zhangsan    useradd -u 1010 zhangsan(uid=1010）

useradd -d /home/www newuser(创建用户newuser 并设置其主目录为/home/www)

useradd -g root pp（创建用户pp，并且指定该用户是属于群组root的成员）

useradd -s /bin/ksh abc（创建用户abc 并且设置该用户的shell类型为 /bin/ksh）

### 修改用户账户（usermod)

可以更改用户的shell类型、所属的组群、用户密码的有效期、更改用户的登录名

usermod -d /home/kkk zhangsan（修改用户zhangsan的主目录为/home/kkk,若不存在该目录就直接创建了)

usermod -l zhaoliu wangwu（将wangwu的登录名修改为zhaoliu）

usermod -c 张三 zhangsan (修改用户zhangsan的用户名全称为张三）

usermod -f 20 zhansgan (在密码过期后20天禁用该用户）

usermod -g root sun (将sun用户的所属群组修改为root,该群组必须事先存在)

usermod -L zhangsan (锁住用户zhangsan密码，使密码无效）

usermod -s /bin/ksh zhangsan (修改用户zhangsan的shell类型为/bin/ksh)

### 删除用户 userdel

userdel lisi （会删除用户，但是用户主目录还在，如果也要删除用户主目录，则要加-r）

## 组群账户

组群有GID   root组群：GID=0

相关文件两个 ：/etc/group 和 /etc/gshadow 。

分为：私有组群和标准组群

私有组群：创建该用户时，没有指定组群，那么就会创建一个与该用户同名的组群，该组群就是私有组群。这个组群只包含这个用户

标准组群：可包含多个用户，在创建用户时，应当指定用户属于哪一个组群。

另外一种方法将组群分为主要组群和次要组群。
1．主要组群：当一个用户账户属于多个组成员时登陆后所属的组群便是主要群组，其它组群是次要群组，一个用户账户只能属于一个主要组群。
2．次要组群：次要群组也称附加群组，一个用户账户可以属于多个次要群组。

### /etc/group文件

一个用户可以归属一个或多个不同的组群，同一组群的用户之间具有相似的特征。比如把某一用户加入到 root 组群，那么这个用户就可以浏览 root 用户主目录的文件，如果 root 用户把某个文件的写执行权限开放， root 组群的所有用户都可以修改此文件；如果是可执行的文件， root 组群的用户也是可以执行的。

### groupadd

groupadd -g 1800 ou（创建组群并且设置gid）

groupadd -r chinese (创建的是系统组群）

### groupmod

groupmod -g 1900 ou（修改组群ou的gid)

groupmod -n shanghai ou （修改组群ou的新组群名称为shanghai)

### groupdel

删除组群账户前需要先删掉组群里的用户

### passwd

passwd it(设置用户it的密码） passwd -l it （锁住用户it的密码）passwd -u it（解锁）

passwd -d it（删除用户it的密码）

### gpasswd

设置一个组群的组群密码，或者是在组群中添加、删除用户。

gpasswd -a it kk（将it用户加到kk组中）

gpasswd -d it kk (删除kk中的it）

gpasswd kk（设置kk密码） gpasswd -r kk(取消kk组群密码）

### su 切换到其他用户账号进行登录

su默认切换到root

su - it 切换为it进行登录，并且连shell环境也切换

su it:shell环境不切换

### newgrp

newgrp 命令是以相同的账户名，不同的组群身份登录系统。若使用该命令，那么用户必须是该组群的用户 ，否则无法使用。

newgrp ou (以组群ou身份登录系统）

### groups

显示指定用户账户的组群成员身份

groups ab (查看用户ab是属于哪些组群的成员）

### id

使用 id 命令可以显示用户的 UID 以及该用户所属组群的 GID

id [选项 ] 用户名

# 第八章 磁盘分区和文件系统管理 （磁盘管理（从新建硬盘到挂载成功）、权限设定）

先分区，再格式化，最后建立文件系统，那么这个分区才能使用，才能在某个磁盘上存储数据

文件系统是指文件在硬盘上的存储方式和排列顺序。主流文件系统：NFS、ext2、ext3、ext4、XFS、JFS

在 Linux 系统中，如果需要在某个磁盘上存储数据，则需要将磁盘进行分区，然后创建文件系统，最后将文件系统挂载到目录下才可以。

在安装 Linux 系统后需要添加更多的交换空间，可以通过添加一个交换分区或添加一个交换文件来实现。

## 磁盘分区和格式化简介

### 磁盘分区的含义（8-1）

磁盘分区是指对硬盘物理介质的逻辑划分。从而有利于对文件的管理，不同分区可以建立不同的文件系统，从而可以在不同分区上安装不同的操作系统。（8-1）

linux需要的分区较多 ，比如/分区   swap分区

分区有三种：主分区、扩展分区、逻辑驱动器。（8-1）扩展分区是逻辑驱动器的容器。只有主分区和逻辑驱动器才能进行数据存储。

### 格式化的含义（8-2）

格式化是指对磁盘分区进行初始化的一种操作，这种操作通常会导致现有的分区中所有的数据被清除。格式化会在磁盘中建立磁道和扇区。建好之后，计算机才可以使用磁盘来存储数据。

在分区后必须进行格式化才可以。

### fdisk进行磁盘分区（8-3）

fdisk [选项 ] [设备 ]

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 14.png)

常用分区类型 （不一定重要）

 id      分区类型    描述

83       linux     普通分区

fd     linux raid 自动   raid使用的分区

8e   linux lvm   LVM使用的分区

82   linux swap 

### 创建文件系统

mkfs [选项 ] [设备] 

### 主流文件系统：XFS  ext2  ext3 ext4 JFS  NFS

fdisk -l /dev/sda（查看当前磁盘上的分区情况）

ls /dev/sda*      partprobe(若要用mkfs创建文件系统，则需实现重启系统，为了避免重启系统使用partprobe)

mkfs -t ext4 /dev/sda5  (格式化/dev/sda5分区，创建ext4文件系统）这条命令也可以将分区格式化成其它文件系统。

### 挂载和卸载文件系统

如果要挂载一个分区，首先需要确认文件系统的类型，然后才能挂载使用，通过使

使用mount和umount可以实现文件系统的挂载和卸载

### mount:将指定分区、光盘挂载到Linux系统的目录下

mount [选项 ] [设备 ] 挂载目录 ]

mkdir /mnt/kk                  mount /dev/sda5  /mnt/kk(挂载分区/dev/sda5到/mnt/kk目录中）

mount -o ro /dev/sda5   /mnt/kk   （以只读的方式挂载）

### 卸载文件系统

umount   /dev/sda5 （卸载分区/dev/sda5文件系统）   df(查看到分区/dev/sda5已经卸载）

### 查看磁盘分区挂载情况（df)

df 命令可以显示每个文件所在的文件系统的信息,检查文件系统的磁盘空间使用情况。

### 开机自动挂载(没怎么看命令）（8-6）

只有将某个分区或是设备挂载以后才能使用，但是当计算机重新启动以后，又需要重新挂载，这个时候可以通过修改/etc/fstab 文件实现开机自动挂载文件系统。

/etc/fstab 文件包含了所有磁盘分区以及存储设备的信息。

编辑 etc/fstab 文件，在该文件末尾添加下列内容。
/dev/sda5  /mnt/www xfs defaults 1 2

## 使用交换空间

Linux 系统中的交换空间在物理内存被用完时使用。

如果系统需要更多的内存资源，而物理内存已经用完，内存中不活跃的页就会被转移到交换空间中。虽然交换空间可以为带有少量内存的计算机提供帮助，但是这种方法不应该被当做是对内存

用户有时需要在安装 Linux 系统后添加更多的交换空间，可以通过添加一个交换分区（推荐优先使
用）或添加一个交换文件来实现。

已经使用fdisk命令创建了/dev/sda5分区

fdisk -l /dev/sda（查看/dev/sda5分区信息）

mkswap /dev/sda5（将分区/dev/sda5创建为交换分区）

swapon /dev/sda5 （启用交换分区）

cat /proc/swaps（查看交换分区是否已启用）

spawoff /dev/sda5   free （禁用交换分区）

## 交换文件

mkswap /swapfile  (创建交换文件）   swapon /swapfile(启用交换文件）swapoff /swapfile    free (删除交换文件）

# 第九章 （rpm、yum、tar（gzip、bzip）、tar zxvf xxx.tar.gz -C /home/lutianxiao解压至指定目录、进程（kill top ps）、cron、at、系统启动过程顺序、）

在 Linux 系统中，最常用的软件包是 RPM 包和tar 包。要管理 RPM 软件包可以使用 rpm 和 yum命令， yum 命令自动化地收集 RPM 软件包的相关信息，检查依赖性，并且一次安装所有依赖的软件包，无需繁琐地一次次安装。

### rpm软件包管理的用途（9-1）

可以安装、删除、升级、刷新和管理 RPM 软件包；（CRUD）

可以查询系统中的 RPM 软件包是否安装并查询其安装的版本；（版本检查）

依赖性的检查，查看是否有 RPM 软件包由于不兼容而扰乱系统。（兼容性）

可以自己开发程序打包为RPM软件包并发布（发布）

## 安装RPM软件包（基本操作模式之一）

rpm -ivh [RPM 软件包文件名称]

若该软件包已经存在 则 rpm -ivh —replace [RPM 软件包文件名称]

## 删除rpm软件包（基本操作模式之一）

rpm -e [RPM 包名称]     rpm-e bind-chroot

## 升级rpm软件包 升级 = 删除+安装 （9-2）（基本操作模式之一）

不管该软件包的早期版本是否已被安装，升级选项都会安装该软件包。

rpm -Uvh [RPM 软件包文件名称]

## 刷新软件包（9-2升级与刷新的区别 升级是不管是否安装，都会安装，而刷新是先前没安装，那么就不会安装）

会比较软件包版本，如果有新的，则会更新到新的版本。如果软件包先前没有安装， RPM 的刷新选项将不会安装该软件包，这和 RPM 的升级选项不同。

rpm -Fvh [RPM 软件包文件名称]

## 查询指定安装包是否已经安装

rpm -q [RPM 包名称]

## 查询所有已安装的软件包

rpm -qa

## 查询已安装软件包的详细信息

rpm -qi [rpm软件包名称]

## 查询RPM包所包含的文件列表(剩余的命令没看）

rpm -ql [rpm 包名称]

### 创建软件仓库的步骤（9-3）：1、安装软件包  2、复制软件包  3、创建软件仓库配置文件  4、创建软件仓库

## 使用yum管理rpm软件包

1.yum help 显示使用信息
2.yum list 列出软件包
3.yum search keyword搜索关键字
4.yum info packagename 列出软件包详细信息
5.yum install packagename 安装软件包
6.yum remove packagename 删除软件包
7.yum update packagename 升级软件包

8.yum deplist bind 列出bind软件包的依赖关系

## tar包

利用tar命令可以把一大堆的文件和目录打包成一个文件(打包并不是压缩）

tar cvf abc.tar  /root/abc  备份 /root/abc 目录及其子目录下的全部文件，备份文件名为 abc.tar

tar tvf abc.tar   查看 abc.tar 备份文件的内容，并显示在显示器上。

tar xvf abc.tar  解压包

tar uvf abc.tar /root/abc/d   更新原来tar包abc.tar中的文件/root/abc/d(相当于在包里添加了一个文件）

## tar包特殊用途

使用 tar 命令可以在打包或解包的同时调用其他的压缩程序，比如调用 gzip 、 bzip2 和xz 等。（9-4）

使用 tar 命令可以在归档或者是解包的同时调用 gzip 压缩程序。以“ “.gz ”结尾的文件就是 gzip 压缩的结果。与 gzip 相对应的解压缩程序是 gunzip tar 命令中使用 z 选项来调用 gzip 。（tar.gz文件)

tar zcvf abc.tar.gz  /root/abc   把 /root/abc 目录包括其子目录全部做备份文件，并进行压缩，文件名为 abc.tar.gz 。

tar ztvf abc.tar.gz 查看压缩文件 abc.tar.gz 的内容，并显示在显示器上。

tar zxvf abc.tar.gz 将压缩文件 abc.tar.gz 解压缩出来。

tar 调用 bzip2

### tar 调用bzip2

以.bz2结尾的文件  tar中使用-j选项来调用bzip2 。

tar jcvf abc.tar.bz2  /root/abc   将目录 /root/abc 及该目录所有文件压缩成 abc.tar.bz2 文件。
tar jtvf abc.tar.bz2   查看压缩文件 abc.tar.bz2 的内容，并显示在显示器上。

tar jxvf abc.tar.bz2   将abc.tar.bz2文件解压缩。

### tar调用xz（压缩同上）

以".xz"结尾的文件就是xz压缩的结果，tar 命令中使用 -J 选项来调用。

tar Jcvf abc.tar.xz  /root/abc  将目录 /root/abc 及该目录所有文件压缩成 abc.tar.xz 文件。

tar Jtvf abc.tar.xz   查看压缩文件 abc.tar.xz 的内容，并显示在显示器上。

tar Jxvf abc.tar.xz  解压缩

# 第十章 权限和所有者

## 权限设置（如何设置权限以及更改文件和目录的所有权）

三种用户访问：文件的用户所有者（属主）、文件的组群所有者（用户所在组的同组用户）、系统中的其它用户。

有读取（r)、写入(w)、执行权限(x)  (-)表示不具有该权限

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 15.png)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 16.png)

## 文字设定法设置权限（chmod)

chmod [操作对象 u、g、o、a] [操作符号 +-= ] [权限] [文件] [目录 ]

chmod u+w a   添加所有者对 a 文件的写入权限。

chmod u-r a  取消所有者对a文件的读取权限

chmod g=w a  重新分配同组用户对 a 文件有写入的权限。

chmod u+rw,g+r,o+rwx a   更改 a 文件权限，添加所有者为读取、写入权限，同组用户为读取权限，其他用户读取、写入和执行的权限。

chmod a-rwx a   取消所有用户的读取、写入和执行权限。

## 用数字表示

r:4  w:2  x:1  -:0

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 17.png)

chmod [n1n2n3] [文件 目录]

n1表示用户所有者的权限 n2 表示组群所    有者的权限， n3 表示其它用户的权限。

chmod 700 a  设置 a 文件权限，所有者拥有读取、写入和执行的权限。

chmod 470 a  设置 a 文件权限，所有者拥有读取，同组用户有读取、写入和执行的权限。

chmod 007 a  设置 a 文件权限，其他用户拥有读取、写入和执行的权限。

chmod -R 777 /home/user  设置 /home/user 目录连同他的子文件夹的权限为 777

## 特殊权限

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 18.png)

chmod u+s a 添加 a 文件的特殊权限为 SUID 。

chmod g+s a 添加 a 文件的特殊权限为 SGID

chmod o+t a 添加 a 文件的特殊权限为 Sticky 。

数字法

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 19.png)

[root@rhel ~]# chmod 4000 a   设置文件 a 具有 SUID 权限。

[root@rhel ~]# chmod 2000 a  设置文件 a 具有 SGID 权限。

[root@rhel ~]# chmod 1000 a  设置文件 a 具有 Sticky 权限。
[root@rhel ~]# chmod 7000 a   设置文件 a 具有 SUID SGID 和 Sticky 权限。

### 更改文件和目录所有者

使用 chown 命令可以更改文件和目录的用户所有者和组群所有者。

chown [选项 ] 用户 组群 ] 文件 目录

chown newuser a  将文件 a 的所有者改成 newuser

chown :newuser a  将文件 a 的用户组改成 newuser 。

chown root.root a   将文件 a 的所有者和用户组一起改成 root

chown -R newuser.newuser /root/b   将目录 /root/b 连同它的下级文件 /root/b/ccc 的所有者和用户组一起更改为 newuser 。

# 第十一章 Linux日常管理和维护 （网络配置文件）

Linux 系统上所有运行的内容都可以称为进程。每个用户任务、每个系统管理守护进程都可以称为进程。 

进程与程序之间还是有明显区别的。程序只是一个静态的命令集合，不占系统的运行资源；而进程是一个随时都可能发生变化的、动态的、使用系统运行资源的程序。一个程序可以启动多个进程。和进程相比较，作业是一系列按一定顺

进程特征：动态、并发、异步、独立

### 进程种类：交互式进程（一个由shell启动并控制的进程）、守护进程（在引导系统时启动，以执行及时的操作系统任务）、批处理进程（安排在指定时间完成一系列的进程）（11-1）

## ps命令

ps -e (显示所有进程）

ps -aux（显示所有不带控制台终端的进程，并显示用户名和进程的起始时间）

ps -u （显示用户名和进程的起始时间）

ps -u root (显示用户root的进程）

ps -t tty1（显示tty1终端下的进程）

ps -p 1659(显示进程号为1659的进程）

## top命令

使用 top 命令可以显示当前正在运行的进程以及关于它们的重要信息，包括它们的内存和 CPU 使用量。

top

## kill命令

ps -ef | grep crond(查到crond的进程号是1659）  kill-9 1659

## 任务计划（cron)

要在固定时间上触发某个作业，就需要创建任务计划，按时执行该作业。

使用cron实现该功能。可以修改/etc/crontab文件或者使用crontab命令来实现。

（只有root用户能修改）/etc/crontab文件配置：（也可以通过在/etc/cron.d目录中创建文件来实现，该目录中的所有文件和/etc/crontab文件使用的语法相同）

minute hour day month  dayofweek(星期几） user name commands

30 21  * * * root  /root/backup.sh  （在每天晚上的 21:30 执行 /root/backup.sh 文件）

45 4 1，10，22 * * root  /root/backup.sh    (在每月 1 、 10 、 22 日的 4:45 执行 /root/backup.sh 文件)

0 ,30 18-23 *  * * root  /root/backup.sh    在每天 18:00 23:00 之间每隔 30 分钟执行 /root/backup.sh

### root以外的用户可以使用crontab命令来配置cron任务。

使用 crontab 命令可以创建、修改、查看以及删除 crontab 条目。

crontab [选项]
crontab [选项 ] [文件]

创建新的crontab，然后提交给crond进程，同时，新创建的crontab的一个副本已经被放在/var/spool/cron目录中。

su zhangsan    crontab -e (打开vi编辑器，编辑用户zhangsan的crontab条目）  8 **** cp /home/zhangsan /aa   /home/zhangsan/bb（编辑的条目） 之后用root用户查看/var/spool/cron/zhangsan文件，即可看到添加的内容。若要修改，以root用户vi上述目录即可。

### 列出crontab

crontab -u zhangsan -l  (以root用户列出zhangsan的crontab)

crontab -l (以普通用户zhangsan列出自己的crontab）

crontab -l >/home/zhangsan/zhangsancron（对/var/spool/cron/zhangsan文件做备份）（zhansgan用户执行）

### 删除crontab

crontab -u zhangsan -r （以用户root删除zhangsan的crontab)

crontab -r （以普通用户zhangsan删除自己的crontab)

### 恢复丢失的crontab文件

crontab /home/zhangsan/zhangsancron

## Linux系统启动过程（11-2）(联系自己开机过程）

Linux 系统的启动是从计算机开机通电自检开始直到登录系统需要经过的多个过程。

1BIOS 自检
2启动 GRUB 2
3加载内核
4执行 systemd 进程，该进程是所有进程的起点。
5初始化系统环境
6执行 /bin/login 程序（最后的时候要登录）

### 维护grub2

GRUB 是 Linux 系统默认的引导加载程序。在 Linux 加载一个系统前，它必须由一个引导加载程序中的特定指令去引导系统。

### grub2新功能：图形接口、使用模块机制、支持脚本语言、支持救援模式、国际化语言、灵活的命令行接口、自动解压（11-3）

### 设置GRUB2加密（11-4两种密码格式）

由于 GRUB 2 负责引导 Linux 系统，作为系统中的第一道屏障的安全性非常重要，对GRUB 2 进行加密可以实现安全性。

明文密码：密码数据没有经过加密，安全性差；
PBKDF2 加密密码：密码经过 PBKDF2 哈希算法进行加密，在文件中存储的是加密，安全性更好。

### grub2配置案例

破解root用户密码

更改网卡名称

# 第12章 Linux网络配置（12-1网卡配置文件的内容)

系统网络设备的配置文件保存在 /etc/sysconfig/network-scripts 目录下，其中文件 ifcfg -eno16777736 包含一块网卡的配置信息，文件 ifcfg-lo 包含回路 IP 地址信息。

### /etc/resolv.conf文件

该文件是由域名解析器使用的配置文件

### /etc/hosts文件

当计算机启动时，在可以查询 DNS 以前，计算机需要查询一些主机名到 IP 地址的匹配。这些匹配信息存放在 /etc/hosts 文件中。在没有域名服务器的情况下，系统上的所有网络程序都通过查询该文件来解析对应于某个主机名的 IP 地址。

### /etc/services文件

该文件定义了Linux系统中所有服务的名称、协议类型、服务的端口等信息。

### traceroute

该命令可以显示数据包到目标主机之间的路径。

traceroute [www.163.com](http://www.163.com/)

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 20.png)

### ifconfig(可以显示和配置网络接口，如ip地址，mac地址）

ifconfig eno16777736 192.168.0.100 netmask 255.255.255.0 up （配置网卡 eno16777736 的 IP 地址， 同时激活该设备。）

ifconfig eno16777736:1 192.168.0.3   （配置网卡 eno16777736 别名设备 eno16777736:1 的 IP）

ifconfig eno16777736:1 up   （激活网卡 eno16777736:1 设备。）

ifconfig eno16777736:1 down  (禁用网卡eno16777736:1设备）

ifconfig eno16777736 （查看网卡 eno16777736 网络接口的配置。）
ifconfig （查看素有网卡网络接口配置）

ifconfig eno16777736 hw ether 00:0C:29:18:2E:3D  (更改网卡的硬件MAC地址）

### ping

ping -s 128 192.168.0.222 (测试连通性，并且每次发送的ICMP数据包大小为128字节）

ping -c 4 192.168.0.5 (测试连通性，要求返回4个icmp数据包）

### netstat（路由表信息）

命令用来显示网络状态的信息，得知整个 Linux 系统的网络情况，比如网络连接、路由表、接口统计、伪装连接和组播成员。

netstat[选项] [延迟]

netstat -r  （显示内核路由表信息）

netstat -antu | grep 22（显示端口号为22的连接情况）

netstat -u （显示UDP传输协议的连接状态）

### arp

使用 arp 命令可以用来增加、删除和显示ARP 缓存条目。

arp [选项 ] [IP 地址 ][MAC 地址 ]

arp (查看系统arp缓存）

arp -s 192.168.0.99 00:60:08:27:CE:B2  (添加一个IP地址和MAC地址的对应记录）

arp -d 192.168.0.99 (删除一个对应记录）

### tcpdump

是 Linux 系统中强大的网络数据采集分析工具之一，可以将网络中传送的数据包的头完全截获下来提供分析。

tcpdump [选项 ] [表达式]

tcpdump -i eno16777736 (使用指定的网络接口 eno16777736 读取数据链路层的数据包头。）

### DNS服务使用什么端口号（12-3） ：  53号

## 管理网络服务

systemd ，它提供更优秀的框架以表示系统服务间的依赖关系，并实现系统初始化时服务的并行启动，同时达到降低 Shell 的系统开销的效果，最终代替现在常用的 System V。

## systemctl命令语法

使用 systemctl 控制单元时，通常需要使用单元文件的全名，包括扩展名（比如sshd.service ）。如果没有指定扩展名systemctl 默认把扩展名当作 .service 。

systemctl [选项 ] [单元命令] [单元文件命令]

systemctl start named.service(启动named服务）

systemctl status named.service(查看named服务当前状态）

停止 ：stop   重启 ：restart     重新加载：reload    开机自动启动：enable   

停止开机自启动：disable

systemctl list-units —type = service（查看所有已启动的服务）

# 第十三章 远程连接服务器配置（ssh、scp、sftp、rsync）

使用 SSH 可以在本地主机和远程服务器之间进行加密地传输数据，ftp和telnet是不安全的

而 OpenSSH 是 SSH 协议的免费开源实现，它用安全、加密的网络连接。（13-1为什么替代telnet）

### openssh服务器配置实例

OpenSSH 服务器 IP 地址： 192.168.0.2 。
OpenSSH 服务器监听端口： 22 。
不允许空口令用户登录。
禁止用户 lisi 登录。

配置如下：修改/etc/ssh/sshd_config文件如下：

Port 22

ListenAddress 192.168.0.2

PermitEmptyPasswords no 

DenyUser lisi

之后执行命令：systemctl  start sshd.service       systemctl enable sshd.service

### ssh

ssh -l zhangsan 192.168.0.100(以用户zhangsan登录到IP地址。。。。）

ssh root@192.168.0.100  ls /boot  (以 root 连接主机 192.168.0.100 ，并执行 ls /boot 命令。)

### scp

使用 scp 命令可以用来通过安全、加密的连接在不同主机之间传输文件

scp [选项 ] [用户 主机 1:] 文件 1 [[ 用户 主机 2:] 文件 2

scp /root/a  root@192.168.0.100:/root/b  (用 root 账号把本地文件 root/a 传送到 192.168.0.100 远程主机下的/root 下，并改名为 b )

scp /ab/*   root@192.168.0.100:/root    用 root 账号把本地 /ab 目录下所有文件传送到 192.168.0.100远程主机的/root 目录。

scp root@192.168.0.100:/root/abc  /root/a   用 root 账号把远程主机 192.168.0.100 上的文件 /root/abc 传送到本地主机/root 目录下，并改名为 a

### VNC服务配置

虚拟网络连接（VNC),允许用户在网络的任何地方使用简单的程序来和一个特定的计算机（服务器）进行交互。

### vnc软件组成部分：服务端的VNC server和客户端的VNC viewer。（13-2）

### 创建或更改VNC登录密码

vncpasswd [密码文件]
vncpasswd [选项]

创建或更改VNC登录密码

vncpasswd (创建或更改VNC登录密码）

### 管理vnc服务器

使用 vncserver 命令可以管理 VNC 服务器，比如启动和停止 VNC 服务器。

vncserver [:虚拟桌面号码 ] [选项 ] [Xvnc 选项]

vncserver -list (列出当前用户的vnc虚拟桌面)

vncserver -kill :1 (杀死号码为 1 的 vnc 虚拟桌面)

vncserver :5 ( 启动号码为 5 的 vnc 虚拟桌面)

vncviewer [选项 ] [主机] [:虚拟桌面号码]（客户端连接）

vncviewer 192.168.0.2:1  (使用 vncviewer 命令连接到 VNC 服务器。)

# 第十四章 NFS服务器配置

## NFS简介（network file system)

### NFS含义：NFS 对于在同一个网络上的多个用户间共享目录和文件很有用途。通过使用NFS ，用户和程序可以像访问本地文件一样访问远程系统上的文件。（14-1）

### /etc/exports文件内容的格式（14-2）：/etc/exports 文件控制着 NFS 服务器要导出的共享目录以及访问控制。

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 21.png)

NFS配置文件位于/etc/exports文件下

通过配置 NFS 服务器 可以让客户机挂载 NFS服务器上的共享目录、文件就如同位于客户机的本地硬盘上一样。

systemctl start nfs-server.service(启动服务）   systemctl status nfs-server.service（查看状态）   systemctl stop nfs-server.service（停止服务）  systemctl restart nfs-server.service(重启）

systemctl enable nfs-server.service(开机自启动）

## 查看NFS共享目录信息

showmount -e 192.168.0.2    查看 NFS 服务器 192.168.0.2 上共享目录的信息。

## 挂载NFS文件系统

mkdir /mnt/it  mount 192.168.0.100:/it  /mnt/it   (挂载远程主机192.168.0.100 的 NFS 目录 /it 到本地主机 /mnt/it)

PE是块

pv是逻辑卷

# 什么是LVM

Logical Volume Manager（逻辑卷管理）。是linux对磁盘分区进行管理的一种机制。屏蔽了底层磁盘布局，便于动态调整磁盘容量。/boot分区用于存放引导文件，不能应用LVM机制。

## pv(physical volume)物理卷:

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 22.png)

先要创建新的物理卷：pvcreate /dev/sda3

之后创建卷组：vgcreate -s 8M wgroup /dev/sda3  格式：vgcreate –s 块大小 卷组名 物理卷设备名

之后创建逻辑卷:lvcreate -n lv1 -L 100M wgroup     格式：lvcreate -n 【逻辑卷名】 –L 【逻辑卷大小】 【已存在卷组名】

之后格式化逻辑卷（建立文件系统）mkfs -t ext4 /dev/mapper/wgroup - lv1

## 扩大（缩小）逻辑卷及文件系统

![Untitled](C:\Users\93190\AppData\Local\Temp\Temp1_Export-高级linux.zip\高级linux c475eb43fd3e49c0937ac3074246a738\Untitled 23.png)

### 扩大逻辑卷 ：Lvextend –L 【扩展大小】 【逻辑卷设备名】

### 扩展文件系统大小：resize2fs –p 逻辑卷设备名

![Untitled](高级linux c475eb43fd3e49c0937ac3074246a738/Untitled 24.png)