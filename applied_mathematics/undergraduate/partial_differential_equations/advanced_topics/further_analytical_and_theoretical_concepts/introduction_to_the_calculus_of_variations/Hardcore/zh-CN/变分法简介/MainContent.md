## 引言
变分法是数学分析的一个分支，它研究如何寻找使某个积分量（称为泛函）达到极值的函数。从最速降线问题到最小作用量原理，自然界和工程领域的许多基本法则都可以表述为优化问题：在所有可能的路径或形状中，哪一个能使能量最低、时间最短或距离最远？变分法为解答这类问题提供了强大的系统性工具，它所解决的知识鸿沟在于，如何从一个全局的“最优”原则，推导出描述系统局部行为的微分方程。

在本文中，我们将系统地探索变分法的世界。读者将学习到：

在“原理与机制”一章中，我们将推导变分法的基石——欧拉-拉格朗日方程，并将其推广至多变量、多函数以及带约束的复杂情况。
在“应用与跨学科联系”一章中，我们将展示变分原理如何统一地描述经典力学、场论、凝聚态物理乃至工程设计中的各种现象。
最后，在“动手实践”部分，你将有机会通过具体问题，应用所学知识来解决真实的物理和几何优化挑战。

让我们首先深入变分法的核心，理解其基本原理与机制。

## 原理与机制

在上一章中，我们介绍了变分法的基本思想，即在所有可能的函数中寻找使某个积分量（称为**泛函**）达到极值的函数。现在，我们将深入探讨变分法的核心原理和机制。本章将推导并应用其中心方程——**欧拉-拉格朗日方程** (Euler-Lagrange equation)，并将其推广到更复杂的物理和几何情境中，包括多变量、多函数以及带约束的系统。

### 欧拉-拉格朗日方程：变分法的基石

变分法的核心工具是欧拉-拉格朗日方程，它为泛函取极值提供了必要条件。考虑最简单的一类泛函，它依赖于一个单变量函数 $y(x)$ 及其一阶导数 $y'(x)$：
$$ J[y] = \int_{a}^{b} F(x, y(x), y'(x)) \, dx $$
其中 $y(x)$ 在端点 $a$ 和 $b$ 的值是固定的，即 $y(a) = y_a$ 和 $y(b) = y_b$。函数 $F$ 通常被称为**拉格朗日量** (Lagrangian)。变分法的目标是找到一条路径 $y(x)$，使得泛函 $J[y]$ 取得（局部）最小值或最大值。

通过考虑对最优路径 $y(x)$ 的任意微小扰动 $\delta y(x)$（在端点为零），并要求泛函 $J[y]$ 的一阶变分为零，可以推导出，任何使得 $J[y]$ 取极值的足够光滑的函数 $y(x)$ 都必须满足以下常微分方程：

$$ \frac{\partial F}{\partial y} - \frac{d}{dx}\left(\frac{\partial F}{\partial y'}\right) = 0 $$

这就是**欧拉-拉格朗日方程**。它将一个寻求函数极值的问题（变分问题）转化为了一个求解微分方程的问题。

为了具体理解其应用，让我们考虑一个物理模型。假设一层薄膜沉积在从 $x=0$ 到 $x=L$ 的基底上，其垂直位移由函数 $y(x)$ 描述。该薄膜的总势能由一个泛函给出，该泛函包含其内部的弹性势能和与基底的相互作用能。一个简化的模型是 [@problem_id:2114893]：
$$ \mathcal{E}[y] = \int_{0}^{L} \left( \frac{\kappa}{2} (y')^2 + V_0 \exp\left(-\frac{y}{h}\right) \right) dx $$
在这里，$\kappa, V_0, h$ 是正常数，分别代表薄膜的弯曲刚度、相互作用强度和相互作用的特征长度。系统将处于使其总势能最小化的平衡构型，该构型由欧拉-拉格朗日方程决定。

对于此系统，拉格朗日量为 $F(y, y') = \frac{\kappa}{2} (y')^2 + V_0 \exp\left(-\frac{y}{h}\right)$。我们计算其对 $y$ 和 $y'$ 的偏导数：

$$ \frac{\partial F}{\partial y} = V_0 \exp\left(-\frac{y}{h}\right) \cdot \left(-\frac{1}{h}\right) = -\frac{V_0}{h} \exp\left(-\frac{y}{h}\right) $$

$$ \frac{\partial F}{\partial y'} = \frac{\kappa}{2} \cdot (2y') = \kappa y' $$

将这些代入欧拉-拉格朗日方程：

$$ -\frac{V_0}{h} \exp\left(-\frac{y}{h}\right) - \frac{d}{dx}(\kappa y') = 0 $$

由于 $\kappa$ 是常数，$\frac{d}{dx}(\kappa y') = \kappa y''$。于是，我们得到描述薄膜平衡形状的二阶常微分方程：

$$ \kappa y'' = -\frac{V_0}{h} \exp\left(-\frac{y}{h}\right) $$

这个例子清晰地展示了如何将一个物理系统的能量最小化原理，通过欧拉-拉格朗日方程，转化为一个可以求解的微分方程。

### 贝尔特拉米等式：一个守恒律的特例

在某些情况下，拉格朗日量 $F$ 不显式地依赖于自变量 $x$，即 $\frac{\partial F}{\partial x} = 0$。在这种情况下，欧拉-拉格朗日方程存在一个**首次积分**，称为**贝尔特拉米等式** (Beltrami identity)：

$$ F - y' \frac{\partial F}{\partial y'} = C $$

其中 $C$ 是一个积分常数。这个恒等式在物理学中非常重要，它通常对应于一个**守恒定律**。例如，在经典力学中，如果拉格朗日量不显式依赖于时间，那么这个守恒量就是系统的总能量。

让我们看一个来自凝聚态物理的例子：描述一维超导体中正常态和超导态之间界面的金兹堡-朗道理论 (Ginzburg-Landau theory) [@problem_id:2114889]。系统的自由能由一个序参量 $\psi(x)$ 的泛函给出：
$$ F[\psi] = \int_{-\infty}^{\infty} \left( K \left(\frac{d\psi}{dx}\right)^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4 \right) dx $$
其中 $K, \alpha_0, \beta$ 是表征材料属性的正常数。描述物理构型的路径 $\psi(x)$ 是使该自由能泛函取极值的路径。

此处的拉格朗日量 $f(\psi, \psi') = K(\psi')^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4$ 不显式依赖于 $x$。因此，我们可以直接应用贝尔特拉米等式：
$$ \left( K(\psi')^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4 \right) - \psi' \frac{\partial}{\partial \psi'} \left( K(\psi')^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4 \right) = C $$
$$ \left( K(\psi')^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4 \right) - \psi' (2K\psi') = C $$
$$ -K(\psi')^2 - \alpha_0 \psi^2 + \frac{\beta}{2} \psi^4 = C $$
这个方程是原欧拉-拉格朗日方程（一个二阶ODE）的首次积分（一个一阶ODE），通常更容易求解。通过物理边界条件（例如，在无穷远处，系统处于均匀超导态，此时 $\psi'$ 趋于零，$\psi$ 趋于一个常数值），可以确定积分常数 $C$，从而得到梯度 $(\frac{d\psi}{dx})^2$ 与序参量 $\psi$ 本身之间的直接关系。这个例子展示了贝尔特라미等式作为求解变分问题的有力工具的价值。

### 多变量的推广：从函数到场

许多物理系统，如电磁场或弹性体的振动，不能用单变量函数描述，而需要用依赖于多个自变量（如空间坐标和时间）的**场** (field) 来描述，例如 $u(x, t)$ 或 $u(x, y)$。变分原理可以自然地推广到场论。

在这种情况下，我们考虑一个作用量积分 $S$，它是**拉格朗日密度** (Lagrangian density) $\mathcal{L}$ 在时空区域上的积分。例如，对于一个依赖于两个自变量 $x, t$ 的场 $u(x, t)$，作用量为：
$$ S[u] = \iint \mathcal{L}(u, u_t, u_x) \, dx \, dt $$
其中 $u_t = \frac{\partial u}{\partial t}$，$u_x = \frac{\partial u}{\partial x}$。

相应的欧拉-拉格朗日方程需要对每个自变量求导，形式如下：
$$ \frac{\partial \mathcal{L}}{\partial u} - \frac{\partial}{\partial t}\left(\frac{\partial \mathcal{L}}{\partial u_t}\right) - \frac{\partial}{\partial x}\left(\frac{\partial \mathcal{L}}{\partial u_x}\right) = 0 $$
这个方程是**场论的欧拉-拉格朗日方程**，它产生的是一个**偏微分方程** (PDE)。

物理学中最基本的PDE之一——**一维波动方程**——就可以通过这个原理导出。为了理解其拉格朗日密度的物理来源，我们可以从一个离散系统出发：一个由质量为 $m$ 的质点和弹性系数为 $k$ 的弹簧构成的一维链条 [@problem_id:2114883]。在连续极限下（质点间距 $a \to 0$），这个离散系统的动力学方程可以转化为一个连续介质的波动方程，$\frac{\partial^2 u}{\partial t^2} = v^2 \frac{\partial^2 u}{\partial x^2}$，其中波速的平方 $v^2 = Y_E / \rho_0$，$\rho_0 = m/a$ 是线密度，$Y_E = ka$ 是杨氏模量。这个过程启发我们，连续介质的动能密度与 $u_t^2$ 成正比，势能密度与 $u_x^2$ 成正比。

因此，一个连续波导的拉格朗日密度可以写成动能密度减去势能密度的形式 [@problem_id:2114880]：
$$ \mathcal{L}(u_t, u_x) = \frac{1}{2}\rho u_t^2 - \frac{1}{2}T u_x^2 $$
这里 $\rho$ 是线质量密度，$T$ 是有效张力。让我们将此 $\mathcal{L}$ 代入场论的欧拉-拉格朗日方程。

首先，计算各偏导数：
$$ \frac{\partial \mathcal{L}}{\partial u} = 0 $$
$$ \frac{\partial \mathcal{L}}{\partial u_t} = \rho u_t $$
$$ \frac{\partial \mathcal{L}}{\partial u_x} = -T u_x $$

代入方程得到：
$$ 0 - \frac{\partial}{\partial t}(\rho u_t) - \frac{\partial}{\partial x}(-T u_x) = 0 $$
假设 $\rho$ 和 $T$ 是常数，这简化为：
$$ -\rho u_{tt} + T u_{xx} = 0 \quad \text{或} \quad u_{tt} = \frac{T}{\rho} u_{xx} $$
这正是标准的一维波动方程，其中波速的平方为 $v^2 = T/\rho$。这个推导是物理学中的一个经典范例，展示了作用量原理如何统一地描述物理定律。

### 多函数的推广：方程组与耦合系统

当一个系统需要由多个函数或场（例如，$u, v$）来描述时，变分原理同样适用。基本原则是：**每个函数（或场）都有其自己独立的欧拉-拉格朗日方程**。

如果一个系统的拉格朗日量 $L$ 依赖于两个函数 $u(x,y), v(x,y)$ 及其偏导数，那么描述该系统的方程组由以下两个欧拉-拉格朗日方程给出：
$$ \frac{\partial L}{\partial u} - \frac{\partial}{\partial x}\left(\frac{\partial L}{\partial u_x}\right) - \frac{\partial}{\partial y}\left(\frac{\partial L}{\partial u_y}\right) = 0 $$
$$ \frac{\partial L}{\partial v} - \frac{\partial}{\partial x}\left(\frac{\partial L}{\partial v_x}\right) - \frac{\partial}{\partial y}\left(\frac{\partial L}{\partial v_y}\right) = 0 $$

考虑一个由拉格朗日密度 $L = u_x v_y + u^2 - v^2$ 描述的两个标量场 $u(x,y)$ 和 $v(x,y)$ 相互作用的简化模型 [@problem_id:2114903]。我们来推导这个系统的场方程。

对于场 $u$：
$\frac{\partial L}{\partial u} = 2u$, $\frac{\partial L}{\partial u_x} = v_y$, $\frac{\partial L}{\partial u_y} = 0$。
其欧拉-拉格朗日方程为：
$2u - \frac{\partial}{\partial x}(v_y) - \frac{\partial}{\partial y}(0) = 0 \implies 2u - v_{xy} = 0$。

对于场 $v$：
$\frac{\partial L}{\partial v} = -2v$, $\frac{\partial L}{\partial v_x} = 0$, $\frac{\partial L}{\partial v_y} = u_x$。
其欧拉-拉格朗日方程为：
$-2v - \frac{\partial}{\partial x}(0) - \frac{\partial}{\partial y}(u_x) = 0 \implies -2v - u_{yx} = 0$。

假设函数足够光滑，混合偏导数相等 ($u_{yx} = u_{xy}$)，则该系统由以下耦合的PDE系统描述：
$$ 2u - v_{xy} = 0 $$
$$ -2v - u_{xy} = 0 $$

变分原理不仅能产生演化方程，还能产生**约束方程**。在一个关于两个标量场 $u(x,t)$ 和 $v(x,t)$ 的一维场论模型中，拉格朗日密度为 [@problem_id:2114915]：
$$ \mathcal{L} = \frac{1}{2}(u_t^2 - c^2 u_x^2) - u v_x $$
对 $u$ 应用欧拉-拉格朗日方程，我们得到一个带有源项的波动方程：$u_{tt} - c^2 u_{xx} = -v_x$。
然而，对 $v$ 应用欧拉-拉格朗日方程（注意到 $\mathcal{L}$ 不依赖于 $v$ 和 $v_t$）给出：
$0 - \frac{\partial}{\partial t}(0) - \frac{\partial}{\partial x}(-u) = 0 \implies u_x = 0$。
第二个方程是一个约束方程，它表明场 $u$ 在空间上必须是均匀的。这表明变分原理是一种强大的形式体系，能够在一个统一的框架内同时产生动力学演化和系统必须遵守的约束。

### 带约束的变分问题：拉格朗日乘子法

在许多实际问题中，我们需要在满足某些额外条件或**约束**的情况下，寻找一个泛函的极值。这类问题被称为**带约束的变分问题**。解决这类问题的标准方法是**拉格朗日乘子法** (method of Lagrange multipliers)。

#### 积分约束与等周问题

一类常见的约束是**积分约束**（或称等周约束），即要求另一个泛函的值固定。例如，我们要寻找使泛函 $J[y]$ 取极值的函数 $y(x)$，同时满足约束条件 $G[y] = \int_a^b K(x, y, y') dx = C$（常数）。

解决方法是引入一个常数 $\lambda$，称为**拉格朗日乘子**，并构造一个新的无约束泛函：
$$ H[y] = J[y] + \lambda G[y] = \int_a^b (F + \lambda K) \, dx $$
然后对这个新的泛函 $H[y]$ 应用标准的欧拉-拉格朗日方程。得到的解将依赖于 $\lambda$，而 $\lambda$ 的值最终由原始的积分约束条件 $G[y]=C$ 确定。

一个典型的例子是设计一根跨越 $(0,0)$ 和 $(L,0)$ 的柔性导线，其形状为 $y(x)$。为了散热，要求导线与x轴围成的面积固定为 $A$，即 $\int_0^L y(x) dx = A$。同时，为了结构稳定，需要最小化其应变能，近似为 $E[y] = \int_0^L (y')^2 dx$ [@problem_id:2114895]。

我们构造辅助泛函 $J[y] = \int_0^L ((y')^2 + \lambda y) dx$。这里的拉格朗日量为 $F(y, y') = (y')^2 + \lambda y$。欧拉-拉格朗日方程为：
$$ \frac{\partial F}{\partial y} - \frac{d}{dx}\left(\frac{\partial F}{\partial y'}\right) = \lambda - \frac{d}{dx}(2y') = 0 $$
这给出了一个简单的二阶ODE：$y'' = \lambda/2$。其通解为抛物线 $y(x) = \frac{\lambda}{4} x^2 + C_1 x + C_2$。利用边界条件 $y(0)=0, y(L)=0$ 和面积约束 $\int_0^L y(x) dx = A$，我们可以确定所有常数，最终得到导线的最佳形状为：
$$ y(x) = \frac{6A}{L^3}(Lx - x^2) $$

这个方法可以推广到更高维度。例如，考虑一个固定体积的液滴在疏水表面上的形状 [@problem_id:2114887]。液滴的表面张力使其趋向于最小化表面积，同时其体积保持不变。这对应于最小化表面积泛函 $A[u] = \iint \sqrt{1 + u_x^2 + u_y^2} \, dx dy$，约束条件为体积泛函 $V[u] = \iint u \, dx dy = V_0$。

引入拉格朗日乘子 $\lambda$ 并最小化 $J[u] = A[u] - \lambda V[u]$。对应的欧拉-拉格朗日方程是：
$$ \nabla \cdot \left( \frac{\nabla u}{\sqrt{1 + |\nabla u|^2}} \right) = -\lambda $$
方程的左侧正好是曲面平均曲率 $H$ 的两倍。因此，我们得到 $2H = -\lambda$，或 $H = -\lambda/2$。这揭示了一个深刻的几何事实：在没有重力的情况下，一个固定体积的液滴其表面必然具有**恒定的平均曲率**。球面和圆柱面就是这样的例子。

#### 归一化约束与本征值问题

另一类重要的约束问题出现在量子力学和振动理论中，它将变分法与线性代数中的**本征值问题** (eigenvalue problem) 联系起来。

考虑一个在区域 $D$ 上定义的弹性薄膜，其边缘固定 ($u=0$ on $\partial D$)。其振动构型对应于狄利克雷能量泛函 $J[u] = \iint_D |\nabla u|^2 \, dA$ 的平稳点，但必须满足归一化条件 $\iint_D u^2 \, dA = 1$ [@problem_id:2114910]。这个约束确保了我们寻找的是非平凡解。

使用拉格朗日乘子法，我们寻求泛函 $H[u] = \iint_D (|\nabla u|^2 - \lambda u^2) \, dA$ 的极值。该泛函的拉格朗日密度为 $L = |\nabla u|^2 - \lambda u^2 = u_x^2 + u_y^2 - \lambda u^2$。其欧拉-拉格朗日方程为：
$$ \frac{\partial L}{\partial u} - \frac{\partial}{\partial x}\left(\frac{\partial L}{\partial u_x}\right) - \frac{\partial}{\partial y}\left(\frac{\partial L}{\partial u_y}\right) = 0 $$
$$ -2\lambda u - \frac{\partial}{\partial x}(2u_x) - \frac{\partial}{\partial y}(2u_y) = 0 $$
$$ -2\lambda u - 2(u_{xx} + u_{yy}) = 0 $$
这可以整理为：
$$ -\Delta u = \lambda u $$
其中 $\Delta = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$ 是拉普拉斯算子。

这个结果意义非凡。它表明，使狄利克雷能量在归一化约束下取极值的函数，正是拉普拉斯算子的**本征函数** (eigenfunction)，而拉格朗日乘子 $\lambda$ 就是对应的**本征值** (eigenvalue)。在物理上，这些本征函数对应于系统的基本振动模式（驻波），而本征值则与这些模式的振动频率的平方相关。例如，对于一个矩形薄膜 $D = [0, L_x] \times [0, L_y]$，其最低能量的本征函数为 $u_1(x, y) = C \sin(\frac{\pi x}{L_x}) \sin(\frac{\pi y}{L_y})$，通过直接代入，我们可以发现其对应的本征值为 $\lambda_1 = \pi^2(\frac{1}{L_x^2} + \frac{1}{L_y^2})$。

总之，欧拉-拉格朗日方程及其推广是连接物理原理与数学方程的桥梁。从简单的力学问题到复杂的场论和几何问题，变分原理提供了一个统一而深刻的视角来理解自然界的规律。