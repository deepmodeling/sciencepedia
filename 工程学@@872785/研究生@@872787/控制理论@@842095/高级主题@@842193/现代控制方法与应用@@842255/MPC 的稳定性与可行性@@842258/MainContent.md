## 引言
[模型预测控制](@entry_id:146965)（MPC）作为一种先进的控制策略，在学术界和工业界都获得了巨大的成功。其核心优势在于其前瞻性的优化能力：通过在线反复求解一个基于系统模型的有限时域[优化问题](@entry_id:266749)，MPC能够显式地处理[多变量系统](@entry_id:169616)的复杂耦合以及各种硬约束，从而在满足安全规范的同时实现最优性能。然而，这种基于滚动优化的方法引出了一系列深刻的理论问题：我们如何确保在每个控制周期，[优化问题](@entry_id:266749)都总能找到一个解？更重要的是，由这一系列局部最优决策构成的闭环系统，其[长期行为](@entry_id:192358)是否稳定？

本文旨在系统性地解答这两个根本问题，深入剖析保证MPC控制器**[递归可行性](@entry_id:167169)（Recursive Feasibility）**和**[闭环稳定性](@entry_id:265949)（Closed-loop Stability）**的理论基石。我们的探讨将分为三个层次，从核心原理逐步走向前沿应用与实践。

在“**原理与机制**”章节中，我们将奠定理论基础。您将学习到MPC[优化问题](@entry_id:266749)的规范化表述，并理解[终端约束](@entry_id:176488)集、终端[代价函数](@entry_id:138681)和[不变性](@entry_id:140168)等关键概念是如何协同工作，从而通过严谨的数学论证，确保控制器永远不会“卡住”（[递归可行性](@entry_id:167169)），并引导系统状态收敛至期望的目标（[渐近稳定性](@entry_id:149743)）。

接下来，在“**应用与[交叉](@entry_id:147634)学科联系**”章节中，我们将展示这些核心原理的强大扩展性。您将看到如何将基础理论进行调整和应用，以应对现实世界中的各种复杂挑战，包括如何设计[鲁棒MPC](@entry_id:174393)来对抗外部干扰和[模型不确定性](@entry_id:265539)，如何通过[经济MPC](@entry_id:174671)实现超越常规设定点跟踪的经济效益优化，以及如何处理时滞、混合逻辑等复杂动态系统。

最后，“**动手实践**”部分将理论付诸于行。通过一系列精心设计的编程练习和计算问题，您将亲手实现和验证本文所学的核心概念，例如计算[不变集](@entry_id:275226)、构造李雅普诺夫函数以及近似[可行域](@entry_id:136622)，从而将抽象的理论转化为具体可感的工程技能。

现在，让我们从最根本的机制出发，深入探索MPC得以可靠运行的内在原理。

## 原理与机制

在“引言”章节中，我们介绍了[模型预测控制](@entry_id:146965)（MPC）的基本思想：在每个时间步，求解一个有限时域[优化问题](@entry_id:266749)，并将所得控制序列的第一个元素施加于系统。这种滚动优化的方法赋予了MPC处理约束和非线性系统的强大能力。然而，为了确保这种控制策略不仅有效，而且可靠和稳定，我们必须深入研究其内在的原理和机制。本章将系统地阐述保证MPC控制器**[递归可行性](@entry_id:167169)（Recursive Feasibility）**和**[闭环稳定性](@entry_id:265949)（Closed-loop Stability）**的核心理论。

### 有限时域[最优控制](@entry_id:138479)问题的规范化表述

[模型预测控制](@entry_id:146965)的核心是一个反复求解的有限时域[最优控制](@entry_id:138479)问题（Finite-Horizon Optimal Control Problem, FHOCP）。为了严谨地分析其性质，我们首先需要精确地定义这个问题。

考虑一个离散时间非线性系统，其动态由状态[更新方程](@entry_id:264802)描述：
$$
x_{k+1} = f(x_k, u_k)
$$
其中 $x_k \in \mathbb{R}^n$ 是系统状态， $u_k \in \mathbb{R}^m$ 是控制输入。系统运行受到[状态和](@entry_id:193625)输入约束的限制，即 $x_k \in \mathcal{X}$ 和 $u_k \in \mathcal{U}$，其中 $\mathcal{X}$ 和 $\mathcal{U}$ 分别是包含原点的[紧致集](@entry_id:147575)。

在每个时刻 $k$，给定当前状态 $x_k$，MPC控制器求解一个[预测时域](@entry_id:261473)为 $N$ 的[优化问题](@entry_id:266749)。该问题旨在最小化一个累积[代价函数](@entry_id:138681)，该函数由**阶段代价（stage cost）** $\ell(x, u)$ 和**终端代价（terminal cost）** $V_f(x)$ 组成。此外，为了保证特定的性质，我们通常会施加一个**[终端约束](@entry_id:176488)（terminal constraint）**，要求预测的最终状态 $x_N$ 必须位于一个预先定义的**[终端集](@entry_id:163892)（terminal set）** $\mathcal{X}_f \subseteq \mathcal{X}$ 内。

这个问题有两种等价的数学表述 [@problem_id:2746588]。第一种是将[状态和](@entry_id:193625)输入序列都作为决策变量：

**表述一：状态与输入联合优化**
$$
\begin{align*}
V_N(x) = \min_{\substack{x_0, \dots, x_N \\ u_0, \dots, u_{N-1}}}  \quad \sum_{i=0}^{N-1} \ell(x_i, u_i) + V_f(x_N) \\
\text{s.t.}  \quad x_0 = x, \\
 \quad x_{i+1} = f(x_i, u_i),  i \in \{0, \dots, N-1\}, \\
 \quad x_i \in \mathcal{X},  i \in \{0, \dots, N-1\}, \\
 \quad u_i \in \mathcal{U},  i \in \{0, \dots, N-1\}, \\
 \quad x_N \in \mathcal{X}_f.
\end{align*}
$$

第二种表述则认识到状态序列完全由初始状态 $x$ 和输入序列 $\{u_0, \dots, u_{N-1}\}$ 唯一确定，因此只将输入序列作为决策变量：

**表述二：仅输入优化**
$$
\begin{align*}
V_N(x) = \min_{u_0, \dots, u_{N-1}}  \quad \sum_{i=0}^{N-1} \ell(x_i, u_i) + V_f(x_N) \\
\text{s.t.}  \quad x_0 = x, \\
 \quad x_{i+1} = f(x_i, u_i),  i \in \{0, \dots, N-1\}, \\
 \quad x_i \in \mathcal{X},  i \in \{1, \dots, N-1\}, \\
 \quad u_i \in \mathcal{U},  i \in \{0, \dots, N-1\}, \\
 \quad x_N \in \mathcal{X}_f.
\end{align*}
$$

在这两种表述中，函数 $V_N(x)$ 被称为**值函数（value function）**，它表示从初始状态 $x$ 出发所能达到的最小代价。如果对于某个状态 $x$，不存在满足所有约束的控制序列，则称该问题是**不可行（infeasible）**的，并定义 $V_N(x) = +\infty$。

假设[优化问题](@entry_id:266749)在时刻 $k$ 的解（即[最优控制](@entry_id:138479)序列）为 $\mathbf{u}_k^\star = \{u_0^\star, u_1^\star, \dots, u_{N-1}^\star\}$。MPC的**[滚动时域](@entry_id:181425)（receding horizon）**策略仅将此序列的第一个元素施加于系统，即 $u_k = u_0^\star$。这个过程定义了一个隐式的[状态反馈控制](@entry_id:271611)律 $\kappa_N(x) = u_0^\star(x)$。在下一时刻 $k+1$，系统到达新状态 $x_{k+1}$，整个优化过程将再次重复。

### [递归可行性](@entry_id:167169)：运行的保障

一个首要且基本的问题是：如果MPC[优化问题](@entry_id:266749)在当前时刻是可行的，我们能否保证在施加控制后，在下一时刻它仍然是可行的？如果不能，控制器可能会在未来的某个时刻“卡住”，无法找到任何满足约束的控制动作，这将导致控制任务失败。

**可行性（Feasibility）**在时刻 $k$ 意味着，对于当前状态 $x_k$，存在至少一个控制序列 $\{u_{i|k}\}_{i=0}^{N-1}$ 能够使得预测的状态轨迹满足所有状态、输入及[终端约束](@entry_id:176488) [@problem_id:2746593]。

**[递归可行性](@entry_id:167169)（Recursive Feasibility）**则是一个更强的性质，它要求：如果问题在时刻 $k$ 对于状态 $x_k$ 是可行的，并且我们施加了[最优控制](@entry_id:138479)序列的第一个元素 $u_k = u_{0|k}^\star$ 得到新状态 $x_{k+1}$，那么问题在时刻 $k+1$ 对于状态 $x_{k+1}$ 必须仍然是可行的 [@problem_id:2746593]。[递归可行性](@entry_id:167169)是MPC能够持续运行的根本保障。

#### [终端集](@entry_id:163892)与[不变性](@entry_id:140168)：可行性的机制

保证[递归可行性](@entry_id:167169)的关键机制在于对终端状态施加约束，即要求 $x_N \in \mathcal{X}_f$。这个[终端集](@entry_id:163892) $\mathcal{X}_f$ 并非任意选择，它必须具备特定的性质，即**不变性（invariance）**。

[不变性](@entry_id:140168)的核心思想是，一旦系统的状态进入了某个“安全”的集合，我们总有办法通过施加允许的控制，使其未来的状态继续保持在该集合内。这为[预测时域](@entry_id:261473)的“接力”提供了保障。

我们定义以下几种[不变性](@entry_id:140168)概念 [@problem_id:2746570]：

-   **（受控）不变性（Control Invariance）**：一个集合 $\mathcal{S} \subseteq \mathcal{X}$ 被称为受控不变的，如果对于每一个状态 $x \in \mathcal{S}$，都**存在**一个容许的控制 $u \in \mathcal{U}$，使得系统的下一个状态 $f(x, u)$ 仍然在 $\mathcal{S}$ 内。即，$\forall x \in \mathcal{S}, \exists u \in \mathcal{U} \text{ s.t. } f(x, u) \in \mathcal{S}$。

-   **正不变性（Positive Invariance）**：如果存在一个固定的[反馈控制](@entry_id:272052)律 $u = \kappa(x)$，对于集合 $\mathcal{S}$ 中的所有状态 $x \in \mathcal{S}$，施加该控制后满足 $\kappa(x) \in \mathcal{U}$ 且下一个状态 $f(x, \kappa(x))$ 仍然在 $\mathcal{S}$ 内，则称集合 $\mathcal{S}$ 在闭环动态 $x_{k+1} = f(x_k, \kappa(x_k))$ 下是正不变的。这是受控不变性的一个更强的、更具建设性的形式。

在存在不确定性（如扰动 $w \in \mathcal{W}$）的系统中，我们还需要更强的鲁棒[不变性](@entry_id:140168)概念：

-   **鲁棒正[不变性](@entry_id:140168)（Robust Positive Invariance, RPI）**：对于一个给定的反馈律 $u = \kappa(x)$，如果对于**所有** $x \in \mathcal{S}$ 和**所有**可能的扰动 $w \in \mathcal{W}$，下一个状态 $f(x, \kappa(x)) + w$ 都依然在 $\mathcal{S}$ 内，则称集合 $\mathcal{S}$ 是鲁棒正不变的。

#### “[移位](@entry_id:145848)-附加”论证

现在我们来阐明一个不变的[终端集](@entry_id:163892)如何保证[递归可行性](@entry_id:167169)。这个证明的核心是一种构造性的方法，称为**“[移位](@entry_id:145848)-附加”（shift-and-append）**论证 [@problem_id:2746593]。

假设在时刻 $k$，对于状态 $x_k$，我们找到了一个最优的[可行解](@entry_id:634783)，包括输入序列 $\{u_{0|k}^\star, \dots, u_{N-1|k}^\star\}$ 和状态序列 $\{x_{0|k}^\star, \dots, x_{N|k}^\star\}$。根据定义，这个解满足所有约束，特别是 $x_{N|k}^\star \in \mathcal{X}_f$。

控制器施加 $u_k = u_{0|k}^\star$，系统到达新状态 $x_{k+1} = f(x_k, u_k) = x_{1|k}^\star$。现在我们需要证明，在时刻 $k+1$ 求解以 $x_{k+1}$ 为初始状态的[优化问题](@entry_id:266749)时，至少存在一个可行解。

我们可以构造一个**候选解（candidate solution）**如下：
1.  **移位（Shift）**：取时刻 $k$ 最优解的“尾巴”，即 $\{u_{1|k}^\star, \dots, u_{N-1|k}^\star\}$，作为新问题的前 $N-1$ 个控制输入。
2.  **附加（Append）**：在序列的末尾附加一个新的控制输入。这个输入由一个预先设计的**终端控制器（terminal controller）** $\kappa_f: \mathcal{X}_f \to \mathcal{U}$ 给出，即 $u_{N-1|k+1}^c = \kappa_f(x_{N|k}^\star)$。

构造出的候选输入序列为 $\{u_{1|k}^\star, \dots, u_{N-1|k}^\star, \kappa_f(x_{N|k}^\star)\}$。现在我们检查这个候选解是否可行：
-   **输入约束**：$\{u_{1|k}^\star, \dots, u_{N-1|k}^\star\}$ 来自一个[可行解](@entry_id:634783)，因此它们满足输入约束。要使整个序列可行，我们必须要求终端控制器对于[终端集](@entry_id:163892)内的所有状态都满足输入约束，即 $\kappa_f(\mathcal{X}_f) \subseteq \mathcal{U}$。
-   **状态约束**：对应的状态序列的前 $N-1$ 个状态为 $\{x_{2|k}^\star, \dots, x_{N|k}^\star\}$，它们同样来自一个[可行解](@entry_id:634783)，故满足状态约束。
-   **[终端约束](@entry_id:176488)**：最关键的一步是检查新的终端状态。新的终端状态是 $x_{N|k+1}^c = f(x_{N|k}^\star, \kappa_f(x_{N|k}^\star))$。为了满足[终端约束](@entry_id:176488) $x_{N|k+1}^c \in \mathcal{X}_f$，我们必须要求对于任意 $x \in \mathcal{X}_f$，都有 $f(x, \kappa_f(x)) \in \mathcal{X}_f$。这正是我们之前定义的，$\mathcal{X}_f$ 在终端控制律 $\kappa_f$ 下是**正不变的**。

综上所述，只要我们设计的[终端集](@entry_id:163892) $\mathcal{X}_f$ 在终端控制器 $\kappa_f$ 的作用下是正不变的，并且 $\kappa_f$ 的输出满足输入约束，我们总能从上一时刻的最优解构造出下一时刻的一个可行解。这便证明了**[递归可行性](@entry_id:167169)**。这个结论也适用于时域长度缩减的情况，例如从 $N$ 变为 $N-1$，因为原解的尾部自然构成了一个长度为 $N-1$ 的可行轨迹 [@problem_id:2746590]。

### [闭环稳定性](@entry_id:265949)：收敛的保障

保证了控制器能够持续运行后，下一个核心问题是：[闭环系统](@entry_id:270770)是否稳定？特别是，对于镇定问题（stabilization problem），我们希望系统状态能收敛到原点。

证明MPC[闭环稳定性](@entry_id:265949)的标准方法是证明其值函数 $V_N(x)$ 是系统的一个**李雅普诺夫函数（Lyapunov function）**。这意味着我们需要证明：
1.  $V_N(x)$ 是正定的（即 $V_N(0)=0$ 且当 $x \neq 0$ 时 $V_N(x) > 0$）。
2.  $V_N(x)$ 沿着[闭环系统](@entry_id:270770)的轨迹是严格递减的（即当 $x_k \neq 0$ 时 $V_N(x_{k+1})  V_N(x_k)$）。

第一点通常通过合理设计[代价函数](@entry_id:138681)来保证。例如，如果阶段代价 $\ell(x,u)$ 是正定的（即 $\ell(x,u)0$ 除非 $x=0, u=0$），且终端代价 $V_f(x)$ 是非负的，那么 $V_N(x)$ 显然是正定的。

关键在于证明第二点：值的递减性。

#### [控制李雅普诺夫函数](@entry_id:164136)：稳定性的机制

与[递归可行性](@entry_id:167169)一样，稳定性的保障也深植于终端代价 $V_f(x)$ 和[终端集](@entry_id:163892) $\mathcal{X}_f$ 的设计之中。具体来说，我们需要终端[代价函数](@entry_id:138681) $V_f(x)$ 在[终端集](@entry_id:163892) $\mathcal{X}_f$ 上扮演一个**[控制李雅普诺夫函数](@entry_id:164136)（Control Lyapunov Function, CLF）**的角色。

一个函数 $V_f: \mathcal{X}_f \to \mathbb{R}_{\ge 0}$ 被称为在[终端集](@entry_id:163892) $\mathcal{X}_f$ 上关于终端控制器 $\kappa_f$ 的一个CLF，如果它是正定的，并且满足以下关键的**李雅普诺夫递减不等式（Lyapunov decrease inequality）** [@problem_id:2746605]：
$$
V_f(f(x, \kappa_f(x))) - V_f(x) \le -\ell(x, \kappa_f(x)) \quad \forall x \in \mathcal{X}_f
$$
这个不等式要求，在[终端集](@entry_id:163892)内，施加终端控制律 $\kappa_f$ 后，终端代价值的单步减小量至少要比该步产生的阶段代价值 $\ell(x, \kappa_f(x))$ 还要多。

#### MP[C值](@entry_id:272975)函数的递减性证明

现在，我们利用这个CLF性质来证明MP[C值](@entry_id:272975)函数 $V_N(x)$ 的递减性。我们再次使用“移位-附加”论证中构造的候选解 [@problem_id:2746594]。

在时刻 $k+1$，值函数 $V_N(x_{k+1})$ 的值必然小于或等于任何可行候选解的代价值。使用我们构造的候选解，其代价值为：
$$
J_{\text{cand}}(x_{k+1}) = \sum_{i=1}^{N-1} \ell(x_{i|k}^\star, u_{i|k}^\star) + \ell(x_{N|k}^\star, \kappa_f(x_{N|k}^\star)) + V_f(f(x_{N|k}^\star, \kappa_f(x_{N|k}^\star)))
$$
时刻 $k$ 的最[优值函数](@entry_id:173036)为：
$$
V_N(x_k) = \ell(x_{0|k}^\star, u_{0|k}^\star) + \sum_{i=1}^{N-1} \ell(x_{i|k}^\star, u_{i|k}^\star) + V_f(x_{N|k}^\star)
$$
由于 $V_N(x_{k+1}) \le J_{\text{cand}}(x_{k+1})$，我们可以得到 $V_N(x_{k+1}) - V_N(x_k)$ 的上界：
$$
\begin{align*}
V_N(x_{k+1}) - V_N(x_k)  \le J_{\text{cand}}(x_{k+1}) - V_N(x_k) \\
 \le -\ell(x_{0|k}^\star, u_{0|k}^\star) + \left[ V_f(f(x_{N|k}^\star, \kappa_f(x_{N|k}^\star))) - V_f(x_{N|k}^\star) + \ell(x_{N|k}^\star, \kappa_f(x_{N|k}^\star)) \right]
\end{align*}
$$
观察方括号内的项。根据CLF的定义，我们有 $V_f(f(x_{N|k}^\star, \kappa_f(x_{N|k}^\star))) - V_f(x_{N|k}^\star) \le -\ell(x_{N|k}^\star, \kappa_f(x_{N|k}^\star))$。因此，方括号内的项小于等于零。

这立即导出了最终的关键不等式：
$$
V_N(x_{k+1}) - V_N(x_k) \le -\ell(x_{0|k}^\star, u_{0|k}^\star) = -\ell(x_k, u_k)
$$
由于阶段代价 $\ell(x,u)$ 是正定的，只要 $x_k \neq 0$，就有 $\ell(x_k, u_k)  0$，从而 $V_N(x_{k+1})  V_N(x_k)$。这证明了 $V_N(x)$ 是[闭环系统](@entry_id:270770)的严格李雅普诺夫函数，从而保证了系统的**[渐近稳定性](@entry_id:149743)（asymptotic stability）**。

### 稳定MPC的统一框架

综上所述，为了设计一个能够保证[递归可行性](@entry_id:167169)和[渐近稳定性](@entry_id:149743)的（[非线性](@entry_id:637147)）MPC控制器，我们需要系统地设计一套“终端组件” [@problem_id:2746599]。一个充分的条件集包括：
1.  **阶段代价** $\ell(x,u)$：连续且正定。
2.  **[终端集](@entry_id:163892)** $\mathcal{X}_f$：一个包含原点的[紧致集](@entry_id:147575)。
3.  **终端控制器** $\kappa_f(x)$：定义在 $\mathcal{X}_f$ 上的一个反馈律。
4.  **终端代价** $V_f(x)$：定义在 $\mathcal{X}_f$ 上的一个[连续函数](@entry_id:137361)。

这些组件必须协同工作，满足以下三个核心条件：
-   **输入[约束满足](@entry_id:275212)**: 对于所有 $x \in \mathcal{X}_f$，$\kappa_f(x) \in \mathcal{U}$。
-   **不变性**: 对于所有 $x \in \mathcal{X}_f$， $f(x, \kappa_f(x)) \in \mathcal{X}_f$。
-   **CLF递减条件**: 对于所有 $x \in \mathcal{X}_f$， $V_f(f(x, \kappa_f(x))) - V_f(x) \le -\ell(x, \kappa_f(x))$。

只要满足这些条件，从[可行域](@entry_id:136622)内的任意初始状态出发，MPC控制器就能保证[闭环系统](@entry_id:270770)始终满足约束，并渐近收敛到原点。[可行域](@entry_id:136622)（或称[吸引域](@entry_id:172179)，Region of Attraction）由所有能够被控制到[终端集](@entry_id:163892) $\mathcal{X}_f$ 的初始状态组成，可以表示为 $N \to \infty$ 时 $N$ 步可行集的并集 [@problem_id:2746607]。

### [线性系统](@entry_id:147850)终端组件的系统化设计

对于线性时不变（LTI）系统 $x_{k+1} = Ax_k + Bu_k$ 和二次型代价函数 $\ell(x,u) = x^\top Qx + u^\top Ru$ ($Q \succeq 0, R \succ 0$)，上述终端组件的设计有非常成熟和系统的方法。

#### DARE：终端代价和控制器的最优选择

对于[LTI系统](@entry_id:271946)，一个绝佳的选择是使用与系统和[代价函数](@entry_id:138681)相关的**离散时间代数里卡提方程（Discrete-time Algebraic Riccati Equation, DARE）**的解来构造终端组件 [@problem_id:2746567]。DARE方程如下：
$$
P = A^\top P A - (A^\top P B)(R+B^\top P B)^{-1}(B^\top P A) + Q
$$
如果 $(A,B)$ 是可镇定的，DARE存在唯一的半正定解 $P_{\text{DARE}}$。我们可以选择：
-   **终端控制器**: $K_{\text{LQR}} = -(R+B^\top P_{\text{DARE}} B)^{-1}B^\top P_{\text{DARE}} A$。这正是无限时域LQR（Linear Quadratic Regulator）的最优[反馈增益](@entry_id:271155)。
-   **终端代价**: $V_f(x) = x^\top P_{\text{DARE}} x$。

这个选择的精妙之处在于，DARE方程本身可以被改写为：
$$
x^\top(A+BK_{\text{LQR}})^\top P_{\text{DARE}} (A+BK_{\text{LQR}})x - x^\top P_{\text{DARE}} x = - (x^\top Qx + x^\top K_{\text{LQR}}^\top R K_{\text{LQR}} x)
$$
这等价于：
$$
V_f((A+BK_{\text{LQR}})x) - V_f(x) = -\ell(x, K_{\text{LQR}}x)
$$
这意味着，CLF递减条件不仅在[终端集](@entry_id:163892) $\mathcal{X}_f$ 内成立，而是在整个状态空间 $\mathbb{R}^n$ 内都**以等式形式成立**。这为[终端集](@entry_id:163892)的设计提供了极大的便利。

#### [终端集](@entry_id:163892)的构造与计算

选择了基于DARE的终端代价和控制器后，我们只需要构造一个满足约束的、在闭环动态 $x_{k+1} = (A+BK_{\text{LQR}})x_k$ 下的正[不变集](@entry_id:275226) $\mathcal{X}_f$。

理论上，最大的[终端集](@entry_id:163892)是满足[状态和](@entry_id:193625)输入约束的集合 $S_{\text{constr}} = \{ x \in \mathcal{X} \mid K_{\text{LQR}}x \in \mathcal{U} \}$ 内部的**最大正[不变集](@entry_id:275226)（Maximal Positively Invariant set）**。相比之下，如果采用一个“手动调整”的、仅在局部满足CLF条件的终端代价 $\tilde{P}$，那么[终端集](@entry_id:163892)必须被限制在 $S_{\text{constr}}$ 和CLF条件成立区域的交集内，这通常会导致一个更小的[终端集](@entry_id:163892)，从而缩小MPC的[吸引域](@entry_id:172179) [@problem_id:2746567]。

在实践中，我们通常选择一个简单形状的集合（如椭球或多胞体）作为 $\mathcal{X}_f$，并调整其大小以满足[不变性](@entry_id:140168)和约束条件。例如，我们可以选择一个椭球 $\mathcal{X}_f = \{x \mid x^\top P x \le \alpha\}$，其中 $P=P_{\text{DARE}}$。为了使其成为一个有效的[终端集](@entry_id:163892)，我们需要找到最大的 $\alpha  0$，使得对于所有 $x \in \mathcal{X}_f$：
1.  $x \in \mathcal{X}$ (状态约束)
2.  $K_{\text{LQR}}x \in \mathcal{U}$ (输入约束)
3.  $(A+BK_{\text{LQR}})x \in \mathcal{X}_f$ ([不变性](@entry_id:140168))

例如，考虑一个二维系统，状态约束为 $|x_1| \le 0.6, |x_2| \le 0.5$，输入约束为 $|u| \le 1$。终端控制器为 $K = \begin{pmatrix} 1  2 \end{pmatrix}$，终端[代价矩阵](@entry_id:634848)为 $P = \begin{pmatrix} 4  1 \\ 1  1 \end{pmatrix}$。要确定椭球 $\mathcal{X}_f = \{x \mid x^\top P x \le \alpha\}$ 的最大尺寸 $\alpha$，我们需要确保椭球完全包含在由约束定义的区域内 [@problem_id:2746612]。这可以通过求解一系列凸[优化问题](@entry_id:266749)（最大化线性函数在椭球上的值）来完成。对于这个具体例子，通过计算可得，为同时满足所有约束，$\alpha$ 的最大值为 $\frac{3}{16}$。

另一个具体的例子是标量系统 $x_{k+1} = 1.5x_k + u_k$，约束为 $|x| \le 10, |u| \le 2$，[终端集](@entry_id:163892)为原点 $\{0\}$。其[可行域](@entry_id:136622)（[吸引域](@entry_id:172179)）的边界可以通过递归计算得出，极限半径 $r_\infty = 4$ [@problem_id:2746607]。这意味着任何初始状态 $|x_0| \le 4$ 都可以通过MPC被稳定地控制到原点。

通过本章的探讨，我们不仅理解了保证MPC可行性与稳定性的深刻原理，还掌握了将这些原理应用于实际系统设计的系统性方法。这些机制是现代先进控制实践的基石。