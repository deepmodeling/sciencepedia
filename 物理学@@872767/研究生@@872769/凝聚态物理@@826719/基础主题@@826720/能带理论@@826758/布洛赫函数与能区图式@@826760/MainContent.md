## 引言
晶体固体中原子的周期性排布是其众多独特性质的根源。[凝聚态物理学](@entry_id:140205)的一个核心问题是，这种周期性如何决定了电子的行为。答案蕴含于[布洛赫定理](@entry_id:137461)之中——这是整个固体理论的基石，它从根本上重塑了我们对电子态的理解，使其超越了简单的自由电[子图](@entry_id:273342)像。本文旨在填补[晶格](@entry_id:196752)周期性的抽象概念与材料宏观属性之间的鸿沟。在接下来的章节中，您将踏上一段系统的学习之旅。第一章“原理与机制”将严格推导[布洛赫定理](@entry_id:137461)，并引入[晶格动量](@entry_id:143609)和布里渊区等基本概念。随后，第二章“应用与[交叉](@entry_id:147634)学科联系”将通过[晶体衍射](@entry_id:139605)、[半导体光学](@entry_id:182889)、电子输运以及能带的拓扑性质等实际问题，展示这些理论的强大威力。最后，“动手实践”部分将提供具体问题以巩固您的理解。现在，让我们开始探索平移对称性对晶体中电子量子力学的深刻影响。

## 原理与机制

在上一章中，我们介绍了晶体固体的周期性结构是其许多独特性质的根本原因。现在，我们将深入探讨这种周期性如何从根本上决定了电子在晶体中的行为。本章的核心是布洛赫定理（Bloch's theorem），它是整个[固体能带理论](@entry_id:144910)的基石。我们将从第一性原理出发，系统地阐述[布洛赫定理](@entry_id:137461)及其推论，定义[晶格动量](@entry_id:143609)和布里渊区等核心概念，并探讨如何在不同的等效方案（zone schemes）中表示[电子能谱](@entry_id:160814)。最后，我们将讨论当完美的周期性被破坏时，这些概念将如何演变。

### 分立[平移对称性](@entry_id:171614)的后果：[布洛赫定理](@entry_id:137461)

考虑一个在晶体中运动的单电子，其[哈密顿量](@entry_id:172864)为：
$$
\hat{H} = \frac{\hat{\mathbf{p}}^2}{2m} + V(\mathbf{r})
$$
其中 $V(\mathbf{r})$ 是[晶格](@entry_id:196752)产生的[周期性势场](@entry_id:140652)。这意味着对于任何布拉维格矢（Bravais lattice vector）$\mathbf{R}$，[势场](@entry_id:143025)都满足：
$$
V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})
$$
这种周期性是[晶体结构](@entry_id:140373)的核心特征。为了理解其对量子力学的影响，我们引入[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$，其作用于任意函数 $f(\mathbf{r})$ 上定义为 $\hat{T}_{\mathbf{R}} f(\mathbf{r}) = f(\mathbf{r} + \mathbf{R})$。由于动能项 $\hat{\mathbf{p}}^2 / 2m$ 在任何平移下都是不变的，而[势能](@entry_id:748988)项根据其定义在格矢平移下也不变，因此[哈密顿量](@entry_id:172864) $\hat{H}$ 与所有格矢[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 对易：
$$
[\hat{H}, \hat{T}_{\mathbf{R}}] = 0 \quad \text{for all } \mathbf{R}
$$
此外，所有的[平移算符](@entry_id:756122)之间也相互对易。根据量子力学基本原理，这意味着我们可以找到一组同时属于 $\hat{H}$ 和所有 $\hat{T}_{\mathbf{R}}$ 的共同本征函数。设 $\psi(\mathbf{r})$ 是这样一个本征函数，那么它必须满足：
$$
\hat{H} \psi(\mathbf{r}) = E \psi(\mathbf{r})
$$
$$
\hat{T}_{\mathbf{R}} \psi(\mathbf{r}) = \psi(\mathbf{r} + \mathbf{R}) = C_{\mathbf{R}} \psi(\mathbf{r})
$$
其中 $E$ 和 $C_{\mathbf{R}}$ 分别是 $\hat{H}$ 和 $\hat{T}_{\mathbf{R}}$ 的[本征值](@entry_id:154894)。由于平移的连续性（$\hat{T}_{\mathbf{R}_1}\hat{T}_{\mathbf{R}_2} = \hat{T}_{\mathbf{R}_1+\mathbf{R}_2}$），[本征值](@entry_id:154894)必须满足 $C_{\mathbf{R}_1}C_{\mathbf{R}_2} = C_{\mathbf{R}_1+\mathbf{R}_2}$。考虑到[波函数](@entry_id:147440)的归一化要求，$\hat{T}_{\mathbf{R}}$ 必须是幺正算符，这意味着 $|C_{\mathbf{R}}| = 1$。满足这些条件的解具有 $C_{\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$ 的形式，其中 $\mathbf{k}$ 是一个实矢量，我们称之为**[晶格动量](@entry_id:143609)**（crystal momentum）。

因此，[周期性势场](@entry_id:140652)中[哈密顿量](@entry_id:172864)的本征函数必须满足以下属性，这便是**[布洛赫定理](@entry_id:137461)**（Bloch's theorem）的第一种表述：
$$
\psi_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r})
$$
这个方程告诉我们，本征函数在经历一个格矢平移后，并不是保持不变，而是获得一个与 $\mathbf{k}$ 和 $\mathbf{R}$ 有关的相位因子。从群论的角度看，[晶格动量](@entry_id:143609) $\mathbf{k}$ 标记了[晶格](@entry_id:196752)分立平移群的[不可约表示](@entry_id:263310) [@problem_id:2972358]。

布洛赫定理还有第二种等价且极为有用的表述。我们可以定义一个新函数 $u_{\mathbf{k}}(\mathbf{r}) = e^{-i\mathbf{k}\cdot\mathbf{r}} \psi_{\mathbf{k}}(\mathbf{r})$。让我们来检验这个函数的周期性：
$$
u_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{-i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})} \psi_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{-i\mathbf{k}\cdot\mathbf{r}} e^{-i\mathbf{k}\cdot\mathbf{R}} (e^{i\mathbf{k}\cdot\mathbf{R}} \psi_{\mathbf{k}}(\mathbf{r})) = e^{-i\mathbf{k}\cdot\mathbf{r}} \psi_{\mathbf{k}}(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r})
$$
这表明函数 $u_{\mathbf{k}}(\mathbf{r})$ 具有与[晶格](@entry_id:196752)完全相同的周期性，我们称之为**[晶胞](@entry_id:143489)周期函数**（cell-periodic function）。因此，[哈密顿量](@entry_id:172864)的本征函数可以写成一个平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 与一个[晶胞](@entry_id:143489)周期函数 $u_{n\mathbf{k}}(\mathbf{r})$ 的乘积。这里我们引入了**能带指标**（band index）$n$，因为它对于给定的 $\mathbf{k}$，薛定谔方程会有一系列分立的[能量本征值](@entry_id:144381) $E_{n}(\mathbf{k})$ 和对应的[本征函数](@entry_id:154705)。这就是布洛赫定理的第二种形式：
$$
\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}), \quad \text{其中 } u_{n\mathbf{k}}(\mathbf{r} + \mathbf{R}) = u_{n\mathbf{k}}(\mathbf{r})
$$
这个形式非常直观：它将晶体中电子的波[函数分解](@entry_id:197881)为一个描述长程传播的[平面波](@entry_id:189798)[部分和](@entry_id:162077)一个描述原胞内部快速[振荡](@entry_id:267781)的周期部分 [@problem_id:2972343]。需要强调的是，[布洛赫定理](@entry_id:137461)是[晶格](@entry_id:196752)周期性的直接结果，它不依赖于任何其他对称性，例如[反演对称性](@entry_id:269948)。

### [晶格动量](@entry_id:143609)与[倒易空间](@entry_id:754151)

[布洛赫定理](@entry_id:137461)引入了[晶格动量](@entry_id:143609) $\mathbf{k}$，这是一个全新的概念，必须与我们熟知的力学动量区分开来。

#### [晶格动量](@entry_id:143609) vs. 力学动量

在量子力学中，力学动量算符为 $\hat{\mathbf{p}} = -i\hbar\nabla$。一个自由电子的[本征态](@entry_id:149904)（平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$）同时也是[动量算符](@entry_id:151743)的本征态，其动量[本征值](@entry_id:154894)为 $\hbar\mathbf{k}$。然而，在晶体中，[布洛赫函数](@entry_id:189422) $\psi_{n\mathbf{k}}(\mathbf{r})$ **不是**[动量算符](@entry_id:151743)的[本征态](@entry_id:149904)。我们可以验证这一点：
$$
\hat{\mathbf{p}} \psi_{n\mathbf{k}}(\mathbf{r}) = -i\hbar\nabla (e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})) = \hbar\mathbf{k} \psi_{n\mathbf{k}}(\mathbf{r}) + e^{i\mathbf{k}\cdot\mathbf{r}}(-i\hbar\nabla u_{n\mathbf{k}}(\mathbf{r}))
$$
由于 $u_{n\mathbf{k}}(\mathbf{r})$ 通常不是常数，第二项不为零。这意味着[布洛赫态](@entry_id:147552)是具有确定[晶格动量](@entry_id:143609) $\mathbf{k}$ 的态，但它没有确定的力学动量。相反，它可以被看作是动量为 $\hbar(\mathbf{k}-\mathbf{G})$ 的一系列平面[波的叠加](@entry_id:166456)，其中 $\mathbf{G}$ 是倒易格矢。

物理上，力学动量的不守恒是容易理解的：周期性势场意味着电子会与[晶格](@entry_id:196752)相互作用（“散射”），从而交换动量。因此，只有电子和整个[晶格](@entry_id:196752)的[总动量](@entry_id:173071)是守恒的。然而，[晶格动量](@entry_id:143609)在某种意义上是守恒的：在电子与[周期性势场](@entry_id:140652)的作用过程中，[晶格动量](@entry_id:143609)守恒，但要以一个倒易格矢 $\mathbf{G}$ 为模，即所谓的**[准动量守恒](@entry_id:145588)**（conservation of crystal momentum）。这是因为[晶格](@entry_id:196752)只能吸收或提供大小为 $\hbar\mathbf{G}$ 的离散动量块 [@problem_id:2972358]。

#### 倒易格点与布里渊区

[晶格动量](@entry_id:143609) $\mathbf{k}$ 的定义存在一种内在的冗余性。考虑一个矢量 $\mathbf{k}' = \mathbf{k} + \mathbf{G}$，其中 $\mathbf{G}$ 是一个特殊的矢量，它满足对于所有布拉维格矢 $\mathbf{R}$ 都有 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$。所有满足这个条件的 $\mathbf{G}$ 构成的集合形成了**倒易点阵**（reciprocal lattice）。让我们看看 $\mathbf{k}$ 和 $\mathbf{k}'$ 对应的平移[本征值](@entry_id:154894)有什么不同：
$$
e^{i\mathbf{k}'\cdot\mathbf{R}} = e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}} e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}
$$
它们完全相同。这意味着 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 标记的是同一个[不可约表示](@entry_id:263310)，它们在描述[平移对称性](@entry_id:171614)方面是等效的。因此，[晶格动量](@entry_id:143609) $\mathbf{k}$ 只在相差一个倒易格矢的意义下是唯一定义的。

为了消除这种冗余，我们可以将所有唯一的 $\mathbf{k}$ 限制在倒易点阵的一个[原胞](@entry_id:159354)（primitive cell）内。最常用和最方便的选择是倒易点阵的[维格纳-赛兹原胞](@entry_id:137574)（Wigner-Seitz cell），我们称之为**[第一布里渊区](@entry_id:269110)**（First Brillouin Zone, BZ）。

倒易点阵由一组[基矢](@entry_id:199546) $\mathbf{b}_j$ 生成，它们与[正空间](@entry_id:754128)[基矢](@entry_id:199546) $\mathbf{a}_i$ 的关系通过 $\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij}$ 定义。例如，考虑一个二维布拉维格点阵，其[基矢](@entry_id:199546)为 $\mathbf{a}_1 = L_1 \hat{\mathbf{x}}$ 和 $\mathbf{a}_2 = L_2 (\cos\theta \hat{\mathbf{x}} + \sin\theta \hat{\mathbf{y}})$。通过求解定义关系，我们可以找到其倒易格矢[基矢](@entry_id:199546) [@problem_id:2972345]：
$$
\mathbf{b}_1 = \frac{2\pi}{L_1 \sin\theta} (\sin\theta \hat{\mathbf{x}} - \cos\theta \hat{\mathbf{y}})
$$
$$
\mathbf{b}_2 = \frac{2\pi}{L_2 \sin\theta} \hat{\mathbf{y}}
$$
有趣的是，可以证明倒易格矢之间的夹角 $\varphi$ 与[正空间](@entry_id:754128)格矢之间的夹角 $\theta$ 的关系为 $\varphi = \pi - \theta$。这反映了[正空间](@entry_id:754128)和倒易空间之间的一种[几何对偶](@entry_id:204458)性。

#### 倒易空间中的周期性

由于 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 的等效性，所有[物理可观测量](@entry_id:154692)都必须是 $\mathbf{k}$ 的[周期函数](@entry_id:139337)，周期为任意倒易格矢 $\mathbf{G}$。最重要的是[能量本征值](@entry_id:144381)：
$$
E_n(\mathbf{k}+\mathbf{G}) = E_n(\mathbf{k})
$$
相应地，作为能量梯度的群速度 $\mathbf{v}_n(\mathbf{k}) = \frac{1}{\hbar}\nabla_{\mathbf{k}}E_n(\mathbf{k})$ 也必须是周期性的 [@problem_id:2972350] [@problem_id:2972358]。

然而，[波函数](@entry_id:147440)本身在这种变换下的行为需要更仔细的考察。我们通常采用一种规范（gauge），使得完整的[波函数](@entry_id:147440)是[倒易空间](@entry_id:754151)中的周期函数，即 $\psi_{n,\mathbf{k}+\mathbf{G}}(\mathbf{r}) = \psi_{n\mathbf{k}}(\mathbf{r})$。在这种约定下，我们可以推导出[晶胞](@entry_id:143489)周期部分 $u_{n\mathbf{k}}(\mathbf{r})$ 的变换规律 [@problem_id:2972343]：
$$
\psi_{n,\mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}} u_{n,\mathbf{k}+\mathbf{G}}(\mathbf{r})
$$
$$
\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})
$$
令两者相等，我们得到：
$$
u_{n,\mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{-i\mathbf{G}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})
$$
这表明，虽然能量是[倒易空间](@entry_id:754151)的[周期函数](@entry_id:139337)，但晶胞周期函数 $u_{n\mathbf{k}}$ 却不是。它在平移一个倒易格矢后会获得一个依赖于位置的相位因子。这个微妙但重要的性质是[贝里相位](@entry_id:159450)（Berry phase）等现代能带理论概念的基础。

### 作为[基组](@entry_id:160309)的[布洛赫函数](@entry_id:189422)

周期性势场中的[哈密顿量](@entry_id:172864)是一个[厄米算符](@entry_id:153410)，其本征函数集——[布洛赫函数](@entry_id:189422) $\{\psi_{n\mathbf{k}}(\mathbf{r})\}$——构成了一个完备的[正交基](@entry_id:264024)组。这意味着任何一个在晶体中定义的状态 $\Psi(\mathbf{r})$ 都可以唯一地展开为[布洛赫函数](@entry_id:189422)的线性组合。

#### [玻恩-冯·卡门边界条件](@entry_id:140446)

为了处理无限大晶体带来的数学困难（例如归一化问题），我们通常采用**[玻恩-冯·卡门](@entry_id:201892)（Born-von Kármán, BvK）边界条件**。我们假设晶体是由 $N_1 \times N_2 \times N_3$ 个[原胞](@entry_id:159354)构成的有限体积，并要求[波函数](@entry_id:147440)在晶体的宏观边界上是周期的。例如，沿 $\mathbf{a}_1$ 方向，我们要求 $\psi(\mathbf{r}) = \psi(\mathbf{r} + N_1\mathbf{a}_1)$。

将这个条件应用于[布洛赫函数](@entry_id:189422) $\psi_{\mathbf{k}}(\mathbf{r})$，我们得到：
$$
\psi_{\mathbf{k}}(\mathbf{r} + N_1\mathbf{a}_1) = e^{i\mathbf{k}\cdot(N_1\mathbf{a}_1)} \psi_{\mathbf{k}}(\mathbf{r}) = \psi_{\mathbf{k}}(\mathbf{r})
$$
这要求 $e^{iN_1\mathbf{k}\cdot\mathbf{a}_1} = 1$，即 $N_1\mathbf{k}\cdot\mathbf{a}_1 = 2\pi m_1$，其中 $m_1$ 为整数。对三个方向都应用此条件，并把 $\mathbf{k}$ 在倒易[基矢](@entry_id:199546)上展开为 $\mathbf{k} = c_1\mathbf{b}_1 + c_2\mathbf{b}_2 + c_3\mathbf{b}_3$，我们发现系数 $c_i$ 被量子化了：
$$
c_i = \frac{m_i}{N_i}, \quad m_i \in \mathbb{Z}
$$
这意味着在BvK边界条件下，原本连续的[晶格动量](@entry_id:143609) $\mathbf{k}$ 变成了在[布里渊区](@entry_id:142395)内[均匀分布](@entry_id:194597)的离散网格点。[第一布里渊区](@entry_id:269110)内的独立 $\mathbf{k}$ 点总数为 $N_1 N_2 N_3$，恰好等于晶体中的[原胞](@entry_id:159354)数目 [@problem_id:2972360]。

在无限晶体的理论处理中，我们实际上是在取[热力学极限](@entry_id:143061) $N_i \to \infty$。在这个极限下，离散的 $\mathbf{k}$ 点网格变得无限密集，最终形成连续体。求和运算也相应地转化为积分：
$$
\frac{1}{N} \sum_{\mathbf{k} \in \text{BZ}} \longrightarrow \frac{\Omega_c}{(2\pi)^d} \int_{\text{BZ}} d^d k
$$
其中 $N = N_1 N_2 N_3$ 是总的原胞数，$\Omega_c$ 是[原胞](@entry_id:159354)的体积， $d$是维度 [@problem_id:2972360]。

#### 完备性与态的展开

对于施加了BvK边界条件的有限晶体，[布洛赫函数](@entry_id:189422)集 $\{\psi_{n\mathbf{k}}\}$ 构成了一个完备的正交归一[基组](@entry_id:160309)，满足：
$$
\int_{\Omega} \psi_{n'\mathbf{k}'}^*(\mathbf{r}) \psi_{n\mathbf{k}}(\mathbf{r}) d^d r = \delta_{nn'} \delta_{\mathbf{k}\mathbf{k}'}
$$
其中积分是在整个晶体体积 $\Omega$ 上进行的。任何一个平方可积的态 $\Psi(\mathbf{r})$ 都可以展开为：
$$
\Psi(\mathbf{r}) = \sum_{n, \mathbf{k} \in \text{BZ}} c_{n\mathbf{k}} \psi_{n\mathbf{k}}(\mathbf{r})
$$
其展开系数由投影给出：
$$
c_{n\mathbf{k}} = \int_{\Omega} \psi_{n\mathbf{k}}^*(\mathbf{r}) \Psi(\mathbf{r}) d^d r
$$
在无限体积的极限下，[归一化条件](@entry_id:156486)变为狄拉克 $\delta$ 函数形式，求和也变为积分。这个完备的[基组](@entry_id:160309)是进行任何微扰计算或[多体理论](@entry_id:169452)分析的出发点 [@problem_id:2972333]。

值得一提的是，即使在具有非[平凡拓扑](@entry_id:154009)性质（如非零陈数）的能带中，虽然无法在整个[布里渊区](@entry_id:142395)上定义一个全局光滑且周期的规范（即相位选择），但这只是关于[本征态](@entry_id:149904)丛的几何性质的陈述，它并不影响本征函数集 $\{\psi_{n\mathbf{k}}\}$ 作为[希尔伯特空间基](@entry_id:153726)组的完备性 [@problem_id:2972333]。

### 表征方案与[能带图](@entry_id:272375)

我们已经知道能量 $E_n(\mathbf{k})$ 是[倒易空间](@entry_id:754151)的周期函数。这种周期性允许我们以多种等效的方式来可视化能带结构 $E_n(\mathbf{k})$ vs. $\mathbf{k}$。

#### 扩展、再现与简约区方案

1.  **扩展区方案 (Extended Zone Scheme)**：在这种方案中，我们为每一个能带指标 $n$ 画出它在整个倒易空间的能量[色散](@entry_id:263750)。这会导致不同能带的曲线在空间中相互重叠和[交叉](@entry_id:147634)，图像比较混乱，但它清晰地展示了能带与自由电子抛物线的[亲缘关系](@entry_id:172505)。

2.  **再现区方案 (Repeated Zone Scheme)**：这种方案利用 $E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})$ 的性质，将[第一布里渊区](@entry_id:269110)内的[能带结构](@entry_id:139379)原封不动地复制到以每个倒易格点为中心的其他布里渊区中。这使得[倒易空间](@entry_id:754151)的周期性一目了然 [@problem_id:2972350]。

3.  **简约区方案 (Reduced Zone Scheme)**：这是最常用、最紧凑的表示方法。其核心思想是将整个[倒易空间](@entry_id:754151)中的所有能量态都“折叠”回第一布里淵区。对于任意一个波矢 $\mathbf{k}$，我们总能找到一个唯一的倒易格矢 $\mathbf{G}_{\mathbf{k}}$，使得 $\mathbf{k}' = \mathbf{k} - \mathbf{G}_{\mathbf{k}}$ 落在[第一布里渊区](@entry_id:269110)内。然后，我们将原来在 $\mathbf{k}$ 处的能量 $E(\mathbf{k})$ 绘制在简约波矢 $\mathbf{k}'$ 处。

这个折叠过程意味着，来自不同扩展区域的多个能量态（它们原本有不同的 $\mathbf{k}$ 值）现在被映射到[第一布里渊区](@entry_id:269110)中的同一个 $\mathbf{k}'$ 上。为了区分这些态，我们必须引入或扩大能带指标的含义。因此，在简约区方案中，每个 $\mathbf{k}'$ 点上都会出现许多条能带，它们对应于扩展区方案中位于 $\mathbf{k}'$, $\mathbf{k}'+\mathbf{G}_1$, $\mathbf{k}'+\mathbf{G}_2$, ... 等位置的能量态 [@problem_id:2972347]。

**[空晶格近似](@entry_id:142756) (Empty-Lattice Approximation)** 是理解简约区方案的绝佳教学工具。在该近似中，我们令[周期性势场](@entry_id:140652) $V(\mathbf{r}) \to 0$，但保留[晶格](@entry_id:196752)的周期性来标记态。此时电子是自由的，能量为 $E(\mathbf{K}) = \frac{\hbar^2 |\mathbf{K}|^2}{2m}$。在简约区方案中，我们将每个[波矢](@entry_id:178620) $\mathbf{K}$ 写成 $\mathbf{K} = \mathbf{k}' + \mathbf{G}$，其中 $\mathbf{k}'$ 在[第一布里渊区](@entry_id:269110)内。于是，能量变为 $\mathbf{k}'$ 的函数，并由 $\mathbf{G}$ 标记：$E_{\mathbf{G}}(\mathbf{k}') = \frac{\hbar^2 |\mathbf{k}'+\mathbf{G}|^2}{2m}$。这意味着，对于每一个倒易格矢 $\mathbf{G}$，我们都得到一条从 $\mathbf{G}$ 点为中心的自由电子抛物线被“折叠”回[第一布里渊区](@entry_id:269110)，从而形成了一系列交叉的能带 [@problem_id:2972347]。

#### [近自由电子模型](@entry_id:138124)中的[能隙](@entry_id:191975)

现在我们重新引入一个弱的周期性势场 $V(\mathbf{r})$，即进入**[近自由电子模型](@entry_id:138124) (Nearly-Free Electron, NFE) **。在简约区方案的空[晶格](@entry_id:196752)图像中，不同 $\mathbf{G}$ 值对应的能带会在某些点交叉。这些交叉点，即[能量简并](@entry_id:203091)点，正是弱周期势场产生最显著效应的地方。

简并条件为 $E_{\mathbf{G}}(\mathbf{k}') = E_{\mathbf{G'}}(\mathbf{k}')$，即 $|\mathbf{k}'+\mathbf{G}| = |\mathbf{k}'+\mathbf{G'}|$。一个特别重要的简并发生在布里渊区的边界上。例如，对于一维情况，$k' = \pi/a$ 是[第一布里渊区](@entry_id:269110)的边界。此处，来自 $\mathbf{G}=0$ 的能带 $E_0(k') = \frac{\hbar^2 k'^2}{2m}$ 和来自 $\mathbf{G}=-2\pi/a$ 的能带 $E_{-2\pi/a}(k') = \frac{\hbar^2 (k' - 2\pi/a)^2}{2m}$ 发生简并。在扩展区方案中，这对应于[波矢](@entry_id:178620) $k=\pi/a$ 和 $k=-\pi/a$ 的两个自由电子态具有相同的能量。

弱周期势场 $V(x) = \sum_G V_G e^{iGx}$ 会耦合这两个简并的[平面波](@entry_id:189798)态。根据[简并微扰理论](@entry_id:143587)，势场的傅里叶分量 $V_G$ 会使得简并被解除，并打开一个能量[禁带](@entry_id:175956)，其宽度（[能隙](@entry_id:191975)）为 $2|V_G|$ [@problem_id:2972309]。

这个[能隙](@entry_id:191975)的物理起源在于电子[波函数](@entry_id:147440)与[周期势](@entry_id:140652)场的相互作用。在布里淵区边界上，$k = G/2$，本征态不再是[行波](@entry_id:185008)，而是两个[驻波](@entry_id:148648)的[线性组合](@entry_id:154743)：一个 $(\psi_-)$ 的电荷密度极大值位于[势阱](@entry_id:151413)的中心（离子实处），从而降低了[势能](@entry_id:748988)；另一个 $(\psi_+)$ 的电荷密度极大值位于[势阱](@entry_id:151413)之间，能量较高。这两个[驻波](@entry_id:148648)态的能量差就是[能隙](@entry_id:191975)。由于驻波的[群速度](@entry_id:147686)为零（$\mathbf{v}_g = \frac{1}{\hbar} dE/dk = 0$），我们看到能带在布里淵区边界处变得平坦，这与[驻波](@entry_id:148648)的物理图像完全一致 [@problem_id:2972369]。

在不同的表征方案中，这个[能隙](@entry_id:191975)的图像是：
-   在**扩展区方案**中，原本连续的自由电子抛物线在布里渊区边界 $k=n\pi/a$ 处发生“断裂”，[形成能](@entry_id:142642)量不连续的区域。
-   在**简约区方案**中，折叠回来的两条能带在布里渊区边界处不再交叉，而是相互“排斥”，形成一个**避免交叉 (avoided crossing)**，两条能带之间的最小垂直距离就是[能隙](@entry_id:191975)的大小 [@problem_id:2972309]。

无论采用何种方案，[能隙](@entry_id:191975)的物理现实及其大小都是不变的。它们只是同一物理现象的不同视觉呈现。所有[物理可观测量](@entry_id:154692)，如[态密度](@entry_id:147894)、[群速度](@entry_id:147686)等，都与选择的表征方案无关 [@problem_id:2972309]。

### 对称性的破坏与恢复

至此，我们的讨论都基于一个理想化的假设：晶体具有完美的周期性。在真实材料中，这种周期性会被各种缺陷所破坏，例如杂质原子、空位或[晶格振动](@entry_id:140970)等。我们以一个弱的、静态的无序势场 $U(\mathbf{r})$ 为例，来探讨这种情况。

此时的总[哈密顿量](@entry_id:172864)为 $\hat{H} = \hat{H}_0 + U(\mathbf{r})$，其中 $\hat{H}_0$ 是完美的周期[哈密顿量](@entry_id:172864)。对于任何一个特定的无序构型 $U(\mathbf{r})$，它通常不具有[晶格](@entry_id:196752)的周期性，即 $U(\mathbf{r}) \neq U(\mathbf{r}+\mathbf{R})$。结果是，总[哈密顿量](@entry_id:172864) $\hat{H}$不再与[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 对易。这意味着：
1.  **[晶格动量](@entry_id:143609)不再是[好量子数](@entry_id:262514)**：$\mathbf{k}$ 不再严格守恒，电子在无序势场中会发生散射，使其 $\mathbf{k}$ 发生改变。
2.  **[本征态](@entry_id:149904)不再是[布洛赫波](@entry_id:144558)**：$\hat{H}$ 的严格本征态是不同 $\mathbf{k}$ 和不同能带的[布洛赫波](@entry_id:144558)的复杂叠加。

然而，如果无序势的**统计性质**是均匀的，即从宏观上看，晶体中每一点的无序环境都是相似的，那么布洛赫的图像在某种平均意义下仍然是有效的。例如，我们假设无序势的系综平均为零 $\langle U(\mathbf{r}) \rangle = 0$，且其关联函数 $\langle U(\mathbf{r}) U(\mathbf{r}') \rangle$ 只依赖于相对位置 $\mathbf{r}-\mathbf{r}'$（并具有[晶格](@entry_id:196752)周期性）。

在这种情况下，虽然单个样本的[平移对称性](@entry_id:171614)被破坏，但**系综平均后的系统恢复了[平移对称性](@entry_id:171614)**。这意味着，任何物理可观测量在经过系综平均后，必须重新表现出[晶格](@entry_id:196752)的周期性。例如，平均[格林函数](@entry_id:147802)必须满足 $\langle G(\mathbf{r}+\mathbf{a}, \mathbf{r}'+\mathbf{a}) \rangle = \langle G(\mathbf{r}, \mathbf{r}') \rangle$。

这一点的关键推论是，在[倒易空间](@entry_id:754151)中，平均[格林函数](@entry_id:147802)在[晶格动量](@entry_id:143609)表象中是**对角的**。也就是说，$\langle G(\mathbf{k}, \mathbf{k}') \rangle \propto \delta_{\mathbf{k}\mathbf{k}'}$。这意味着，即使在[无序系统](@entry_id:145417)中，$\mathbf{k}$ 仍然是标记平均谱性质的一个有用标签。

无序散射的效应被包含在一个称为**[自能](@entry_id:145608)**（self-energy）$\Sigma(\mathbf{k}, \omega)$的量中。平均[格林函数](@entry_id:147802)可以写为：
$$
\langle G(\mathbf{k}, \omega) \rangle = \frac{1}{\omega - E_{\mathbf{k}}^0 - \Sigma(\mathbf{k}, \omega)}
$$
其中 $E_{\mathbf{k}}^0$ 是纯净系统中的能量。自能通常是一个复数。它的实部 $\text{Re}[\Sigma]$ 会使能带发生移动，而它的虚部 $\text{Im}[\Sigma]$ 则赋予了电子态一个有限的寿命，因为散射会使一个原本处于特定 $\mathbf{k}$ 态的电子衰变到其他态。这反映在[谱函数](@entry_id:147628) $A(\mathbf{k}, \omega) = -\frac{1}{\pi}\text{Im}\langle G(\mathbf{k}, \omega) \rangle$上，它不再是纯净系统中的 $\delta$ 函数峰，而是在原能量 $E_{\mathbf{k}}^0$ 附近展宽成一个具有一定宽度的峰。

因此，尽管严格的对称性已被打破，[晶格动量](@entry_id:143609) $\mathbf{k}$ 的概念依然顽强地存在，并作为描述电子在无序晶体中平均传播行为的不可或缺的工具 [@problem_id:2972310]。这一思想的延伸构成了现代凝聚态物理中处理电子输运和局域化等复杂现象的理论基础。