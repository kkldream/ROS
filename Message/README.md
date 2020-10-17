# 目錄
* [回主目錄](https://github.com/kkldream/ROS-Note/)
* [資源](#資源)
* [建立自定義的.msg檔](#建立自定義的.msg檔)
* [使用自定義的.msg檔](#使用自定義的.msg檔)
  * [Python](#Python)
  * [C++](#C++)
  
# 資源
### 官方提供的Message格式：(點擊圖片前往連結)
[![官方提供的message格式](https://ithelp.ithome.com.tw/upload/images/20181105/20112348d5eEuZCaMg.png)](http://wiki.ros.org/msg)

# 建立自定義的.msg檔
### `package.xml`：
```xml
<build_depend>message_generation</build_depend>
<exec_depend>message_runtime</exec_depend>
```
### `CMakeList.txt`：
```python
find_package(catkin REQUIRED COMPONENTS
   roscpp
   rospy
   std_msgs
   message_generation
)
...

catkin_package(
  # INCLUDE_DIRS include
  # LIBRARIES beginner_tutorials
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
  # DEPENDS system_lib
)
...

generate_messages(
   DEPENDENCIES
   std_msgs
)
...

add_message_files(
   FILES
   msg_name.msg
)

```
### Msg 建立位置：
```sh
roscd package_name
mkdir msg
cd msg
touch msg_name.msg
```

### `Msg_Name.msg` 範例：
```
int64 id
string title
```

### 最後：
```sh
catkin_make
```

# 使用自定義的.msg檔
## Python
```python
from package_name.msg import msg_name
msg = msg_name()
msg.id = 1
msg.title = "hello"
```
## C++
`talker.cpp`：
```c++
#include "ros/ros.h"
#include "package_name/msg_name.h"
int main(int argc, char **argv)
{
   ros::init(argc, argv, "talker");
   ros::NodeHandle n;
   ros::Publisher chatter_pub = n.advertise<package_name::msg_name>("chatter", 1000); 
   ros::Rate loop_rate(10);
   int count = 0;
   while (ros::ok())
   {
      package_name::msg_name msg;
      msg.id = count;
      msg.title = "hello";
      msg.content = "hello from c++";

      chatter_pub.publish(msg);
      ros::spinOnce(); 
      loop_rate.sleep();
      ++count;
   }
   return 0;
}
```
