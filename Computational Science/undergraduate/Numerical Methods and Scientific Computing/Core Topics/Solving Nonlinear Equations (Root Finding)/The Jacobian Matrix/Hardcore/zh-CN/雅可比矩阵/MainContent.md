## 引言
在单变量微积分中，导数衡量了函数在一点上的瞬时变化率，是理解函数局部行为的基石。然而，当我们面对更复杂的现实世界问题时——从机器人的多关节运动到经济模型的多变量交互——我们通常需要处理从一个多维空间到另一个多维空间的函数。此时，一个简单的数字已不足以描述其变化。我们如何将导数的概念推广到高维空间，以精确捕捉这种复杂的变化呢？

[雅可比矩阵](@entry_id:264467)正是这个问题的答案。它不仅是单变量导数向多维的自然延伸，更是一个强大的数学工具，其应用遍及科学与工程的各个角落。本文将带领您系统地探索雅可比矩阵的奥秘。首先，在**“原理与机制”**一章中，我们将从其定义出发，深入理解它如何作为[最佳线性近似](@entry_id:164642)，并探讨其[行列式](@entry_id:142978)和迹等量的深刻几何与物理意义。接着，在**“应用与跨学科联系”**一章中，我们将展示[雅可比矩阵](@entry_id:264467)如何在[机器人学](@entry_id:150623)、动力[系统稳定性](@entry_id:273248)分析、数值计算和机器学习等前沿领域中扮演关键角色。最后，通过**“动手实践”**部分，您将有机会亲手计算和应用[雅可比矩阵](@entry_id:264467)，巩固所学知识。

通过这趟学习之旅，您将掌握一个连接微积分、线性代数和众多应用学科的核心概念。现在，让我们从雅可比矩阵的基本原理开始。

## 原理与机制

在单变量微积分中，导数是描述函数局部行为的核心工具。它给出了函数图形在某一点上[切线的斜率](@entry_id:192479)，从而为我们提供了该点附近函数的[最佳线性近似](@entry_id:164642)。当我们从单变量函数迈向多变量[向量值函数](@entry_id:261164)时，即形如 $F: \mathbb{R}^n \to \mathbb{R}^m$ 的映射，我们需要一个更强大的工具来描述其局部变化。这个工具就是**雅可比矩阵 (Jacobian Matrix)**。本章将深入探讨[雅可比矩阵](@entry_id:264467)的定义、核心原理及其在多个学科领域中的关键作用。

### 雅可比矩阵的定义与结构

考虑一个[向量值函数](@entry_id:261164) $\mathbf{y} = F(\mathbf{x})$，它将 $n$ 维空间中的点 $\mathbf{x} = (x_1, x_2, \dots, x_n)$ 映射到 $m$ 维空间中的点 $\mathbf{y} = (y_1, y_2, \dots, y_m)$。该函数由 $m$ 个分量函数组成：
$$
\begin{aligned}
y_1 = F_1(x_1, x_2, \dots, x_n) \\
y_2 = F_2(x_1, x_2, \dots, x_n) \\
\vdots \\
y_m = F_m(x_1, x_2, \dots, x_n)
\end{aligned}
$$
为了完全刻画函数 $F$ 在某一点的局部行为，我们需要了解每一个输出分量 $y_i$ 如何随每一个输入变量 $x_j$ 的变化而变化。这种变化率正是由偏导数 $\frac{\partial F_i}{\partial x_j}$ 来描述的。

**[雅可比矩阵](@entry_id:264467)** $J_F$ 正是将所有这些一阶偏导数组织在一起而形成的矩阵。对于一个[可微函数](@entry_id:144590) $F: \mathbb{R}^n \to \mathbb{R}^m$，其在点 $\mathbf{x}$ 的雅可比矩阵是一个 $m \times n$ 矩阵，定义如下：
$$
J_F(\mathbf{x}) = \begin{pmatrix}
\frac{\partial F_1}{\partial x_1}  \frac{\partial F_1}{\partial x_2}  \cdots  \frac{\partial F_1}{\partial x_n} \\
\frac{\partial F_2}{\partial x_1}  \frac{\partial F_2}{\partial x_2}  \cdots  \frac{\partial F_2}{\partial x_n} \\
\vdots  \vdots  \ddots  \vdots \\
\frac{\partial F_m}{\partial x_1}  \frac{\partial F_m}{\partial x_2}  \cdots  \frac{\partial F_m}{\partial x_n}
\end{pmatrix}
$$
矩阵的第 $i$ 行是第 $i$ 个分量函数 $F_i$ 的梯度向量 $\nabla F_i$ 的转置，而第 $j$ 列则包含了所有输出分量对输入变量 $x_j$ 的[偏导数](@entry_id:146280)。

让我们通过一个具体的例子来理解其构造 。考虑一个从 $\mathbb{R}^3$ 到 $\mathbb{R}^2$ 的函数 $F(x, y, z) = (F_1, F_2)$，其中：
$$
F_1(x, y, z) = x^2 y + \sin(z)
$$
$$
F_2(x, y, z) = z \exp(x) - y^2
$$
根据定义，其雅可比矩阵是一个 $2 \times 3$ 矩阵：
$$
J_{F}(x,y,z)=\begin{pmatrix}
\frac{\partial F_{1}}{\partial x}  \frac{\partial F_{1}}{\partial y}  \frac{\partial F_{1}}{\partial z} \\
\frac{\partial F_{2}}{\partial x}  \frac{\partial F_{2}}{\partial y}  \frac{\partial F_{2}}{\partial z}
\end{pmatrix}
$$
我们逐一计算这些偏导数：
$$
\frac{\partial F_{1}}{\partial x}=2xy, \quad \frac{\partial F_{1}}{\partial y}=x^{2}, \quad \frac{\partial F_{1}}{\partial z}=\cos(z)
$$
$$
\frac{\partial F_{2}}{\partial x}=z\exp(x), \quad \frac{\partial F_{2}}{\partial y}=-2y, \quad \frac{\partial F_{2}}{\partial z}=\exp(x)
$$
将这些表达式代入，得到雅可比矩阵的一般形式：
$$
J_{F}(x,y,z)=\begin{pmatrix}
2xy  x^2  \cos(z) \\
z\exp(x)  -2y  \exp(x)
\end{pmatrix}
$$
通常，我们更关心雅可比矩阵在特定点的值，因为它描述了函数在该点邻域的局部特性。例如，在点 $P_0 = (0, 1, \pi)$，我们只需将这些坐标值代入上述矩阵：
$$
J_{F}(0,1,\pi)=\begin{pmatrix}
2(0)(1)  0^2  \cos(\pi) \\
\pi\exp(0)  -2(1)  \exp(0)
\end{pmatrix} = \begin{pmatrix}
0  0  -1 \\
\pi  -2  1
\end{pmatrix}
$$
这个 $2 \times 3$ 矩阵精确地捕捉了函数 $F$ 在点 $(0, 1, \pi)$ 附近的线性变化行为。

### 作为线性近似的[雅可比矩阵](@entry_id:264467)

雅可比矩阵最重要的作用是提供了[向量值函数](@entry_id:261164)在某一点附近的**[最佳线性近似](@entry_id:164642)**。这完全是单变量导数概念的自然推广。对于单变量函数 $f(x)$，其在 $x_0$ 附近的线性近似为 $f(x) \approx f(x_0) + f'(x_0)(x-x_0)$。类似地，对于[向量值函数](@entry_id:261164) $F(\mathbf{x})$，其在 $\mathbf{x}_0$ 附近的线性近似（或一阶泰勒展开）由下式给出：
$$
F(\mathbf{x}) \approx F(\mathbf{x}_0) + J_F(\mathbf{x}_0)(\mathbf{x} - \mathbf{x}_0)
$$
这里，$F(\mathbf{x}_0)$ 是函数在基准点的值，它是一个 $m \times 1$ 的向量。$\mathbf{x} - \mathbf{x}_0$ 是一个 $n \times 1$ 的输入位移向量。而 $m \times n$ 的雅可比矩阵 $J_F(\mathbf{x}_0)$ 扮演了一个线性变换的角色，它将输入空间中的微小位移向量 $(\mathbf{x} - \mathbf{x}_0)$ 映射到输出空间中的近似位移向量 $F(\mathbf{x}) - F(\mathbf{x}_0)$。

一个直观的特例是当函数本身就是线性变换时。考虑一个[线性变换](@entry_id:149133) $T: \mathbb{R}^3 \to \mathbb{R}^2$ ，它可以表示为矩阵乘法 $T(\mathbf{x}) = A\mathbf{x}$。例如：
$$
\mathbf{y} = \begin{pmatrix} y_1 \\ y_2 \end{pmatrix} = \begin{pmatrix} 2  -1  5 \\ 3  0  -4 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix}
$$
展开后得到分量函数：
$$
\begin{aligned}
y_1 = 2x_1 - x_2 + 5x_3 \\
y_2 = 3x_1 - 4x_3
\end{aligned}
$$
计算这个变换的雅可比矩阵，我们会发现其元素恰好是矩阵 $A$ 的元素：
$$
J_T = \begin{pmatrix}
\frac{\partial y_1}{\partial x_1}  \frac{\partial y_1}{\partial x_2}  \frac{\partial y_1}{\partial x_3} \\
\frac{\partial y_2}{\partial x_1}  \frac{\partial y_2}{\partial x_2}  \frac{\partial y_2}{\partial x_3}
\end{pmatrix} = \begin{pmatrix} 2  -1  5 \\ 3  0  -4 \end{pmatrix} = A
$$
这验证了一个重要的结论：一个[线性变换](@entry_id:149133)的[最佳线性近似](@entry_id:164642)就是它自身，其雅可比矩阵就是定义该变换的矩阵，且不随点的变化而变化。

在工程实践中，线性近似具有巨大的价值，因为它能将复杂的[非线性](@entry_id:637147)问题简化为易于分析的线性问题。一个典型的例子是机器人学中的[运动学](@entry_id:173318) 。一个二连杆平面机械臂的末端执行器位置 $(x, y)$ 是其关节角度 $(\theta_1, \theta_2)$ 的[非线性](@entry_id:637147)函数：
$$
\begin{aligned}
x(\theta_1, \theta_2) = L_1 \cos(\theta_1) + L_2 \cos(\theta_1 + \theta_2) \\
y(\theta_1, \theta_2) = L_1 \sin(\theta_1) + L_2 \sin(\theta_1 + \theta_2)
\end{aligned}
$$
其中 $L_1$ 和 $L_2$ 是连杆长度。要控制机械臂进行微小、精确的移动，我们可以利用[雅可比矩阵](@entry_id:264467)在某个工作姿态 $(\theta_{1,0}, \theta_{2,0})$ 附近建立一个[线性模型](@entry_id:178302)。例如，在 $(\theta_{1,0}, \theta_{2,0}) = (0, \pi/2)$ 附近，我们首先计算该点的末端位置 $P(0, \pi/2) = (L_1, L_2)$。然后计算[雅可比矩阵](@entry_id:264467) $J_P(\theta_1, \theta_2)$ 并在该点求值，得到：
$$
J_P(0, \pi/2) = \begin{pmatrix} -L_2  -L_2 \\ L_1  0 \end{pmatrix}
$$
根据线性近似公式，末端位置 $P(\theta_1, \theta_2)$ 可以近似为：
$$
\begin{aligned}
P(\theta_1, \theta_2) \approx P(0, \pi/2) + J_P(0, \pi/2) \begin{pmatrix} \theta_1 - 0 \\ \theta_2 - \pi/2 \end{pmatrix} \\
\approx \begin{pmatrix} L_1 \\ L_2 \end{pmatrix} + \begin{pmatrix} -L_2  -L_2 \\ L_1  0 \end{pmatrix} \begin{pmatrix} \theta_1 \\ \theta_2 - \pi/2 \end{pmatrix} = \begin{pmatrix} L_1 - L_2\theta_1 - L_2(\theta_2 - \pi/2) \\ L_2 + L_1\theta_1 \end{pmatrix}
\end{aligned}
$$
这个线性关系式直接关联了关节角度的微小变化与末端执行器位置的微小变化，对于设计控制器至关重要。

### [雅可比矩阵](@entry_id:264467)的几何诠释

除了作为线性近似的代数工具，[雅可比矩阵](@entry_id:264467)及其相关量具有深刻的几何意义。

#### [雅可比行列式](@entry_id:137120)：局部体积/面积的缩放因子

当雅可比矩阵为方阵时（即映射 $F: \mathbb{R}^n \to \mathbb{R}^n$），其[行列式](@entry_id:142978)被称为**[雅可比行列式](@entry_id:137120) (Jacobian Determinant)**，记作 $\det(J_F)$ 或 $\frac{\partial(F_1, \dots, F_n)}{\partial(x_1, \dots, x_n)}$。

雅可比行列式的值衡量了函数 $F$ 在某一点附近对“体积”的局部缩放效应。更准确地说，在点 $\mathbf{x}$ 处的一个无穷小区域，其体积为 $dV$，经过 $F$ 变换后，其像的体积近似为 $|\det(J_F(\mathbf{x}))| dV$。

这个性质是[多重积分](@entry_id:146170)换元公式的核心。当我们将积分从一个[坐标系](@entry_id:156346)（如笛卡尔坐标 $(x,y)$）变换到另一个[坐标系](@entry_id:156346)（如极坐标 $(r, \theta)$ 或任意的 $(u,v)$ 坐标）时，面积（或体积）微元会发生改变。这个改变的[比例因子](@entry_id:266678)恰好是雅可比行列式的[绝对值](@entry_id:147688)。例如，在二维情况下，面积微元的关系为：
$$
dA_{xy} = \left| \frac{\partial(x,y)}{\partial(u,v)} \right| du \, dv
$$
考虑一个从 $(u,v)$ 平面到 $(x,y)$ 平面的[坐标变换](@entry_id:172727) $x(u,v) = u \exp(v)$, $y(u,v) = u \exp(-v)$ 。为了计算 $(u,v)$ 平面中一个矩形区域 $R: \{1 \le u \le 2, 0 \le v \le \ln(3)\}$ 经过变换后在 $(x,y)$ 平面中形成的区域 $S$ 的面积，我们首先计算雅可比行列式：
$$
J(u,v) = \det \begin{pmatrix} \frac{\partial x}{\partial u}  \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u}  \frac{\partial y}{\partial v} \end{pmatrix} = \det \begin{pmatrix} \exp(v)  u \exp(v) \\ \exp(-v)  -u \exp(-v) \end{pmatrix} = -u \exp(v)\exp(-v) - u \exp(v)\exp(-v) = -2u
$$
区域 $S$ 的面积可以通过对区域 $R$ 积分雅可比行列式的[绝对值](@entry_id:147688)得出：
$$
\text{Area}(S) = \iint_R |J(u,v)| \,du\,dv = \int_{0}^{\ln(3)} \int_{1}^{2} |-2u| \,du\,dv = \int_{0}^{\ln(3)} \int_{1}^{2} 2u \,du\,dv = 3\ln(3)
$$
这个强大的工具使我们能够计算由复杂变换定义的区域的面积或体积 。

#### 雅可比矩阵的列向量：变换后的[基向量](@entry_id:199546)

[雅可比矩阵](@entry_id:264467)的列向量本身也具有直观的几何意义。考虑一个从 $(u,v)$ 平面到 $(x,y)$ 平面的映射 $F(u,v) = (x(u,v), y(u,v))$。

- **第一列**: $\begin{pmatrix} \frac{\partial x}{\partial u} \\ \frac{\partial y}{\partial u} \end{pmatrix}$。这是当 $v$ 保持不变时，位置向量 $(x,y)$ 随 $u$ 变化的速率。因此，它是在 $(x,y)$ 平面中，由 $u$-坐标线（即 $v = \text{const}$）的像所形成的曲线的切向量。
- **第二列**: $\begin{pmatrix} \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial v} \end{pmatrix}$。同理，这是由 $v$-坐标线（即 $u = \text{const}$）的像所形成的曲线的[切向量](@entry_id:265494)。

因此，雅可比矩阵的列向量告诉我们输入空间中相互正交的网格线在变换后变成了什么方向的曲线，以及这些曲线的“伸展”程度。这揭示了变换如何扭曲和旋转空间。

例如，一个坐标变换 $x(u,v) = u \cosh(av)$, $y(u,v) = -u \sinh(av)$  将 $(u,v)$ 平面中的正交网格线 $u=u_0$ 和 $v=v_0$ 变换为 $(x,y)$ 平面中的两条曲线。在交点处，这两条曲线的[切向量](@entry_id:265494)恰好是[雅可比矩阵](@entry_id:264467)在 $(u_0, v_0)$ 点的两个列向量。通过计算这两个列向量的[点积](@entry_id:149019)，我们可以确定变换后的曲线是否仍然正交。对于这个特定的变换，可以证明变换后曲线之间的夹角 $\theta$ 满足 $\cos\theta = \tanh(2av_0)$。这表明，除非 $v_0=0$，否则原本正交的网格线在变换后将不再正交。

#### [雅可比矩阵](@entry_id:264467)的迹：[向量场的散度](@entry_id:136342)

当[雅可比矩阵](@entry_id:264467)是方阵时，其对角[线元](@entry_id:196833)素之和，即**迹 (trace)**，也具有重要的物理意义。对于一个向量场 $F: \mathbb{R}^n \to \mathbb{R}^n$，其[雅可比矩阵](@entry_id:264467)的迹定义为：
$$
\text{tr}(J_F) = \sum_{i=1}^n \frac{\partial F_i}{\partial x_i}
$$
这与向量微积分中**散度 (divergence)** 的定义完全相同：
$$
\nabla \cdot F = \frac{\partial F_1}{\partial x_1} + \frac{\partial F_2}{\partial x_2} + \dots + \frac{\partial F_n}{\partial x_n}
$$
因此，**向量场的雅可比矩阵的迹就是该[向量场的散度](@entry_id:136342)**。散度衡量了向量场在某一点的源或汇的强度，即流体从该点流出（扩张）或流入（压缩）的倾向。例如，一个描述旋转和膨胀气体云的速度场 $\mathbf{v}(x, y, z) = \langle \alpha x - \omega y, \omega x + \alpha y, \beta z \rangle$ ，其[雅可比矩阵](@entry_id:264467)为：
$$
J = \begin{pmatrix} \alpha  -\omega  0 \\ \omega  \alpha  0 \\ 0  0  \beta \end{pmatrix}
$$
其迹为 $\text{tr}(J) = \alpha + \alpha + \beta = 2\alpha + \beta$。同时，其散度为 $\nabla \cdot \mathbf{v} = \frac{\partial}{\partial x}(\alpha x - \omega y) + \frac{\partial}{\partial y}(\omega x + \alpha y) + \frac{\partial}{\partial z}(\beta z) = \alpha + \alpha + \beta = 2\alpha + \beta$。两者完全相等，都量化了气体云的局部膨胀率。

### 基本性质及其在分析中的应用

[雅可比矩阵](@entry_id:264467)遵循一些类似于单变量导数的重要规则，这些规则在理论分析和实际应用中都至关重要。

#### [雅可比矩阵](@entry_id:264467)的链式法则

与单变量微积分中的[链式法则](@entry_id:190743) $(g(f(x)))' = g'(f(x))f'(x)$ 相对应，[向量值函数](@entry_id:261164)复合的导数由雅可比矩阵的乘积给出。如果 $f: \mathbb{R}^n \to \mathbb{R}^m$ 和 $g: \mathbb{R}^m \to \mathbb{R}^p$ 是[可微函数](@entry_id:144590)，那么它们的[复合函数](@entry_id:147347) $h = g \circ f: \mathbb{R}^n \to \mathbb{R}^p$ 的雅可比矩阵为：
$$
J_h(\mathbf{x}) = J_g(f(\mathbf{x})) \cdot J_f(\mathbf{x})
$$
这里，乘法是标准的矩阵乘法。$J_f(\mathbf{x})$ 是一个 $m \times n$ 矩阵，$J_g(f(\mathbf{x}))$ 是一个 $p \times m$ 矩阵，它们的乘积 $J_h(\mathbf{x})$ 是一个 $p \times n$ 矩阵，这与 $h$ 的映射维度完全一致。这个法则表明，复合映射的[局部线性近似](@entry_id:263289)等于各个映射的[局部线性近似](@entry_id:263289)的复合。

例如，给定 $f: \mathbb{R}^2 \to \mathbb{R}^3$ 和 $g: \mathbb{R}^3 \to \mathbb{R}^2$，我们可以通过计算 $J_f$ 和 $J_g$ 并将它们相乘来求得 $h = g \circ f$ 的[雅可比矩阵](@entry_id:264467) $J_h$ 。这个过程比直接计算 $h$ 的表达式再求导要系统得多，尤其是在函数复杂时。

#### [反函数](@entry_id:141256)的[雅可比矩阵](@entry_id:264467)

[链式法则](@entry_id:190743)是推导[反函数导数](@entry_id:266277)公式的有力工具。考虑一个可逆的、可微的函数 $f: \mathbb{R}^n \to \mathbb{R}^n$ 及其反函数 $f^{-1}$。我们有恒等关系 $f^{-1}(f(\mathbf{x})) = \mathbf{x}$。对这个恒等式两边关于 $\mathbf{x}$ 求雅可比矩阵，并应用链式法则：
$$
J_{f^{-1}}(f(\mathbf{x})) \cdot J_f(\mathbf{x}) = J_{\text{id}}(\mathbf{x}) = I
$$
其中 $I$ 是 $n \times n$ 的[单位矩阵](@entry_id:156724)。只要 $J_f(\mathbf{x})$ 是可逆的（即[雅可比行列式](@entry_id:137120)非零），我们就可以得到[反函数](@entry_id:141256)雅可比矩阵的公式：
$$
J_{f^{-1}}(f(\mathbf{x})) = [J_f(\mathbf{x})]^{-1}
$$
令 $\mathbf{y} = f(\mathbf{x})$，则 $\mathbf{x} = f^{-1}(\mathbf{y})$。上述公式可以写为：
$$
J_{f^{-1}}(\mathbf{y}) = [J_f(f^{-1}(\mathbf{y}))]^{-1}
$$
这说明，[反函数](@entry_id:141256)在点 $\mathbf{y}$ 的[雅可比矩阵](@entry_id:264467)，是原函数在对应点 $\mathbf{x}$ 的[雅可比矩阵](@entry_id:264467)的逆矩阵。这个结论在[坐标变换](@entry_id:172727)和理论推导中非常有用。例如，要找到一个变换 $f(u,v) = (u+v^2, v+u^2)$ 的反函数在点 $(x,y)=(3,5)$ 处的雅可比矩阵 ，我们首先需要找到对应的 $(u,v)$ 点，即解[方程组](@entry_id:193238)得到 $(u,v)=(2,1)$。然后计算 $f$ 在 $(2,1)$ 的[雅可比矩阵](@entry_id:264467) $J_f(2,1) = \begin{pmatrix} 1  2 \\ 4  1 \end{pmatrix}$。最后，通过求该矩阵的逆，我们便能得到 $J_{f^{-1}}(3,5) = [J_f(2,1)]^{-1} = \frac{1}{-7} \begin{pmatrix} 1  -2 \\ -4  1 \end{pmatrix}$。

#### 雅可比矩阵在数值方法中的应用

[雅可比矩阵](@entry_id:264467)在科学计算中扮演着核心角色，特别是在[求解非线性方程](@entry_id:177343)组时。考虑一个形如 $F(\mathbf{x}) = \mathbf{0}$ 的[方程组](@entry_id:193238)，其中 $F: \mathbb{R}^n \to \mathbb{R}^n$。**[牛顿法](@entry_id:140116) (Newton's method)** 是求解此类问题的标准迭代算法。其迭代公式为：
$$
\mathbf{x}_{k+1} = \mathbf{x}_k - [J_F(\mathbf{x}_k)]^{-1} F(\mathbf{x}_k)
$$
这个公式的本质是，在每一步中，用函数 $F$ 在当前点 $\mathbf{x}_k$ 的线性近似来代替原函数，然后求解这个[线性方程组](@entry_id:148943)来找到下一个近似解。从公式中可以看出，算法的每一步都要求解一个以[雅可比矩阵](@entry_id:264467)为系数矩阵的线性系统，这等价于计算[雅可比矩阵](@entry_id:264467)的逆。

因此，[雅可比矩阵](@entry_id:264467)的性质直接决定了牛顿法的性能。如果在一个解 $\mathbf{x}^*$ 附近，雅可比矩阵 $J_F(\mathbf{x}^*)$ 是**病态的 (ill-conditioned)**，即接近奇异（其[行列式](@entry_id:142978)接近于零），那么它的[逆矩阵](@entry_id:140380)的元素会非常大。这会导致数值计算上的不稳定性，使得迭代步长 $\Delta\mathbf{x}_k = - [J_F(\mathbf{x}_k)]^{-1} F(\mathbf{x}_k)$ 对 $F(\mathbf{x}_k)$ 中的微小误差极其敏感，从而可能导致算法收敛缓慢甚至发散。

我们可以通过分析雅可比矩阵的**条件数 (condition number)** 来量化这种病态程度 。一个大的条件数意味着矩阵接近奇异。考虑一个依赖于参数 $\epsilon$ 的系统，其解为 $(1,1)$。如果在该解处的雅可比矩阵的[行列式](@entry_id:142978)为 $-2\epsilon$，那么当 $\epsilon \to 0$ 时，矩阵的条件数 $\kappa_F(J)$ 将趋向于无穷大（具体表达式为 $\frac{\epsilon^2+2\epsilon+10}{2|\epsilon|}$）。这表明，对于接近零的 $\epsilon$ 值，用[牛顿法](@entry_id:140116)求解该系统将变得非常困难，这为我们选择或改进数值算法提供了重要的理论指导。