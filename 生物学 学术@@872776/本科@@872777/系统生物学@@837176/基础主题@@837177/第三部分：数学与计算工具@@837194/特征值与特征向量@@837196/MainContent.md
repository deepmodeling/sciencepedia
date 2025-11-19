## 引言
在生命科学的广阔图景中，从基因调控到生态系统演替，我们无时无刻不面对着由众多相互作用的组分构成的复杂系统。如何洞察这些系统内部的运行规律，并预测其未来的动态行为，是系统生物学面临的核心挑战。一个关键的难题在于，这些系统中的变量往往是高度耦合的，单个组分的变化会牵一发而动全身，使得直观分析变得异常困难。线性代数中的[特征值与特征向量](@entry_id:748836)概念，为我们解开这个“戈尔迪之结”提供了一把锋利的数学之剑。

本文旨在系统地阐释[特征值与特征向量](@entry_id:748836)这一强大工具，并展示其在系统生物学研究中的核心地位。我们将带领读者穿越理论的殿堂，深入应用的腹地，最终通过实践来巩固所学。在“**原理与机制**”一章中，我们将回归本源，详细解读[特征值与特征向量](@entry_id:748836)的数学定义、计算方法及其与系统[动力学稳定性](@entry_id:150175)的深刻联系。随后，在“**应用与交叉学科联系**”一章中，我们将展示这些抽象概念如何在[种群生态学](@entry_id:142920)、流行病学、高维数据分析和[网络科学](@entry_id:139925)等具体生物学问题中大放异彩，成为连接数学模型与生物学洞见的桥梁。最后，在“**动手实践**”部分，你将有机会通过具体的计算练习，将理论知识转化为解决实际问题的能力。通过这一系列的学习，你将掌握分析复杂生物系统的关键数学方法。

## 原理与机制

在研究复杂系统时，我们常常关注其动态[演化过程](@entry_id:175749)。无论是[基因调控网络](@entry_id:150976)中[蛋白质浓度](@entry_id:191958)的变化，还是生态系统中物种数量的波动，这些过程通常可以用一组变量来描述，这些变量构成系统的**状态 (state)**。线性代数，特别是[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的概念，为我们提供了一套强有力的数学工具，来解析和预测这些线性或近似线性的系统动力学行为。本章将深入探讨[特征值与特征向量](@entry_id:748836)的基本原理及其在[系统分析](@entry_id:263805)中的核心机制。

### 核心思想：不变方向与缩放因子

线性变换是描述系统状态变化的基本数学模型。一个$n$维系统中的状态可以表示为一个向量 $\mathbf{v} \in \mathbb{R}^n$。当系统演化一步（例如，经过一个时间单位或一次迭代）后，其新状态 $\mathbf{v}'$ 可以通过一个 $n \times n$ 的矩阵 $A$ 作用于原状态 $\mathbf{v}$ 得到，即 $\mathbf{v}' = A\mathbf{v}$。

通常情况下，[变换矩阵](@entry_id:151616) $A$ 会同时改变向量 $\mathbf{v}$ 的长度和方向。然而，对于任何给定的线性变换，几乎总存在一些特殊的非零向量，当它们被变换时，其方向保持不变（或恰好反向）。变换对这些向量的作用仅仅是进行缩放。这些特殊的向量被称为**[特征向量](@entry_id:151813) (eigenvectors)**，而对应的缩放因子则被称为**[特征值](@entry_id:154894) (eigenvalues)**。

这个核心概念可以用一个简洁的方程来表达：

$A\mathbf{v} = \lambda\mathbf{v}$

这里，$\mathbf{v}$ 是一个非零的[特征向量](@entry_id:151813)，$\lambda$ 是与之对应的[特征值](@entry_id:154894)，它是一个标量。这个方程的几何意义是，向量 $A\mathbf{v}$ 与向量 $\mathbf{v}$ 共线。

这个概念在系统生物学中具有深刻的物理意义。例如，在一个由两种相互作用的物种组成的生态系统中，我们可以用一个种群向量 $\mathbf{p} = \begin{pmatrix} p_1 \\ p_2 \end{pmatrix}$ 来表示它们的数量。系统的年度变化可以用一个[转移矩阵](@entry_id:145510) $A$ 来描述，使得下一年的种群为 $\mathbf{p}_{\text{next}} = A\mathbf{p}$。如果存在一个种群[分布](@entry_id:182848) $\mathbf{p}$，使得 $A\mathbf{p} = \lambda\mathbf{p}$，这意味着物种之间的相对比例 $p_1:p_2$ 在下一年保持不变。整个种群向量只是被因子 $\lambda$ 统一缩放了。这样的状态被称为“[平衡分布](@entry_id:263943)”或“[稳态](@entry_id:182458)增长模式”，而[特征值](@entry_id:154894) $\lambda$ 则代表了这个种群组合的年增长率 [@problem_id:1360110]。

要验证一个给定的向量 $\mathbf{v}$ 是否是矩阵 $A$ 的[特征向量](@entry_id:151813)，我们只需直接计算 $A\mathbf{v}$，然后检查结果是否是原向量 $\mathbf{v}$ 的一个标量倍。例如，考虑一个由矩阵 $A = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix}$ 描述的系统。我们来检验向量 $\mathbf{v}_B = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是否是一个[特征向量](@entry_id:151813)：

$A\mathbf{v}_B = \begin{pmatrix} 3  -1 \\ 2  0 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 3 \cdot 1 - 1 \cdot 1 \\ 2 \cdot 1 + 0 \cdot 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$

我们观察到，结果 $\begin{pmatrix} 2 \\ 2 \end{pmatrix}$ 正好是原向量 $\begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 的两倍。因此，我们可以写成 $A\mathbf{v}_B = 2\mathbf{v}_B$。这证实了 $\mathbf{v}_B = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 是矩阵 $A$ 的一个[特征向量](@entry_id:151813)，其对应的[特征值](@entry_id:154894)为 $\lambda = 2$ [@problem_id:1360110]。

### [特征值与特征向量](@entry_id:748836)的计算

虽然直接验证很直观，但我们通常需要一个系统性的方法来找出矩阵的所有[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)，而不是靠猜测。

#### 特征方程

我们的出发点仍然是定义式 $A\mathbf{v} = \lambda\mathbf{v}$。为了求解这个方程中的 $\mathbf{v}$ 和 $\lambda$，我们可以将其改写。引入 $n \times n$ 的[单位矩阵](@entry_id:156724) $I$，我们可以将右边写成 $\lambda I \mathbf{v}$。于是，方程变为：

$A\mathbf{v} - \lambda I \mathbf{v} = \mathbf{0}$

$(A - \lambda I)\mathbf{v} = \mathbf{0}$

这个方程的含义是，[特征向量](@entry_id:151813) $\mathbf{v}$ 位于矩阵 $(A - \lambda I)$ 的**[零空间](@entry_id:171336) (null space)** 中。根据定义，[特征向量](@entry_id:151813)不能是[零向量](@entry_id:156189)。一个[齐次线性方程组](@entry_id:153432) $(A - \lambda I)\mathbf{v} = \mathbf{0}$ 要有非零解，当且仅当系数矩阵 $(A - \lambda I)$ 是**奇异的 (singular)**，也就是说，它的[行列式](@entry_id:142978)必须为零。

$\det(A - \lambda I) = 0$

这个方程被称为**特征方程 (characteristic equation)**。对于一个 $n \times n$ 矩阵 $A$，$\det(A - \lambda I)$ 是一个关于 $\lambda$ 的 $n$ 次多项式，称为**[特征多项式](@entry_id:150909) (characteristic polynomial)**。这个[多项式的根](@entry_id:154615)就是矩阵 $A$ 的所有[特征值](@entry_id:154894)。

让我们通过一个例子来演示这个过程。假设一个二维变换由矩阵 $A = \begin{pmatrix} 7  -2 \\ 4  1 \end{pmatrix}$ 描述，我们希望找到它的[特征值](@entry_id:154894)，也就是可能的缩放因子 [@problem_id:2168104]。

首先，构建矩阵 $A - \lambda I$：
$A - \lambda I = \begin{pmatrix} 7  -2 \\ 4  1 \end{pmatrix} - \lambda \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 7 - \lambda  -2 \\ 4  1 - \lambda \end{pmatrix}$

接下来，计算其[行列式](@entry_id:142978)并令其为零：
$\det(A - \lambda I) = (7 - \lambda)(1 - \lambda) - (-2)(4) = 0$
$\lambda^2 - 8\lambda + 7 + 8 = 0$
$\lambda^2 - 8\lambda + 15 = 0$

这是一个关于 $\lambda$ 的二次方程。我们可以通过分解因式或使用求根公式来求解：
$(\lambda - 3)(\lambda - 5) = 0$

因此，我们得到两个[特征值](@entry_id:154894)：$\lambda_1 = 3$ 和 $\lambda_2 = 5$。这意味着该[线性变换](@entry_id:149133)存在两个不变方向，一个方向上的向量被拉伸为原来的3倍，另一个方向上的向量被拉伸为原来的5倍。

#### [特征空间](@entry_id:638014)

一旦找到了[特征值](@entry_id:154894)，我们就可以通过求解方程 $(A - \lambda I)\mathbf{v} = \mathbf{0}$ 来找到每个[特征值](@entry_id:154894)对应的[特征向量](@entry_id:151813)。对于一个给定的[特征值](@entry_id:154894) $\lambda_i$，所有满足这个方程的向量 $\mathbf{v}$（包括零向量）构成一个[向量空间](@entry_id:151108)，称为对应于 $\lambda_i$ 的**[特征空间](@entry_id:638014) (eigenspace)**，记作 $E_{\lambda_i}$。特征空间 $E_{\lambda_i}$ 的维度被称为[特征值](@entry_id:154894) $\lambda_i$ 的**[几何重数](@entry_id:155584) (geometric multiplicity)**。

例如，在研究一个线性分子的[振动](@entry_id:267781)动力学时，其法向[振动](@entry_id:267781)模式（即所有粒子以相同频率进行正弦运动的模式）就对应于系统矩阵的[特征向量](@entry_id:151813) [@problem_id:1360138]。假设系统由矩阵 $A = \begin{pmatrix} 5  2  0 \\ 2  4  -1 \\ 0  -1  2 \end{pmatrix}$ 描述，并且已知 $\lambda = 3$ 是一个[特征值](@entry_id:154894)。为了找到对应的[特征空间](@entry_id:638014) $E_3$，我们需求解 $(A - 3I)\mathbf{v} = \mathbf{0}$。

$A - 3I = \begin{pmatrix} 5-3  2  0 \\ 2  4-3  -1 \\ 0  -1  2-3 \end{pmatrix} = \begin{pmatrix} 2  2  0 \\ 2  1  -1 \\ 0  -1  -1 \end{pmatrix}$

令 $\mathbf{v} = \begin{pmatrix} x \\ y \\ z \end{pmatrix}$，我们得到线性方程组：
$\begin{cases} 2x + 2y = 0 \\ 2x + y - z = 0 \\ -y - z = 0 \end{cases}$

从第一个方程得到 $x = -y$。从第三个方程得到 $z = -y$。将这两个关系代入第二个方程进行验证：$2(-y) + y - (-y) = -2y + y + y = 0$，说明[方程组](@entry_id:193238)是相容的。

因此，所有属于 $E_3$ 的向量都可以写成 $\begin{pmatrix} -y \\ y \\ -y \end{pmatrix} = y \begin{pmatrix} -1 \\ 1 \\ -1 \end{pmatrix}$ 的形式，其中 $y$ 是任意实数。这意味着特征空间 $E_3$ 是一条穿过原点的直线，它由向量 $\begin{pmatrix} -1 \\ 1 \\ -1 \end{pmatrix}$（或其任意非零标量倍，如 $\begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix}$）张成。所以，$\left\{ \begin{pmatrix} 1 \\ -1 \\ 1 \end{pmatrix} \right\}$ 是特征空间 $E_3$ 的一组基，其维度（[几何重数](@entry_id:155584)）为1。

### 性质与捷径

在求解[特征值](@entry_id:154894)时，有一些有用的性质可以简化计算或用于验证结果。对于任意一个 $n \times n$ 的矩阵 $A$，其[特征值](@entry_id:154894) $\lambda_1, \lambda_2, \dots, \lambda_n$ 与矩阵的**迹 (trace)** 和**[行列式](@entry_id:142978) (determinant)** 之间存在直接关系：

1.  **[特征值](@entry_id:154894)之和等于矩阵的迹**：
    $\sum_{i=1}^{n} \lambda_i = \lambda_1 + \lambda_2 + \dots + \lambda_n = \text{tr}(A)$
    其中，[矩阵的迹](@entry_id:139694)定义为主对角线上元素的和，即 $\text{tr}(A) = \sum_{i=1}^{n} A_{ii}$。

2.  **[特征值](@entry_id:154894)之积等于[矩阵的行列式](@entry_id:148198)**：
    $\prod_{i=1}^{n} \lambda_i = \lambda_1 \cdot \lambda_2 \cdot \dots \cdot \lambda_n = \det(A)$

这些关系源于[特征多项式](@entry_id:150909)的系数。对于一个 $2 \times 2$ 矩阵 $A = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$，其[特征多项式](@entry_id:150909)为 $\lambda^2 - (a+d)\lambda + (ad-bc) = 0$。如果其根为 $\lambda_1$ 和 $\lambda_2$，那么根据[韦达定理](@entry_id:150627)，$\lambda_1 + \lambda_2 = a+d = \text{tr}(A)$ 且 $\lambda_1 \lambda_2 = ad-bc = \det(A)$。

这个性质非常有用。例如，在一个离散时间动力学系统中，状态由矩阵 $A = \begin{pmatrix} 3  -1 \\ -2  2 \end{pmatrix}$ 驱动。我们无需计算具体的[特征值](@entry_id:154894)，就可以直接确定它们的和与积 [@problem_id:1674208]：
- **[特征值](@entry_id:154894)之和**: $\lambda_1 + \lambda_2 = \text{tr}(A) = 3 + 2 = 5$
- **[特征值](@entry_id:154894)之积**: $\lambda_1 \lambda_2 = \det(A) = (3)(2) - (-1)(-2) = 6 - 2 = 4$

这为我们提供了一种快速检查[特征值计算](@entry_id:145559)是否正确的方法。

### [特征值](@entry_id:154894)与线性[系统动力学](@entry_id:136288)

特征分析最强大的应用之一在于理解[线性动力系统](@entry_id:150282)的行为。[特征向量](@entry_id:151813)构成了系统的“自然[坐标系](@entry_id:156346)”。当系统沿着[特征向量](@entry_id:151813)的方向演化时，其行为会变得异常简单。

#### [连续时间系统](@entry_id:276553)：$\frac{d\mathbf{x}}{dt} = A\mathbf{x}$

许多生物过程，如化学反应网络或[种群动态](@entry_id:136352)，都可以用[常微分方程组](@entry_id:266774)来描述。在[平衡点](@entry_id:272705)附近，这些系统通常可以线性化为 $\frac{d\mathbf{x}}{dt} = A\mathbf{x}$ 的形式。

这个[方程组](@entry_id:193238)的解的基本形式是 $\mathbf{x}(t) = e^{\lambda t}\mathbf{v}$，其中 $\lambda$ 和 $\mathbf{v}$ 是矩阵 $A$ 的一个[特征值](@entry_id:154894)-[特征向量](@entry_id:151813)对。代入验证：
$\frac{d}{dt}(e^{\lambda t}\mathbf{v}) = \lambda e^{\lambda t}\mathbf{v}$
$A(e^{\lambda t}\mathbf{v}) = e^{\lambda t}(A\mathbf{v}) = e^{\lambda t}(\lambda \mathbf{v})$
两侧相等，证明了它是一个解。

如果矩阵 $A$ 有一套完整的线性无关的[特征向量](@entry_id:151813) $\mathbf{v}_1, \dots, \mathbf{v}_n$（即 $A$ 是可对角化的），那么系统的通解可以表示为这些[基本解](@entry_id:184782)的线性组合：
$\mathbf{x}(t) = c_1 e^{\lambda_1 t}\mathbf{v}_1 + c_2 e^{\lambda_2 t}\mathbf{v}_2 + \dots + c_n e^{\lambda_n t}\mathbf{v}_n$

这里的系数 $c_1, \dots, c_n$ 由系统的初始状态 $\mathbf{x}(0)$ 决定。通过将初始[状态表示](@entry_id:141201)为[特征向量](@entry_id:151813)的[线性组合](@entry_id:154743) $\mathbf{x}(0) = c_1\mathbf{v}_1 + \dots + c_n\mathbf{v}_n$，我们就可以唯一确定这些系数。本质上，[特征向量](@entry_id:151813)分解将一个耦合的、难以求解的[方程组](@entry_id:193238)，转换成了一组独立的、简单的指数增长或衰减问题 [@problem_id:1674212]。

**连续系统的稳定性**

系统的长期行为完全由[特征值](@entry_id:154894)的实部 $\text{Re}(\lambda)$ 决定：
- 如果所有[特征值](@entry_id:154894)的**实部都为负** ($\text{Re}(\lambda_i)  0$ for all $i$)，那么所有 $e^{\lambda_i t}$ 项都会随着时间 $t \to \infty$ 而趋于零。系统会从任何初始状态收敛到[平衡点](@entry_id:272705) $\mathbf{x}=\mathbf{0}$。这种情况称为**[渐近稳定](@entry_id:168077) (asymptotically stable)** [@problem_id:2168092]。系统恢复平衡的最慢速率由具有最大实部（即最接近零的负数）的[特征值](@entry_id:154894)决定。
- 如果**至少有一个[特征值](@entry_id:154894)的实部为正** ($\text{Re}(\lambda_i) > 0$)，那么对应的 $e^{\lambda_i t}$ 项会指数级增长，导致系统偏离[平衡点](@entry_id:272705)。这种情况是**不稳定的 (unstable)**。
- 如果[特征值](@entry_id:154894)是**复数**，$\lambda = \alpha \pm i\beta$，解中会包含 $e^{\alpha t}\cos(\beta t)$ 和 $e^{\alpha t}\sin(\beta t)$ 这样的项。这意味着系统会表现出[振荡](@entry_id:267781)行为。
    - 实部 $\alpha$ 决定振幅的变化：$\alpha  0$ 导致**衰减[振荡](@entry_id:267781)**（[稳定螺线](@entry_id:269578)），系统螺旋式地收敛到[平衡点](@entry_id:272705)；$\alpha > 0$ 导致**增长[振荡](@entry_id:267781)**（不[稳定螺线](@entry_id:269578)）；$\alpha = 0$ 导致**持续[振荡](@entry_id:267781)**（[中心点](@entry_id:636820)）。
    - 虚部 $\beta$ 决定了[振荡](@entry_id:267781)的频率。
    在捕食者-被捕食者模型中，复数[特征值](@entry_id:154894)直接对应于两个物种种群数量的周期性波动。例如，[特征值](@entry_id:154894) $\lambda = -0.05 \pm i(0.8)$ 意味着系统是稳定的（因为实部 $-0.05  0$），并且会以衰减的[振荡](@entry_id:267781)方式返回到共存的[稳态](@entry_id:182458) [@problem_id:1430884]。

#### 离散时间系统：$\mathbf{x}_{k+1} = A\mathbf{x}_k$

对于按时间步演化的离散系统，其状态在 $k$ 步后为 $\mathbf{x}_k = A^k \mathbf{x}_0$。同样，使用[特征向量](@entry_id:151813)作为基底可以极大地简化分析。如果 $\mathbf{x}_0 = c_1\mathbf{v}_1 + \dots + c_n\mathbf{v}_n$，那么：
$\mathbf{x}_k = A^k(c_1\mathbf{v}_1 + \dots + c_n\mathbf{v}_n) = c_1 A^k\mathbf{v}_1 + \dots + c_n A^k\mathbf{v}_n$
由于 $A\mathbf{v}_i = \lambda_i\mathbf{v}_i$，那么 $A^k\mathbf{v}_i = \lambda_i^k\mathbf{v}_i$。因此，
$\mathbf{x}_k = c_1 \lambda_1^k \mathbf{v}_1 + c_2 \lambda_2^k \mathbf{v}_2 + \dots + c_n \lambda_n^k \mathbf{v}_n$

系统的长期行为由具有最大[绝对值](@entry_id:147688)的[特征值](@entry_id:154894)（即**[谱半径](@entry_id:138984) (spectral radius)** $\rho(A) = \max_i |\lambda_i|$）主导。当 $k$ 足够大时，$\lambda_i^k$ 中[绝对值](@entry_id:147688)最大的那一项将远超其他项，系统[状态向量](@entry_id:154607) $\mathbf{x}_k$ 的方向将趋向于该主导[特征值](@entry_id:154894)对应的[特征向量](@entry_id:151813)方向 [@problem_id:2168102]。

**离散系统的稳定性**

系统的长期行为由[特征值](@entry_id:154894)的**[绝对值](@entry_id:147688) (magnitude)** $|\lambda|$ 决定：
- 如果所有[特征值](@entry_id:154894)的**[绝对值](@entry_id:147688)都小于1** ($|\lambda_i|  1$ for all $i$)，那么所有 $\lambda_i^k$ 项都会随着 $k \to \infty$ 而趋于零。系统是**[渐近稳定](@entry_id:168077)的**。
- 如果**至少有一个[特征值](@entry_id:154894)的[绝对值](@entry_id:147688)大于1** ($|\lambda_i| > 1$)，系统是**不稳定的**。
- 如果最大的[绝对值](@entry_id:147688)为1，而其余的[绝对值](@entry_id:147688)都小于1，系统可能是中性稳定的或不稳定的，这取决于具体情况。

在一个[生态模型](@entry_id:186101)中，如果物种间的相互作用强度 $\alpha$ 使得[系统矩阵](@entry_id:172230) $A$ 的所有[特征值](@entry_id:154894)的[绝对值](@entry_id:147688)都小于1，那么种群数量的微小偏离会随时间衰减，恢复到平衡状态。这为我们确定系统保持稳定的参数范围提供了明确的判据 [@problem_id:1674229]。

### 深入探讨：[可对角化性](@entry_id:748379)与重数

我们之前的分析大多依赖于一个隐含的假设：$n \times n$ 矩阵 $A$ 具有 $n$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，足以构成整个空间 $\mathbb{R}^n$ 的一组基。拥有这套完整[特征向量基](@entry_id:163721)的矩阵被称为**可对角化的 (diagonalizable)**。

然而，并非所有矩阵都如此。一个[特征值](@entry_id:154894)可能有多个[特征向量](@entry_id:151813)（形成一个多维特征空间），也可能“缺失”[特征向量](@entry_id:151813)。这就需要我们区分两种“重数”：
- **[代数重数](@entry_id:154240) (Algebraic Multiplicity)**：一个[特征值](@entry_id:154894) $\lambda$ 作为[特征多项式](@entry_id:150909) $\det(A - \lambda I) = 0$ 的根的次数。
- **[几何重数](@entry_id:155584) (Geometric Multiplicity)**：对应于该[特征值](@entry_id:154894)的特征空间 $E_\lambda$ 的维度，即 $\dim(E_\lambda)$。

一个基本定理是，对于任何[特征值](@entry_id:154894)，其[几何重数](@entry_id:155584)总是小于或等于其[代数重数](@entry_id:154240)：$1 \le \text{几何重数} \le \text{代数重数}$。

一个矩阵是**可对角化的，当且仅当对其每一个[特征值](@entry_id:154894)，其[几何重数](@entry_id:155584)都等于其[代数重数](@entry_id:154240)**。这意味着所有[特征空间](@entry_id:638014)的维度之和恰好等于矩阵的维度 $n$，从而能够找到一组覆盖整个空间的[特征向量基](@entry_id:163721)底。

当一个[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)小于其[代数重数](@entry_id:154240)时，矩阵是**有缺陷的 (defective)** 并且**不可对角化**。一个典型的例子是[剪切变换](@entry_id:151272)矩阵。例如，矩阵 $A = \begin{pmatrix} 1  -4 \\ 0  1 \end{pmatrix}$ [@problem_id:2168126]。
- **[代数重数](@entry_id:154240)**：其特征多项式为 $\det(A-\lambda I) = (1-\lambda)^2 = 0$，因此有唯一的[特征值](@entry_id:154894) $\lambda=1$，[代数重数](@entry_id:154240)为2。
- **[几何重数](@entry_id:155584)**：我们求解 $(A-1I)\mathbf{v} = \mathbf{0}$，即 $\begin{pmatrix} 0  -4 \\ 0  0 \end{pmatrix}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$。这给出的唯一约束是 $-4x_2=0$，即 $x_2=0$。而 $x_1$ 是自由的。因此，[特征空间](@entry_id:638014)是所有形如 $\begin{pmatrix} x_1 \\ 0 \end{pmatrix}$ 的向量，它由[基向量](@entry_id:199546) $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 张成。这个空间的维度是1。

由于[特征值](@entry_id:154894) $\lambda=1$ 的[代数重数](@entry_id:154240)（2）大于其[几何重数](@entry_id:155584)（1），该矩阵是不可对角化的。这意味着我们无法找到两个线性无关的[特征向量](@entry_id:151813)来张成整个二维空间。这类系统的动力学行为更为复杂，其解可能包含形如 $t e^{\lambda t}$（连续情况）或 $k \lambda^k$（离散情况）的项，这预示着除了纯指数行为之外，还存在线性增长的成分。对这类系统的深入分析需要借助更高级的工具，如若尔当标准型 (Jordan Normal Form)。