## 引言
经典[连续介质力学](@entry_id:155125)在过去两个世纪中为工程科学的发展奠定了坚实的理论基础，然而，其基于位移场空间导数的数学框架在面对材料内部出现裂纹、空洞等不连续性时，遇到了根本性的困难。在这些不连续点，位移场不再光滑，其导数失去定义，导致传统控制方程失效。为了突破这一瓶颈，[近场动力学](@entry_id:191791)（Peridynamics, PD）理论应运而生，它通过一种全新的非局域作用思想，彻底重构了固体力学的数学基础。

本文旨在为读者提供一个关于[近场动力学](@entry_id:191791)理论的全面而深入的介绍，系统性地解决经典理论在处理[不连续性](@entry_id:144108)时的局限性。我们将引领读者从最基本的运动学概念出发，逐步构建起一个不依赖空间导数、转而使用积分方程来描述物体变形与内力响应的力学框架。

在接下来的内容中，您将学习到：
*   **原理与机制**：我们将深入探讨[近场动力学](@entry_id:191791)的核心概念，如“键”、“视域”和“键伸长”，并详细介绍从简单的键基模型到普适的态基模型的发展历程，阐明其如何描述各种材料行为并自然地引入损伤。
*   **应用与跨学科联系**：本章将展示[近场动力学](@entry_id:191791)在[断裂力学](@entry_id:141480)、复杂[材料建模](@entry_id:751724)（如各向异性与[弹塑性](@entry_id:193198)）、多物理场耦合问题（如热-力耦合）等前沿领域的强大应用，并揭示其如何与经典理论建立联系。
*   **动手实践**：通过一系列精心设计的计算练习，您将有机会亲手实现[近场动力学](@entry_id:191791)的基本算法，将抽象的理论知识转化为具体的计算能力，加深对非局域理论的理解。

通过这三个章节的逐层递进，本文将为您揭示[近场动力学](@entry_id:191791)如何为模拟材料从连续变形到断裂失效的全过程提供一个统一而强大的理论工具。

## 原理与机制

本章旨在深入阐述[近场动力学](@entry_id:191791)（Peridynamics, PD）理论的核心原理与力学机制。我们将从其独特的非局域[运动学](@entry_id:173318)描述出发，系统地建立其[本构关系](@entry_id:186508)，并最终探讨其在模拟材料损伤与断裂方面的强大能力。我们将摒弃经典[连续介质力学](@entry_id:155125)中对变形梯度的依赖，转而构建一个基于积分形式的、在数学上更具普适性的力学框架。

### 基本运动学：键与伸长

经典[连续介质力学](@entry_id:155125)的基石是假设物[质点](@entry_id:186768)间的相对运动在局部可以由一个线性映射——变形梯度——来近似。然而，当材料内部出现裂纹等[不连续性](@entry_id:144108)时，位移场不再光滑，变形梯度也随之失去定义，这给经典理论带来了根本性的挑战。[近场动力学](@entry_id:191791)通过一种全新的[运动学](@entry_id:173318)描述方式，从根本上规避了这一问题。

#### 键、伸长与视域

在[近场动力学](@entry_id:191791)中，我们关注的是物质点对之间的相互作用，而非单个物质点的无限小邻域。考虑两个物[质点](@entry_id:186768)，其在参考构型中的位置分别为 $\mathbf{x}$ 和 $\mathbf{x}'$。连接这两点的矢量被称为**键 (bond)**，记为 $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$。经过变形后，这两点运动到新的位置 $\mathbf{y}(\mathbf{x}, t)$ 和 $\mathbf{y}(\mathbf{x}', t)$。此时，变形后的键矢量为 $\boldsymbol{\xi} + \boldsymbol{\eta} = \mathbf{y}(\mathbf{x}', t) - \mathbf{y}(\mathbf{x}, t)$，其中 $\boldsymbol{\eta} = \mathbf{u}(\mathbf{x}', t) - \mathbf{u}(\mathbf{x}, t)$ 是两点的**相对位移**，$\mathbf{u}$ 是位移场。

[近场动力学](@entry_id:191791)中最核心的运动学度量是**键伸长 (bond stretch)** $s$，它被定义为键的相对伸长率：
$$
s = \frac{|\boldsymbol{\xi} + \boldsymbol{\eta}| - |\boldsymbol{\xi}|}{|\boldsymbol{\xi}|}
$$
这个标量值直接描述了两个物质点之间距离的变化，是构建本构关系的基础。

[近场动力学](@entry_id:191791)的一个核心假设是**非局域性 (nonlocality)**。一个物质点 $\mathbf{x}$ 并非与其所有其他物质点都发生相互作用，而是只与其一定范围内的点发生作用。这个范围被称为**视域 (horizon)**，通常是一个以 $\mathbf{x}$ 为中心、半径为 $\delta$ 的球形区域 $H_{\mathbf{x}}$。因此，$\delta$ 是[近场动力学](@entry_id:191791)模型中一个內禀的长度尺度，它决定了非局域相互作用的范围 [@problem_id:2667647]。

#### 与经典应变理论的对比

键伸长 $s$ 与经典理论中的[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\top})$ 在概念上存在本质区别 [@problem_id:2667612]：

1.  **客观性 (Objectivity)**：键伸长 $s$ 的定义只涉及点间距离，这是一个几何量。在任意刚体运动（包括有限旋转）下，点间距离保持不变，因此 $s$ 是完全客观的。相比之下，[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$ 仅在无穷小[刚体转动](@entry_id:191086)下为零；对于有限转动，即使物体未发生任何实际变形（所有键的 $s=0$），$\boldsymbol{\varepsilon}$ 也可能非零。

2.  **[适用范围](@entry_id:636189)**：$s$ 的定义不依赖于变形的大小，因此它天然适用于[大应变](@entry_id:751152)和大转动问题。而 $\boldsymbol{\varepsilon}$ 是通过线性化[格林-拉格朗日应变张量](@entry_id:187745)得到的，仅在[位移梯度](@entry_id:165352)远小于1时（即小应变和小转动）有效。

3.  **局域性与[非局域性](@entry_id:140165)**：$\boldsymbol{\varepsilon}$ 是一个**局域**量，它在单一点 $\mathbf{x}$ 上通过位移场的梯度定义。而 $s$ 是一个**非局域**量，因为它依赖于两个不同点 $\mathbf{x}$ 和 $\mathbf{x}'$ 的位移。

4.  **对不连续性的处理**：这是[近场动力学](@entry_id:191791)最显著的优势。当[位移场](@entry_id:141476) $\mathbf{u}$ 存在跳跃不连续（例如在裂纹面两侧）时，其梯度 $\nabla\mathbf{u}$ 在数学上是无定义的，因此经典[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 也无法计算。然而，即使键跨越了[不连续面](@entry_id:180188)，只要键两端的点 $\mathbf{x}$ 和 $\mathbf{x}'$ 的位移是确定的，它们的相对位移 $\boldsymbol{\eta}$ 和键伸长 $s$ 就总是良定义的。这使得[近场动力学](@entry_id:191791)能够自然地描述裂纹等不连续现象的产生和演化 [@problem_id:2667612] [@problem_id:2667608]。

尽管存在这些区别，[近场动力学](@entry_id:191791)与经典理论之间也存在深刻的联系。可以证明，当[位移场](@entry_id:141476)足够光滑时，在 $\boldsymbol{\xi} \to 0$ 的极限下，键伸长 $s$ 趋近于经典应变张量在键方向上的法向分量 [@problem_id:2667612]：
$$
s \approx \mathbf{n} \cdot \boldsymbol{\varepsilon}(\mathbf{x}, t) \mathbf{n}
$$
其中 $\mathbf{n} = \boldsymbol{\xi} / |\boldsymbol{\xi}|$ 是键方向的单位矢量。这一**[对应原理](@entry_id:155778) (correspondence principle)** 确保了在宏观均匀变形下，[近场动力学](@entry_id:191791)能够回归到经典[弹性理论](@entry_id:184142)。

最后，视域 $\delta$ 的存在意味着[近场动力学](@entry_id:191791)方程本质上是一个积分算子，它会对[位移场](@entry_id:141476)进行[空间平均](@entry_id:203499)。这种平均效应使得模型天然地对高波数（短波长）的变形模式不敏感，表现为一种**低通滤波**特性。因此，任何尺寸远小于 $\delta$ 的特征都将被“平滑”掉，无法被模型精确解析。这与[数值离散化](@entry_id:752782)参数 $h$（如节点间距）是两个独立的概念：无论 $h$ 多么小，都无法消除由物理参数 $\delta$ 决定的內禀非局域性 [@problem_id:2667647]。

### 本构模型：从键到态

基于上述[运动学](@entry_id:173318)描述，下一步是建立变形与力之间的关系，即[本构模型](@entry_id:174726)。[近场动力学](@entry_id:191791)提供了一个层次化的建模框架，从简单的键基模型到普适的态[基模](@entry_id:165201)型。

#### 键基[近场动力学](@entry_id:191791)

最简单的模型是**键基 (bond-based)** [近场动力学](@entry_id:191791)。其核心假设是：任意一对物质点之间的相互作用力**只依赖于连接它们的那个键自身**的变形。

对于一个**微弹性 (microelastic)** 材料，点对间的力可以从一个标量微[势能](@entry_id:748988) $\omega$ 导出。如果材料还是**各向同性 (isotropic)** 的，那么势能 $\omega$ 只能依赖于变形后键的长度 $|\boldsymbol{\xi}+\boldsymbol{\eta}|$，因为这是唯一不受[坐标系](@entry_id:156346)旋转影响的标量。由此推论，势能对变形后键矢量 $\mathbf{Y} = \boldsymbol{\xi}+\boldsymbol{\eta}$ 的梯度，即点[对力](@entry_id:159909) $\mathbf{f}$，必然与 $\mathbf{Y}$ 本身共线 [@problem_id:2667588]。这意味着在键基各向同性模型中，点对力必然是**中心力 (central force)**，即力的方向总是沿着连接两点的直线（在当前构型中）。

对于线性微弹性行为，可以假设力的标量大小与键伸长 $s$ 成正比。因此，点对力矢量可以写为：
$$
\mathbf{f} = c(|\boldsymbol{\xi}|) s \mathbf{e}
$$
其中 $c(|\boldsymbol{\xi}|) \ge 0$ 是一个依赖于初始[键长](@entry_id:144592)的**微模量 (micromodulus)** 函数，它表征了键的刚度；$\mathbf{e} = (\boldsymbol{\xi}+\boldsymbol{\eta})/|\boldsymbol{\xi}+\boldsymbol{\eta}|$ 是变形后键方向的单位矢量。

键基模型以其简洁性而著称，但其[中心力](@entry_id:267832)假设也带来了严重的局限性。可以证明，这种模型在三维情况下预测的泊松比 $\nu$ 恒为 $1/4$，在二维情况下恒为 $1/3$。这是因为它对[剪切变形](@entry_id:170920)（即键的切向相对位移）在一阶上没有抵抗力 [@problem_id:2667612]。为了模拟具有任意泊松比的材料，必须超越键基框架。

#### 态基[近场动力学](@entry_id:191791)

**态基 (state-based)** [近场动力学](@entry_id:191791)通过一个更广义的假设克服了键[基模](@entry_id:165201)型的局限：作用于一个键上的力可以依赖于**视域内所有键**的集体变形状态。这引入了**态 (state)** 的概念，一个态是一个将视域内每个键 $\boldsymbol{\xi}$ 映射到一个值（标量、矢量或张量）的函数。例如，力态 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ 表示由键 $\boldsymbol{\xi}$ 施加在中心点上的力密度。

##### 常规态[基模](@entry_id:165201)型 (Ordinary State-Based Models)

常规态[基模](@entry_id:165201)型（OSB）是态基模型的一个简化版本，它依然保留了“力与键共线”的假设，但力的**大小**可以依赖于邻域的集体行为。具体而言，OS[B模型](@entry_id:159413)将邻域的变形分解为**体积变形 (volumetric)** 和**剪切变形 (deviatoric)** 两部分，并分别用独立的材料参数——[体积模量](@entry_id:160069) $\kappa$ 和[剪切模量](@entry_id:167228) $\mu$——来描述 [@problem_id:2667632]。

首先，定义一个标量场**膨胀率 (dilatation)** $\theta(\mathbf{x})$，它通过对视域内所有键的伸长分量进行加权平均得到，代表了点 $\mathbf{x}$ 处的局部体积变化。然后，每个键的伸长可以分解为一个由 $\theta(\mathbf{x})$ 决定的球量[部分和](@entry_id:162077)一个偏量部分 $e^d$。力态 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ 于是被构建为两部分之和：一部分由集体膨胀率 $\theta(\mathbf{x})$ 和[体积模量](@entry_id:160069) $\kappa$ 驱动，另一部分由单个键的偏量伸长 $e^d$ 和剪切模量 $\mu$ 驱动。一个典型的OSB力态表达式为 [@problem_id:2667632]：
$$
\mathbf{T}(\mathbf{x})\langle \boldsymbol{\xi} \rangle = \left[ \kappa\,\theta(\mathbf{x})\,\omega(|\boldsymbol{\xi}|)\,|\boldsymbol{\xi}| + 2\mu\,\omega(|\boldsymbol{\xi}|)\,e^d(\mathbf{x},\boldsymbol{\xi}) \right] \frac{\boldsymbol{\xi}}{|\boldsymbol{\xi}|}
$$
其中 $\omega$ 是一个[影响函数](@entry_id:168646)。通过独立地调节 $\kappa$ 和 $\mu$，OS[B模型](@entry_id:159413)可以模拟具有任意物理允许泊松比的材料，从而极大地扩展了模型的适用性。

##### 非常规态基模型 (Non-Ordinary State-Based Models)

非常规态[基模](@entry_id:165201)型（NOSB）是[近场动力学](@entry_id:191791)中最普适的框架。它彻底抛弃了力与键共线的限制，允许力态 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ 与键 $\boldsymbol{\xi}$ 之间存在任意夹角。这使得模型能够描述最一般的材料响应，并与经典连续介质力学建立完美的对应关系 [@problem_id:2667661]。

NOS[B模型](@entry_id:159413)的核心思想是“先计算，后分配”。首先，利用视域内所有键的变形信息，计算出一个等效的**非局域变形梯度** $\widehat{\mathbf{F}}(\mathbf{x})$。这个 $\widehat{\mathbf{F}}$ 被定义为在加权最小二乘意义下，将参考构型中的键 $\boldsymbol{\xi}$ 映射到当前构型中键 $\mathbf{Y}\langle\boldsymbol{\xi}\rangle$ 的最佳线性变换。其表达式为 [@problem_id:2667661] [@problem_id:2667635]：
$$
\widehat{\mathbf{F}}(\mathbf{x}) = \left(\int_{\mathcal{H}_{\mathbf{x}}} \omega(|\boldsymbol{\xi}|)\,\mathbf{Y}\langle \boldsymbol{\xi} \rangle \otimes \boldsymbol{\xi}\,\mathrm{d}V_{\boldsymbol{\xi}}\right) \mathbf{M}(\mathbf{x})^{-1}
$$
其中 $\mathbf{M}(\mathbf{x})$ 是一个被称为**形状张量 (shape tensor)** 的[二阶张量](@entry_id:199780)，它只依赖于参考构型和[影响函数](@entry_id:168646)：
$$
\mathbf{M}(\mathbf{x}) = \int_{\mathcal{H}_{\mathbf{x}}} \omega(|\boldsymbol{\xi}|)\,\boldsymbol{\xi} \otimes \boldsymbol{\xi}\,\mathrm{d}V_{\boldsymbol{\xi}}
$$
一旦获得了非局域变形梯度 $\widehat{\mathbf{F}}$，我们就可以像在经典理论中一样，利用**任何经典[本构关系](@entry_id:186508)**（例如，胡克定律或更复杂的[弹塑性](@entry_id:193198)模型）来计算[应力张量](@entry_id:148973)，如[第一皮奥拉-基尔霍夫应力](@entry_id:163971) $\mathbf{P}$。

最后一步，是将宏观的应力 $\mathbf{P}$ “分配”回每个微观的键上，形成力态 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$。这一分配通过以下关系实现 [@problem_id:2667661] [@problem_id:2667635]：
$$
\mathbf{T}\langle \boldsymbol{\xi} \rangle = \omega(|\boldsymbol{\xi}|) \mathbf{P}(\mathbf{x}) \mathbf{M}(\mathbf{x})^{-1} \boldsymbol{\xi}
$$
通过这种方式，NOS[B模型](@entry_id:159413)可以完全输入任何经典材料模型，并将其转化为一个非局域的[近场动力学](@entry_id:191791)模型，从而能够模拟具有任意泊松比和其他复杂行为的材料，同时保留了[近场动力学](@entry_id:191791)处理[不连续性](@entry_id:144108)的能力。

作为一个具体例子，对于一个三维、视域为单位半径球、[影响函数](@entry_id:168646) $\omega=1$ 的情况，形状张量 $\mathbf{M}$ 为 $\frac{4\pi}{15}\mathbf{I}$，其中 $\mathbf{I}$ 是单位张量。因此，其逆张量中的系数为 $\alpha = \frac{15}{4\pi}$ [@problem_id:2667621]。

### 断裂与[损伤建模](@entry_id:202568)

[近场动力学](@entry_id:191791)最成功的应用领域之一是材料的断裂与损伤模拟。其非局域的、基于积分的性质使其能够自然地引入和演化裂纹，而无需像有限元法那样需要额外的判据和网格重剖分技术。

#### 基于临界伸长的[脆性断裂](@entry_id:158949)

最简单的损伤模型是基于**临界键伸长** $s_c$ 的[脆性断裂](@entry_id:158949)准则。其核心思想是：当一个键的伸长 $s$ 首次达到或超过预设的临界值 $s_c$ 时，该键发生断裂。

一个关键的物理要求是损伤的**不[可逆性](@entry_id:143146) (irreversibility)**。一旦一个键断裂，它就永久失去了承载能力，即使后续变形使得其理论伸长值回到 $s_c$ 以下。为了在数学上实现这一点，我们引入一个历史依赖的布尔变量 $\mu(\mathbf{x}, \mathbf{x}', t) \in \{0, 1\}$ 来表示键的状态（1代表完好，0代表断裂）。$\mu$ 的值不取决于当前的伸长 $s(t)$，而是取决于到当前时刻为止所经历的**最大伸长** [@problem_id:25867586]：
$$
\mu(\mathbf{x},\mathbf{x}',t) = H\Big(s_{c} - \sup_{0 \le \tau \le t} s(\mathbf{x},\mathbf{x}',\tau)\Big)
$$
其中 $H(\cdot)$ 是赫维赛德[阶跃函数](@entry_id:159192)。一旦在某个时刻 $t^*$，伸长 $s(t^*)$ 超过 $s_c$，那么历史最大伸长就会永久地大于 $s_c$，从而 $\mu$ 将永久地变为0。

点对力 $\mathbf{f}$ 于是被修正为 $\mu \cdot \mathbf{f}_{\text{intact}}$，其中 $\mathbf{f}_{\text{intact}}$ 是完好键的力。当 $\mu=0$ 时，力自动变为零。同时，当键断裂时，其储存的[弹性势能](@entry_id:168893) $\psi(s_c)$ 被瞬间释放，这部分能量被视为耗散掉了，通常转化为断裂[表面能](@entry_id:161228)和热能。

基于键的断裂状态，我们可以在每个物质点 $\mathbf{x}$ 处定义一个局域的**[损伤变量](@entry_id:197066) (damage variable)** $d(\mathbf{x}, t)$，它被定义为该点视域内断裂键的加权比例 [@problem_id:25867586]：
$$
d(\mathbf{x},t) = 1 - \frac{\int_{\mathcal{H}_{\mathbf{x}}} \mu(\mathbf{x},\mathbf{x}',t)\, \omega(|\mathbf{x}' - \mathbf{x}|) \,\mathrm{d}V_{\mathbf{x}'}}{\int_{\mathcal{H}_{\mathbf{x}}} \omega(|\mathbf{x}' - \mathbf{x}|) \,\mathrm{d}V_{\mathbf{x}'}}
$$
[损伤变量](@entry_id:197066) $d$ 的范围从0（完全完好）到1（邻域内所有键均断裂），它提供了一个连续的场来描述材料从完好到完全失效的[演化过程](@entry_id:175749)。

#### 与宏观断裂能的联系

在上述模型中，$s_c$ 是一个微观参数。然而，在工程应用中，我们更关心的是宏观的材料属性，例如**断裂能** $G_c$（或[断裂韧性](@entry_id:157609)）。$G_c$ 定义为材料中每形成一个单位面积的新裂纹所需要耗散的能量。为了使[近场动力学](@entry_id:191791)模型具有物理预测能力，必须在微观参数 $s_c$ 和宏观属性 $G_c$ 之间建立联系。

可以证明，材料的断裂能 $G_c$ 等于裂纹面单位面积上所有被切断的键在断裂瞬间所储存的弹性势能之和。对于线性微弹性材料，单个键在断裂时储存的能量与 $s_c^2$ 成正比。因此，总的断裂能 $G_c$ 可以表示为 [@problem_id:2667609]：
$$
G_c = \int_{\text{断裂面几何}} \frac{1}{2} c(|\boldsymbol{\xi}|) s_c^2 |\boldsymbol{\xi}| \, \mathrm{d}(\text{几何}) = \frac{1}{2} s_c^2 A(\delta)
$$
其中积分项 $A(\delta)$ 仅依赖于微模量函数 $c$ 和视域 $\delta$ 的几何形状。

从上式可以看出，如果将 $s_c$ 视为一个固定的材料常数，那么模型预测的[断裂能](@entry_id:174458) $G_c$ 将会随着模型参数 $\delta$ 的改变而改变，这是不符合物理事实的。为了保证 $G_c$ 是一个与模型参数无关的真实材料常数，我们必须反过来，让微观的 $s_c$ 依赖于 $\delta$ [@problem_id:2667609]：
$$
s_c(\delta) = \sqrt{\frac{2G_c}{A(\delta)}}
$$
通过这种方式，我们可以利用宏观实验测得的断裂能 $G_c$ 来校准[近场动力学](@entry_id:191791)模型中的临界伸长参数。这确保了无论我们选择多大的视域 $\delta$ 来进行模拟，模型所耗散的能量都与材料的真实物理属性保持一致，从而使得模拟结果具有客观性和预测性。