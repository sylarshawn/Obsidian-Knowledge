---
aliases:
  - TH
  - TH方程
tags:
  - Physics
time: 2026-06-22T18:23:00
---
**摘要**
此文档介绍适用于椭圆参考轨道的线性化模型Tschauner-Hempel方程（TH方程），该模型是[[Clohessy-Wiltshire方程|CW方程]]在任意偏心率开普勒轨道上的推广，当参考轨道偏心率为$0$时会退化为[[Clohessy-Wiltshire方程|CW方程]]。文档主要涵盖了方程的基本假设，推导过程，以及多种表达形式及其关系。


# 概念

Tschauner-Hempel方程简称为TH方程，于1964年由学者Joseph Tschauner和Paul Hempel提出，用于描述目标航天器沿开普勒椭圆轨道运动时，追踪航天器相对于目标航天器的近距离相对运动演化规律。

与[[Clohessy-Wiltshire方程|CW方程]]仅适用于圆形参考轨道不同，TH方程可以覆盖任意偏心率的椭圆参考轨道，是[[Clohessy-Wiltshire方程|CW方程]]的广义形式。其核心应用场景与[[Clohessy-Wiltshire方程|CW方程]]保持一致，但在高轨椭圆轨道，大偏心率探测轨道等[[Clohessy-Wiltshire方程|CW方程]]模型误差显著的任务场景中，TH方程更加精准可靠。

# 前提假设

TH方程与[[Clohessy-Wiltshire方程|CW方程]]同为二体问题下的线性化模型，推导与应用需满足以下假设，特别是轨道约束与[[Clohessy-Wiltshire方程|CW方程]]存在核心差异：

1. 目标航天器轨道约束：目标航天器在中心引力场中做无摄动开普勒椭圆轨道运动，轨道半长轴、偏心率恒定，瞬时轨道半径与瞬时角速度随真近点角动态变化；
2. 