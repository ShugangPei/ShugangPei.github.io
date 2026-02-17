---
title: "我的开源项目一览：DPP 软件生态与工具链"
date: 2026-02-02T00:00:00+09:00
draft: false
tags: ["open-source", "dpp", "slicer", "opencv", "tooling"]
categories: ["项目总览"]
---

这篇文章整理我在个人主页上的主要开源项目：它们围绕自研的 DPP（超声振动干粉 3D 打印）设备，目标是构建一套“从切片到执行、从标定到闭环”的软件生态。

> 个人主页：`https://github.com/ShugangPei`

---

## 1. 切片与 G-code 生成

### 1.1 CuraEngine-Yang（DPP 专用切片内核改造）
- 仓库：`https://github.com/kasumi-link/CuraEngine-Yang`
- 方向：在 CuraEngine 的基础上做深度改造，输出适配 DPP 设备的定制 G-code。
- 重点能力（典型）：
  - 支持设备特有的工艺参数（例如起止补偿 LA/LB 等）
  - 更贴近实际运动学（加减速/延迟）的路径与参数输出
  - 为后续“自动补偿/闭环控制”提供统一的数据接口与可追溯输出

---

## 2. 粉道标定与图像测量

### 2.1 Powder_Process（粉道标定 + 尺寸测量 + 自动补偿入口）
- 仓库：`https://github.com/ShugangPei/Powder_Process`
- 方向：通过图像识别/机器学习，对单道铺粉结果进行**标定、检测宽度/长度**，并反向校正切片输出中的补偿参数（例如 LA/LB）。
- 你可以把它理解为：把“经验调参”变成“数据驱动的标定与回写”。

### 2.2 CAMERA（OpenCV 视觉测量与鲁棒性增强方向）
- 仓库：`https://github.com/ShugangPei/CAMERA`
- 方向：围绕粉道图像的视觉算法沉淀工程化实现，比如：
  - 二值化/形态学/骨架化等稳定提取
  - 划痕、光照不均、模糊等干扰处理
  - 输出可量化指标（长度、宽度、偏差），为闭环控制提供反馈量

---

## 3. 上位机控制、监控与可视化

### 3.1 Monitor（上位机控制与状态监控）
- 仓库：`https://github.com/ShugangPei/Monitor`
- 方向：上位机侧的设备控制/监控工具，用于把“切片输出”真正落到“设备执行”，并为工艺验证提供可视化与日志基础。
- 典型功能方向：任务下发、状态监控、参数面板、运行日志、故障定位等。

### 3.2 GCodeViewer3D（桌面端 G-code 3D 可视化）
- 仓库：`https://github.com/ShugangPei/GCodeViewer3D`
- 方向：把 G-code 路径可视化（3D/分层），用于验证切片输出是否符合预期，尤其适合调试定制指令与补偿逻辑。

### 3.3 GGBond（Web 端 G-code 可视化/交互）
- 仓库：`https://github.com/ShugangPei/GGBond`
- 方向：基于 Web 的 G-code 浏览与交互，方便跨平台展示与分享（例如给同学/老师快速演示某段路径或策略）。

---

## 4. 路径策略与工艺探索

### 4.1 laser（路径生成/扫描策略实验仓）
- 仓库：`https://github.com/ShugangPei/laser`
- 方向：用于探索不同扫描/填充策略（例如棋盘格等），把策略从“想法”落到“可生成、可验证、可对比”的实现。

---

## 5. 我接下来会怎么把它们串成“闭环系统”
我的目标不是做很多孤立工具，而是形成一个闭环：

1) **切片生成**：CuraEngine-Yang 输出可追溯的工艺 G-code（包含补偿入口）  
2) **执行与监控**：Monitor 执行任务 + 记录过程数据  
3) **视觉反馈**：Powder_Process / CAMERA 输出量化误差（长度/宽度/偏差）  
4) **自动回写**：把误差映射成 LA/LB 等参数更新，形成迭代标定或在线补偿

当这个闭环打通后，才真正从“手动调参”走向“自动标定 + 数据驱动补偿”。

---

## 结语
如果你对这些项目或 DPP 软件生态感兴趣，欢迎通过主页或邮箱联系我：

- GitHub：`https://github.com/ShugangPei`
- Email：`shugangpei@hrbeu.edu.cn`
