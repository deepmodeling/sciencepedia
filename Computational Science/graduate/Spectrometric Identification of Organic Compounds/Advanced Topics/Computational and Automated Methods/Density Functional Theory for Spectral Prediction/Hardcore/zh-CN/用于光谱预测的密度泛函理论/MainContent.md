## 引言
在有机化合物的结构鉴定中，光谱分析是不可或缺的工具。然而，仅凭实验谱图往往难以对复杂的分子结构做出唯一、明确的指认。因此，发展精确且高效的理论计算方法，从第一性原理层面预测和解析[光谱](@entry_id:185632)，对于补充和验证实验数据至关重要。[密度泛函理论](@entry_id:139027)（DFT）及其含时扩展（TDDFT）正是在这一背景下应运而生的强大计算工具，它在计算成本与精度之间取得了卓越的平衡，已成为现代[量子化学](@entry_id:140193)计算的标准方法之一。

本文旨在为读者提供一个关于使用DFT进行[光谱](@entry_id:185632)预测的全面指南。我们将分三步展开：在**“原理与机制”**一章中，我们将奠定理论基石，从电子密度这一核心变量出发，深入探讨[科恩-沈方程](@entry_id:143968)、[交换相关泛函](@entry_id:142042)的层次结构，以及预测电子和[磁共振](@entry_id:143712)[光谱](@entry_id:185632)的具体机制。随后，在**“应用与跨学科连接”**一章中，我们将通过丰富的案例展示该理论如何解决从[结构异构体](@entry_id:146226)辨析到复杂环境模拟等实际化学问题，并揭示其在[材料科学](@entry_id:152226)和生物物理等[交叉](@entry_id:147634)领域的应用。最后，在**“动手实践”**部分，读者将有机会通过具体的计算练习，亲身体验影响DFT计算精度的关键因素。

通过这一结构化的学习路径，本文将帮助您建立从基础理论到实际应用的完整知识体系。现在，让我们从第一章开始，深入探索DFT进行[光谱](@entry_id:185632)预测的原理与机制。

## 原理与机制

本章旨在深入探讨[密度泛函理论](@entry_id:139027)（DFT）及其含时扩展（TDDFT）在[光谱](@entry_id:185632)预测中的核心原理与机制。我们将从理论的基石——电子密度是基本变量这一概念出发，逐步构建科恩-沈（Kohn-Sham）框架，并探索近似[交换相关泛函](@entry_id:142042)的“[雅各布天梯](@entry_id:139901)”。随后，我们将详细阐述如何利用该理论预测紫外-可见（UV-Vis）、核[磁共振](@entry_id:143712)（NMR）和[电子顺磁共振](@entry_id:155215)（EPR）[光谱](@entry_id:185632)。最后，我们将讨论标准近似方法的主要局限性，并介绍旨在克服这些挑战的先进解决方案。

### 理论基石：电子密度作为核心变量

[量子化学](@entry_id:140193)的中心任务是求解多电子体系的薛定谔方程，然而，由于电子间的相互作用，这是一个极其复杂的多体问题。密度泛函理论（DFT）提供了一条迥然不同的路径，其革命性思想在于证明了体系的所有性质均可由其电子密度 $n(\mathbf{r})$——一个仅与三个空间坐标相关的函数——唯一确定。这一思想由两个深刻的霍恩伯格-科恩（Hohenberg-Kohn, HK）定理奠定。

电子密度 $n(\mathbf{r})$ 是一个在物理上直观且可测量的量。对于一个含 $N$ 个电子、[基态](@entry_id:150928)[波函数](@entry_id:147440)为 $\Psi(\mathbf{r}_1, \ldots, \mathbf{r}_N)$ 的体系，电子密度定义为在空间中某一点 $\mathbf{r}$ 找到任意一个电子的[概率密度](@entry_id:175496)。数学上，它可以表示为对[波函数](@entry_id:147440)概率密度的积分，或者通过[密度算符](@entry_id:138151) $\hat{n}(\mathbf{r}) = \sum_{i=1}^{N} \delta(\mathbf{r}-\mathbf{r}_i)$ 的[期望值](@entry_id:153208)得到 ：

$$
n(\mathbf{r}) = N \int |\Psi(\mathbf{r}, \mathbf{r}_2, \ldots, \mathbf{r}_N)|^2 \, d\mathbf{r}_2 \cdots d\mathbf{r}_N = \langle \Psi | \hat{n}(\mathbf{r}) | \Psi \rangle
$$

对密度在全空间积分，可得到体系的总电子数 $N$。

**第一[霍恩伯格-科恩定理](@entry_id:139793)** 指出，对于一个（非简并）[基态](@entry_id:150928)，体系的[基态](@entry_id:150928)电子密度 $n_0(\mathbf{r})$ 与外势 $v(\mathbf{r})$ 之间存在一一对应关系（最多相差一个无关紧要的常数）。对于分子体系，外势即为[原子核](@entry_id:167902)对电子的库仑吸引势，它完全由[原子核](@entry_id:167902)的位置和[电荷](@entry_id:275494)决定。因此， $n_0(\mathbf{r})$ 唯一地确定了外势 $v(\mathbf{r})$，进而确定了整个[哈密顿算符](@entry_id:144286) $\hat{H}$。由于[哈密顿算符](@entry_id:144286)包含了体系的所有信息，这意味着[基态](@entry_id:150928)、[激发态](@entry_id:261453)以及所有其他[可观测性](@entry_id:152062)质，原则上都是[基态](@entry_id:150928)电子密度的泛函 。这一结论是颠覆性的，它将求解一个复杂的 $3N$ 维[波函数](@entry_id:147440)的问题，转化为了求解一个三维密度函数的问题。

**第二[霍恩伯格-科恩定理](@entry_id:139793)** 为通过密度求解体系能量提供了[变分原理](@entry_id:198028)。该定理断言，存在一个不依赖于外势的[普适泛函](@entry_id:140176) $F_{HK}[n]$，它包含了体系的动能和[电子-电子相互作用](@entry_id:139900)能。总电子能量可以写成：

$$
E_v[n] = F_{HK}[n] + \int v(\mathbf{r}) n(\mathbf{r}) \, d\mathbf{r}
$$

对于给定的外势 $v(\mathbf{r})$，真实的基态密度 $n_0(\mathbf{r})$ 能使能量泛函 $E_v[n]$ 达到最小值，这个最小值就是体系的[基态能量](@entry_id:263704) $E_0$ 。

然而，HK定理只是“[存在性证明](@entry_id:267253)”，它们并未告诉我们[普适泛函](@entry_id:140176) $F_{HK}[n]$ 的具体形式。这催生了科恩-沈（Kohn-Sham, KS）方法的诞生，它为DFT的实际应用铺平了道路。

### [科恩-沈方程](@entry_id:143968)：一种实用的计算方案

[科恩-沈方法](@entry_id:263733)的核心思想是引入一个辅助的、无相互作用的电子体系，该体系在某个[有效势](@entry_id:142581) $v_{KS}(\mathbf{r})$ 中运动，并精确地产生与真实相互作用体系相同的[基态](@entry_id:150928)电子密度 $n(\mathbf{r})$。由于这个辅助体系是无相互作用的，其[基态](@entry_id:150928)[波函数](@entry_id:147440)可以严格地写成一个单[斯莱特行列式](@entry_id:139034)（Slater determinant），由一组称为[科恩-沈轨道](@entry_id:171979)的单电子[波函数](@entry_id:147440) $\{\psi_i\}$ 构成。电子密度则可由这些[轨道](@entry_id:137151)简单求和得到：

$$
n(\mathbf{r}) = \sum_{i=1}^{N} |\psi_i(\mathbf{r})|^2
$$

[科恩-沈方法](@entry_id:263733)巧妙地将总能量泛函 $E[n]$ 分解为几个部分：

$$
E[n] = T_s[n] + \int v_{\text{ext}}(\mathbf{r}) n(\mathbf{r}) \, d\mathbf{r} + E_H[n] + E_{xc}[n]
$$

其中，$T_s[n]$ 是无相互作用体系的动能（可以精确地通过KS[轨道](@entry_id:137151)计算），$E_H[n]$ 是电子密度间经典静电排斥的哈特里（Hartree）能量。所有复杂的、非经典的量子[多体效应](@entry_id:173569)——包括交换作用、电子相关以及真实动能与 $T_s[n]$ 之间的差值——都被归入了一个唯一的未知项：**交换相关（exchange-correlation, XC）能** $E_{xc}[n]$。

对总[能量泛函](@entry_id:170311)应用变分原理，即可导出一系列类似于[Hartree-Fock方程](@entry_id:194386)的单电子方程，即[科恩-沈方程](@entry_id:143968)：

$$
\left[ -\frac{1}{2}\nabla^2 + v_{KS}(\mathbf{r}) \right] \psi_i(\mathbf{r}) = \varepsilon_i \psi_i(\mathbf{r})
$$

其中，有效势 $v_{KS}(\mathbf{r})$ 由外势、哈特里势和[交换相关势](@entry_id:180254)组成：

$$
v_{KS}(\mathbf{r}) = v_{\text{ext}}(\mathbf{r}) + v_H(\mathbf{r}) + v_{xc}(\mathbf{r})
$$

哈特里势 $v_H(\mathbf{r}) = \int \frac{n(\mathbf{r}')}{|\mathbf{r}-\mathbf{r}'|} \, d\mathbf{r}'$，$v_{xc}(\mathbf{r})$ 则是[交换相关能](@entry_id:138029)对密度的泛函导数 $v_{xc}(\mathbf{r}) = \frac{\delta E_{xc}[n]}{\delta n(\mathbf{r})}$。整个KS方案的成败完全取决于对未知[交换相关泛函](@entry_id:142042) $E_{xc}[n]$ 的近似精度。

### [交换相关泛函](@entry_id:142042)的“[雅各布天梯](@entry_id:139901)”

寻找精确的 $E_{xc}[n]$ 是DFT发展的核心。物理学家John Perdew提出了一个名为**“[雅各布天梯](@entry_id:139901)”（Jacob's Ladder）**的概念，将XC泛函按照其依赖的物理量和预期的精度进行分层。从梯子的低层向高层攀登，泛函变得越来越复杂，计算成本也随之增加，但通常能提供更准确的物理描述 。

**第一阶：[局域密度近似](@entry_id:138982)（Local Density Approximation, LDA）**
这是最简单的近似，它假设在空间中每一点的[交换相关能](@entry_id:138029)密度只依赖于该点的电子密度值 $n(\mathbf{r})$。其形式来源于[均匀电子气](@entry_id:163911)的精确解。[LDA](@entry_id:138982)在描述[键长](@entry_id:144592)和[振动频率](@entry_id:199185)等性质时存在系统性偏差，例如，它通常会过度估计分子的结合能，导致预测的[振动频率](@entry_id:199185)偏高。

**第二阶：[广义梯度近似](@entry_id:274118)（Generalized Gradient Approximation, GGA）**
[GGA泛函](@entry_id:190164)在LDA的基础上，引入了电子密度的梯度 $\nabla n(\mathbf{r})$ 作为变量。这使得泛函能够“感知”密度的变化率，从而更好地区分不同化学环境。[GGA泛函](@entry_id:190164)的形式可以写为 $E_{\mathrm{xc}}^{\mathrm{GGA}} = \int n(\mathbf{r}) \epsilon_{\mathrm{xc}}(n(\mathbf{r}), \nabla n(\mathbf{r})) d\mathbf{r}$。通过[变分法](@entry_id:163656)，可以推导出其对应的XC势 ：

$$
v_{\mathrm{xc}}(\mathbf{r}) = \frac{\partial [n \epsilon_{\mathrm{xc}}]}{\partial n} - \nabla \cdot \left[ \frac{\partial [n \epsilon_{\mathrm{xc}}]}{\partial (\nabla n)} \right]
$$

相较于LDA，GGA显著改善了对分子几何、[原子化](@entry_id:155635)能和[振动频率](@entry_id:199185)的预测。梯度依赖性使得XC响应核 $f_{\mathrm{xc}}(\mathbf{r}, \mathbf{r}')$ 具有半局域性（包含狄拉克$\delta$函数及其导数），这通常能改进对[极化率](@entry_id:143513)等响应性质的预测，但对于需要非局域描述的现象仍然力不从心。

**第三阶：元[广义梯度近似](@entry_id:274118)（[meta-GGA](@entry_id:191648)）**
[meta-GGA泛函](@entry_id:177894)在GGA的基础上，进一步包含了与KS[轨道](@entry_id:137151)动能密度 $\tau(\mathbf{r})$ 相关的信息。$\tau(\mathbf{r})$ 能够更精细地识别化学键的类型（如[单键](@entry_id:188561)、双键、三键），从而提供更高的准确性。

**第四阶：[杂化泛函](@entry_id:164921)（Hybrid Functionals）**
[杂化泛函](@entry_id:164921)是DFT在化学应用中取得巨大成功的关键。其核心思想是，LDA和GGA等近似泛函存在**[自相互作用误差](@entry_id:139981)（self-interaction error, SIE）**。具体而言，[哈特里能量](@entry_id:167303) $E_H[n]$ 包含了一个电子与其自身密度之间的虚假排斥作用，而在精确理论中，这一项应由交换能精确抵消。近似泛函对这种抵消处理得并不完美 。

SIE会导致许多问题：
1.  **[电荷](@entry_id:275494)[离域](@entry_id:183327)**：虚假的自排斥使得电子倾向于“散开”，导致电子密度过度[离域](@entry_id:183327)。
2.  **[轨道能级](@entry_id:151753)错误**： occupie[d轨道](@entry_id:261792)的能量被系统性地抬高（不够负），特别是最高占据分子[轨道](@entry_id:137151)（HOMO）。根据[Koopmans定理](@entry_id:139178)的DFT推广（$I \approx -\varepsilon_{\text{HOMO}}$），这导致[电离势](@entry_id:198846)的严重低估 。
3.  **错误的解离行为**：在分子解离极限下给出错误的结果。

[杂化泛函](@entry_id:164921)通过引入一定比例（记为 $\alpha$）的“精确”[哈特里-福克](@entry_id:142303)（HF）交换能来缓解SIE。HF[交换能](@entry_id:137069)天然无自相互作用。增加HF交换的比例 $\alpha$ 会带来显著影响 ：
*   **[轨道](@entry_id:137151)[能隙](@entry_id:191975)增大**：HF[交换能](@entry_id:137069)会更强烈地稳定占据[轨道](@entry_id:137151)（能量降低）并 destabilize 未占据[轨道](@entry_id:137151)（能量升高），从而“打开”KS的[HOMO-LUMO能隙](@entry_id:139325) $\Delta_{\text{KS}}$。
*   **改善[光谱](@entry_id:185632)预测**：对于局域价[电子激发](@entry_id:190531)，增大的[轨道](@entry_id:137151)[能隙](@entry_id:191975)和修正的XC核通常会使TDDFT预测的激发能升高，更接近实验值。

**第五阶：[双杂化泛函](@entry_id:177273)（Double-Hybrid Functionals）**
这是天梯的更高层，它不仅混合了HF[交换能](@entry_id:137069)，还引入了来自[波函数](@entry_id:147440)理论（如二阶[Møller-Plesset微扰理论](@entry_id:142108)，MP2）的相关能。这些泛函依赖于未占据的KS[轨道](@entry_id:137151)，计算成本更高，但通常能达到[化学精度](@entry_id:171082)的要求。

### 利用[含时密度泛函理论](@entry_id:200019)（TDDFT）预测[电子光谱](@entry_id:154403)

[基态](@entry_id:150928)DFT主要用于计算分子的结构、能量和相关性质。要预测[电子光谱](@entry_id:154403)（如UV-Vis吸收光谱），我们需要一个能描述[激发态](@entry_id:261453)的理论。虽然HK定理原则上保证了[激发态](@entry_id:261453)是基态密度的泛函，但其具体形式未知。**[含时密度泛函理论](@entry_id:200019)（TDDFT）**为此提供了强大的计算工具。

TDDFT的基石是**龙格-格罗斯（Runge-Gross）定理**，它将HK定理推广到含时领域，建立了含时密度 $n(\mathbf{r}, t)$ 与含时外势 $v(\mathbf{r}, t)$ 之间的一一对应关系 。在**[线性响应](@entry_id:146180)**框架下，我们可以计算体系对微弱、[振荡](@entry_id:267781)的[电磁场](@entry_id:265881)（如光）的响应。该理论的一个核心结论是：体系的真实[电子激发](@entry_id:190531)能对应于相互作用密度-密度响应函数 $\chi$ 的极点。

在实践中，求解这些极点被转化为一个矩阵[本征值问题](@entry_id:142153)，即著名的**卡西达（Casida）方程** 。对于一个闭壳层体系的单重态激发，该方程可写为：

$$
\begin{pmatrix}
\mathbf{A} & \mathbf{B} \\
\mathbf{B} & \mathbf{A}
\end{pmatrix}
\begin{pmatrix}
\mathbf{X} \\
\mathbf{Y}
\end{pmatrix}
= \omega
\begin{pmatrix}
\mathbf{1} & \mathbf{0} \\
\mathbf{0} & -\mathbf{1}
\end{pmatrix}
\begin{pmatrix}
\mathbf{X} \\
\mathbf{Y}
\end{pmatrix}
$$

其中，$\omega$ 是预测的激发能。矩阵 $\mathbf{A}$ 和 $\mathbf{B}$ 的矩阵元构建于KS单电子跃迁（从占据[轨道](@entry_id:137151) $i$ 到空[轨道](@entry_id:137151) $a$）的基础上：

$$
A_{ia, jb} = \delta_{ij}\delta_{ab}(\varepsilon_a - \varepsilon_i) + K_{ia, jb}
$$
$$
B_{ia, jb} = K'_{ia, jb}
$$

这里的 $\varepsilon_a - \varepsilon_i$ 是KS[轨道能级](@entry_id:151753)差，可以看作是“零级”的[激发能](@entry_id:190368)。关键在于**[耦合矩阵](@entry_id:191757)** $K$ 和 $K'$，它们描述了不同单电子跃迁之间的相互作用。这些矩阵元由哈特里（库仑）项和[交换相关核](@entry_id:195258) $f_{xc}(\mathbf{r}, \mathbf{r}') = \frac{\delta v_{xc}(\mathbf{r})}{\delta n(\mathbf{r}')}$ 积分得到。因此，TDDFT的激发能是对KS[轨道能级](@entry_id:151753)差的修正。例如，对于一个由两个KS跃迁（$\Delta_1 = 2.50 \, \text{eV}$ 和 $\Delta_2 = 3.20 \, \text{eV}$）主导的体系，如果其间的[耦合矩阵](@entry_id:191757)元非零，那么最终的激发能将不再是 $2.50 \, \text{eV}$ 和 $3.20 \, \text{eV}$，而是这两个跃迁混合后的结果，例如可能变为 $2.78 \, \text{eV}$ 和 $3.40 \, \text{eV}$ 。

### TDDFT的挑战与高级解决方案

尽管TDDFT取得了巨大成功，但标准的近似方法也面临严峻挑战。

#### [电荷转移](@entry_id:155270)（CT）激发

对于由空间上分离的给体（Donor, D）和受体（Acceptor, A）组成的分子，其最低[激发态](@entry_id:261453)往往具有电荷转移（CT）特征。在这种激发中，HOMO和LUMO几乎没有空间重叠。对于[LDA](@entry_id:138982)和GGA等（半）局域泛函，XC核 $f_{xc}$ 随距离迅速衰减。这意味着对于长程CT激发，[耦合矩阵](@entry_id:191757)元几乎为零，激发能退化为KS[轨道能级](@entry_id:151753)差 $\omega_{CT} \approx \varepsilon_{\text{LUMO}} - \varepsilon_{\text{HOMO}}$ 。这导致了两个灾难性后果：
1.  由于SIE，KS[能隙](@entry_id:191975)本身就被严重低估。
2.  TDDFT计算完全忽略了分离后的正负[电荷](@entry_id:275494)（[电子-空穴对](@entry_id:142506)）之间的库侖吸引能（应为 $-1/R$）。

这两个因素共同导致TDDFT严重低估长程CT[激发能](@entry_id:190368)。虽然全局[杂化泛函](@entry_id:164921)能通过增大KS[能隙](@entry_id:191975)部分缓解问题，但其XC核的渐进行为仍然是错误的。

**解决方案：[范围分离杂化泛函](@entry_id:184447)（Range-Separated Hybrid, RSH）**
[RSH泛函](@entry_id:184447)是为解决此问题而设计的。它将[库仑算符](@entry_id:178946) $1/r$ 分割为短程（short-range, SR）和长程（long-range, LR）两部分，通常使用[互补误差函数](@entry_id:190973)来实现平滑过渡 ：

$$
\frac{1}{r} = \frac{\operatorname{erfc}(\omega r)}{r}_{\text{SR}} + \frac{\operatorname{erf}(\omega r)}{r}_{\text{LR}}
$$

其中，$\omega$ 是范围分离参数。[RSH泛函](@entry_id:184447)对短程部分使用DFT交换，而对长程部分使用100%的HF交换。由于HF交换的非局域性，这确保了XC势和XC核在长程极限下具有正确的 $-1/r$ 行为。通过“调节”参数 $\omega$ 以满足某些物理约束（如使 $-\varepsilon_{\text{HOMO}}$ 逼近[电离势](@entry_id:198846) $I$），RSH TDDFT可以准确地预测CT激发能。

#### 双激发与[绝热近似](@entry_id:143074)

标准TDDFT是在**[绝热近似](@entry_id:143074)（adiabatic approximation）**下进行的，即假设XC核 $f_{xc}$ 不依赖于频率 $\omega$ 。这种近似的直接后果是，TDDFT的[激发态](@entry_id:261453)[流形](@entry_id:153038)完全由单粒子-单空穴（$1p-1h$）激发构成。因此，它无法描述那些主要由**双激发**（即两个电子同时被激发，形成 $2p-2h$ 态）主导的[激发态](@entry_id:261453)。

对于某些分子，如[共轭多烯](@entry_id:266209)[烃](@entry_id:145872)，其低能区存在重要的、具有双激发特征的暗态（如 $2^1A_g$ 态）。绝热TDDFT会完全“丢失”这些态，或者将它们错误地置于非常高的能量处，从而导致对[光谱](@entry_id:185632)和[光物理过程](@entry_id:154565)的定性错误预测 。引入频率依赖的XC核或采用更高级的理论，如自旋反转（Spin-Flip）TDDFT或基于[波函数](@entry_id:147440)的[EOM-CCSD](@entry_id:166585)方法，是解决这一问题的途径。

### 预测[磁共振](@entry_id:143712)[光谱](@entry_id:185632)

DFT的应用远不止于[电子光谱](@entry_id:154403)，它也是预测[磁共振](@entry_id:143712)参数的强大工具。

#### 核[磁共振](@entry_id:143712)（NMR）[光谱](@entry_id:185632)

NMR谱中的化学位移源于[原子核](@entry_id:167902)周围的电子云对外[磁场](@entry_id:153296) $\mathbf{B}_0$ 的响应。电子产生一个感应场 $\mathbf{B}_{\text{ind}}$，它“屏蔽”了[原子核](@entry_id:167902)，使其感受到的[有效磁场](@entry_id:139861) $\mathbf{B}_{\text{eff}}$ 与外场不同。在线性响应范围内，这种关系由**核[磁屏蔽](@entry_id:192877)张量** $\boldsymbol{\sigma}$ 定义 ：

$$
\mathbf{B}_{\text{ind}} = -\boldsymbol{\sigma} \mathbf{B}_0 \quad \implies \quad \mathbf{B}_{\text{eff}} = (\mathbf{I} - \boldsymbol{\sigma}) \mathbf{B}_0
$$

负号表示电子云通常起屏蔽作用（反磁性）。在溶液中，分子快速翻滚，我们观测到的是各向同性[屏蔽常数](@entry_id:152583) $\sigma_{\text{iso}} = \frac{1}{3}\mathrm{Tr}(\boldsymbol{\sigma})$。实验上测量的**化学位移** $\delta$ 是相对于一个标准物（如[四甲基硅烷](@entry_id:755877), TMS）定义的，其近似关系为：

$$
\delta \approx \sigma_{\text{ref,iso}} - \sigma_{\text{iso}}
$$

DFT是计算 $\boldsymbol{\sigma}$ 张量的标准方法。然而，SIE在这里再次成为关键。LDA/[GGA泛函](@entry_id:190164)由于过度[离域电子](@entry_id:274811)云，会系统性地高估屏蔽效应（计算出的 $\sigma_{\text{iso}}$ 偏大），从而低估[化学位移](@entry_id:140028)。[杂化泛函](@entry_id:164921)通过减轻SIE，能够更准确地描述局域电子环境，因此是计算[NMR化学位移](@entry_id:204209)的常规选择 。例如，对于一个质子，若计算出的 $\sigma_{\text{iso}}$ 为 $30.5 \, \text{ppm}$，而TMS的参考值为 $31.9 \, \text{ppm}$，则预测的化学位移为 $\delta = 31.9 - 30.5 = 1.4 \, \text{ppm}$ 。

#### [电子顺磁共振](@entry_id:155215)（EPR）[光谱](@entry_id:185632)

EPR是研究含有未成对电子的[自由基](@entry_id:164363)物种的有力工具。DFT可用于预测EPR谱图的两个关键参数：**g-张量**和**[超精细耦合](@entry_id:174861)张量 A** 。

*   **g-张量**: 它描述了[电子自旋](@entry_id:137016)磁矩与外[磁场](@entry_id:153296)的有效[耦合强度](@entry_id:275517)。对于一个自由电子，g值是一个标量 $g_e \approx 2.0023$。在分子中，由于电子的轨道运动与自旋之间的**[自旋-轨道耦合](@entry_id:143520)**（一种相对论效应），g变成了一个张量 $\mathbf{g}$。DFT计算g-张量正是通过微扰论处理这些相对论效应。在溶液中，观测到的是其各向同性值 $g_{\text{iso}}$。

*   **[超精细耦合](@entry_id:174861)张量 A**: 它描述了电子自旋与磁性[原子核](@entry_id:167902)自旋之间的相互作用。该张量可分解为两部分：
    1.  **费米接触项**：一个各向同性的项，正比于未成对电子在[原子核](@entry_id:167902)位置的自旋密度。这是液体EPR谱中观测到的[超精细分裂](@entry_id:152361)的来源。
    2.  **[偶极-偶极相互作用](@entry_id:144039)项**：一个各向异性的、无迹的项，源于电子和核自旋[磁偶极子](@entry_id:275765)间的经典相互作用。在溶液中，其贡献被平均为零。

对于一个电子自旋 $S=1/2$ 与一个核自旋 $I=1/2$ 相互作用的体系，EPR共振条件为 $h\nu = g_{\text{iso}} \mu_B B + h A_{\text{iso}} m_I$。由于 $m_I$ 可以取 $\pm 1/2$，谱图将分裂成两条线，其中心位置由 $g_{\text{iso}}$ 决定，分裂大小 $\Delta B$ 由各向同性[超精细耦合常数](@entry_id:178227) $A_{\text{iso}}$ 决定 $\Delta B = \frac{h A_{\text{iso}}}{g_{\text{iso}} \mu_B}$。DFT通过计算自旋密度，可以相当准确地预测这些参数，从而帮助鉴定[自由基](@entry_id:164363)的结构 。