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
\left\{\begin{aligned}
	\ddot{x} - 2\,\dot{\theta}\,\dot{y} - \ddot{\theta}\,y - (\dot{\theta}^2 + \frac{2\,\mu}{r_\mathrm{t}^3})\,x &= 0\\
	\ddot{y} + 2\,\dot{\theta}\,\dot{x} + \ddot{\theta}\,x - (\dot{\theta}^2 - \frac{\mu}{r_\mathrm{t}^3}\,y) &= 0\\
	\ddot{z} + \frac{\mu}{r_\mathrm{r}^3}\,z &= 0
\end{aligned}\right.
\tag{2}
$$

*注：当轨道为圆轨道时，偏心率$e=0$，$r_\mathrm{t}$为常数，此时角速度值$\dot{\theta} = n = \sqrt{u/r_\mathrm{t}^3}$，角加速度值$\ddot{\theta} = 0$，代入Eq. (2)中可以直接得到[[Clohessy-Wiltshire方程|CW方程]]的在[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的标量形式。*

## 其他方程形式

由于椭圆轨道下角速度$\dot{\theta}$与$r_\mathrm{t}$均随时间变化，时间域的[[Tschauner-Hempel方程#时间域标量TH方程|TH方程]]实际为线性时变系统，直接以时间为自变量难以获得简洁的解析解形式。因此一般需要将自变量从时间$t$调整为真近点角$\theta$，而后利用[[角动量#角动量守恒定律|角动量守恒]]关系完成导数算子的转换，可以得到真近点角域方程。

*注：绝大多数工程应用论文中大多采用时间域形式呈现[[Tschauner-Hempel方程#时间域标量TH方程|TH方程]]，且一般进行瞬时冻结近似，即假定真近点角在一段时间内为恒定常值。这主要是因为航天任务如交会对接、近距离绕飞等任务持续时间通常远小于轨道周期（几十分钟到几小时，低轨轨道周期约$90$分钟），短时间内得真近点角$\theta$，轨道半径$r_\mathrm{t}$以及角速度大小$\dot{\theta}$的变化幅度可以忽略不计。*

此处不对真近点角域的方程形式进行推导和整理，该形式很少出现在工程实现环节，但确实是整个TH方程理论体系的基础。真近点角域方程提供了对时间域[[Tschauner-Hempel方程|TH方程]]的解析分析方法，避免了纯数值积分求解的误差。

## TH方程矢量形式

TH方程矢量形式的推导过程与[[Clohessy-Wiltshire方程|CW方程]]中[[Clohessy-Wiltshire方程#矢量形式|矢量形式]]的分析基本一致。

根据Eq. (1-5)，引力差项矢量表示为：

$$
\Delta\boldsymbol{g} = \frac{\mu}{r_\mathrm{c}^3}\boldsymbol{r}_\mathrm{c} - \frac{\mu}{r_\mathrm{t}^3}\boldsymbol{r}_\mathrm{t}
\tag{3-1}
$$

因此，Eq. (1-5)可以进一步写作：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}} + \boldsymbol{\dot{\omega}}\times \boldsymbol{\rho} + 2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B} + \boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) = -\Delta\boldsymbol{g}
\tag{3-2}
$$

显然，Eq. (1-8)基本等价于引力差项的实际值，即

$$
\Delta\boldsymbol{g} \approx \frac{\mu}{r_\mathrm{t}^3}\,\begin{bmatrix} 2\,x\\-y\\-z \end{bmatrix}
\tag{3-3}
$$

进而，可以将Eq. (3-3)中的三份量结果拆解为不依赖坐标系的通用矢量表达式形式。考虑[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的相对位置矢量$\boldsymbol{\rho}$的实际形式为：

$$
\frac{\mu}{r_\mathrm{t}^3}\,\boldsymbol{\rho} = \frac{\mu}{r_\mathrm{t}^3}\,\begin{bmatrix} x\\y\\z \end{bmatrix} = \begin{bmatrix} \mu\,x/r_\mathrm{t}^3\\ \mu\,y/r_\mathrm{t}^3\\ \mu\,z/r_\mathrm{t}^3 \end{bmatrix}
\tag{3-4}
$$

同时，径向分量的矢量可以表示为$\boldsymbol{\rho}\,\boldsymbol{\hat{x}} = x$，其中，$\boldsymbol{\hat{x}}$是[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系$x$轴的单位矢量。进而有：

$$
\frac{3\,\mu}{r_\mathrm{t}^3}\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\,\boldsymbol{\hat{x}} = \begin{bmatrix} 3\,\mu\,x/r_\mathrm{t}^3\\ 0\\ 0 \end{bmatrix}
\tag{3-5}
$$

根据Eqs. (3-3), (3-4), (3-5)的分量结构，可以将Eq. (3-3)重新表示为：

$$
\frac{\mu}{r_\mathrm{t}^3}\,\boldsymbol{\rho} = \begin{bmatrix} 2\,\mu\,x/r_\mathrm{t}^3\\ -\mu\,y/r_\mathrm{t}^3\\ -\mu\,z/r_\mathrm{t}^3 \end{bmatrix} = \begin{bmatrix} \mu\,x/r_\mathrm{t}^3\\ \mu\,y/r_\mathrm{t}^3\\ \mu\,z/r_\mathrm{t}^3 \end{bmatrix} - \begin{bmatrix} 3\,\mu\,x/r_\mathrm{t}^3\\ 0\\ 0 \end{bmatrix}
\tag{3-6}
$$

整理得：

$$
\Delta\boldsymbol{g} \approx \frac{\mu}{r_\mathrm{t}^3}\,\boldsymbol{\rho} - \frac{3\,\mu}{r_\mathrm{t}^3}\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\,\boldsymbol{\hat{x}}
\tag{3-7}
$$

*注：Eq. (3-7)的实际物理意义为，近距离下的引力差项，可以分解为与相对位置成正比的梯度项，加上沿径向修正的潮汐项。*

将Eq. (3-7)代入Eq. (3-2)中，整理得**TH方程的通用矢量形式**：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}} + \boldsymbol{\dot{\omega}}\times \boldsymbol{\rho} + 2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B} + \boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) + \frac{\mu}{r_\mathrm{t}^3}\,\boldsymbol{\rho} - \frac{3\,\mu}{r_\mathrm{t}^3}\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\,\boldsymbol{\hat{x}} = \boldsymbol{0}
\tag{3-8}
$$

同时，可以基于矢量式Eq. (3-8)验证TH方程与[[Clohessy-Wiltshire方程#矢量形式|CW方程矢量形式]]的关系。当参考轨道退化为圆轨道时，轨道半径$r_\mathrm{t}$为常数，瞬时角速度$\boldsymbol{\omega} = [0,\,0,\,n]^\mathrm{T}$，且圆轨道下角速度恒定，角加速度$\boldsymbol{\dot{\omega}} = \boldsymbol{0}$，因此$\boldsymbol{\dot{\omega}}\times \boldsymbol{\rho}=\boldsymbol{0}$，根据上述分析，Eq. (3-8)可以写作：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}+2\,\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}+\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) + n^2\,\boldsymbol{\rho} - 3\,n^2\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\,\boldsymbol{\hat{x}} = \boldsymbol{0}
\end{aligned}
\tag{3-9}
$$

即[[Clohessy-Wiltshire方程|CW方程]]的[[Clohessy-Wiltshire方程#矢量形式|矢量形式]]。

# TH状态空间方程

为便于系统规划和控制，可以将TH方程写作一阶线性状态空间方程的形式。定义相对运动状态矢量为：

$$
\boldsymbol{X} = [x,y,z,\dot{x},\dot{y},\dot{z}]^\mathrm{T}
\tag{4-1}
$$

则时间域下带控制输入的状态空间方程形式为：

$$
\boldsymbol{\dot{X}} = \boldsymbol{A}\,\boldsymbol{X}+\boldsymbol{B}\,\boldsymbol{u}
\tag{4-2}
$$
其中，控制输入$\boldsymbol{u} = [u_x\,u_y,\,u_z]^\mathrm{T}$为[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的控制加速度，控制输入矩阵$\boldsymbol{B}$与[[Clohessy-Wiltshire方程#CW状态空间方程|CW状态空间方程]]完全一致，即：

$$
\boldsymbol{B} = \begin{bmatrix} 0& 0& 0\\ 0& 0& 0\\ 0& 0& 0\\ 1& 0& 0\\ 0& 1& 0\\ 0& 0& 1\end{bmatrix}
$$

时变状态矩阵$\boldsymbol{A}(t)$为：

$$
\boldsymbol{A}(t)=\begin{bmatrix}
0 &0 &0 &1 &0 &0\\
0 &0 &0 &0 &1 &0\\
0 &0 &0 &0 &0 &1\\
\dot{\theta}^2 + 2\,\mu/r_\mathrm{t}^3 &\ddot{\theta} &0 &0 &2\,\dot{\theta} &0\\
-\ddot{\theta} &\dot{\theta}^2 - \mu/r_\mathrm{t}^3 &0 &-2\,\dot{\theta} &0 &0\\
0 &0 &-\mu/r_\mathrm{t}^3 &0 &0 &0
\end{bmatrix}
$$

显然，当偏心率的值$e=0$时，轨道角速度值$\dot{\theta} = n$，角加速度值$\ddot{\theta} = 0$，该矩阵退化为[[Clohessy-Wiltshire方程|CW方程]]的常值状态矩阵。

[[Tschauner-Hempel方程|TH方程]]为线性时变系统，其状态转移矩阵无法像[[Clohessy-Wiltshire方程|CW方程]]一样通过常值矩阵指数直接求解，但如前文所述，以真近点角为自变量时，可以获得解析形式的状态转移矩阵。目前广泛采用2002年提出的Yamanaka-Ankersen状态转移矩阵，该形式简洁且数值稳定性较好，适用于任意偏心率的椭圆轨道。Y-A形式的离散化为精确的离散处理，但需要复杂的时间域与真近点角域转换，很少应用到工程中，因此本文当前只给出冻结系数情况下的零阶保持离散近似。


## TH方程离散

记第$k$个采样时刻为$t_k$，采样区间为$[t_k,\,t_{k+1}]$，采样周期为$T=t_{k+1}-t_k$，在该区间内，将时变状态矩阵冻结为第$k$个时刻的常值矩阵：

$$
\boldsymbol{A}(t) \approx \boldsymbol{A}_k = \boldsymbol{A}(t_k),\,\,t\in[t_k,\,t_{k+1}]
$$

此时区间内的系统被近似为线性时不变系统，可以直接套用[[Clohessy-Wiltshire方程|CW方程]]中系统的零阶保持离散化方法。

假定冻结后，$t_k$时刻的轨道瞬时参数分别为，瞬时轨道半径$r_{\mathrm{t},\,k} = r_{\mathrm{t}}(t_k)$，瞬时角速度$\dot{\theta}_k = \dot{\theta}(t_k)$，瞬时角加速度$\ddot{\theta}_k = \ddot{\theta}(t_k)$，则其常值状态矩阵$\boldsymbol{A}_k$为：

$$
\boldsymbol{A}(t)=\begin{bmatrix}
0 &0 &0 &1 &0 &0\\
0 &0 &0 &0 &1 &0\\
0 &0 &0 &0 &0 &1\\
\dot{\theta}_k^2 + 2\,\mu/r_{\mathrm{t},\,k}^3 &\ddot{\theta}_k &0 &0 &2\,\dot{\theta}_k &0\\
-\ddot{\theta}_k &\dot{\theta}_k^2 - \mu/r_{\mathrm{t},\,k}^3 &0 &-2\,\dot{\theta}_k &0 &0\\
0 &0 &-\mu/r_{\mathrm{t},\,k}^3 &0 &0 &0
\end{bmatrix}
$$

显然，该形式与[[Clohessy-Wiltshire方程|CW方程]]的离散分析过程一致，此处不再赘述。在$t_k$时刻，TH方程的离散形式可以整理为：

$$
\boldsymbol{X}_{k+1} = \boldsymbol{\Phi}\,\boldsymbol{X}_k+\boldsymbol{\Gamma}\,\boldsymbol{u}_k
\tag{5-1}
$$
其中，$\boldsymbol{\Phi}_k$为离散状态转移矩阵，$\boldsymbol{\Gamma}_k$为离散控制输入矩阵，且$\boldsymbol{X}_{k+1} =\boldsymbol{X}(t_k)$。

### 离散状态转移矩阵

离散形式的TH方程状态转移矩阵在冻结假设下，也可以表示为矩阵指数函数形式：

$$
\boldsymbol{\Phi}_k = e^{\boldsymbol{A}_k\,t_k}
\tag{5-2}
$$

由于冻结后的$\boldsymbol{A}_k$一般为$6$阶常值矩阵，不存在像[[Clohessy-Wiltshire方程|CW方程]]类似的三角函数解析表达式，工程上通常通过矩阵指数的级数展开或数值积分等方式进行解算。

### 离散控制输入矩阵

与[[Clohessy-Wiltshire方程|CW方程]]的离散控制输入矩阵积分式类似，即：

$$
\boldsymbol{\Gamma}_k = \int_0^T e^{\boldsymbol{A}_k\,s}\,\boldsymbol{B}\,\mathrm{d}\,s
\tag{5-3}
$$

结合矩阵指数的积分性质，当状态转移矩阵$\boldsymbol{A}_k$可逆时，对矩阵指数求导有：

$$
\frac{\mathrm{d}\,}{\mathrm{d}\,s}\,e^{\boldsymbol{A}_k\,s} = \boldsymbol{A}_k\,e^{\boldsymbol{A}_k\,s}
\tag{5-4}
$$

因而积分Eq. (5-3)可以闭合为：

$$
\boldsymbol{\Gamma}_k = \int_0^T e^{\boldsymbol{A}_k\,s}\,\boldsymbol{B}\,\mathrm{d}\,s = \boldsymbol{A}_k^{-1}\,(e^{\boldsymbol{A}_k\,T}-\boldsymbol{I})\,\boldsymbol{B}
\tag{5-5}
$$

同时，控制输入矩阵$\boldsymbol{B}$的前三行为$0$，后三行为单位矩阵，因此式Eq. (5-5)中的$\boldsymbol{\Gamma}_k$的前三行与$\int_0^T e^{\boldsymbol{A}_k\,s}\mathrm{d}\,s$一致，后三行与$\int_0^T e^{\boldsymbol{A}_k\,s}\mathrm{d}\,s$的后三行一致。

需要注意的时，工程中一般不直接使用Eq. (5-5)进行控制输入矩阵的计算，因为当状态矩阵$\boldsymbol{A}_k$接近奇异或条件数很大时，求逆会引入显著的数值误差。通用的处理方式是采用增广矩阵法，通过一次矩阵指数运算同时得到状态转移矩阵$\boldsymbol{\Phi}_k$和控制输入矩阵$\boldsymbol{\Gamma}_k$。

首先，构造$9\times 9$增广矩阵为：

$$
\boldsymbol{M}_k = \begin{bmatrix} \boldsymbol{A}_k &\boldsymbol{B}\\
\boldsymbol{0}_{3\times 6} & \boldsymbol{0}_{3\times 3}
\end{bmatrix}
\tag{5-6}
$$

对Eq. (5-6)作矩阵指数运算并乘以采样周期得：

$$
\begin{aligned}
	\exp(\boldsymbol{M}\,T) &= \begin{bmatrix} e^{\boldsymbol{A}_k\,T} & \int_0^T e^{\boldsymbol{A}_k\,s}\,\boldsymbol{B}\,\mathrm{d}\,s \\
	\boldsymbol{0}_{3\times 6} & \boldsymbol{I}_{3\times 3}
	\end{bmatrix}\\
	&= \begin{bmatrix} \boldsymbol{\Phi}_k & \boldsymbol{\Gamma}_k\\
	\boldsymbol{0}{3\times 6} & \boldsymbol{I}_{3\times 3} \end{bmatrix}
\end{aligned}
\tag{5-7}
$$

一次矩阵指数处理后，左上角$6\times 6$子块为状态转移矩阵$\boldsymbol{\Phi}_k$，右上角$6\times 3$子块为控制输入矩阵$\boldsymbol{\Gamma}_k$，不涉及矩阵求逆，数值稳定性好。

关于上述增广矩阵法的详细推导过程可以参考[[Tschauner-Hempel方程#附1 增广矩阵法求解TH方程状态转移矩阵与控制输入矩阵|增广矩阵法求解TH方程状态转移矩阵与控制输入矩阵]]。

# 附录

## 附1 增广矩阵法求解TH方程状态转移矩阵与控制输入矩阵

增广矩阵法求解TH方程的状态转移矩阵$\boldsymbol{\Phi}_k$和控制输入矩阵$\boldsymbol{\Gamma}_k$的核心思想是，将控制输入$\boldsymbol{u}(t)$扩展为增广状态的一部分，利用零阶保持（ZOH）假设下“控制量导数为$0$”的特性，将原本带输入的非齐次系统，转化为一个更高维度的其次线性系统。此时增广系统的状态转移矩阵天然包含了原系统的状态转移与控制积分效应，只需一次矩阵指数运算即可得到两个矩阵的值。

定义增广状态矢量，将控制量并入状态：

$$
\boldsymbol{X}_\mathrm{a}(t) = \begin{bmatrix} \boldsymbol{X}(t)\\ \boldsymbol{u}(t) \end{bmatrix} \in \mathbb{R}^{n+m}
\tag{app-1}
$$

根据ZOH假设，一个周期内控制量恒定，因此控制量的时间导数为$0$，即$\boldsymbol{\dot{u}}(t) = 0$。结合原系统的状态空间方程Eq. (4-2)，可以得到增广系统的齐次状态方程：

$$
\left\{\begin{aligned}
	\boldsymbol{\dot{X}} &= \boldsymbol{A}\,\boldsymbol{X}+\boldsymbol{B}\,\boldsymbol{u}\\
	\boldsymbol{\dot{u}} &= \boldsymbol{0}_{m\times 1}
\end{aligned}\right.
\tag{app-2}
$$

方程Eq. (app-2)可以写为更紧凑的矩阵形式，即：

$$
\begin{bmatrix} \boldsymbol{\dot{X}}\\ \boldsymbol{\dot{u}} \end{bmatrix} = \boldsymbol{\dot{X}}_\mathrm{a} = 
\underbrace{\begin{bmatrix} \boldsymbol{A} & \boldsymbol{B} \\ \boldsymbol{0} & \boldsymbol{0} \end{bmatrix}}_{\boldsymbol{M}_\mathrm{a}}
\underbrace{\begin{bmatrix} 
\boldsymbol{X} \\ \boldsymbol{u} \end{bmatrix}}_{\boldsymbol{X}_\mathrm{a}}
\tag{app-3}
$$
其中，$\boldsymbol{M}_\mathrm{a}\in\mathbb{R}^{(n+m)\times(n+m)}$称为增广状态矩阵，是一个典型分块下三角结构的常值矩阵。显然，经过上述变换，原带控制输入的系统被转化为了一个无外部输入的齐次增广系统。

结合[[Clohessy-Wiltshire方程#附1 关于<u>线性时不变（LTI）系统的状态转移矩阵是矩阵指数函数</u>的证明|线性时不变（LTI）系统的状态转移矩阵是矩阵指数函数]]的分析，上述齐次LTI系统的状态演化过程可以由矩阵指数严格描述：

$$
\boldsymbol{X}_\mathrm{a} = e^{\boldsymbol{M}_\mathrm{a}\,T}\,\boldsymbol{X}_\mathrm{a}(0)
\tag{app-4}
$$

代入初始时刻与终端时刻的增广状态，并展开为分块形式得：

$$
\begin{bmatrix} \boldsymbol{X}\\ \boldsymbol{u} \end{bmatrix} = e^{\boldsymbol{M}_\mathrm{a} T} \begin{bmatrix} \boldsymbol{X}(0) \\ \boldsymbol{u}(0) \end{bmatrix}
\tag{app-5}
$$

对Eq. (app-5)中的增广矩阵的指数按相同维度进行分块处理，假设：

$$
e^{\boldsymbol{M}_\mathrm{a} T} = \begin{bmatrix} \boldsymbol{M}_{11}& \boldsymbol{M}_{12}\\ \boldsymbol{M}_{21}& \boldsymbol{M}_{22} \end{bmatrix}
\tag{app-6}
$$
其中，$\boldsymbol{M}_{11}\in\mathbb{R}^{n\times n}$，$\boldsymbol{M}_{11}\in\mathbb{R}^{n\times m}$，$\boldsymbol{M}_{11}\in\mathbb{R}^{m\times n}$，$\boldsymbol{M}_{11}\in\mathbb{R}^{m\times m}$。

以下可以通过矩阵指数的幂级数定义，分析四个分块所对应的物理意义。

对任意的方阵$\boldsymbol{M}$，矩阵指数的定义为绝对收敛的幂级数：

$$
e^{\boldsymbol{M}\, T} = \sum_{k=0}^{\infty}\,\frac{(\boldsymbol{M}\,T)^k}{k!} = \boldsymbol{I} + \boldsymbol{M}\,T + \frac{(\boldsymbol{M}\,T)^2}{2!} + \frac{(\boldsymbol{M}\,T)^3}{3!} + \dots
$$

进一步地，考虑采用数学归纳法，对增广矩阵$\boldsymbol{M}_\mathrm{a}\,T$的低次幂进行计算，并寻找分块规律：

$$
\begin{aligned}
	(\boldsymbol{M}_\mathrm{a}\,T)^0 &= \boldsymbol{I}_{n+m} = \begin{bmatrix} \boldsymbol{I}_n& \boldsymbol{0}_{n\times m}\\ \boldsymbol{0}_{m\times n}& \boldsymbol{I}_m \end{bmatrix}\\
	(\boldsymbol{M}_\mathrm{a}\,T)^1 &= \begin{bmatrix} \boldsymbol{A}\,T& \boldsymbol{B}\,T\\ \boldsymbol{0}& \boldsymbol{0} \end{bmatrix}\\
	(\boldsymbol{M}_\mathrm{a}\,T)^2 &= \begin{bmatrix} \boldsymbol{A}\,T& \boldsymbol{B}\,T\\ \boldsymbol{0}& \boldsymbol{0} \end{bmatrix}\,\begin{bmatrix} \boldsymbol{A}\,T& \boldsymbol{B}\,T\\ \boldsymbol{0}& \boldsymbol{0} \end{bmatrix} = \begin{bmatrix} (\boldsymbol{A}\,T)^2& \boldsymbol{A}\,T\,\boldsymbol{B}\,T\\ \boldsymbol{0}& \boldsymbol{0} \end{bmatrix}\\
	(\boldsymbol{M}_\mathrm{a}\,T)^3 &= \begin{bmatrix} (\boldsymbol{A}\,T)^3& (\boldsymbol{A}\,T)^2\,\boldsymbol{B}\,T\\ \boldsymbol{0}& \boldsymbol{0} \end{bmatrix}
\end{aligned}
\tag{app-7}
$$

通过归纳分析，可以证明，对于任意整数$k\geq 1$，增广矩阵的$k$次幂满足统一形式：

$$
(\boldsymbol{M}_\mathrm{a}\,T)^k = \begin{bmatrix} (\boldsymbol{A}\,T)^k& (\boldsymbol{A}\,T)^{k-1}\,\boldsymbol{B}\,T\\ \boldsymbol{0}_{m\times n}& \boldsymbol{0}_{m\times m} \end{bmatrix}
\tag{app-8}
$$

将上述幂次结果代入矩阵指数的幂级数展开式，按照四个分块结构分别求和。其一，所有$k$次幂的左下角均为$\boldsymbol{0}$矩阵，因此求和后仍为零矩阵，即：

$$
\boldsymbol{M}_{21} = \boldsymbol{0}_{m\times n}
$$

其二，右下角分块仅在$k=0$时有单位矩阵项，所有$k\geq 1$次幂的右下角矩阵均为零矩阵，因此有：

$$
\boldsymbol{M}_{22} = \boldsymbol{I}_m
$$

其三，左上角分块求和如下：

$$
\boldsymbol{M}_{11} = \boldsymbol{I}_{n} + \sum_{k=1}^{\infty}\frac{(\boldsymbol{A}\,T)^k}{k!} = \sum_{k=0}^{\infty}\frac{(\boldsymbol{A}\,T)^k}{k!} = e^{\boldsymbol{A}\,T} = \boldsymbol{\Phi}
\tag{app-9}
$$
即恰好为原系统的离散状态转移矩阵。

其四，右上角分块求和如下：

$$
\boldsymbol{M}_{12} = \sum_{k=1}^{\infty}\,\frac{1}{k!}\,(\boldsymbol{A}\,T)^{k-1}\,\boldsymbol{B}\,T
$$

令$j=k-1$，则$k=j+1$，求和下限从$k=1$变为$j=0$，即：

$$
\boldsymbol{M}_{12} = \sum_{j = 0}^{\infty}\,\frac{T^{j+1}}{(j+1)!}\,\boldsymbol{A}^j\,\boldsymbol{B} = \left( \sum_{j=0}^{\infty}\,\frac{\boldsymbol{A}^j\,T^{j+1}}{(j+1)!} \right)\,\boldsymbol{B}
$$

注意到级数项与积分的等价关系：

$$
\int_{0}^T\frac{(\boldsymbol{A}\,s)^j}{j!}\,\mathrm{d}\,s = \frac{\boldsymbol{A}^j}{j!}\,\int_{0}^T s^j\,\mathrm{d}\,s = \frac{\boldsymbol{A}^j\,T^{j+1}}{j!\,(j+1)} = \frac{\boldsymbol{A}^j\,T^{j+1}}{(j+1)!}
$$

因此级数求和等价于积分：

$$
\sum_{j=0}^\infty \frac{\boldsymbol{A}^j\,T^{j+1}}{(j+1)!} = \int_{0}^T \sum_{j=0}^{\infty}\frac{(\boldsymbol{A}\,s)^j}{j!}\,\mathrm{d}\,s = \int_0^T e^{\boldsymbol{A}\,s}\,\mathrm{d}\,s
$$

代入$\boldsymbol{M}_{12}$的整合式得：

$$
\boldsymbol{M}_{12} = \int_0^T e^{\boldsymbol{A}\,s}\,\boldsymbol{B}\,\mathrm{d}\,s = \boldsymbol{\Gamma}
\tag{app-10}
$$

恰为原系统的离散控制输入矩阵。

综上，增广矩阵的矩阵指数与离散矩阵存在严格的分块对应关系，即：

$$
\exp\left( \begin{bmatrix} \boldsymbol{A}& \boldsymbol{B}\\\boldsymbol{0}_{m\times n}& \boldsymbol{0}_{m\times m} \end{bmatrix}\,T\right) = \begin{bmatrix}\boldsymbol{\Phi}& \boldsymbol{\Gamma}\\ \boldsymbol{0}_{m\times n}& \boldsymbol{I}_m \end{bmatrix}
\tag{app-11}
$$
