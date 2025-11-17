## 引言
在物理学和工程学的广阔天地中，[坐标系](@entry_id:156346)不仅仅是为空间中的点贴上标签的静态网格，它们是理解和量化我们宇宙的几何与动态行为的基础性工具。从描述行星的[轨道](@entry_id:137151)到设计机器ンの动作，选择合适的[坐标系](@entry_id:156346)往往是解决问题的关键第一步。本文旨在深入探讨[坐标系](@entry_id:156346)背后的丰富数学结构，揭示其作为[张量分析](@entry_id:161423)基石的深刻意义。

我们将超越[笛卡尔坐标系](@entry_id:169789)的直观性，进入一个由[曲线坐标](@entry_id:178535)、变换规则和内蕴几何构成的更为普适的世界。本文旨在填补从基本坐标概念到高级张量应用的知识鸿沟，系统性地阐明为何我们需要像度规张量、协变导数和曲率这样的复杂工具，以及它们如何为描述弯曲空间和物理定律提供一个统一的语言。

在接下来的内容中，读者将踏上一段从基础到前沿的旅程。第一章**“原理与机制”**将奠定坚实的数学基础，从[坐标变换](@entry_id:172727)和雅可比矩阵出发，引入[协变与逆变](@entry_id:189600)[基矢](@entry_id:199546)量、度规张量，并最终探讨在曲[线空间](@entry_id:173313)中进行微积分所必需的[联络与曲率](@entry_id:158520)概念。第二章**“应用与跨学科联系”**将展示这些抽象原理如何在[机器人学](@entry_id:150623)、地理信息系统（GIS）、工程力学乃至广义相对论等不同领域中发挥其强大威力。最后，在**“动手实践”**部分，通过具体的计算问题，您将有机会亲手应用所学知识，巩固并深化理解。现在，让我们从构建这一强大框架的基石——坐标变换及其数学描述开始。

## 原理与机制

在本章中，我们将深入探讨[坐标系](@entry_id:156346)的数学框架，这是[张量分析](@entry_id:161423)的基石。我们将超越将[坐标系](@entry_id:156346)仅仅视为标记空间中点的方式，而是将其理解为定义和测量几何与物理量（如距离、角度、矢量和张量）的动态工具。我们的旅程将从坐标变换的基础开始，逐步引入协变和[逆变基](@entry_id:197906)矢量、[度规张量](@entry_id:160222)等核心概念，并最终探讨在这些[广义坐标](@entry_id:156576)系下进行微积分运算时出现的联络和曲率。

### 坐标变换与雅可比矩阵

描述物理空间最直观的方式是使用笛卡尔坐标系，其[基矢](@entry_id:199546)量是处处恒定且相互正交的。然而，许多物理问题具有特定的对称性（如球对称或[轴对称](@entry_id:173333)），使用能反映这些对称性的[曲线坐标系](@entry_id:172561)（如[球坐标](@entry_id:146054)或[柱坐标](@entry_id:271645)）会使问题大大简化。这就引出了在不同[坐标系](@entry_id:156346)之间进行转换的需求。

一个**坐标变换**是一个数学关系，它将一个[坐标系](@entry_id:156346)中的点 $(x^1, x^2, \dots, x^n)$ 映射到另一个[坐标系](@entry_id:156346)中的点 $(\bar{x}^1, \bar{x}^2, \dots, \bar{x}^n)$。这种关系通常由一组函数给出：$\bar{x}^j = \bar{x}^j(x^1, \dots, x^n)$。

在任意一[点的邻域](@entry_id:144055)内，这种变换可以被近似为线性的。描述这种[局部线性](@entry_id:266981)关系的正是**雅可比矩阵**。从旧[坐标系](@entry_id:156346) $x^i$ 到新[坐标系](@entry_id:156346) $\bar{x}^j$ 的[雅可比矩阵](@entry_id:264467) $J$ 定义为：
$J^j_i = \frac{\partial \bar{x}^j}{\partial x^i}$

反之，从新[坐标系](@entry_id:156346) $\bar{x}^j$ 到旧[坐标系](@entry_id:156346) $x^i$ 的变换也由一个雅可比矩阵描述：
$\bar{J}^i_j = \frac{\partial x^i}{\partial \bar{x}^j}$

根据链式法则，这两个矩阵互为逆矩阵，即 $J \bar{J} = I$，其中 $I$ 是[单位矩阵](@entry_id:156724)。

让我们考虑一个具体的例子：二维[欧几里得空间](@entry_id:138052)中从[笛卡尔坐标](@entry_id:167698) $(x, y)$ 到一个旋转了角度 $\alpha$ 的新笛卡尔坐标 $(x', y')$ 的变换 [@problem_id:1500056]。变换关系如下：
$x' = x \cos\alpha + y \sin\alpha$
$y' = -x \sin\alpha + y \cos\alpha$

我们的任务是求从新坐标 $(\bar{x}^1, \bar{x}^2) = (x', y')$ 到旧坐标 $(x^1, x^2) = (x, y)$ 的[雅可比矩阵](@entry_id:264467) $\bar{J}^i_j = \frac{\partial x^i}{\partial \bar{x}^j}$。为此，我们首先需要得到反向变换的表达式，即用 $(x', y')$ 表示 $(x, y)$。我们可以将上述[方程组](@entry_id:193238)视为一个[矩阵方程](@entry_id:203695)：
$\begin{pmatrix} x' \\ y' \end{pmatrix} = \begin{pmatrix} \cos\alpha  \sin\alpha \\ -\sin\alpha  \cos\alpha \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}$

由于[旋转矩阵](@entry_id:140302)是正交矩阵，其[逆矩阵](@entry_id:140380)等于其[转置](@entry_id:142115)。因此，我们可以立即写出反向变换：
$\begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} \cos\alpha  -\sin\alpha \\ \sin\alpha  \cos\alpha \end{pmatrix} \begin{pmatrix} x' \\ y' \end{pmatrix}$

即：
$x = x' \cos\alpha - y' \sin\alpha$
$y = x' \sin\alpha + y' \cos\alpha$

现在，我们可以计算[雅可比矩阵](@entry_id:264467)的各个分量：
$\frac{\partial x}{\partial x'} = \cos\alpha$, $\frac{\partial x}{\partial y'} = -\sin\alpha$
$\frac{\partial y}{\partial x'} = \sin\alpha$, $\frac{\partial y}{\partial y'} = \cos\alpha$

因此，所求的[雅可比矩阵](@entry_id:264467)为：
$\bar{J} = \begin{pmatrix} \frac{\partial x}{\partial x'}  \frac{\partial x}{\partial y'} \\ \frac{\partial y}{\partial x'}  \frac{\partial y}{\partial y'} \end{pmatrix} = \begin{pmatrix} \cos\alpha  -\sin\alpha \\ \sin\alpha  \cos\alpha \end{pmatrix}$

这个例子清晰地展示了雅可比矩阵在[坐标变换](@entry_id:172727)中的核心作用，它捕捉了坐标网格在变换下的局部拉伸和旋转。

### [协变基](@entry_id:198968)矢量与[逆变基](@entry_id:197906)矢量

在[笛卡尔坐标系](@entry_id:169789)中，[基矢](@entry_id:199546)量 $\hat{i}, \hat{j}$ 是恒定的。但在[曲线坐标系](@entry_id:172561)中，情况发生了根本性的变化。[基矢](@entry_id:199546)量的方向和大小都可能随空间位置而改变。这促使我们引入两种相互关联但概念上不同的[基矢](@entry_id:199546)量：[协变基](@entry_id:198968)矢量和[逆变基](@entry_id:197906)矢量。

**[协变基](@entry_id:198968)矢量**（Covariant Basis Vectors），记作 $\vec{g}_i$，被定义为位置矢量 $\vec{p}$ 沿坐标曲线 $x^i$ 的变化率。它们自然地与坐标曲线相切。
$\vec{g}_i = \frac{\partial \vec{p}}{\partial x^i}$

让我们以二维极[坐标系](@entry_id:156346) $(r, \theta)$ 为例 [@problem_id:1500086]。位置矢量 $\vec{p}$ 可以用笛卡尔[基矢](@entry_id:199546)量 $\hat{i}, \hat{j}$ 表示为 $\vec{p}(r, \theta) = x(r, \theta)\hat{i} + y(r, \theta)\hat{j} = r\cos\theta\,\hat{i} + r\sin\theta\,\hat{j}$。
根据定义，[协变基](@entry_id:198968)矢量为：
$\vec{g}_r = \frac{\partial \vec{p}}{\partial r} = \cos\theta\,\hat{i} + \sin\theta\,\hat{j}$
$\vec{g}_\theta = \frac{\partial \vec{p}}{\partial \theta} = -r\sin\theta\,\hat{i} + r\cos\theta\,\hat{j}$

$\vec{g}_r$ 是一个指向径向的单位矢量。然而，$\vec{g}_\theta$ 的大小（模）为 $|\vec{g}_\theta|^2 = \vec{g}_\theta \cdot \vec{g}_\theta = (-r\sin\theta)^2 + (r\cos\theta)^2 = r^2$。因此，$|\vec{g}_\theta| = r$。这表明，角向的[基矢](@entry_id:199546)量的大小取决于离原点的距离，这正是[曲线坐标系](@entry_id:172561)的一个典型特征。

与[协变基](@entry_id:198968)矢量相对应的是**[逆变基](@entry_id:197906)矢量**（Contravariant Basis Vectors），或称**对偶[基矢](@entry_id:199546)量**（Dual Basis Vectors），记作 $\vec{g}^j$。它们不是通过求导定义的，而是通过与[协变基](@entry_id:198968)矢量的代数关系来定义：
$\vec{g}^j \cdot \vec{g}_i = \delta^j_i$
其中 $\delta^j_i$ 是克罗内克（Kronecker）delta符号（当 $i=j$ 时为1，否则为0）。这个关系式表明，$\vec{g}^j$ 垂直于所有 $i \neq j$ 的[协变基](@entry_id:198968)矢量 $\vec{g}_i$。在一个[正交坐标](@entry_id:166074)系中（如极[坐标系](@entry_id:156346)），$\vec{g}^i$ 与 $\vec{g}_i$ 方向相同，但大小可能不同。

考虑一个简单的[线性缩放](@entry_id:197235)[坐标系](@entry_id:156346) $u=ax, v=by$ [@problem_id:1500052]。位置矢量为 $\vec{p}(u,v) = \frac{u}{a}\hat{i} + \frac{v}{b}\hat{j}$。
[协变基](@entry_id:198968)矢量为：
$\vec{e}_u = \frac{\partial \vec{p}}{\partial u} = \frac{1}{a}\hat{i}$, $\quad \vec{e}_v = \frac{\partial \vec{p}}{\partial v} = \frac{1}{b}\hat{j}$
它们的模的平方为 $|\vec{e}_u|^2 = \frac{1}{a^2}$ 和 $|\vec{e}_v|^2 = \frac{1}{b^2}$。

为了满足对偶关系 $\vec{e}^i \cdot \vec{e}_j = \delta^i_j$，我们可以推导出[逆变基](@entry_id:197906)矢量：
$\vec{e}^u = a\hat{i}$, $\quad \vec{e}^v = b\hat{j}$
它们的模的平方为 $|\vec{e}^u|^2 = a^2$ 和 $|\vec{e}^v|^2 = b^2$。这个例子清晰地展示了[协变基](@entry_id:198968)矢量的分量与坐标变换成反比（$1/a, 1/b$），而[逆变基](@entry_id:197906)矢量的分量与[坐标变换](@entry_id:172727)成正比（$a, b$）。

引入对偶[基矢](@entry_id:199546)量的巨大优势在于它简化了物理量的表示和运算。任何矢量 $\vec{A}$ 都可以用这两种[基矢](@entry_id:199546)量展开：
$\vec{A} = A^i \vec{g}_i = A_j \vec{g}^j$
其中 $A^i$ 称为**[逆变分量](@entry_id:185440)**，而 $A_j$ 称为**协变分量**。

对偶[基矢](@entry_id:199546)量的正交性使得计算两个矢量的[点积](@entry_id:149019)变得异常简洁。例如，考虑一个力矢量 $\vec{F}$ 和一个速度矢量 $\vec{v}$。我们可以将 $\vec{F}$ 用[逆变基](@entry_id:197906)矢量展开，将其速度 $\vec{v}$ 用[协变基](@entry_id:198968)矢量展开 [@problem_id:1500039]。
$\vec{F} = F_i \vec{g}^i$
$\vec{v} = v^j \vec{g}_j$
那么，力对物体做功的功率 $P = \vec{F} \cdot \vec{v}$ 就是：
$P = (F_i \vec{g}^i) \cdot (v^j \vec{g}_j) = F_i v^j (\vec{g}^i \cdot \vec{g}_j) = F_i v^j \delta^i_j = F_i v^i$
最终结果是[协变](@entry_id:634097)分量和[逆变分量](@entry_id:185440)的简单乘积求和，这在形式上与笛卡尔坐标系中的[点积](@entry_id:149019)完全一样，体现了[张量表示](@entry_id:180492)的优雅和普适性。

### 度规张量

空间的所有几何信息，如长度和角度，都蕴含在一个被称为**度规张量**（Metric Tensor）的核心对象中。度规张量将坐标差与物理距离联系起来。空间中两个无限接近的点之间的距离平方，即**[线元](@entry_id:196833)**（Line Element）$ds^2$，可以表示为：
$ds^2 = g_{ij} dx^i dx^j$
（这里我们采用了爱因斯坦求和约定，即对重复出现的上下标自动求和）。

这个表达式中的系数 $g_{ij}$ 构成了**[协变](@entry_id:634097)度规张量**。从定义可以看出，$g_{ij}$ 是一个[对称张量](@entry_id:148092)（$g_{ij}=g_{ji}$）。更深刻的是，协变度规张量的分量恰好是[协变基](@entry_id:198968)矢量的[点积](@entry_id:149019)：
$g_{ij} = \vec{g}_i \cdot \vec{g}_j$
这直接源于 $d\vec{p} = \frac{\partial \vec{p}}{\partial x^i} dx^i = \vec{g}_i dx^i$，所以 $ds^2 = d\vec{p} \cdot d\vec{p} = (\vec{g}_i dx^i) \cdot (\vec{g}_j dx^j) = (\vec{g}_i \cdot \vec{g}_j) dx^i dx^j$。

例如，对于一个由[线元](@entry_id:196833) $ds^2 = du^2 + \cosh^2(u) \, dv^2$ 定义的二维[曲面](@entry_id:267450) [@problem_id:1500082]，我们可以直接读出其协变度规张量的分量。令 $(x^1, x^2)=(u,v)$，则 $dx^1=du, dx^2=dv$。比较[线元](@entry_id:196833)表达式，我们得到：
$g_{uu} = 1$, $\quad g_{vv} = \cosh^2(u)$, $\quad g_{uv} = g_{vu} = 0$
以矩阵形式表示为：
$g_{ij} = \begin{pmatrix} 1  0 \\ 0  \cosh^2(u) \end{pmatrix}$

与协变度规张量相对应，**逆变[度规张量](@entry_id:160222)** $g^{ij}$ 定义为 $g_{ij}$ 的矩阵逆：
$g^{ik} g_{kj} = \delta^i_j$
同样地，逆变[度规张量](@entry_id:160222)的分量是[逆变基](@entry_id:197906)矢量的[点积](@entry_id:149019)：
$g^{ij} = \vec{g}^i \cdot \vec{g}^j$

对于上述例子，由于 $g_{ij}$ 是[对角矩阵](@entry_id:637782)，其[逆矩阵](@entry_id:140380)就是将对角元素取倒数：
$g^{ij} = \begin{pmatrix} 1  0 \\ 0  \frac{1}{\cosh^2(u)} \end{pmatrix}$

同样，对于极[坐标系](@entry_id:156346)，其[线元](@entry_id:196833)为 $ds^2 = dr^2 + r^2 d\theta^2$。因此其[协变](@entry_id:634097)度规张量为 $g_{ij} = \begin{pmatrix} 1  0 \\ 0  r^2 \end{pmatrix}$。其逆矩阵，即逆变[度规张量](@entry_id:160222)，就是 [@problem_id:1500068]：
$g^{ij} = \begin{pmatrix} 1  0 \\ 0  \frac{1}{r^2} \end{pmatrix}$

[度规张量](@entry_id:160222)是[张量分析](@entry_id:161423)中的核心工具。它不仅定义了距离，还允许我们在[协变](@entry_id:634097)分量和[逆变分量](@entry_id:185440)之间进行转换，这一过程称为**[升降指标](@entry_id:161292)**。例如，$A_i = g_{ij} A^j$ 和 $A^i = g^{ij} A_j$。

### 矢量和张量分量的变换法则

张量的一个关键特性是其分量在坐标变换下遵循特定的变换法则。这些法则确保了张量所描述的物理实体是独立于我们选择的[坐标系](@entry_id:156346)的。

对于一个矢量的**[逆变分量](@entry_id:185440)** $V^i$，其变换法则为：
$\bar{V}^k = \frac{\partial \bar{x}^k}{\partial x^i} V^i$
注意，其变换矩阵 $\frac{\partial \bar{x}^k}{\partial x^i}$ 与坐标[微分](@entry_id:158718) $d\bar{x}^k = \frac{\partial \bar{x}^k}{\partial x^i} dx^i$ 的变换矩阵相同，这正是“逆变”（contravariant）一词的来源（与[基矢](@entry_id:199546)量的变换相反）。

对于一个矢量的**[协变](@entry_id:634097)分量** $V_i$，其变换法则为：
$\bar{V}_k = \frac{\partial x^i}{\partial \bar{x}^k} V_i$
它的[变换矩阵](@entry_id:151616) $\frac{\partial x^i}{\partial \bar{x}^k}$ 与梯度向量 $\frac{\partial \phi}{\partial \bar{x}^k} = \frac{\partial x^i}{\partial \bar{x}^k} \frac{\partial \phi}{\partial x^i}$ 的[变换矩阵](@entry_id:151616)相同，因此被称为“协变”（covariant）。

让我们看一个具体的计算 [@problem_id:1500091]。假设一个矢量场在笛卡尔坐标系 $(x,y)$ 下的[逆变分量](@entry_id:185440)为 $V^x = x^2 - y^2$ 和 $V^y = 2xy$。我们希望找到它在极[坐标系](@entry_id:156346) $(r, \theta)$ 下的[逆变分量](@entry_id:185440) $(V^r, V^\theta)$。变换法则为：
$V^r = \frac{\partial r}{\partial x} V^x + \frac{\partial r}{\partial y} V^y$
$V^\theta = \frac{\partial \theta}{\partial x} V^x + \frac{\partial \theta}{\partial y} V^y$

首先，我们需要计算雅可比矩阵的分量。由 $r = \sqrt{x^2+y^2}$ 和 $\theta = \arctan(y/x)$ 可得：
$\frac{\partial r}{\partial x} = \frac{x}{r} = \cos\theta$, $\quad \frac{\partial r}{\partial y} = \frac{y}{r} = \sin\theta$
$\frac{\partial \theta}{\partial x} = -\frac{y}{r^2} = -\frac{\sin\theta}{r}$, $\quad \frac{\partial \theta}{\partial y} = \frac{x}{r^2} = \frac{\cos\theta}{r}$

然后，我们将 $V^x$ 和 $V^y$ 用极坐标表示：
$V^x = (r\cos\theta)^2 - (r\sin\theta)^2 = r^2\cos(2\theta)$
$V^y = 2(r\cos\theta)(r\sin\theta) = r^2\sin(2\theta)$

代入变换公式：
$V^r = (\cos\theta)(r^2\cos(2\theta)) + (\sin\theta)(r^2\sin(2\theta)) = r^2 \cos(\theta - 2\theta) = r^2\cos(-\theta) = r^2\cos\theta$
$V^\theta = (-\frac{\sin\theta}{r})(r^2\cos(2\theta)) + (\frac{\cos\theta}{r})(r^2\sin(2\theta)) = r(\sin(2\theta)\cos\theta - \cos(2\theta)\sin\theta) = r\sin(2\theta-\theta) = r\sin\theta$

因此，在极坐标下，该矢量场的分量为 $(V^r, V^\theta) = (r^2\cos\theta, r\sin\theta)$。这个过程展示了如何系统地应用变换法则来获得矢量在不同[坐标系](@entry_id:156346)下的表示。

### 联络、[协变导数](@entry_id:152476)与曲率

在[曲线坐标系](@entry_id:172561)中，由于[基矢](@entry_id:199546)量本身是变化的，对张量分量简单地求偏导数并不能得到一个张量。为了定义一个在坐标变换下行为正确的导数，我们需要引入**协变导数**（Covariant Derivative），记为 $\nabla_i$。

[协变导数](@entry_id:152476)的出现是为了“修正”普通偏导数，它通过引入一个称为**[克里斯托费尔符号](@entry_id:159831)**（Christoffel Symbols）或**[联络系数](@entry_id:157618)**（Connection Coefficients）的附加项，来抵消[基矢](@entry_id:199546)量变化带来的影响。对于一个逆变矢量 $V^k$，其协变导数定义为：
$\nabla_j V^k = \frac{\partial V^k}{\partial x^j} + \Gamma^k_{ji} V^i$

[克里斯托费尔符号](@entry_id:159831) $\Gamma^k_{ij}$（第二类）本身不是张量，但它包含了关于[坐标系](@entry_id:156346)如何扭曲的所有信息。它可以完全由度规张量及其导数计算得出：
$\Gamma^k_{ij} = \frac{1}{2} g^{kl} \left( \frac{\partial g_{li}}{\partial x^j} + \frac{\partial g_{lj}}{\partial x^i} - \frac{\partial g_{ij}}{\partial x^l} \right)$

这个公式看起来复杂，但在许多情况下，由于[度规张量](@entry_id:160222)的许多分量为零或为常数，计算会大大简化。让我们以三维柱坐标 $(r, \theta, z)$ 为例 [@problem_id:1500059]。其[线元](@entry_id:196833)为 $ds^2 = dr^2 + r^2 d\theta^2 + dz^2$。[度规张量](@entry_id:160222)为 $g_{ij} = \mathrm{diag}(1, r^2, 1)$。唯一的非恒定分量是 $g_{\theta\theta} = g_{22} = r^2$。因此，唯一不为零的[偏导数](@entry_id:146280)是 $\frac{\partial g_{22}}{\partial r} = 2r$。
代入公式，我们可以系统地计算出所有非零的[克里斯托费尔符号](@entry_id:159831)（利用其对称性 $\Gamma^k_{ij} = \Gamma^k_{ji}$）：
$\Gamma^1_{22} = \Gamma^r_{\theta\theta} = \frac{1}{2}g^{11}( - \frac{\partial g_{22}}{\partial x^1} ) = \frac{1}{2}(1)(-2r) = -r$
$\Gamma^2_{12} = \Gamma^\theta_{r\theta} = \frac{1}{2}g^{22}( \frac{\partial g_{22}}{\partial x^1} ) = \frac{1}{2}(\frac{1}{r^2})(2r) = \frac{1}{r}$
所有其他的[克里斯托费尔符号](@entry_id:159831)都为零。这些非零的 $\Gamma$ 项正是描述“[惯性力](@entry_id:169104)”（如离心力和科里奥利力）在[拉格朗日力学](@entry_id:147054)和广义相对论中出现的根源。

协变导数的一个重要应用是计算标量场的[拉普拉斯算子](@entry_id:146319)。在[广义坐标](@entry_id:156576)中，[拉普拉斯算子](@entry_id:146319) $\nabla^2\Phi$ 的张量表达式为 $\nabla^2 \Phi = g^{ij}\nabla_i (\nabla_j \Phi)$。由于对标量 $\Phi$ 的[协变导数](@entry_id:152476)就是普通偏导数（$\nabla_j \Phi = \partial_j \Phi$），上式可展开为：
$\nabla^2 \Phi = g^{ij}(\partial_i \partial_j \Phi - \Gamma^k_{ij} \partial_k \Phi)$
这个表达式清楚地显示，[拉普拉斯算子](@entry_id:146319)由两部分组成：常规的[二阶偏导数](@entry_id:635213)项，以及一个涉及克里斯托费尔符号的“曲率修正项” $C = -g^{ij}\Gamma^k_{ij}\partial_k \Phi$ [@problem_id:1500076]。这个修正项正是由于坐标网格本身的弯曲造成的。

最后，我们必须区分由[坐标系](@entry_id:156346)选择引起的“表观曲率”（由非零的 $\Gamma$ 反映）和空间本身的**内在曲率**（Intrinsic Curvature）。衡量内在曲率的终极工具是**[黎曼曲率张量](@entry_id:160189)**（Riemann Curvature Tensor）。它由[克里斯托费尔符号](@entry_id:159831)及其导数构成：
$R^\alpha{}_{\beta\gamma\delta} = \frac{\partial \Gamma^\alpha_{\delta\beta}}{\partial x^\gamma} - \frac{\partial \Gamma^\alpha_{\gamma\beta}}{\partial x^\delta} + \Gamma^\alpha_{\gamma\epsilon}\Gamma^\epsilon_{\delta\beta} - \Gamma^\alpha_{\delta\epsilon}\Gamma^\epsilon_{\gamma\beta}$

[黎曼曲率张量](@entry_id:160189)描述了将一个矢量沿一个微小闭合回路平行移动后与自身的变化。如果一个空间的所有[黎曼张量分量](@entry_id:188469)都为零，那么这个空间就是**平直**的（flat）。

一个深刻的例子是计算平直[欧几里得空间](@entry_id:138052)在球坐标下的[黎曼张量](@entry_id:160847) [@problem_id:1500036]。尽管[球坐标系](@entry_id:167517)的[克里斯托费尔符号](@entry_id:159831)（如 $\Gamma^r_{\theta\theta}=-r, \Gamma^\theta_{r\theta}=1/r$ 等）大多不为零，这表明坐标网格是弯曲的，但当我们计算[黎曼张量](@entry_id:160847)的分量时，例如 $R^r{}_{\theta r \theta}$，会发现一个奇妙的抵消：
$R^r{}_{\theta r \theta} = \underbrace{\frac{\partial \Gamma^r_{\theta\theta}}{\partial r}}_{-1} - \underbrace{\frac{\partial \Gamma^r_{r\theta}}{\partial \theta}}_{0} + \underbrace{\Gamma^r_{r\epsilon}\Gamma^\epsilon_{\theta\theta}}_{0} - \underbrace{\Gamma^r_{\theta\epsilon}\Gamma^\epsilon_{r\theta}}_{\Gamma^r_{\theta\theta}\Gamma^\theta_{r\theta} = (-r)(1/r) = -1}$
$R^r{}_{\theta r \theta} = -1 - 0 + 0 - (-1) = 0$

事实上，可以证明，对于[球坐标系](@entry_id:167517)，所有黎曼张量的分量都为零。这证实了一个基本事实：[欧几里得空间](@entry_id:138052)是内在平直的，无论我们使用多么“弯曲”的[坐标系](@entry_id:156346)来描述它。[克里斯托费尔符号](@entry_id:159831)反映的是[坐标系](@entry_id:156346)的选择，而[黎曼曲率张量](@entry_id:160189)则揭示了空间本身的几何本质。这一区分是广义相对论的核心，在该理论中，[引力](@entry_id:175476)不再是力，而是时空内在曲率的表现。