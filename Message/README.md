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
   <Msg_Name.msg>
)

```
### Msg 建立位置：
```sh
roscd <Package_Name>
mkdir msg
cd msg
touch <Msg_Name.msg>
```

### `Msg_Name.msg` 範例：
```
int64 id
string title
string content
```

### 最後：
```sh
catkin_make
```
