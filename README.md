<h1 align="center">钉钉的AppImage打包</h1>

<p align="center">
<img alt="GitHub stars" src="https://img.shields.io/github/stars/TwinklerG/dingtalk-appimage">
<img alt="GitHub All Releases" src="https://img.shields.io/github/downloads/TwinklerG/dingtalk-appimage/total">
</p>


# 免责声明

本项目源于钉钉官方deb包的解包结果，不保证稳定性和跨发行版，可供自用，目前在我的fedora41 workstation平台下没有任何问题

由于钉钉是商业软件，我没有对其二进制文件分发的权利，只是进行一些简单打包，方便linux平台用户使用

# 快速开始

访问Release界面下载并运行appImage文件

```shell
chmox +x ./dingtalk.AppImage
./dingtalk.AppImage
```

# 友情提醒

如何不想使用AppImage版本或者想解包运行，可以参考以下教程，我在fedora41平台实测没有问题

以下友情提醒来自fedora吧老哥：

**钉钉自带libm的版本有问题，需要删除,注意删的是钉钉自带的**

```shell
sudo rm libm.so.6
```
**缺少libcrypt.so.1**

```shell
sudo dnf install libxcrypt-compat
```
不同人的电脑上缺少的东西可能不同，可以使用ldd检查
```shell
cd /opt/apps/com.alibabainc.dingtalk/files/7.5.10-Release.404071
ldd com.alibabainc.dingtalk
ldd dingtalk_dll.so
```
**启动脚本计算libc版本有点问题**

打开Elevator.sh，发现用下面的命令来获得libc的版本
```shell
libc_version=`ldd --version | grep ldd | cut -d' ' -f5`
```
但是在我的电脑上只能获取到空，需要改为
```shell
libc_version=`ldd --version | grep ldd | cut -d' ' -f4`
```
就是将f5改为f4
