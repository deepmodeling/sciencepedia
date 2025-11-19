## 引言
在众多科学与工程领域中，如何在不确定的动态环境下做出最优决策是一个核心且普遍的挑战。[随机最优控制](@entry_id:190537)为解决此类问题提供了一个强大而严谨的数学框架，它研究如何设计控制策略以引导一个受随机噪声干扰的系统，使其在满足特定约束的同时，达成预设的最优性能指标。然而，从理论上精确刻画并求解这些[最优策略](@entry_id:138495)，尤其是在连续时间下，需要一套复杂的分析工具。本文旨在系统性地攻克这一难题，为读者构建一个关于[随机最优控制](@entry_id:190537)与动态规划的完整知识体系。

本文将分为三个核心部分。首先，在“原理与机制”章节中，我们将深入探讨[随机最优控制](@entry_id:190537)的理论基石，从受控[随机微分方程](@entry_id:146618)的严格定义出发，详细阐述动态规划原理（DPP）、哈密顿-[雅可比](@entry_id:264467)-贝尔曼（HJB）方程的推导与验证，并介绍处理非光滑问题的黏性解理论，以及提供最优性必要条件的庞特里亚金最大值原理（PMP）。接着，在“应用与[交叉](@entry_id:147634)学科联系”章节中，我们将展示这些理论如何在[控制工程](@entry_id:149859)（如著名的LQG问题与分离原理）、金融经济学和数理生物学等领域转化为解决实际问题的有力工具，揭示其广泛的适用性。最后，“动手实践”部分将通过一系列精心设计的问题，引导读者动手实践，加深对核心概念的理解。

现在，让我们从构建这一理论大厦的基础开始，深入探索其核心的原理与机制。

## 原理与机制

在介绍了[随机最优控制](@entry_id:190537)的基本概念之后，本章将深入探讨其核心理论支柱：动态规划原理（Dynamic Programming Principle, DPP）与哈密顿-雅可比-贝尔曼（Hamilton-Jacobi-Bellman, HJB）方程。我们将从严格定义受控随机系统开始，逐步建立这些基本原理，并探讨其在经典解和更广泛的黏性解（viscosity solution）框架下的应用。此外，我们还将介绍另一套重要的[最优性条件](@entry_id:634091)——随机庞特里亚金最大值原理（Stochastic Pontryagin's Maximum Principle），并讨论松弛控制（relaxed control）这一确保最优解存在的理论工具。

### 受控随机系统：严格定义

[随机最优控制](@entry_id:190537)问题的核心是描述在一个不确定环境下，决策如何影响系统状态的演化。这个系统通常由一个受控的伊藤（Itô）[随机微分方程](@entry_id:146618)（SDE）来建模。

考虑一个在时间区间 $[0,T]$ 上的受控[扩散过程](@entry_id:170696) $X_t$，其状态位于 $\mathbb{R}^n$。其动态由以下SDE描述：
$$
\mathrm{d}X_t = b(t, X_t, a_t)\,\mathrm{d}t + \sigma(t, X_t, a_t)\,\mathrm{d}W_t, \quad X_0 = x
$$
这里，$W_t$ 是在一个给定的带滤（filtered）概率空间 $(\Omega, \mathcal{F}, \mathbb{F}, \mathbb{P})$ 上定义的 $d$ 维标准布朗运动，其中滤 $\mathbb{F} = (\mathcal{F}_t)_{t \in [0,T]}$ 满足通常条件（即，它是右连续的，且 $\mathcal{F}_0$ 包含所有 $\mathbb{P}$-零测集）。过程 $a_t$ 是控制过程，其取值于一个给定的控制集 $A \subset \mathbb{R}^m$。系数 $b: [0,T] \times \mathbb{R}^n \times A \to \mathbb{R}^n$ 称为[漂移系数](@entry_id:199354)，$\sigma: [0,T] \times \mathbb{R}^n \times A \to \mathbb{R}^{n \times d}$ 称为[扩散](@entry_id:141445)系数。

上述[微分形式](@entry_id:146747)是随机积分方程的一个简写。严格来说，一个受控扩散过程是一个 $\mathbb{F}$-适应的连续过程 $X=(X_t)_{t\in[0,T]}$，它几乎必然地满足以下积分方程 [@problem_id:2998149]：
$$
X_t = x + \int_0^t b(s, X_s, a_s)\,\mathrm{d}s + \int_0^t \sigma(s, X_s, a_s)\,\mathrm{d}W_s, \quad t \in [0,T]
$$

为了使这个方程有意义，特别是为了让伊藤积分 $\int \sigma \,\mathrm{d}W_s$ 得到良好定义，控制过程 $a_t$ 必须满足特定的[可测性条件](@entry_id:197557)。一个基本要求是 **非预见性（non-anticipativity）**，即在时刻 $t$ 的控制决策 $a_t$ 不能依赖于未来的信息。在数学上，这通常意味着 $a_t$ 对每个 $t$ 都是 $\mathcal{F}_t$-可测的，这样的过程称为 **适应的（adapted）**。然而，为了保证伊藤积分的良好性质，我们需要一个更强的条件：被积函数，即过程 $\sigma(s, X_s, a_s)$，必须是 **循序可测的（progressively measurable）**。

一个过程 $(Z_t)_{t \ge 0}$ 被称为循序可测的，如果对于每一个 $t \ge 0$，映射 $(s, \omega) \mapsto Z_s(\omega)$ 在 $[0,t] \times \Omega$ 上是 $\mathcal{B}([0,t]) \otimes \mathcal{F}_t$-可测的 [@problem_id:2998152]。这个条件比适应性更强，它保证了过程在时间和概率空间上的联合可测性。幸运的是，一个重要的定理指出，如果一个[适应过程](@entry_id:187710)的样本[轨道](@entry_id:137151)几乎必然是右连续或左连续的，那么它就是循序可测的。由于SDE的解通常是连续路径的，只要控制过程 $a_t$ 本身是循序可测的，并且系数 $b$ 和 $\sigma$ 是[Borel可测](@entry_id:140719)的，那么复合过程 $b(t, X_t, a_t)$ 和 $\sigma(t, X_t, a_t)$ 也将是循序可测的。因此，我们将 **容许控制（admissible control）** 定义为一个取值于 $A$ 的 $\mathbb{F}$-循序可测过程 $a_t$，并满足一定的可积性条件，例如：
$$
\mathbb{E}\left[\int_0^T \left( \| \sigma(t, X_t, a_t) \|^2 + | b(t, X_t, a_t) | \right)\,\mathrm{d}t\right]  \infty
$$

为了保证对于任意给定的容许控制 $a_t$，SDE都存在唯一的 **[强解](@entry_id:198344)（strong solution）**（即，在一个预先固定的[概率空间](@entry_id:201477)和布朗运动上定义的解），我们通常对系数施加更强的条件。标准的充分条件是 $b$ 和 $\sigma$ 关于[状态变量](@entry_id:138790) $x$ 满足 **一致全局[Lipschitz连续性](@entry_id:142246)** 和 **一致线性增长** 条件 [@problem_id:2998149]。也就是说，存在常数 $L, C > 0$，使得对于所有 $t \in [0,T]$，$x, y \in \mathbb{R}^n$ 和 $a \in A$：
$$
|b(t,x,a)-b(t,y,a)| + \|\sigma(t,x,a)-\sigma(t,y,a)\| \le L|x-y|
$$
$$
|b(t,x,a)| + \|\sigma(t,x,a)\| \le C(1+|x|)
$$
在这些条件下，对于每个容许控制，都存在唯一的[强解](@entry_id:198344) $X_t$。这是[随机控制](@entry_id:170804)的 **强表述（strong formulation）**，其中噪声源 $W_t$ 是固定的。相对地，**弱表述（weak formulation）** 则不[固定概率](@entry_id:178551)空间和布朗运动，而是将它们作为解的一部分，控制策略实质上是选择过程的定律（law）。在弱表述中，控制影响的是过程的局部特征——漂移和扩散矩阵，这等价于解决一个受控的[鞅问题](@entry_id:204145)（martingale problem）[@problem_id:2998155]。除非特别说明，本书主要采用强表述。

### 动态规划原理 (DPP)

[随机最优控制](@entry_id:190537)的目标是选择一个容许控制 $a_\cdot$，以最小化（或最大化）一个给定的性能指标或[成本泛函](@entry_id:268062) $J$。一个典型的形式是：
$$
J(t,x;a) := \mathbb{E}\left[ \int_t^T \ell(s, X_s^{t,x,a}, a_s)\,\mathrm{d}s + g(X_T^{t,x,a}) \right]
$$
其中 $\ell$ 是运行成本， $g$ 是终端成本，$X_s^{t,x,a}$ 表示从时刻 $t$ 和状态 $x$ 出发，在控制 $a$ 下的系统状态。**值函数（value function）** $V(t,x)$ 被定义为在所有容许控制下的最优成本：
$$
V(t,x) := \inf_{a \in \mathcal{A}_t} J(t,x;a)
$$
其中 $\mathcal{A}_t$ 表示从时刻 $t$ 开始的容许控制集合。

动态规划原理是联系不同时间和状态下值函数的核心关系。其基本思想是“[最优策略](@entry_id:138495)的任何一部分仍然是最优的”。对于一个固定的时间步长 $h > 0$，DPP可以表述为：
$$
V(t,x) = \inf_{a \in \mathcal{A}_t} \mathbb{E}\left[ \int_t^{t+h} \ell(s, X_s, a_s)\,\mathrm{d}s + V(t+h, X_{t+h}) \right]
$$
这个等式表明，从 $(t,x)$ 开始的最优成本，等于在初始小段时间 $[t, t+h]$ 上选择最优控制的成本，加上在 $t+h$ 时刻到达新状态 $X_{t+h}$ 后继续执行[最优策略](@entry_id:138495)的未来成本 $V(t+h, X_{t+h})$ 的[期望值](@entry_id:153208)。

这个原理可以被推广到任意的 $\mathbb{F}$-停时 $\tau$，其取值在 $[t,T]$ 区间内。这个更强大的版本是证明和推导理论结果的关键。推广后的DPP表述为 [@problem_id:2998160]：
$$
V(t,x) = \inf_{a \in \mathcal{A}_t} \mathbb{E}\left[ \int_t^{\tau} \ell(s, X_s^{t,x,a}, a_s)\,\mathrm{d}s + V(\tau, X_{\tau}^{t,x,a}) \right]
$$
为了使这一原理的证明严谨，我们需要能够在一个随机时刻 $\tau$ 将两个不同的控制策略“拼接”起来。给定两个容许控制 $a, b \in \mathcal{A}_t$ 和一个停时 $\tau$，我们可以定义一个新的拼接控制 $c = a \otimes_{\tau} b$，它在 $[t, \tau)$ 上遵循 $a$，在 $[\tau, T]$ 上遵循 $b$。其[路径依赖](@entry_id:138606)的定义为：
$$
(a \otimes_{\tau} b)_s(\omega) := a_s(\omega)\,\mathbf{1}_{[t, \tau(\omega))}(s) + b_s(\omega)\,\mathbf{1}_{[\tau(\omega), T]}(s)
$$
可以证明，如果 $a$ 和 $b$ 是容许的（即循序可测的），那么拼接后的控制 $c$ 也是容许的。这个构造是证明DPP和后续理论的基石。

### 哈密顿-[雅可比](@entry_id:264467)-贝尔曼 (HJB) 方程

动态规划原理描述了值函数在有限时间间隔上的性质。通过取一个无穷小的时间间隔 $h \to 0$，我们可以推导出值函数应满足的一个[偏微分方程](@entry_id:141332)（PDE），即哈密顿-[雅可比](@entry_id:264467)-贝尔曼（HJB）方程。

假设值函数 $V(t,x)$ 足够光滑（例如，$V \in C^{1,2}([0,T] \times \mathbb{R}^n)$），我们可以对 $V(t, X_t)$ 应用伊藤公式。从DPP出发，经过一系列推导 [@problem_id:2998182]，我们得到[HJB方程](@entry_id:140124)：
$$
\frac{\partial V}{\partial t} + \inf_{a \in A} \left\{ \mathcal{L}^a V(t,x) + \ell(t,x,a) \right\} = 0
$$
其中 $\mathcal{L}^a$ 是与控制值 $a$ 相关的二阶[微分算子](@entry_id:140145)，定义为：
$$
\mathcal{L}^a \phi(x) = b(t,x,a) \cdot \nabla_x \phi(x) + \frac{1}{2} \text{Tr}\left( \sigma(t,x,a) \sigma(t,x,a)^T \nabla_x^2 \phi(x) \right)
$$
这里 $\nabla_x \phi$ 是 $\phi$ 关于 $x$ 的梯度，$\nabla_x^2 \phi$ 是其Hessian矩阵。[HJB方程](@entry_id:140124)必须在区域 $[0,T) \times \mathbb{R}^n$ 内满足，并配上终端条件 $V(T,x) = g(x)$。

为了以更紧凑的形式书写[HJB方程](@entry_id:140124)，我们引入 **[哈密顿量](@entry_id:172864)（Hamiltonian）** $H$。在[随机控制](@entry_id:170804)中，[哈密顿量](@entry_id:172864)通常被定义为在控制变量上进行优化的项。对于一个依赖于状态 $x$ 和“协态”变量 $p$（它将对应于值函数的梯度 $\nabla_x V$）的[哈密顿量](@entry_id:172864)，其定义为 [@problem_id:2998182]：
$$
H(t,x,p) = \inf_{a \in A} \left\{ b(t,x,a) \cdot p + \ell(t,x,a) \right\}
$$
注意，这个定义仅包含了对控制有显式依赖的项。更广义的[哈密顿量](@entry_id:172864)可以包含二阶项，但上述形式在与庞特里亚金最大值原理的联系中尤为重要。使用这个定义，并将[扩散](@entry_id:141445)项中不受控制影响的部分分离出来（如果 $\sigma$ 不依赖于 $a$），[HJB方程](@entry_id:140124)可以写为：
$$
\frac{\partial V}{\partial t} + \frac{1}{2} \text{Tr}\left( \sigma\sigma^T \nabla_x^2 V \right) + H(t,x,\nabla_x V) = 0
$$
这个[非线性偏微分方程](@entry_id:169481)是[随机最优控制](@entry_id:190537)的核心。它将一个无穷维的[优化问题](@entry_id:266749)（在函数空间上寻找最优控制过程）转化为了一个有限维的（虽然可能是[非线性](@entry_id:637147)的）PDE求解问题。

### [验证定理](@entry_id:185180)

[HJB方程](@entry_id:140124)为我们提供了一个候选值函数应满足的条件。但反过来，如果我们找到了一个满足[HJB方程](@entry_id:140124)的函数，我们如何能确定它就是真正的值函数，并如何从中找到[最优控制](@entry_id:138479)呢？**[验证定理](@entry_id:185180)（Verification Theorem）** 回答了这个问题，它为我们提供了一套充分条件。

一个典型的[验证定理](@entry_id:185180)陈述如下 [@problem_id:2998173]：

假设我们找到了一个函数 $\tilde{V} \in C^{1,2}([0,T] \times \mathbb{R}^n)$，它满足以下条件：
1.  **[HJB方程](@entry_id:140124)**：对于所有 $(t,x) \in [0,T) \times \mathbb{R}^n$，
    $$
    \frac{\partial \tilde{V}}{\partial t}(t,x) + \inf_{u \in A} \left\{ \mathcal{L}^u \tilde{V}(t,x) + \ell(t,x,u) \right\} = 0
    $$
2.  **终端条件**：对于所有 $x \in \mathbb{R}^n$，$\tilde{V}(T,x) = g(x)$。
3.  **最优控制的存在性**：存在一个可测的反馈函数 $u^*(t,x)$，使得对于每个 $(t,x)$，它都能实现上述[HJB方程](@entry_id:140124)中的[下确界](@entry_id:140118)。即，$u^*(t,x)$ 是[哈密顿量](@entry_id:172864)的极小化子。
4.  **[闭环系统](@entry_id:270770)的[适定性](@entry_id:148590)**：由[反馈控制](@entry_id:272052) $u_t^* = u^*(t,X_t)$ 定义的闭环SDE
    $$
    \mathrm{d}X_t = b(t,X_t,u^*(t,X_t))\,\mathrm{d}t + \sigma(t,X_t,u^*(t,X_t))\,\mathrm{d}W_t
    $$
    存在唯一的[强解](@entry_id:198344)。

如果这些条件都满足，那么我们可以得出结论：
-   对于任何容许控制 $u$，成本 $J(t,x;u) \ge \tilde{V}(t,x)$。
-   对于由 $u^*$ 生成的[反馈控制](@entry_id:272052)，成本 $J(t,x;u^*) = \tilde{V}(t,x)$。

因此，$\tilde{V}(t,x)$ 就是真正的最[优值函数](@entry_id:173036)，即 $\tilde{V}(t,x) = V(t,x)$，并且 $u^*$ 是一个最优反馈控制策略。

这个定理的证明核心在于对过程 $M_t = \tilde{V}(t,X_t) + \int_s^t \ell(r,X_r,u_r)\mathrm{d}r$ 应用伊藤公式。可以证明，对于任意控制 $u$，$M_t$ 是一个[下鞅](@entry_id:263978)（submartingale）；而对于[最优控制](@entry_id:138479) $u^*$，$M_t$ 是一个[鞅](@entry_id:267779)（martingale）。这个性质直接导出了上述的不等式和等式。

### 黏性解与[比较原理](@entry_id:165563)

[验证定理](@entry_id:185180)的一个主要障碍是它要求值函数 $V$ 是 $C^{1,2}$ 的，即经典解。然而，在许多实际问题中，由于控制的切换或状态约束等原因，值函数可能不够光滑，甚至在某些点上不可微。例如，[最优控制](@entry_id:138479)可能在某个边界上从一个值跳变到另一个值，导致值函数的导数出现不连续（即产生“扭结”）。

为了处理这类非光滑的值函数，20世纪80年代发展出了 **黏性解（viscosity solution）** 理论。其核心思想是，不再要求函数逐点满足PDE（这需要导数存在），而是通过一组光滑的“测试函数”来“探测”函数是否满足PDE的某种弱形式。

- **黏性子解（Viscosity Subsolution）**：一个上半连续（usc）函数 $V$ 是[HJB方程](@entry_id:140124) $F(t,x,V,D_tV, D_xV, D_{xx}^2V)=0$ 的一个黏性子解，如果在任何一点 $(t,x)$，只要有一个[光滑函数](@entry_id:267124) $\varphi \in C^{1,2}$ 从上方“接触”$V$（即 $V-\varphi$ 在 $(t,x)$ 达到局部最大值且 $V(t,x)=\varphi(t,x)$），那么在这一点上，测试函数 $\varphi$ 的导数必须满足 $F(t,x,V,D_t\varphi, D_x\varphi, D_{xx}^2\varphi) \le 0$ [@problem_id:2998132]。

- **黏性超解（Viscosity Supersolution）**：类似地，一个下半连续（lsc）函数 $V$ 是一个黏性超解，如果在任何一点 $(t,x)$，只要有一个光滑函数 $\varphi$ 从下方“接触”$V$（即 $V-\varphi$ 在 $(t,x)$ 达到局部最小值），那么必须有 $F(t,x,V,D_t\varphi, D_x\varphi, D_{xx}^2\varphi) \ge 0$ [@problem_id:2998132]。

一个函数如果既是黏性子解又是黏性超解，就被称为 **黏性解**。一个关键的理论结果是，在相当普适的条件下，[随机最优控制](@entry_id:190537)问题的值函数是其对应[HJB方程](@entry_id:140124)的唯一黏性解。

黏性解理论的基石是 **[比较原理](@entry_id:165563)（Comparison Principle）**。它指出，如果 $u$ 是一个黏性子解，$v$ 是一个黏性超解，并且在区域的（抛物）边界上有 $u \le v$，那么在整个区域内部也必然有 $u \le v$ [@problem_id:2998143]。这个原理保证了黏性[解的唯一性](@entry_id:143619)：如果 $V_1$ 和 $V_2$ 都是黏性解且在边界上相等，那么根据[比较原理](@entry_id:165563)，既有 $V_1 \le V_2$ 又有 $V_2 \le V_1$，从而 $V_1=V_2$。正是这种唯一性使得我们可以将值函数与[HJB方程](@entry_id:140124)的黏性解等同起来，从而为非光滑问题提供了坚实的理论基础。

### 随机庞特里亚金[最大值原理](@entry_id:138611) (PMP)

除了基于动态规划和[HJB方程](@entry_id:140124)的方法，还有一种源于[变分法](@entry_id:163656)的强大工具——庞特里亚金最大值原理。其随机版本为[随机最优控制](@entry_id:190537)问题提供了一套 **必要条件**。

与寻找值函数的HJB方法不同，PMP直接刻画最优控制 $u^*$ 和最优状态 $X^*$ 的性质。它引入了一组伴随过程（adjoint processes），$(p_t, q_t)$，其中 $p_t \in \mathbb{R}^n$ 是协态过程， $q_t \in \mathbb{R}^{n \times d}$ 是其[鞅表示](@entry_id:182858)的一部分。这两个过程满足一个 **[倒向随机微分方程](@entry_id:200232)（Backward Stochastic Differential Equation, BSDE）**。

对于在 [@problem_id:2998137] 中定义的[哈密顿量](@entry_id:172864) $H(t,x,u,p,q) = \ell(t,x,u) + p^\top b(t,x,u) + \text{Tr}(q^\top \sigma(t,x,u))$，随机PMP可以表述为：如果 $u^*$ 是最优控制，$X^*$ 是对应的最优状态，那么存在唯一的[适应过程](@entry_id:187710)对 $(p_t, q_t)$ 满足以下BSDE：
$$
\mathrm{d}p_t = -H_x(t, X_t^*, u_t^*, p_t, q_t)\,\mathrm{d}t + q_t\,\mathrm{d}W_t
$$
其中 $H_x$ 是[哈密顿量](@entry_id:172864)关于[状态变量](@entry_id:138790) $x$ 的梯度。这个方程需要配上一个终端条件：
$$
p_T = g_x(X_T^*)
$$
此外，[最优控制](@entry_id:138479) $u_t^*$ 必须在每个时刻[几乎必然](@entry_id:262518)地满足一个关于[哈密顿量](@entry_id:172864)的优化条件。如果控制集 $A$ 是凸的，这个条件表现为一个[变分不等式](@entry_id:172788) [@problem_id:2998137]：
$$
\langle H_u(t, X_t^*, u_t^*, p_t, q_t), v - u_t^* \rangle \ge 0, \quad \text{for all } v \in A
$$
其中 $H_u$ 是[哈密顿量](@entry_id:172864)关于[控制变量](@entry_id:137239) $u$ 的梯度。这个条件直观地意味着，在最优控制 $u_t^*$ 处，[哈密顿量](@entry_id:172864)沿任何指向控制集内部的[可行方向](@entry_id:635111)的导数都必须是非负的。如果 $u_t^*$ 位于 $A$ 的内部，该条件简化为 $H_u(t, X_t^*, u_t^*, p_t, q_t) = 0$。

PMP提供了一套强大的必要条件，它将[最优控制](@entry_id:138479)问题转化为求解一个由前向SDE（[状态方程](@entry_id:274378)）和后向SDE（伴随方程）耦合在一起的系统，这被称为[前向-后向随机微分方程](@entry_id:635996)组（FBSDE）。

### 松弛控制

在某些情况下，一个[最优控制](@entry_id:138479)问题可能没有经典意义上的最优解。例如，如果控制集 $A$ 非凸，或者[成本函数](@entry_id:138681)关于控制 $a$ 的行为很“剧烈”，那么最小化序列可能不会收敛到 $A$ 中的一个点。为了解决这个问题并建立一个更完整的存在性理论，引入了 **松弛控制（relaxed controls）** 的概念。

一个松弛控制 $\mu_t$ 是一个取值于控制集 $A$ 上的[概率测度](@entry_id:190821)空间 $\mathcal{P}(A)$ 的过程 [@problem_id:2998134]。直观上，它允许在每个瞬间以一种“加权平均”的方式同时使用多个经典控制。例如，一个松弛控制可以是 $\mu_t = 0.5\delta_{a_1} + 0.5\delta_{a_2}$，表示在时刻 $t$ “一半用 $a_1$，一半用 $a_2$”。

在松弛控制下，系统的动态不是通过简单地平均系数来定义的。特别地，直接平均[扩散](@entry_id:141445)系数 $\sigma(x,\mu_t) = \int_A \sigma(x,a)\,\mu_t(\mathrm{d}a)$ 是错误的，因为它没有正确地处理二次变差。正确的做法是平均生成元（generator），这等价于平均漂移项和 **[协方差矩阵](@entry_id:139155)** [@problem_id:2998134]：
- 平均漂移：$b(x, \mu) = \int_A b(x,a)\,\mu(\mathrm{d}a)$
- 平均协方差矩阵：$q(x,\mu) = \int_A \sigma(x,a)\sigma(x,a)^\top\,\mu(\mathrm{d}a)$

松弛系统的动态对应于一个漂移为 $b(x,\mu_t)$、[扩散矩阵](@entry_id:182965)为 $q(x,\mu_t)$ 的过程。同样，[成本泛函](@entry_id:268062)中的运行成本也通过积分来定义：$\ell(x,\mu_t) = \int_A \ell(x,a)\,\mu_t(\mathrm{d}a)$。

松弛控制理论的一个基本结果是，在相当普遍的条件下（例如，控制集 $A$ 紧凑，系数连续），松弛控制问题的最优值与原始严格控制问题的最优值是相等的 [@problem_id:2998134]。即，
$$
\inf_{a \text{ is strict}} J(a) = \inf_{\mu \text{ is relaxed}} J(\mu)
$$
此外，由于 $\mathcal{P}(A)$ 具有良好的紧性和[凸性](@entry_id:138568)，松弛控制问题通常保证存在一个最优解。这使得松弛控制成为证明[最优控制](@entry_id:138479)存在性和分析最优值性质的强大理论工具。