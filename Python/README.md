### 常用程式：
```python
#!/usr/bin/python
## coding=utf-8
import rospy                            # import rospy 模組
frq = rospy.get_param("/print_frq", 10) # 取得 parameter 變數 或 預設值
rospy.init_node('hello_python_node')    # 初始化 hello_python_node
while not rospy.is_shutdown():          # 在 rospy 還沒結束前，執行下列指令:
    rospy.loginfo('Hello World')        # 印出 Hello World
    rospy.sleep(frq)                    # 間隔 frq 秒
```