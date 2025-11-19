## 引言
纳维-斯托克斯方程是描述粘性流体运动的基本定律，是[流体力学](@entry_id:136788)乃至众多科学与工程领域的基石。然而，这些复杂的[非线性偏微分方程](@entry_id:169481)在绝大多数实际情况下无法求得解析解，必须依赖于数值方法进行近似求解。这便引出了一个核心挑战：如何将连续的物理定律转化为计算机可以理解和处理的离散代数问题？本文旨在系统性地填补这一知识鸿沟，为读者提供一个关于[纳维-斯托克斯方程](@entry_id:142275)有限元[半离散化](@entry_id:163562)（即仅在空间上离散）的完整理论框架。

本文将分为三个核心章节，带领读者逐步深入这一主题。首先，在“原理和机制”一章中，我们将从第一性原理出发，详细推导方程的弱形式，探讨[函数空间](@entry_id:143478)的选择，并揭示离散化后产生的关键[鞍点问题](@entry_id:174221)结构和[LBB稳定性条件](@entry_id:751194)，最终构建出描述系统演化的矩阵形式[微分](@entry_id:158718)-[代数方程](@entry_id:272665)。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这一理论框架如何应用于解决实际物理问题，讨论从[雷诺数](@entry_id:136372)的影响到复杂几何处理的实际考量，并将其拓展到[流固耦合](@entry_id:171183)、[随机建模](@entry_id:261612)和数据驱动等前沿[交叉](@entry_id:147634)领域。最后，通过“动手实践”部分，您将有机会通过具体练习，将理论知识转化为解决问题的实践能力。通过这一系列的学习，您将能够透彻理解从连续物理模型到离散数值系统的完整推导路径，为进行高级[计算流体动力学](@entry_id:147500)研究与应用打下坚实的基础。

## 原理和机制

在前一章介绍不[可压缩纳维-斯托克斯](@entry_id:747591)方程的物理背景和重要性之后，本章将深入探讨其数学原理和[数值离散化](@entry_id:752782)的核心机制。我们的目标是将这些[偏微分方程](@entry_id:141332)（PDEs）转化为一个适合计算机求解的代数系统。这一过程被称为[半离散化](@entry_id:163562)（在空间上离散，在时间上保持连续），它构成了[计算流体动力学](@entry_id:147500)中许多现代有限元方法的基础。本章将系统地阐述从连续方程的弱形式表述到最终的矩阵形式[微分](@entry_id:158718)-代数方程（DAE）的推导过程，并阐明其中涉及的关键概念，如[函数空间](@entry_id:143478)的选择、[鞍点问题](@entry_id:174221)结构、稳定性和边界条件处理。

### 弱形式的推导

将一个[偏微分方程](@entry_id:141332)问题转化为有限元方法可以求解的形式，第一步是推导其等价的积分形式，即**弱形式**或**[变分形式](@entry_id:166033)**。这个过程不仅降低了对解的光滑性要求，还自然地将某些类型的边界条件（即自然边界条件）融入到问题表述中。

#### 从强形式到弱形式

我们从有界Lipschitz区域 $\Omega \subset \mathbb{R}^d$（其中 $d=2$ 或 $3$）上的不[可压缩纳维-斯托克斯](@entry_id:747591)方程的强形式（即[微分形式](@entry_id:146747)）出发：

$$
\begin{align*}
\partial_t \boldsymbol{u} + (\boldsymbol{u} \cdot \nabla) \boldsymbol{u} - \nu \Delta \boldsymbol{u} + \nabla p = \boldsymbol{f} \quad \text{在 } \Omega \times (0,T] \text{ 内} \\
\nabla \cdot \boldsymbol{u} = 0 \quad \text{在 } \Omega \times (0,T] \text{ 内}
\end{align*}
$$

这里，$\boldsymbol{u}$ 是流体速度场，$p$ 是压[力场](@entry_id:147325)，$\nu > 0$ 是运动粘度，$\boldsymbol{f}$ 是单位质量的[体力](@entry_id:174230)。为简单起见，我们首先考虑最常见的边界条件：在整个边界 $\partial\Omega$ 上的**无滑移[Dirichlet边界条件](@entry_id:142800)**，即 $\boldsymbol{u}=\boldsymbol{0}$。

推导弱形式的核心思想是**[Galerkin方法](@entry_id:260906)**：将方程乘以一个合适的**[检验函数](@entry_id:166589)（test function）**，然后在整个计算域 $\Omega$ 上积分。我们为动量方程选择一个速度检验函数 $\boldsymbol{v}$，为连续性方程选择一个压力检验函数 $q$。

对动量方程进行此操作，得到：
$$
\int_\Omega (\partial_t \boldsymbol{u} \cdot \boldsymbol{v}) \, dx + \int_\Omega ((\boldsymbol{u} \cdot \nabla) \boldsymbol{u} \cdot \boldsymbol{v}) \, dx - \nu \int_\Omega (\Delta \boldsymbol{u} \cdot \boldsymbol{v}) \, dx + \int_\Omega (\nabla p \cdot \boldsymbol{v}) \, dx = \int_\Omega (\boldsymbol{f} \cdot \boldsymbol{v}) \, dx
$$

这个积分形式仍然包含解 $\boldsymbol{u}$ 的[二阶导数](@entry_id:144508)（在拉普拉斯项 $\Delta \boldsymbol{u}$ 中），这对函数的光滑性要求很高。为了“减弱”这个要求，我们使用**分部积分法**（即高维的[Green第一恒等式](@entry_id:170345)）。

- **粘性项**：对于粘性项 $-\nu \int_\Omega (\Delta \boldsymbol{u} \cdot \boldsymbol{v}) \, dx$，分部积分得到：
$$
- \nu \int_\Omega (\Delta \boldsymbol{u} \cdot \boldsymbol{v}) \, dx = \nu \int_\Omega \nabla \boldsymbol{u} : \nabla \boldsymbol{v} \, dx - \nu \int_{\partial\Omega} \boldsymbol{v} \cdot (\nabla \boldsymbol{u} \cdot \mathbf{n}) \, dS
$$
其中“$:$”表示矩阵的[Frobenius内积](@entry_id:153693)。注意到边界积分项的出现。

- **压力项**：类似地，对压力项 $\int_\Omega (\nabla p \cdot \boldsymbol{v}) \, dx$ 进行分部积分：
$$
\int_\Omega (\nabla p \cdot \boldsymbol{v}) \, dx = - \int_\Omega p (\nabla \cdot \boldsymbol{v}) \, dx + \int_{\partial\Omega} p (\boldsymbol{v} \cdot \mathbf{n}) \, dS
$$

[分部积分](@entry_id:136350)成功地将导数从解变量（$\boldsymbol{u}$ 和 $p$）转移到了[检验函数](@entry_id:166589)（$\boldsymbol{v}$）上。现在，我们可以明智地[选择检验](@entry_id:182706)函数空间来简化方程。如果我们要求速度[检验函数](@entry_id:166589) $\boldsymbol{v}$ 满足与解相同的齐次[Dirichlet边界条件](@entry_id:142800)，即在 $\partial\Omega$ 上 $\boldsymbol{v}=\boldsymbol{0}$，那么上述两个边界积分项都将自动消失。

这一观察引出了用于速度的[函数空间](@entry_id:143478)的关键选择。**[Sobolev空间](@entry_id:141995)** $H^1(\Omega)$ 是所有在 $\Omega$ 上平方可积且其一阶[弱导数](@entry_id:189356)也平方可积的函数集合。而[子空间](@entry_id:150286) $H_0^1(\Omega)$ 则进一步要求函数在边界上的迹（trace）为零。因此，通过为速度解和检验函数选择 $V = H_0^1(\Omega)^d$ 空间，我们不仅强制执行了[无滑移边界条件](@entry_id:186229)，还简化了弱形式。

对于压力，由于它在弱形式中只出现了一阶导数（在项 $\nabla \cdot \boldsymbol{v}$ 中），我们只需要它在 $L^2(\Omega)$ 空间中，即平方可积。

综合以上步骤，不[可压缩纳维-斯托克斯](@entry_id:747591)问题的标准[弱形式](@entry_id:142897)表述为：寻找 $\boldsymbol{u}(t) \in V$ 和 $p(t) \in Q$（其中 $V=H_0^1(\Omega)^d$，$Q=L^2(\Omega)$）使得对于所有[检验函数](@entry_id:166589) $\boldsymbol{v} \in V$ 和 $q \in Q$：
$$
\begin{align*}
(\partial_t \boldsymbol{u}, \boldsymbol{v}) + \nu (\nabla \boldsymbol{u}, \nabla \boldsymbol{v}) + ((\boldsymbol{u} \cdot \nabla) \boldsymbol{u}, \boldsymbol{v}) - (p, \nabla \cdot \boldsymbol{v}) = (\boldsymbol{f}, \boldsymbol{v}) \\
(q, \nabla \cdot \boldsymbol{u}) = 0
\end{align*}
$$
这里，$(\cdot, \cdot)$ 表示标准的 $L^2(\Omega)$ [内积](@entry_id:158127)。这就是我们进行[空间离散化](@entry_id:172158)的出发点 [@problem_id:2582634]。

#### [函数空间](@entry_id:143478)的选择与压力唯一性

上述推导引出了一个微妙但至关重要的问题：压力的唯一性。在弱形式的动量方程中，压力 $p$ 通过项 $-(p, \nabla \cdot \boldsymbol{v})$ 发挥作用。现在，考虑将压力替换为 $p+c$，其中 $c$ 是任意一个空间常数。该项变为：
$$
-(p+c, \nabla \cdot \boldsymbol{v}) = -(p, \nabla \cdot \boldsymbol{v}) - c \int_\Omega \nabla \cdot \boldsymbol{v} \, dx
$$
根据散度定理，由于[检验函数](@entry_id:166589) $\boldsymbol{v} \in H_0^1(\Omega)^d$ 在边界 $\partial\Omega$ 上为零，我们有 $\int_\Omega \nabla \cdot \boldsymbol{v} \, dx = \int_{\partial\Omega} \boldsymbol{v} \cdot \mathbf{n} \, dS = 0$。这意味着 $-(p+c, \nabla \cdot \boldsymbol{v}) = -(p, \nabla \cdot \boldsymbol{v})$。换言之，给压力加上任意常数都不会改变[方程组](@entry_id:193238)。因此，压力解是不唯一的，它只能被确定到一个任意的常数。

为了得到一个唯一确定的压力解，我们必须施加一个额外的约束。标准做法是要求压力具有零均值，即 $\int_\Omega p \, dx = 0$。这通过将压力空间从 $L^2(\Omega)$ 限制到其[子空间](@entry_id:150286) $Q = L_0^2(\Omega) = \{q \in L^2(\Omega) : \int_\Omega q \, dx = 0\}$ 来实现。

从线性代数的角度来看，这种不确定性对应于离散化后[系统矩阵](@entry_id:172230)的奇异性。如果[常数函数](@entry_id:152060)属于压力有限元空间，那么它将位于[离散梯度](@entry_id:171970)算子的[零空间](@entry_id:171336)中，导致整个[鞍点系统](@entry_id:754480)矩阵有一个与常数[压力模](@entry_id:159654)式相关的零[特征值](@entry_id:154894)，从而使得代数系统不可解 [@problem_id:2582669]。因此，选择 $Q_h \subset L_0^2(\Omega)$ 对于获得一个适定的离散系统至关重要。

#### 非齐次与自然边界条件

虽然齐次[无滑移边界条件](@entry_id:186229)在学术问题中很常见，但实际工程应用通常涉及更复杂的边界情况。

- **非齐次[Dirichlet边界条件](@entry_id:142800)**：当边界上指定了非零速度 $\boldsymbol{u}=\boldsymbol{g}$（例如，在入口处）时，我们不能再假设解和[检验函数](@entry_id:166589)都在同一个零边界空间 $V$ 中。一种强大的标准技术是**提升法（lifting）**。我们将解分解为两部分：$\boldsymbol{u}_h(t) = \boldsymbol{w}_h(t) + \boldsymbol{R}(\boldsymbol{g})(t)$。其中，$\boldsymbol{R}(\boldsymbol{g})$ 是一个已知的“[提升函数](@entry_id:175709)”，它满足[非齐次边界条件](@entry_id:750645) $\boldsymbol{R}(\boldsymbol{g})|_{\Gamma_D}=\boldsymbol{g}$，而 $\boldsymbol{w}_h(t)$ 是新的未知量，它生活在齐次空间 $V_h$ 中（即 $\boldsymbol{w}_h|_{\Gamma_D}=\boldsymbol{0}$）。将这个分解代入弱形式，所有与 $\boldsymbol{w}_h$ 和 $p_h$ 相关的项保留在左侧，而所有仅涉及已知函数 $\boldsymbol{R}(\boldsymbol{g})$ 的项都被移到右侧，成为新的**附加力项**。例如，时间导数项 $(\partial_t \boldsymbol{u}_h, \boldsymbol{v}_h)$ 会产生 $(\partial_t \boldsymbol{R}(\boldsymbol{g}), \boldsymbol{v}_h)$，粘性项 $(\nabla \boldsymbol{u}_h, \nabla \boldsymbol{v}_h)$ 会产生 $(\nabla \boldsymbol{R}(\boldsymbol{g}), \nabla \boldsymbol{v}_h)$，[非线性](@entry_id:637147)[对流](@entry_id:141806)项 $((\boldsymbol{u}_h \cdot \nabla) \boldsymbol{u}_h, \boldsymbol{v}_h)$ 会产生多个[交叉](@entry_id:147634)项和 $\boldsymbol{R}(\boldsymbol{g})$ 的自作用项。同样，[不可压缩性约束](@entry_id:750592)也变为 $(q_h, \nabla \cdot \boldsymbol{w}_h) = - (q_h, \nabla \cdot \boldsymbol{R}(\boldsymbol{g}))$，除非[提升函数](@entry_id:175709) $\boldsymbol{R}(\boldsymbol{g})$ 被特殊构造为[无散度](@entry_id:190991)的 [@problem_id:2582662]。

- **自然（Neumann）边界条件**：当边界上规定的是应力而非速度时，例如在出口处的牵[引力](@entry_id:175476)条件 $\boldsymbol{\sigma}(\boldsymbol{u},p)\mathbf{n}=\mathbf{h}$，其中 $\boldsymbol{\sigma} = 2\nu\boldsymbol{\varepsilon}(\boldsymbol{u}) - p\mathbf{I}$ 是柯西应力张量。这种条件被称为**自然边界条件**，因为它们会自然地出现在弱形式的边界积分项中。回顾粘性项和压力项的[分部积分](@entry_id:136350)，我们得到的边界项是 $\int_{\partial\Omega} \boldsymbol{v} \cdot (\boldsymbol{\sigma} \mathbf{n}) \, dS$。在[弱形式](@entry_id:142897)中，这个积分在Dirichlet边界 $\Gamma_D$ 上为零（因为 $\boldsymbol{v}=\boldsymbol{0}$），但在Neumann边界 $\Gamma_N$ 上，它变为 $\int_{\Gamma_N} \boldsymbol{v} \cdot \mathbf{h} \, dS$。这个项不包含解的导数，可以直接作为力向量的一部分处理 [@problem_id:2582672]。

### 抽象算子与[能量守恒](@entry_id:140514)

为了更深入地分析其数学结构，将[弱形式](@entry_id:142897)写成抽象算子形式是很有帮助的。这种形式揭示了问题的核心[代数结构](@entry_id:137052)，并有助于能量分析。

#### 算子形式

我们将弱形式中的每个项与一个算子关联起来。对于 $\boldsymbol{u} \in V, p \in Q$ 和 $\boldsymbol{v} \in V, q \in Q$：
- **粘性算子 A**：$a(\boldsymbol{u},\boldsymbol{v}) := \nu (\nabla \boldsymbol{u}, \nabla \boldsymbol{v})$ 定义了线性、对称、正定的粘性算子 $A: V \to V'$，其中 $\langle A\boldsymbol{u}, \boldsymbol{v} \rangle = a(\boldsymbol{u},\boldsymbol{v})$。（$V'$ 是 $V$ 的[对偶空间](@entry_id:146945)）。
- **[对流](@entry_id:141806)算子 N(u)**：$c(\boldsymbol{w};\boldsymbol{u},\boldsymbol{v}) := ((\boldsymbol{w} \cdot \nabla)\boldsymbol{u}, \boldsymbol{v})$ 定义了[非线性](@entry_id:637147)[对流](@entry_id:141806)算子 $N(\boldsymbol{u}): V \to V'$，其中 $\langle N(\boldsymbol{u}), \boldsymbol{v} \rangle = c(\boldsymbol{u};\boldsymbol{u},\boldsymbol{v})$。这个算子是[纳维-斯托克斯方程](@entry_id:142275)所有[非线性](@entry_id:637147)的来源 [@problem_id:2582637]。
- **[散度算子](@entry_id:265975) B** 和 **[梯度算子](@entry_id:275922) $B^T$**：$b(\boldsymbol{v},q) := -(q, \nabla \cdot \boldsymbol{v})$ 定义了[散度算子](@entry_id:265975) $B: V \to Q'$ 和[梯度算子](@entry_id:275922) $B^T: Q \to V'$。它们是伴随（[转置](@entry_id:142115)）关系，满足 $\langle B\boldsymbol{v}, q \rangle = \langle \boldsymbol{v}, B^T q \rangle = b(\boldsymbol{v},q)$。

利用这些定义，纳维-斯托克斯方程的[弱形式](@entry_id:142897)可以紧凑地写成一个在对偶空间中成立的算子[方程组](@entry_id:193238)：
$$
\begin{align*}
\partial_t \boldsymbol{u} + A\boldsymbol{u} + N(\boldsymbol{u}) + B^T p = \boldsymbol{f} \quad \text{在 } V' \text{ 中} \\
B\boldsymbol{u} = 0 \quad \text{在 } Q' \text{ 中}
\end{align*}
$$
这种形式清晰地分离了问题的线性（粘性）、[非线性](@entry_id:637147)（[对流](@entry_id:141806)）和约束（不可压缩性）部分。

一个特别重要的细节是[对流](@entry_id:141806)项 $c(\boldsymbol{w};\boldsymbol{u},\boldsymbol{v})$ 的具体形式。标准形式 $((\boldsymbol{w} \cdot \nabla)\boldsymbol{u}, \boldsymbol{v})$ 在离散后通常不保持[能量守恒](@entry_id:140514)。一个常用的替代形式是**斜对称形式**：
$$
c_{skew}(\boldsymbol{w};\boldsymbol{u},\boldsymbol{v}) := \frac{1}{2} \left( ((\boldsymbol{w} \cdot \nabla)\boldsymbol{u}, \boldsymbol{v}) - ((\boldsymbol{w} \cdot \nabla)\boldsymbol{v}, \boldsymbol{u}) \right)
$$
当 $\boldsymbol{w}$ 是[无散场](@entry_id:260932)时，这个形式与[标准形式](@entry_id:153058)等价。其关键性质是 $c_{skew}(\boldsymbol{w};\boldsymbol{u},\boldsymbol{u}) = 0$，这意味着[对流](@entry_id:141806)项在能量平衡中不会产生或消耗能量，这对于长时间模拟的稳定性至关重要 [@problem_id:2582665]。

#### 动能平衡

通过在[动量方程](@entry_id:197225)的弱形式中[选择检验](@entry_id:182706)函数为解本身（即 $\boldsymbol{v}=\boldsymbol{u}$），我们可以推导出系统的动能平衡方程。动能定义为 $E(t) = \frac{1}{2} \|\boldsymbol{u}(t)\|_{L^2}^2$。其时间导数为：
$$
\frac{dE}{dt} = (\partial_t \boldsymbol{u}, \boldsymbol{u}) = (\boldsymbol{f},\boldsymbol{u}) - a(\boldsymbol{u},\boldsymbol{u}) - c(\boldsymbol{u};\boldsymbol{u},\boldsymbol{u}) - b(\boldsymbol{u},p)
$$
- $(\boldsymbol{f},\boldsymbol{u})$ 是外力所做的功率。
- $a(\boldsymbol{u},\boldsymbol{u}) = \nu \|\nabla \boldsymbol{u}\|_{L^2}^2 \ge 0$ 是[粘性耗散](@entry_id:143708)，它总是消耗能量。
- 如果使用斜对称形式，$c(\boldsymbol{u};\boldsymbol{u},\boldsymbol{u}) = 0$。如果使用[标准形式](@entry_id:153058)，在 $\nabla \cdot \boldsymbol{u} = 0$ 和 $\boldsymbol{u}|_{\partial\Omega}=\boldsymbol{0}$ 的条件下，[分部积分](@entry_id:136350)显示 $c(\boldsymbol{u};\boldsymbol{u},\boldsymbol{u}) = 0$。因此，在封闭系统中，[对流](@entry_id:141806)不改变总动能。
- $b(\boldsymbol{u},p) = -(p, \nabla \cdot \boldsymbol{u}) = 0$ 因为 $\nabla \cdot \boldsymbol{u} = 0$。这意味着在不可压缩流中，压力在内部不做功。

因此，对于一个封闭系统（$\boldsymbol{u}|_{\partial\Omega}=\boldsymbol{0}$），[能量平衡](@entry_id:150831)简化为：
$$
\frac{1}{2}\frac{d}{dt}\|\boldsymbol{u}\|_{L^2}^2 + \nu \|\nabla \boldsymbol{u}\|_{L^2}^2 = (\boldsymbol{f},\boldsymbol{u})
$$
动能的变化率加上[粘性耗散](@entry_id:143708)等于外力做功。如果存在Neumann边界，则牵[引力](@entry_id:175476)做的功和通过边界的能量[对流](@entry_id:141806)也会出现在[能量平衡方程](@entry_id:191484)中，为系统增加或带走能量 [@problem_id:2582672]。

### Galerkin[半离散化](@entry_id:163562)

[Galerkin方法](@entry_id:260906)的核心思想是用有限维[子空间](@entry_id:150286) $V_h \subset V$ 和 $Q_h \subset Q$ 来近似无限维的函数空间 $V$ 和 $Q$。然后，在这些[子空间](@entry_id:150286)中求解弱形式问题。

#### 有限元空间与[鞍点](@entry_id:142576)结构

我们首先需要一个计算域 $\Omega$ 的**构形[三角剖分](@entry_id:272253)** $\mathcal{T}_h$，它由有限个单纯形（二维中的三角形，三维中的四面体）组成，且任意两个单纯形的交集是空集、一个公共顶点、一条公共边或一个公共面 [@problem_id:2582654]。

在这样的网格上，我们构建由分片多项式组成的有限元空间。例如，一个著名的稳定单元对是**[Taylor-Hood单元](@entry_id:165658)**，它对速度使用 $k+1$ 次连续多项式，对压力使用 $k$ 次连续多项式（$k \ge 1$）。记为 $P_{k+1}/P_k$。
- **[速度空间](@entry_id:181216) $V_h$**：由定义在 $\mathcal{T}_h$ 上的分片 $(k+1)$ 次多项式向量场构成，这些向量场在整个 $\Omega$ 上是连续的，并且在边界 $\partial\Omega$ 上为零。这个构造确保了 $V_h \subset H_0^1(\Omega)^d$，这对于粘性项的[适定性](@entry_id:148590)和[齐次边界条件](@entry_id:750371)的强施加是必需的 [@problem_id:2582654]。
- **压力空间 $Q_h$**：由定义在 $\mathcal{T}_h$ 上的分片 $k$ 次多项式构成，这些多项式是连续的，并且具有零均值，以确保 $Q_h \subset L_0^2(\Omega)$。

将解 $(\boldsymbol{u}_h, p_h)$ 和[检验函数](@entry_id:166589) $(\boldsymbol{v}_h, q_h)$ 限制在这些有限维空间 $V_h \times Q_h$ 中，我们得到的离散问题是一个典型的**[鞍点问题](@entry_id:174221)**。其性质与标准的[椭圆问题](@entry_id:146817)有很大不同。特别是，整个系统的双线性形式在乘积空间 $V_h \times Q_h$ 上不是强制的（coercive）[@problem_id:2582637]。这意味着不能直接应用[Lax-Milgram定理](@entry_id:137966)来保证解的存在性和唯一性。

#### LBB（inf-sup）稳定性条件

[鞍点问题](@entry_id:174221)的[适定性](@entry_id:148590)由更一般的[Babuška-Brezzi理论](@entry_id:178586)来保证。该理论要求两个关键条件：
1. 粘性双线性形式 $a(\cdot,\cdot)$ 在离散[无散度速度](@entry_id:192418)空间 $Z_h = \{\boldsymbol{v}_h \in V_h : (q_h, \nabla \cdot \boldsymbol{v}_h) = 0 \quad \forall q_h \in Q_h\}$ 上是强制的。由于 $a(\cdot,\cdot)$ 在整个 $V_h$ 上是强制的，这个条件通常是满足的 [@problem_id:2582637]。
2. 速度和压力空间对 $(V_h, Q_h)$ 必须满足**Ladyzhenskaya-Babuška-Brezzi (LBB)** 条件，也称为**[inf-sup条件](@entry_id:746626)**：存在一个与网格尺寸 $h$ 无关的常数 $\beta_0 > 0$，使得
$$
\inf_{0 \neq q_h \in Q_h} \sup_{0 \neq \boldsymbol{v}_h \in V_h} \frac{-(q_h, \nabla \cdot \boldsymbol{v}_h)}{\|\boldsymbol{v}_h\|_{H^1} \|q_h\|_{L^2}} \ge \beta_0
$$
[LBB条件](@entry_id:746626)在直观上意味着，对于任何一个非零的离散[压力模](@entry_id:159654)式 $q_h$，都必须存在一个离散[速度场](@entry_id:271461) $\boldsymbol{v}_h$，其散度 $\nabla \cdot \boldsymbol{v}_h$ 能够“感知”到这个[压力模](@entry_id:159654)式。如果这个条件不满足，就会出现虚假的、物理上不存在的压力[振荡](@entry_id:267781)，即所谓的**[伪压力模式](@entry_id:755261)（spurious pressure modes）**。

一个经典的失败案例是使用**等阶插值**，例如 $P_1/P_1$（对速度和压力都使用线性连续多项式）。在这种情况下，离散[速度场](@entry_id:271461)的散度空间“太小”，无法控制压力空间中的所有模式。特别是，在某些网格上，可以构造出在单元上剧烈[振荡](@entry_id:267781)的“棋盘格”[压力模](@entry_id:159654)式，它与所有离散[速度场](@entry_id:271461)的散度正交，因此无法被[不可压缩性约束](@entry_id:750592)所抑制。这种不稳定性无法通过加密网格来消除；事实上，它通常会随着网格的细化而恶化 [@problem_id:2582671]。因此，选择满足[LBB条件](@entry_id:746626)的单元对（如[Taylor-Hood单元](@entry_id:165658)）或引入额外的稳定化项是求解[不可压缩流](@entry_id:140301)问题的关键。

### 半离散矩阵系统

最后一步是将位于有限元空间中的[变分问题](@entry_id:756445)转化为一个[常微分方程](@entry_id:147024)（ODE）或[微分](@entry_id:158718)-[代数方程](@entry_id:272665)（DAE）的矩阵系统。我们通过在 $V_h$ 和 $Q_h$ 中选择一组[基函数](@entry_id:170178) $\{\boldsymbol{\phi}_i\}_{i=1}^{N_u}$ 和 $\{\psi_k\}_{k=1}^{N_p}$ 来实现这一点。然后将未知解 $\boldsymbol{u}_h(t)$ 和 $p_h(t)$ 写成这些[基函数](@entry_id:170178)的[线性组合](@entry_id:154743)：
$$
\boldsymbol{u}_h(x,t) = \sum_{j=1}^{N_u} U_j(t) \boldsymbol{\phi}_j(x), \qquad p_h(x,t) = \sum_{l=1}^{N_p} P_l(t) \psi_l(x)
$$
其中 $\mathbf{U}(t) \in \mathbb{R}^{N_u}$ 和 $\mathbf{P}(t) \in \mathbb{R}^{N_p}$ 是待求的随时间变化的系数向量。

将这些展开式代入半离散弱形式，并依次选择每个[基函数](@entry_id:170178)作为[检验函数](@entry_id:166589)（$\boldsymbol{v}_h = \boldsymbol{\phi}_i, q_h = \psi_k$），我们得到一个矩阵系统 [@problem_id:2582673]：
$$
\begin{align*}
\mathbf{M} \dot{\mathbf{U}}(t) + \nu \mathbf{K} \mathbf{U}(t) + \mathbf{C}(\mathbf{U}(t))\mathbf{U}(t) + \mathbf{B}^T \mathbf{P}(t) = \mathbf{F}(t) \\
\mathbf{B} \mathbf{U}(t) = \mathbf{0}
\end{align*}
$$
其中矩阵和向量的定义如下：
- **[质量矩阵](@entry_id:177093) $\mathbf{M}$**（对称正定）：$M_{ij} = (\boldsymbol{\phi}_j, \boldsymbol{\phi}_i)$
- **刚度矩阵 $\mathbf{K}$**（[对称正定](@entry_id:145886)）：$K_{ij} = (\nabla \boldsymbol{\phi}_j, \nabla \boldsymbol{\phi}_i)$
- **[对流矩阵](@entry_id:747848) $\mathbf{C}(\mathbf{U})$**（依赖于解）：$C(\mathbf{U})_{ij} = c(\boldsymbol{u}_h; \boldsymbol{\phi}_j, \boldsymbol{\phi}_i) = \sum_{m=1}^{N_u} U_m \int_\Omega (\boldsymbol{\phi}_m \cdot \nabla)\boldsymbol{\phi}_j \cdot \boldsymbol{\phi}_i \, dx$
- **离散散度矩阵 $\mathbf{B}$**：$B_{kj} = -( \psi_k, \nabla \cdot \boldsymbol{\phi}_j )$
- **[载荷向量](@entry_id:635284) $\mathbf{F}$**：$F_i(t) = (\boldsymbol{f}(t), \boldsymbol{\phi}_i)$

这个系统具有以下显著特性：
1.  它是一个**[微分](@entry_id:158718)-[代数方程](@entry_id:272665)（DAE）**，因为没有时间导数项 $\dot{\mathbf{P}}$ 出现。更具体地说，它是一个**指数-2**的DAE系统，因为需要对代数约束 $\mathbf{B}\mathbf{U}=\mathbf{0}$ [微分](@entry_id:158718)一次才能求解出压力 $\mathbf{P}$ [@problem_id:2582619]。
2.  即使对于线性的[稳态](@entry_id:182458)[Stokes问题](@entry_id:755479)（忽略 $\dot{\mathbf{U}}$ 和 $\mathbf{C}(\mathbf{U})\mathbf{U}$），[系统矩阵](@entry_id:172230) $\begin{pmatrix} \nu \mathbf{K} & \mathbf{B}^T \\ \mathbf{B} & \mathbf{0} \end{pmatrix}$ 也是一个**不定（indefinite）的[鞍点](@entry_id:142576)矩阵**，而不是[对称正定](@entry_id:145886)的。这需要专门的[线性求解器](@entry_id:751329)。
3.  [LBB条件](@entry_id:746626)的满足在代数上意味着离散散度矩阵 $\mathbf{B}$ 具有**满行秩**。这保证了与压力相关的Schur补算子 $\mathbf{B} \mathbf{K}^{-1} \mathbf{B}^T$ 是可逆的，从而确保了压力的唯一性和稳定性 [@problem_id:2582619]。
4.  离散[能量守恒](@entry_id:140514)得以保持。通过用 $\mathbf{U}^T$ 左乘[动量方程](@entry_id:197225)，并利用 $\mathbf{U}^T \mathbf{B}^T \mathbf{P} = (\mathbf{B}\mathbf{U})^T \mathbf{P} = 0$ 和（如果使用斜对称形式）$\mathbf{U}^T \mathbf{C}(\mathbf{U}) \mathbf{U} = 0$，我们恢复了离散动能[平衡方程](@entry_id:172166)：$\frac{1}{2}\frac{d}{dt}(\mathbf{U}^T \mathbf{M} \mathbf{U}) + \nu \mathbf{U}^T \mathbf{K} \mathbf{U} = \mathbf{U}^T \mathbf{F}$。这表明离散压力和[对流](@entry_id:141806)项在能量上是中性的，与物理现实一致 [@problem_id:2582619]。

通过本章的推导，我们已经将一个复杂的物理问题系统地转化为一个结构清晰、性质明确的矩阵方程组，为下一章讨论[时间离散化](@entry_id:169380)和[非线性](@entry_id:637147)求解策略铺平了道路。