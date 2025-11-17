## 引言
在[量子信息科学](@entry_id:150091)的宏伟蓝图中，[量子比特](@entry_id:137928)的相干性和纠缠是其强大算力的根基。然而，任何量子系统都不可避免地与周围环境发生相互作用，导致信息的丢失和计算的错误。[振幅阻尼](@entry_id:146861)和[相位阻尼](@entry_id:147888)通道是描述这种相互作用最基本、也最普遍的两个物理模型，它们分别刻画了能量的耗散和相位的退相干。理解这两种噪声的原理和影响，是设计稳健的[量子技术](@entry_id:142946)、从[量子通信](@entry_id:138989)到[量子计算](@entry_id:142712)的关键一步。本文旨在填补理论模型与实际应用之间的知识鸿沟，系统性地解析这两种基本量子通道。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“**原理与机制**”一章中，我们将剖析振幅和[相位阻尼](@entry_id:147888)通道的数学结构，包括它们的 [Kraus 算符](@entry_id:144882)、对 Bloch 球的作用以及由 Lindblad 主方程描述的[连续动力学](@entry_id:268176)。随后，在“**应用与跨学科联系**”一章中，我们将展示这些理论模型如何应用于分析现实世界的问题，例如它们如何导致量子通信协议中纠缠的衰减，以及如何挑战[量子纠错码](@entry_id:266787)的性能，并探讨其在[量子计量学](@entry_id:138980)和[热力学](@entry_id:141121)中的作用。最后，在“**动手实践**”部分，你将有机会通过具体问题来巩固所学知识，亲手计算和分析噪声通道对[量子态](@entry_id:146142)的影响。让我们一同开启对量子世界中噪声与保真度之间博弈的探索之旅。

## 原理与机制

在本章中，我们将深入探讨两种基本且无处不在的量子噪声模型：**[振幅阻尼](@entry_id:146861) (amplitude damping)** 和 **[相位阻尼](@entry_id:147888) (phase damping)** 通道。这些通道为理解[开放量子系统](@entry_id:138632)中的耗散（能量损失）和退相干（相干性损失）提供了基础。我们将首先分别阐述它们的物理动机和数学描述，然后研究它们的组合效应，并最终将我们的讨论扩展到一些更高级的主题，如与环境的信息交换和[非马尔可夫动力学](@entry_id:142796)。

### [振幅阻尼](@entry_id:146861)通道

[振幅阻尼](@entry_id:146861)通道是描述量子系统[能量耗散](@entry_id:147406)到其环境中的基本模型。最典型的例子是处于[激发态](@entry_id:261453)的原子通过[自发辐射](@entry_id:140032)[光子](@entry_id:145192)而弛豫到[基态](@entry_id:150928)。这个过程通常被称为 **$T_1$ 弛豫**。假设环境处于零温度，因此它只能吸收能量而不能提供能量。

#### [Kraus 算符](@entry_id:144882)表示

对于一个[量子比特](@entry_id:137928)，[振幅阻尼](@entry_id:146861)通道 $\mathcal{E}_{AD}(\gamma)$ 的作用可以用一组 **[Kraus 算符](@entry_id:144882)** $\{E_k\}$ 来描述。其演化由[算符和表示](@entry_id:140073)给出：$\mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger$。对于[振幅阻尼](@entry_id:146861)，我们有两个 [Kraus 算符](@entry_id:144882) [@problem_id:45914]：
$$
E_0 = \begin{pmatrix} 1  0 \\ 0  \sqrt{1-\gamma} \end{pmatrix}, \quad E_1 = \begin{pmatrix} 0  \sqrt{\gamma} \\ 0  0 \end{pmatrix}
$$
这里，$\gamma \in [0, 1]$ 是**阻尼参数**，表示[量子比特](@entry_id:137928)从[激发态](@entry_id:261453) $|1\rangle$ 衰变到[基态](@entry_id:150928) $|0\rangle$ 的概率。从算符的形式可以看出，$E_1$ 算符将态 $|1\rangle$ 映射到 $|0\rangle$，模拟了能量的损失。$E_0$ 算符则描述了[量子比特](@entry_id:137928)保持在 $|1\rangle$ 态的概率幅衰减。这两个算符满足[完备性关系](@entry_id:139077) $E_0^\dagger E_0 + E_1^\dagger E_1 = I$，确保了该映射是保迹的。

若将此通道作用于一个一般的单[量子比特](@entry_id:137928)[密度矩阵](@entry_id:139892) $\rho = \begin{pmatrix} \rho_{00}  \rho_{01} \\ \rho_{10}  \rho_{11} \end{pmatrix}$，我们得到：
$$
\mathcal{E}_{AD}(\rho) = E_0 \rho E_0^\dagger + E_1 \rho E_1^\dagger = \begin{pmatrix} \rho_{00} + \gamma \rho_{11}  \rho_{01}\sqrt{1-\gamma} \\ \rho_{10}\sqrt{1-\gamma}  (1-\gamma)\rho_{11} \end{pmatrix}
$$
从这个结果可以清楚地看到：
1.  布居数（对角元素）发生变化：处于[激发态](@entry_id:261453) $|1\rangle$ 的布居数 $\rho_{11}$ 以因子 $(1-\gamma)$ 衰减，这部分损失的布居数 $\gamma\rho_{11}$ 被加到了[基态](@entry_id:150928) $|0\rangle$ 的布居数 $\rho_{00}$ 上。
2.  相干性（非对角元素）发生衰减：非对角项 $\rho_{01}$ 和 $\rho_{10}$ 以因子 $\sqrt{1-\gamma}$ 减少。
3.  [基态](@entry_id:150928) $|0\rangle$ 是一个[不动点](@entry_id:156394)：如果系统初始处于 $\rho = |0\rangle\langle 0|$，则 $\mathcal{E}_{AD}(|0\rangle\langle 0|) = |0\rangle\langle 0|$。这是符合物理直觉的，因为在零温环境下，[基态](@entry_id:150928)无法再损失能量。

#### Bloch 球表示

量子通道对单[量子比特](@entry_id:137928)态的作用可以通过它如何变换 **Bloch 球** 来进行可视化。一个态 $\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})$ 由 Bloch 向量 $\vec{r} = (r_x, r_y, r_z)$ 唯一确定。[振幅阻尼](@entry_id:146861)通道将输入向量 $\vec{r}$ 变换为一个新的向量 $\vec{r}'$，这是一个[仿射变换](@entry_id:144885) [@problem_id:45838] [@problem_id:45810]：
$$
r'_x = \sqrt{1-\gamma} r_x \\
r'_y = \sqrt{1-\gamma} r_y \\
r'_z = (1-\gamma) r_z + \gamma
$$
这个变换有两个效果：首先，Bloch 球在 $x$ 和 $y$ 方向上以 $\sqrt{1-\gamma}$ 的比例收缩，在 $z$ 方向上以 $(1-\gamma)$ 的比例收缩。其次，整个球体沿 $z$ 轴正方向移动了 $\gamma$ 的距离。最终，初始的单位球体被映射到一个位于其内部的、中心在 $(0, 0, \gamma)$ 的较小[椭球体](@entry_id:165811)。所有状态最终都会向代表[基态](@entry_id:150928) $|0\rangle$ 的北极点 $(0,0,1)$ 移动。

一个具象化的例子是考察该通道对 Bloch 球赤道面上 $x-z$ 平面内的[大圆](@entry_id:268970)（即满足 $r_y=0$ 和 $r_x^2 + r_z^2 = 1$ 的所有[纯态](@entry_id:141688)）的作用。可以证明，这个圆被映射到一个椭圆。计算该椭圆的**[偏心率](@entry_id:266900) (eccentricity)**，可以发现它恰好等于 $\sqrt{\gamma}$，这直观地将几何形变与物理阻尼参数联系起来 [@problem_id:45838]。

#### Lindblad [主方程](@entry_id:142959)

当阻尼过程随时间连续发生时，其动力学由 **Lindblad 主方程** 描述。对于一个随时间变化的衰减率 $\Gamma(t)$，方程形式为 $\frac{d\rho}{dt} = \mathcal{L}_t(\rho)$。对于恒定的衰减率 $\Gamma$，[振幅阻尼](@entry_id:146861)的 Lindblad 生成元 $\mathcal{L}_{AD}$ 为：
$$
\mathcal{L}_{AD}(\rho) = \Gamma \left( \sigma_- \rho \sigma_+ - \frac{1}{2} \{\sigma_+ \sigma_-, \rho\} \right)
$$
其中 $\sigma_+ = |0\rangle\langle 1|$ 和 $\sigma_- = |1\rangle\langle 0|$ 是泡利[升降算符](@entry_id:197899)，$\{\cdot, \cdot\}$ 是[反对易子](@entry_id:139754)。这个方程描述了密度矩阵随时间的[微分](@entry_id:158718)演化。例如，我们可以用它来计算一个初始处于叠加态 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 的[量子比特](@entry_id:137928)的相干项 $\langle\sigma_x(t)\rangle$ 的演化。可以发现，相干项随时间指数衰减，其衰减速率由 $\Gamma$ 决定 [@problem_id:45867]。

在希森堡图像中，算符（可观测量）的演化由对偶生成元 $\mathcal{L}^\dagger$ 决定。对于[振幅阻尼](@entry_id:146861)，其作用在算符 $A$ 上为 $\mathcal{L}^\dagger(A) = \Gamma (\sigma_+ A \sigma_- - \frac{1}{2}\{\sigma_+\sigma_-, A\})$。通过分析 $\mathcal{L}^\dagger$ 的本征算符和[本征值](@entry_id:154894)，我们可以深入理解动力学的模式 [@problem_id:45944]。

### [相位阻尼](@entry_id:147888)通道

与能量耗散不同，[相位阻尼](@entry_id:147888)（或称**退相干 (dephasing)**）描述了量子系统在不与环境[交换能](@entry_id:137069)量的情况下，其叠加态中不同成分之间相位关系的损失。这可以想象成系统受到了环境的“测量”但没有发生能级跃迁，例如通过[弹性散射](@entry_id:152152)过程。这种过程通常与 **$T_2$ 弛豫** 有关。

#### [Kraus 算符](@entry_id:144882)表示

[相位阻尼](@entry_id:147888)通道 $\mathcal{E}_{PD}(\lambda)$ 的一种常见 [Kraus 算符](@entry_id:144882)表示为 [@problem_id:45865]：
$$
E_0 = \sqrt{1-p} I, \quad E_1 = \sqrt{p} \sigma_z
$$
其中 $p$ 是发生相位翻转的概率。为了与连续时间模型联系，通常使用参数 $\lambda$ 定义通道 $\mathcal{E}_{PD}(\rho) = (1-\lambda) \rho + \lambda \sigma_z \rho \sigma_z$。这两种形式是等价的。

将此通道作用于[密度矩阵](@entry_id:139892) $\rho = \begin{pmatrix} \rho_{00}  \rho_{01} \\ \rho_{10}  \rho_{11} \end{pmatrix}$：
$$
\mathcal{E}_{PD}(\rho) = \begin{pmatrix} \rho_{00}  (1-2\lambda)\rho_{01} \\ (1-2\lambda)\rho_{10}  \rho_{11} \end{pmatrix}
$$
我们观察到：
1.  布居数（对角元素）保持不变。这印证了没有能量交换的物理图像。
2.  [相干性](@entry_id:268953)（非对角元素）以因子 $(1-2\lambda)$ 衰减。这正是相位信息的损失。

#### Bloch 球与超算符表示

在 Bloch 球图像中，[相位阻尼](@entry_id:147888)通道的变换非常直观 [@problem_id:45801]：
$$
r'_x = (1-\lambda') r_x \\
r'_y = (1-\lambda') r_y \\
r'_z = r_z
$$
（这里的 $\lambda'$ 与上面定义的形式略有不同，但效果相同）。Bloch 球沿 $x$ 和 $y$ 方向收缩，但 $z$ 方向保持不变。这意味着整个球体被“压扁”成一个沿 $z$ 轴的椭球体。任何初始态的 Bloch 向量都会被投影到 $z$ 轴上。

理解这种变换的另一种方式是通过**超算符 (superoperator)** 的视角。量子通道是作用于算符空间上的[线性映射](@entry_id:185132)。我们可以选择泡利矩阵 $\{I, \sigma_x, \sigma_y, \sigma_z\}$ 作为算符空间的基。一个有趣的练习是考察[相位阻尼](@entry_id:147888)通道对这些基算符的作用 [@problem_id:45865]。我们会发现，这些[泡利算符](@entry_id:144061)本身就是该超算符的**本征算符**：
*   $\mathcal{E}_{PD}(I) = I$ ([本征值](@entry_id:154894)为 1)
*   $\mathcal{E}_{PD}(\sigma_z) = \sigma_z$ ([本征值](@entry_id:154894)为 1)
*   $\mathcal{E}_{PD}(\sigma_x) = (1-2\lambda)\sigma_x$ ([本征值](@entry_id:154894)为 $1-2\lambda$)
*   $\mathcal{E}_{PD}(\sigma_y) = (1-2\lambda)\sigma_y$ ([本征值](@entry_id:154894)为 $1-2\lambda$)

这些[本征值](@entry_id:154894)直接对应于 Bloch 向量各分量的缩放因子。超算符的[行列式](@entry_id:142978)，即[本征值](@entry_id:154894)的乘积 $(1-2\lambda)^2$，量化了通道对算符“体积”的改变 [@problem_id:45865]。

#### Lindblad [主方程](@entry_id:142959)与纯度衰减

[相位阻尼](@entry_id:147888)的连续时间演化由 Lindblad 主方程描述，其生成元为 $\mathcal{L}_{PD}(\rho) = \Gamma (\sigma_z \rho \sigma_z - \rho)$，其中 $\Gamma$ 是[退相干](@entry_id:145157)速率。这个方程只影响非对角元，$\dot{\rho}_{01} = -2\Gamma \rho_{01}$。

我们可以利用这个方程来研究[量子态](@entry_id:146142)**纯度 (purity)** $P = \text{Tr}(\rho^2)$ 的演化。纯度是衡量[态混合](@entry_id:148060)程度的指标，纯[态的纯度](@entry_id:185476)为1。对于一个初始处于 $|+\rangle$ 态的[量子比特](@entry_id:137928)，其初始纯度为1。在[相位阻尼](@entry_id:147888)作用下，其非对角元指数衰减，导致纯度也随之下降。可以精确计算出纯度从1衰减到特定值（例如 $3/4$）所需的时间 [@problem_id:45790]。

### 通道的组合与推广

在现实世界中，量子系统常常同时受到多种噪声过程的影响。我们可以通过组合基本通道来构建更复杂的[噪声模型](@entry_id:752540)。

#### 通道的组合

通道的组合主要有两种方式：**级联 (concatenation)** 和 **凸组合 (convex combination)**。

*   **级联**：指一个通道接着另一个通道作用，即 $\mathcal{E} = \mathcal{E}_2 \circ \mathcal{E}_1$。一个重要的性质是，某些通道家族在级联下是封闭的。例如，将一个[振幅阻尼](@entry_id:146861)通道 $\mathcal{E}_{AD}(\gamma)$ 自身级联一次，得到的复合通道 $\mathcal{E}_{AD}(\gamma) \circ \mathcal{E}_{AD}(\gamma)$ 仍然是一个[振幅阻尼](@entry_id:146861)通道，只是其有效阻尼参数变为 $\gamma_{eff} = 2\gamma - \gamma^2$ [@problem_id:45914]。通道的顺序通常是重要的，即 $\mathcal{E}_2 \circ \mathcal{E}_1 \neq \mathcal{E}_1 \circ \mathcal{E}_2$。

*   **[凸组合](@entry_id:635830)**：指以一定概率应用某个通道，即 $\mathcal{E} = p\mathcal{E}_1 + (1-p)\mathcal{E}_2$。这代表了系统可能经历不同物理过程的经典不确定性。例如，一个通道以概率 $p$ 是[振幅阻尼](@entry_id:146861)，以概率 $1-p$ 是[相位阻尼](@entry_id:147888)。我们可以分析这种混合通道如何改变 Bloch 球的体积 [@problem_id:45810]。

#### [复合动力学](@entry_id:192159)与弛豫时间

当[振幅阻尼](@entry_id:146861)和[相位阻尼](@entry_id:147888)过程同时独立发生时，它们的 Lindblad 生成元可以直接相加：$\mathcal{L}_{total} = \mathcal{L}_{AD} + \mathcal{L}_{PD}$ [@problem_id:45885] [@problem_id:45867]。这使得我们能够分析组合效应。

对非对角元 $\rho_{01}$ 的演化方程变为：
$$
\frac{d\rho_{01}}{dt} = (\mathcal{L}_{AD}(\rho) + \mathcal{L}_{PD}(\rho))_{01} = -\frac{\Gamma_1}{2}\rho_{01} - \Gamma_\phi \rho_{01} = -\left(\frac{\Gamma_1}{2} + \Gamma_\phi\right)\rho_{01}
$$
其中 $\Gamma_1$ 是[振幅阻尼](@entry_id:146861)速率，$\Gamma_\phi$ 是纯[相位阻尼](@entry_id:147888)速率。非对角元的衰减速率因此是两者贡献之和。这直接引出了核[磁共振](@entry_id:143712)等领域中著名的**横向弛豫时间 $T_2$** 和**纵向[弛豫时间](@entry_id:191572) $T_1$** 的关系。$T_1$ 与[能量弛豫](@entry_id:136820)（[振幅阻尼](@entry_id:146861)）相关，$\Gamma_1 = 1/T_1$。$T_2$ 与总的[相干性](@entry_id:268953)损失相关，其衰减速率为 $1/T_2$。从上式可知：
$$
\frac{1}{T_2} = \frac{1}{2T_1} + \frac{1}{T_\phi}
$$
其中 $T_\phi = 1/\Gamma_\phi$ 是纯[退相干时间](@entry_id:154396)。这个公式明确指出，[能量弛豫](@entry_id:136820)（$T_1$ 过程）本身也会导致[相干性](@entry_id:268953)损失，对 $T_2$ 有贡献 [@problem_id:45909] [@problem_id:45867]。

#### 广义[振幅阻尼](@entry_id:146861)与热环境

标准的[振幅阻尼](@entry_id:146861)模型假设环境处于零温。**广义[振幅阻尼](@entry_id:146861) (Generalized Amplitude Damping, GAD)** 通道将此模型推广到有限温度的[热库](@entry_id:143608)。在有限温度下，环境不仅能吸收能量，还能向系统提供能量，导致从 $|0\rangle$ 到 $|1\rangle$ 的激发过程。

GAD 通道由四个 [Kraus 算符](@entry_id:144882)描述，并依赖于一个与热库温度相关的参数 $p = (N+1)/(2N+1)$，其中 $N$ 是环境中[热激发](@entry_id:275697)的平均数量 [@problem_id:45854]。当 $N=0$ ($p=1$) 时，GAD 通道退化为标准[振幅阻尼](@entry_id:146861)通道。

一个关键区别在于通道的**[不动点](@entry_id:156394) (fixed point)**，即满足 $\mathcal{E}(\rho_{fix}) = \rho_{fix}$ 的状态。对于标准[振幅阻尼](@entry_id:146861)，唯一[不动点](@entry_id:156394)是[基态](@entry_id:150928) $|0\rangle\langle 0|$ [@problem_id:45824]。而对于 GAD 通道（或者更一般地，一个[振幅阻尼](@entry_id:146861)和振幅泵浦的混合通道），唯一[不动点](@entry_id:156394)是一个对角[混合态](@entry_id:141568)，其布居数[分布](@entry_id:182848)对应于系统的热平衡态 [@problem_id:45900] [@problem_id:45854]。该[不动点](@entry_id:156394)的纯度 $P = \frac{2N^2+2N+1}{4N^2+4N+1}$，仅当 $N=0$ 时才为1 [@problem_id:45854]。我们可以通过计算零温和有限温度通道输出态之间的**[迹距离](@entry_id:142668) (trace distance)** 来量化温度效应的显著性 [@problem_id:45938]。

### 信息论性质与高等专题

除了作为物理过程的模型，量子通道还具有深刻的信息论含义。

#### Stinespring 膨胀与熵交换

**Stinespring 膨胀定理** 指出，任何量子通道 $\mathcal{E}$ 都可以被看作是一个更大的封闭系统（系统 S + 环境 E）上[幺正演化](@entry_id:145020) $U_{SE}$ 的结果。即，如果我们从一个纯态环境 $|0\rangle_E$ 开始，那么通道作用可以写成：
$$
\mathcal{E}(\rho_S) = \text{Tr}_E (U_{SE} (\rho_S \otimes |0\rangle_E\langle 0|_E) U_{SE}^\dagger)
$$
这个观点将抽象的通道与具体的物理交互联系起来。例如，[振幅阻尼](@entry_id:146861)通道可以由一个在系统和环境比特之间交换激发的幺正算符导出 [@problem_id:45946]。

这种系统-环境的交互通常会导致两者之间产生纠缠，这意味着信息从系统“泄漏”到了环境。**熵交换 (entropy exchange)** $S_{exch}$ 是量化这种信息流失的工具。它被定义为交互后环境状态的[冯·诺依曼熵](@entry_id:143216)。对于给定的初始态 $\rho$ 和 [Kraus 算符](@entry_id:144882) $\{E_k\}$，熵交换可以通过计算一个矩阵 $W$ 的熵来得到，其中 $W_{kl} = \text{Tr}(E_k \rho E_l^\dagger)$。通过对一般[纯态](@entry_id:141688)计算[振幅阻尼](@entry_id:146861)和[相位阻尼](@entry_id:147888)通道的熵交换，我们可以看到信息损失是如何依赖于初始态和阻尼参数的 [@problem_id:45836] [@problem_id:45846]。

#### 通道的对称化：[泡利旋转](@entry_id:138667)

在处理复杂的未知噪声时，一种强大的技术是**[泡利旋转](@entry_id:138667) ([Pauli twirling](@entry_id:138667))**。这是一个通过对[泡利群](@entry_id:136414)上的所有幺正算符进行平均来对称化一个量子通道的过程。对于单[量子比特](@entry_id:137928)，旋转后的通道 $\mathcal{E}_{twirl}$ 定义为：
$$
\mathcal{E}_{twirl}(\rho) = \frac{1}{4} \sum_{k \in \{I,X,Y,Z\}} \sigma_k \mathcal{E}(\sigma_k \rho \sigma_k) \sigma_k
$$
一个显著的结果是，任何单[量子比特](@entry_id:137928)通道在[泡利旋转](@entry_id:138667)后都会变成一个**泡利通道**，其 [Kraus 算符](@entry_id:144882)本身就是泡利矩阵。对于许多非对称的通道，如[振幅阻尼](@entry_id:146861)和[相位阻尼](@entry_id:147888)，[泡利旋转](@entry_id:138667)会将其简化为一个简单的**退极化通道 (depolarizing channel)** $\mathcal{E}_{depol}(\rho) = (1-p)\rho + p \frac{I}{2}$。我们可以精确地计算出由[振幅阻尼](@entry_id:146861) [@problem_id:45829] 或[相位阻尼](@entry_id:147888) [@problem_id:45801] 得到的等效退极化参数 $p$。

#### 纠缠破坏通道

一类特别的通道被称为**纠缠破坏 (entanglement-breaking)** 通道。无论输入态与另一个系统存在何种纠缠，经过这种通道作用后，输出态总是可分离的。判断一个通道是否是纠缠破坏的，一个关键工具是其 **Choi 矩阵** $\chi_\mathcal{E} = (I \otimes \mathcal{E})(|\Phi^+\rangle\langle\Phi^+|)$，其中 $|\Phi^+\rangle$ 是一个最大[纠缠态](@entry_id:152310)。一个通道是纠缠破坏的，当且仅当其 Choi 矩阵是可分离的。对于两个[量子比特](@entry_id:137928)的系统，可分离性等价于在[部分转置](@entry_id:136776)下保持正定（PPT准则）。我们可以利用这个准则来推导复合通道，例如级联的振幅和[相位阻尼](@entry_id:147888)通道，成为纠缠破坏通道的条件 [@problem_id:45874]。

#### [非马尔可夫动力学](@entry_id:142796)

我们目前讨论的 Lindblad 方程描述的是**马尔可夫 (Markovian)** 过程，其特点是信息单向地从系统流向环境，环境没有“记忆”。然而，当系统与一个结构化的、有记忆效应的环境耦合时，可能出现**非马尔可夫 (non-Markovian)** 动力学。在这种情况下，信息可以暂时从环境“回流”到系统，表现为相干性的短暂恢复。

在时间局域的（time-local）主方程 $\frac{d\rho}{dt} = \mathcal{L}_t(\rho)$ 的框架下，非马尔可夫性的一个标志是生成元 $\mathcal{L}_t$ 中的某些衰减率暂时变为负值。例如，如果[振幅阻尼](@entry_id:146861)的衰减率 $\Gamma(t)$ 在某些时间区间内为负，那么演化就是**CP-不可分的 (CP-indivisible)**，即非马尔可夫的 [@problem_id:45786] [@problem_id:45929]。我们可以通过积分衰减率为负的时间段来量化非马尔可夫性的总量。这种行为在物理上源于环境内部的动力学，例如当一个[量子比特](@entry_id:137928)与一个[量子自旋链](@entry_id:146460)的边界耦合时，[自旋链](@entry_id:139648)内部的激发传播和反射就会导致信息的回流 [@problem_id:45866]。