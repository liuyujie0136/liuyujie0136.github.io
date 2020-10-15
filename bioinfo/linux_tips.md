# Linux使用技巧与注意事项
> Collected by liuyujie0136

## Docker
> Docker is a tools to run Linux containers based on selected images.

### [Docker从入门到实践](https://yeasy.gitbook.io/docker_practice/)

### Win10家庭版用WSL2运行Docker Desktop，将数据从C盘迁移到其他目录

Win10开始使用Hyper-V运行docker，家庭版无此功能，所以只能pro版本才能用docker desktop。后来升级到2004系统后，家庭版升级WSL(Windows Subsystem for Linux)至WSL2后，便可基于WSL2运行docker desktop，但相较于Hyper-V的区别在于，其数据由WSL2代为管理，无法在docker里设置镜像存储路径。

安装docker后，docker会自动创建2个发行版：docker-desktop和docker-desktop-data，其默认安装在C盘，在%LOCALAPPDATA%/Docker/wsl目录里，而docker的运行数据、镜像文件都存在%LOCALAPPDATA%/Docker/wsl/data/ext4.vhdx中，比较占用C盘空间，故考虑将其迁移至D盘。

对于WSL发行版的迁移，网上教程基本均需使用LxRunOffline，但其虽然可以迁移例如Ubuntu的发行版，但迁移不了docker自动创建的2个发行版。故考虑如下两种方式：

**方法一：使用wsl命令**

* 关闭docker desktop
* 关闭所有发行版
```
wsl --shutdown
```
* 导出docker-desktop-data
```
wsl --export docker-desktop-data D:\docker-desktop-data.tar
```
* 注销docker-desktop-data
```
wsl --unregister docker-desktop-data
```
* 重新导入docker-desktop-data
```
wsl --import docker-desktop-data D:\Tools\WSL\docker-desktop-data\ D:\docker-desktop-data.tar --version 2
```
* _注：只迁移docker-desktop-data即可，另一个占用空间较小_

**方法二：修改注册表（未直接验证，理论上及其他操作证明应当可行）**

* 关闭docker desktop
* 打开`powershell`，输入`whoami /user`，获得[SID]；用`wsl --shutdown`命令关闭所有发行版
* 运行`regedit`，跳转至`HKEY_USERS\[SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss`
* 在下属的文件文件夹中（文件夹名为一个UUID）找到`DistributionName`为`docker-desktop-data`的项
* 将其`BasePath`改为目标目录，如`\\?\D:\Tools\WSL\docker-desktop-data`，并将原目录下`ext4.vhdx`拷贝至该目录
* 重启即可使用

### Docker创建共享文件夹

* 检查docker是否安装成功
```
docker info
```
* 装载镜像
```
docker load -i ~/Downloads/bioinfo_PartI-PartII-PartIII1-3.tar.gz
```
* 创建共享文件夹
```
mkdir ~/Documents/bioinfo_tsinghua_share
```
* 创建容器**（win10下共享文件夹需用绝对路径）**
```
docker run --name=bioinfo_tsinghua -dt -h bioinfo_docker --restart unless-stopped -v C:/Users/[username]/Documents/bioinfo_tsinghua_share:/home/test/share bioinfo_tsinghua
```
* 将docker中的`/home/test/share`由`root`所有改为`test`所有
```
docker exec -u root bioinfo_tsinghua chown test:test /home/test/share
```
* 以`test`用户运行docker
```
docker exec -it bioinfo_tsinghua bash
```
* _注：以`root`用户运行docker_
```
docker exec -it -u root bioinfo_tsinghua bash
```

## [鳥哥的Linux私房菜](http://linux.vbird.org/linux_basic/)

## [Linux常用命令](https://mp.weixin.qq.com/s/cri9CEbVJizZIO9WwiCJ0g)

## [Linux特殊符号](https://mp.weixin.qq.com/s/IO8Ckahig14RIvyDPX5lhw)

## Linux查看系统基本信息

1. 查看版本当前操作系统内核信息
```bash
uname -a
```
2. 查看当前操作系统版本信息
```bash
cat /proc/version
```
3. 查看版本当前操作系统发行版信息
```bash
cat /etc/issue
```
4. 查看cpu相关信息，包括型号、主频、内核信息等
```bash
cat /proc/cpuinfo
```
5. 查看服务器名称
```bash
hostname
```
6. 查看网络信息
```bash
cat /etc/sysconfig/network-scripts/ifcfg-eth0
cat /etc/sysconfig/network-scripts/ifcfg-l0
```
7. 查看磁盘信息
```bash
lsblk		#查看磁盘信息 - 列出所有可用块设备的信息，而且还能显示他们之间的依赖关系，但是它不会列出RAM盘的信息
fdisk -l		#观察硬盘实体使用情况，也可对硬盘分区
df -k		#用于显示磁盘分区上的可使用的磁盘空间
```
8. 查看进程与用户信息
```bash
ps -ef		#查看所有进程
top		#实时显示进程状态
w		#查看活动用户
id <username>	#查看指定用户信息
```
9. [更多内容](https://blog.csdn.net/qq_31278903/article/details/83146031)

## Bash和Sh的区别
> Bash is the most commonly used linux shell.

## 利用.bashrc个性化配制bash环境



## 利用.vimrc个性化配置vim



## Linux中for循环的几个常用写法

1. 数字性循环
```bash
#!/bin/bash

for((i=1;i<=10;i++));
do
	echo $(expr $i \* 3 + 1);
done

for i in $(seq 1 10)
do
	echo $(expr $i \* 3 + 1);
done

for i in {1..10}
do
	echo $(expr $i \* 3 + 1);
done

awk 'BEGIN{for(i=1; i<=10; i++) print i}'

exit 0
```
2. 字符性循环
```bash
#!/bin/bash

for i in `ls`;
do 
	echo $i is file name\! ;
done

for i in $* ;
do
	echo $i is input chart\! ;
done

for i in f1 f2 f3 ;
do
	echo $i is appoint ;
done

list="rootfs usr data data2"
for i in $list;
do
	echo $i is appoint ;
done

exit 0
```
3. 路径查找
```bash
#!/bin/bash

for file in /proc/*;
do
	echo $file is file path \! ;
done

for file in $(ls *.sh)
do
	echo $file is file path \! ;
done

exit 0
```

## Linux下ls命令只显示目录的方法

```bash
ls -F | grep '/$'	#最易用，若将其结果保存在变量里，可用循环遍历并用cd访问
ls -l | grep '^d'	#显示信息最完整
```
附：ls与cd连用示例
```bash
#!/bin/bash

dir=`ls -F | grep "/$"`
for i in $dir
do
	cd $i
	files=`ls`	# or files=$(ls)
	for j in $files
	do
		cat $j >> /home/test/share/all.out
	done
	cd ..
done
exit 0
```

## Linux下替换^M字符方法

在Linux下使用`vi`或`cat -A`查看一些在Windows下创建的文本文件，有时会发现在行尾有一些`^M`，既影响文件的查看，也影响利用`awk`等命令对文件进行操作，见下：
```bash
test@bioinfo_docker:~/share$ cat -A text.txt
1^M$
2^M$
3^M$
4^M$
5^M$
6^M$
7^M$
8^M$
```
有如下解决方法：

* 使用`dos2unix`命令（**建议所有在win下创建的文件均先在root用户下运行此命令转换一下格式**）
```bash
dos2unix text.txt
```
* 使用vi的替换功能，在vi的命令模式下输入:
```
:%s/^M$//g		#去掉行尾的^M
:%s/^M//g		#去掉所有的^M
:%s/^M/[ctrl-v]+[enter]/g	#将^M替换成回车
:%s/^M/\r/g		#将^M替换成回车
```
* 使用`sed`命令
```bash
sed -e 's/^M/\n/g' text.txt	#注意：^M需使用[ctrl-v] [ctrl-m]生成，并非直接输入
```
* 注：在vim的.vimrc文件中把fileformat=unix去掉便不会显示（默认不显示^M）

## Linux下将多行文件合并为一行

* _注意，对于win下文件（非linux创建），建议先运行`dos2unix`命令_

* 使用`awk`命令
```bash
awk 'BEGIN{ORS=" "} {print}' text.txt
#ORS：输出行分隔符，默认\n，此处改为空格，故可使两行合并

awk 'BEGIN{RS=EOF} {gsub(/\n/," "); print}' text.txt
#RS：输入行分隔符，默认\n，此处改为EOF文件结尾，故可一次读入整个文件，方便替换操作
```

* 使用`sed`命令
`sed`默认按行处理，`N`可以让其读入下一行，再对\n进行替换，这样就可以将两行并做一行。但为了将所有行并作一行，需要采用其跳转功能。`:flag`在代码开始处设置一个标记`flag`，在代码执行到结尾处时利用跳转命令`t flag`重新跳转到标号`flag`处，重新执行代码，这样就可以递归将所有行合并成一行。
```bash
sed ':flag; N; s/\n/ /g; t flag;' text.txt
```

* 使用`xargs`命令
```bash
cat text.txt | xargs
```

* 附：文件合并、行筛选、多行合并脚本示例
```bash
#!/bin/bash

if [ all.out ]; then rm all.out; fi

dir=`ls -F | grep "/$"`
for i in $dir
do
	echo $i >> all.out
	cd $i
	files=`ls`
	for j in $files
	do
		dos2unix $j
		echo $j >> ../all.out
		awk 'BEGIN{ORS=" "}; /^[^0-9]/{print}' $j >> ../all.out
		echo -e "\n" >> ../all.out
	done
	cd ..
done
exit 0
```

## Ubuntu镜像使用帮助

* [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/)
* Ubuntu的软件源配置文件是`/etc/apt/sources.list`。将系统自带的该文件做个备份，再将该文件替换为下面内容，即可使用TUNA的软件源镜像。

```vim
# ubuntu版本: 18.04 LTS
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

## Ubuntu下使用`apt install XX`(`sudo apt install XX`)报错`Unable to locate package`
* 解决方法一：正常情况下只需要更新软件列表
```bash
sudo apt update
```
* 解决方法二：方法一无效时
```bash
sudo apt upgrade
```
* 注：一般情况下更改了软件源之后需要重新`update`

---

**声明：上述内容根据多种参考资料整理，在此不一一列举，仅供个人学习，版权归原作者所有。**


