## 引言
在最优化理论中，找到一个函数的临界点——即梯度为零的点——仅仅是寻找最优解的第一步。一阶条件无法告诉我们这个点是山谷（局部最小值）、山峰（局部最大值），还是一个平坦的鞍部。为了解决这个模糊性，我们必须深入考察函数在临界点附近的局部几何形状，即其“曲率”。这正是最优性的二阶条件所要解决的核心问题，它为我们提供了一套更强大的数学工具来辨别最优解的性质。

本文将系统地引导您掌握最优性的二阶必要条件。首先，在“原理与机制”章节中，我们将从无约束问题出发，介绍Hessian矩阵及其半正定性如何揭示函数的局部曲率；随后，我们将这一概念扩展到更复杂的有约束问题，阐明为何必须分析拉格朗日函数的Hessian在特定可行方向（临界锥）上的性质。接着，在“应用与跨学科联系”章节中，您将看到这些理论原理如何在机器学习、物理、工程和经济学等多个领域中发挥关键作用，从验证算法的稳定性到解释复杂的物理和经济现象。最后，“动手实践”部分将提供精选的练习，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

在上一章中，我们确立了最优化问题的基础，并介绍了最优解存在的一阶必要条件。我们知道，对于可微函数，任何局部最优解都必须是一个**临界点** (critical point)，即目标函数在该点的梯度为零。然而，梯度为零仅仅告诉我们函数在该点是“平坦的”，它可能是局部最小值、局部最大值，也可能是一个鞍点。为了区分这些情况，我们必须考察函数在临界点周围的**曲率** (curvature)。这便引出了二阶最优性条件，它通过分析函数的二阶导数（即Hessian矩阵）来提供更深层次的洞察。本章将系统地阐述无约束和有约束问题的二阶必要条件，揭示其背后的几何原理与分析机制。

### 无约束情形：临界点的曲率

对于一个无约束优化问题 `minimize` $f(\mathbf{x})$，其中 $f: \mathbb{R}^n \to \mathbb{R}$ 是一个二次连续可微函数，我们首先定位其临界点 $\mathbf{x}^*$，满足 $\nabla f(\mathbf{x}^*) = \mathbf{0}$。现在，我们想知道，为了使 $\mathbf{x}^*$ 成为一个局部最小值，它还需要满足什么条件？

#### 二阶必要条件 (Second-Order Necessary Condition, SONC)

直观上，如果 $\mathbf{x}^*$ 是一个局部最小值，那么从 $\mathbf{x}^*$ 出发，沿任何方向移动一小步，函数值都应该增加或至少保持不变。我们可以通过泰勒展开来精确地描述这个思想。在临界点 $\mathbf{x}^*$ 附近，对于一个微小的位移向量 $\mathbf{d}$，函数的二阶泰勒展开式为：
$$
f(\mathbf{x}^* + \mathbf{d}) \approx f(\mathbf{x}^*) + \nabla f(\mathbf{x}^*)^T \mathbf{d} + \frac{1}{2}\mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d}
$$
由于 $\mathbf{x}^*$ 是一个临界点，$\nabla f(\mathbf{x}^*) = \mathbf{0}$，线性项消失，展开式简化为：
$$
f(\mathbf{x}^* + \mathbf{d}) - f(\mathbf{x}^*) \approx \frac{1}{2}\mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d}
$$
其中 $\nabla^2 f(\mathbf{x}^*)$ 是 $f$ 在 $\mathbf{x}^*$ 点的Hessian矩阵。为了使 $\mathbf{x}^*$ 成为一个局部最小值，对于所有足够小的非零向量 $\mathbf{d}$，我们必须有 $f(\mathbf{x}^* + \mathbf{d}) - f(\mathbf{x}^*) \ge 0$。这意味着二次型项 $\mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d}$ 必须是非负的。这个结论必须对**所有**可能的方向 $\mathbf{d} \in \mathbb{R}^n$ 都成立。

一个实对称矩阵 $H$ 如果对于所有非零向量 $\mathbf{d}$ 都满足 $\mathbf{d}^T H \mathbf{d} \ge 0$，则称该矩阵为**半正定矩阵** (positive semidefinite, PSD)。因此，我们得到了无约束优化的二阶必要条件：

**如果 $\mathbf{x}^*$ 是一个局部最小值，那么它的Hessian矩阵 $\nabla^2 f(\mathbf{x}^*)$ 必须是半正定的。**

一个等价且在实践中更常用的判别方法是检查Hessian矩阵的特征值。一个矩阵是半正定的，当且仅当它的所有特征值都为非负数 [@problem_id:2200669]。请注意，这个条件是必要的，但非充分的。也就是说，如果一个临界点的Hessian矩阵存在负特征值，它就绝不可能是局部最小值。但如果所有特征值均为非负，我们仍然无法断定它一定是局部最小值。

#### 条件的直观理解：函数切片与平坦方向

为了更直观地理解Hessian矩阵半正定的意义，我们可以想象将多变量函数“切片”成一系列单变量函数。对于任意一个固定的方向 $\mathbf{d} \in \mathbb{R}^n$，我们可以定义一个通过 $\mathbf{x}^*$ 的直线上的函数：
$$
g(t) = f(\mathbf{x}^* + t\mathbf{d})
$$
根据单变量微积分，如果 $\mathbf{x}^*$ 是一个局部最小值，那么对于任何方向 $\mathbf{d}$，$t=0$ 都必须是函数 $g(t)$ 的一个局部最小值点。这意味着 $g'(0)=0$ 和 $g''(0) \ge 0$。通过链式法则，我们可得：
$$
g'(t) = \nabla f(\mathbf{x}^* + t\mathbf{d})^T \mathbf{d} \implies g'(0) = \nabla f(\mathbf{x}^*)^T \mathbf{d} = 0
$$
$$
g''(t) = \mathbf{d}^T \nabla^2 f(\mathbf{x}^* + t\mathbf{d}) \mathbf{d} \implies g''(0) = \mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d}
$$
因此，$g''(0) \ge 0$ 的要求，正等价于我们之前推导出的 $\mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d} \ge 0$。Hessian矩阵的半正定性，实际上是要求函数在所有可能的方向上的“截面”都具有非负的曲率。

一个有趣的情形是当Hessian矩阵的某个特征值为零时。这对应于存在一个方向 $\mathbf{d}$，使得 $\mathbf{d}^T \nabla^2 f(\mathbf{x}^*) \mathbf{d} = 0$。这意味着在那个方向上，函数的二阶导数为零，函数在该方向上是“局部平坦的”。

考虑函数 $f(x, y) = (x+y-1)^2$ [@problem_id:2200671]。其梯度为 $\nabla f(x,y) = \begin{pmatrix} 2(x+y-1) \\ 2(x+y-1) \end{pmatrix}^T$。所有满足 $x+y=1$ 的点都是临界点。其Hessian矩阵是常数矩阵：
$$
\nabla^2 f(x,y) = \begin{pmatrix} 2 & 2 \\ 2 & 2 \end{pmatrix}
$$
该矩阵的特征值为 $\lambda_1=4$ 和 $\lambda_2=0$。由于所有特征值均非负，该Hessian矩阵是半正定的，因此所有临界点都满足二阶必要条件。特征值 $0$ 对应的特征向量是 $\mathbf{d} = \begin{pmatrix} 1 \\ -1 \end{pmatrix}^T$（及其倍数）。这正是沿着直线 $x+y=1$ 的方向。如果你在临界线上选择一点 $P$，并沿着 $\mathbf{d}$ 方向移动，函数值 $f(P+t\mathbf{d})$ 始终为零。在这个特定方向上，函数的二阶（乃至所有高阶）曲率都为零。这清晰地表明，二阶必要条件允许存在曲率为零的“平坦”方向。

#### 条件的检验：西尔维斯特准则

在实际应用中，例如在机器学习中调试损失函数时，我们可能需要检查一个给定的Hessian矩阵是否为半正定。除了计算特征值，另一个强大的工具是**西尔维斯特准则** (Sylvester's Criterion) 的推广。一个 $n \times n$ 的对称矩阵是半正定的，当且仅当它的所有**主子式** (principal minors) 均为非负。主子式是通过选择行和列的相同索引子集所构成的子矩阵的行列式。

假设一个模型参数 $\mathbf{w} = (w_1, w_2, w_3)^T$ 在临界点 $\mathbf{w}^*$ 处的Hessian矩阵为 [@problem_id:2200675]：
$$
H = \begin{pmatrix} 2 & -1 & 0 \\ -1 & \alpha & -2 \\ 0 & -2 & 5 \end{pmatrix}
$$
其中 $\alpha$ 是一个待定参数。为了使 $\mathbf{w}^*$ 满足局部最小值的二阶必要条件，Hessian矩阵 $H$ 必须是半正定的。我们通过检查所有主子式来找到满足条件的最小 $\alpha$ 值。
- $1$阶主子式（对角元素）：$2 \ge 0$, $\alpha \ge 0$, $5 \ge 0$。这要求 $\alpha \ge 0$。
- $2$阶主子式：
  $$ \det\begin{pmatrix} 2 & -1 \\ -1 & \alpha \end{pmatrix} = 2\alpha - 1 \ge 0 \implies \alpha \ge \frac{1}{2} $$
  $$ \det\begin{pmatrix} 2 & 0 \\ 0 & 5 \end{pmatrix} = 10 \ge 0 \quad (\text{恒成立}) $$
  $$ \det\begin{pmatrix} \alpha & -2 \\ -2 & 5 \end{pmatrix} = 5\alpha - 4 \ge 0 \implies \alpha \ge \frac{4}{5} $$
- $3$阶主子式（矩阵本身）：
  $$ \det(H) = 2(5\alpha-4) - (-1)(-5) = 10\alpha - 8 - 5 = 10\alpha - 13 \ge 0 \implies \alpha \ge \frac{13}{10} $$
综合所有条件（$\alpha \ge 0$, $\alpha \ge \frac{1}{2}$, $\alpha \ge \frac{4}{5}$, $\alpha \ge \frac{13}{10}$），我们必须取最严格的那个，即 $\alpha \ge \frac{13}{10}$。因此，使得该临界点满足二阶必要条件的最小 $\alpha$ 值为 $\frac{13}{10}$。

#### 二阶信息的局限性

当一个临界点的Hessian矩阵是半正定但非正定（即至少有一个零特征值）时，二阶必要条件得到满足，但二阶**充分**条件（要求Hessian为正定）则不满足。在这种情况下，二阶分析是**不确定的** (inconclusive)。该点可能是局部最小值，也可能是鞍点。

一个经典的例子是函数 $f(\mathbf{x}) = \|\mathbf{x}\|^4$ [@problem_id:3175901]。在 $\mathbf{x}^* = \mathbf{0}$ 处，我们有 $\nabla f(\mathbf{0}) = \mathbf{0}$ 和 $\nabla^2 f(\mathbf{0}) = \mathbf{0}$（零矩阵）。零矩阵是半正定的（所有特征值都是$0$），因此二阶必要条件满足。然而，它并不是正定的，所以二阶充分条件不满足。仅凭二阶信息，我们无法判断 $\mathbf{x}^*=\mathbf{0}$ 的性质。但是，通过直接观察函数本身，我们知道 $f(\mathbf{x}) = \|\mathbf{x}\|^4 > 0 = f(\mathbf{0})$ 对于所有 $\mathbf{x} \ne \mathbf{0}$ 都成立。因此，$\mathbf{x}^*=\mathbf{0}$ 是一个严格的全局最小值。这个结论是通过分析函数的四阶行为得到的，超越了二阶分析的范畴。

### 有约束情形：可行域上的曲率

当优化问题包含约束时，情况变得更加复杂且有趣。我们不再能沿任意方向移动，而必须保持在由约束定义的可行域内。这意味着，即使目标函数或拉格朗日函数在某个方向上具有负曲率（向下弯曲），只要该方向是“不可行”的，它就不会影响一个点的局部最优性。核心思想是，我们只需在**可行方向**上检验曲率。

#### 拉格朗日函数：融合目标与约束的曲率

在有约束优化中，正确的分析对象不再是目标函数 $f(\mathbf{x})$ 的Hessian，而是**拉格朗日函数** (Lagrangian) $L(\mathbf{x}, \boldsymbol{\mu}, \boldsymbol{\lambda})$ 的Hessian。对于一个包含等式约束 $\mathbf{h}(\mathbf{x}) = \mathbf{0}$ 和不等式约束 $\mathbf{g}(\mathbf{x}) \le \mathbf{0}$ 的问题，拉格朗日函数定义为：
$$
L(\mathbf{x}, \boldsymbol{\mu}, \boldsymbol{\lambda}) = f(\mathbf{x}) + \boldsymbol{\mu}^T \mathbf{g}(\mathbf{x}) + \boldsymbol{\lambda}^T \mathbf{h}(\mathbf{x})
$$
其中 $\boldsymbol{\mu}$ 和 $\boldsymbol{\lambda}$ 是拉格朗日乘子向量。为什么是拉格朗日函数？因为它巧妙地将约束的曲率融入了分析中。考虑一个KKT点 $(\mathbf{x}^*, \boldsymbol{\mu}^*, \boldsymbol{\lambda}^*)$，拉格朗日函数关于 $\mathbf{x}$ 的Hessian矩阵为：
$$
\nabla^2_{xx} L(\mathbf{x}^*, \boldsymbol{\mu}^*, \boldsymbol{\lambda}^*) = \nabla^2 f(\mathbf{x}^*) + \sum_{i=1}^m \mu_i^* \nabla^2 g_i(\mathbf{x}^*) + \sum_{j=1}^p \lambda_j^* \nabla^2 h_j(\mathbf{x}^*)
$$
这个Hessian矩阵包含了目标函数自身的曲率（$\nabla^2 f$）和由约束定义的曲面几何的曲率（$\nabla^2 g_i$ 和 $\nabla^2 h_j$），并通过拉格朗日乘子进行加权。一个很好的例子 [@problem_id:3175919] 说明了这一点：对于问题 `min` $x+y$ s.t. $y-x^2=0$ 和 $-y \le 0$，在KKT点 $(-\frac{1}{2}, \frac{1}{4})$ 处，目标函数 $f(x,y)=x+y$ 是线性的，其Hessian $\nabla^2 f$ 是零矩阵，不提供任何曲率信息。然而，拉格朗日函数的Hessian $\nabla^2_{xx}L$ 却是一个非零矩阵，它揭示了在可行流形上的真实曲率，最终显示出该点具有正曲率，从而满足二阶必要条件。

#### 等式约束与切空间

对于只含等式约束 $\mathbf{h}(\mathbf{x})=\mathbf{0}$ 的问题，一个点 $\mathbf{x}^*$ 要成为局部最小值，其曲率必须在所有可行的移动方向上为非负。在 $\mathbf{x}^*$ 处，这些方向构成了可行曲面的**切空间** (tangent space)。这个空间可以通过将约束线性化来近似，其定义为：
$$
\mathcal{T}(\mathbf{x}^*) = \{ \mathbf{d} \in \mathbb{R}^n \mid \nabla h_j(\mathbf{x}^*) \mathbf{d} = 0, \text{ for all } j=1,\dots,p \}
$$
即所有与所有约束函数的梯度正交的方向的集合。

**等式约束下的二阶必要条件**：假设 $\mathbf{x}^*$ 是一个满足KKT条件的正则点（即约束梯度线性无关），并对应拉格朗日乘子 $\boldsymbol{\lambda}^*$。如果 $\mathbf{x}^*$ 是一个局部最小值，那么必须有：
$$
\mathbf{d}^T \nabla^2_{xx} L(\mathbf{x}^*, \boldsymbol{\lambda}^*) \mathbf{d} \ge 0, \quad \text{for all } \mathbf{d} \in \mathcal{T}(\mathbf{x}^*)
$$
这个条件深刻地揭示了约束优化的本质。$\nabla^2_{xx} L$ 本身可能是**不定**的（即有正有负的特征值），但只要它在切空间 $\mathcal{T}(\mathbf{x}^*)$ 这个子空间上是半正定的，二阶必要条件就得到满足。

考虑问题：最小化 $f(x_1, x_2) = x_1^2 - x_2^2$ subject to $h(x_1, x_2) = x_2 = 0$ [@problem_id:3175832]。KKT点是 $\mathbf{x}^*=(0,0)$，对应的乘子是 $\lambda^*=0$。拉格朗日函数 $L = x_1^2 - x_2^2 + \lambda x_2$，其Hessian矩阵为：
$$
\nabla^2_{xx} L(\mathbf{x}^*, \lambda^*) = \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix}
$$
这是一个不定的矩阵，在 $(0,1)$ 方向上曲率为负。然而，约束 $x_2=0$ 的梯度是 $\nabla h = (0,1)$。因此，切空间由满足 $(0,1)\mathbf{d}=0$ 的方向 $\mathbf{d}=(d_1, d_2)$ 构成，即 $d_2=0$。切空间就是 $x_1$ 轴。现在，我们将Hessian的二次型限制在切空间上：
$$
\mathbf{d}^T \nabla^2_{xx} L \mathbf{d} = \begin{pmatrix} d_1 & 0 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 0 & -2 \end{pmatrix} \begin{pmatrix} d_1 \\ 0 \end{pmatrix} = 2d_1^2
$$
对于切空间中任何非零向量（$d_1 \ne 0$），$2d_1^2$ 总是严格为正。因此，尽管拉格朗日Hessian在整个空间上是不定的，但在所有可行方向上，它都表现出正曲率。二阶必要条件得到满足。这个问题 [@problem_id:3175921] 也阐述了完全相同的原理。

一个涉及非线性约束的例子是：最小化 $f(x_1, x_2)=x_1^2+x_2^2$ subject to $h(x_1, x_2)=x_1^2-x_2=0$ [@problem_id:3175879]。KKT点同样是 $\mathbf{x}^*=(0,0)$，乘子 $\lambda^*=0$。在 $\mathbf{x}^*$ 处，约束的梯度是 $\nabla h(0,0)=(0,-1)$，切空间依然是 $x_1$ 轴（即 $d_2=0$）。拉格朗日Hessian $\nabla^2_{xx} L(\mathbf{x}^*, \lambda^*)$ 计算出来是 $\begin{pmatrix} 2 & 0 \\ 0 & 2 \end{pmatrix}$。在切空间上，二次型的值为 $2d_1^2 \ge 0$。因此，二阶必要条件满足。

#### 不等式约束与临界锥

当问题包含不等式约束 $g_i(\mathbf{x}) \le 0$ 时，可行方向的集合变得更加复杂。在KKT点 $\mathbf{x}^*$ 处，对于一个**非激活**的不等式约束（$g_i(\mathbf{x}^*)  0$），我们可以在其附近自由移动而不违反它，因此它不限制我们的方向。我们只需要关注**激活**的不等式约束，即 $g_i(\mathbf{x}^*) = 0$。

对于一个激活的约束 $g_i$，任何可行的方向 $\mathbf{d}$ 都必须指向可行域的“内部”或沿着其边界，即满足 $\nabla g_i(\mathbf{x}^*) \mathbf{d} \le 0$。

综合等式约束和不等式约束，我们定义**临界锥** (critical cone) $C(\mathbf{x}^*, \boldsymbol{\mu}^*)$，它包含了所有满足一阶近似的“可行”方向。一个方向 $\mathbf{d}$ 属于临界锥，如果：
1.  $\nabla h_j(\mathbf{x}^*) \mathbf{d} = 0$，对于所有等式约束 $j$。
2.  $\nabla g_i(\mathbf{x}^*) \mathbf{d} \le 0$，对于所有激活的不等式约束 $i \in \mathcal{A}(\mathbf{x}^*)$。
3.  一个更精细的条件：如果某个激活约束 $i$ 对应的乘子 $\mu_i^* > 0$（称为强激活或互补松弛严格成立），则方向 $\mathbf{d}$ 必须满足更严格的等式 $\nabla g_i(\mathbf{x}^*) \mathbf{d} = 0$。

**一般情况下的二阶必要条件**：假设 $\mathbf{x}^*$ 是一个满足KKT条件的正则点，对应乘子 $\boldsymbol{\mu}^*$ 和 $\boldsymbol{\lambda}^*$。如果 $\mathbf{x}^*$ 是一个局部最小值，那么必须有：
$$
\mathbf{d}^T \nabla^2_{xx} L(\mathbf{x}^*, \boldsymbol{\mu}^*, \boldsymbol{\lambda}^*) \mathbf{d} \ge 0, \quad \text{for all } \mathbf{d} \in C(\mathbf{x}^*, \boldsymbol{\mu}^*)
$$
这是一个普适而强大的结论：在任何KKT点，拉格朗日Hessian在临界锥上的投影必须是半正定的。

让我们通过一个完整的例子来演示这个过程 [@problem_id:3175860]。考虑问题：最小化 $f(x)=x_1^2+x_2^2$ s.t. $g_1(x) = 1-x_1 \le 0$ 和 $g_2(x) = 3-x_1-x_2 \le 0$。通过求解KKT方程组，我们找到唯一的KKT点是 $\mathbf{x}^* = (\frac{3}{2}, \frac{3}{2})$，对应的乘子为 $\boldsymbol{\mu}^*=(0, 3)$。
- 在 $\mathbf{x}^*$ 处，$g_1(\mathbf{x}^*) = 1 - \frac{3}{2} = -\frac{1}{2}  0$ (非激活)，$g_2(\mathbf{x}^*) = 3 - \frac{3}{2} - \frac{3}{2} = 0$ (激活)。
- 激活集为 $\mathcal{A}(\mathbf{x}^*) = \{2\}$。由于对应的乘子 $\mu_2^* = 3 > 0$，临界锥 $C(\mathbf{x}^*, \boldsymbol{\mu}^*)$ 中的方向 $\mathbf{d}$ 必须满足 $\nabla g_2(\mathbf{x}^*) \mathbf{d} = 0$。
- $\nabla g_2(x) = (-1, -1)$，所以条件是 $-d_1-d_2=0$，即 $d_2 = -d_1$。临界锥是一条穿过原点的直线。
- 拉格朗日Hessian为 $\nabla^2_{xx} L(\mathbf{x}^*, \boldsymbol{\mu}^*) = \nabla^2 f + \mu_1^* \nabla^2 g_1 + \mu_2^* \nabla^2 g_2 = \begin{pmatrix} 2  0 \\ 0  2 \end{pmatrix} + 0 + 3 \cdot \mathbf{0} = \begin{pmatrix} 2  0 \\ 0  2 \end{pmatrix}$。
- 现在检验曲率：对于临界锥中的任一方向 $\mathbf{d} = (d_1, -d_1)$，二次型的值为：
  $$ \mathbf{d}^T \begin{pmatrix} 2  0 \\ 0  2 \end{pmatrix} \mathbf{d} = 2d_1^2 + 2(-d_1)^2 = 4d_1^2 \ge 0 $$
  条件得到满足。对于单位长度的临界方向（$d_1 = \pm \frac{1}{\sqrt{2}}$），该二次型的最小值为 $2$。

#### 关于约束规范的注记

上述所有有约束的二阶条件，都隐含地依赖于一个前提：在临界点 $\mathbf{x}^*$ 附近，由约束梯度定义的线性化可行方向（切空间或临界锥）能够很好地近似真实的可行域。保证这一点的条件被称为**约束规范** (Constraint Qualification, CQ)，其中最常用的是**线性无关约束规范** (LICQ)，它要求在 $\mathbf{x}^*$ 处所有激活约束的梯度是线性无关的。

如果CQ不成立，标准的一阶和二阶必要条件可能失效，甚至给出误导性信息。考虑一个例子 [@problem_id:3175886]：最小化 $f(x,y)=-x^2-y^2$ s.t. $h_1(x,y)=x^3=0$ 和 $h_2(x,y)=y^3=0$。唯一的可行点是 $\mathbf{x}^*=(0,0)$，因此它是一个严格的局部最小值。然而，在 $(0,0)$ 点，两个约束的梯度都是零向量，它们线性相关，LICQ不成立。
- KKT点是 $(0,0)$，乘子 $\boldsymbol{\lambda}$ 可以是任意值。
- 临界锥是整个 $\mathbb{R}^2$。
- 拉格朗日Hessian在 $(0,0)$ 处为 $\nabla^2_{xx} L = \begin{pmatrix} -2  0 \\ 0  -2 \end{pmatrix}$，与 $\boldsymbol{\lambda}$ 无关。
- 这个Hessian在整个 $\mathbb{R}^2$ 上是负定的，而不是半正定的。因此，标准的二阶必要条件在这里**失败**了。

这个失败并不意味着 $(0,0)$ 不是一个最小值，而是表明当约束的几何性质变得“退化”（即CQ不成立）时，基于线性化假设的标准分析工具可能不再适用。这提醒我们，在应用最优性条件时，理解其背后的假设和适用范围至关重要。