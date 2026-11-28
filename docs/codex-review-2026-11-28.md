# Codex 工程审阅注释（2026-11-28）

审阅者：Codex。本页仅依据仓库中的配置和脚本提出检查点；没有连接设备，也没有运行 ROS 2 或 Gazebo。它不是团队的实测记录。

## 1. 雷达方向要同时核对配置与 TF

`Rui_03` 分支的 [SCL.yaml](https://github.com/ianhequn/ros2_22_orangpi3b_261101/blob/Rui_03/others/ydlidar_scl_params/SCL.yaml) 指定了 `frame_id: lidar_scan_link`，并设置扫描方向相关参数。最近两次提交调整了这份配置。下一次实机检查时，可把固定障碍物依次放在车体前、左、右三个已知方向，记录 `/scan` 在 RViz 中的方位，并同时核对 `base_link` 到 `lidar_scan_link` 的 TF。仅看雷达图像“转正”不足以判断导航使用的坐标方向也正确。

## 2. 速度指令要确认到达控制器

[qos_relay.py](https://github.com/ianhequn/ros2_22_orangpi3b_261101/blob/Rui_03/src/dd_chassis_001_driver/scripts/qos_relay.py) 把 `/cmd_vel` 转发到 `/diff_drive_controller/cmd_vel_unstamped`，并在累计转发时打印计数。排查“规划成功但车不动”时，分别检查输入和输出话题的发布者、订阅者及 QoS，再检查控制器是否收到非零速度；仅有 `/cmd_vel` 消息不能证明底盘已收到命令。停机或失联时的零速度行为也应单独验证。

## 3. 左右轮方向与比例分别验证

[ros2_control 配置](https://github.com/ianhequn/ros2_22_orangpi3b_261101/blob/Rui_03/src/dd_chassis_001_driver/config/dd_chassis_001.ros2_control.xacro) 分别设置左右电机序号、速度比例和方向翻转。调试时先让单侧车轮低速转动，确认电机序号与轮子对应，再分别记录左右轮的指令值和反馈值，最后测试前进与原地转向。这样可以区分轮子接反、符号反向和比例标定误差。

以上三项完成后，建议把设备型号、固件版本、启动命令、话题/TF 截图或日志以及失败案例链接回本页，再更新“已验证”状态。
