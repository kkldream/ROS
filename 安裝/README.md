# 目錄
* [根目錄](https://github.com/kkldream/ROS-Note/)
    * [安裝](安裝)
    * [Message](Message)
    * [Python](Python)
* [環境安裝筆記](#環境安裝筆記)
    * [Raspberry Pi 4 Ubuntu 18.04 aarch64 (2020/10/31)](#Raspberry-Pi-4-Ubuntu-18.04-aarch64-20201031)
    * [Windows 虛擬機 (2020/9/26)](#Windows-虛擬機-2020926)
    * [Raspberry Pi 3/4 Ubiquity (2020/9/25)](#Raspberry-Pi-3/4-Ubiquity-2020925)
* [環境配置](#環境配置)
    * [修改自動配置網路](#修改自動配置網路)
    * [Ubuntu 上安裝與設定 VNC Server](#Ubuntu-上安裝與設定-VNC-Server)

# 環境安裝筆記
## Raspberry Pi 4 Ubuntu 18.04 aarch64 (2020/10/31)
* Raspberry Pi 4 Model B 4GB
* [Ubuntu 18.04 64位元](https://github.com/TheRemote/Ubuntu-Server-raspi4-unofficial/releases/tag/v28)
* ROS Melodic Morenia
1. 添加 sources.list
```sh
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
2. 添加公钥
```sh
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
3. 安装
```sh
sudo apt update
# 桌面完整版（推荐）： : 包含 ROS、rqt、rviz、机器人通用库、2D/3D 模拟器、导航以及 2D/3D 感知包。
sudo apt install ros-melodic-desktop-full
#桌面版： 包含 ROS，rqt，rviz 和机器人通用库
sudo apt install ros-melodic-desktop
# ROS-基础包： 包含 ROS 包，构建和通信库。没有图形界面工具。
sudo apt install ros-melodic-ros-base
# 单独的包： 你也可以安装某个指定的ROS软件包（使用软件包名称替换掉下面的PACKAGE）：
sudo apt install ros-melodic-PACKAGE
# 如：
sudo apt install ros-melodic-slam-gmapping
# 要查找可用软件包，请运行：
apt search ros-melodic
```
4. 初始化 rosdep
```sh
sudo rosdep init
rosdep update
```
5. 设置环境
```sh
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
6. 构建工厂依赖
```sh
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
```
原文連結：http://wiki.ros.org/cn/melodic/Installation/Ubuntu

## Windows 虛擬機 (2020/9/26)
* VirtualBox
* [Ubuntu 18.04](https://www.ubuntu-tw.org/modules/tinyd0/)
* ROS Melodic Morenia

原文連結：https://medium.com/@gino6178/ros-%E9%96%8B%E7%99%BC%E8%88%87%E5%AF%A6%E6%88%B0-%E5%AE%89%E8%A3%9Dmelodic-4a2d76ceb68b

## Raspberry Pi 3 Ubiquity (2020/9/25)
* Raspberry Pi 3 Model B+ 1GB
* Ubuntu 16.04
* ROS Kinetic Kame 

ROS 專用 ISO 檔 Ubiquity Robotics 下載連接：https://downloads.ubiquityrobotics.com/

原文連結：http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi

# 環境配置
## 修改自動配置網路
修改 `/etc/network/interfaces`
```sh
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

allow-hotplug wlan0
auto wlan0
iface wlan0 inet dhcp
    wpa-ssid YOUR-SSID-HERE
    wpa-psk YOUR-PASSWORD-HERE
```
原文連結：https://www.itread01.com/content/1550025751.html

## Ubuntu 上安裝與設定 VNC Server
```sh
sudo apt install vnc4server -y
sudo apt install xfce4 xfce4-goodies autocutsel-y
```
修改 `~/.vnc/xstartup`：
```sh
#!/bin/bash
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
 
autocutsel -fork
vncconfig -iconic &
vncconfig -nowin &
startxfce4 &
```
使用方法：
```sh
# 建立
vncserver :1
vncserver -geometry 1200x800 :1
# 刪除
vncserver -kill :1
# 查看
nmap localhost # 需先安裝 sudo apt install nmap
```
原文連結：https://peterli.website/%E5%A6%82%E4%BD%95%E5%9C%A8ubuntu-16-04%E6%88%9618-04%E4%B8%8A%E5%AE%89%E8%A3%9D%E8%88%87%E8%A8%AD%E5%AE%9Avnc-server/

