# 当前状态与证据边界

本页依据已上传的七个仓库及 [大创项目文档](https://github.com/ianhequn/da_chuang_20261112) 整理工程状态。文档中的“拟研究”“候选”和“预期”不算已完成。

| 能力 | 目前可确认的基础 | 仍需完成的连接或验证 |
| --- | --- | --- |
| 底盘仿真、建图、导航 | [ChassisNav_02_u22_wsl](https://github.com/ianhequn/ChassisNav_02_u22_wsl) 有自建底盘 URDF、Gazebo、SLAM Toolbox 与 Nav2 配置和迭代 | 与统一观测、任务和机械臂接口联调；完整任务重复实验 |
| 真机底盘 | [ros2_22_orangpi3b_261101](https://github.com/ianhequn/ros2_22_orangpi3b_261101) 有串口驱动及 IMU/轮速相关实现、分级验证记录 | 与仿真观测接口对齐，确认采样时间、坐标、标定和稳定性 |
| 机械臂及数据流 | [ArmPi_Ultra_260913](https://github.com/ianhequn/ArmPi_Ultra_260913) 记录 ROS 2 控制、反馈与 LeRobot 流的真机验证 | 成为具备状态和失败反馈的操作技能；与移动底盘协同 |
| 模型训练链路 | [remote_SmolVLA](https://github.com/ianhequn/remote_SmolVLA) 有数据检查、训练和环境脚本 | 模型结果、真机任务效果及与任务层的协作需单独验证 |
| Agent、环境认知、技能编排 | [项目文档](https://github.com/ianhequn/da_chuang_20261112) 已有分层设计、研究问题与验证工作稿 | 统一接口、长期任务运行、地图状态维护及整机闭环尚未由这七个仓库证明 |

**边界：**目前没有证据表明七个仓库可直接组合启动一个完成寻物取回的系统。当前仅确认独立组件和部分链路的验证基础；本仓库负责把后续集成任务和证据持续连起来。
