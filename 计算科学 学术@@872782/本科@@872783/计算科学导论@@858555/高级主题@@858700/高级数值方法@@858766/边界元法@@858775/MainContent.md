## 引言
在计算科学与工程领域，[偏微分方程](@entry_id:141332)（PDEs）是描述从热传导、[流体流动](@entry_id:201019)到[电磁场](@entry_id:265881)和结构应力等各种物理现象的通用语言。然而，直接求解这些方程往往极具挑战性。边界元法（Boundary Element Method, BEM）作为一种强大而优雅的数值技术应运而生，它为解决一大类PDE问题提供了独特的视角。与[有限元法](@entry_id:749389)（FEM）等对整个物理域进行[网格划分](@entry_id:269463)的“域方法”不同，BEM的核心思想是将问题的维度降低一维，仅在问题的边界上进行离散和求解。这种降维特性不仅显著减少了计算自由度，也使其在处理具有大体积表面积比或无限域的特定问题时，拥有无与伦比的效率和精度。

本文旨在为读者全面解析边界元法。我们将从其深刻的数学根源出发，逐步揭示它如何将一个复杂的域问题转化为一个更易于处理的边界问题。通过三章内容的学习，读者将能够：

*   在“原理与机制”一章中，深入理解BEM的数学基石，包括[格林公式](@entry_id:173118)、[基本解](@entry_id:184782)、[边界积分方程](@entry_id:746942)的推导以及离散化为[线性系统](@entry_id:147850)的全过程。
*   在“应用与跨学科连接”一章中，探索BEM在[静电学](@entry_id:140489)、[固体力学](@entry_id:164042)、[声学](@entry_id:265335)、[生物物理学](@entry_id:154938)等多个前沿领域的实际应用，领略其解决真实世界问题的强大能力。
*   在“动手实践”部分，通过具体的编程练习，将理论知识转化为实际的计算技能。

现在，让我们从边界元法的核心——其精妙的数学原理与机制——开始我们的探索之旅。

## 原理与机制

边界元法（Boundary Element Method, BEM）的核心思想是通过数学变换，将一个定义在物理域（domain）上的[偏微分方程](@entry_id:141332)（Partial Differential Equation, PDE）问题，转化为一个只涉及该域的边界（boundary）的积分方程。这种[降维](@entry_id:142982)特性是边界元法最引人注目之处。本章将深入探讨支撑这一方法的数学原理与核心机制，从[格林公式](@entry_id:173118)的基础出发，系统阐述[边界积分方程](@entry_id:746942)的推导、离散化过程，并分析其计算特性与面临的挑战。

### 基本原理：从[格林恒等式](@entry_id:176369)到边界积分表示

边界元法的理论基石是**[格林第二恒等式](@entry_id:169499)（Green's second identity）**。对于一个定义在域 $\Omega$ 上且具有光滑边界 $\Gamma$ 的两个足够光滑的标量场 $u$ 和 $v$，该恒等式建立了[体积分](@entry_id:171119)与面积分（或线积分）之间的关系：
$$
\int_{\Omega} (u \Delta v - v \Delta u) \, d\Omega = \int_{\Gamma} (u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n}) \, d\Gamma
$$
其中，$\Delta$ 是[拉普拉斯算子](@entry_id:146319)，$\frac{\partial}{\partial n}$ 表示沿边界外法线方向的[方向导数](@entry_id:189133)。[格林恒等式](@entry_id:176369)的美妙之处在于，它将与域内PDE算子（如 $\Delta u$）相关的信息，与边界上的函数值 ($u$) 及其[法向导数](@entry_id:169511) ($\frac{\partial u}{\partial n}$) 联系起来。

为了利用此恒等式求解一个特定的PDE（例如，拉普拉斯方程 $\Delta u = 0$），我们需要一个特殊的辅助函数 $v$。这个函数就是**[基本解](@entry_id:184782)（fundamental solution）**，通常记为 $G(\boldsymbol{x}, \boldsymbol{\xi})$。[基本解](@entry_id:184782)是对应偏微分算子在自由空间中由一个[点源](@entry_id:196698)所激发的响应，其定义满足如下[分布](@entry_id:182848)意义下的方程：
$$
\Delta_{\boldsymbol{x}} G(\boldsymbol{x}, \boldsymbol{\xi}) = -\delta(\boldsymbol{x} - \boldsymbol{\xi})
$$
其中，$\boldsymbol{x}$ 是场点（field point），$\boldsymbol{\xi}$ 是源点（source point），$\delta(\cdot)$ 是狄拉克-[德尔塔函数](@entry_id:273429)。基本解可以被视为在源点 $\boldsymbol{\xi}$ 处放置一个单位强度的[点源](@entry_id:196698)所产生的场。

现在，我们将 $u$ 视为待求的谐[波函数](@entry_id:147440)（即满足 $\Delta u = 0$），并令 $v = G(\boldsymbol{x}, \boldsymbol{\xi})$。将它们代入[格林第二恒等式](@entry_id:169499)，并利用[德尔塔函数](@entry_id:273429)的[筛选性质](@entry_id:265662)，我们可以得到对于域内任意一点 $\boldsymbol{\xi} \in \Omega$ 的解的积分表达式：
$$
u(\boldsymbol{\xi}) = \int_{\Gamma} \left( G(\boldsymbol{x}, \boldsymbol{\xi}) \frac{\partial u(\boldsymbol{x})}{\partial n} - u(\boldsymbol{x}) \frac{\partial G(\boldsymbol{x}, \boldsymbol{\xi})}{\partial n} \right) d\Gamma(\boldsymbol{x})
$$
这个公式是边界元法的核心，它揭示了一个深刻的原理：对于某些类型的PDE（如拉普拉斯方程），域内任意一点的解完全由其边界上的值（狄利克雷数据 $u$）和[法向导数](@entry_id:169511)值（诺伊曼数据 $q = \frac{\partial u}{\partial n}$）所决定。这不仅为BEM提供了理论依据，也从一个侧面证明了[边值问题](@entry_id:193901)的[解的唯一性](@entry_id:143619)。例如，对于[狄利克雷问题](@entry_id:274408)，如果两个解 $u_1$ 和 $u_2$ 在边界上具有相同的值，那么它们的差 $w = u_1 - u_2$ 在边界上为零。通过在[格林第一恒等式](@entry_id:170345)中令 $v=w$ 可以证明 $w$ 在整个域内恒为零，从而确保了[解的唯一性](@entry_id:143619)。[@problem_id:3103684]

为了更具体地理解这一过程，我们可以考察最简单的一维拉普拉斯方程 $\frac{d^2u}{dx^2}=0$。其一维[基本解](@entry_id:184782)满足 $\frac{\partial^2 G}{\partial x^2} = \delta(x-\xi)$，可以求得为 $G(x,\xi) = \frac{1}{2}|x-\xi|$。对于定义在区间 $(0,L)$ 上的问题，其边界是两个点 $x=0$ 和 $x=L$。应用上述积分表示（此时积分为在两个端点的求和），可以推导出，对于任意 $x \in (0,L)$，解 $u(x)$ 都可以表示为边界值 $U_0=u(0)$ 和 $U_L=u(L)$ 的[线性组合](@entry_id:154743)，最终得到熟悉的线性插值解 $u(x) = U_0(1 - \frac{x}{L}) + U_L\frac{x}{L}$。[@problem_id:2377276] 这个简单的例子完美地展示了BEM如何将一个[微分方程](@entry_id:264184)问题转化为一个仅依赖于边界值的代数问题。

### [边界积分方程](@entry_id:746942)：将方程约束到边界上

上一节得到的积分表达式虽然功能强大，但它给出的只是域[内点](@entry_id:270386) $\boldsymbol{\xi}$ 的解，前提是边界上的 $u$ 和 $q$ 都已知。在实际问题中，通常只有一半的边界信息是已知的（例如，在[狄利克雷问题](@entry_id:274408)中已知 $u$，但 $q$ 未知）。为了求解未知的边界量，我们需要一个只在边界 $\Gamma$ 上建立约束的方程，这就是**[边界积分方程](@entry_id:746942)（Boundary Integral Equation, BIE）**。

BIE是通过一个极限过程得到的：将积分表达式中的观察点 $\boldsymbol{\xi}$ 从域内移动到边界上的一点 $\boldsymbol{\xi}_0 \in \Gamma$。当 $\boldsymbol{\xi}$ 趋近于 $\boldsymbol{\xi}_0$ 时，积分核 $G(\boldsymbol{x}, \boldsymbol{\xi})$ 和 $\frac{\partial G(\boldsymbol{x}, \boldsymbol{\xi})}{\partial n}$ 会在 $\boldsymbol{x} \to \boldsymbol{\xi}_0$ 时表现出奇异性，使得积分需要特殊处理。

这一极限过程的分析，通常借助所谓的**层势理论（layer potential theory）**。由[基本解](@entry_id:184782)构成的积分可以被看作是定义在边界上的密度函数（$\sigma$ 或 $\mu$）所产生的势场，例如：
*   **单层势（Single-Layer Potential）**: $(S\sigma)(\boldsymbol{\xi}) = \int_{\Gamma} G(\boldsymbol{x}, \boldsymbol{\xi}) \sigma(\boldsymbol{x}) d\Gamma(\boldsymbol{x})$
*   **双层势（Double-Layer Potential）**: $(D\mu)(\boldsymbol{\xi}) = \int_{\Gamma} \frac{\partial G(\boldsymbol{x}, \boldsymbol{\xi})}{\partial n} \mu(\boldsymbol{x}) d\Gamma(\boldsymbol{x})$

当观察点 $\boldsymbol{\xi}$ 穿过边界 $\Gamma$ 时，这些[势场](@entry_id:143025)会表现出特定的**跳跃关系（jump relations）**。单层势是连续穿过边界的，但其[法向导数](@entry_id:169511)会发生跳跃。而双层势本身在穿过边界时就会发生跳跃。具体来说，当点 $\boldsymbol{\xi}$ 从域外（+) 和域内（-）趋近于[边界点](@entry_id:176493) $\boldsymbol{\xi}_0$ 时，双层势的极限满足：
$$
\lim_{\boldsymbol{\xi} \to \boldsymbol{\xi}_0^{\pm}} (D\mu)(\boldsymbol{\xi}) = (D_0\mu)(\boldsymbol{\xi}_0) \mp \frac{1}{2}\mu(\boldsymbol{\xi}_0)
$$
其中 $(D_0\mu)(\boldsymbol{\xi}_0)$ 是在 $\boldsymbol{\xi}_0$ 处的[柯西主值](@entry_id:192761)积分。从域外到域内的跳跃幅度恰好是该点的密度值 $\mu(\boldsymbol{\xi}_0)$。[@problem_id:3103601]

正是双层势的这种跳跃行为，导致在BIE中出现了一个与边界局部几何相关的系数。当我们将积分表达式的极限取到边界点 $\boldsymbol{\xi}_0$ 时，会得到如下形式的直接BIE：
$$
c(\boldsymbol{\xi}_0)u(\boldsymbol{\xi}_0) + \int_{\Gamma} u(\boldsymbol{x}) \frac{\partial G(\boldsymbol{x}, \boldsymbol{\xi}_0)}{\partial n} d\Gamma(\boldsymbol{x}) = \int_{\Gamma} q(\boldsymbol{x}) G(\boldsymbol{x}, \boldsymbol{\xi}_0) d\Gamma(\boldsymbol{x})
$$
这里的积分通常需要在[柯西主值](@entry_id:192761)意义下理解。系数 $c(\boldsymbol{\xi}_0)$ 被称为**自由项系数（free-term coefficient）**，它代表了域在点 $\boldsymbol{\xi}_0$ 处所占的立体角分数。对于二维问题，它的值由该点的内角 $\theta$ 决定：
$$
c(\boldsymbol{\xi}_0) = \frac{\theta}{2\pi}
$$
其中角度 $\theta$ 以[弧度](@entry_id:171693)为单位。在一个光滑的[边界点](@entry_id:176493)上，内角 $\theta = \pi$，因此 $c(\boldsymbol{\xi}_0) = \frac{1}{2}$。[@problem_id:2560745] 而在一个多边形域的角点处，$\theta$ 是该角的实际内角。例如，在一个内角为 $\frac{3\pi}{2}$ 的凹角（re-entrant corner）处，系数为 $c(\boldsymbol{\xi}_0) = \frac{3\pi/2}{2\pi} = \frac{3}{4}$。[@problem_id:2560772] 这个系数的正确取值对于建立一个自洽的离散系统至关重要。

### [核函数](@entry_id:145324)的奇异性

BIE中的积分核函数（$G$ 和 $\frac{\partial G}{\partial n}$）在积分点 $\boldsymbol{x}$ 趋近于源点 $\boldsymbol{y}$ 时会变得奇异。奇异性的强度决定了积分的性质以及数值计算的难度。

我们首先需要确定不同维度下[基本解](@entry_id:184782)的具体形式。通过对定义方程 $\Delta G = -\delta$ 在以源点为中心的小球（或圆）上积分，并应用[高斯散度定理](@entry_id:188065)，可以推导出：
*   在三维空间（$n=3$）中，[拉普拉斯方程](@entry_id:143689)的[基本解](@entry_id:184782)为 $G(r) = \frac{1}{4\pi r}$，其中 $r=|\boldsymbol{x}-\boldsymbol{y}|$。
*   在二维空间（$n=2$）中，[基本解](@entry_id:184782)为 $G(r) = -\frac{1}{2\pi}\ln(r)$。

根据这些形式，我们可以分析积分核的奇异性。一个形如 $r^{-\alpha}$ 的[核函数](@entry_id:145324)，在维度为 $d$ 的边界上积分（例如，在三维空间中 $d=2$ 的[曲面](@entry_id:267450)或二维空间中 $d=1$ 的曲线），其积分表现得像 $\int_0 \rho^{-\alpha} \rho^{d-1} d\rho$。[积分收敛](@entry_id:139742)的条件是 $d-1-\alpha > -1$，即 $\alpha  d$。
*   **弱奇异（Weakly Singular）**: 如果 $\alpha  d$，积分是收敛的，可以直接用标准[数值积分方法](@entry_id:141406)（经过[坐标变换](@entry_id:172727)后）处理。
*   **强奇异（Strongly Singular）**: 如果 $\alpha = d$，积分发散，但其[柯西主值](@entry_id:192761)（Cauchy Principal Value, CPV）存在。
*   **超奇异（Hypersingular）**: 如果 $\alpha > d$，积分在[主值](@entry_id:189577)意义下也发散，需要更高阶的[正则化方法](@entry_id:150559)。

根据这个分类：[@problem_id:2560788]
*   **在三维中 ($d=2$)**:
    *   单层核 $G \sim r^{-1}$ ($\alpha=1$)。因为 $\alpha=1  d=2$，所以是**弱奇异**的。
    *   双层核的梯度部分 $\|\nabla G\| \sim r^{-2}$ ($\alpha=2$)。因为 $\alpha=2 = d=2$，所以是**强奇异**的。
*   **在二维中 ($d=1$)**:
    *   单层核 $G \sim \ln r$。这种对数奇异[性比](@entry_id:172643)任何幂次 $r^{-\alpha}$（$\alpha>0$）都弱，积分是收敛的，因此是**弱奇异**的。
    *   双层核的梯度部分 $\|\nabla G\| \sim r^{-1}$ ($\alpha=1$)。因为 $\alpha=1 = d=1$，所以是**强奇异**的。

理解[核函数](@entry_id:145324)的奇异性等级是实现稳健BEM代码的关键，因为它直接决定了在计算[矩阵元](@entry_id:186505)素，特别是对角线元素时，必须采用何种[数值积分](@entry_id:136578)策略。

### 离散化：从[边界积分方程](@entry_id:746942)到线性代数

为了数值求解BIE，我们需要将其离散化为一个线性代数系统。最常用的方法是**[配置法](@entry_id:142690)（collocation method）**，也称点配法。
1.  **边界离散化**：首先，将连续的边界 $\Gamma$ 分割成一系列小的边界**单元（elements）**，如直线段（2D）或三角形/四边形面片（3D）。这些单元的顶点被称为**节点（nodes）**。
2.  **[函数近似](@entry_id:141329)**：在每个单元上，未知的边界函数（如 $u$ 和 $q$）被近似为简单的[基函数](@entry_id:170178)（或形函数）的线性组合，其系数是这些函数在节点上的值。例如，在节点 $\boldsymbol{\xi}_j$ 处的值为 $u_j$ 和 $q_j$。
3.  **配置**：将离散化的函数代入连续的BIE中，然后要求该方程在所有节点 $\boldsymbol{\xi}_i$（称为[配置点](@entry_id:169000)）上精确成立。

对每个[配置点](@entry_id:169000) $\boldsymbol{\xi}_i$ 应用此过程，我们得到一个线性方程。将所有 $N$ 个节点的[方程组](@entry_id:193238)合在一起，就形成了一个 $N \times N$ 的[线性方程组](@entry_id:148943)，其矩阵形式通常写作：
$$
[H] \{u\} = [G] \{q\}
$$
其中，$\{u\}$ 和 $\{q\}$ 是包含所有节点上 $u_j$ 和 $q_j$ 值的列向量。矩阵 $[H]$ 和 $[G]$ 被称为**影响矩阵（influence matrices）**，其元素 $H_{ij}$ 和 $G_{ij}$ 表示节点 $j$ 处的[基函数](@entry_id:170178)对[配置点](@entry_id:169000) $i$ 处方程的贡献。它们的定义为：
$$
G_{ij} = \int_{\Gamma_j} N_j(\boldsymbol{x}) G(\boldsymbol{x}, \boldsymbol{\xi}_i) d\Gamma(\boldsymbol{x})
$$
$$
H_{ij} = \int_{\Gamma_j} N_j(\boldsymbol{x}) \frac{\partial G(\boldsymbol{x}, \boldsymbol{\xi}_i)}{\partial n} d\Gamma(\boldsymbol{x})
$$
这里 $N_j(\boldsymbol{x})$ 是与节点 $j$ 相关的形函数，积分在包含节点 $j$ 的单元 $\Gamma_j$ 上进行。

在组装这些矩阵时，对角[线元](@entry_id:196833)素（$i=j$）的处理需要特别小心，因为此时源点和积分点重合。
*   $G_{ii}$ 的积分包含一个弱奇异核（$\ln r$ 或 $r^{-1}$），这个积分是可积的，可以通过解析积分或特殊的[数值积分](@entry_id:136578)技术精确计算。
*   $H_{ii}$ 的积分包含一个强奇异核，需要在[柯西主值](@entry_id:192761)意义下计算。在[配置法](@entry_id:142690)中，自由项系数 $c(\boldsymbol{\xi}_i)$ 通常与[主值](@entry_id:189577)积分项合并在一起，以形成最终的对角元。对于光滑边界上的节点，$c_i = 1/2$，这个值会直接加入到 $H_{ii}$ 的计算中。[@problem_id:2560745] 在角点处，则必须使用正确的、与角度相关的 $c_i$ 值。[@problem_id:2560772]

对于一个给定的[边值问题](@entry_id:193901)（例如，已知 $\{u\}$，求解 $\{q\}$），上述[矩阵方程](@entry_id:203695)可以被重新[排列](@entry_id:136432)成一个标准形式 $A\boldsymbol{x}=\boldsymbol{b}$ 并求解。

### 计算特性与实际挑战

边界元法独特的数学结构赋予了它一系列区别于[有限元法](@entry_id:749389)（FEM）或有限差分法（FDM）等域方法的计算特性、优势和挑战。

#### BEM的优势与适用场景

1.  **降维**：BEM只在问题的边界上进行离散化，将三维问题转化为二维，二维问题转化为一维。这意味着对于具有复杂内部结构但表面相对简单的物体（所谓的“体表比”小的问题），BEM所需的未知数数量（$N$）远少于域方法。[@problem_id:3103656]

2.  **高精度与几何灵活性**：由于BEM使用了精确满足控制方程的[基本解](@entry_id:184782)，其唯一的近似误差来源于边界离散化和边界函数近似。对于光滑边界和光滑的边界数据，BEM可以达到非常高的精度。它能够精确地表示弯曲的边界，而无需像基于笛卡尔网格的FDM那样使用“阶梯状”近似，从而避免了由此引入的几何误差。[@problem_id:3103656]

3.  **自然处理无限域问题**：基本解本身就满足无穷远处的[衰减条件](@entry_id:157952)（例如，拉普拉斯问题的解在无穷远处趋于零，或亥姆霍兹问题的解满足[Sommerfeld辐射条件](@entry_id:168772)）。因此，BEM是求解声学和[电磁散射](@entry_id:182193)等外部问题（exterior problems）的理想选择，因为它无需引入人工边界来截断计算域，从而避免了FEM/FDM中 truncation error 的问题。[@problem_id:2377314]

#### 计算复杂性

BEM的降维优势伴随着一个巨大的计算代价：其产生的**影响矩阵 $[H]$ 和 $[G]$ 是全填充的、稠密的（dense）**。这是因为基本解 $G(\boldsymbol{x}, \boldsymbol{y})$ 是非局部的，边界上任意两点之间都存在相互作用。这与FEM/FDM形成的[稀疏矩阵](@entry_id:138197)形成鲜明对比。
对于一个有 $N$ 个边界未知数的问题，一个“朴素”的BEM实现具有以下计算复杂性：[@problem_id:2560743] [@problem_id:2377314]
*   **内存**：存储[稠密矩阵](@entry_id:174457)需要 $O(N^2)$ 的内存。
*   **矩阵组装**：计算 $N^2$ 个矩阵元素需要 $O(N^2)$ 的时间。
*   **求解**：
    *   使用直接法（如高斯消元）求解稠密[线性系统](@entry_id:147850)需要 $O(N^3)$ 的时间。
    *   使用[迭代法](@entry_id:194857)（如GMRES）求解，每次迭代需要一次矩阵-向量乘法，成本为 $O(N^2)$。

$O(N^2)$ 的内存和 $O(N^3)$ 或 $O(N^2)$ 的求解时间使得朴素BEM对于大規模问题（例如，$N > 10^5$）变得不可行。这一瓶颈催生了**快速边界元法**的发展，如**[快速多极子方法](@entry_id:140932)（Fast Multipole Method, FMM）**和**[分层矩阵](@entry_id:750110)（Hierarchical Matrices, H-Matrices）**技术。这些先进算法通过近似[远场](@entry_id:269288)交互，将矩阵-向量乘法的成本降低到接近线性的 $O(N\log^p N)$ 或 $O(N)$，同时内存需求也降至同等级别，从而极大地扩展了BEM的应用范围。[@problem_id:2560743]

#### 高级挑战与对策

除了[计算复杂性](@entry_id:204275)，BEM在特定物理问题中还会遇到一些独特的挑战。

1.  **伪特征频率问题（Fictitious Eigenfrequencies）**：在使用BEM求解外部波动问题（如由[亥姆霍兹方程](@entry_id:149977) $\nabla^2 u + k^2 u = 0$ 描述的[声学](@entry_id:265335)或[电磁散射](@entry_id:182193)）时，某些特定的[边界积分方程](@entry_id:746942) formulations 会在特定的频率 $k$ 上失效。这些频率恰好对应于物体 *内部* 区域的狄利克雷或[诺伊曼问题](@entry_id:176713)的特征频率（eigenfrequencies）。在这些频率上，BIE的解不再唯一，导致数值解崩溃。这是一个属于[连续算子](@entry_id:143297)本身的数学缺陷，而非离散化伪影。幸运的是，这个问题有成熟的解决方案，例如**[组合场积分方程](@entry_id:747497)（Combined Field Integral Equation, CFIE）**，它通过将单层势和双层势进行特定组合，构造出一个在所有实数频率上都保证唯一解的[积分方程](@entry_id:138643)。另一种方法是在[波数](@entry_id:172452) $k$ 中引入一个小的虚部（代表物理上的微小损耗），从而避开实数轴上的特征频率。[@problem_id:2377284]

2.  **薄体问题（Thin Body Problems）**：当BEM用于模拟非常薄的结构（例如，两个表面彼此非常靠近，间距 $\delta$ 远小于其尺寸）时，标准BEM formulation 会导致极其严重的**病态（ill-conditioning）**。这是因为来自两个靠近表面的[积分方程](@entry_id:138643)变得近似线性相关，使得[系统矩阵](@entry_id:172230)接近奇异。其[条件数](@entry_id:145150)会随着 $\delta \to 0$ 而急剧增长（例如，$\kappa \sim O(\delta^{-1})$）。直接求解这样的系统会因[舍入误差](@entry_id:162651)而被放大，导致结果完全不可信。处理这一挑战的策略包括：
    *   **方程重构**：引入新的变量，如两个表面上密度的和与差，将原始的第一类[Fredholm积分方程](@entry_id:277002)组转化为在 $\delta \to 0$ 极限下表现良好的第二[类方程](@entry_id:144428)组。
    *   **专用[预条件子](@entry_id:753679)**：设计一个“物理感知”的块预条件子，它能够解析地近似[病态矩阵](@entry_id:147408)的逆，从而在迭代求解过程中显著改善条件数，使其不再依赖于 $\delta$。[@problem_id:2377306]

这些挑战及其解决方案体现了边界元法研究领域的深度和活力，它不仅是一种数值计算工具，更是一个与数学物理和[算子理论](@entry_id:139990)紧密相连的丰富领域。