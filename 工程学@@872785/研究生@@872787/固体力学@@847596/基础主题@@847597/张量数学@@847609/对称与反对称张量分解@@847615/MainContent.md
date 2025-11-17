## 引言
在探索材料与[结构力学](@entry_id:276699)行为的宏伟画卷中，张量是描绘应力、应变与运动等物理量的通用语言。然而，一个原始的张量（如[速度梯度](@entry_id:261686)）往往混合了多种物理效应，使得直接解读其物理内涵变得困难。一个核心的挑战在于：我们如何从一个复杂的运动场中，精确地分离出材料真实的形状改变（变形）与整体的刚性旋转（自旋）？这种分离对于建立准确的材料[本构模型](@entry_id:174726)和理解[能量耗散](@entry_id:147406)至关重要。

本文正是为了解决这一根本问题，系统地介绍了二阶张量的[对称与反对称分解](@entry_id:204005)。通过这一强大的数学工具，我们将揭示隐藏在[张量代数](@entry_id:161671)结构背后的深刻物理意义。

本文将分为三个主要部分，引领读者逐步深入这一主题。在“**原理与机制**”一章中，我们将奠定坚实的数学基础，探讨分解的定义、唯一性、正交性及其几何解释。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示这一理论的强大威力，看它如何在运动学、能量学和本构理论中扮演核心角色，并触及其在计算科学和广义连续体理论中的延伸。最后，通过“**动手实践**”部分，你将有机会通过具体的计算问题，将理论知识转化为解决实际问题的能力。

让我们首先进入第一章，探索这一基本分解的原理与机制。

## 原理与机制

在连续介质力学中，张量是描述物理量（如应力、应变和运动）的核心数学工具。理解张量的[代数结构](@entry_id:137052)对于洞察其物理意义至关重要。[二阶张量](@entry_id:199780)最基本也是最重要的性质之一是它可以被唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分。本章将深入探讨这一分解的原理、其在[运动学](@entry_id:173318)中的物理解释，以及它在能量和[本构关系](@entry_id:186508)等领域的深刻应用。

### [二阶张量](@entry_id:199780)的对称/反对称分解

#### 定义与唯一性

任意一个[二阶张量](@entry_id:199780) $A$ 都可以表示为一个**[对称张量](@entry_id:148092) (symmetric tensor)** $S$ 和一个**[反对称张量](@entry_id:199349) (skew-symmetric tensor)**（或称[斜对称张量](@entry_id:199349)）$W$ 的和。一个张量 $S$ 如果等于其自身的转置 ($S = S^{\mathsf{T}}$)，则为[对称张量](@entry_id:148092)。一个张量 $W$ 如果等于其[转置](@entry_id:142115)的负值 ($W = -W^{\mathsf{T}}$)，则为[反对称张量](@entry_id:199349)。

给定任意张量 $A$，其分解形式为：
$A = S + W$

为了找出 $S$ 和 $W$，我们可以对上式进行[转置](@entry_id:142115)：
$A^{\mathsf{T}} = (S + W)^{\mathsf{T}} = S^{\mathsf{T}} + W^{\mathsf{T}} = S - W$

现在我们得到一个关于 $S$ 和 $W$ 的线性方程组：
1. $A = S + W$
2. $A^{\mathsf{T}} = S - W$

将两式相加，可以解出对称部分 $S$：
$A + A^{\mathsf{T}} = 2S \implies S = \frac{1}{2}(A + A^{\mathsf{T}})$

将第二式从第一式中减去，可以解出反对称部分 $W$：
$A - A^{\mathsf{T}} = 2W \implies W = \frac{1}{2}(A - A^{\mathsf{T}})$

这些表达式被称为张量 $A$ 的**对称部分 (symmetric part)** 和**反对称部分 (skew-symmetric part)**，通常分别记为 $\mathrm{sym}(A)$ 和 $\mathrm{skw}(A)$。这种分解是唯一的，因为任何一个既对称又反对称的张量 $T$（即 $T=T^{\mathsf{T}}$ 且 $T=-T^{\mathsf{T}}$）必然是零张量 ($T=-T \implies 2T=0 \implies T=0$) [@problem_id:2692697]。

在[标准正交基](@entry_id:147779)下，张量的分量表示为矩阵 $[A_{ij}]$。[转置](@entry_id:142115)操作对应于[矩阵转置](@entry_id:155858)，即 $(A^{\mathsf{T}})_{ij} = A_{ji}$。因此，对称和反对称部分的分量形式为 [@problem_id:2692710]：
$(A^{\mathrm{sym}})_{ij} = \frac{1}{2}(A_{ij} + A_{ji})$
$(A^{\mathrm{skw}})_{ij} = \frac{1}{2}(A_{ij} - A_{ji})$

从分量形式可以直观地验证其性质。例如，对于反对称部分，我们有 $(A^{\mathrm{skw}})_{ji} = \frac{1}{2}(A_{ji} - A_{ij}) = -\frac{1}{2}(A_{ij} - A_{ji}) = -(A^{\mathrm{skw}})_{ij}$，这正是反对称的定义。特别地，[反对称张量](@entry_id:199349)的对角[线元](@entry_id:196833)素恒为零，因为 $W_{ii} = -W_{ii} \implies W_{ii}=0$。

#### 正交性与几何解释

为了更深入地理解这种分解，我们可以引入张量空间的几何结构。[二阶张量](@entry_id:199780)的空间可以被赋予一个[内积](@entry_id:158127)，最常用的是 **Frobenius [内积](@entry_id:158127) (Frobenius inner product)**，定义为 [@problem_id:2692703]：
$\langle A, B \rangle = A:B = \mathrm{tr}(A^{\mathsf{T}}B)$

在分量形式下，这等价于所有分量乘积之和：$A:B = A_{ij}B_{ij}$（此处使用爱因斯坦求和约定）。这个[内积](@entry_id:158127)满足对称性、双线性和[正定性](@entry_id:149643)，因此它赋予了二阶张量空间一个欧几里得结构，使得我们可以讨论张量之间的“角度”和“长度”（范数）。由该[内积诱导的范数](@entry_id:201671)称为 Frobenius 范数：$\|A\|_{F} = \sqrt{A:A} = \sqrt{\mathrm{tr}(A^{\mathsf{T}}A)}$。

在此几何框架下，对称/反对称分解具有一个美妙的性质：它是**[正交分解](@entry_id:148020) (orthogonal decomposition)**。这意味着任意对称张量 $S$ 与任意[反对称张量](@entry_id:199349) $W$ 的 Frobenius [内积](@entry_id:158127)恒为零 [@problem_id:2692710]。证明如下：
$\langle S, W \rangle = S:W = S_{ij}W_{ij}$
由于 $S$ 是对称的 ($S_{ij}=S_{ji}$)，而 $W$ 是反对称的 ($W_{ij}=-W_{ji}$)，我们可以进行如下推导：
$S_{ij}W_{ij} = S_{ji}W_{ij}$
交换[哑指标](@entry_id:188070) $i$ 和 $j$：
$S_{ji}W_{ij} = S_{ij}W_{ji} = S_{ij}(-W_{ij}) = -S_{ij}W_{ij}$
因此，我们得到 $S_{ij}W_{ij} = -S_{ij}W_{ij}$，这意味着 $2 S_{ij}W_{ij} = 0$，故 $S:W = 0$。

这表明，所有[对称张量](@entry_id:148092)构成的[子空间](@entry_id:150286) ($\mathsf{Sym}$) 与所有[反对称张量](@entry_id:199349)构成的[子空间](@entry_id:150286) ($\mathsf{Skew}$) 在 Frobenius [内积](@entry_id:158127)下是正交的。由于任何张量都可以唯一地分解为这两个[子空间](@entry_id:150286)中元素的和，因此这两个[子空间](@entry_id:150286)是正交补的关系 [@problem_id:2692703]。

这种正交性带来两个重要的推论：
1.  **毕达哥拉斯定理 (Pythagorean Theorem)**：对于任意张量 $A$，其范数的平方等于其对称和反对称部分范数的平方和 [@problem_id:2692718]。
    $\|A\|_{F}^{2} = \|A^{\mathrm{sym}} + A^{\mathrm{skw}}\|_{F}^{2} = \langle A^{\mathrm{sym}} + A^{\mathrm{skw}}, A^{\mathrm{sym}} + A^{\mathrm{skw}} \rangle_{F} = \|A^{\mathrm{sym}}\|_{F}^{2} + \|A^{\mathrm{skw}}\|_{F}^{2} + 2\langle A^{\mathrm{sym}}, A^{\mathrm{skw}} \rangle_{F}$
    由于正交性 $\langle A^{\mathrm{sym}}, A^{\mathrm{skw}} \rangle_{F} = 0$，我们得到：
    $\|A\|_{F}^{2} = \|A^{\mathrm{sym}}\|_{F}^{2} + \|A^{\mathrm{skw}}\|_{F}^{2}$

2.  **最佳逼近 (Best Approximation)**：在所有对称张量中，$A^{\mathrm{sym}}$ 是在 Frobenius 范数意义下与 $A$ “最近”的张量。换句话说，$A^{\mathrm{sym}}$ 是 $A$ 在对称[子空间](@entry_id:150286) $\mathsf{Sym}$ 上的正交投影。最小化问题 $\min_{S \in \mathsf{Sym}} \|A - S\|_{F}$ 的唯一解是 $S = A^{\mathrm{sym}}$，并且最小距离的平方等于其反对称部分范数的平方：$\|A - A^{\mathrm{sym}}\|_{F}^{2} = \|A^{\mathrm{skw}}\|_{F}^{2}$ [@problem_id:2692718]。

### 运动学解释：变形与[刚体转动](@entry_id:191086)

对称/反对称分解的威力在[连续介质运动学](@entry_id:747813)中得到了最充分的体现。它能够将一个复杂的运动在局部拆分为纯粹的变形和纯粹的[刚体转动](@entry_id:191086)。

#### [速度梯度张量](@entry_id:270928)的分解

考虑一个连续体的运动，其速度场为 $\mathbf{v}(\mathbf{x}, t)$。**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)** $L$ 定义为速度场的空间梯度，$L = \nabla \mathbf{v}$，其分量为 $L_{ij} = \partial v_i / \partial x_j$。该张量描述了邻近[质点](@entry_id:186768)间的相对速度。

将[速度梯度张量](@entry_id:270928) $L$ 进行对称/反对称分解：
$L = D + W$
其中：
- $D = \frac{1}{2}(L + L^{\mathsf{T}})$ 是 $L$ 的对称部分，被称为 **率-变形张量 (rate-of-deformation tensor)** 或 **[拉伸张量](@entry_id:193200) (stretching tensor)**。
- $W = \frac{1}{2}(L - L^{\mathsf{T}})$ 是 $L$ 的反对称部分，被称为 **[自旋张量](@entry_id:187346) (spin tensor)** 或 **[涡量张量](@entry_id:189621) (vorticity tensor)**。

这个分解具有深刻的物理意义：张量 $D$ 描述了物质微元体形状和尺寸的变化率（即变形），而张量 $W$ 则描述了该微元体作为一个整体的刚性旋转速率（即自旋） [@problem_id:2693299]。

#### 纯刚体运动分析

为了验证上述物理解释，我们可以考察一种没有变形的特殊运动——纯刚体运动。一个刚体的[速度场](@entry_id:271461)可以表示为 $\mathbf{v}(\mathbf{x}) = \boldsymbol{\omega} \times \mathbf{x} + \mathbf{c}$，其中 $\boldsymbol{\omega}$ 是角速度矢量，$\mathbf{c}$ 是平移速度矢量，两者在空间上是常数。

利用 Levi-Civita 符号 $\epsilon_{ijk}$，[叉积](@entry_id:156672)可以写为 $(\boldsymbol{\omega} \times \mathbf{x})_i = \epsilon_{ijk}\omega_j x_k$。[速度梯度](@entry_id:261686)的分量为：
$L_{il} = \frac{\partial v_i}{\partial x_l} = \frac{\partial}{\partial x_l} (\epsilon_{ijk}\omega_j x_k + c_i) = \epsilon_{ijk}\omega_j \frac{\partial x_k}{\partial x_l} = \epsilon_{ijk}\omega_j \delta_{kl} = \epsilon_{ijl}\omega_j$

现在计算率-变形张量 $D$ 的分量：
$D_{il} = \frac{1}{2}(L_{il} + L_{li}) = \frac{1}{2}(\epsilon_{ijl}\omega_j + \epsilon_{lji}\omega_j)$
由于 Levi-Civita 符号的反对称性，$\epsilon_{lji} = -\epsilon_{ijl}$。因此：
$D_{il} = \frac{1}{2}(\epsilon_{ijl}\omega_j - \epsilon_{ijl}\omega_j) = 0$
这表明，对于纯[刚体运动](@entry_id:193355)，率-变形张量恒为零，这与刚体“不变形”的直观认识完全一致 [@problem_id:2692724]。

同时，[自旋张量](@entry_id:187346) $W$ 的分量为：
$W_{il} = \frac{1}{2}(L_{il} - L_{li}) = \frac{1}{2}(\epsilon_{ijl}\omega_j - \epsilon_{lji}\omega_j) = \frac{1}{2}(\epsilon_{ijl}\omega_j + \epsilon_{ijl}\omega_j) = \epsilon_{ijl}\omega_j = L_{il}$
这意味着在刚体运动中，[速度梯度](@entry_id:261686)完全由其反对称部分（[自旋张量](@entry_id:187346)）构成，即 $L=W$。

#### [反对称张量](@entry_id:199349)与轴矢

上述结果表明[自旋张量](@entry_id:187346) $W$ 与角速度矢量 $\boldsymbol{\omega}$ 之间存在直接联系。在三维空间中，任何一个[反对称张量](@entry_id:199349) $W$ 都与一个唯一的矢量——**轴矢 (axial vector)** $\boldsymbol{\omega}$——相对应。这种对应关系使得 $W$ 对任意矢量 $\mathbf{x}$ 的作用等价于其轴矢 $\boldsymbol{\omega}$ 与 $\mathbf{x}$ 的叉积 [@problem_id:2692695]。

具体来说，若 $\boldsymbol{\omega} = (\omega_1, \omega_2, \omega_3)^{\mathsf{T}}$，其对应的[反对称张量](@entry_id:199349) $W$ 的矩阵形式为：
$W = \begin{pmatrix} 0  -\omega_3  \omega_2 \\ \omega_3  0  -\omega_1 \\ -\omega_2  \omega_1  0 \end{pmatrix}$

我们可以通过直接计算来验证 $W\mathbf{x} = \boldsymbol{\omega} \times \mathbf{x}$ 这一关键恒等式。例如，计算结果向量的第一个分量：
$(W\mathbf{x})_1 = 0 \cdot x_1 - \omega_3 x_2 + \omega_2 x_3 = \omega_2 x_3 - \omega_3 x_2$
这恰好等于[叉积](@entry_id:156672) $(\boldsymbol{\omega} \times \mathbf{x})_1$ 的分量。对其他分量进行类似的计算也会得到相同的结果 [@problem_id:2692695]。

这个恒等式是理解[自旋张量](@entry_id:187346)物理意义的基石。它清楚地表明，速度梯度[张量的反对称部分](@entry_id:193562) $W$ 所描述的运动，正是一个[角速度](@entry_id:192539)为 $\boldsymbol{\omega} = \mathrm{axl}(W)$ 的瞬时刚体旋转。

### 在连续介质力学中的应用

将运动分解为变形和旋转的能力，在[连续介质力学](@entry_id:155125)的多个领域都有着至关重要的应用。

#### [主应变率](@entry_id:264248)与[主方向](@entry_id:276187)

率-变形张量 $D$ 是一个[对称张量](@entry_id:148092)。根据谱定理，任何实对称张量都具有实数[特征值](@entry_id:154894)和一组正交的[特征向量](@entry_id:151813)。$D$ 的[特征值](@entry_id:154894)被称为**[主应变率](@entry_id:264248) (principal strain rates)**，其对应的[特征向量](@entry_id:151813)给出了**[主方向](@entry_id:276187) (principal directions)**。

物理上，主方向是指在当前时刻，物质微元经历纯拉伸或压缩而没有[剪切变形](@entry_id:170920)的三个相互正交的方向。相应的[主应变率](@entry_id:264248)则量化了在这些方向上的拉伸或压缩速率。例如，如果在一个主方向上[主应变率](@entry_id:264248)为正，则沿该方向的物质线段正在伸长；如果为负，则正在缩短；如果为零，则长度瞬时不变 [@problem_id:2692722]。

考虑一个[速度梯度张量](@entry_id:270928) $A = \begin{pmatrix} 0  2  0\\ -2  1  0\\ 0  0  3 \end{pmatrix}$。其对称部分（率-变形张量）为：
$D = A^{\mathrm{sym}} = \frac{1}{2}(A + A^{\mathsf{T}}) = \begin{pmatrix} 0  0  0 \\ 0  1  0 \\ 0  0  3 \end{pmatrix}$
这是一个[对角矩阵](@entry_id:637782)，其[特征值](@entry_id:154894)（[主应变率](@entry_id:264248)）显然为 $\lambda_1=0$, $\lambda_2=1$, $\lambda_3=3$ ($\mathrm{s}^{-1}$)，对应的主方向是坐标轴方向 $\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3$。这表示该点的物质正在 $\mathbf{e}_3$ 方向以最快速率 ($3 \, \mathrm{s}^{-1}$) 拉伸，在 $\mathbf{e}_2$ 方向以较慢速率 ($1 \, \mathrm{s}^{-1}$) 拉伸，而在 $\mathbf{e}_1$ 方向长度保持不变 [@problem_id:2692722]。

#### [应力功率](@entry_id:182907)与能量耗散

**[应力功率](@entry_id:182907)密度 (stress power density)** $\mathcal{P}$ 是单位体积[内应力](@entry_id:193721)所做的功的速率，定义为柯西应力张量 $\boldsymbol{\sigma}$ 与[速度梯度张量](@entry_id:270928) $L$ 的[双点积](@entry_id:748648)：
$\mathcal{P} = \boldsymbol{\sigma} : L = \boldsymbol{\sigma} : (D+W) = \boldsymbol{\sigma} : D + \boldsymbol{\sigma} : W$

在经典（非极性）连续介质理论中，[角动量守恒](@entry_id:156798)定律要求柯西应力张量 $\boldsymbol{\sigma}$ 必须是对称的。正如我们已经证明的，一个[对称张量](@entry_id:148092)（如 $\boldsymbol{\sigma}$）与一个[反对称张量](@entry_id:199349)（如 $W$）的[双点积](@entry_id:748648)恒为零 [@problem_id:2691193]。因此，$\boldsymbol{\sigma} : W = 0$。

[应力功率](@entry_id:182907)密度表达式由此简化为：
$\mathcal{P} = \boldsymbol{\sigma} : D$

这个优美的结果揭示了一个深刻的物理事实：只有运动的**变形部分**（由 $D$ 描述）才会与应力耦合产生内功，而运动的**刚性旋转部分**（由 $W$ 描述）不产生内功。换言之，应力“看不见”纯粹的刚体旋转。因此，$\boldsymbol{\sigma}:D$ 通常被认为是材料内部的**[耗散功率](@entry_id:177328)密度**，它代表了转化为热量或用于产生塑性变形等不[可逆过程](@entry_id:276625)的能量。这也解释了为什么对于一个正在作刚体运动的物体（此时 $D=0$），其内部[应力功率](@entry_id:182907)为零 [@problem_id:2691193]。

#### 客观性与[本构关系](@entry_id:186508)

**[本构关系](@entry_id:186508) (constitutive relation)** 是描述材料物理性质的方程，例如应力如何依赖于变形。一个基本的物理要求是，[本构关系](@entry_id:186508)必须是**客观的 (objective)**，或者说是**物质标架无关的 (material frame-indifferent)**。这意味着材料的响应不应取决于观察者自身的[刚体运动](@entry_id:193355)。

考虑一个叠加在原运动上的任意刚体运动 $x^{\ast}(t) = Q(t)x(t) + c(t)$，其中 $Q(t)$ 是一个[旋转张量](@entry_id:191990)。客观性要求，在新的（带星号的）标架下观察到的物理张量应与原标架下的张量通过旋转 $Q$ 联系起来。例如，柯西[应力张量](@entry_id:148973)的变换法则是 $\boldsymbol{\sigma}^{\ast} = Q\boldsymbol{\sigma}Q^{\mathsf{T}}$。

可以证明，率-变形张量 $D$ 和[自旋张量](@entry_id:187346) $W$ 在这种叠加运动下的变换法则是不同的 [@problem_id:2692689]：
$D^{\ast} = QDQ^{\mathsf{T}}$  （这是一个客观的变换）
$W^{\ast} = QWQ^{\mathsf{T}} + \dot{Q}Q^{\mathsf{T}}$  （这不是一个客观的变换）

$W$ 的变换式中多出的一项 $\dot{Q}Q^{\mathsf{T}}$ 代表了观察者自身的旋转速率。由于 $W$ 的值依赖于观察者的运动，它不是一个客观的量度。因此，任何形如 $\boldsymbol{\sigma} = h(W)$ 的本构关系，除非 $h$ 是一个恒为零的函数，否则都将违反[客观性原理](@entry_id:185412)。因为对于一个静止的材料（$W=0$），一个旋转的观察者会测量到一个非零的 $W^{\ast} = \dot{Q}Q^{\mathsf{T}}$，并根据该本构律错误地计算出一个非零的应力。

相比之下，由于 $D$ 是客观的，形如 $\boldsymbol{\sigma} = g(D)$ 的[本构关系](@entry_id:186508)（若 $g$ 是一个[各向同性张量](@entry_id:195105)函数）可以是客观的。这从根本上解释了为什么材料的[本构模型](@entry_id:174726)总是将应力与变形（如 $D$）而不是与自旋（$W$）联系起来 [@problem_id:2692689]。

### 与其他[张量分解](@entry_id:173366)的关系

对称/反对称分解是众多[张量分解](@entry_id:173366)中的一种。另一个在固体力学中至关重要的是将[张量分解](@entry_id:173366)为体积部分和偏量部分。

#### 体积/偏[张量分解](@entry_id:173366)

任何[二阶张量](@entry_id:199780) $A$（特别是对称的应力或[应变张量](@entry_id:193332)）可以被分解为一个**球形张量 (spherical tensor)** 和一个**[偏张量](@entry_id:185837) (deviatoric tensor)** 的和。
$A = \mathrm{sph}(A) + \mathrm{dev}(A)$

球形张量正比于单位张量 $I$，代表了纯体积变化或[静水压力](@entry_id:275365)状态。它由 $A$ 的迹唯一确定：
$\mathrm{sph}(A) = \frac{1}{3}\mathrm{tr}(A)I$

[偏张量](@entry_id:185837)是 $A$ 减去其球形部分，其迹恒为零。它代表了保持体积不变的形状畸变或剪切应力状态。
$\mathrm{dev}(A) = A - \frac{1}{3}\mathrm{tr}(A)I$

这个分解也是正交的。可以证明，任何球形张量（形如 $kI$）与任何[偏张量](@entry_id:185837)（迹为零的张量）的 Frobenius [内积](@entry_id:158127)为零 [@problem_id:2692697], [@problem_id:2692703]。例如，对于一个对称张量 $S$ 的分解 $S = \mathrm{sph}(S) + \mathrm{dev}(S)$，其正交性验证如下：
$\langle \mathrm{sph}(S), \mathrm{dev}(S) \rangle = \langle \frac{1}{3}\mathrm{tr}(S)I, S - \frac{1}{3}\mathrm{tr}(S)I \rangle = \frac{1}{3}\mathrm{tr}(S) \mathrm{tr}(I^{\mathsf{T}}(S - \frac{1}{3}\mathrm{tr}(S)I)) = \frac{1}{3}\mathrm{tr}(S) \mathrm{tr}(S - \frac{1}{3}\mathrm{tr}(S)I)$
由于 $\mathrm{tr}(\mathrm{dev}(S)) = \mathrm{tr}(S - \frac{1}{3}\mathrm{tr}(S)I) = \mathrm{tr}(S) - \frac{1}{3}\mathrm{tr}(S)\mathrm{tr}(I) = \mathrm{tr}(S) - \frac{1}{3}\mathrm{tr}(S) \cdot 3 = 0$，故[内积](@entry_id:158127)为零。

在塑性理论中，像 von Mises 等效应变率这样的量，正是基于率-变形张量的偏量部分定义的，因为它隔离了引起[塑性流动](@entry_id:201346)的[剪切变形](@entry_id:170920)部分 [@problem_id:2693299]。

#### 完整的[正交分解](@entry_id:148020)

我们可以将这两种分解结合起来，将任意一个二阶张量 $A$ 分解为三个相互正交的部分：一个反对称部分，一个对称偏量部分，以及一个球形部分 [@problem_id:2692703]。
$A = \mathrm{skw}(A) + \mathrm{sym}(A) = \mathrm{skw}(A) + \mathrm{dev}(\mathrm{sym}(A)) + \mathrm{sph}(\mathrm{sym}(A))$

由于[反对称张量](@entry_id:199349)的迹为零，我们有 $\mathrm{tr}(A) = \mathrm{tr}(\mathrm{sym}(A))$。因此，完整的分解可以写为：
$A = \underbrace{\frac{1}{2}(A - A^{\mathsf{T}})}_{\text{反对称}} + \underbrace{\left(\frac{1}{2}(A + A^{\mathsf{T}}) - \frac{1}{3}\mathrm{tr}(A)I\right)}_{\text{对称偏量}} + \underbrace{\frac{1}{3}\mathrm{tr}(A)I}_{\text{球形}}$

这三个分量——反对称的、对称偏量的、球形的——构成了三个相互正交的[子空间](@entry_id:150286)。这提供了一个对[二阶张量](@entry_id:199780)空间 $\mathbb{R}^{3 \times 3}$ 的完整[正交分解](@entry_id:148020)。因此，张量范数的平方可以相应地分解为三部分之和：
$\|A\|_{F}^{2} = \|\mathrm{skw}(A)\|_{F}^{2} + \|\mathrm{dev}(\mathrm{sym}(A))\|_{F}^{2} + \|\mathrm{sph}(A)\|_{F}^{2}$

这个分解清晰地揭示了任意一个二阶张量所包含的不同物理效应：刚性旋转（反对称部分）、等体积变形（对称偏量部分）和体积变化（球形部分）。理解这些基本分解是掌握现代[连续介质力学](@entry_id:155125)的关键一步。