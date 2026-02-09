## 引言
在微分几何中，理解曲面如何在三维空间中弯曲是核心任务之一。第一基本形式让我们能够在曲面上测量距离和角度，描述其“内蕴”几何，但它无法区分像平面和圆柱面这样本质弯曲不同的曲面。为了捕捉这种“外在”的弯曲，我们必须研究曲面法向量的变化。温加滕方程正是为解决这一问题而生的关键工具，它精确地量化了法向量如何随位置变化，从而揭示了曲面外在曲率的秘密。

本文将分为三个部分，系统地引导您掌握这一概念。在“原理与机制”一章中，我们将从定义形算子出发，推导温加滕方程的矩阵形式，并揭示其与高斯曲率、平均曲率的深刻联系。接下来，“应用与交叉学科联系”一章将展示温加滕方程如何在工程、物理学和计算机图形学等领域中定义特殊曲面（如极小曲面）并解决实际问题。最后，通过“动手实践”部分的精选习题，您将有机会亲手计算并应用温加滕映射，将理论知识转化为解决问题的能力。

## 原理与机制

在上一章中，我们引入了曲面的概念，并探讨了如何通过第一基本形式来描述其内在几何性质，例如在曲面上测量长度和角度。然而，第一基本形式本身并不能完全捕捉曲面在三维欧几里得空间中的弯曲方式。例如，一个平面和一个圆柱面可以局部地具有相同的内蕴几何（它们是局部等距的），但它们在周围空间中的形状显然是不同的。为了量化这种“外在”的弯曲，我们必须研究曲面[法向量](@entry_id:264185)的变化。本章将介绍一个核心工具——Weingarten 映射，它精确地描述了法向量如何随我们在曲面上的移动而改变，从而揭示了曲面的外在曲率。

### 形状算子与 Weingarten 映射

想象一个嵌入在三维欧几里得空间 $\mathbb{R}^3$ 中的光滑曲面 $S$。在曲面上的每一点 $p$，我们都可以定义一个切平面 $T_pS$ 和一个与之垂直的单位法向量 $\mathbf{N}$。当我们沿着曲面上的一条路径移动时，这个法向量的方向通常会发生变化。正是这种变化率揭示了曲面在该点的弯曲信息。如果法向量在某个区域内保持不变，那么该区域必然是平的。

为了形式化地描述这一点，我们考虑在点 $p$ 处沿切向量 $\mathbf{v} \in T_pS$ 方向上单位法向量场 $\mathbf{N}$ 的变化。这个变化由方向导数 $D_{\mathbf{v}}\mathbf{N}$ 给出。一个关键且并非显而易见的性质是，这个导数向量 $D_{\mathbf{v}}\mathbf{N}$ 本身也位于切平面 $T_pS$ 中。我们可以通过对恒等式 $\langle \mathbf{N}, \mathbf{N} \rangle = 1$ 求导来证明这一点：
$$
\langle D_{\mathbf{v}}\mathbf{N}, \mathbf{N} \rangle + \langle \mathbf{N}, D_{\mathbf{v}}\mathbf{N} \rangle = 2 \langle D_{\mathbf{v}}\mathbf{N}, \mathbf{N} \rangle = 0
$$
这个结果表明 $D_{\mathbf{v}}\mathbf{N}$ 与 $\mathbf{N}$ 正交，因此它必须位于与 $\mathbf{N}$ 正交的切平面 $T_pS$ 中 [@problem_id:1685663]。

既然对于任意切向量 $\mathbf{v} \in T_pS$，其对应的法向量变化率 $D_{\mathbf{v}}\mathbf{N}$ 也是一个切向量，这便允许我们定义一个从切平面到其自身的线性映射。这个映射被称为**形状算子 (Shape Operator)** 或 **Weingarten 映射**，记为 $L_p$，其定义为：
$$
L_p(\mathbf{v}) = -D_{\mathbf{v}}\mathbf{N}
$$
定义中的负号是一个惯例，它使得对于一个标准的球面，其曲率为正值。形状算子 $L_p$ 是一个作用于 $T_pS$ 上的线性算子，它将一个“方向”向量 $\mathbf{v}$ 映射到该方向上法向量的变化率（带有负号）。因此，它完整地编码了曲面在点 $p$ 处如何弯曲的所有信息。

### Weingarten 方程：映射的矩阵表示

为了进行具体的计算，我们需要为形状算子找到一个矩阵表示。假设曲面由一个正则参数化 $\mathbf{x}(u, v)$ 给出。在任意一点，切平面 $T_pS$ 都由基向量 $\{\mathbf{x}_u, \mathbf{x}_v\}$ 张成，其中 $\mathbf{x}_u = \frac{\partial \mathbf{x}}{\partial u}$ 且 $\mathbf{x}_v = \frac{\partial \mathbf{x}}{\partial v}$。

根据形状算子的定义，它在基向量上的作用为：
$$
L_p(\mathbf{x}_u) = -\frac{\partial \mathbf{N}}{\partial u} = -\mathbf{N}_u
$$
$$
L_p(\mathbf{x}_v) = -\frac{\partial \mathbf{N}}{\partial v} = -\mathbf{N}_v
$$
由于 $-\mathbf{N}_u$ 和 $-\mathbf{N}_v$ 都是切向量，它们可以表示为基向量 $\{\mathbf{x}_u, \mathbf{x}_v\}$ 的线性组合。我们将这些关系式写出，便得到了 **Weingarten 方程**：
$$
\begin{align*}
\mathbf{N}_u = a \mathbf{x}_u + b \mathbf{x}_v \\
\mathbf{N}_v = p \mathbf{x}_u + q \mathbf{x}_v
\end{align*}
$$
其中系数 $a, b, p, q$ 是关于 $u$ 和 $v$ 的函数。这些方程明确地将法向量的偏导数与切向量基底联系起来。

如果我们用 $W$ 表示形状算子 $L_p$ 在基 $\{\mathbf{x}_u, \mathbf{x}_v\}$ 下的矩阵，那么该矩阵的列就是 $L_p$ 作用于基向量后所得向量的坐标。具体来说：
$$
L_p(\mathbf{x}_u) = -\mathbf{N}_u = -a \mathbf{x}_u - b \mathbf{x}_v
$$
$$
L_p(\mathbf{x}_v) = -\mathbf{N}_v = -p \mathbf{x}_u - q \mathbf{x}_v
$$
因此，Weingarten 矩阵 $W$ 为：
$$
W = \begin{pmatrix} -a  -p \\ -b  -q \end{pmatrix}
$$
换言之，Weingarten 矩阵的第一列是向量 $-\mathbf{N}_u$ 在基 $\{\mathbf{x}_u, \mathbf{x}_v\}$ 下的坐标，第二列是向量 $-\mathbf{N}_v$ 在该基下的坐标 [@problem_id:1685625]。

### 联结基本形式：计算 Weingarten 矩阵

Weingarten 方程的系数 $a, b, p, q$ 不是凭空产生的。它们与我们在之前章节中遇到的第一和第二基本形式密切相关。回顾一下，第一基本形式的系数为 $E = \langle \mathbf{x}_u, \mathbf{x}_u \rangle$, $F = \langle \mathbf{x}_u, \mathbf{x}_v \rangle$, $G = \langle \mathbf{x}_v, \mathbf{x}_v \rangle$；第二基本形式的系数为 $L = \langle \mathbf{x}_{uu}, \mathbf{N} \rangle$, $M = \langle \mathbf{x}_{uv}, \mathbf{N} \rangle$, $N = \langle \mathbf{x}_{vv}, \mathbf{N} \rangle$。

通过对恒等式 $\langle \mathbf{N}, \mathbf{x}_u \rangle = 0$ 和 $\langle \mathbf{N}, \mathbf{x}_v \rangle = 0$ 求导，我们可以得到：
$$
\langle \mathbf{N}_u, \mathbf{x}_u \rangle = -\langle \mathbf{N}, \mathbf{x}_{uu} \rangle = -L
$$
$$
\langle \mathbf{N}_u, \mathbf{x}_v \rangle = -\langle \mathbf{N}, \mathbf{x}_{uv} \rangle = -M
$$
$$
\langle \mathbf{N}_v, \mathbf{x}_u \rangle = -\langle \mathbf{N}, \mathbf{x}_{vu} \rangle = -M
$$
$$
\langle \mathbf{N}_v, \mathbf{x}_v \rangle = -\langle \mathbf{N}, \mathbf{x}_{vv} \rangle = -N
$$
现在，我们将 Weingarten 方程 $\mathbf{N}_u = a \mathbf{x}_u + b \mathbf{x}_v$ 与 $\mathbf{x}_u$ 和 $\mathbf{x}_v$ 作内积：
$$
\langle \mathbf{N}_u, \mathbf{x}_u \rangle = a \langle \mathbf{x}_u, \mathbf{x}_u \rangle + b \langle \mathbf{x}_v, \mathbf{x}_u \rangle \implies -L = aE + bF
$$
$$
\langle \mathbf{N}_u, \mathbf{x}_v \rangle = a \langle \mathbf{x}_u, \mathbf{x}_v \rangle + b \langle \mathbf{x}_v, \mathbf{x}_v \rangle \implies -M = aF + bG
$$
类似地，从 $\mathbf{N}_v = p \mathbf{x}_u + q \mathbf{x}_v$ 可得：
$$
-M = pE + qF
$$
$$
-N = pF + qG
$$
这些方程可以优雅地写成矩阵形式。令第一和第二基本形式的矩阵分别为 $\mathbf{I}$ 和 $\mathbf{II}$：
$$
\mathbf{I} = \begin{pmatrix} E  F \\ F  G \end{pmatrix}, \quad \mathbf{II} = \begin{pmatrix} L  M \\ M  N \end{pmatrix}
$$
那么上述四个方程可以表示为：
$$
-\mathbf{II} = \begin{pmatrix} E  F \\ F  G \end{pmatrix} \begin{pmatrix} a  p \\ b  q \end{pmatrix} = \mathbf{I} (-W)
$$
因此，我们得到了计算 Weingarten 矩阵的核心公式：
$$
W = \mathbf{I}^{-1} \mathbf{II}
$$
这个公式是微分几何的基石之一，它将抽象的形状算子与可以通过参数化直接计算的两个基本形式联系起来。

**示例：螺旋面的 Weingarten 矩阵**
让我们以一个右螺旋面为例，其参数化为 $\mathbf{x}(u, v) = (u \cos v, u \sin v, c v)$ [@problem_id:1685687]。
1.  **第一基本形式**:
    $\mathbf{x}_u = (\cos v, \sin v, 0)$
    $\mathbf{x}_v = (-u \sin v, u \cos v, c)$
    计算内积得到 $E = 1$, $F = 0$, $G = u^2 + c^2$。由于 $F=0$，这是一个正交参数化。
    矩阵 $\mathbf{I} = \begin{pmatrix} 1  0 \\ 0  u^2+c^2 \end{pmatrix}$。

2.  **第二基本形式**:
    单位法向量 $\mathbf{N} = \frac{1}{\sqrt{u^2+c^2}}(c \sin v, -c \cos v, u)$。
    二阶偏导数 $\mathbf{x}_{uu} = (0,0,0)$, $\mathbf{x}_{uv} = (-\sin v, \cos v, 0)$, $\mathbf{x}_{vv} = (-u \cos v, -u \sin v, 0)$。
    计算与 $\mathbf{N}$ 的内积得到 $L=0$, $M = -\frac{c}{\sqrt{u^2+c^2}}$, $N=0$。
    矩阵 $\mathbf{II} = \begin{pmatrix} 0  -c/\sqrt{u^2+c^2} \\ -c/\sqrt{u^2+c^2}  0 \end{pmatrix}$。

3.  **Weingarten 矩阵**:
    $\mathbf{I}^{-1} = \begin{pmatrix} 1  0 \\ 0  1/(u^2+c^2) \end{pmatrix}$。
    $W = \mathbf{I}^{-1} \mathbf{II} = \begin{pmatrix} 1  0 \\ 0  1/(u^2+c^2) \end{pmatrix} \begin{pmatrix} 0  -c/\sqrt{u^2+c^2} \\ -c/\sqrt{u^2+c^2}  0 \end{pmatrix} = \begin{pmatrix} 0  -c/(u^2+c^2)^{1/2} \\ -c/(u^2+c^2)^{3/2}  0 \end{pmatrix}$。
    这个矩阵描述了螺旋面上任意一点的形状算子。例如，在另一个螺旋面参数化 [@problem_id:1510681] 的计算中，也可以通过类似步骤得到其 Weingarten 矩阵的系数。

### 几何不变量：形状算子的特征值

由于形状算子 $L_p$ 是一个作用于二维向量空间 $T_pS$ 上的线性算子，我们可以研究它的特征值和特征向量。这些量具有深刻的几何意义。

一个至关重要的性质是，**形状算子是自伴的 (self-adjoint)**。这意味着对于任意两个切向量 $\mathbf{w}_1, \mathbf{w}_2 \in T_pS$，以下关系成立：
$$
\langle L_p(\mathbf{w}_1), \mathbf{w}_2 \rangle_I = \langle \mathbf{w}_1, L_p(\mathbf{w}_2) \rangle_I
$$
其中 $\langle \cdot, \cdot \rangle_I$ 是由第一基本形式定义的内积。其矩阵形式为 $W^T \mathbf{I} = \mathbf{I} W$。这个性质可以由 $W=\mathbf{I}^{-1}\mathbf{II}$ 以及 $\mathbf{I}$ 和 $\mathbf{II}$ 都是对称矩阵直接导出 [@problem_id:1685672]。自伴算子的一个重要推论是它的特征值总是实数，并且对应不同特征值的特征向量在此内积下是正交的。

- **主曲率和主方向**: 形状算子 $L_p$ 的两个实数特征值，记为 $\kappa_1$ 和 $\kappa_2$，被称为曲面的**主曲率**。它们对应的特征向量所指的方向被称为**主方向**。从几何上看，主方向是曲面在这一点上弯曲得最厉害和最平缓的方向，而主曲率则量化了这些方向上的法曲率。

- **高斯曲率和平均曲率**: 形状算子的矩阵不变量（即不依赖于基选择的量）定义了曲面最重要的两个曲率不变量。
    - **高斯曲率 (Gaussian Curvature)**, $K$，定义为形状算子的行列式：
      $$K = \det(L_p) = \kappa_1 \kappa_2$$
      利用 $W = \mathbf{I}^{-1}\mathbf{II}$，我们得到 $K = \det(\mathbf{I}^{-1}\mathbf{II}) = \frac{\det(\mathbf{II})}{\det(\mathbf{I})} = \frac{LN - M^2}{EG - F^2}$。这是一个非常著名的公式 [@problem_id:1685645]。
    - **平均曲率 (Mean Curvature)**, $H$，定义为形状算子迹的一半：
      $$H = \frac{1}{2} \text{tr}(L_p) = \frac{1}{2}(\kappa_1 + \kappa_2)$$
      利用矩阵的迹，可以得到 $H = \frac{1}{2} \text{tr}(\mathbf{I}^{-1}\mathbf{II}) = \frac{EN - 2FM + GL}{2(EG - F^2)}$。

高斯曲率和平均曲率为我们提供了描述和分类曲面形状的强大工具 [@problem_id:1685682]。例如，在某点 $p$ 处，如果 $\kappa_1$ 和 $\kappa_2$ 同号（$K>0$），则该点是**椭圆点**（如球面）；如果异号（$K<0$），则是**双曲点**（如马鞍面）；如果其中一个为零（$K=0$），则是**抛物点**。一个典型的计算例子是在椭圆抛物面 $z = 2x^2 + y^2$ 的原点处，其形状算子矩阵恰好为 $\begin{pmatrix} 4  0 \\ 0  2 \end{pmatrix}$，主曲率为 $4$ 和 $2$ [@problem_id:1685663]。

### 内蕴几何 vs. 外在几何

Weingarten 映射是研究**外在曲率**的终极工具，它描述了曲面如何嵌入到周围空间中。这与仅由第一基本形式决定的**内蕴几何**形成对比。

一个经典的例子是平面和圆柱面的比较 [@problem_id:1685629]。
- 平面 $\mathbf{x}(u,v) = (u,v,0)$ 的第一基本形式为 $E=1, F=0, G=1$。它的法向量处处恒定，因此 $\mathbf{N}_u = \mathbf{N}_v = \mathbf{0}$，Weingarten 矩阵为零矩阵。主曲率 $\kappa_1=\kappa_2=0$，高斯曲率 $K=0$，平均曲率 $H=0$。
- 半径为 $R$ 的圆柱面 $\mathbf{y}(u,v) = (R \cos(u/R), R \sin(u/R), v)$ 也具有相同的第一基本形式 $E=1, F=0, G=1$。这意味着从内蕴几何的角度看，它和平面是不可区分的（它们是局部等距的）。然而，它的 Weingarten 矩阵不是零矩阵。计算可得其主曲率为 $\kappa_1 = -1/R$ 和 $\kappa_2 = 0$。因此，高斯曲率 $K=0$，但平均曲率 $H = -1/(2R)$。

这个例子清晰地表明，尽管平面和圆柱面在“内部”看起来一样，但 Weingarten 映射及其特征值（主曲率）捕捉到了圆柱面在三维空间中的弯曲，而平面没有。因此，Weingarten 映射是研究外在几何的关键。

### 高斯-科达齐方程与曲面基本定理

我们已经看到，曲面的几何由第一和第二基本形式决定。高斯公式将二阶导数 $\mathbf{x}_{ij}$ 分解到切向和法向，而 Weingarten 方程将法向量的导数 $\mathbf{N}_i$ 分解到切向。这两个方程组共同构成了一个关于活动标架 $\{\mathbf{x}_u, \mathbf{x}_v, \mathbf{N}\}$ 的一阶偏微分方程组。

一个自然的问题是：是否任意给定的一组第一和第二基本形式都能对应一个实际存在的曲面？答案是否定的。这些形式必须满足一定的相容性条件，这些条件源于三阶导数的可交换性（Clairaut 定理）。

例如，由 $(\mathbf{x}_{uu})_v = (\mathbf{x}_{uv})_u$ 可导出两个方程 [@problem_id:1669373]：
1.  比较法向分量，得到一个**科达齐-梅纳尔迪 (Codazzi-Mainardi) 方程**。例如，$L_v - M_u = L \Gamma^1_{12} + M(\Gamma^2_{12} - \Gamma^1_{11}) - N \Gamma^2_{11}$。
2.  比较切向分量，得到著名的**高斯方程 (Gauss Equation)**，它将高斯曲率 $K$ 完全用第一基本形式的系数及其导数（即 Christoffel 符号 $\Gamma^k_{ij}$）表示。这便是高斯“绝妙定理”的分析形式。

同样，由 $(\mathbf{x}_{uv})_v = (\mathbf{x}_{vv})_u$ 可以得到另一个 Codazzi-Mainardi 方程。这些相容性条件统称为**高斯-科达齐 (Gauss-Codazzi) 方程**。

这些方程的重要性体现在**曲面基本定理 (Fundamental Theorem of Surface Theory)** 中：
> 只要给定的第一基本形式（正定）和第二基本形式（对称）满足高斯-科达齐方程，那么在 $\mathbb{R}^3$ 中就唯一地（在刚体运动意义下）存在一个曲面，它以这两个形式为其基本形式。

因此，Weingarten 映射和高斯公式不仅是分析已知曲面的工具，它们和其相容性条件（高斯-科达齐方程）一起，构成了从抽象的度量和曲率信息“构建”曲面的理论基础 [@problem_id:1685635]。

综上所述，Weingarten 映射是连接曲面内蕴几何（第一基本形式）和外在几何（第二基本形式）的桥梁。它通过描述法向量的变化来量化曲面的弯曲，其特征值和不变量（主曲率、高斯曲率、平均曲率）是现代微分几何中描述和分类曲面的核心概念。