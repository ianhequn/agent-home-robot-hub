# 工作区地图

盘点时间：2026-11-23（北京时间）。范围：本机 `D:\大创`。这里记录**目录与仓库的实际关系**，不是新的项目目标或已经完成的整机能力。技术结论以对应源码和实验记录为准；项目定义以 `da_chuang_20261112` 的当前文档为准。

## 1. 顶层目录

```text
D:\大创\
├─ da_chuang_20261112\       项目定义、申报书与调研；独立 Git 仓库
├─ workplace\
│  ├─ ArmPi_Ultra_260913\    机械臂控制、LeRobot 数据流
│  ├─ ChassisNav_01\         早期底盘导航仿真
│  ├─ ChassisNav_02_u22_wsl\ 自建底盘 Gazebo/SLAM/Nav2 仿真
│  ├─ ros2_22_orangpi3b_261101\ 香橙派底盘驱动
│  ├─ remote_SmolVLA\        SmolVLA 训练脚本
│  └─ robot_dev_note_261109\ 环境、安装与调试笔记
├─ agent-home-robot-hub\     七个仓库的公开入口；独立 Git 仓库
└─ .github_migration\        GitHub 同步使用的临时镜像与脚本
```

顶层 `D:\大创` 和 `workplace` **没有共同的 `.git`**；上图共 8 个独立工作树。七个原仓库的本地 `origin` 指向 Codeup；总站的本地 `origin` 指向 GitHub。七个公开 GitHub 仓库是原历史的作者身份改写副本，提交 SHA 与 Codeup 不同。后续跨站同步需要按仓库处理，不能直接把 Codeup 分支推到 GitHub 覆盖。

## 2. 项目文档的阅读路径

`da_chuang_20261112` 的当前主线：

```text
项目说明.md（目标、问题、边界）
  → 研究问题分解.md（六项研究内容）
  → 架构设计.md（层级与接口）
  → 正文思路.md / 正文逻辑链条.md（申报论证）
  → 立项依据.md（正式正文）
```

辅助目录：`search/` 是调研、引用核查及候选技术路线；`ai_note/` 是设计和讨论工作稿；`ai_session_note/` 是会话记录；`old_docs/` 是旧稿；`资料/` 是学校模板与操作指南；`others/` 是团队记录和外部工具资料。**这些目录不等于新的运行模块。**

当前 `立项依据.md` 已包含第（1）至（7）节及参考文献。第（7）节新增底层 MCU 框架、机械臂 SmolVLA 抓取、底盘仿真与真机导航等团队已有基础陈述；这些属于申报材料中的团队陈述，具体实验范围仍应对照相应代码、运行记录和测试结果核查。11 月 20—21 日新增了第（1）至（6）节的全文来源核验记录、参考资料摘录，以及 `资料/` 下的申报书 DOCX。11 月 22 日已修正根目录 `README.md` 的章节进度。`others/SKILLS/` 存放大量外部工具资料，和机器人运行代码分开看。

`others/gdut-dachuang-guide` 与 `others/stardust-agent` 被 Git 记录为 gitlink，但仓库没有 `.gitmodules`，本地目录也没有可读内容。它们目前不能作为可直接复现的依赖入口；需补来源地址或移除失效引用后再引用。

## 3. 六个工程仓库

| 本地目录 / GitHub | 主要入口 | 已有基础 | 尚未由此仓库证明 |
| --- | --- | --- | --- |
| [ArmPi_Ultra_260913](https://github.com/ianhequn/ArmPi_Ultra_260913) | `My_note/README.md`；`src/arm_lerobot_dataset_stream/README.md` | ROS 2 Jazzy 机械臂控制、反馈、TCP/LeRobot 上下行；文档记录真机验证；`src/` 还包含 YDLidar ROS 2 驱动包 | RGB-D 接入、相机与底盘统一时空标定、整机抓取任务 |
| [ChassisNav_01](https://github.com/ianhequn/ChassisNav_01) | `src/chassis_sim/`、`src/chassis_bringup/` | 早期 Gazebo/Nav2 相关仿真实验 | 默认 `master` 与更新的 `main`/实验分支并非同一最新版本；根 README 仍是模板，不能当作可复现说明 |
| [ChassisNav_02_u22_wsl](https://github.com/ianhequn/ChassisNav_02_u22_wsl) | `src/dd_chassis_01_description/launch/`；`src/dd_chassis_001_driver/` | 自建差速底盘、Gazebo、雷达、IMU、SLAM Toolbox、Nav2 配置；11 月 23 日增加 Xacro 拆分、串口和硬件接口相关代码 | 没有根 README；新增代码的运行验证和与真机部署的对应关系仍需记录 |
| [ros2_22_orangpi3b_261101](https://github.com/ianhequn/ros2_22_orangpi3b_261101) | `src/DD_Chassis_001_driver/README.md`；`dev_note/`；`Rui_03` 分支 | ROS 2 Humble/香橙派底盘串口、轮速、IMU 与 ros2_control 实现；新增驱动实验分支 | 该驱动包明确不含激光雷达；与仿真导航及机械臂的整机联调 |
| [remote_SmolVLA](https://github.com/ianhequn/remote_SmolVLA) | `README.md`；`scripts/` | HPC 上的数据检查、训练和冒烟测试脚本，面向单路 RGB 的 ArmPi 数据 | 模型训练脚本不等于真机任务成功率或 Agent 技能接入 |
| [robot_dev_note_261109](https://github.com/ianhequn/robot_dev_note_261109) | `ros2/`；`orangepi3b_u22`、`wsl_24` 分支 | WSL、香橙派与 ROS 2 环境记录；`orangepi3b_u22` 新增虚拟串口服务和 MCU 调试笔记 | 各分支笔记不是统一安装脚本；默认分支没有总览 README |

这些仓库覆盖不同运行环境：机械臂工作区记录 ROS 2 Jazzy，香橙派底盘驱动记录 ROS 2 Humble，另有 Windows/WSL 与 HPC 训练环境。应分别按仓库构建和运行，再用经过验证的消息与服务接口联调。

## 4. 当前工程关系

```mermaid
flowchart LR
    D[项目文档与申报] --> H[总站：状态与接口索引]
    S1[ChassisNav_01<br/>早期仿真] --> S2[ChassisNav_02<br/>自建底盘仿真]
    R[香橙派底盘驱动] --> I[待验证的跨平台接入]
    S2 --> I
    A[ArmPi 控制与数据流] --> I
    M[SmolVLA 训练实验] -. 模型候选 .-> I
    N[环境与调试笔记] -. 支撑 .-> R
    N -. 支撑 .-> A
    H --> I
    I -. 后续 .-> C[环境认知 + Agent + 技能服务 + 寻物取回实验]
```

图中的“待验证”是实际工程缺口：传感器采样和时间基准、坐标/标定、数据新鲜度、仿真与真机接口、技能状态与失败反馈、环境认知、Agent 运行时，以及物理任务结果记录。当前仓库没有证据支持七者已共同完成寻物取回闭环。

## 5. 同步与维护注意点

- 截至本次盘点，项目文档本地、Codeup 与 GitHub 均已包含 **141 个提交**；GitHub 历史因统一作者身份而具有不同 SHA，但各阶段提交仍分别保留。11 月 22 日的 README 修正已同步。
- 11 月 23 日已同步四个工程仓库的远端分支更新：`ChassisNav_01/ros2_control_test_01_demo`、`ChassisNav_02_u22_wsl/master`、`robot_dev_note_261109/orangepi3b_u22`、`ros2_22_orangpi3b_261101/Rui_02_wsl`，并发布新分支 `Rui_03`。其余三个原仓库没有新提交。GitHub 镜像保留各分支和原提交时间，作者身份改写使 SHA 与 Codeup 不同。
- 本轮检查时七个原工作树及总站均无未提交修改；底盘仿真本地 `master` 已快进到 Codeup 最新。分支历史不能仅看当前检出的分支，例如 `ChassisNav_01` 的 `master` 停在 10 月，另有 11 月的 `main` 和实验分支。
- `.github_migration/` 是 GitHub 历史同步所用的本地临时镜像和脚本，不是机器人代码或第三方依赖；本轮临时 SSH 部署密钥已撤销并删除。

## 6. 当前最有回报的下一步

1. **补齐可核查入口：**处理两个缺少来源的 gitlink；为第（7）节新增的真机抓取和导航陈述补对应实验记录链接。
2. **补可运行说明：**先为 `ChassisNav_02_u22_wsl` 和真机底盘写清最小启动、话题、TF、时钟来源及验证命令；`ChassisNav_01` 标注为历史实验。
3. **做一个传感器适配闭环：**选同类仿真/真机输入，记录采样与到达时间、frame、单位、标定版本和新鲜度；先让上层通过同一接口读取，再接 Agent。
4. **逐项接技能和环境认知：**导航、观测搜索、机械臂操作分别提供状态/取消/失败反馈，随后用受控场景验证完整寻物取回。

完成每一步后，把运行命令、设备条件、失败案例与结果链接回本站。未实际测试的部分保留为计划。
