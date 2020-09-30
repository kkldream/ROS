# 環境安裝筆記

# 安裝

## Windows 虛擬機：
* VirtualBox
* Ubuntu 18.04
* ROS Melodic Morenia

參考連結：https://medium.com/@gino6178/ros-%E9%96%8B%E7%99%BC%E8%88%87%E5%AF%A6%E6%88%B0-%E5%AE%89%E8%A3%9Dmelodic-4a2d76ceb68b

## Raspberry Pi 3/4：
* Ubuntu 16.04
* ROS Kinetic Kame 

ROS 專用 ISO 檔 Ubiquity Robotics 下載連接：https://downloads.ubiquityrobotics.com/

參考連結：http://wiki.ros.org/ROSberryPi/Installing%20ROS%20Kinetic%20on%20the%20Raspberry%20Pi

# 環境配置
## 修改自動配置網路：
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
參考網址：https://www.itread01.com/content/1550025751.html

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
參考網址：https://peterli.website/%E5%A6%82%E4%BD%95%E5%9C%A8ubuntu-16-04%E6%88%9618-04%E4%B8%8A%E5%AE%89%E8%A3%9D%E8%88%87%E8%A8%AD%E5%AE%9Avnc-server/