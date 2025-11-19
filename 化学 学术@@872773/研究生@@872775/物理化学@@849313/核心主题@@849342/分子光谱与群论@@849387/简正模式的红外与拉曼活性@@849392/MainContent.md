## 引言

[振动光谱](@entry_id:176233)，作为探测分子结构与动力学的核心工具，能够揭示原子间微妙的集体运动。然而，一个根本性的问题是：为什么有些[振动](@entry_id:267781)模式能在红外[光谱](@entry_id:185632)中被观测到，有些则出现在拉曼[光谱](@entry_id:185632)中，还有些两者皆可或两者皆无？这一问题的答案深植于量子力学与[分子对称性](@entry_id:202199)的基本原理之中，理解它，是精通[振动光谱学](@entry_id:140278)的关键。

本文旨在系统性地阐明分子简正[振动](@entry_id:267781)模式的红外（IR）与拉曼（Raman）活性的物理机制与[选择定则](@entry_id:140784)。我们将跨越三个核心章节，引领读者从基础理论走向前沿应用。
*   在“原理与机制”一章中，我们将从经典力学的简正模式分析出发，建立起基于偶极矩和[极化率](@entry_id:143513)变化的[量子力学选择定则](@entry_id:151895)，并引入群论这一强大工具来利用对称性进行预测。
*   接着，在“应用与跨学科连接”一章，我们将展示这些理论如何在化学、物理学和[材料科学](@entry_id:152226)的真实场景中大放异彩，用于解析[分子结构](@entry_id:140109)、探测[晶格动力学](@entry_id:145448)以及研究表面现象。
*   最后，通过一系列“动手实践”环节，您将有机会亲手应用所学知识，解决具体的[物理化学](@entry_id:145220)问题，从而加深对核心概念的理解。

通过本次学习，您将能够不仅“知其然”（知道哪些[振动](@entry_id:267781)是活性的），更能“知其所以然”（理解其背后的物理与对称性根源）。

## 原理与机制

本章旨在深入探讨分子振动在红外（IR）和拉曼（Raman）[光谱](@entry_id:185632)中表现出活性的物理原理与基本机制。在前一章介绍性内容的基础上，我们将从经典力学和量子力学的基本原理出发，系统地建立[振动光谱](@entry_id:176233)的选择定则。我们将阐明这些定则如何源于分子的对称性以及其电学性质（如偶极矩和[极化率](@entry_id:143513)）随[振动](@entry_id:267781)发生的变化。通过对这些原理的剖析，我们将能够预测并解释特定分子振动的[光谱](@entry_id:185632)活性。

### [振动](@entry_id:267781)的力学基础：[简正模](@entry_id:139640)式

从经典力学的角度看，一个[多原子分子](@entry_id:268323)可以被视为一个由质点（[原子核](@entry_id:167902)）通过弹簧（化学键）连接而成的体系。在平衡构型附近，分子的势能 $V$ 可以近似为原子位移的二次函数，而动能 $T$ 则是速度的二次函数。若用一个包含所有 $N$ 个原子在笛卡尔坐标中位移的 $3N$ 维列向量 $\Delta \mathbf{r}$ 来描述分子的[振动](@entry_id:267781)，其动能和[势能](@entry_id:748988)可以表示为：

$$
T = \frac{1}{2} \dot{\Delta \mathbf{r}}^{\mathsf{T}} \mathbf{M} \dot{\Delta \mathbf{r}}
$$

$$
V = \frac{1}{2} \Delta \mathbf{r}^{\mathsf{T}} \mathbf{K} \Delta \mathbf{r}
$$

这里，$\dot{\Delta \mathbf{r}}$ 是速度向量，$\mathbf{M}$ 是一个对角的[质量矩阵](@entry_id:177093)，$\mathbf{K}$ 是[力常数](@entry_id:156420)矩阵（Hessian矩阵），它描述了[原子核](@entry_id:167902)偏离平衡位置时恢复力的大小。

通常情况下，$\mathbf{K}$ 矩阵并非对角阵，这意味着不同原子的运动是相互耦合的，使得整个体系的[运动方程](@entry_id:170720)极为复杂。为了简化这个问题，我们需要找到一组新的坐标，在这组坐标下，动能和[势能矩阵](@entry_id:178016)能够[同时对角化](@entry_id:196036)。这样，分子复杂的耦合[振动](@entry_id:267781)就可以被分解为一系列相互独立的、简谐的集体运动模式，这些模式被称为**[简正模](@entry_id:139640)式**（normal modes）。

这个数学过程 [@problem_id:2645733] 分为两步。首先，引入[质量加权坐标](@entry_id:164904) $\mathbf{q} = \mathbf{M}^{1/2} \Delta \mathbf{r}$，这一变换可以使动能项[对角化](@entry_id:147016)，形式变为 $T = \frac{1}{2} \dot{\mathbf{q}}^{\mathsf{T}} \dot{\mathbf{q}}$。接着，在[质量加权坐标](@entry_id:164904)下，[势能](@entry_id:748988)变为 $V = \frac{1}{2} \mathbf{q}^{\mathsf{T}} \mathbf{K}' \mathbf{q}$，其中 $\mathbf{K}' = \mathbf{M}^{-1/2} \mathbf{K} \mathbf{M}^{-1/2}$ 是质量加权力常数矩阵。由于 $\mathbf{K}'$ 是[实对称矩阵](@entry_id:192806)，它可以通过一个正交变换对角化。求解 $\mathbf{K}'$ 的[本征值](@entry_id:154894)和[本征向量](@entry_id:151813)，即 $\mathbf{K}' \mathbf{L} = \mathbf{L} \mathbf{\Lambda}$，其中 $\mathbf{\Lambda}$ 是由[本征值](@entry_id:154894) $\lambda_k$ 构成的[对角矩阵](@entry_id:637782)，$\mathbf{L}$ 的列是对应的[本征向量](@entry_id:151813)。

最后，我们定义**[简正坐标](@entry_id:143194)**（normal coordinates）$\mathbf{Q}$，使得 $\mathbf{q} = \mathbf{L} \mathbf{Q}$。在这组坐标下，分子的[振动](@entry_id:267781)[哈密顿量](@entry_id:172864)被完全解耦：

$$
H = T + V = \frac{1}{2} \sum_{k} \dot{Q}_k^2 + \frac{1}{2} \sum_{k} \lambda_k Q_k^2
$$

每个[简正坐标](@entry_id:143194) $Q_k$ 描述了一个独立的简谐[振动](@entry_id:267781)，其[振动频率](@entry_id:199185)为 $\omega_k = \sqrt{\lambda_k}$。从最初的笛卡尔坐标到[简正坐标](@entry_id:143194)的完整变换关系为：

$$
\Delta \mathbf{r} = \mathbf{M}^{-\frac{1}{2}} \mathbf{L} \mathbf{Q}
$$

这一关系是理解[分子振动](@entry_id:140827)[光谱](@entry_id:185632)的核心，因为它将微观的原子位移与宏观的、可被[光谱](@entry_id:185632)探测的[集体振动模](@entry_id:160059)式联系了起来。

### 红外[光谱](@entry_id:185632)：变化偶极矩的选择定则

当[电磁波](@entry_id:269629)与[分子相互作用](@entry_id:263767)时，如果光的[振荡](@entry_id:267781)[电场](@entry_id:194326)能够与分子的某种[振荡](@entry_id:267781)电学性质耦合，就可能发生能量吸收。在红外[光谱](@entry_id:185632)区域，这种耦合主要是通过分子的[电偶极矩](@entry_id:178520) $\boldsymbol{\mu}$ 实现的。

从量子力学角度看，从初态 $|\Psi_i\rangle$ 到末态 $|\Psi_f\rangle$ 的跃迁强度正比于**跃迁偶极矩**（transition dipole moment）积分模的平方，$|\boldsymbol{\mu}_{fi}|^2 = |\langle \Psi_f | \boldsymbol{\mu} | \Psi_i \rangle|^2$。对于振动光谱，我们关心的是[振动能级](@entry_id:193001)的跃迁。在[谐振子近似](@entry_id:268588)下，[振动](@entry_id:267781)[基态](@entry_id:150928)（$v=0$）到第一[激发态](@entry_id:261453)（$v=1$）的跃迁被称为**[基频](@entry_id:268182)跃迁**。

为了导出[选择定则](@entry_id:140784)，我们将[分子偶极矩](@entry_id:152656) $\boldsymbol{\mu}$ 在平衡构型附近按[简正坐标](@entry_id:143194) $Q_k$ 进行泰勒展开 [@problem_id:2645646]：

$$
\boldsymbol{\mu}(\mathbf{Q}) = \boldsymbol{\mu}_0 + \sum_{k} \left( \frac{\partial \boldsymbol{\mu}}{\partial Q_k} \right)_0 Q_k + \frac{1}{2} \sum_{k,l} \left( \frac{\partial^2 \boldsymbol{\mu}}{\partial Q_k \partial Q_l} \right)_0 Q_k Q_l + \dots
$$

其中，$\boldsymbol{\mu}_0$ 是分子的[永久偶极矩](@entry_id:163961)，下标 $0$ 表示在平衡构型（$\mathbf{Q}=\mathbf{0}$）处取值。对于[基频](@entry_id:268182)跃迁 $|0_k\rangle \to |1_k\rangle$，跃迁偶极矩为：

$$
\boldsymbol{\mu}_{10} = \langle 1_k | \boldsymbol{\mu}(Q_k) | 0_k \rangle = \langle 1_k | \boldsymbol{\mu}_0 | 0_k \rangle + \left( \frac{\partial \boldsymbol{\mu}}{\partial Q_k} \right)_0 \langle 1_k | Q_k | 0_k \rangle + \dots
$$

第一项，$\langle 1_k | \boldsymbol{\mu}_0 | 0_k \rangle = \boldsymbol{\mu}_0 \langle 1_k | 0_k \rangle$，由于[谐振子](@entry_id:155622)波[函数的正交性](@entry_id:160337)（$\langle 1_k | 0_k \rangle = 0$）而等于零。这揭示了一个重要事实：分子的[永久偶极矩](@entry_id:163961)本身不引起[振动跃迁](@entry_id:167069)，一个分子即使没有[永久偶极矩](@entry_id:163961)（如 $\text{CO}_2$），也可能具有[红外活性](@entry_id:267987)。

第二项是决定基频跃迁是否发生的关键。对于[谐振子](@entry_id:155622)，矩阵元 $\langle 1_k | Q_k | 0_k \rangle$ 是非零的。因此，跃迁偶极矩是否为零完全取决于其系数——偶极矩对[简正坐标](@entry_id:143194)的一阶导数。这就引出了红外[光谱](@entry_id:185632)的**总体[选择定则](@entry_id:140784)**（gross selection rule）：

**一个[振动](@entry_id:267781)模式是红外活性的，当且仅当在该[振动](@entry_id:267781)过程中分子的偶极矩发生变化。**

数学上，这意味着 $(\partial \boldsymbol{\mu} / \partial Q_k)_0 \neq \mathbf{0}$。跃迁的强度则正比于 $|\!|(\partial \boldsymbol{\mu} / \partial Q_k)_0|\!|^2$。

一个经典的例子是[同核双原子分子](@entry_id:155474)，如 $\text{N}_2$ 或 $\text{O}_2$ [@problem_id:2645677]。由于其对称性，无论键长如何变化，分子的偶极矩始终为零，即 $\boldsymbol{\mu}(Q) \equiv \mathbf{0}$。因此，其对[简正坐标](@entry_id:143194)的任何阶导数都为零，特别是 $(\partial \boldsymbol{\mu} / \partial Q)_0 = \mathbf{0}$。所以，这类分子的[振动](@entry_id:267781)是红外非活性的。

### 拉曼[光谱](@entry_id:185632)：变化极化率的选择定则

拉曼[光谱](@entry_id:185632)是一种散射技术，其物理机制与[红外吸收](@entry_id:188893)不同。当一束[单色光](@entry_id:178750)（频率为 $\omega_0$）照射分子时，光的[电场](@entry_id:194326) $\mathbf{E}$ 会在分子中诱导出一个偶极矩 $\mathbf{p}_{ind}$，其大小由分子的**极化率**（polarizability）张量 $\boldsymbol{\alpha}$ 决定：

$$
\mathbf{p}_{ind} = \boldsymbol{\alpha} \mathbf{E}
$$

这个被诱导的[振荡](@entry_id:267781)偶极矩会重新辐射[电磁波](@entry_id:269629)。大部分[光子](@entry_id:145192)会以与入射光相同的频率 $\omega_0$ 被[弹性散射](@entry_id:152152)，这称为[瑞利散射](@entry_id:178255)（Rayleigh scattering）。然而，如果分子在散射过程中发生了[振动能级](@entry_id:193001)的跃迁，散射光的频率就会发生改变，产生非弹性散射，即拉曼散射。

我们可以通过一个经典模型来理解其选择定则 [@problem_id:2645709]。假设入射光的[电场](@entry_id:194326)为 $\mathbf{E}(t) = \mathbf{E}_0 \cos(\omega_0 t)$，分子沿某一[简正坐标](@entry_id:143194) $Q_k$ 的[振动](@entry_id:267781)为 $Q_k(t) = \hat{Q}_k \cos(\omega_v t)$。分子的极化率也会随[原子核](@entry_id:167902)的运动而改变，可以将其展开为：

$$
\boldsymbol{\alpha}(Q_k) \approx \boldsymbol{\alpha}_0 + \left( \frac{\partial \boldsymbol{\alpha}}{\partial Q_k} \right)_0 Q_k(t)
$$

将这些代入[诱导偶极矩](@entry_id:262417)的表达式中：

$$
\mathbf{p}_{ind}(t) \approx \left[ \boldsymbol{\alpha}_0 + \left( \frac{\partial \boldsymbol{\alpha}}{\partial Q_k} \right)_0 \hat{Q}_k \cos(\omega_v t) \right] \mathbf{E}_0 \cos(\omega_0 t)
$$

$$
\mathbf{p}_{ind}(t) \approx \boldsymbol{\alpha}_0 \mathbf{E}_0 \cos(\omega_0 t) + \left( \frac{\partial \boldsymbol{\alpha}}{\partial Q_k} \right)_0 \hat{Q}_k \mathbf{E}_0 \cos(\omega_v t) \cos(\omega_0 t)
$$

第一项是频率为 $\omega_0$ 的瑞利散射。第二项利用三角函数关系式 $\cos(A)\cos(B) = \frac{1}{2}[\cos(A+B) + \cos(A-B)]$，可以得到：

$$
\frac{1}{2} \left( \frac{\partial \boldsymbol{\alpha}}{\partial Q_k} \right)_0 \hat{Q}_k \mathbf{E}_0 [\cos((\omega_0 + \omega_v)t) + \cos((\omega_0 - \omega_v)t)]
$$

这表明[诱导偶极矩](@entry_id:262417)中包含了新的频率成分 $\omega_0 + \omega_v$（[反斯托克斯散射](@entry_id:271867)）和 $\omega_0 - \omega_v$（[斯托克斯散射](@entry_id:159214)）。这些非弹性散射成分的存在，前提是它们的振幅不为零。因此，我们得到了拉曼[光谱](@entry_id:185632)的**总体选择定则**：

**一个[振动](@entry_id:267781)模式是拉曼活性的，当且仅当在该[振动](@entry_id:267781)过程中分子的极化率发生变化。**

数学上，这意味着张量 $(\partial \boldsymbol{\alpha} / \partial Q_k)_0$ 至少有一个分量不为零。

### 对称性、选择定则与互斥原理

群论为判断分子振动的[光谱](@entry_id:185632)活性提供了一个无需计算导数的、更为严谨和普适的框架。其基本原理是：一个跃迁是允许的，当且仅当跃迁矩积分的被积函数在分子所属点群的所有[对称操作](@entry_id:143398)下都是对称的（即属于全对称表示）。

对于从[振动](@entry_id:267781)[基态](@entry_id:150928)（全对称）到单量子[激发态](@entry_id:261453)（其对称性与简正模式 $Q_k$ 相同，记为 $\Gamma(Q_k)$）的基频跃迁，该规则简化为：

-   **红外活性**：如果简正模式的对称性 $\Gamma(Q_k)$ 与偶极矩算符分量（$x, y, z$）之一的对称性相同。
-   **[拉曼活性](@entry_id:264824)**：如果简正模式的对称性 $\Gamma(Q_k)$ 与[极化率张量](@entry_id:191938)分量（$x^2, y^2, z^2, xy, xz, yz$ 等二次型）之一的对称性相同。

我们可以利用这个原理来分析具体的分子 [@problem_id:2645648]。例如，对于 $\text{C}_{3v}$ 点群（如氨分子），$z$ 坐标属于 $\text{A}_1$ 表示。因此，所有 $\text{A}_1$ 对称性的[振动](@entry_id:267781)（如对称伸缩）都是[红外活性](@entry_id:267987)的，其跃迁偶极矩沿 $z$ 轴。而对于 $\text{T}_d$ 点群（如甲烷），没有任何偶极矩分量属于 $\text{A}_1$ 表示（它们共同属于 $\text{T}_2$ 表示），因此其 $\text{A}_1$ [振动](@entry_id:267781)模式（对称伸缩）是红外非活性的。

[对称性分析](@entry_id:174795)最重要的推论之一是**互斥原理**（Rule of Mutual Exclusion）。该原理适用于所有具有[反演中心](@entry_id:141957)（inversion center, $i$）的分子（即[中心对称分子](@entry_id:166437)）。其核心在于，不同算符在反演操作下的对称性不同 [@problem_id:2898241] [@problem_id:2959326]：

-   [电偶极矩](@entry_id:178520)算符 $\boldsymbol{\mu}$ 是一个矢量，在反演操作下会改变符号（$\mathbf{r} \to -\mathbf{r}$），因此它具有**奇（ungerade, u）**宇称。
-   [极化率张量](@entry_id:191938) $\boldsymbol{\alpha}$ 的分量是坐标的二次型（如 $x^2, xy$），在反演操作下保持不变（$(-x)(-y) = xy$），因此它具有**偶（gerade, g）**宇称。

根据群论[选择定则](@entry_id:140784)，对于一个[中心对称分子](@entry_id:166437)：
-   若要一个[振动](@entry_id:267781)模式是**红外活性**的，该模式的对称性必须是**奇（u）**的，这样才能与奇宇称的偶极矩算符耦合。
-   若要一个[振动](@entry_id:267781)模式是**[拉曼活性](@entry_id:264824)**的，该模式的对称性必须是**偶（g）**的，这样才能与偶宇称的[极化率](@entry_id:143513)算符耦合。

由于任何一个[振动](@entry_id:267781)模式的对称性不可能同时既是奇的又是偶的，我们得出结论：

**对于[中心对称分子](@entry_id:166437)，凡是红外活性的[振动](@entry_id:267781)模式一定是拉曼非活性的，反之亦然。**

这就是互斥原理。例如，$\text{CO}_2$（$\text{D}_{\infty h}$[点群](@entry_id:142456)）的对称伸缩[振动](@entry_id:267781)是 $g$ 宇称，因而是拉曼活性、红外非活性的；而其反[对称伸缩](@entry_id:165187)[振动](@entry_id:267781)是 $u$ 宇称，因而是[红外活性](@entry_id:267987)、拉曼非活性的。[@problem_id:2645677]

### 超越基频：泛频与组合频

上述讨论主要基于“力学谐性”（势能是二次的）和“电学谐性”（偶极矩/[极化率](@entry_id:143513)是线性的）近似。这些近似解释了最强的[基频](@entry_id:268182)跃迁。然而，在实验[光谱](@entry_id:185632)中，我们经常观察到一些较弱的谱带，它们的频率大约是某个[基频](@entry_id:268182)的整数倍（**泛频**，overtones）或两个或多个[基频](@entry_id:268182)之和/差（**组合频**，combination bands）。

这些“禁戒”跃迁的出现，源于**非谐性**。非谐性主要有两种来源：
1.  **力学[非谐性](@entry_id:137191)**：分子的实际[势能](@entry_id:748988)并非严格的二次型，包含了 $Q^3, Q^4$ 等高次项。这导致了[振动能级](@entry_id:193001)不再是等间距的，并且谐振子的[波函数](@entry_id:147440)会发生混合。
2.  **电学非谐性**：分子的偶极矩或极化率对[简正坐标](@entry_id:143194)的依赖关系不是严格线性的，其[泰勒展开](@entry_id:145057)式中包含 $Q^2, Q_k Q_l$ 等高次项。

即使在力学谐性（即势能函数严格为二次型）的理想情况下，仅仅电学非谐性就足以使泛频和组合频具有强度。

考虑红外[光谱](@entry_id:185632)中的电学[非谐性](@entry_id:137191) [@problem_id:2645659]。偶极矩展开式中的二次项 $\frac{1}{2} \sum_{kl} \boldsymbol{\mu}_{kl}'' Q_k Q_l$ 可以引起双[量子跃迁](@entry_id:145857)。
-   当 $k=l$ 时，算符 $Q_k^2$ 连接的是 $\Delta v_k = \pm 2$ 的能级，因此可以产生泛频跃迁（$|0\rangle \to |2_k\rangle$）。其强度正比于 $||\boldsymbol{\mu}_{kk}''||^2 = ||(\partial^2 \boldsymbol{\mu} / \partial Q_k^2)_0||^2$。
-   当 $k \neq l$ 时，算符 $Q_k Q_l$ 可以同时改变两个模式的量子数，引起组合频跃迁（$|0\rangle \to |1_k, 1_l\rangle$）。其强度正比于 $||\boldsymbol{\mu}_{kl}''||^2 = ||(\partial^2 \boldsymbol{\mu} / \partial Q_k \partial Q_l)_0||^2$。

通过精确计算，可以得到泛频强度与基频强度的比值，例如：
$$
R_{\text{overtone}}(k) = \frac{I(0\to 2_k)}{I(0\to 1_k)} \propto \frac{\hbar}{\omega_k} \frac{||\boldsymbol{\mu}_{kk}''||^2}{||\boldsymbol{\mu}_k'||^2}
$$
由于[二阶导数](@entry_id:144508)通常远小于一阶导数，这些跃迁的强度一般比基频弱得多。

完全类似的分析也适用于拉曼[光谱](@entry_id:185632) [@problem_id:2645698]。[极化率](@entry_id:143513)展开式中的二次项 $\frac{1}{2} \sum_{ij} \boldsymbol{\alpha}_{ij}'' Q_i Q_j$ 是导致[拉曼活性](@entry_id:264824)泛频和组合频的主要原因（在纯[谐振子模型](@entry_id:178080)中）。

### 拓展至晶体：声学与[光学声子](@entry_id:136993)

[分子振动](@entry_id:140827)的概念可以自然地推广到周期性晶体中，形成[晶格振动](@entry_id:140970)的概念，其量子化的[元激发](@entry_id:140859)被称为**[声子](@entry_id:140728)**。对于每个波矢 $\mathbf{q}$，一个含有 $N$ 个原子的原胞会产生 $3N$ 个[振动](@entry_id:267781)分支。

这些分支可分为两类：
-   **[声学声子](@entry_id:141298)**（Acoustic Phonons）：共 3 个分支。在布里渊区中心（$\Gamma$点，$\mathbf{q}=\mathbf{0}$），它们对应于整个[原胞](@entry_id:159354)内所有原子的同向、等幅平移，宏观上表现为晶体的刚性平移。
-   **[光学声子](@entry_id:136993)**（Optical Phonons）：共 $3N-3$ 个分支。在$\Gamma$点，它们对应于原胞内不同原子（或子[晶格](@entry_id:196752)）之间的相对运动，而原胞的[质心](@entry_id:265015)保持不动。

光与[晶格](@entry_id:196752)的相互作用主要发生在 $\mathbf{q} \approx \mathbf{0}$ 的长波极限下。一个关键的问题是：这些[声子模式](@entry_id:201212)是否具有红外或拉曼活性？[@problem_id:2645666]

对于**[声学声子](@entry_id:141298)**，在$\Gamma$点，其运动是整个[电中性](@entry_id:157680)原胞的刚性平移。
-   **[红外活性](@entry_id:267987)**：由于原胞是[电中性](@entry_id:157680)的，整体平移不会产生或改变宏观偶极矩。因此，$\partial \mathbf{p} / \partial Q_{acoustic} = \mathbf{0}$。这被称为**[声学求和规则](@entry_id:746229)**（acoustic sum rule）。所以，$\Gamma$点的[声学声子](@entry_id:141298)总是**红外非活性**的。
-   **[拉曼活性](@entry_id:264824)**：刚性平移不改变[原胞](@entry_id:159354)内部的原子间相对位置和成键情况，因此也不会改变其电子云的[分布](@entry_id:182848)和对外[电场](@entry_id:194326)的响应能力，即极化率不变。因此，$\partial \boldsymbol{\alpha} / \partial Q_{acoustic} = \mathbf{0}$。所以，$\Gamma$点的[声学声子](@entry_id:141298)也总是**拉曼非活性**的。

对于**[光学声子](@entry_id:136993)**，情况则完全不同。在$\Gamma$点，[光学声子](@entry_id:136993)涉及[原胞](@entry_id:159354)内正负离子（或不同原子）的相对运动。
-   这种[相对运动](@entry_id:169798)可以产生一个[振荡](@entry_id:267781)的宏观偶极矩，因此[光学声子](@entry_id:136993)**可以**是红外活性的。
-   这种[相对运动](@entry_id:169798)也改变了键长和键角，从而调制了晶体的[宏观极化](@entry_id:141855)率，因此光学声子也**可以**是[拉曼活性](@entry_id:264824)的。

具体某个光学声子模式是否具有红外或[拉曼活性](@entry_id:264824)，取决于该模式的对称性是否满足相应[晶体点群](@entry_id:183880)的[选择定则](@entry_id:140784)，其分析方法与孤立分子完全相同。例如，在[中心对称](@entry_id:144242)的晶体中，[互斥](@entry_id:752349)原理同样适用，[奇宇称](@entry_id:147965)的光学声子是[红外活性](@entry_id:267987)的，而偶宇称的光学声子是[拉曼活性](@entry_id:264824)的。