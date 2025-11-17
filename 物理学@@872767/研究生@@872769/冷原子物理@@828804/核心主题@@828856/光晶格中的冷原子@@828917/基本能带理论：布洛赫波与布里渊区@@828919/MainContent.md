## 引言
在晶体等周期性结构中，粒子的行为遵循着与自由空间截然不同的规则。这些规则的核心便是[能带理论](@entry_id:139801)，它解释了为何固体材料会呈现出导体、[半导体](@entry_id:141536)或绝缘体等迥异的电学特性。能带理论的核心思想是，原本孤立的[原子能级](@entry_id:148255)在形成晶体后会展宽为连续的能量区间（能带），并在某些能量处形成不允许任何电子态存在的[禁区](@entry_id:175956)（[带隙](@entry_id:191975)）。然而，这些能带与[带隙](@entry_id:191975)是如何形成的？它们又如何决定了材料的宏观性质？

本文旨在系统地回答这些问题，为读者构建一个关于[能带理论](@entry_id:139801)的完整知识框架。我们将分三步深入探索这个迷人领域。首先，在**“原理与机制”**一章中，我们将从量子力学第一性原理出发，介绍[布洛赫定理](@entry_id:137461)和布里渊区的概念，并运用[近自由电子模型](@entry_id:138124)和[紧束缚模型](@entry_id:143446)揭示能带[结构的起源](@entry_id:159888)。接着，在**“应用与[交叉](@entry_id:147634)学科联系”**一章中，我们将展示[能带理论](@entry_id:139801)如何应用于分析真实材料（如[石墨烯](@entry_id:143512)）、解释[半经典动力学](@entry_id:140913)（如[布洛赫振荡](@entry_id:138656)），并如何延伸至拓扑物理、[光子](@entry_id:145192)学和[声学](@entry_id:265335)等前沿交叉领域。最后，**“动手实践”**部分提供了一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。

现在，让我们从构成这一切基础的核心原理开始。

## 原理与机制

在晶体等周期性结构中，粒子的量子行为与自由空间中的行为截然不同。单个原子或分子的离散能级在晶体中会展宽为连续的能量区间，即所谓的**能带（energy bands）**，而在某些能量范围内，则不存在任何定态，这些区域被称为**[带隙](@entry_id:191975)（bandgaps）**。[能带结构](@entry_id:139379)决定了材料的导电性、光学特性及热力学性质。本章旨在阐述能带理论的核心原理与机制，从[布洛赫定理](@entry_id:137461)出发，探讨[布里渊区](@entry_id:142395)的几何结构，并介绍两种互补的理论模型——[近自由电子模型](@entry_id:138124)和[紧束缚模型](@entry_id:143446)，以揭示能带与[带隙](@entry_id:191975)的形成机制。

### [晶格](@entry_id:196752)周期性与布洛赫定理

周期性势场中粒子运动的理论基石是**[布洛赫定理](@entry_id:137461)（Bloch's Theorem）**。考虑一个粒子在[三维晶格](@entry_id:188146)中运动，其所处的势能 $V(\mathbf{r})$ 具有[晶格](@entry_id:196752)的平移对称性，即对于任意[晶格矢量](@entry_id:161583) $\mathbf{R}$，都有 $V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$。体系的[哈密顿量](@entry_id:172864) $H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$ 同样具有这种对称性。

我们可以定义一个[平移算符](@entry_id:756122) $T_{\mathbf{R}}$，其作用于任意函数 $\psi(\mathbf{r})$ 上会使其坐标平移一个[晶格矢量](@entry_id:161583) $\mathbf{R}$，即 $T_{\mathbf{R}}\psi(\mathbf{r}) = \psi(\mathbf{r} + \mathbf{R})$。由于[哈密顿量](@entry_id:172864)在平移操作下保持不变，它与[平移算符](@entry_id:756122)对易：$[H, T_{\mathbf{R}}] = 0$。根据量子力学基本原理，这意味着[哈密顿量](@entry_id:172864)与所有[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 拥有一组共同的[本征函数](@entry_id:154705)。

一个函数的集合若要成为所有 $T_{\mathbf{R}}$ 的共同本征函数，其[本征值](@entry_id:154894)必须满足特定的[群表示](@entry_id:156757)关系。对于平移群，其[不可约表示](@entry_id:263310)是一维的。因此，[哈密顿量](@entry_id:172864)的本征函数 $\psi(\mathbf{r})$ 必然满足 $T_{\mathbf{R}}\psi(\mathbf{r}) = \lambda_{\mathbf{R}}\psi(\mathbf{r})$，其中 $\lambda_{\mathbf{R}}$ 是与 $\mathbf{R}$ 相关的复数[本征值](@entry_id:154894)。由于连续平移的复合性 ($T_{\mathbf{R}_1}T_{\mathbf{R}_2} = T_{\mathbf{R}_1+\mathbf{R}_2}$)，[本征值](@entry_id:154894)必须满足 $\lambda_{\mathbf{R}_1}\lambda_{\mathbf{R}_2} = \lambda_{\mathbf{R}_1+\mathbf{R}_2}$。这种关系唯一地导向了[本征值](@entry_id:154894)的指数形式 $\lambda_{\mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}}$，其中 $\mathbf{k}$ 是一个连续的矢量，被称为**晶矢**或**[晶体动量](@entry_id:136369)（crystal momentum）**。

因此，[能量本征态](@entry_id:152154) $\psi(\mathbf{r})$ 必须满足如下条件：
$$ \psi(\mathbf{r} + \mathbf{R}) = e^{i\mathbf{k} \cdot \mathbf{R}} \psi(\mathbf{r}) $$
这正是布洛赫定理的一种表述 [@problem_id:2830842]。它意味着，尽管[波函数](@entry_id:147440)本身不一定是周期的，但它在一个[晶格矢量](@entry_id:161583)平移下的变化只是获得一个相位因子。

布洛赫定理还有一种等价且更具物理洞察力的形式。我们可以将任何满足上述条件的[波函数](@entry_id:147440) $\psi(\mathbf{r})$ 写成如下形式：
$$ \psi_{\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k} \cdot \mathbf{r}} u_{\mathbf{k}}(\mathbf{r}) $$
其中，$u_{\mathbf{k}}(\mathbf{r})$ 是一个与[晶格](@entry_id:196752)具有相同周期性的函数，即 $u_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = u_{\mathbf{k}}(\mathbf{r})$。这表明，晶体中的电子[波函数](@entry_id:147440)是一个**[布洛赫波](@entry_id:144558)（Bloch wave）**，其形态为一个自由粒子平面波 $e^{i\mathbf{k} \cdot \mathbf{r}}$ 被一个具有[晶格](@entry_id:196752)周期性的函数 $u_{\mathbf{k}}(\mathbf{r})$ 所调制。晶矢 $\mathbf{k}$ 成为了标记[量子态](@entry_id:146142)的一个良[好量子数](@entry_id:262514)。值得注意的是，晶体动量 $\mathbf{k}$ 并非粒子的真实动量（其算符为 $\hat{\mathbf{p}} = -i\hbar\nabla$）。由于[势能](@entry_id:748988) $V(\mathbf{r})$ 的存在，真实动量通常不守恒，因为它与[哈密顿量](@entry_id:172864)不对易。晶体动量是平移对称性的产物，它描述的是[波函数](@entry_id:147440)在[晶格](@entry_id:196752)平移下的变换性质。

### [倒易空间](@entry_id:754151)与[布里渊区](@entry_id:142395)

[布洛赫定理](@entry_id:137461)揭示了晶矢 $\mathbf{k}$ 的核心地位。所有与晶体动量相关的计算和分析都在一个被称为**[倒易空间](@entry_id:754151)（reciprocal space）**的数学空间中进行。

对于一个由[原胞基矢](@entry_id:142930) $\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\}$ 定义的实空间[晶格](@entry_id:196752)，其对应的**倒易晶格（reciprocal lattice）**由一组矢量 $\mathbf{G}$ 构成，这些矢量满足条件 $e^{i\mathbf{G} \cdot \mathbf{R}} = 1$ 对于所有实空间[晶格矢量](@entry_id:161583) $\mathbf{R}$ 都成立。[倒易晶格](@entry_id:136718)本身也是一个布拉维格，其[基矢](@entry_id:199546) $\{\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3\}$ 可以通过关系 $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij}$ 找到。

从[布洛赫定理](@entry_id:137461)的相位因子 $e^{i\mathbf{k} \cdot \mathbf{R}}$ 可以看出，如果我们将晶矢 $\mathbf{k}$ 替换为 $\mathbf{k}' = \mathbf{k} + \mathbf{G}$（其中 $\mathbf{G}$ 是任意一个[倒易晶格矢量](@entry_id:263351)），相位因子将变为 $e^{i(\mathbf{k}+\mathbf{G}) \cdot \mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}}e^{i\mathbf{G} \cdot \mathbf{R}} = e^{i\mathbf{k} \cdot \mathbf{R}}$。这意味着晶矢 $\mathbf{k}$ 和 $\mathbf{k} + \mathbf{G}$ 描述的是完全相同的平移对称性，它们在物理上是等效的。因此，为了避免重复描述，我们只需考虑倒易空间中的一个[原胞](@entry_id:159354)即可。

习惯上，我们选择一个具有高度对称性的特定原胞，即**[第一布里渊区](@entry_id:269110)（First Brillouin Zone, FBZ）**。[第一布里渊区](@entry_id:269110)被定义为[倒易空间](@entry_id:754151)中围绕原点 $\mathbf{k}=0$ 的**[维格纳-赛兹原胞](@entry_id:137574)（Wigner-Seitz cell）**。几何上，它是倒易空间中所有这样的点的集合：这些点到原点的距离比它们到任何其他倒易格点 $\mathbf{G}$ 的距离都要近 [@problem_id:2865825]。构建[第一布里渊区](@entry_id:269110)的方法是，从原点向所有其他倒易格点作连线，然后画出这些连线的中垂面（二维中为[中垂线](@entry_id:163148)）。由这些中垂面所包围的最小体积（或面积）区域就是[第一布里渊区](@entry_id:269110)。

作为一个具体的例子，我们来构造一个二维三角[晶格](@entry_id:196752)的[第一布里渊区](@entry_id:269110) [@problem_id:1229401]。设实空间[原胞基矢](@entry_id:142930)为 $\mathbf{a}_1 = a(1, 0)$ 和 $\mathbf{a}_2 = a(1/2, \sqrt{3}/2)$。通过求解 $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij}$，可得倒易晶格[基矢](@entry_id:199546)为 $\mathbf{b}_1 = \frac{2\pi}{a}(1, -1/\sqrt{3})$ 和 $\mathbf{b}_2 = \frac{2\pi}{a}(0, 2/\sqrt{3})$。最短的非零倒易格矢是 $\mathbf{b}_1$, $\mathbf{b}_2$, $\mathbf{b}_1-\mathbf{b}_2$ 等六个矢量。例如，我们考虑沿正 $k_y$ 轴方向最短的倒易格矢 $\mathbf{G} = \mathbf{b}_2 = (0, 4\pi/(a\sqrt{3}))$。[第一布里渊区](@entry_id:269110)的边界由条件 $\mathbf{k} \cdot \mathbf{G} = \frac{1}{2}|\mathbf{G}|^2$ 给出。将 $\mathbf{k}=(k_x, k_y)$ 和 $\mathbf{G}$ 代入，我们得到 $k_y \cdot (4\pi/(a\sqrt{3})) = \frac{1}{2}(4\pi/(a\sqrt{3}))^2$，解得 $k_y = 2\pi/(a\sqrt{3})$。这条水平线构成了六边形布里渊区的一个面。对其他最短的 $\mathbf{G}$ 矢量重复此过程，即可得到完整的六边形[第一布里渊区](@entry_id:269110)。

### [近自由电子模型](@entry_id:138124)与[带隙](@entry_id:191975)的形成

为了求解特定[周期势](@entry_id:140652)下的[能量本征值](@entry_id:144381) $E_n(\mathbf{k})$，即**[能带结构](@entry_id:139379)**，物理学家发展了两种极限近似方法。第一种是**[近自由电子模型](@entry_id:138124)（nearly-free electron model）**，它从[自由电子气](@entry_id:145649)出发，将[晶格](@entry_id:196752)[势能](@entry_id:748988) $V(\mathbf{r})$ 视为一个微扰。

在没有任何势能的情况下（$V(\mathbf{r})=0$），电子是自由的，其[能量色散关系](@entry_id:145014)为 $E(\mathbf{k}) = \frac{\hbar^2 |\mathbf{k}|^2}{2m}$。这是一个在 $\mathbf{k}$ 空间中连续的抛物面。为了将这个无限延伸的色散关系与[晶格](@entry_id:196752)的周期性对应起来，我们采用**[简约布里渊区方案](@entry_id:265307)（reduced zone scheme）**。任何一个[波矢](@entry_id:178620) $\mathbf{k}_{\text{unf}}$ 都可以被唯一地写成 $\mathbf{k}_{\text{unf}} = \mathbf{k} + \mathbf{G}$，其中 $\mathbf{k}$ 位于[第一布里渊区](@entry_id:269110)内，$\mathbf{G}$ 是某个倒易格矢。通过这种方式，我们将所有自由电子态“折叠”回[第一布里渊区](@entry_id:269110)。这导致在FBZ内部，每个 $\mathbf{k}$ 点都对应着无穷多个能量状态，其色散关系为 $E_{\mathbf{G}}(\mathbf{k}) = \frac{\hbar^2 |\mathbf{k}+\mathbf{G}|^2}{2m}$ [@problem_id:2865825]。这些抛物线在[布里渊区](@entry_id:142395)内部和边界处相互交叠，形成简并。

现在，我们引入一个微弱的周期性势能 $V(\mathbf{r})$。根据微扰理论，这个势能主要会影响那些简并或[近简并](@entry_id:172107)的态。简并发生在满足 $E_{\mathbf{G}}(\mathbf{k}) = E_{\mathbf{G'}}(\mathbf{k})$ 的地方，即 $|\mathbf{k}+\mathbf{G}|^2 = |\mathbf{k}+\mathbf{G'}|^2$。特别重要的简并发生在布里渊区的边界上。[布里渊区](@entry_id:142395)的边界正满足条件 $|\mathbf{k}| = |\mathbf{k}-\mathbf{G}|$，这等价于 $2\mathbf{k} \cdot \mathbf{G} = |\mathbf{G}|^2$，这正是晶体[X射线衍射](@entry_id:147790)的**[布拉格条件](@entry_id:271151)**。在这些边界点，自由电子态 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 和 $e^{i(\mathbf{k}-\mathbf{G})\cdot\mathbf{r}}$ 具有相同的能量。

周期性[势能](@entry_id:748988) $V(\mathbf{r})$ 可以展开为傅里叶级数 $V(\mathbf{r}) = \sum_{\mathbf{G}} V_{\mathbf{G}} e^{i\mathbf{G}\cdot\mathbf{r}}$。势能在两个[平面波](@entry_id:189798)态 $| \mathbf{k}' \rangle$ 和 $| \mathbf{k} \rangle$ 之间的[矩阵元](@entry_id:186505)为 $\langle \mathbf{k}' | V | \mathbf{k} \rangle = V_{\mathbf{k}' - \mathbf{k}}$。因此，一个傅里叶分量 $V_{\mathbf{G}}$ 会耦合波矢相差 $\mathbf{G}$ 的两个态。恰好在[布里渊区](@entry_id:142395)边界上简并的态，如 $| \mathbf{k} \rangle$ 和 $| \mathbf{k}-\mathbf{G} \rangle$，就会被[势能](@entry_id:748988)分量 $V_{\mathbf{G}}$ 和 $V_{-\mathbf{G}}$ 耦合起来。

考虑一个简单的一维情况，在[布里渊区](@entry_id:142395)边界 $k = \pi/a$ 处，态 $e^{i\pi x/a}$ 和 $e^{-i\pi x/a}$ 简并。对应的倒易格矢为 $G=2\pi/a$。我们可以构建一个 $2 \times 2$ 的[哈密顿量](@entry_id:172864)矩阵来描述这两个态的混合 [@problem_id:2915043]。在基 $\{|k\rangle, |k-G\rangle\}$ 下，[哈密顿量](@entry_id:172864)矩阵为：
$$ \mathbf{H} = \begin{pmatrix} \frac{\hbar^2 k^2}{2m}  V_G \\ V_G^*  \frac{\hbar^2(k-G)^2}{2m} \end{pmatrix} $$
在[布里渊区](@entry_id:142395)边界 $k=G/2=\pi/a$，对角元相等。求解该矩阵的[本征值](@entry_id:154894)，得到两个能量：
$$ E_{\pm} = \frac{\hbar^2(\pi/a)^2}{2m} \pm |V_G| $$
原本简并的能级分裂为两个，它们之间形成了一个宽度为 $\Delta E = 2|V_G|$ 的能量区间，其中不存在[定态](@entry_id:137260)。这就是**[带隙](@entry_id:191975)**。[带隙](@entry_id:191975)的大小由与该布里渊区[边界对应](@entry_id:167571)的倒易格矢 $\mathbf{G}$ 的势能傅里叶分量 $V_G$ 的大小决定。

这个原理是普适的。例如，对于一个一维[势能](@entry_id:748988) $V(x) = V_1 \sin(2\pi x/a) + V_2 \cos(4\pi x/a)$ [@problem_id:1229460]，[第一布里渊区](@entry_id:269110)边界（$k=\pi/a$）对应的倒易格矢为 $G=2\pi/a$。我们需要计算 $V_G = \frac{1}{a}\int_0^a V(x) e^{-iGx} dx$。计算表明，只有[势能](@entry_id:748988)中与 $e^{\pm iGx}$ 相关的项，即 $V_1 \sin(Gx) = V_1(e^{iGx}-e^{-iGx})/(2i)$，对 $V_G$ 有贡献。积分结果为 $V_G = V_1/(2i)$。因此，在[第一布里渊区](@entry_id:269110)边界打开的[带隙](@entry_id:191975)大小为 $\Delta E = 2|V_G| = 2|V_1/(2i)| = |V_1|$。$V_2$ 项的周期是 $a/2$，它对应于 $G=4\pi/a$，会在第二布里渊区的边界打开[带隙](@entry_id:191975)。

[带隙](@entry_id:191975)的形成伴随着[波函数](@entry_id:147440)性质的深刻变化 [@problem_id:2830842] [@problem_id:1229405]。在[布里渊区](@entry_id:142395)边界，分裂后的两个[本征态](@entry_id:149904)不再是行波 $e^{\pm ikx}$，而是它们的线性组合——[驻波](@entry_id:148648)。能量较低的态 $\psi_-$ 对应于 $\cos(\pi x/a)$ 或 $\sin(\pi x/a)$ 型的[驻波](@entry_id:148648)，其电荷密度倾向于集中在[势能](@entry_id:748988) $V(x)$ 的谷底，从而降低了能量。能量较高的态 $\psi_+$ 则对应于另一种[驻波](@entry_id:148648)，其[电荷密度](@entry_id:144672)倾向于集中在势能的峰顶，从而提升了能量。作为驻波，这些在能带边沿的态不携带净的[粒子流](@entry_id:753205)，其**[概率流密度](@entry_id:152013)** $j(x)$ 严格为零。例如，对于一维势 $V(x) = 2V_1 \cos(2\pi x/a)$ ($V_1>0$)，在 $k=\pi/a$ 处的较高[能量本征态](@entry_id:152154)是 $\psi(x) \propto \cos(\pi x/a)$，这是一个实函数，其[概率流密度](@entry_id:152013) $j(x) = \frac{\hbar}{2mi}(\psi^*\psi' - \psi\psi'^*)$ 显然为零 [@problem_id:1229405]。

在更高维度和更复杂的[晶格](@entry_id:196752)中，简并可能涉及三个或更多的态。例如，在一个二维三角[晶格](@entry_id:196752)中，[第一布里渊区](@entry_id:269110)的高对称K点处，有三个自由电子态简并。一个微弱的周期势会将此三重简并破除。通过在三维简并[子空间](@entry_id:150286)中构建[哈密顿量](@entry_id:172864)矩阵，可以发现能级分裂为一个非[简并态](@entry_id:274678)和两个[简并态](@entry_id:274678)，其能量分裂正比于势的相关傅里叶分量 $U_0$ [@problem_id:1229378]。

### [紧束缚模型](@entry_id:143446)

与[近自由电子模型](@entry_id:138124)相对的另一个极端是**[紧束缚模型](@entry_id:143446)（tight-binding model）**。该模型假设电子被紧密地束缚在各自的原子周围，[晶格](@entry_id:196752)[势能](@entry_id:748988)非常强。我们从孤立原子的[波函数](@entry_id:147440)（原子轨道）出发，将整个晶体的[波函数](@entry_id:147440)看作是这些[原子轨道](@entry_id:140819)的[线性组合](@entry_id:154743)（LCAO）。

考虑一个[一维单原子链](@entry_id:269574)，格点间距为 $a$。每个格点 $n$ 上有一个[原子轨道](@entry_id:140819) $|n\rangle$，其孤立时的能量为 $\epsilon_0 = \langle n|H|n \rangle$。当原子组成晶体后，电子有可能从一个原子“隧穿”或“跳跃”到相邻的原子。这种相互作用由**跳跃积分（hopping integral）** $t = \langle n|H|n\pm 1 \rangle$ 来描述，我们通常只考虑最近邻跳跃。

根据布洛赫定理，晶体中的[本征态](@entry_id:149904) $|\psi_k\rangle$ 可以写成原子轨道的线性组合：
$$ |\psi_k\rangle = \frac{1}{\sqrt{N}} \sum_n e^{ikna} |n\rangle $$
其中 $N$ 是原子总数，相位因子 $e^{ikna}$ 保证了态满足布洛赫条件。该态的能量 $E(k)$ 可以通过求解薛定谔方程 $H|\psi_k\rangle = E(k)|\psi_k\rangle$ 得到。将该方程左乘 $\langle m|$，我们有：
$$ \sum_n e^{ikna} \langle m|H|n \rangle = E(k) e^{ikma} $$
利用[哈密顿矩阵元](@entry_id:201928) $\langle m|H|n \rangle = \epsilon_0 \delta_{mn} + t(\delta_{m, n+1} + \delta_{m, n-1})$，上式左边变为：
$$ e^{ik(m-1)a}t + e^{ikma}\epsilon_0 + e^{ik(m+1)a}t = e^{ikma}(\epsilon_0 + t(e^{-ika} + e^{ika})) $$
两边消去 $e^{ikma}$，并利用[欧拉公式](@entry_id:176440)，我们得到一维[紧束缚模型](@entry_id:143446)的[能带色散](@entry_id:138609)关系 [@problem_id:2866099]：
$$ E(k) = \epsilon_0 + 2t\cos(ka) $$
这个结果表明，原本分立的原子能级 $\epsilon_0$ 在晶体中展宽成了一个能量范围从 $\epsilon_0 - 2|t|$ 到 $\epsilon_0 + 2|t|$ 的连续能带，能带的宽度为 $4|t|$。带宽正比于跳跃积分 $t$ 的大小，反映了原子间[轨道](@entry_id:137151)交叠的程度。

### 万尼尔函数：[布洛赫波](@entry_id:144558)的实空间图像

[布洛赫波](@entry_id:144558)是在 $\mathbf{k}$ 空间中描述电子态的自然语言，它们是延展于整个晶体的。为了获得一个更局域化的[实空间](@entry_id:754128)图像，我们可以引入**万尼尔函数（Wannier functions）**。一个位于[晶胞](@entry_id:143489) $\mathbf{R}_m$ 的万尼尔函数 $|W_m\rangle$ 定义为[布洛赫波函数](@entry_id:144223) $|\psi_{\mathbf{k}}\rangle$ 的[傅里叶变换](@entry_id:142120)：
$$ |W_m\rangle = \frac{V_{\text{cell}}}{(2\pi)^d} \int_{\text{FBZ}} d\mathbf{k} \, e^{-i\mathbf{k}\cdot\mathbf{R}_m} |\psi_{\mathbf{k}}\rangle $$
万尼尔函数构成了一组正交归一的基，它们在[实空间](@entry_id:754128)中是局域化的，每个 $|W_m\rangle$ 大致定域在[晶胞](@entry_id:143489) $\mathbf{R}_m$ 附近。它们可以被看作是晶体中的“广义[原子轨道](@entry_id:140819)”。[布洛赫态](@entry_id:147552)和万尼尔态是描述相同物理的两种等价的表象，分别在[倒易空间](@entry_id:754151)和实空间中提供了最简洁的图像。在包含多个原子或[轨道](@entry_id:137151)的复杂模型中（如[Su-Schrieffer-Heeger模型](@entry_id:139249)），计算万尼尔函数可以揭示化学键和[电荷分布](@entry_id:144400)的深刻信息 [@problem_id:1229337]。

### 对称性与强制简并

在[近自由电子模型](@entry_id:138124)中我们看到，微弱的周期势通常会破除[布里渊区](@entry_id:142395)边界上的简并。然而，这并非总是如此。某些[晶体对称性](@entry_id:198772)可以“保护”能带在特定点或线上必须简并。

一个重要的例子是**非点式对称性（non-symmorphic symmetries）**，如滑移面或[螺旋轴](@entry_id:268289)，它们是点群操作（如旋转、反射）与非整数[晶格矢量](@entry_id:161583)平移的组合。考虑一个二维矩形[晶格](@entry_id:196752)，它具有一个滑移反射对称性 $g$，其操作为 $g\mathbf{r} = (x+a_1/2, -y)$。设体系同时具有时间反演对称性 $\mathcal{T}$。在[布里渊区](@entry_id:142395)边界的高[对称点](@entry_id:174836) $X = (\pi/a_1, 0)$，滑移反射算符 $G$ 和时间反演算符 $\mathcal{T}$ 的组合形成一个新的[反幺正算符](@entry_id:197532) $\Theta = G\mathcal{T}$。

可以证明，在 $X$ 点的任何[布洛赫态](@entry_id:147552)上，这个组合算符作用两次会得到 $-1$，即 $\Theta^2 = -1$ [@problem_id:1229425]。这个性质类似于自旋 $1/2$ 粒子[时间反演](@entry_id:182076)算符的性质（克莱默斯定理）。它导致一个必然的结论：在 $X$ 点，所有能带都必须至少是两重简并的。对于任何一个本征态 $|\Psi_1\rangle$，它的“伙伴”态 $|\Psi_2\rangle = \Theta|\Psi_1\rangle$ 与它正交且能量相同。这种由对称性保证的简并是晶体[能带结构](@entry_id:139379)的一个深刻特征，它超越了[微扰理论](@entry_id:138766)的范畴，展示了对称性在凝聚态物理中的强大威力。