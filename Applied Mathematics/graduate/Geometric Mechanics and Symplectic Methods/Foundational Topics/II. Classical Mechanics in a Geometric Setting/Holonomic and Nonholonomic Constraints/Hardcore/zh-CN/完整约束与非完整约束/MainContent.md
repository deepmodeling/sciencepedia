## 引言
在力学世界中，约束无处不在，它们是塑造系统运动行为的无形规则。从行星沿轨道运行到机器人在复杂环境中导航，约束从根本上限制了系统的可能性，并要求我们超越牛顿力学的传统框架。区分完整约束（可积分为位置约束）与非完整约束（不可积的速度约束）是理解这些系统的第一步，但其背后蕴含着深刻的几何结构与动力学后果，这正是本篇文章旨在解决的核心问题。

本文将带领读者深入几何力学的腹地，系统性地揭示约束的本质。在“**原理与机制**”一章中，我们将学习如何使用流形、分布和[李括号](@entry_id:636461)等几何语言来精确描述和区分两类约束，并探讨[Lagrange-d'Alembert原理](@entry_id:1126999)与Vakonomic原理等不同动力学框架的微妙之处。接下来，在“**应用与跨学科联系**”一章中，我们将把这些抽象理论应用于现实世界，考察[非完整约束](@entry_id:167828)如何在[机器人运动规划](@entry_id:162933)中实现“不可能”的运动，如何改变分子动力学模拟的统计基础，以及如何打破力学中神圣的对称性-守恒律关系。最后，通过“**动手实践**”中的一系列引导性问题，读者将有机会亲手计算[约束力](@entry_id:170052)、推导约束流形，从而将理论知识内化为解决实际问题的能力。通过这一趟旅程，我们不仅将掌握分析约束系统的工具，更将领略到几何学如何为物理学提供深刻的洞察力。

## 原理与机制

在力学系统的研究中，**约束** (constraints) 是指对系统运动状态（如位置或速度）施加的限制。这些限制从根本上改变了系统的动力学行为，并要求我们发展新的数学框架来描述其运动。本章将从[几何力学](@entry_id:169959)的视角出发，系统地阐述约束的分类、动力学原理以及相应的哈密顿形式。

### 约束的几何描述

从几何角度看，约束将系统的运动限制在[位形空间](@entry_id:149531)或相空间的一个子集上。约束的性质，特别是其[可积性](@entry_id:142415)，决定了系统的基本动力学特征。

#### [完整约束](@entry_id:140686)作为[子流形](@entry_id:159439)

最简单的一类约束是**[完整约束](@entry_id:140686)** (holonomic constraints)，它们可以表示为仅依赖于系统[广义坐标](@entry_id:156576) $q \in Q$ 的[函数方程](@entry_id:199663)。给定一个 $n$ 维光滑位形流形 $Q$ 和一个[光滑映射](@entry_id:203730) $f: Q \to \mathbb{R}^r$，一组完整约束可以写作 $f(q) = 0$。如果 $f$ 的[微分](@entry_id:158422) $df$ 在约束集 $\mathcal{C} = \{ p \in Q \mid f(p) = 0 \}$ 上是满秩的（即秩为 $r$），那么根据[正则值定理](@entry_id:158611)，$\mathcal{C}$ 是 $Q$ 的一个 $n-r$ 维光滑子流形。

系统的运动被完全限制在该[子流形](@entry_id:159439) $\mathcal{C}$ 上。因此，在任意一点 $q \in \mathcal{C}$，系统允许的[瞬时速度](@entry_id:167797)（即[切向量](@entry_id:265494)）必须位于 $\mathcal{C}$ 的切空间 $T_q\mathcal{C}$ 内。一个[切向量](@entry_id:265494) $v \in T_qQ$ 属于 $T_q\mathcal{C}$ 的条件可以通过考虑一条位于 $\mathcal{C}$ 内且通过 $q$ 点的曲线 $\gamma(t)$ 推导得出。设 $\gamma(0) = q$ 且 $\dot{\gamma}(0) = v$。由于对所有 $t$，都有 $f(\gamma(t)) = 0$，应用[链式法则](@entry_id:190743)可得：
$$
\frac{d}{dt} (f \circ \gamma)(t) \Big|_{t=0} = df_q(\dot{\gamma}(0)) = df_q(v) = 0
$$
这意味着[切空间](@entry_id:199137) $T_q\mathcal{C}$ 是[微分](@entry_id:158422)映射 $df_q: T_qQ \to \mathbb{R}^r$ 的核（kernel）。若将 $f$ 写为分量形式 $f=(f^1, \dots, f^r)$，则该条件等价于一组[线性方程](@entry_id:151487)：
$$
T_q\mathcal{C} = \{ v \in T_qQ \mid df^i_q(v) = 0 \text{ for all } i = 1, \dots, r \}
$$
根据[秩-零度定理](@entry_id:154441)，$\dim(T_q\mathcal{C}) = \dim(\ker(df_q)) = \dim(T_qQ) - \mathrm{rank}(df_q) = n-r$，这与[子流形](@entry_id:159439) $\mathcal{C}$ 的维数相符。

如果位形流形 $Q$ 配备了黎曼度规 $g$，我们可以引入一个更有物理意义的视角。度规 $g$ 在每个[切空间](@entry_id:199137) $T_qQ$ 和其[余切空间](@entry_id:270516) $T_q^*Q$ 之间建立了一个[典范同构](@entry_id:202335)。对于每个约束函数 $f^i$，其[微分](@entry_id:158422) $df^i_q$ 是一个 [1-形式](@entry_id:270392)（co-vector）。我们可以定义其对应的**[梯度向量](@entry_id:141180)** (gradient vector) $\nabla f^i(q) \in T_qQ$，它满足：
$$
g_q(\nabla f^i(q), v) = df^i_q(v) \quad \forall v \in T_qQ
$$
利用这个关系，允许速度 $v$ 所满足的条件 $df^i_q(v)=0$ 可以重写为：
$$
g_q(v, \nabla f^i(q)) = 0 \quad \text{for all } i = 1, \dots, r
$$
这个方程表明，允许速度向量 $v$ 必须与所有约束函数的[梯度向量](@entry_id:141180)正交。换言之，$T_q\mathcal{C}$ 是由[梯度向量](@entry_id:141180) $\{\nabla f^i(q)\}_{i=1}^r$ 张成的空间在 $T_qQ$ 中的[正交补](@entry_id:149922)空间。这为我们提供了一个关键的物理图像：约束力（将在后面讨论）正比于[梯度向量](@entry_id:141180)，因此总是垂直于约束[子流形](@entry_id:159439)，不对任何允许的运动做功 。

#### [非完整约束](@entry_id:167828)作为分布

许多力学系统，例如滚动接触问题，其约束涉及速度，并且不能被积分为纯粹依赖于坐标的形式。这类约束被称为**非完整约束** (nonholonomic constraints)。最常见的一类是线性速度约束，其形式为 $A(q)\dot{q}=0$。

在几何上，这样一组 $m$ 个独立的线性速度约束在位形流形 $Q$ 的每一点 $q$ 定义了一个切空间 $T_qQ$ 的一个子空间 $D(q)$。这个子空间集合 $D = \bigcup_{q \in Q} D(q)$ 被称为一个**分布** (distribution)。具体而言，如果约束由 $m$ 个光滑的 1-形式 $\omega^1, \dots, \omega^m$ 给出，则在每一点 $q$，允许的速度 $v$ 必须满足：
$$
\omega^a(q)(v) = 0, \quad a=1, \dots, m
$$
因此，分布的纤维 (fiber) 是 $D(q) = \bigcap_{a=1}^m \ker(\omega^a(q))$。

为了使 $D$ 成为一个良定义的几何对象——即 $TQ$ 的一个光滑向量子丛——其纤维的维数必须在 $Q$ 上是常数。根据[秩-零度定理](@entry_id:154441)，$\dim(D(q)) = n - \mathrm{rank}(\{\omega^a(q)\})$，其中 $n = \dim Q$。因此，为了使 $\dim(D(q))$ 恒为 $n-m$，要求这 $m$ 个 [1-形式](@entry_id:270392) $\{\omega^a(q)\}$ 在 $Q$ 的每一点都是[线性无关](@entry_id:148207)的。这个**常秩条件** (constant rank condition) 是保证 $D$ 是 $TQ$ 的一个光滑子丛的充分必要条件 。值得注意的是，这个条件只关乎分布的正则性，而与其是否可积（即是否为完整约束）无关。

#### 可积性与 Frobenius 定理

[完整约束](@entry_id:140686)与非完整约束之间的根本区别在于**[可积性](@entry_id:142415)** (integrability)。一个分布 $D$ 被称为可积的，如果它能被“积分”成位形空间 $Q$ 的一个[叶状结构](@entry_id:160209) (foliation)，也就是说，$Q$ 可以被划分为一族互不相交的子流形（叶），而分布 $D$ 恰好是这些叶的[切丛](@entry_id:161294)。从物理上讲，这意味着速度约束可以等价地表示为一组纯粹的位置约束 $f(q)=0$。在这种情况下，非完整形式的速度约束实际上是“伪装的”[完整约束](@entry_id:140686)。

判断一个分布是否可積的准则是著名的 **Frobenius 定理**。该定理指出，一个光滑分布 $D$ 是可积的，当且仅当它是**对合的** (involutive)，即对于任意两个取值于 $D$ 的向量场 $X, Y$（即 $X(q), Y(q) \in D(q)$ 对所有 $q$ 成立），它们的[李括号](@entry_id:636461) $[X, Y]$ 也取值于 $D$。

对于由单个非零 1-形式 $\omega$ 定义的[余维](@entry_id:273141)为 1 的分布 $D = \ker \omega$，Frobenius 条件有一个更简洁的表述：$D$ 是可积的当且仅当 $\omega \wedge d\omega = 0$，其中 $d\omega$ 是 $\omega$ 的外微分。如果 $\omega \wedge d\omega \neq 0$，则该约束是真正非完整的。

例如，考虑 $\mathbb{R}^3$ 上的约束，由 [1-形式](@entry_id:270392) $\omega_{\alpha,\beta} = dz - x\,dy + \alpha\, y\,dx + \beta\, z\,dx$ 定义 。
首先计算其[外微分](@entry_id:161900)：
$$
d\omega_{\alpha,\beta} = -d(x \wedge dy) + \alpha\, d(y \wedge dx) + \beta\, d(z \wedge dx) = -dx \wedge dy - \alpha\, dx \wedge dy + \beta\, dz \wedge dx = -(1+\alpha)dx \wedge dy + \beta\, dz \wedge dx
$$
然后计算 $\omega_{\alpha,\beta} \wedge d\omega_{\alpha,\beta}$：
$$
\begin{align*}
\omega_{\alpha,\beta} \wedge d\omega_{\alpha,\beta}  = (dz - x\,dy + \dots) \wedge (-(1+\alpha)dx \wedge dy + \beta\,dz \wedge dx) \\
 = dz \wedge (-(1+\alpha)dx \wedge dy) - x\,dy \wedge (\beta\,dz \wedge dx) + \dots \\
 = -(1+\alpha)dz \wedge dx \wedge dy - x\beta\, dy \wedge dz \wedge dx \\
 = (-1-\alpha-x\beta) dx \wedge dy \wedge dz
\end{align*}
$$
其中我们利用了 $dx \wedge dx = 0$ 等性质。Frobenius 条件 $\omega_{\alpha,\beta} \wedge d\omega_{\alpha,\beta} = 0$ 要求系数函数恒为零，即 $-1-\alpha-x\beta = 0$ 对所有 $x,y,z$ 成立。这只有在 $\beta=0$ 和 $\alpha=-1$ 时才可能。因此，仅当 $(\alpha, \beta)=(-1, 0)$ 时，该约束是完整的。对于其他参数值，例如著名的接触形式 $dz-ydx$（对应于 $\alpha=0, x \to y, y \to z$ 的[坐标变换](@entry_id:172727)），约束是不可积的。

### 动力学原理与[运动方程](@entry_id:264286)

约束的存在从根本上改变了系统的[动力学方程](@entry_id:751029)。我们需要修正标准的拉格朗日或[哈密顿原理](@entry_id:175601)，以纳入约束的影响。

#### 完整系统与[拉格朗日乘子](@entry_id:142696)

对于受完整约束 $f(q)=0$ 的系统，其运动轨迹被限制在子流形 $\mathcal{C}$ 上。根据[哈密顿原理](@entry_id:175601)，真实路径使作用量 $S = \int L(q, \dot{q}) dt$ 在所有满足约束的路径变分中取驻值。这意味着路径变分 $\delta q$ 必须是 $\mathcal{C}$ 的切向量，即满足 $df(\delta q) = 0$。

应用[变分法](@entry_id:166033)，我们得到：
$$
\delta S = \int \left( \frac{\partial L}{\partial q^i} - \frac{d}{dt}\frac{\partial L}{\partial \dot{q}^i} \right) \delta q^i dt = 0
$$
由于变分 $\delta q$ 不是完全任意的，而是受限于 $\sum_i (\partial f_a / \partial q^i) \delta q^i = 0$，我们不能直接断定括号内的 Euler-Lagrange 表达式为零。然而，根据[拉格朗日乘子法](@entry_id:176596)，这意味着 Euler-Lagrange 表达式向量必须是约束[梯度向量](@entry_id:141180)的[线性组合](@entry_id:154743)。因此，存在一组时间依赖的**[拉格朗日乘子](@entry_id:142696)** (Lagrange multipliers) $\lambda^a(t)$，使得：
$$
\frac{d}{dt}\frac{\partial L}{\partial \dot{q}^i} - \frac{\partial L}{\partial q^i} = \sum_{a=1}^m \lambda^a \frac{\partial f_a}{\partial q^i}
$$
方程右边代表了**[广义约束力](@entry_id:178528)**。如果我们采用一个黎曼度规，可以将此力从[余向量](@entry_id:157727)转换为向量形式 $F_{reac} = \sum_{a=1}^m \lambda^a \nabla f_a(q)$ 。这再次印证了[约束力](@entry_id:170052)正交于约束子流形的几何图像。

#### [非完整系统](@entry_id:173158)：Lagrange-[d'](@entry_id:902691)Alembert 原理

对于[非完整系统](@entry_id:173158)，情况变得更加微妙。描述其运动的公认正确的物理原理是 **Lagrange-[d'](@entry_id:902691)Alembert 原理**。该原理假设[约束力](@entry_id:170052)是**理想的** (ideal)，即它们在任何**允许的[虚位移](@entry_id:168781)** (admissible virtual displacements) 上不做功。

这里的核心是 "允许的虚位移" 的定义。根据 **Chetaev 法则**，在时刻 $t$，一个[虚位移](@entry_id:168781) $\delta q$ 是允许的，当且仅当它满足[约束方程](@entry_id:138140)的齐次线性部分 。对于速度约束 $\omega^a(q) \cdot \dot{q} + \sigma^a(q) = 0$，允许的[虚位移](@entry_id:168781) $\delta q$ 满足 $\omega^a(q) \cdot \delta q = 0$，即 $\delta q \in D(q)$。

Lagrange-[d'](@entry_id:902691)Alembert 原理可以表述为：
$$
\left( \frac{d}{dt}\frac{\partial L}{\partial \dot{q}} - \frac{\partial L}{\partial q} \right) \cdot \delta q = 0, \quad \forall \delta q \in D(q)
$$
这等价于说 Euler-Lagrange 表达式向量必须正交于允许的虚位移空间 $D(q)$。因此，它必须是定义 $D(q)$ 的 1-形式 $\omega^a$ 的线性组合。这产生了**[非完整运动](@entry_id:1128847)方程**：
$$
\frac{d}{dt}\frac{\partial L}{\partial \dot{q}^i} - \frac{\partial L}{\partial q^i} = \sum_{a=1}^m \mu_a(t) A_{ai}(q)
$$
其中 $A_{ai}$ 是 [1-形式](@entry_id:270392) $\omega^a$ 的分量，$\mu_a(t)$ 是[拉格朗日乘子](@entry_id:142696)。值得注意的是，Gauss 最小约束原理和 Gibbs-Appell 方程在理想齐次[线性约束](@entry_id:636966)的情况下与 Lagrange-[d'](@entry_id:902691)Alembert 原理等价 。

#### Vakonomic 原理：一个微妙的陷阱

一个看似合理的替代方法是**Vakonomic 原理**（也称约束[变分原理](@entry_id:198028)）。该方法将约束直接通过拉格朗日乘子加入到作用量中，形成一个增广作用量：
$$
S[q,\lambda] = \int_{t_0}^{t_1} \left( L(q,\dot q) + \lambda_a(t) c^a(q, \dot{q}) \right) dt
$$
然后对这个增广作用量应用标准的[哈密顿原理](@entry_id:175601)，将 $q(t)$ 和 $\lambda(t)$ 都视为独立的变分路径。

对 $q$ 进行变分并分部积分后，得到的[运动方程](@entry_id:264286)（**vakonomic 方程**）与非完整方程有显著不同 。具体而言，vakonomic 方程包含与约束形式 $A_{ia}$ 的导数（即分布 $D$ 的曲率）相关的项。对于一般的[非完整约束](@entry_id:167828)，vakonomic 方程为：
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot q^\beta}\right) - \frac{\partial L}{\partial q^\beta} = \lambda_a \left( \frac{\partial A_{a\alpha}}{\partial q^\beta} \dot{q}^\alpha - \frac{d}{dt}A_{a\beta} \right) = -A_{a\beta}\dot{\lambda}_a + \lambda_a (\partial_\beta A_{a\alpha} - \partial_\alpha A_{a\beta})\dot{q}^\alpha
$$
这个方程右侧与非完整方程中的[约束力](@entry_id:170052)项 $\mu_a A_{a\beta}$ 在结构上完全不同。

这个差异的根源在于，vakonomic 原理隐含地假设路径变分 $\delta q$ 和速度变分 $\delta \dot{q}$ 之间存在关系 $\delta \dot{q} = d(\delta q)/dt$，而 Lagrange-d'Alembert 原理仅在瞬时层面限制[虚位移](@entry_id:168781) $\delta q$，并不对 $\delta \dot{q}$ 做任何假设 。

对于完整约束，由于其对应的分布是可积的（曲率为零），vakonomic 方程与 Lagrange-d'Alembert 方程是等价的  。然而，对于真正的[非完整约束](@entry_id:167828)，两者会给出不同的动力学预测。例如，在一个无滑动的滚动圆盘问题中，Lagrange-d'Alembert 原理正确地预测其[方向角](@entry_id:167868) $\theta$ 的[角加速度](@entry_id:1131116)为零 ($\ddot{\theta}_{nh}=0$)。而 vakonomic 原理却预测了一个非零的[角加速度](@entry_id:1131116) $\ddot{\theta}_{vak} = \frac{R\dot{\phi}}{I_{\theta}}(\lambda_1\sin\theta - \lambda_2\cos\theta)$，这与物理实验不符 。因此，Lagrange-d'Alembert 原理被公认为是描述[非完整系统](@entry_id:173158)的正确物理框架。

### 约束的哈密顿形式

将[约束理论](@entry_id:1122946)推广到哈密顿框架中，会引出更深刻和丰富的几何结构。

#### 预辛几何与约束

当一个系统的[拉格朗日量](@entry_id:174593)是退化的，或者当我们将一个受约束的拉格朗日系统进行勒让德变换时，我们得到的可能不是一个[辛流形](@entry_id:161608)，而是一个**预[辛流形](@entry_id:161608)** (presymplectic manifold) $(M, \omega)$，其上的 2-形式 $\omega$ 是闭合的但可能是退化的。

在这样的流形上，[哈密顿向量场](@entry_id:158846) $X_H$ 的定义方程 $\iota_{X_H} \omega = dH$ 可能没有解，或者解不唯一。
- **解的存在性**：在一点 $m \in M$，方程有解的充要条件是 $dH(m)$ 属于 $\omega_m$ 定义的[线性映射的像](@entry_id:200465)空间。这等价于 $dH(m)$ 必须在 $\omega_m$ 的核空间 $\ker \omega_m$ 上为零。所有满足此条件的点 $m \in M$ 构成的集合 $C$ 称为**主约束集** (primary constraint set) 。动力学只在这个子集上有意义。
- **[解的唯一性](@entry_id:143619)**：如果解存在，其不唯一性由 $\ker \omega_m$ 决定。任意两个解相差一个属于 $\ker \omega_m$ 的向量。这种不确定性被称为**[规范自由度](@entry_id:160491)** (gauge freedom)。
- **[一致性条件](@entry_id:637057)**：为了保证系统的轨迹始终停留在主约束集 $C$ 内，哈密頓向量场 $X_H$ 必须与 $C$ 相切。这个要求可能会导致新的约束，即**[次级约束](@entry_id:165897)** (secondary constraints)。重复此过程，直到所有约束都满足[一致性条件](@entry_id:637057)，这就是 **Dirac-Bergmann 约束算法**。

由于 $\omega$ 是闭合的，分布 $\ker \omega$ 是对合的，因此是可积的。在[正则性条件](@entry_id:166962)下，我们可以通过对约束集 $C$ 按 $\ker \omega$ 的[叶状结构](@entry_id:160209)作[商空间](@entry_id:274314)，从而得到一个真正辛的**简约相空间** (reduced phase space)，其上的动力学是标准的哈密顿动力学 。

#### 二类约束与 Dirac 括号

在哈密顿框架中，约束函数 $\phi_a(q,p)=0$ 根据它们之间的[泊松括号](@entry_id:151133)关系被分类。如果一个约束 $\phi_a$ 与所有其他约束的泊松括号在约束子流形上都为零（即 $\{\phi_a, \phi_b\} \approx 0$），则称之为**一类约束** (first-class constraints)，它们通常与[规范自由度](@entry_id:160491)相关。

如果约束矩阵 $C_{ab} = \{\phi_a, \phi_b\}$ 在约束子流形上是可逆的，则称这组约束为**二类约束** (second-class constraints)。二类约束代表了相空间中真正的冗余自由度。为了在约束[子流形](@entry_id:159439)上定义一个自洽的[哈密顿动力学](@entry_id:156273)，我们需要修改[泊松括号](@entry_id:151133)，这就是 **Dirac 括号** (Dirac bracket) 的由来。

对于任意两个函数 $F, G$，其 Dirac 括号定义为：
$$
\{F, G\}_D = \{F, G\} - \sum_{a,b} \{F, \phi_a\} (C^{-1})_{ab} \{\phi_b, G\}
$$
Dirac 括号具有泊松括号的所有性质（[反对称性](@entry_id:261893)、[双线性](@entry_id:146819)和雅可比恒等式），并且它自动满足约束，即对任意函数 $F$ 和任意约束 $\phi_a$，都有 $\{F, \phi_a\}_D = 0$。通过 Dirac 括号，约束被“强加”到代数结构中，系统的动力学演化由新的[哈密顿方程](@entry_id:156213) $\dot{F} = \{F, H\}_D$ 给出。

例如，在 $T^*\mathbb{R}^2$ 上考虑约束 $\phi_1=q_2=0$ 和 $\phi_2=p_2=0$。约束矩阵为 $C = \begin{pmatrix} 0  1 \\ -1  0 \end{pmatrix}$，其逆为 $C^{-1} = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$。计算剩余坐标的 Dirac 括号：
$$
\{q_1, p_1\}_D = \{q_1, p_1\} - (\{q_1, q_2\}(C^{-1})_{12}\{p_2, p_1\} + \{q_1, p_2\}(C^{-1})_{21}\{q_2, p_1\}) = 1 - (0 \cdot (-1) \cdot 0 + 0 \cdot 1 \cdot 0) = 1
$$
这表明，在约束子流形上，Dirac 括号退化为剩余自由度 $(q_1, p_1)$ 上的标准典范泊松括号 。

#### [非完整括号](@entry_id:1128844)

对于非完整系统，也可以定义一种括号结构，即**[非完整括号](@entry_id:1128844)** (nonholonomic bracket)。然而，与 Dirac 括号根本不同的是，[非完整括号](@entry_id:1128844)**不满足雅可比恒等式**，因此它不是一个[泊松括号](@entry_id:151133)，而是一个**殆[泊松括号](@entry_id:151133)** (almost-Poisson bracket)。

[非完整括号](@entry_id:1128844)可以通过将典范哈密顿向量场按动力学度规[正交投影](@entry_id:144168)到[约束分布](@entry_id:1122944)上来构造。这种括号的非零值，特别是那些在典范[泊松括号](@entry_id:151133)下为零的量，反映了[非完整约束](@entry_id:167828)引起的动力学“混合”效应。例如，对于一个具有[非完整约束](@entry_id:167828) $p_3 - (q^1/\ell)p_2 = 0$ 的系统，可以计算出 $\{q^2, p_3\}_{nh} = \frac{q^1/\ell}{1+(q^1/\ell)^2}$。而对于一个相关的完整系统（如 $q^3=0, p_3=0$），对应的 Dirac 括号为 $\{q^2, p_3\}_D = 0$。这个差异 $\Delta = \frac{q^1\ell}{(q^1)^2+\ell^2}$ 明确地展示了由[非完整约束](@entry_id:167828)引入的非平凡代数结构，这是 Dirac 括号所不具备的 。这种结构上的差异深刻地反映了[完整约束](@entry_id:140686)和非完整约束在动力学層面上的本质区别。