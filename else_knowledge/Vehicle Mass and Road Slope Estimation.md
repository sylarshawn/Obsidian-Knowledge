---
aliases:
tags:
  - vehicle
time: 11/10/2025 21:03
---
**Abstract**
This essay aims to introduce a method for estimating vehicle mass and road slope. To estimate the vehicle mass, the Least Squares Method (LSM) is used to minimize the cost function with respect to the vehicle mass. Further, the estimation of the rod slope, which combines the estimated mass, is also based on the LSM.

# Longitudinal Dynamics

Obviously, the longitudinal acceleration contains the driving force, rolling resistance, and ramp resistance, which are described in Fig. 1. Furthermore, based on the analysis of the project reality, the longitudinal dynamics of the vehicle can be summarized as 

![[Longitudinal Dynamic Model.png | Fig.1 Longitudinal Dynamic Model]]

$$
\begin{aligned}
	F_x = m\dot{v}_x+\frac{1}{2}\rho C_d Av_x^2+mg(\sin\theta+f\cos\theta)
\end{aligned}
\tag{1}
$$
where, $F_x$ denotes the longitudinal driving force; $m$ means the mass of the vehicle; $\dot{v}_x$ is the longitudinal velocity, and $\dot{v}_x$ is its first-order derivative, which also denotes the longitudinal acceleration; $\rho$ is the air density; $C_d$ is the drag coefficient; $A$ represents the windward area of the vehicle; $g$ is the gravity acceleration; $\theta$ is the road slope; And $f$ denotes the pavement rolling drag coefficient.
And then, differentiate the acceleration $\dot{v}_x$ from Eq. 1:
$$
\begin{aligned}
	\frac{\mathrm{d}F_x}{d\dot{v}_x} = m + \rho C_d Av_x\frac{\mathrm{d}v_x}{\mathrm{d}\dot{v}_x}+mg(\cos\theta-\sin\theta)\frac{\mathrm{d}\theta}{\mathrm{d}\dot{v}_x}
\end{aligned}
\tag{2}
$$
To be clear, the method using to estimate the road slope supposes that the random change of slope is small, and then, which is not directly related to the acceleration of the vehicle. So the differentiation of slope to the acceleration can be represented as 
$$
\frac{\mathrm{d}\theta}{\mathrm{d}\dot{v}_x} = 0
\tag{3}
$$
Meanwhile, the change frequency of the driving force always be high, and when the frequency is large, the driving acceleration change rate is bigger than which about the velocity. Therefore, comparing with the differentiation of the driving acceleration, it can be assumed that the velocity differentiation is a small part, so we have 
$$
\frac{\mathrm{d}v_x}{\mathrm{d}\dot{v}_x} = 0
\tag{4}
$$
Combine Eqs. 3-4, when the change frequency of driving force is large, Eq. 2 can be rewritten or simplified as 
$$
m = \frac{\mathrm{d}F_x}{\mathrm{d}\dot{v}_x}
\tag{5}
$$
Obviously, when the driving force changes a lot, the wind resistance, rolling resistance and the road slope can be ignored to estimate the vehicle mass. Meanwhile, someone can get the mass per time when the vehicle drives, which approximately equal to the differentiation of driving force to the acceleration.

# High-Pass Filter Design

 By analysis of the frequency, from Eq. 5, it is obvious that the differentiation of driving force to acceleration can be approximated as the fraction of them. So the result differentiation can be calculated by using high-pass filter to get the high-pass information. To be honest, the original signal contains both the high-pass (acceleration, driving force etc.) and low-pass (wind and rolling resistance etc.) parts. And the differentiation can be explained as zoom in the high-pass signals and zoom out the low-pass parts.
 The most important part to use the high-pass filter is to find a proper cutoff frequency. On the one hand, if choose low one, the filter can not remove the impact of the low frequency part like wind and rolling resistance. On the other hand, if choose high one, the filter will remove lots of useful high frequency information. Consequently, the choose of the cutoff frequency should combine the features of different vehicles. Without loss of generality, the cutoff frequency can be got by experiments, and then, we can design the respect band-pass filter using Butterworth method.
 By high-pass filtering of the acceleration signal $\dot{v}_x$ and the driving force signal $F_x$, the high parts of them, which means $\dot{v}_x^*$ and $F_x^*$ can be presented. Because the two filters used are same, on the basis of the high-pass filter principle, Eq. 5 can be further written as 
$$
m = \frac{F_x^*}{\dot{v}_x^*}
\tag{6}
$$ which also is the base equation to estimate the vehicle mass.

# Least Square Estimation Method

It is important to note that the noise of the original signals is always large, use Eq. 6 directly to estimate the vehicle mass might be influenced by the acceleration and force noise. Therefore, the high-pass filtering results requires regression process.
Let $y = F_x^*,\,\,\phi = \dot{v}_x^*$, Eq. 6 can be converted to
$$
y = \phi \hat{m}
\tag{7}
$$
 where, $\hat{m}$ is the estimation vehicle mass. Then, considering let the estimation error minimal, the cost function can be written as 
$$
V(\hat{m}(k),\,k)=\frac{1}{2}\sum^k_{i=1}(y(i) - \phi(i)\hat{m}(k))^2
\tag{8}
$$
wherein $k$ denotes the sample time.
Eq. 8 is a classical LSM problem, in a linear system, solve the problem can be equal to find a proper parametric to let the function $V(\hat{m}(k),\,k)$ get its minimal value.
When Eq. 8 take the minimal value,
$$
\hat{m}(k) = (\sum_{i=1}^k\phi(i)^2)^{-1}(\sum^k_{i=1}\phi(i)y(i))
\tag{9}
$$
From Eq. 9, by the increase of $k$, the calculation complexity also increase gradually. Because the estimation of vehicle mass is conducted in real time, so the estimation method are also converted to the Recursive Least Squares (RLS), which means that the current sample information can corrects the former sample estimation information. The principle of the RLS can be summarized as 
$$
\begin{aligned}
\hat{m}(k) &= \hat{m}(k - 1) + L(k) (y(k)-\phi(k)\hat{m}(k-1)) \\
L(k) &= P(k-1)\phi(k)(1+\phi(k)P(k-1)\phi(k))^{-1}\\
P(k) &= (1-L(k)\phi(k))P(k-1)
\end{aligned}
\tag{10}
$$
where, $k$ denotes the current sample time and $k-1$ is the former one; $L$ is the least square gain; $P$ is the error covariance.
According to Eq. 10, one can estimates the vehicle mass about every sample time.

# Road Slope Estimation

The direct methods to estimate the road slope can be summarized as two types, kinematic methods and dynamics methods, both of them need the estimation of vehicle mass.
## Kinematic Estimation

The dynamic sensors are often fixed to the vehicle, the observed value of $a_x$ will be influenced by both of the driving force acceleration and the road slope. From Fig. 2, $a_x$ is the longitudinal acceleration observed by the sensors, $\dot{v}_x$ denotes the acceleration.

![[Longitudinal Kinematic Model.png|Fig.2 Longitudinal Kinematic Model]]

Furthermore, based on the kinematic method, the estimation of the road slope can be written as 
$$
\theta_k = \arcsin(\frac{a_x-\dot{v}_x}{g})
\tag{11}
$$

## Dynamic Estimation

The dynamic estimation method uses the same longitudinal dynamics Eq. 1, in which, all params except the road slope $\theta_d$ are considered as known or can be calculated. 
Similarly, let $y = F_x$, $u = m\dot{v}_x+0.5\rho C_d Av_x^2$, $b = mg(\sin\theta+f\cos\theta)$, and then Eq. 1 can be rewritten as 
$$
y = u+b
\tag{12}
$$
where, $y$ is the longitudinal driving force, which can be got by the feedback signal from the distributed drive motor; $u$ is the function of vehicle mass $m$ and velocity $v_x$, which is considered as known when the mass is known; $b$ is the function of vehicle $m$ and road slope $\theta$, the estimation of $b$ equals to the road slope $\theta$.
Based on the above analysis, the estimation of $b$ can use LSM. But because of the road slope and $b$ are both time-varying, so we can use the LSM with a forgetting factor. The cost function are chosen as 
$$
V(\hat{b}(k),\,k) =\frac{1}{2} \sum_{i=1}^k\lambda^{k-i}(y(i)-u(i)-\hat{b}(k))
\tag{13}
$$
where, $\lambda$ is the forgetting factor. It should be noticed that, $\lambda$ bigger, the perception of road slope can be more accuracy, but unavoidable the convergence slow down. The choose of $\lambda$ should consider both of the accuracy and the convergence speed.
When Eq. 13 take the minimal value, 
$$
\hat{b}(k)=(\sum_{i=1}^{k}\lambda^{k-i})^{-1}(\sum_{i=1}^{k}\lambda^{k-i}(y(i)-u(i)))
\tag{14}
$$
Similar to the estimation of vehicle mass, to deduce the calculation and improve the real-time property, the RLS with a forgetting factor $\lambda$ can be summarized as 
$$
\begin{aligned}
\hat{b}(k)&=\hat{b}(k-1)+L(k)(y(k)-u(k))\\
L(k)&=P(k-1)/(\lambda+P(k-1))\\
P(k)&=(1-L(k))P(k-1)/\lambda
\end{aligned}
\tag{15}
$$
and then, based on Eq. 15, one can estimate the value of $b$ at every sample time. Meanwhile, the value of road slope $\theta_d$ can be got together.

## Combination Estimation

The road slope can be considered as the mix of high and low frequency. On the one hand, the above dynamics estimation accuracy depends on the vehicle model, whose observed params are easily influenced by the high frequency noise. Therefore, the dynamics estimation result $\theta_d$ should be processed using the low-pass filter, which will remove the high frequency part and reserve the low part. On the other hand, the shortcoming of the kinematics methods is that the observed $a_x$ always influenced by the stable error, which belongs to the low frequency part. To guarantee the effectiveness of the kinematic estimation, the result $\theta_k$ should be processed using the high-pass filter to preserve the high part information. 
Combine the strength of kinematic and dynamic estimation, the combination estimation can use the kinematic to estimate when the road slope changes drastically and use the dynamic to estimate when the road slope changes slowly.
