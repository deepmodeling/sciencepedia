## 引言
[笛卡尔坐标](@entry_id:167698)系是我们在物理学中接触最早、最直观的空间描述体系。然而，在电动力学领域，它的作用远不止于标记位置——它是一套强大的分析语言，是运用矢量微积分揭示[电场](@entry_id:194326)、[磁场](@entry_id:153296)与时变现象背后深刻物理规律的基础框架。许多学习者常常将其视为简单的几何背景，而忽略了它在系统化表述和求解[麦克斯韦方程组](@entry_id:150940)中的核心作用，从而在理论与实际问题之间产生了知识鸿沟。

本文旨在填补这一鸿沟，系统性地展示[笛卡尔坐标](@entry_id:167698)系作为电动力学分析工具的强大功能。通过以下章节，您将全面掌握其应用：在**“原理与机制”**中，我们将深入探讨梯度、[散度和旋度](@entry_id:270881)等关键算符，并阐明它们如何联系场与源；在**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将通过解决具体的[静电学](@entry_id:140489)、粒子动力学和波导问题，展示这些原理的实际应用；最后，在**“动手实践”**中，您将通过练习来巩固所学，将理论转化为解决问题的能力。通过这一结构化的学习路径，您将掌握在[笛卡尔坐标](@entry_id:167698)系中自如分析和解决复杂电磁问题的核心技能。

## 原理与机制

在[电动力学](@entry_id:158759)的研究中，[笛卡尔坐标](@entry_id:167698)系 $(x, y, z)$ 不仅是一种空间描述工具，更是应用[麦克斯韦方程组](@entry_id:150940)、分析场与源相互作用的基础语言。本章将深入探讨在笛卡尔坐标系下，描述[电磁场](@entry_id:265881)行为的核心原理与关键机制。我们将从场与势的基本关系出发，系统地介绍梯度、[散度和旋度](@entry_id:270881)等矢量算符，并通过它们揭示[电荷](@entry_id:275494)、电流与[电磁场](@entry_id:265881)之间深刻的内在联系。

### 静电场与标势

在无时变[磁场](@entry_id:153296)的静电学（electrostatics）中，[电场](@entry_id:194326) $\vec{E}$ 是一个[无旋场](@entry_id:183486)，即 $\nabla \times \vec{E} = \vec{0}$。这一性质保证了我们可以引入一个标量函数，即**[电势](@entry_id:267554)**（electric potential）$V$，将矢量场 $\vec{E}$ 的计算简化为标量场 $V$ 的计算。它们之间的关系由以下基本方程定义：

$$
\vec{E} = -\nabla V
$$

这里的 $\nabla$ 符号代表**梯度**（gradient）算符。在[笛卡尔坐标](@entry_id:167698)系中，它作用于一个标量函数 $V(x, y, z)$ 时，会产生一个矢量，该矢量指向函数 $V$ 增长最快的方向，其大小为该方向上的变化率。其具体表达式为：

$$
\nabla V = \frac{\partial V}{\partial x}\hat{x} + \frac{\partial V}{\partial y}\hat{y} + \frac{\partial V}{\partial z}\hat{z}
$$

其中 $\hat{x}, \hat{y}, \hat{z}$ 分别是 $x, y, z$ 轴的单位矢量。负号表示[电场](@entry_id:194326)指向[电势](@entry_id:267554)降低的方向。

理解梯度与[电势](@entry_id:267554)的关系，是分析静电场[分布](@entry_id:182848)的第一步。让我们通过几个例子来阐明这一概念。

考虑一个[电势](@entry_id:267554)由 $V(x, y, z) = -E_0 (x + 2y)$ 描述的区域，其中 $E_0$ 为一个具有[电场](@entry_id:194326)单位的正常数。这个[电势](@entry_id:267554)在空间中是线性变化的。为了求出对应的[电场](@entry_id:194326) $\vec{E}$，我们计算[电势](@entry_id:267554) $V$ 的梯度：

$$
\nabla V = \frac{\partial}{\partial x}(-E_0(x+2y))\hat{x} + \frac{\partial}{\partial y}(-E_0(x+2y))\hat{y} + \frac{\partial}{\partial z}(-E_0(x+2y))\hat{z} = -E_0\hat{x} - 2E_0\hat{y}
$$

因此，[电场](@entry_id:194326)为：

$$
\vec{E} = -\nabla V = E_0\hat{x} + 2E_0\hat{y}
$$

这个结果表明，一个线性变化的[电势](@entry_id:267554)对应一个**均匀[电场](@entry_id:194326)**。该[电场](@entry_id:194326)的各个分量不随空间位置 $(x, y, z)$ 的变化而改变。尽管场是均匀的，但其方向既不沿 $x$ 轴也不沿 $y$ 轴，而是两者的矢量和。其大小为 $|\vec{E}| = \sqrt{E_0^2 + (2E_0)^2} = \sqrt{5}E_0$，与 $x$ 轴正方向的夹角 $\theta = \arctan(E_y/E_x) = \arctan(2) \approx 63.4^{\circ}$。[@problem_id:1570770]

[电势](@entry_id:267554)的形式可以更加复杂，从而产生非均匀的[电场](@entry_id:194326)。例如，在一个二维静电[离子阱](@entry_id:192565)的简化模型中，[电势](@entry_id:267554)可能由 $V(x, y, z) = V_0 \frac{y^2 - x^2}{a^2}$ 给出，其中 $V_0$ 和 $a$ 是常数。这种形式的[电势](@entry_id:267554)在静电[四极透镜](@entry_id:268574)或[离子阱](@entry_id:192565)中非常关键。我们同样可以通过计算梯度的负值来获得[电场](@entry_id:194326)[分布](@entry_id:182848)：

$$
E_x = -\frac{\partial V}{\partial x} = -\frac{V_0}{a^2}(-2x) = \frac{2V_0 x}{a^2}
$$

$$
E_y = -\frac{\partial V}{\partial y} = -\frac{V_0}{a^2}(2y) = -\frac{2V_0 y}{a^2}
$$

$$
E_z = -\frac{\partial V}{\partial z} = 0
$$

所以，[电场](@entry_id:194326)矢量为 $\vec{E}(x, y) = \frac{2V_0}{a^2}(x\hat{x} - y\hat{y})$。这是一个**[非均匀电场](@entry_id:270120)**，其大小和方向都随位置变化。例如，在 $x$ 轴上 ($y=0$)，[电场](@entry_id:194326)指向 $x$ 轴正方向；而在 $y$ 轴上 ($x=0$)，[电场](@entry_id:194326)指向 $y$ 轴负方向。这种场结构能够在特定区域内对[带电粒子](@entry_id:160311)产生[约束力](@entry_id:170052)。[@problem_id:1787693]

### 电荷密度与[高斯定律](@entry_id:141493)

[电场](@entry_id:194326)的源头是[电荷](@entry_id:275494)。描述[电场](@entry_id:194326)与其源（[电荷](@entry_id:275494)）之间局域关系的，是麦克斯韦方程组中的**[高斯定律](@entry_id:141493)**（Gauss's law）的[微分形式](@entry_id:146747)：

$$
\nabla \cdot \vec{E} = \frac{\rho}{\epsilon_0}
$$

这里的 $\rho$ 是**[体电荷密度](@entry_id:264747)**（volume charge density），$\epsilon_0$ 是[真空介电常数](@entry_id:204253)。算符 $\nabla \cdot$ 代表**散度**（divergence），它衡量的是矢量场在一个点上“发散”或“汇聚”的程度。在笛卡尔坐标系中，矢量场 $\vec{F} = F_x\hat{x} + F_y\hat{y} + F_z\hat{z}$ 的散度定义为：

$$
\nabla \cdot \vec{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}
$$

物理上，[电场的散度](@entry_id:272995)正比于该点的[电荷密度](@entry_id:144672)。正[电荷](@entry_id:275494)是[电场线](@entry_id:277009)的“源头”（正散度），负[电荷](@entry_id:275494)是电场线的“汇点”（负散度）。

如果已知一个区域的静电场[分布](@entry_id:182848)，我们便可以利用[高斯定律的微分形式](@entry_id:191832)来反推出产生该[电场](@entry_id:194326)的[电荷分布](@entry_id:144400)。假设在一个空间区域中，[电场](@entry_id:194326)由 $\vec{E} = K(2x\hat{x} - y\hat{y} + 5z\hat{z})$ 给出，其中 $K$ 是一个常数。我们可以通过计算该[电场的散度](@entry_id:272995)来确定电荷密度 $\rho$：

$$
\nabla \cdot \vec{E} = \frac{\partial}{\partial x}(2Kx) + \frac{\partial}{\partial y}(-Ky) + \frac{\partial}{\partial z}(5Kz) = 2K - K + 5K = 6K
$$

根据[高斯定律](@entry_id:141493)，$\frac{\rho}{\epsilon_0} = 6K$，因此[电荷密度](@entry_id:144672)为 $\rho = 6K\epsilon_0$。有趣的是，尽管[电场](@entry_id:194326) $\vec{E}$ 本身是随空间位置变化的非均匀场，但产生它的电荷密度 $\rho$ 却是一个常数，即[电荷](@entry_id:275494)是[均匀分布](@entry_id:194597)的。[@problem_id:1787695]

高斯定律的积分形式，即 $\oint_S \vec{E} \cdot d\vec{A} = \frac{Q_{enc}}{\epsilon_0}$，与微分形式通过**[散度定理](@entry_id:143110)**联系在一起。这一定理在处理具有特定对称性的问题时尤其强大。例如，考虑一个中心在原点、边长为 $a$ 的立方体，其内部的[电荷密度](@entry_id:144672)为 $\rho(x) = \frac{\rho_0 x}{a}$。要计算通过立方体右侧面（位于 $x=a/2$）的[电通量](@entry_id:266049) $\Phi = \int \vec{E} \cdot d\vec{A}$，我们首先需要知道该表面上的[电场](@entry_id:194326)。

由于电荷分布只依赖于 $x$ 坐标，且关于 $x=0$ 平面呈反对称（$\rho(x) = -\rho(-x)$），我们可以推断[电场](@entry_id:194326)主要沿 $x$ 方向，即 $\vec{E} \approx E_x(x)\hat{x}$。利用[高斯定律的微分形式](@entry_id:191832) $\frac{dE_x}{dx} = \frac{\rho(x)}{\epsilon_0} = \frac{\rho_0 x}{a \epsilon_0}$，通[过积分](@entry_id:753033)可得 $E_x(x) = \frac{\rho_0 x^2}{2a\epsilon_0} + C$。根据对称性，$x=0$ 平面上的[电场](@entry_id:194326)应为零，即 $E_x(0)=0$，这使得积分常数 $C=0$。因此，立方体内部的[电场](@entry_id:194326)为 $\vec{E}(x) = \frac{\rho_0 x^2}{2a\epsilon_0}\hat{x}$。

在 $x=a/2$ 的表面上，[电场](@entry_id:194326)是均匀的，大小为 $E_x(a/2) = \frac{\rho_0 (a/2)^2}{2a\epsilon_0} = \frac{\rho_0 a}{8\epsilon_0}$。由于该表面的法向矢量为 $\hat{x}$，[电通量](@entry_id:266049)就是[电场](@entry_id:194326)大小乘以表面积 $a^2$：

$$
\Phi = E_x(a/2) \cdot A = \left(\frac{\rho_0 a}{8\epsilon_0}\right) a^2 = \frac{\rho_0 a^3}{8\epsilon_0}
$$

这个例子展示了如何结合[微分](@entry_id:158718)和[积分形式的高斯定律](@entry_id:271314)来解决更复杂的电荷分布问题。[@problem_id:1570763]

### 静[磁场](@entry_id:153296)与[矢势](@entry_id:153642)

与[电场](@entry_id:194326)不同，[磁场](@entry_id:153296) $\vec{B}$ 是一个[无散场](@entry_id:260932)，这意味着它满足麦克斯韦方程组中的另一条基本定律——[高斯磁定律](@entry_id:182942)：

$$
\nabla \cdot \vec{B} = 0
$$

这条定律的物理解释是自然界中不存在**磁单极子**（magnetic monopoles）。[磁场](@entry_id:153296)线总是闭合的，它们没有起点或终点。因此，任何物理上可能存在的[磁场](@entry_id:153296)都必须满足散度为零的条件。

我们可以利用这一性质来检验一个假设的[磁场](@entry_id:153296)是否符合物理规律。例如，考虑一个假设的静[磁场](@entry_id:153296) $\vec{B}(x, y, z) = C(z\hat{x} + x\hat{y} + y\hat{z})$。为了判断其物理实在性，我们首先计算它的散度：

$$
\nabla \cdot \vec{B} = \frac{\partial}{\partial x}(Cz) + \frac{\partial}{\partial y}(Cx) + \frac{\partial}{\partial z}(Cy) = 0 + 0 + 0 = 0
$$

由于其散度为零，该[磁场](@entry_id:153296)满足[高斯磁定律](@entry_id:182942)，因此它至少是数学上可能的。[@problem_id:1787685]

因为[磁场的散度](@entry_id:273621)恒为零，我们可以引入一个**[磁矢势](@entry_id:141246)**（magnetic vector potential）$\vec{A}$，使得：

$$
\vec{B} = \nabla \times \vec{A}
$$

这里的 $\nabla \times$ 算符代表**旋度**（curl）。一个矢量场 $\vec{F}$ 的旋度在[笛卡尔坐标](@entry_id:167698)系下的定义为：

$$
\nabla \times \vec{F} = \left(\frac{\partial F_z}{\partial y} - \frac{\partial F_y}{\partial z}\right)\hat{x} + \left(\frac{\partial F_x}{\partial z} - \frac{\partial F_z}{\partial x}\right)\hat{y} + \left(\frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y}\right)\hat{z}
$$

之所以可以这样定义，是因为一个[梯度的旋度](@entry_id:274168)恒为零（$\nabla \times (\nabla f) = 0$），而一个[旋度的散度](@entry_id:271562)也恒为零（$\nabla \cdot (\nabla \times \vec{F}) = 0$）。因此，将 $\vec{B}$ 写成 $\vec{A}$ 的旋度自动满足了 $\nabla \cdot \vec{B}=0$ 的条件。

与[电势](@entry_id:267554) $V$ 不同，磁矢势 $\vec{A}$ 并不唯一。对于给定的[磁场](@entry_id:153296) $\vec{B}$，可以选择无穷多个满足条件的 $\vec{A}$。这种选择的自由度称为**规范自由度**（gauge freedom）。具体来说，如果我们有一个[矢势](@entry_id:153642) $\vec{A}$，那么 $\vec{A}' = \vec{A} + \nabla \psi$（其中 $\psi$ 是任意标量函数）会给出完全相同的[磁场](@entry_id:153296) $\vec{B}$，因为 $\nabla \times \vec{A}' = \nabla \times \vec{A} + \nabla \times (\nabla \psi) = \nabla \times \vec{A}$。

作为一个例子，考虑一个沿 $z$ 轴方向的均匀[磁场](@entry_id:153296) $\vec{B} = B_0\hat{z}$。我们可以检验多个不同的[矢势](@entry_id:153642)表达式。例如，以下三种形式的 $\vec{A}$ 都是该[磁场](@entry_id:153296)的有效[矢势](@entry_id:153642)：
1.  $\vec{A} = \frac{B_0}{2}(-y\hat{x} + x\hat{y})$
2.  $\vec{A} = B_0 x \hat{y}$
3.  $\vec{A} = -B_0 y \hat{x}$

对以上任意一种形式计算旋度，例如第一种：

$$
\nabla \times \vec{A} = \left(\frac{\partial}{\partial x}\left(\frac{B_0}{2}x\right) - \frac{\partial}{\partial y}\left(-\frac{B_0}{2}y\right)\right)\hat{z} = \left(\frac{B_0}{2} + \frac{B_0}{2}\right)\hat{z} = B_0\hat{z}
$$

这证实了对于同一个[磁场](@entry_id:153296)，[矢势](@entry_id:153642)的选择具有多样性。在具体计算时，我们可以选择一种最方便的规范（即选择特定的 $\vec{A}$ 形式）来简化问题。[@problem_id:1570766]

[磁场](@entry_id:153296)的源是电流。**[安培定律](@entry_id:140092)**（Ampère's law）描述了电流如何产生[磁场](@entry_id:153296)。其[微分形式](@entry_id:146747)为 $\nabla \times \vec{B} = \mu_0 \vec{J}$，其中 $\vec{J}$ 是电流密度，$\mu_0$ 是[真空磁导率](@entry_id:186031)。积分形式则为 $\oint_C \vec{B} \cdot d\vec{l} = \mu_0 I_{enc}$，它表明[磁场](@entry_id:153296)沿任意闭合路径 $C$ 的线积分等于该路径所包围的净电流 $I_{enc}$ 乘以 $\mu_0$。

[安培定律的积分形式](@entry_id:270391)在计算具有高度对称性的电流[分布](@entry_id:182848)所产生的[磁场](@entry_id:153296)时非常有用，或者在计算给定[磁场](@entry_id:153296)沿闭合路径的[环路积分](@entry_id:164828)时可以大大简化计算。例如，一根平行于 $z$ 轴的无限长直导线穿过 $xy$ 平面上的点 $(L/4, 0, 0)$，承载电流 $I$。我们要计算[磁场](@entry_id:153296) $\vec{B}$ 沿一个位于 $xy$ 平面、中心在原点、边长为 $L$ 的正方形回路的[线积分](@entry_id:141417) $\oint \vec{B} \cdot d\vec{l}$。

我们无需计算回路每一点的 $\vec{B}$ 场然后进行复杂的积分。根据[安培定律](@entry_id:140092)，我们只需要判断回路是否包围了电流。该正方形回路的范围是 $-L/2 \le x \le L/2$ 和 $-L/2 \le y \le L/2$。由于导线的位置 $(L/4, 0)$ 在这个范围内，所以回路包围了电流 $I$。因此，根据[安培定律](@entry_id:140092)：

$$
\oint \vec{B} \cdot d\vec{l} = \mu_0 I_{enc} = \mu_0 I
$$

这个结果与回路的具体形状（正方形）以及导线在回路内的具体位置无关，只要导线被回路包围即可。[@problem_id:1787682]

### [电动力学](@entry_id:158759)与[法拉第定律](@entry_id:149836)

当[电场和磁场](@entry_id:261347)随时间变化时，它们会相互耦合，进入[电动力学](@entry_id:158759)（electrodynamics）的范畴。其中一个关键的耦合关系由**[法拉第感应定律](@entry_id:146175)**（Faraday's law of induction）的微分形式给出：

$$
\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}
$$

这个方程揭示了时变[磁场](@entry_id:153296)可以产生[电场](@entry_id:194326)。与由静[电荷](@entry_id:275494)产生的[电场](@entry_id:194326)（其旋度为零）不同，由时变[磁场](@entry_id:153296)感生出的[电场](@entry_id:194326)是有旋的（$\nabla \times \vec{E} \neq \vec{0}$）。这意味着感生[电场](@entry_id:194326)不是[保守场](@entry_id:137555)，[电势](@entry_id:267554)的概念需要被修正。

假设在一个区域，[磁场](@entry_id:153296)随时间变化，但空间上是均匀的，例如 $\vec{B}(t) = B_0 (\frac{t}{\tau})^3 \hat{x}$，其中 $B_0$ 和 $\tau$ 是常数。这个变化的[磁场](@entry_id:153296)将在周围空间中感生出[电场](@entry_id:194326) $\vec{E}$。我们可以用[法拉第定律](@entry_id:149836)来求出这个感生[电场的旋度](@entry_id:182875)：

首先计算[磁场](@entry_id:153296)对时间的偏导数：

$$
\frac{\partial \vec{B}}{\partial t} = \frac{d}{dt} \left[ B_0 \left(\frac{t}{\tau}\right)^3 \hat{x} \right] = B_0 \cdot 3 \left(\frac{t}{\tau}\right)^2 \cdot \frac{1}{\tau} \hat{x} = \frac{3 B_0}{\tau^3} t^2 \hat{x}
$$

然后根据法拉第定律，我们得到感生[电场的旋度](@entry_id:182875)：

$$
\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t} = -\frac{3 B_0}{\tau^3} t^2 \hat{x}
$$

这个结果表明，一个沿 $x$ 轴方向变化的[磁场](@entry_id:153296)会产生一个具有非零旋度的[电场](@entry_id:194326)。这个[电场](@entry_id:194326)的[场线](@entry_id:172226)会形成闭合回路，驱动导体中的[涡电流](@entry_id:275449)。[@problem_id:1787675]

### 笛卡尔坐标系中的[边值问题](@entry_id:193901)

在许多实际工程问题中，我们常常不知道空间中的[电荷](@entry_id:275494)或电流[分布](@entry_id:182848)，但知道某些边界上的[电势](@entry_id:267554)或场值。这类问题称为**边值问题**（boundary-value problems）。在无源（$\rho=0, \vec{J}=0$）的静态区域，问题通常归结为求解**拉普拉斯方程**（Laplace's equation）或**泊松方程**（Poisson's equation）。在无源的[静电学](@entry_id:140489)区域，[电势](@entry_id:267554)满足拉普拉斯方程：

$$
\nabla^2 V = \nabla \cdot (\nabla V) = \frac{\partial^2 V}{\partial x^2} + \frac{\partial^2 V}{\partial y^2} + \frac{\partial^2 V}{\partial z^2} = 0
$$

对于具有简单几何边界的系统，我们可以用一些强大的方法来求解。

**镜像法**（Method of Images）是一种巧妙的技术，适用于处理点电荷与简单形状导体（如无限大平面或球体）之间的相互作用。其核心思想是用一个或多个虚拟的“[镜像电荷](@entry_id:266998)”来替代导体，使得[镜像电荷](@entry_id:266998)与原[电荷](@entry_id:275494)共同产生的[电势](@entry_id:267554)在导体表面上满足给定的边界条件（例如，接地导体表面[电势](@entry_id:267554)为零）。

考虑一个位于 $(0, 0, d)$ 处的点电荷 $+q$，下方是在 $z=0$ 处的一个无限大接地导体平面。为了求解 $z>0$ 区域的[电场](@entry_id:194326)，我们可以用一个位于对称位置 $(0, 0, -d)$ 的镜像电荷 $-q$ 来替代导体平面。原[电荷](@entry_id:275494) $+q$ 和[镜像电荷](@entry_id:266998) $-q$ 共同在 $z=0$ 平面上产生的[电势](@entry_id:267554)恰好为零，满足了边界条件。

因此，真实[电荷](@entry_id:275494) $+q$ 受到的力，就是由[镜像电荷](@entry_id:266998) $-q$ 施加给它的库仑力。两个[电荷](@entry_id:275494)之间的距离是 $2d$，方向沿 $z$ 轴。作用在 $+q$ 上的力为：

$$
\vec{F} = \frac{1}{4\pi\epsilon_0} \frac{(+q)(-q)}{(2d)^2} \hat{z} = -\frac{q^2}{16\pi\epsilon_0 d^2} \hat{z}
$$

这个力指向导体平面（负 $z$ 方向），表明[电荷](@entry_id:275494)被吸引向接地导体。镜像法将一个复杂的边界问题转化为了一个简单的两[电荷](@entry_id:275494)相互作用问题。[@problem_id:1787713]

**[分离变量法](@entry_id:168509)**（Separation of Variables）是[求解偏微分方程](@entry_id:138485)（如[拉普拉斯方程](@entry_id:143689)）的标准解析方法，尤其适用于矩形、圆柱形或球形等[坐标系](@entry_id:156346)可分离的边界。

考虑一个由 $x=0, a$，$y=0, b$，$z=0, c$ 所围成的矩形空腔。其中五个面接地（$V=0$），而顶面 $z=c$ 的[电势](@entry_id:267554)被维持在 $V(x,y,c) = V_0 \sin(\frac{n\pi x}{a})\sin(\frac{m\pi y}{b})$。我们的目标是求解[空腔](@entry_id:197569)内部的[电势](@entry_id:267554) $V(x,y,z)$。

由于腔内无[电荷](@entry_id:275494)，[电势](@entry_id:267554) $V$ 满足[拉普拉斯方程](@entry_id:143689) $\nabla^2 V = 0$。我们假设解可以写成三个只依赖于单个变量的函数之积：$V(x,y,z) = X(x)Y(y)Z(z)$。代入拉普拉斯方程并除以 $V$，得到：

$$
\frac{1}{X}\frac{d^2X}{dx^2} + \frac{1}{Y}\frac{d^2Y}{dy^2} + \frac{1}{Z}\frac{d^2Z}{dz^2} = 0
$$

由于三项之和为零，每一项都必须是一个常数。我们设 $\frac{X''}{X}=-k_x^2$, $\frac{Y''}{Y}=-k_y^2$, $\frac{Z''}{Z}=k_z^2$，且 $k_z^2 = k_x^2+k_y^2$。

对于 $x$ 方向，方程 $X''+k_x^2 X=0$ 及其边界条件 $X(0)=0, X(a)=0$ 的解是 $X(x) \propto \sin(\frac{n\pi x}{a})$，其中 $n$ 是正整数。同理，$Y(y) \propto \sin(\frac{m\pi y}{b})$。

对于 $z$ 方向，方程是 $Z'' - (k_x^2+k_y^2)Z = 0$。设 $\gamma = \sqrt{(\frac{n\pi}{a})^2 + (\frac{m\pi}{b})^2}$，通解为 $Z(z) = A\sinh(\gamma z) + B\cosh(\gamma z)$。边界条件 $V(x,y,0)=0$ 要求 $Z(0)=0$，这意味着 $B=0$。

将这些解组合起来，并利用顶面 $z=c$ 的边界条件来确定最终的系数，我们得到内部[电势](@entry_id:267554)的完整解：

$$
V(x,y,z) = V_0 \sin\left(\frac{n\pi x}{a}\right)\sin\left(\frac{m\pi y}{b}\right) \frac{\sinh\left(z\sqrt{\left(\frac{n\pi}{a}\right)^2+\left(\frac{m\pi}{b}\right)^2}\right)}{\sinh\left(c\sqrt{\left(\frac{n\pi}{a}\right)^2+\left(\frac{m\pi}{b}\right)^2}\right)}
$$

这个解精确地描述了在给定边界条件下，空腔内部每一点的[电势](@entry_id:267554)[分布](@entry_id:182848)，是解决此类工程设计问题的基础。[@problem_id:1787704]

综上所述，[笛卡尔坐标](@entry_id:167698)系为我们提供了一个强大的框架，通过[梯度、散度、旋度](@entry_id:269893)等数学工具，系统地应用[麦克斯韦方程组](@entry_id:150940)，从而能够分析从简单的场[分布](@entry_id:182848)到复杂的边界值问题在内的各种电磁现象。