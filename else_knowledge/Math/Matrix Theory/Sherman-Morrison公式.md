---
aliases:
tags:
  - Math
time: 2025-11-28T18:00:00
---
**摘要**
此文档介绍一种求解逆矩阵的方法，即公式，又称为谢尔曼-莫里森公式。

# 述

对于$n$阶可逆矩阵$\boldsymbol{A}\in\mathbb{R}^{n\times n}$，以及$n$维列向量$\boldsymbol{\alpha},\,\boldsymbol{\beta}\in\mathbb{R}^{n}$，Sherman-Morrison公式表示为：

$$
(\boldsymbol{A}+\boldsymbol{\alpha}\boldsymbol{\beta^\top})^{-1}=\boldsymbol{A}^{-1}-\frac{\boldsymbol{A}^{-1}\boldsymbol{\alpha}\boldsymbol{\beta}^\top\boldsymbol{A}^{-1}}{1+\boldsymbol{\beta}^{\top}\boldsymbol{A}^{-1}\boldsymbol{\alpha}}
\tag{1}
$$

该公式由Sherman和Morrison在1950年提出。

显然，根据公式Eq. (1)，求解$\boldsymbol{A}+\boldsymbol{\alpha}\boldsymbol{\beta^\top}$逆矩阵的过程，被简化为了求解$\boldsymbol{A}^{-1}$以及部分简单矩阵运算。

Sherman-Morrison公式提供了一种更加简洁地判别矩阵的和的可逆性以及求逆矩阵的方法。

对于该公式的证明可以参考理论数学论文[Sherman-Morrison公式的五种证明方法](https://pdf.hanspub.org/PM20240100000_98956933.pdf)。