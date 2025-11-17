## 引言
[哈密顿力学](@entry_id:146202)是理论物理的基石，它不仅是[牛顿力学](@entry_id:162125)或[拉格朗日力学](@entry_id:147054)的一种等价表述，更是一种能够揭示动力学系统内在几何结构与对称性的深刻语言。然而，从学生在初级课程中学到的经典哈密顿坐标方程，到其在[辛几何](@entry_id:160783)与泊松[流形](@entry_id:153038)上的抽象推广，往往存在着一条概念上的鸿沟，而后者正是现代物理与数学研究中的标准工具。本文旨在系统地跨越这一鸿沟，带领读者从基础原理出发，深入探索[哈密顿力学](@entry_id:146202)的现代几何框架及其在广阔科学领域中的强大生命力。

在接下来的内容中，我们将分三步构建完整的知识图景。首先，在 **“原理与机制”** 一章中，我们将建立[哈密顿向量场](@entry_id:270696)、辛结构和[泊松括号](@entry_id:151133)等核心几何概念，揭示[哈密顿动力学](@entry_id:156273)优雅的数学本质。随后，在 **“应用与跨学科联系”** 一章，我们将展示这些抽象工具如何在从[天体力学](@entry_id:147389)到[量子场论](@entry_id:138177)的多个学科中，为理解守恒律、可积性与对称性提供无可比拟的洞见。最后，通过 **“动手实践”** 部分，您将有机会通过解决具体问题来巩固和应用所学知识。让我们首先深入哈密顿力学的核心，探索其优雅的原理与机制。

## 原理与机制

本章将深入探讨[哈密顿力学](@entry_id:146202)的核心原理与机制。我们将从经典的[哈密顿方程](@entry_id:156213)出发，逐步过渡到其优雅的几何表述，即[辛几何](@entry_id:160783)。在此框架下，我们将引入[哈密顿向量场](@entry_id:270696)、泊松括号和[正则变换](@entry_id:178165)等关键概念。通过这些工具，我们不仅能够以更深刻的视角理解动力学演化，还能揭示物理系统背后优美的[对称性与守恒律](@entry_id:160300)。

### [哈密顿函数](@entry_id:172864)与哈密顿方程

从[拉格朗日力学](@entry_id:147054)过渡到哈密顿力学的核心一步，是将描述体系的坐标从[构型空间](@entry_id:149531)（由[广义坐标](@entry_id:156576) $q$ 张成）扩展到**相空间**（由[广义坐标](@entry_id:156576) $q$ 和其共轭的[广义动量](@entry_id:165699) $p$共同张成）。对于一个具有 $n$ 个自由度的系统，其相空间是一个 $2n$ 维的空间，坐标为 $(q_1, \dots, q_n, p_1, \dots, p_n)$。

系统的动力学由一个定义在相空间上的光滑函数——**[哈密顿函数](@entry_id:172864)** $H(q, p)$ 所支配。在许多物理情境中，[哈密顿函数](@entry_id:172864)代表系统的总能量。给定[哈密顿函数](@entry_id:172864)，系统状态随时间的演化遵循一组[一阶微分方程](@entry_id:173139)，即**[哈密顿方程](@entry_id:156213)**：

$$
\dot{q}_i = \frac{\partial H}{\partial p_i}, \quad \dot{p}_i = - \frac{\partial H}{\partial q_i}
$$

其中 $i=1, \dots, n$，上方的点表示对时间的导数。这组方程是哈密顿力学的基石，它以一种高度对称的形式描述了相空间中每一点的运动趋势。

### 几何表述：辛结构与[哈密顿向量场](@entry_id:270696)

哈密顿方程的对称性暗示了相空间具有一种深刻的内在几何结构。这种结构被称为**辛结构**。对于一个具有一个自由度的系统，其二维相空间 $\mathbb{R}^2$ 上的**标准辛形式**是一个2-形式，记作 $\omega$：

$$
\omega = dq \wedge dp
$$

在 $2n$ 维相空间中，标准辛形式推广为 $\omega = \sum_{i=1}^n dq_i \wedge dp_i$。[辛形式](@entry_id:165896)为我们提供了一种测量相空间中“面积”的方法，但更重要的是，它为每个[哈密顿函数](@entry_id:172864) $H$ 唯一地确定了一个向量场，即**[哈密顿向量场](@entry_id:270696)** $X_H$。

$X_H$ 描述了由 $H$ 生成的动力学流。它与 $H$ 的关系由以下内在的[几何方程](@entry_id:173321)定义：

$$
\iota_{X_H}\omega = dH
$$

这里，$dH$ 是 $H$ 的外微分，$dH = \frac{\partial H}{\partial q} dq + \frac{\partial H}{\partial p} dp$。$\iota_{X_H}\omega$ 表示向量场 $X_H$ 与[2-形式](@entry_id:188008) $\omega$ 的**[内积](@entry_id:158127)**。如果我们将[哈密顿向量场](@entry_id:270696)写为 $X_H = A(q,p)\frac{\partial}{\partial q} + B(q,p)\frac{\partial}{\partial p}$，那么上述几何关系就精确地还原为我们熟悉的[哈密顿方程](@entry_id:156213)：

$$
\iota_{X_H}(dq \wedge dp) = A \, dp - B \, dq
$$

$$
dH = \frac{\partial H}{\partial p} dp + \frac{\partial H}{\partial q} dq
$$

比较 $dp$ 和 $dq$ 的系数，我们得到 $A = \frac{\partial H}{\partial p}$ 和 $-B = \frac{\partial H}{\partial q}$，即 $\dot{q} = A$ 和 $\dot{p} = B$。这表明，看似抽象的几何定义 $\iota_{X_H}\omega = dH$ 是[哈密顿方程](@entry_id:156213)更基本、更普适的表达。

这个关系是双向的。给定一个[哈密顿函数](@entry_id:172864) $H$，我们可以唯一确定其[哈密顿向量场](@entry_id:270696) $X_H$。反之，给定一个向量场 $X$，如果存在一个函数 $H$ 使得 $X=X_H$，我们就称 $X$ 是[哈密顿向量场](@entry_id:270696)。例如，考虑相空间 $\mathbb{R}^2$ 上的一个向量场 $X = q^2 \frac{\partial}{\partial q} - 2qp \frac{\partial}{\partial p}$ [@problem_id:962932]。为了找到生成它的[哈密顿函数](@entry_id:172864) $H(q,p)$，我们利用哈密顿方程：

$$
\frac{\partial H}{\partial p} = q^2
$$
$$
-\frac{\partial H}{\partial q} = -2qp \implies \frac{\partial H}{\partial q} = 2qp
$$

对第一个方程关于 $p$ 积分，我们得到 $H(q,p) = q^2 p + f(q)$，其中 $f(q)$ 是一个只依赖于 $q$ 的任意函数。接着，对这个表达式关于 $q$ 求导，并与第二个方程比较：

$$
\frac{\partial H}{\partial q} = 2qp + f'(q) = 2qp
$$

这要求 $f'(q)=0$，意味着 $f(q)$ 是一个常数 $C$。因此，所有能生成该向量场的[哈密顿函数](@entry_id:172864)都具有 $H(q,p) = q^2 p + C$ 的形式。如果我们补充一个条件，例如 $H(2, 1) = 5$，我们就可以唯一确定这个常数：$(2)^2(1) + C = 5 \implies C = 1$。最终得到 $H(q,p) = q^2 p + 1$。

[哈密顿方程](@entry_id:156213)的解描述了相空间中的一条轨迹，称为**[积分曲线](@entry_id:161858)**。从任意初始点 $(q_0, p_0)$ 出发，系统随时间的演化由一个单参数映射族 $\Phi_t^H$ 描述，该映射族被称为**哈密顿流**：$\Phi_t^H(q_0, p_0) = (q(t), p(t))$。我们也可以从已知的流反推出生成它的[哈密顿函数](@entry_id:172864)。设想一个系统的演化由以下[线性变换](@entry_id:149133)给出 [@problem_id:962889]：

$$
\begin{pmatrix} q(t) \\ p(t) \end{pmatrix} = \begin{pmatrix} \cosh(\alpha t) & \frac{1}{\beta}\sinh(\alpha t) \\ \beta\sinh(\alpha t) & \cosh(\alpha t) \end{pmatrix} \begin{pmatrix} q_0 \\ p_0 \end{pmatrix}
$$

为了找到对应的[哈密顿函数](@entry_id:172864)，我们首先通过对时间求导来找到向量场 $(\dot{q}, \dot{p})$：

$$
\dot{q}(t) = \alpha\sinh(\alpha t) q_0 + \frac{\alpha}{\beta}\cosh(\alpha t) p_0 = \frac{\alpha}{\beta} \left( \beta\sinh(\alpha t) q_0 + \cosh(\alpha t) p_0 \right) = \frac{\alpha}{\beta} p(t)
$$
$$
\dot{p}(t) = \alpha\beta\cosh(\alpha t) q_0 + \alpha\sinh(\alpha t) p_0 = \alpha\beta \left( \cosh(\alpha t) q_0 + \frac{1}{\beta}\sinh(\alpha t) p_0 \right) = \alpha\beta q(t)
$$

现在我们有了[哈密顿方程](@entry_id:156213)：$\dot{q} = \frac{\alpha}{\beta} p$ 和 $\dot{p} = \alpha\beta q$。将其与 $\dot{q} = \partial H / \partial p$ 和 $\dot{p} = -\partial H / \partial q$ 对比，可得：

$$
\frac{\partial H}{\partial p} = \frac{\alpha}{\beta} p, \quad \frac{\partial H}{\partial q} = -\alpha\beta q
$$

通[过积分](@entry_id:753033)，我们可以重构[哈密顿函数](@entry_id:172864)。假设 $H$ 是 $q$ 和 $p$ 的二次型，积分后可得 $H(q,p) = \frac{\alpha}{2} (\frac{p^2}{\beta} - \beta q^2)$，这里我们已使用[归一化条件](@entry_id:156486) $H(0,0)=0$。这个例子展示了动力学流与[哈密顿函数](@entry_id:172864)之间的深刻联系。

### 推广与深化：从[辛流形](@entry_id:161608)到泊松[流形](@entry_id:153038)

#### 一般[辛流形](@entry_id:161608)上的[哈密顿向量场](@entry_id:270696)

哈密顿力学的几何框架不仅限于具有标准[辛形式](@entry_id:165896)的 $\mathbb{R}^{2n}$。任何一个配备了辛形式（一个闭合的、非退化的2-形式）$\omega$ 的[流形](@entry_id:153038)，即**[辛流形](@entry_id:161608)**，都可以作为哈密顿系统的相空间。在这种更广阔的背景下，一个向量场 $X$ 被称为**[哈密顿向量场](@entry_id:270696)**，如果它与[辛形式](@entry_id:165896)的[内积](@entry_id:158127) $\iota_X \omega$ 是一个**闭[1-形式](@entry_id:270392)**，即 $d(\iota_X \omega) = 0$。

如果 $\iota_X \omega$ 不仅是闭的，而且是**恰当的**（即它可以表示为某个函数 $H$ 的外微分，$\iota_X \omega = dH$），那么我们就说 $X$ 是一个**恰当[哈密顿向量场](@entry_id:270696)**，而 $H$ 是其[哈密顿函数](@entry_id:172864)。

这个定义的威力在于它适用于任何[辛形式](@entry_id:165896)，而不仅仅是标准形式。考虑一个在相空间[上半平面](@entry_id:199119) $p>0$ 运动的粒子，其几何由一个非标准的[辛形式](@entry_id:165896) $\omega = \frac{1}{p^2} dq \wedge dp$ 定义 [@problem_id:962924]。给定一个向量场 $X = (p^4 + \lambda q^2 p^2)\frac{\partial}{\partial q} - 4qp^3\frac{\partial}{\partial p}$，我们可以通过检验 $d(\iota_X \omega) = 0$ 来确定参数 $\lambda$ 的值，以确保该向量场是哈密顿的。

首先，计算[内积](@entry_id:158127) $\iota_X \omega$：
$$
\iota_X \omega = \iota_{(p^4 + \lambda q^2 p^2)\partial_q - 4qp^3\partial_p} \left(\frac{1}{p^2} dq \wedge dp\right) = \frac{p^4 + \lambda q^2 p^2}{p^2} dp - \frac{-4qp^3}{p^2} dq = (p^2 + \lambda q^2) dp + 4qp \, dq
$$
这个1-形式是 $\alpha = \alpha_q dq + \alpha_p dp$，其中 $\alpha_q = 4qp$ 且 $\alpha_p = p^2 + \lambda q^2$。它闭合的条件是 $\frac{\partial \alpha_p}{\partial q} - \frac{\partial \alpha_q}{\partial p} = 0$。计算[偏导数](@entry_id:146280)：
$$
\frac{\partial \alpha_p}{\partial q} = \frac{\partial}{\partial q}(p^2 + \lambda q^2) = 2\lambda q
$$
$$
\frac{\partial \alpha_q}{\partial p} = \frac{\partial}{\partial p}(4qp) = 4q
$$
因此，闭合条件变为 $2\lambda q - 4q = 0$，即 $(2\lambda - 4)q = 0$。由于这对所有 $q$ 都必须成立，我们得到 $2\lambda - 4 = 0$，从而唯一确定 $\lambda = 2$。

#### [泊松括号](@entry_id:151133)与泊松[流形](@entry_id:153038)

除了通过向量场，我们还可以用一种[代数结构](@entry_id:137052)来描述[哈密顿动力学](@entry_id:156273)，这就是**泊松括号**。对于相空间上的任意两个[光滑函数](@entry_id:267124)（即可观测量）$F(q,p)$ 和 $G(q,p)$，它们在标准辛结构下的[泊松括号](@entry_id:151133)定义为：

$$
\{F, G\} = \sum_{i=1}^n \left( \frac{\partial F}{\partial q_i}\frac{\partial G}{\partial p_i} - \frac{\partial F}{\partial p_i}\frac{\partial G}{\partial q_i} \right)
$$

利用泊松括号，任意可观测量 $F$ 的[时间演化](@entry_id:153943)可以简洁地表示为：

$$
\frac{dF}{dt} = \{F, H\}
$$

特别地，当 $F$ 分别取 $q_i$ 和 $p_i$ 时，上式就退化为哈密顿方程。

一个有效的[泊松括号](@entry_id:151133)必须满足三个基本性质：
1.  **[反对称性](@entry_id:261893)**: $\{F, G\} = -\{G, F\}$
2.  **莱布尼兹法则**: $\{F, GH\} = \{F, G\}H + G\{F, H\}$
3.  **雅可比恒等式**: $\{F, \{G, K\}\} + \{G, \{K, F\}\} + \{K, \{F, G\}\} = 0$

[雅可比恒等式](@entry_id:140480)是一个深刻的约束，它保证了动力学的一致性。任何配备了满足这三个性质的括号运算的[流形](@entry_id:153038)被称为**泊松[流形](@entry_id:153038)**。[辛流形](@entry_id:161608)是泊松[流形](@entry_id:153038)的一个重要特例，但泊松[流形](@entry_id:153038)的概念更为广泛。

我们可以构造一些非标准的括号，但它们不一定满足[雅可比恒等式](@entry_id:140480)。例如，考察一个由标准括号缩放而来的新括号 $\{F, G\}_* = \omega(q,p)\{F, G\}_{\text{can}}$ [@problem_id:962938]。一般而言，这样的构造会破坏雅可比恒等式。我们可以通过计算**雅可比子 (Jacobiator)** $J(A,B,C) = \{A, \{B, C\}_*\}_* + \{B, \{C, A\}_*\}_* + \{C, \{A, B\}_*\}_*$ 来检验。如果对任意函数 $A,B,C$ 都有 $J(A,B,C)=0$，那么该括号就是一个合法的[泊松括号](@entry_id:151133)。

泊松[流形](@entry_id:153038)的一个重要例子是[李代数](@entry_id:137954)的[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 上定义的**[李-泊松结构](@entry_id:157559)**。例如，与李代数 $\mathfrak{su}(2)$ 相关的相空间可以等同于 $\mathbb{R}^3$，其坐标为 $(x_1, x_2, x_3)$。其上的[李-泊松括号](@entry_id:159190)为：

$$
\{f, g\} = \mathbf{x} \cdot (\nabla f \times \nabla g) = \sum_{i,j,k=1}^3 \epsilon_{ijk} x_k \frac{\partial f}{\partial x_i} \frac{\partial g}{\partial x_j}
$$

其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。让我们计算两个函数 $F = \alpha x_1^2 + \beta x_2$ 和 $G = \gamma x_2^2 + \delta x_3$ 的[李-泊松括号](@entry_id:159190) [@problem_id:962910]。首先，计算它们的梯度：

$$
\nabla F = (2\alpha x_1, \beta, 0), \quad \nabla G = (0, 2\gamma x_2, \delta)
$$

然后计算叉乘：

$$
\nabla F \times \nabla G = (\beta\delta, -2\alpha\delta x_1, 4\alpha\gamma x_1 x_2)
$$

最后，与位置向量 $\mathbf{x} = (x_1, x_2, x_3)$ 做[点积](@entry_id:149019)：

$$
\{F, G\} = x_1(\beta\delta) + x_2(-2\alpha\delta x_1) + x_3(4\alpha\gamma x_1 x_2) = \beta\delta x_1 - 2\alpha\delta x_1 x_2 + 4\alpha\gamma x_1 x_2 x_3
$$

这个例子中的[泊松括号](@entry_id:151133)在原点 $\mathbf{x}=0$ 处是退化的，因此该[流形](@entry_id:153038)不是[辛流形](@entry_id:161608)，这展示了泊松[流形](@entry_id:153038)概念的广[泛性](@entry_id:161765)。

### 对称性、守恒律与[正则变换](@entry_id:178165)

#### 守恒律与泊松定理

在哈密顿框架中，[对称性与守恒律](@entry_id:160300)之间存在着直接而优美的联系。一个可观测量（由函数 $F$ 代表）是**[守恒量](@entry_id:150267)**（或运动常数），当且仅当它在哈密顿流下保持不变，即 $\frac{dF}{dt} = 0$。根据[演化方程](@entry_id:268137) $\frac{dF}{dt} = \{F, H\}$，这等价于：

$$
\{F, H\} = 0
$$

这个简洁的条件是[诺特定理](@entry_id:145690)在[哈密顿力学](@entry_id:146202)中的体现。守恒量所构成的集合自身也具有一个封闭的[代数结构](@entry_id:137052)，这由**泊松定理**所保证：若 $F$ 和 $G$ 都是系统的守恒量，则它们的泊松括号 $\{F, G\}$ 也必定是守恒量。

该定理的证明是雅可比恒等式的一个直接应用：
$$
\{\{F, G\}, H\} = -\{\{G, H\}, F\} - \{\{H, F\}, G\}
$$
由于 $\{F, H\} = 0$ 和 $\{G, H\} = 0$，上式右边为零，因此 $\{\{F, G\}, H\} = 0$，证明了 $\{F, G\}$ 也是一个[守恒量](@entry_id:150267)。

一个经典的例子是[中心力](@entry_id:267832)场中的角动量。对于一个在[中心势](@entry_id:148563) $V(r)$ 中运动的粒子，其[哈密顿量](@entry_id:172864)为 $H = \frac{1}{2m}(p_x^2 + p_y^2 + p_z^2) + V(r)$。角动量的三个分量 $L_x, L_y, L_z$ 都是[守恒量](@entry_id:150267)，即 $\{L_i, H\}=0$。根据泊松定理，它们之间的[泊松括号](@entry_id:151133)也应该是守恒量。我们可以直接验证这一点 [@problem_id:963092]。首先计算 $\{L_x, L_y\}$：

$$
\{L_x, L_y\} = \{y p_z - z p_y, z p_x - x p_z\} = x p_y - y p_x = L_z
$$

现在我们需要验证 $\{L_z, H\}=0$。由于 $\{L_z, H\} = \{L_z, T\} + \{L_z, V(r)\}$，我们分别计算这两项。
$$
\{L_z, T\} = \{x p_y - y p_x, \frac{1}{2m}(p_x^2+p_y^2+p_z^2)\} = \frac{1}{m}(p_y p_x - p_x p_y) = 0
$$
$$
\{L_z, V(r)\} = \{x p_y - y p_x, V(\sqrt{x^2+y^2+z^2})\} = y\frac{\partial V}{\partial x} - x\frac{\partial V}{\partial y} = y\frac{V'(r)x}{r} - x\frac{V'(r)y}{r} = 0
$$
因此，我们得到 $\{\{L_x, L_y\}, H\} = \{L_z, H\} = 0$，这完美地印证了泊松定理。

#### [正则变换](@entry_id:178165)

**[正则变换](@entry_id:178165)**是相空间坐标 $(q,p)$ 到新坐标 $(Q,P)$ 的一种特殊变换，它保持[哈密顿方程](@entry_id:156213)的形式不变。从几何上看，这意味着变换保持了辛结构；从代数上看，这意味着变换保持了基本泊松括号的关系：

$$
\{Q_i, P_j\} = \delta_{ij}, \quad \{Q_i, Q_j\} = 0, \quad \{P_i, P_j\} = 0
$$
其中括号是关于原坐标 $(q,p)$ 计算的。

对于连接新旧坐标列向量 $Z=(Q,P)^T$ 和 $z=(q,p)^T$ 的线性变换 $Z=Mz$，其成为[正则变换](@entry_id:178165)的充要条件是矩阵 $M$ 是一个**[辛矩阵](@entry_id:142706)**，即满足：

$$
M^T J M = J, \quad \text{其中} \quad J = \begin{pmatrix} 0_n & I_n \\ -I_n & 0_n \end{pmatrix}
$$

这里 $I_n$ 和 $0_n$ 分别是 $n \times n$ 的[单位矩阵](@entry_id:156724)和零矩阵。例如，考虑一个 $n=2$ 的系统，一个[分块矩阵](@entry_id:148435) $M = \begin{pmatrix} A & B \\ C & D \end{pmatrix}$ 成为[辛矩阵](@entry_id:142706)需要其子块满足 $A^T D - C^T B = I_2$ 等一系列条件 [@problem_id:963018]。这些条件保证了变换保持了相空间的内在几何。

对于[非线性变换](@entry_id:636115)，**母函数**是构造[正则变换](@entry_id:178165)的有力工具。存在四类母函数 $F_1(q,Q), F_2(q,P), F_3(p,Q), F_4(p,P)$，它们通过勒让德变换相互关联。例如，给定一个1类母函数 $F_1(q,Q)$，变换方程由下式给出：

$$
p = \frac{\partial F_1}{\partial q}, \quad P = -\frac{\partial F_1}{\partial Q}
$$

而相应的2类母函数 $F_2(q,P)$ 可以通过[勒让德变换](@entry_id:146727)得到：$F_2(q,P) = F_1(q,Q) + PQ$。例如，从 $F_1(q,Q) = \frac{1}{2\alpha}(q^2+Q^2) - \frac{\beta}{\alpha} qQ$ 出发 [@problem_id:962892]，我们可以首先导出变换方程 $P = \frac{\beta}{\alpha}q - \frac{1}{\alpha}Q$，从中解出 $Q = \beta q - \alpha P$。然后将 $Q$ 代入勒让德变换的表达式，最终可以得到对应的2类[母函数](@entry_id:146702) $F_2(q,P) = \frac{1-\beta^2}{2\alpha}q^2 + \beta qP - \frac{\alpha}{2}P^2$。

### [哈密顿动力学](@entry_id:156273)的后果：[刘维尔定理](@entry_id:191167)

哈密顿流的一个深刻后果是它保持相空间的体积不变。这被称为**[刘维尔定理](@entry_id:191167)**。从几何上讲，哈密顿流 $\Phi_t$ 保持[辛形式](@entry_id:165896)不变，即 $\Phi_t^*\omega = \omega$。由此可以推导出，由[辛形式](@entry_id:165896)定义的[体积元](@entry_id:267802) $\Omega = \frac{1}{n!}\omega \wedge \dots \wedge \omega$ 也是[不变量](@entry_id:148850)。

这意味着，如果我们将相空间中的一个初始区域看作是由大量系统初始状态组成的“流体”，那么在哈密顿流的作用下，这个区域的形状可能会发生剧烈变化，但其总体积始终保持恒定。

我们可以通过一个简单的例子直观地验证这一点。考虑由[哈密顿量](@entry_id:172864) $H=qp$ 生成的动力学 [@problem_id:963097]。[哈密顿方程](@entry_id:156213)为 $\dot{q}=q, \dot{p}=-p$，其解为 $q(t) = q_0 e^t, p(t) = p_0 e^{-t}$。现在考虑一个初始位于 $q \in [q_0, q_0+\Delta q], p \in [p_0, p_0+\Delta p]$ 的矩形区域 $R_0$。其面积为 $\Delta q \Delta p$。在时间 $t$ 之后，这个矩形的四个顶点演化到新位置，形成一个新的矩形 $R_t$。新矩形的边长变为 $\Delta q e^t$ 和 $\Delta p e^{-t}$。因此，新区域 $R_t$ 的面积为 $(\Delta q e^t)(\Delta p e^{-t}) = \Delta q \Delta p$，与初始面积完全相同。尽管矩形在 $q$ 方向被拉伸，在 $p$ 方向被压缩，但其总面积保持不变。

然而，需要注意的是，刘维尔定理中的“体积”是指由[辛形式](@entry_id:165896)自然诱导的体积元。[哈密顿向量场](@entry_id:270696)对于这个自然体积元是无散度的。如果我们使用一个不同的体[积度量](@entry_id:637352)，[哈密顿向量场](@entry_id:270696)的散度可能不为零。

例如，考虑一个具有非标准辛形式 $\omega = e^q dq \wedge dp$ 的相空间，以及[哈密顿量](@entry_id:172864) $H=\frac{p^2}{2m}$ [@problem_id:963000]。通过 $\iota_{X_H}\omega=dH$ 可得[哈密顿向量场](@entry_id:270696)为 $X_H = \frac{p}{m e^q}\frac{\partial}{\partial q}$。现在，我们计算这个向量场相对于**标准欧几里得体积元** $dq \wedge dp$ 的散度：

$$
\text{div}(X_H) = \frac{\partial X^q}{\partial q} + \frac{\partial X^p}{\partial p} = \frac{\partial}{\partial q}\left(\frac{p}{m e^q}\right) + 0 = -\frac{p}{m e^q}
$$

这个结果不为零。这并不与刘维尔定理矛盾。它恰恰说明了，[哈密顿向量场](@entry_id:270696) $X_H$ 保持的[体积元](@entry_id:267802)是 $\omega = e^q dq \wedge dp$，而不是我们用来计算散度的标准[体积元](@entry_id:267802) $dq \wedge dp$。这个例子强调了在更广义的几何框架下精确理解[刘维尔定理](@entry_id:191167)的重要性。