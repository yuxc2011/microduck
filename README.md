https://github.com/search?q=microduck&type=repositories
https://github.com/AI-FanGe/Microduck-build-tutorial.git
https://github.com/fanhao375/microduck-replica
https://github.com/fanhao375/microduck-replica-cad
Microduck 复刻更新 

专门改成适配国产飞特舵机版本，重新修改了腿部、头部干涉零件，解决原版装配卡滞问题。

https://github.com/fanhao375/microduck-replica-cad

https://github.com/fanhao375/microduck-replica

xhs 和dy号： 机械行者 Robo 

开源 solidworks图纸 见上面链接 可下载 。部分可编辑 solidworks2021



# Microduck 机器鸭 —— 资料包

本目录包含 Hugging Face / Pollen Robotics 开源机器鸭 **Microduck** 的 BOM（物料清单）、程序（SDK/固件）与 3D 打印图纸，下载于 2026-09-15。

> 注意：搜索资料中常写作 "miroduck / MicroDuck / microduck"，本项目官方名称为 **Microduck**。

## 目录结构

| 文件夹 | 大小 | 内容 | 来源 |
|---|---|---|---|
| `microduck/` | ~8 MB | **程序（SDK/固件）**：Rust 源码（`duck-control` 控制、`robotd`、`duckctl`、`btd` 蓝牙、`configd` 配置、`kinematics` 运动学、`deploy` 部署脚本等）、文档 | 官方 [pollen-robotics/microduck](https://github.com/pollen-robotics/microduck)（Apache-2.0，分支 main） |
| `microduck_rl/` | ~25 MB | **官方 3D 打印网格 + 仿真/训练**：`src/mjlab_microduck/robot/microduck/assets/` 下 **47 个官方 STL 网格**、MJCF 仿真模型（`robot_walk.xml` 等）、PPO/RL 训练栈 | 官方 [pollen-robotics/microduck_rl](https://github.com/pollen-robotics/microduck_rl)（Apache-2.0，分支 develop） |
| `microduck-replica/` | ~128 MB | **BOM + 复刻图纸（社区）**：`BOM.md` 整机物料清单、`print/打印件/` 打印 STL（45 个）、`cad/` 装配体 STL（16 个）、`assembly-drawings/` 装配图、`hardware/` 电控方案（IMU→舵机板原理图/PCB/接线表）、`docs/` 采购清单与选型文档 | 社区复刻 [fanhao375/microduck-replica](https://github.com/fanhao375/microduck-replica)（分支 master） |

## 入门建议

1. **BOM**：`microduck-replica/BOM.md`（官方从未公布 BOM，此为社区从 MJCF/STL/源码反推的完整清单，含数量、依据与价格量级）
2. **3D 打印**：`microduck_rl/src/mjlab_microduck/robot/microduck/assets/*.stl`（官方原网格）；打印参数参考 `microduck-replica/print/打印件/`（社区整理的分件文件，命名带中文部件名）
3. **程序**：`microduck/README.md` 开始；控制核心在 `microduck/duck-control/`；真机部署看 `microduck/docs/robot/`
4. **装配**：`microduck-replica/assembly-drawings/` + `cad/00_Microduck_整机装配体.stl`

## 许可说明

- 官方软件仓库（microduck、microduck_rl）为 **Apache-2.0**。
- 官方 3D 模型文件（STL/MJCF）为 **CC BY-SA-NC**（可分享、可改、须署名、不可商用）。
- 复刻仓库 `microduck-replica` 自带 `LICENSE`，使用前请阅读其条款。
