## 引言
密度泛函理论（DFT）已成为现代计算材料科学、凝聚态物理和[量子化学](@entry_id:140193)中不可或缺的基石。其成功的核心在于一个巧妙的平衡：在保证足够精度的同时，维持了计算上的可行性。这一成功的关键，全部系于一个核心却又难以捉摸的量——交换关联（XC）泛函。理论上，精确的交换关联泛函能够完美描述电子间的相互作用，从而给出任何系统的精确[基态](@entry_id:150928)性质。然而，其精确形式至今未知。

这一知识上的空白催生了计算科学领域最活跃的研究方向之一：发展和验证近似的交换关联泛函。这导致了一个庞大且看似复杂的“泛函动物园”，从简单的[局域密度近似](@entry_id:138982)（[LDA](@entry_id:138982)）到复杂的完全非局域方法，每一类都有其独特的优势和固有的局限性。对于研究者和学生而言，如何在这个“动物园”中导航，理解不同泛函背后的物理原理，并为特定问题选择最合适的工具，已成为一项关键的挑战和必备的技能。

本文旨在系统性地梳理这一复杂领域，为读者搭建一座从基础理论通往实际应用的桥梁。我们将分为三个章节，逐步深入交换关联泛函的世界。首先，在“原理与机制”一章中，我们将回顾DFT的形式基础，阐明[Kohn-Sham方案](@entry_id:146049)如何将问题聚焦于交换关联能，并详细介绍被誉为“[雅各布天梯](@entry_id:139901)”的泛函层级结构，剖析每一级泛函的设计哲学和关键缺陷。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将通过具体的应用实例，展示这些泛函在预测材料结构、[电子性质](@entry_id:748898)、弱相互作用和[强关联体系](@entry_id:145791)时的表现，并探讨DFT如何与[多体微扰理论](@entry_id:168555)等前沿方法相结合。最后，在“动手实践”部分，我们将通过精心设计的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将能够建立起对交换关联泛函的深刻理解，从而更自信、更准确地运用DFT解决科学与工程问题。

## 原理与机制

在介绍性章节中，我们确立了密度泛函理论（DFT）的核心思想，即一个多电子体系的[基态](@entry_id:150928)性质完全由其[基态](@entry_id:150928)电子密度 $n(\mathbf{r})$ 唯一决定。本章将深入探讨支撑这一理论的数学原理和物理机制。我们将从形式化的理论基础出发，过渡到实用的计算方案，并最终系统地审视构建近似交换关联泛函的现代策略及其固有的局限性。

### 密度泛函理论的形式基础

DFT 的理论基石由 Hohenberg-Kohn (HK) 定理奠定，它们为以电子密度作为基本变量的量子力学理论提供了严格的[数学证明](@entry_id:137161)。

第一个 Hohenberg-Kohn 定理是一个[存在性定理](@entry_id:261096)。它断言，对于一个处于非简并[基态](@entry_id:150928)的相互作用电子体系，其[基态](@entry_id:150928)电子密度 $n_0(\mathbf{r})$ 与系统所处的外势 $v(\mathbf{r})$ 之间存在一一对应关系（最多相差一个无关紧要的常数）。这个定理的推论是深远的：由于 $v(\mathbf{r})$ 决定了系统的[哈密顿量](@entry_id:172864) $\hat{H}$，而 $\hat{H}$ 又决定了系统的所有性质（包括[多体波函数](@entry_id:203043)），因此，所有[基态](@entry_id:150928)性质都可以被视为基[态密度](@entry_id:147894) $n_0(\mathbf{r})$ 的泛函。例如，系统的动能 $T[n_0]$、势能 $V[n_0]$ 以及总能量 $E_0[n_0]$ 都是密度的泛函。[@problem_id:2821083]

第二个 Hohenberg-Kohn 定理建立了一个基于密度的[变分原理](@entry_id:198028)。它定义了一个[普适泛函](@entry_id:140176) $F[n]$，该泛函仅依赖于电子密度 $n(\mathbf{r})$，而与具体系统所处的外势 $v(\mathbf{r})$ 无关。总[能量泛函](@entry_id:170311)可以写作：

$$
E_v[n] = F[n] + \int n(\mathbf{r}) v(\mathbf{r}) d\mathbf{r}
$$

该定理指出，对于真实的基态密度 $n_0(\mathbf{r})$，[能量泛函](@entry_id:170311) $E_v[n]$ 会取其[全局最小值](@entry_id:165977)，这个最小值就是体系的基态能量 $E_0$。这意味着我们可以通过最小化 $E_v[n]$ 来寻找基态密度和基态能量，前提是 $F[n]$ 的形式是已知的。

这个**[普适泛函](@entry_id:140176) $F[n]$** 包含了相互作用体系的动能和电子间[相互作用能](@entry_id:264333)。对其最严格的定义来自 Levy-Lieb 的**约[束搜索](@entry_id:634146)**（constrained search）表述 [@problem_id:2821083]。在此表述中，$F[n]$ 被定义为在所有产生给定密度 $n(\mathbf{r})$ 的 $N$ 电子[反对称波函数](@entry_id:153813) $\Psi$ 中，动能与[电子-电子相互作用](@entry_id:139900)能之和的最小值：

$$
F[n] = \min_{\Psi \to n} \langle \Psi | \hat{T} + \hat{W} | \Psi \rangle
$$

其中 $\hat{T}$ 是[动能算符](@entry_id:265633)，$\hat{W}$ 是电子-电子[库仑相互作用](@entry_id:747947)算符。这种表述的优越性在于它明确了 $F[n]$ 的定义域是所有“$N$-可表示”的密度，即那些可以从某个合法的[反对称波函数](@entry_id:153813)得到的密度。然而，HK 定理虽然证明了 $F[n]$ 的存在性和普适性，却没有给出其具体的解析形式。这便是 DFT 发展的核心挑战：寻找 $F[n]$ 的精确或足够准确的近似形式。

### Kohn-Sham 构造：从相互作用体系到非相互作用体系的映射

直接近似[普适泛函](@entry_id:140176) $F[n]$ 是极其困难的，尤其是其中的动能部分 $T[n]$。对于相互作用体系，动能与电子密度之间的关系非常复杂。Kohn-Sham (KS) 方法巧妙地规避了这个问题。其核心思想是引入一个虚拟的、无相互作用的电子体系，该体系被设计为与真实的相互作用体系具有完全相同的[基态](@entry_id:150928)电子密度 $n(\mathbf{r})$。

由于这个辅助体系是无相互作用的，其动能 $T_s[n]$ 可以精确地通过单粒子[轨道](@entry_id:137151) $\phi_i(\mathbf{r})$ 来表示：

$$
T_s[n] = -\frac{1}{2} \sum_{i=1}^N \int \phi_i^*(\mathbf{r}) \nabla^2 \phi_i(\mathbf{r}) d\mathbf{r}
$$

其中密度由这些 KS [轨道](@entry_id:137151)构成：$n(\mathbf{r}) = \sum_{i=1}^N |\phi_i(\mathbf{r})|^2$。

通过这种方式，Kohn 和 Sham 将[普适泛函](@entry_id:140176) $F[n]$ 分解为三部分 [@problem_id:2821174]：
1.  **无相互作用动能 $T_s[n]$**：如上定义的、易于计算的部分。
2.  **哈特里能 (Hartree energy) $E_H[n]$**：电子密度[分布](@entry_id:182848)的经典静电自排斥能。
    $$
    E_H[n] = \frac{1}{2} \iint \frac{n(\mathbf{r}) n(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} d\mathbf{r} d\mathbf{r}'
    $$
3.  **交换关联能 (exchange-correlation energy) $E_{xc}[n]$**：这是一个“[余项](@entry_id:159839)”，但包含了所有非经典、多体的复杂效应。其定义为：
    $$
    E_{xc}[n] = (T[n] - T_s[n]) + (W[n] - E_H[n])
    $$
    它包括了真实动能与无相互作用动能之差，以及真实电子[相互作用能](@entry_id:264333)与经典哈特里能之差。前者包含了与关联效应相关的动能贡献，后者则包含了[泡利不相容原理](@entry_id:141850)导致的交换效应和电子运动的动态关联效应。

现在，总能量泛函可以写作：
$$
E[n] = T_s[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) d\mathbf{r} + E_H[n] + E_{xc}[n]
$$

根据变分原理，通过最小化这个[能量泛函](@entry_id:170311)，我们可以推导出一组类似于单粒子薛定谔方程的[自洽方程](@entry_id:155949)，即 **Kohn-Sham 方程** [@problem_id:2821174]：

$$
\left[ -\frac{1}{2}\nabla^2 + v_s(\mathbf{r}) \right] \phi_i(\mathbf{r}) = \epsilon_i \phi_i(\mathbf{r})
$$

这里的 $\epsilon_i$ 是 KS [轨道能量](@entry_id:158481)，而 $v_s(\mathbf{r})$ 是局域的**有效 Kohn-Sham 势**，它由三部分组成：

$$
v_s(\mathbf{r}) = v_{\text{ext}}(\mathbf{r}) + v_H(\mathbf{r}) + v_{xc}(\mathbf{r})
$$

其中，$v_H(\mathbf{r}) = \int \frac{n(\mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} d\mathbf{r}'$ 是哈特里势，而**交换关联势** $v_{xc}(\mathbf{r})$ 被严格定义为交换关联能对密度的泛函导数：

$$
v_{xc}(\mathbf{r}) = \frac{\delta E_{xc}[n]}{\delta n(\mathbf{r})}
$$

KS 方法的巨大成功在于，它将寻找未知泛函 $F[n]$ 的艰巨任务，转化为寻找一个相对较小但至关重要的部分——交换关联能泛函 $E_{xc}[n]$ 的近似。DFT 的所有近似都集中在对 $E_{xc}[n]$ 的建模上。

### 交换与关联的物理图像：交换关联洞

在深入探讨各种 $E_{xc}[n]$ 的近似形式之前，我们有必要建立一个关于交换与关联的物理图像。这可以通过**交换关联洞 (exchange-correlation hole)** $n_{xc}(\mathbf{r}, \mathbf{r}')$ 的概念来实现。

想象在 $\mathbf{r}$ 处有一个参考电子。由于[泡利不相容原理](@entry_id:141850)（交换效应）和[库仑排斥](@entry_id:181876)（关联效应），在 $\mathbf{r}$ 的周围找到另一个电子的概率会降低。交换关联洞 $n_{xc}(\mathbf{r}, \mathbf{r}')$ 描述的正是这种相对于平均密度 $n(\mathbf{r}')$ 的电子密度亏损。更形式化地，它将体系的二体密度 $n_2(\mathbf{r}, \mathbf{r}')$ 与一体密度的乘积联系起来 [@problem_id:2821191]：

$$
n_2(\mathbf{r}, \mathbf{r}') = n(\mathbf{r}) \left[ n(\mathbf{r}') + n_{xc}(\mathbf{r}, \mathbf{r}') \right]
$$

交换关联洞有一个极其重要的**求和规则 (sum rule)**。通过对上式积分并利用粒子数守恒，可以证明，对于任意参考电子位置 $\mathbf{r}$，其周围的交换关联洞所包含的总[电荷](@entry_id:275494)恰好为一个电子 [@problem_id:2821191]：

$$
\int n_{xc}(\mathbf{r}, \mathbf{r}') d\mathbf{r}' = -1
$$

这个规则意味着，每个电子都被一个等效的、携带 $+1e$ [电荷](@entry_id:275494)的“洞”所包裹，形成一个[电中性](@entry_id:157680)的[准粒子](@entry_id:136584)。这个图像为理解[电子屏蔽效应](@entry_id:142169)提供了基础。

交换关联能 $E_{xc}[n]$ 的物理意义也因此变得清晰：它是在**[绝热连接](@entry_id:199259) (adiabatic connection)** 框架下，一个电子与其周围的交换关联洞（在不同[相互作用强度](@entry_id:192243)下平均）之间的[静电相互作用](@entry_id:166363)能 [@problem_id:2821191]。

$$
E_{xc}[n] = \frac{1}{2} \int n(\mathbf{r}) d\mathbf{r} \int \frac{\bar{n}_{xc}(\mathbf{r}, \mathbf{r}')}{|\mathbf{r} - \mathbf{r}'|} d\mathbf{r}'
$$

其中 $\bar{n}_{xc}$ 是沿着一个将相互作用从 0（KS 系统）连续变化到 1（物理系统）的路径上对洞函数的平均。我们还可以进一步将洞分解为**交换洞 (exchange hole)** $n_x$ 和**关联洞 (correlation hole)** $n_c$。交换洞来自[泡利不相容原理](@entry_id:141850)，仅存在于自旋相同的电子之间，它满足 $\int n_x(\mathbf{r}, \mathbf{r}') d\mathbf{r}' = -1$。关联洞则描述了电子为躲避彼此而产生的额外运动，它满足电荷守恒 $\int n_c(\mathbf{r}, \mathbf{r}') d\mathbf{r}' = 0$ [@problem_id:2821191]。这两个求和规则是构建和检验近似泛函的重要约束条件。

### 近似泛函的层级：[雅各布天梯](@entry_id:139901)

寻找精确 $E_{xc}[n]$ 的努力催生了大量近似泛函。Perdew 将这些泛函的演进归纳为一个富有想象力的层级结构，称为**[雅各布天梯](@entry_id:139901) (Jacob's Ladder)**。每一级“阶梯”代表一类泛函，通过引入更复杂的、能够描述更多[物理信息](@entry_id:152556)的“原料”，从而在向“[化学精度](@entry_id:171082)”这一天堂攀升的过程中达到更高的准确性 [@problem_id:2821054]。

#### 第一级：局域密度近似 (LDA)

[LDA](@entry_id:138982) 是最简单、也是最基础的近似。它假设在空间的每一点 $\mathbf{r}$，非[均匀电子气](@entry_id:163911)的交换关联能密度与一个具有相同局域密度 $n(\mathbf{r})$ 的**[均匀电子气](@entry_id:163911) (Uniform Electron Gas, UEG)** 的交换关联能密度相同。其数学形式为 [@problem_id:2821157]：

$$
E_{xc}^{\text{LDA}}[n] = \int n(\mathbf{r}) \varepsilon_{xc}^{\text{UEG}}(n(\mathbf{r})) d\mathbf{r}
$$

这里，唯一的“原料”是局域电子密度 $n(\mathbf{r})$。$\varepsilon_{xc}^{\text{UEG}}(n)$ 是[均匀电子气](@entry_id:163911)的交换关联能（每个粒子）。值得强调的是，LDA 是一个完全的**第一性原理**方法。它的核心输入量 $\varepsilon_{xc}^{\text{UEG}}(n)$ 并非通[过拟合](@entry_id:139093)实验数据得到，而是基于对 UEG 这一理论模型的精确计算：其交换部分有解析解（狄拉克公式），而关联部分则通过高精度的**[量子蒙特卡洛](@entry_id:144383) (Quantum Monte Carlo, QMC)** 模拟得到，并拟合成关于密度的[解析函数](@entry_id:139584) [@problem_id:2821157]。LDA 对于 UEG 是精确的，并且处处满足交换关联洞的归一化求和规则 [@problem_id:2821054]。尽管 LDA 对[键能](@entry_id:142761)有过高估计的倾向，但它在描述金属和高密度体系方面取得了惊人的成功。

#### 第二级：[广义梯度近似 (GGA)](@entry_id:140295)

真实材料中的电子密度很少是均匀的。为了修正 LDA 的局域性假设，GGA 引入了电子密度的**梯度 $\nabla n(\mathbf{r})$** 作为额外的原料。GGA 泛函的一般形式为：

$$
E_{xc}^{\text{GGA}}[n] = \int f(n(\mathbf{r}), |\nabla n(\mathbf{r})|) d\mathbf{r}
$$

引入梯度使得泛函能够感知密度的变化快慢，从而更好地区分不同的化学环境。现代非经验性 GGA 的设计并非简单地进行梯度展开，而是巧妙地满足一系列已知的精确约束。以 **PBE (Perdew-Burke-Ernzerhof)** 泛函为例，它的成功源于其构造哲学 [@problem_id:2821135]：
*   通过使用一个在均匀[标度变换](@entry_id:166413)下不变的**无量纲梯度** $s = |\nabla n| / (2 k_F n)$，确保了交换能的正确[标度性质](@entry_id:273821)。
*   通过限制交换增强因子的大小，严格遵守了**李-牛津下限 (Lieb-Oxford bound)**，这是一个对交换关联能的严格约束。
*   它放弃了对缓变密度气体的梯度展开系数的强制满足，而是通过一个巧妙的构造，使得交换和关联的梯度修正项在描述 UEG 的[线性响应](@entry_id:146180)时相互抵消，从而恢复了 [LDA](@entry_id:138982) 在这方面的正确行为 [@problem_id:2821054, @problem_id:2821135]。

GGA，特别是 PBE，极大地改善了对分子几何、[原子化](@entry_id:155635)能和[化学反应](@entry_id:146973)能的描述，成为过去几十年中最受欢迎的泛函之一。

#### 第三级：元[广义梯度近似](@entry_id:274118) ([meta-GGA](@entry_id:191648))

为了进一步提升泛函的辨识能力，[meta-GGA](@entry_id:191648) 在 GGA 的基础上引入了更多的半局域信息，最常用的是**Kohn-Sham 动能密度** $\tau(\mathbf{r})$：

$$
\tau(\mathbf{r}) = \frac{1}{2} \sum_{i}^{\text{occ}} |\nabla \phi_i(\mathbf{r})|^2
$$

由于 $\tau$ 依赖于 KS [轨道](@entry_id:137151)，[meta-GGA](@entry_id:191648) 属于隐式[轨道](@entry_id:137151)依赖泛函。$\tau$ 的引入使得泛函能够区分单[轨道](@entry_id:137151)区域（如原子尾部、氢原子）和多轨道重叠区域（如[共价键](@entry_id:141465)）。以**SCAN (Strongly Constrained and Appropriately Normed)** 泛函为例，它利用一个**等[轨道](@entry_id:137151)指示因子** $\alpha$ 来识别不同的化学环境 [@problem_id:2821173]：

$$
\alpha(\mathbf{r}) = \frac{\tau(\mathbf{r}) - \tau_W(\mathbf{r})}{\tau_{\text{unif}}(n(\mathbf{r}))}
$$

其中 $\tau_W$ 是 von Weizsäcker 动能密度，$\tau_{\text{unif}}$ 是 UEG 的动能密度。这个指示因子有明确的物理含义：在单[轨道](@entry_id:137151)区域，$\tau = \tau_W$，因此 $\alpha = 0$；在类均匀气体区域，$\tau \approx \tau_{\text{unif}}$，因此 $\alpha \approx 1$。通过设计一个依赖于 $\alpha$ 的[插值函数](@entry_id:262791)，SCAN 能够同时满足 17 个已知的精确约束，使其在描述[共价键](@entry_id:141465)、金属键、[离子键](@entry_id:186832)和弱相互作用方面都达到了前所未有的平衡和准确性 [@problem_id:2821054, @problem_id:2821173]。

#### 第四级：[杂化泛函](@entry_id:164921) (Hybrid Functionals)

前面三级阶梯的泛函都是“半局域”的，即在点 $\mathbf{r}$ 处的能量密度只依赖于该点及其无穷小邻域的信息。然而，交换效应本质上是非局域的。为了弥补这一点，杂化泛函通过混合一定比例的**[精确交换](@entry_id:178558)能 (exact exchange)** 来引入非局域性。[精确交换](@entry_id:178558)能的形式与 [Hartree-Fock](@entry_id:142303) 理论中的[交换能](@entry_id:137069)相同，依赖于所有占据的 KS [轨道](@entry_id:137151)。

最简单的**全局杂化泛函**（如 B3LYP 和 PBE0）混合一个固定的[精确交换](@entry_id:178558)比例 $a$：
$$
E_{xc}^{\text{hyb}} = a E_x^{\text{exact}} + (1-a) E_x^{\text{GGA}} + E_c^{\text{GGA}}
$$

更先进的**[范围分离杂化泛函](@entry_id:184447) (range-separated hybrids, RSH)** 则将电子间的库仑相互作用 $1/r$ 分解为短程和长程两部分，并对不同部分采用不同的理论处理 [@problem_id:2821213]。例如，通过[误差函数](@entry_id:176269)将 $1/r$ 分解：

$$
\frac{1}{r} = \underbrace{\frac{\text{erfc}(\omega r)}{r}}_{\text{短程}} + \underbrace{\frac{\text{erf}(\omega r)}{r}}_{\text{长程}}
$$

这里的 $\omega$ 是一个范围分离参数，单位是长度的倒数，它定义了一个相互作用的[特征长度尺度](@entry_id:266383) $1/\omega$。一种常见的 RSH 方案是 HSE (Heyd-Scuseria-Ernzerhof) 泛函，它在短程部分使用[精确交换](@entry_id:178558)，在长程部分使用 GGA 交换。这种设计在保持对[短程相互作用](@entry_id:145678)的精确描述的同时，通过在长程部分使用计算代价较低的 GGA，有效降低了计算成本，尤其适用于固态[能带结构计算](@entry_id:270613)。

#### 第五级：完全非局域泛函

[雅各布天梯](@entry_id:139901)的最高级完全放弃了半局域的限制，转而利用所有占据和未占据的 KS [轨道](@entry_id:137151)来构造 $E_{xc}$。这类方法通常基于**[绝热连接涨落-耗散定理](@entry_id:192440) (Adiabatic-Connection Fluctuation-Dissipation Theorem, ACFDT)** [@problem_id:2821140]。该定理将关联能 $E_c$ 与体系的动[态密度](@entry_id:147894)-密度响应函数 $\chi_\lambda(i\omega)$ 联系起来：

$$
E_{c}[n] = -\frac{1}{2\pi} \int_{0}^{1} d\lambda \int_{0}^{\infty} d\omega \, \text{Tr}\left\{ v \left[ \chi_{\lambda}(i\omega) - \chi_{0}(i\omega) \right] \right\}
$$

其中 $v$ 是[库仑相互作用](@entry_id:747947)核，$\chi_\lambda$ 是[相互作用强度](@entry_id:192243)为 $\lambda$ 时的响应函数，$\chi_0$ 是无相互作用的 KS [响应函数](@entry_id:142629)。

最简单的 ACFDT 近似是**随机相近似 (Random Phase Approximation, RPA)**，它用 $\chi_0$ 来近似构造 $\chi_\lambda$ [@problem_id:2821054]。RPA 的重要性在于，它是[雅各布天梯](@entry_id:139901)上第一个能够从第一性原理出发，系统地描述长程**范德华 (van der Waals) / [色散](@entry_id:263750) (dispersion)** 相互作用的泛函。这是因为[色散力](@entry_id:153203)源于空间上分离的瞬时[电荷](@entry_id:275494)涨落之间的关联，是一种内禀的非局域效应，无法被任何半局域泛函正确描述。

### 近似泛函的关键缺陷与精确条件

攀登[雅各布天梯](@entry_id:139901)的动力源于低阶泛函存在的一些系统性缺陷。理解这些缺陷以及它们所违背的精确条件，对于选择和发展泛函至关重要。

#### 自相互作用误差 (Self-Interaction Error, SIE)

对于一个单电子体系（如氢原子），电子不应与自身发生相互作用。在精确的 DFT 中，[交换能](@entry_id:137069) $E_x[n]$ 必须精确地抵消掉虚假的哈特里[自相互作用](@entry_id:201333)能 $E_H[n]$，即 $E_{xc}[n_{1e}] = -E_H[n_{1e}]$ [@problem_id:2821191]。然而，大多数近似泛函，特别是 [LDA](@entry_id:138982) 和 GGA，都无法满足这个条件，由此产生的残[余能](@entry_id:192009)量被称为**自相互作用误差**。

我们可以通过一个具体的计算来量化这个问题。对于 1s 态的氢原子，其电子密度为 $n(r) = \frac{1}{\pi} e^{-2r}$。我们可以精确计算其哈特里能 $E_H[n] = 5/16$ a.u.。同时，使用[自旋极化](@entry_id:164038)的 LDA (LSD) 交换泛函，可以计算出其交换能为 $E_x^{\text{LSD}}[n] = -\frac{81}{256} (6/\pi^2)^{1/3}$ a.u.。显然，这两项之和 $E_H[n] + E_x^{\text{LSD}}[n]$ 并不为零，这个非零值就是 LSD 泛函[对氢](@entry_id:753096)原子的[自相互作用误差](@entry_id:139981) [@problem_id:47685]。SIE 会导致许多问题，如对[定域电子](@entry_id:751389)态（如 d/f 电子）的错误描述、对反应能垒的低估以及对分子解离曲线的错误行为。[meta-GGA](@entry_id:191648) 和[杂化泛函](@entry_id:164921)通过引入[轨道](@entry_id:137151)依赖性，可以在很大程度上缓解 SIE。

#### [非局域性](@entry_id:140165)问题：[色散](@entry_id:263750)相互作用

如前所述，色散力源于远处[瞬时偶极](@entry_id:139165)之间的长程电动力学关联。任何纯粹依赖于局域密度及其有限阶梯度的泛函（如 [LDA](@entry_id:138982) 和 GGA），其数学形式决定了它们无法描述这种“远距离作用”。当两个分子或片段的电子云没有重叠时，这些泛函计算出的[相互作用能](@entry_id:264333)基本为零，这与物理事实严重不符 [@problem_id:2821187]。

要正确描述[色散力](@entry_id:153203)，必须采用具有内禀[非局域性](@entry_id:140165)的泛函。RPA 就是一个例子。另一类方法是**非局域[范德华密度泛函](@entry_id:203596) (nonlocal van der Waals density functionals, [vdW-DF](@entry_id:203596))**，它们在标准的半局域泛函之上，增加了一个明确的[非局域关联](@entry_id:180194)项 [@problem_id:2821187]：

$$
E_c^{\text{nonlocal}} = \frac{1}{2} \iint n(\mathbf{r}_1) K(\mathbf{r}_1, \mathbf{r}_2) n(\mathbf{r}_2) d\mathbf{r}_1 d\mathbf{r}_2
$$

这里的积分核 $K(\mathbf{r}_1, \mathbf{r}_2)$ 被设计用来捕捉长程关联。此外，在凝聚态体系中，两个实体间的[范德华相互作用](@entry_id:168429)还会受到周围介质的**多体[屏蔽效应](@entry_id:136974) (many-body screening)**，使得[相互作用强度](@entry_id:192243)相比真空中有所减弱 [@problem_id:2821187]。这些都是[高精度计算](@entry_id:200567)中必须考虑的复杂物理。

#### [导数不连续性](@entry_id:136336)与[带隙问题](@entry_id:143831)

对于精确的泛函，总能量 $E(N)$ 作为电子数 $N$ 的函数，在整数之间是**[分段线性](@entry_id:201467) (piecewise linear)** 的 [@problem_id:2821197]。这意味着，化学势 $\mu = \partial E / \partial N$ 在整数 $N$ 处会发生一个跳变。从 $N$ 的左侧逼近时，$\mu = -I$（$I$ 是电离能）；从右侧逼近时，$\mu = -A$（$A$ 是电子亲和能）。

这个物理上的跳变反映在 Kohn-Sham 势中，表现为交换关联势 $v_{xc}(\mathbf{r})$ 在穿过整数电子数时会发生一个不连续的、数值为常数的跃升。这个跃升被称为**[导数不连续性](@entry_id:136336) (derivative discontinuity)** $\Delta_{xc}$。它将基本[带隙](@entry_id:191975) $E_g = I - A$ 与 KS [轨道](@entry_id:137151)[能隙](@entry_id:191975) $\varepsilon_L - \varepsilon_H$（LUMO-HOMO 能量差）联系起来 [@problem_id:2821197]：

$$
E_g = (\varepsilon_L - \varepsilon_H) + \Delta_{xc}
$$

这就是 DFT 中著名的**[带隙问题](@entry_id:143831) (band gap problem)** 的根源。对于 LDA 和 GGA 这类近似泛函，其能量对密度是光滑可导的，导致 $\Delta_{xc} \approx 0$。因此，它们计算出的基本[带隙](@entry_id:191975)约等于 KS [轨道](@entry_id:137151)[能隙](@entry_id:191975)，而后者通常远小于实验测得的真实[带隙](@entry_id:191975)。杂化泛函和更高级的方法由于其非局域性和[轨道](@entry_id:137151)依赖性，能够部分地恢复这种不连续性，从而在预测[带隙](@entry_id:191975)方面表现得更好。理解[导数不连续性](@entry_id:136336)是理解近似 DFT 局限性的关键。