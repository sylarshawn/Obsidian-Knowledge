---
aliases:
  - CW
  - CW方程
tags:
  - Physics
time: 2026-03-24T16:38:00
---
**摘要**
此文档介绍航天器相对运动建模过程中，常用的线性化模型Clohessy-Wiltshire方程（简称CW方程，又称为Hill-Clohessy-Wiltshire方程），主要包括该方程的具体推导和实际应用。

# 概念

CW方程（Clohessy-Wiltshire方程，又称为Hill-Clohessy-Wiltshire方程），1960年由Clohessy和Wiltshire两位学者提出，用于描述两个航天器之间的相对运动关系。

简单而言，其核心应用场景为：以在圆轨道上运行的**目标航天器**（如空间站、在轨卫星，作为相对运动的参考基准）为原点建立旋转坐标系，描述**追踪航天器**（如货运飞船、交会对接飞行器、编队伴飞卫星）相对于目标航天器的位置、速度状态的演化规律。该方程广泛应用于航天器交会对接、近距离编队飞行、相对导航与轨道控制等任务场景。

# 前提假设

CW方程由[[二体问题]]下的简化线性模型，其推导与应用必须严格满足以下假设，偏离假设会导致模型误差显著增大：

1. **目标航天器轨道约束**：目标航天器在地球中心引力场中做**无摄动圆轨道运动**，轨道半径、轨道角速度恒定不变；
2. **近距离相对运动约束**：追踪航天器与目标航天器的相对距离远小于目标航天器的轨道半径（工程中一般要求相对距离小于轨道半径的$1\%$），可对非线性引力项做一阶泰勒展开，忽略二阶及以上高阶小量；
3. **无摄动假设**：忽略地球以外的所有摄动影响（如大气阻力、太阳光压、第三体引力、地球非球形引力等），仅考虑地球中心引力的作用；
4. **质点假设**：将目标航天器与追踪航天器均视为质点，忽略航天器自身姿态运动、结构挠性对相对运动的影响；
5. **坐标系旋转约束**：相对运动的参考坐标系（LVLH 系）与目标航天器轨道固连，随目标航天器同步做圆轨道运动，无额外的姿态旋转。

# 符号约定

为避免符号冲突与概念混淆，本文采用如下符号体系：

| 符号                    | 物理含义                                                                                                                  |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| $G$                   | 万有引力常数                                                                                                                |
| $M$                   | 地球质量                                                                                                                  |
| $\mu$                 | 地球引力常数，$\mu=GM\approx 3.986004418\times 10^14\mathrm{m^3/s^2}$                                                        |
| $\boldsymbol{r}_t$    | 目标航天器相对于地心的位置矢量（[[ECI-地心惯性坐标系]]下），标量模长$r_t=\Vert\boldsymbol{r}_t\Vert$                                                |
| $\boldsymbol{r}_c$    | 追踪航天器相对于地心的位置矢量（[[ECI-地心惯性坐标系]]下），标量模长$r_c=\Vert\boldsymbol{r}_c\Vert$                                                |
| $\boldsymbol{\rho}$   | 追踪航天器相对于目标航天器的相对位置矢量，满足$\boldsymbol{\rho}=\boldsymbol{r}_c-\boldsymbol{r}_t$，标量模长$\rho=\Vert \boldsymbol{\rho} \Vert$ |
| $n$                   | 目标航天器的轨道平均角速度，圆轨道下为恒定值                                                                                                |
| $\boldsymbol{\omega}$ | [[LVLH-本地垂直-本地水平坐标系]]相对于[[ECI-地心惯性坐标系]]的角速度矢量                                                                         |

同时，采用$\mathrm{d}\,/\mathrm{d}\,t|_\boldsymbol{I},\,\mathrm{d}\,/\mathrm{d}\,t|_\boldsymbol{B}$分别表示[[ECI-地心惯性坐标系]]下的绝对时间导数算子和[[LVLH-本地垂直-本地水平坐标系]]下的相对时间导数算子。

*注：圆轨道下，[[LVLH-本地垂直-本地水平坐标系]]相对于[[ECI-地心惯性坐标系]]的角速度矢量大小为轨道角速度$n$，方向沿$Z$轴正方向，因此$\boldsymbol{\omega}$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的分量形式为$\boldsymbol{\omega}=[0,0,n]^\mathrm{T}$。同时，圆轨道下角速度恒定，因此角加速度$\boldsymbol{\dot{\omega}}=\mathrm{d}\,\boldsymbol{\omega}/\mathrm{d}\,t=\boldsymbol{0}$。*

# CW方程推导

航天器绕地球运动遵循[[二体问题]]动力学方程。其推导可以分为以下几个步骤：首先，基于[[二体问题]]建立目标与追踪航天器的绝对运动方程；其次，通过[[旋转矢量微分法则]]，将[[惯性与非惯性坐标系#惯性坐标系|惯性系]]下的绝对加速度差转换为[[LVLH-本地垂直-本地水平坐标系|LVLH]]旋转系下的相对加速度；进一步地，基于近距离假设对非线性引力项作一阶泰勒展开线性化；最后，整理得到[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的CW方程标量形式与矢量形式。

## 二体问题绝对运动方程

在[[ECI-地心惯性坐标系|ECI]]惯性系下，航天器绕地球的无摄动运动满足[[二体问题|二体动力学方程]]，其矢量形式为：

$$
\frac{\mathrm{d}^2\,\boldsymbol{r}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}} = -\frac{\mu}{r^3}\boldsymbol{r}
\tag{1}
$$

其中，$\mu=G(M+m)\approx GM\in\mathbb{R}$，$\boldsymbol{r}\in\mathbb{R}^3$是惯性坐标系下航天器相对于地心的位置矢量，$r\in\mathbb{R}$为其对应的标量距离。

### 目标航天器的绝对运动方程

对于圆轨道运动的目标航天器，其轨道半径$r_{t}\in\mathbb{R}$为常数，将其矢量形式$\boldsymbol{r}_{t}\in\mathbb{R}^3$（目标相对于地心的位置矢量）代入二体运动方程Eq. (1)：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=-\frac{\mu}{r_t^3}\boldsymbol{r}_t
\end{aligned}
\tag{2}
$$

同时，对于角速度为$n$，轨道半径为$r_t$的匀速圆周运动，其向心加速度大小满足：

$$
a_{\mathrm{centripetal}}=n^2r_t
\tag{3}
$$

由于目标航天器的向心加速度完全由引力提供，则引力加速度的大小等于向心加速度大小，联立Eq. (1)和Eq. (3)得：

$$
\left\Vert \frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}} \right\Vert=\frac{\mu}{r_t^2}=n^2r_t
\tag{4}
$$
整理得，目标航天器轨道角速度$n$可以写作：

$$
n=\sqrt{\frac{\mu}{r_t^3}}
\tag{5}
$$

因而，目标航天器的绝对运动方程可表述为：

$$
\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=-n^2\boldsymbol{r}_t
\tag{6}
$$

### 追踪航天器的绝对运动方程

与之类似地，追踪航天器的绝对运动方程同样满足二体问题假设：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{r}_c}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=-\frac{\mu}{r_c^3}\boldsymbol{r}_c
\end{aligned}
\tag{7}
$$

同时，定义追踪航天器与目标航天器之间的相对距离矢量为$\boldsymbol{\rho}=\boldsymbol{r}_c-\boldsymbol{r}_t$，该差矢量在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的分量形式为$\boldsymbol{\rho}=[x,y,z]^\mathrm{T}$。对等式两侧在[[ECI-地心惯性坐标系|ECI]]惯性系下求二阶时间导数，得到绝对加速度的关系：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=
	\frac{\mathrm{d}^2\,\boldsymbol{r}_c}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}
\end{aligned}
\tag{8}
$$

将式Eq. (2)与Eq. (7)代入Eq. (8)中得到在[[ECI-地心惯性坐标系|ECI]]惯性系下的相对加速度方程：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}&=
	-\frac{\mu}{r_c^3}\boldsymbol{r}_c+n^2\boldsymbol{r}_t\\
	&=-\Delta\boldsymbol{g}
\end{aligned}
\tag{9}
$$

其中，$\Delta\boldsymbol{g}$为引力差项，亦即[[ECI-地心惯性坐标系|惯性系]]下相对位置矢量$\boldsymbol{\rho}$的绝对二阶导数。

### 旋转坐标系中的加速度转换

式Eq. (9)中的$\mathrm{d}^2\,\boldsymbol{\rho}/\mathrm{d}\,t^2|_\boldsymbol{I}$是相对位置矢量在[[ECI-地心惯性坐标系|ECI]]惯性系下的绝对二阶导数，而工程中关注的是**LVLH 旋转系下的相对加速度**，因此需要通过[[旋转矢量微分法则#带平动的任意运动坐标系的二阶通用形式|带平动的二阶旋转矢量微分法则通用形式]]完成转换。

对于原点随目标航天器平动、同时随目标航天器旋转的[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系，相对位置矢量$\boldsymbol{\rho}$的绝对二阶导数与相对二阶导数的转换关系为：

$$
\frac{\mathrm{d}^2\,\boldsymbol{r}_c}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}=\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}+\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}+\boldsymbol{\dot{\omega}}\times \boldsymbol{\rho}+2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}+\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})
\tag{10}
$$

移项得：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}=
\frac{\mathrm{d}^2\,\boldsymbol{r}_c}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\boldsymbol{\dot{\omega}}\times \boldsymbol{\rho}-2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}-\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})
\tag{11}
$$

### 角加速度项简化

目标航天器在圆轨道上运动，轨道角速度$n$为定值，因此[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系的角加速度$\boldsymbol{\dot{\omega}}=0$，进而Eq. (11)中的角加速度牵连项$\boldsymbol{\dot{\omega}}\times \boldsymbol{\rho}=0$。因此，Eq. (11)可以简化为：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}=
\frac{\mathrm{d}^2\,\boldsymbol{r}_c}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-\frac{\mathrm{d}^2\,\boldsymbol{r}_t}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{I}}-2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}-\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})
\tag{12}
$$

结合Eq. (8)和Eq. (9)，Eq. (12)可以进一步写作包含平动加速度项的形式，亦是[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的相对运动矢量方程：

$$
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}=
-\frac{\mu}{r_c^3}\boldsymbol{r}_c+n^2\boldsymbol{r}_t-2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}-\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})
\tag{13}
$$

### 非线性项线性化

在Eq. (13)中，包含非线性项$-\mu\,\boldsymbol{r}_c/r_c^3$，需要基于近距离假设作一阶展开线性化。

由$\boldsymbol{r}_c=\boldsymbol{r}_t+\boldsymbol{\rho}$，对其模长作平方展开得：

$$
\begin{aligned}
r_c^2&=\Vert \boldsymbol{r}_t+\boldsymbol{\rho} \Vert^2\\
&=\Vert \boldsymbol{r}_t \Vert^2+\Vert \rho \Vert^2+2\boldsymbol{r}_t\cdot\boldsymbol{\rho}\\
&=r_t^2+\rho^2+2\boldsymbol{r}_t\cdot\boldsymbol{\rho}
\end{aligned}
\tag{14}
$$

根据[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系的定义，$\boldsymbol{r}_t$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的分量为$\boldsymbol{r}_t=[r_t,0,0]^\mathrm{T}$，相对位置矢量$\boldsymbol{\rho}$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的分量为$\boldsymbol{\rho}=[x,y,z]^\mathrm{T}$，因此Eq. (14)中的点积$\boldsymbol{r}_t\cdot\boldsymbol{\rho}=r_t\,x$，代入Eq. (14)中得：

$$
r_c^2=r_t^2+2r_t\,x+\rho^2
\tag{15}
$$

由于近距离假设中$\rho\ll r_t$，且$\rho^2$为二阶小量可以忽略，因此Eq. (14)可以写作：

$$
r_c\approx\sqrt{r_t^2+2r_t\,x}=r_t\sqrt{1+\frac{2\,x}{r_t}}
\tag{16}
$$

引力项中的核心非线性部分为$r_c^{-3}$，即：

$$
r_c^{-3}=r_t^{-3}\,(1+\frac{2\,x}{r_t})^\frac{-3}{2}
\tag{17}
$$

基于小参数泰勒展开公式：当$\vert \epsilon\vert\ll 1$时，$(1+\epsilon)^\alpha\approx 1+\alpha\,\epsilon$，显然，Eq. (17)可以进一步写作：

$$
r_c^{-3}=r_t^{-3}(1-\frac{3}{2}\,\frac{2\,x}{r_t})=r_t^{-3}(1-\frac{3\,x}{r_t})
\tag{18}
$$

又结合$n^2=\mu/r_t^3$，Eq. (18)可改写为：

$$
\frac{\mu}{r_c^3}\approx n^2(1-\frac{3\,x}{r_t})
\tag{19}
$$

同时，$\boldsymbol{r}_c=\boldsymbol{r}_t+\boldsymbol{\rho}$在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的分量形式为：

$$
\boldsymbol{r}_c=\begin{bmatrix} r_t+x\\y\\z \end{bmatrix}
\tag{20}
$$

综合Eq. (19)和Eq. (20)，展开并忽略二阶小量，非线性引力项可以近似表示为：

$$
\begin{aligned}
	-\frac{\mu}{r_c^3}\,\boldsymbol{r}_c&\approx-n^2(1-\frac{3\,x}{r_t})\begin{bmatrix} r_t+x\\y\\z \end{bmatrix}\\
	&= -n^2\begin{bmatrix} r_t+x-3\,x-\frac{3\,x^2}{r_t^2}\\y-\frac{3\,x\,y}{r_t}\\ z-\frac{3\,x\,z}{r_t} \end{bmatrix}\\
	&\approx -n^2\begin{bmatrix} r_t-2\,x\\y\\z \end{bmatrix}
\end{aligned}
\tag{21}
$$

进一步，已知：

$$
\boldsymbol{\omega}=[0,0,n]^\mathrm{T},\,\,
\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}=[\dot{x},\dot{y},\dot{z}]^\mathrm{T},\,\,
\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_\boldsymbol{B}=[\ddot{x},\ddot{y},\ddot{z}]^\mathrm{T}
$$

针对Eq. (13)中的科氏加速度项，向心牵连加速度项，目标航天器引力加速度项，在[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下作分量展开：

$$
\begin{aligned}
	-2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B} &= \begin{bmatrix} 2n\,\dot{y}\\-2n\,x\\0 \end{bmatrix},\\
	-\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) &= \begin{bmatrix} n^2\,x\\n^2\,y\\0 \end{bmatrix},\\
	n^2\,\boldsymbol{r}_t&=\begin{bmatrix} n^2\,r_t\\0\\0 \end{bmatrix}.\\
\end{aligned}
\tag{22}
$$

### CW方程

#### 标量形式

将Eq. (21)，Eq. (22)代入Eq. (13)中，并按照三轴方向分别合并，可得[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系下的CW方程标量形式为：

$$
\left\{\begin{matrix}\begin{aligned}
&\ddot{x}-2\,n\,\dot{y}-3\,n^2\,x=0\\
&\ddot{y}+2\,n\,\dot{x}=0\\
&\ddot{z}+n^2\,z=0
\end{aligned}\end{matrix}\right.
\tag{23}
$$

#### 矢量形式

基于通用公式Eq. (13)，整理可得相对加速度的基本矢量方程：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}+2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}+\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho})=
	-\frac{\mu}{r_c^3}\boldsymbol{r}_c+n^2\boldsymbol{r}_t
\end{aligned}
\tag{24-1}
$$

显然，Eq. (24-1)的等号右侧即为Eq. (9)的右侧，即引力差项$\Delta\boldsymbol{g}$的负值，而后对此部分进行线性化处理。代入Eq. (19)与Eq. (20)，可以推得该引力差项在[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的分量形式：

$$
\begin{aligned}
	\Delta\boldsymbol{g} &\approx -n^2\,(1-\frac{3\,x}{r_t})\,\begin{bmatrix} r_t+x\\y\\z \end{bmatrix} + n^2\,\begin{bmatrix} r_t\\0\\0 \end{bmatrix}
\end{aligned}
\tag{24-2}
$$

Eq. (24-2)中等式右侧的第一项实际为Eq. (21)，结合Eq. (21)的线性化结果得：

$$
\begin{aligned}
	\Delta\boldsymbol{g} &\approx -n^2\,\begin{bmatrix} r_t-2\,x\\ y\\ z \end{bmatrix} + n^2\,\begin{bmatrix} r_t\\0\\0 \end{bmatrix}\\
	&= \begin{bmatrix} 2\,n^2\,x\\ -n^2\,y\\ -n^2\,z \end{bmatrix}
\end{aligned}
\tag{24-3}
$$
而后，将Eq. (24-3)分量形式转化为通用矢量形式。考虑[[LVLH-本地垂直-本地水平坐标系|LVLH]]系下的相对位置矢量$\boldsymbol{\rho}$的实际形式为：

$$
n^2\,\boldsymbol{\rho} = n^2\,\begin{bmatrix} x\\ y\\ z \end{bmatrix} = \begin{bmatrix} n^2\,x\\ n^2\,y\\ n^2\,z \end{bmatrix}
\tag{24-4}
$$

同时，径向分量的矢量可以表示为$\boldsymbol{\rho}\,\boldsymbol{\hat{x}} = x$，其中，$\boldsymbol{\hat{x}}$是[[LVLH-本地垂直-本地水平坐标系|LVLH]]坐标系$x$轴的单位矢量。进而有：

$$
3\,n^2\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\,\boldsymbol{\hat{x}} = 3\,n^2\,x\,\begin{bmatrix} 1\\ 0\\ 0 \end{bmatrix} = \begin{bmatrix} 3\,n^2\,x\\ 0\\ 0 \end{bmatrix}
\tag{24-5}
$$

观察有，Eq. (24-3)可以写作Eq. (24-4)与Eq. (24-5)的结合：

$$
\begin{bmatrix} 2\,n^2\,x\\ -n^2\,y\\ -n^2\,z \end{bmatrix} = \begin{bmatrix} n^2\,x\\ n^2\,y\\ n^2\,z \end{bmatrix} - \begin{bmatrix} 3\,n^2\,x\\ 0\\ 0 \end{bmatrix}
\tag{24-6}
$$

结合Eq. (24-6)，引力差项可以进一步写作：

$$
\Delta\boldsymbol{g} \approx n^2\,\boldsymbol{\rho} - 3\,n^2\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\boldsymbol{\hat{x}}
\tag{24-7}
$$

将Eq. (24-7)代入Eq. (24-1)中可得**CW方程的通用矢量形式**为：

$$
\begin{aligned}
	\frac{\mathrm{d}^2\,\boldsymbol{\rho}}{\mathrm{d}\,t^2}\Bigg|_{\boldsymbol{B}}+2\boldsymbol{\omega}\times\frac{\mathrm{d}\,\boldsymbol{\rho}}{\mathrm{d}\,t}\Bigg|_\boldsymbol{B}+\boldsymbol{\omega}\times(\boldsymbol{\omega}\times\boldsymbol{\rho}) + n^2\,\boldsymbol{\rho} - 3\,n^2\,(\boldsymbol{\rho}\,\boldsymbol{\hat{x}})\boldsymbol{\hat{x}} = \boldsymbol{0}
\end{aligned}
\tag{25}
$$

## CW状态空间方程

为便于系统规划和控制，可以将CW方程写作一阶线性状态空间方程的形式。定义相对运动状态矢量为：

$$
\boldsymbol{X} = [x,y,z,\dot{x},\dot{y},\dot{z}]^\mathrm{T}
\tag{25}
$$

则状态空间方程为：

$$
\boldsymbol{\dot{X}} = \boldsymbol{A}\boldsymbol{X}
\tag{26}
$$

其中，

$$
\boldsymbol{A}=\begin{bmatrix}
0&0&0&1&0&0\\
0&0&0&0&1&0\\
0&0&0&0&0&1\\
3\,n^2&0&0&0&2\,n&0\\
0&0&0&-2\,n&0&0\\
0&0&-n^2&0&0&0
\end{bmatrix}
$$

带控制输入的连续CW方程为：

$$
\boldsymbol{\dot{X}} = \boldsymbol{A}\,\boldsymbol{X}+\boldsymbol{B}\,\boldsymbol{u}
\tag{27}
$$

其中，$\boldsymbol{u} = [u_x,\,u_y,\,u_z]^\mathrm{T}$，单位为$\mathrm{m/s^2}$，控制输入矩阵为

$$
\boldsymbol{B} = \begin{bmatrix} 0& 0& 0\\ 0& 0& 0\\ 0& 0& 0\\ 1& 0& 0\\ 0& 1& 0\\ 0& 0& 1\end{bmatrix}
$$

#### 离散形式

由于轨道控制系统均为离散时间采样系统，控制指令仅在离散采样时刻更新，需要将原连续时间CW方程转化为离散形式。离散方法采用零阶保持（Zero Order Hold，ZOH），即控制加速度在一个采样周期内保持恒定。

##### 连续时间状态转移矩阵

对于线性时不变系统$\boldsymbol{\dot{X}} = \boldsymbol{A}\boldsymbol{X}$，其状态转移矩阵为矩阵指数函数：

$$
\begin{aligned}
	\boldsymbol{\Phi}(\tau) = e^{\boldsymbol{A}\,\tau},\,\,\tau=t-t_0
\end{aligned}
\tag{28}
$$

其中，$t_0,\,t$分别为初始时刻和当前时刻，$\tau$是两者的时间间隔。

注：关于<u>线性时不变系统的状态转移矩阵是矩阵指数函数</u>的分析可以参考本节[[Clohessy-Wiltshire方程#附录|附录]]中[[Clohessy-Wiltshire方程#附录#附1 关于<u>线性时不变（LTI）系统的状态转移矩阵是矩阵指数函数</u>的证明|关于线性时不变（LTI）系统的状态转移矩阵是矩阵指数函数的证明]]。

通过[[矩阵分解#特征值分解|矩阵特征值分解]]求解矩阵指数，结合[[Clohessy-Wiltshire方程]]在轨道面内与轨道面外解耦的特性（即$z$方向的运动与$x\text{-}y$平面的运动完全独立），可以得到$\boldsymbol{\Phi}(\tau)$的解析分块对角形式：

$$
\boldsymbol{\Phi}(\tau) = \begin{bmatrix}
\boldsymbol{\Phi}_{x\,y}(\tau)& \boldsymbol{0}_{4\times 2}\\
\boldsymbol{0}_{2\times 4}& \boldsymbol{\Phi}_z(\tau)
\end{bmatrix}
\tag{29}
$$

其中，轨道面$x\text{-}y$的子矩阵$\boldsymbol{\Phi}_{x\,y}(\tau)$为

$$
\boldsymbol{\Phi}_{x\,y}(\tau) = \begin{bmatrix}
4-3\,\cos(n\,\tau) & 0 & \sin(n\,\tau)/n & 2\,(1-\cos(n\,\tau))/n \\
6\,(\sin(n\,\tau)-n\,\tau) & 1 & 2\,(\cos(n\,\tau)-1)/n & (4\,\sin(n\,\tau)-3\,n\,\tau)/n \\
3\,n\,\sin(n\,\tau) & 0 & \cos(n\,\tau) & 2\,\sin(n\,\tau) \\
6\,n\,(\cos(n\,\tau)-1) & 0 & -2\,\sin(n\,\tau) & 4\,\cos(n\,\tau)-3
\end{bmatrix}
$$

轨道面外$z$方向的子矩阵$\boldsymbol{\Phi}_z(\tau)$为

$$
\boldsymbol{\Phi}_{z}(\tau) = \begin{bmatrix}
\cos(n\,\tau) & \sin(n\,\tau) \\
-n\,\sin(n\,\tau) & \cos(n\,\tau)
\end{bmatrix}
$$

进一步地，带控制输入的线性时不变系统的通解为：

$$
\boldsymbol{X}(t) = \boldsymbol{\Phi}(t-t_0)\,\boldsymbol{X}(t_0) + \int_{t_0}^t\boldsymbol{\Phi}(T-\tau)\,\boldsymbol{B}\,\mathrm{d}\,\tau\,\boldsymbol{u}_k
\tag{30-1}
$$

其中，离散状态转移矩阵$\boldsymbol{\Phi}_k = \boldsymbol{\Phi}(T)$，因系统时不变，该矩阵实际与$k$无关，后文简化为$\boldsymbol{\Phi}$表示；离散控制输入矩阵$\boldsymbol{\Gamma}_k = \int_0^T\boldsymbol{\Phi}(T-t)\,\boldsymbol{B}\,\mathrm{d}\,\tau$，显然该矩阵亦与$k$无关，后文简化为$\boldsymbol{\Gamma}$表示。

因此，[[Clohessy-Wiltshire方程]]的离散状态空间方程的最终形式为：

$$
\boldsymbol{X}_{k+1} = \boldsymbol{\Phi}\,\boldsymbol{X}_k+\boldsymbol{\Gamma}\,\boldsymbol{u}_k
\tag{30-2}
$$

接下来需要对离散控制输入矩阵$\boldsymbol{\Gamma}$的元素进行分析。
从Eq. (27)中可知，控制输入矩阵$\boldsymbol{B}$的前三行为$0$，后三行为单位矩阵，因此式Eq. (30)中的$\boldsymbol{\Phi}(T-\tau)\,\boldsymbol{B}$的前三行为$0$，后三行与$\boldsymbol{\Phi}(T-\tau)$的后三行一致。替换Eq. (30)中的积分变量为$s = T-\tau$，则有$\mathrm{d}\,\tau = -\mathrm{d}\,s$，积分上下限反转，即：

$$
\boldsymbol{\Gamma}(T) = \int_0^T\boldsymbol{\Phi}(s)\,\boldsymbol{B}\,\mathrm{d}\,s
\tag{31-1}
$$

逐项计算离散控制输入矩阵$\boldsymbol{\Gamma}$的元素：

$x$方向控制输入：
$$
\begin{aligned}
	\Gamma_{11} &= \int_0^T \frac{\sin(ns)}{n}\mathrm{d}s = \frac{1-\cos(nT)}{n^2}\\
	\Gamma_{21} &= \int_0^T \frac{2(\cos(ns)-1)}{n}\mathrm{d}s = \frac{2(\sin(nT)-nT)}{n^2}\\
	\Gamma_{31} &= 0\\
	\Gamma_{41} &= \int_0^T \cos(ns)\mathrm{d}s = \frac{\sin(nT)}{n}\\
	\Gamma_{51} &= \int_0^T -2\sin(ns)\mathrm{d}s = \frac{2(\cos(nT)-1)}{n}\\
	\Gamma_{61} &= 0
\end{aligned}
\tag{31-2}
$$

$y$方向控制输入：

$$
\begin{aligned}
	\Gamma_{12} &= \int_0^T \frac{2(1-\cos(ns))}{n}\mathrm{d}s = \frac{2(nT-\sin(nT))}{n^2}\\
	\Gamma_{22} &= \int_0^T \frac{4\sin(ns)-3ns}{n}\mathrm{d}s = \frac{4(1-\cos(nT))-\frac{3}{2}n^2T^2}{n^2}\\
	\Gamma_{32} &= 0\\
	\Gamma_{42} &= \int_0^T 2\sin(ns)\mathrm{d}s = \frac{2(1-\cos(nT))}{n}\\
	\Gamma_{52} &= \int_0^T (4\cos(ns)-3)\mathrm{d}s = \frac{4\sin(nT)-3nT}{n}\\
	\Gamma_{62} &= 0
\end{aligned}
\tag{31-3}
$$


$z$方向控制输入：

$$
\begin{aligned}
	\Gamma_{13} &= 0\\
	\Gamma_{23} &= 0\\
	\Gamma_{33} &= \int_0^T \frac{\sin(ns)}{n}\mathrm{d}s = \frac{1-\cos(nT)}{n^2}\\
	\Gamma_{43} &= 0\\
	\Gamma_{53} &= 0\\
	\Gamma_{63} &= \int_0^T \cos(ns)\mathrm{d}s = \frac{\sin(nT)}{n}
\end{aligned}
\tag{31-4}
$$

结合 Eqs. (30-3), (30-4), (30-5)，离散控制输入矩阵$\boldsymbol{\Gamma}$可以整理为：

$$
\boldsymbol{\Gamma}(T) = 
\begin{bmatrix}
	(1-\cos(n\,T))/n^2 & 2\,(n\,T-\sin(n\,T))/n^2 & 0\\
	2\,(\sin(n\,T)-n\,T)/n^2 & (4\,(1-\cos(n\,T))-1.5\,n^2\,T^2)/n^2 & 0\\
	0 & 0 & (1-\cos(n\,T))/n^2\\
	\sin(n\,T)/n & 2\,(1-\cos(n\,T))/n & 0\\
	2\,(\cos(n\,T)-1)/n & (4\,\sin(n\,T)-3\,n\,T)/n & 0\\
	0 & 0 & \sin(n\,T)/n
\end{bmatrix}
\tag{31-5}
$$

同时，由于该方程显得十分复杂，可以进行极限一致性检验。当采样周期$T\rightarrow 0$时，利用下述泰勒展开：

$$
\cos(n\,T) \approx 1-\ \frac{(n\,T)^2}{2},\,\,\sin(n\,T) \approx n\,T
$$

可得：

$$
\boldsymbol{\Phi}(T) = \boldsymbol{I} + \boldsymbol{A}\,T,\,\,\boldsymbol{\Gamma(T)} \approx \boldsymbol{B}\,T
\tag{32-1}
$$

代入离散方程Eq. (30-2)中得：

$$
\begin{aligned}
	\frac{\boldsymbol{X}_{k+1} - \boldsymbol{X}_k}{T} 
	&= \frac{(\boldsymbol{\Phi} - \boldsymbol{I})\,\boldsymbol{X}_k + \boldsymbol{\Gamma}\,\boldsymbol{u}_k}{T} \\
	&\approx \frac{\boldsymbol{A}\,T\,\boldsymbol{X}_k - \boldsymbol{B}\,T\,\boldsymbol{u}_k}{T}\\
	&\approx \boldsymbol{A}\,\boldsymbol{X}_k + \boldsymbol{B}\,\boldsymbol{u}_k
\end{aligned}
\tag{32-2}
$$

显然Eq. (32-2)与Eq. (27)保持一致，可以判定基本正确。


# 附录

## 附1 关于线性时不变（LTI）系统的状态转移矩阵是矩阵指数函数的证明

对于标量范畴下的一阶常微分方程$\dot{x} = a\,x(t)$，初值$x(0) = x_0$，该微分方程的解为$x(t) = \exp(a\,t)\,x_0$。
显然，对于方程解的解释从另一个角度而言，相当于将状态从$0$时刻转移到$t$时刻的某种映射，即标量形势下的状态转移因子。

进一步地，将标量$a$调整为$n\times n$方阵$\boldsymbol{A}$，状态$\boldsymbol{x}(t)\in\mathbb{R}^n$，有：

$$
\boldsymbol{\dot{x}}(t) = \boldsymbol{A}\,\boldsymbol{x}(t),\,\boldsymbol{x}(0) = \boldsymbol{x}_0
\tag{app-1}
$$

对于Eq. (app-1)，希望其具有与标量形式下$x(t) = e^{a\,t}\,x_0$相同形式的解，即保持形式：

$$
\boldsymbol{x}(t) = e^{\boldsymbol{A}\,t}\,\boldsymbol{x}_0
\tag{app-2}
$$

显然，需要定义矩阵的指数函数$\exp(\boldsymbol{A}\,t)$，并对该形式进行验证。

首先，考虑矩阵指数$\exp(\boldsymbol{A}\,t)$的幂级数形式：

$$
e^{\boldsymbol{A}\,t} = \boldsymbol{I} + \boldsymbol{A}\,t + \frac{(\boldsymbol{A}\,t)^2}{2!} + \frac{(\boldsymbol{A}\,t)^3}{3!} + \dots
\tag{app-3}
$$

根据幂级数的基本形式，Eq. (app-3)对于所有的方阵$\boldsymbol{A}$都绝对收敛，同时具有以下良好性质：初始条件满足$\exp(\boldsymbol{A}\,0) = \boldsymbol{I}$，且其时间导数为$\boldsymbol{A}\,\exp(\boldsymbol{A}\,t)$。

其次，为了验证Eq. (app-3)是否为状态转移矩阵，假设$\boldsymbol{\Phi}(t) = \exp(\boldsymbol{A}\,t)$，则有：

$$
\boldsymbol{\dot{\Phi}}(t) = \boldsymbol{A}\,\boldsymbol{\Phi}(t),\,\boldsymbol{\Phi}(0) = \boldsymbol{I}
\tag{app-4-1}
$$

令$\boldsymbol{x}(t) = \boldsymbol{\Phi}(t)\,\boldsymbol{x}_0$，则有：

$$
\boldsymbol{\dot{x}}(t) = \boldsymbol{\dot{\Phi}}(t)\,\boldsymbol{x}_0 = \boldsymbol{A}\,\boldsymbol{\Phi}(t)\,\boldsymbol{x}_0 = \boldsymbol{A}\,\boldsymbol{x}(t)
\tag{app-4-2}
$$

且$\boldsymbol{x}(0) = \boldsymbol{I}\,\boldsymbol{x}_0 = \boldsymbol{x}_0$，显然，Eq. (app-2)即为Eq. (app-1)的解。

进一步地，对于任意初始时刻$t_0$，有：

$$
\boldsymbol{x}(t) = e^{\boldsymbol{A}\,(t-t_0)}\,\boldsymbol{x}(t_0)
\tag{app-4-3}
$$

因此，状态转移矩阵为：

$$
\boldsymbol{\Phi}(t,\,t_0) = e^{\boldsymbol{A}\,(t-t_0)}
\tag{app-4-4}
$$

显然，从Eq. (app-4-4)中得，该状态转移矩阵只依赖于时间差$t-t_0$，这也反映了系统的时不变本质。

当然，这也可以从拉普拉斯变换的角度进行解释。对$\boldsymbol{\dot{x}} = \boldsymbol{A}\,\boldsymbol{x}$两边同时进行拉普拉斯变换，假定初始条件为$\boldsymbol{x}(0) = \boldsymbol{x}_0$，则有：

$$
\begin{aligned}
	&\qquad s\,\boldsymbol{X}(s) - \boldsymbol{s} = \boldsymbol{A}\,\boldsymbol{X}(s)\\
	&\Rightarrow \boldsymbol{X}(s) = (s\,\boldsymbol{I} - \boldsymbol{A})^{-1}\,\boldsymbol{x}_0
\end{aligned}
\tag{app-5}
$$

反变化得到：

$$
\boldsymbol{x}(t) = \mathcal{L}^{-1}\{ (s\,\boldsymbol{I} - \boldsymbol{A})^{-1} \}\,\boldsymbol{x}_0
\tag{app-5-1}
$$

其中$(s\,\boldsymbol{I} - \boldsymbol{A})^{-1}$的拉普拉斯逆变换恰为$\exp(\boldsymbol{A}\,t)$，上述分析从变换域的角度说明了LTI系统的状态转移矩阵为矩阵指数。

在得到上述基本结论后，不妨考虑前置定语<u>线性时不变系统</u>的限制，当系统具有时变性时，即：

$$
\boldsymbol{\dot{x}}(t) = \boldsymbol{A}(t)\,\boldsymbol{x}(t)
\tag{app-6-1}
$$

状态转移矩阵$\boldsymbol{\Phi}(t,\,t_0)$仍然满足：

$$
\frac{\partial\,}{\partial\,t}\boldsymbol{\Phi}(t,\,t_0) = \boldsymbol{A}(t)\,\boldsymbol{\Phi}(t,\,t_0),\,\,\boldsymbol{\Phi}(t_0,\,t_0) = \boldsymbol{I}
\tag{app-6-2}
$$

但需要注意，$\boldsymbol{A}(t)$在不同时刻非常值，$\boldsymbol{\Phi}(t,\,t_0)$也无法写作$\exp(\int_{t_0}^t\,\boldsymbol{A}(\tau)\,\mathrm{d}\,\tau)$的形式，即，只有在LTI系统中，状态转移矩阵才恰好是矩阵指数函数。