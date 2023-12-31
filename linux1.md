#### 建立一个新文件

```
touch  创建空白文件或修改文件时间

vi/vim 创建文件编辑文件并保存

>      定向输出到文件，如果文件不存在则创建文件；若文件存在，则将其清空

cat    一次显示整个文件；
       从键盘创建一个文件，只能创建新文件，不能编辑已有文件；
       将几个文件合并为一个文件。
       cat file1 file2 > file3 ：将两个文件拼接在一起生成一个新的文件 
       cat file1 >> file2  ：将文件1直接接在文件2的结尾  
```

#### Linux启动过程

```
BIOS加电自检
硬盘0柱面 0磁道 第一扇区读512字节 MBR主引导记录
运行引导程序Grub并根据初始化配置执行/etc/rc.sysinit脚本
根据第三步读取道德runlevel值启动对应的服务
运行/etc/rc.local
生成终端待用户登录

https://www.linuxidc.com/Linux/2014-03/97862.htm
--init启动进程 读取 /etc/inittab
```

#### Linux系统调用

```
用户进程调用内核功能的接口

systemd,用户进程调用内核的虚拟接口 
5个系统调用∶open,write,read,close,ioctl 
```

<br/>

#### DNS服务器主配置文件

```
/etc/named.conf
```

#### 结束进程

```
kill pid 退出进程
kill %job number 杀掉进程
```

 #### 文件句柄

```
文件IO中读取文件首先调用系统函数并传送文件名，选择一个路径打开文件。
函数取回的顺序号就是文件句柄。 

文件句柄 0 ，1 ，2分别是 标准输入(键盘)，标准输出(显示器)，标准错误(显示器)
3 ， 4 标准辅助(串行口)， 标准列表(打印机)
```

#### 在某文件夹内查找内容含有"abc"的文件

```
grep "abc"*  根据文件内容查找

`find . | xargs grep -ri "abc"`: 这个命令首先使用`find`命令在当前目录（`.`）及其子目录中查找所有文件，并将结果通过管道传递给`xargs`命令。`xargs`命令将`find`命令的输出作为参数传递给`grep`命令，然后使用`grep`命令在这些文件中递归地搜索匹配模式"abc"的行。
选项`-ri`表示忽略大小写（`-i`）并递归搜索（`-r`）。 

find -name "abc" 精确查找，按文件名查找文件
find会遍历当前目录甚至整个文件系统来查找文件或目录

```

#### 操作文件权限
```
chmod

```

#### du/df命令
```
du  //disk usage 用于显示目录或文件的大小，du会显示指定的目录或文件所占用的磁盘空间。
df  //disk free 命令用于显示目前在Linux系统上的文件系统磁盘使用情况统计。

```
#### vi编辑器删除最后一行
```
G  --> Shift + G  表示跳转到最后一行
dd --> dd         表示删除一行
```
#### vi编辑器删除第7到第10行内容
```
光标移动到第7行
4dd ---表示删除当前行开始4行数据
ndd ---删除当前行开始的连续n行
n1,n2d ---删除n1到n2行
n,$d ---删除从n行开始至文本末尾
```
#### OSI模型
```
HTTP协议工作在第7层，交换机工作在第2层

物理层： RJ45 、 CLOCK 、 IEEE802.3 （中继器，集线器，网关） -     
数据链路： PPP 、 FR 、 HDLC 、 VLAN 、 MAC （网桥，交换机） -     
网络层： IP 、 ICMP 、 ARP 、 RARP 、 OSPF 、 IPX 、 RIP 、 IGRP 、 （路由器） -     
传输层： TCP 、 UDP 、 SPX -     
会话层： NFS 、 SQL 、 NETBIOS 、 RPC -     
表示层： JPEG 、 MPEG 、 ASII -     
应用层： FTP 、 DNS 、 Telnet 、 SMTP 、 HTTP 、 WWW 、 NFS
```
#### 给定文件中查找与设定条件相符字符串的命令
```
grep
```
#### Linux安装RHELx，系统默认安装DHCP服务器软件包
```
RHEL5

DHCP服务器的配置文件为/etc/dhcpd.conf
DHCP服务器的配置文件默认是不存在的，需要手工创建


RHEL6/RHEL7

DHCP服务器的配置文件为/etc/dhcp/dhcpd.conf
DHCP服务器的配置文件默认是存在的，不需要创建
```

#### 侦测主机到目的主机之前所经过的路由
```
traceroute 探测路由经过

ping 检测两部主机之间的传输信道是否畅通，或远程主机是否正常

route 显示目前本机路由表的内容，并且还可以针对路由表中的记录来进行相应的添加、删除或修改等操作

ifconfig 检测和设置本机的网络接口
```

#### 文件权限10位长度(四段内容)
```
1，代表文件类型，一般有三类，- 代表普通的二进制文件，l 代表符号链接文件（软链接），d 代表目录文件 
2-4，代表文件所有者的权限表示情况，分别对应 可读(r) 可写(w) 可执行(w)，- 代表没有该项权限 
5-7，代表文件所有这所属组的权限表示情况。分别对应 可读(r) 可写(w) 可执行(w)，- 代表没有该项权限 
8-10,代表除文件所有者和所属组的其他人所拥有的权限表示情况。分别对应 可读(r) 可写(w) 可执行(w)，- 代表没有该项权限 

创建一个文件的默认权限应该就是777-022=755 
由于 执行权限(x) 比较危险，Linux默认不会赋予此权限，所以实际创建文件的默认权限是 755-111=644 
如果此时创建的是一个软链接文件，则权限位为 lrx-r--r-；如果此时创建的是一个普通文件，则权限位为 -rx-r--r--；如果此时创建的是一个目录文件，则权限位为 drx-r--r--

```

#### 用户操作命令
```
useradd 命令用于建立用户帐号；
usermod 命令用于修改用户帐号；
groupadd 命令用于创建一个新的工作组，新工作组的信息将被添加到系统文件中；
userdel 命令用于删除用户帐号。
```

#### socket
```
socket存在两种模式:阻塞和非阻塞

如果socket设置成非阻塞模式,当socket的输入缓冲区没有可读数据时,read操作会返回错误

在阻塞socket上调用write函数发送数据,函数返回时,表示数据已经发送出去

```阻塞模式发送成功并接受才会返回；非阻塞模式发送后立即返回。```
```非阻塞模式下如果缓冲区没内容，表示没数据可读取，立即返回非0。```
```阻塞模式下，write有返回时未必发送成功，也可能是错误。 ```

```

#### awk'BEGIN { Arr[2,79]=78 __________ }'为了让执行的结果是78，应该填（）语句
```
https://blog.csdn.net/ithomer/article/details/8478716

awk 中数组叫做关联数组(associative arrays)，下标可以是数字也可以是字符串。awk 中的数组不必提前声明，也不必声明大小，初始化数组元素用 0 或空串，这根据上下文而定。

语法： awk '{pattern + action}'    或   awk 'pattern {action}'

/*
pattern 表示 AWK 在数据中查找的内容， action 是在找到匹配内容时所执行的一系列命令。花括号 {} 不需要在程序中始终出现，但它们用于根据特定的模式对一系列指令进行分组（作用域）。
*/

print Arr["2\03479"]
/

print Arr[2,79]
/

idx=2 SUBSEP 79;print Arr[idx]
/

print Arr[ 2, 79]
/

```

#### bash配置文件
```
.bash_logout：退出shell时，要执行的命令

.bash_profile：每个用户都可使用该文件输入专用于自己使用的shell信息，当用户登录时，该文件仅仅执行一次!默认情况下

/etc/profile：此文件为系统的每个用户设置环境信息，当用户第一次登录时，该文件被执行


.bash_profile 类似于编程中的构造函数，当登录shell时，shell会寻找该文件做环境初始化。 .bashrc 是在bash环境时.bash_profile的替补。 .bash_logout 类似于编程中的析构函数，当登录shell退出时，shell会寻找该文件，并按其指示办事。 /etc/profile是系统文件,对系统下全体用户起作用
```