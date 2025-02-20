---
title: 读书笔记-机器学习 Appendix & Ch3
date: 2024-10-26 23:25:14
hidden: true
tags:
- 读书笔记
- 机器学习
categories:
- 读书笔记-机器学习
---

<!--more-->

<p><font size = 5><b>目录</b></font></p>

- [Appendix: 数学预备知识](#appendix-数学预备知识)
  - [矩阵](#矩阵)
    - [基本演算](#基本演算)

## Appendix: 数学预备知识

### 矩阵

#### 基本演算

- **矩阵元素:** 实矩阵$\mathbf{A} \in \mathbb{R}^{m \times n}$第$i$行第$j$列元素为$(\mathbf{A})_{ij} = A_{ij}$

- **转置(Transpose):** $\mathbf{A}^{T}$, 有$(\mathbf{A}^{T})_{ij} = \mathbf{A}_{ji}$

    > - $(\mathbf{A} + \mathbf{B})^T = \mathbf{A}^T + \mathbf{B}^T$
    > - $(\mathbf{A}\mathbf{B})^T = \mathbf{B}^T \mathbf{A}^T$

- **方阵:** 对于$\mathbf{A} \in \mathbb{R}^{m \times n}$, 若$m=n$则称为n阶方阵. 用$\mathbf{I}_n$表示$n$阶单位阵

- **逆矩阵:** $\mathbf{A}$的逆矩阵$\mathbf{A}^{-1}$满足$\mathbf{A}\mathbf{A}^{-1} = \mathbf{A}^{-1}\mathbf{A} = I$

    > - $(\mathbf{A}^T)^{-1} = (\mathbf{A}^{-1})^{T}$
    > - $(\mathbf{A}\mathbf{B})^{-1} = \mathbf{B}^{-1}\mathbf{A}^{-1}$

- **矩阵的迹(Trace):** 对于$n$阶方阵$\mathbf{A}$, 迹为主对角线上元素之和. $tr(\mathbf{A}) = \sum^{n}_{i=1} \mathbf{A}_{ii}$

    > - $tr(\mathbf{A}^T) = tr(\mathbf{A})$
    > - $tr(\mathbf{A} + \mathbf{B}) = tr(\mathbf{A}) + tr(\mathbf{B})$
    > - $tr(\mathbf{AB}) = tr(\mathbf{BA})$
    > - $tr(\mathbf{ABC}) = tr(\mathbf{BCA}) = tr(\mathbf{CAB})$

- **行列式(Determinant):** $det(\mathbf{A}) = \sum_{\sigma \in S_n} par(\sigma)A_{1\sigma_{1}}A_{2\sigma_{2}}...A_{n\sigma_{n}}$, 其中$S_n$为所有的$n$阶排列(permutation)的集合, $par(\sigma)$取值为$1$或$-1$, 取决于$\sigma$排列中的逆序对数量(偶正奇负).

    > - $det(\mathbf{I}) = 1$
    > - $det(c\mathbf{A}) = c^ndet(\mathbf{A})$
    > - $det(\mathbf{A}^T) = det(\mathbf{A})$
    > - $det(\mathbf{AB}) = det(\mathbf{A})det(\mathbf{B})$
    > - $det(\mathbf{A^{-1}}) = det(\mathbf{A})^{-1}$
    > - $det(\mathbf{A}^n) = det(\mathbf{A})^n$

- **范数(Norm):** 