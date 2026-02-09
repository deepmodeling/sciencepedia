## 引言
不连续伽辽金（DG）方法是求解偏微分方程的一种强大数值技术，但其公式常涉及复杂的体积分与面积分混合，这使得理论分析和计算实现变得复杂。为应对此挑战，提升算子作为一种优雅的数学工具应运而生，为DG公式提供了统一的框架。本文旨在全面探讨DG方法中的提升算子公式，通过系统地将面积分信息转化为体积分，以弥合抽象理论与实际应用之间的鸿沟。读者将通过本文开启一段结构化的学习之旅：第一章“原理与机制”将奠定理论基础，定义提升算子并探索其基本性质。随后的“应用与交叉学科联系”将展示该算子在构建先进数值格式及其与多个科学领域关联方面的多样性。最后，“动手实践”部分将通过具体的计算示例来巩固理解并指导实际实现。

## 原理与机制

本章深入探讨不连续伽辽金（DG）方法中提升算子公式的核心原理和机制。我们将正式定义提升算子，探索其基本性质，并展示其在构建和分析稳定高效的DG格式中的核心作用。

### 提升算子的定义与动机

在不连续伽辽金（DG）方法中，一个核心特征是在单元边界（或称“面”）上处理数值通量和解的跳跃。这自然地在弱形式中引入了大量的面积分。虽然这种方法在理论上很健全，但从计算角度来看，同时处理体积分和面积分会使实现变得复杂。此外，在理论分析中，混合使用不同维度的积分也会带来挑战。

**提升算子（lifting operator）** 提供了一个优雅的解决方案。它是一个数学工具，其基本功能是将定义在单元面上的函数（“面函数”）映射为定义在单元内部的函数（“体函数”）。通过这种方式，我们可以将面积分等效地转化为体积分，从而在统一的框架下进行处理。

**形式化定义：基于Riesz表示定理**

提升算子的存在性和唯一性是建立在有限维希尔伯特空间中的 **Riesz表示定理** 之上的。该定理指出，空间上的任何连续线性泛函都可以表示为与该空间中一个唯一元素的内积。

让我们从最简单的标量提升算子开始。考虑一个单元 $K$ 上的有限维多项式空间 $V_h(K)$，它配备了标准的 $L^2(K)$ 内积 $(\cdot, \cdot)_K$。对于任意定义在单元边界 $\partial K$ 上的函数 $g \in L^2(\partial K)$，我们可以定义一个线性泛函 $v \mapsto \langle g, v \rangle_{\partial K}$，其中 $\langle \cdot, \cdot \rangle_{\partial K}$ 是边界上的 $L^2$ 对偶。根据Riesz表示定理，存在一个唯一的元素，我们记为 $L_{\partial K} g \in V_h(K)$，使得对于所有检验函数 $v \in V_h(K)$，以下关系成立：

$$
\big(L_{\partial K} g, v\big)_K = \langle g, v \rangle_{\partial K}
$$

这个方程定义了**边界提升算子** $L_{\partial K}: L^2(\partial K) \to V_h(K)$ [@problem_id:3396012]。它将边界数据 $g$ “提升”到了单元内部。

**示例：一维 $\mathbb{P}_1$ 单元上的提升**

为了更具体地理解这个定义，让我们计算一个简单的情形。考虑一维参考单元 $K=[-1,1]$，其上的逼近空间为 $V_h = \mathbb{P}_1(K)$，即最多一次的多项式空间。我们选择一组基 $\{\phi_0(x), \phi_1(x)\} = \{1, x\}$。我们希望计算在右侧面 $F=\{1\}$ 上常数值 $g=1$ 的提升 $L_F(g)$ [@problem_id:3395997]。

根据定义，我们要寻找一个线性多项式 $L_F(g)(x) = c_0 + c_1 x$，使得对于所有 $v \in V_h$：

$$
\int_{-1}^{1} (c_0 + c_1 x) v(x) \, dx = \int_{\{1\}} 1 \cdot v(s) \, ds = v(1)
$$

我们只需对基函数 $v=\phi_0(x)=1$ 和 $v=\phi_1(x)=x$ 强制该方程成立。

当 $v(x) = 1$ 时：
$$
\int_{-1}^{1} (c_0 + c_1 x) \cdot 1 \, dx = 1 \implies [c_0 x + c_1 \frac{x^2}{2}]_{-1}^{1} = 1 \implies 2c_0 = 1
$$

当 $v(x) = x$ 时：
$$
\int_{-1}^{1} (c_0 + c_1 x) \cdot x \, dx = 1 \implies [c_0 \frac{x^2}{2} + c_1 \frac{x^3}{3}]_{-1}^{1} = 1 \implies \frac{2}{3}c_1 = 1
$$

这个线性方程组可以写作矩阵形式 $\mathbf{M} \mathbf{c} = \mathbf{b}$，其中 $\mathbf{M}$ 是质量矩阵：

$$
\begin{pmatrix}
\int_K \phi_0 \phi_0 dx & \int_K \phi_0 \phi_1 dx \\
\int_K \phi_1 \phi_0 dx & \int_K \phi_1 \phi_1 dx
\end{pmatrix}
\begin{pmatrix} c_0 \\ c_1 \end{pmatrix}
=
\begin{pmatrix}
\phi_0(1) \\ \phi_1(1)
\end{pmatrix}
\implies
\begin{pmatrix} 2 & 0 \\ 0 & \frac{2}{3} \end{pmatrix}
\begin{pmatrix} c_0 \\ c_1 \end{pmatrix}
=
\begin{pmatrix} 1 \\ 1 \end{pmatrix}
$$

解得 $c_0 = \frac{1}{2}$ 和 $c_1 = \frac{3}{2}$。因此，所求的提升函数是：

$$
L_F(g)(x) = \frac{1}{2} + \frac{3}{2}x
$$

这个具体的例子清晰地展示了如何通过求解一个与质量矩阵相关的线性系统来确定提升算子的作用。

**向量值提升算子与内部面**

在处理像扩散问题这样的二阶偏微分方程时，我们更关心的是法向通量的积分。这需要定义一个**向量值提升算子**。对于单元 $K$ 的一个面 $F \subset \partial K$，我们定义 $r_F^K: L^2(F) \to [V_h(K)]^d$ (其中 $[V_h(K)]^d$ 是 $d$ 维向量值多项式空间)，使得对于所有向量检验函数 $\mathbf{w} \in [V_h(K)]^d$：

$$
(r_F^K g, \mathbf{w})_K = \langle g, \mathbf{w} \cdot \mathbf{n}_K \rangle_F
$$

这里 $\mathbf{n}_K$ 是 $F$ 上指向 $K$ 外部的单位法向量。

对于DG方法至关重要的**内部面** $F = \partial K^+ \cap \partial K^-$，提升算子 $R_F$ 自然地通过叠加相邻单元的贡献来定义。我们将 $R_F g$ 定义在单元片 $\omega_F = K^+ \cup K^-$ 上，其在 $K^\pm$ 上的限制就是 $r_F^{K^\pm} g$。这通常简写为 $R_F g = r_F^{K^+} g + r_F^{K^-} g$。其关键性质是 [@problem_id:3395996]：

$$
(R_F g, \mathbf{w})_{\omega_F} = (r_F^{K^+} g, \mathbf{w}|_{K^+})_{K^+} + (r_F^{K^-} g, \mathbf{w}|_{K^-})_{K^-} = \langle g, (\mathbf{w}|_{K^+}) \cdot \mathbf{n}_{K^+} \rangle_F + \langle g, (\mathbf{w}|_{K^-}) \cdot \mathbf{n}_{K^-} \rangle_F
$$

注意到内部面上法向量方向相反，即 $\mathbf{n}_{K^-} = -\mathbf{n}_{K^+}$，上式可以写成检验函数跳跃的形式：

$$
(R_F g, \mathbf{w})_{\omega_F} = \langle g, (\mathbf{w}|_{K^+} - \mathbf{w}|_{K^-}) \cdot \mathbf{n}_{K^+} \rangle_F = \langle g, [\![\mathbf{w}]\!] \cdot \mathbf{n}_{K^+} \rangle_F
$$

其中 $[\![\mathbf{w}]\!]$ 表示 $\mathbf{w}$ 穿过面 $F$ 的跳跃。这个关系是提升算子理论的基石，它揭示了提升算子如何自然地将检验函数的**跳跃**编码到体积分中。

### 基本性质与应用

**守恒的转换：抵消性质**

理解提升算子的一个核心要点是，它被构造出来的目的就是为了精确地替代一个面积分项。这意味着，由提升算子产生的体积分项和它所替代的面积分项在数值上是相等且符号相反的（取决于定义）。考虑这样一个表达式 [@problem_id:3395988]：

$$
S = \int_{K} r_{F}(\psi_{F}) \cdot \boldsymbol{\tau} \, dx + \int_{F} \psi_{F} \, \boldsymbol{\tau} \cdot \mathbf{n}_{K} \, ds
$$

其中，提升算子 $r_F$ 的定义（可能带有负号）为 $(\int_{K} r_{F}(\psi_{F}) \cdot \boldsymbol{\tau} \, dx = - \int_{F} \psi_{F} \, \boldsymbol{\tau} \cdot \mathbf{n}_{K} \, ds)$。根据这个定义，我们立刻可以看到 $S = 0$。这并不是一个巧合，而是提升算子定义的直接推论。它强调了提升算子是一种**等效表示**，而不是引入了新的物理或数值效应。它仅仅是将边界上的信息以一种体积守恒的方式转移到了单元内部。

**应用：边界条件的弱施加**

提升算子的一个直接应用是通过体积项来**弱施加**狄利克雷（Dirichlet）边界条件，例如在Nitsche方法中。对称Nitsche方法的 bilinear form 中包含了如下的边界项：

$$
-\langle \kappa \nabla u_h \cdot \mathbf{n}, v_h \rangle_{\partial \Omega} - \langle \kappa \nabla v_h \cdot \mathbf{n}, u_h \rangle_{\partial \Omega} + \langle (\eta/h) u_h, v_h \rangle_{\partial \Omega}
$$

使用我们之前定义的标量边界提升算子 $L_{\partial K}$，这些面积分可以逐单元地转化为体积分 [@problem_id:3396012]：

$$
-\big(L_{\partial K}(\kappa \nabla u_h \cdot \mathbf{n}), v_h\big)_K - \big(L_{\partial K}(\kappa \nabla v_h \cdot \mathbf{n}), u_h\big)_K + \big(L_{\partial K}((\eta/h) u_h), v_h\big)_K
$$

这种转换使得边界条件的处理可以完全整合到单元的体积分计算中，简化了代码结构，并为某些高级方法（如静态凝聚）提供了便利。然而，需要注意的是，提升算子本身只是一种表示工具，它并不能替代罚函数 $\langle (\eta/h) u_h, v_h \rangle_{\partial \Omega}$ 在保证 coercivity（矫顽性）方面的作用。

**稳定性界**

提升算子的一个重要理论性质是其范数界。通过其Riesz表示定义和标准的迹不等式（trace inequality）与逆迹不等式（inverse trace inequality），我们可以推导出其算子范数的尺度行为。对于定义在单元 $K$ 上的提升算子 $L_{\partial K}$，其范数满足以下基于逆迹不等式的稳定性界 [@problem_id:3396012]：

$$
\|L_{\partial K} g\|_{0,K} \le C h_K^{-1/2} \|g\|_{0,\partial K}
$$

其中 $\|\cdot\|_{0,K}$ 和 $\|\cdot\|_{0,\partial K}$ 分别是单元和边界上的 $L^2$ 范数，$h_K$ 是单元直径，$C$ 是一个不依赖于 $h_K$ 的常数。这个 $h_K^{-1/2}$ 的尺度因子在DG方法的稳定性与收敛性分析中扮演着至关重要的角色，它确保了提升项与梯度项在能量范数中的尺度平衡。

### 提升算子在DG格式中的应用

提升算子不仅是分析DG方法的工具，更是构建DG格式的核心组件。

**与对称内罚伽辽金法（SIPG）的联系**

对称内罚伽辽金法（Symmetric Interior Penalty Galerkin, SIPG）是求解椭圆问题的经典DG方法。其双线性形式包含四部分：体梯度项、两个对称的相容性项和一个罚项。对于泊松方程，内部面上的积分项为：

$$
- \sum_{F \in \mathcal{F}_i} \int_F \{\nabla u_h\} \cdot \mathbf{n}_F \, [v_h] \, ds - \sum_{F \in \mathcal{F}_i} \int_F \{\nabla v_h\} \cdot \mathbf{n}_F \, [u_h] \, ds + \sum_{F \in \mathcal{F}_i} \int_F \frac{\eta_F}{h_F} \, [u_h] \, [v_h] \, ds
$$

其中 $\{\cdot\}$ 和 $[\cdot]$ 分别代表平均和跳跃。有趣的是，前两个相容性项可以被一个提升算子等效表示。如果我们定义一个提升算子 $R_h$ ，它将**函数跳跃**提升为一个向量场，其性质由下式定义 [@problem_id:3395987]：

$$
\int_{\Omega} R_h [\phi] \cdot \boldsymbol{\tau}_h \, dx = - \sum_{F \in \mathcal{F}_i} \int_F [\phi] \, \{\boldsymbol{\tau}_h \cdot \boldsymbol{n}_F\} \, ds
$$

那么，SIPG的两个相容性项就可以精确地写成体积分形式：

$$
\int_{\Omega} \nabla u_h \cdot R_h [v_h] \, dx + \int_{\Omega} \nabla v_h \cdot R_h [u_h] \, dx
$$

这表明，SIPG方法可以被看作是一个在体梯度项的基础上，通过提升算子引入体积校正的格式。

**Bassi–Rebay 2 (BR2) 格式**

与SIPG不同，Bassi–Rebay 2 (BR2) 格式是一种**原生**使用提升算子构建的DG方法。其双线性形式直接定义为 [@problem_id:3396013]：

$$
a(u_h, v_h) = \sum_{K \in \mathcal{T}_h} (\nabla u_h, \nabla v_h)_K - \sum_{F \in \mathcal{F}_i} (r_F[u_h], \nabla v_h)_{\omega_F} - \sum_{F \in \mathcal{F}_i} (r_F[v_h], \nabla u_h)_{\omega_F} + \sum_{F \in \mathcal{F}_i} \eta_F (r_F[u_h], r_F[v_h])_{\omega_F}
$$

这里的 $r_F$ 是将函数跳跃 $[u_h]$ 提升为向量场的算子。前三项共同确保了相容性和对称性，而最后一项是稳定项，它惩罚的是**提升后的跳跃**，而非跳跃本身。

**稳定化方法的等价性**

尽管SIPG的罚项和BR2的稳定项形式不同（前者作用于面上的函数跳跃，后者作用于体内的提升函数），它们在本质上是等价的。考虑一个简单的一维双单元、分片常数逼近问题，我们可以分别计算SIPG罚项和BR2稳定项对应的刚度矩阵 [@problem_id:3396032]。

SIPG罚项为 $\sigma [u][v] = \sigma(u_1-u_2)(v_1-v_2)$，其矩阵为：
$$
A_{SIPG} = \sigma \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$

BR2稳定项为 $\mu \int_{\Omega} R_F[u] R_F[v] dx$。对于分片常数函数，可以计算出 $R_F[u]$ 在整个区域上是一个常数 $-\frac{[u]}{2h}$。因此，稳定项等于 $\frac{\mu}{2h}[u][v]$，其矩阵为：
$$
A_{BR2} = \frac{\mu}{2h} \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix}
$$

显然，这两个矩阵仅相差一个系数。如果我们选择稳定参数使得两种方法的稳定化能量相等，即 $\sigma = \frac{\mu}{2h}$，那么它们的代数贡献是完全相同的。这揭示了不同DG稳定化机制之间的深刻联系。

**BR2方法的矫頑性**

BR2方法的稳定性分析也依赖于提升算子的性质。为了保证双线性形式 $a(v_h, v_h)$ 的正定性，我们需要选择合适的稳定参数 $\eta_F$。通过对 $a(v_h, v_h)$ 应用柯西-施瓦茨不等式，我们可以得到一个关于 broken gradient 范数 $X = \|\nabla_h v_h\|_{L^2(\Omega)}$ 和提升跳跃范数 $Y = (\sum_F \|r_F[v_h]\|^2_{\omega_F})^{1/2}$ 的二次型 [@problem_id:3396013]：

$$
a(v_h, v_h) \ge X^2 - 2\sqrt{d}XY + \eta Y^2
$$
(在二维，$d=2$的特殊情况下，可以得到更紧的界，例如在特定的网格上是 $X^2 - 2\sqrt{3}XY + \eta Y^2$)。为使该二次型非负，其判别式必须非正，这要求 $\eta$ 足够大。对于二维非钝角三角形组成的网格，可以证明保证矫顽性的最小稳定参数为 $\eta=3$。这个结果对于DG方法的理论分析和参数选择至关重要。

### 高级主题与计算方面

**计算实现**

在实际计算中，我们如何应用提升算子？我们需要求解一个与质量矩阵相关的线性系统。从向量值提升算子的定义出发：

$$
(r_{F}(g), \mathbf{w})_{K} = \langle g, \mathbf{w}\cdot\mathbf{n}_{F}\rangle_{F}
$$

将 $r_F(g)$ 和 $\mathbf{w}$ 用基函数展开，$r_F(g) = \sum_j \boldsymbol{\rho}_j \boldsymbol{\psi}_j$ 和 $\mathbf{w} = \boldsymbol{\psi}_i$，并假设面函数 $g$ 也用面基底展开 $g = \sum_q \mathbf{g}_q \phi_q$，我们可以得到如下的离散线性系统 [@problem_id:3396020]：

$$
M_{K} \boldsymbol{\rho} = C_{F}^{\top} \mathbf{g}
$$

其中 $M_K$ 是单元 $K$ 上的向量值质量矩阵，其元素为 $(M_K)_{ij} = (\boldsymbol{\psi}_i, \boldsymbol{\psi}_j)_K$，而 $C_F$ 是耦合矩阵，其元素为 $(C_F)_{qi} = \langle \phi_q, \boldsymbol{\psi}_i \cdot \mathbf{n}_F \rangle_F$。

这个代数形式揭示了一个关键的计算优势：质量矩阵 $M_K$ 只依赖于单元 $K$ 的几何和基函数，而与具体哪个面 $F$ 无关。因此，对于每个单元，我们可以预先计算并存储 $M_K$ 的逆或LU分解。这样，对于该单元的**每一个面**，计算提升算子所需的边际成本就只是构造右端项 $C_F^\top \mathbf{g}$（一次矩阵-向量乘法）和求解线性系统（一次矩阵-向量乘法或前后代入），其复杂度约为 $\mathcal{O}(N_K^2)$，其中 $N_K$ 是单元上的自由度数量。这使得基于提升算子的方法在计算上非常高效。

**与可杂交DG（HDG）方法的关系**

提升算子还揭示了DG方法不同变体之间的深层联系，特别是与**可杂交不连续伽遼金（Hybridizable Discontinuous Galerkin, HDG）** 方法的关系。HDG方法引入了一个定义在网格骨架（所有面的集合）上的全局未知量——数值迹 $\hat{u}_h$，以此为“粘合剂”将原本相互独立的单元问题耦合起来。HDG的局部问题在每个单元上求解，而全局耦合仅发生在骨架上，这使其非常适合并行计算和静态凝聚。

一个深刻的洞察是，HDG方法可以通过代数操作（静态凝聚）与原始的DG格式相互转化。具体来说，如果我们从HDG格式中**消去**杂交变量 $\hat{u}_h$，我们就可以得到一个仅含体未知量 $(u_h, \mathbf{q}_h)$ 的全局DG系统 [@problem_id:3396001]。

在这个消去过程中，HDG中起稳定作用的项 $\langle \tau(u_h - \hat{u}_h), v_h \rangle_{\partial K}$ 会被转化为体积分形式的耦合项。这些新产生的体积项，其作用完全类似于传统DG方法中对面函数跳跃进行提升所产生的校正项。换句话说，HDG中的面残差 $u_h - \hat{u}_h$ 扮演了类似于原始DG方法中跳跃 $[u_h]$ 的角色，而消去 $\hat{u}_h$ 的过程在代数上等价于对这个面残差进行提升。

我们可以通过一个简单的一维问题来验证这种等价性 [@problem_id:3395993]。考虑一个双单元区间上的扩散问题，我们可以分别用HDG和原始DG（如SIPG）方法求解。通过静态凝聚，两种方法都可以化简为一个关于界面上单个未知量 $\lambda$ 的 $1 \times 1$ 系统。计算表明，两种方法得到的刚度系数完全相同（例如，均为 $\frac{2}{h}$）。这雄辩地证明了HDG方法在凝聚後等价于一种特定的、基于提升算子的原始DG方法，从而将这两种看似不同的DG方法统一在了一个共同的理论框架之下。

总而言之，提升算子不仅是一种将面积分转化为体积分的计算技巧，它更是一种深刻的理论工具，揭示了不同DG格式的内在结构和等价性，并为DG方法的稳定性分析和高效实现提供了坚实的基础。