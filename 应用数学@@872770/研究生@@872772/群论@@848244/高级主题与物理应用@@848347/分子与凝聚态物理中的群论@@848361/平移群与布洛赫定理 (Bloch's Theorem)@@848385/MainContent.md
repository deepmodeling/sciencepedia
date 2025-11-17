## 引言
固态物质的宏观性质，从导电性到光学响应，都深植于其微观世界中电子的行为。在晶体这一高度有序的结构中，理解电子运动规律的关键在于认识其最根本的对称性——离散[平移对称性](@entry_id:171614)。布洛赫定理正是这一对称性在量子力学中的深刻体现，它为描述周期性势场中的粒子行为提供了普适的理论框架，并构成了整个能带理论的基石。然而，从抽象的对称性群论到具体的[材料性质预测](@entry_id:751725)，这其中存在着一条需要严谨推导和概念辨析的知识路径。初学者往往困惑于[晶体动量](@entry_id:136369)与力学动量的区别，或是难以将离域的[布洛赫波](@entry_id:144558)与局域的原子轨道直观地联系起来。

本文旨在系统性地解决这些问题。我们将带领读者深入探索平移群与[布洛赫定理](@entry_id:137461)的内在联系及其广泛应用。在“原理与机制”一章中，我们将从群论出发，严格推导布洛赫定理，阐明晶体动量、能带和[瓦尼尔函数](@entry_id:145994)等核心概念，并探讨理想模型的局限性。随后，在“应用与交叉学科联系”一章中，我们将展示如何运用这些原理来计算[能带结构](@entry_id:139379)、解释宏观物理性质，并揭示其在[光子](@entry_id:145192)学、拓扑物理等前沿领域的强大生命力。最后，通过“动手实践”部分提供的一系列计算问题，读者将有机会亲手应用所学知识，将理论框架转化为解决实际问题的能力。

## 原理与机制

本章旨在系统性地阐述晶体平移对称性的深刻物理内涵，即布洛赫定理，并探讨其在描述晶体中电子行为时的核心作用。我们将从[基本对称性](@entry_id:161256)原理出发，构建布洛赫定理的理论框架，阐释其关键概念如晶体动量和能带，并进一步探讨[布洛赫态](@entry_id:147552)的正交性、完备性及其与局域化的[瓦尼尔函数](@entry_id:145994)之间的对偶关系。最后，我们将审视理想模型的局限性，讨论在更复杂的物理情景下，如存在无序、外[磁场](@entry_id:153296)或超结构时，[布洛赫定理](@entry_id:137461)如何被修正或失效。

### [平移对称性](@entry_id:171614)与[布洛赫定理](@entry_id:137461)

在量子力学中，系统的对称性与其[守恒量](@entry_id:150267)和本征态的性质密切相关。对于一个理想的完美晶体，其最根本的对称性是原子实离子构成的[势场](@entry_id:143025) $V(\mathbf{r})$ 所具有的**离散[平移不变性](@entry_id:195885)**。这意味着[势场](@entry_id:143025)在沿着任意布拉维格矢 $\mathbf{R}$ 平移后保持不变：
$$
V(\mathbf{r}+\mathbf{R}) = V(\mathbf{r})
$$
其中，布拉维格矢 $\mathbf{R}$ 是基元格矢 $\mathbf{a}_i$ 的整数[线性组合](@entry_id:154743)，即 $\mathbf{R} = n_1\mathbf{a}_1 + n_2\mathbf{a}_2 + n_3\mathbf{a}_3$，其中 $n_i$ 为整数。

描述晶体中单个电子的[哈密顿算符](@entry_id:144286)为：
$$
H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})
$$
其中 $m$ 是电子质量，$\hbar$ 是约化普朗克常数。由于拉普拉斯算符 $\nabla^2$ 在坐标平移下不变，而势函数 $V(\mathbf{r})$ 具有格点周期性，因此[哈密顿算符](@entry_id:144286) $H$ 与任意格点[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 是对易的。[平移算符](@entry_id:756122)的定义为 $(T_{\mathbf{R}}\psi)(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R})$。[对易关系](@entry_id:136780) $[H, T_{\mathbf{R}}] = 0$ 意味着我们可以找到一组同时是 $H$ 和所有 $T_{\mathbf{R}}$ 的共同[本征函数](@entry_id:154705)。

[平移算符](@entry_id:756122)集合 $\{T_{\mathbf{R}}\}$ 构成一个阿贝尔群（因为 $T_{\mathbf{R}}T_{\mathbf{R}'} = T_{\mathbf{R}+\mathbf{R}'} = T_{\mathbf{R}'}T_{\mathbf{R}}$）。根据群论，阿贝尔群的[不可约表示](@entry_id:263310)是一维的。因此，对于一个共同[本征函数](@entry_id:154705) $\psi(\mathbf{r})$，其在[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 作用下的[本征值](@entry_id:154894) $\lambda(\mathbf{R})$ 是一个复数。由于 $T_{\mathbf{R}}$ 是幺正算符（保持[波函数归一化](@entry_id:152806)），其[本征值](@entry_id:154894)的模必须为1，即 $|\lambda(\mathbf{R})|=1$。此外，从平移的复合性质可知，[本征值](@entry_id:154894)必须满足同态关系 $\lambda(\mathbf{R}+\mathbf{R}') = \lambda(\mathbf{R})\lambda(\mathbf{R}')$。满足此性质的唯一[连续函数](@entry_id:137361)形式为 $\lambda(\mathbf{R}) = \exp(i\mathbf{k}\cdot\mathbf{R})$，其中 $\mathbf{k}$ 是一个实数向量。

因此，[哈密顿量](@entry_id:172864)的任何本征态 $\psi(\mathbf{r})$ 都可以被选择为满足以下条件：
$$
\psi(\mathbf{r}+\mathbf{R}) = T_{\mathbf{R}}\psi(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{R}} \psi(\mathbf{r})
$$
这个关系式是布洛赫定理的一种表述。它表明，在[晶格](@entry_id:196752)平移下，[波函数](@entry_id:147440)仅仅获得一个相位因子。向量 $\mathbf{k}$ 被称为**晶体动量**或**波矢**，它标记了平移群的[不可约表示](@entry_id:263310)。

我们可以进一步揭示这些本征函数的形式。定义一个函数 $u_{\mathbf{k}}(\mathbf{r}) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi(\mathbf{r})$。考察它在平移 $\mathbf{R}$ 下的行为：
$$
u_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})}\psi(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot\mathbf{r}}e^{-i\mathbf{k}\cdot\mathbf{R}} (e^{i\mathbf{k}\cdot\mathbf{R}}\psi(\mathbf{r})) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r})
$$
这表明函数 $u_{\mathbf{k}}(\mathbf{r})$ 具有与[晶格](@entry_id:196752)完全相同的周期性。因此，[哈密顿量](@entry_id:172864)的本征函数可以写成一个平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 与一个具有[晶格](@entry_id:196752)周期性的函数 $u_{\mathbf{k}}(\mathbf{r})$ 的乘积。这便是**[布洛赫定理](@entry_id:137461)**最常见的表述 [@problem_id:2802925]：

**对于周期性势场中的粒子，其能量[本征函数](@entry_id:154705) $\psi_{n\mathbf{k}}(\mathbf{r})$ 可以写成如下形式：**
$$
\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})
$$
**其中 $u_{n\mathbf{k}}(\mathbf{r})$ 是一个具有[晶格](@entry_id:196752)周期性的函数，即 $u_{n\mathbf{k}}(\mathbf{r}+\mathbf{R}) = u_{n\mathbf{k}}(\mathbf{r})$。**

这里的整数 $n$ 称为**能带指数**，它用于区分在同一个波矢 $\mathbf{k}$ 下可能存在的不同[能量本征态](@entry_id:152154)。[能量本征值](@entry_id:144381) $E$ 现在依赖于 $n$ 和 $\mathbf{k}$，记作 $E_n(\mathbf{k})$，这便是**[能带结构](@entry_id:139379)**。

值得注意的是，晶体动量 $\mathbf{k}$ 的定义不是唯一的。如果我们用 $\mathbf{k}' = \mathbf{k} + \mathbf{G}$ 替换 $\mathbf{k}$，其中 $\mathbf{G}$ 是任意一个**[倒格矢](@entry_id:263351)**（满足 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$ 对所有 $\mathbf{R}$ 成立），则平移的[本征值](@entry_id:154894)不变：$e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$。这意味着 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 描述的是同一个平移对称性表示，它们是等价的。因此，我们只需要考虑倒易空间中的一个原胞即可，通常选择的是**[第一布里渊区](@entry_id:269110)** (First Brillouin Zone, BZ)。能量 $E_n(\mathbf{k})$ 和[波函数](@entry_id:147440)在倒易空间中也具有周期性：$E_n(\mathbf{k}+\mathbf{G}) = E_n(\mathbf{k})$。

### [布洛赫态](@entry_id:147552)的性质与诠释

#### 正交性与完备性

[布洛赫函数](@entry_id:189422)作为[哈密顿量](@entry_id:172864)的本征函数，构成了一个完备的正交归一基。对于在整个晶体体积 $V$ 上归一化的[布洛赫函数](@entry_id:189422)，其正交归一性关系为：
$$
\int_V \psi_{n\mathbf{k}}^*(\mathbf{r}) \psi_{n'\mathbf{k}'}(\mathbf{r}) \, d^3\mathbf{r} = \delta_{nn'} \delta_{\mathbf{k}\mathbf{k}'}
$$
其中 $\delta$ 是克罗内克符号。$\delta_{nn'}$ 表明不同能带的态是正交的，而 $\delta_{\mathbf{k}\mathbf{k}'}$ 表明对于同一能带，不同[晶体动量](@entry_id:136369)的态也是正交的。

这个正交性有一个重要的推论。即使元胞[周期函数](@entry_id:139337) $u_{n\mathbf{k}}(\mathbf{r})$ 和 $u_{n\mathbf{k}'}(\mathbf{r})$ 在单个[原胞](@entry_id:159354)内的积分不正交，对应的[布洛赫函数](@entry_id:189422) $\psi_{n\mathbf{k}}(\mathbf{r})$ 和 $\psi_{n\mathbf{k}'}(\mathbf{r})$ 在整个晶体（或施加周期性边界条件的超胞）上仍然是正交的。这可以通过将整个晶体的积分分解为对 $N$ 个原胞的积分和来证明 [@problem_id:828367]。这个性质是晶体动量作为一个[好量子数](@entry_id:262514)的直接体现。

此外，[布洛赫函数](@entry_id:189422)集是完备的。对于一个给定的非简并能带 $n$，其所有 $N$ 个（在[第一布里渊区](@entry_id:269110)内的离散 $\mathbf{k}$ 点）[布洛赫函数](@entry_id:189422) $\psi_{n\mathbf{k}}(\mathbf{r})$ 张成了一个希尔伯特[子空间](@entry_id:150286)。我们可以定义投影到该[子空间](@entry_id:150286)的[投影算符](@entry_id:154142) $\hat{P}_n$，其在[实空间](@entry_id:754128)的核为 $P_n(\mathbf{r}, \mathbf{r}') = \sum_{\mathbf{k} \in \text{BZ}} \psi_{n\mathbf{k}}(\mathbf{r}) \psi_{n\mathbf{k}}^*(\mathbf{r}')$。通过计算这个核的对角部分在单个原胞内的积分，可以得到一个深刻的结果 [@problem_id:828393]：
$$
\int_{V_{\text{cell}}} P_n(\mathbf{r}, \mathbf{r}) \, d^3\mathbf{r} = \sum_{\mathbf{k} \in \text{BZ}} \int_{V_{\text{cell}}} |\psi_{n\mathbf{k}}(\mathbf{r})|^2 \, d^3\mathbf{r} = \sum_{\mathbf{k} \in \text{BZ}} \frac{1}{N} = \frac{N}{N} = 1
$$
这个结果表明，对于任何一个能带，其所有状态在空间中[分布](@entry_id:182848)的“总概率”平均到每个[原胞](@entry_id:159354)正好是1。换言之，一个满带恰好为晶体的每个[原胞](@entry_id:159354)提供一个[量子态](@entry_id:146142)。

#### 晶体动量与力学动量

初学者常常混淆**晶体动量** $\hbar\mathbf{k}$ 和**力学动量** $\mathbf{p} = -i\hbar\nabla$。区分这两者至关重要。力学[动量算符](@entry_id:151743)是连续空间平移的生成元，但在[周期势](@entry_id:140652)场中，连续[平移对称性](@entry_id:171614)被破坏，只剩下离散平移对称性。因此，力学动量 $\mathbf{p}$ **不是**晶体中电子的[守恒量](@entry_id:150267)。电子与[晶格](@entry_id:196752)的相互作用可以改变其力学动量，交换的动量为 $\hbar\mathbf{G}$ 的整数倍。相比之下，在没有其他破坏周期性相互作用（如[声子](@entry_id:140728)或[缺陷散射](@entry_id:273067)）的情况下，[晶体动量](@entry_id:136369) $\hbar\mathbf{k}$ 是守恒的（或更准确地说，是准守恒的，即守恒至相差一个[倒格矢](@entry_id:263351) $\hbar\mathbf{G}$）[@problem_id:2997745]。

[布洛赫态](@entry_id:147552) $\psi_{n\mathbf{k}}$ **不是**力学[动量算符](@entry_id:151743) $\mathbf{p}$ 的本征态。力学动量在[布洛赫态](@entry_id:147552)中的[期望值](@entry_id:153208)为：
$$
\langle \psi_{n\mathbf{k}} | \mathbf{p} | \psi_{n\mathbf{k}} \rangle = \int_V e^{-i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}^*(\mathbf{r}) (-i\hbar\nabla) e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}) \, d^3\mathbf{r} = \hbar\mathbf{k} + \langle u_{n\mathbf{k}} | \mathbf{p} | u_{n\mathbf{k}} \rangle_{V_{\text{cell}}}
$$
可见，力学动量的[期望值](@entry_id:153208)由两部分组成：$\hbar\mathbf{k}$ 部分，有时称为“赝动量”，以及元胞周期函数 $u_{n\mathbf{k}}$ 在原胞内动量的平均值 $\langle u_{n\mathbf{k}} | \mathbf{p} | u_{n\mathbf{k}} \rangle$。只有在自由电子情况下（$V(\mathbf{r})=0, u_{n\mathbf{k}}$ 为常数），后者才为零，此时 $\langle \mathbf{p} \rangle = \hbar\mathbf{k}$。

在具有[时间反演](@entry_id:182076)和空间反演对称性的晶体中，对于[布里渊区](@entry_id:142395)中心（$\mathbf{k}=\mathbf{0}$）的非简并能带边缘态 $u_{n\mathbf{0}}$，其动量[期望值](@entry_id:153208)为零，$\langle u_{n\mathbf{0}} | \mathbf{p} | u_{n\mathbf{0}} \rangle = \mathbf{0}$。然而，一旦 $\mathbf{k}$ 偏离中心，由于 $\mathbf{k}\cdot\mathbf{p}$ 微扰理论所描述的带间耦合效应，$\langle u_{n\mathbf{k}} | \mathbf{p} | u_{n\mathbf{k}} \rangle$ 通常不再为零，而是与 $\mathbf{k}$ [线性相关](@entry_id:185830)。因此，一般情况下 $\langle \psi_{n\mathbf{k}} | \mathbf{p} | \psi_{n\mathbf{k}} \rangle \neq \hbar\mathbf{k}$ [@problem_id:2997745]。

电子在晶体中的速度由其[群速度](@entry_id:147686)定义，可以通过[海森堡运动方程](@entry_id:140445)或著名的海尔曼-费曼定理得到：
$$
\mathbf{v}_n(\mathbf{k}) = \frac{1}{\hbar}\nabla_{\mathbf{k}} E_n(\mathbf{k})
$$
这个速度也是力学动量[期望值](@entry_id:153208)与真[实质](@entry_id:149406)量 $m_0$ 的比值，即 $\mathbf{v}_n(\mathbf{k}) = \frac{1}{m_0}\langle \psi_{n\mathbf{k}} | \mathbf{p} | \psi_{n\mathbf{k}} \rangle$。这与自由电子的 $\mathbf{v}=\mathbf{p}/m_0=\hbar\mathbf{k}/m_0$ 显著不同，因为[能带结构](@entry_id:139379) $E_n(\mathbf{k})$ 通常不是 $\mathbf{k}^2$ 的简单二次函数。能带的曲率决定了电子的**[有效质量](@entry_id:142879)**，这正是[晶格](@entry_id:196752)势场影响电子动力学行为的集中体现。

#### 能带的对称性

除了[平移对称性](@entry_id:171614)，晶体通常还具有**[点群对称性](@entry_id:141230)**（如旋转、反映）。如果一个点群操作 $\mathcal{R}$ 保持[晶格](@entry_id:196752)不变，那么它作用在[哈密顿量](@entry_id:172864)上会使其保持不变。这意味着，如果 $\psi_{n\mathbf{k}}(\mathbf{r})$ 是一个能量为 $E_n(\mathbf{k})$ 的本征态，那么经过 $\mathcal{R}$ 操作后的态 $\psi'(\mathbf{r}) = \psi_{n\mathbf{k}}(\mathcal{R}^{-1}\mathbf{r})$ 也必然是能量为 $E_n(\mathbf{k})$ 的本征态。可以证明，这个新的态 $\psi'(\mathbf{r})$ 对应于波矢 $\mathcal{R}\mathbf{k}$。因此，晶体的[点群对称性](@entry_id:141230)导致了能带能量的对称性 [@problem_id:828276]：
$$
E_n(\mathbf{k}) = E_n(\mathcal{R}\mathbf{k})
$$
这表明在布里渊区中，通过[对称操作](@entry_id:143398)可以相互关联的 $\mathbf{k}$ 点（构成所谓的“星”）具有相同的能量，即[能量简并](@entry_id:203091)。例如，在一个具有四重旋转对称性的二维正方[晶格](@entry_id:196752)中，能量[色散](@entry_id:263750)满足 $E(k_x, k_y) = E(-k_y, k_x)$。如果施加单轴应力破坏了这种对称性（例如 $E(k_x, k_y) = E_0 + c_1 k_x^2 + c_2 k_y^2$ 且 $c_1 \neq c_2$），那么原来简并的态 $(\mathbf{k}_A, \mathbf{k}_B=\mathcal{R}\mathbf{k}_A)$ 之间的简并将会被解除。

### 局域图像：瓦尼尔函数

[布洛赫函数](@entry_id:189422)是扩展到整个晶体的[离域](@entry_id:183327)[波函数](@entry_id:147440)，这对于理解能带结构和[输运性质](@entry_id:203130)非常有用。然而，在许多情况下，一个更符合化学直觉的局域图像是必要的，例如在[紧束缚模型](@entry_id:143446)中描述原子轨道间的相互作用。**瓦尼尔函数 (Wannier function)** 提供了这样一种等价的局域化表述。

对于一个孤立的能带 $n$，中心位于格点 $\mathbf{R}_m$ 的[瓦尼尔函数](@entry_id:145994) $w_n(\mathbf{r}-\mathbf{R}_m)$ 定义为该能带所有[布洛赫函数](@entry_id:189422)的[傅里叶变换](@entry_id:142120) [@problem_id:828299] [@problem_id:828285]：
$$
w_n(\mathbf{r}-\mathbf{R}_m) = \frac{1}{\sqrt{N}} \sum_{\mathbf{k} \in \text{BZ}} e^{-i\mathbf{k}\cdot\mathbf{R}_m} \psi_{n\mathbf{k}}(\mathbf{r})
$$
其中 $N$ 是晶体中的原胞总数。反过来，[布洛赫函数](@entry_id:189422)也可以由[瓦尼尔函数](@entry_id:145994)线性组合而成：
$$
\psi_{n\mathbf{k}}(\mathbf{r}) = \frac{1}{\sqrt{N}} \sum_m e^{i\mathbf{k}\cdot\mathbf{R}_m} w_n(\mathbf{r}-\mathbf{R}_m)
$$
[瓦尼尔函数](@entry_id:145994)集 $\{w_n(\mathbf{r}-\mathbf{R}_m)\}_m$ 构成了与[布洛赫函数](@entry_id:189422)集 $\{\psi_{n\mathbf{k}}(\mathbf{r})\}_{\mathbf{k}}$ 等价的描述能带 $n$ 的另一组正交归一基。与[布洛赫函数](@entry_id:189422)是[哈密顿量](@entry_id:172864)和[平移算符](@entry_id:756122)的共同[本征函数](@entry_id:154705)不同，[瓦尼尔函数](@entry_id:145994)是局域在特定格点 $\mathbf{R}_m$ 附近的，但通常不是[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)。

这种对偶关系的美妙之处在于它将[倒空间](@entry_id:754151)的[能带色散](@entry_id:138609) $E_n(\mathbf{k})$ 与[实空间](@entry_id:754128)的[哈密顿量](@entry_id:172864)[矩阵元](@entry_id:186505)联系起来。在瓦尼尔函数基底下，[哈密顿量](@entry_id:172864)的[矩阵元](@entry_id:186505)为 $H_{ml} = \langle w_m | H | w_l \rangle$。由于[平移对称性](@entry_id:171614)，这些[矩阵元](@entry_id:186505)只依赖于格点指数的差 $m-l$，代表了从格点 $l$ 到格点 $m$ 的“跳跃几率幅”。可以证明，这些跳跃项正是能带能量 $E_n(\mathbf{k})$ 的[傅里叶系数](@entry_id:144886) [@problem_id:828285]：
$$
H_{m-l} = \frac{1}{N} \sum_{\mathbf{k} \in \text{BZ}} e^{i\mathbf{k}\cdot(\mathbf{R}_m-\mathbf{R}_l)} E_n(\mathbf{k})
$$
例如，如果一个一维体系的能带为 $E(k) = C_0 - 2C_1 \cos(ka) - 2C_2 \cos(2ka)$，那么通过[傅里叶变换](@entry_id:142120)可以立即得到零点能量为 $H_0 = C_0$，最近邻跳跃项为 $H_{\pm 1} = -C_1$，次近邻跳跃项为 $H_{\pm 2} = -C_2$。这清晰地展示了[倒空间](@entry_id:754151)的[能带色散](@entry_id:138609)与[实空间](@entry_id:754128)的局域相互作用之间的深刻联系。

### 超越[理想晶体](@entry_id:138314)：布洛赫定理的修正与失效

布洛赫定理是建立在[理想晶体](@entry_id:138314)完美周期性的基础之上的。在更真实的物理系统中，这种完美周期性可能被打破，导致[布洛赫定理](@entry_id:137461)需要修正甚至完全失效。探讨这些边界情况对于深入理解电子在真实材料中的行为至关重要 [@problem_id:2914631]。

#### 无序与缺陷

晶体中的缺陷、杂质或热[振动](@entry_id:267781)会引入一个随机的、非周期性的**无序势** $U_{\text{dis}}(\mathbf{r})$。这个势的加入破坏了[哈密顿量](@entry_id:172864)的离散平移对称性，即 $[H, T_{\mathbf{R}}] \neq 0$。因此，对于任意一个特定的无序构型，严格意义上的[布洛赫态](@entry_id:147552)已不复存在，晶体动量 $\mathbf{k}$ 也不再是[好量子数](@entry_id:262514)。电子[波函数](@entry_id:147440)不再是扩展到整个晶体的[布洛赫波](@entry_id:144558)，而可能被散射，甚至在强无序情况下发生**安德森局域化**。尽管体系的**系综平均**性质可能仍然反映出[晶格](@entry_id:196752)的周期性，但这并不能保证单个样本的本征态是[布洛赫态](@entry_id:147552)。

然而，在弱无序的情况下，如果散射较弱，布洛赫图像仍然可以作为一种近似描述。此时，$\mathbf{k}$ 可被视为一个“近似”的[好量子数](@entry_id:262514)，态的寿命和[平均自由程](@entry_id:139563)成为描述电子动力学的关键参数。

#### 外[磁场](@entry_id:153296)

当施加一个均匀的外[磁场](@entry_id:153296) $\mathbf{B}$ 时，描述电子的[哈密顿量](@entry_id:172864)包含磁矢势 $\mathbf{A}(\mathbf{r})$。即使在没有[晶格](@entry_id:196752)势的情况下，普通[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 也不再与动能项 $\frac{1}{2m}(\mathbf{p}+e\mathbf{A})^2$ 对易。这是因为不存在一个既能产生均匀[磁场](@entry_id:153296)又同时具有[晶格](@entry_id:196752)周期性的[磁矢势](@entry_id:141246) $\mathbf{A}(\mathbf{r})$。

为了恢复一种广义的平移对称性，需要引入**磁[平移算符](@entry_id:756122)**。然而，两个不同方向的磁[平移算符](@entry_id:756122)通常不对易，它们的[对易关系](@entry_id:136780)包含一个正比于穿过两平移矢量所围面积的[磁通量](@entry_id:268943)的相位因子。只有当穿过每个[晶格](@entry_id:196752)原胞的磁通量 $\Phi$ 是磁通量子 $\Phi_0 = h/e$ 的一个**有理数**倍时，即 $\Phi/\Phi_0 = p/q$（其中 $p, q$ 为整数），才可能构建一个扩大的**磁[原胞](@entry_id:159354)**（面积为原先的 $q$ 倍）。在此磁原胞的格点上，磁[平移算符](@entry_id:756122)可以对易，从而建立一个**广义布洛赫定理**。其结果是，原来的[布里渊区](@entry_id:142395)被折叠成一个更小的**磁布里渊区**，原来的能带分裂成 $q$ 个磁子能带 [@problem_id:1355551]。如果磁通量是无理数倍的磁通量子，则不存在任何平移对称性，能谱呈现出复杂的分形结构，即著名的“霍夫施塔特蝴蝶”。

#### 超结构

当晶体中出现额外的周期性调制时，例如**[电荷密度波 (CDW)](@entry_id:273303)** 或[自旋密度波](@entry_id:139011)，体系的周期性会发生改变。
- **公度超结构**：如果调制的周期与原始[晶格](@entry_id:196752)周期成简单的整数比，系统会形成一个周期更大的**超晶格**。原始的[平移对称性](@entry_id:171614)在更小的尺度上被破坏，但在超晶格的尺度上建立起新的[平移对称性](@entry_id:171614)。因此，布洛赫定理仍然适用，但应基于新的、更大的超原胞和相应的、更小的折叠[布里渊区](@entry_id:142395) [@problem_id:2914631]。
- **非公度超结构**：如果调制的周期与[晶格](@entry_id:196752)周期不成有理数比，则系统完全丧失了离散平移对称性，成为所谓的“[准晶](@entry_id:141956)”。在这种情况下，严格的[布洛赫定理](@entry_id:137461)不成立。然而，如果调制势很弱，可以将其作为微扰处理，[晶体动量](@entry_id:136369)在远离[共振散射](@entry_id:185638)的条件下仍然是一个近似的[好量子数](@entry_id:262514)。

最后，值得一提的是，在计算物理中广泛使用的**[扭转边界条件](@entry_id:756246)**（即[波函数](@entry_id:147440)跨越超胞边界时获得一个额外的相位 $e^{i\theta}$），并不会使[布洛赫定理](@entry_id:137461)失效。它仅仅是改变了[布里渊区](@entry_id:142395)中允许的 $\mathbf{k}$ 点的离散网格，相当于将整个网格进行了一个平移，而[布洛赫函数](@entry_id:189422)的基本形式和能带结构本身保持不变 [@problem_id:2914631]。