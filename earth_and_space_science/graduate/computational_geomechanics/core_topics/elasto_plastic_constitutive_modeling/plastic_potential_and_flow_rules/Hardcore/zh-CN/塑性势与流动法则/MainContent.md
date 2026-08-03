## 引言
在弹塑性力学领域，屈服面定义了材料从弹性向塑性行为转变的界限。然而，一旦应力触及此边界，材料将如何变形？其不可恢复的塑性应变将朝哪个方向发展？仅仅依靠屈服准则无法回答这些问题，这构成了描述完整塑性响应的关键知识缺口。本文旨在填补这一缺口，深入探讨控制塑性变形方向与模式的核心概念——**塑性势**与**流动法则**。

本文将通过三个循序渐进的章节，带领读者全面掌握这一主题。首先，在“**原理与机制**”中，我们将建立正交流动法则的数学框架，辨析关联与非关联流动的本质区别，并阐明其对剪胀、材料稳定性和本构关系的影响。接着，在“**应用与跨学科交叉**”部分，我们将展示这些理论如何在岩土工程、计算力学和断裂力学等领域解决实际问题，突显其强大的应用价值。最后，通过一系列精心设计的“**动手实践**”，读者将有机会亲手实现并分析基于这些原理的本构模型。

现在，让我们从塑性流动理论的基石——塑性势的定义及其与应变方向的关系——开始我们的探索。

## 原理与机制

在上一章中，我们探讨了屈服面作为区分材料弹性行为和塑性行为的边界。一旦应力状态达到并试图超越这个边界，材料将发生不可恢复的塑性变形。然而，仅有屈服面不足以完全描述塑性行为。我们还需要一个法则来规定塑性应变增量的方向和演化。本章将深入探讨控制塑性流动方向的核心概念：**塑性势**（plastic potential）和**流动法则**（flow rule）。这些原理是构建精确、稳健的岩土材料本构模型，并将其应用于计算分析的基石。

### 塑性势与正交流动法则

为了描述塑性应变增量的方向，我们引入一个在应力空间中定义的标量函数，称为**塑性势函数**（plastic potential function），记为 $g(\boldsymbol{\sigma})$。这个函数的等值面（$g=\text{常数}$）构成了一族曲面。塑性流动的基本假设，即**正交流动法则**（normality rule），指出塑性应变增量张量 $d\boldsymbol{\varepsilon}^p$ 的方向与塑性势函数 $g$ 在当前应力点 $\boldsymbol{\sigma}$ 的梯度方向一致。

数学上，正交流动法则表达为：
$$
d\boldsymbol{\varepsilon}^p = d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
其中，$d\lambda$ 是一个非负标量，称为**塑性乘子**（plastic multiplier）。梯度 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 是一个二阶张量，其分量为 $(\frac{\partial g}{\partial \boldsymbol{\sigma}})_{ij} = \frac{\partial g}{\partial \sigma_{ij}}$。这个梯度向量在几何上正交（垂直）于 $g(\boldsymbol{\sigma})$ 的等值面。

塑性乘子 $d\lambda$ 决定了塑性应变增量的**大小**。在塑性加载过程中，$d\lambda > 0$；如果应力状态保持在屈服面内部（弹性卸载或中性加载），则 $d\lambda = 0$，不产生塑性应变。塑性乘子的大小并非任意，而是由**一致性条件**（consistency condition）所决定，我们将在后续章节中详细讨论。

一个重要的推论是，对于各向同性材料，其力学行为不应依赖于坐标系的选择。因此，其屈服函数和塑性势函数都必须是应力张量[不变量](@entry_id:148850)的函数，例如应力张量的第一不变量 $I_1 = \operatorname{tr}(\boldsymbol{\sigma})$、偏应力张量的第二不变量 $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$ 和第三不变量 $J_3 = \det(\boldsymbol{s})$。在这种情况下，可以证明一个基本性质：**共轴性**（coaxiality）。即应力张量 $\boldsymbol{\sigma}$ 和塑性应变率（或增量）张量 $d\boldsymbol{\varepsilon}^p$ 具有相同的主方向 [@problem_id:3551064]。这是因为，当 $g$ 是应力不变量的函数时，其梯度 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 可以表示为 $\boldsymbol{\sigma}$ 和单位张量 $\boldsymbol{I}$ 的线性组合，这意味着 $\boldsymbol{\sigma}$ 的任何一个特征向量也必然是 $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ 的特征向量。这一性质极大地简化了在主应力空间中的分析。

### 关联与非关联流动法则

根据塑性势函数 $g$ 与屈服函数 $f$ 之间的关系，流动法则可以分为两类：

1.  **关联流动法则 (Associated Flow Rule)**：当塑性势函数与屈服函数完全相同时，即 $g = f$，我们称之为关联流动法则。在这种情况下，塑性应变增量的方向垂直于屈服面本身。这一假设在金属塑性理论中被广泛采用，因为它与 Drucker 稳定性公设直接相关，保证了模型的内在稳定性。

2.  **非关联流动法则 (Non-Associated Flow Rule)**：当塑性势函数与屈服函数不同时，即 $g \neq f$，我们称之为非关联流动法则。这意味着塑性应变增量的方向垂直于塑性势面，但与屈服面斜交。

对于许多岩土材料，如砂土、黏土和岩石，实验观察表明，若采用关联流动法则，通常会高估材料的塑性体积应变（即剪胀性）。例如，一个与实际强度吻合的 Mohr-Coulomb 屈服面，若采用关联流动，会预测出比实际大得多的剪胀。为了更准确地描述材料的强度和变形特性，引入一个独立的塑性势函数 $g$ 变得至关重要。

以经典的 Drucker-Prager 模型为例，其屈服函数可写为 $f(p,q) = q + a p - k$，其中 $p$ 是平均应力，$q$ 是等效剪应力，$a$ 是与摩擦角相关的参数。我们可以为其定义一个形式相似但参数不同的塑性势 $g(p,q) = q + b p$，其中 $b$ 是与剪胀角相关的参数 [@problem_id:3551055] [@problem_id:3551066]。只有当 $b=a$ 时，该流动法则才是关联的。

### 塑性流动的分解：体积应变与偏应变

为了更深入地理解塑性流动，我们通常将其分解为**体积**（volumetric）和**偏**（deviatoric）两个部分，分别对应于体积变化和形状变化。对于依赖于应力不变量 $p$ 和 $q$ 的各向同性塑性势 $g(p,q)$，我们可以推导这两个分量的表达式。

塑性应变增量 $d\boldsymbol{\varepsilon}^p$ 可以通过链式法则展开：
$$
d\boldsymbol{\varepsilon}^p = d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}} = d\lambda \left( \frac{\partial g}{\partial p} \frac{\partial p}{\partial \boldsymbol{\sigma}} + \frac{\partial g}{\partial q} \frac{\partial q}{\partial \boldsymbol{\sigma}} \right)
$$
利用标准的不变量导数关系 $\frac{\partial p}{\partial \boldsymbol{\sigma}} = \frac{1}{3}\boldsymbol{I}$ 和 $\frac{\partial q}{\partial \boldsymbol{\sigma}} = \frac{3}{2q}\boldsymbol{s}$（其中 $\boldsymbol{s}$ 是偏应力张量），我们得到：
$$
d\boldsymbol{\varepsilon}^p = d\lambda \left( \frac{1}{3}\frac{\partial g}{\partial p} \boldsymbol{I} + \frac{3}{2q}\frac{\partial g}{\partial q} \boldsymbol{s} \right)
$$
塑性体积应变增量 $d\varepsilon_v^p$ 是 $d\boldsymbol{\varepsilon}^p$ 的迹：
$$
d\varepsilon_v^p = \operatorname{tr}(d\boldsymbol{\varepsilon}^p) = d\lambda \left( \frac{1}{3}\frac{\partial g}{\partial p} \operatorname{tr}(\boldsymbol{I}) + \frac{3}{2q}\frac{\partial g}{\partial q} \operatorname{tr}(\boldsymbol{s}) \right)
$$
由于 $\operatorname{tr}(\boldsymbol{I})=3$ 且 $\operatorname{tr}(\boldsymbol{s})=0$，上式简化为：
$$
d\varepsilon_v^p = d\lambda \frac{\partial g}{\partial p}
$$
等效塑性偏应变增量 $d\varepsilon_q^p$（或等效塑性剪应变增量 $d\varepsilon_s^p$）则与 $d\boldsymbol{\varepsilon}^p$ 的偏量部分相关。经过推导 [@problem_id:3551045]，可以得到：
$$
d\varepsilon_q^p = d\lambda \left| \frac{\partial g}{\partial q} \right|
$$
这些表达式清晰地表明，塑性体积变化由塑性势 $g$ 对平均应力 $p$ 的偏导数控制，而塑性形状变化由 $g$ 对等效剪应力 $q$ 的偏导数控制。

### 剪胀比：体积-剪切耦合的度量

**剪胀比**（dilatancy ratio），通常记为 $D$ 或 $\psi$，定义为塑性体积应变增量与等效塑性偏应变增量之比：
$$
D = \frac{d\varepsilon_v^p}{d\varepsilon_q^p} = \frac{\partial g / \partial p}{|\partial g / \partial q|}
$$
这个比率量化了材料在塑性剪切过程中发生体积变化的倾向，是塑性势函数 $g$ 几何形状的直接体现。

**示例 1：线性 Drucker-Prager 势**
对于塑性势 $g = q + \beta p$ [@problem_id:3551066]，我们有 $\frac{\partial g}{\partial p} = \beta$ 和 $\frac{\partial g}{\partial q} = 1$。因此，剪胀比非常简洁：
$$
D = \beta
$$
参数 $\beta$ 直接控制剪胀行为。当 $\beta > 0$ 时，材料在剪切时发生扩容（剪胀）；当 $\beta  0$ 时，发生收缩（剪缩）；当 $\beta = 0$ 时，塑性流动是等容的。这个简单的结果揭示了非关联流动中参数 $b$ (或 $\beta$) 的物理意义，它直接决定了剪胀的大小，例如在不排水条件下，正的剪胀会导致孔隙水压的降低，而剪缩则导致孔压的升高。

**示例 2：Mohr-Coulomb 势**
在 Mohr-Coulomb 模型中，剪胀性通常用**剪胀角** $\psi$ 来描述。其对应的塑性势函数在 $(p,q)$ 平面上可以写成 $g(p,q) = q + M_g p$，其中 $M_g = \frac{6 \sin \psi}{3 - \sin \psi}$ [@problem_id:3551048]。此时，$\frac{\partial g}{\partial p} = M_g$ 且 $\frac{\partial g}{\partial q} = 1$。因此，剪胀比为：
$$
D = M_g = \frac{6 \sin \psi}{3 - \sin \psi}
$$
这直接将抽象的剪胀比与物理上可测量的剪胀角 $\psi$ 联系起来。

**示例 3：修正剑桥模型 (Modified Cam-Clay)**
对于更复杂的模型，如修正剑桥模型，剪胀比不再是常数，而是依赖于当前的应力状态。考虑一个非关联的 MCC 模型，其屈服函数为 $f(p',q,p_{c}') = q^{2} + M^{2} p' (p' - p_{c}')$，塑性势为 $g(p',q,p_{c}') = q^{2} + M_{g}^{2} p' (p' - p_{c}')$ [@problem_id:3551040]。剪胀比为：
$$
D = \frac{\partial g / \partial p'}{\partial g / \partial q} = \frac{M_{g}^{2} (2p' - p_{c}')}{2q}
$$
由于材料处于屈服状态，满足 $f=0$，我们可以从中解出硬化参数 $p_{c}' = p' + \frac{q^2}{M^2 p'}$，并代入上式，得到：
$$
D = \frac{M_{g}^{2}}{M^2} \frac{M^2 (p')^2 - q^2}{2 p' q}
$$
这个结果表明，对于 MCC 模型，剪胀比不仅取决于材料参数 $M$ 和 $M_g$，还与当前应力比 $q/p'$ 密切相关。

### 流动法则的高级议题与推论

#### 材料稳定性与塑性耗散

根据热力学第二定律，任何不可逆过程的内能耗散率必须为非负。在等温塑性变形中，这表现为**塑性耗散**（plastic dissipation）$W^p = \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^p \ge 0$。这也被称为 **Drucker 稳定性公设**。

将流动法则代入，我们得到：
$$
W^p = \boldsymbol{\sigma} : \left( d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}} \right) = d\lambda \left( \boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \right)
$$
对于**关联流动**（$g=f$），如果屈服面 $f$ 是凸的，那么 $\boldsymbol{\sigma} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \ge 0$ 恒成立，因此材料总是稳定的。然而，对于**非关联流动**，稳定性不再是必然的。

考虑一个非关联的 Drucker-Prager 模型：屈服函数 $f = q + \beta p - c$，塑性势 $g = q + \alpha p$ [@problem_id:3551082]。塑性耗散为 $W^p = d\lambda (q + \alpha p)$。在屈服面上，$q = c - \beta p$，代入后得到 $W^p = d\lambda(c + (\alpha - \beta)p)$。如果 $\alpha  \beta$ 并且 $p$ 足够大，那么 $(\alpha - \beta)p$ 这一项可能为负，并超过常数 $c$，导致 $W^p  0$。这种情况违反了稳定性公设，可能预示着材料的失稳，如应变局部化（剪切带的形成）。因此，在选择非关联塑性势时，必须谨慎考虑其对材料稳定性的影响。通常，要求 $\boldsymbol{\sigma} : \frac{\partial g}{\partial \boldsymbol{\sigma}} \ge 0$ 对所有可能的应力状态成立，这为塑性势参数（如 $\alpha$）的选择施加了约束。

#### 一致性条件与弹塑性切线模量

在持续的塑性加载过程中，应力状态必须始终停留在（或跟随）演化中的屈服面上。这一要求通过**一致性条件** $df=0$ 来数学化表达。对于一个包含硬化的屈服函数 $f(\boldsymbol{\sigma}, \kappa) = 0$，其全微分为：
$$
df = \frac{\partial f}{\partial \boldsymbol{\sigma}} : d\boldsymbol{\sigma} + \frac{\partial f}{\partial \kappa} d\kappa = 0
$$
这个方程是求解塑性乘子 $d\lambda$ 的关键。我们可以将应力增量 $d\boldsymbol{\sigma} = \boldsymbol{C}^e : (d\boldsymbol{\varepsilon} - d\boldsymbol{\varepsilon}^p)$ 和塑性流动 $d\boldsymbol{\varepsilon}^p = d\lambda \frac{\partial g}{\partial \boldsymbol{\sigma}}$ 以及硬化规律（如 $d\kappa = d\lambda$）代入一致性条件，从而建立起塑性乘子 $d\lambda$ 与总应变增量 $d\boldsymbol{\varepsilon}$ 之间的关系。

一旦求得 $d\lambda$，我们就可以推导出总应力增量 $d\boldsymbol{\sigma}$ 和总应变增量 $d\boldsymbol{\varepsilon}$ 之间的增量关系，即**弹塑性切线模量**（elasto-plastic tangent modulus）$\boldsymbol{C}^{ep}$：
$$
d\boldsymbol{\sigma} = \boldsymbol{C}^{ep} : d\boldsymbol{\varepsilon}
$$
这个切线模量是进行隐式有限元分析的核心，它反映了在当前应力状态和加载方向下材料的刚度。例如，在一个恒定围压的轴向压缩试验中，可以推导出轴向切线模量 $E_{\text{alg}} = d\sigma_a / d\varepsilon_a$ 的表达式，它将弹性模量、硬化参数以及屈服函数和塑性势的形状参数（$M$ 和 $\eta$）联系在一起 [@problem_id:3551084]。

#### Lode 角依赖性与屈服面角点

实际岩土材料的强度不仅依赖于 $p$ 和 $q$，还依赖于第三应力不变量，通常用 **Lode 角** $\theta$ 来表示。Lode 角描述了偏应力平面上应力状态点的形状。为了更精确地模拟材料行为，塑性势（和屈服面）可以包含 Lode 角的依赖项，例如 $g(p, q, \theta) = q \cdot r(\theta) - M p$ [@problem_id:3551044]。这使得模型能够区分三轴压缩、三轴拉伸和纯剪切等不同应力路径下的材料响应。

许多经典屈服准则（如 Mohr-Coulomb 和 Tresca）在偏应力平面上呈现为多边形，存在**角点**（corners）。在这些角点处，屈服函数的梯度不是唯一的。从数学上讲，流动方向属于一个由相邻光滑面法向量张成的凸锥，这个法向量集合被称为**次微分**（subdifferential）。在计算实践中，这种不唯一性带来了挑战。处理角点的一种常用方法是采用**光滑化**技术，例如使用 log-sum-exp 正则化函数来近似多边形屈服面 [@problem_id:3551036]。这种光滑的近似函数在任何地方都具有唯一的、良定义的梯度，从而为塑性流动提供了一个明确的方向，便于数值实现。

### 结论

本章系统地阐述了塑性势和流动法则在岩土力学中的核心地位。我们看到，塑性势函数 $g$ 和正交流动法则共同决定了塑性应变增量的方向。关联与非关联流动的区别，为准确模拟岩土材料的强度和变形特性（特别是剪胀性）提供了必要的灵活性。通过将塑性流动分解为体积和偏量部分，并引入剪胀比的概念，我们能量化和理解剪切-体积耦合效应。此外，流动法则的选择对材料的稳定性和增量刚度有深远影响，这些都是高级计算分析中的关键考量。从简单的线性势到考虑 Lode 角和角点效应的复杂模型，本章介绍的原理为理解和应用现代岩土本构模型奠定了坚实的基础。