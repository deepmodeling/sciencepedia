## 引言
矢量微积分是描述物理世界中场的语言，尤其在电动力学领域，它扮演着不可或缺的角色。从[电荷](@entry_id:275494)周围的静电场到宇宙中的[磁场](@entry_id:153296)，矢量微积分提供了一套精确而优雅的工具来刻画它们的行为与相互作用。然而，学生们在学习过程中常常只关注于记忆抽象的数学公式，而忽略了这些恒等式背后深刻的物理内涵及其在解决实际问题中的强大威力。本文旨在填补这一鸿沟，将抽象的数学与生动的物理图像联系起来。

本文将分为三个部分，引领读者逐步深入矢量微积分的世界。在第一章“原理与机制”中，我们将系统地介绍[梯度、散度、旋度](@entry_id:269893)等基本算符，以及高斯定理和[斯托克斯定理](@entry_id:264534)等核心积分法则，并揭示它们之间内在的恒等关系。随后的“应用与跨学科联系”章节将展示这些工具的威力，看它们如何构建起宏伟的麦克斯韦理论大厦，并延伸至[流体力学](@entry_id:136788)、凝聚态物理等多个前沿领域。最后，通过“动手实践”中的具体问题，您将有机会亲自运用所学知识，巩固理解。

现在，让我们从最基础的概念开始，深入探索矢量场的微积分。

## 原理与机制

本章在前一章介绍矢量概念的基础上，深入探讨矢量场的微积分。矢量微积分是电动力学的数学基石，它不仅为麦克斯韦方程组提供了简洁而深刻的表述语言，也揭示了[电磁场](@entry_id:265881)内在的结构与对称性。我们将系统地介绍梯度、[散度和旋度](@entry_id:270881)等基本[微分](@entry_id:158718)算符，阐述[高斯散度定理](@entry_id:188065)和[斯托克斯定理](@entry_id:264534)这两个核心[积分定理](@entry_id:183680)，并最终展示这些数学工具如何被用于推导物理学中的一些基本结论，如[势函数](@entry_id:176105)的存在性、[泊松方程](@entry_id:143763)[解的唯一性](@entry_id:143619)以及[亥姆霍兹分解](@entry_id:181767)的正交性。

### 矢量场的[微分](@entry_id:158718)：梯度、[散度和旋度](@entry_id:270881)

描述物理现象的场可以是标量场（如温度或势能），也可以是矢量场（如[电场](@entry_id:194326)或流速场）。矢量微积分提供了一套工具来描述这些场在空间中的变化规律。核心是**del算符** $\nabla$，它在笛卡尔坐标系下定义为：
$$
\nabla = \hat{x}\frac{\partial}{\partial x} + \hat{y}\frac{\partial}{\partial y} + \hat{z}\frac{\partial}{\partial z}
$$
$\nabla$ 算符本身不是一个矢量，而是一个矢量[微分](@entry_id:158718)算符，它可以作用于[标量场](@entry_id:151443)或矢量场，产生新的物理上有意义的场。

#### 梯度 (Gradient)

当 $\nabla$ 算符作用于一个标量场 $f(x, y, z)$ 时，其结果是一个矢量场，称为 $f$ 的**梯度 (gradient)**，记作 $\nabla f$。
$$
\nabla f = \frac{\partial f}{\partial x}\hat{x} + \frac{\partial f}{\partial y}\hat{y} + \frac{\partial f}{\partial z}\hat{z}
$$
梯度的方向指向标量场 $f$ 增加最快的方向，其大小表示该方向上的变化率。在物理学中，许多[力场](@entry_id:147325)都是保守场，可以表示为某个势能[标量场](@entry_id:151443) $U$ 的负梯度，即 $\mathbf{F} = -\nabla U$。同样，静电场 $\mathbf{E}$ 也是一个保守场，可以由[电势](@entry_id:267554) $V$ 得到：$\mathbf{E} = -\nabla V$。

一个在[静电学](@entry_id:140489)和[引力](@entry_id:175476)理论中反复出现的关键函数是[点源](@entry_id:196698)势，它与到源点的距离 $r$ 的倒数成正比。计算 $1/r$ 的梯度是许多问题的起点。设 $r = |\mathbf{r}| = \sqrt{x^2+y^2+z^2}$，我们来计算 $\nabla(1/r)$ [@problem_id:1629456]。运用链式法则，我们对 $x$ 分量求导：
$$
\frac{\partial}{\partial x}\left(\frac{1}{r}\right) = \frac{\partial}{\partial x}(x^2+y^2+z^2)^{-1/2} = -\frac{1}{2}(x^2+y^2+z^2)^{-3/2}(2x) = -\frac{x}{r^3}
$$
对 $y$ 和 $z$ 分量进行类似计算，得到：
$$
\nabla\left(\frac{1}{r}\right) = -\frac{x}{r^3}\hat{x} - \frac{y}{r^3}\hat{y} - \frac{z}{r^3}\hat{z} = -\frac{\mathbf{r}}{r^3}
$$
由于径向单位矢量 $\hat{\mathbf{r}} = \mathbf{r}/r$，这个重要的结果可以更简洁地写为：
$$
\nabla\left(\frac{1}{r}\right) = -\frac{\hat{\mathbf{r}}}{r^2}
$$
这个恒等式表明，一个与 $1/r$ 成正比的标量势（如[点电荷的电势](@entry_id:188444)）所对应的矢量场（[电场](@entry_id:194326)）是一个沿径向向外且强度按 $1/r^2$ 规律衰减的场。

梯度算符是线性算符，这意味着 $\nabla(f+g) = \nabla f + \nabla g$。这个性质是[电场](@entry_id:194326)叠加原理的数学基础。如果一个[电势](@entry_id:267554)由多个部分组成，例如 $V = V_1 + V_2$，那么总[电场](@entry_id:194326)就是各个分[电场](@entry_id:194326)的矢量和，$\mathbf{E} = -\nabla(V_1+V_2) = -\nabla V_1 - \nabla V_2 = \mathbf{E}_1 + \mathbf{E}_2$ [@problem_id:1629503]。

#### 散度 (Divergence)

当 $\nabla$ 算符与一个矢量场 $\mathbf{F}$ 作[点积](@entry_id:149019)时，其结果是一个[标量场](@entry_id:151443)，称为 $\mathbf{F}$ 的**散度 (divergence)**，记作 $\nabla \cdot \mathbf{F}$。
$$
\nabla \cdot \mathbf{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}
$$
散度衡量了矢量场在某一点的“源”或“汇”的强度。正散度表示该点是场的源头（如正[电荷](@entry_id:275494)），矢量线从该点向外发散；负散度表示该点是场的汇点（如负[电荷](@entry_id:275494)）。如果一个矢量场的散度处处为零，$\nabla \cdot \mathbf{F} = 0$，则称该场为**[螺线场](@entry_id:260932) (solenoidal field)** 或[无散场](@entry_id:260932)。这种场没有源或汇，其[场线](@entry_id:172226)必须是闭合的回路或从无穷远处来、到无穷远处去。

一个重要的例子是[磁场](@entry_id:153296) $\mathbf{B}$。根据麦克斯韦方程组之一（[高斯磁定律](@entry_id:182942)），$\nabla \cdot \mathbf{B} = 0$。这表明不存在磁单极子——即独立的磁“北极”或“南极”。

我们可以通过一个假设的例子来理解散度的物理含义。设想一个理论上存在的[磁场](@entry_id:153296) $\mathbf{B}(\mathbf{r}) = k\mathbf{r}$，其中 $k$ 是常数 [@problem_id:1629481]。这个场的散度是：
$$
\nabla \cdot \mathbf{B} = \nabla \cdot (k\mathbf{r}) = k \left(\frac{\partial x}{\partial x} + \frac{\partial y}{\partial y} + \frac{\partial z}{\partial z}\right) = 3k
$$
由于其散度不为零，这个场在物理上不可能是真实的[磁场](@entry_id:153296)，因为它违反了 $\nabla \cdot \mathbf{B} = 0$ 的基本定律。非零的散度意味着空间中每一点都是[磁场](@entry_id:153296)的“源”，这与[磁场](@entry_id:153296)线必须形成闭合回路的实验事实相矛盾。

#### 旋度 (Curl)

当 $\nabla$ 算符与一个矢量场 $\mathbf{F}$ 作[叉积](@entry_id:156672)时，其结果是另一个矢量场，称为 $\mathbf{F}$ 的**旋度 (curl)**，记作 $\nabla \times \mathbf{F}$。
$$
\nabla \times \mathbf{F} = \left(\frac{\partial F_z}{\partial y} - \frac{\partial F_y}{\partial z}\right)\hat{x} + \left(\frac{\partial F_x}{\partial z} - \frac{\partial F_z}{\partial x}\right)\hat{y} + \left(\frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y}\right)\hat{z}
$$
旋度衡量了矢量场在某一点周围的“环流”或“涡旋”的程度。旋度矢量的方向是环流最强的平面的[法线](@entry_id:167651)方向（遵循[右手定则](@entry_id:156766)），其大小[表示环](@entry_id:136421)流的强度。如果一个[矢量场的旋度](@entry_id:146155)处处为零，$\nabla \times \mathbf{F} = \mathbf{0}$，则称该场为**[无旋场](@entry_id:183486) (irrotational field)** 或**保守场 (conservative field)**。静电场就是一个典型的[无旋场](@entry_id:183486)，其基本性质由麦克斯韦方程 $\nabla \times \mathbf{E} = \mathbf{0}$ 决定。一个场是保守的，意味着可以将它表示为某个标量势的梯度。

让我们考察一个假设的[电场](@entry_id:194326) $\mathbf{E}(x, y, z) = \alpha (y \hat{x} - x \hat{y})$，其中 $\alpha$ 为常数 [@problem_id:1629452]。这个场的旋度为：
$$
\nabla \times \mathbf{E} = \left(\frac{\partial E_y}{\partial x} - \frac{\partial E_x}{\partial y}\right)\hat{z} = \left(\frac{\partial (-\alpha x)}{\partial x} - \frac{\partial (\alpha y)}{\partial y}\right)\hat{z} = (-\alpha - \alpha)\hat{z} = -2\alpha \hat{z}
$$
由于旋度不为零，这个场不是一个[静电场](@entry_id:268546)。它具有恒定的涡旋特性，围绕 z 轴旋转。这种场无法由一个标量[电势](@entry_id:267554) $V$ 导出，因为它不是[保守场](@entry_id:137555)。在[电动力学](@entry_id:158759)中，变化的[磁场](@entry_id:153296)可以产生这种有旋的[电场](@entry_id:194326)，这是法拉第电磁感应定律的体现。

### 矢量[积分定理](@entry_id:183680)

[积分定理](@entry_id:183680)建立了[微分](@entry_id:158718)算符（如[散度和旋度](@entry_id:270881)）的局部行为与矢量场在有限区域或边界上的积分行为之间的深刻联系。

#### [散度定理](@entry_id:143110) (Divergence Theorem)

**[高斯散度定理](@entry_id:188065) (Gauss's Divergence Theorem)** 指出，一个矢量场 $\mathbf{F}$ 通过一个封闭[曲面](@entry_id:267450) $S$ 的总通量，等于该场的散度在 $S$所包围的体积 $V$ 内的[体积分](@entry_id:171119)。
$$
\oint_S \mathbf{F} \cdot d\mathbf{A} = \int_V (\nabla \cdot \mathbf{F}) dV
$$
这里 $d\mathbf{A}$ 是指向[曲面](@entry_id:267450)外部的面积元矢量。该定理的直观意义是：一个区域内部所有源（和汇）的总和，等于流出（或流入）该区域边界的总流量。

散度定理的一个直接而重要的应用是证明通过任意闭合[曲面](@entry_id:267450)的[磁通量](@entry_id:268943)恒为零 [@problem_id:1629469]。磁通量 $\Phi_B$ 定义为 $\Phi_B = \oint_S \mathbf{B} \cdot d\mathbf{A}$。根据散度定理，我们可以将其转化为[体积分](@entry_id:171119)：
$$
\Phi_B = \oint_S \mathbf{B} \cdot d\mathbf{A} = \int_V (\nabla \cdot \mathbf{B}) dV
$$
由于[高斯磁定律](@entry_id:182942)指出 $\nabla \cdot \mathbf{B} = 0$，上式右边的被积函数恒为零，因此积分结果也为零。
$$
\Phi_B = \int_V 0 \, dV = 0
$$
这个结果与[曲面](@entry_id:267450)形状和大小无关，它从根本上反映了[磁场](@entry_id:153296)是[无源场](@entry_id:178017)这一事实。我们也可以用散度定理来验证前面提到的假设场 $\mathbf{B} = k\mathbf{r}$ 会产生非零磁通量，这再次证明了其非物理性 [@problem_id:1629481]。

#### 斯托克斯定理 (Stokes' Theorem)

**[斯托克斯定理](@entry_id:264534)**指出，一个矢量场 $\mathbf{F}$ 沿一个闭合路径 $C$ 的[线积分](@entry_id:141417)（环流），等于该场的旋度通过以 $C$ 为边界的任意[曲面](@entry_id:267450) $S$ 的通量。
$$
\oint_C \mathbf{F} \cdot d\mathbf{l} = \int_S (\nabla \times \mathbf{F}) \cdot d\mathbf{A}
$$
路径 $C$ 的方向和[曲面](@entry_id:267450)法向 $d\mathbf{A}$ 的方向由右手定则关联。该定理的直观意义是：一个[曲面](@entry_id:267450)上所有微小涡旋的总和，等于该[曲面](@entry_id:267450)边界上的总环流量。

斯托克斯定理为[静电场](@entry_id:268546)的保守性提供了最根本的物理解释 [@problem_id:1629495]。在[静电学](@entry_id:140489)中，[电场](@entry_id:194326)力对一个[电荷](@entry_id:275494) $q$ 沿闭合路径 $C$ 做的功为 $W = q \oint_C \mathbf{E} \cdot d\mathbf{l}$。根据[斯托克斯定理](@entry_id:264534)，这个线积分可以转化为[面积分](@entry_id:275394)：
$$
W = q \int_S (\nabla \times \mathbf{E}) \cdot d\mathbf{A}
$$
对于任何静电场，[麦克斯韦方程组](@entry_id:150940)中的[法拉第定律](@entry_id:149836)静态形式给出 $\nabla \times \mathbf{E} = \mathbf{0}$。因此，被积函数恒为零，功也恒为零：
$$
W = q \int_S \mathbf{0} \cdot d\mathbf{A} = 0
$$
这个结论对任意闭合路径都成立，它表明[静电场](@entry_id:268546)力做功与路径无关，这正是保守场的定义。这也是为什么可以引入一个标量[电势](@entry_id:267554) $V$ 使得 $\mathbf{E} = -\nabla V$ 的根本原因。

### 二阶[微分](@entry_id:158718)算符与[亥姆霍兹定理](@entry_id:275687)

通过组合梯度、[散度和旋度](@entry_id:270881)，我们可以构造二阶[微分](@entry_id:158718)算符，它们揭示了矢量场更深层次的结构。

#### [二阶导数](@entry_id:144508)恒等式

有两个恒等式在矢量分析中至关重要，因为它们的结果恒为零：
1.  **[梯度的旋度](@entry_id:274168)恒为零 (Curl of Gradient is Zero):** $\nabla \times (\nabla f) = \mathbf{0}$。
    这个恒等式表明，任何可以表示为标量场梯度的矢量场（即[保守场](@entry_id:137555)）必定是[无旋场](@entry_id:183486)。这为“$\mathbf{E}=-\nabla V$”与“$\nabla \times \mathbf{E} = \mathbf{0}$”之间提供了直接的数学联系。

2.  **[旋度的散度](@entry_id:271562)恒为零 (Divergence of Curl is Zero):** $\nabla \cdot (\nabla \times \mathbf{F}) = 0$。
    这个恒等式表明，任何可以表示为另一个矢量场旋度的矢量场必定是[无散场](@entry_id:260932)（[螺线场](@entry_id:260932)）。这解释了为什么[磁场](@entry_id:153296) $\mathbf{B}$ 可以用矢量势 $\mathbf{A}$ 表示为 $\mathbf{B} = \nabla \times \mathbf{A}$，因为这自动满足了 $\nabla \cdot \mathbf{B} = 0$ 的物理要求。

另一个关键的二阶算符是**拉普拉斯算符 (Laplacian)**, $\nabla^2$。作用于标量场 $f$ 时，它定义为[梯度的散度](@entry_id:270716)：
$$
\nabla^2 f = \nabla \cdot (\nabla f) = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} + \frac{\partial^2 f}{\partial z^2}
$$
在[静电学](@entry_id:140489)中，将 $\mathbf{E} = -\nabla V$ 代入[高斯定律](@entry_id:141493) $\nabla \cdot \mathbf{E} = \rho / \epsilon_0$，我们得到**泊松方程 (Poisson's equation)**: $\nabla^2 V = -\rho / \epsilon_0$。在没有[电荷](@entry_id:275494)的区域（$\rho = 0$），该方程简化为**[拉普拉斯方程](@entry_id:143689) (Laplace's equation)**: $\nabla^2 V = 0$ [@problem_id:1629464]。这个方程是解决大量[静电边值问题](@entry_id:276026)的基础。

一个特别值得关注的计算是 $\nabla^2(1/r)$。在 $r \neq 0$ 的区域，直接计算表明 $\nabla^2(1/r) = 0$。然而，在原点 $r=0$ 处存在奇异性。我们可以通过散度定理来探究其本质。考虑一个以原点为中心的半径为 $R$ 的球面 $S$，计算场 $\mathbf{F} = \nabla(1/r)$ 通过该球面的通量 [@problem_id:1629430]：
$$
\Phi = \oint_S \nabla\left(\frac{1}{r}\right) \cdot d\mathbf{A} = \int_V \nabla^2\left(\frac{1}{r}\right) dV
$$
直接在球面上计算通量，我们已经知道 $\nabla(1/r) = -\hat{\mathbf{r}}/r^2$。在半径为 $R$ 的球面上，$r=R$，向外的面积元是 $d\mathbf{A} = \hat{\mathbf{r}} dA$。因此，
$$
\Phi = \oint_S \left(-\frac{\hat{\mathbf{r}}}{R^2}\right) \cdot (\hat{\mathbf{r}} dA) = -\frac{1}{R^2} \oint_S dA = -\frac{1}{R^2} (4\pi R^2) = -4\pi
$$
这个结果 $-4\pi$ 是一个常数，与半径 $R$ 无关。这意味着[体积分](@entry_id:171119) $\int_V \nabla^2(1/r) dV$ 总是 $-4\pi$，无论体积多小，只要它包含原点。这表明 $\nabla^2(1/r)$ 在 $r \neq 0$ 时为零，但在 $r=0$ 处是一个具有积分值为 $-4\pi$ 的无穷大的“尖峰”。这种行为在数学上用狄拉克 $\delta$ 函数描述：$\nabla^2(1/r) = -4\pi \delta(\mathbf{r})$。

对于矢量场，也存在**矢量[拉普拉斯算符](@entry_id:146319)**，它与其它[二阶导数](@entry_id:144508)通过以下重要恒等式联系起来：
$$
\nabla \times (\nabla \times \mathbf{F}) = \nabla(\nabla \cdot \mathbf{F}) - \nabla^2 \mathbf{F}
$$
这个恒等式在[电磁波](@entry_id:269629)理论和[流体力学](@entry_id:136788)中非常有用，它将一个场的环流的环流（左侧）分解为与其源相关的部分和与其自身[分布](@entry_id:182848)平滑度相关的部分（右侧）[@problem_id:1629480]。

#### [亥姆霍兹定理](@entry_id:275687)及其推论

**[亥姆霍兹定理](@entry_id:275687) (Helmholtz's Theorem)** 是矢量分析的中心定理之一。它指出，在全空间中，任何表现良好（在无穷远处足够快地衰减）的矢量场 $\mathbf{F}$ 都可以唯一地分解为一个无旋部分 $\mathbf{F}_{ir}$ 和一个无散部分 $\mathbf{F}_{sol}$ 的和：
$$
\mathbf{F} = \mathbf{F}_{ir} + \mathbf{F}_{sol}
$$
其中 $\nabla \times \mathbf{F}_{ir} = \mathbf{0}$ 且 $\nabla \cdot \mathbf{F}_{sol} = \mathbf{0}$。根据我们之前的恒等式，这意味着无旋部分可以写成标量势 $\phi$ 的梯度 ($\mathbf{F}_{ir} = -\nabla \phi$)，而无散部分可以写成矢量势 $\mathbf{A}$ 的旋度 ($\mathbf{F}_{sol} = \nabla \times \mathbf{A}$)。因此，任何矢量场都可以表示为：
$$
\mathbf{F} = -\nabla \phi + \nabla \times \mathbf{A}
$$
这个定理为我们使用[标量势和矢量势](@entry_id:266240)来描述[电场和磁场](@entry_id:261347)提供了坚实的数学基础。

**推论1：规范自由度 (Gauge Freedom)**
势的定义不是唯一的。例如，对于[磁矢量势](@entry_id:141246) $\mathbf{A}$，我们知道 $\mathbf{B} = \nabla \times \mathbf{A}$。如果我们用一个新的势 $\mathbf{A}' = \mathbf{A} + \nabla \lambda$ 来替换 $\mathbf{A}$，其中 $\lambda$ 是任意[标量场](@entry_id:151443)，那么新的[磁场](@entry_id:153296)为：
$$
\mathbf{B}' = \nabla \times \mathbf{A}' = \nabla \times (\mathbf{A} + \nabla \lambda) = \nabla \times \mathbf{A} + \nabla \times (\nabla \lambda)
$$
由于[梯度的旋度](@entry_id:274168)恒为零，$\nabla \times (\nabla \lambda) = \mathbf{0}$，因此 $\mathbf{B}' = \mathbf{B}$。这意味着可以有无穷多个不同的矢量势（例如 $\mathbf{A}_1$ 和 $\mathbf{A}_2$）产生完全相同的[磁场](@entry_id:153296)。它们之间的差 $\mathbf{C} = \mathbf{A}_1 - \mathbf{A}_2$ 必须是一个[无旋场](@entry_id:183486)，因此可以表示为某个标量函数的梯度 [@problem_id:1629476]。这种选择不同[势函数](@entry_id:176105)而不改变物理场（$\mathbf{E}$ 和 $\mathbf{B}$）的自由度被称为**规范自由度**，它在现代物理学中扮演着核心角色。

**推论2：正交性与唯一性**
矢量恒等式和[积分定理](@entry_id:183680)的强大威力体现在证明一些深刻的物理定理上。
首先，[亥姆霍兹分解](@entry_id:181767)中的无旋部分和无散部分是**正交的**。这意味着在全空间积分中，它们的[点积](@entry_id:149019)为零 [@problem_id:1629462]。要证明这一点，我们计算积分 $I = \int_{\mathbb{R}^3} \mathbf{F}_{ir} \cdot \mathbf{F}_{sol} \, dV$。由于 $\mathbf{F}_{ir}$ 是[无旋场](@entry_id:183486)，我们可以写出 $\mathbf{F}_{ir} = \nabla \phi$。积分变为：
$$
I = \int_{\mathbb{R}^3} (\nabla \phi) \cdot \mathbf{F}_{sol} \, dV
$$
使用乘积法则 $\nabla \cdot (\phi \mathbf{F}_{sol}) = (\nabla \phi) \cdot \mathbf{F}_{sol} + \phi (\nabla \cdot \mathbf{F}_{sol})$，并利用 $\mathbf{F}_{sol}$ 是[无散场](@entry_id:260932)（$\nabla \cdot \mathbf{F}_{sol} = 0$）的性质，我们得到 $(\nabla \phi) \cdot \mathbf{F}_{sol} = \nabla \cdot (\phi \mathbf{F}_{sol})$。将此代入积分并应用[散度定理](@entry_id:143110)：
$$
I = \int_{\mathbb{R}^3} \nabla \cdot (\phi \mathbf{F}_{sol}) \, dV = \oint_{S_\infty} (\phi \mathbf{F}_{sol}) \cdot d\mathbf{A}
$$
由于场在无穷远处衰减为零，这个在无穷大[曲面](@entry_id:267450)上的积分也为零。因此，$I = 0$，证明了正交性。

其次，矢量恒等式可以用来证明**静电学[边值问题](@entry_id:193901)[解的唯一性](@entry_id:143619)**。假设对于给定的[电荷分布](@entry_id:144400) $\rho$ 和边界条件（例如，在闭合[曲面](@entry_id:267450) $S$ 上[电势](@entry_id:267554)为 $V_S$），存在两个不同的解 $V_1$ 和 $V_2$。我们定义差值势 $\psi = V_1 - V_2$ [@problem_id:1629443]。由于 $V_1$ 和 $V_2$ 都满足泊松方程 $\nabla^2 V = -\rho/\epsilon_0$，$\psi$ 必然满足拉普拉斯方程 $\nabla^2 \psi = 0$。在边界 $S$ 上，$\psi = V_1 - V_2 = V_S - V_S = 0$。现在考虑与 $\psi$ 相关的“差值[电场](@entry_id:194326)”$\mathbf{E}_\psi = -\nabla\psi$ 在体积 $V$ 内储存的能量：
$$
U_\psi = \frac{\epsilon_0}{2} \int_V |\mathbf{E}_\psi|^2 dV = \frac{\epsilon_0}{2} \int_V |\nabla \psi|^2 dV
$$
应用[格林第一恒等式](@entry_id:170345)（它本身是[散度定理](@entry_id:143110)和[乘积法则](@entry_id:158393)的推论），我们有：
$$
\int_V |\nabla \psi|^2 dV = \oint_S \psi (\nabla \psi) \cdot d\mathbf{A} - \int_V \psi (\nabla^2 \psi) dV
$$
由于边界上 $\psi=0$，[曲面积分](@entry_id:144805)为零。由于体积内 $\nabla^2\psi=0$，[体积分](@entry_id:171119)也为零。因此，$\int_V |\nabla \psi|^2 dV = 0$。因为被积函数 $|\nabla \psi|^2$ 是非负的，积分值为零的唯一可能是被积函数处处为零，即 $|\nabla \psi|^2 = 0$。这意味着 $\nabla \psi = \mathbf{0}$，所以 $\psi$ 在整个体积内是一个常数。又因为 $\psi$ 在边界上为零，所以这个常数必须是零。因此，$\psi = V_1 - V_2 = 0$ 处处成立，即 $V_1 = V_2$。这证明了在给定的边界条件下，[泊松方程](@entry_id:143763)的解是唯一的。这个强大的结论保证了[静电学](@entry_id:140489)问题的确定性，而其证明的核心，正是矢量微积分的恒等式与[积分定理](@entry_id:183680)。