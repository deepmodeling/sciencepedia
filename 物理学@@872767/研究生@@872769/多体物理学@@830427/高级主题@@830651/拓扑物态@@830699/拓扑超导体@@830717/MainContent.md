## 引言
拓扑[超导体](@entry_id:191025)代表了[凝聚态物理学](@entry_id:140205)的一个前沿领域，它将超[导电性](@entry_id:137481)与拓扑[物态](@entry_id:139436)这两个深刻的物理概念相结合。这些奇异材料的核心魅力在于其预测能够承载[马约拉纳零模](@entry_id:136627)——一种作为自身反粒子的[准粒子](@entry_id:136584)。由于其独特的非阿贝尔统计特性，[马约拉纳零模](@entry_id:136627)为构建具有内禀[容错](@entry_id:142190)能力的[拓扑量子计算](@entry_id:138660)机提供了理论基础，有望解决当前[量子计算](@entry_id:142712)技术面临的主要障碍之一：[退相干](@entry_id:145157)。然而，理解这些复杂[物态](@entry_id:139436)的形成机制、掌握其探测方法并最终实现对其的精确操控，构成了该领域的核心挑战与知识鸿沟。

本文旨在为读者提供一个关于拓扑[超导体](@entry_id:191025)的系统性介绍。我们将从“原理与机制”一章开始，深入探讨描述拓扑[超导体](@entry_id:191025)的核心数学框架，包括 Bogoliubov-de Gennes (BdG) 形式主义和[对称性分类](@entry_id:184862)，并阐明其最关键的物理表现——[体边对应](@entry_id:146387)关系。随后，在“应用与跨学科连接”一章中，我们将视野扩展到现实世界，探索实现和探测拓扑超导态的各种实验平台，并揭示其与[材料科学](@entry_id:152226)、[量子计算](@entry_id:142712)等领域的深刻[交叉](@entry_id:147634)。最后，通过“动手实践”中的具体问题，读者将有机会将理论知识应用于解决实际计算问题，从而巩固和深化对这一迷人领域的理解。

## 原理与机制

在上一章节中，我们介绍了拓扑[超导体](@entry_id:191025)的基本概念及其在[容错量子计算](@entry_id:142498)中的潜在应用。本章将深入探讨支撑这些奇异物态的数学框架和物理原理。我们将从平均场理论出发，构建描述[超导体](@entry_id:191025)的普适[哈密顿量](@entry_id:172864)，即[Bogoliubov-de Gennes (BdG) 哈密顿量](@entry_id:136941)。随后，我们将引入[对称性分类](@entry_id:184862)的概念，特别是Altland-Zirnbauer (AZ) 分类法，它为拓扑物相提供了一个系统的“[元素周期表](@entry_id:190860)”。在此基础上，我们将定义和计算各种[拓扑不变量](@entry_id:138526)，如陈数和绕数，它们是区分不同[拓扑相](@entry_id:141674)的数学指纹。最后，我们将阐述拓扑[超导体](@entry_id:191025)最核心的物理表现——[体边对应](@entry_id:146387)关系，即非平凡的[体拓扑不变量](@entry_id:143658)如何保证边界上存在受保护的马约拉纳束缚态，并讨论相互作用对非相互作用分类的修正。

### Bogoliubov-de Gennes (BdG) 形式主义

超导现象的核心是电子通过与[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）的相互作用形成束缚对，即库珀对。在平均场近似下，这种复杂的相互作用可以被一个序参量——[配对能隙](@entry_id:160388)函数 $\Delta$ 所描述。然而，这种处理方式引入了一个复杂性：[哈密顿量](@entry_id:172864)不再保持粒子数守恒，因为它包含了同时产生或湮灭两个电子的项。为了解决这个问题，我们需要引入Bogoliubov-de Gennes (BdG) 形式主义。

#### Nambu 旋量与 BdG [哈密顿量](@entry_id:172864)

BdG 形式主义的关键在于将电子的产生和[湮灭算符](@entry_id:165390)组合成一个新的矢量，称为 **Nambu [旋量](@entry_id:158054) (Nambu spinor)**。对于一个平移不变的单带自旋无相互作用的系统，我们考虑动量为 $\mathbf{k}$ 和 $-\mathbf{k}$ 的电子配对。我们可以定义 Nambu 旋量为：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}} \\ c_{-\mathbf{k}}^{\dagger} \end{pmatrix}
$$
其中 $c_{\mathbf{k}}$ 是动量为 $\mathbf{k}$ 的电子的[湮灭算符](@entry_id:165390)，$c_{-\mathbf{k}}^{\dagger}$ 是动量为 $-\mathbf{k}$ 的电子的[产生算符](@entry_id:191512)。注意，$c_{-\mathbf{k}}^{\dagger}$ 在这个新空间中扮演着一个“空穴”的[湮灭算符](@entry_id:165390)的角色。

通过这个旋量，包含配对项的[平均场哈密顿量](@entry_id:751814)可以被写成一个紧凑的二次型：
$$
H_{\mathrm{MF}} = \frac{1}{2} \sum_{\mathbf{k}} \Psi_{\mathbf{k}}^{\dagger} H_{\mathrm{BdG}}(\mathbf{k}) \Psi_{\mathbf{k}} + \text{const.}
$$
这里的 $H_{\mathrm{BdG}}(\mathbf{k})$ 就是 **Bogoliubov-de Gennes [哈密顿量](@entry_id:172864)**。它是一个作用于 Nambu 空间的 $2 \times 2$ 矩阵。从[二次量子化](@entry_id:137766)的基本原理出发，并利用[费米子](@entry_id:146235)[反对易关系](@entry_id:153815)，我们可以推导出它的普适形式 [@problem_id:3022218]。

考虑一个具有单粒子[色散](@entry_id:263750) $\epsilon_{\mathbf{k}}$ 和配对振幅 $\Delta_{\mathbf{k}}$ 的系统，其[平均场哈密顿量](@entry_id:751814)为：
$$
H_{\mathrm{MF}} = \sum_{\mathbf{k}} (\epsilon_{\mathbf{k}} - \mu) c_{\mathbf{k}}^{\dagger} c_{\mathbf{k}} + \sum_{\mathbf{k}} \left( \Delta_{\mathbf{k}} c_{\mathbf{k}}^{\dagger} c_{-\mathbf{k}}^{\dagger} + \Delta_{\mathbf{k}}^* c_{-\mathbf{k}} c_{\mathbf{k}} \right)
$$
其中 $\mu$ 是化学势。我们定义正规态[色散](@entry_id:263750)为 $\xi_{\mathbf{k}} = \epsilon_{\mathbf{k}} - \mu$。将此[哈密顿量](@entry_id:172864)用 Nambu [旋量表示](@entry_id:141362)，并仔细处理求和与算符顺序，可以得到 BdG [哈密顿量](@entry_id:172864)的矩阵形式：
$$
H_{\mathrm{BdG}}(\mathbf{k}) = \begin{pmatrix} \xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^{\ast} & -\xi_{-\mathbf{k}} \end{pmatrix}
$$
这个形式包含了几个深刻的物理约束：
1.  **[厄米性](@entry_id:141899) (Hermiticity)**: 由于总[哈密顿量](@entry_id:172864)必须是厄米的，$H_{\mathrm{BdG}}(\mathbf{k})$ 也必须是[厄米矩阵](@entry_id:155147)。这要求对角元 $\xi_{\mathbf{k}}$ 和 $-\xi_{-\mathbf{k}}$ 是实数（这自然成立，因为能量是实数），并且非对角元满足 $(H_{21}) = (H_{12})^*$，即 $(\Delta_{\mathbf{k}}^*) = (\Delta_{\mathbf{k}})^*$，这在我们的构造中已经自动满足。
2.  **[色散](@entry_id:263750)对称性**: 一般来说，$\xi_{\mathbf{k}}$ 不一定等于 $\xi_{-\mathbf{k}}$。只有当正规态具有空间反演对称性（$I$）或时间反演对称性（$T$）时，我们才有 $\xi_{\mathbf{k}} = \xi_{-\mathbf{k}}$。在缺乏这些对称性的系统中（例如，在没有反演中心的晶体中），必须保留 $-\xi_{-\mathbf{k}}$ 这一项。
3.  **[费米子统计](@entry_id:148436)**: [泡利不相容原理](@entry_id:141850)要求两个全同[费米子](@entry_id:146235)的总[波函数](@entry_id:147440)在交换时是反对称的。这对配对函数 $\Delta_{\mathbf{k}}$ 施加了宇称约束。对于自旋单态配对（如 s-波），自旋部分是反对称的，因此空间部分必须是偶宇称的，即 $\Delta_{\mathbf{k}} = \Delta_{-\mathbf{k}}$。对于自旋三重态或自旋无（spinless）[费米子配对](@entry_id:158762)（如 p-波），空间部分必须是奇宇称的，即 $\Delta_{\mathbf{k}} = -\Delta_{-\mathbf{k}}$。
4.  **[粒子-空穴对称性](@entry_id:142469) (Particle-Hole Symmetry, PHS)**: BdG [哈密顿量](@entry_id:172864)具有一个内禀的对称性，称为[粒子-空穴对称性](@entry_id:142469)。它将能量为 $E$ 的[准粒子激发](@entry_id:138475)与能量为 $-E$ 的准空穴激发联系起来。在 Nambu 空间中，该对称性由一个[反幺正算符](@entry_id:197532) $\mathcal{C}$ 实现，它满足关系 $\mathcal{C} H_{\mathrm{BdG}}(\mathbf{k}) \mathcal{C}^{-1} = -H_{\mathrm{BdG}}(-\mathbf{k})$。对于上述自旋无的 $2 \times 2$ 模型，这个算符可以写为 $\mathcal{C} = \tau_x \mathcal{K}$，其中 $\tau_x$ 是作用于 Nambu 空间的泡利矩阵，$\mathcal{K}$ 是[复共轭](@entry_id:174690)算符。这个对称性保证了 BdG 谱关于零能是对称的：如果 $E$ 是一个[本征值](@entry_id:154894)，那么 $-E$ 也必然是[本征值](@entry_id:154894)。

对于更一般的多[轨道](@entry_id:137151)、自旋系统，Nambu 旋量会包含更多的分量，例如 $\Psi_{\mathbf{k}} = (c_{\mathbf{k},\alpha}, c_{-\mathbf{k},\alpha}^{\dagger})^T$，其中 $\alpha$ 概括了自旋、[轨道](@entry_id:137151)等内部自由度。此时，$H_{\mathrm{BdG}}(\mathbf{k})$ 成为一个更大的[块矩阵](@entry_id:148435) [@problem_id:3022258]：
$$
H_{\mathrm{BdG}}(\mathbf{k}) = \begin{pmatrix} h(\mathbf{k}) & \Delta(\mathbf{k}) \\ \Delta^{\dagger}(\mathbf{k}) & -h^{\mathrm{T}}(-\mathbf{k}) \end{pmatrix}
$$
其中 $h(\mathbf{k})$ 是正规态的单粒子[哈密顿量](@entry_id:172864)矩阵，$\Delta(\mathbf{k})$ 是配对矩阵。费米统计的要求推广为 $\Delta(\mathbf{k}) = -\Delta^{\mathrm{T}}(-\mathbf{k})$。这个更一般的形式同样具有内禀的[粒子-空穴对称性](@entry_id:142469)，其算符和约束关系与单带模型类似，确保了谱的对称性。

### 拓扑[超导体](@entry_id:191025)的[对称性分类](@entry_id:184862)

BdG [哈密顿量](@entry_id:172864)的[拓扑性质](@entry_id:141605)由其遵从的[离散对称性](@entry_id:146994)（[时间反演](@entry_id:182076)、粒子-空穴和[手性对称性](@entry_id:141715)）决定。**Altland-Zirnbauer (AZ) 分类方案** 根据这些对称性的有无及其平方（$\mathcal{T}^2 = \pm 1$, $\mathcal{C}^2 = \pm 1$）将[哈密顿量](@entry_id:172864)分到十个不同的对称性类别中。每个类别在不同的空间维度上具有独特的[拓扑分类](@entry_id:154529)（例如，$\mathbb{Z}$、$\mathbb{Z}_2$ 或平庸）。

-   **[粒子-空穴对称性](@entry_id:142469) (PHS)**: 如上所述，所有[超导体](@entry_id:191025)都具有内禀的 PHS，其算符 $\mathcal{C}$ 满足 $\mathcal{C} H(\mathbf{k}) \mathcal{C}^{-1} = -H(-\mathbf{k})$。对于自旋单态配对，通常有 $\mathcal{C}^2=+1$（D 类），而对于某些[自旋三重态配对](@entry_id:144256)，则有 $\mathcal{C}^2=-1$（C 类）。

-   **[时间反演对称性](@entry_id:138094) (TRS)**: 如果系统不受[磁场](@entry_id:153296)或磁性杂质影响，它通常具有时间反演对称性。TRS 由一个[反幺正算符](@entry_id:197532) $\mathcal{T}$ 表示，满足 $\mathcal{T} H(\mathbf{k}) \mathcal{T}^{-1} = H(-\mathbf{k})$。对于自旋-$1/2$ [费米子](@entry_id:146235)，由于自旋的存在，$\mathcal{T}^2=-1$。对于自旋无系统或在特定表示下，可以有 $\mathcal{T}^2=+1$。

-   **[手性对称性](@entry_id:141715) (Chiral Symmetry)**: 当一个系统同时具有 PHS 和 TRS 时，通常会产生一个幺正的[手性对称性](@entry_id:141715) $\mathcal{S} = \mathcal{T}\mathcal{C}$，它与[哈密顿量](@entry_id:172864)反对易：$\mathcal{S} H(\mathbf{k}) \mathcal{S}^{-1} = -H(\mathbf{k})$。

让我们通过几个例子来具体理解这个分类。

#### D 类拓扑[超导体](@entry_id:191025)
当[时间反演对称性](@entry_id:138094)被破坏时（例如，施加了塞曼场），但[粒子-空穴对称性](@entry_id:142469)依然存在，系统就可能属于 D 类。一个典型的例子是 s-波[超导体](@entry_id:191025)在塞曼场下的模型 [@problem_id:3022189]。其 BdG [哈密顿量](@entry_id:172864)为：
$$
H(\mathbf{k}) = \begin{pmatrix} h_{0}(\mathbf{k}) & \Delta\, i \sigma_{y} \\ -\Delta\, i \sigma_{y} & -h_{0}^{T}(-\mathbf{k}) \end{pmatrix}
$$
其中 $h_{0}(\mathbf{k}) = \epsilon(\mathbf{k})\, \mathbb{1}_{\sigma} + \mathbf{b}\cdot \boldsymbol{\sigma}$ 包含了塞曼场 $\mathbf{b}$。由于塞曼场在[时间反演](@entry_id:182076)下会反向（$\mathcal{T}(\mathbf{b}\cdot \boldsymbol{\sigma})\mathcal{T}^{-1} = -\mathbf{b}\cdot \boldsymbol{\sigma}$），TRS 被破坏。然而，可以验证该系统仍然具有 PHS，且 $\mathcal{C}^2=+1$。因此，该系统属于 **D 类**。在二维空间中，D 类的[拓扑分类](@entry_id:154529)是 $\mathbb{Z}$，由陈数（Chern number）标记。一个著名的例子是**手性 p-波[超导体](@entry_id:191025)**，它天然地破坏 TRS [@problem_id:3022268]。

#### DIII 类拓扑[超导体](@entry_id:191025)
当系统同时具有 TRS（$\mathcal{T}^2=-1$）和 PHS（$\mathcal{C}^2=+1$）时，它属于 **DIII 类**。这种情况通常出现在具有强自旋-轨道耦合且配对函数在时间反演下为偶的[超导体](@entry_id:191025)中 [@problem_id:3022237]。[自旋-轨道耦合](@entry_id:143520)本身是保持时间反演对称的，因此在没有外[磁场](@entry_id:153296)的情况下，TRS 得以保留。DIII 类在一维和三维空间中都具有 $\mathbb{Z}_2$ [拓扑分类](@entry_id:154529)，预示着存在受[拓扑保护](@entry_id:145388)的、以 Kramers 对形式出现的马约拉纳边界态。

### [体拓扑不变量](@entry_id:143658)

拓扑相的“指纹”是**拓扑不变量**——一个在不关闭体[能隙](@entry_id:191975)的情况下、在连续形变下保持不变的量子数。它的值只能通过**[拓扑相变](@entry_id:137214)**（即体[能隙](@entry_id:191975)关闭再打开的过程）来改变。

#### 一维系统：绕数
对于一维系统，最典型的[拓扑不变量](@entry_id:138526)是**绕数 (winding number)**。让我们以著名的 **Kitaev 链模型**为例 [@problem_id:3022269]。这是一个描述自旋无[费米子](@entry_id:146235)的 p-波超导链，其[哈密顿量](@entry_id:172864)为：
$$
H=-t\sum_{j}\left(c_{j}^{\dagger}c_{j+1}+\mathrm{h.c.}\right)-\mu\sum_{j}\left(c_{j}^{\dagger}c_{j}-\tfrac{1}{2}\right)+\Delta\sum_{j}\left(c_{j}c_{j+1}+\mathrm{h.c.}\right)
$$
其中 $t$ 是最近邻跃迁振幅，$\mu$ 是化学势，$\Delta$ 是 p-波配对振幅。通过将[费米子算符](@entry_id:149120)分解为两个马约拉纳算符 $c_j = \frac{1}{2}(\gamma_{j,1}+i\gamma_{j,2})$，该模型可以被精确求解。分析表明，当 $|\mu|  2|t|$ 时，系统处于拓扑非平庸相；当 $|\mu| > 2|t|$ 时，处于拓扑平庸相。[相变](@entry_id:147324)点 $|\mu|=2|t|$ 正是[动量空间](@entry_id:148936)中 BdG [哈密顿量](@entry_id:172864)[能隙](@entry_id:191975)关闭的地方 [@problem_id:1213347]。

对于具有[手性对称性](@entry_id:141715)的一维系统（属于 AIII、BDI 或 CII 类），拓扑不变量是一个整数绕数 $W$。如果[哈密顿量](@entry_id:172864)可以写成非对角块的形式：
$$
H(k)=\begin{pmatrix} 0  q(k) \\ q^{\dagger}(k)  0 \end{pmatrix}
$$
那么绕数 $W$ 就定义为当动量 $k$ 遍历整个[布里渊区](@entry_id:142395)时，复数 $\det q(k)$ 的[相角](@entry_id:274491)绕原点缠绕的[圈数](@entry_id:267135) [@problem_id:3022250]。它可以用一个积分公式来计算：
$$
W=\dfrac{1}{2\pi i}\int_{-\pi}^{\pi}dk\,\partial_{k}\ln\det q(k) = \dfrac{1}{2\pi i}\int_{-\pi}^{\pi}dk\,\mathrm{Tr}\left[q^{-1}(k)\,\partial_{k}q(k)\right]
$$
这个整数 $W$ 直接对应于[系统边界](@entry_id:158917)上马约拉纳[零能模](@entry_id:172472)的数量。

#### 二维系统：陈数
对于二维系统，一个关键的拓扑不变量是**陈数 (Chern number)**，它是一个整数。对于一个两能带模型，如手性 p-波[超导体](@entry_id:191025)，其 BdG [哈密顿量](@entry_id:172864)可以写成 $\mathcal{H}(\mathbf{k}) = \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\tau}$ 的形式，其中 $\boldsymbol{\tau}$ 是泡利矩阵矢量。陈数 $C$ 描述了单位矢量 $\hat{\mathbf{d}}(\mathbf{k}) = \mathbf{d}(\mathbf{k}) / |\mathbf{d}(\mathbf{k})|$ 在 $\mathbf{k}$ 遍历二维[布里渊区](@entry_id:142395)（一个环面 $T^2$）时，覆盖目标空间（一个球面 $S^2$）的次数 [@problem_id:1213356]。

陈数可以通过对整个[布里渊区积分](@entry_id:188454)**[贝里曲率](@entry_id:136846) (Berry curvature)** 来计算：
$$
C = \frac{1}{2\pi}\sum_{n\in\text{occ}}\int_{\text{BZ}} \Omega_n(\mathbf{k})\,d^2k
$$
其中求和遍历所有被占据的（负能）BdG 能带。贝里曲率 $\Omega_n$ 源于**[贝里联络](@entry_id:136662) (Berry connection)** $\mathcal{A}_{n}(\mathbf{k})=i\langle u_{n}(\mathbf{k})|\nabla_{\mathbf{k}}|u_{n}(\mathbf{k})\rangle$，其中 $|u_{n}(\mathbf{k})\rangle$ 是第 $n$ 个能带的 BdG [本征态](@entry_id:149904) [@problem_id:3022273]。[贝里联络](@entry_id:136662)和曲率是动量空间中的几何相位效应的体现，它们在电磁规范变换下具有明确的变换性质，但陈数作为它们的积分是规范不变的物理量。

#### [对称性指标](@entry_id:144050)
在某些情况下，计算像陈数这样的积分[不变量](@entry_id:148850)可能很复杂，或者[不变量](@entry_id:148850)本身是 $\mathbb{Z}_2$ 类型的（即只能取 0 或 1）。这时，可以利用额外的[晶格](@entry_id:196752)对称性（如空间反演）来构造更简单的**拓扑指标 (topological indicator)**。一个重要的例子是 Fu-Berg 提出的用于判断具有[反演对称性](@entry_id:269948)的奇宇称[超导体](@entry_id:191025)的准则 [@problem_id:3022197]。对于一个三维时间反演不变的[奇宇称](@entry_id:147965)[超导体](@entry_id:191025)（DIII 类），其强 $\mathbb{Z}_2$ [不变量](@entry_id:148850) $\nu_0$ 可以通过检查[费米面拓扑](@entry_id:138700)来确定。具体来说，如果包裹了奇数个时间反演不变动量点（TRIM）的费米面有奇数个，则系统是拓扑非平庸的（$\nu_0=1$）。这个判据仅依赖于正规态能带在各个 TRIM 点的能量相对于化学势的符号，而不需要复杂的积分计算。

### [体边对应](@entry_id:146387)与[马约拉纳模](@entry_id:200998)

拓扑[超导体](@entry_id:191025)最引人注目的物理后果是**[体边对应](@entry_id:146387) (bulk-boundary correspondence)** 原理：一个非平庸的[体拓扑不变量](@entry_id:143658)必然导致在系统的边界上出现受[拓扑保护](@entry_id:145388)的、能量在体[能隙](@entry_id:191975)之内的[激发态](@entry_id:261453)。对于拓扑[超导体](@entry_id:191025)，这些边界态就是**[马约拉纳模](@entry_id:200998) (Majorana modes)**。

-   **一维：马约拉纳[零能模](@entry_id:172472) (Majorana Zero Modes, MZMs)**
    对于一维拓扑[超导体](@entry_id:191025)（如 Kitaev 链），[体边对应](@entry_id:146387)表现为在链的两端各出现一个马约拉纳[零能模](@entry_id:172472) [@problem_id:3022269]。这两个离域的[马约拉纳模](@entry_id:200998)共同构成一个非局域的[费米子](@entry_id:146235)态，其能量精确为零，受到[拓扑保护](@entry_id:145388)。同样，在两种[拓扑性质](@entry_id:141605)不同的材料的界面上，例如[拓扑相](@entry_id:141674)和真空（或平庸相）的界面，也会形成束缚态。这种由质量项的“[畴壁](@entry_id:144723)”束缚[零能模](@entry_id:172472)的现象是[拓扑物质](@entry_id:161097)的普遍特征 [@problem_id:1213343] [@problem_id:1213367]。

-   **二维：手性马约拉纳边界模**
    对于具有非零陈数 $C$ 的二维拓扑[超导体](@entry_id:191025)（如手性 p-波[超导体](@entry_id:191025)），[体边对应](@entry_id:146387)预言在其一维边界上存在 $|C|$ 个手性[马约拉纳模](@entry_id:200998)。这些模是无能隙的，并沿着边界[单向传播](@entry_id:174820)，其传播方向由陈数的符号决定。这个对应关系可以通过一个思想实验——**[谱流](@entry_id:146831) (spectral flow)** 来严格论证 [@problem_id:3022257]。将系统置于一个圆柱体上，并穿入一个磁通量子。当磁通从 0 增加到 $2\pi$ 时，边界态的能谱会发生演化。一个重要的[指标定理](@entry_id:637636)指出，在这个过程中，穿过零能级的净能谱流（从下往上穿过的能级数减去从上往下穿过的能级数）严格等于体陈数 $C$。而每一个手性马约拉纳边界模恰好对[谱流](@entry_id:146831)贡献 $\pm 1$。因此，为了满足这个[指标定理](@entry_id:637636)，边界上必须存在 $|C|$ 个手性[马约拉纳模](@entry_id:200998)。

-   **缺陷束缚的[马约拉纳模](@entry_id:200998)**
    除了在系统的宏观边界上，[马约拉纳模](@entry_id:200998)也可以被束缚在体内的拓扑缺陷上。最著名的例子是二维手性 p-波[超导体](@entry_id:191025)中的**[磁通](@entry_id:191239)涡旋 (vortex)**。一个具有绕数 $N$ 的涡旋，其核心处[能隙](@entry_id:191975)为零，可以束缚马约拉纳[零能模](@entry_id:172472)。一个深刻的[指标定理](@entry_id:637636)（Jackiw-Rossi 定理）指出，在拓扑非平庸相中，这样一个涡旋会束缚 $|N|$ 个马约拉纳[零能模](@entry_id:172472) [@problem_id:3022239]。

#### [马约拉纳模](@entry_id:200998)的探测
由于[马约拉纳模](@entry_id:200998)是电中性的，直接探测它们非常困难。一个关键的电学输运特征是**[安德烈夫反射](@entry_id:146699) (Andreev reflection)**。在一个普通金属-[超导体](@entry_id:191025)（NS）结中，当一个能量低于超导能隙的电子从金属端入射到[超导体](@entry_id:191025)界面时，它无法作为[准粒子](@entry_id:136584)进入[超导体](@entry_id:191025)。取而代之，它会在界面上与另一个电子形成库珀对进入超导凝聚体，同时在金属端反射一个空穴。

对于拓扑[超导体](@entry_id:191025)，如果界面上存在一个马约拉纳[零能模](@entry_id:172472)，这个过程会发生质变 [@problem_id:3022202]。在零偏压（即入射电子能量为零）时，入射电子会与[马约拉纳模](@entry_id:200998)共振，导致**完美的[安德烈夫反射](@entry_id:146699)**——入射电子被完全转化为反射空穴，而正常的电子反射过程被完全抑制。这会在[电导](@entry_id:177131)上产生一个量子化的峰值 $2e^2/h$。这个现象可以通过分析散射矩阵来精确描述。在零能时，NS 结的反射矩阵 $r(0)$ 的[行列式](@entry_id:142978) $\det r(0)$ 可以作为拓扑不变量：在平庸相中，$\det r(0) = +1$；而在拓扑相中，由于完美[安德烈夫反射](@entry_id:146699)，$\det r(0) = -1$。

### 相互作用的角色：从 $\mathbb{Z}$ 到 $\mathbb{Z}_8$

我们至今的讨论都基于无相互作用的平均场理论。然而，电子间的相互作用可以深刻地改变[拓扑分类](@entry_id:154529)。一个惊人的例子发生在具有 BDI 对称性类别（$\mathcal{T}^2=+1$, $\mathcal{C}^2=+1$）的一维拓扑[超导体](@entry_id:191025)中。

在无相互作用的情况下，该类别的[拓扑分类](@entry_id:154529)是 $\mathbb{Z}$，由整数绕数 $W$ 标记，对应于边界上存在 $|W|$ 个马约拉纳[零能模](@entry_id:172472)。然而，Fidkowski 和 Kitaev 指出，当考虑局域的、保持对称性的电子相互作用时，这个分类会塌缩为 $\mathbb{Z}_8$ [@problem_id:3022204]。

其物理图像如下：单个马约拉纳[零能模](@entry_id:172472)或少量[马约拉纳模](@entry_id:200998)是绝对稳定的，因为任何能够打开[能隙](@entry_id:191975)的局域微扰（例如，一个形如 $im\gamma_a\gamma_b$ 的质量项）都会破坏[时间反演对称性](@entry_id:138094)。然而，当边界上恰好有 8 个[马约拉纳模](@entry_id:200998)时，可以构造一个特殊的、由四[费米子](@entry_id:146235)构成的[相互作用项](@entry_id:637283)，它既能保持所有对称性，又能完全打开[能隙](@entry_id:191975)，使 8 个[马约拉纳模](@entry_id:200998)融合形成一个唯一的、平庸的、有[能隙](@entry_id:191975)的[基态](@entry_id:150928)。这意味着，在相互作用存在的情况下，8 个[马约拉纳模](@entry_id:200998)不再受拓扑保护，可以被“湮灭”。因此，[拓扑不变量](@entry_id:138526)的性质从整数加法（$\mathbb{Z}$）变为模 8 的整数加法（$\mathbb{Z}_8$）。这个机制揭示了相互作用在拓扑[物态](@entry_id:139436)分类中的关键作用，并激发了对“[对称性保护的拓扑相](@entry_id:147660)”（SPT）的更深入研究。

至此，我们已经建立了描述拓扑[超导体](@entry_id:191025)的核心理论框架，从 BdG [哈密顿量](@entry_id:172864)到[对称性分类](@entry_id:184862)，再到体[不变量](@entry_id:148850)和边界态。在下一章中，我们将转向具体的材料体系和实验进展，探讨如何在真实世界中寻找和验证这些迷人的拓扑[物态](@entry_id:139436)。