## 引言
在计算科学与工程领域，许多物理系统，尤其是那些包含[不可压缩性](@entry_id:274914)或接触等约束条件的系统，其数学模型天然地导向一类被称为“[鞍点问题](@entry_id:174221)”的结构。当使用有限元等数值方法求解这些问题时，一个核心的挑战是确保解的稳定性和准确性。然而，研究人员和工程师们早已发现，一些看似最直接、最自然的离散化方案（例如，对所有未知场使用相同类型的简单[插值函数](@entry_id:262791)）往往会产生灾难性的后果，例如出现完全非物理的[振荡](@entry_id:267781)或“锁定”现象，导致计算结果毫无意义。这种数值不稳定的背后，隐藏着深刻的数学原理，而理解并克服这一难题，正是通向可靠[数值模拟](@entry_id:137087)的关键。

本文旨在系统性地阐述保证[鞍点问题](@entry_id:174221)数值稳定性的核心理论——Ladyzhenskaya-Babuška-Brezzi (LBB) 条件。通过三个层层递进的章节，读者将踏上一段从抽象理论到具体实践的探索之旅：
- **第一章：原理与机制** 将深入[鞍点问题](@entry_id:174221)的数学心脏，介绍抽象的Brezzi[稳定性理论](@entry_id:149957)，并聚焦于其核心——LBB (inf-sup) 条件。我们将以经典的不可压缩[斯托克斯方程](@entry_id:196346)为例，揭示[LBB条件](@entry_id:746626)如何保证压[力场](@entry_id:147325)的稳定性，并剖析当该条件失效时，为何会出现[棋盘格压力](@entry_id:164851)模式等[伪解](@entry_id:275285)。
- **第二章：应用与跨学科联系** 将展示LBB原理的普适性和强大生命力，探讨其在[流体力学](@entry_id:136788)、固体力学、[多孔介质](@entry_id:154591)、乃至[计算电磁学](@entry_id:265339)和最优化控制等多个学科领域的关键应用。本章还将讨论[压力鲁棒性](@entry_id:167963)等进阶主题，展现LBB思想的深化与扩展。
- **第三章：动手实践** 则将理论付诸实践，通过具体的编程和分析练习，读者将学习如何量化计算LBB稳定性常数，诊断不稳定现象，并应用稳定化技术来修正不稳定的离散格式。

通过对这些内容的学习，您将不仅理解[LBB条件](@entry_id:746626)的定义，更能掌握其在设计和评估现代数值方法中的指导性作用，为解决复杂的科学与工程问题打下坚实的理论基础。

## 原理与机制

在上一章中，我们介绍了[鞍点问题](@entry_id:174221)在物理和工程建模中的普遍性，特别是那些涉及约束条件的系统。本章将深入探讨这些问题的数学核心，阐述其混合[变分形式](@entry_id:166033)的[适定性](@entry_id:148590)（well-posedness）所依赖的基本原理和关键机制。我们将建立一个抽象的理论框架，然后将其应用于[不可压缩流体](@entry_id:181066)力学中的斯托克斯（Stokes）方程，并最终揭示保证离散化后数值解稳定性的核心条件——即著名的Ladyzhenskaya-Babuška-Brezzi (LBB) 条件。

### 抽象[鞍点问题](@entry_id:174221)与Brezzi稳定性条件

许多[约束优化](@entry_id:635027)问题和守恒律方程在经过变分推导后，都可以归结为一个统一的抽象[鞍点问题](@entry_id:174221)。该问题旨在寻找一对解 $(\boldsymbol{u}, p)$，它们分属于两个希尔伯特（Hilbert）空间 $V$ 和 $Q$。其中，$\boldsymbol{u} \in V$ 通常代表主变量（如[速度场](@entry_id:271461)或[位移场](@entry_id:141476)），而 $p \in Q$ 代表施加约束的拉格朗日乘子（Lagrange multiplier）（如压力）。这个问题的混合[变分形式](@entry_id:166033)通常写作：求解 $(\boldsymbol{u}, p) \in V \times Q$，使得对于所有的[检验函数](@entry_id:166589) $(\boldsymbol{v}, q) \in V \times Q$，以下[方程组](@entry_id:193238)成立：
$$
\begin{cases}
a(\boldsymbol{u}, \boldsymbol{v}) + b(\boldsymbol{v}, p) = \ell(\boldsymbol{v}) \\
b(\boldsymbol{u}, q) = g(q)
\end{cases}
$$
这里，$a(\cdot, \cdot): V \times V \to \mathbb{R}$ 和 $b(\cdot, \cdot): V \times Q \to \mathbb{R}$ 是双线性形式（bilinear forms），而 $\ell(\cdot): V \to \mathbb{R}$ 和 $g(\cdot): Q \to \mathbb{R}$ 是给定的[连续线性泛函](@entry_id:262913)，通常代表外力或[源项](@entry_id:269111)。第一个方程通常源于物理上的能量平衡或动量守恒，而第二个方程则以弱形式（weak form）强制施加了约束条件。

一个自然而核心的问题是：在何种条件下，这个[鞍点问题](@entry_id:174221)存在唯一的、稳定的解？答案由Franco Brezzi（以及独立工作的Olga Ladyzhenskaya和Ivo Babuška）在上世纪70年代给出的三个基本条件所限定。这些条件，统称为**Brezzi条件**或[Babuška-Brezzi条件](@entry_id:746625)，为整个[混合有限元](@entry_id:178533)方法的理论分析奠定了基石。

这三个条件是 [@problem_id:3414758] [@problem_id:3414783]：

1.  **[双线性形式](@entry_id:746794)的连续性 (Continuity)**：存在正常数 $M_a$ 和 $M_b$，使得对于所有的 $\boldsymbol{u}, \boldsymbol{v} \in V$ 和 $q \in Q$，成立
    $$
    |a(\boldsymbol{u}, \boldsymbol{v})| \le M_a \|\boldsymbol{u}\|_V \|\boldsymbol{v}\|_V \quad \text{和} \quad |b(\boldsymbol{v}, q)| \le M_b \|\boldsymbol{v}\|_V \|q\|_Q
    $$
    此条件保证了算子的有界性，是大多数[变分问题](@entry_id:756445)分析的基本前提。

2.  **$a(\cdot, \cdot)$ 在 $b$ 的核空间上的强制性 (Coercivity on the Kernel)**：定义 $b$ 的核空间为 $Z = \ker(b) := \{\boldsymbol{v} \in V \mid b(\boldsymbol{v}, q) = 0, \forall q \in Q\}$。这个空间包含了所有弱意义下满足约束条件的场。该条件要求，$a(\cdot, \cdot)$ 在这个[子空间](@entry_id:150286) $Z$ 上是强制的（coercive），即存在一个常数 $\alpha > 0$，使得对于所有 $\boldsymbol{v} \in Z$，成立
    $$
    a(\boldsymbol{v}, \boldsymbol{v}) \ge \alpha \|\boldsymbol{v}\|_V^2
    $$
    从物理上看，$a(\boldsymbol{v}, \boldsymbol{v})$ 通常与系统的能量有关（例如[应变能](@entry_id:162699)）。此条件确保了在满足约束的解空间中，任何非零的解都具有正能量，从而保证了[解的唯一性](@entry_id:143619) [@problem_id:3414743]。

3.  **LBB (inf-sup) 条件**：存在一个常数 $\beta > 0$，使得
    $$
    \inf_{q \in Q \setminus \{0\}} \sup_{\boldsymbol{v} \in V \setminus \{0\}} \frac{b(\boldsymbol{v}, q)}{\|\boldsymbol{v}\|_V \|q\|_Q} \ge \beta
    $$
    这个条件也被称为Ladyzhenskaya-[Babuška-Brezzi条件](@entry_id:746625)，是混合方法稳定性的核心。它的直观意义是，对于压力空间 $Q$ 中的任何一个非零元素 $q$，我们总能在速度空间 $V$ 中找到一个元素 $\boldsymbol{v}$，使得它与 $q$ 的耦合作用 $b(\boldsymbol{v}, q)$ 足够强。换言之，速度空间 $V$ 必须足够“丰富”，以至于能够“控制”压力空间 $Q$ 中的所有模式。如果这个条件不满足，[拉格朗日乘子](@entry_id:142696) $p$ 的解可能会变得不稳定，甚至出现非物理的[伪解](@entry_id:275285)（spurious solutions） [@problem_id:3414743]。这三个条件的有效性都与所选的范数 $\|\cdot\|_V$ 和 $\|\cdot\|_Q$ 密切相关 [@problem_id:3414743]。

### 典范应用：不可压缩[斯托克斯方程](@entry_id:196346)

为了将上述抽象理论具体化，我们考察不可压缩黏性流动的[稳态](@entry_id:182458)[斯托克斯方程](@entry_id:196346)。在一个有界区域 $\Omega \subset \mathbb{R}^d$ ($d=2,3$) 中，该[方程组](@entry_id:193238)描述了速度场 $\boldsymbol{u}$ 和压[力场](@entry_id:147325) $p$ 的关系：
$$
-\nu \Delta \boldsymbol{u} + \nabla p = \boldsymbol{f} \quad \text{in } \Omega, \qquad \nabla \cdot \boldsymbol{u} = 0 \quad \text{in } \Omega
$$
这里 $\nu > 0$ 是流体的运动粘度，$\boldsymbol{f}$ 是体积力。我们考虑固壁边界条件 $\boldsymbol{u} = \boldsymbol{0}$ on $\partial\Omega$。压力的解存在一个任意常数的自由度，为了唯一确定压力，通常施加零均值约束 $\int_{\Omega} p \, dx = 0$。

为了得到[弱形式](@entry_id:142897)，我们将[动量方程](@entry_id:197225)与一个速度检验函数 $\boldsymbol{v} \in V = H_0^1(\Omega)^d$ 作[内积](@entry_id:158127)并分部积分，将不可压缩条件与一个压力检验函数 $q \in Q = L_0^2(\Omega)$ 作[内积](@entry_id:158127)。这样，我们就得到了与前述抽象形式完全对应的混合[变分问题](@entry_id:756445) [@problem_id:3414758]。其中，双线性形式为：
$$
a(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} \nu \nabla \boldsymbol{u} : \nabla \boldsymbol{v} \, dx \quad \text{或等价地} \quad a(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} 2\nu \varepsilon(\boldsymbol{u}) : \varepsilon(\boldsymbol{v}) \, dx
$$
$$
b(\boldsymbol{v}, p) = - \int_{\Omega} p (\nabla \cdot \boldsymbol{v}) \, dx
$$
这里 $\varepsilon(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^T)$ 是对称梯度张量。$a(\boldsymbol{u}, \boldsymbol{u})$ 代表了流体因黏性耗散的能量，而 $b(\boldsymbol{u}, q)=0$ 则精确地以[弱形式](@entry_id:142897)表达了[不可压缩性约束](@entry_id:750592) $\nabla \cdot \boldsymbol{u} = 0$。

对于这个具体的系统，Brezzi稳定性条件转化为：
1.  **连续性**：通过柯西-施瓦茨（Cauchy-Schwarz）不等式容易验证 $a(\cdot,\cdot)$ 和 $b(\cdot,\cdot)$ 都是连续的。
2.  **核上的强制性**：$b$ 的核空间是所有散度为零的函数构成的空间 $Z = \{\boldsymbol{v} \in H_0^1(\Omega)^d \mid \nabla \cdot \boldsymbol{v} = 0\}$。对于[斯托克斯方程](@entry_id:196346)，一个关键的数学结果是**[Korn不等式](@entry_id:174794)**，它确保了在 $H_0^1(\Omega)^d$ 空间中，对称梯度的 $L^2$ 范数可以控制整个梯度的 $L^2$ 范数。结合庞加莱（Poincaré）不等式，这保证了 $a(\cdot, \cdot)$ 在整个空间 $V$ 上都是强制的，因此自然也在其[子空间](@entry_id:150286) $Z$ 上是强制的 [@problem_id:3414743]。
3.  **[LBB条件](@entry_id:746626)**：对于斯托克斯算子和所选的空间 $V=H_0^1(\Omega)^d$ 与 $Q=L_0^2(\Omega)$，[LBB条件](@entry_id:746626)成立。这是一个深刻的分析结果，它保证了压力解的稳定性。

### [LBB条件](@entry_id:746626)的直接推论：压力稳定性

[LBB条件](@entry_id:746626)为何如此关键？因为它直接提供了控制压力范数的能力。从[LBB条件](@entry_id:746626)的定义出发，对于任何 $p \in Q$，我们有：
$$
\|p\|_Q \le \frac{1}{\beta} \sup_{\boldsymbol{v} \in V \setminus \{0\}} \frac{b(\boldsymbol{v}, p)}{\|\boldsymbol{v}\|_V}
$$
利用[变分方程](@entry_id:635018)的第一式 $b(\boldsymbol{v}, p) = \ell(\boldsymbol{v}) - a(\boldsymbol{u}, \boldsymbol{v})$，我们可以将右端替换掉：
$$
\|p\|_Q \le \frac{1}{\beta} \sup_{\boldsymbol{v} \in V \setminus \{0\}} \frac{\ell(\boldsymbol{v}) - a(\boldsymbol{u}, \boldsymbol{v})}{\|\boldsymbol{v}\|_V} \le \frac{1}{\beta} \left( \|\ell\|_{V'} + M_a \|\boldsymbol{u}\|_V \right)
$$
这个不等式表明，压力的范数被数据（外力）和速度解的范数所控制。再结合从 $a(\cdot,\cdot)$ 的强制性得到的速度稳定性界 $\|\boldsymbol{u}\|_V \le \frac{1}{\alpha} \|\ell\|_{V'}$，我们最终可以得到一个完全由数据决定的压力界：
$$
\|p\|_Q \le C \|\ell\|_{V'}
$$
其中常数 $C$ 仅依赖于 $\alpha, \beta, M_a$ 和定义域。这个过程清晰地展示了，[LBB条件](@entry_id:746626)是连接压力 $p$ 与数据 $\ell$ 的桥梁，是保证整个系统[适定性](@entry_id:148590)的关键环节 [@problem_id:3384307]。

### 离散化与离散[LBB条件](@entry_id:746626)的挑战

在有限元方法中，我们不再在无限维的[函数空间](@entry_id:143478) $V$ 和 $Q$ 中求解，而是在其有限维[子空间](@entry_id:150286) $V_h \subset V$ 和 $Q_h \subset Q$ 中寻找离散解 $(\boldsymbol{u}_h, p_h)$。此时，所有的稳定性条件都必须在离散层面上重新审视。

离散Brezzi条件要求连续性、核上的强制性以及[LBB条件](@entry_id:746626)在离散空间 $V_h$ 和 $Q_h$ 上成立，并且最关键的是，相应的常数 $\alpha_h$ 和 $\beta_h$ 必须**与网格尺寸 $h$ 无关**（或者说，有一个不依赖于 $h$ 的统一正下界）[@problem_id:3414783]。
$$
\beta_h := \inf_{q_h \in Q_h \setminus \{0\}} \sup_{\boldsymbol{v}_h \in V_h \setminus \{0\}} \frac{b(\boldsymbol{v}_h, q_h)}{\|\boldsymbol{v}_h\|_V \|q_h\|_Q} \ge \beta_0 > 0
$$
这个“统一有界”的要求至关重要。如果离散LBB常数 $\beta_h$ 随着网格加密而趋向于零（$\beta_h \to 0$ as $h \to 0$），那么即使对于每个固定的网格问题都是可解的，其解的稳定性也会随 $h$ 的减小而恶化，导致数值方法在极限情况下是发散的。

不幸的是，一个在连续层面稳定的问题，其离散化不一定稳定。稳定性强烈依赖于离散空间 $V_h$ 和 $Q_h$ 的选择。一个看似自然的选择，比如对速度和压力采用相同阶次的多项式（例如，在四边形网格上都使用分片[双线性](@entry_id:146819)函数，$Q_1-Q_1$），往往会导致灾难性的失败 [@problem_id:3414754]。

### 稳定性失效的实例：[棋盘格压力](@entry_id:164851)模式

让我们通过一个经典的例子来审视[LBB条件](@entry_id:746626)失效的后果。考虑在均匀四边形网格上使用连续分片[双线性](@entry_id:146819)函数（$Q_1$）来近似速度和压力（即 $Q_1-Q_1$ 单元）。这个单元对不满足离散[LBB条件](@entry_id:746626)。

我们可以构造一个特定的、非零的离散[压力模](@entry_id:159654)式 $q_h^* \in Q_h$，其在网格节点上的值呈 `+1, -1, +1, -1, ...` 交替[分布](@entry_id:182848)，就像棋盘格一样。通过在每个单元上进行计算可以严格证明，这个“棋盘格”[压力模](@entry_id:159654)式 $q_h^*$ 满足一个特殊的性质：对于**任何**离散[速度场](@entry_id:271461) $\boldsymbol{v}_h \in V_h$，耦合项 $b(\boldsymbol{v}_h, q_h^*) = -\int_{\Omega} q_h^* (\nabla \cdot \boldsymbol{v}_h) dx$ 恒等于零 [@problem_id:3414772]。

这个结果的直接推论是，对于这个特定的 $q_h^*$，[LBB条件](@entry_id:746626)中的商为零：
$$
\sup_{\boldsymbol{v}_h \in V_h \setminus \{0\}} \frac{b(\boldsymbol{v}_h, q_h^*)}{\|\boldsymbol{v}_h\|_V \|q_h^*\|_Q} = 0
$$
由于LBB常数 $\beta_h$ 是对所有非零 $q_h \in Q_h$ 取[下确界](@entry_id:140118)，而我们已经找到了一个使商为零的元素，因此 $\beta_h$ 必然为零。这意味着[LBB条件](@entry_id:746626)完全失效。在数值计算中，这种不稳定表现为压力解中出现大幅度的、非物理性的棋盘格[振荡](@entry_id:267781)，这些[振荡](@entry_id:267781)是无法通过加密网格来消除的[伪解](@entry_id:275285)。

### 稳定性的代数观点：[舒尔补](@entry_id:142780)（Schur Complement）

[LBB条件](@entry_id:746626)的美妙之处在于它不仅是一个[泛函分析](@entry_id:146220)的概念，还与离散后得到的线性代数系统有着深刻的联系。离散的[鞍点问题](@entry_id:174221)可以写成如下的矩阵形式：
$$
\begin{pmatrix} A & B^T \\ B & 0 \end{pmatrix} \begin{pmatrix} u \\ p \end{pmatrix} = \begin{pmatrix} f \\ g \end{pmatrix}
$$
其中 $A$ 是与 $a(\cdot, \cdot)$ 相关的刚度矩阵，$B$ 是与 $b(\cdot, \cdot)$ 相关的梯度矩阵，$u, p$ 是未知解的系数向量。通过从第一个方程中消去 $u$ ($u = A^{-1}(f - B^T p)$)，我们可以得到一个只关于压力 $p$ 的方程：
$$
(B A^{-1} B^T) p = B A^{-1} f - g
$$
这个方程中的矩阵 $S = B A^{-1} B^T$ 被称为**[舒尔补](@entry_id:142780)**。整个系统的[适定性](@entry_id:148590)，特别是压力[解的唯一性](@entry_id:143619)和稳定性，取决于[舒尔补](@entry_id:142780)矩阵 $S$ 的性质。

一个非常深刻的结论是，离散LBB常数 $\beta_h$ 的平方，与[舒尔补](@entry_id:142780)矩阵的最小特征值直接相关。可以证明，如果范数 $\|\cdot\|_V$ 由矩阵 $A$ 导出（能量范数），范数 $\|\cdot\|_Q$ 由质量矩阵 $M_Q$ 导出，那么[广义特征值问题](@entry_id:151614) $S q = \lambda M_Q q$ 的[最小特征值](@entry_id:177333) $\lambda_{\min}$ 恰好等于 $\beta_h^2$ [@problem_id:3414779]。
$$
\lambda_{\min}(M_Q^{-1}S) = \beta_h^2
$$
这个关系完美地连接了分析与代数：
-   $\beta_h > 0$（[LBB条件](@entry_id:746626)满足）等价于 $S$ 是正定的，压力问题唯一可解且稳定。
-   $\beta_h = 0$（[LBB条件](@entry_id:746626)失效，如 $Q_1-Q_1$ 单元）等价于 $S$ 是奇异的，压力问题存在非零的[零空间](@entry_id:171336)（棋盘格模式），导致解不唯一和不稳定。

### 确保稳定性的机制：Fortin投影与稳定单元

既然我们已经了解了不稳定的原因，那么如何设计稳定的有限元方法呢？现代有限[元理论](@entry_id:638043)提供了一个强大的工具来证明离散[LBB条件](@entry_id:746626)的成立，即**Fortin投影**（或Fortin算子）。

Fortin投影是一个线性算子 $\Pi_h: V \to V_h$，它将连续空间中的函数映射到离散[速度空间](@entry_id:181216)，并满足两个关键性质 [@problem_id:3414790] [@problem_id:3414769]：
1.  **散度保持性**：对于所有 $q_h \in Q_h$，$\Pi_h$ 保持了原函数散度在离散压力空间上的投影，即 $b(\boldsymbol{v}, q_h) = b(\Pi_h \boldsymbol{v}, q_h)$。
2.  **[一致有界性](@entry_id:141342)**：存在一个与网格尺寸 $h$ 无关的常数 $C$，使得 $\|\Pi_h \boldsymbol{v}\|_V \le C \|\boldsymbol{v}\|_V$。

如果能为一对[离散空间](@entry_id:155685) $(V_h, Q_h)$ 构造出这样一个Fortin投影，那么就可以直接从连续[LBB条件](@entry_id:746626)推导出离散[LBB条件](@entry_id:746626)，且离散常数 $\beta_h \ge \beta/C$，从而证明了方法的稳定性。构造这样的[投影算子](@entry_id:154142)是证明一个单元对是否稳定的核心步骤。以下是一些经典的稳定单元及其稳定机制：

-   **[Taylor-Hood单元](@entry_id:165658)** ($P_{k+1}-P_k$, $k \ge 1$)：这类单元采用比压力高一阶的多项式来近似速度（例如，速度用分片二次函数，压力用分片线性函数）。这种[速度空间](@entry_id:181216)的“丰富性”是其稳定性的来源。其深层数学原理在于，在多项式层面，[散度算子](@entry_id:265975) $\nabla \cdot$ 是一个从 $[\mathbb{P}_{k+1}]^d$ 到 $\mathbb{P}_k$ 的满射。这个性质是**多项式[de Rham复形](@entry_id:178752)**（polynomial de Rham complex）正合性的一个推论，它保证了构造Fortin投影所需的局部性质 [@problem_id:3414769]。

-   **MINI单元** ($P_1$-bubble/$P_1$)：这个单元对速度和压力都采用分片线性函数，但对[速度空间](@entry_id:181216)进行了“增强”：在每个单元内部增加了一个“[气泡函数](@entry_id:176111)”（bubble function）。[气泡函数](@entry_id:176111)是在单元内部非零、在边界上为零的函数。这种设计非常巧妙：由于[气泡函数](@entry_id:176111)在单元边界上为零，它不影响速度场的整体连续性；但因为它在内部非零，它为[速度场](@entry_id:271461)提供了额外的、纯内部的自由度。这些自由度恰好可以用来调整每个单元内的散度，以满足Fortin投影所需的散度保持性，从而“修复”了原本不稳定的 $P_1-P_1$ 单元对 [@problem_id:3414790]。

### 统一的框架：[有限元外微分](@entry_id:174585)（FEEC）

从Taylor-Hood和MINI等单元的分析中可以看出，[LBB条件](@entry_id:746626)的满足与微分算子（如梯度、旋度、散度）在多项式空间的代数性质密切相关。**[有限元外微分](@entry_id:174585)**（Finite Element Exterior Calculus, FEEC）为这一领域提供了统一而深刻的理论框架。

FEEC将微分几何中的[de Rham复形](@entry_id:178752)理论与有限元方法相结合。它指出，许多物理[方程组](@entry_id:193238)都可以抽象为[微分](@entry_id:158718)复形的形式。一个稳定的有限元方法可以通过构造一组[离散空间](@entry_id:155685) $(S_h, W_h, V_h, Q_h, \dots)$ 来系统地构建，这组空间本身也构成一个离散的**[子复形](@entry_id:264130)**（subcomplex），并且保持原复形的正合性。此外，还需要存在一组在相应范数下一致有界，并与[微分算子](@entry_id:140145)**可交换**的投影算子或拟插值算子（commuting quasi-interpolants）[@problem_id:3414777]。
$$
\begin{array}{ccccccccccc}
H(\text{grad}) & \xrightarrow{\text{grad}} & H(\text{curl}) & \xrightarrow{\text{curl}} & H(\text{div}) & \xrightarrow{\text{div}} & L^2 \\
\downarrow \Pi_{\text{grad}} & & \downarrow \Pi_{\text{curl}} & & \downarrow \Pi_{\text{div}} & & \downarrow \Pi_{L^2} \\
V_h^{\text{grad}} & \xrightarrow{\text{grad}} & V_h^{\text{curl}} & \xrightarrow{\text{curl}} & V_h^{\text{div}} & \xrightarrow{\text{div}} & V_h^{L^2}
\end{array}
$$
可交换性（例如 $\mathrm{div}\,\Pi_{\mathrm{div},h} = P_h\,\mathrm{div}$）正是Fortin投影中散度保持性的抽象形式。这个强大的框架不仅解释了[斯托克斯方程](@entry_id:196346)的LBB稳定性，还统一了达西（Darcy）流动、麦克斯韦（Maxwell）方程、弹性力学等众多问题的[混合有限元](@entry_id:178533)方法的[稳定性理论](@entry_id:149957)，揭示了其背后共通的代数拓扑结构。