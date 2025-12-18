## 引言
在量子世界中，系统的状态并非总是纯粹的。当我们研究一个与广阔环境交换能量与信息的[开放系统](@entry_id:147845)，或者当我们对系统的知识不完备时，我们必须使用[混合态](@entry_id:141568)和密度算符来描述它。混合态的出现似乎引入了经典概率的模糊性，掩盖了量子系统内在的相[干性](@entry_id:900268)。然而，“纯化”这一深刻概念提供了一个革命性的视角：任何[混合态](@entry_id:141568)都并非是内禀的，而是我们观察局限性的结果。它揭示了任何混合态都可以被看作一个更大、更完整的孤立系统中所处纯态的一部分。

本文旨在系统性地阐述混合态纯化的理论及其广泛应用。我们首先将在“原理与机制”一章中，深入探讨纯化的数学构造、其与[施密特分解](@entry_id:145934)的内在联系，以及其表示的自由度。接着，在“应用与跨学科关联”一章中，我们将展示纯化思想如何成为连接量子信息、开放[系统动力学](@entry_id:136288)、[测量理论](@entry_id:153616)、[量子热力学](@entry_id:140152)乃至多体物理等前沿领域的关键桥梁。最后，通过“动手实践”部分，读者将有机会亲手应用这些概念，加深对这一强大工具的理解。通过本次学习，您将掌握一种将复杂混合态问题转化为更简洁[纯态](@entry_id:141688)问题的思维方式，为深入研究量子物理的诸多分支奠定坚实的基础。

## 原理与机制

在量子力学中，一个[孤立系统](@entry_id:159201)可以用其希尔伯特空间中的一个纯态向量来完备地描述。然而，当我们考虑一个与环境相互作用的[开放系统](@entry_id:147845)，或者我们对系统的知识不完备时，系统的状态通常由[密度算符](@entry_id:138151) $\rho_S$ 描述，这是一个[混合态](@entry_id:141568)。[混合态](@entry_id:141568)的概念引入了经典概率的不确定性，掩盖了潜在的量子相干性。**纯化 (Purification)** 是一种极其深刻且强大的观念，它允许我们将任何[混合态](@entry_id:141568)“提升”为一个更[大系统](@entry_id:166848)中的[纯态](@entry_id:141688)。这个过程不仅是一个数学技巧，更是一种根本性的视角，它揭示了[混合态](@entry_id:141568)、[量子纠缠](@entry_id:136576)和开放[系统动力学](@entry_id:136288)之间密不可分的联系。本章将深入探讨纯化的基本原理及其在量子信息、[测量理论](@entry_id:153616)和[量子热力学](@entry_id:140152)中的核心机制。

### 纯化的基本原理

#### 纯化的概念

考虑一个量子系统 $S$，其状态由希尔伯特空间 $\mathcal{H}_S$ 上的密度算符 $\rho_S$ 描述。如果 $\rho_S$ 是一个混合态，我们总可以引入一个[辅助系统](@entry_id:142219)（或称“环境”）$A$，其[希尔伯特空间](@entry_id:261193)为 $\mathcal{H}_A$，并构建一个复合系统 $S+A$ 上的**[纯态](@entry_id:141688)** $|\Psi\rangle_{SA} \in \mathcal{H}_S \otimes \mathcal{H}_A$。如果这个[纯态](@entry_id:141688) $|\Psi\rangle_{SA}$ 满足以下条件，即对辅助系统 $A$ 取[偏迹](@entry_id:146482)（partial trace）后可以恢复系统 $S$ 的原始混合态，那么 $|\Psi\rangle_{SA}$ 就被称为 $\rho_S$ 的一个**纯化**：

$$
\rho_S = \mathrm{Tr}_A \left( |\Psi\rangle_{SA}\langle\Psi|_{SA} \right)
$$

这个定义意味着，系统 $S$ 的混合性可以被理解为其与另一个系统 $A$ 之间存在[量子纠缠](@entry_id:136576)的结果。所有关于 $S$ 处于[混合态](@entry_id:141568)的不确定性，都被归因于我们忽略了系统 $A$ 的自由度。从这个角度看，宇宙的整体状态可能是纯的，而我们观察到的局部混合态，仅仅是因为我们未能接触到与之纠缠的全部环境。

#### 存在性与构造：[施密特分解](@entry_id:145934)的视角

任何给定的混合态 $\rho_S$ 都存在纯化，并且构造方法十分直接，这与[施密特分解](@entry_id:145934)（Schmidt decomposition）密切相关。根据[谱定理](@entry_id:136620)，任何[密度算符](@entry_id:138151) $\rho_S$ 都可以被[对角化](@entry_id:147016)：

$$
\rho_S = \sum_{i=1}^{r} \lambda_i |s_i\rangle\langle s_i|
$$

其中 $\lambda_i > 0$ 是 $\rho_S$ 的非零本征值，满足 $\sum_i \lambda_i = 1$，$r = \mathrm{rank}(\rho_S)$ 是 $\rho_S$ 的秩，而 $\{|s_i\rangle\}$ 是对应于这些本征值的正交归一的[本征向量](@entry_id:151813)集合。

基于此[谱分解](@entry_id:173707)，我们可以立即构造一个纯化。为此，我们引入一个[辅助系统](@entry_id:142219) $A$，其[希尔伯特空间](@entry_id:261193) $\mathcal{H}_A$ 的维度至少为 $r$。我们可以在 $\mathcal{H}_A$ 中选取一个包含 $r$ 个正交归一向量的集合 $\{|a_i\rangle\}_{i=1}^r$。然后，可以定义如下的[纯态](@entry_id:141688) $|\Psi\rangle_{SA}$：

$$
|\Psi\rangle_{SA} = \sum_{i=1}^{r} \sqrt{\lambda_i} |s_i\rangle \otimes |a_i\rangle
$$

通过计算该[纯态](@entry_id:141688)对系统 $A$ 的[偏迹](@entry_id:146482)，我们可以验证它确实是 $\rho_S$ 的一个纯化：

$$
\mathrm{Tr}_A \left( |\Psi\rangle_{SA}\langle\Psi|_{SA} \right) = \mathrm{Tr}_A \left( \sum_{i,j=1}^{r} \sqrt{\lambda_i \lambda_j} |s_i\rangle\langle s_j| \otimes |a_i\rangle\langle a_j| \right) = \sum_{i,j=1}^{r} \sqrt{\lambda_i \lambda_j} |s_i\rangle\langle s_j| \mathrm{Tr}(|a_i\rangle\langle a_j|)
$$

由于 $\{|a_i\rangle\}$ 是正交归一的，$\mathrm{Tr}(|a_i\rangle\langle a_j|) = \langle a_j|a_i\rangle = \delta_{ij}$。因此，上式简化为：

$$
\rho_S = \sum_{i=1}^{r} \lambda_i |s_i\rangle\langle s_i|
$$

这正是 $\rho_S$ 的[谱分解](@entry_id:173707)。值得注意的是，上述构造的纯化形式 $|\Psi\rangle_{SA} = \sum_{i} \sqrt{\lambda_i} |s_i\rangle \otimes |a_i\rangle$ 正是复合系统[纯态](@entry_id:141688)的[施密特分解](@entry_id:145934)形式。这揭示了一个至关重要的联系：**一个混合态 $\rho_S$ 的非零本征值集合 $\{ \lambda_i \}$，与其任何[纯化态](@entry_id:137734) $|\Psi\rangle_{SA}$ 的[施密特系数](@entry_id:137823)的平方集合 $\{ s_k^2 \}$ 是完全相同的**。因此，$\rho_S$ 的谱的简并度模式也完全决定了其[纯化态](@entry_id:137734)[施密特系数](@entry_id:137823)的简并度模式。例如，如果一个秩为 3 的态 $\rho_S$ 的本征值为 $\{\frac{1}{2}, \frac{1}{4}, \frac{1}{4}\}$，那么它的任何[纯化态](@entry_id:137734)的非零[施密特系数](@entry_id:137823)必然是 $\{\sqrt{\frac{1}{2}}, \sqrt{\frac{1}{4}}, \sqrt{\frac{1}{4}}\}$ ()。

#### 最小辅助维度与秩

从上述构造中可以清楚地看到，为了构造一个包含 $r$ 个正交归一向量的集合 $\{|a_i\rangle\}$，[辅助系统](@entry_id:142219) $A$ 的希尔伯特空间维度 $d_A$ 必须至少为 $r$。因此，**纯化一个秩为 $r$ 的[混合态](@entry_id:141568)所需的最小辅助系统维度等于 $r$**。如果选择的辅助系统维度 $d_A > r$，我们仍然可以构造纯化，但这并不会改变[纯化态](@entry_id:137734)的[施密特秩](@entry_id:154893)，该值仍然是 $r$。多余的维度仅仅意味着[辅助系统](@entry_id:142219)的施密特基矢 $\{|a_i\rangle\}$ 张成的是 $\mathcal{H}_A$ 的一个 $r$ 维子空间。任何超出此范围的[施密特系数](@entry_id:137823)都将为零 ()。

#### 纯化的自由度

纯化并非唯一。对于给定的混合态 $\rho_S$，存在无穷多个不同的纯态 $|\Psi\rangle_{SA}$ 都能作为其纯化。这种不唯一性可以用一个称为 **休斯顿-约萨-伍特斯 (Hughston-Jozsa-Wootters, HJW) 定理** 的基本结果来精确刻画。该定理指出，如果 $|\Psi\rangle_{SA}$ 和 $|\Phi\rangle_{SA'}$ 是同一[混合态](@entry_id:141568) $\rho_S$ 的两个纯化，那么它们之间必然通过一个作用在[辅助系统](@entry_id:142219)上的[局部等距](@entry_id:158618)算符（isometry）相关联。如果两个纯化都使用了最小维度（即 $d_A = d_{A'} = \mathrm{rank}(\rho_S)$），那么这个等距算符就是一个酉算符（unitary operator） $W_A$：

$$
|\Phi\rangle_{SA} = (\mathbb{I}_S \otimes W_A) |\Psi\rangle_{SA}
$$

这里的 $\mathbb{I}_S$ 是系统 $S$ 上的恒等算符。这个定理的本质是，在不改变系统 $S$ 的[约化密度矩阵](@entry_id:146315)的前提下，我们可以在[辅助系统](@entry_id:142219) $A$ 上自由地进行任何[酉变换](@entry_id:152599)。这种自由度可以看作是对[辅助系统](@entry_id:142219)基矢的“重新标记” (, )。

一个关键的推论是，这种**纯化的自由度不会改变系统 $S$ 和 $A$ 之间的纠缠度**。纠缠度是由[施密特系数](@entry_id:137823)的分布决定的，例如通过[冯·诺依曼熵](@entry_id:143216) $S(\rho_S) = -\sum_i \lambda_i \ln \lambda_i$ 来量化。由于局部[酉变换](@entry_id:152599) $W_A$ 不会改变[施密特系数](@entry_id:137823) $\sqrt{\lambda_i}$，因此系统的[纠缠熵](@entry_id:140818) $S(\rho_S)$ 以及任何其他仅依赖于[纠缠谱](@entry_id:138110) $\{\lambda_i\}$ 的[纠缠度量](@entry_id:139894)，在纯化的酉自由度下都是不变量。例如，对[纯化态](@entry_id:137734) $|\Psi\rangle = \sum_k \sqrt{\lambda_k} |s_k\rangle \otimes |a_k\rangle$ 施加一个局部酉算符 $U_S \otimes V_A$，会得到新态 $|\Psi'\rangle = \sum_k \sqrt{\lambda_k} (U_S|s_k\rangle) \otimes (V_A|a_k\rangle)$。由于 $\{U_S|s_k\rangle\}$ 和 $\{V_A|a_k\rangle\}$ 仍然是正交归一基，这正是 $|\Psi'\rangle$ 的[施密特分解](@entry_id:145934)，其[施密特系数](@entry_id:137823) $\sqrt{\lambda_k}$ 保持不变 ()。因此，我们无法通过只在系统 $S$ 上进行测量来区分使用了哪种纯化表示。

### 纯化的机制与应用

纯化不仅是一个理论构造，它还在[量子信息处理](@entry_id:158111)、[动力学建模](@entry_id:204326)和[测量理论](@entry_id:153616)中扮演着核心角色。

#### 通过辅助系统测量实现[状态制备](@entry_id:152204)

纯化提供了一种通过测量来远程“操控”（steer）量子系统状态的机制。假设我们已经制备了系统 $S$ 的一个[纯化态](@entry_id:137734) $|\Psi\rangle_{SA}$。如果我们现在只对辅助系统 $A$ 进行测量，那么根据测量结果，系统 $S$ 的状态将会被概率性地投影到一个新的、通常是纯的态上。

让我们通过一个具体的例子来理解这个过程 ()。设初始[纯化态](@entry_id:137734)为 $|\Psi\rangle = \sum_{i,\mu} C_{i\mu} |i\rangle_S \otimes |\mu\rangle_A$。我们对辅助系统 $A$ 进行一个投影测量，测量算符为 $\{\Pi_A, \mathbb{I}_A - \Pi_A\}$，其中 $\Pi_A = |\phi\rangle_A\langle\phi|_A$ 是一个秩为 1 的[投影算符](@entry_id:154142)，对应于测量到归一化态 $|\phi\rangle_A$。

根据[玻恩定则](@entry_id:154470)，测量到结果 $\Pi_A$ 的概率 $p$ 是：
$$
p = \mathrm{Tr}_{SA} \left( (\mathbb{I}_S \otimes \Pi_A) |\Psi\rangle\langle\Psi| \right) = \langle\Psi| (\mathbb{I}_S \otimes \Pi_A) |\Psi\rangle
$$
计算结果表明，这个概率为 $p = \sum_{i} \left| \sum_{\mu} C_{i\mu} \langle\phi|\mu\rangle_A \right|^2$。

根据吕德斯态更新规则（Lüders state-update rule），在得到结果 $\Pi_A$ 的条件下，复合系统的后验态是：
$$
\rho'_{SA} = \frac{(\mathbb{I}_S \otimes \Pi_A) |\Psi\rangle\langle\Psi| (\mathbb{I}_S \otimes \Pi_A)^\dagger}{p}
$$
经过计算，这个后验态可以写成一个乘积态的形式：$|\psi_S^{\text{final}}\rangle\langle\psi_S^{\text{final}}| \otimes |\phi\rangle_A\langle\phi|_A$。其中 $|\psi_S^{\text{final}}\rangle$ 是一个归一化的纯态，由下式给出：
$$
|\psi_S^{\text{final}}\rangle = \frac{1}{\sqrt{p}} \sum_{i} \left( \sum_{\mu} C_{i\mu} \langle\phi|\mu\rangle_A \right) |i\rangle_S
$$
对这个后验态取关于 $A$ 的[偏迹](@entry_id:146482)，我们得到系统 $S$ 的最终状态 $\rho'_S = |\psi_S^{\text{final}}\rangle\langle\psi_S^{\text{final}}|$。这表明，通过在辅助系统上进行投影测量并[后选择](@entry_id:154665)特定结果，我们成功地将系统 $S$ 制备到了一个纯态上。这个过程是[量子信息处理](@entry_id:158111)中实现远程[状态制备](@entry_id:152204)和量子操控的基础。

#### 纯化与开放系统：[Stinespring 扩张](@entry_id:1132403)

纯化的概念在描述开放量子系统动力学时达到了其理论的顶峰。一个系统的演化，如果由于与环境的相互作用而变得非酉，其动力学过程可以用一个完全正定保迹（Completely Positive Trace-Preserving, CPTP）映射 $\mathcal{E}$ 来描述。**[Stinespring 扩张定理](@entry_id:138524) (Stinespring Dilation Theorem)** 保证，任何这样的 CPTP 映射都可以被“扩张”或“纯化”为一个在更[大系统](@entry_id:166848)（系统+环境）上的[酉演化](@entry_id:145020) ()。

具体来说，对于任何作用在 $\mathcal{H}_S$ 上的 CPTP 映射 $\mathcal{E}$，总存在一个环境[希尔伯特空间](@entry_id:261193) $\mathcal{H}_E$，一个固定的初始环境纯态 $|0\rangle_E$，以及一个在 $\mathcal{H}_S \otimes \mathcal{H}_E$ 上的酉算符 $U_{SE}$，使得对于任何系统初态 $\rho_S$，其演化后的状态可以表示为：
$$
\mathcal{E}(\rho_S) = \mathrm{Tr}_E \left[ U_{SE} (\rho_S \otimes |0\rangle_E\langle 0|_E) U_{SE}^\dagger \right]
$$
这个定理意味着，任何看似复杂的非[酉演化](@entry_id:145020)和退相干过程，都可以被看作是一个更大的封闭系统进行标准酉演化的结果，我们只是忽略了环境部分。这为[开放系统](@entry_id:147845)提供了一个清晰的物理图像。

[Stinespring 扩张](@entry_id:1132403)还与另一种描述量子通道的方式——**[克劳斯表示](@entry_id:138071) (Kraus representation)** 紧密相连。通过在环境[希尔伯特空间](@entry_id:261193) $\mathcal{H}_E$ 中选择一个正交归一基 $\{|k\rangle_E\}$，我们可以将映射 $\mathcal{E}$ 写成算符和形式：
$$
\mathcal{E}(\rho_S) = \sum_k K_k \rho_S K_k^\dagger, \quad \text{其中} \quad K_k = \langle k|_E U_{SE} |0\rangle_E
$$
这里的 $\{K_k\}$ 就是[克劳斯算符](@entry_id:144882)。纯化中的酉自由度在此体现为[克劳斯表示](@entry_id:138071)的自由度。选择不同的环境测量基 $\{|k\rangle_E\}$（这等价于对环境施加一个[酉变换](@entry_id:152599)），会得到一组新的、通过[酉矩阵](@entry_id:138978)混合的[克劳斯算符](@entry_id:144882)，但它们描述的是完全相同的 CPTP 映射 $\mathcal{E}$ ()。

这种自由度具有深刻的物理含义。不同的[克劳斯表示](@entry_id:138071)对应于对环境进行不同方式的连续测量，从而产生不同的**量子轨迹 (quantum trajectories)**。虽然每条轨迹（系统状态的随机演化路径）都不同，但所有轨迹的系综平均结果总是恢复为由 CPTP 映射 $\mathcal{E}$ 描述的确定性主方程演化。因此，所有依赖于系综平均的物理量（如平均能量、平均熵）在这种表示自由度下保持不变，但依赖于单次测量结果的轨迹层面的量（如随机热交换）则会依赖于测量基的选择 (, )。

#### 纯化与[测量理论](@entry_id:153616)：Naimark 扩张

纯化的思想同样可以应用于理解[量子测量](@entry_id:272490)的本质。一个[广义测量](@entry_id:154280)（由一组正定算符值测量 POVM 元素 $\{E_m\}$ 描述）可以通过 **Naimark [扩张定理](@entry_id:139304) (Naimark's Dilation Theorem)** 被建模。该定理表明，任何在系统 $S$ 上的 POVM 都可以通过引入一个辅助的“测量仪器”系统 $A$，让 $S$ 和 $A$ 发生一次酉相互作用，然后对仪器 $A$ 进行标准投影测量来实现 ()。

在这个模型中，仪器的初始状态 $\rho_A$ 至关重要。如果仪器初始处于一个[纯态](@entry_id:141688)，测量过程对系统的反作用（back-action）通常更具相[干性](@entry_id:900268)。如果仪器初始处于一个[混合态](@entry_id:141568)，例如[完全混合态](@entry_id:139247) $\rho_A = \mathbb{I}_A / d_A$，测量过程可能会变得非常“嘈杂”。我们可以通过一个具体的例子来阐明这一点。考虑一个 CNOT 门 $U = \mathrm{CNOT}_{S \to A}$ 作为系统与仪器的相互作用。

-   **纯仪器态**: 如果仪器初态为 $|0\rangle_A$，计算表明，在仪器上测量到 $|0\rangle_A$ 或 $|1\rangle_A$ 分别对应于将系统 $S$ 投影到 $|0\rangle_S$ 或 $|1\rangle_S$。这实现了一个对系统 $S$ 的标准投影测量。
-   **混合仪器态**: 如果仪器初态为[完全混合态](@entry_id:139247) $\mathbb{I}_A/2$，计算表明，无论在仪器上测量到什么结果，系统 $S$ 的后验态都会变成一个完全退相干的态（密度矩阵的非对角元被抹除），而且测量结果的概率与系统初态无关。这种情况下，我们没有从测量中获得任何关于系统初态相[干性](@entry_id:900268)的信息，但测量过程本身却破坏了系统的相[干性](@entry_id:900268)。

从纯化的角度看，一个混合的仪器态 $\rho_A$ 可以被看作是一个更大的“仪器+环境”复合系统上某个[纯态](@entry_id:141688)的约化态。然而，这种形式上的“纯化”只是一个数学工具，它并不会改变对系统 $S$ 的有效测量过程。由混合仪器导致的退相干效应是真实存在的，并不能通过这种数学重构来消除 ()。

### 纯化在[量子热力学](@entry_id:140152)与多体物理中的应用

#### [热场双态](@entry_id:144349)：纯化热力学态

在[量子统计力学](@entry_id:140244)和量子热力学中，与温度为 $\beta^{-1}$ 的[热库](@entry_id:143608)平衡的系统处于吉布斯态（Gibbs state）$\rho(\beta) = \exp(-\beta H) / Z(\beta)$，这是一个典型的混合态。**[热场双态](@entry_id:144349) (Thermofield Double, TFD)** 是吉布斯态的一个非常重要的规范纯化。

对于一个具有[哈密顿量](@entry_id:144286) $H = \sum_n E_n |n\rangle\langle n|$ 的系统，其[热场双态](@entry_id:144349)定义在两个相同的希尔伯特空间 $\mathcal{H}_A \otimes \mathcal{H}_B$ 上：
$$
|{\rm TFD}(\beta)\rangle \equiv \frac{1}{\sqrt{Z(\beta)}} \sum_{n} e^{-\beta E_n / 2} |n\rangle_A \otimes |n\rangle_B
$$
其中 $Z(\beta) = \sum_n e^{-\beta E_n}$ 是[配分函数](@entry_id:140048)。通过对系统 $B$ 取[偏迹](@entry_id:146482)，可以验证系统 $A$ 的[约化密度矩阵](@entry_id:146315)恰好是吉布斯态 $\rho_A(\beta) = \rho(\beta)$。

[热场双态](@entry_id:144349)最引人注目的性质之一是它在纠缠与[热力学熵](@entry_id:155885)之间建立的深刻联系。通过计算约化态 $\rho_A(\beta)$ 的[冯·诺依曼熵](@entry_id:143216)，我们会发现它恰好等于原始吉布斯态的[热力学熵](@entry_id:155885) $S(\rho(\beta))$ ()。
$$
S(\rho_A(\beta)) = -\mathrm{Tr}[\rho_A \ln \rho_A] = S(\rho(\beta))
$$
这意味着，一个系统的[热力学熵](@entry_id:155885)，可以被等同地看作是其热场双纯化中两个子系统之间的[纠缠熵](@entry_id:140818)。这个结果是 AdS/CFT 对偶等前沿物理领域中的一个基石，它暗示了[引力](@entry_id:189550)、[时空几何](@entry_id:139497)与[量子纠缠](@entry_id:136576)之间的深层联系。

#### 信息论视角：[条件熵](@entry_id:136761)与[相干信息](@entry_id:147583)

纯化过程从信息论的角度看，是系统与辅助系统之间建立关联的过程。我们可以用**[条件熵](@entry_id:136761) (conditional entropy)** $S(S|A) = S(\rho_{SA}) - S(\rho_A)$ 来量化这种关联。

-   在纯化之前，系统 $S$ 和辅助系统 $A$ 处于不相关的乘积态 $\rho_{SA} = \rho_S \otimes \rho_A$。此时，[联合熵](@entry_id:262683)等于熵之和，$S(\rho_{SA}) = S(\rho_S) + S(\rho_A)$，因此[条件熵](@entry_id:136761) $S(S|A) = S(\rho_S) \ge 0$。非负的[条件熵](@entry_id:136761)反映了[经典关联](@entry_id:136367)的特征。

-   在纯化之后，复合系统处于纯态 $|\Psi\rangle_{SA}$，其[联合熵](@entry_id:262683) $S(\rho_{SA}) = 0$。由于纠缠，约化态 $\rho_S$ 和 $\rho_A$ 具有相同的非零熵，$S(\rho_S) = S(\rho_A)$。此时[条件熵](@entry_id:136761)变为 $S(S|A) = 0 - S(\rho_A) = -S(\rho_S) \le 0$ ()。

[条件熵](@entry_id:136761)从非负变为非正，是[量子纠缠](@entry_id:136576)建立的标志。负的[条件熵](@entry_id:136761)意味着，由于 $S$ 和 $A$ 之间的[量子关联](@entry_id:136327)，我们对复合系统 $SA$ 的知识（熵为0）比我们对其中一个子系统 $A$ 的知识（熵为 $S(\rho_A) > 0$）还要确定。这个差值由**[相干信息](@entry_id:147583) (coherent information)** $I(S\rangle A) = -S(S|A)$ 来度量。对于[纯化态](@entry_id:137734)， $I(S\rangle A) = S(\rho_S)$，它量化了可以从 $S$ 发送到持有 $A$ 的另一方的量子信息量。

#### [多体系统](@entry_id:144006)中的近似纯化

在处理由大量粒子组成的[多体量子系统](@entry_id:161678)时，希尔伯特空间的维度随粒子数指数增长。一个典型的多体混合态（如有限温度下的吉布斯态）的秩可能非常大，这意味着其精确纯化需要一个同样巨大的[辅助系统](@entry_id:142219)，这在理论分析和[数值模拟](@entry_id:146043)中都是不现实的。

因此，**近似纯化 (approximate purification)** 的概念变得至关重要 ()。其核心思想是，在可控的[误差范围](@entry_id:169950)内，用一个秩较低的态来近似原始的混合态。一个非常有效且最优的策略是保留原始[密度矩阵](@entry_id:139892) $\rho$ 中最大的 $k$ 个本征值，并舍弃其余部分。具体来说，给定 $\rho = \sum_{i=1}^d \lambda_i |\psi_i\rangle\langle\psi_i|$（其中 $\lambda_1 \ge \lambda_2 \ge \dots$），我们构造一个秩为 $k$ 的近似态：
$$
\sigma_k = \frac{1}{\sum_{i=1}^k \lambda_i} \sum_{i=1}^k \lambda_i |\psi_i\rangle\langle\psi_i|
$$
这个态 $\sigma_k$ 只需一个维度为 $k$ 的[辅助系统](@entry_id:142219)即可纯化。近似的误差可以用[迹距离](@entry_id:142668) $D(\rho, \sigma_k)$ 来衡量。一个简洁而重要的结果是，这种近似策略的误差恰好等于被舍弃的本征值之和：
$$
D(\rho, \sigma_k) = \sum_{i=k+1}^d \lambda_i
$$
这个结果不仅给出了一个明确的误差估计，还揭示了这种近似策略在迹距离度量下是最优的。这意味着，对于任何给定的辅助维度 $k$，不可能找到比 $\sigma_k$ 更好的秩为 $k$ 的近似态。这个原理构成了现代[张量网络算法](@entry_id:755855)（如[密度矩阵重整化群](@entry_id:137826) DMRG 和[矩阵乘积态](@entry_id:143296) MPS）的理论基础，这些算法通过智能地截断[纠缠谱](@entry_id:138110)来实现对多体量子态的高效表示和模拟。