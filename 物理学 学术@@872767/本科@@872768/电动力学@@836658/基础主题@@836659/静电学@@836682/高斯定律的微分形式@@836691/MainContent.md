## 引言
高斯定律是静电学中的一个基本支柱，它以其积分形式将闭合[曲面](@entry_id:267450)上的[电通量](@entry_id:266049)与内部的总[电荷](@entry_id:275494)联系起来。然而，积分形式提供的是一种全局性的描述，无法揭示[电场](@entry_id:194326)与[电荷](@entry_id:275494)在空间每一点的精确对应关系。为了弥补这一知识空白，并更深入地探究[电场](@entry_id:194326)的局部行为，我们必须转向其微分形式。本文旨在系统地阐述[高斯定律的微分形式](@entry_id:191832)，为理解电磁现象提供一个更为精细和强大的数学工具。

在接下来的内容中，我们将分三步深入探索。在“原理与机制”一章中，我们将从积分形式出发，通过散度定理推导出[高斯定律的微分形式](@entry_id:191832)，并探讨其物理意义、与泊松方程的关系以及在[电介质](@entry_id:147163)中的推广。随后，在“应用与跨学科联系”一章，我们将展示该定律如何应用于从场推断源、[分析物](@entry_id:199209)质中的电磁现象，并揭示其在[引力](@entry_id:175476)、[流体力学](@entry_id:136788)和天体物理等多个学科中的深刻类比。最后，通过“动手实践”部分，你将有机会通过具体问题来巩固所学知识。

现在，让我们从最基本的第一步开始，探讨如何从我们熟悉的高斯定律积分形式，过渡到描述点对点关系的微分形式。

## 原理与机制

在上一章中，我们探讨了[高斯定律](@entry_id:141493)的积分形式，它将穿过任意闭合[曲面](@entry_id:267450)的[电通量](@entry_id:266049)与该[曲面](@entry_id:267450)所包围的总[电荷](@entry_id:275494)联系起来。虽然积分形式在处理具有高度对称性的电荷分布时非常有效，但它提供的是一种全局性的描述。为了更深入地理解[电场](@entry_id:194326)与其源（[电荷](@entry_id:275494)）之间的局部关系，即在空间中每一点的关系，我们需要发展一种微分形式的描述。本章将推导并阐释[高斯定律的微分形式](@entry_id:191832)，揭示[电场](@entry_id:194326)在空间中的行为如何直接反映其所在位置的电荷密度。

### 从积分到[微分](@entry_id:158718)：散度的物理意义

[静电学](@entry_id:140489)中的高斯定律积分形式表述为：

$$
\oint_{\partial V} \vec{E} \cdot d\vec{a} = \frac{Q_{\text{enc}}}{\epsilon_0}
$$

其中，左侧是对闭合[曲面](@entry_id:267450) $\partial V$ 的面积分，代表穿过该[曲面](@entry_id:267450)的总[电通量](@entry_id:266049)，而 $Q_{\text{enc}}$ 是该[曲面](@entry_id:267450)所包围的净[电荷](@entry_id:275494)。[电荷](@entry_id:275494) $Q_{\text{enc}}$ 本身可以通过对体积 $V$ 内的电荷密度 $\rho$ 进行积分得到：

$$
Q_{\text{enc}} = \int_V \rho(\vec{r}) \, d\tau
$$

将这两个表达式结合，我们得到：

$$
\oint_{\partial V} \vec{E} \cdot d\vec{a} = \frac{1}{\epsilon_0} \int_V \rho(\vec{r}) \, d\tau
$$

这个方程的左边是关于[曲面](@entry_id:267450)的积分，而右边是关于体积的积分。为了建立一个点对点的关系，我们需要将两者都转换成体积积分。这可以通过应用一个重要的矢量微[积分定理](@entry_id:183680)——**散度定理**（或高斯定理）来实现。散度定理指出，任何矢量场（在此为 $\vec{E}$）穿过一个闭合[曲面](@entry_id:267450)的通量，等于该矢量场的**散度**（divergence）在该[曲面](@entry_id:267450)所包围的体积上的积分：

$$
\oint_{\partial V} \vec{E} \cdot d\vec{a} = \int_V (\nabla \cdot \vec{E}) \, d\tau
$$

这里的 $\nabla \cdot \vec{E}$ 就是[电场](@entry_id:194326) $\vec{E}$ 的散度。它在笛卡尔坐标系中定义为：

$$
\nabla \cdot \vec{E} = \frac{\partial E_x}{\partial x} + \frac{\partial E_y}{\partial y} + \frac{\partial E_z}{\partial z}
$$

现在，我们可以将高斯定律的两个体积积分形式等同起来：

$$
\int_V (\nabla \cdot \vec{E}) \, d\tau = \int_V \frac{\rho}{\epsilon_0} \, d\tau
$$

由于这个关系对于任意选取的体积 $V$ 都必须成立，这意味着两个积分内部的被积函数必须在空间的每一点都相等。由此，我们得到了**[高斯定律的微分形式](@entry_id:191832)**：

$$
\nabla \cdot \vec{E} = \frac{\rho}{\epsilon_0}
$$

这个优雅的方程是[麦克斯韦方程组](@entry_id:150940)之一，它深刻地揭示了[电场](@entry_id:194326)的局部性质。它的物理意义是：**在空间中任意一点，[电场的散度](@entry_id:272995)正比于该点的[电荷密度](@entry_id:144672)**。正[电荷](@entry_id:275494)是[电场线](@entry_id:277009)的“源头”，电场线从其出发向外发散，因此在有正[电荷](@entry_id:275494)的地方，散度为正。负[电荷](@entry_id:275494)是[电场线](@entry_id:277009)的“汇点”，[电场线](@entry_id:277009)汇入其中，因此在有负[电荷](@entry_id:275494)的地方，散度为负。在没有[电荷](@entry_id:275494)的区域（$\rho = 0$），[电场的散度](@entry_id:272995)为零（$\nabla \cdot \vec{E} = 0$），这意味着进入该区域任意一个无穷小[体积元](@entry_id:267802)的电场线数量等于穿出的数量。

### 应用：从[电场](@entry_id:194326)确定[电荷分布](@entry_id:144400)

高斯定律[微分形式](@entry_id:146747)的一个直接应用是，如果我们知道了空间中某区域的[电场](@entry_id:194326) $\vec{E}$ [分布](@entry_id:182848)，就可以反推出产生该[电场](@entry_id:194326)的电荷密度 $\rho$ [分布](@entry_id:182848)。这提供了一种强大的工具来探测和理解[电荷](@entry_id:275494)是如何[分布](@entry_id:182848)的。

#### 在不同[坐标系](@entry_id:156346)下的计算

计算散度依赖于所使用的[坐标系](@entry_id:156346)。让我们通过几个例子来熟悉这个过程。

考虑一个为[离子阱](@entry_id:192565)设计的复杂静电场，在[笛卡尔坐标系](@entry_id:169789)下由下式给出 [@problem_id:1583467]：
$$
\vec{E}(x, y, z) = \alpha(x^2 - y^2)\hat{x} - 2\alpha xy \hat{y} + \beta z \exp\left(-\frac{z^2}{L^2}\right)\hat{z}
$$
其中 $\alpha$, $\beta$, 和 $L$ 是常数。要找出产生此[电场](@entry_id:194326)的[电荷密度](@entry_id:144672) $\rho$，我们计算其散度：
$$
\nabla \cdot \vec{E} = \frac{\partial E_x}{\partial x} + \frac{\partial E_y}{\partial y} + \frac{\partial E_z}{\partial z}
$$
分别计算各个[偏导数](@entry_id:146280)：
$$
\frac{\partial E_x}{\partial x} = \frac{\partial}{\partial x} \left(\alpha(x^2 - y^2)\right) = 2\alpha x
$$
$$
\frac{\partial E_y}{\partial y} = \frac{\partial}{\partial y} (-2\alpha xy) = -2\alpha x
$$
$$
\frac{\partial E_z}{\partial z} = \frac{\partial}{\partial z} \left(\beta z \exp\left(-\frac{z^2}{L^2}\right)\right) = \beta \exp\left(-\frac{z^2}{L^2}\right) + \beta z \exp\left(-\frac{z^2}{L^2}\right) \left(-\frac{2z}{L^2}\right) = \beta \exp\left(-\frac{z^2}{L^2}\right) \left(1 - \frac{2z^2}{L^2}\right)
$$
将它们相加，我们发现前两项恰好抵消：
$$
\nabla \cdot \vec{E} = 2\alpha x - 2\alpha x + \beta \exp\left(-\frac{z^2}{L^2}\right) \left(1 - \frac{2z^2}{L^2}\right) = \beta \exp\left(-\frac{z^2}{L^2}\right) \left(1 - \frac{2z^2}{L^2}\right)
$$
因此，[电荷密度](@entry_id:144672)为：
$$
\rho(z) = \epsilon_0 (\nabla \cdot \vec{E}) = \epsilon_0 \beta \exp\left(-\frac{z^2}{L^2}\right) \left(1 - \frac{2z^2}{L^2}\right)
$$
有趣的是，尽管[电场](@entry_id:194326)的 $x$ 和 $y$ 分量依赖于 $x$ 和 $y$ 坐标，但最终的电荷密度只依赖于 $z$ 坐标。

对于具有[球对称性](@entry_id:272852)的系统，使用球坐标系 $(r, \theta, \phi)$ 会使计算大大简化。在球坐标中，对于一个纯径向场 $\vec{E} = E_r(r) \hat{r}$，散度的表达式为：
$$
\nabla \cdot \vec{E} = \frac{1}{r^2} \frac{d}{dr}(r^2 E_r)
$$
假设一个非均匀带电的天体模型，其内部[电场](@entry_id:194326)由 $\vec{E}(r) = A \frac{r^2}{R^2} \exp(-\frac{r}{R}) \hat{r}$ 描述 [@problem_id:1583489]。我们可以通过计算散度来确定其内部的[电荷密度](@entry_id:144672)[分布](@entry_id:182848) $\rho(r)$。首先，计算 $r^2 E_r$：
$$
r^2 E_r(r) = r^2 \left(A \frac{r^2}{R^2} \exp\left(-\frac{r}{R}\right)\right) = \frac{A}{R^2} r^4 \exp\left(-\frac{r}{R}\right)
$$
然后对 $r$ 求导：
$$
\frac{d}{dr}(r^2 E_r) = \frac{A}{R^2} \left[ 4r^3 \exp\left(-\frac{r}{R}\right) + r^4 \left(-\frac{1}{R}\right) \exp\left(-\frac{r}{R}\right) \right] = \frac{A}{R^2} \exp\left(-\frac{r}{R}\right) (4r^3 - \frac{r^4}{R})
$$
最后，除以 $r^2$ 得到散度：
$$
\nabla \cdot \vec{E} = \frac{1}{r^2} \left[ \frac{A}{R^2} \exp\left(-\frac{r}{R}\right) (4r^3 - \frac{r^4}{R}) \right] = A \exp\left(-\frac{r}{R}\right) \left(\frac{4r}{R^2} - \frac{r^2}{R^3}\right)
$$
于是，电荷密度为：
$$
\rho(r) = \epsilon_0 (\nabla \cdot \vec{E}) = \epsilon_0 A \exp\left(-\frac{r}{R}\right) \left(\frac{4r}{R^2} - \frac{r^2}{R^3}\right)
$$

#### 从电荷密度到总[电荷](@entry_id:275494)

一旦我们通过[高斯定律的微分形式](@entry_id:191832)求得了[电荷密度](@entry_id:144672) $\rho$，就可以通过对该密度在特定体积内进行积分来计算总[电荷](@entry_id:275494)。例如，假设在一个特殊材料块中，测得[电场的散度](@entry_id:272995)为 $\nabla \cdot \vec{E} = \alpha z^2$ [@problem_id:1583482]。这意味着该材料内部的[电荷密度](@entry_id:144672)为 $\rho = \epsilon_0 \alpha z^2$。要计算一个尺寸为 $W \times D \times H$ 的矩形块内的总[电荷](@entry_id:275494) $Q$，我们需要对该体积进行积分：
$$
Q = \int_V \rho \, d\tau = \int_0^W dx \int_0^D dy \int_0^H (\epsilon_0 \alpha z^2) \, dz
$$
这是一个简单的[三重积分](@entry_id:183331)：
$$
Q = \epsilon_0 \alpha \left(\int_0^W dx\right) \left(\int_0^D dy\right) \left(\int_0^H z^2 \, dz\right) = \epsilon_0 \alpha (W)(D)\left[\frac{z^3}{3}\right]_0^H = \frac{\epsilon_0 \alpha W D H^3}{3}
$$

### 点电荷与狄拉克 $\delta$ 函数

[高斯定律的微分形式](@entry_id:191832)在处理[连续电荷分布](@entry_id:270971)时非常自然，但对于像点电荷这样的[奇异分布](@entry_id:265958)，则会遇到困难。一个位于原点的[点电荷](@entry_id:263616) $q$ 产生的[电场](@entry_id:194326)是库仑场：
$$
\vec{E}(\vec{r}) = \frac{1}{4\pi\epsilon_0} \frac{q}{r^2} \hat{r}
$$
如果我们尝试在 $r>0$ 的任意点计算这个场的散度，会得到：
$$
\nabla \cdot \vec{E} = \frac{1}{r^2} \frac{d}{dr} \left(r^2 \cdot \frac{q}{4\pi\epsilon_0 r^2}\right) = \frac{1}{r^2} \frac{d}{dr} \left(\frac{q}{4\pi\epsilon_0}\right) = 0
$$
这似乎导出了一个悖论：在 $r>0$ 的区域，电荷密度为零，但我们明明知道在原点有一个[电荷](@entry_id:275494)。这是否意味着[高斯定律的微分形式](@entry_id:191832)失效了？

答案是否定的。问题在于[点电荷](@entry_id:263616)的密度在原点是无限大，而在其他任何地方都是零。常规的函数无法描述这种行为。为了在[微分](@entry_id:158718)框架下正确处理点电荷，我们需要引入一种特殊的数学工具：**狄拉克 $\delta$ 函数**。三维的 $\delta$ 函数 $\delta^{(3)}(\vec{r})$ 被定义为具有以下性质的“函数”：
1.  当 $\vec{r} \neq \vec{0}$ 时, $\delta^{(3)}(\vec{r}) = 0$。
2.  $\int_V \delta^{(3)}(\vec{r}) \, d\tau = 1$，如果积分体积 $V$ 包含原点；否则积分为0。

[点电荷](@entry_id:263616) $q$ 在原点的电荷密度可以精确地表示为 $\rho(\vec{r}) = q \delta^{(3)}(\vec{r})$。现在，[高斯定律的微分形式](@entry_id:191832) $\nabla \cdot \vec{E} = \rho/\epsilon_0$ 应该可以容纳这种奇异性。通过结合积分形式和[散度定理](@entry_id:143110)，我们可以确认点电荷[电场的散度](@entry_id:272995) [@problem_id:1611345]：
$$
\nabla \cdot \left(\frac{1}{4\pi\epsilon_0} \frac{q}{r^2} \hat{r}\right) = \frac{q}{\epsilon_0} \delta^{(3)}(\vec{r})
$$
这个表达式完美地解决了悖论。它告诉我们，[点电荷](@entry_id:263616)[电场的散度](@entry_id:272995)在所有 $r>0$ 的地方都为零，但在原点处是一个无穷大的尖峰，其强度恰好对应于那里的点电荷。

这个概念对于理解更复杂的物理模型至关重要。例如，在一个原子中，[原子核](@entry_id:167902)可以被看作一个[点电荷](@entry_id:263616)，而周围环绕着负[电荷](@entry_id:275494)云。这种[电荷](@entry_id:275494)云会“屏蔽”[原子核](@entry_id:167902)的[电场](@entry_id:194326)。一个描述这种屏蔽效应的简化[电场](@entry_id:194326)模型由以下形式给出 [@problem_id:1583466]：
$$
\vec{E}(\vec{r}) = \frac{Ze}{4\pi\epsilon_0 r^2} \exp\left(-\frac{\alpha r}{Z}\right) \hat{r}
$$
对于 $r>0$，我们可以计算这个场的散度来找出连续[电荷](@entry_id:275494)云的密度 $\rho_{\text{cloud}}(r)$：
$$
\nabla \cdot \vec{E} = -\frac{\alpha e}{4\pi r^2} \exp\left(-\frac{\alpha r}{Z}\right)
$$
因此，$\rho_{\text{cloud}}(r) = \epsilon_0 (\nabla \cdot \vec{E}) = -\frac{\alpha e}{4\pi r^2} \exp(-\frac{\alpha r}{Z})$。这个密度是负的，代表了电子云。完整的[电荷密度](@entry_id:144672)是这个连续的负[电荷](@entry_id:275494)云与位于原点的正点电荷之和：
$$
\rho_{\text{total}}(\vec{r}) = Ze \delta^{(3)}(\vec{r}) - \frac{\alpha e}{4\pi r^2} \exp\left(-\frac{\alpha r}{Z}\right)
$$

### 与[静电势](@entry_id:188370)的关系：[泊松方程](@entry_id:143763)与[拉普拉斯方程](@entry_id:143689)

[静电场](@entry_id:268546)的一个基本性质是它是**保守场**，这意味着它可以表示为一个标量函数（即**[静电势](@entry_id:188370)** $V$）的负梯度：
$$
\vec{E} = -\nabla V
$$
将这个关系代入[高斯定律的微分形式](@entry_id:191832) $\nabla \cdot \vec{E} = \rho/\epsilon_0$，我们得到：
$$
\nabla \cdot (-\nabla V) = -\nabla^2 V = \frac{\rho}{\epsilon_0}
$$
整理后得到**[泊松方程](@entry_id:143763)** (Poisson's equation)：
$$
\nabla^2 V = -\frac{\rho}{\epsilon_0}
$$
其中 $\nabla^2 = \nabla \cdot \nabla$ 是**拉普拉斯算子**。在笛卡尔坐标系下，$\nabla^2 V = \frac{\partial^2 V}{\partial x^2} + \frac{\partial^2 V}{\partial y^2} + \frac{\partial^2 V}{\partial z^2}$。泊松方程是[静电学](@entry_id:140489)中最核心的方程之一，它直接将[电势](@entry_id:267554)与其源（[电荷密度](@entry_id:144672)）联系起来。

在一个没有[电荷](@entry_id:275494)的区域（$\rho = 0$），[泊松方程](@entry_id:143763)简化为**拉普拉斯方程** (Laplace's equation)：
$$
\nabla^2 V = 0
$$
满足拉普拉斯方程的函数被称为**调和函数**。一个重要的推论是，即使在一个无[电荷](@entry_id:275494)的区域，[电势](@entry_id:267554)和[电场](@entry_id:194326)也未必为零。这些非零的场是由该区域*外部*的[电荷](@entry_id:275494)产生的。例如，考虑由 $V(x, y, z) = -k(x^2 + y^2 - 2z^2)$ 描述的[电势](@entry_id:267554) [@problem_id:1583445]。我们可以通过计算它的拉普拉斯算子来确定产生它的电荷密度：
$$
\frac{\partial^2 V}{\partial x^2} = -2k, \quad \frac{\partial^2 V}{\partial y^2} = -2k, \quad \frac{\partial^2 V}{\partial z^2} = 4k
$$
$$
\nabla^2 V = -2k - 2k + 4k = 0
$$
由于 $\nabla^2 V = 0$，根据泊松方程，我们立即得出该区域的电荷密度 $\rho = -\epsilon_0 \nabla^2 V = 0$。这意味着这个复杂的、随空间变化的[电场](@entry_id:194326)是由位于我们所考虑区域之外的[电荷](@entry_id:275494)配置所产生的。

### [电介质](@entry_id:147163)中的场：极化与[电位移场](@entry_id:273493)

到目前为止，我们的讨论都局限在真空中。当[电场](@entry_id:194326)存在于**[电介质](@entry_id:147163)**（如玻璃、水或塑料）中时，物质本身会对[电场](@entry_id:194326)做出响应。在外[电场](@entry_id:194326)作用下，介质中原子的正负[电荷中心](@entry_id:267066)会发生微小分离，或者固有极性分子会发生取向，从而在宏观上产生一个净**[电偶极矩](@entry_id:178520)密度**，我们称之为**极化强度** $\vec{P}$。

这种极化会在介质内部和表面产生净[电荷](@entry_id:275494)，即**束缚[电荷](@entry_id:275494)**。束缚[电荷](@entry_id:275494)的体密度 $\rho_b$ 与[极化强度](@entry_id:188176)的关系为 [@problem_id:1592217]：
$$
\rho_b = -\nabla \cdot \vec{P}
$$
这个关系的直观理解是：如果[极化矢量](@entry_id:269389)场在某区域汇聚（散度为负），就会有更多的偶极子正端指向该区域，从而累积起净的正束缚[电荷](@entry_id:275494)。

在介质中，总电荷密度 $\rho_{\text{total}}$ 是**自由电荷**密度 $\rho_f$（例如，导体中可移动的电子或[掺杂半导体](@entry_id:145553)中的载流子）和束缚[电荷密度](@entry_id:144672) $\rho_b$ 的和。因此，微观[高斯定律](@entry_id:141493)应写为：
$$
\nabla \cdot \vec{E} = \frac{\rho_{\text{total}}}{\epsilon_0} = \frac{\rho_f + \rho_b}{\epsilon_0}
$$
将 $\rho_b = -\nabla \cdot \vec{P}$ 代入，我们得到：
$$
\nabla \cdot \vec{E} = \frac{\rho_f - \nabla \cdot \vec{P}}{\epsilon_0}
$$
这个方程虽然精确，但将场的源与场对物质的响应（$\vec{P}$）混在了一起。为了简化问题，物理学家们将与场相关的项移到等式一边：
$$
\nabla \cdot \vec{E} + \frac{\nabla \cdot \vec{P}}{\epsilon_0} = \frac{\rho_f}{\epsilon_0} \implies \nabla \cdot (\epsilon_0 \vec{E} + \vec{P}) = \rho_f
$$
括号内的项被定义为一个新的辅助矢量场，称为**[电位移场](@entry_id:273493)** $\vec{D}$：
$$
\vec{D} \equiv \epsilon_0 \vec{E} + \vec{P}
$$
于是，我们得到了**宏观[高斯定律](@entry_id:141493)**：
$$
\nabla \cdot \vec{D} = \rho_f
$$
这个形式非常有用，因为它表明[电位移场](@entry_id:273493) $\vec{D}$ 的源*仅仅*是[自由电荷](@entry_id:264392)。束缚[电荷](@entry_id:275494)的影响已经被隐含地包含在 $\vec{D}$ 的定义中了。因此，在处理[电介质](@entry_id:147163)问题时，如果我们只关心由自由电荷产生的场，使用 $\vec{D}$ 会方便得多。

例如，假设在一种特殊介质中，我们测得其[电位移场](@entry_id:273493)为 $\vec{D} = \alpha r \cos(\theta) \hat{r} + \beta r \sin(\theta) \hat{\theta}$ [@problem_id:1583463]。要找到[自由电荷](@entry_id:264392)密度，我们只需计算 $\vec{D}$ 的散度（在[球坐标](@entry_id:146054)中）：
$$
\rho_f = \nabla \cdot \vec{D} = \frac{1}{r^2}\frac{\partial}{\partial r}(r^2 D_r) + \frac{1}{r\sin\theta}\frac{\partial}{\partial \theta}(\sin\theta D_\theta)
$$
计算后可得 $\rho_f = (3\alpha + 2\beta)\cos(\theta)$。
类似地，如果已知[材料的极化](@entry_id:271610)强度 $\vec{P}$，我们可以通过计算其散度的负值来找到束缚[电荷](@entry_id:275494)的[分布](@entry_id:182848) [@problem_id:14189]。

### 边界上的[不连续性](@entry_id:144108)

[微分形式](@entry_id:146747)的定律在场函数连续可微的点上成立。然而，在不同介质的交界面或存在面[电荷](@entry_id:275494)的地方，[电场](@entry_id:194326)可能会发生突变。我们可以通过将微分形式在跨越界面的一个无穷小“药丸盒”体积上积分，来推导场在边界上的行为。

考虑一个带有面[电荷密度](@entry_id:144672) $\sigma$ 的表面。将 $\nabla \cdot \vec{E} = \rho/\epsilon_0$ 在一个穿过该表面的微小圆柱体（“药丸盒”）上积分，并应用[散度定理](@entry_id:143110)，当圆柱体的高度趋于零时，可以得到**[电场](@entry_id:194326)法向分量的边界条件**：
$$
\vec{E}_{2,\perp} - \vec{E}_{1,\perp} = \frac{\sigma}{\epsilon_0}
$$
其中 $\vec{E}_{1,\perp}$ 和 $\vec{E}_{2,\perp}$ 是紧邻界面两侧的[电场](@entry_id:194326)沿[法线](@entry_id:167651)方向的分量（从区域1指向区域2）。这表明，[电场](@entry_id:194326)的法向分量在穿过一个面[电荷](@entry_id:275494)层时是不连续的，其跳变量正好是 $\sigma/\epsilon_0$。

我们可以用一个分段定义的[电场](@entry_id:194326)来阐明这一点 [@problem_id:1583480]。假设[电场](@entry_id:194326)为：
$$
\vec{E}(\vec{r}) = \begin{cases} (A z + B) \hat{k} & \text{for } z > 0 \\ C \hat{k} & \text{for } z  0 \end{cases}
$$
在 $z>0$ 的区域，$\rho^+ = \epsilon_0 \nabla \cdot \vec{E} = \epsilon_0 \frac{\partial}{\partial z}(Az+B) = \epsilon_0 A$。
在 $z0$ 的区域，$\rho^- = \epsilon_0 \nabla \cdot \vec{E} = \epsilon_0 \frac{\partial}{\partial z}(C) = 0$。
在 $z=0$ 的界面处，[电场](@entry_id:194326)的法向（$z$ 方向）分量从 $E_z(0^-)=C$ 跳变到 $E_z(0^+)=B$。根据边界条件，该界面上必定存在一个面[电荷密度](@entry_id:144672) $\sigma$：
$$
\sigma = \epsilon_0 (E_z(0^+) - E_z(0^-)) = \epsilon_0 (B - C)
$$
这个例子清楚地显示了[体电荷密度](@entry_id:264747)如何产生连续变化的[电场](@entry_id:194326)，而面电荷密度则导致[电场](@entry_id:194326)法向分量的阶跃式不连续。

### [静电场](@entry_id:268546)的一个必要条件：$\vec{E}$ 的旋度

高斯定律描述了[电场的散度](@entry_id:272995)特性，但它并非静电场的唯一约束。静电场是保守场，这意味着将一个[电荷](@entry_id:275494)沿任意闭合路径移动一圈，[电场](@entry_id:194326)做的功为零。数学上，这表示为[电场](@entry_id:194326)的[环路积分](@entry_id:164828)为零：
$$
\oint \vec{E} \cdot d\vec{l} = 0
$$
根据**[斯托克斯定理](@entry_id:264534)** (Stokes' theorem)，一个矢量场的[环路积分](@entry_id:164828)等于其**旋度**（curl）穿过该环路所围成[曲面](@entry_id:267450)的通量。因此，上述条件等价于：
$$
\nabla \times \vec{E} = \vec{0}
$$
这个方程是静电学的另一个基本定律（它是法拉第[电磁感应](@entry_id:181154)定律在静态情况下的特例）。它意味着[静电场](@entry_id:268546)是一个**[无旋场](@entry_id:183486)**。

因此，一个矢量场要成为一个合法的、物理上可能的**[静电场](@entry_id:268546)**，它必须**同时满足**两个[微分方程](@entry_id:264184)：
1.  $\nabla \cdot \vec{E} = \rho / \epsilon_0$ (有源性)
2.  $\nabla \times \vec{E} = \vec{0}$ (无旋性)

仅仅满足其中一个是不够的。例如，考虑一个假设的场 $\vec{E} = C(y \hat{x} - x \hat{y})$ [@problem_id:1583459]。让我们来检验它是否满足这两个条件。首先是散度：
$$
\nabla \cdot \vec{E} = \frac{\partial(Cy)}{\partial x} + \frac{\partial(-Cx)}{\partial y} = 0 + 0 = 0
$$
它的散度为零，这与一个无[电荷](@entry_id:275494)的区域是相符的。但是，它的旋度呢？
$$
\nabla \times \vec{E} = \left(\frac{\partial E_y}{\partial x} - \frac{\partial E_x}{\partial y}\right)\hat{z} = \left(\frac{\partial(-Cx)}{\partial x} - \frac{\partial(Cy)}{\partial y}\right)\hat{z} = (-C - C)\hat{z} = -2C\hat{z}
$$
只要 $C \neq 0$，这个场的旋度就不为零。因此，尽管它满足无源区域的高斯定律，但它**不能**代表一个[静电场](@entry_id:268546)。这样的一个场实际上与一个随时间变化的[磁场](@entry_id:153296)有关（根据完整的法拉第定律 $\nabla \times \vec{E} = -\partial \vec{B}/\partial t$）。这个例子强调了区分静电学和完整[电动力学](@entry_id:158759)的重要性，并突显了[高斯定律](@entry_id:141493)微分形式在整个电磁理论框架中的位置。