## 引言
在[计算声学](@entry_id:172112)领域，[边界元法](@entry_id:141290)（Boundary Element Method, BEM）是一种用于求解声波传播与散射问题的强大数值技术。与[有限元法](@entry_id:749389)（FEM）等需要对整个计算域进行离散的“域方法”不同，BEM仅需对问题的边界进行离散化。这一特性使其在处理涉及无界域的外部声学问题（如潜艇的[声辐射](@entry_id:1120707)或飞机的[声散射](@entry_id:182666)）时具有无与伦比的优势，因为它能自然且精确地满足无穷远处的辐射条件，避免了人工截断边界和复杂的[吸收边界条件](@entry_id:164672)。

然而，BEM的强大功能背后是一套独特的数学理论和数值挑战。初学者常常面临的知识鸿沟在于，如何将抽象的亥姆霍兹[偏微分](@entry_id:194612)方程，通过格林函数和[积分变换](@entry_id:186209)，转化为可在计算机上求解的代数系统，并理解其内在的性质与陷阱。本文旨在系统性地填补这一鸿沟，为读者提供一条从理论基础到高级应用的清晰学习路径。

在本系列文章中，我们将分三章系统地探索声学BEM。第一章“原理与机制”将奠定数学基础，从亥姆霍兹方程的[基本解](@entry_id:184782)出发，推导[边界积分方程](@entry_id:746942)，并讨论离散化过程以及如何解决关键的“伪频”问题。第二章“应用与跨学科联系”将展示BEM在声学设计、[振动声学耦合](@entry_id:1133804)、[心理声学](@entry_id:900388)等领域的广泛应用，并探讨以[快速多极子方法](@entry_id:140932)为代表的现代加速算法。最后，第三章“动手实践”将提供一系列精心设计的编程练习，引导读者亲手实现一个BEM求解器，将理论知识转化为实践技能。让我们首先深入BEM的核心，从它的基本原理与数学机制开始。

## 原理与机制

本章旨在阐述声学边界元法（BEM）背后的基本原理和核心机制。我们将从控制波动现象的亥姆霍兹方程出发，推导其[基本解](@entry_id:184782)。随后，我们将展示如何利用[格林公式](@entry_id:173118)将定义在无限域中的[偏微分](@entry_id:194612)方程转化为仅在问题边界上定义的[积分方程](@entry_id:138643)。在此基础上，我们将详细介绍[边界积分算子](@entry_id:173789)及其数学性质，并探讨如何针对不同类型的边界条件（如声软、声硬和阻抗边界）构建具体的[边界积分方程](@entry_id:746942)（BIE）。最后，我们将讨论[边界积分方程](@entry_id:746942)在特定频率下可能出现的非唯一性问题，并介绍确保解唯一存在的组合场方法。本章的结尾将简要概述如何将连续的积分方程离散化为可供计算机求解的线性代数系统，为后续章节中详细的数值实现奠定基础。

### [亥姆霍兹方程](@entry_id:149977)的[基本解](@entry_id:184782)

时间谐波声学问题的数学描述基于[亥姆霍兹方程](@entry_id:149977)。在一个均匀、无粘性的流体介质中，声压的相量 $p$ 满足如下方程：
$$
\Delta p + k^2 p = 0
$$
其中 $\Delta$ 是[拉普拉斯算子](@entry_id:146319)，$k = \omega/c$ 是[声波数](@entry_id:1120717)，$\omega$ 是[角频率](@entry_id:261565)，$c$ 是介质中的声速。[边界元法](@entry_id:141290)的核心思想是利用一个特殊的解，即该方程在自由空间中的**[基本解](@entry_id:184782)**（fundamental solution），也称为**[格林函数](@entry_id:147802)**（Green's function）。

[基本解](@entry_id:184782) $G(\mathbf{x}, \mathbf{y})$ 物理上代表了位于源点 $\mathbf{y}$ 的一个单位点声源在场点 $\mathbf{x}$ 处产生的声压。因此，它满足一个带奇异源项的非齐次亥姆霍兹方程：
$$
(\nabla^2 + k^2) G(\mathbf{x}, \mathbf{y}) = -\delta(\mathbf{x} - \mathbf{y})
$$
其中 $\delta(\cdot)$ 是狄拉克-[德尔塔函数](@entry_id:273429)。对于无界域中的外问题（如散射问题），物理上合理的解必须代表从声源向无穷远处传播的波。这一要求通过施加**[索末菲辐射条件](@entry_id:168772)**（Sommerfeld radiation condition）来实现，该条件确保波在无穷远处是纯粹向外的。对于三维问题，该条件表述为：
$$
\lim_{r \to \infty} r \left( \frac{\partial G}{\partial r} - ikG \right) = 0
$$
其中 $r = |\mathbf{x} - \mathbf{y}|$。

为了推导出三维[基本解](@entry_id:184782)的具体形式，我们可以利用其物理对称性。 由于点源是各向同性的，其产生的场也应具有[球对称性](@entry_id:272852)，即 $G(\mathbf{x}, \mathbf{y})$ 仅依赖于源点与场点间的距离 $r$。在[球坐标系](@entry_id:167517)下，对于球[对称函数](@entry_id:177113) $g(r)$，[拉普拉斯算子](@entry_id:146319)简化为 $\Delta g(r) = g''(r) + \frac{2}{r}g'(r)$。在源点之外（$r > 0$），[基本解](@entry_id:184782)满足齐次亥姆霍兹方程：
$$
g''(r) + \frac{2}{r} g'(r) + k^2 g(r) = 0
$$
通过代换 $g(r) = u(r)/r$，上述方程可以简化为一个简单[谐振子](@entry_id:155622)方程 $u''(r) + k^2 u(r) = 0$。其通解为 $u(r) = C_1 e^{ikr} + C_2 e^{-ikr}$。因此，$g(r)$ 的通解为：
$$
g(r) = \frac{C_1 e^{ikr}}{r} + \frac{C_2 e^{-ikr}}{r}
$$
这两项分别代表了“出射波”（outgoing wave）和“入射波”（incoming wave）。[索末菲辐射条件](@entry_id:168772)的作用正是从中筛选出物理上有意义的解。通过计算可以验证，只有 $e^{ikr}/r$ 项满足[辐射条件](@entry_id:1130495)，而 $e^{-ikr}/r$ 项不满足。因此，解的形式必为 $g(r) = C_1 e^{ikr}/r$。

常数 $C_1$ 的值通过源点的强度来确定。我们将非齐次[亥姆霍兹方程](@entry_id:149977)在以 $\mathbf{y}$ 为中心、半径为 $\epsilon$ 的小球 $V_\epsilon$ 上积分，并利用[散度定理](@entry_id:143110)：
$$
\int_{V_\epsilon} (\nabla^2 + k^2) G \, dV = -1
$$
当 $\epsilon \to 0$ 时，$k^2 G$ 项的积分为零。利用散度定理，$\int_{V_\epsilon} \nabla^2 G \, dV = \int_{S_\epsilon} \frac{\partial G}{\partial n} \, dS$。计算可得，为了使该积分等于 $-1$，常数 $C_1$ 必须为 $\frac{1}{4\pi}$。

综上所述，三维[亥姆霍兹方程](@entry_id:149977)在自由空间中的出射[基本解](@entry_id:184782)为：
$$
G(\mathbf{x}, \mathbf{y}) = \frac{e^{ik|\mathbf{x}-\mathbf{y}|}}{4\pi |\mathbf{x}-\mathbf{y}|}
$$
这个函数是边界元法的基石。

### 从[场方程](@entry_id:1124935)到边界积分：[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)公式

边界元法的核心优势在于将问题的维度降低一维，即将需求解的三维（或二维）[偏微分](@entry_id:194612)方程转化为仅在问题边界上定义的积分方程。这一转化的数学工具是**[格林第二恒等式](@entry_id:169499)**，它与亥姆霍兹方程及[基本解](@entry_id:184782)相结合，构成了**[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)公式**（Kirchhoff-Helmholtz integral representation）。

考虑一个声学散射问题，其中声场 $p$ 在散射体 $\Omega$ 的外部区域 $\Omega_e$ 中满足齐次亥姆霍兹方程和[索末菲辐射条件](@entry_id:168772)。我们在区域 $\Omega_e$ 中对声场 $p$ 和[基本解](@entry_id:184782) $G$ 应用[格林第二恒等式](@entry_id:169499)。该区域的边界由散射体表面 $\Gamma$ 和一个半径为 $R$ 的[远场](@entry_id:269288)大球面 $S_R$ 构成。[格林公式](@entry_id:173118)给出：
$$
\int_{\Omega_e} (p \Delta G - G \Delta p) \, dV = \int_{\Gamma \cup S_R} \left( p \frac{\partial G}{\partial n} - G \frac{\partial p}{\partial n} \right) \, dS
$$
由于 $p$ 和 $G$ 都是[亥姆霍兹方程](@entry_id:149977)的解，左侧积分项为零。因此，场 $p$ 在区域内任意一点 $\mathbf{x}$ 的值可以通过其在边界上的值（狄利克雷数据 $p|_\Gamma$）和法向导数值（诺伊曼数据 $\partial_n p|_\Gamma$）来表示。

一个关键的步骤是证明当 $R \to \infty$ 时，在[远场](@entry_id:269288)球面 $S_R$ 上的积分会趋于零。 这一结论并非显而易见，因为球面面积 $4\pi R^2$ 会随 $R$ 增大而增大。其之所以成立，完全依赖于声场 $p$ 和[基本解](@entry_id:184782) $G$ 均满足[索末菲辐射条件](@entry_id:168772)。[辐射条件](@entry_id:1130495)不仅规定了 $p$ 和 $G$ 的衰减行为（$O(R^{-1})$），更重要的是规定了它们的径向导数与函数本身之间的特定相位关系。通过一个精巧的代数变换，可以将 $S_R$ 上的被积函数重写为：
$$
p\frac{\partial G}{\partial r} - G\frac{\partial p}{\partial r} = p\left(\frac{\partial G}{\partial r} - ikG\right) - G\left(\frac{\partial p}{\partial r} - ikp\right)
$$
由于[辐射条件](@entry_id:1130495)，括号中的两项都比 $p$ 或 $G$ 本身衰减得更快。具体来说，$p$ 满足的[辐射条件](@entry_id:1130495)意味着 $(\partial_r p - ikp)$ 是 $o(R^{-1})$，而 $G$ 满足的[辐射条件](@entry_id:1130495)可以更精确地表示为 $(\partial_r G - ikG)$ 是 $O(R^{-2})$。因此，整个被积函数的衰减速度快于 $O(R^{-3})$，这足以抵消球面面积 $O(R^2)$ 的增长，使得整个积分在 $R \to \infty$ 时收敛于零。

最终，我们得到了[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)公式，它将外部区域中任意一点 $\mathbf{x}$ 的声压 $p(\mathbf{x})$ 表示为仅涉及散射体边界 $\Gamma$ 上的积分：
$$
p(\mathbf{x}) = \int_{\Gamma} \left( G(\mathbf{x}, \mathbf{y}) \frac{\partial p(\mathbf{y})}{\partial n_y} - \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_y} p(\mathbf{y}) \right) \, d\Gamma_y
$$
这个公式是所有直接边界元法的出发点。它表明，只要我们知道了边界上的声压及其[法向导数](@entry_id:169511)，就可以确定整个外部声场。

### [边界积分算子](@entry_id:173789)及其性质

从[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)公式中，我们可以识别出两种基本的[积分变换](@entry_id:186209)，它们被称为**层势**（layer potentials）。将场点 $\mathbf{x}$ 移动到边界 $\Gamma$ 上，这些层势就定义了BEM中的四[类核](@entry_id:178267)心**[边界积分算子](@entry_id:173789)**。

1.  **单层势与单层算子 (Single-Layer Operator)**:
    单层势由分布在边界 $\Gamma$ 上的单极子源（密度为 $\phi$）产生。其对应的[边界积分算子](@entry_id:173789) $S$ (有时也记为 $V$) 定义为：
    $$
    S[\phi](\mathbf{x}) = \int_\Gamma G_k(\mathbf{x},\mathbf{y}) \phi(\mathbf{y})\, d\Gamma_y, \quad \mathbf{x} \in \Gamma
    $$
    该[算子的核](@entry_id:272757)函数 $G_k(\mathbf{x},\mathbf{y})$ 在 $\mathbf{x} \to \mathbf{y}$ 时表现为 $O(|\mathbf{x}-\mathbf{y}|^{-1})$，属于**弱奇异**核。在数学上，$S$ 是一个负一阶的[伪微分算子](@entry_id:192996)。这意味着它具有“平滑”效应，可以将一个[函数空间](@entry_id:143478)中的函数映射到更光滑的[函数空间](@entry_id:143478)中。具体而言，$S$ 是从[索伯列夫空间](@entry_id:141995) $H^s(\Gamma)$到 $H^{s+1}(\Gamma)$ 的一个[有界线性算子](@entry_id:180446)。例如，它将 $H^{-1/2}(\Gamma)$ 映射到 $H^{1/2}(\Gamma)$。

2.  **双层势与双层算子 (Double-Layer Operator)**:
    双层势由分布在边界 $\Gamma$ 上的偶极子源（密度为 $\psi$）产生。其对应的[边界积分算子](@entry_id:173789) $D$ (有时也记为 $K$) 定义为：
    $$
    D[\psi](\mathbf{x}) = \int_\Gamma \frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial n_y} \psi(\mathbf{y})\, d\Gamma_y, \quad \mathbf{x} \in \Gamma
    $$
    该[算子的核](@entry_id:272757)函数 $\partial_{n_y}G_k$ 在 $\mathbf{x} \to \mathbf{y}$ 时表现为 $O(|\mathbf{x}-\mathbf{y}|^{-2})$，属于**强奇异**核。这个积分必须在[柯西主值](@entry_id:192761)的意义下理解。$D$ 是一个零阶[伪微分算子](@entry_id:192996)，它保持函数的光滑性，即 $D: H^s(\Gamma) \to H^s(\Gamma)$ 是有界的。与 $S$ 不同，$D$ 通常不是一个[紧算子](@entry_id:139189)。

3.  **伴随双层算子 (Adjoint Double-Layer Operator)**:
    $D$ 的[伴随算子](@entry_id:140236) $D'$ (或 $K'$) 定义为：
    $$
    D'[\phi](\mathbf{x}) = \int_\Gamma \frac{\partial G_k(\mathbf{x},\mathbf{y})}{\partial n_x} \phi(\mathbf{y})\, d\Gamma_y, \quad \mathbf{x} \in \Gamma
    $$
    它也是一个零阶[伪微分算子](@entry_id:192996)。

4.  **[超奇异算子](@entry_id:1126297) (Hypersingular Operator)**:
    [超奇异算子](@entry_id:1126297) $H$ (或 $W$) 是对双层势求法向导数得到的，其核函数在 $\mathbf{x} \to \mathbf{y}$ 时表现为 $O(|\mathbf{x}-\mathbf{y}|^{-3})$，具有**超奇异性**。积分需要在Hadamard有限部分意义下理解。$H$ 是一个一阶[伪微分算子](@entry_id:192996)，具有“粗化”效应，将 $H^s(\Gamma)$ 映射到 $H^{s-1}(\Gamma)$。

当场点 $\mathbf{x}$ 从区域内部或外部趋近于边界 $\Gamma$ 时，层势的值会发生跳跃。这些**跳跃关系**（jump relations）是推导[边界积分方程](@entry_id:746942)的关键。例如，对于双层势，其在边界内外的迹（trace）相差一个由密度函数本身决定的量。正是这个跳跃，在[边界积分方程](@entry_id:746942)中引入了关键的“$\frac{1}{2}I$”项（$I$ 是[恒等算子](@entry_id:204623)），从而使得许多BIE成为第二类[Fredholm积分方程](@entry_id:277002)。 

### [边界积分方程](@entry_id:746942)的构建

[边界积分方程](@entry_id:746942)的构建通常采用**直接法**（direct method）。该方法从散射场 $p^s = p - p^{\text{inc}}$ 的[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)表达式出发。将场点 $\mathbf{x}$ 置于边界 $\Gamma$ 上，并利用层势的跳跃关系，可以得到联系散射场边界数据（即迹）$f = p^s|_\Gamma$ 和 $g = \partial_n p^s|_\Gamma$ 的方程组。这个方程组通常被称为**卡尔德隆投影**（Calderón identities），对于外问题，其[标准形式](@entry_id:153058)为：
$$
(\tfrac{1}{2}I + D)f = Sg
$$
$$
Hf = (\tfrac{1}{2}I - D')g
$$
根据具体的物理问题，边界上会给出关于总声场 $p = p^{\text{inc}} + p^s$ 的条件。我们将这些条件代入上述方程组，以消去一个未知量，从而得到只包含一个未知边界密度函数的积分方程。

-   **[狄利克雷问题](@entry_id:274408)（[声软边界](@entry_id:1131970)）**: 边界条件为 $p|_\Gamma = 0$，这意味着 $f = p^s|_\Gamma = -p^{\text{inc}}|_\Gamma$ 是已知的。未知量是[法向导数](@entry_id:169511) $g = \partial_n p^s|_\Gamma$。将 $f$ 代入第一个卡尔德隆恒等式，我们得到一个关于未知[法向导数](@entry_id:169511) $g$ 的**第一类[Fredholm积分方程](@entry_id:277002)**：
    $$
    Sg = -(\tfrac{1}{2}I + D)(p^{\text{inc}}|_\Gamma)
    $$
    该方程将未知的[法向导数](@entry_id:169511) $g$ 与已知的入射场数据直接联系起来。

-   **[诺伊曼问题](@entry_id:176713)（[声硬边界](@entry_id:1131968)）**: 边界条件为 $\partial_n p|_\Gamma = 0$，这意味着 $g = \partial_n p^s|_\Gamma = -\partial_n p^{\text{inc}}|_\Gamma$ 是已知的。未知量是声压 $f = p^s|_\Gamma$。将已知的 $g$ 代入第一个卡尔德隆恒等式，我们得到一个关于 $f$ 的**第二类[Fredholm积分方程](@entry_id:277002)**：
    $$
    (\tfrac{1}{2}I + D)f = -S(\partial_n p^{\text{inc}}|_\Gamma)
    $$
    由于第二类[Fredholm方程](@entry_id:266485)通常具有更好的数值性质，这成为求解[诺伊曼问题](@entry_id:176713)的首选方法。

-   **罗宾问题（阻抗边界）**: 边界条件为 $\partial_n p + Z p = 0$，其中 $Z$ 是阻抗。这给出了 $f$ 和 $g$ 之间的一个线性关系。将此关系代入卡尔德隆投影中的一个方程，即可消去一个未知量，从而得到一个关于另一个未知量的积分方程，该方程通常是第二类[Fredholm积分方程](@entry_id:277002)。

### 非唯一性问题：伪频

一个核心的理论与实践问题是：我们构建的[边界积分方程](@entry_id:746942)是否对所有波数 $k>0$ 都具有唯一解？答案是否定的。对于外问题，标准的BIEs会在一系列离散的波数（或频率）上失效，导致解不唯一。这些波数被称为**伪频**（spurious frequencies）或**[不规则频率](@entry_id:1126746)**（irregular frequencies）。

这个现象的根源在于，为**外问题**（exterior problem）建立的积分方程，其[解的唯一性](@entry_id:143619)却“意外地”与对应的**内问题**（interior problem）的共振特性联系在一起。具体来说：
- 用于求解外部**[狄利克雷问题](@entry_id:274408)**的BIE，其伪频恰好是内部区域 $\Omega$ 在**狄利克雷边界条件**（$p|_\Gamma=0$）下的[特征频率](@entry_id:911376)。 
- 用于求解外部**[诺伊曼问题](@entry_id:176713)**的BIE，其伪频恰好是内部区域 $\Omega$ 在**诺伊曼边界条件**（$\partial_n p|_\Gamma=0$）下的[特征频率](@entry_id:911376)。

在数学上，当波数 $k$ 是一个伪频时，齐次[边界积分方程](@entry_id:746942)（即右端项为零的方程）会存在非[平凡解](@entry_id:155162)。根据[Fredholm二择一](@entry_id:138045)理论，这意味着非[齐次方程](@entry_id:163650)的解要么不存在，要么不唯一。无论哪种情况，数值求解都会失败。

例如，对于外部声软散射问题，如果采用纯双层势表示 $p^s = D[\lambda]$，得到的BIE为 $(-\frac{1}{2}I + D)[\lambda] = -p^{\text{inc}}|_\Gamma$。当 $k$ 是内部[狄利克雷问题](@entry_id:274408)的[特征频率](@entry_id:911376)时，相应的[齐次方程](@entry_id:163650)存在非[平凡解](@entry_id:155162)，导致整个算子不可逆。

### 保证唯一性：组合场方法

为了克服伪频问题，发展出了多种方法，其中最著名和最可靠的是**[组合场积分方程](@entry_id:747497)**（Combined Field Integral Equation, CFIE）方法。其思想是[线性组合](@entry_id:154743)两个不同的[边界积分方程](@entry_id:746942)，使得组合后的方程在所有实数波数 $k>0$ 下都具有唯一解。

一种广泛应用的CFIE是基于**间接法**（indirect method）的**Brakhage-Leis-Panich**公式。它不再使用基尔霍夫-亥姆霍兹表达式，而是直接假设散射场 $p^s$ 可以表示为一个单层势和一个双层势的线性组合，且两者由**同一个**未知密度函数 $\lambda$ 驱动：
$$
p^s(\mathbf{x}) = (D\lambda)(\mathbf{x}) - i\eta (S\lambda)(\mathbf{x})
$$
这里的关键在于引入了一个**复数[耦合参数](@entry_id:747983)**，通常取为 $-i\eta$，其中 $\eta$ 是一个实常数（$\eta \neq 0$）。

对上式取边界上的迹并施加狄利克雷边界条件 $p^s|_\Gamma = -p^{\text{inc}}|_\Gamma$，我们得到一个关于 $\lambda$ 的**第二类[Fredholm积分方程](@entry_id:277002)**：
$$
(-\tfrac{1}{2}I + D - i\eta S)\lambda = -p^{\text{inc}}|_\Gamma
$$
可以严格证明，由于耦合参数的虚部存在，这个组合算子 $(-\tfrac{1}{2}I + D - i\eta S)$ 对于所有实数 $k>0$ 都是可逆的。证明的思路是：假设[齐次方程](@entry_id:163650)存在非[平凡解](@entry_id:155162) $\lambda_0$，它生成的[势场](@entry_id:143025)在外部为零。利用[格林公式](@entry_id:173118)和内外边界的跳跃关系，可以推导出该[势场](@entry_id:143025)在内部区域的能量关系。最终会发现，能量关系的一边是纯实数，而另一边是纯虚数（这正是因为耦合参数 $i\eta$），这迫使两者都必须为零，从而导出 $\lambda_0=0$ 的矛盾。 这种方法有效地消除了所有伪频。

类似的组合思想也可以应用于直接法，形成所谓的**[Burton-Miller公式](@entry_id:1121956)**，即[线性组合](@entry_id:154743)直接法的狄利克雷BIE和诺伊曼BIE。

### 离散化：从积分方程到线性系统

最后一步是将连续的[边界积分方程](@entry_id:746942)转化为可由计算机求解的代数方程组。最常用的方法是**[配置法](@entry_id:138885)**（Collocation Method），它属于[加权余量法](@entry_id:756686)的一种。

离散化过程如下：
1.  **[网格划分](@entry_id:1127808)**：将散射体边界 $\Gamma$ 剖分为一个由 $N_e$ 个小单元（如三角形）组成的网格。网格共有 $N_n$ 个节点。

2.  **基函数展开**：将未知的边界密度函数（例如声软问题中的[法向导数](@entry_id:169511) $g$）用一组定义在网格上的**基函数**（basis functions）的[线性组合](@entry_id:154743)来近似。常见的选择有：
    - **分片常数基函数**：假设 $g$ 在每个单元上为常数。未知量是这 $N_e$ 个常数值。
    $$ g(\mathbf{y}) \approx \sum_{j=1}^{N_e} x_j \chi_j(\mathbf{y}) $$
    其中 $\chi_j$ 是第 $j$ 个单元的特征函数。
    - **分片线性基函数**：假设 $g$ 在每个单元上线性变化，其值由节点值决定。未知量是 $N_n$ 个节点上的函数值。
    $$ g(\mathbf{y}) \approx \sum_{j=1}^{N_n} x_j N_j(\mathbf{y}) $$
    其中 $N_j$ 是与第 $j$ 个节点关联的“帽状”基函数。

3.  **[配置点](@entry_id:169000)**：选择一组**[配置点](@entry_id:169000)**（collocation points）$\{\mathbf{x}_i\}$，并在这些点上强制要求[积分方程](@entry_id:138643)精确成立。[配置点](@entry_id:169000)的选择通常与基函数的选择相匹配：
    - 对于分片常数基函数，通常选择每个单元的**形心**作为[配置点](@entry_id:169000)。
    - 对于分片线性基函数，通常选择网格的**节点**作为[配置点](@entry_id:169000)。

4.  **形成线性系统**：将基函数展开式代入BIE，并在每个[配置点](@entry_id:169000) $\mathbf{x}_i$ 上计算该方程，就得到一个线性代数方程组 $A\mathbf{x} = \mathbf{b}$。

以声软问题的直接BIE为例，采用分片常[数基](@entry_id:634389)函数和形心配置，得到的方程组中：
- 未知向量 $\mathbf{x}$ 的分量 $x_j$ 是第 $j$ 个单元上的未知[法向导数](@entry_id:169511)值。
- 矩阵 $A$ 的元素 $A_{ij}$ 表示第 $j$ 个单元上的单[位密度](@entry_id:1129991)在第 $i$ 个[配置点](@entry_id:169000)（第 $i$ 个单元的形心）处产生的单层势：
  $$
  A_{ij} = \int_{\Gamma_j} G_k(\mathbf{x}_i, \mathbf{y}) \, d\Gamma_y
  $$
- 右端向量 $\mathbf{b}$ 的分量 $b_i$ 包含所有已知量在[配置点](@entry_id:169000) $\mathbf{x}_i$ 上的贡献，由 $Sg = -(\tfrac{1}{2}I + D)p^{\text{inc}}$ 给出：
  $$
  b_i = -\left( \frac{1}{2} p^{\text{inc}}(\mathbf{x}_i) + \int_{\Gamma} \frac{\partial G_k(\mathbf{x}_i, \mathbf{y})}{\partial n_y} p^{\text{inc}}(\mathbf{y}) \, d\Gamma_y \right)
  $$
  (这里假设 $p^{\text{inc}}$ 在整个边界 $\Gamma$ 上进行积分)。

求解这个稠密的、复数值的[线性系统](@entry_id:147850) $A\mathbf{x}=\mathbf{b}$，即可得到未知边界函数的离散近似。一旦边界上的声压和[法向导数](@entry_id:169511)都已知，便可利用[基尔霍夫-亥姆霍兹积分](@entry_id:1126941)公式计算外部声场中任意一点的声压。计算矩阵元素 $A_{ij}$ 和右端项 $b_i$ 涉及在单元上的积分，特别是当[配置点](@entry_id:169000) $\mathbf{x}_i$ 位于积分单元 $\Gamma_j$ 上时，需要处理[核函数](@entry_id:145324)的奇异性，这是BEM数值实现中的一个核心挑战。