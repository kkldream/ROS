# 目錄
* [根目錄](https://github.com/kkldream/ROS-Note/)
* [必要](#必要：)
* [常用](#常用：)

### 必要：
```python
#!/usr/bin/env python
## coding=utf-8
import rospy
rospy.init_node('hello_python_node')
```

### 常用：
```python
# 取得 parameter 變數 或 預設值
var = rospy.get_param("/print_frq", 10)
# 回傳 rospy 是否中止
var = rospy.is_shutdown():
# 印出字串
rospy.loginfo('Hello World')
# 延遲 1 秒
rospy.sleep(1)
```

