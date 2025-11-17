## 引言
在现代[计算力学](@entry_id:174464)中，精确施加边界条件是获得可靠数值解的基石。然而，对于[非贴体网格](@entry_id:168901)方法（如[CutFEM](@entry_id:163318)）或非连续[伽辽金法](@entry_id:749698)等前沿技术，传统的强施加方法面临着根本性的挑战，甚至可能导致数值不稳定。为了克服这些局限性，学术界发展了多种弱式施加边界条件的技术，其中 Nitsche 方法因其理论的完备性、数学的优雅性以及应用的灵活性而备受瞩目。它在不引入额外自由度的情况下，通过修改[变分形式](@entry_id:166033)，将本质边界条件转化为自然边界条件，为解决复杂几何和多物理场问题提供了强大的框架。

本文旨在系统性地介绍 Nitsche 方法。在接下来的内容中，我们将首先在“原理与机制”一章中深入探讨该方法的数学构造、稳定机理及其与罚函数法和[拉格朗日乘子法](@entry_id:176596)的理论对比。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示 Nitsche 方法如何应用于[接触力学](@entry_id:177379)、[多物理场耦合](@entry_id:171389)和数据驱动建模等复杂场景。最后，通过“动手实践”部分提供的一系列练习，读者将有机会将理论知识转化为实际的计算技能。通过本课程的学习，读者将全面掌握这一先进数值工具的核心思想与应用技巧。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨弱边界条件施加的数学原理和数值机制。我们将重点关注 Nitsche 方法，从其基本动机和理论构建出发，系统地推导其在标量问题和矢量弹性问题中的具体形式。此外，本章还将分析该方法的关键组成部分，如稳定项的作用，并将其与经典的罚函数法和拉格朗日乘子法进行对比，以阐明其在计算力学中的独特优势和理论特性。

### 动机：强施加法的局限性

在经典的有限元方法中，狄利克雷（Dirichlet）边界条件，也称为本质边界条件，通常通过“强”施加的方式来处理。这种方法要求试探解和检验函数所在的离散[函数空间](@entry_id:143478)本身就满足边界条件。具体而言，[检验函数](@entry_id:166589)在狄利克雷边界上为零，而试探解则通过插值或约束节点值等方式，精确地匹配给定的边界位移。这种强施加法在网格与物理域边界完全贴合（body-fitted meshes）且采用连续形函数的标准有限元场景中，既直观又高效。

然而，在许多现代计算力学的前沿应用中，强施加法遇到了根本性的挑战。当离散函数空间不再满足边界整合性（boundary conformity）时，强加边界条件可能会变得不适定（ill-posed），甚至是不可能的。这种情况主要出现在以下两种重要场景中：

1.  **非连续伽辽金（Discontinuous Galerkin, DG）方法**：在此类方法中，所用的离散[函数空间](@entry_id:143478) $V_h$ 由在单元边界上可以不连续的函数构成。因此，这些函数不属于传统的[索博列夫空间](@entry_id:141995) $H^1(\Omega)$，其在边界 $\Gamma_D$ 上的迹（trace）在标准意义下是未定义的。这意味着，约束集合 $\{ \boldsymbol{v}_h \in V_h : \boldsymbol{v}_h|_{\Gamma_D} = \boldsymbol{g} \}$ 本身就是不明确的，无法直接构建。

2.  **非贴体或浸入式边界方法（Unfitted/Immersed Methods）**：这类方法，如[切割有限元法](@entry_id:163318)（[CutFEM](@entry_id:163318)），允许[计算网格](@entry_id:168560)独立于几何体的精确边界。物理边界可以任意切割单元。在这种情况下，通常不存在恰好位于物理边界上的“边界节点”。试图通过约束邻近节点的自由度来强加边界条件是一种权宜之计，但这会导致严重的数值问题。特别是，当边界切割单元只留下一小部分在计算域内时（即“小切割单元问题”），强行约束相[关节点](@entry_id:637448)的位移会过度[约束系统](@entry_id:164587)，或导致刚度[矩阵的条件数](@entry_id:150947)随着切割单元尺寸的减小而急剧恶化，从而破坏数值稳定性 [@problem_id:3584360]。

这些局限性促使我们必须寻求一种替代方案，即在变分[形式的积分](@entry_id:158607)意义上“弱”地施加边界条件。Nitsche 方法正是在这一背景下应运而生的一种强大而灵活的工具。它通过修改[变分方程](@entry_id:635018)，引入与边界条件相关的积分项，从而在不直接约束[函数空间](@entry_id:143478)的前提下保证解的收敛性，同时避免了引入额外的[拉格朗日乘子](@entry_id:142696)自由度。

### Nitsche 方法：从基本原理构建

为了清晰地阐述 Nitsche 方法的构建原理，我们首先以一个简单的标量泊松（Poisson）问题作为模型 [@problem_id:3584385]。考虑在有界域 $\Omega \subset \mathbb{R}^d$ 上的[扩散](@entry_id:141445)问题：
$$
-\nabla\cdot(\kappa\nabla u) = f \quad \text{in } \Omega, \qquad u = g \quad \text{on } \Gamma_D
$$
其中 $\kappa$ 是[扩散](@entry_id:141445)系数，$\Gamma_D$ 是狄利克雷边界。

我们从其标准弱形式的推导过程出发。将控制方程与[检验函数](@entry_id:166589) $v \in H^1(\Omega)$ 相乘并在域 $\Omega$ 上积分，通过[分部积分](@entry_id:136350)（即[散度定理](@entry_id:143110)）得到：
$$
\int_{\Omega} \kappa\nabla u \cdot \nabla v \, \mathrm{d}\Omega - \int_{\partial\Omega} (\kappa\nabla u \cdot \boldsymbol{n}) v \, \mathrm{d}S = \int_{\Omega} f v \, \mathrm{d}\Omega
$$
其中 $\boldsymbol{n}$ 是边界上的单位外法向。在强施加法中，我们要求[检验函数](@entry_id:166589) $v$ 在 $\Gamma_D$ 上为零，从而消除了边界积分项中未知的法向通量（flux）$\kappa\nabla u \cdot \boldsymbol{n}$。

在弱施加法中，我们不再对[试探函数](@entry_id:756165)和[检验函数](@entry_id:166589)空间施加边界约束，即 $u_h, v_h \in V_h \subset H^1(\Omega)$。因此，上述恒等式中的边界积分项必须被处理。Nitsche 方法的核心思想是围绕这一边界积分项，通过添加和减去特定项来构造一个新的、自洽的[变分形式](@entry_id:166033)。这一过程包含三个关键步骤。

#### 一致性、对称性与变体

Nitsche 方法的构造可以通过一个由参数 $\theta$ 控制的统一形式来表达 [@problem_id:3584427]。完整的[双线性形式](@entry_id:746794) $a_h(u,v)$ 由以下几部分组成：

1.  **标准体积项**：源自原偏[微分算子](@entry_id:140145)的体积积分，即 $\int_{\Omega} \kappa\nabla u \cdot \nabla v \, \mathrm{d}\Omega$。

2.  **一致性项（Consistency Term）**：这是从[分部积分](@entry_id:136350)中直接产生的边界项 $-\int_{\Gamma_D} (\kappa\nabla u \cdot \boldsymbol{n}) v \, \mathrm{d}S$。包含此项是为了确保当我们将精确解 $u$ 代入离散方程时，方程能够得到满足（即方法是一致的）。

3.  **对称性/非对称性项（Symmetry/Nonsymmetry Term）**：为了控制[双线性形式](@entry_id:746794)的对称性，我们引入一个额外的项 $-\theta \int_{\Gamma_D} (\kappa\nabla v \cdot \boldsymbol{n}) u \, \mathrm{d}S$。参数 $\theta$ 的取值决定了方法的变体：
    *   **对称 Nitsche 法（Symmetric Nitsche Method）**：当 $\theta = +1$ 时，[双线性形式](@entry_id:746794)关于其两个变量是对称的。这对于自伴随的原始问题（如泊松方程和线弹性问题）来说是一种自然的选择，因为它能保持离散系统的对称性。
    *   **非对称 Nitsche 法（Nonsymmetric Nitsche Method）**：当 $\theta = -1$ 时，双线性形式变为非对称。有时这种选择在特定问题（如[对流](@entry_id:141806)占优问题）中可能具有优势。
    
4.  **稳定项（Stabilization Term）**：仅有上述项还不足以保证[变分问题](@entry_id:756445)的[适定性](@entry_id:148590)。我们需要加入一个惩罚项 $+\int_{\Gamma_D} \gamma u v \, \mathrm{d}S$ 来确保最终的双线性形式是强制性的（coercive）。$\gamma$ 是一个正的稳定参数（或称罚参数）。

综合以上各项，Nitsche 方法的双线性形式 $a_h(u_h, v_h)$ 可以统一写为：
$$
a_h(u_h, v_h) = \int_{\Omega} \kappa\nabla u_h \cdot \nabla v_h \, \mathrm{d}\Omega - \int_{\Gamma_D} (\kappa\nabla u_h \cdot \boldsymbol{n}) v_h \, \mathrm{d}S - \theta \int_{\Gamma_D} (\kappa\nabla v_h \cdot \boldsymbol{n}) u_h \, \mathrm{d}S + \int_{\Gamma_D} \gamma u_h v_h \, \mathrm{d}S
$$
相应的[线性形式](@entry_id:276136) $l_h(v_h)$ 也包含来自边界数据 $g$ 的贡献。对于 **对称 Nitsche 法**（$\theta=+1$）和 **非对称 Nitsche 法**（$\theta=-1$），其双线性形式分别为 [@problem_id:3584427]：
$$
a_h^{\text{sym}}(u_h,v_h) = \int_{\Omega} \kappa \nabla u_h \cdot \nabla v_h \,\mathrm{d}\Omega - \int_{\Gamma_D} (\kappa \partial_n u_h) v_h \,\mathrm{d}S - \int_{\Gamma_D} (\kappa \partial_n v_h) u_h \,\mathrm{d}S + \int_{\Gamma_D} \gamma u_h v_h \,\mathrm{d}S
$$
$$
a_h^{\text{nonsym}}(u_h,v_h) = \int_{\Omega} \kappa \nabla u_h \cdot \nabla v_h \,\mathrm{d}\Omega - \int_{\Gamma_D} (\kappa \partial_n u_h) v_h \,\mathrm{d}S + \int_{\Gamma_D} (\kappa \partial_n v_h) u_h \,\mathrm{d}S + \int_{\Gamma_D} \gamma u_h v_h \,\mathrm{d}S
$$
其中 $\partial_n u = \nabla u \cdot \boldsymbol{n}$。这种构造与强施加法有本质区别：Nitsche 方法将[狄利克雷条件](@entry_id:137096)视为自然边界条件，通过[变分形式](@entry_id:166033)自身来施加，而不是通过约束函数空间。

### 稳定参数：保证强制性的关键

Nitsche 方法的成功实现依赖于对稳定参数 $\gamma$ 的恰当选择。这个参数必须足够大，以抵消由一致性和对称性项引入的“负”能量，从而保证整个[双线性形式](@entry_id:746794)的强制性（coercivity），即存在常数 $\beta > 0$ 使得 $a_h(v_h, v_h) \ge \beta \|v_h\|_{E}^2$（其中 $\|\cdot\|_{E}$ 是一个合适的能量范数）。

#### 参数尺度的推导

我们可以通过数值分析中的标准工具来推导 $\gamma$ 所需的尺度 [@problem_id:3584422]。考虑对称 Nitsche 法的二次型 $a_h(v_h, v_h)$：
$$
a_h(v_h, v_h) = \int_{\Omega} \kappa |\nabla v_h|^2 \, \mathrm{d}\Omega - 2\int_{\Gamma_D} (\kappa\nabla v_h \cdot \boldsymbol{n}) v_h \, \mathrm{d}S + \int_{\Gamma_D} \gamma |v_h|^2 \, \mathrm{d}S
$$
为了约束中间的边界项，我们使用柯西-[施瓦茨不等式](@entry_id:202153)和带参数的[杨氏不等式](@entry_id:158732)：
$$
\left| 2\int_{\Gamma_D} (\kappa\nabla v_h \cdot \boldsymbol{n}) v_h \, \mathrm{d}S \right| \le 2 \|\kappa\nabla v_h \cdot \boldsymbol{n}\|_{L^2(\Gamma_D)} \|v_h\|_{L^2(\Gamma_D)} \le \delta \|\kappa\nabla v_h \cdot \boldsymbol{n}\|_{L^2(\Gamma_D)}^2 + \frac{1}{\delta} \|v_h\|_{L^2(\Gamma_D)}^2
$$
这里的挑战在于边界上的[法向导数](@entry_id:169511)范数 $\|\nabla v_h \cdot \boldsymbol{n}\|_{L^2(\Gamma_D)}$ 无法由[体积分](@entry_id:171119)内的能量范数 $\|\nabla v_h\|_{L^2(\Omega)}$ 控制。然而，在离散的有限元空间 $V_h$ 中，我们可以利用一个关键的 **[逆不等式](@entry_id:750800)（inverse inequality）**。对于网格尺寸为 $h$ 的单元 $K$，其边界上的[法向导数](@entry_id:169511)可以被单元内的梯度所约束：
$$
\|\nabla v_h \cdot \boldsymbol{n}\|_{L^2(\partial K)}^2 \le C_{\text{inv}} h^{-1} \|\nabla v_h\|_{L^2(K)}^2
$$
将此关系推广到整个边界 $\Gamma_D$ 并代入之前的估计，我们发现为了使二次型 $a_h(v_h, v_h)$ 保持正定，稳定参数 $\gamma$ 必须能够“压制”与 $\kappa/h$ 成比例的项。因此，$\gamma$ 的正确尺度必须是：
$$
\gamma = c \frac{\kappa}{h}
$$
其中 $c$ 是一个足够大但与网格尺寸 $h$ 和材料参数 $\kappa$ 无关的无量纲常数。这个尺度关系是 Nitsche 方法稳定性的核心。它直观地表明，随着网格加密（$h \to 0$），罚的力度需要相应增强，以控制更精细尺度上的[函数振荡](@entry_id:160838)。

#### 一维实例分析

这个抽象的推导可以通过一个简单的一维问题变得非常具体 [@problem_id:3584385]。考虑在长度为 $h$ 的单元 $[0, h]$ 上，使用线性形函数，并在 $x=0$ 处施加狄利克雷边界条件。一个定义在该单元上的线性函数 $v(x)$ 可由其节点值 $v_0 = v(0)$ 和 $v_h = v(h)$ 唯一确定。其导数为常数 $v'(x) = (v_h - v_0)/h$。在 $x=0$ 处，外法向为 $n=-1$，因此[法向导数](@entry_id:169511)为 $\nabla v \cdot n = v'(0) \cdot (-1) = -(v_h-v_0)/h$。

将这些代入对称 Nitsche 法的二次型 $a_e(v,v)$，并设 $\gamma = \beta \kappa/h$（其中 $\beta$ 是无量纲罚因子），经过化简可得：
$$
a_e(v,v) = \frac{\kappa}{h} \left[ v_h^2 + (\beta - 1)v_0^2 \right]
$$
为了使该二次型对任意非零函数 $v$（即 $(v_0, v_h) \ne (0,0)$）恒为正，矩阵 $\begin{pmatrix} \beta-1  0 \\ 0  1 \end{pmatrix}$ 必须是正定的。这直接要求 $\beta - 1 > 0$，即 $\beta > 1$。这个清晰的结果表明，为了保证单元级别的稳定性，无量纲罚因子必须大于一个临界值。在实践中，通常会选择一个远大于临界值的“安全”因子（例如 $\beta=10$ 或更高）来确保全局稳定性。

### Nitsche 方法在[线性弹性](@entry_id:166983)问题中的应用

将 Nitsche 方法从标量问题推广到矢量值的线弹性问题是直接的，但需要关注其张量和矢量特性 [@problem_id:3584406]。对于[位移场](@entry_id:141476) $\boldsymbol{u}$，其对称 Nitsche [双线性形式](@entry_id:746794)为：
$$
a_h(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}\Omega - \int_{\Gamma_D} (\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n}) \cdot \boldsymbol{v} \, \mathrm{d}S - \int_{\Gamma_D} (\boldsymbol{\sigma}(\boldsymbol{v})\boldsymbol{n}) \cdot \boldsymbol{u} \, \mathrm{d}S + \int_{\Gamma_D} (\boldsymbol{\gamma} \boldsymbol{u}) \cdot \boldsymbol{v} \, \mathrm{d}S
$$
这里，$\boldsymbol{\sigma}(\cdot)$ 是应力张量，$\boldsymbol{\varepsilon}(\cdot)$ 是[应变张量](@entry_id:193332)，稳定参数 $\boldsymbol{\gamma}$ 现在可以是一个[二阶张量](@entry_id:199780)。对称性项的结构 $-\int ((\boldsymbol{\sigma}(\boldsymbol{u})\boldsymbol{n}) \cdot \boldsymbol{v} + (\boldsymbol{\sigma}(\boldsymbol{v})\boldsymbol{n}) \cdot \boldsymbol{u}) \mathrm{d}S$ 的对称性源于应力张量的次对称性（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^\top$）以及欧几里得[内积](@entry_id:158127)的交换律。

#### 各向异性罚参数

对于弹性问题，一个更精细的做法是设计一个与材料方向刚度相关的各向异性稳定张量 $\boldsymbol{\gamma}$ [@problem_id:3584435]。在边界上，我们可以将位移和牵[引力](@entry_id:175476)分解为[法向和切向分量](@entry_id:166204)。利用[投影算子](@entry_id:154142) $\boldsymbol{P}_n = \boldsymbol{n} \otimes \boldsymbol{n}$ 和 $\boldsymbol{P}_t = \boldsymbol{I} - \boldsymbol{n} \otimes \boldsymbol{n}$，稳定张量可以写成[对角形式](@entry_id:264850)：
$$
\boldsymbol{\gamma} = \gamma_n \boldsymbol{P}_n + \gamma_t \boldsymbol{P}_t
$$
物理上，法向罚参数 $\gamma_n$ 应与材料抵抗法向变形的刚度成正比，而切向罚参数 $\gamma_t$ 应与抵抗[剪切变形](@entry_id:170920)的刚度成正比。对于[各向同性线弹性](@entry_id:185899)材料，其拉梅参数为 $\lambda$ 和 $\mu$：

*   **法向刚度** 对应于[平面应变](@entry_id:167046)或[平面应力条件](@entry_id:168184)下的纵波模量，即 $\lambda + 2\mu$。它描述了在没有[横向应变](@entry_id:157965)情况下的单轴刚度。
*   **切向刚度** 对应于[剪切模量](@entry_id:167228) $\mu$。

因此，一个物理上合理的、各向异性的罚参数选择是：
$$
\gamma_n = c \frac{\lambda + 2\mu}{h}, \qquad \gamma_t = c \frac{\mu}{h}
$$
其中 $c$ 是一个无量纲安全因子。例如，对于杨氏模量 $E=100\,\text{GPa}$、[泊松比](@entry_id:158876) $\nu=0.25$ 的材料（此时 $\lambda = \mu = 40\,\text{GPa}$），在网格尺寸 $h=0.05\,\text{m}$ 和安全因子 $c=10$ 的条件下，我们可以计算出罚参数为 $\gamma_n = 2.4 \times 10^4\,\text{GPa/m}$ 和 $\gamma_t = 8.0 \times 10^3\,\text{GPa/m}$ [@problem_id:3584435]。这种精细化的选择可以改善方法的性能，特别是在处理具有复杂接触和界面行为的问题时。

### 理论性质与方法比较

理解 Nitsche 方法的完整图景，需要将其与其他弱施加方法进行比较，并考察其关键的理论性质。

#### 与罚函数法的对比

经典的**[罚函数法](@entry_id:636090)**（Penalty Method）通过在[变分形式](@entry_id:166033)中仅添加一个罚项来弱施加边界条件：
$$
a_h(u_h, v_h) = \int_{\Omega} \nabla u_h \cdot \nabla v_h \, \mathrm{d}\Omega + \gamma \int_{\Gamma_D} u_h v_h \, \mathrm{d}S
$$
Nitsche 方法与[罚函数法](@entry_id:636090)的一个根本区别在于 **一致性**（consistency）[@problem_id:3584395]。
*   **Nitsche 方法是“一致的”**：由于其构造中包含了从[分部积分](@entry_id:136350)导出的所有项，精确解 $u$ 可以完美地满足离散方程，即对任意有限的 $\gamma > 0$，其变分残差为零。
*   **[罚函数法](@entry_id:636090)是“不一致的”**：当将精确解 $u$ 代入罚函数法的[变分方程](@entry_id:635018)时，会留下一个非零的残差项 $\int_{\Gamma_D} (\partial_n u) v_h \, \mathrm{d}S$。这个“变分犯罪”（variational crime）意味着方法本身引入了一个[建模误差](@entry_id:167549)，该误差仅在罚参数 $\gamma \to \infty$ 时才趋于零。

这种不一致性对[误差估计](@entry_id:141578)有重要影响。对称 Nitsche 方法是 **伴随一致的**（adjoint-consistent），这意味着它满足标准的[伽辽金正交性](@entry_id:173536)，从而可以通过标准的对偶性论证（Aubin-Nitsche trick）得到最优的 $L^2$ [范数收敛](@entry_id:261322)阶。而[罚函数法](@entry_id:636090)由于其伴随不一致性，其 $L^2$ 误差估计会退化，除非采取特殊的技巧或对罚参数 $\gamma$ 的增长有特定要求 [@problem_id:3584395]。

#### 与拉格朗日乘子法的对比

**[拉格朗日乘子法](@entry_id:176596)**（Lagrange Multiplier Method）是另一种经典的弱施加方法。它引入一个新的未知场 $\boldsymbol{\lambda}$（[拉格朗日乘子](@entry_id:142696)），其物理意义是边界上的[反作用](@entry_id:203910)力。这导致了一个[鞍点](@entry_id:142576)（saddle-point）问题，求解的是位移-乘子对 $(\boldsymbol{u}, \boldsymbol{\lambda})$。
Nitsche 方法与[拉格朗日乘子法](@entry_id:176596)的主要区别在于 [@problem_id:3584386]：

*   **系统结构**：拉格朗日乘子法产生一个对称但 **不定** 的[鞍点系统](@entry_id:754480)。而（对称）Nitsche 方法产生一个对称 **正定** 的系统（只要 $\gamma$ 足够大），仅涉及原始的位移自由度。这在代数求解器层面是一个显著优势。
*   **稳定性条件**：拉格朗日乘子法的稳定性依赖于位移和乘子的离散[函数空间](@entry_id:143478)对必须满足 **Ladyzhenskaya–Babuška–Brezzi (LBB) 或 [inf-sup 条件](@entry_id:174538)**。这个条件对函数空间的选择施加了严格的限制，例如，不能对位移和乘子使用相同阶次的标准连续形函数。相比之下，Nitsche 方法通过稳定项来保证稳定性，因此它**不要求 LBB 条件**，可以与任何标准的有限元空间对结合使用，提供了更大的灵活性。

#### 收敛阶：对称与非对称 Nitsche 法

Nitsche 方法变体的选择对其收敛性质有微妙但重要的影响，这主要源于**伴随一致性**的概念 [@problem_id:3584378]。对于光滑解（例如，$\boldsymbol{u} \in H^{p+1}$，其中 $p$ 是形函数的多项式次数），我们期望在 $L^2$ 范数下达到最优的[收敛阶](@entry_id:146394) $\mathcal{O}(h^{p+1})$。

*   **对称 Nitsche 法**（$\theta=1$）是伴随一致的。这意味着它在对偶问题中的表现与原始问题一致，使得标准的对偶性论证能够顺利进行，从而证明其可以达到最优的 $\mathcal{O}(h^{p+1})$ 收敛阶。

*   **非对称 Nitsche 法**（$\theta=-1$）是伴随不一致的。这种不对称性在对偶性论证中引入了一个额外的、无法被完全抵消的边界项。这个项量化了伴随不一致性的大小 [@problem_id:3584377]。在一个一维模型问题中，这个不一致性项可以被精确地推导为 $J(z;e) = 2z'(0)e(0)$，其中 $z$ 是对偶问题的解，$e$ 是误差。这个项的存在通常会导致 $L^2$ 收敛阶的“污染”，使其从最优的 $\mathcal{O}(h^{p+1})$ 退化为次优的 $\mathcal{O}(h^{p+1/2})$ [@problem_id:3584378]。

因此，对于追求高精度解的自伴随问题，对称 Nitsche 方法通常是首选，因为它能保证最优的收敛性。

总结而言，Nitsche 方法为在复杂场景下施加[狄利克雷边界条件](@entry_id:173524)提供了一个坚实、灵活且理论完备的框架。它通过在[变分形式](@entry_id:166033)中精心构造一致性、对称性和稳定项，成功地将本质边界条件转化为自然边界条件处理，从而绕过了强施加法的内在局限性。