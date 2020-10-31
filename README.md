# 目錄
* [根目錄](https://github.com/kkldream/ROS-Note/)
    * [安裝](安裝)
    * [Message](Message)
    * [Python](Python)
* [工作區](#工作區)
* [其他](#其他)
    * [如何在ROS中使用Python3](#如何在ROS中使用Python3)
* [常見問題](#常見問題)

# 工作1[]2{}3<>4
創建一個ROS工作區
```sh
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
```
進入環境
```sh
source devel/setup.bash
```
看當前環境變量目錄
```sh
echo $ROS_PACKAGE_PATH
```
編譯目錄 (必須在根目錄下)
```sh
catkin_make
```
建立 Package
```sh
catkin_create_pkg <package_name> [depend1] [depend2] [depend3] ...
catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
```
後台啟動
```sh
roscore &
```
刪除roscore進程
```sh
killall -9 roscore
killall -9 rosmaster
```
說明
```sh
SHELL
```
## Launch file
建立：
```sh
roscd <package_name>
mkdir launch
cd launch
touch startup.launch
```
in `startup.launch`：
```xml
<launch>
    <param name="/print_frq" type="double" value="2.0" />
    <node name="talker" pkg="beginner_tutorials" type="talker.py" />
</launch>
```
執行：
```sh
roslaunch [package] [filename.launch]
```

# 其他
## 如何在ROS中使用Python3
```sh
pip3 install catkin-tools rospkg
```
Python 開頭加上：
```python
#!/usr/bin/env python3
```

# 常見問題
參考連結：https://www.cnblogs.com/h46incon/p/6207145.html
## "roscore" command not found

    sudo apt install ros-melodic-desktop

參考連結：https://codeleading.com/article/42014334083/

## ROS: Can't find package configuration files

    sudo apt-get install ros-<distro>-rospy
    sudo apt-get install ros-melodic-rospy

參考連結：https://stackoverflow.com/questions/38664936/ros-cant-find-package-configuration-files
