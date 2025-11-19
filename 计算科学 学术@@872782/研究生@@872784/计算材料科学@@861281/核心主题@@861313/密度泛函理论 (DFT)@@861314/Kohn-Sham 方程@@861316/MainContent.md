## 引言
在现代计算科学领域，密度泛函理论（DFT）无疑是一场革命，它使得从第一性原理出发预测和理解物质性质成为可能。而这场革命的核心，正是精巧而强大的科恩-沈（Kohn-Sham）方程。它为处理困扰物理学家和化学家数十年的多电子相互作用问题提供了一条优雅且切实可行的路径。

尽管[Hohenberg-Kohn定理](@entry_id:139793)从理论上证明了电子密度是描述系统[基态](@entry_id:150928)性质的基本变量，但它并未给出如何利用密度计算关键物理量——尤其是动能——的具体方案。[科恩-沈方程](@entry_id:143968)的提出巧妙地绕过了这一障碍，它将真实相互作用体系的问题映射到一个虚拟的、更易于处理的无相互作用体系上，从而将计算的核心挑战转移到了对一个被称为“交换关联能”的项进行近似上。这种方法论上的突破，为DFT的广泛应用铺平了道路。

本文旨在系统性地剖析[科恩-沈方程](@entry_id:143968)的理论框架与实践应用。在“原理与机制”一章中，我们将追溯其理论源头，详细推导方程的数学形式，并深入探讨交换关联能的物理内涵以及求解方程的[自洽场方法](@entry_id:184373)。随后，在“应用与跨学科联系”一章中，我们将展示[科恩-沈方程](@entry_id:143968)如何在[材料科学](@entry_id:152226)、化学、[核物理](@entry_id:136661)等多个领域大放异彩，揭示其作为连接不同学科的普适性工具的强大能力。最后，“动手实践”部分将通过一系列精心设计的问题，帮助读者巩固理论知识，亲身体验DFT计算中的核心挑战与解决方案。通过这趟旅程，读者将对这一现代计算科学的基石建立起深刻而全面的理解。

## 原理与机制

继前一章对[密度泛函理论](@entry_id:139027) (DFT) 的背景和意义进行了总体介绍之后，本章将深入探讨其核心——Kohn-Sham (KS) 方程——的理论基础和工作机制。我们将从其赖以建立的 Hohenberg-Kohn 定理出发，系统地阐述 Kohn-Sham 方法的巧妙构思、核心方程的推导，以及交换关联能这一关键概念的内涵。此外，我们还将讨论如何通过[自洽场方法](@entry_id:184373)在实践中求解这些方程，并探讨一些深化我们理解的理论前沿问题，如 [V-可表示性](@entry_id:143721)和[导数不连续性](@entry_id:136336)。

### [密度泛函理论](@entry_id:139027)的基石：Hohenberg-Kohn 定理

[密度泛函理论](@entry_id:139027)的现代形式建立在 Walter Kohn 和 Pierre Hohenberg 于 1964 年提出的两个基本定理之上。这些定理为使用电子密度 $n(\mathbf{r})$ 作为基本变量来描述多电子体系的[基态](@entry_id:150928)性质提供了严格的理论依据。

第一个 Hohenberg-Kohn (HK) 定理确立了[基态](@entry_id:150928)电子密度 $n(\mathbf{r})$ 与系统外势 $v_{\mathrm{ext}}(\mathbf{r})$ 之间存在的[一一对应](@entry_id:143935)关系。具体而言，对于一个粒子数 $N$ 固定的相互作用电子体系，其[基态](@entry_id:150928)电子密度 $n(\mathbf{r})$ 可以唯一地确定（最多相差一个无关紧要的常数）产生该密度的外势 $v_{\mathrm{ext}}(\mathbf{r})$。由于外势 $v_{\mathrm{ext}}(\mathbf{r})$ 和粒子数 $N$ 完全定义了体系的[哈密顿算符](@entry_id:144286)，因此，基态密度也唯一地决定了体系的[基态](@entry_id:150928)[波函数](@entry_id:147440)以及所有[基态](@entry_id:150928)[可观测量](@entry_id:267133)。

这个定理的证明异常简洁而深刻，它采用的是一种基于[瑞利-里兹变分原理](@entry_id:185834)的[归谬法](@entry_id:276604) [@problem_id:3493888]。假设存在两个不同的外势 $v_{\mathrm{ext}}(\mathbf{r})$ 和 $v'_{\mathrm{ext}}(\mathbf{r})$，它们之间的差不为一个常数。这两个外势分别对应于[哈密顿算符](@entry_id:144286) $\hat{H}$ 和 $\hat{H}'$，以及非简并的[基态](@entry_id:150928)[波函数](@entry_id:147440) $\Psi$ 和 $\Psi'$。我们假设这两个不同的系统“偶然”地具有完全相同的基态密度 $n(\mathbf{r})$。

根据变分原理，将 $\Psi'$ 作为体系 $\hat{H}$ 的一个[试探波函数](@entry_id:142892)，其[能量期望值](@entry_id:174035)必然严格大于 $\hat{H}$ 的基态能量 $E_0$：
$$
E_0  \langle \Psi' | \hat{H} | \Psi' \rangle = \langle \Psi' | \hat{H}' - \hat{V}'_{\mathrm{ext}} + \hat{V}_{\mathrm{ext}} | \Psi' \rangle = E'_0 + \int n(\mathbf{r}) [v_{\mathrm{ext}}(\mathbf{r}) - v'_{\mathrm{ext}}(\mathbf{r})] \,d\mathbf{r}
$$
其中 $E'_0$ 是 $\hat{H}'$ 的基态能量。

对称地，将 $\Psi$ 作为体系 $\hat{H}'$ 的试探波函数，我们同样得到：
$$
E'_0  \langle \Psi | \hat{H}' | \Psi \rangle = \langle \Psi | \hat{H} - \hat{V}_{\mathrm{ext}} + \hat{V}'_{\mathrm{ext}} | \Psi \rangle = E_0 + \int n(\mathbf{r}) [v'_{\mathrm{ext}}(\mathbf{r}) - v_{\mathrm{ext}}(\mathbf{r})] \,d\mathbf{r}
$$

将这两个不等式相加，得到 $E_0 + E'_0  E'_0 + E_0$，这是一个明显的逻辑矛盾。因此，最初的假设——两个不同的外势可以产生相同的基[态密度](@entry_id:147894)——必然是错误的。这便证明了从基[态密度](@entry_id:147894) $n(\mathbf{r})$ 到外势 $v_{\mathrm{ext}}(\mathbf{r})$ 的映射是唯一的（除去一个常数）。需要强调的是，这一证明的严格性依赖于一些前提条件，例如[基态](@entry_id:150928)的非简并性。对于简并[基态](@entry_id:150928)，需要引入系综理论进行更复杂的论证，但结论依然成立 [@problem_id:3493942]。

第二个 Hohenberg-Kohn 定理提出了一个关于能量的变分原理。它指出，对于一个给定的外势 $v_{\mathrm{ext}}(\mathbf{r})$，存在一个[能量泛函](@entry_id:170311) $E[n]$，当且仅当将真实的基态密度 $n_0(\mathbf{r})$ 代入该泛函时，泛函的取值达到其最小值，即体系的基态能量 $E_0$。这个[能量泛函](@entry_id:170311)可以写成：
$$
E[n] = F_{\mathrm{HK}}[n] + \int n(\mathbf{r}) v_{\mathrm{ext}}(\mathbf{r}) \,d\mathbf{r}
$$
其中，与外势无关的部分 $F_{\mathrm{HK}}[n] = T[n] + E_{\mathrm{ee}}[n]$ 被称为 **Hohenberg-Kohn 泛函**。它包含了相互作用体系的动能 $T[n]$ 和[电子-电子相互作用](@entry_id:139900)能 $E_{\mathrm{ee}}[n]$。$F_{\mathrm{HK}}[n]$ 是一个**[普适泛函](@entry_id:140176)**，意味着它对于任何具有相同相互作用形式的 $N$ 电子体系都具有相同的数学形式，不依赖于具体的[原子核](@entry_id:167902)位置或外场。

然而，HK 定理虽然在理论上奠定了 DFT 的基础，却并未给出[普适泛函](@entry_id:140176) $F_{\mathrm{HK}}[n]$ 的具体形式。特别是，相互作用体系的动能泛函 $T[n]$ 的精确形式是未知的，而且直接对其进行精确近似也极为困难。这构成了早期 DFT 发展的主要障碍，直到 Kohn-Sham 方法的出现。

### Kohn-Sham 方法：一个巧妙的构造

1965 年，Walter Kohn 和 Lu Jeu Sham 提出了一种革命性的方法，巧妙地绕过了直接求解未知动能泛函 $T[n]$ 的难题。其核心思想是引入一个虚拟的、无相互作用的辅助体系，并要求这个 **Kohn-Sham (KS) 体系** 的[基态](@entry_id:150928)电子密度与我们关心的真实相互作用体系的基态密度完全相同。

由于 KS 体系是无相互作用的，其[基态](@entry_id:150928)[波函数](@entry_id:147440)可以精确地表示为一个由单粒子[轨道](@entry_id:137151) $\{\phi_i\}$ 构成的[斯莱特行列式](@entry_id:139034)。因此，该体系的动能 $T_s[n]$ 就可以通过这些[轨道](@entry_id:137151)精确地计算出来：
$$
T_s[n] = -\frac{1}{2} \sum_{i=1}^{N} \int \phi_i^*(\mathbf{r}) \nabla^2 \phi_i(\mathbf{r}) \,d\mathbf{r}
$$
其中密度 $n(\mathbf{r}) = \sum_{i=1}^N |\phi_i(\mathbf{r})|^2$。

有了这个精确已知的无相互作用动能 $T_s[n]$，Kohn 和 Sham 对真实体系的总[能量泛函](@entry_id:170311)进行了重新划分 [@problem_id:3493895] [@problem_id:3493892]。他们首先从总能量中分离出 $T_s[n]$，并将真实动能与它的差值藏入一个新定义的项中。然后，他们从总的[电子-电子相互作用](@entry_id:139900)能 $E_{\mathrm{ee}}[n]$ 中分离出经典[静电排斥](@entry_id:162128)能，即 **Hartree 能** $E_{\mathrm{H}}[n]$，这部分能量可以根据密度直接写出：
$$
E_{\mathrm{H}}[n] = \frac{1}{2} \iint \frac{n(\mathbf{r})n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} \,d\mathbf{r}d\mathbf{r}'
$$

经过这样的重新组合，总[能量泛函](@entry_id:170311)被精确地写为：
$$
E[n] = T_s[n] + E_{\mathrm{H}}[n] + E_{\mathrm{xc}}[n] + \int n(\mathbf{r}) v_{\mathrm{ext}}(\mathbf{r}) \,d\mathbf{r}
$$

所有复杂的、未知的[多体效应](@entry_id:173569)都被“打包”进了一个新的泛函——**交换关联能** ($E_{\mathrm{xc}}[n]$) 中。根据定义，它包含了以下所有部分：
$$
E_{\mathrm{xc}}[n] \equiv (T[n] - T_s[n]) + (E_{\mathrm{ee}}[n] - E_{\mathrm{H}}[n])
$$
这个定义揭示了 $E_{\mathrm{xc}}[n]$ 深刻的物理内涵 [@problem_id:3493892]：
1.  **动能相关** ($T_c[n] = T[n] - T_s[n]$): 这是真实相互作用体系的动能与无相互作用 KS 体系动能之间的差值。它反映了电子由于[库仑相互作用](@entry_id:747947)而彼此回避，导致其运动状态改变，从而对动能产生的修正。
2.  **[交换能](@entry_id:137069)** ($E_x[n]$): 这是源于[波函数反对称性](@entry_id:152377)的纯量子效应，即[泡利不相容原理](@entry_id:141850)。它描述了自旋相同的电子之间的有效排斥。
3.  **势能相关** ($E_c^{\mathrm{pot}}[n]$): 这是[电子-电子相互作用](@entry_id:139900)能中，除去经典 Hartree 能和交换能之外的剩余部分。它描述了电子运动的动态关联。

此外，Hartree 能包含了一个虚假的电子与自身相互作用的项 (self-interaction)。精确的交换关联泛函必须能够精确地抵消掉这个自相互作用。例如，对于任何单电子体系，其 $E_{\mathrm{ee}}[n]=0$，因此精确的泛函必须满足 $E_{\mathrm{H}}[n] + E_{\mathrm{xc}}[n] = 0$。

Kohn-Sham 方法的绝妙之处在于，尽管 $E_{\mathrm{xc}}[n]$ 的精确形式仍然是未知的，但它通常只占总能量的一小部分。更重要的是，动能的主要部分 ($T_s[n]$) 已经被精确处理，使得对 $E_{\mathrm{xc}}[n]$ 的近似变得更加可行和有效。整个 DFT 的现代应用都建立在寻找和发展对 $E_{\mathrm{xc}}[n]$ 的精确近似之上。

### Kohn-Sham 方程的推导与应用

在 Kohn-Sham 的框架下，我们的任务是通过变分法求解使总能量 $E[n]$ 最小化的那组正交归一的[轨道](@entry_id:137151) $\{\phi_i\}$。我们将总能量视为[轨道](@entry_id:137151)的泛函，并引入拉格朗日乘子 $\varepsilon_{ij}$ 来处理[轨道](@entry_id:137151)间的正交归一约束条件 $\int \phi_i^*(\mathbf{r}) \phi_j(\mathbf{r}) \,d\mathbf{r} = \delta_{ij}$ [@problem_id:2768067]。

构造拉格朗日泛函 $\mathcal{L}$ 并使其对 $\phi_k^*(\mathbf{r})$ 的泛函导数为零，经过一系列推导，我们可以得到一组耦合的单粒子方程。通过对[轨道](@entry_id:137151)进行适当的[酉变换](@entry_id:152599)，这组方程可以被对角化，最终得到一组形式上类似于单[电子薛定谔方程](@entry_id:177999)的规范方程，这就是著名的 **Kohn-Sham 方程**：
$$
\left[ -\frac{1}{2}\nabla^2 + v_{\mathrm{eff}}(\mathbf{r}) \right] \phi_i(\mathbf{r}) = \varepsilon_i \phi_i(\mathbf{r})
$$
其中 $\varepsilon_i$ 是 KS [轨道能量](@entry_id:158481)。方程中的 **有效势** $v_{\mathrm{eff}}(\mathbf{r})$ 是一个局域的[单体](@entry_id:136559)势，由三部分组成：
$$
v_{\mathrm{eff}}(\mathbf{r}) = v_{\mathrm{ext}}(\mathbf{r}) + v_{\mathrm{H}}(\mathbf{r}) + v_{\mathrm{xc}}(\mathbf{r})
$$
这里，$v_{\mathrm{H}}(\mathbf{r}) = \frac{\delta E_{\mathrm{H}}[n]}{\delta n(\mathbf{r})} = \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} \,d\mathbf{r}'$ 是 Hartree 势，而 $v_{\mathrm{xc}}(\mathbf{r}) = \frac{\delta E_{\mathrm{xc}}[n]}{\delta n(\mathbf{r})}$ 是交换关联势。

KS 方程的结构揭示了其内在的[自洽性](@entry_id:160889)：[有效势](@entry_id:142581) $v_{\mathrm{eff}}$ 依赖于电子密度 $n(\mathbf{r})$，而电子密度又是由 KS 方程的解——[轨道](@entry_id:137151) $\{\phi_i\}$ ——所决定的。这意味着我们无法直接求解 KS 方程，而必须采用迭代的[自洽场方法](@entry_id:184373)。

为了更具体地理解密度与[有效势](@entry_id:142581)之间的关系，我们可以考虑一个简单的[逆问题](@entry_id:143129) [@problem_id:2768067]。假设我们已知一个自旋非极化的双电子球对称体系的基态密度为 $n(r) = 2 \frac{Z^3}{\pi} \exp(-2Zr)$。这对应于一个被双电子占据的[轨道](@entry_id:137151) $\phi(r) = \sqrt{n(r)/2} = \sqrt{Z^3/\pi} \exp(-Zr)$。我们可以通过反转 KS 方程来求解产生该[轨道](@entry_id:137151)的[有效势](@entry_id:142581)：
$$
v_{\mathrm{eff}}(r) = \varepsilon + \frac{\frac{1}{2}\nabla^2 \phi(r)}{\phi(r)}
$$
通过计算球坐标下的拉普拉斯算子 $\nabla^2 \phi(r)$，我们发现 $\nabla^2 \phi(r) = (Z^2 - 2Z/r)\phi(r)$。代入上式得到 $v_{\mathrm{eff}}(r) = \varepsilon + \frac{Z^2}{2} - \frac{Z}{r}$。如果我们施加物理边界条件，要求势在无穷远处为零，即 $v_{\mathrm{eff}}(r \to \infty) \to 0$，则可以确定 $\varepsilon = -Z^2/2$。最终，我们得到了一个惊人地简洁的结果：$v_{\mathrm{eff}}(r) = -Z/r$。这表明，要在一个无相互作用的体系中产生一个[类氢原子](@entry_id:164890) $1s$ [轨道](@entry_id:137151)的密度[分布](@entry_id:182848)，所需要的[有效势](@entry_id:142581)恰好就是核[电荷](@entry_id:275494)为 $Z$ 的[库仑势](@entry_id:154276)。这个例子清晰地展示了密度与有效势之间存在的直接而深刻的联系。

### 实践中的 Kohn-Sham 方法

理论的优雅需要转化为计算的可行性。这主要涉及两个方面：对未知的交换关联能 $E_{\mathrm{xc}}[n]$ 进行近似，以及设计有效的算法求解自洽的 KS 方程。

#### [局域密度近似](@entry_id:138982) (Local Density Approximation, LDA)

最简单也最具历史意义的近似是**[局域密度近似](@entry_id:138982) (LDA)**。[LDA](@entry_id:138982) 的核心思想是，在空间中每一点 $\mathbf{r}$ 的交换关联能密度，可以近似为具有相同电子密度 $n(\mathbf{r})$ 的[均匀电子气](@entry_id:163911) (Uniform Electron Gas, UEG) 的交换关联能密度。总的交换关联能就是对整个空间进行积分：
$$
E_{\mathrm{xc}}^{\mathrm{LDA}}[n] = \int n(\mathbf{r}) \varepsilon_{\mathrm{xc}}^{\mathrm{unif}}(n(\mathbf{r})) \,d\mathbf{r}
$$
其中 $\varepsilon_{\mathrm{xc}}^{\mathrm{unif}}(n)$ 是[均匀电子气](@entry_id:163911)中每个粒子的交换关联能，它是密度 $n$ 的函数。

$\varepsilon_{\mathrm{xc}}^{\mathrm{unif}}(n)$ 可以分为交换部分 $\varepsilon_{\mathrm{x}}^{\mathrm{unif}}(n)$ 和相关部分 $\varepsilon_{\mathrm{c}}^{\mathrm{unif}}(n)$。交换部分可以通过对填充了平面波[轨道](@entry_id:137151)的 Slater [行列式](@entry_id:142978)进行 Hartree-Fock 计算而得到解析解 [@problem_id:3493933]：
$$
\varepsilon_{\mathrm{x}}^{\mathrm{unif}}(n) = -\frac{3}{4}\left(\frac{3}{\pi}\right)^{1/3} n^{1/3}
$$
相关部分 $\varepsilon_{\mathrm{c}}^{\mathrm{unif}}(n)$ 没有简单的解析形式，但可以通过高精度的[量子蒙特卡洛](@entry_id:144383)模拟进行数值计算，并拟合成不同密度范围下的[解析函数](@entry_id:139584)。例如，在高密度极限下，其形式为 $\varepsilon_c(n) = A \ln r_s + B$，其中 $r_s = (3/4\pi n)^{1/3}$ 是 Wigner-Seitz 半径。尽管 [LDA](@entry_id:138982) 非常简单，它在描述固体结合能、[晶格常数](@entry_id:158935)等方面取得了惊人的成功，为 DFT 的广泛应用奠定了基础。

#### 自洽场 (Self-Consistent Field, SCF) 循环

由于 KS 方程的解依赖于其自身的[势场](@entry_id:143025)，求解过程必须迭代进行，直至达到自洽，这一过程被称为**[自洽场 (SCF)](@entry_id:136511) 循环** [@problem_id:3493899]。一个典型的 SCF 循环步骤如下：
1.  **初始猜测**：从一个初始的电子密度 $n^{(0)}(\mathbf{r})$ 出发（例如，由重叠的原子密度构成）。
2.  **构建势**：利用当前的密度 $n^{(k)}(\mathbf{r})$，计算 Hartree 势 $v_{\mathrm{H}}[n^{(k)}]$ 和交换关联势 $v_{\mathrm{xc}}[n^{(k)}]$，从而构建[有效势](@entry_id:142581) $v_{\mathrm{eff}}^{(k)}(\mathbf{r})$。
3.  **求解 KS 方程**：求解当前的单粒子 KS 方程 $\{-\frac{1}{2}\nabla^2 + v_{\mathrm{eff}}^{(k)}\} \phi_i^{(k)} = \varepsilon_i^{(k)} \phi_i^{(k)}$，得到一组新的 KS [轨道](@entry_id:137151) $\{\phi_i^{(k)}\}$ 和[轨道](@entry_id:137151)能 $\{\varepsilon_i^{(k)}\}$。对于晶体，这一步需要在布里渊区的一系列 $\mathbf{k}$ 点上进行。
4.  **计算新密度**：根据得到的[轨道](@entry_id:137151)和[费米-狄拉克分布](@entry_id:138909)（或零温下的阶梯函数）确定[轨道](@entry_id:137151)占据数，计算出新的输出密度 $n_{\mathrm{out}}^{(k)}(\mathbf{r}) = \sum_i f_i^{(k)} |\phi_i^{(k)}(\mathbf{r})|^2$。
5.  **密度混合**：直接用 $n_{\mathrm{out}}^{(k)}$ 作为下一次迭代的输入密度 $n^{(k+1)}$ 常常会导致[振荡](@entry_id:267781)或发散。因此，需要将输入和输出密度进行混合，例如简单的线性混合 $n^{(k+1)} = (1-\alpha)n^{(k)} + \alpha n_{\mathrm{out}}^{(k)}$，或者更高效的 Pulay 或 Broyden 混合方案。
6.  **收敛判断**：检查是否达到自洽。一个严格的收敛标准通常需要同时满足两个条件：(a) 总能量在连续两次迭代之间的变化小于一个阈值（例如 $10^{-6}$ eV/atom）；(b) 输入和输出密度之间的差异（例如其 L2 范数）小于一个阈值。如果未收敛，则返回第 2 步，开始新的迭代。

只有当输入密度和输出密度几乎完全一致，即找到了密度-[势场](@entry_id:143025)映射的[不动点](@entry_id:156394)时，SCF 循环才结束，此时得到的密度、能量和[波函数](@entry_id:147440)才是 Kohn-Sham 理论的解。

### 理论深度：有效性与局限性

Kohn-Sham 方法的成功依赖于一些深刻的理论假设，理解这些假设的边界是掌握 DFT 的关键。

#### [V-可表示性问题](@entry_id:202181)

Kohn-Sham 理论的一个核心假设是：真实的、相互作用体系的基[态密度](@entry_id:147894) $n(\mathbf{r})$ 是**无相互作用 V-可表示 (non-interacting v-representable, NIVR)** 的。这意味着，必然存在一个局域的单粒子势 $v_s(\mathbf{r})$，使得无相互作用体系在该势下的基态密度恰好就是 $n(\mathbf{r})$ [@problem_id:3493934]。

然而，并非所有数学上合理的密度函数都满足 NIVR 条件。一个密度要成为物理上可接受的基[态密度](@entry_id:147894)，其对应的动能必须是有限的。通过 Levy-Lieb 的约[束搜索](@entry_id:634146)原理，无相互作用动能泛函 $T_s[n]$ 被定义为在所有产生密度 $n$ 的单[行列式](@entry_id:142978)[波函数](@entry_id:147440)中，动能[期望值](@entry_id:153208)的最小值。如果对于某个密度 $n$，这个最小动能是无穷大，那么它就不可能是任何有限能量体系的基[态密度](@entry_id:147894)。

一个典型的例子可以揭示这一点 [@problem_id:3493913]。考虑一个一维双电子体系，其密度在原点附近表现为 $n(x) \propto |x|$。这对应于一个 KS [轨道](@entry_id:137151) $\phi(x) \propto |x|^{1/2}$。对该[轨道](@entry_id:137151)求[二阶导数](@entry_id:144508)并反解 KS 方程会发现，产生该[轨道](@entry_id:137151)所需的势在原点附近具有 $v_s(x) \sim -1/(8x^2)$ 的形式。这种 $-1/x^2$ 形式的吸引势在量子力学中是病态的：当其系数的[绝对值](@entry_id:147688)超过一个临界值时（在一维情况下为 $1/8$），[哈密顿量](@entry_id:172864)将不再有下界，即不存在稳定的[基态](@entry_id:150928)。此外，我们也可以直接计算该[轨道](@entry_id:137151)的动能，发现 $\int |\phi'(x)|^2 dx \propto \int |x|^{-1} dx$ 在原点发散。这两种分析都表明，这种在原点具有尖锐“V”形（线性）的密度不是 NIVR 的。

相比之下，如果密度在原点附近的行为被“软化”为 $n(x) \propto |x|^\alpha$ 且 $\alpha > 1$，那么其对应的动能将是有限的，并且所需的势在原点处的[奇点](@entry_id:137764)是“亚临界”的，可以支持稳定的[基态](@entry_id:150928)。这类密度就是 NIVR 的。[V-可表示性问题](@entry_id:202181)提醒我们，密度空间中存在着 KS 映射无法到达的“[禁区](@entry_id:175956)”，这对发展无需[轨道](@entry_id:137151)的 DFT 理论 (Orbital-Free DFT) 提出了严峻的挑战。

#### [导数不连续性](@entry_id:136336)与[能隙问题](@entry_id:143831)

Kohn-Sham 理论的另一个深刻之处在于其对[能隙](@entry_id:191975)的描述。对于一个有 $N$ 个电子的体系，其电离能 $I=E(N-1)-E(N)$，[电子亲和能](@entry_id:147520) $A=E(N)-E(N+1)$，基本[能隙](@entry_id:191975)定义为 $E_g = I - A$。理论分析表明，对于精确的泛函，总能量 $E(N)$ 作为电子数 $N$ 的函数，在整数之间是[分段线性](@entry_id:201467)的 [@problem_id:3493928]。

这意味着化学势 $\mu = \partial E / \partial N$ 在整数 $N$ 处会发生跳变。在 $N$ 的左侧，$\mu(N^-) = -I$；在 $N$ 的右侧，$\mu(N^+) = -A$。因此，化学势在整数处的跳变幅度恰好等于基本[能隙](@entry_id:191975)：$\Delta\mu = \mu(N^+) - \mu(N^-) = I - A = E_g$ [@problem_id:3493928] [@problem_id:3493942]。

在 Kohn-Sham 体系中，对于精确的泛函，最高占据[轨道](@entry_id:137151) (HOMO) 的能量等于负的电离能，即 $\varepsilon_{\mathrm{H}} = -I$。然而，最低未占[轨道](@entry_id:137151) (LUMO) 的能量 $\varepsilon_{\mathrm{L}}$ 并不等于负的[电子亲和能](@entry_id:147520)。为了让 KS 体系的化学势也发生正确的跳变，交换关联势 $v_{\mathrm{xc}}(\mathbf{r})$ 本身在电子数穿过整数时必须有一个不连续的跳变。这个跳变是一个空间上均匀的常数 $\Delta_{\mathrm{xc}}$，被称为**[导数不连续性](@entry_id:136336)**。

这一[不连续性](@entry_id:144108)修正了 LUMO 的物理意义，使得 $-A = \varepsilon_{\mathrm{L}} + \Delta_{\mathrm{xc}}$。将这些关系整合，我们得到基本[能隙](@entry_id:191975)与 KS [轨道](@entry_id:137151)[能隙](@entry_id:191975)之间的精确关系：
$$
E_g = (\varepsilon_{\mathrm{L}} - \varepsilon_{\mathrm{H}}) + \Delta_{\mathrm{xc}} = E_g^{\mathrm{KS}} + \Delta_{\mathrm{xc}}
$$
这个结果表明，真实的物理[能隙](@entry_id:191975)等于 KS [轨道](@entry_id:137151)[能隙](@entry_id:191975)加上一个来自交换关联势的[导数不连续性](@entry_id:136336)修正。

这完美地解释了为何 LDA 和 GGA 等半局域近似严重低估[半导体](@entry_id:141536)和绝缘体[能隙](@entry_id:191975)的原因：这些近似的[能量泛函](@entry_id:170311)对于密度是光滑可导的，其对应的交换关联势 $v_{\mathrm{xc}}$ 是连续的，因此 $\Delta_{\mathrm{xc}} \approx 0$。这导致 $E_g \approx E_g^{\mathrm{KS}}$，而 KS [能隙](@entry_id:191975)本身通常远小于实验[能隙](@entry_id:191975)。

相反，包含部分[精确交换](@entry_id:178558)的[杂化泛函](@entry_id:164921)等更高级的近似，通过引入非局域的[交换算符](@entry_id:156554)，能够部分地将[导数不连续性](@entry_id:136336)的效应“内化”到[轨道](@entry_id:137151)能的计算中，从而显著“打开”KS [能隙](@entry_id:191975)，使其更接近真实的物理[能隙](@entry_id:191975) [@problem_id:3493928]。理解[导数不连续性](@entry_id:136336)是理解和超越标准 DFT 近似局限性的关键。