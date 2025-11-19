## 引言
在[数值模拟](@entry_id:137087)领域，有限元法（FEM）和[边界元法](@entry_id:141290)（BEM）是[求解偏微分方程](@entry_id:138485)的两种主流方法，各自拥有独特的优势和适用范围。[有限元法](@entry_id:749389)以其处理复杂几何、[非线性](@entry_id:637147)材料和非均质介质的强大灵活性而著称，但当求解域延伸至无限远时，它会面临人工截断边界和网格剖分困难的挑战。相反，[边界元法](@entry_id:141290)通过将问题转化为边界上的积分方程，天然地适用于无限域或[半无限域](@entry_id:175316)问题，并能以极高的精度计算边界上的场量，但其应用通常局限于线性和均匀介质。

如何有效结合这两种方法的优点，以应对那些既包含复杂内部结构又涉及无限外部环境的工程与科学问题？这正是有限元-边界元（FEM-BEM）耦合策略所要解决的核心知识鸿沟。这种耦合不仅是一种数值技巧，更是一种深刻的建模思想，它允许我们将一个复杂问题分解为最适合各自方法处理的[子域](@entry_id:155812)，从而实现[计算效率](@entry_id:270255)和精度的最优化。

本文旨在为读者提供一个关于FEM-BEM耦合策略的系统性指南。我们将从三个层面逐步深入：首先，在“原理与机制”一章中，我们将奠定坚实的数学基础，详细阐述界面传输条件、[边界积分算子](@entry_id:173789)理论以及对称与非[对称耦合](@entry_id:176860)的[变分形式](@entry_id:166033)。接着，在“应用与跨学科连接”一章中，我们将展示这些理论如何在[静电学](@entry_id:140489)、波传播、固体力学等多个领域中大放异彩，揭示其解决实际问题的强大能力。最后，通过“动手实践”部分，我们提供了一系列精心设计的练习，引导读者将理论知识转化为具体的数值实现，加深对[耦合方法](@entry_id:195982)核心环节的理解。

## 原理与机制

有限元法 (FEM) 与[边界元法 (BEM)](@entry_id:746941) 的耦合，其核心在于将一个问题的求解域分割为两个部分：一个是由有限元法处理的有限内部域，另一个是由[边界元法](@entry_id:141290)处理的无限或复杂的外部域。本章旨在深入阐述支撑这些耦合策略的数学原理和核心机制。我们将从定义域边界上的物理传输条件出发，建立所需的数学框架，然后介绍作为[边界元法](@entry_id:141290)基石的积分表示和算子，最后推导并分析几种关键的耦合[变分形式](@entry_id:166033)及其离散化后的[代数结构](@entry_id:137052)。

### 界面上的数学与物理基础

耦合策略的起点是准确描述内部域 $\Omega$ 和外部域 $\Omega^c$ 共享的界面 $\Gamma$ 上的场行为。这些行为由物理[守恒定律](@entry_id:269268)决定，并必须转化为严谨的数学条件。

#### 传输条件

考虑一个典型的传输问题，其中内部域 $\Omega$ 的物理特性（例如，由张量 $A$ 描述的[扩散](@entry_id:141445)系数）与外部域不同。设内部场为 $u_{\mathrm{int}}$，外部场为 $u_{\mathrm{ext}}$。在界面 $\Gamma$ 上，两个基本物理原理必须得到满足：

1.  **[势场](@entry_id:143025)的连续性**：除非界面上存在偶极子源，否则物理[势场](@entry_id:143025)（如温度、[电势](@entry_id:267554)或位移）在跨越界面时必须是连续的。这可以用[迹算子](@entry_id:183665) $\gamma^-$（从内部逼近 $\Gamma$）和 $\gamma^+$（从外部逼近 $\Gamma$）来表示。因此，第一个传输条件是：
    $$ \gamma^- u_{\mathrm{int}} = \gamma^+ u_{\mathrm{ext}} $$
    这个等式描述了狄利克雷数据 (Dirichlet data) 在界面上的连续性。

2.  **通量的平衡**：第二个条件源于通量守恒。穿过界面的净通量必须等于界面上源的强度。内部域的通量由其控制方程导出，例如，对于内部方程 $-\nabla \cdot (A \nabla u_{\mathrm{int}}) = f$，其在 $\Gamma$ 上的法向通量为 $(A \nabla u_{\mathrm{int}}) \cdot \mathbf{n}$，其中 $\mathbf{n}$ 是从 $\Omega$ 指向外部的[单位法向量](@entry_id:178851)。外部场的法向通量则根据其自身的控制方程（如[拉普拉斯方程](@entry_id:143689) $\Delta u_{\mathrm{ext}} = 0$）定义。特别需要注意的是法向量的定义。若外部域 $\Omega^c$ 的外法向为 $\mathbf{n}^+ = -\mathbf{n}$，并且其[法向导数](@entry_id:169511)定义为 $\partial_n u_{\mathrm{ext}} := \nabla u_{\mathrm{ext}} \cdot \mathbf{n}^+$，那么[通量平衡](@entry_id:637776)（考虑界面上可能存在的单极子源密度 $g$）可以表示为两个通量之和等于源密度。从 $\Omega$ 流出的通量为 $(A \nabla u_{\mathrm{int}}) \cdot \mathbf{n}$，而从 $\Omega^c$ 流入 $\Omega$ 的通量为 $-(\nabla u_{\mathrm{ext}} \cdot \mathbf{n}^+)$，因为 $\mathbf{n}^+$ 是 $\Omega^c$ 的外法向。因此，第二个传输条件是 [@problem_id:2551198]：
    $$ (A \nabla u_{\mathrm{int}}) \cdot \mathbf{n} + \partial_n u_{\mathrm{ext}} = g $$
    此条件描述了诺伊曼数据 (Neumann data) 在界面上的跳跃或平衡关系。

#### [变分形式](@entry_id:166033)的[函数空间](@entry_id:143478)框架

为了将这些传输条件融入稳健的变分公式中，我们需要一个严格的[函数空间](@entry_id:143478)框架。这由索博列夫空间 (Sobolev spaces) 理论提供。

根据[迹定理](@entry_id:203967)，定义在区域 $\Omega$ 上的 $H^1(\Omega)$ 空间中的函数，其在边界 $\Gamma$ 上的迹（即其边界值）存在于一个分数阶索博列夫空间 $H^{1/2}(\Gamma)$ 中。这个空间是狄利克雷数据的自然选择。具体而言，$H^{1/2}(\Gamma)$ 可以被定义为 $H^1(\Omega)$ 在[迹算子](@entry_id:183665) $\gamma$ 下的像空间，并赋予[商范数](@entry_id:270575)：
$$ \|\phi\|_{H^{1/2}(\Gamma)} := \inf\{\|u\|_{H^1(\Omega)} : u \in H^1(\Omega),\, \gamma u = \phi\} $$

相应地，诺伊曼数据（[法向导数](@entry_id:169511)）所在的自然空间是 $H^{1/2}(\Gamma)$ 的[对偶空间](@entry_id:146945)，记为 $H^{-1/2}(\Gamma)$。它定义为 $H^{1/2}(\Gamma)$ 上的所有[连续线性泛函](@entry_id:262913)构成的空间，即 $H^{-1/2}(\Gamma) := (H^{1/2}(\Gamma))'$。这两个空间之间的关系通过一个对偶作用 (duality pairing) $\langle \cdot, \cdot \rangle_{\Gamma}$ 来实现，该作用是 $L^2(\Gamma)$ [内积](@entry_id:158127)的自然延拓。如果 $\lambda \in L^2(\Gamma)$，那么它在 $H^{-1/2}(\Gamma)$ 中对应的泛函作用于 $\phi \in H^{1/2}(\Gamma)$ 时，其值就是 $L^2$ [内积](@entry_id:158127) $\int_{\Gamma} \lambda \phi \, \mathrm{d}s$。这个由 $H^{1/2}(\Gamma) \hookrightarrow L^2(\Gamma) \hookrightarrow H^{-1/2}(\Gamma)$ 构成的结构被称为[Gelfand三元组](@entry_id:195116)，其中 $L^2(\Gamma)$ 作为中心枢轴空间 (pivot space)。在耦合公式中，所有边界上的变分项都将通过这个对偶作用来表达 [@problem_id:2551169]。

### 外部解的积分表示

[边界元法](@entry_id:141290)的威力在于它能够将外部域 $\Omega^c$ 中的[偏微分方程](@entry_id:141332)求解问题，转化为一个只涉及边界 $\Gamma$ 的[积分方程](@entry_id:138643)。这一转化的关键工具是[格林公式](@entry_id:173118) (Green's representation formula)。

#### 格林表示公式

对于在外部域 $\Omega^c$ 中满足 $(\Delta + k^2)u = 0$（其中 $k \ge 0$ 为波数，对于[拉普拉斯方程](@entry_id:143689) $k=0$）的解 $u$，格林表示公式给出了 $u$ 在 $\Omega^c$ 中任意点 $\boldsymbol{x}$ 的值，该值由其在边界 $\Gamma$ 上的狄利克雷迹 $\gamma u$ 和诺伊曼迹 $\gamma_1 u$ 表示。公式如下 [@problem_id:2551146]：
$$ u(\boldsymbol{x}) = \int_{\Gamma} \left( \frac{\partial G_k(\boldsymbol{x},\boldsymbol{y})}{\partial \nu_{\boldsymbol{y}}} \, \gamma u(\boldsymbol{y}) - G_k(\boldsymbol{x},\boldsymbol{y}) \, \gamma_1 u(\boldsymbol{y}) \right) \, \mathrm{d}s_{\boldsymbol{y}}, \quad \forall \boldsymbol{x} \in \Omega^c $$
其中，$G_k$ 是亥姆霍兹 (Helmholtz) 算子的**[基本解](@entry_id:184782)**（或称[格林函数](@entry_id:147802)），满足 $(\Delta_y + k^2)G_k(\boldsymbol{x},\boldsymbol{y}) = -\delta(\boldsymbol{y}-\boldsymbol{x})$。$\nu$ 是指向 $\Omega^c$ 的[单位法向量](@entry_id:178851)。该公式的成立依赖于解 $u$ 在无穷远处的适当衰减或辐射条件，例如，对于三维亥姆霍兹方程，要求满足[Sommerfeld辐射条件](@entry_id:168772)；对于[三维拉普拉斯方程](@entry_id:170096)，要求 $u(\boldsymbol{x}) = \mathcal{O}(|\boldsymbol{x}|^{-1})$。

#### 层势理论与跳跃关系

格林表示公式中的两个积分项具有深刻的物理和数学意义。它们被称为**单层势 (single-layer potential)** 和**双层势 (double-layer potential)**。

给定边界上的源密度函数 $\varphi$（称为单层密度）和偶极矩密度函数 $\psi$（称为双层密度），我们可以定义：
- **单层势** $u_S(\boldsymbol{x}) := \int_{\Gamma} G(\boldsymbol{x},\boldsymbol{y})\,\varphi(\boldsymbol{y})\,ds_{\boldsymbol{y}}$
- **双层势** $u_D(\boldsymbol{x}) := \int_{\Gamma} \frac{\partial G}{\partial n_{\boldsymbol{y}}}(\boldsymbol{x},\boldsymbol{y})\,\psi(\boldsymbol{y})\,ds_{\boldsymbol{y}}$

这些[势函数](@entry_id:176105)在整个空间（除了源所在的边界 $\Gamma$）都满足齐次的[偏微分方程](@entry_id:141332)。当观测点 $\boldsymbol{x}$ 趋近于边界 $\Gamma$ 时，这些势及其[法向导数](@entry_id:169511)表现出特定的**跳跃关系 (jump relations)** [@problem_id:2551214]。

- **单层势 $u_S$**：其本身是跨越边界 $\Gamma$ 连续的，但其[法向导数](@entry_id:169511)会发生跳跃，跳跃量恰好等于源密度 $\varphi$。
  - $\gamma^+ u_S - \gamma^- u_S = 0$
  - $\partial_n^+ u_S - \partial_n^- u_S = \varphi$

- **双层势 $u_D$**：其[法向导数](@entry_id:169511)在跨越边界 $\Gamma$ 时是连续的（在适当的正则性假设下），但其本身会发生跳跃，跳跃量等于负的偶极矩密度 $-\psi$。
  - $\gamma^+ u_D - \gamma^- u_D = -\psi$
  - $\partial_n^+ u_D - \partial_n^- u_D = 0$

这些跳跃关系是推导[边界积分方程](@entry_id:746942)的基础，因为它们将边界上的未知量（迹和通量）与定义它们的层密度联系起来。

### [边界积分算子](@entry_id:173789)

为了系统地处理边界上的[变分问题](@entry_id:756445)，我们将层势在边界上的迹和[法向导数](@entry_id:169511)迹定义为四个基本的**[边界积分算子](@entry_id:173789) (Boundary Integral Operators, BIOs)**。这些算子是FEM-BEM耦合[变分形式](@entry_id:166033)的核心构件 [@problem_id:2551168]。

对于[拉普拉斯方程](@entry_id:143689)，这四个算子定义如下（$\boldsymbol{x} \in \Gamma$）：
- **单层算子 (Single-Layer Operator, $V$)**:
  $$ (V \varphi)(\boldsymbol{x}) := \int_{\Gamma} G(\boldsymbol{x},\boldsymbol{y})\,\varphi(\boldsymbol{y})\,\mathrm{d}s_{\boldsymbol{y}} $$
  它将诺伊曼数据 $\varphi \in H^{-1/2}(\Gamma)$ 映射为狄利克雷数据 $V\varphi \in H^{1/2}(\Gamma)$。这是一个[平滑算子](@entry_id:636528)，且是自伴和正定的。

- **双层算子 (Double-Layer Operator, $K$)**:
  $$ (K \psi)(\boldsymbol{x}) := \mathrm{p.v.} \int_{\Gamma} \frac{\partial G}{\partial n_{\boldsymbol{y}}}(\boldsymbol{x},\boldsymbol{y})\,\psi(\boldsymbol{y})\,\mathrm{d}s_{\boldsymbol{y}} $$
  它将狄利克雷数据 $\psi \in H^{1/2}(\Gamma)$ 映射到同一空间。积分是强奇异的，需在[柯西主值](@entry_id:192761) (p.v.) 意义下理解。

- **伴随双层算子 (Adjoint Double-Layer Operator, $K'$)**:
  $$ (K' \varphi)(\boldsymbol{x}) := \mathrm{p.v.} \int_{\Gamma} \frac{\partial G}{\partial n_{\boldsymbol{x}}}(\boldsymbol{x},\boldsymbol{y})\,\varphi(\boldsymbol{y})\,\mathrm{d}s_{\boldsymbol{y}} $$
  它是 $K$ 在 $L^2(\Gamma)$ [内积](@entry_id:158127)下的[伴随算子](@entry_id:140236)，将诺伊曼数据 $\varphi \in H^{-1/2}(\Gamma)$ 映射到同一空间。

- **超奇异算子 (Hypersingular Operator, $W$)**:
  $$ (W \psi)(\boldsymbol{x}) := - \frac{\partial}{\partial n_{\boldsymbol{x}}} \int_{\Gamma} \frac{\partial G}{\partial n_{\boldsymbol{y}}}(\boldsymbol{x},\boldsymbol{y})\,\psi(\boldsymbol{y})\,\mathrm{d}s_{\boldsymbol{y}} $$
  它将狄利克雷数据 $\psi \in H^{1/2}(\Gamma)$ 映射为诺伊曼数据 $W\psi \in H^{-1/2}(\Gamma)$。负号是约定俗成的，以保证算子的[正定性](@entry_id:149643)。

#### 超奇异算子与正则化

超奇异算子 $W$ 在[对称耦合](@entry_id:176860)格式中扮演着核心角色，但其数值处理也最具挑战性。其积分核 $\frac{\partial^2 G}{\partial n_{\boldsymbol{x}} \partial n_{\boldsymbol{y}}}$ 的奇异性非常强，当 $\boldsymbol{y} \to \boldsymbol{x}$ 时，其行为在三维空间中如 $|\boldsymbol{x}-\boldsymbol{y}|^{-3}$，在二维空间中如 $|\boldsymbol{x}-\boldsymbol{y}|^{-2}$。这种强度的奇异性导致积分在经典意义下是发散的，甚至[柯西主值](@entry_id:192761)也不存在。因此，该积分必须在更广义的Hadamard有限部分 (Hadamard finite-part) 意义下进行解释 [@problem_id:2551170]。在数值计算中，直接使用标准求积公式（如[高斯求积](@entry_id:146011)）计算其离散[矩阵元](@entry_id:186505)素是不可行的，必须采用**正则化 (regularization)** 技术。这通常通过在边界上进行分部积分，将[超奇异积分](@entry_id:750482)转化为弱[奇异积分](@entry_id:167381)（其核的奇异性较弱，如 $\ln|\boldsymbol{x}-\boldsymbol{y}|$ 或 $|\boldsymbol{x}-\boldsymbol{y}|^{-1}$）或使用为[超奇异积分](@entry_id:750482)专门设计的特殊求积法则来实现。

### 变分耦合公式

有了上述数学工具，我们便可以将内部域的FEM[变分形式](@entry_id:166033)与外部域的BEM[积分方程](@entry_id:138643)结合起来，形成一个统一的[变分问题](@entry_id:756445)。

#### Johnson-Nédélec 非[对称耦合](@entry_id:176860)

Johnson-Nédélec耦合是一种经典的非对称格式。其未知量是内部场的解 $u \in H^1(\Omega)$ 和外部场的诺伊曼迹 $\lambda \in H^{-1/2}(\Gamma)$。通过对内部问题的[弱形式](@entry_id:142897)和外部问题的直接[边界积分方程](@entry_id:746942)进行组合，可以得到一个耦合的[双线性形式](@entry_id:746794) $b((u,\lambda);(v,\mu))$，其中 $(v,\mu)$ 是测试函数。

推导过程如下：
1.  **内部方程**：将内部方程 $-\nabla \cdot (A \nabla u) = f$ 乘以测试函数 $v \in H^1(\Omega)$ 并在 $\Omega$ 上积分，利用[格林公式](@entry_id:173118)和通量传输条件 $(A \nabla u) \cdot \mathbf{n} = \phi_0 - \lambda$，得到第一个[变分方程](@entry_id:635018)。
2.  **[边界积分方程](@entry_id:746942)**：外部场的迹 $(\eta, \lambda) = (\gamma^+ u^{\mathrm{ext}}, \partial_n^+ u^{\mathrm{ext}})$ 满足Calderón[投影算子](@entry_id:154142)给出的关系，例如 $(\frac{1}{2}I - K)\eta + V\lambda = 0$。利用[势场](@entry_id:143025)连续性条件 $\eta = \gamma u - u_0$，得到一个连接 $\gamma u$ 和 $\lambda$ 的算子方程。
3.  **组合**：将上述两个[方程组](@entry_id:193238)合，得到一个关于 $(u, \lambda)$ 的[鞍点问题](@entry_id:174221)，其[双线性形式](@entry_id:746794)为 [@problem_id:2551192]：
    $$ b\big((u,\lambda);(v,\mu)\big) = \int_{\Omega} (A \nabla u) \cdot \nabla v \, \mathrm{d}x + \langle \lambda, \gamma v \rangle_{\Gamma} + \big\langle \left(\tfrac{1}{2} I - K\right) \gamma u, \mu \big\rangle_{\Gamma} + \langle V \lambda, \mu \rangle_{\Gamma} $$
    由于 $\langle \lambda, \gamma v \rangle_{\Gamma}$ 和 $\langle (\frac{1}{2}I-K)\gamma u, \mu \rangle_{\Gamma}$ 这两个[交叉](@entry_id:147634)项的存在，该形式关于[试探函数](@entry_id:756165) $(u, \lambda)$ 和测试函数 $(v, \mu)$ 并不是对称的。

#### Costabel [对称耦合](@entry_id:176860)

对称的耦合格式在代数求解上通常更具优势（例如，可以使用[共轭梯度法](@entry_id:143436)）。Costabel提出的对称格式通过精心选择[变分方程](@entry_id:635018)和利用算子的伴随性质来实现对称性。其未知量通常是内部解 $u \in H^1(\Omega)$ 和一个边界通量未知量 $\phi \in H^{-1/2}(\Gamma)$。

对称格式的构造利用了外部问题的两个[边界积分方程](@entry_id:746942)，并与内部弱形式巧妙地结合。最终得到的双线性形式结构上是完全对称的，典型形式如下 [@problem_id:2551177]：
$$ a\big((u,\phi),(v,\chi)\big) = (\nabla u,\nabla v)_{\Omega} + \langle W\gamma u, \gamma v\rangle_{\Gamma} + \langle \big(\tfrac{1}{2}I - K\big)\gamma u, \chi\rangle_{\Gamma} + \langle \big(\tfrac{1}{2}I - K\big)\gamma v, \phi\rangle_{\Gamma} + \langle V\phi, \chi\rangle_{\Gamma} $$
此处的对称性源于：第一项和第二项显然是对称的（$V$ 和 $W$ 是自伴算子），而两个交叉项互为转置（利用了 $K$ 和 $K'$ 的伴随关系），最后一项也是对称的。

#### [数值稳定性](@entry_id:146550)与Inf-Sup条件

对于非对称或[混合格式](@entry_id:167436)，其[数值方法的收敛性](@entry_id:635470)和稳定性由所谓的**[inf-sup条件](@entry_id:746626)**（或称Ladyzhenskaya-Babuška-Brezzi (LBB) 条件）保证。对于耦合项 $b_h(v_h, \mu_h) = \int_{\Gamma} \gamma v_h \mu_h ds$，需要保证存在一个与网格尺寸无关的常数 $c > 0$，使得：
$$ \inf_{\mu_h \in Y_h \setminus \{0\}} \sup_{v_h \in M_h \setminus \{0\}} \frac{\int_{\Gamma} \gamma v_h \mu_h ds}{\|v_h\|_{H^{1/2}(\Gamma)} \|\mu_h\|_{H^{-1/2}(\Gamma)}} \ge c $$
其中 $M_h$ 和 $Y_h$ 分别是狄利克雷和诺伊曼数据的离散边界空间。如果简单地为这两个空间选择标准函数（例如，在同一套边界网格上的连续分片线性和分片常数），这个条件可能不被满足，导致数值解出现[伪振荡](@entry_id:152404)。

一个有效的稳定化策略是为诺伊曼数据空间 $Y_h$ 选择一个特殊的**对偶基底 (biorthogonal basis)**。具体而言，如果 $M_h$ 的基底是 $\{\varphi_i\}$，我们构造 $Y_h$ 的基底 $\{\psi_j\}$，使其满足 $L^2$ 对偶条件 $\int_{\Gamma} \varphi_i \psi_j ds = \delta_{ij}$。通过这种构造，离散的inf-sup常数可以被证明等于1，从而确保了与网格无关的稳定性 [@problem_id:2551145]。

### 离散化与代数系统

最后，通过[Galerkin方法](@entry_id:260906)将[变分形式](@entry_id:166033)转化为线性[代数方程](@entry_id:272665)组。我们将未知场 $u$ 和边界未知量（如 $\lambda$ 或 $\phi$）用有限元和边界元[基函数](@entry_id:170178)展开。

最终得到的线性系统通常具有一个显著的**[分块矩阵](@entry_id:148435)结构**。例如，对于一个三场耦合（内部解 $U$，边界迹 $\Psi$，边界通量 $\Phi$），其[系统矩阵](@entry_id:172230)可能呈现如下形式 [@problem_id:2551173]：
$$
\begin{bmatrix}
\mathbf{K}_{\text{FEM}} & \mathbf{C}^\top & \mathbf{0} \\
\mathbf{C} & \mathbf{W}_{\text{BEM}} & \mathbf{M}_{\text{BEM}} \\
\mathbf{0} & \mathbf{M}_{\text{BEM}}^\top & \mathbf{V}_{\text{BEM}}
\end{bmatrix}
\begin{bmatrix}
U \\ \Psi \\ \Phi
\end{bmatrix}
=
\begin{bmatrix}
F_1 \\ F_2 \\ F_3
\end{bmatrix}
$$

这个结构的关键特征是不同块的**稀疏性 (sparsity)** 和**稠密性 (density)**：
- **稀疏块**：源于有限元法 (FEM) 的矩阵块，如[刚度矩阵](@entry_id:178659) $\mathbf{K}_{\text{FEM}}$ 和FEM-BEM[耦合矩阵](@entry_id:191757) $\mathbf{C}$，通常是稀疏的。这是因为FEM的[基函数](@entry_id:170178)具有局部支集，一个[基函数](@entry_id:170178)只与邻近的少数几个[基函数](@entry_id:170178)有相互作用。
- **稠密块**：源于[边界元法 (BEM)](@entry_id:746941) 的矩阵块，如 $\mathbf{V}_{\text{BEM}}$, $\mathbf{W}_{\text{BEM}}$, $\mathbf{M}_{\text{BEM}}$（来自 $K$ 和 $K'$），是完全稠密的。这是因为[基本解](@entry_id:184782) $G(\boldsymbol{x},\boldsymbol{y})$ 是一个非局部核，边界上任意一点的未知量都会影响到边界上所有其他点，导致每个边界[基函数](@entry_id:170178)都与所有其他边界[基函数](@entry_id:170178)相互作用。

这种“稀疏-稠密”的混合结构对[线性系统](@entry_id:147850)的求解策略提出了特殊要求。[直接求解器](@entry_id:152789)（如[LU分解](@entry_id:144767)）的计算成本可能非常高，通常需要借助[迭代求解器](@entry_id:136910)，并结合[快速多极子方法](@entry_id:140932) (Fast Multipole Method, FMM) 或[分层矩阵](@entry_id:750110) (Hierarchical Matrices, $\mathcal{H}$-matrices) 等技术来加速稠密BEM矩阵与向量的乘法运算，以降低计算复杂度和内存需求。