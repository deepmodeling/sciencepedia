## 引言
在线性代数与[微分方程](@entry_id:264184)的交汇处，[常系数](@entry_id:269842)[线性微分方程组](@entry_id:155297) $\mathbf{x}'(t) = A \mathbf{x}(t)$ 是描述从物理[振动](@entry_id:267781)到[化学反应](@entry_id:146973)等众多系统的基础模型。其解的核心在于计算[矩阵指数](@entry_id:139347) $\exp(At)$。当矩阵 $A$ 可[对角化](@entry_id:147016)时，这一计算过程相对直接，但当 $A$ 不可[对角化](@entry_id:147016)时，我们便遇到了一个关键的知识鸿沟：如何系统地求解这[类方程](@entry_id:144428)组，并理解其解的独特结构？

本文旨在填补这一鸿沟，全面阐述约当标准型（Jordan Canonical Form）在解决此类问题中的强大作用。通过学习本文，您将不仅掌握一种计算方法，更能深入理解系统动态行为背后的深刻数学原理。

文章分为三个核心部分：在第一章**“原理与机制”**中，我们将揭示约当分解如何成为求解不可对角化系统的通用钥匙，并从根本上解释解中为何会出现 $t^k\exp(\lambda t)$ 这样的多项式-指数项。接着，在第二章**“应用与跨学科联系”**中，我们将理论付诸实践，探讨约当型在分析系统稳定性、理解临界阻尼和共振等现象，以及在现代计算科学中的重要角色。最后，在**“动手实践”**部分，您将通过解决一系列精心设计的问题，巩固并应用所学知识，将理论转化为可操作的技能。

让我们开始这段探索之旅，揭开不可对角化系统背后隐藏的结构与美感。

## 原理与机制

在上一章中，我们已经了解到[常系数](@entry_id:269842)[线性微分方程组](@entry_id:155297) $\mathbf{x}'(t) = A \mathbf{x}(t)$ 的解可以用矩阵指数表示为 $\mathbf{x}(t) = \exp(At) \mathbf{x}(0)$。当矩阵 $A$ 可[对角化](@entry_id:147016)时，即 $A=PDP^{-1}$，其中 $D$ 为[对角矩阵](@entry_id:637782)，计算[矩阵指数](@entry_id:139347)相对直接：$\exp(At) = P \exp(Dt) P^{-1}$，而 $\exp(Dt)$ 是一个[对角矩阵](@entry_id:637782)，其对角线元素为 $e^{\lambda_i t}$，其中 $\lambda_i$ 是 $A$ 的[特征值](@entry_id:154894)。然而，当矩阵 $A$ 不可对角化时，情况变得更为复杂。本章将深入探讨如何利用约当标准型（Jordan Canonical Form）来系统地求解这[类方程](@entry_id:144428)组，并揭示解的结构中所蕴含的深刻机理及其对系统动态行为的影响。

### 通过[矩阵指数](@entry_id:139347)的通解

处理[不可对角化矩阵](@entry_id:148047) $A$ 的关键工具是约当分解。任何一个方阵 $A$ 都可以通过[相似变换](@entry_id:152935)化为其约当标准型 $J$，即存在一个可逆矩阵 $P$，使得 $A = PJP^{-1}$。矩阵 $P$ 的列由 $A$ 的[特征向量](@entry_id:151813)和[广义特征向量](@entry_id:152349)构成，构成了所谓的**约当基**。约当标准型矩阵 $J$ 是一个分[块对角矩阵](@entry_id:145530)，每个对角块是一个**约当块**。

利用这个分解，我们可以推导[求解微分方程](@entry_id:137471)组的通用公式。与可[对角化](@entry_id:147016)情况类似，我们可以通过以下方式计算矩阵指数 $\exp(At)$：
$$
\exp(At) = \exp(PJP^{-1}t) = \sum_{k=0}^{\infty} \frac{(PJP^{-1}t)^k}{k!} = \sum_{k=0}^{\infty} \frac{P(Jt)^k P^{-1}}{k!} = P \left( \sum_{k=0}^{\infty} \frac{(Jt)^k}{k!} \right) P^{-1} = P\exp(Jt)P^{-1}
$$
因此，微分方程组的解可以表示为：
$$
\mathbf{x}(t) = P\exp(Jt)P^{-1}\mathbf{x}(0)
$$
这个公式是解决所有[常系数](@entry_id:269842)[线性微分方程组](@entry_id:155297)的基石 [@problem_id:1348235]。它将原问题分解为三个步骤：
1.  **坐标变换**：通过左乘 $P^{-1}$，将[初始条件](@entry_id:152863) $\mathbf{x}(0)$ 从标准[基变换](@entry_id:189626)到约当基，得到 $\mathbf{y}(0) = P^{-1}\mathbf{x}(0)$。
2.  **在约当基中演化**：在由[广义特征向量](@entry_id:152349)构成的约当基中，系统的演化由更简单的矩阵 $J$ 描述。在新坐标 $\mathbf{y}(t) = P^{-1}\mathbf{x}(t)$ 下，原[方程组](@entry_id:193238) $\mathbf{x}'=A\mathbf{x}$ 变为 $\mathbf{y}' = J\mathbf{y}$。其解为 $\mathbf{y}(t) = \exp(Jt)\mathbf{y}(0)$。
3.  **变换回标准基**：通过左乘 $P$，将解从约当[基变换](@entry_id:189626)回标准基，得到最终解 $\mathbf{x}(t) = P\mathbf{y}(t) = P\exp(Jt)P^{-1}\mathbf{x}(0)$。

这个过程的优雅之处在于，它将一个耦合的、难以直接处理的系统，通过[基变换](@entry_id:189626)，转化为一个近乎[解耦](@entry_id:637294)的系统（由 $J$ 描述），在更简单的[坐标系](@entry_id:156346)中求解后，再变换回来。现在的核心任务就变成了计算 $\exp(Jt)$。

### 约当形式的矩阵指数

约当矩阵 $J$ 是一个分[块对角矩阵](@entry_id:145530)，其形式为：
$$
J = \begin{pmatrix} J_1  0  \cdots  0 \\ 0  J_2  \cdots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \cdots  J_s \end{pmatrix}
$$
其中每个 $J_k$ 是一个与[特征值](@entry_id:154894) $\lambda_k$ 相关的约当块。由于 $J$ 是分块[对角形式](@entry_id:264850)，其矩阵指数也是分块对角的：
$$
\exp(Jt) = \begin{pmatrix} \exp(J_1 t)  0  \cdots  0 \\ 0  \exp(J_2 t)  \cdots  0 \\ \vdots  \vdots  \ddots  \vdots \\ 0  0  \cdots  \exp(J_s t) \end{pmatrix}
$$
因此，我们只需关注如何计算单个约当块的指数。一个大小为 $m \times m$、[特征值](@entry_id:154894)为 $\lambda$ 的约当块 $J_k$ 可以写成一个对角矩阵和一个**[幂零矩阵](@entry_id:152732)**（nilpotent matrix）之和：
$$
J_k = \begin{pmatrix} \lambda  1  0  \cdots \\ 0  \lambda  1  \cdots \\ \vdots   \ddots  1 \\ 0  \cdots  0  \lambda \end{pmatrix} = \lambda I + N
$$
其中 $I$ 是单位矩阵，$N$ 是一个主对角线和次对角线全为零，仅在第一条上对角线（superdiagonal）上元素为1的矩阵。这个矩阵 $N$ 具有 $N^m=0$ 的性质。

由于对角矩阵 $\lambda I$ 与任何矩阵都可交换，我们有 $\exp(J_k t) = \exp((\lambda I + N)t) = \exp(\lambda t I) \exp(Nt) = \exp(\lambda t) \exp(Nt)$。计算 $\exp(Nt)$ 因 $N$ 的[幂零性](@entry_id:147926)质而变得异常简单。矩阵指数的级数定义会自然截断：
$$
\exp(Nt) = I + tN + \frac{t^2}{2!}N^2 + \dots + \frac{t^{m-1}}{(m-1)!}N^{m-1}
$$
例如，对于一个 $3 \times 3$ 的约当块，其[特征值](@entry_id:154894)为 $\lambda = -2$ [@problem_id:1348236]，矩阵为：
$$
A = \begin{pmatrix} -2  1  0 \\ 0  -2  1 \\ 0  0  -2 \end{pmatrix} = -2I + N, \quad N = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ 0  0  0 \end{pmatrix}
$$
这里 $N^2 = \begin{pmatrix} 0  0  1 \\ 0  0  0 \\ 0  0  0 \end{pmatrix}$ 且 $N^3 = 0$。因此，
$$
\exp(Nt) = I + tN + \frac{t^2}{2}N^2 = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} + t\begin{pmatrix} 0  1  0 \\ 0  0  1 \\ 0  0  0 \end{pmatrix} + \frac{t^2}{2}\begin{pmatrix} 0  0  1 \\ 0  0  0 \\ 0  0  0 \end{pmatrix} = \begin{pmatrix} 1  t  t^2/2 \\ 0  1  t \\ 0  0  1 \end{pmatrix}
$$
于是，该约当块的[矩阵指数](@entry_id:139347)为：
$$
\exp(At) = \exp(-2t)\exp(Nt) = \exp(-2t)\begin{pmatrix} 1  t  t^2/2 \\ 0  1  t \\ 0  0  1 \end{pmatrix} = \begin{pmatrix} \exp(-2t)  t\exp(-2t)  \frac{t^2}{2}\exp(-2t) \\ 0  \exp(-2t)  t\exp(-2t) \\ 0  0  \exp(-2t) \end{pmatrix}
$$
这个结果清晰地展示了多项式因子 $t$ 和 $t^2$ 是如何从[幂零矩阵](@entry_id:152732) $N$ 的结构中自然产生的。

### 多项式-指数形式解的来源

上一节的计算揭示了解中出现 $t^k \exp(\lambda t)$ 形式项的数学根源。当矩阵 $A$ 的某个[特征值](@entry_id:154894) $\lambda$ 的**[几何重数](@entry_id:155584)**（geometric multiplicity，即线性无关[特征向量](@entry_id:151813)的个数）小于其**[代数重数](@entry_id:154240)**（algebraic multiplicity，即[特征方程](@entry_id:265849)中[根的重数](@entry_id:635479)）时，该[特征值](@entry_id:154894)对应的约当标准型中必然包含至少一个尺寸大于 $1 \times 1$ 的约当块。正是这些尺寸大于1的约当块，导致了解中出现多项式与指数函数相乘的项 [@problem_id:1348256]。

一个尺寸为 $m$ 的约当块，对应于一个由1个[特征向量](@entry_id:151813) $\mathbf{v}$ 和 $m-1$ 个**[广义特征向量](@entry_id:152349)** $\mathbf{w}_1, \dots, \mathbf{w}_{m-1}$ 构成的链。它们满足：
$$
(A-\lambda I)\mathbf{v} = \mathbf{0}, \quad (A-\lambda I)\mathbf{w}_1 = \mathbf{v}, \quad (A-\lambda I)\mathbf{w}_2 = \mathbf{w}_1, \quad \dots
$$
对于一个 $2 \times 2$ 的约当块（$\lambda$ 的[代数重数](@entry_id:154240)为2，[几何重数](@entry_id:155584)为1），其对应的两个[基向量](@entry_id:199546)是[特征向量](@entry_id:151813) $\mathbf{v}$ 和[广义特征向量](@entry_id:152349) $\mathbf{w}$。系统的通解中，与这个块相关的部分可以写为：
$$
\mathbf{x}(t) = \exp(\lambda t) \left[ c_1 \mathbf{v} + c_2 (t\mathbf{v} + \mathbf{w}) \right]
$$
其中 $c_1$ 和 $c_2$ 是任意常数 [@problem_id:1348255]。这个表达式直观地展示了[广义特征向量](@entry_id:152349) $\mathbf{w}$ 如何引入了 $t$ 因子。第一部分 $c_1 \exp(\lambda t)\mathbf{v}$ 是我们熟悉的纯指数解。第二部分 $c_2 \exp(\lambda t)(t\mathbf{v} + \mathbf{w})$ 则是一个新的、线性无关的解，它包含一个随时间[线性增长](@entry_id:157553)的项 $t \exp(\lambda t)\mathbf{v}$。

总结来说，我们建立了以下关键联系：
-   **[代数重数](@entry_id:154240) vs. [几何重数](@entry_id:155584)**：一个[特征值](@entry_id:154894) $\lambda$ 的[几何重数](@entry_id:155584)小于其[代数重数](@entry_id:154240)，是系统不可对角化的标志。
-   **约当块尺寸**：[几何重数](@entry_id:155584)与[代数重数](@entry_id:154240)之差，决定了与 $\lambda$ 相关的约当块的“缺陷”程度。$\lambda$ 对应的最大约当块的尺寸 $m$ 决定了解中多项式因子的最高次数。
-   **解的结构**：如果与[特征值](@entry_id:154894) $\lambda$ 关联的最大约当块尺寸为 $m$，则解的各个分量中会出现 $\exp(\lambda t), t\exp(\lambda t), \dots, t^{m-1}\exp(\lambda t)$ 这些项的线性组合。

这一深刻的联系使我们能够从系统解的函数形式反推其内部结构。例如，如果我们通过实验观察到一个四维系统的解包含 $\exp(2t), t\exp(2t), \exp(-t), t\exp(-t)$ 这些项，我们就可以断定该系统的[系数矩阵](@entry_id:151473) $A$ 的约当标准型必然由一个对应于[特征值](@entry_id:154894) $\lambda=2$ 的 $2 \times 2$ 约当块和一个对应于[特征值](@entry_id:154894) $\lambda=-1$ 的 $2 \times 2$ 约当块构成 [@problem_id:1348259]。

### 示例分析

为了巩固上述原理，我们通过几个具体的例子来演示如何应用约当形式[求解微分方程](@entry_id:137471)组。

#### 示例 1：一个 $2 \times 2$ 不可对角化系统

考虑系统 $\mathbf{x}'(t) = A\mathbf{x}(t)$，其中 $A = \begin{pmatrix} -3  1 \\ -1  -1 \end{pmatrix}$，[初始条件](@entry_id:152863)为 $\mathbf{x}(0) = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$ [@problem_id:1348251]。

1.  **分析矩阵 $A$**：其特征多项式为 $\det(A-\lambda I) = (\lambda+2)^2$，因此有重根 $\lambda = -2$，[代数重数](@entry_id:154240)为2。求解 $(A-(-2)I)\mathbf{v}=\mathbf{0}$，即 $\begin{pmatrix} -1  1 \\ -1  1 \end{pmatrix}\mathbf{v}=\mathbf{0}$，得到唯一的[特征向量](@entry_id:151813)方向 $\mathbf{v} = (1,1)^T$。[几何重数](@entry_id:155584)为1，因此 $A$ 不可对角化。

2.  **计算[矩阵指数](@entry_id:139347)**：我们可以将 $A$ 写成 $A = -2I + B$，其中 $B = A+2I = \begin{pmatrix} -1  1 \\ -1  1 \end{pmatrix}$。容易验证 $B^2=0$，所以 $B$ 是[幂零矩阵](@entry_id:152732)。因此：
    $$
    \exp(At) = \exp(-2t)\exp(Bt) = \exp(-2t)(I+tB) = \exp(-2t)\begin{pmatrix} 1-t  t \\ -t  1+t \end{pmatrix}
    $$

3.  **求解**：代入[初始条件](@entry_id:152863)，
    $$
    \mathbf{x}(t) = \exp(At)\mathbf{x}(0) = \exp(-2t)\begin{pmatrix} 1-t  t \\ -t  1+t \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \exp(-2t)\begin{pmatrix} (1-t)+2t \\ -t+2(1+t) \end{pmatrix} = \exp(-2t)\begin{pmatrix} 1+t \\ 2+t \end{pmatrix}
    $$
    解的每个分量都包含了 $t\exp(-2t)$ 这一项，这正是 $A$ 不可[对角化](@entry_id:147016)的直接体现。

#### 示例 2：可对角化与不可[对角化](@entry_id:147016)系统的对比

考虑两个系统，它们都具有相同的[重复特征值](@entry_id:154579) $\lambda=2$，但结构不同 [@problem_id:1348244]。
系统 1: $\mathbf{x}'=A\mathbf{x}$，其中 $A = \begin{pmatrix} 2  0 \\ 0  2 \end{pmatrix}$。
系统 2: $\mathbf{y}'=B\mathbf{y}$，其中 $B = \frac{1}{3}\begin{pmatrix} 4  1 \\ -4  8 \end{pmatrix}$。
[初始条件](@entry_id:152863)均为 $\mathbf{x}(0) = \mathbf{y}(0) = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$。

对于系统1，$A=2I$ 是一个[对角矩阵](@entry_id:637782)。解非常简单：
$$
\mathbf{x}(t) = \exp(2It)\mathbf{x}(0) = \exp(2t)I \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \exp(2t)\begin{pmatrix} 1 \\ 1 \end{pmatrix}
$$
所以 $x_1(t) = \exp(2t)$。

对于系统2，矩阵 $B$ 的[特征多项式](@entry_id:150909)为 $\det(B-\lambda I) = (\lambda-2)^2$。它也只有一个[特征值](@entry_id:154894) $\lambda=2$。然而，它只有一个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，因此它不可对角化，其约当块是一个 $2 \times 2$ 块。我们用 $B = 2I+C$ 的方法，其中 $C=B-2I = \begin{pmatrix} -2/3  1/3 \\ -4/3  2/3 \end{pmatrix}$。可以验证 $C^2=0$。解为：
$$
\mathbf{y}(t) = \exp(Bt)\mathbf{y}(0) = \exp(2t)(I+tC)\mathbf{y}(0) = \exp(2t)\left(\begin{pmatrix} 1 \\ 1 \end{pmatrix} + t \begin{pmatrix} -1/3 \\ -2/3 \end{pmatrix}\right) = \exp(2t)\begin{pmatrix} 1-t/3 \\ 1-2t/3 \end{pmatrix}
$$
所以 $y_1(t) = \exp(2t)(1-t/3)$。

比较两个系统的第一个分量，我们看到 $y_1(t) - x_1(t) = -\frac{t}{3}\exp(2t)$。这个差异项直接源于系统2中存在的非零幂零部分 $C$。尽管两个系统都由相同的[特征值](@entry_id:154894) $\lambda=2$ 主导，但不可[对角化](@entry_id:147016)系统的解中多出的 $t$ 因子导致了截然不同的动态行为。

#### 示例 3：一个物理模型——级联反应器

考虑一个三级[串联](@entry_id:141009)反应器模型，其中溶质质量 $x_1, x_2, x_3$ 的变化由以下[方程组](@entry_id:193238)描述 [@problem_id:1348248]：
$$
\frac{dx_1}{dt} = -k x_1, \quad \frac{dx_2}{dt} = k x_1 - k x_2, \quad \frac{dx_3}{dt} = k x_2 - k x_3
$$
其矩阵形式为 $\mathbf{x}'=A\mathbf{x}$，其中
$$
A = \begin{pmatrix} -k  0  0 \\ k  -k  0 \\ 0  k  -k \end{pmatrix}
$$
矩阵 $A$ 是一个下三角矩阵，其[特征值](@entry_id:154894)是其对角线元素，即 $\lambda=-k$（[代数重数](@entry_id:154240)为3）。求解 $(A-(-k)I)\mathbf{v}=\mathbf{0}$，即 $\begin{pmatrix} 0  0  0 \\ k  0  0 \\ 0  k  0 \end{pmatrix}\mathbf{v}=\mathbf{0}$，得到 $v_1=0, v_2=0$，因此特征空间仅由 $(0,0,1)^T$ 张成，[几何重数](@entry_id:155584)为1。这表明 $A$ 对应于一个单一的 $3 \times 3$ 约当块。

令 $A = -kI + N$，其中 $N = \begin{pmatrix} 0  0  0 \\ k  0  0 \\ 0  k  0 \end{pmatrix}$。计算 $N$ 的幂：
$N^2 = \begin{pmatrix} 0  0  0 \\ 0  0  0 \\ k^2  0  0 \end{pmatrix}$，而 $N^3=0$。
因此，
$$
\exp(At) = \exp(-kt)(I+tN+\frac{t^2}{2}N^2) = \exp(-kt)\begin{pmatrix} 1  0  0 \\ kt  1  0 \\ k^2t^2/2  kt  1 \end{pmatrix}
$$
如果[初始条件](@entry_id:152863)为第一个反应器中有质量 $M_0$，其他为零，即 $\mathbf{x}(0) = (M_0, 0, 0)^T$，则解为：
$$
\mathbf{x}(t) = \exp(At)\begin{pmatrix} M_0 \\ 0 \\ 0 \end{pmatrix} = \exp(-kt)\begin{pmatrix} M_0 \\ kM_0t \\ k^2M_0t^2/2 \end{pmatrix}
$$
第二个反应器中的溶质质量为 $x_2(t) = kM_0t\exp(-kt)$。这个解的形式——一个线性项 $t$ 乘以指数衰减项——在描述[串联](@entry_id:141009)过程或级联衰变等物理现象时非常典型，其数学根源正是系统的[系数矩阵](@entry_id:151473)具有不可对角化的约当结构。

### 在[系统稳定性](@entry_id:273248)中的应用

约当标准型理论不仅提供了[求解方程组](@entry_id:152624)的方法，更重要的是，它为分析系统[长期行为](@entry_id:192358)和稳定性提供了强有力的工具。一个系统如果其所有解在 $t \to \infty$ 时都保持有界，则称其为（李雅普诺夫意义下）**稳定**的。

解的每个分量都是形如 $t^k \exp(\lambda t)$ 的项的[线性组合](@entry_id:154743)。这些项的长期行为由其实部 $\text{Re}(\lambda)$ 决定。
1.  **$\text{Re}(\lambda)  0$**：此时 $\exp(\text{Re}(\lambda)t)$ 是一个指数衰减项。即使存在多项式因子 $t^k$，指数衰减的威力也远超[多项式增长](@entry_id:177086)，因此 $\lim_{t\to\infty} t^k \exp(\text{Re}(\lambda)t) = 0$。与这类[特征值](@entry_id:154894)相关的解分量会趋于零。

2.  **$\text{Re}(\lambda) > 0$**：此时 $\exp(\text{Re}(\lambda)t)$ 是一个指数增长项，它会压倒任何多项式因子，导致解无界增长。

3.  **$\text{Re}(\lambda) = 0$**：这是最微妙的情况。[特征值](@entry_id:154894)是纯虚数 $\lambda = i\omega$。解的项形如 $t^k \exp(i\omega t)$，其模为 $t^k$。
    -   如果与该[特征值](@entry_id:154894)相关的约当块都是 $1 \times 1$ 的（即[几何重数](@entry_id:155584)等于[代数重数](@entry_id:154240)），则 $k=0$。解是 $\exp(i\omega t)$ 的[线性组合](@entry_id:154743)，表现为纯[振荡](@entry_id:267781)（如 $\cos(\omega t), \sin(\omega t)$），因此是有界的。
    -   如果存在尺寸大于1的约当块（[几何重数](@entry_id:155584)小于[代数重数](@entry_id:154240)），则至少存在 $k \ge 1$ 的项。形如 $t \cos(\omega t)$ 或 $t \sin(\omega t)$ 的项的振幅随时间线性增长，导致解是无界的。

综合以上分析，我们可以得出系统稳定的充要条件 [@problem_id:1348241]：
**系统 $\mathbf{x}'=A\mathbf{x}$ 的所有解都有界，当且仅当矩阵 $A$ 的所有[特征值](@entry_id:154894) $\lambda$ 都满足以下两个条件：**
**(1) 其实部非正，即 $\text{Re}(\lambda) \le 0$。**
**(2) 所有实部为零的[特征值](@entry_id:154894)，其[几何重数](@entry_id:155584)必须等于[代数重数](@entry_id:154240)（即这些[特征值](@entry_id:154894)都是半单的，对应的约当块都是 $1 \times 1$ 的）。**

应用此判据，我们可以分析具体系统的稳定性：
-   **系统A**：[特征值](@entry_id:154894)为 $-3, \pm 2i$，且均为半单。实部为-3或0，且实部为0的[特征值](@entry_id:154894)是半单的。因此，**系统稳定**。
-   **系统B**：[特征值](@entry_id:154894)为 $-2$，但存在 $2 \times 2$ 的约当块。尽管存在 $t\exp(-2t)$ 这样的项，但由于 $\text{Re}(\lambda)=-20$，这些项仍然是有界的。因此，**系统稳定**。
-   **系统C**：[特征值](@entry_id:154894)为 $0, -4$。[特征值](@entry_id:154894)0具有一个 $2 \times 2$ 的约当块。$\text{Re}(0)=0$，但该[特征值](@entry_id:154894)不是半单的，解中会出现形如 $t$ 的项，导致解无界。因此，**系统不稳定**。
-   **系统D**：[特征值](@entry_id:154894)为 $0.01 \pm i, -5$。存在实部为正的[特征值](@entry_id:154894) $0.01$，导致指数增长。因此，**系统不稳定**。
-   **系统E**：[特征值](@entry_id:154894)为 $\pm i$，且均为半单（[代数重数](@entry_id:154240)=[几何重数](@entry_id:155584)=2）。所有[特征值](@entry_id:154894)实部为零且都是半单的。因此，**系统稳定**。

通过约当标准型，我们不仅能“解”出系统的动态轨迹，更能“看”透其内在结构，从而预测其长期的稳定性和行为模式。这正是线性代数理论在动力[系统分析](@entry_id:263805)中的威力所在。