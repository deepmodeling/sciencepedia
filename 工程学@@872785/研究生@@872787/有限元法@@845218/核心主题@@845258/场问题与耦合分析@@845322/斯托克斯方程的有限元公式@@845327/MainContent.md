## 引言
[斯托克斯方程](@entry_id:196346)是描述低雷诺数下[粘性不可压缩流](@entry_id:756537)体运动的基础模型，在计算流体动力学、地球物理学和[生物工程](@entry_id:270890)等领域中扮演着核心角色。然而，将这些方程转化为可靠的[数值算法](@entry_id:752770)并非易事。其固有的[鞍点问题](@entry_id:174221)结构给[有限元离散化](@entry_id:193156)带来了独特的挑战，即速度和压力近似空间必须满足严格的[相容性条件](@entry_id:637057)，否则将导致解的严重不稳定。本文旨在系统性地解决这一知识鸿沟，为读者提供一套关于[斯托克斯方程](@entry_id:196346)有限元格式的完整理论与实践指南。

在接下来的内容中，我们将分三步深入探讨这一主题。第一章“原理与机制”将奠定理论基础，从弱形式的推导讲起，重点剖析确保稳定性的核心——Ladyzhenskaya–Babuška–Brezzi (LBB) 条件，并介绍几种经典的稳定单元设计。第二章“应用与交叉学科联系”将展示理论的实践价值，通过分析[流体力学](@entry_id:136788)基准问题，并探索其在固体力学、[多孔介质](@entry_id:154591)及[生物力学](@entry_id:153973)中的深刻类比，揭示其广泛的适用性。最后，在“动手实践”部分，我们将通过具体的编程练习，将抽象的理论转化为可操作的代码。

通过本章的学习，您将不仅理解[斯托克斯方程](@entry_id:196346)有限元方法的数学精髓，更能掌握在多样化工程与科学问题中成功应用这些方法的关键技术。

## 原理与机制

本章深入探讨了不可压[斯托克斯方程](@entry_id:196346)[有限元离散化](@entry_id:193156)的核心原理与关键机制。我们将从[变分形式](@entry_id:166033)的推导开始，建立有限元法的基础，然后系统地分析稳定性这一中心挑战，并介绍几种经典[稳定有限元](@entry_id:176475)对的设计。最后，我们将讨论一些旨在提升方法鲁棒性和求解效率的高级技术。

### [斯托克斯问题](@entry_id:755479)的[变分形式](@entry_id:166033)

[斯托克斯方程](@entry_id:196346)的有限元处理始于将其从强形式（即[偏微分方程](@entry_id:141332)形式）转化为[弱形式](@entry_id:142897)（或称[变分形式](@entry_id:166033)）。这一过程不仅为在有限维函数空间中寻找近似解提供了理论框架，也自然地揭示了对解（速度和压力）的[光滑性](@entry_id:634843)要求以及边界条件的处理方式。

#### 弱形式的推导与函数空间

考虑在有界Lipschitz区域 $\Omega \subset \mathbb{R}^d$ ($d=2,3$) 上的定常不可压[斯托克斯方程](@entry_id:196346)，其强形式为：
$$
\begin{cases}
-\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}, p) = \boldsymbol{f}  \text{ in } \Omega \\
\nabla \cdot \boldsymbol{u} = 0  \text{ in } \Omega
\end{cases}
$$
其中 $\boldsymbol{u}$ 是流体速度， $p$ 是压力，$\boldsymbol{f}$ 是体积力。柯西应力张量 $\boldsymbol{\sigma}(\boldsymbol{u}, p)$ 对于[牛顿流体](@entry_id:263796)定义为 $\boldsymbol{\sigma}(\boldsymbol{u}, p) = 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) - p\boldsymbol{I}$，其中 $\mu$ 是[动力粘度](@entry_id:268228)，$\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})$ 是应变率张量，$\boldsymbol{I}$ 是单位张量。

为了推导弱形式，我们将动量方程与一个任意的速度“检验”函数 $\boldsymbol{v}$ 做[内积](@entry_id:158127)，并在区域 $\Omega$ 上积分：
$$
-\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \boldsymbol{v} \, d\boldsymbol{x} = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\boldsymbol{x}
$$
利用[散度定理](@entry_id:143110)（或[分部积分](@entry_id:136350)），左侧项可以展开为：
$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla \boldsymbol{v} \, d\boldsymbol{x} - \int_{\partial\Omega} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{v} \, dS = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\boldsymbol{x}
$$
其中“$:$”表示张量的[Frobenius内积](@entry_id:153693)，$\boldsymbol{n}$ 是边界 $\partial\Omega$ 上的单位外[法向量](@entry_id:264185)。边界积分项 $\int_{\partial\Omega} (\boldsymbol{\sigma}\boldsymbol{n}) \cdot \boldsymbol{v} \, dS$ 的处理取决于边界条件。对于[流体力学](@entry_id:136788)中常见的固壁[无滑移边界条件](@entry_id:186229)，速度在边界上为零，即 $\boldsymbol{u} = \boldsymbol{0}$ on $\partial\Omega$。这是一个本质边界条件，我们在选择函数空间时会直接施加在速度的[试探函数](@entry_id:756165)和检验函数上。具体来说，我们要求[速度场](@entry_id:271461)和检验函数都属于[Sobolev空间](@entry_id:141995) $H_0^1(\Omega)^d$，该空间包含了所有在 $H^1(\Omega)^d$ 中且在边界上迹为零的函数。由于检验函数 $\boldsymbol{v}$ 在边界 $\partial\Omega$ 上为零，上述边界积分自然消失。[@problem_id:2600983]

将[应力张量](@entry_id:148973)的定义代入，体积积分项可写为：
$$
\int_{\Omega} (2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) - p\boldsymbol{I}) : \nabla \boldsymbol{v} \, d\boldsymbol{x} = \int_{\Omega} 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\boldsymbol{x} - \int_{\Omega} p (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x}
$$
这里利用了 $\boldsymbol{\varepsilon}(\boldsymbol{u})$ 的对称性以及 $\boldsymbol{I} : \nabla\boldsymbol{v} = \nabla \cdot \boldsymbol{v}$。

同样，我们将不可压缩条件 $\nabla \cdot \boldsymbol{u} = 0$ 与一个压力[检验函数](@entry_id:166589) $q$ 做[内积](@entry_id:158127)并在 $\Omega$ 上积分，得到 $\int_{\Omega} q (\nabla \cdot \boldsymbol{u}) \, d\boldsymbol{x} = 0$。

综合以上步骤，我们得到[斯托克斯问题](@entry_id:755479)的标准弱形式：寻找[速度场](@entry_id:271461) $\boldsymbol{u} \in \boldsymbol{V}$ 和压[力场](@entry_id:147325) $p \in Q$，使得对于所有的[检验函数](@entry_id:166589) $(\boldsymbol{v}, q) \in \boldsymbol{V} \times Q$，满足：
$$
\begin{cases}
\int_{\Omega} 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\boldsymbol{x} - \int_{\Omega} p (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x} = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, d\boldsymbol{x} \\
\int_{\Omega} q (\nabla \cdot \boldsymbol{u}) \, d\boldsymbol{x} = 0
\end{cases}
$$
基于上述推导，我们确定了合适的函数空间。对于速度场，由于积分项中包含[一阶导数](@entry_id:749425)（$\nabla\boldsymbol{u}$ 和 $\nabla\boldsymbol{v}$），并且需要满足齐次[Dirichlet边界条件](@entry_id:142800)，其自然的选择是[Sobolev空间](@entry_id:141995) $\boldsymbol{V} = H_0^1(\Omega)^d$。对于压[力场](@entry_id:147325)，它与速度的散度 $\nabla \cdot \boldsymbol{v}$ 配对，而对于 $\boldsymbol{v} \in H_0^1(\Omega)^d$，我们有 $\nabla \cdot \boldsymbol{v} \in L^2(\Omega)$。因此，为了使积分 $\int p (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x}$ 有意义，压力空间只需取为 $Q = L^2(\Omega)$。[@problem_id:2600894]

#### 压力的非唯一性与处理

一个关键的观察是，在上述[弱形式](@entry_id:142897)中，压力 $p$ 仅以其梯度形式出现（通过分部积分，$- \int p (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x}$ 等价于 $\int \nabla p \cdot \boldsymbol{v} \, d\boldsymbol{x}$）。这意味着如果 $(\boldsymbol{u}, p)$ 是一个解，那么对于任意常数 $c$，$(\boldsymbol{u}, p+c)$ 同样是一个解，因为 $\nabla (p+c) = \nabla p$。从弱形式的角度看，对于任意常数 $c$ 和任意[检验函数](@entry_id:166589) $\boldsymbol{v} \in H_0^1(\Omega)^d$，我们有：
$$
\int_{\Omega} c (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x} = c \int_{\Omega} \nabla \cdot \boldsymbol{v} \, d\boldsymbol{x} = c \int_{\partial\Omega} \boldsymbol{v} \cdot \boldsymbol{n} \, dS = 0
$$
由于 $\boldsymbol{v}$ 在边界上为零。这表明常数压[力场](@entry_id:147325)在动量方程的弱形式中没有贡献，导致压力解的非唯一性。

为了得到唯一解，我们必须移除这个不定常数。有两种等价的标准做法：
1.  **施加零均值约束**：将压力空间限制为 $Q = L_0^2(\Omega) := \{ q \in L^2(\Omega) : \int_{\Omega} q \, d\boldsymbol{x} = 0 \}$。这相当于在所有相差一个常数的等价类中，选择那个积分为零的唯一代表。
2.  **使用商空间**：在商空间 $Q = L^2(\Omega)/\mathbb{R}$ 中求解压力。该空间中的元素是压力的[等价类](@entry_id:156032) $[p] = \{ p+c : c \in \mathbb{R} \}$。

在实际计算中，施加零均值约束是更常用和直接的方法。[@problem_id:2600894]

#### 粘性项的不同形式

粘性项 $a(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\boldsymbol{x}$ 直接源于物理应力张量，这是最“物理”的表达形式。然而，在某些情况下，特别是当流体不可压缩时，会使用一种简化的形式。回顾动量方程的强形式，粘性项也可以写作 $-\mu\Delta \boldsymbol{u}$，前提是粘度 $\mu$ 为常数。对应的弱形式为 $a_{\nabla}(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} \mu \nabla\boldsymbol{u} : \nabla\boldsymbol{v} \, d\boldsymbol{x}$。

这两种形式之间的关系可以通过一个恒等式揭示：
$$
\int_{\Omega} 2\mu\boldsymbol{\varepsilon}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\boldsymbol{x} = \int_{\Omega} \mu \nabla\boldsymbol{u} : \nabla\boldsymbol{v} \, d\boldsymbol{x} + \int_{\Omega} \mu (\nabla \cdot \boldsymbol{u})(\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x}
$$
对于[斯托克斯问题](@entry_id:755479)的精确解 $\boldsymbol{u}$，由于它满足 $\nabla \cdot \boldsymbol{u} = 0$，上式右边的第二项为零。因此，对于精确解而言，两种粘性项的提法是等价的。然而，当进行有限元离散时，离散速度解 $\boldsymbol{u}_h$ 通常不精确满足[无散条件](@entry_id:755034)（即 $\nabla \cdot \boldsymbol{u}_h \neq 0$）。在这种情况下，使用对称梯度形式 $a_{\epsilon}$ 或全梯度形式 $a_{\nabla}$ 会导致不同的离散系统和不同的解。尽管在 $H_0^1(\Omega)^d$ 空间上，由这两种双线性形式诱导的能量范数是等价的（这可以通过[Korn不等式](@entry_id:174794)证明），但在实际计算中，它们的差异可能很重要。物理上更准确的 $a_{\epsilon}$ 形式通常是首选。[@problem_id:2600922]

### 离散化与稳定性挑战

Galerkin[有限元法](@entry_id:749389)的核心思想是将[变分问题](@entry_id:756445)限制在有限维的[子空间](@entry_id:150286)中。我们选择速度和压力的有限元空间 $\boldsymbol{V}_h \subset \boldsymbol{V}$ 和 $Q_h \subset Q$，然后求解离散问题：寻找 $(\boldsymbol{u}_h, p_h) \in \boldsymbol{V}_h \times Q_h$，使得对于所有 $(\boldsymbol{v}_h, q_h) \in \boldsymbol{V}_h \times Q_h$，满足离散[变分方程](@entry_id:635018)。

#### [协调有限元](@entry_id:170866)方法

一个离散方法被称为**协调的 (conforming)**，如果其离散函数空间是连续问题[函数空间](@entry_id:143478)的[真子集](@entry_id:152276)，即 $\boldsymbol{V}_h \subset \boldsymbol{V} = H_0^1(\Omega)^d$ 和 $Q_h \subset Q = L_0^2(\Omega)$。要成为 $H^1$ 协调的，有限元函数必须是全局连续的（$C^0$连续性）。因此，协调的速度空间 $\boldsymbol{V}_h$ 通常由定义在网格上的连续分片多项式构成，并且在区域边界 $\partial\Omega$ 上取值为零。同样，协调的压力空间 $Q_h$ 通常由连续的分片多项式构成，并附加零均值约束。例如，经典的[Taylor-Hood单元](@entry_id:165658)（$\mathbb{P}_{k+1}/\mathbb{P}_k$）和MINI单元都属于[协调有限元](@entry_id:170866)方法。[@problem_id:2600949]

#### 离散inf-sup (LBB) 条件

[斯托克斯问题](@entry_id:755479)的[鞍点](@entry_id:142576)结构要求速度和压力[离散空间](@entry_id:155685)之间必须满足一个关键的相容性条件，即**离散[inf-sup条件](@entry_id:746626)**，也称为Ladyzhenskaya–Babuška–Brezzi (LBB)条件。该条件要求存在一个与网格尺寸 $h$ 无关的正常数 $\beta_0$，使得：
$$
\inf_{0 \neq q_h \in Q_h} \sup_{0 \neq \boldsymbol{v}_h \in \boldsymbol{V}_h} \frac{-\int_{\Omega} q_h (\nabla \cdot \boldsymbol{v}_h) \, d\boldsymbol{x}}{\|\boldsymbol{v}_h\|_{H^1(\Omega)} \|q_h\|_{L^2(\Omega)}} \ge \beta_0 > 0
$$
这个条件本质上保证了离散压力空间 $Q_h$ 不能“太大”以至于离散速度空间 $\boldsymbol{V}_h$ 的散度空间 $\nabla \cdot \boldsymbol{V}_h$ 无法控制它。如果[LBB条件](@entry_id:746626)不满足，离散问题将是不稳定的，表现为压力解中出现伪 (spurious) 震荡，这种震荡污染了整个数值解，使其毫无意义。

[LBB条件](@entry_id:746626)的违反是许多看似合理的有限元对失败的根源。一个典型的例子是**等阶插值**，例如在每个单元上都使用连续分片线性函数来逼近速度和压力（$\mathbb{P}_1/\mathbb{P}_1$ 单元）。这种选择之所以不稳定，是因为离散[速度空间](@entry_id:181216)的散度空间“太小”。对于一个 $\mathbb{P}_1$ [速度场](@entry_id:271461) $\boldsymbol{v}_h$，其散度 $\nabla \cdot \boldsymbol{v}_h$ 在每个单元上是一个常数（$\mathbb{P}_0$）。然而，压力空间是连续分片线性的（$\mathbb{P}_1$）。这意味着我们试图用一个分片常数的空间去“控制”一个分片线性的空间，这是不可能的。存在非零的线性[压力模](@entry_id:159654)式 $q_h$，它与所有分片常数函数在其 $L^2$ [内积](@entry_id:158127)意义下正交。这样的 $q_h$ 会导致[inf-sup条件](@entry_id:746626)中的商为零，从而 $\beta_h=0$。

一个著名的例子是在矩形网格上使用 $\mathbb{Q}_1/\mathbb{Q}_1$ 单元（[双线性](@entry_id:146819)速度/[双线性](@entry_id:146819)压力）。这种单元对存在一种称为“棋盘”模式的伪压力解：在网格节点上交替赋值 $+1$ 和 $-1$。这种[压力模](@entry_id:159654)式在每个单元内部都是非零的，但它与任何[双线性](@entry_id:146819)速度场的散度（其形式为 $c_1 + c_2x + c_3y$）正交。因此，这种[压力模](@entry_id:159654)式位于离散[散度算子](@entry_id:265975)作用下的“核”中，无法被唯一确定，导致了数值不稳定。[@problem_id:2600924]

### [稳定有限元](@entry_id:176475)对的设计

为了克服稳定性问题，研究人员设计了多种满足[LBB条件](@entry_id:746626)的有限元对。其基本思想是，相对于压力空间，速度空间必须足够“丰富”。

#### Fortin准则

证明一个有限元对满足[LBB条件](@entry_id:746626)的一个强大理论工具是**Fortin准则**（或Fortin引理）。该准则指出，如果存在一个[线性算子](@entry_id:149003) $\Pi_F: \boldsymbol{V} \to \boldsymbol{V}_h$（称为Fortin算子），满足以下两个条件：
1.  **散度保持性**：对于所有 $q_h \in Q_h$，算子保持与离散压力的配对，即 $\int_{\Omega} q_h (\nabla \cdot (\Pi_F \boldsymbol{v})) \, d\boldsymbol{x} = \int_{\Omega} q_h (\nabla \cdot \boldsymbol{v}) \, d\boldsymbol{x}$ for all $\boldsymbol{v} \in \boldsymbol{V}$。
2.  **稳定性**：算子在 $\boldsymbol{V}$ 范数下是有界的，即存在一个与网格无关的常数 $C_F$，使得 $\|\Pi_F \boldsymbol{v}\|_{\boldsymbol{V}} \le C_F \|\boldsymbol{v}\|_{\boldsymbol{V}}$。

那么，离散inf-sup常数 $\beta_h$ 就有一个不依赖于网格尺寸的下界：$\beta_h \ge \beta / C_F$，其中 $\beta$ 是连续问题的inf-sup常数。Fortin准则将证明离散稳定性的复杂任务转化为了构造一个具有特定性质的插值算子的问题。[@problem_id:2600959]

#### [Taylor-Hood单元](@entry_id:165658)族 ($\mathbb{P}_{k+1}/\mathbb{P}_k$)

[Taylor-Hood单元](@entry_id:165658)族是求解不可压流动问题最著名和最广泛使用的[稳定有限元](@entry_id:176475)对之一。对于单纯形网格（二维为三角形，三维为四面体），其定义为：
*   **[速度空间](@entry_id:181216) $\boldsymbol{V}_h$**：由分片 $k+1$ 次（$\mathbb{P}_{k+1}$）的连续多项式组成。
*   **压力空间 $Q_h$**：由分片 $k$ 次（$\mathbb{P}_k$）的连续多项式组成。

其中 $k \ge 1$。最经典的例子是 $\mathbb{P}_2/\mathbb{P}_1$ 单元。这个单元族是协调的，并且已被证明对于任意 $k \ge 1$ 和空间维度 $d=2,3$，在形状规则的网格上都满足离散[inf-sup条件](@entry_id:746626)。其稳定性的标准证明正是通过构造一个满足Fortin准则的算子来完成的。[@problem_id:2600964]

#### MINI单元（$\mathbb{P}_1$-bubble/$\mathbb{P}_1$）

另一种稳定化策略不是提高速度多项式的次数，而是在[速度空间](@entry_id:181216)中加入**“泡泡”函数 (bubble function)**。MINI单元（由Arnold, Brezzi, Fortin提出）就是一个典型例子，它对不稳定的 $\mathbb{P}_1/\mathbb{P}_1$ 单元进行了修正：
*   **速度空间 $\boldsymbol{V}_h$**：由标准的连续分片线性[函数空间](@entry_id:143478)，并辅以单元内部的[气泡函数](@entry_id:176111) (element-wise bubble functions) 构成。每个[气泡函数](@entry_id:176111)都是一个在单元边界上为零的高次多项式。
*   **压力空间 $Q_h$**：标准的连续分片线性[函数空间](@entry_id:143478)。

泡泡函数的核心作用是丰富离散速度场的散度空间。一个典型的泡泡函数 $b_K$（例如，在[三角形单元](@entry_id:167871)上是三个[重心坐标](@entry_id:155488)的乘积）的散度在单元内部是非零的多项式。例如，$\nabla \cdot (b_K \boldsymbol{e}_i) = \partial b_K / \partial x_i$，这是一个次数比常数高的多项式。这些额外的“内部”散度模式，使得[速度空间](@entry_id:181216)足以控制分片线性的压力空间，从而满足[LBB条件](@entry_id:746626)。泡泡函数由于其局部支撑（仅在单个单元内非零），可以在单元级别通过[静态凝聚](@entry_id:176722)（static condensation）被消除，从而不增加全局问题的自由度数量，这使得该方法在计算上非常高效。[@problem_id:2600974]

### 高级主题：鲁棒性与求解

对于大规模的[斯托克斯问题](@entry_id:755479)，高效的[迭代求解器](@entry_id:136910)至关重要。这引出了对离散格式的更深入分析，包括稳定化方法和对物理参数的鲁棒性。

#### Grad-div稳定化

**Grad-div稳定化**是在[动量方程](@entry_id:197225)的[弱形式](@entry_id:142897)中添加一个惩罚项 $\gamma \int_{\Omega} (\nabla \cdot \boldsymbol{u}_h)(\nabla \cdot \boldsymbol{v}_h) \, d\boldsymbol{x}$，其中 $\gamma > 0$ 是一个惩罚参数。这个项有两个主要作用：
1.  对于不满足[LBB条件](@entry_id:746626)的有限元对（如等阶插值），它可以起到稳定化的作用，抑制[伪压力模式](@entry_id:755261)。
2.  对于LBB稳定的单元对，它可以改善线性系统的代数性质，使得[迭代求解器](@entry_id:136910)（特别是预处理器）的设计更加简单和鲁棒。

从代数角度看，grad-div项在速度-速度[耦合矩阵](@entry_id:191757) $A$ 上增加了一个矩阵 $\gamma G$。通过傅里叶分析可以揭示其对系统谱性质的深刻影响 (profound effect on the system's spectral properties)。它使得增广后的速度块 $\tilde{A} = A + \gamma G$ 对于表示无旋模式 (irrotational modes) 的向量变得更“硬”。更重要的是，它极大地改变了压力[Schur补](@entry_id:142780) $S = B\tilde{A}^{-1}B^{\top}$ 的性质。对于标准的斯托克斯系统，[Schur补](@entry_id:142780)在谱上等价于一个与粘度成反比的[拉普拉斯算子](@entry_id:146319)。而对于grad-div稳定化的系统，[Schur补](@entry_id:142780)在谱上等价于一个与 $(\mu+\gamma)^{-1}$ 成正比的**[质量矩阵](@entry_id:177093)**。这意味着一个简单的、由 $(\mu+\gamma)^{-1}$ 缩放 (scaled) 的压力[质量矩阵](@entry_id:177093)就可以作为Schur补的优秀预条件子，其性能与网格尺寸和参数 $\gamma$ 无关。同时，为了有效[预处理](@entry_id:141204)高度各向异性 (highly anisotropic) 的速度块 $\tilde{A}$，需要使用能够处理这种各向异性的多重网格光滑子（例如Vanka型或Braess-Sarazin型光滑子）。[@problem_id:2600927]

#### [压力鲁棒性](@entry_id:167963)

在标准的有限元方法中，速度的离散误差通常会依赖于压力的逼近误差。当问题的解包含大[压力梯度](@entry_id:274112)时，这种依赖性会导致速度解的精度显著下降。一个**压力鲁棒 (pressure-robust)** 的离散方法，其速度误差不依赖于压力（或者说，不依赖于力的无旋部分）。

这个概念源于对连续方程的观察。通过[Helmholtz-Hodge分解](@entry_id:140525)，任何[力场](@entry_id:147325) $\boldsymbol{f}$ 都可以分解为一个无散 (solenoidal) 部分 $\boldsymbol{g}$ 和一个无旋 (irrotational) 部分 $\nabla\phi$：$\boldsymbol{f} = \boldsymbol{g} + \nabla\phi$。在[斯托克斯方程](@entry_id:196346)中，速度 $\boldsymbol{u}$ 完全由无散力 $\boldsymbol{g}$ 决定，而压力 $p$ 则与无旋力 $\nabla\phi$ 相关。标准的有限元方法破坏了这种[解耦](@entry_id:637294)。由于离散[速度空间](@entry_id:181216)通常不是精确无散的（$\nabla \cdot \boldsymbol{v}_h \neq 0$），无旋力 $\nabla\phi$ 会对离散动量方程产生非零贡献（$\int \nabla\phi \cdot \boldsymbol{v}_h \, d\boldsymbol{x} = -\int \phi (\nabla \cdot \boldsymbol{v}_h) \, d\boldsymbol{x} \neq 0$），从而污染速度解。[@problem_id:2600893]

实现[压力鲁棒性](@entry_id:167963)有两种主要途径：
1.  **使用精确无散的有限元**：如果离散速度空间中的函数满足精确[无散条件](@entry_id:755034)（$\nabla \cdot \boldsymbol{v}_h = 0$），例如Scott-Vogelius单元，那么无旋力的贡献自动为零。这类方法天然具有[压力鲁棒性](@entry_id:167963)。
2.  **修正[变分形式](@entry_id:166033)**：对于非精确无散的单元（如Taylor-Hood），可以通过修改右端项来实现。具体做法是引入一个速度重构算子 $\mathcal{R}_h$，将检验函数 $\boldsymbol{v}_h$ 映射到一个精确无散的（或至少在离散意义下正交于[梯度场](@entry_id:264143)）速度场 $\mathcal{R}_h \boldsymbol{v}_h$，然后用 $\int \boldsymbol{f} \cdot (\mathcal{R}_h \boldsymbol{v}_h) \, d\boldsymbol{x}$ 代替原来的右端项。这样，无旋力部分的作用就被有效地消除了，从而恢复了[压力鲁棒性](@entry_id:167963)。[@problem_id:2600893]