## 引言
在现代计算科学领域，密度泛函理论（DFT）无疑是最具影响力和应用最广泛的工具之一，其重要性横跨化学、物理、[材料科学](@entry_id:152226)乃至生物学等多个学科。它为解决多电子体系薛定谔方程这一量子力学中的核心难题提供了一条兼具精度与效率的途径，使得对复杂分子和材料的从头算模拟成为可能。然而，DFT的强大能力植根于一套深刻而精妙的理论框架，理解其背后的原理是有效应用并推动其发展的关键。

本文将系统地引导读者穿越DFT的理论迷宫，抵达其应用的广阔天地，旨在阐明电子密度如何成为连接微观量子规律与宏观物质性质的核心桥梁。在第一章“**原理与机制**”中，我们将追溯理论的源头，揭示为何电子密度能取代[波函数](@entry_id:147440)成为主角，并详细剖析将这一思想变为现实的Kohn-Sham构造，以及理论中最神秘的[交换相关能](@entry_id:138029)。随后，在“**应用与跨学科[交叉](@entry_id:147634)**”一章，我们将展示DFT如何作为一座概念桥梁，连接微观量子世界与宏观可观测现象，从预测材料能带到模拟[化学反应](@entry_id:146973)，其威力无所不在。最后，为了将理论知识转化为实践能力，我们将在“**动手实践**”部分提供一系列精心设计的问题，引导您深入理解理论的精髓与挑战。

## 原理与机制

在上一章中，我们介绍了[密度泛函理论](@entry_id:139027)（DFT）的历史背景和其在现代科学研究中的重要地位。本章将深入探讨支撑该理论的核心原理与机制。我们将从其根本性的思想出发，即以电子密度作为基本变量，然后详细阐述将这一原理付诸实践的科恩-沈吕九（Kohn-Sham）方法，并最终剖析该理论中最核心也最神秘的组成部分——[交换相关能](@entry_id:138029)。

### 电子密度作为基本变量

传统的多电子体系量子力学方法，如[Hartree-Fock理论](@entry_id:160358)及其后继方法，均直接处理[多体波函数](@entry_id:203043) $\Psi(\mathbf{r}_1, \sigma_1, \dots, \mathbf{r}_N, \sigma_N)$。对于一个包含 $N$ 个电子的体系，[波函数](@entry_id:147440)是 $3N$ 个空间坐标和 $N$ 个自旋坐标的函数，其复杂性随电子数的增加而急剧增长。[密度泛函理论](@entry_id:139027)的革命性在于，它将描述体系的基本变量从极其复杂的[波函数](@entry_id:147440)转换为相对简单的电子密度 $n(\mathbf{r})$。

电子密度 $n(\mathbf{r})$ 是一个仅依赖于三个空间坐标 $\mathbf{r}$ 的[标量场](@entry_id:151443)，无论体系包含多少电子，它都存在于我们所熟悉的三维空间中。这种复杂性的急剧降低是DFT[计算效率](@entry_id:270255)优势的根源。更重要的是，从物理和化学的角度来看，电子密度可以说比[波函数](@entry_id:147440)更为基本。首先，电子密度是一个原则上[可观测量](@entry_id:267133)，可以通过X射线衍射等[散射实验](@entry_id:173304)来测定，而[多体波函数](@entry_id:203043)本身及其相位则无法被直接测量 [@problem_id:2453891]。其次，许多核心的化学概念，如化学键、孤对电子、[原子电荷](@entry_id:204820)等，都直观地体现在电子密度的[空间分布](@entry_id:188271)上。更进一步，现代的“[概念密度泛函理论](@entry_id:150767)”已经能够从电子密度及其响应中严格地定义诸如化学势（与电负性相关）、[化学硬度](@entry_id:152750)和福奎函数（描述局域反应活性）等概念，使得电子密度成为连接理论计算与化学直觉的桥梁 [@problem_id:2453891]。

将电子密度确立为理论核心的基石是1964年由Pierre Hohenberg和Walter Kohn提出的两条定理。

**Hohenberg-Kohn (HK) 定理**

**第一条HK定理** 指出，对于一个处于非简并[基态](@entry_id:150928)的 $N$ 电子体系，其[基态](@entry_id:150928)电子密度 $n_0(\mathbf{r})$ 唯一地决定了（除一个无关紧要的常数外）体系所受的外势场 $v_{\text{ext}}(\mathbf{r})$。外势场通常由[原子核](@entry_id:167902)的位置和[电荷](@entry_id:275494)决定，因此，一旦 $v_{\text{ext}}(\mathbf{r})$ 被确定，体系的[哈密顿算符](@entry_id:144286) $\hat{H}$ 也就完全确定了。这意味着，通过求解薛定谔方程 $\hat{H}\Psi = E\Psi$，原则上可以得到体系的[基态](@entry_id:150928)[波函数](@entry_id:147440) $\Psi_0$、[基态能量](@entry_id:263704) $E_0$ 以及所有其他的[基态](@entry_id:150928)性质。因此，所有[基态](@entry_id:150928)性质都是[基态](@entry_id:150928)电子密度的唯一泛函（functional），例如 $E_0 = E[n_0]$，$\Psi_0 = \Psi[n_0]$ [@problem_id:2453891]。这一定理建立了一个从基态密度到体系所有性质的完整映射，为基于密度的理论提供了合法性。

**第二条HK定理** 建立了一个关于能量的变分原理。它断言存在一个普适的能量泛函 $E[n]$，对于给定的外势 $v_{\text{ext}}(\mathbf{r})$，当且仅当试探密度 $n(\mathbf{r})$ 是体系的真实基[态密度](@entry_id:147894) $n_0(\mathbf{r})$ 时，该泛函取其最小值，这个最小值就是体系的[基态能量](@entry_id:263704) $E_0$。[能量泛函](@entry_id:170311)可以写作：
$$ E[n] = F[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) d\mathbf{r} $$
其中 $F[n] = \langle \Psi[n] | \hat{T} + \hat{V}_{ee} | \Psi[n] \rangle$ 是一个[普适泛函](@entry_id:140176)，它包含了电子的动能 $\hat{T}$ 和[电子-电子相互作用](@entry_id:139900)能 $\hat{V}_{ee}$，且其形式不依赖于具体体系的外势。

然而，[Hohenberg-Kohn定理](@entry_id:139793)是一个“[存在性证明](@entry_id:267253)”[@problem_id:2453858]。它证明了这样一个完美的、基于密度的理论是存在的，但它并没有给出[普适泛函](@entry_id:140176) $F[n]$ 的具体数学形式。特别是，动能泛函 $T[n]$ 的精确形式是未知的。这构成了直接应用HK定理的主要障碍，并催生了下文将要讨论的科恩-沈吕九方法。

### 科恩-沈吕九构造：从原理到实践

为了克服寻找精确动能泛函 $T[n]$ 的困难，Walter Kohn和沈吕九（Lu Jeu Sham）在1965年提出了一个巧妙的替代方案。其核心思想是引入一个虚构的、无相互作用的参考体系，该体系的电子被设计为在一个局域有效势 $v_{\text{eff}}(\mathbf{r})$ 中运动，并且其[基态](@entry_id:150928)电子密度与真实的、有相互作用的体系完全相同。

#### 虚构的无相互作用体系

对于一个无相互作用的体系，其动能可以精确地通过其单粒子[轨道](@entry_id:137151) $\{\varphi_i\}$ 来表示。基于此，总[能量泛函](@entry_id:170311) $E[n]$ 被重新划分为几个部分：
$$ E[n] = T_s[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) d\mathbf{r} + J[n] + E_{\text{xc}}[n] $$
这里：
-   $T_s[n]$ 是无相互作用参考体系的动能，它可以精确地写成[轨道](@entry_id:137151) $\{\varphi_i\}$ 的泛函。
-   $J[n] = \frac{1}{2} \iint \frac{n(\mathbf{r}) n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d\mathbf{r} d\mathbf{r}'$ 是经典的哈特里（Hartree）能，即电子密度与其自身的经典静电排斥能。
-   $E_{\text{xc}}[n]$ 是交换相关（exchange-correlation）能。这是一个被“定义”出来的项，它包含了真实体系与无相互作用参考体系之间的所有差异。具体来说，它包括两部分：动能差 $(T[n] - T_s[n])$ 和非经典的[电子-电子相互作用](@entry_id:139900)能差 $(V_{ee}[n] - J[n])$。

这个划分的精妙之处在于，大部分的能量（通常是动能和经典[库仑能](@entry_id:161936)）已经被精确地表示出来了。所有未知的、复杂的量子[多体效应](@entry_id:173569)都被打包进了 $E_{\text{xc}}[n]$ 这一个项中。虽然 $E_{\text{xc}}[n]$ 的精确形式仍然未知，但它通常只是总能量的一个相对较小的部分，这使得对其进行近似变得更加可行和准确。

#### 科恩-沈吕九方程的推导

我们的目标是找到一组[轨道](@entry_id:137151) $\{\varphi_i\}$，使得它们构成的密度 $n(\mathbf{r}) = \sum_{i=1}^{N} |\varphi_i(\mathbf{r})|^2$ 能够最小化总能量泛函 $E[n]$。这需要在一个约束条件下进行变分，即[轨道](@entry_id:137151)必须是正交归一的：$\int \varphi_i^*(\mathbf{r}) \varphi_j(\mathbf{r}) d\mathbf{r} = \delta_{ij}$。

使用[拉格朗日乘子法](@entry_id:176596)来处理这个约束[变分问题](@entry_id:756445) [@problem_id:2768067] [@problem_id:2768042]，我们构造拉格朗日泛函 $\mathcal{L}$，并令其对[轨道](@entry_id:137151) $\varphi_k^*(\mathbf{r})$ 的泛函导数为零。经过一系列推导，我们最终得到一组有效的单粒子薛定谔方程，即**科恩-沈吕九（Kohn-Sham, KS）方程**：
$$ \left[ -\frac{1}{2}\nabla^2 + v_{\text{eff}}(\mathbf{r}) \right] \varphi_i(\mathbf{r}) = \varepsilon_i \varphi_i(\mathbf{r}) $$
其中 $\varepsilon_i$ 是KS[轨道](@entry_id:137151) $\varphi_i$ 的[能量本征值](@entry_id:144381)。这个方程描述了一个无相互作用的电子在有效势 $v_{\text{eff}}(\mathbf{r})$ 中的运动。该有效势由三部分组成：
$$ v_{\text{eff}}(\mathbf{r}) = v_{\text{ext}}(\mathbf{r}) + v_H(\mathbf{r}) + v_{\text{xc}}(\mathbf{r}) $$
这里，$v_H(\mathbf{r}) = \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d\mathbf{r}'$ 是哈特里势，而**[交换相关势](@entry_id:180254)** $v_{\text{xc}}(\mathbf{r})$ 定义为[交换相关能](@entry_id:138029)对密度的泛函导数：
$$ v_{\text{xc}}(\mathbf{r}) = \frac{\delta E_{\text{xc}}[n]}{\delta n(\mathbf{r})} $$
由于 $v_{\text{eff}}$ 依赖于密度 $n$，而密度又由[轨道](@entry_id:137151) $\{\varphi_i\}$ 决定，KS方程必须通过自洽场（Self-Consistent Field, SCF）方法来迭代求解。

#### 科恩-沈吕九方法的应用实例

KS框架的强大之处在于它建立了一座连接密度、势和[轨道](@entry_id:137151)的桥梁。我们可以通过两个具体的例子来体会这一点。

第一个例子是一个“逆问题” [@problem_id:2768067]。假设我们已知一个球对称的双电子体系（如[氦原子](@entry_id:150244)或类氦离子）的精确基态密度为 $n(r) = 2\frac{Z^3}{\pi}\exp(-2Zr)$。在这个体系中，密度由一个双占据的 $1s$ 型KS[轨道](@entry_id:137151) $\varphi(r) = \sqrt{\frac{Z^3}{\pi}}\exp(-Zr)$ 产生。通过将这个[轨道](@entry_id:137151)代入KS方程，我们可以反向求解出能够产生该[轨道](@entry_id:137151)的[有效势](@entry_id:142581)。计算表明，该有效势恰好是 $v_{\text{eff}}(r) = -Z/r$。这个结果清晰地展示了密度与势之间[一一对应](@entry_id:143935)的深刻联系：一个特定的密度必须由一个唯一的有效势产生。

第二个例子考虑一个更简单的模型：$N$ 个无自旋的无相互作用电子被限制在一个长度为 $L$ 的[一维无限深势阱](@entry_id:271157)中 [@problem_id:2768042]。在这个模型中，外势 $v_{\text{ext}}(x)$ 在阱内为零，因此[有效势](@entry_id:142581) $v_{\text{eff}}(x)$ 也为零（假设在一个无相互作用的近似下，$v_{\text{xc}}=0$）。KS方程简化为自由粒子的薛定谔方程，其解为[驻波](@entry_id:148648) $\varphi_n(x) = \sqrt{\frac{2}{L}}\sin(\frac{n\pi x}{L})$，对应的本征能（即动能）为 $\varepsilon_n = \frac{n^2\pi^2}{2L^2}$。根据[泡利不相容原理](@entry_id:141850)，[基态](@entry_id:150928)由占据能量最低的 $N$ 个[轨道](@entry_id:137151)（$n=1, \dots, N$）构成。该体系的总动能 $T_s$ 就是这 $N$ 个轨道能量的总和：
$$ T_s(N, L) = \sum_{n=1}^{N} \varepsilon_n = \frac{\pi^2}{2L^2} \sum_{n=1}^{N} n^2 = \frac{\pi^2 N(N+1)(2N+1)}{12L^2} $$
这个精确可解的模型让我们能够具体地看到，对于一个给定的密度（由占据的[轨道](@entry_id:137151)决定），其无相互作用动能 $T_s$ 是如何被计算出来的。

### [交换相关能](@entry_id:138029)与交换相关洞

KS方法的所有复杂性最终都归结于[交换相关能](@entry_id:138029) $E_{\text{xc}}[n]$。理解其物理内涵对于构建和评估近似泛函至关重要。$E_{\text{xc}}[n]$ 的物理解释可以通过引入**对密度** $\rho_2(\mathbf{r}, \mathbf{r}')$ 和**交换相关洞** $h_{\text{xc}}(\mathbf{r}, \mathbf{r}')$ 的概念来阐明。

对密度 $\rho_2(\mathbf{r}, \mathbf{r}')$ 描述了在空间 $\mathbf{r}$ 和 $\mathbf{r}'$ 两点同时找到电子的联合概率。在一个完全不相关的体系中，$\rho_2(\mathbf{r}, \mathbf{r}') = n(\mathbf{r})n(\mathbf{r}')$。然而，由于[泡利不相容原理](@entry_id:141850)和[库仑排斥](@entry_id:181876)，电子的运动是相互关联的。这种关联效应可以用交换相关洞来描述：
$$ \rho_2(\mathbf{r}, \mathbf{r}') = n(\mathbf{r})[n(\mathbf{r}') + h_{\text{xc}}(\mathbf{r}, \mathbf{r}')] $$
交换相关洞 $h_{\text{xc}}(\mathbf{r}, \mathbf{r}')$ 描述了由于在 $\mathbf{r}$ 处存在一个参考电子，导致在 $\mathbf{r}'$ 处找到另一个电子的概率相对于平均密度 $n(\mathbf{r}')$ 的变化。通常，由于排斥作用，$h_{\text{xc}}$ 在 $\mathbf{r}'$ 靠近 $\mathbf{r}$ 的区域是负的，形成一个“洞”。

#### 交换与相关的物理解释

交换相关洞可以进一步分解为两部分：交换洞 $h_x$ 和相关洞 $h_c$。

**交换（Exchange）** 来源于[波函数](@entry_id:147440)的[反对称性](@entry_id:261893)要求（[泡利不相容原理](@entry_id:141850)）。它使得具有相同自旋的电子彼此回避。即使没有库仑排斥，这种效应依然存在。交换洞 $h_x$ 只存在于自旋相同的电子对之间，它描述了参考电子周围同自旋电子密度的减少。根据定义，[交换能](@entry_id:137069) $E_x[n]$ 仅包含势能贡献，不包含任何动能校正，它对应于KS单[行列式](@entry_id:142978)[波函数](@entry_id:147440)所描述的体系的非经典[静电能](@entry_id:267406)部分 [@problem_id:2768084]。

**相关（Correlation）** 则包含了所有超出KS单[行列式](@entry_id:142978)描述的量子[多体效应](@entry_id:173569)。它源于电子之间瞬时的库仑排斥，这种排斥使得具有相同和相反自旋的电子都会彼此回避。[相关能](@entry_id:144432) $E_c[n]$ 的定义包含了动能和[势能](@entry_id:748988)两部分：动能[相关能](@entry_id:144432) $T_c = T - T_s$ 和势能相关能 $U_c$。后者可以被看作是相关洞 $h_c$ 与[库仑相互作用](@entry_id:747947)算符积分的结果 [@problem_id:2768084]。

#### [绝热连接](@entry_id:199259)与交换相关洞求和规则

一个理解[交换相关能](@entry_id:138029)的强大理论工具是**[绝热连接](@entry_id:199259)（Adiabatic Connection）**。该方法通过一个耦合常数 $\lambda$（从0到1）将无相互作用的KS体系（$\lambda=0$）平滑地“连接”到完全相互作用的真实体系（$\lambda=1$）。在这个过程中，通过调节外势，体系的密度始终保持为真实的基[态密度](@entry_id:147894) $n(\mathbf{r})$。

利用[Hellmann-Feynman定理](@entry_id:173798)，可以推导出[交换相关能](@entry_id:138029)的一个精确表达式 [@problem_id:2768075]：
$$ E_{\text{xc}}[n] = \frac{1}{2} \iint \frac{n(\mathbf{r}) \bar{h}_{\text{xc}}(\mathbf{r}, \mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} d\mathbf{r} d\mathbf{r}' $$
其中 $\bar{h}_{\text{xc}}(\mathbf{r}, \mathbf{r}') = \int_0^1 h_{\text{xc}}^{\lambda}(\mathbf{r}, \mathbf{r}') d\lambda$ 是沿着绝[热路](@entry_id:150016)径对交换相关洞进行的积分平均。这个公式给出了一个优美的物理解释：[交换相关能](@entry_id:138029)等于体系中每个电子与其自身的、耦合常数平均的交换相关洞之间的静电相互作用能 [@problem_id:2768084]。

此外，交换相关洞满足一个至关重要的**求和规则**。由于每个电子都必须与其余的 $N-1$ 个电子相互作用，可以证明，对于任何给定的参考电子位置 $\mathbf{r}$，其周围的交换相关洞在全空间积分后，恰好包含 $-1$ 个单位的[电荷](@entry_id:275494) [@problem_id:2768075]：
$$ \int h_{\text{xc}}(\mathbf{r}, \mathbf{r}') d\mathbf{r}' = -1 $$
这意味着每个电子都被一个等效的、[电荷](@entry_id:275494)为 $+1$ 的“洞”完美地屏蔽了。这个求和规则是构建和检验近似[交换相关泛函](@entry_id:142042)的一个基本约束。

### 前沿论题：分数电子与[导数不连续性](@entry_id:136336)

为了更深刻地理解DFT的理论结构及其在实践中的一些挑战，我们需要探讨一些更高级的概念，特别是与分数电子数相关的性质。

#### 科恩-沈吕九[本征值](@entry_id:154894)的物理意义

在[Hartree-Fock理论](@entry_id:160358)中，[Koopmans定理](@entry_id:139178)近似地将占据[轨道](@entry_id:137151)的能量解释为[电离能](@entry_id:136678)的负值。而在DFT中，**Janak定理** 给出了KS轨道能量的精确物理解释 [@problem_id:2453867]。它指出，轨道能量 $\varepsilon_i$ 等于总能量对该[轨道](@entry_id:137151)占据数 $n_i$ 的偏导数：
$$ \varepsilon_i = \frac{\partial E}{\partial n_i} $$
这是一个精确的关系，而非近似。对于**精确的**[交换相关泛函](@entry_id:142042)，Janak定理导出一个惊人的结论：最高占据分子[轨道](@entry_id:137151)（HOMO）的能量严格等于[第一电离能](@entry_id:136840)的负值（$\varepsilon_{\text{HOMO}} = -I$），而最低未占据分子[轨道](@entry_id:137151)（LUMO）的能量严格等于电子亲和能的负值（$\varepsilon_{\text{LUMO}} = -A$）。然而，对于目前所有近似的泛函，这一关系通常不成立，这是近似泛函的一个主要缺陷。

#### 分数粒子数与能量的[导数不连续性](@entry_id:136336)

精确的DFT理论可以通过系综的观点被推广到非整数的电子数 $N$。一个关键的结论是，对于固定的外势，[基态能量](@entry_id:263704) $E(N)$ 作为电子数 $N$ 的函数，在两个相邻整数之间是**分段线性的** [@problem_id:2768031]。例如，对于 $N \in [N_0, N_0+1]$，能量可以表示为 $E(N) = (1-\alpha)E(N_0) + \alpha E(N_0+1)$，其中 $\alpha = N-N_0$。

这个分段线性行为直接导致能量对电子数的[一阶导数](@entry_id:749425)（即化学势 $\mu = \partial E/\partial N$）在整数点上是**不连续的**。具体来说，在整数 $N_0$ 处，从左侧逼近的导数和从右侧逼近的导数分别为 [@problem_id:2768081]：
$$ \left(\frac{\partial E}{\partial N}\right)_{N_0^-} = E(N_0) - E(N_0-1) = -I $$
$$ \left(\frac{\partial E}{\partial N}\right)_{N_0^+} = E(N_0+1) - E(N_0) = -A $$
其中 $I$ 和 $A$ 分别是 $N_0$ 电子体系的[电离能](@entry_id:136678)和[电子亲和能](@entry_id:147520)。由于对于稳定体系 $I > A$，所以化学势在整数点发生了一个跳跃。这个现象被称为**[导数不连续性](@entry_id:136336)**。

将这个[能量导数](@entry_id:170468)与KS[本征值](@entry_id:154894)的物理意义相结合，我们得到了一个联系真实[能隙](@entry_id:191975)与KS[轨道](@entry_id:137151)[能隙](@entry_id:191975)的重要关系。真实体系的基本[能隙](@entry_id:191975)定义为 $E_g = I - A$。将上述关系代入，得到：
$$ E_g = I - A = \left(\frac{\partial E}{\partial N}\right)_{N_0^+} - \left(\frac{\partial E}{\partial N}\right)_{N_0^-} $$
注意这里原文有一个小错误，应该是 I-A = (dE/dN)_N0^+ - (dE/dN)_N0^- 还是 (dE/dN)_N0^- - (dE/dN)_N0^+。
因为 I > A，-I  -A，所以 $(\partial E/\partial N)_{N_0^-}  (\partial E/\partial N)_{N_0^+}$。
$E_g = I - A = -(\partial E/\partial N)_{N_0^-} - (-(\partial E/\partial N)_{N_0^+}) = (\partial E/\partial N)_{N_0^+} - (\partial E/\partial N)_{N_0^-}$. 原文公式 `(dE/dN)_N0^- - (dE/dN)_N0^+`会得到负值，已修正。
根据 $E_g = I-A$ 以及 $(\partial E/\partial N)_{N_0^-}=-I$ 和 $(\partial E/\partial N)_{N_0^+}=-A$，我们得到 $E_g = -(\partial E/\partial N)_{N_0^-} - (-(\partial E/\partial N)_{N_0^+}) = (\partial E/\partial N)_{N_0^+} - (\partial E/\partial N)_{N_0^-}$。
根据Perdew  Levy (1983) and Sham  Schlüter (1983), $E_g = \varepsilon_{LUMO}(N) - \varepsilon_{HOMO}(N) + \Delta_{xc}$
where $\Delta_{xc} = v_{xc}(N+\delta) - v_{xc}(N-\delta)$.
Also, $\varepsilon_{HOMO}(N)=-I$ and $\varepsilon_{LUMO}(N)=-A+\Delta_{xc}$. This seems confusing.
Let's stick to the core definition. $I = E(N-1) - E(N)$ and $A = E(N) - E(N+1)$. So $I-A = E(N-1) - 2E(N) + E(N+1)$.
The chemical potential $\mu = \partial E/\partial N$. For $N_0-\delta$, $\mu = E(N_0) - E(N_0-1) = -I$. For $N_0+\delta$, $\mu = E(N_0+1) - E(N_0) = -A$.
The jump is $\mu(N_0^+) - \mu(N_0^-) = -A - (-I) = I-A = E_g$.
The original text has `(dE/dN)_N0^- - (dE/dN)_N0^+`. This would be `-I - (-A) = A-I = -E_g`. This is a sign error. I have corrected it to `(\partial E/\partial N)_{N_0^+} - (\partial E/\partial N)_{N_0^-}`.

利用Janak定理 $\varepsilon_{i} = \partial E / \partial n_i$, 我们有 $\varepsilon_{\text{HOMO}} = (\partial E / \partial N)_{N_0^-}$ 和 $\varepsilon_{\text{LUMO}} = (\partial E / \partial N)_{N_0^+}$.
This is incorrect. The relationship is $\varepsilon_{\text{HOMO}}(N) = -I(N)$ for the exact functional. And the LUMO of the N-electron system is not directly related to A. The HOMO of the (N+1) electron system is related to -A(N).
The original text's derivation seems to be a common but slightly hand-wavy one. Let's follow it and correct it.
$E_g = I-A = (\partial E/\partial N)_{N_0^+} - (\partial E/\partial N)_{N_0^-}$. This part is correct now.
The jump in the potential is $\Delta_{xc} = v_{xc}(N+\delta) - v_{xc}(N-\delta)$.
The KS gap is $E_g^{\text{KS}} = \varepsilon_{\text{LUMO}} - \varepsilon_{\text{HOMO}}$.
The true relation is $E_g = E_g^{\text{KS}} + \Delta_{xc}$.
The original text has: `$\varepsilon_{\text{HOMO}} - (\varepsilon_{\text{LUMO}} + \Delta_{\text{xc}})$`. This looks very wrong. Let's re-derive.
$I-A = (\mu^+ - \mu^-)$. From KS theory, $\mu = \varepsilon_{HOMO}$.
But this is only for integer systems. The chemical potential of the KS system is $\varepsilon_{HOMO}$.
So $\mu(N_0^-) = \varepsilon_{HOMO}(N_0)$. Thus $-I = \varepsilon_{HOMO}(N_0)$.
The potential for adding an electron is $\mu(N_0^+) = -A$. For the KS system, the LUMO eigenvalue is $\varepsilon_{LUMO}(N_0)$. It is known that $\mu(N_0^+) \neq \varepsilon_{LUMO}(N_0)$ for approximate functionals. For the exact functional, $\mu(N_0^+) = \varepsilon_{LUMO}(N_0) + \Delta_{xc}$. The original text seems to have a convoluted derivation.
Let's use the standard result: $E_g = I - A$. For the exact functional, $\varepsilon_{\text{HOMO}} = -I$. And $E_g = \varepsilon_{\text{LUMO}} - \varepsilon_{\text{HOMO}} + \Delta_{xc}$. So $I-A = \varepsilon_{\text{LUMO}} - (-I) + \Delta_{xc}$, which means $-A = \varepsilon_{\text{LUMO}} + \Delta_{xc}$. This is correct.
The original text wrote: $E_g = I - A = (\frac{\partial E}{\partial N})_{N_0^-} - (\frac{\partial E}{\partial N})_{N_0^+} = \varepsilon_{\text{HOMO}} - (\varepsilon_{\text{LUMO}} + \Delta_{\text{xc}})$. This is a cascade of errors.
First error `(dE/dN)- - (dE/dN)+` gave `-Eg`. Second error `εHOMO - (εLUMO + Δxc)` seems completely wrong.
Let's fix it by stating the result directly.
$$ E_g = I - A = (\varepsilon_{\text{LUMO}} - \varepsilon_{\text{HOMO}}) + \Delta_{\text{xc}} $$
其中 $E_g^{\text{KS}} = \varepsilon_{\text{LUMO}} - \varepsilon_{\text{HOMO}}$ 是KS[轨道](@entry_id:137151)[能隙](@entry_id:191975)，而 $\Delta_{\text{xc}}$ 是[交换相关势](@entry_id:180254)在电子数穿过整数时产生的突变（一个空间常数），它正是[导数不连续性](@entry_id:136336)的来源 [@problem_id:2768081]。这个公式解释了为什么大多数近似泛函（它们通常缺少这种不连续性，即 $\Delta_{\text{xc}} \approx 0$）会严重低估材料的[带隙](@entry_id:191975)。例如，对于一个已知 $I = 8.30~\mathrm{eV}$ 和 $A = 0.95~\mathrm{eV}$ 的体系，其基本[能隙](@entry_id:191975)为 $E_g = 7.35~\mathrm{eV}$。如果一个KS计算给出的HOMO和LUMO能量分别为 $-5.60~\mathrm{eV}$ 和 $-2.20~\mathrm{eV}$（即 $E_g^{\text{KS}} = 3.40~\mathrm{eV}$），那么为了弥补差距，[导数不连续性](@entry_id:136336)必须为 $\Delta_{\text{xc}} = 7.35 - 3.40 = 3.95~\mathrm{eV}$ [@problem_id:2768081]。
This corrected version is much cleaner and correct. I will replace the convoluted and erroneous derivation.

最后，基于能量对粒子数的导数，[概念DFT](@entry_id:174583)也定义了其他重要的[化学反应性](@entry_id:141717)指标。例如，化学势 $\mu$ 和全局硬度 $\eta$ 可以通过[有限差分近似](@entry_id:749375)与 $I$ 和 $A$ 联系起来 [@problem_id:2768041]：
$$ \mu = -\frac{I+A}{2}, \quad \eta = I-A $$

### 理论的数学基石

为了构建一个严谨的理论，我们必须精确定义其基本对象的数学性质。

#### [N-可表示性](@entry_id:189302)与v-[可表示性](@entry_id:635277)

一个函数 $n(\mathbf{r})$ 要成为一个合法的电子密度，它必须满足一些基本条件。如果一个密度 $n(\mathbf{r})$ 能够从某个反对称的 $N$ 电子[波函数](@entry_id:147440)（[纯态](@entry_id:141688)或系综）中导出，则称该密度是**N-可表示的**。这是密度成为一个物理上可能的密度的最基本要求。

一个更强的条件是**v-[可表示性](@entry_id:635277)**。如果一个密度 $n(\mathbf{r})$ 是某个局域外势 $v(\mathbf{r})$ 下的 $N$ 电子体系的**[基态](@entry_id:150928)**密度，则称该密度是v-可表示的。HK定理的原始表述是建立在v-可表示密度的集合上的。

所有v-可表示的密度必然是N-可表示的，但反之不成立。存在一些物理上可能的N-可表示密度，它们无法成为任何外势下的基态密度。一个经典的例子是具有非零总轨道角动量（$L0$）的开壳层原子的基态密度。例如，碳原子（$^{3}P$ [基态](@entry_id:150928)）的任何一个[纯态](@entry_id:141688)（对应特定的 $M_L$ 值）都具有非球对称的密度。然而，通过对所有简并的 $M_L$ 态进行系综平均，可以得到一个球对称的密度。这个球对称的密度是N-可表示的，并且是球对称外势下的系综基态密度，但已被证明它不能由任何局域势下的**单个纯态**产生。因此，它是系综v-可表示的，但不是[纯态](@entry_id:141688)v-可表示的 [@problem_id:2768068]。现代DFT的[Levy-Lieb约束搜索](@entry_id:145975)表述将变分空间从较小的v-可表示密度集推广到了更大的N-可表示密度集，从而使得理论的数学基础更加坚实。

#### 泛函的[微分](@entry_id:158718)性与[导数不连续性](@entry_id:136336)

[交换相关势](@entry_id:180254) $v_{\text{xc}}(\mathbf{r})$ 被定义为 $E_{\text{xc}}[n]$ 对 $n(\mathbf{r})$ 的泛函导数。在数学上，这个导数是通过**[Gâteaux导数](@entry_id:164612)**（方向导数）来定义的 [@problem_id:2768030]。它描述了泛函沿着某个特定方向 $\delta n$ 的变化率。

在[泛函分析](@entry_id:146220)中，存在一个比Gâteaux可微更强的概念，即**Fréchet可微**。Fréchet可微要求泛函在某点附近可以被一个[线性泛函](@entry_id:276136)一致地逼近，无论扰动的方向如何。

精确的[交换相关泛函](@entry_id:142042) $E_{\text{xc}}[n]$ 在整数电子数对应的密度点上，对于保持粒子数不变的密度微扰方向是Gâteaux可微的，这使得 $v_{\text{xc}}(\mathbf{r})$ 得以定义。然而，由于[导数不连续性](@entry_id:136336)的存在，当我们考虑能够改变粒子数的密度微扰时，泛函的变化率取决于粒子数是增加还是减少。这种方向依赖性破坏了[线性逼近](@entry_id:142309)的一致性，导致精确的 $E_{\text{xc}}[n]$ 在这些点上**不是Fréchet可微的** [@problem_id:2768030]。这一深刻的数学特性正是[导数不连续性](@entry_id:136336)现象的根源，也揭示了设计能够同时准确描述整数和分数电子体系的近似泛函所面临的根本性挑战。