

# microduck学习笔记





![微信群](Readme.jpg)







# 1.模型：



# 2.硬件：



# 3.硬件组装：



# 4.步态训练：

git clone https://github.com/pollen-robotics/microduck_rl
cd microduck_rl



uv run train Mjlab-Velocity-Flat-MicroDuck --env.scene.num-envs 4096 --gpu-ids []

选择3



查看训练效果

uv run play Mjlab-Velocity-Flat-MicroDuck --checkpoint-file logs\rsl_rl\velocity\2026‑09‑24_14‑20‑00_velocity\model_2500.pt --num-envs 1 --viewer native

浏览器可视化

```
uv run play Mjlab-Velocity-Flat-MicroDuck --checkpoint-file 你的model.pt路径 --num-envs 1 --viewer viser
```

<style>
 table { border-collapse: collapse; width: 100%; }
 th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
 </style>

| 按键  | 作用               |
| --- | ---------------- |
| ↑ ↓ | 前进 / 后退          |
| A E | 左转、右转            |
| P   | 施加外力推机器人，测试抗扰动恢复 |
| 空格  | 置零速度指令           |





导出 ONNX

```
uv run scripts/export.py Mjlab-Velocity-Flat-MicroDuck --checkpoint-file logs\rsl_rl\velocity\2026‑09‑24_14‑20‑00_velocity\model_2500.pt
```



再跑一遍键盘控制仿真，进行仿真验证

```
uv run scripts/infer_policy.py --walking output.onnx --new-cmd-obs
```

部署到实体 MicroDuck 机器人

1. 电脑和 MicroDuck 连同一个 WiFi，ssh 登录机器人

```
ssh user@microduck.local
```

2. 电脑端 scp 上传你的`my_walk.onnx`到机器人策略目录

```
# Windows PowerShell执行（本地电脑）
scp my_walk.onnx user@microduck.local:/home/user/policies/
```

### 在真机加载自定义策略

ssh 进机器人终端：

```
# 查看全部可用策略
robotctl policy list

# 加载你上传的模型（去掉后缀.onnx）
robotctl policy load my_walk
```

加载完成，手柄就可以控制鸭子使用你自己训出来的步态走路。

> robotd 会以 50Hz 自动跑 ONNX 推理，读取 IMU、舵机反馈，输出舵机目标位置，不需要再写控制循环代码。

### 常用真机调试命令

```
robotctl status          # 查看robotd运行状态
robotctl drive           # 进入手柄驾驶模式
robotctl policy list     # 列出所有策略
robotctl policy load xxx # 切换策略
```







uv run train Mjlab-Velocity-Flat-MicroDuck --env.scene.num-envs 1024 --gpu-ids 0



# 5.软件调试：





网址备忘



https://github.com/search?q=microduck&type=repositories
https://github.com/AI-FanGe/Microduck-build-tutorial.git
https://github.com/fanhao375/microduck-replica
https://github.com/fanhao375/microduck-replica-cad



ZERO 3W & 3E 操作指南：
https://docs.radxa.com/zero/zero3
ZERO 3W参数介绍：
https://radxa.com/products/zeros/zero3w#techspec
ZERO 3E参数介绍
https://radxa.com/products/zeros/zero3e#techspec
ZERO 3E PoE hat操作指南：
https://docs.radxa.com/zero/zero3/accessories/3e-poe-hat
3W开源资料（规格书/原理图/位号图/3D图/2D图）：
https://radxa.com/products/zeros/zero3w#downloads
3E开源资料（规格书/原理图/位号图/3D图/2D图）：
https://radxa.com/products/zeros/zero3e#downloads
注意：超过 5V的供电会烧坏板子。如使用 Type-℃ 供电，请使用标准 PD 适配器(或 5V)和线材，请勿使用诱导线，请问使用【华为】或【荣耀】的电源。

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

| 文件夹                  | 大小      | 内容                                                                                                                                                                | 来源                                                                                                        |
| -------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `microduck/`         | ~8 MB   | **程序（SDK/固件）**：Rust 源码（`duck-control` 控制、`robotd`、`duckctl`、`btd` 蓝牙、`configd` 配置、`kinematics` 运动学、`deploy` 部署脚本等）、文档                                             | 官方 [pollen-robotics/microduck](https://github.com/pollen-robotics/microduck)（Apache-2.0，分支 main）          |
| `microduck_rl/`      | ~25 MB  | **官方 3D 打印网格 + 仿真/训练**：`src/mjlab_microduck/robot/microduck/assets/` 下 **47 个官方 STL 网格**、MJCF 仿真模型（`robot_walk.xml` 等）、PPO/RL 训练栈                                 | 官方 [pollen-robotics/microduck_rl](https://github.com/pollen-robotics/microduck_rl)（Apache-2.0，分支 develop） |
| `microduck-replica/` | ~128 MB | **BOM + 复刻图纸（社区）**：`BOM.md` 整机物料清单、`print/打印件/` 打印 STL（45 个）、`cad/` 装配体 STL（16 个）、`assembly-drawings/` 装配图、`hardware/` 电控方案（IMU→舵机板原理图/PCB/接线表）、`docs/` 采购清单与选型文档 | 社区复刻 [fanhao375/microduck-replica](https://github.com/fanhao375/microduck-replica)（分支 master）             |

## 入门建议

1. **BOM**：`microduck-replica/BOM.md`（官方从未公布 BOM，此为社区从 MJCF/STL/源码反推的完整清单，含数量、依据与价格量级）
2. **3D 打印**：`microduck_rl/src/mjlab_microduck/robot/microduck/assets/*.stl`（官方原网格）；打印参数参考 `microduck-replica/print/打印件/`（社区整理的分件文件，命名带中文部件名）
3. **程序**：`microduck/README.md` 开始；控制核心在 `microduck/duck-control/`；真机部署看 `microduck/docs/robot/`
4. **装配**：`microduck-replica/assembly-drawings/` + `cad/00_Microduck_整机装配体.stl`

## 许可说明

- 官方软件仓库（microduck、microduck_rl）为 **Apache-2.0**。
- 官方 3D 模型文件（STL/MJCF）为 **CC BY-SA-NC**（可分享、可改、须署名、不可商用）。
- 复刻仓库 `microduck-replica` 自带 `LICENSE`，使用前请阅读其条款。
