## 引言
周期性结构，从微波[天线阵列](@entry_id:271559)到纳米级的光子晶体，在现代电磁学和[光子](@entry_id:145192)学中无处不在，它们能够以前所未有的方式操控[电磁波](@entry_id:269629)。然而，分析这些在空间上无限延伸的系统带来了巨大的挑战：我们如何用一个简洁的数学模型来描述波在其中的行为？又如何能在有限的计算资源下精确地模拟它们？传统的直觉和方法在此常常失效，这构成了理论与实践之间的一道鸿沟。

本文旨在系统地介绍解决这一核心问题的强大理论工具——[弗洛凯定理](@entry_id:175204)及其在计算电磁学中的应用。通过本文的学习，您将掌握分析和设计周期性电磁系统的完整知识体系。在“原理与机制”一章中，我们将深入弗洛凯-布洛赫定理的数学精髓，揭示[周期系统](@entry_id:185882)中波的[准周期性](@entry_id:272343)本质和[能带结构](@entry_id:139379)的由来。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示该理论如何驱动[光子晶体](@entry_id:137347)、超材料等前沿技术的创新，并揭示其与[拓扑光子学](@entry_id:146464)、[量子化学](@entry_id:140193)等领域的深刻联系。最后，通过“动手实践”部分，您将有机会将理论知识转化为解决实际问题的计算技能。

## 原理与机制

在“引言”章节中，我们已经了解了周期性结构在电磁学中的重要性。本章将深入探讨分析这些结构所依赖的基础理论框架——[弗洛凯定理](@entry_id:175204)（Floquet's Theorem），以及它在计算电磁学中的具体实现，即周期性边界条件。我们将从[一般性](@entry_id:161765)的数学原理出发，逐步过渡到空间周期性系统中的具体应用，并探讨[布洛赫波](@entry_id:144558)（Bloch waves）的性质、计算方法及其在先进应用中的角色。

### 周期性系统的基本理论：[弗洛凯定理](@entry_id:175204)

许多物理系统，无论是时间上的还是空间上的，都表现出周期性。描述这类系统的[线性微分方程](@entry_id:150365)有一个优美的普适结构，由法国数学家 Gaston Floquet 给出。虽然我们的主要兴趣在于空间[周期性电磁结构](@entry_id:753348)，但从更普遍且更简单的时域系统入手，有助于我们建立核心概念。

考虑一个由[一阶线性常微分方程](@entry_id:164502)组描述的系统，其[状态向量](@entry_id:154607)为 $\mathbf{x}(t)$：
$$
\frac{d\mathbf{x}(t)}{dt} = \mathbf{A}(t)\mathbf{x}(t)
$$
其中，系统矩阵 $\mathbf{A}(t)$ 是一个周期函数，周期为 $T$，即 $\mathbf{A}(t+T) = \mathbf{A}(t)$。这种系统被称为线性时变周期（Linear Time-Periodic, LTP）系统，在时间调制介质的研究中十分常见。[弗洛凯定理](@entry_id:175204)深刻地刻画了这类系统解的结构。

该定理指出，LTP 系统的任意一个基本解矩阵 $\mathbf{\Phi}(t)$（满足 $\dot{\mathbf{\Phi}}(t) = \mathbf{A}(t)\mathbf{\Phi}(t)$ 且 $\mathbf{\Phi}(0)=\mathbf{I}$，其中 $\mathbf{I}$ 是单位矩阵）可以分解为如下形式：
$$
\mathbf{\Phi}(t) = \mathbf{P}(t)e^{\mathbf{B}t}
$$
这里，$\mathbf{P}(t)$ 是一个与 $\mathbf{A}(t)$ 具有相同周期 $T$ 的可逆矩阵，即 $\mathbf{P}(t+T)=\mathbf{P}(t)$，而 $\mathbf{B}$ 是一个常数矩阵。这个分解告诉我们，系统的解行为由两部分组成：一个纯周期性的部分 $\mathbf{P}(t)$ 和一个[指数增长](@entry_id:141869)/衰减/[振荡](@entry_id:267781)的部分 $e^{\mathbf{B}t}$。

这个定理的核心在于一个被称为**单值矩阵**（[monodromy](@entry_id:174849) matrix）的关键对象，定义为[基本解](@entry_id:184782)矩阵在一个周期结束时的值：$\mathbf{M} = \mathbf{\Phi}(T)$。可以证明，$\mathbf{\Phi}(t+T) = \mathbf{\Phi}(t)\mathbf{M}$。因此，单值矩阵 $\mathbf{M}$ 描述了系统状态在一个周期内的演化。$\mathbf{M}$ 的[特征值](@entry_id:154894) $\mu_i$ 被称为**[弗洛凯乘子](@entry_id:265040)**（Floquet multipliers）。它们与常数矩阵 $\mathbf{B}$ 的[特征值](@entry_id:154894) $\lambda_i$（被称为**[弗洛凯指数](@entry_id:266352)**，Floquet exponents）通过关系 $\mu_i = \exp(\lambda_i T)$ 联系起来。

系统的稳定性完全由[弗洛凯乘子](@entry_id:265040)决定。因为 $\mathbf{P}(t)$ 是周期的，所以它是有界的。因此，解 $\mathbf{x}(t) = \mathbf{\Phi}(t)\mathbf{x}(0)$ 的长期行为取决于 $e^{\mathbf{B}t}$。系统是指数稳定的（即当 $t \to \infty$ 时，所有解都趋于零），当且仅当所有的[弗洛凯乘子](@entry_id:265040)的模都小于1，即 $|\mu_i|  1$。这等价于所有[弗洛凯指数](@entry_id:266352) $\lambda_i$ 的实部都为负。如果所有 $|\mu_i|=1$，系统是中性稳定的；如果存在某个 $|\mu_i|  1$，系统则是不稳定的。

值得注意的是，那种认为周期系数 $\mathbf{A}(t)$ 必然导致周期解 $\mathbf{x}(t)$ 的直觉是错误的。周期解 $\mathbf{x}(t+T) = \mathbf{x}(t)$ 仅在单值矩阵 $\mathbf{M}$ 为单位矩阵时（即所有[弗洛凯乘子](@entry_id:265040)均为1）才对所有初始条件成立，这只是一个非常特殊的情况。

### 空间周期性电磁学：弗洛凯-布洛赫定理

[弗洛凯定理](@entry_id:175204)的思想可以优美地从时域推广到空间域，这在固体物理和[光子](@entry_id:145192)学中被称为**弗洛凯-布洛赫定理**（Floquet-Bloch theorem），或简称为**布洛赫定理**。

考虑一个无源、无损的周期性电磁介质，其[介电常数张量](@entry_id:274052) $\boldsymbol{\epsilon}(\mathbf{r})$ 和[磁导率](@entry_id:154559)张量 $\boldsymbol{\mu}(\mathbf{r})$ 满足空间周期性，即对于任意格矢 $\mathbf{R}$（属于某个布拉维[晶格](@entry_id:196752) $\mathcal{L}$），都有 $\boldsymbol{\epsilon}(\mathbf{r}+\mathbf{R})=\boldsymbol{\epsilon}(\mathbf{r})$ 和 $\boldsymbol{\mu}(\mathbf{r}+\mathbf{R})=\boldsymbol{\mu}(\mathbf{r})$。在[频域](@entry_id:160070)中，麦克斯韦方程可以写成一个关于[电场](@entry_id:194326) $\mathbf{E}(\mathbf{r})$ 的二阶亥姆霍兹型算符方程：
$$
\nabla\times\left(\boldsymbol{\mu}^{-1}(\mathbf{r})\,\nabla\times \mathbf{E}(\mathbf{r})\right) = \omega^2\,\boldsymbol{\epsilon}(\mathbf{r})\,\mathbf{E}(\mathbf{r})
$$
由于介质参数是周期性的，该亥姆霍兹算符与[晶格](@entry_id:196752)[平移算符](@entry_id:756122) $T_{\mathbf{R}}$（定义为 $(T_{\mathbf{R}} f)(\mathbf{r})=f(\mathbf{r}+\mathbf{R})$）是对易的。根据线性代数的基本原理，对易的算符族拥有共同的本征函数。[平移算符](@entry_id:756122)的[本征函数](@entry_id:154705)满足 $T_{\mathbf{R}}\mathbf{E} = \lambda_{\mathbf{R}}\mathbf{E}$，其[本征值](@entry_id:154894)必然具有 $\lambda_{\mathbf{R}} = \exp(i\mathbf{k}\cdot\mathbf{R})$ 的形式，其中 $\mathbf{k}$ 是一个向量，称为**[布洛赫波矢](@entry_id:746866)**（Bloch wavevector）或晶矢。因此，麦克斯韦方程在周期性介质中的本征解（称为**布洛赫模**）可以被选择为同时满足：
$$
\mathbf{E}(\mathbf{r}+\mathbf{R}) = \mathbf{E}(\mathbf{r})\,e^{i\mathbf{k}\cdot\mathbf{R}}
$$
这个条件被称为**[准周期性](@entry_id:272343)**。这正是[弗洛凯定理](@entry_id:175204)在空间域的体现。这里的相位因子 $e^{i\mathbf{k}\cdot\mathbf{R}}$ 扮演了类似于[弗洛凯乘子](@entry_id:265040)的角色。

与时间[周期系统](@entry_id:185882)中的分解类似，满足[准周期性](@entry_id:272343)的布洛赫模 $\mathbf{E}_{\mathbf{k}}(\mathbf{r})$ 总可以被写成一个平面波包络和一个严格[周期函数](@entry_id:139337)的乘积：
$$
\mathbf{E}_{\mathbf{k}}(\mathbf{r}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r})e^{i\mathbf{k}\cdot\mathbf{r}}
$$
其中，$\mathbf{u}_{\mathbf{k}}(\mathbf{r})$ 具有与[晶格](@entry_id:196752)相同的周期性，即 $\mathbf{u}_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = \mathbf{u}_{\mathbf{k}}(\mathbf{r})$。

[布洛赫波矢](@entry_id:746866) $\mathbf{k}$ 定义在**[倒易空间](@entry_id:754151)**（reciprocal space）中。这个空间由倒易格矢 $\mathbf{G}$ 张成，其定义为满足 $\mathbf{G}\cdot\mathbf{R} = 2\pi m$（其中 $m$为整数）的所有向量。[波矢](@entry_id:178620) $\mathbf{k}$ 并不是全局唯一的。如果两个[波矢](@entry_id:178620) $\mathbf{k}$ 和 $\mathbf{k}'$ 相差一个倒易格矢 $\mathbf{G}$，即 $\mathbf{k}' = \mathbf{k} + \mathbf{G}$，那么它们描述的是完全相同的[准周期性](@entry_id:272343)，因为 $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$。因此，我们只需要在倒易空间的一个基本单元——即**[第一布里渊区](@entry_id:269110)**（First Brillouin Zone, BZ）——内考虑所有不等价的[波矢](@entry_id:178620) $\mathbf{k}$，就可以得到系统的所有[本征模](@entry_id:174677)。

### 布洛赫模的性质与能带结构

对于给定的[布洛赫波矢](@entry_id:746866) $\mathbf{k}$，[亥姆霍兹方程](@entry_id:149977)成为一个在单个原胞（unit cell）上的[本征值问题](@entry_id:142153)，其解为一系列离散的本征频率 $\omega_n(\mathbf{k})$ 和对应的[本征模](@entry_id:174677) $\mathbf{E}_{n,\mathbf{k}}(\mathbf{r})$。这些频率作为 $\mathbf{k}$ 的函数关系 $\omega_n(\mathbf{k})$ 构成了光子晶体的**能带结构**（band structure）。

#### 正交性

在无损介质中（即 $\boldsymbol{\epsilon}$ 和 $\boldsymbol{\mu}$ 为实[对称正定](@entry_id:145886)张量），对于一个固定的[波矢](@entry_id:178620) $\mathbf{k}$，不同本征频率 $\omega_m \neq \omega_n$ 所对应的布洛赫模是正交的。这里的正交性是相对于一个权重为 $\boldsymbol{\epsilon}$ 的[内积](@entry_id:158127)来定义的：
$$
\langle \mathbf{E}_{m,\mathbf{k}}, \mathbf{E}_{n,\mathbf{k}} \rangle = \int_{\Omega} \mathbf{E}_{m,\mathbf{k}}^{*}(\mathbf{r}) \cdot \boldsymbol{\epsilon}(\mathbf{r}) \,\mathbf{E}_{n,\mathbf{k}}(\mathbf{r}) \, d\mathbf{r} = 0, \quad \text{若 } \omega_m \neq \omega_n
$$
其中积分在单个[原胞](@entry_id:159354) $\Omega$ 上进行。通过适当的归一化，我们可以使这些模式构成一个正交归一基底，即 $\langle \mathbf{E}_{m,\mathbf{k}}, \mathbf{E}_{n,\mathbf{k}} \rangle = \delta_{mn}$。这个性质的根源在于，对于实数[波矢](@entry_id:178620) $\mathbf{k}$ 和无损介质，亥姆霍兹算符是自伴的（Hermitian）。

#### 复数波矢与倏逝模

到目前为止，我们主要考虑的是实数波矢 $\mathbf{k}$，它们对应于在晶体中无衰减传播的模式。然而，允许 $\mathbf{k}$ 为复数，即 $\mathbf{k} = \mathbf{k}' + i\mathbf{k}''$，可以揭示更丰富的物理现象。此时，[场模](@entry_id:189270)式的振幅会随空间呈指数变化：
$$
|\mathbf{E}_{\mathbf{k}}(\mathbf{r})| = e^{-\mathbf{k}''\cdot\mathbf{r}} |\mathbf{u}_{\mathbf{k}}(\mathbf{r})|
$$
一个非零的虚部 $\mathbf{k}''$ 对应于指数衰减或增长。这在两种重要的物理情境中出现，即使在完全无损的介质中也是如此：

1.  **[光子带隙](@entry_id:272781)中的倏逝模**：[光子](@entry_id:145192)[能带结构](@entry_id:139379)中可能存在某些频率区间，其中没有任何实数 $\mathbf{k}$ 的解，这些区间被称为**[光子带隙](@entry_id:272781)**（photonic band gaps）。对于落在[带隙](@entry_id:191975)中的实数频率 $\omega$，麦克斯韦方程的解只存在于复数波矢 $\mathbf{k}$。这些解被称为**倏逝模**（evanescent modes），它们在空间上迅速衰减。例如，一个半无限大的光子晶体被频率在[带隙](@entry_id:191975)内的[电磁波](@entry_id:269629)入射时，[电磁场](@entry_id:265881)将无法深入晶体内部，而是以指数形式衰减。

2.  **开放结构中的泄漏模**：考虑一个开放的周期性结构，例如嵌入在均匀介质中的[光子晶体波导](@entry_id:160774)。这样的结构可以将能量辐射到周围空间中。从[波导模式](@entry_id:275892)的角度看，这是一种[能量损失](@entry_id:159152)，即使构成波导的材料本身是无损的。为了在计算中模拟这种辐射损失（例如通过[完美匹配层](@entry_id:753330)，PML），所求解的[本征问题](@entry_id:748835)变得非厄米（non-Hermitian）。非厄米问题的一个关键特征是其[本征值](@entry_id:154894)（在这里是波矢 $\mathbf{k}$）可以是复数。此时，$\mathbf{k}$ 的虚部 $\mathbf{k}''$ 量化了模式因辐射损耗而在传播方向上的衰减率。这些模式被称为**泄漏模**（leaky modes）。

#### 对称性与不可约[布里渊区](@entry_id:142395)

计算整个[布里渊区](@entry_id:142395)的[能带结构](@entry_id:139379)往往是冗余的。如果晶体原胞的几何结构具有[点群对称性](@entry_id:141230)（例如旋转、反射），那么其能带结构 $\omega(\mathbf{k})$ 也会表现出相应的对称性。例如，若介质在点群操作 $\mathsf{R}_g$ 下不变，则能带满足 $\omega(\mathsf{R}_g \mathbf{k}) = \omega(\mathbf{k})$。此外，对于无损互易介质，[时间反演对称性](@entry_id:138094)保证了 $\omega(-\mathbf{k}) = \omega(\mathbf{k})$。

这些对称性意味着我们只需在布里渊区的一个最小子区域内计算能带，就能通过对称操作重构出整个BZ的[能带图](@entry_id:272375)。这个最小区域被称为**不可约布里渊区**（Irreducible Brillouin Zone, IBZ）。例如，对于具有 $C_{4v}$ 对称性（正方形的对称性）的二维晶体，IBZ 是一个由 $\Gamma$ 点（中心）、$X$ 点（$k_x$轴边界中点）和 $M$ 点（角点）构成的三角形，其面积是整个BZ的1/8。

利用IBZ可以极大地减少计算量。在对BZ进行积分（例如计算态密度）时，需要对IBZ内的采样点进行加权。一个 $\mathbf{k}$ 点的权重与其“[轨道](@entry_id:137151)”（orbit）的大小成正比，即通过所有[对称操作](@entry_id:143398)能生成的不同 $\mathbf{k}$ 点的数量。位于IBZ内部的点通常具有最大的[轨道](@entry_id:137151)，而位于IBZ边界或顶点上的点由于具有更高的对称性（它们的“小群”非平庸），[轨道](@entry_id:137151)尺寸较小，因此权重也较低。

### 计算实现：周期性与准周期性边界条件

在[计算电磁学](@entry_id:265339)中，为了求解单个[原胞](@entry_id:159354)内的场，我们必须将弗洛凯-布洛赫定理转化为边界条件。这通过在[原胞](@entry_id:159354)的相对边界上施加**准周期性边界条件**（Quasi-Periodic Boundary Conditions, QPBC）来实现。

考虑一个由[基矢](@entry_id:199546) $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$ 张成的[原胞](@entry_id:159354)。对于每一对由平移向量 $\mathbf{a}_\ell$ 连接的相对面（例如 $S_\ell^-$ 和 $S_\ell^+$），场需要满足：
$$
\mathbf{E}(\mathbf{r}+\mathbf{a}_\ell) = e^{i\mathbf{k}\cdot\mathbf{a}_\ell} \mathbf{E}(\mathbf{r})
$$
其中 $\mathbf{r} \in S_\ell^-$。在数值方法（如有限元法FEM或有限差分法FDTD）中，这个条件需要应用到离散的自由度上。然而，必须小心处理边界自由度的定义和方向。一个关键点是，相对面的外法向是相反的，即 $\mathbf{n}_\ell^+ = -\mathbf{n}_\ell^-$。

-   对于使用切向场迹 $\mathbf{n}\times\mathbf{E}$ 作为边界自由度的旋度适定元（curl-conforming elements），正确的边界条件包含一个负号：
    $$
    \mathbf{n}_{\ell}^{+}\times \mathbf{E}(\mathbf{r}^{+}) = - e^{i\mathbf{k}\cdot \mathbf{a}_{\ell}} (\mathbf{n}_{\ell}^{-} \times \mathbf{E}(\mathbf{r}^{-}))
    $$
    这个负号源于 $\mathbf{n}_\ell^+ = -\mathbf{n}_\ell^-$。

-   对于使用法向通量 $\mathbf{n}\cdot\mathbf{D}$ 作为自由度的散度适定元（div-conforming elements）或有限体积法，同样因为法向相反，也存在一个负号：
    $$
    \mathbf{n}_{\ell}^{+}\cdot \mathbf{D}(\mathbf{r}^{+}) = - e^{i\mathbf{k}\cdot \mathbf{a}_{\ell}} (\mathbf{n}_{\ell}^{-} \cdot \mathbf{D}(\mathbf{r}^{-}))
    $$
    以及积分通量 $F_D^+ = -e^{i\mathbf{k}\cdot \mathbf{a}_{\ell}} F_D^-$。

-   对于使用边元（edge elements）的Nédélec方法，其自由度是沿网格边的线积分 $\int \mathbf{E}\cdot d\boldsymbol{\ell}$。一个边界边上的自由度与相对边界上对应边的自由度通过布洛赫相位因子相联系，但还需考虑一个额外的 $\pm 1$ 符号，取决于两条边的预定方向在平移后是相同还是相反。

#### 特殊情况：反周期边界条件

在计算能带结构时，常常需要对布里渊区边界上的高[对称点](@entry_id:174836)进行采样。一个重要的特殊情况是**反周期边界条件**（anti-periodic boundary conditions），它对应于布洛赫相位因子为 $-1$ 的情况。例如，对于沿 $x$ 轴周期为 $a_x$ 的一维系统，反周期条件 $\mathbf{E}(x+a_x) = -\mathbf{E}(x)$ 意味着 $e^{ik_x a_x} = -1$，这等价于选择[波矢](@entry_id:178620) $k_x = \pi/a_x$。这个点恰好是1D[布里渊区](@entry_id:142395)的边界。

在二维正方[晶格](@entry_id:196752)中，不同边界条件的组合可以用来方便地计算高[对称点](@entry_id:174836)的模式：
-   沿 $x$ 方向反周期、沿 $y$ 方向周期 $\implies \mathbf{k}=(\pi/a_x, 0)$，即 $X$ 点。
-   沿 $x$ 和 $y$ 方向都反周期 $\implies \mathbf{k}=(\pi/a_x, \pi/a_y)$，即 $M$ 点。

在FDFD或FDTD等基于网格的求解器中，这些条件通过修改跨越边界的“环绕”耦合项来实现：对于反周期边界，这些[耦合系数](@entry_id:273384)乘以 $-1$。

### 应用与高级主题

弗洛凯-布洛赫理论及其计算实现是分析和设计周期性电磁器件的基石。以下是几个重要的应用和相关的高级概念。

#### 超[原胞](@entry_id:159354)方法与[能带折叠](@entry_id:272980)

为了用周期性边界条件来模拟[周期结构](@entry_id:753351)中的孤立缺陷（例如[光子晶体](@entry_id:137347)中的一个缺失或改变的孔洞），我们采用**超[原胞](@entry_id:159354)方法**（supercell approach）。其思想是构建一个包含该缺陷的、足够大的新原胞（即超原胞），然后将这个超原胞作为基本单元进行周期性重复。

这种方法的一个重要后果是**[能带折叠](@entry_id:272980)**（band folding）。由于超原胞在[实空间](@entry_id:754128)中更大（例如，$N_1 \times N_2$ 倍[原胞](@entry_id:159354)大小），其对应的[布里渊区](@entry_id:142395)在[倒易空间](@entry_id:754151)中会相应变小（$1/(N_1 N_2)$ 倍）。完美晶体的原始[能带结构](@entry_id:139379)被“折叠”到这个更小的SBZ中。原本在原始BZ中的一个能带，在SBZ中会表现为 $N_1 N_2$ 个交错的能带。

当超[原胞](@entry_id:159354)中包含一个缺陷时，如果该缺陷能够支持一个局域模，这个模式的频率将出现在[完美晶体](@entry_id:138314)[能带结构](@entry_id:139379)的[带隙](@entry_id:191975)之中。在超[原胞](@entry_id:159354)的[能带图](@entry_id:272375)中，这个局域模对应一个几乎平坦的能带（[色散](@entry_id:263750)极小），因为它在空间上是局域的，与其周期性“镜像”的相互作用很弱。

#### 衍射光栅与伍德异常

弗洛凯-布洛赫理论也完美地描述了[衍射光栅](@entry_id:178037)等周期性散射问题。当一束[平面波](@entry_id:189798)入射到周期为 $\Lambda$ 的[光栅](@entry_id:178037)上时，散射场可以被展开为一系列离散的**[衍射级](@entry_id:174263)**（diffraction orders），每个[衍射级](@entry_id:174263)（由整数 $m$ 标记）的切向波矢为 $k_{x,m} = k_x + 2\pi m/\Lambda$，其中 $k_x$ 是入射波的切向[波矢](@entry_id:178620)。

每个[衍射级](@entry_id:174263)的纵向[波矢](@entry_id:178620) $k_{z,m}$ 由[色散关系](@entry_id:140395) $k_{z,m} = \sqrt{k^2 - k_{x,m}^2}$ 决定。如果 $k_{z,m}$ 为实数，该[衍射级](@entry_id:174263)为传播波；如果 $k_{z,m}$ 为纯虚数，则为倏逝波。从传播到倏逝的[临界点](@entry_id:144653)发生在 $k_{z,m} = 0$ 时，即 $|k_{x,m}| = k$。这个条件被称为**瑞利截止**（Rayleigh cut-off）。当改变[入射角](@entry_id:192705)或频率使得某个[衍射级](@entry_id:174263)恰好满足瑞利截止条件时，衍射效率会发生急剧变化，这种现象被称为**伍德异常**（Wood's anomaly）。从数学上看，瑞利截止条件对应于[色散关系](@entry_id:140395)中[平方根函数](@entry_id:184630)的**[支点](@entry_id:166575)**（branch points）。散射场的解析性质在这些点上发生突变，从而导致了可观测到的异常现象。

#### [平面波展开法](@entry_id:146091)的收敛性问题

**[平面波展开法](@entry_id:146091)**（Plane Wave Expansion, PWE）是一种经典的能带计算方法，它将[介电常数](@entry_id:146714)和场都展开为傅里叶级数。当[介电常数](@entry_id:146714) $\epsilon(\mathbf{r})$ 存在阶跃不连续时（例如空气和介质的界面），其[傅里叶系数衰减](@entry_id:274275)缓慢（$O(1/|\mathbf{G}|)$），并且截断的[傅里叶级数](@entry_id:139455)在界面附近表现出**[吉布斯现象](@entry_id:138701)**（Gibbs phenomenon）的[振荡](@entry_id:267781)。

一个简单的PWE实现，即直接用截断的[傅里叶级数](@entry_id:139455)相乘来计算 $\mathbf{D} = \epsilon_0 \epsilon \mathbf{E}$ 的傅里叶系数（这在[谱域](@entry_id:755169)中是一个卷积），收敛会非常缓慢。问题的根源在于，这种“直接”卷积规则没有正确地处理场分量在界面上的连续性。例如，在介质界面上，$D_n$ (法向位移场)和 $E_t$ ([切向电场](@entry_id:267195))是连续的，而 $E_n$ 和 $D_t$ 是不连续的。乘积 $D_n = \epsilon_0 \epsilon E_n$ 是一个[连续函数](@entry_id:137361)，但它由两个在同一位置不连续的函数相乘得到。

为了解决这个问题，需要采用更复杂的**[傅里叶分解](@entry_id:160101)**（Fourier factorization）方法。该方法根据不同场分量和乘积的连续性，应用不同的卷积规则（“直接规则”或“逆规则”），从而在数值上正确地体现麦克斯韦方程的[界面条件](@entry_id:750725)。这种方法可以显著改善PWE的收敛速度和精度。