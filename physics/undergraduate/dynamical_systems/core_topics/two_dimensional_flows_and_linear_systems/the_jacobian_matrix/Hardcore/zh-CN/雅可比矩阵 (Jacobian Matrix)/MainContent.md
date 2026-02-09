## 引言
在科学与工程的广阔天地中，从行星的轨道运动到神经网络的学习过程，我们随处可见由多个相互作用的变量所描述的复杂系统。理解并预测这些系统的行为，是现代科学的核心挑战之一。然而，当系统具有非线性特性时，其动态会变得异常复杂，难以直接求解。这就引出了一个根本性的问题：我们如何才能在不牺牲过多精度的前提下，简化对这些复杂系统的分析？

答案在于一个强大的数学工具——**雅可比矩阵**。雅可比矩阵是单变量导数概念向多维空间的自然延伸，它能够捕捉一个非线性系统在任意一点附近的局部线性行为。通过这种“线性化”的视角，我们可以将棘手的非线性问题转化为我们熟知的、易于分析的线性代数问题。这不仅使我们能够判断一个平衡状态是稳定还是不稳定，还能揭示系统在平衡点周围的精细几何结构。

本文将带领读者系统地探索雅可比矩阵的理论与实践。我们将在第一章 **“原理与机制”** 中，从基本定义出发，阐明雅可比矩阵作为最佳线性近似的深刻内涵，并详细介绍如何利用它来分析动力系统不动点的稳定性。随后，在第二章 **“应用与跨学科联系”** 中，我们将展示雅可比矩阵的惊人威力，看它如何成为连接物理学、生态学、机器人学乃至混沌理论等不同领域的统一语言。最后，在第三章 **“动手实践”** 中，你将通过具体的计算和分析问题，亲手运用雅可比矩阵来解决实际问题，从而将理论知识转化为真正的分析能力。

## 原理与机制

在深入研究多维系统的动态行为时，我们必须超越单变量微积分的范畴。当一个系统的状态由多个相互依赖的变量描述时，我们需要一个强大的工具来刻画其局部变化。这个工具就是 **雅可比矩阵 (Jacobian matrix)**。本章将系统地阐述雅可比矩阵的定义、核心原理及其在动力系统分析中的关键作用。

### 定义雅可比矩阵：导数的推广

对于单变量函数 $y = f(x)$，其导数 $\frac{dy}{dx}$ 衡量了当 $x$ 发生微小变化时 $y$ 的变化率。现在，我们考虑一个更一般的情形：一个向量值函数 $\mathbf{F}$，它将一个 $n$ 维空间中的点 $\mathbf{x} = (x_1, x_2, \dots, x_n)$ 映射到 $m$ 维空间中的一个点 $\mathbf{y} = (y_1, y_2, \dots, y_m)$。我们写作 $\mathbf{F}: \mathbb{R}^n \to \mathbb{R}^m$。这个函数的每个输出分量 $y_i$ 都是所有输入分量 $x_j$ 的函数，即 $y_i = F_i(x_1, x_2, \dots, x_n)$。

在这种情况下，我们如何描述 $\mathbf{F}$ 的“导数”呢？答案是，我们需要一个包含所有可能变化率信息的对象。**雅可比矩阵** 正是为此而生。函数 $\mathbf{F}$ 在点 $\mathbf{x}$ 的雅可比矩阵，记作 $J_{\mathbf{F}}(\mathbf{x})$ 或 $D\mathbf{F}(\mathbf{x})$，是一个 $m \times n$ 的矩阵，其元素由 $\mathbf{F}$ 的所有一阶偏导数构成：

$$
J_{\mathbf{F}}(\mathbf{x}) = \begin{pmatrix}
\frac{\partial F_1}{\partial x_1}  \frac{\partial F_1}{\partial x_2}  \cdots  \frac{\partial F_1}{\partial x_n} \\
\frac{\partial F_2}{\partial x_1}  \frac{\partial F_2}{\partial x_2}  \cdots  \frac{\partial F_2}{\partial x_n} \\
\vdots  \vdots  \ddots  \vdots \\
\frac{\partial F_m}{\partial x_1}  \frac{\partial F_m}{\partial x_2}  \cdots  \frac{\partial F_m}{\partial x_n}
\end{pmatrix}
$$

矩阵的第 $i$ 行是第 $i$ 个分量函数 $F_i$ 的梯度向量 $(\nabla F_i)^T$。矩阵的第 $j$ 列则包含了所有输出分量相对于输入分量 $x_j$ 的变化率。因此，雅可比矩阵的维度是“输出维度 $\times$ 输入维度”。

为了具体理解其构造过程，我们来看一个例子。考虑一个从 $\mathbb{R}^3$到 $\mathbb{R}^2$ 的映射 $F(x, y, z) = (F_1(x, y, z), F_2(x, y, z))$，其中分量函数定义为 [@problem_id:2325284]：
$$
F_1(x, y, z) = x^2 y + \sin(z)
$$
$$
F_2(x, y, z) = z \exp(x) - y^2
$$
该函数的雅可比矩阵是一个 $2 \times 3$ 矩阵，其通用形式为：
$$
J_{F}(x,y,z)=\begin{pmatrix}
\frac{\partial F_{1}}{\partial x}  \frac{\partial F_{1}}{\partial y}  \frac{\partial F_{1}}{\partial z} \\
\frac{\partial F_{2}}{\partial x}  \frac{\partial F_{2}}{\partial y}  \frac{\partial F_{2}}{\partial z}
\end{pmatrix}
$$
计算各个偏导数，我们得到：
$$
\frac{\partial F_{1}}{\partial x}=2xy, \quad \frac{\partial F_{1}}{\partial y}=x^{2}, \quad \frac{\partial F_{1}}{\partial z}=\cos(z)
$$
$$
\frac{\partial F_{2}}{\partial x}=z\exp(x), \quad \frac{\partial F_{2}}{\partial y}=-2y, \quad \frac{\partial F_{2}}{\partial z}=\exp(x)
$$
将这些表达式代入，便得到雅可比矩阵：
$$
J_F(x, y, z) = \begin{pmatrix}
2xy  x^2  \cos(z) \\
z\exp(x)  -2y  \exp(x)
\end{pmatrix}
$$
这个矩阵在空间中每一点都是不同的。例如，在点 $P_0 = (0, 1, \pi)$，我们只需将这些值代入即可得到一个常数矩阵：
$$
J_F(0, 1, \pi) = \begin{pmatrix}
2(0)(1)  0^2  \cos(\pi) \\
\pi\exp(0)  -2(1)  \exp(0)
\end{pmatrix} = \begin{pmatrix}
0  0  -1 \\
\pi  -2  1
\end{pmatrix}
$$
这个矩阵精确地捕捉了函数 $F$ 在点 $P_0$ 附近的行为特征。

### 核心原理：最佳线性近似

仅仅将雅可比矩阵看作偏导数的集合，会忽略其最深刻的数学意义。雅可比矩阵的真正威力在于，它定义了函数在某一点附近的 **最佳线性近似 (best linear approximation)**。

我们回忆一下单变量函数 $f(x)$ 在点 $a$ 附近的一阶泰勒展开：$f(a+h) \approx f(a) + f'(a)h$。这个公式用一条直线（一个线性函数）来近似原函数在点 $a$ 附近的行为，而 $f'(a)$正是这条直线的斜率。

雅可比矩阵将这个思想推广到多维空间。对于向量函数 $\mathbf{f}: \mathbb{R}^n \to \mathbb{R}^m$，其在点 $\mathbf{a}$ 附近的一阶近似为：
$$
\mathbf{f}(\mathbf{a}+\mathbf{h}) \approx \mathbf{f}(\mathbf{a}) + J_{\mathbf{f}}(\mathbf{a})\mathbf{h}
$$
这里，$\mathbf{a}$ 是我们关注的点，$\mathbf{h}$ 是一个无穷小的位移向量。$J_{\mathbf{f}}(\mathbf{a})$ 是函数 $\mathbf{f}$ 在点 $\mathbf{a}$ 处的雅可比矩阵，它是一个常数矩阵。乘积 $J_{\mathbf{f}}(\mathbf{a})\mathbf{h}$ 是一个矩阵与向量的乘法，其结果是一个 $m$ 维向量。这个公式表明，函数值在 $\mathbf{a}$ 点附近的变化 $\mathbf{f}(\mathbf{a}+\mathbf{h}) - \mathbf{f}(\mathbf{a})$ 可以由一个线性变换 $J_{\mathbf{f}}(\mathbf{a})\mathbf{h}$ 来近似。雅可比矩阵 $J_{\mathbf{f}}(\mathbf{a})$ 正是这个最佳线性变换的矩阵表示。

让我们通过一个计算实例来阐明这个原理 [@problem_id:2325302]。考虑函数 $f(u, v) = (u^2 v, u \exp(v))$。我们希望利用线性近似来估计在点 $\mathbf{a} = (2, 0)$ 附近的点 $(2.1, -0.1)$ 处的函数值。

1.  **计算函数在基准点的值**：
    $\mathbf{f}(\mathbf{a}) = f(2, 0) = (2^2 \cdot 0, 2\exp(0)) = (0, 2)$。

2.  **计算位移向量**：
    $\mathbf{h} = (2.1, -0.1) - (2, 0) = (0.1, -0.1)$。

3.  **计算雅可比矩阵**：
    $J_f(u,v) = \begin{pmatrix} \frac{\partial}{\partial u}(u^2v)  \frac{\partial}{\partial v}(u^2v) \\ \frac{\partial}{\partial u}(u\exp(v))  \frac{\partial}{\partial v}(u\exp(v)) \end{pmatrix} = \begin{pmatrix} 2uv  u^2 \\ \exp(v)  u\exp(v) \end{pmatrix}$。

4.  **在基准点评估雅可比矩阵**：
    $J_f(2, 0) = \begin{pmatrix} 2(2)(0)  2^2 \\ \exp(0)  2\exp(0) \end{pmatrix} = \begin{pmatrix} 0  4 \\ 1  2 \end{pmatrix}$。

5.  **应用线性近似公式**：
    $$
    \mathbf{f}(2.1, -0.1) \approx \mathbf{f}(2, 0) + J_f(2, 0) \mathbf{h}
    $$
    $$
    \approx \begin{pmatrix} 0 \\ 2 \end{pmatrix} + \begin{pmatrix} 0  4 \\ 1  2 \end{pmatrix} \begin{pmatrix} 0.1 \\ -0.1 \end{pmatrix}
    $$
    $$
    \approx \begin{pmatrix} 0 \\ 2 \end{pmatrix} + \begin{pmatrix} 0(0.1) + 4(-0.1) \\ 1(0.1) + 2(-0.1) \end{pmatrix} = \begin{pmatrix} 0 \\ 2 \end{pmatrix} + \begin{pmatrix} -0.4 \\ -0.1 \end{pmatrix} = \begin{pmatrix} -0.4 \\ 1.9 \end{pmatrix}
    $$
    因此， $f(2.1, -0.1)$ 的线性近似值为 $(-0.4, 1.9)$。这个过程完美地展示了雅可比矩阵如何将一个复杂的非线性函数的局部行为转化为简单的线性代数运算。

### 雅可比矩阵在动力系统中的应用：线性化流场

雅可比矩阵在动力系统理论中扮演着核心角色。一个连续时间动力系统通常由一组一阶常微分方程描述：$\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$，其中 $\mathbf{x}$ 是状态向量，$\mathbf{f}(\mathbf{x})$ 是定义系统演化规律的向量场。

这个向量场 $\mathbf{f}(\mathbf{x})$ 本身就是一个从 $\mathbb{R}^n$到 $\mathbb{R}^n$ 的函数。因此，我们可以计算它的雅可比矩阵 $J_{\mathbf{f}}(\mathbf{x})$。这个矩阵描述了向量场（即相空间中每一点的速度向量）如何随位置的变化而变化。例如，著名的 **Rössler 系统** 是一个展示混沌行为的三维系统 [@problem_id:1717067]：
$$
\begin{aligned}
\frac{dx}{dt} = -y - z \\
\frac{dy}{dt} = x + ay \\
\frac{dz}{dt} = b + z(x - c)
\end{aligned}
$$
这里的向量场是 $\mathbf{f}(x, y, z) = (-y-z, x+ay, b+zx-cz)$。其雅可比矩阵 $J(x,y,z)$ 是一个 $3 \times 3$ 矩阵，通过计算偏导数得到：
$$
J(x,y,z) = \begin{pmatrix}
\frac{\partial f_1}{\partial x}  \frac{\partial f_1}{\partial y}  \frac{\partial f_1}{\partial z} \\
\frac{\partial f_2}{\partial x}  \frac{\partial f_2}{\partial y}  \frac{\partial f_2}{\partial z} \\
\frac{\partial f_3}{\partial x}  \frac{\partial f_3}{\partial y}  \frac{\partial f_3}{\partial z}
\end{pmatrix} = \begin{pmatrix}
0  -1  -1 \\
1  a  0 \\
z  0  x-c
\end{pmatrix}
$$
注意到，对于这个非线性系统，雅可比矩阵的元素依赖于系统的状态 $(x, y, z)$。

动力系统分析的一个关键任务是研究 **不动点 (fixed points)** 或 **平衡点 (equilibria)** 的稳定性。不动点 $\mathbf{x}^*$ 是满足 $\mathbf{f}(\mathbf{x}^*) = \mathbf{0}$ 的点。在不动点，系统状态不再随时间变化。为了理解系统在不动点附近的行为，我们考察一个小的扰动 $\mathbf{h} = \mathbf{x} - \mathbf{x}^*$。扰动的动力学由以下方程描述：
$$
\dot{\mathbf{h}} = \dot{\mathbf{x}} = \mathbf{f}(\mathbf{x}^* + \mathbf{h})
$$
利用线性近似，我们得到：
$$
\dot{\mathbf{h}} \approx \mathbf{f}(\mathbf{x}^*) + J_{\mathbf{f}}(\mathbf{x}^*)\mathbf{h}
$$
由于 $\mathbf{f}(\mathbf{x}^*) = \mathbf{0}$，上式简化为：
$$
\dot{\mathbf{h}} = J_{\mathbf{f}}(\mathbf{x}^*)\mathbf{h}
$$
这是一个常系数线性微分方程组！$J_{\mathbf{f}}(\mathbf{x}^*)$ 是一个常数矩阵，因为它是在不动点 $\mathbf{x}^*$ 处评估的。这个过程称为在不动点附近的 **线性化 (linearization)**。通过分析这个线性系统的行为，我们就能（在大多数情况下）推断出原始非线性系统在不动点附近的局部行为。

例如，在一个模拟两个相互抑制的神经元活动的模型中，不动点 $(0,0)$ 的稳定性至关重要 [@problem_id:1717082]。在该不动点计算雅可比矩阵，可以得到一个描述系统对微小扰动响应的线性系统。类似地，在分析两个物种竞争的生态模型时，共存平衡点 $(x^*, y^*)$ 的稳定性决定了两个物种是否能够长期共存 [@problem_id:1717077]。计算在该平衡点处的雅可比矩阵是分析其稳定性的第一步。

### 通过特征值进行稳定性分析

线性化后的系统 $\dot{\mathbf{h}} = J\mathbf{h}$ (其中 $J = J_{\mathbf{f}}(\mathbf{x}^*)$) 的解完全由矩阵 $J$ 的 **特征值 (eigenvalues)** 和 **特征向量 (eigenvectors)** 决定。这为我们提供了一个强大的、系统化的稳定性分类方法。

#### 连续时间系统

对于 $\dot{\mathbf{h}} = J\mathbf{h}$ 形式的连续时间系统，稳定性判据如下：
-   如果 $J$ 的所有特征值的 **实部都为负**，则不动点 $\mathbf{x}^*$ 是 **渐近稳定的 (asymptotically stable)**。附近的所有轨道都会随时间收敛到该不动点。
-   如果 $J$ 至少有一个特征值的 **实部为正**，则不动点是 **不稳定的 (unstable)**。至少存在一个方向，轨道会从该不动点附近离开。
-   如果 $J$ 的特征值中既有正实部的，也有负实部的，则该不动点是一个 **鞍点 (saddle point)**。

一个重要的定理，**Hartman-Grobman 定理**，指出如果一个不动点是 **双曲的 (hyperbolic)**（即雅可比矩阵的任何特征值都没有零实部），那么原始非线性系统在不动点附近的局部相图与其线性化系统的相图是拓扑共轭的。这意味着线性分析给出的稳定性结论（稳定、不稳定或鞍点）直接适用于原非线性系统。

对于二维系统，我们可以通过雅可比矩阵的 **迹 (trace)** $\text{Tr}(J)$ 和 **行列式 (determinant)** $\det(J)$ 快速了解特征值 $\lambda_1, \lambda_2$ 的性质，因为 $\lambda_1 + \lambda_2 = \text{Tr}(J)$ 且 $\lambda_1 \lambda_2 = \det(J)$。例如，在前面提到的物种竞争模型中 [@problem_id:1717077]，计算出在共存平衡点 $(5, 4)$ 处的雅可比矩阵为 $J = \begin{pmatrix} -0.5  -0.625 \\ -0.64  -0.2 \end{pmatrix}$。其行列式为 $\det(J) = (-0.5)(-0.2) - (-0.625)(-0.64) = 0.1 - 0.4 = -0.3$。由于行列式为负，这意味着两个特征值必定异号（一个正，一个负），因此该平衡点是一个鞍点，是不稳定的。

#### 离散时间系统

雅可比矩阵同样适用于分析离散时间动力系统 $\mathbf{x}_{k+1} = \mathbf{f}(\mathbf{x}_k)$。其不动点 $\mathbf{x}^*$ 满足 $\mathbf{x}^* = \mathbf{f}(\mathbf{x}^*)$。扰动 $\mathbf{h}_k = \mathbf{x}_k - \mathbf{x}^*$ 的线性化动态变为：
$$
\mathbf{h}_{k+1} \approx J_{\mathbf{f}}(\mathbf{x}^*)\mathbf{h}_k
$$
对于离散系统，稳定性判据与连续系统不同，它关注特征值的 **模 (magnitude)**：
-   如果 $J$ 的所有特征值的 **模都小于 1** ($|\lambda_i|  1$)，则不动点 $\mathbf{x}^*$ 是 **渐近稳定的**。
-   如果 $J$ 至少有一个特征值的 **模大于 1** ($|\lambda_i| > 1$)，则不动点是 **不稳定的**。

让我们来看一个两种微生物竞争的离散模型 [@problem_id:2216481]。该系统存在一个共存不动点 $(\frac{1}{2}, \frac{1}{3})$。在该点计算雅可比矩阵得到：
$$
J(\frac{1}{2}, \frac{1}{3}) = \begin{pmatrix} -0.5  -0.75 \\ -0.4  0.2 \end{pmatrix}
$$
通过求解特征方程 $\det(J - \lambda I) = 0$，我们发现特征值为 $\lambda_1 = 0.5$ 和 $\lambda_2 = -0.8$。因为这两个特征值的模都小于 1（$|0.5|  1$ 且 $|-0.8|  1$），我们可以断定这个共存不动点是渐近稳定的。由于特征值是实数，它是一个 **稳定结点 (stable node)**。

### 从雅可比矩阵获得的几何洞察

雅可比矩阵不仅能判断稳定性，还能揭示不动点周围相空间流动的精细几何结构。

#### 特征向量与稳定/不稳定流形

在鞍点类型的不动点处，存在一些特殊的轨道，它们直接趋向或离开不动点。这些轨道的集合构成了 **稳定流形 (stable manifold)** 和 **不稳定流形 (unstable manifold)**。Hartman-Grobman 定理告诉我们，在不动点处，非线性系统的这些流形与线性化系统的 **稳定与不稳定子空间** 相切。而这些子空间恰恰是由雅可比矩阵的特征向量张成的。

具体来说：
-   对应于负实部特征值的特征向量，张成了稳定子空间，它在不动点处与稳定流形相切。
-   对应于正实部特征值的特征向量，张成了不稳定子空间，它在不动点处与不稳定流形相切。

考虑一个在双阱势中运动的阻尼粒子模型 [@problem_id:1717045]。系统在原点 $(0,0)$ 有一个不动点。其线性化矩阵为 $A = \begin{pmatrix} 0  1 \\ \alpha  -\delta \end{pmatrix}$。其特征值为 $\lambda_{s,u} = \frac{-\delta \pm \sqrt{\delta^2 + 4\alpha}}{2}$。由于 $\alpha, \delta > 0$，我们得到一个负特征值 $\lambda_s$ 和一个正特征值 $\lambda_u$，确认原点是一个鞍点。与特征值 $\lambda$ 对应的特征向量为 $\begin{pmatrix} 1 \\ \lambda \end{pmatrix}$。因此，稳定流形在原点的切向量是 $\begin{pmatrix} 1 \\ \lambda_s \end{pmatrix}$，而不稳定流形在原点的切向量是 $\begin{pmatrix} 1 \\ \lambda_u \end{pmatrix}$。这些向量精确地指明了轨道趋向和离开原点的局部方向。

#### 迹、散度与体积变化

雅可比矩阵的另一个重要不变量是它的迹。矩阵的迹与向量微积分中的一个核心概念——**散度 (divergence)**——有着直接的联系。对于一个向量场 $\mathbf{f}$，其雅可比矩阵的迹等于向量场的散度：
$$
\text{Tr}(J_{\mathbf{f}}) = \sum_{i=1}^n \frac{\partial f_i}{\partial x_i} = \nabla \cdot \mathbf{f}
$$
这一点可以从一个旋转膨胀的气体云模型中得到清晰的验证 [@problem_id:1717046]。

散度的物理意义是向量场在某一点的源或汇的强度。在流体动力学的背景下，它代表了单位体积流体随时间变化的速率。在动力系统中，$\nabla \cdot \mathbf{f}$ 描述了相空间中一个微小体积（或面积）元随系统演化而膨胀或收缩的局部速率。具体来说，体积元 $V$ 的相对变化率为 $\frac{1}{V}\frac{dV}{dt} = \nabla \cdot \mathbf{f}$。

-   如果 $\nabla \cdot \mathbf{f} > 0$，相空间体积在局部是膨胀的。
-   如果 $\nabla \cdot \mathbf{f}  0$，相空间体积在局部是收缩的（这种情况称为耗散系统）。
-   如果 $\nabla \cdot \mathbf{f} = 0$，相空间体积是守恒的（例如在哈密顿系统中）。

在一个二维种群动态模型中 [@problem_id:1717065]，我们可以计算任意点 $(x,y)$ 的面积变化率：$\frac{1}{A}\frac{dA}{dt} = \frac{\partial \dot{x}}{\partial x} + \frac{\partial \dot{y}}{\partial y}$。这为我们提供了一个定量衡量在相空间特定区域，初始条件集合是倾向于发散还是聚集的工具。

### 进阶性质与局限性

#### 反函数的雅可比矩阵

雅可比矩阵在坐标变换中也很有用。根据 **反函数定理**，如果一个可微函数 $\mathbf{y} = \mathbf{f}(\mathbf{x})$ 在点 $\mathbf{x}_0$ 的雅可比矩阵 $J_{\mathbf{f}}(\mathbf{x}_0)$ 是可逆的（即行列式非零），那么在 $\mathbf{y}_0 = \mathbf{f}(\mathbf{x}_0)$ 的一个邻域内，反函数 $\mathbf{x} = \mathbf{f}^{-1}(\mathbf{y})$ 存在且可微。更重要的是，反函数的雅可比矩阵恰好是原函数雅可比矩阵的逆：
$$
J_{\mathbf{f}^{-1}}(\mathbf{y}_0) = [J_{\mathbf{f}}(\mathbf{x}_0)]^{-1}
$$
这个性质非常强大，因为它允许我们计算反函数的线性近似，而无需显式地求出反函数的解析表达式。例如，对于一个从 $(u,v)$ 坐标到 $(x,y)$ 坐标的复杂变换，如果我们想知道 $J_{f^{-1}}$ 在点 $(x,y)=(3,5)$ 的值，我们首先需要找到对应的原像点 $(u,v)=(2,1)$。然后计算正向变换在 $(2,1)$ 的雅可比矩阵 $J_f(2,1)$，最后对该矩阵求逆，即可得到 $J_{f^{-1}}(3,5)$ [@problem_id:2325295]。

#### 当线性化失效：非双曲点

尽管线性稳定性分析非常强大，但它有其局限性。Hartman-Grobman 定理的前提是，不动点必须是双曲的，即雅可比矩阵的所有特征值实部都不能为零。当存在一个或多个特征值的实部为零时，该不动点被称为 **非双曲的 (non-hyperbolic)**。

在这些临界情况下，线性化系统无法捕捉到原始非线性系统的真实动态。不动点的稳定性将由系统中的 **非线性项** 决定。

让我们看一个极具启发性的例子 [@problem_id:1717043]。考虑以下三个系统，它们都在原点 $(0,0)$ 有一个不动点：
1.  $\dot{x} = -x^3, \dot{y} = -y^3$
2.  $\dot{x} = x^3, \dot{y} = y^3$
3.  $\dot{x} = x^3, \dot{y} = -y^3$

对于这三个系统，在原点 $(0,0)$ 计算得到的雅可比矩阵都是 **零矩阵** $\begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}$。这意味着它的两个特征值都为零。线性分析完全失效，它无法提供任何关于稳定性的信息。

然而，通过直接分析非线性方程（例如，使用李雅普诺夫函数或分离变量法），我们可以确定它们的真实稳定性：
-   系统 (I) 的原点是 **渐近稳定的**。所有轨道都趋向于原点。
-   系统 (II) 的原点是 **不稳定的**。所有轨道都远离原点。
-   系统 (III) 的原点是一个 **鞍点**。在 $y$ 轴方向是稳定的，在 $x$ 轴方向是不稳定的。

这个例子清楚地表明，当遇到非双曲不动点时，我们必须超越线性化，采用更高阶的分析方法（如中心流形理论或范式理论）来确定其稳定性。雅可比矩阵是第一步，也是最重要的一步，但理解它的局限性同样至关重要。