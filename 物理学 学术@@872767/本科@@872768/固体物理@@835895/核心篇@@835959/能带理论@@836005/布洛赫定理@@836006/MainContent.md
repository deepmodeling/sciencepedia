## 引言
晶体，作为自然界与人造材料中最有序的物质形态之一，其内部包含了数量巨大（约 $10^{23}$ 个/立方厘米）且相互作用的电子。理解这些电子的集体行为是整个[凝聚态物理学](@entry_id:140205)的核心任务，也是开发新型电子和光学器件的基石。然而，直接求解这样一个多体系统的薛定谔方程几乎是不可能的。幸运的是，[晶格](@entry_id:196752)完美的周期性为我们提供了一把解开这个难题的钥匙——[布洛赫定理](@entry_id:137461)。

本文将系统地阐述布洛赫定理及其深刻的物理内涵。我们将从基本原理出发，逐步揭示这一强大理论如何塑造我们对固体世界的理解。

在第一章“**原理与机制**”中，我们将从[晶格](@entry_id:196752)的平移对称性出发，严格推导布洛赫定理。我们将阐明[布洛赫波](@entry_id:144558)、晶体动量、能带、[带隙](@entry_id:191975)以及[有效质量](@entry_id:142879)等核心概念是如何从这一定理中自然产生的。

接下来的第二章“**应用与跨学科联系**”，我们将探讨这些理论概念的广泛应用。您将看到能带结构如何决定材料的[导电性](@entry_id:137481)，以及布洛赫定理的思想如何延伸至[声子](@entry_id:140728)、[光子晶体](@entry_id:137347)、[计算化学](@entry_id:143039)乃至生物系统等多个领域，展示其作为波在周期性介质中传播的普适[范式](@entry_id:161181)。

最后，在第三章“**动手实践**”中，我们将通过一系列精心设计的计算练习，引导您亲手推导[能带色散](@entry_id:138609)关系、计算有效质量，并模拟能带的形成过程，从而将抽象的理论知识转化为具体的物理直觉和解决问题的能力。

## 原理与机制

在上一章的引言中，我们了解了晶体固体中电子行为的复杂性。本章将深入探讨支配这些行为的核心原理——[布洛赫定理](@entry_id:137461) (Bloch's Theorem)，并阐明其引出的关键机制，如[能带结构](@entry_id:139379)的形成、[晶体动量](@entry_id:136369)的概念以及有效[质量的起源](@entry_id:161752)。

### [布洛赫定理](@entry_id:137461)的起源：晶体中的平移对称性

[理想晶体](@entry_id:138314)的最根本特征是其原子[排列](@entry_id:136432)的周期性。这种空间上的周期性直接反映在电子感受到的[势场](@entry_id:143025) $V(\mathbf{r})$ 上。对于[晶格](@entry_id:196752)中的任意一个格矢 $\mathbf{R}$，势能函数都满足[平移不变性](@entry_id:195885)：

$V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$

这一对称性是理解晶体中电子行为的钥匙。在量子力学中，系统的对称性由与[哈密顿量](@entry_id:172864)对易的算符来描述。让我们定义一个**[平移算符](@entry_id:756122)** $\hat{T}_\mathbf{R}$，其作用是将任意函数 $f(\mathbf{r})$ 的坐标平移一个格矢 $\mathbf{R}$。在某些约定中，其定义为 $\hat{T}_\mathbf{R}f(\mathbf{r}) = f(\mathbf{r}+\mathbf{R})$ 或 $\hat{T}_\mathbf{R}f(\mathbf{r}) = f(\mathbf{r}-\mathbf{R})$，这两种定义在物理上是等价的，仅影响[布洛赫波函数](@entry_id:144223)中相位的符号。此处我们采用 $\hat{T}_\mathbf{R}\psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R})$。

晶体的[哈密顿量](@entry_id:172864)为 $\hat{H} = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$。由于[动能算符](@entry_id:265633) $\hat{K} = -\frac{\hbar^2}{2m}\nabla^2$ 与空间平移对易，而[势能](@entry_id:748988)算符 $\hat{V}$ 又具有[晶格](@entry_id:196752)的周期性，因此整个[哈密顿量](@entry_id:172864)与任何格矢[平移算符](@entry_id:756122) $\hat{T}_\mathbf{R}$ 都是对易的 [@problem_id:1762595]：

$[\hat{H}, \hat{T}_\mathbf{R}] = 0$

这是因为对于任意[波函数](@entry_id:147440) $\psi(\mathbf{r})$，我们有：
$\hat{H}\hat{T}_\mathbf{R}\psi(\mathbf{r}) = \hat{H}\psi(\mathbf{r}+\mathbf{R}) = \left(-\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})\right)\psi(\mathbf{r}+\mathbf{R})$
由于 $\nabla$ 算符作用在 $\mathbf{r}$ 上，而 $\psi$ 的变量是 $\mathbf{r}+\mathbf{R}$，这等价于 $\nabla_{\mathbf{r}+\mathbf{R}}$ 作用在 $\psi(\mathbf{r}+\mathbf{R})$ 上。同时 $V(\mathbf{r}) = V(\mathbf{r}+\mathbf{R})$。所以：
$\hat{H}\hat{T}_\mathbf{R}\psi(\mathbf{r}) = \left(-\frac{\hbar^2}{2m}\nabla_{\mathbf{r}+\mathbf{R}}^2 + V(\mathbf{r}+\mathbf{R})\right)\psi(\mathbf{r}+\mathbf{R}) = (\hat{H}\psi)(\mathbf{r}+\mathbf{R}) = \hat{T}_\mathbf{R}(\hat{H}\psi(\mathbf{r}))$
这就证明了 $\hat{H}\hat{T}_\mathbf{R} = \hat{T}_\mathbf{R}\hat{H}$。

根据量子力学基本原理，当两个算符对易时，它们拥有一组共同的[本征函数](@entry_id:154705)。这意味着晶体[哈密顿量](@entry_id:172864)的定态解（[能量本征态](@entry_id:152154)）也必然是[平移算符](@entry_id:756122) $\hat{T}_\mathbf{R}$ 的本征态。

[平移算符](@entry_id:756122)的[本征值](@entry_id:154894)是什么呢？由于连续两次平移 $\hat{T}_\mathbf{R}\hat{T}_\mathbf{R}$ 必须保持[波函数](@entry_id:147440)的归一化，其[本征值](@entry_id:154894)的模必须为1。因此，$\hat{T}_\mathbf{R}$ 的[本征值](@entry_id:154894)必然是纯相位因子，通常记作 $e^{i\theta}$。对于所有格矢 $\mathbf{R} = n_1\mathbf{a}_1 + n_2\mathbf{a}_2 + n_3\mathbf{a}_3$，[本征值](@entry_id:154894)必须满足加法规则，这要求相位 $\theta$ 必须是 $\mathbf{R}$ 的线性函数。因此，我们可以引入一个矢量 $\mathbf{k}$，使得[本征值方程](@entry_id:192306)写作：

$\hat{T}_\mathbf{R}\psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R}) = C_\mathbf{R} \psi(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{R}}\psi(\mathbf{r})$

这个矢量 $\mathbf{k}$ 被称为**[波矢](@entry_id:178620)**或**晶体[波矢](@entry_id:178620)**。它是一个[量子数](@entry_id:145558)，用于标记由平移对称性产生的不同[本征态](@entry_id:149904)。值得注意的是，如果[晶格](@entry_id:196752)的平移对称性被破坏，例如，施加一个均匀外[电场](@entry_id:194326)（其势能项为 $U(x) = -e\mathcal{E}x$），则[哈密顿量](@entry_id:172864)将不再与[平移算符](@entry_id:756122)对易 [@problem_id:1762595]。在这种情况下，$[\hat{H}, \hat{T}_a] \neq 0$，[布洛赫定理](@entry_id:137461)的严格前提便不再成立，系统也不再具有静态的[能带结构](@entry_id:139379)。

### 布洛赫定理的表述与形式

综合以上讨论，我们便得到了**[布洛赫定理](@entry_id:137461)**的两种等价表述：

1.  **平移性质形式**：对于周期势场 $V(\mathbf{r})$ 中的粒子，其能量本征函数 $\psi(\mathbf{r})$ 必然满足如下性质：在任意格矢 $\mathbf{R}$ 的平移下，[波函数](@entry_id:147440)仅仅改变一个相位因子。
    $\psi(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}\psi(\mathbf{r})$

2.  **[布洛赫函数](@entry_id:189422)形式**：能量本征函数 $\psi(\mathbf{r})$ 可以写成一个平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 与一个具有[晶格](@entry_id:196752)周期性的函数 $u_\mathbf{k}(\mathbf{r})$ 的乘积。
    $\psi_\mathbf{k}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_\mathbf{k}(\mathbf{r})$
    其中 $u_\mathbf{k}(\mathbf{r}+\mathbf{R}) = u_\mathbf{k}(\mathbf{r})$。

这两种形式是完[全等](@entry_id:273198)价的。从第二种形式出发，我们可以轻易验证第一种形式：
$\psi_\mathbf{k}(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})} u_\mathbf{k}(\mathbf{r}+\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{r}} e^{i\mathbf{k}\cdot\mathbf{R}} u_\mathbf{k}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{R}} \psi_\mathbf{k}(\mathbf{r})$

[布洛赫函数](@entry_id:189422) $u_\mathbf{k}(\mathbf{r})$ 调制了[平面波](@entry_id:189798)包络，体现了原子实[势场](@entry_id:143025)对电子[波函数](@entry_id:147440)的局部影响。为了具体理解哪些函数可以作为[布洛赫波函数](@entry_id:144223)，我们可以考察一些一维的例子 [@problem_id:1355526]。在一个周期为 $a$ 的[晶格](@entry_id:196752)中：
*   形如 $\psi_A(x) = A \sin(\frac{2\pi x}{a})$ 的函数是合法的。因为 $\psi_A(x+a) = A \sin(\frac{2\pi x}{a} + 2\pi) = \psi_A(x)$，这对应于 $e^{ika}=1$，即 $k=0$（或 $k$ 为[倒格矢](@entry_id:263351) $2\pi m/a$）。
*   形如 $\psi_B(x) = B \cos(\frac{\pi x}{a})$ 的函数也是合法的。因为 $\psi_B(x+a) = B \cos(\frac{\pi x}{a} + \pi) = -\psi_B(x)$，这对应于 $e^{ika}=-1$，即 $k=\pi/a$。
*   然而，像高斯函数 $\psi_C(x) = C \exp(-x^2 / \lambda^2)$ 这样的局域函数，其平移后的比值 $\psi_C(x+a)/\psi_C(x)$ 依赖于 $x$，因此不是一个常数相位因子，故不是[布洛赫函数](@entry_id:189422)。
*   一个有趣的形式是 $\psi_E(x) = E \sum_{n=-\infty}^{\infty} \exp\left(-\frac{(x-na)^2}{2\sigma^2}\right)$。这是一个由在每个格点处放置相同函数（这里是高斯函数）并求和构造的函数。通过变量代换可以证明 $\psi_E(x+a)=\psi_E(x)$，因此它是一个合法的[布洛赫函数](@entry_id:189422)，且晶体[波矢](@entry_id:178620) $k=0$ [@problem_id:1355526]。

[布洛赫定理](@entry_id:137461)的一个直接而重要的物理推论是，电子在晶体中的**概率密度** $|\psi_\mathbf{k}(\mathbf{r})|^2$ 具有[晶格](@entry_id:196752)的周期性。
$|\psi_\mathbf{k}(\mathbf{r})|^2 = |e^{i\mathbf{k}\cdot\mathbf{r}} u_\mathbf{k}(\mathbf{r})|^2 = |e^{i\mathbf{k}\cdot\mathbf{r}}|^2 |u_\mathbf{k}(\mathbf{r})|^2 = |u_\mathbf{k}(\mathbf{r})|^2$
由于 $u_\mathbf{k}(\mathbf{r})$ 是[周期函数](@entry_id:139337)，所以 $|\psi_\mathbf{k}(\mathbf{r})|^2$ 也是周期函数。这意味着，尽管电子作为一个波在整个晶体中传播，但找到它的概率在每个原胞中的[分布](@entry_id:182848)是完全相同的。电子并非[均匀分布](@entry_id:194597)，而是倾向于出现在原胞内的某些特定区域 [@problem_id:2082262]。例如，对于一个[布洛赫函数](@entry_id:189422)，其周期部分为 $u_k(x) = C(1 + \beta \cos(2\pi x/a))$，其[概率密度](@entry_id:175496)与 $|u_k(x)|^2$ 成正比。密度的最大值和最小值之比为 $((1+|\beta|)/(1-|\beta|))^2$，这表明[电子概率密度](@entry_id:197449)在[原胞](@entry_id:159354)内部受到了显著的调制。

### 晶体动量与[布里渊区](@entry_id:142395)

#### 晶体动量 vs. [机械动量](@entry_id:156068)

与[布洛赫波矢](@entry_id:746866) $\mathbf{k}$ 相关的物理量 $\hbar\mathbf{k}$ 被称为**[晶体动量](@entry_id:136369)** (crystal momentum) 或**[准动量](@entry_id:143609)** (quasimomentum)。这个名称具有启发性，但也容易引起误解。必须强调，**晶体动量 $\hbar\mathbf{k}$ 不是电子的[机械动量](@entry_id:156068)**。[机械动量](@entry_id:156068)算符是 $\hat{\mathbf{p}} = -i\hbar\nabla$。一个[布洛赫态](@entry_id:147552) $\psi_\mathbf{k}$ 通常不是 $\hat{\mathbf{p}}$ 的[本征态](@entry_id:149904)，除非[势场](@entry_id:143025) $V(\mathbf{r})$ 为零（自由电子情况）。

作用动量算符于[布洛赫函数](@entry_id:189422)上可以清楚地看到这一点：
$\hat{\mathbf{p}}\psi_\mathbf{k}(\mathbf{r}) = -i\hbar\nabla(e^{i\mathbf{k}\cdot\mathbf{r}} u_\mathbf{k}(\mathbf{r})) = -i\hbar(i\mathbf{k} e^{i\mathbf{k}\cdot\mathbf{r}} u_\mathbf{k}(\mathbf{r}) + e^{i\mathbf{k}\cdot\mathbf{r}}\nabla u_\mathbf{k}(\mathbf{r})) = \hbar\mathbf{k}\psi_\mathbf{k}(\mathbf{r}) + e^{i\mathbf{k}\cdot\mathbf{r}}(-i\hbar\nabla u_\mathbf{k}(\mathbf{r}))$
只有当 $u_\mathbf{k}(\mathbf{r})$ 是常数时（自由电子），$\psi_\mathbf{k}$ 才是动量本征态。一般而言，[布洛赫态](@entry_id:147552)是多个不同[机械动量](@entry_id:156068)的平面波的叠加。

我们可以通过一个具体的例子来计算[布洛赫态](@entry_id:147552)的平均[机械动量](@entry_id:156068) $\langle\hat{p}\rangle$ [@problem_id:2082285]。考虑一个一维[布洛赫态](@entry_id:147552)，其周期部分 $u_k(x)$ 是两个平面波的叠加 $u_k(x) = C_0 + C_1 e^{-iGx}$，其中 $G=2\pi/a$ 是[倒格矢](@entry_id:263351)。在布里渊区边界 $k=\pi/a$，[波函数](@entry_id:147440)可以写成 $\psi_k(x) = C_0 e^{ikx} + C_1 e^{-ikx}$。通过计算可以发现，该状态的平均[机械动量](@entry_id:156068)为：
$\langle\hat{p}\rangle = \hbar k \frac{C_0^2 - C_1^2}{C_0^2 + C_1^2} = \hbar k \frac{1 - r^2}{1 + r^2}$
其中 $r = C_1/C_0$。这个结果清楚地表明，$\langle\hat{p}\rangle$ 并不等于晶体动量 $\hbar k$，除非 $C_1=0$（自由电子波）。特别地，当 $C_0=C_1$ ($r=1$) 时，[波函数](@entry_id:147440)是[驻波](@entry_id:148648) $\psi_k(x) \propto \cos(kx)$，其平均[机械动量](@entry_id:156068) $\langle\hat{p}\rangle=0$，即使其晶体动量为 $\hbar k = \hbar\pi/a$。这深刻揭示了晶体动量描述的是[波函数](@entry_id:147440)在[晶格](@entry_id:196752)平移下的变换性质，而非粒子的真实动量。

#### 倒易点阵与布里渊区

波矢 $\mathbf{k}$ 的取值范围是在一个被称为**倒易空间** (reciprocal space) 的数学空间中。对于给定的[实空间](@entry_id:754128)[晶格](@entry_id:196752)（由[基矢](@entry_id:199546) $\mathbf{a}_i$ 定义），其对应的倒易点阵 (reciprocal lattice) 由一组**[倒格矢](@entry_id:263351)** $\mathbf{G}$ 构成，这些矢量满足条件 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$ (即 $\mathbf{G}\cdot\mathbf{R} = 2\pi \times \text{整数}$) 对所有实空间格矢 $\mathbf{R}$ 成立。

[波矢](@entry_id:178620) $\mathbf{k}$ 的定义存在冗余。如果我们将 $\mathbf{k}$ 替换为 $\mathbf{k}+\mathbf{G}$，其中 $\mathbf{G}$ 是任意一个[倒格矢](@entry_id:263351)，[布洛赫定理](@entry_id:137461)的平移性质仍然成立，只是函数 $u_\mathbf{k}(\mathbf{r})$ 会相应地改变：
$\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}} u_{\mathbf{k}+\mathbf{G}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} (e^{i\mathbf{G}\cdot\mathbf{r}} u_{\mathbf{k}+\mathbf{G}}(\mathbf{r}))$
我们可以定义一个新的周期函数 $u'_\mathbf{k}(\mathbf{r}) = e^{i\mathbf{G}\cdot\mathbf{r}} u_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$，这样 $\psi_{\mathbf{k}+\mathbf{G}}(\mathbf{r})$ 就等价于一个[波矢](@entry_id:178620)为 $\mathbf{k}$ 但周期部分不同的[布洛赫函数](@entry_id:189422)。更重要的是，能量是倒易空间的周期函数：$E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})$ [@problem_id:2972775]。

为了消除这种冗余，我们将 $\mathbf{k}$ 的取值限制在一个倒易空间中的基本单元内。这个标准的基本单元被称为**[第一布里渊区](@entry_id:269110)** (First Brillouin Zone, BZ)。[第一布里渊区](@entry_id:269110)的标准定义是倒易点阵的**[维格纳-赛兹原胞](@entry_id:137574)** (Wigner-Seitz cell)。它是在[倒易空间](@entry_id:754151)中，从原点 $(\mathbf{k}=0)$ 出发，到所有邻近倒格点的连线的中垂面（或线）所围成的最小体积区域 [@problem_id:2972775]。例如，对于[实空间](@entry_id:754128)中的二维三角[晶格](@entry_id:196752)，其[倒易晶格](@entry_id:136718)也是三角[晶格](@entry_id:196752)，而其[第一布里渊区](@entry_id:269110)则是一个正六边形。

[第一布里渊区](@entry_id:269110)的体积是一个重要的物理量，它与[实空间](@entry_id:754128)[原胞](@entry_id:159354)的体积 $V_{\text{cell}}$ 有着简单的关系：$V_{\text{BZ}} = (2\pi)^d / V_{\text{cell}}$，其中 $d$ 是维度。这个体积决定了每个能带中独立电子态的总数 [@problem_id:2972775]。

对于一个宏观晶体，我们通常施加**周期性边界条件**（[玻恩-冯·卡门边界条件](@entry_id:140446)）。例如，对于一个长度为 $L=Na$ 的一维晶体链，要求 $\psi(x) = \psi(x+L)$。将布洛赫定理代入此条件可得 $e^{ikL}=1$，这导致波矢 $k$ 的取值是量子化的 [@problem_id:1762559]：
$k = \frac{2\pi n}{L} = \frac{2\pi n}{Na}$，其中 $n$ 为整数。
在[第一布里渊区](@entry_id:269110) $(-\pi/a, \pi/a]$ 内，共有 $N$ 个独立的 $k$ 值。由于 $N$ 在宏观晶体中是巨大数目（约 $10^{23}$），这些离散的 $k$ 值形成了一个**准连续**的变量。

### 能带与[带隙](@entry_id:191975)

至此，我们已经建立了描述晶体中电子态的两个量子数：准连续的[波矢](@entry_id:178620) $\mathbf{k}$（标记平移对称性）和另一个[量子数](@entry_id:145558)，我们称之为**能带指标** (band index) $n$ [@problem_id:1355548]。对于每一个允许的[波矢](@entry_id:178620) $\mathbf{k}$，薛定谔方程存在一系列离散的[能量本征值](@entry_id:144381)，我们用整数 $n=1, 2, 3, \ldots$ 来标记它们。这些[能量本征值](@entry_id:144381) $E_{n}(\mathbf{k})$ 随着 $\mathbf{k}$ 在布里渊区内的变化而形成连续的曲[线或](@entry_id:170208)[曲面](@entry_id:267450)，这些曲线或[曲面](@entry_id:267450)就是**能带** (energy bands)。

#### 无散射传播与[能隙的起源](@entry_id:187265)

[布洛赫定理](@entry_id:137461)最深刻的结论之一是：在完美的[周期性势场](@entry_id:140652)中，一个处于[布洛赫态](@entry_id:147552)的电子可以不受散射地在晶体中传播 [@problem_id:1762587]。这是因为[布洛赫态](@entry_id:147552)已经是整个周期性系统（电子+所有离子）的[哈密顿量](@entry_id:172864)的定态解。一个系统处于定态时，其概率密度 $|\psi(\mathbf{r})|^2$ 不随时间改变，因此不会发生散射。散射事件本质上是电子从一个本征态到另一个[本征态](@entry_id:149904)的跃迁，这需要一个破坏系统完美周期性的扰动，如晶格振动（[声子](@entry_id:140728)）、杂质或缺陷。

然而，[周期性势场](@entry_id:140652)本身并非无足轻重。它深刻地改变了自由电子的能量-动量关系 $E = \hbar^2k^2/2m$。当电子的德布罗意波长与[晶格](@entry_id:196752)周期具有特定的匹配关系时，会发生类似于[X射线衍射](@entry_id:147790)的**[布拉格反射](@entry_id:184358)** (Bragg reflection)。这种情况恰好发生在[布里渊区](@entry_id:142395)的边界上。

在[布里渊区](@entry_id:142395)边界，一个波矢为 $\mathbf{k}$ 的电子波会与其被[晶格](@entry_id:196752)反射回来的波（波矢为 $\mathbf{k}-\mathbf{G}$）强烈干涉。在**[近自由电子模型](@entry_id:138124)** (nearly-free electron model) 中，我们可以清晰地看到这一现象 [@problem_id:2082278]。在[布里渊区](@entry_id:142395)边界，自由电子的态 $\mathbf{k}$ 和 $\mathbf{k}-\mathbf{G}$ 的能量是简并的 ($E(\mathbf{k}) = E(\mathbf{k}-\mathbf{G})$)。微弱的周期势场 $V(\mathbf{r})$ 会耦合这两个简并态，导致[能量简并](@entry_id:203091)被解除，形成一个能量[禁带](@entry_id:175956)，即**[带隙](@entry_id:191975)** (band gap)。

[带隙](@entry_id:191975)的大小可以通过[微扰理论](@entry_id:138766)计算。对于一个由 $V(x) = 2U \cos(2\pi x/a)$ 描述的势场，其傅里叶分量为 $V_G = V_{-G} = U$，其中 $G=2\pi/a$。在[第一布里渊区](@entry_id:269110)边界 $k=\pi/a$ 处，[简并微扰理论](@entry_id:143587)给出两个新的[能量本征值](@entry_id:144381) $E_{\pm} = E^{(0)}(\pi/a) \pm |V_G|$。这两个能级之间的能量差 $\Delta E_g = 2|V_G| = 2U$ 就是[带隙](@entry_id:191975)的宽度 [@problem_id:2082278]。这表明，[带隙](@entry_id:191975)的大小直接取决于周期势中对应[倒格矢](@entry_id:263351)的傅里叶分量的强度。

**克罗尼格-彭尼模型** (Kronig-Penney model) 从另一个角度也揭示了能带和[带隙](@entry_id:191975)的形成 [@problem_id:1762585]。该模型求解了一个周期性梳状delta[势场](@entry_id:143025)中的薛定谔方程，得到了一个关于能量 $E$ 和波矢 $k$ 的[超越方程](@entry_id:276279)：$\cos(ka) = f(E)$。由于 $\cos(ka)$ 的值域是 $[-1, 1]$，只有当函数 $f(E)$ 的值落在这个区间内时，方程才有实数解 $k$，这些能量 $E$ 的范围构成了允许的**能带**。而当 $|f(E)| \gt 1$ 时，方程没有实数解 $k$（只有虚数解，对应于在晶体中衰减的波），这些能量范围就是**[带隙](@entry_id:191975)**。利用该模型，可以推算出在弱[势场](@entry_id:143025)极限下，第一[带隙](@entry_id:191975)的宽度近似为 $\Delta E_g \approx \frac{2\hbar^2 P}{ma^2}$，其中 $P$ 是一个与[势场](@entry_id:143025)强度成正比的[无量纲参数](@entry_id:169335)。

#### 能带的对称性

除了平移对称性，[晶格](@entry_id:196752)的其他空间对称性（如旋转、反映）也会对[能带结构](@entry_id:139379) $E_n(\mathbf{k})$ 施加约束。一个普遍且重要的对称性是**反演对称性** (inversion symmetry)，即[势场](@entry_id:143025)满足 $V(\mathbf{r}) = V(-\mathbf{r})$。如果晶体具有反演对称性，那么[能量本征值](@entry_id:144381)必然满足 $E_n(\mathbf{k}) = E_n(-\mathbf{k})$ [@problem_id:1762572]。这是因为如果 $\psi_{n,\mathbf{k}}(\mathbf{r})$ 是一个能量为 $E_n(\mathbf{k})$ 的[布洛赫态](@entry_id:147552)，那么通过空间反演得到的函数 $\phi(\mathbf{r}) = \psi_{n,\mathbf{k}}(-\mathbf{r})$ 必定是另一个能量相同但[波矢](@entry_id:178620)为 $-\mathbf{k}$ 的[布洛赫态](@entry_id:147552)。

### 能带中的电子动力学：有效质量

[布洛赫定理](@entry_id:137461)不仅解释了静态的[能带结构](@entry_id:139379)，还为理解电子在能带中如何响应外力（如[电场](@entry_id:194326)或[磁场](@entry_id:153296)）提供了基础。在半经典图像中，外力 $\mathbf{F}_{ext}$ 不会引起电子在能带间的跃迁，而是使其[晶体动量](@entry_id:136369) $\hbar\mathbf{k}$ 随时间演化：

$\hbar \frac{d\mathbf{k}}{dt} = \mathbf{F}_{ext}$

电子的加速度则由其群速度 $v_g = \frac{1}{\hbar}\nabla_\mathbf{k}E(\mathbf{k})$ 对时间的导数给出。结合这两个关系，我们可以得到电子的加速度与外力的关系，这类似于牛顿第二定律 $\mathbf{a} = \mathbf{F}/m$。然而，这里的[惯性质量](@entry_id:267233)不再是自由电子的质量 $m_e$，而是由能带的形状决定的**有效质量** (effective mass) $m^*$。

有效质量是一个张量，其逆矩阵定义为：
$(\mathbf{m}^{*-1})_{ij} = \frac{1}{\hbar^2} \frac{\partial^2 E_n(\mathbf{k})}{\partial k_i \partial k_j}$

这个定义表明，有效质量正比于能带曲率的倒数。在能带底部（能量极小值处），$E(\mathbf{k})$ 通常是 $\mathbf{k}$ 的二次型，曲率为正，[有效质量](@entry_id:142879)为正。电子在此处的行为类似于一个普通的带正质量的粒子。而在能带顶部（能量极大值处），曲率为负，[有效质量](@entry_id:142879)为负。这意味着在外[电场](@entry_id:194326)作用下，该电子的加速度方向与作用力相反，其行为如同一个带相反[电荷](@entry_id:275494)的粒子——这正是**空穴** (hole) 概念的起源。

[有效质量](@entry_id:142879)不一定是常数，它可以依赖于在[倒易空间](@entry_id:754151)中的位置 $\mathbf{k}$，并且可以是各向异性的。考虑一个[二维材料](@entry_id:142244)，其能带底部附近的[色散关系](@entry_id:140395)为 $E(k_x, k_y) = E_{\min} + A k_x^2 + B k_y^4$ [@problem_id:1762550]。根据定义，我们可以计算出[有效质量张量](@entry_id:147018)的对角分量：
$m^*_{xx} = \frac{\hbar^2}{2A}$
$m^*_{yy} = \frac{\hbar^2}{12B k_y^2}$

可见，在 $k_x$ 方向，[有效质量](@entry_id:142879)是恒定的。但在 $k_y$ 方向，有效质量依赖于 $k_y$ 的值。这说明电子在不同方向上对相同外力的响应是不同的，并且这种响应还取决于电子自身的状态 $\mathbf{k}$。[有效质量](@entry_id:142879)的概念将复杂的[晶格](@entry_id:196752)相互作用“打包”进一个参数中，极大地简化了对晶体中[载流子动力学](@entry_id:180791)的描述。

综上所述，源于[晶格](@entry_id:196752)[平移对称性](@entry_id:171614)的布洛赫定理，不仅为我们提供了描述电子态的[布洛赫函数](@entry_id:189422)和[晶体动量](@entry_id:136369)，更从根本上解释了固体物理中最重要的概念——能带、[带隙](@entry_id:191975)和[有效质量](@entry_id:142879)。这些概念是理解和设计[半导体器件](@entry_id:192345)、金属、绝缘体等各类材料电学和光学性质的基石。