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
2. 近距离相对运动约束：追踪航天器与目标航天器的相对距离远小于目标航天器的瞬时轨道半径，由此可以对非线性引力项作一阶泰勒展开，忽略二阶及以上高阶小量；
3. 无摄动假设：忽略所有摄动影响（如大气阻力、太阳光压、第三体引力、地球非球形引力等），仅考虑中心天体的质点引力作用；
4. 质点假设：将目标航天器与追踪航天器均视为质点，忽略航天器自身姿态运动，结构挠性等对相对运动的影响；
5. 坐标系旋转约束：相对运动参考坐标系[[LVLH-本地垂直-本地水平坐标系|LVLH]]与目标轨道固连，随目标航天器同步沿椭圆轨道运动，坐标系原点始终位于目标航天器质心，无额外姿态旋转；

# 符号约定

为避免符号冲突与概念混淆，本文采用如下符号体系：

| 符号                                      | 物理含义                                                                                                                                                                                                                                     |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $G$                                     | 万有引力常数                                                                                                                                                                                                                                   |
| $M$                                     | 地球质量                                                                                                                                                                                                                                     |
| $\mu$                                   | 地球引力常数，$\mu=GM\approx 3.986004418\times 10^14\mathrm{m^3/s^2}$                                                                                                                                                                           |
| $\boldsymbol{r}_t$                      | 目标航天器相对于地心的位置矢量（[[ECI-地心惯性坐标系]]下），标量模长$r_t=\Vert\boldsymbol{r}_t\Vert$                                                                                                                                                                   |
| $\boldsymbol{r}_c$                      | 追踪航天器相对于地心的位置矢量（[[ECI-地心惯性坐标系]]下），标量模长$r_c=\Vert\boldsymbol{r}_c\Vert$                                                                                                                                                                   |
| $\boldsymbol{\rho}$                     | 追踪航天器相对于目标航天器的相对位置矢量，满足$\boldsymbol{\rho}=\boldsymbol{r}_c-\boldsymbol{r}_t$，标量模长$\rho=\Vert \boldsymbol{\rho} \Vert$                                                                                                                    |
| $e$                                     | 目标航天器轨道偏心率，$0 \leq e < 1$                                                                                                                                                                                                                |
| $a$                                     | 目标航天器轨道半长轴                                                                                                                                                                                                                               |
| $p$                                     | 目标航天器轨道半通径，$p = a\,(1-e^2)$                                                                                                                                                                                                              |
| $h$                                     | 目标航天器轨道角动量大小，$h=\sqrt{\mu\,p}$，二体轨道下[[角动量#角动量守恒定律\|角动量守恒]]                                                                                                                                                                               |
| $\theta,\,\dot{\theta},\,\ddot{\theta}$ | 目标航天器的[[轨道根数-轨道六要素#真近点角$ theta$或$f$(True Anomaly)\|真近点角]]大小；轨道瞬时角速度大小，即[[LVLH-本地垂直-本地水平坐标系\|LVLH]]系相对于[[ECI-地心惯性坐标系\|惯性系]]的角速度大小，$\dot{\theta} = h/r_\mathrm{t}^2$；轨道瞬时角加速度大小，$\ddot{\theta} = -2\,\mu\,e\,\sin \theta / r_\mathrm{t}^3$ |
| $\boldsymbol{\omega}$                   | [[LVLH-本地垂直-本地水平坐标系]]相对于[[ECI-地心惯性坐标系]]的角速度矢量，[[LVLH-本地垂直-本地水平坐标系\|LVLH]]系下的分量为$\boldsymbol{w} = [0,\,0,\,\dot{\theta}]^\mathrm{T}$                                                                                                      |

同时，采用$\mathrm{d}\,/\mathrm{d}\,t|_\boldsymbol{I},\,\mathrm{d}\,/\mathrm{d}\,t|_\boldsymbol{B}$分别表示[[ECI-地心惯性坐标系]]下的绝对时间导数算子和[[LVLH-本地垂直-本地水平坐标系]]下的相对时间导数算子。

# TH方程推导

TH方程的推导过程与[[Clohessy-Wiltshire方程|CW方程]]基本一致，但由于TH方程面向椭圆轨道，瞬时轨道半径、角速度、角加速度均随真近点角发生变化，且角加速度牵连项不可忽略。TH方程的推导过程主要分为以下几个步骤：首先，构建[[二体问题|二体]]绝对运动方程；其次，通过[[旋转矢量微分法则]]完成加速度坐标系转换；而后，基于近距离假设线性化引力差项；最后，整理得到时间域与真近点角域的方程形式。

在[[ECI-地心惯性坐标系]]下，[[二体问题]]的航天器无摄动运动满足二体动力学方程，矢量形式为：

$$
\frac{\mathrm{d}^2\,\boldsymbol{r}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}} = -\frac{\mu}{r^3}\boldsymbol{r}
\tag{1-1}
$$

其中，$\mu=G(M+m)\approx GM\in\mathbb{R}$，$\boldsymbol{r}\in\mathbb{R}^3$是惯性坐标系下航天器相对于地心的位置矢量，$r\in\mathbb{R}$为其对应的标量距离。

目标与追踪航天器的绝对运动均满足Eq. (1)，因而有：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{t}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=-\frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{t},\,\,\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{c}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=-\frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{c}
\end{aligned}
\tag{1-2}
$$

定义相对位置矢量$\boldsymbol{\rho} = \boldsymbol{r}_\mathrm{c} - \boldsymbol{r}_\mathrm{t}$，对其在[[ECI-地心惯性坐标系]]下求二阶导数，则[[ECI-地心惯性坐标系|惯性系]]下的相对加速度可以表示为：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=
	\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{c}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{t}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}} = \frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{t} - \frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{c}
\end{aligned}
\tag{1-3}
$$

Eq. (1-3)等式右侧即为两航天器的引力速度差，即引力差项。

对于原点随目标平动，同步旋转的[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系，相对位置矢量的二阶导数满足带平动的[[旋转矢量微分法则#带平动的任意运动坐标系的二阶通用形式|旋转矢量二阶微分通用公式]]：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}=
\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{c}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\frac{\mathrm{d}^2\,\boldsymbol{r}_\mathrm{t}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\boldsymbol{\dot{\omega}}\times \boldsymbol{\rho}-2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}-\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})
\tag{1-4}
$$

*注：不同于[[Clohessy-Wiltshire方程|CW方程]]，椭圆轨道下轨道角速度随真近点角变化，因此角加速度$\boldsymbol{\dot{\omega}}\neq 0$，即Eq. (1-4)中的角加速度牵连项$\boldsymbol{\dot{\omega}}\times\boldsymbol{\rho}$无法消除。*

将Eq. (1-3)代入Eq. (1-4)中得：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}} + \boldsymbol{\dot{\omega}}\times \boldsymbol{\rho} + 2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B} + \boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) = \frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{t} - \frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{c}
\tag{1-5}
$$

其余部分与[[Clohessy-Wiltshire方程|CW方程]]的线性化方法基本一致，基于$\boldsymbol{r}_\mathrm{c} = \boldsymbol{r}_\mathrm{t} + \boldsymbol{\rho}$且近距离假设中$\rho\ll r_\mathrm{t}$，结合[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系的基本定义，$\boldsymbol{r}_\mathrm{t}$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的分量为$\boldsymbol{r}_\mathrm{t} = [r_\mathrm{t},\,0,\,0]$，$\boldsymbol{\rho} = [x,\,y,\,z]^\mathrm{T}$，因此有：

$$
r_\mathrm{c}^2=r_\mathrm{t}^2+2r_\mathrm{t}\,x+\rho^2
\tag{1-5}
$$

忽略二阶小量$\rho^2$，对$1/r_\mathrm{c}^3$作一阶泰勒展开：

$$
\begin{aligned}
	r_\mathrm{c}^{-3} &= (r_\mathrm{t} + 2\,r_\mathrm{t}\,x)^{-3/2}\\
	&= r_\mathrm{t}^{-3}\,(1 + \frac{2\,x}{r_\mathrm{t}})^{-3/2}\\
	&\approx  r_\mathrm{t}^{-3}\,(1 - \frac{3\,x}{ r_\mathrm{t}^3\,})
\end{aligned}
\tag{1-6}
$$

结合椭圆轨道瞬时角速度关系$n^2 = \mu/r_\mathrm{t}^3$，其中，$n$是目标航天器瞬时角速度的大小，仅用于形式处理，Eq. (1-6)可以改写为：

$$
\frac{\mu}{r_\mathrm{c}^{3}} \approx \frac{\mu}{r_\mathrm{t}^{3}}\,(1-\frac{3\,x}{r_\mathrm{t}})
\tag{1-7}
$$

将Eq. (1-7)与$\boldsymbol{r}_\mathrm{c} = [r_\mathrm{t}+x,\,y,\,z]^\mathrm{T}$代入引力差项中，展开并忽略所有二阶小量得：

$$
\begin{aligned}
	&\quad\frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{t} - \frac{\mu}{r_t^3}\boldsymbol{r}_\mathrm{c} \\
	&\approx \frac{\mu}{r_\mathrm{t}^3}\,\begin{bmatrix} r_\mathrm{t}\\0\\0 \end{bmatrix} - \frac{\mu}{r_\mathrm{t}^3}\,(1-\frac{3\,x}{r_\mathrm{t}})\,\begin{bmatrix} r_\mathrm{t} + x\\y\\z \end{bmatrix}\\
	&\approx \frac{\mu}{r_\mathrm{t}^3}\,\begin{bmatrix} r_\mathrm{t} - (r_\mathrm{t}+x-3\,x)\\-y\\-z \end{bmatrix}\\
	&\approx \frac{\mu}{r_\mathrm{t}^3}\,\begin{bmatrix} 2\,x\\-y\\-z \end{bmatrix}
\end{aligned}
\tag{1-8}
$$

将角速度$\boldsymbol{\omega}$，角加速度$\boldsymbol{\dot{\omega}}$，相对速度$\mathrm{d}\,\boldsymbol{\rho}/\mathrm{d}\,t|_\boldsymbol{B}$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下分别展开：

$$
\boldsymbol{\omega} = \begin{bmatrix} 0\\0\\ \dot{\theta} \end{bmatrix},\,\,\boldsymbol{\dot{\omega}} = \begin{bmatrix} 0\\0\\ \ddot{\theta} \end{bmatrix},\,\,\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_{\boldsymbol{B}} = \begin{bmatrix} \dot{x}\\\dot{y}\\ \ddot{z} \end{bmatrix}
\tag{1-9}
$$

逐项计算科氏加速度项，向心牵连加速度项，角加速度牵连项的形式得：

$$
\begin{aligned}
	2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B} &= \begin{bmatrix} -2\,\dot{\theta}\,\dot{y}\\2\,\dot{\theta}\,\dot{x}\\0 \end{bmatrix},\\
	\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) &= \begin{bmatrix} -\dot{\theta}^2\,x\\ \,-\dot{\theta}^2\,y\\0 \end{bmatrix},\\
	\boldsymbol{\dot{\omega}}\times\boldsymbol{\rho}&=\begin{bmatrix} -\ddot{\theta}\,y\\ \ddot{\theta}\,x\\0 \end{bmatrix}.\\
\end{aligned}
\tag{1-10}
$$

## 时间域标量TH方程

将Eq. (1-8)中的线性化引力差项与Eq. (1-10)中的各牵连项结合，按三轴分别整理，得到时间域下的齐次TH方程标量形式，亦即线性近似方程：

$$

\tag{2}
$$