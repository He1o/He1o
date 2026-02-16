---
title: Linux
date: 2022-01-09
category: Command
---
<!--more-->
# Linux

## 1. 命令
Linux 的目录结构是一个树形结构，没有盘符的概念，只有一个根目录 / ，Linux 层级关系 / 表示，Windows \ 表示

linux 中一切都是文件

- bin Binary的缩写，这个目录存放着最经常使用的命令
  - /bin, /usr/bin, /usr/local/bin
  - sbin Super user,这里存放系统管理员使用的系统管理程序
- home 存放普通用户的主目录
- root
- lib 系统开机所需要最基本的动态链接共享库，作用类似windows里dll文件，几乎所有应用程序都需要这些共享库
- lost+found 一般是空的，系统非法关机后就存放一些文件
- etc 所有系统管理所需要的配置文件和子目录
- usr 非常重要的目录，用户很多应用程序和文件都放在这个目录下，类似windows program files目录
- boot 启动相关核心文件
- dev 设备管理器，
- mnt 系统提供该目录是为了让用户临时挂载别的稳健性，我们可以将外部的存储挂载在/mnt上，然后进入该目录就可以查看里面的内容
- opt 主机额外安装软件所存放的目录
- var 这个目录存放不断扩充的东西，包括各种日志文件

远程：xshell，xftp

命令：即Linux 程序

命令行：是一种命令提示符页面，以纯字符的形式操作系统

command [-options][parameter] 命令本身 可选选项 可选参数

### 系统
```bash
shutdown -h now //立即关机
shutdown -h 1 //一分钟后关机
reboot 重启
sync 把内存数据同步到磁盘
```

### 文件操作命令
```bash
ls [-a -l -h] 后面可以跟路径，展示目标路径文件
-a 展示所有文件，包括隐藏文件
-l 展示更多信息 ls -la组合使用
-h human易于阅读的形式
```

```bash
cd Change Directory
cd 直接回到home目录
cd / 取到根目录
pwd Print Work Directory
```

```bash
mkdir -p 创建连续多层级目录
touch 创建文件路径
cp -r 递归复制
rm -rf 
mv 可以用来重命名
```

### 文件内容命令

命令的本体是二进制可执行程序，相当于.exe

```bash
ctrl ＋ L 清空命令行
cat [-n 显示行号] 展示文件所有内容
more 翻页查看内容
cat 文件名 | more
```

```bash
less 指令用来分屏查看文件内容，less显示文件内容时，并不是一次将整个文件加载出来后显示，而是根据显示需要加载内容，对于显示大型文件具有较高的效率
空格、pagedown 向下翻动一页
pageup 向上翻动一页
/字符串 向下搜索，n向上查找，N向上查找
```

```bash
tail [-f -num] Linux 路径
-f 表示持续跟踪
-num 查看尾部多少行，默认10行
tail -5 test.txt

head [-n] 显示文件开头内容
head -n 5 test.txt
```

```bash
which cd 查看命令文件存在哪里
/usr/bin/cd
```

### 查找统计
```bash
find 起始路径 -name "被查找的文件名"
find 起始路径 -size + | -n[kMG]
find / -size +1G 查找大于1G的文件
```

```bash
grep [-n] 关键字 文件路径
从文件中通过关键字过滤文件行
grep -n "test" test.txt
```

```bash
wc 命令统计文件的行数、单词数量
-c 统计字节数
-m 统计字符数量
-l 统计行数
-w 统计单词数量
```

管道符
```bash
管道符 ｜
含义：将管道符左边命令的结果作为右边命令的输入
cat test.txt | grep "test"
ls /usr/bin | grep gtf
ls -l /usr/bin | wc -l 输出文件数量
```


```bash
echo 在命令行中输出指定内容
echo "Hello world"
` 反引号也称为飘号，被包围的内容会被作为命令执行而非普通字符
echo `pwd`
```

重定向符
```bash
重定向符 >和>>
> 将左侧命令的结果，覆盖写入符号右侧指定的文件中
>> 将左侧命令的结果，追加写入到符号右侧指定的文件中
```

### 其他
```bash
ln 软链接也称为符号链接
ln -s /root /home/myroot

history 查看已经执行过的历史命令
history 10 展示10条
!387  执行历史编号为387的命令
```
### 时间日期




## 2. vi编辑器
visual interface是Linux中最经典的文本编辑器

vim是vi的加强版本，兼容vi所有指令，不仅能编辑文本，还具有shell程序编辑的功能，可以不同颜色的字体来辨别语法的正确性，极大方便了程序的设计和编辑性。

- 命令模式， vi 进入，:wq退出
- 输入模式， i a o 进入，esc退出
- 底线命令模式 ， :进入 回车结束


## 3. 用户管理
无论windows、macos、linux均采用多用户的管理模式进行权限管理。
- 在linux中，拥有最大权限的账户名为root
- su - root 切换到root用户
- 普通用户的权限一般在HOME目录内室不受限的，一旦除了HOME目录，大多数地方，普通用户仅有只读和执行权限，无修改权限

### 创建与删除用户
```bash
useradd 用户名
useradd -d 指定目录 新的用户名
passwd 用户名 修改密码，不指定用户名则是当前登录的用户
userdel 用户名 删除用户
userdel -r 用户名 把家目录一起删除
```

### 查看用户
```bash
id 用户名
whoami 显示第一次登录到这个主机的用户信息，切换到别的用户后，也显示一开始的用户信息
```

### 切换用户
```bash
su 切换账户 switch user
su [-] [用户名]
- 符号可选，表示是否在切换用户后加载环境变量
省略用户名表示切换到root
切换用户后，使用logout退出用户，可以通过exit命令退回上一个用户，也可以使用快捷键ctrl+d
```
- 使用普通用户，切换到其它用户需要输入密码，如切换到root用户
- 使用root用户切换到其它用户，无需密码，可以直接切换

### 用户组
```bash
groupadd 用户组
groupdel 用户组
usermod -g 用户组 用户名
```
如果没有指定组，新增用户的时候会创建同名的组并把新用户放入其中。

- /etc/passwd 用户的配置文件，记录用户的各种信息
- 每行的含义：用户名：口令：用户标识号：组标识号：注释性描述：主目录：登录shell
- /etc/shadow 口令的配置文件
- 每行的含义：登录名：加密口令：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志
- /etc/group 组的配置文件，记录linux包含的组的信息
- 每行的含义：组名：口令：组标识号：组内用户列表


## 网络

### 网络第一包慢
```bash
ping -n refclient.ext.here.com
```
>PING refclient.ext.here.com (108.139.1.24) 56(84) bytes of data.
>64 bytes from 108.139.1.24: icmp_seq=1 ttl=243 time=1.18 ms
>64 bytes from 108.139.1.24: icmp_seq=2 ttl=243 time=1.18 ms
>64 bytes from 108.139.1.24: icmp_seq=3 ttl=243 time=1.14 ms
>64 bytes from 108.139.1.24: icmp_seq=4 ttl=243 time=1.15 ms
>64 bytes from 108.139.1.24: icmp_seq=5 ttl=243 time=1.14 ms
>64 bytes from 108.139.1.24: icmp_seq=6 ttl=243 time=1.14 ms

```bash
time ping -n refclient.ext.here.com -c 1
```
>1 packets transmitted, 1 received, 0% packet loss, time 0ms
>rtt min/avg/max/mdev = 1.188/1.188/1.188/0.000 ms
>real    0m5.011s
>user    0m0.000s
>sys     0m0.000s


## git 
.ssh/config 文件中配置


>Host github.com
>  User git
>  ProxyCommand nc -v -x 127.0.0.1:7897 %h %p