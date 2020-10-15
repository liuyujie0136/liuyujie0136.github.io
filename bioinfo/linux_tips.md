# Linux使用技巧与注意事项
> 根据多种参考资料整理，在此不一一列举，仅供个人学习，版权归原作者所有

## Docker
> Docker is a tools to run Linux containers based on selected images.

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
* 打开`powershell`，输入`whoami /user`，获得[SID]；用`wsl --shutdown`关闭所有发行版
* 运行`regedit`，跳转至`HKEY_USERS\[SID]\SOFTWARE\Microsoft\Windows\CurrentVersion\Lxss`
* 在下属的文件文件夹中（文件夹名为一个UUID）找到`DistributionName`为`docker-desktop-data`的项
* 将其`BasePath`改为目标目录，如`\\?\D:\Tools\WSL\docker-desktop-data`，并将原目录下`ext4.vhdx`拷贝至该目录
* 重启即可使用

### Docker创建共享文件夹









