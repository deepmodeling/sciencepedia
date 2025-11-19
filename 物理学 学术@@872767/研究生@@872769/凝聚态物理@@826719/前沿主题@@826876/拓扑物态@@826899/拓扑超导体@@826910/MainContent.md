## 引言
拓扑[超导体](@entry_id:191025)是凝聚态物理学前沿的一类新型量子[物态](@entry_id:139436)，它将[超导体](@entry_id:191025)的宏观量子相干性与物质的[拓扑性质](@entry_id:141605)巧妙地结合起来，预示着一系列奇异的物理现象和革命性的技术应用。其中，最引人注目的便是其边界上存在的[马约拉纳费米子](@entry_id:137199)——一种自身即是其反粒子的神秘粒子，它为构建[容错量子计算机](@entry_id:141244)提供了理论基石。然而，理解这种复杂量子相的内在原理、如何在现实世界中创造并验证它们，是该领域面临的核心挑战。本文旨在系统性地回答这些问题，为读者铺设一条从基础理论到前沿应用的清晰路径。

在接下来的内容中，我们将分三个章节逐步深入。首先，在“原理与机制”一章，我们将建立描述拓扑超导的核心理论框架，即 Bogoliubov-de Gennes (BdG) 形式主义，并探讨[对称性分类](@entry_id:184862)、[拓扑不变量](@entry_id:138526)以及连接体态与边界[马约拉纳模](@entry_id:200998)的[体边对应](@entry_id:146387)原理。随后，“应用与跨学科交叉”一章将把理论与实践联系起来，展示如何通过“拓扑[量子工程](@entry_id:146874)”在实验中构筑拓扑[超导体](@entry_id:191025)，介绍探测[马约拉纳模](@entry_id:200998)的标志性实验证据，并探索其与高阶拓扑、[量子场论](@entry_id:138177)等领域的深刻联系，最终聚焦于其在拓扑量子计算中的核心角色。最后，通过“动手实践”部分提供的具体计算问题，读者将有机会亲手演练关键概念，从而将理论知识内化为解决实际问题的能力。

## 原理与机制

在引言章节中，我们概述了拓扑[超导体](@entry_id:191025)的基本概念及其在[容错量子计算](@entry_id:142498)中的潜在应用。本章将深入探讨支撑这一迷人物质相的数学和物理原理。我们将从平均场描述出发，建立 [Bogoliubov-de Gennes (BdG) 哈密顿量](@entry_id:136941)这一核心理论框架。接着，我们将系统地分析其对称性，并以此为基础对拓扑[超导体](@entry_id:191025)进行分类。随后，我们将引入拓扑不变量，这是区分不同[拓扑相](@entry_id:141674)的关键量。最后，我们将阐述[体边对应](@entry_id:146387)原理，揭示体[拓扑性质](@entry_id:141605)与边界上奇异的马约拉纳费米子之间的深刻联系。

### Bogoliubov-de Gennes 形式主义

超导的微观理论始于一个包含电子间吸引相互作用的系统。在 Bardeen-Cooper-Schrieffer (BCS) 理论的平均场近似中，这种相互作用导致了动量为 $\mathbf{k}$ 和 $-\mathbf{k}$ 的电子配对形成[库珀对](@entry_id:143370)。为了处理这种既包含单粒子激发又包含库珀对产生的复杂多体问题，Bogoliubov-de Gennes (BdG) 形式主义应运而生。其核心思想是通过引入粒子-空穴自由度来倍增希尔伯特空间，从而将问题转化为一个可对角化的二次型[哈密顿量](@entry_id:172864)。

#### Nambu 旋量与 BdG [哈密顿量](@entry_id:172864)

考虑一个平移不变的单带自旋无色[费米子](@entry_id:146235)体系。其[平均场哈密顿量](@entry_id:751814)可以写作：
$$ H_{\mathrm{MF}} = \sum_{\mathbf{k}} \xi_{\mathbf{k}} c_{\mathbf{k}}^{\dagger} c_{\mathbf{k}} + \sum_{\mathbf{k}} \left( \Delta_{\mathbf{k}} c_{\mathbf{k}}^{\dagger} c_{-\mathbf{k}}^{\dagger} + \Delta_{\mathbf{k}}^* c_{-\mathbf{k}} c_{\mathbf{k}} \right) $$
其中，$c_{\mathbf{k}}^{\dagger}$ ($c_{\mathbf{k}}$) 是动量为 $\mathbf{k}$ 的[费米子](@entry_id:146235)的产生（湮灭）算符，$\xi_{\mathbf{k}} = \epsilon_{\mathbf{k}} - \mu$ 是相对于化学势 $\mu$ 的单粒子[色散](@entry_id:263750)，而 $\Delta_{\mathbf{k}}$ 是动量依赖的配对振幅或超导能隙函数。

这个[哈密顿量](@entry_id:172864)混合了粒子算符 $c_{\mathbf{k}}$ 和空穴算符 $c_{-\mathbf{k}}^{\dagger}$。为了使其结构更清晰，我们引入 **Nambu 旋量** [@problem_id:3022218]：
$$ \Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}} \\ c_{-\mathbf{k}}^{\dagger} \end{pmatrix} $$
Nambu [旋量](@entry_id:158054)的上半部分是粒子[湮灭算符](@entry_id:165390)，下半部分是空穴[产生算符](@entry_id:191512)。利用这个旋量，整个[平均场哈密顿量](@entry_id:751814)可以被重写为一个紧凑的二次型：
$$ H_{\mathrm{MF}} = \frac{1}{2}\sum_{\mathbf{k}} \Psi_{\mathbf{k}}^{\dagger} H_{\mathrm{BdG}}(\mathbf{k}) \Psi_{\mathbf{k}} + \text{常数} $$
这里的 $H_{\mathrm{BdG}}(\mathbf{k})$ 就是 **[Bogoliubov-de Gennes (BdG) 哈密顿量](@entry_id:136941)**。通过仔细地重新组合 $H_{\mathrm{MF}}$ 中的各项并利用[费米子](@entry_id:146235)[反对易关系](@entry_id:153815)，可以推导出 $H_{\mathrm{BdG}}(\mathbf{k})$ 的矩阵形式 [@problem_id:3022218]：
$$ H_{\mathrm{BdG}}(\mathbf{k}) = \begin{pmatrix} \xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^{\ast} & -\xi_{-\mathbf{k}} \end{pmatrix} $$
这个 $2 \times 2$ 矩阵作用在由粒子和空穴组成的 Nambu 空间上。让我们剖析这个[哈密顿量](@entry_id:172864)的结构：
1.  **对角项**: $\xi_{\mathbf{k}}$ 代表动量为 $\mathbf{k}$ 的粒子的能量。$-\xi_{-\mathbf{k}}$ 代表动量为 $-\mathbf{k}$ 的空穴的能量。值得注意的是，除非体系的正常态具有额外的对称性（如空间反演或[时间反演对称性](@entry_id:138094)），否则一般情况下 $\xi_{\mathbf{k}} \neq \xi_{-\mathbf{k}}$。因此，保留 $-\xi_{-\mathbf{k}}$ 的形式至关重要。
2.  **非对角项**: $\Delta_{\mathbf{k}}$ 和 $\Delta_{\mathbf{k}}^{\ast}$ 描述了粒子和空穴之间的转换，即库珀对的产生和湮灭。[哈密顿量](@entry_id:172864)的[厄米性](@entry_id:141899)要求右下角元为左上角元的[复共轭](@entry_id:174690)。
3.  **[费米子统计](@entry_id:148436)**: [泡利不相容原理](@entry_id:141850)要求两个全同[费米子](@entry_id:146235)的总[波函数](@entry_id:147440)在交换时是反对称的。这对配对振幅 $\Delta_{\mathbf{k}}$ 施加了基本约束。对于自旋无色的[费米子](@entry_id:146235)，空间[波函数](@entry_id:147440)必须是[奇宇称](@entry_id:147965)的，这意味着 $\Delta_{\mathbf{k}} = -\Delta_{-\mathbf{k}}$（例如 p-波配对）。对于[自旋单重态](@entry_id:153133)配对（如 s-波），自旋部分是反对称的，因此空间部分必须是偶宇称的，即 $\Delta_{\mathbf{k}} = \Delta_{-\mathbf{k}}$。

对于更复杂的包含自旋和多[轨道](@entry_id:137151)自由度的系统，上述形式主义可以被直接推广 [@problem_id:3022258]。此时，Nambu 旋量将包含所有内部自由度，例如 $\Psi_{\mathbf{k}}=\left(c_{\mathbf{k},\alpha}, c_{-\mathbf{k},\alpha}^{\dagger}\right)^{\mathrm{T}}$，其中 $\alpha$ 包含了自旋和[轨道](@entry_id:137151)指标。$H_{\mathrm{BdG}}(\mathbf{k})$ 相应地变成一个更大的矩阵：
$$ H_{\mathrm{BdG}}(\mathbf{k}) = \begin{pmatrix} h(\mathbf{k}) & \Delta(\mathbf{k}) \\ \Delta^{\dagger}(\mathbf{k}) & -h^{\mathrm{T}}(-\mathbf{k}) \end{pmatrix} $$
其中 $h(\mathbf{k})$ 是正常态的单粒子[哈密顿量](@entry_id:172864)矩阵，$\Delta(\mathbf{k})$ 是配对矩阵。[费米子](@entry_id:146235)[反对易关系](@entry_id:153815)此时要求配对矩阵满足 $\Delta(\mathbf{k}) = -\Delta^{\mathrm{T}}(-\mathbf{k})$。这个通用的结构是研究所有类型拓扑[超导体](@entry_id:191025)的出发点。

### 对称性与[拓扑分类](@entry_id:154529)

BdG [哈密顿量](@entry_id:172864)的对称性是其拓扑性质的根源。根据 Wigner-Dyson 对[随机矩阵](@entry_id:269622)的分类，系统的对称性决定了其所属的普适类。Altland 和 Zirnbauer 将此推广到包含[粒子-空穴对称性](@entry_id:142469)的[哈密顿量](@entry_id:172864)，形成了所谓的“十重分类法”，为拓扑绝缘体和[超导体](@entry_id:191025)的分类奠定了基础。三种关键的[离散对称性](@entry_id:146994)是：时间反演对称性 (TRS)、[粒子-空穴对称性](@entry_id:142469) (PHS) 和手征对称性 (CS)。

#### [粒子-空穴对称性](@entry_id:142469) (PHS)

[粒子-空穴对称性](@entry_id:142469)是 BdG 形式主义的内在属性，源于 Nambu 空间的冗余描述。它反映了体系中能量为 $E$ 的[准粒子激发](@entry_id:138475)与能量为 $-E$ 的[准粒子激发](@entry_id:138475)之间的对称关系。该对称性由一个[反幺正算符](@entry_id:197532) $\mathcal{C}$ 来描述，它满足如下关系：
$$ \mathcal{C}H_{\mathrm{BdG}}(\mathbf{k})\mathcal{C}^{-1} = -H_{\mathrm{BdG}}(-\mathbf{k}) $$
算符 $\mathcal{C}$ 可以写成一个幺[正矩阵](@entry_id:149490) $U_{\mathcal{C}}$ 和复共轭算符 $\mathcal{K}$ 的乘积，即 $\mathcal{C} = U_{\mathcal{C}}\mathcal{K}$。对于任何 BdG [哈密顿量](@entry_id:172864)，总能找到这样一个 $\mathcal{C}$。例如，在自旋无色（或[自旋单重态](@entry_id:153133)）的情况下，幺正部分可以由 Nambu 空间中的泡利矩阵 $\tau_x$ 给出，即 $U_{\mathcal{C}} = \tau_x$ [@problem_id:3022218]。对于包含自旋的更一般情况，它是 $\tau_x \otimes \mathbb{1}_{\sigma}$ [@problem_id:3022258]。

一个至关重要的性质是 $\mathcal{C}^2$ 的值。对于自旋为 $1/2$ 的[费米子](@entry_id:146235)体系，根据配对的类型（[单重态](@entry_id:154728)或[三重态](@entry_id:156705)），$\mathcal{C}^2$ 可以是 $+1$ 或 $-1$。
- 对于 s-波或 d-波等[自旋单重态](@entry_id:153133)[超导体](@entry_id:191025)，$\mathcal{C}^2 = +1$。
- 对于 p-波等自旋三重态[超导体](@entry_id:191025)，$\mathcal{C}^2 = -1$。
- 对于自旋无色[费米子](@entry_id:146235)，$\mathcal{C}^2 = +1$。

这个符号是区分不同拓扑类别的关键指标之一。

#### 时间反演对称性 (TRS)

与 PHS 不同，时间反演对称性不是 BdG [哈密顿量](@entry_id:172864)的固有属性，而是一种物理对称性，它可能存在，也可能被破坏。TRS 由一个[反幺正算符](@entry_id:197532) $\mathcal{T} = U_{\mathcal{T}}\mathcal{K}$ 描述，满足：
$$ \mathcal{T}H_{\mathrm{BdG}}(\mathbf{k})\mathcal{T}^{-1} = H_{\mathrm{BdG}}(-\mathbf{k}) $$
对于自旋 $1/2$ 系统，$\mathcal{T}^2 = -1$；对于自旋为整数（包括自旋无色）的系统，$\mathcal{T}^2 = +1$。外[磁场](@entry_id:153296)、磁性杂质或某些具有内禀手性的配对（如 $p_x+ip_y$ 波）都会破坏[时间反演对称性](@entry_id:138094)。例如，在一个普通的 s-波[超导体](@entry_id:191025)中施加一个塞曼场 $\mathbf{b}$，正常态[哈密顿量](@entry_id:172864) $h_0(\mathbf{k})$ 包含 $\mathbf{b} \cdot \boldsymbol{\sigma}$ 项。由于[时间反演](@entry_id:182076)算符会反转自旋，$\mathcal{T}(\mathbf{b} \cdot \boldsymbol{\sigma})\mathcal{T}^{-1} = -\mathbf{b} \cdot \boldsymbol{\sigma}$，这破坏了[哈密顿量](@entry_id:172864)在 $\mathbf{b} \neq \mathbf{0}$ 时的 TRS [@problem_id:3022189]。

#### Altland-Zirnbauer (AZ) 分类

根据系统是否具有 TRS 和 PHS，以及 $\mathcal{T}^2$ 和 $\mathcal{C}^2$ 的值，BdG [哈密顿量](@entry_id:172864)可以被归入十个 Altland-Zirnbauer [对称类](@entry_id:137548)中的一个。如果 TRS 和 PHS 都存在，系统还可能具有由 $\mathcal{S} = \mathcal{T}\mathcal{C}$ 定义的手征对称性。下表总结了与拓扑[超导体](@entry_id:191025)最相关的几个类别：

| 类别 | TRS | PHS | CS | $\mathcal{T}^2$ | $\mathcal{C}^2$ | 典型例子 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---|
| D | 0 | + | 0 | N/A | +1 | 自旋无色 p-波 SC；有塞曼场的 s-波 SC |
| DIII | + | + | + | -1 | +1 | 时间反演不变的拓扑[超导体](@entry_id:191025) |
| BDI | + | + | + | +1 | +1 | Kitaev 链 (实参数) |
| C | 0 | - | 0 | N/A | -1 | 自旋[三重态](@entry_id:156705) p-波 SC |

让我们通过两个重要的例子来理解这个分类过程：
1.  **二维手性 p-波[超导体](@entry_id:191025)**：考虑一个二维自旋无色[费米子](@entry_id:146235)系统，具有手性 $p_x+ip_y$ 配对 [@problem_id:3022268]。该系统具有 PHS，且由于是自旋无色，$\mathcal{C}^2=+1$。然而，复数配对形式 $\Delta_{\mathbf{k}} \propto k_x+ik_y$ 在 $\mathbf{k} \to -\mathbf{k}$ 时变为 $-k_x-ik_y = - \Delta_{-\mathbf{k}}^*$，这破坏了 TRS。因此，该系统属于 **D 类**。
2.  **有塞曼场的 s-波[超导体](@entry_id:191025)**：这是一个在实验上实现拓扑超导的重要平台 [@problem_id:3022189]。一个[自旋单重态](@entry_id:153133)的 s-波[超导体](@entry_id:191025)本身具有 TRS 和 PHS。然而，外加的塞曼场会破坏 TRS。系统仍然保留了 PHS，并且由于是[自旋单重态](@entry_id:153133)配对，我们发现 $\mathcal{C}^2=+1$。因此，这个系统也属于 **D 类**。

这两个例子揭示了一个深刻的道理：来自截然不同物理背景的系统可以拥有相同的[基本对称性](@entry_id:161256)，从而属于同一个拓扑[普适类](@entry_id:143033)，并共享相似的[拓扑性质](@entry_id:141605)。

### [体拓扑不变量](@entry_id:143658)

在给定的[对称类](@entry_id:137548)和空间维度下，不同的[拓扑相](@entry_id:141674)由一个整数或 $\mathbb{Z}_2$ 的 **[拓扑不变量](@entry_id:138526)** 来区分。这个[不变量](@entry_id:148850)在同一拓扑相内保持不变，只有当系统的体[能隙](@entry_id:191975)在所谓的[拓扑相变](@entry_id:137214)点闭合时才会发生改变。

#### D 类在二维：陈数

对于 D 类的二维系统，其[拓扑不变量](@entry_id:138526)是 **陈数 (Chern number)** $C \in \mathbb{Z}$。陈数是一个整数，它量化了 BdG [哈密顿量](@entry_id:172864)的占据带（负能带）在整个[布里渊区](@entry_id:142395)上的“扭曲”程度。对于一个可以写成 $H(\mathbf{k}) = \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\tau}$ 形式的 $2 \times 2$ BdG [哈密顿量](@entry_id:172864)（其中 $\boldsymbol{\tau}$ 是 Nambu 空间中的泡利矩阵），陈数可以通过对单位矢量场 $\hat{\mathbf{d}}(\mathbf{k}) = \mathbf{d}(\mathbf{k})/|\mathbf{d}(\mathbf{k})|$ 的缠绕数积分来计算 [@problem_id:1213356]：
$$ C = \frac{1}{4\pi} \int_{\text{BZ}} d^2k \left( \hat{\mathbf{d}} \cdot \left(\frac{\partial \hat{\mathbf{d}}}{\partial k_x} \times \frac{\partial \hat{\mathbf{d}}}{\partial k_y}\right) \right) $$
这个积分计算了当动量 $\mathbf{k}$ 遍历二维布里渊区（一个环面 $T^2$）时，单位矢量 $\hat{\mathbf{d}}$ 覆盖单位球面 $S^2$ 的次数。

在实际计算中，对于许多[晶格模型](@entry_id:184345)，陈数可以通过一种更简单的方法确定。它依赖于“质量项” $d_z(\mathbf{k})$ 在[布里渊区](@entry_id:142395)中四个[时间反演](@entry_id:182076)不变动量点 (TRIMs) 的符号：$(0,0), (0,\pi), (\pi,0), (\pi,\pi)$。通过分析一个二维手性 p-波[超导体](@entry_id:191025)的具体[晶格模型](@entry_id:184345) [@problem_id:1213356]，在特定参数下，我们发现 $d_z(\mathbf{k}) = \xi(\mathbf{k})$ 在这四个点的符号分别为 $(-1, +1, +1, -1)$。根据相应的公式，可以计算出陈数 $C=2$。这意味着该系统处于一个非平庸的[拓扑相](@entry_id:141674)。

#### 一维手征类：绕数

对于具有手征对称性的一维系统（如 BDI 或 AIII 类），[拓扑不变量](@entry_id:138526)是一个整数 **绕数 (winding number)** $W \in \mathbb{Z}$。在这类系统中，BdG [哈密顿量](@entry_id:172864)可以变换为一个块非对角的形式：
$$ H(k) = \begin{pmatrix} 0 & q(k) \\ q^{\dagger}(k) & 0 \end{pmatrix} $$
此时，体系的[能隙](@entry_id:191975)由 $q(k)$ 的奇异值决定。只要[能隙](@entry_id:191975)不关闭，$\det q(k) \neq 0$。拓扑不变量 $W$ 就定义为当动量 $k$ 遍历一维[布里渊区](@entry_id:142395)时，复数 $\det q(k)$ 的相位绕原点转动的圈数 [@problem_id:3022250]。它可以通过以下等价的积分公式计算：
$$ W = \frac{1}{2\pi i} \int_{-\pi}^{\pi} dk \, \partial_{k} \ln\det q(k) = \frac{1}{2\pi i} \int_{-\pi}^{\pi} dk \, \mathrm{Tr}\left[q^{-1}(k) \partial_{k}q(k)\right] $$
系统的[拓扑相变](@entry_id:137214)发生在体[能隙](@entry_id:191975)关闭的[临界点](@entry_id:144653)，即 $\det q(k)=0$ 的点。通过求解一个具有最近邻和次近邻相互作用的广义 Kitaev 链模型 [@problem_id:1213347]，我们可以找到[能隙](@entry_id:191975)在动量空间中闭合的条件。这些条件确定了化学势 $\mu$ 的临界值，这些值构成了不同[拓扑相](@entry_id:141674)（具有不同绕数 $W$）之间的相边界。

### [马约拉纳费米子](@entry_id:137199)与[体边对应](@entry_id:146387)

[拓扑不变量](@entry_id:138526)不仅仅是数学上的抽象概念，它具有深刻的物理后果。**[体边对应](@entry_id:146387) (bulk-boundary correspondence)** 原理指出，一个非平庸的[体拓扑不变量](@entry_id:143658)必然导致在[系统边界](@entry_id:158917)上出现受[拓扑保护](@entry_id:145388)的、[无能](@entry_id:201612)隙的束缚态。在拓扑[超导体](@entry_id:191025)中，这些奇异的边界态就是由马约拉纳费米子构成的。

#### [马约拉纳费米子](@entry_id:137199)

一个常规的复[费米子](@entry_id:146235)（如电子）与其反粒子不同。而 **[马约拉纳费米子](@entry_id:137199)** 是一种特殊的粒子，它本身就是自己的反粒子。在凝聚态物理中，[马约拉纳费米子](@entry_id:137199)作为[准粒子激发](@entry_id:138475)出现。我们可以将一个常规的复[费米子算符](@entry_id:149120) $c_j$ 分解为两个马约拉纳算符 $\gamma_{j,1}$ 和 $\gamma_{j,2}$ [@problem_id:3022269]：
$$ c_j = \frac{1}{2}(\gamma_{j,1} + i\gamma_{j,2}), \quad c_j^{\dagger} = \frac{1}{2}(\gamma_{j,1} - i\gamma_{j,2}) $$
其中马约拉纳算符是厄米的（$\gamma^{\dagger} = \gamma$）并满足特殊的[反对易关系](@entry_id:153815) $\lbrace \gamma_{j,a}, \gamma_{k,b} \rbrace = 2\delta_{jk}\delta_{ab}$。

A. Kitaev 提出的 **Kitaev 链** 模型是理解[马约拉纳模](@entry_id:200998)的最简洁范例 [@problem_id:3022269]。这是一个一维自旋无色 p-波[超导体](@entry_id:191025)。当用马约拉纳算符重写其[哈密顿量](@entry_id:172864)时，其结构变得异常清晰：
$$ H = \frac{i}{2} \sum_{j=1}^{N} \left[-\mu \, \gamma_{j,1}\gamma_{j,2}\right] + \frac{i}{2} \sum_{j=1}^{N-1} \left[ (-t+\Delta) \, \gamma_{j,1}\gamma_{j+1,2} + (t+\Delta) \, \gamma_{j,2}\gamma_{j+1,1} \right] $$
在拓扑相（例如当 $\mu=0, t=\Delta > 0$ 时），[哈密顿量](@entry_id:172864)简化为 $H = i t \sum_j \gamma_{j,2}\gamma_{j+1,1}$。这意味着来自相邻格点的马约拉纳算符 $\gamma_{j,2}$ 和 $\gamma_{j+1,1}$ 配对形成了一个常规的[费米子](@entry_id:146235)，并具有有限的能量。然而，在链的两端，$\gamma_{1,1}$ 和 $\gamma_{N,2}$ 无法找到配对伙伴。它们从[哈密顿量](@entry_id:172864)中完全解耦，形成了两个独立的 **马约拉纳[零能模](@entry_id:172472) (Majorana Zero Modes, MZMs)**。这两个[零能模](@entry_id:172472)共同构成了一个非局域的、能量严格为零的[费米子](@entry_id:146235)态，这是[拓扑量子比特](@entry_id:146112)的基本组成部分。

#### [体边对应](@entry_id:146387)原理

[体边对应](@entry_id:146387)原理将[体拓扑不变量](@entry_id:143658)与边界态的数量联系起来。
-   **一维系统**：对于 Kitaev 链这样的 BDI 类系统，其整数绕数 $W$ 的[绝对值](@entry_id:147688) $|W|$ 等于系统两端出现的马约拉纳[零能模](@entry_id:172472)的对数。
-   **二维系统**：对于二维 D 类拓扑[超导体](@entry_id:191025)，其体陈数 $\mathcal{N}$ 的[绝对值](@entry_id:147688) $|\mathcal{N}|$ 等于系统单个边界上受[拓扑保护](@entry_id:145388)的 **手性马约拉纳边界模** 的数量 [@problem_id:3022257]。这些边界模是[无能](@entry_id:201612)隙的，并沿着边界[单向传播](@entry_id:174820)，其传播方向由 $\mathcal{N}$ 的符号决定。

这一深刻联系可以通过 **[谱流](@entry_id:146831) (spectral flow)** 参数来论证 [@problem_id:3022257]。想象将一个二维拓扑[超导体](@entry_id:191025)制成一个圆柱体，并在其中穿入一个绝热变化的[磁通量](@entry_id:268943) $\phi$。这个过程相当于在边界的一维[能谱](@entry_id:181780)中平移其动量。一个重要的拓扑定理指出，当磁通量从 $0$ 变为一个磁通量子 $2\pi$ 时，穿过零能量的能级净数量（从下往上为正，从上往下为负）严格等于体的陈数 $\mathcal{N}$。这个净[谱流](@entry_id:146831)正是由 $|\mathcal{N}|$ 个手性马约拉纳边界模贡献的。每个边界模的色散关系 $E(k_y)$ 都是单向的，因此在动量平移一个周期时，它必然会净一次地穿越零能量，从而为总[谱流](@entry_id:146831)贡献 $\pm 1$。因此，边界态的数量必须恰好为 $|\mathcal{N}|$，才能与[体拓扑不变量](@entry_id:143658)相匹配。

我们甚至可以具体地求解边界态的性质。例如，对于一个占据半平面 $x \ge 0$ 的二维 $p_x-ip_y$ [超导体](@entry_id:191025)，通过在 $x=0$ 处施加硬墙边界条件来求解 BdG 方程，可以得到局域在边界上的[马约拉纳模](@entry_id:200998)的色散关系。在小动量极限下，其[色散](@entry_id:263750)是线性的 $E(k_y) \approx v_M \hbar k_y$，其中手性[马约拉纳模](@entry_id:200998)的速度 $v_M$ 可以被精确计算出来，其值与配对振幅 $\Delta$ 直接相关 [@problem_id:1213345]。这为[体边对应](@entry_id:146387)的抽象原理提供了具体的物理图像。