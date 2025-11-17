## 引言
在[分析力学](@entry_id:166738)的宏伟殿堂中，哈密顿形式以其对称性和深刻的几何结构而著称。为了充分挖掘这一框架的潜力，我们常常需要跳出原始的[广义坐标](@entry_id:156576)和动量，寻求一种新的视角来简化问题。[正则变换](@entry_id:178165)正是实现这一目标的关键钥匙——它是一种特殊的相空间[坐标变换](@entry_id:172727)，能够在改变坐标描述的同时，奇迹般地保持[哈密顿运动方程](@entry_id:176972)的优美形式。这种变换的重要性不言而喻，它能将一个看似棘手的复杂系统，转化为一个简单甚至平凡可解的模型，从而揭示其内在的守恒律和动力学对称性。

然而，一个核心问题随之而来：我们如何系统地寻找和构建这些强大的变换？仅仅是凭空猜测或依赖灵感是远远不够的。答案在于一个优雅而强大的数学工具——**[母函数](@entry_id:146702) (generating function)**。[母函数](@entry_id:146702)理论为我们提供了一套明确的“配方”，通过构造一个恰当的标量函数，我们便能生成所需的[正则变换](@entry_id:178165)。

本文将带领你深入探索[正则变换](@entry_id:178165)母函数的完整世界。在 **第一章：原理与机制** 中，我们将从[哈密顿原理](@entry_id:175601)出发，推导出母函数的由来，并系统学习四种[基本类](@entry_id:158335)型的母函数及其变换方程。我们将掌握它们之间的勒让德变换关系，并理解如何运用泊松括号来检验变换的正则性。在 **第二章：应用与交叉学科联系** 中，我们将领略母函数的强大威力，看它如何用于解耦耦合系统、通过[哈密顿-雅可比理论](@entry_id:165642)求解问题，并作为桥梁连接经典光学、电磁学乃至量子力学等多个物理分支。最后，在 **第三章：动手实践** 中，你将通过一系列精心设计的练习，将理论知识转化为解决实际问题的能力，亲手构建和分析由[母函数](@entry_id:146702)生成的变换。

## 原理与机制

在[哈密顿力学](@entry_id:146202)中，[正则变换](@entry_id:178165)是保持[哈密顿方程](@entry_id:156213)形式不变的相空间[坐标变换](@entry_id:172727)。虽然引言章节已经阐述了进行此类变换的动机——即通过寻找新的坐标和动量来简化或揭示系统的动力学行为——但我们尚未深入探讨实现这些变换的具体机制。本章旨在系统地阐述这些机制，其核心是一种被称为**母函数 (generating function)** 的强大数学工具。我们将看到，一个恰当选择的标量函数可以完全确定一个[正则变换](@entry_id:178165)，将旧的坐标 $(q, p)$ 映射到新的坐标 $(Q, P)$。

### [母函数](@entry_id:146702)的起源：修正的[哈密顿原理](@entry_id:175601)

要理解[母函数](@entry_id:146702)的来源，我们需回顾[分析力学](@entry_id:166738)的基石——[作用量原理](@entry_id:154742)。一个系统的动力学轨迹使作用量 $S = \int L \, dt$ 取极值。在哈密顿形式下，这等价于[哈密顿原理](@entry_id:175601)：

$$
\delta \int_{t_1}^{t_2} \left( \sum_i p_i \dot{q}_i - H(q, p, t) \right) dt = 0
$$

如果从[坐标系](@entry_id:156346) $(q, p)$ 到 $(Q, P)$ 的变换是正则的，那么在新[坐标系](@entry_id:156346)中，动力学演化也必须遵循同样形式的[哈密顿原理](@entry_id:175601)：

$$
\delta \int_{t_1}^{t_2} \left( \sum_i P_i \dot{Q}_i - K(Q, P, t) \right) dt = 0
$$

其中 $K(Q, P, t)$ 是新的[哈密顿量](@entry_id:172864)。这两个积分变分为零的条件意味着，它们的被积函数之间最多只能相差一个任意函数 $F$ 的[全时间导数](@entry_id:172646)。为了保持最广泛的适用性，我们引入一个缩放因子 $\lambda$（通常取为1），得到以下基本关系式：

$$
\sum_i p_i \dot{q}_i - H = \lambda \left( \sum_i P_i \dot{Q}_i - K \right) + \frac{dF}{dt}
$$

在本章中，我们将始终考虑最常见的情况，即**辛变换 (symplectic transformation)**，其中 $\lambda = 1$。因此，我们的出发点是：

$$
\sum_i p_i \dot{q}_i - H = \sum_i P_i \dot{Q}_i - K + \frac{dF}{dt}
$$

这个函数 $F$ 就是**[母函数](@entry_id:146702)**。它的巧妙之处在于，通过选择其[自变量](@entry_id:267118)，我们可以系统地推导出旧坐标与新坐标之间的变换关系。

### 四种[基本类](@entry_id:158335)型的母函数

一个具有 $n$ 个自由度的系统，其相空间有 $2n$ 个维度。一个[正则变换](@entry_id:178165)涉及 $4n$ 个变量（$n$ 个旧坐标 $q_i$、 $n$  个旧动量 $p_i$、 $n$ 个新坐标 $Q_i$ 和 $n$ 个新动量 $P_i$）。然而，由于变换方程的约束，只有 $2n$ 个变量是独立的。我们可以选择一个旧变量（坐标或动量）和一个新变量（坐标或动量）的混合组合作为母函数的自变量。这自然地引出了四种[基本类](@entry_id:158335)型的[母函数](@entry_id:146702)。为简洁起见，我们以单自由度系统为例进行说明。

#### 第一类母函数: $F_1(q, Q, t)$

当母函数是旧坐标 $q$、新坐标 $Q$ 和时间 $t$ 的函数时，我们称之为**第一类[母函数](@entry_id:146702)** $F_1(q, Q, t)$。我们将 $F_1$ 的全时间导数展开：

$$
\frac{dF_1}{dt} = \frac{\partial F_1}{\partial q}\dot{q} + \frac{\partial F_1}{\partial Q}\dot{Q} + \frac{\partial F_1}{\partial t}
$$

代入基本关系式 $p\dot{q} - H = P\dot{Q} - K + \frac{dF_1}{dt}$，我们得到：

$$
p\dot{q} - H = P\dot{Q} - K + \frac{\partial F_1}{\partial q}\dot{q} + \frac{\partial F_1}{\partial Q}\dot{Q} + \frac{\partial F_1}{\partial t}
$$

重新整理上式，按 $\dot{q}$ 和 $\dot{Q}$ 的系数进行分组：

$$
\left(p - \frac{\partial F_1}{\partial q}\right)\dot{q} - \left(P + \frac{\partial F_1}{\partial Q}\right)\dot{Q} - \left(H - K + \frac{\partial F_1}{\partial t}\right) = 0
$$

由于 $q$ 和 $Q$ 被选为独立变量，它们的运动（即 $\dot{q}$ 和 $\dot{Q}$）也是独立的。因此，为使上式对任意运动都成立，各项系数必须为零。这就给出了第一类[母函数](@entry_id:146702)的变换方程：

$$
p = \frac{\partial F_1}{\partial q}, \quad P = -\frac{\partial F_1}{\partial Q}, \quad K = H + \frac{\partial F_1}{\partial t}
$$

要使 $F_1(q, Q)$ 成为一个有效的[母函数](@entry_id:146702)，一个基本前提是变量 $q$ 和 $Q$ 必须是[相互独立](@entry_id:273670)的。如果 $Q$ 可以完全由 $q$ 决定（反之亦然），那么它们就不能作为独立的坐标来描述相空间的一个区域。例如，对于变换 $Q = e^q$，变量 $Q$ 仅仅是 $q$ 的函数，它们是函数依赖的。这意味着从 $(q,p)$ 到 $(q,Q)$ 的坐标变换是奇异的，其[雅可比行列式](@entry_id:137120)为零 [@problem_id:1246524]。因此，不存在一个全局的 $F_1(q,Q)$ 来生成这个变换。

此外，为了确保我们能够从 $(q, Q)$ 反解出 $(q, p)$ 或 $(Q, P)$，变换必须是局部可逆的。例如，从 $p = \frac{\partial F_1}{\partial q}$ 和 $P = -\frac{\partial F_1}{\partial Q}$ 中求解 $Q(q,p)$ 需要满足[隐函数定理](@entry_id:147247)的条件。一个关键的可逆性条件是混合[二阶偏导数](@entry_id:635213)不为零，即 $\frac{\partial^2 F_1}{\partial q \partial Q} \neq 0$。这个条件确保了 $p$ 对 $Q$ 的依赖性以及 $P$ 对 $q$ 的依赖性，从而使得坐标间的反解成为可能 [@problem_id:2054657]。

#### 第二类[母函数](@entry_id:146702): $F_2(q, P, t)$

在实际应用中，将新动量 $P$ 而不是新坐标 $Q$ 作为独立变量通常更为方便。我们可以通过**勒让德变换 (Legendre Transformation)** 从 $F_1$ 得到一种新的[母函数](@entry_id:146702) $F_2$。定义：

$$
F_2(q, P, t) = F_1(q, Q, t) + PQ
$$

这里的思想是用 $P$ 来替换 $Q$ 作为自变量，这要求我们利用关系式 $P = -\frac{\partial F_1}{\partial Q}$ 将 $Q$ 表示为 $q$ 和 $P$ 的函数，$Q=Q(q,P,t)$。

$F_2$ 的[全微分](@entry_id:171747)是 $dF_2 = dF_1 + P dQ + Q dP$。而已知 $dF_1 = p dq - P dQ$ (忽略时间依赖)，所以 $dF_2 = p dq - P dQ + P dQ + Q dP = p dq + Q dP$。从这个微分形式，或者通过代入基本关系式，我们可以推导出**第二类母函数**的变换方程：

$$
p = \frac{\partial F_2}{\partial q}, \quad Q = \frac{\partial F_2}{\partial P}, \quad K = H + \frac{\partial F_2}{\partial t}
$$

$F_2$ 型[母函数](@entry_id:146702)非常常用。让我们通过几个例子来理解它的应用。

**示例 1：坐标平移**
考虑一个简单的坐标平移变换：$Q = q + a$，$P = p$，其中 $a$ 是一个常数。这是一个[正则变换](@entry_id:178165)。我们来寻找生成它的 $F_2(q, P)$。根据变换方程，我们有：
$p = P = \frac{\partial F_2}{\partial q}$
$Q = q + a = \frac{\partial F_2}{\partial P}$
对第一个方程关于 $q$ 积分（视 $P$ 为常数），得到 $F_2(q, P) = qP + g(P)$，其中 $g(P)$ 是一个只与 $P$ 有关的待定函数。
将此结果代入第二个方程：
$q + a = \frac{\partial}{\partial P}(qP + g(P)) = q + g'(P)$
由此可知 $g'(P) = a$，积分得到 $g(P) = aP + C$。取积分常数 $C=0$，我们便得到生成此平移变换的母函数 [@problem_id:2054679]：
$$
F_2(q, P) = qP + aP = P(q + a)
$$

**示例 2：[线性变换](@entry_id:149133)**
考虑一个更复杂的线性[正则变换](@entry_id:178165) [@problem_id:2054658]：
$$
Q = 2q + \frac{1}{2}p, \quad P = 2q + p
$$
要找到相应的 $F_2(q, P)$，我们首先需要将旧动量 $p$ 表示为 $q$ 和 $P$ 的函数。从第二个方程可以解得 $p = P - 2q$。
根据 $F_2$ 的定义，$p = \frac{\partial F_2}{\partial q}$，我们对 $p$ 关于 $q$ 积分：
$$
F_2(q, P) = \int (P - 2q) \, dq = Pq - q^2 + f(P)
$$
其中 $f(P)$ 是一个待定函数。接下来，我们使用另一个关系式 $Q = \frac{\partial F_2}{\partial P}$：
$$
Q = \frac{\partial}{\partial P}(Pq - q^2 + f(P)) = q + f'(P)
$$
另一方面，我们也可以从原变换中将 $Q$ 表示为 $q$ 和 $P$ 的函数。将 $p = P - 2q$ 代入 $Q$ 的表达式：
$$
Q = 2q + \frac{1}{2}(P - 2q) = q + \frac{1}{2}P
$$
比较两个 $Q$ 的表达式，我们得到 $q + f'(P) = q + \frac{1}{2}P$，这意味着 $f'(P) = \frac{1}{2}P$。积分后得到 $f(P) = \frac{1}{4}P^2$（忽略积分常数）。因此，最终的母函数为：
$$
F_2(q, P) = Pq - q^2 + \frac{1}{4}P^2
$$

#### 第三类和第四类母函数

通过对 $F_1$ 的两个变量都进行勒让德变换，我们可以得到另外两种[母函数](@entry_id:146702)。

**第三类[母函数](@entry_id:146702) $F_3(p, Q, t)$** 通过变换 $F_3(p, Q, t) = F_1(q, Q, t) - pq$ 得到，其变换方程为：

$$
q = -\frac{\partial F_3}{\partial p}, \quad P = -\frac{\partial F_3}{\partial Q}, \quad K = H + \frac{\partial F_3}{\partial t}
$$

一个经典的例子是相空间反演变换 $Q = -q, P = -p$。要找到生成它的 $F_3(p, Q)$，我们将变换关系代入定义式中。从 $q = -Q = -\frac{\partial F_3}{\partial p}$，我们得到 $\frac{\partial F_3}{\partial p} = Q$。对 $p$ 积分得 $F_3(p, Q) = pQ + g(Q)$。再利用 $P = -p = -\frac{\partial F_3}{\partial Q} = -(p + g'(Q))$，我们发现 $g'(Q) = 0$，即 $g(Q)$ 为常数。取常数为零，我们得到生成该反演变换的母函数为 $F_3(p, Q) = pQ$ [@problem_id:2054671]。

**第四类[母函数](@entry_id:146702) $F_4(p, P, t)$** 通过变换 $F_4(p, P, t) = F_1(q, Q, t) - pq + PQ$ 得到，其变换方程为：

$$
q = -\frac{\partial F_4}{\partial p}, \quad Q = \frac{\partial F_4}{\partial P}, \quad K = H + \frac{\partial F_4}{\partial t}
$$

这四种母函数为我们操控哈密顿系统提供了完整的工具箱。它们之间的关系可以通过[勒让德变换](@entry_id:146727)清晰地建立起来。

### 母函数之间的[勒让德变换](@entry_id:146727)

[勒让德变换](@entry_id:146727)是连接不同类型母函数的桥梁。它本质上是一种切换函数[自变量](@entry_id:267118)的方法，在[热力学](@entry_id:141121)和[分析力学](@entry_id:166738)中都扮演着核心角色。让我们通过实例来具体展示如何从 $F_1$ 变换到 $F_2$。

**示例 1：**
假设一个[正则变换](@entry_id:178165)由第一类[母函数](@entry_id:146702) $F_1(q, Q) = \frac{k}{2}(q - Q)^2$ 生成 [@problem_id:2054663]。我们希望找到对应的第二类[母函数](@entry_id:146702) $F_2(q, P)$。
[勒让德变换](@entry_id:146727)的公式是 $F_2(q, P) = F_1(q, Q) + PQ$。为了完成变换，我们需要将 $Q$ 表示为 $q$ 和 $P$ 的函数。
从 $F_1$ 的定义，我们有 $P = -\frac{\partial F_1}{\partial Q} = -k(q - Q)(-1) = k(q - Q)$。
由此解出 $Q$：$Q = q - \frac{P}{k}$。
现在，我们将 $Q$ 的表达式代回 $F_1$ 和 $PQ$ 中：
$F_1 = \frac{k}{2}\left(q - \left(q - \frac{P}{k}\right)\right)^2 = \frac{k}{2}\left(\frac{P}{k}\right)^2 = \frac{P^2}{2k}$。
$PQ = P\left(q - \frac{P}{k}\right) = Pq - \frac{P^2}{k}$。
将两者相加，得到 $F_2(q, P)$：
$$
F_2(q, P) = \frac{P^2}{2k} + \left(Pq - \frac{P^2}{k}\right) = Pq - \frac{P^2}{2k}
$$

**示例 2：**
再考虑一个不同的例子，$F_1(q, Q) = q(1+Q^2)$ [@problem_id:1246452]。
首先，计算 $P$：$P = -\frac{\partial F_1}{\partial Q} = -2qQ$。
从中解出 $Q$：$Q = -\frac{P}{2q}$。
现在，应用勒让德变换 $F_2(q, P) = F_1(q, Q(q,P)) + PQ(q,P)$：
$$
F_2(q, P) = q\left(1 + \left(-\frac{P}{2q}\right)^2\right) + P\left(-\frac{P}{2q}\right)
$$
$$
= q\left(1 + \frac{P^2}{4q^2}\right) - \frac{P^2}{2q} = q + \frac{P^2}{4q} - \frac{P^2}{2q} = q - \frac{P^2}{4q}
$$
这些例子表明，只要给定一种类型的[母函数](@entry_id:146702)，原则上就可以通过系统的代数步骤推导出其他类型的[母函数](@entry_id:146702)。

### [正则变换](@entry_id:178165)的性质与应用

掌握了生成[正则变换](@entry_id:178165)的机制后，我们现在可以探讨其关键性质和强大应用。

#### 泊松括号的[不变性](@entry_id:140168)

[正则变换](@entry_id:178165)的一个根本性质是它保持了**基本[泊松括号](@entry_id:151133) (fundamental Poisson brackets)** 的结构。对于任意一对[正则坐标](@entry_id:175654) $(q_i, p_i)$，它们满足：
$$
\{q_i, q_j\}_{q,p} = 0, \quad \{p_i, p_j\}_{q,p} = 0, \quad \{q_i, p_j\}_{q,p} = \delta_{ij}
$$
一个变换 $(q,p) \rightarrow (Q,P)$ 是正则的，当且仅当新坐标也满足同样的关系：
$$
\{Q_i, Q_j\}_{q,p} = 0, \quad \{P_i, P_j\}_{q,p} = 0, \quad \{Q_i, P_j\}_{q,p} = \delta_{ij}
$$
注意这里的泊松括号是关于旧坐标 $(q, p)$ 计算的。这个性质为我们提供了一个直接检验变换是否正则的有力工具。

例如，让我们验证由 $F_2(q, P) = \alpha q^2 P$（其中 $\alpha$ 为非零常数）生成的变换是否是正则的 [@problem_id:2054660]。
首先，我们导出变换方程：
$Q = \frac{\partial F_2}{\partial P} = \alpha q^2$
$p = \frac{\partial F_2}{\partial q} = 2\alpha q P$
为了计算泊松括号 $\{Q, P\}_{q,p}$，我们需要将 $Q$ 和 $P$ 都表示为 $(q, p)$ 的函数。
$Q(q,p) = \alpha q^2$
$P(q,p) = \frac{p}{2\alpha q}$
现在计算所需的偏导数：
$\frac{\partial Q}{\partial q} = 2\alpha q$, $\frac{\partial Q}{\partial p} = 0$
$\frac{\partial P}{\partial q} = -\frac{p}{2\alpha q^2}$, $\frac{\partial P}{\partial p} = \frac{1}{2\alpha q}$
将它们代入[泊松括号](@entry_id:151133)的定义 $\{A, B\}_{q,p} = \frac{\partial A}{\partial q}\frac{\partial B}{\partial p} - \frac{\partial A}{\partial p}\frac{\partial B}{\partial q}$：
$$
\{Q, P\}_{q,p} = (2\alpha q)\left(\frac{1}{2\alpha q}\right) - (0)\left(-\frac{p}{2\alpha q^2}\right) = 1 - 0 = 1
$$
由于 $\{Q, P\}_{q,p} = 1$（同时可以验证 $\{Q, Q\}=0$ 和 $\{P, P\}=0$），这证实了该变换确实是正则的。

#### 简化[哈密顿量](@entry_id:172864)与寻找[守恒量](@entry_id:150267)

[正则变换](@entry_id:178165)最强大的应用在于简化问题的[哈密顿量](@entry_id:172864)。其终极目标是找到一组新的[正则坐标](@entry_id:175654) $(Q, P)$，使得新的[哈密顿量](@entry_id:172864) $K(Q, P)$ 具有尽可能简单的形式。最理想的情况是，新的[哈密顿量](@entry_id:172864)不依赖于某个新坐标 $Q_i$（即 $Q_i$ 是**[循环坐标](@entry_id:166220)**）。在这种情况下，哈密顿方程给出：
$$
\dot{P}_i = -\frac{\partial K}{\partial Q_i} = 0
$$
这意味着新动量 $P_i$ 是一个**守恒量**，即[运动积分](@entry_id:163455)。找到系统的所有[守恒量](@entry_id:150267)等价于完全解出该系统。

让我们通过一个精妙的例子来展示这一思想的应用 [@problem_id:1246408]。考虑一个一维谐振子，其[哈密顿量](@entry_id:172864)为 $H = \frac{p^2}{2m} + \frac{1}{2}kq^2$。我们引入一个由第三类[母函数](@entry_id:146702) $F_3(p, Q) = -\frac{p^2}{2\alpha} \tan(Q)$ 生成的[正则变换](@entry_id:178165)，其中 $\alpha$ 是一个待定常数。
变换方程为：
$q = -\frac{\partial F_3}{\partial p} = \frac{p}{\alpha}\tan(Q)$
$P = -\frac{\partial F_3}{\partial Q} = \frac{p^2}{2\alpha}\sec^2(Q)$
我们可以从这些关系中反解出旧坐标 $p, q$ 来表示新坐标 $P, Q$：
$p^2 = 2\alpha P \cos^2(Q)$
$q^2 = \frac{p^2}{\alpha^2}\tan^2(Q) = \frac{2P}{\alpha}\sin^2(Q)$
将它们代入旧的[哈密顿量](@entry_id:172864) $H$ 即可得到新的[哈密顿量](@entry_id:172864) $K$：
$$
K(Q,P) = H(q(Q,P), p(Q,P)) = \frac{2\alpha P \cos^2(Q)}{2m} + \frac{1}{2}k \frac{2P}{\alpha}\sin^2(Q)
$$
$$
K(Q,P) = P \left( \frac{\alpha}{m}\cos^2(Q) + \frac{k}{\alpha}\sin^2(Q) \right)
$$
我们的目标是让 $K$ 尽可能简单，例如让它不依赖于 $Q$。观察括号内的项，如果系数满足 $\frac{\alpha}{m} = \frac{k}{\alpha}$，即 $\alpha^2 = km$，则括号内的项变为 $\frac{\alpha}{m}(\cos^2(Q) + \sin^2(Q)) = \frac{\alpha}{m}$，这是一个常数。
因此，如果我们策略性地选择 $\alpha = \sqrt{km}$，新的[哈密顿量](@entry_id:172864)就简化为：
$$
K(P) = \frac{\sqrt{km}}{m} P = \sqrt{\frac{k}{m}} P = \omega P
$$
其中 $\omega = \sqrt{k/m}$ 是谐振子的[角频率](@entry_id:261565)。这个新的[哈密顿量](@entry_id:172864)不依赖于 $Q$，所以 $P$ 是一个[守恒量](@entry_id:150267)：$\dot{P} = -\frac{\partial K}{\partial Q} = 0$。这个例子完美地展示了如何通过精心设计一个母函数来找到系统的一个非平凡的守恒量，从而极大地简化了动力学问题。

#### [无穷小正则变换](@entry_id:164301) (ICT)

当一个[正则变换](@entry_id:178165)与[恒等变换](@entry_id:264671) ($Q=q, P=p$) 相差一个无穷小量时，我们称之为**[无穷小正则变换](@entry_id:164301) (Infinitesimal Canonical Transformation, ICT)**。设此变换由一个函数 $G(q,p)$ 和一个无穷小参数 $\epsilon$ 生成。其第二类母函数可以写成：
$$
F_2(q, P) = qP + \epsilon G(q, P)
$$
[恒等变换](@entry_id:264671)本身由 $F_2 = qP$ 生成，而 $\epsilon G$ 则是无穷小的修正。
变换方程为：
$Q = \frac{\partial F_2}{\partial P} = q + \epsilon \frac{\partial G}{\partial P}$
$p = \frac{\partial F_2}{\partial q} = P + \epsilon \frac{\partial G}{\partial q}$
将 $P = p - \epsilon \frac{\partial G}{\partial q}$ 代入第一个方程，并忽略 $\epsilon^2$ 的高阶项，我们得到 $Q \approx q + \epsilon \frac{\partial G(q,p)}{\partial p}$。因此，坐标的无穷小变化量为：
$\delta q = Q - q = \epsilon \frac{\partial G}{\partial p}$
$\delta p = P - p = -\epsilon \frac{\partial G}{\partial q}$
对于相空间中的任意函数 $f(q,p)$，其在一阶无穷小变化为：
$$
\delta f = f(Q,P) - f(q,p) \approx \frac{\partial f}{\partial q}\delta q + \frac{\partial f}{\partial p}\delta p = \epsilon \left(\frac{\partial f}{\partial q}\frac{\partial G}{\partial p} - \frac{\partial f}{\partial p}\frac{\partial G}{\partial q}\right)
$$
括号内的表达式正是[泊松括号](@entry_id:151133) $\{f, G\}$。因此，我们得到了一个极为重要的结果：
$$
\delta f = \epsilon \{f, G\}
$$
这表明，任何函数 $G(q,p)$ 都可以被看作一个[无穷小正则变换](@entry_id:164301)的**生成元**，它所引起的任意物理量 $f$ 的变化量由 $f$ 与 $G$ 的泊松括号决定。

例如，考虑一个由 $G(q,p) = qp$ 生成的ICT，它作用于一个[谐振子](@entry_id:155622)系统 $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2 q^2$ [@problem_id:1246478]。[哈密顿量](@entry_id:172864)的一阶变化 $\delta H$ 是：
$$
\delta H = \epsilon \{H, G\} = \epsilon \left( \frac{\partial H}{\partial q}\frac{\partial G}{\partial p} - \frac{\partial H}{\partial p}\frac{\partial G}{\partial q} \right)
$$
计算各[偏导数](@entry_id:146280)：$\frac{\partial H}{\partial q} = m\omega^2 q$, $\frac{\partial H}{\partial p} = \frac{p}{m}$, $\frac{\partial G}{\partial q} = p$, $\frac{\partial G}{\partial p} = q$。
代入得：
$$
\delta H = \epsilon \left( (m\omega^2 q)(q) - \left(\frac{p}{m}\right)(p) \right) = \epsilon \left( m\omega^2 q^2 - \frac{p^2}{m} \right)
$$
这个结果不仅展示了ICT的计算方法，更揭示了深刻的物理内涵。时间演化本身就是一种连续的[无穷小正则变换](@entry_id:164301)，其生成元正是[哈密顿量](@entry_id:172864) $H$ 本身。因此，任何物理量 $f$ 的时间演化方程可以写作 $\frac{df}{dt} = \{f, H\} + \frac{\partial f}{\partial t}$。如果一个物理量 $A$ 的[泊松括号](@entry_id:151133)与[哈密顿量](@entry_id:172864)为零，$\{A, H\} = 0$，则 $A$ 就是一个守恒量。这为我们从对称性和生成元的角度理解守恒律提供了坚实的基础。

总之，母函数不仅是执行[正则变换](@entry_id:178165)的技术工具，它们也构成了哈密顿力学理论结构的支柱，连接了[坐标变换](@entry_id:172727)、守恒律和系统的动力学演化。