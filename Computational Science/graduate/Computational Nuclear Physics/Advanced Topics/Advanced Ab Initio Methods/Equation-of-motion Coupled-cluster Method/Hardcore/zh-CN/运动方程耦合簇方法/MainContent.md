## 引言
在现代核物理研究中，从[核子](@entry_id:158389)间的[基本相互作用](@entry_id:749649)出发，精确预测[原子核](@entry_id:167902)的结构与反应性质，即“[第一性原理计算](@entry_id:198754)”，是理解[量子多体问题](@entry_id:146763)的核心挑战。尽管[原子核](@entry_id:167902)由相对简单的构建块（质子和中子）组成，但它们之间复杂的相互作用催生了从[单粒子运动](@entry_id:159951)到集体[振动](@entry_id:267781)与转动的丰富现象。[运动方程耦合簇](@entry_id:185022) (Equation-of-Motion Coupled-Cluster, [EOM-CC](@entry_id:266204)) 方法正是在这一背景下应运而生的一种强大理论工具，它旨在提供一个统一且系统精确的框架，不仅能描述[原子核](@entry_id:167902)的[基态](@entry_id:150928)，还能同样精确地计算其激发谱、邻近[核素](@entry_id:145039)的性质以及对弱相互作用探针的响应。

本文旨在全面介绍[EOM-CC](@entry_id:266204)方法。我们将分为三个循序渐进的章节：第一章“原理和机制”将深入剖析该方法的理论根基，从[耦合簇](@entry_id:190682)指数[拟设](@entry_id:184384)和大小[广延性](@entry_id:144932)，到关键的非厄米[相似变换](@entry_id:152935)[哈密顿量](@entry_id:172864)，为理解其工作方式奠定坚实基础。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示[EOM-CC](@entry_id:266204)在解决实际物理问题中的威力，探讨其如何用于计算核谱、[分离能](@entry_id:754696)和跃迁强度，并揭示其与核反应、天体物理乃至机器学习等领域的深刻联系。最后，在第三章“动手实践”中，我们将通过一系列精心设计的计算练习，将抽象的理论转化为具体的代码实现和物理洞察。通过这趟旅程，读者将全面掌握[EOM-CC](@entry_id:266204)这一前沿计算方法的核心思想与实践能力。

## 原理和机制

本章深入探讨[运动方程耦合簇](@entry_id:185022) (Equation-of-Motion Coupled-Cluster, [EOM-CC](@entry_id:266204)) 方法的理论基础。我们将从[耦合簇理论](@entry_id:141746)的基石——指数拟设 (exponential ansatz)——出发，阐明其关键特性，如大小[广延性](@entry_id:144932) (size-extensivity)。随后，我们将引入[相似变换](@entry_id:152935)[哈密顿量](@entry_id:172864) (similarity-transformed Hamiltonian)，并探讨其非[厄米性](@entry_id:141899) (non-Hermiticity) 的深刻含义。最后，我们将构建[运动方程](@entry_id:170720)框架本身，展示如何通过在[耦合簇](@entry_id:190682)[基态](@entry_id:150928)上施加线性激发算符来系统地描述[激发态](@entry_id:261453)和邻近[核素](@entry_id:145039)。本章旨在为后续章节中复杂的核结构应用奠定坚实的理论基础。

### [耦合簇](@entry_id:190682)[基态](@entry_id:150928)拟设

[耦合簇理论](@entry_id:141746)为多体[基态](@entry_id:150928)[波函数](@entry_id:147440) $|\Psi_0\rangle$ 提供了一个优雅且强大的[参数化](@entry_id:272587)形式，即**指数[拟设](@entry_id:184384)**：

$|\Psi_0\rangle = e^{T} |\Phi_0\rangle$

在此， $|\Phi_0\rangle$ 是一个单 Slater [行列式](@entry_id:142978)构成的**参考态**，通常通过 [Hartree-Fock](@entry_id:142303) 计算得到。它代表了系统的零阶近似，即一个充满了最低单粒子[轨道](@entry_id:137151)的[费米海](@entry_id:136725)。算符 $T$ 被称为**簇算符 (cluster operator)**，它是一个通过在参考态 $|\Phi_0\rangle$ 上产生粒子-空穴对激发来引入多体关联的激发算符。

簇算符 $T$ 可以展开为不同激发阶数的和：

$T = T_1 + T_2 + T_3 + \dots$

其中 $T_n$ 产生 $n$-粒子-$n$-空穴 ($npnh$) 激发。在实践中，这个级数必须被截断。最常见的截断方案是**[耦合簇单双激发](@entry_id:747959) (Coupled-Cluster Singles and Doubles, CCSD)**，其中 $T \approx T_1 + T_2$。在第二量子化形式下，使用相对于 $|\Phi_0\rangle$ 的粒子-空穴形式，这些算符可以明确地写出 。我们用索引 $i, j, k, \dots$ 表示在 $|\Phi_0\rangle$ 中被占据的[轨道](@entry_id:137151)（**空穴态**），用 $a, b, c, \dots$ 表示未被占据的[轨道](@entry_id:137151)（**粒子态**）。

$T_1$ 算符描述了所有的单激发（$1p1h$）：

$T_1 = \sum_{ia} t_i^a a_a^{\dagger} a_i$

$T_2$ 算符描述了所有的双激发（$2p2h$）：

$T_2 = \frac{1}{4} \sum_{ijab} t_{ij}^{ab} a_a^{\dagger} a_b^{\dagger} a_j a_i$

这里的 $t_i^a$ 和 $t_{ij}^{ab}$ 分别是单激发和双激发的**簇振幅 (cluster amplitudes)**。这些振幅是通过求解[耦合簇](@entry_id:190682)方程得到的数值。算符 $a_p^{\dagger}$ 和 $a_p$ 分别是[费米子](@entry_id:146235)的产生和湮灭算符。请注意，$T_2$ 算符中的因子 $\frac{1}{4}$ 是一个组合因子，它用于在对所有 $i,j,a,b$ 进行无限制求和时避免重复计数。由于[费米子统计](@entry_id:148436)，产生（或湮灭）算符是反对称的（例如，$a_a^{\dagger} a_b^{\dagger} = -a_b^{\dagger} a_a^{\dagger}$），这要求簇振幅也必须具有相应的反对称性，以确保每个物理上独特的激发只对应一个唯一的振幅：$t_{ij}^{ab} = -t_{ji}^{ab} = -t_{ij}^{ba}$ 。

#### 大小[广延性](@entry_id:144932)

[耦合簇方法](@entry_id:199711)的一个标志性优点是其**大小[广延性](@entry_id:144932)**。一个理论如果对于由两个不相互作用的子系统 $\mathcal{A}$ 和 $\mathcal{B}$ 组成的系统，其总能量等于子系统能量之和，即 $E(\mathcal{A} \oplus \mathcal{B}) = E(\mathcal{A}) + E(\mathcal{B})$，那么这个理论就是大小广延的。

指数拟设天生就能保证大小[广延性](@entry_id:144932) 。考虑一个复合系统，其簇算符是各个子系统算符之和，$T = T_{\mathcal{A}} + T_{\mathcal{B}}$。由于 $T_{\mathcal{A}}$ 和 $T_{\mathcal{B}}$ 作用在不相交的[轨道空间](@entry_id:148658)上，它们相互对易。这使得总[波函数](@entry_id:147440)可以正确地因子化：

$|\Psi_{\mathrm{CC}}\rangle = e^{T} |\Phi_0\rangle = e^{T_{\mathcal{A}} + T_{\mathcal{B}}} |\Phi_0^{\mathcal{A}}\rangle \otimes |\Phi_0^{\mathcal{B}}\rangle = (e^{T_{\mathcal{A}}} |\Phi_0^{\mathcal{A}}\rangle) \otimes (e^{T_{\mathcal{B}}} |\Phi_0^{\mathcal{B}}\rangle) = |\Psi_{\mathrm{CC}}^{\mathcal{A}}\rangle \otimes |\Psi_{\mathrm{CC}}^{\mathcal{B}}\rangle$

这种[波函数](@entry_id:147440)的因子化能力是大小[广延性](@entry_id:144932)的核心。与之形成鲜明对比的是，被截断的**[组态相互作用](@entry_id:195713) (Configuration Interaction, CI)** 方法，例如 CISD，其[波函数](@entry_id:147440)是一个线性的激发算符作用在参考态上：$|\Psi_{\mathrm{CISD}}\rangle = (1 + C_1 + C_2) |\Phi_0\rangle$。这种线性拟设无法因子化。例如，描述系统 $\mathcal{A}$ 上的一个双激发和系统 $\mathcal{B}$ 上的一个双激发同时发生的状态，需要一个四重激发算符。这个项（一个非关联的四重激发）自然地包含在 $e^{T_2}$ 的展开中（作为 $T_{2,\mathcal{A}} T_{2,\mathcal{B}}$），但在 CISD 中却被严格截断掉了。这种缺陷导致截断 CI 方法不是大小广延的，这是一个严重的理论缺陷，尤其是在描述大系统时。

#### 参考态的质量：$T_1$ 诊断

[耦合簇方法](@entry_id:199711)是单参考方法，其成功与否严重依赖于[参考态](@entry_id:151465) $|\Phi_0\rangle$ 是否是真实[基态](@entry_id:150928)的一个良好零阶近似。当系统中存在显著的**静态关联 (static correlation)** 或[近简并](@entry_id:172107)性时，可能没有一个单一的 Slater [行列式](@entry_id:142978)能够很好地描述系统，这种情况被称为具有**多参考特性 (multi-reference character)**。

一个实用的衡量标准是 **$T_1$ 诊断**，通常定义为单激发振幅向量的[欧几里得范数](@entry_id:172687) ：

$D_{T_1} = \sqrt{\sum_{ia} |t_i^a|^2}$

在理想的单参考情况下，[Hartree-Fock](@entry_id:142303) 参考态已经很好地描述了[轨道](@entry_id:137151)，因此 $T_1$ 振幅应该很小（仅反映了小的[轨道弛豫](@entry_id:265723)效应）。一个大的 $D_{T_1}$ 值表明，从[参考态](@entry_id:151465)到真实[波函数](@entry_id:147440)需要进行显著的单粒子激发混合，这意味着 $|\Phi_0\rangle$ 本身并不是一个好的出发点。在实践中，大的 $T_1$ 诊断值是一个警示信号，表明单参考 CCSD 的结果可能不可靠，并且可能需要包含更高阶的激发（如三重激发，即 CCSDT）或使用真正的[多参考方法](@entry_id:170058)。这对于通过粒子附加或移除方案计算的开壳核尤为重要，因为其闭壳层母核的 $D_{T_1}$ 值会直接影响子核谱的可靠性 。

### 相似变换[哈密顿量](@entry_id:172864)

求解簇振幅 $t$ 和基态能量 $E_0$ 的[耦合簇](@entry_id:190682)方程，是通过将 Schrödinger 方程 $H|\Psi_0\rangle = E_0 |\Psi_0\rangle$ 左乘 $e^{-T}$ 得到的：

$e^{-T} H e^T |\Phi_0\rangle = E_0 |\Phi_0\rangle$

这自然地引出了**[相似变换](@entry_id:152935)[哈密顿量](@entry_id:172864)** $\bar{H}$：

$\bar{H} \equiv e^{-T} H e^T$

利用这个算符，[耦合簇](@entry_id:190682)方程可以更紧凑地写成：

$\bar{H} |\Phi_0\rangle = E_0 |\Phi_0\rangle$

然后通过投影到不同的激发组态空间上来求解能量和振幅。例如，[基态能量](@entry_id:263704)由投影到[参考态](@entry_id:151465)上得到：$E_0 = \langle \Phi_0 | \bar{H} | \Phi_0 \rangle$。

#### 非[厄米性](@entry_id:141899)及其推论

[相似变换](@entry_id:152935)[哈密顿量](@entry_id:172864) $\bar{H}$ 的一个至关重要的特性是，即使原始[哈密顿量](@entry_id:172864) $H$ 是厄米的，$\bar{H}$ 通常是**非厄米的** 。这是因为 $e^T$ 变换不是幺正变换。一个变换是幺正的，当且仅当其[厄米共轭](@entry_id:191215)等于其逆。对于 $e^T$ 来说，$(e^T)^\dagger = e^{T^\dagger}$，而其逆是 $e^{-T}$。[幺正性](@entry_id:138773)要求 $T^\dagger = -T$，即 $T$ 必须是反厄米的。然而，簇算符 $T$ 是一个纯激发算符，其共轭 $T^\dagger$ 是一个纯退激发算符，因此 $T$ 显然不是反厄米的。

$\bar{H}$ 的非[厄米性](@entry_id:141899)带来了几个深刻的后果：
1.  **实数谱**：尽管 $\bar{H}$ 非厄米，但它与[厄米算符](@entry_id:153410) $H$ 是相似的。线性代数的一个基本定理是相似变换保持本征谱不变。因此，在完备（未截断）的理论中，$\bar{H}$ 的[本征值](@entry_id:154894)与 $H$ 的[本征值](@entry_id:154894)完全相同，并且是实数。然而，在截断的近似计算中，可能会出现小的虚部，这通常是近似不足的信号 。
2.  **左右本征矢量**：非[厄米算符](@entry_id:153410)的左本征矢量和右本征矢量通常是不同的。这意味着我们需要求解两个独立的本征值问题，并采用**双正交 (biorthogonal)** 形式。
3.  **关联簇展开**：根据**关联簇定理 (linked-cluster theorem)**，$\bar{H}$ 的 Baker-Campbell-Hausdorff (BCH) 展开式 $\bar{H} = H + [H, T] + \frac{1}{2}[[H, T], T] + \dots$ 只包含**关联图 (connected diagrams)**。这意味着所有[非关联图](@entry_id:192455)（描述不相互作用的激发）都在代数上被精确消除了。这正是 CC 方法大小[广延性](@entry_id:144932)的根源 [@problem_id:3557965, 3558021]。$\bar{H}$ 的这种纯关联结构确保了能量计算的正确标度行为。

### 运动方程 (EOM) 形式

[EOM-CC](@entry_id:266204) 方法将[耦合簇理论](@entry_id:141746)从仅仅计算[基态](@entry_id:150928)扩展到了一个可以系统地计算[激发态](@entry_id:261453)和其他[量子态](@entry_id:146142)的强大框架。其核心思想是在已经很精确的 CC [基态](@entry_id:150928) $|\Psi_0\rangle = e^T |\Phi_0\rangle$ 之上，通过一个线性的激发算符 $R_k$ 来构建目标态 $|\Psi_k\rangle$：

$|\Psi_k\rangle = R_k |\Psi_0\rangle = R_k e^T |\Phi_0\rangle$

将此拟设代入 Schrödinger 方程 $H|\Psi_k\rangle = E_k |\Psi_k\rangle$，并左乘 $e^{-T}$，我们得到：

$e^{-T} H R_k e^T |\Phi_0\rangle = E_k R_k e^T |\Phi_0\rangle$

这个方程的形式并不直接明了。一个更标准的推导是注意到，[相似变换](@entry_id:152935)后的 Schrödinger 方程为 $\bar{H} |\Psi_k\rangle_{\text{eff}} = E_k |\Psi_k\rangle_{\text{eff}}$，其中有效[波函数](@entry_id:147440)为 $|\Psi_k\rangle_{\text{eff}} = e^{-T}|\Psi_k\rangle = R_k |\Phi_0\rangle$。因此，我们得到了 [EOM-CC](@entry_id:266204) 的核心[本征值问题](@entry_id:142153)：

$\bar{H} R_k |\Phi_0\rangle = E_k R_k |\Phi_0\rangle$

这个方程的物理意义是：在由 $R_k |\Phi_0\rangle$ 张成的激发组态空间中对角化非[厄米算符](@entry_id:153410) $\bar{H}$。我们通常更关心相对于[基态能量](@entry_id:263704) $E_0$ 的**激发能** $\omega_k = E_k - E_0$。通过将 $\bar{H}$ 替换为 $\bar{H}_N = \bar{H} - E_0$，我们可以得到直接求解激发能的本征方程 ：

$\bar{H}_N R_k |\Phi_0\rangle = \omega_k R_k |\Phi_0\rangle$

由于 $\bar{H}$ 的非[厄米性](@entry_id:141899)，存在一个相应的左[本征问题](@entry_id:748835) ：

$\langle \Phi_0 | L_k \bar{H}_N = \omega_k \langle \Phi_0 | L_k$

其中 $L_k$ 是左激发算符。左右本征矢量构成一个双[正交集](@entry_id:268255)，其[归一化条件](@entry_id:156486)为：

$\langle \Phi_0 | L_j R_k |\Phi_0 \rangle = \delta_{jk}$

这个双正交框架对于计算跃迁几率和其它[可观测量](@entry_id:267133)至关重要 。例如，算符 $O$ 的[期望值](@entry_id:153208)由 $\langle O \rangle = \langle \Psi_j^L | O | \Psi_k^R \rangle$ 给出，其中 $|\Psi_k^R\rangle = R_k e^T |\Phi_0\rangle$ 和 $\langle \Psi_j^L| = \langle\Phi_0| L_j e^{-T}$。

与 CC [基态能量](@entry_id:263704)的大小[广延性](@entry_id:144932)相对应，[EOM-CC](@entry_id:266204) 的激发能是**大小强度 (size-intensive)** 的，意味着一个局域激发能不依赖于系统中是否存在遥远的不相互作用的其他部分。这同样源于 $\bar{H}$ 的纯关联结构和可分离性 。

### 特定扇区的 EOM 算符

算符 $R_k$ 和 $L_k$ 的具体形式取决于我们想要描述的物理问题，即所谓的**扇区 (sector)**。

#### 中性激发 (EE-[EOM-CC](@entry_id:266204))

这是最常见的情况，用于计算与[基态](@entry_id:150928)具有相同粒子数的[激发态](@entry_id:261453)。在这种情况下，$R_k$ 是一个保持粒子数不变的[粒子-空穴激发](@entry_id:137289)算符。在 [EOM-CCSD](@entry_id:166585) 级别，它被截断为包含一个常数项 $r_0$（通常为零）、单激发项 $R_1$ 和双激发项 $R_2$ ：

$R_k = r_0 + R_1 + R_2 = r_0 + \sum_{ia} r_i^a(k) a_a^{\dagger} a_i + \frac{1}{4} \sum_{ijab} r_{ij}^{ab}(k) a_a^{\dagger} a_b^{\dagger} a_j a_i$

通过将本征方程投影到 $1p1h$ 和 $2p2h$ 组态空间，我们得到一个矩阵[本征值问题](@entry_id:142153)，其解为[激发能](@entry_id:190368) $\omega_k$ 和相应的振幅 $r(k)$。

#### 粒子附加 (PA-[EOM-CC](@entry_id:266204))

为了描述比参考态多一个[核子](@entry_id:158389)的系统（例如，从 $^{16}$O 计算 $^{17}$O），$R_k$ 算符必须使粒子数增加 1。在最低阶近似中，这包括附加一个粒子 ($1p$) 和附加两个粒子并移除一个空穴 ($2p1h$)。因此，在 [EOM-CCSD](@entry_id:166585)PA 级别，$R_k$ 的形式为 ：

$R_k^{\mathrm{PA}} = \sum_a r^a(k) a_a^{\dagger} + \frac{1}{2} \sum_{iab} r_i^{ab}(k) a_a^{\dagger} a_b^{\dagger} a_i$

注意 $2p1h$ 项中的组合因子 $\frac{1}{2}$，这是因为产生了两个等效的粒子。

#### 粒子移除 (PR-[EOM-CC](@entry_id:266204))

类似地，为了描述比参考态少一个[核子](@entry_id:158389)的系统（例如，从 $^{16}$O 计算 $^{15}$O），$R_k$ 算符必须使粒子数减少 1。这可以通过移除一个空穴 ($1h$) 或移除两个空穴并增加一个粒子 ($2h1p$) 来实现。在 [EOM-CCSD](@entry_id:166585)PR 级别，$R_k$ 的形式为 ：

$R_k^{\mathrm{PR}} = \sum_i r_i(k) a_i + \frac{1}{2} \sum_{ija} r_{ij}^a(k) a_a^{\dagger} a_j a_i$

这里，组合因子 $\frac{1}{2}$ 对应于湮灭了两个等效的空穴。

### [核物理](@entry_id:136661)中的实践考量

在将 [EOM-CC](@entry_id:266204) 应用于[原子核](@entry_id:167902)时，一个核心的挑战是处理**质心 (center-of-mass, CM) 运动**。

#### 内禀[哈密顿量](@entry_id:172864)

[核子](@entry_id:158389)间的相互作用应当是平移不变的，这意味着它们只依赖于相对坐标。然而，在实际计算中，我们通常使用一个固定的、局域化的单粒[子基](@entry_id:151637)，例如[谐振子基](@entry_id:750178)。这样的基破坏了[平移对称性](@entry_id:171614)。一个在固定原点周围构建的 Slater [行列式](@entry_id:142978)[参考态](@entry_id:151465) $|\Phi_0\rangle$ 不是[总动量](@entry_id:173071) $\mathbf{P}$ 的本征态，而是不同[质心动量](@entry_id:171180)的波包。

为了处理这个问题，第一步是使用**内禀[哈密顿量](@entry_id:172864) (intrinsic Hamiltonian)** $H_{\mathrm{int}}$。它通过从总[哈密顿量](@entry_id:172864) $H$ 中减去[质心](@entry_id:265015)动能 $T_{\mathrm{CM}}$ 得到 ：

$H_{\mathrm{int}} = H - T_{\mathrm{CM}} = H - \frac{\mathbf{P}^2}{2Am}$

其中 $A$ 是[质量数](@entry_id:142580)，$m$ 是[核子](@entry_id:158389)质量。在精确理论中，总[哈密顿量](@entry_id:172864)可以干净地分离为内禀部分和[质心](@entry_id:265015)部分 $H = H_{\mathrm{int}} + T_{\mathrm{CM}}$。在被截断的、破坏对称性的基中，直接对角化 $H$ 会导致物理的内禀激发与虚假的质心[激发态](@entry_id:261453)发生混合。通过使用 $H_{\mathrm{int}}$，我们从[哈密顿量](@entry_id:172864)层面抑制了这种虚假的[质心运动](@entry_id:178374)激发，从而得到一个更干净的内禀能谱。

#### [质心](@entry_id:265015)污染的诊断与缓解

然而，即使使用了 $H_{\mathrm{int}}$，基的截断本身仍然会导致计算出的[波函数](@entry_id:147440)中含有虚假的[质心](@entry_id:265015)激发成分，这被称为**质心污染 (center-of-mass contamination)**。因此，诊断和缓解这种污染至关重要。

一个有效的诊断方法是计算质心[哈密顿量](@entry_id:172864)算符的[期望值](@entry_id:153208)。在 [EOM-CC](@entry_id:266204) 的双正交框架下，这对应于计算 ：

$\langle H_{\mathrm{cm}} \rangle_k = \langle \Phi_0 | L_k \bar{H}_{\mathrm{cm}} R_k |\Phi_0 \rangle$

对于一个理想的、无污染的[基态](@entry_id:150928)（$N_{\mathrm{cm}}=0$ 的质心[振动](@entry_id:267781)），这个[期望值](@entry_id:153208)应该是 $\frac{3}{2}\hbar\Omega$（在使用[谐振子基](@entry_id:750178)的情况下）。任何显著的偏离都表明存在[质心](@entry_id:265015)污染。

一种强大的缓解策略是**Lawson 方法**。该方法通过在[哈密顿量](@entry_id:172864)中增加一个惩罚项来将虚假的质心[激发态](@entry_id:261453)推向高能区，从而使其与我们感兴趣的低能物理态[解耦](@entry_id:637294)。修改后的[哈密顿量](@entry_id:172864)为：

$H' = H_{\mathrm{int}} + \beta H_{\mathrm{cm}}$

其中 $\beta$ 是一个正常数。参数 $\beta$ 越大，对[质心](@entry_id:265015)激发的能量惩罚就越强。一个稳健的计算应该表现出其物理可观测量（如内禀激发能）对 $\beta$ 和基参数（如 $\hbar\Omega$）的取值不敏感 。通过监控[质心](@entry_id:265015)诊断值并结合 Lawson 方法，可以在有限的计算资源下获得可靠的核结构结果。