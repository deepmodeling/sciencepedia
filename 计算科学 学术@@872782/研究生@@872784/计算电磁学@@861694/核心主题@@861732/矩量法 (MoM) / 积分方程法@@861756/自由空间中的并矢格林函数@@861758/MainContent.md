## 引言
[并矢格林函数](@entry_id:152029)（Dyadic Green's Function, DGF）是电磁学，特别是波动与辐射理论中的一个基石性概念。它代表了系统对最基本的激励——一个矢量[点源](@entry_id:196698)——的响应，如同物理世界中的“[基本解](@entry_id:184782)”或“脉冲响应”。理解[并矢格林函数](@entry_id:152029)，就是掌握了从[微观电流](@entry_id:184920)源出发，构建宏观[电磁场](@entry_id:265881)的普适性语言。然而，从抽象的数学定义到其在[天线设计](@entry_id:746476)、[电磁散射](@entry_id:182193)、[量子光学](@entry_id:140582)乃至前沿计算方法中的广泛应用，其间存在着一条需要系统梳理的知识路径。本文旨在填补这一鸿沟，为读者提供一个关于自由空间[并矢格林函数](@entry_id:152029)的全面而深入的指南。

在接下来的内容中，我们将分三步展开探索。首先，在“原理与机制”一章中，我们将从其标量基础出发，逐步构建起完整的电[并矢格林函数](@entry_id:152029)理论，深入剖析其数学结构、物理性质、[谱域](@entry_id:755169)特征及远场行为。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这一强大工具如何跨越学科界限，在[电磁散射](@entry_id:182193)、[天线分析](@entry_id:266538)、计算电磁学、现代光学和量子物理等领域发挥核心作用。最后，通过“动手实践”环节，你将有机会将理论知识应用于具体问题，解决从[天线辐射](@entry_id:265286)到数值奇异性处理的实际挑战。通过这一结构化的学习路径，你将不仅学会“是什么”，更能深刻理解“为什么”以及“如何用”，从而真正掌握[并矢格林函数](@entry_id:152029)这一贯穿经典与现代电磁学理论的精髓。

## 原理与机制

本章旨在深入探讨自由空间[并矢格林函数](@entry_id:152029)的基本原理和内在机制。我们将从其标量基础出发，逐步构建起完整的电磁[并矢格林函数](@entry_id:152029)的理论框架。这一过程不仅将揭示其数学结构，还将阐明其在物理学和工程学中的深刻含义，特别是在[电磁波](@entry_id:269629)辐射、传播及散射问题中的核心作用。

### 标量基础：亥姆霍兹方程的[格林函数](@entry_id:147802)

在研究矢量[电磁波](@entry_id:269629)之前，我们首先考察其基础——标量波动现象。在[时谐场](@entry_id:755985)（时间依赖关系为 $e^{-i\omega t}$）中，无源区的标量波场 $\psi(\mathbf{r})$ 满足齐次亥姆霍兹方程：$(\nabla^2 + k^2)\psi(\mathbf{r}) = 0$，其中 $k$ 是波数。格林函数方法的核心思想是研究系统对最简单激励——一个位于 $\mathbf{r}'$ 处的单位点源——的响应。该响应，即标量格林函数 $g(\mathbf{r}, \mathbf{r}')$，由非齐次亥姆霍兹方程定义：
$$
(\nabla^2 + k^2)g(\mathbf{r}, \mathbf{r}') = -\delta(\mathbf{r}-\mathbf{r}')
$$
其中 $\delta(\cdot)$ 是[三维狄拉克δ函数](@entry_id:274703)。物理上，$g(\mathbf{r}, \mathbf{r}')$ 代表了在 $\mathbf{r}'$ 点的一个点源在 $\mathbf{r}$ 点产生的场。

在无界、均匀的自由空间中，由于空间的[平移不变性](@entry_id:195885)，[格林函数](@entry_id:147802)仅依赖于观测点与源点之间的距离 $R = |\mathbf{r}-\mathbf{r}'|$。满足上述方程且代表向外传播波动（即满足外行辐射条件）的解是：
$$
g(\mathbf{r}, \mathbf{r}') = g(R) = \frac{e^{ikR}}{4\pi R}
$$
我们可以通过直接验证来确立此解的正确性 [@problem_id:3303071]。

首先，在源点之外的区域（$R > 0$），$\delta$函数为零，格林函数必须满足齐次[亥姆霍兹方程](@entry_id:149977)。由于 $g(R)$ 具有球对称性，我们可以使用[球坐标](@entry_id:146054)下的拉普拉斯算子 $\nabla^2 f(R) = \frac{1}{R^2}\frac{\partial}{\partial R}(R^2 \frac{\partial f}{\partial R})$。对 $g(R)$ 进行直接求导计算可得：
$$
\nabla^2 g(R) = \frac{\partial^2 g}{\partial R^2} + \frac{2}{R}\frac{\partial g}{\partial R} = -k^2 g(R)
$$
这表明 $(\nabla^2 + k^2)g(R) = 0$ 在 $R > 0$ 时成立。

其次，为了验证源项 $-\delta(\mathbf{r}-\mathbf{r}')$，我们需要在[分布](@entry_id:182848)的意义上进行考察。我们将方程 $(\nabla^2 + k^2)g = -\delta$ 在包含源点 $\mathbf{r}'$ 的一个半径为 $\epsilon$ 的小球 $B_\epsilon$ 上积分。根据狄拉克δ函数的性质，$\int_{B_\epsilon} -\delta(\mathbf{r}-\mathbf{r}') dV = -1$。对方程左边进行积分：
$$
\int_{B_\epsilon} (\nabla^2 + k^2)g \, dV = \int_{B_\epsilon} \nabla^2 g \, dV + \int_{B_\epsilon} k^2 g \, dV
$$
利用[高斯散度定理](@entry_id:188065)，第一项变为在球表面 $S_\epsilon$ 上的积分：
$$
\lim_{\epsilon \to 0} \int_{B_\epsilon} \nabla^2 g \, dV = \lim_{\epsilon \to 0} \oint_{S_\epsilon} \nabla g \cdot d\mathbf{S} = \lim_{\epsilon \to 0} \left( 4\pi\epsilon^2 \frac{\partial g}{\partial R}\Big|_{R=\epsilon} \right) = -1
$$
对于第二项，由于 $g(R)$ 在 $R=0$ 处是 $O(R^{-1})$ 的奇性，其在体积 $dV \sim R^2 dR$ 上的积分是收敛的，并且在 $\epsilon \to 0$ 的极限下趋于零。因此，
$$
\lim_{\epsilon \to 0} \int_{B_\epsilon} (\nabla^2 + k^2)g \, dV = -1 + 0 = -1
$$
这在[分布](@entry_id:182848)意义上严格验证了 $g(R)$ 是亥姆霍兹方程的[基本解](@entry_id:184782)。

### [索末菲辐射条件](@entry_id:168772)与唯一性

在无界空间中求解波动方程时，必须施加一个边界条件来确保[解的唯一性](@entry_id:143619)。对于由有限区域内的源激发的辐射问题，这个条件就是**[索末菲辐射条件](@entry_id:168772) (Sommerfeld Radiation Condition, SRC)**。它规定在无穷远处，场必须表现为纯粹的向外传播的波，不允许有来自无穷远处的能量汇入。

对于标量格林函数，SRC 的数学表达式为 [@problem_id:3303071]：
$$
\lim_{R\to\infty} R\left(\frac{\partial g}{\partial R}-i k g\right)=0
$$
我们可以直接验证所给的 $g(R) = \frac{e^{ikR}}{4\pi R}$ 满足此条件。计算括号内的表达式：
$$
\frac{\partial g}{\partial R}-i k g = \frac{e^{ikR}}{4\pi R^2}(ikR - 1) - ik\frac{e^{ikR}}{4\pi R} = -\frac{e^{ikR}}{4\pi R^2}
$$
代入极限中，我们得到：
$$
\lim_{R\to\infty} R\left(-\frac{e^{ikR}}{4\pi R^2}\right) = \lim_{R\to\infty} -\frac{e^{ikR}}{4\pi R} = 0
$$
这证实了 $g(R)$ 描述的是一个纯粹的外[行波](@entry_id:185008)。

SRC 的重要性在于它保证了辐射问题解的**唯一性** [@problem_id:3303046]。考虑两个由相同[紧支集](@entry_id:276214)源 $\mathbf{J}$ 产生的不同解 $\mathbf{E}_1$ 和 $\mathbf{E}_2$。它们的差场 $\mathbf{F} = \mathbf{E}_1 - \mathbf{E}_2$ 满足齐次[亥姆霍兹方程](@entry_id:149977)，并且由于 $\mathbf{E}_1$ 和 $\mathbf{E}_2$ 都满足 SRC，$\mathbf{F}$ 也满足 SRC。通过应用[格林第二恒等式](@entry_id:169499)于 $\mathbf{F}$ 的各个笛卡尔分量及其[复共轭](@entry_id:174690)，可以证明，任何在全空间中满足齐次亥姆霍兹方程和 SRC 的场必须恒等于零。这一证明的核心步骤表明，满足 SRC 的场的[远场辐射](@entry_id:265518)功率积分为零，这意味着[远场](@entry_id:269288)振幅为零。根据 Rellich 引理和[椭圆算子](@entry_id:181616)的[唯一延拓](@entry_id:168709)定理，如果一个解在无穷[远区](@entry_id:185115)域为零，那么它在整个定义域内都必须为零。因此，$\mathbf{F} \equiv \mathbf{0}$，即 $\mathbf{E}_1 \equiv \mathbf{E}_2$。SRC 通过排除所有内[行波解](@entry_id:272909)，确保了物理上有意义的辐射解是唯一的。

### 电[并矢格林函数](@entry_id:152029)

现在我们将讨论从[标量场](@entry_id:151443)推广到矢量[电磁场](@entry_id:265881)。在[频域](@entry_id:160070)中，由电流源 $\mathbf{J}$ 产生的[电场](@entry_id:194326) $\mathbf{E}$ 满足矢量亥姆霍兹方程：
$$
\nabla \times \nabla \times \mathbf{E}(\mathbf{r}) - k^2 \mathbf{E}(\mathbf{r}) = i\omega\mu\mathbf{J}(\mathbf{r})
$$
类似于标量情况，我们定义**电[并矢格林函数](@entry_id:152029) (Electric Dyadic Green's Function)** $\mathbf{G}^E(\mathbf{r}, \mathbf{r}')$ 作为对单位矢量[点源](@entry_id:196698)（电偶极子）响应的 $3 \times 3$ 张量（并矢）。其定义方程为 [@problem_id:3303085]：
$$
(\nabla \times \nabla \times - k^2)\mathbf{G}^E(\mathbf{r},\mathbf{r}') = \mathbf{I}\delta(\mathbf{r}-\mathbf{r}')
$$
其中 $\mathbf{I}$ 是单位并矢。$\mathbf{G}^E$ 的每一列代表了沿一个坐标轴方向的单位偶极子源所产生的矢量[电场](@entry_id:194326)。

一个至关重要的联系是，矢量算子的格林函数 $\mathbf{G}^E$ 可以通过标量[格林函数](@entry_id:147802) $g$ 来构造。其关系式为：
$$
\mathbf{G}^E(\mathbf{r},\mathbf{r}') = \left(\mathbf{I} + \frac{1}{k^2}\nabla\nabla\right)g(\mathbf{r},\mathbf{r}')
$$
这个表达式的正确性可以通过将其直接代入 $\mathbf{G}^E$ 的定义方程来验证 [@problem_id:3303097]。利用矢量恒等式 $\nabla \times \nabla \times (g\mathbf{I}) = \nabla\nabla g - \mathbf{I}\nabla^2 g$ 和 $\nabla \times (\nabla\nabla g) = \mathbf{0}$（由于混合偏导的对称性），我们可以证明：
\begin{align*}
(\nabla \times \nabla \times - k^2) \left(\mathbf{I} + \frac{1}{k^2}\nabla\nabla\right)g &= (\nabla\nabla g - \mathbf{I}\nabla^2 g) - k^2\left(g\mathbf{I} + \frac{1}{k^2}\nabla\nabla g\right) \\
&= -\mathbf{I}(\nabla^2 g + k^2 g) \\
&= -\mathbf{I}(-\delta(\mathbf{r}-\mathbf{r}')) \\
&= \mathbf{I}\delta(\mathbf{r}-\mathbf{r}')
\end{align*}
这个推导是理解[并矢格林函数](@entry_id:152029)结构的核心。它表明，复杂的矢量波动问题可以通过一个标量波动问题和一个[微分算子](@entry_id:140145)来解决。

电[并矢格林函数](@entry_id:152029)还具有其他几个重要性质 [@problem_id:3303085]：
- **散度性质**：对 $\mathbf{G}^E$ 的表达式求散度，并利用 $(\nabla^2 + k^2)g = -\delta$，可以得到 $\nabla \cdot \mathbf{G}^E = -\frac{1}{k^2}\nabla\delta(\mathbf{r}-\mathbf{r}')$。这表明 $\mathbf{G}^E$ 在源点处不是无散的，其源包含一个与[电荷](@entry_id:275494)偶极子对应的部分。在源点之外的任何区域（$\mathbf{r} \neq \mathbf{r}'$），$\nabla \cdot \mathbf{G}^E = \mathbf{0}$。

- **互易性**：在自由空间这种互易介质中，[格林函数](@entry_id:147802)满足对称关系 $\mathbf{G}^E(\mathbf{r},\mathbf{r}') = [\mathbf{G}^E(\mathbf{r}',\mathbf{r})]^\top$。这反映了“源”和“场”点互换的对称性，即在 $\mathbf{r}'$ 处的 $j$ 方向偶极子在 $\mathbf{r}$ 点产生的 $i$ 方向[电场](@entry_id:194326)，等于在 $\mathbf{r}$ 处的 $i$ 方向偶极子在 $\mathbf{r}'$ 点产生的 $j$ 方向[电场](@entry_id:194326)。

### 显式形式与[渐近行为](@entry_id:160836)

为了深入理解 $\mathbf{G}^E$ 的物理行为，我们需要其显式表达式。通过对 $\mathbf{G}^E = (\mathbf{I} + \frac{1}{k^2}\nabla\nabla)g$ 中的[二阶导数](@entry_id:144508)项 $\nabla\nabla g$ 进行细致的计算，我们可以得到其分量形式 [@problem_id:3303070]。设 $\hat{\mathbf{R}} = (\mathbf{r}-\mathbf{r}')/R$，其分量为 $\hat{R}_i$，则 $\mathbf{G}^E$ 的 $(i,j)$ 分量为：
$$
G^{E}_{ij}(\mathbf{r},\mathbf{r}') = \left[ \left(1+\frac{i}{kR}-\frac{1}{(kR)^{2}}\right)\delta_{ij} - \left(1+\frac{3i}{kR}-\frac{3}{(kR)^{2}}\right)\hat{R}_{i}\hat{R}_{j} \right] \frac{e^{ikR}}{4\pi R}
$$
这个复杂的表达式完整地描述了从源点到无穷远处的[电场](@entry_id:194326)行为。各项的 $R$ 依赖关系揭示了不同区域的场特性：
- **近场区 ($kR \ll 1$)**：此时 $(kR)^{-2}$ 和 $(kR)^{-1}$ 项占主导。场分量衰减最慢的是 $R^{-3}$ 项，这对应于静电偶极子和静[磁偶极子](@entry_id:275765)场的行为，是[准静态场](@entry_id:201091)。
- **[远场区](@entry_id:185115) ($kR \gg 1$)**：此时 $(kR)^{-1}$ 和 $(kR)^{-2}$ 项可以忽略。场的[主导项](@entry_id:167418)衰减为 $R^{-1}$，这是向外传播的球面波的典型特征。

在[远场区](@entry_id:185115)，我们可以对 $\mathbf{G}^E$ 进行[渐近展开](@entry_id:173196) [@problem_id:3303087]。保留至 $R^{-1}$ 的[主导项](@entry_id:167418)，我们得到 [@problem_id:3303085]：
$$
\mathbf{G}^E(\mathbf{r},\mathbf{r}') \sim \frac{e^{ikR}}{4\pi R}(\mathbf{I} - \hat{\mathbf{R}}\hat{\mathbf{R}}) \quad \text{as } R \to \infty
$$
这里的并矢 $(\mathbf{I} - \hat{\mathbf{R}}\hat{\mathbf{R}})$ 是一个**横向投影算子**。它将任意矢量投影到垂直于传播方向 $\hat{\mathbf{R}}$ 的平面上。这精确地反映了[电磁波](@entry_id:269629)在[远场区](@entry_id:185115)是横波的物理事实。

为了更精确地描述场，例如在[天线分析](@entry_id:266538)中，我们可能需要更高阶的修正项。保留到 $R^{-2}$ 阶的[渐近展开](@entry_id:173196)为 [@problem_id:3303087]：
$$
\mathbf{G}^E(\mathbf{r},\mathbf{r}') \sim \frac{e^{ikR}}{4\pi R} \left[ (\mathbf{I} - \hat{\mathbf{R}}\hat{\mathbf{R}}) + \frac{i}{kR}(\mathbf{I} - 3\hat{\mathbf{R}}\hat{\mathbf{R}}) \right]
$$
这揭示了从近场到[远场](@entry_id:269288)的平滑过渡。

### [谱域](@entry_id:755169)视角

[傅里叶变换](@entry_id:142120)（或[谱域](@entry_id:755169)分析）为理解格林函数提供了另一种强有力的视角。通过对 $\mathbf{G}^E$ 的定义方程进行三维[空间傅里叶变换](@entry_id:176346)，[微分](@entry_id:158718)运算 $\nabla$ 变为代数乘法 $i\mathbf{k}$，其中 $\mathbf{k}$ 是[谱域](@entry_id:755169)中的波矢量。变换后的方程变为一个代数方程 [@problem_id:3303069]：
$$
\left( (|\mathbf{k}|^2 - k^2)\mathbf{I} - \mathbf{k}\mathbf{k} \right) \widehat{\mathbf{G}}^E(\mathbf{k}) = \mathbf{I}
$$
其中 $\widehat{\mathbf{G}}^E(\mathbf{k})$ 是 $\mathbf{G}^E(\mathbf{r})$ 的[傅里叶变换](@entry_id:142120)。

为了求解 $\widehat{\mathbf{G}}^E(\mathbf{k})$，我们引入**纵向投影算子** $P_L(\mathbf{k}) = \mathbf{k}\mathbf{k}/|\mathbf{k}|^2$ 和**横向[投影算子](@entry_id:154142)** $P_T(\mathbf{k}) = \mathbf{I} - P_L(\mathbf{k})$。这些算子可以将任何矢量分解为平行于 $\mathbf{k}$（纵向）和垂直于 $\mathbf{k}$（横向）的分量。通过这种分解，可以求得算子矩阵的逆，即 $\widehat{\mathbf{G}}^E(\mathbf{k})$：
$$
\widehat{\mathbf{G}}^E(\mathbf{k}) = \frac{P_T(\mathbf{k})}{|\mathbf{k}|^2 - k^2} - \frac{P_L(\mathbf{k})}{k^2}
$$
这个[谱域](@entry_id:755169)表达式极其深刻地揭示了 $\mathbf{G}^E$ 的双重性质：
- **横向部分**：第一项 $\frac{P_T(\mathbf{k})}{|\mathbf{k}|^2 - k^2}$ 在分母为零时存在[奇点](@entry_id:137764)，即当 $|\mathbf{k}| = k$ 时。这个球面在[谱域](@entry_id:755169)中被称为“光锥”或“在壳层”（on-shell），它对应于所有可能自由传播的平面波。这一项完全描述了辐射和波动现象。
- **纵向部分**：第二项 $-\frac{P_L(\mathbf{k})}{k^2}$ 没有 $|\mathbf{k}|^2 - k^2$ 的分母，因此与传播波无关。它描述了场的纵向（非辐射）分量，与源区的电荷分布产生的准静态库仑场直接相关。

正是由于这个非零的纵向部分，$\mathbf{G}^E$ 本身并不是一个纯横向的并矢。例如，当它作用于一个纵向矢量 $\mathbf{k}$ 时，结果非零：$\widehat{\mathbf{G}}^E(\mathbf{k}) \mathbf{k} = -\mathbf{k}/k^2$。然而，对于无散的源电流（满足 $\mathbf{k} \cdot \widehat{\mathbf{J}}(\mathbf{k}) = 0$），由于 $\widehat{\mathbf{J}}$ 是纯横向的，它产生的[电场](@entry_id:194326)也将是纯横向的，因为纵向投影 $P_L(\mathbf{k})\widehat{\mathbf{J}}(\mathbf{k}) = \mathbf{0}$ [@problem_id:3303069]。

### 高级主题与应用

#### 磁[并矢格林函数](@entry_id:152029)

与[电场](@entry_id:194326)相对应，我们也可以定义**磁[并矢格林函数](@entry_id:152029) (Magnetic Dyadic Green's Function)** $\mathbf{G}^H$，它将电流源与产生的[磁场](@entry_id:153296)联系起来。通过法拉第定律 $\nabla \times \mathbf{E} = i\omega\mu\mathbf{H}$，我们可以直接从 $\mathbf{G}^E$ 定义 $\mathbf{G}^H$：
$$
\mathbf{G}^H(\mathbf{r},\mathbf{r}') = \frac{1}{i\omega\mu}\nabla \times \mathbf{G}^E(\mathbf{r},\mathbf{r}')
$$
一个重要的性质是，在源点之外，$\mathbf{G}^H$ 是无散的 [@problem_id:3303078]。这可以通过矢量恒等式 $\nabla \cdot (\nabla \times \mathbf{F}) = 0$ 证明。由于 $\mathbf{G}^E$ 的每一列在源外都是光滑的矢量场，因此 $\nabla \cdot (\nabla \times \mathbf{G}^E) = \mathbf{0}$。这在物理上反映了[磁场](@entry_id:153296)是无源的，即不存在[磁单极子](@entry_id:142817)。

#### 奇异性与自场项

格林函数在源点 $R=0$ 处是奇异的。在电磁[积分方程](@entry_id:138643)的数值计算中，当观测点与源点重合或非常接近时，必须特殊处理这种奇异性。特别是 $\mathbf{G}^E$ 中的 $\nabla\nabla g$ 项，其奇异性为 $O(R^{-3})$，导致积分发散。

为了处理这个问题，需要计算[奇异积分](@entry_id:167381)的**[柯西主值](@entry_id:192761) (Cauchy Principal Value)**。通过在一个包含[奇点](@entry_id:137764)的小球上进行积分，并利用散度定理，可以分离出发散部分并得到一个有限的“自场项”或“源并矢”。对于 $\nabla\nabla g$ 项，其在极限小球上的积分为 [@problem_id:3303056]：
$$
\text{P.V.} \int_{B_a(\mathbf{r})} \nabla_{\mathbf{r}'}\nabla_{\mathbf{r}'} g(\mathbf{r},\mathbf{r}') \, d\mathbf{r}' = -\frac{1}{3}\mathbf{I}
$$
这个结果在[矩量法](@entry_id:752140) (Method of Moments) 等数值方法中至关重要，它构成了[阻抗矩阵](@entry_id:274892)对角线元素的一部分。

#### 低频失效问题

[并矢格林函数](@entry_id:152029)的结构也解释了[计算电磁学](@entry_id:265339)中一个著名的问题：[电场积分方程](@entry_id:748872) (EFIE) 的**低频失效 (low-frequency breakdown)** [@problem_id:3303092]。EFIE 的算子可以分解为与矢量势 $\mathbf{A}$（来自 $\mathbf{J}$）和标量势 $\Phi$（来自[电荷](@entry_id:275494) $\rho$）相关的两部分。在低频极限下（$k \to 0$），这两部分的标度行为截然不同：矢量势部分与频率成正比（$\sim k$），而[标量势](@entry_id:276177)部分与频率成反比（$\sim 1/k$）。

这种不平衡源于 $\mathbf{G}^E$ 的双重性质。利用[亥姆霍兹分解](@entry_id:181767)将电流分为无散的**[螺线管](@entry_id:261182)分量** $\mathbf{J}_s$ 和无旋的**非旋分量** $\mathbf{J}_i$。
- [螺线管](@entry_id:261182)分量 $\mathbf{J}_s$ 不产生[电荷](@entry_id:275494)，因此只与矢量势的磁效应（准磁静态）相互作用，其[算子范数](@entry_id:752960) $\sim k$。
- 非旋分量 $\mathbf{J}_i$ 产生[电荷](@entry_id:275494)，主要与标量势的电效应（准静电）相互作用，其算子范数 $\sim 1/k$。

当用数值方法离散这个算子时，得到的[矩阵的条件数](@entry_id:150947)会随着频率的降低而急剧恶化（$\sim k^{-2}$），导致数值解的崩溃。解决这个问题的先进方法，如“[电荷](@entry_id:275494)-电流混合法”，正是基于对格林函数[谱域](@entry_id:755169)结构的深刻理解。通过对非旋电流部分（或等效的[电荷](@entry_id:275494)）进行适当的频率缩放，可以平衡两个[子空间](@entry_id:150286)的标度，从而在从静态到高频的整个[频谱](@entry_id:265125)范围内获得稳定、准确的数值解。这充分展示了从基本原理出发研究格林函数对于解决前沿工程问题的指导意义。