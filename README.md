創建一個ROS工作區

    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws/
    catkin_make

進入環境

    source devel/setup.bash

看當前環境變量目錄

    echo $ROS_PACKAGE_PATH

# 常見問題

## "roscore" command not found

    sudo apt install ros-melodic-desktop

參考連結：https://codeleading.com/article/42014334083/

---

## ROS: Can't find package configuration files

    sudo apt-get install ros-<distro>-rospy
    sudo apt-get install ros-melodic-rospy

參考連結：https://stackoverflow.com/questions/38664936/ros-cant-find-package-configuration-files

---
