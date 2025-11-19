## 引言
在探索弯曲空间和[流形](@entry_id:153038)的几何学时，[联络系数](@entry_id:157618)是定义协变导数、描述矢量如何在空间中“平行”移动的核心工具。它们量化了[基矢](@entry_id:199546)从一点到另一点的微小变化，构成了微分几何的基石。然而，一个根本性的问题随之产生：这个描述几何变化的关键量——[联络系数](@entry_id:157618)——本身是否遵循张量所特有的、优雅的坐标变换法则？对这个问题的解答，不仅是[张量分析](@entry_id:161423)中的一个关键技术细节，更揭示了[引力](@entry_id:175476)、惯性与空间几何之间深刻的内在联系。

本文旨在系统性地剖析[联络系数](@entry_id:157618)的变换定律。我们将首先在“原理与机制”一章中，通过严谨的数学推导，揭示其非张量性的本质，并阐明其变换法则中非齐次项的几何来源。接着，在“应用与跨学科联系”一章，我们将探讨这一定律如何在广义相对论、[非惯性参考系](@entry_id:169712)和内禀曲率等概念中发挥核心作用，将抽象的数学与具体的物理世界联系起来。最后，通过“动手实践”部分提供的计算练习，读者将有机会亲手验证这些原理，从而将理论知识内化为解决实际问题的能力。通过这一系列的学习，读者将深刻理解为何[联络系数](@entry_id:157618)以其独特的方式变换，以及这一特性如何成为现代物理学和几何学的基础。

## 原理与机制

在前一章中，我们引入了[联络系数](@entry_id:157618)作为在[流形](@entry_id:153038)上定义协变导数的关键工具，它量化了[基矢](@entry_id:199546)从一点到另一点的变化。一个自然而然的问题是：[联络系数](@entry_id:157618)本身是否构成一个张量？本章将深入探讨[联络系数](@entry_id:157618)的变换定律，揭示其非张量性的本质，并阐明这一定律背后深刻的几何与物理原理。

### [联络系数](@entry_id:157618)的变换定律

为了判断一个量是否为张量，我们必须检验其在[坐标变换](@entry_id:172727)下的行为。让我们首先回忆一个(1,2)型张量 $T^k_{ij}$ 的变换法则。若从一个[坐标系](@entry_id:156346) $\{x^p\}$ 变换到另一个[坐标系](@entry_id:156346) $\{x'^k\}$，其分量变换如下：
$$
T'^{k}_{ij} = \frac{\partial x'^{k}}{\partial x^p} \frac{\partial x^q}{\partial x'^{i}} \frac{\partial x^r}{\partial x'^{j}} T^p_{qr}
$$
这是一个齐次、线性的变换关系，其中只涉及[坐标变换](@entry_id:172727)的一阶偏导数（雅可比矩阵的元素）。

然而，[联络系数](@entry_id:157618) $\Gamma^k_{ij}$ 的变换法则却有所不同。对于一个[仿射联络](@entry_id:160152)，其分量的变换规律由下式给出：
$$
\Gamma'^{k}_{ij} = \frac{\partial x'^{k}}{\partial x^p} \frac{\partial x^q}{\partial x'^{i}} \frac{\partial x^r}{\partial x'^{j}} \Gamma^p_{qr} + \frac{\partial x'^{k}}{\partial x^p} \frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}
$$
仔细观察这个表达式，我们可以发现它由两部分组成。第一部分与张量的变换法则形式完全相同，我们称之为**齐次项**或**张量性部分**。第二部分，$\frac{\partial x'^{k}}{\partial x^p} \frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}$，是一个仅依赖于坐标变换本身的附加项，它包含坐标变换的[二阶偏导数](@entry_id:635213)。这个项被称为**非齐次项**或**非张量性部分**。

正是这个非齐次项的存在，使得[联络系数](@entry_id:157618)的变换行为与张量截然不同。一个直接的推论是，即使在一个[坐标系](@entry_id:156346)中所有[联络系数](@entry_id:157618)分量均为零，在另一个[坐标系](@entry_id:156346)中它们也可能非零。

为了更清晰地说明这一点，让我们考虑一个平直的二维[欧氏空间](@entry_id:138052)。在标准的笛卡尔坐标系 $(x, y)$ 中，[度规张量](@entry_id:160222)是常数（[单位矩阵](@entry_id:156724)），因此所有克氏符（Christoffel symbols）$\Gamma^k_{ij}$ 均为零。现在，我们引入一个新的[抛物线坐标](@entry_id:166304)系 $(u, v)$，其变换关系为 $x = \frac{1}{2}(u^2 - v^2)$ 和 $y = uv$。[@problem_id:1561013]

考虑一个在[笛卡尔坐标系](@entry_id:169789)中所有分量均为零的(1,2)型[张量场](@entry_id:190170) $T^k_{ij}$。根据[张量变换定律](@entry_id:185176)，它在任何其他[坐标系](@entry_id:156346)（包括这个[抛物线坐标](@entry_id:166304)系）中的分量也必定为零，即 $T'^{k}_{ij} = 0$。然而，[联络系数](@entry_id:157618)的情况却大相径庭。由于在原[坐标系](@entry_id:156346)中 $\Gamma^p_{qr}=0$，$\Gamma'$ 的变换法则简化为只剩下非齐次项：
$$
\Gamma'^{k}_{ij} = \frac{\partial x'^{k}}{\partial x^p} \frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}
$$
通过计算，我们可以求得在 $(u, v)$ [坐标系](@entry_id:156346)下的一个[联络系数](@entry_id:157618)分量，例如 $\Gamma'^{u}_{vv}$（在索引表示中为 $\Gamma'^{1}_{22}$）。经过一番推导，我们发现：
$$
\Gamma'^{1}_{22} = -\frac{u}{u^2+v^2}
$$
这个结果显然不为零。因此，$\Gamma'^{k}_{ij}$ 与 $T'^{k}_{ij}$ 的差值 $D'^{k}_{ij} = \Gamma'^{k}_{ij} - T'^{k}_{ij}$ 在新[坐标系](@entry_id:156346)中不为零，这无可辩驳地证明了[联络系数](@entry_id:157618) $\Gamma^k_{ij}$ 并不是张量的分量。

### 非零[联络系数](@entry_id:157618)的几何根源

我们已经看到，从[笛卡尔坐标系](@entry_id:169789)变换到[曲线坐标系](@entry_id:172561)可以产生非零的[联络系数](@entry_id:157618)。这背后的几何图像是什么呢？其根源在于[曲线坐标系](@entry_id:172561)的**[基矢](@entry_id:199546)本身是空间位置的函数**。在[笛卡尔坐标系](@entry_id:169789)中，[基矢](@entry_id:199546) $\mathbf{e}_x, \mathbf{e}_y$ 在空间中每一点都指向相同的方向。然而，在[曲线坐标系](@entry_id:172561)中，例如极[坐标系](@entry_id:156346) $(r, \theta)$，[基矢](@entry_id:199546) $\mathbf{e}_r, \mathbf{e}_\theta$ 的方向是随点的位置而变化的。[联络系数](@entry_id:157618)恰恰就是量化这种[基矢](@entry_id:199546)变化的数学工具。

变换法则中的非齐次项 $\frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}$ 精确地捕捉了旧[坐标系](@entry_id:156346)[基矢](@entry_id:199546)相对于新[坐标系](@entry_id:156346)的变化率。让我们以从笛卡尔坐标 $(x,y)$ 到极坐标 $(r, \theta)$ 的变换为例。变换关系为 $x = r \cos\theta, y = r \sin\theta$。在[笛卡尔坐标系](@entry_id:169789)中 $\Gamma^k_{ij} = 0$。我们来考察极[坐标系](@entry_id:156346)中的克氏符 $\tilde{\Gamma}^r_{\theta\theta}$。根据简化的变换法则：
$$
\tilde{\Gamma}^r_{\theta\theta} = \frac{\partial r}{\partial x} \frac{\partial^2 x}{\partial \theta^2} + \frac{\partial r}{\partial y} \frac{\partial^2 y}{\partial \theta^2}
$$
要使 $\tilde{\Gamma}^r_{\theta\theta}$ 非零，求和式中至少要有一项非零。我们来计算这些[二阶导数](@entry_id:144508)：
$$
\frac{\partial x}{\partial \theta} = -r \sin\theta \implies \frac{\partial^2 x}{\partial \theta^2} = -r \cos\theta
$$
$$
\frac{\partial y}{\partial \theta} = r \cos\theta \implies \frac{\partial^2 y}{\partial \theta^2} = -r \sin\theta
$$
显然，$\frac{\partial^2 x}{\partial \theta^2}$ 和 $\frac{\partial^2 y}{\partial \theta^2}$ 都不为零 [@problem_id:1561065]。正是这些非零的[二阶导数](@entry_id:144508)导致了即使在[平直空间](@entry_id:204618)中，只要使用[曲线坐标](@entry_id:178535)，就会出现非零的[联络系数](@entry_id:157618)。将所有项代入，我们可以计算出 $\tilde{\Gamma}^r_{\theta\theta} = -r$ [@problem_id:1500350]。

这个结果说明，当你沿着半径为 $r$ 的圆周移动时（即只改变 $\theta$），径向[基矢](@entry_id:199546) $\mathbf{e}_r$ 的方向会发生改变，这种改变的“加速度”效应（由[二阶导数](@entry_id:144508)体现）就被克氏符 $\tilde{\Gamma}^r_{\theta\theta}$ 所捕捉。

计算新[坐标系](@entry_id:156346)中[联络系数](@entry_id:157618)主要有两种方法：
1.  **直接使用变换法则**：如上所述，如果已知原[坐标系](@entry_id:156346)的 $\Gamma$ 和坐标变换函数，可以直接代入公式计算。例如，对于从[笛卡尔坐标系](@entry_id:169789)到 $x=u^2-v^2, y=2uv$ [坐标系](@entry_id:156346)的变换，直接使用变换法则可以求得 $\bar{\Gamma}^u_{vv} = -\frac{u}{u^2+v^2}$ [@problem_id:1561030]。
2.  **通过度规张量计算**：首先，将原[坐标系](@entry_id:156346)的[度规张量](@entry_id:160222) $g_{ij}$ 变换到新[坐标系](@entry_id:156346)，得到 $g'_{ij}$。然后，利用克氏符和度规的关系式进行计算：
    $$
    \Gamma'^{k}_{ij} = \frac{1}{2} g'^{kl} \left( \frac{\partial g'_{jl}}{\partial x'^i} + \frac{\partial g'_{il}}{\partial x'^j} - \frac{\partial g'_{ij}}{\partial x'^l} \right)
    $$
    例如，对于 $x = \frac{1}{2}(u^2 - v^2), y=uv$ 的变换，可以先求出 $(u,v)$ 系下的度规为 $ds^2 = (u^2+v^2)du^2 + (u^2+v^2)dv^2$，然后用上述公式计算得到 $\tilde{\Gamma}^u_{uv} = \frac{v}{u^2+v^2}$ [@problem_id:1561032]。

这两种方法殊途同归，其结果都源于[坐标系](@entry_id:156346)的[非线性](@entry_id:637147)特性。

### 变换定律的深刻推论

[联络系数](@entry_id:157618)的变换定律虽然复杂，但它引出了一系列重要而深刻的结论。

#### 构建真正的张量

尽管[联络系数](@entry_id:157618)本身不是张量，但我们可以利用它来构造真正的张量。关键在于变换法则中的非张量性部分 $\frac{\partial x'^{k}}{\partial x^p} \frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}$ 并不依赖于联络本身，而只依赖于[坐标变换](@entry_id:172727)。

**1. 两个联络之差是张量**

假设在同一个[流形](@entry_id:153038)上定义了两个不同的[仿射联络](@entry_id:160152) $\Gamma^k_{ij}$ 和 $\hat{\Gamma}^k_{ij}$。它们各自的变换法则是：
$$
\Gamma'^{k}_{ij} = (\text{齐次项})_\Gamma + (\text{非齐次项})
$$
$$
\hat{\Gamma}'^{k}_{ij} = (\text{齐次项})_{\hat{\Gamma}} + (\text{非齐次项})
$$
由于非齐次项只与[坐标变换](@entry_id:172727)有关，所以对两个联络来说是完全相同的。定义一个新量 $T^k_{ij} = \Gamma^k_{ij} - \hat{\Gamma}^k_{ij}$，它在新[坐标系](@entry_id:156346)中的分量为：
$$
T'^{k}_{ij} = \Gamma'^{k}_{ij} - \hat{\Gamma}'^{k}_{ij} = [(\text{齐次项})_\Gamma - (\text{齐次项})_{\hat{\Gamma}}] + [(\text{非齐次项}) - (\text{非齐次项})]
$$
非齐次项相互抵消，只剩下齐次项的差，这正好满足(1,2)型张量的变换规律。因此，**两个联络之差是一个张量**。[@problem_id:1560994]

**2. [挠率张量](@entry_id:204137)**

另一个重要的例子是**[挠率张量](@entry_id:204137)**（Torsion Tensor），其分量定义为 $T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji}$，即[联络系数](@entry_id:157618)关于下标记的反对称部分。让我们看看它如何变换：
$$
T'^{k}_{ij} = \Gamma'^{k}_{ij} - \Gamma'^{k}_{ji}
$$
将 $\Gamma'$ 的变换法则代入，我们发现非齐次项 $\frac{\partial x'^{k}}{\partial x^p} \frac{\partial^2 x^p}{\partial x'^{i} \partial x'^{j}}$ 关于下标 $i, j$ 是对称的（假设坐标函数足够光滑，混合偏导的次序可以交换）。因此，在相减时，非齐次项同样被消除了。
$$
T'^{k}_{ij} = \frac{\partial x'^{k}}{\partial x^p} \frac{\partial x^q}{\partial x'^{i}} \frac{\partial x^r}{\partial x'^{j}} T^p_{qr}
$$
这表明挠率是一个(1,2)型张量。我们可以利用这一性质来计算它在不同[坐标系](@entry_id:156346)下的分量 [@problem_id:1561060]。如果一个联络是对称的，即 $\Gamma^k_{ij} = \Gamma^k_{ji}$（如黎曼几何中由度规诱导的Levi-Civita联络），则其[挠率张量](@entry_id:204137)恒为零。

#### [局域惯性系](@entry_id:198325)的存在性

[联络系数](@entry_id:157618)变换法则最重要的推论之一，便是**[局域惯性系](@entry_id:198325)**（Local Inertial Frame）的存在性。在牛顿物理中，[惯性力](@entry_id:169104)（如离心力、科里奥利力）是由于选择了[非惯性参考系](@entry_id:169712)而出现的“虚拟”力。通过切换到合适的惯性参考系，这些力就会消失。广义相对论中的[引力](@entry_id:175476)在某种意义上与此类似。[联络系数](@entry_id:157618)在几何上扮演了“[惯性力](@entry_id:169104)”或“[引力场](@entry_id:169425)强度”的角色。变换定律告诉我们，我们总能通过一个局域的[坐标变换](@entry_id:172727)，使得在某一点 $P$ 上的所有[联络系数](@entry_id:157618)都为零。

让我们来证明这一点。假设在点 $P$，原[坐标系](@entry_id:156346) $\{x^k\}$ 中的[联络系数](@entry_id:157618)为 $\Gamma^k_{ij}(P)$。我们希望找到一个新[坐标系](@entry_id:156346) $\{x'^\alpha\}$，使得在新[坐标系](@entry_id:156346)的原点 $P$ 处，[联络系数](@entry_id:157618)为零，即 $\tilde{\Gamma}^\gamma_{\alpha\beta}(P)=0$。
变换法则可以反过来写：
$$
\Gamma^k_{ij} = \frac{\partial x^k}{\partial x'^\gamma} \frac{\partial x'^\alpha}{\partial x^i} \frac{\partial x'^\beta}{\partial x^j} \tilde{\Gamma}^\gamma_{\alpha\beta} - \frac{\partial x^k}{\partial x'^\gamma} \frac{\partial^2 x'^\gamma}{\partial x^i \partial x^j}
$$
在点 $P$，我们要求 $\tilde{\Gamma}^\gamma_{\alpha\beta}(P)=0$。同时，我们可以选择[坐标变换](@entry_id:172727)，使其在 $P$ 点的雅可比矩阵为单位阵，即 $\frac{\partial x^k}{\partial x'^\gamma}|_P = \delta^k_\gamma$ 和 $\frac{\partial x'^\alpha}{\partial x^i}|_P = \delta^\alpha_i$。在这种选择下，上式在点 $P$ 处简化为：
$$
\Gamma^k_{ij}(P) = - \frac{\partial^2 x'^k}{\partial x^i \partial x^j}\bigg|_P
$$
或者等价地：
$$
\frac{\partial^2 x'^k}{\partial x^i \partial x^j}\bigg|_P = -\Gamma^k_{ij}(P)
$$
这个方程表明，只要我们能找到一个坐标变换 $x' = f(x)$，其在点 $P$ 处的[一阶导数](@entry_id:749425)是单位阵，且[二阶导数](@entry_id:144508)满足上述条件，我们就能在该点实现 $\tilde{\Gamma}(P)=0$。[泰勒展开](@entry_id:145057)定理保证了这样的[光滑函数](@entry_id:267124)总是存在的。这揭示了一个深刻的物理事实：[引力场](@entry_id:169425)在任何一点都可以在局部被“消除”，这正是爱因斯坦**等效原理**的数学表述。[@problem_id:1535641]

我们甚至可以构造出实现这一目标的坐标变换的[二阶近似](@entry_id:141277)。考虑从新[坐标系](@entry_id:156346) $\{x'\}$ 到旧[坐标系](@entry_id:156346) $\{x\}$ 的变换，在点 $P$（两个[坐标系](@entry_id:156346)的原点）附近展开：
$$
x^k(x') = (\frac{\partial x^k}{\partial x'^\alpha})_P x'^\alpha + \frac{1}{2} (\frac{\partial^2 x^k}{\partial x'^\alpha \partial x'^\beta})_P x'^\alpha x'^\beta + \dots
$$
选择 $(\frac{\partial x^k}{\partial x'^\alpha})_P = \delta^k_\alpha$，并利用变换法则，可以证明，为了使 $\tilde{\Gamma}(P)=0$，我们必须有 $(\frac{\partial^2 x^k}{\partial x'^\alpha \partial x'^\beta})_P = - \Gamma^k_{\alpha\beta}(P)$。因此，所需的[坐标变换](@entry_id:172727)近似为：
$$
x^k(x') = x'^k - \frac{1}{2} (\Gamma^k_{\alpha\beta})_P x'^\alpha x'^\beta + O((x')^3)
$$
这明确地给出了建立[局域惯性系](@entry_id:198325)的坐标变换形式，其中常数因子 $A = -1/2$ 是由变换法则唯一确定的 [@problem_id:1561036]。

### 总结

本章深入剖析了[联络系数](@entry_id:157618)的坐标变换定律。我们确立了以下核心原理与机制：

1.  **非张量性**：[联络系数](@entry_id:157618)的变换法则包含一个非齐次的、依赖于[坐标变换](@entry_id:172727)[二阶导数](@entry_id:144508)的附加项，这使得它不是一个张量。
2.  **几何意义**：非齐次项反映了[曲线坐标系](@entry_id:172561)中[基矢](@entry_id:199546)随位置变化的效应。因此，即使在[平直空间](@entry_id:204618)中，采用[曲线坐标](@entry_id:178535)也会导致非零的[联络系数](@entry_id:157618)。
3.  **构造张量**：尽管[联络系数](@entry_id:157618)本身非张量，但两个联络之差以及联络的反对称部分（挠率）都是真正的张量，因为在构造过程中非齐次项被抵消了。
4.  **等效原理**：变换法则保证了我们总可以在任意一点 $P$ 找到一个局域[坐标系](@entry_id:156346)（[局域惯性系](@entry_id:198325)），使得在该点的所有[联络系数](@entry_id:157618)均为零。这为[引力](@entry_id:175476)的几何描述奠定了基础。

对[联络系数](@entry_id:157618)变换定律的理解，是从[张量分析](@entry_id:161423)的计算层面，迈向微分几何的深刻思想层面的关键一步。它不仅解释了为什么需要[协变导数](@entry_id:152476)，也揭示了空间几何结构与物理定律之间的内在联系。