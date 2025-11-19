## 引言
[麦克斯韦方程组](@entry_id:150940)是19世纪物理学的巅峰之作，它将电、磁、光现象完美地统一在一个自洽的理论框架内，构成了[经典电动力学](@entry_id:270496)的基石。这组优美而深刻的方程不仅解释了所有宏观电磁现象，其最重要的预言——[电磁波](@entry_id:269629)的存在——更是从根本上改变了我们对宇宙的认知，并直接催生了现代无线通信技术。然而，对于初学者而言，从抽象的矢量微积分方程到可感知的物理实在（如光）之间存在着概念上的鸿沟。本文旨在跨越这一鸿沟，系统性地阐述麦克斯韦方程组在真空中的内涵与应用。

在接下来的内容中，读者将踏上一段从基本原理到前沿应用的探索之旅。第一章“原理与机制”将深入剖析[方程组](@entry_id:193238)的每一项，揭示[电场](@entry_id:194326)与[磁场](@entry_id:153296)动态耦合的奥秘，并一步步推导出电磁[波动方程](@entry_id:139839)，见证光速如何从两个基本常数中诞生。第二章“应用与跨学科联系”将理论付诸实践，探讨[电磁波的能量](@entry_id:275250)、干涉、在[波导](@entry_id:198471)中的传播等具体现象，并展示麦克斯韦理论如何与[狭义相对论](@entry_id:275552)和量子物理等现代物理学分支紧密相连。最后，在“动手实践”部分，通过精选的计算练习，读者可以亲手验证理论、检验物理构型的可能性，从而将理论知识内化为解决问题的能力。通过这一结构化的学习路径，本文将帮助你建立对真空中电磁现象的坚实理解。

## 原理与机制

继引言之后，本章旨在深入剖析麦克斯韦方程组在真空中的基本原理和内在机制。我们将从[方程组](@entry_id:193238)本身出发，探讨其对静态场和动态场的约束，揭示[电场](@entry_id:194326)与[磁场](@entry_id:153296)之间动态耦合的奥秘，并最终推导出电磁理论最伟大的预言——[电磁波](@entry_id:269629)的存在。最后，我们将简要介绍更为深刻的规范不变性和相对论[协变](@entry_id:634097)性，以展现该理论的内在和谐与优美。

### 麦克斯韦真空[方程组](@entry_id:193238)：基本定律

在不存在[电荷](@entry_id:275494)和电流的真空区域中，[电磁场](@entry_id:265881)由以下四条[麦克斯韦方程组](@entry_id:150940)所支配，它们以[微分形式](@entry_id:146747)呈现，简洁而深刻：

I.  **[高斯电场定律](@entry_id:146732) (Gauss's Law for Electricity):** $\vec{\nabla} \cdot \vec{E} = 0$
II. **高斯[磁场](@entry_id:153296)定律 (Gauss's Law for Magnetism):** $\vec{\nabla} \cdot \vec{B} = 0$
III. **法拉第电磁感应定律 (Faraday's Law of Induction):** $\vec{\nabla} \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$
IV. **[安培-麦克斯韦定律](@entry_id:266368) (Ampère-Maxwell Law):** $\vec{\nabla} \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$

此处，$\vec{E}$ 代表[电场](@entry_id:194326)强度，$\vec{B}$ 代表[磁感应强度](@entry_id:144179)，$\mu_0$ 是[真空磁导率](@entry_id:186031)，$\epsilon_0$ 是[真空介电常数](@entry_id:204253)。这组方程是[电动力学](@entry_id:158759)的基石，任何在真空中可能存在的[电磁场](@entry_id:265881)都必须同时满足这全部四个条件。

每条方程都有其明确的物理意义：
- **[高斯电场定律](@entry_id:146732)**指出，在没有[电荷](@entry_id:275494)的区域，[电场的散度](@entry_id:272995)为零。这意味着[电场线](@entry_id:277009)既无起点也无终点，它们要么从无穷远处来，到无穷远处去，要么形成闭合回路。
- **高斯[磁场](@entry_id:153296)定律**断言，[磁场的散度](@entry_id:273621)恒为零。这从数学上表达了一个基本的物理事实：自然界中不存在磁单极子。磁感线永远是闭合的曲线。
- **法拉第电磁感应定律**描述了变化的[磁场](@entry_id:153296)如何产生[电场](@entry_id:194326)。一个随时间变化的[磁场](@entry_id:153296) $\vec{B}$ 会在其周围感生出一个旋度不为零的[电场](@entry_id:194326) $\vec{E}$。这种[电场](@entry_id:194326)是涡旋状的，与由静[电荷](@entry_id:275494)产生的[无旋场](@entry_id:183486)有着本质区别。
- **[安培-麦克斯韦定律](@entry_id:266368)**则揭示了其对偶过程：变化的[电场](@entry_id:194326)也能产生[磁场](@entry_id:153296)。方程右侧的 $\mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$ 项由麦克斯韦引入，被称为**位移电流 (displacement current)**，它与传统电流一样，是[磁场](@entry_id:153296)的源泉。正是这一项，补全了电与磁的对称性，并预示了[电磁波](@entry_id:269629)的存在。

为了深刻理解这些定律的约束力，我们可以检验一个假设的场构型。例如，设想在某真空区域内存在如下[电磁场](@entry_id:265881) [@problem_id:1807890]：
$$ \vec{E}(x, y, z, t) = C_1 x \hat{x} $$
$$ \vec{B}(x, y, z, t) = C_2 t \hat{y} $$
其中 $C_1$ 和 $C_2$ 为非零常数。为了判断这组场是否物理可能，我们必须逐一检验麦克斯韦方程：

1.  **检验[高斯电场定律](@entry_id:146732)**：$\vec{\nabla} \cdot \vec{E} = \frac{\partial}{\partial x}(C_1 x) = C_1$。由于 $C_1 \neq 0$，该场违反了[高斯电场定律](@entry_id:146732)，因为它暗示了空间中存在一个均匀的净电荷密度，这与真空假设矛盾。

2.  **检验高斯[磁场](@entry_id:153296)定律**：$\vec{\nabla} \cdot \vec{B} = \frac{\partial}{\partial y}(C_2 t) = 0$。该定律得到满足。

3.  **检验[法拉第定律](@entry_id:149836)**：[电场的旋度](@entry_id:182875) $\vec{\nabla} \times \vec{E} = \vec{0}$，因为 $\vec{E}$ 的各分量仅依赖于对应的坐标或为零。然而，[磁场](@entry_id:153296)的时间导数 $-\frac{\partial \vec{B}}{\partial t} = -C_2 \hat{y}$。由于 $C_2 \neq 0$，我们有 $\vec{\nabla} \times \vec{E} \neq -\frac{\partial \vec{B}}{\partial t}$。因此，法拉第定律被违反。

4.  **检验[安培-麦克斯韦定律](@entry_id:266368)**：[磁场的旋度](@entry_id:261797) $\vec{\nabla} \times \vec{B} = \vec{0}$。[电场](@entry_id:194326)的时间导数 $\frac{\partial \vec{E}}{\partial t} = \vec{0}$。因此，$\vec{\nabla} \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$ 成立。

这个简单的例子表明，一个看似合理的场构型，若不能同时满足所有四个麦克斯韦方程，它在物理上就是不可能存在的。

### 静态场约束与势的概念

当[电磁场](@entry_id:265881)不随时间变化时（即 $\frac{\partial}{\partial t} = 0$），麦克斯韦方程组简化为两组独立的静电学和[静磁学](@entry_id:140120)方程：
- **[静电场](@entry_id:268546)**: $\vec{\nabla} \cdot \vec{E} = 0$ 和 $\vec{\nabla} \times \vec{E} = 0$
- **静[磁场](@entry_id:153296)**: $\vec{\nabla} \cdot \vec{B} = 0$ 和 $\vec{\nabla} \times \vec{B} = 0$

高斯[磁场](@entry_id:153296)定律 $\vec{\nabla} \cdot \vec{B} = 0$ 是一个无条件的约束，无论场是静态还是动态，它都必须成立。这一性质在数学上有一个重要的推论。基于矢量恒等式“[旋度的散度](@entry_id:271562)恒为零”，即 $\vec{\nabla} \cdot (\vec{\nabla} \times \vec{A}) = 0$ 对任意矢量场 $\vec{A}$ 成立，我们可以引入一个辅助场——**[磁矢量势](@entry_id:141246) (magnetic vector potential)** $\vec{A}$，并定义：
$$ \vec{B} = \vec{\nabla} \times \vec{A} $$
通过这种方式定义的[磁场](@entry_id:153296) $\vec{B}$，其散度将自动为零，从而天然地满足了高斯[磁场](@entry_id:153296)定律。这不仅为求解[磁场](@entry_id:153296)问题提供了一个有力的数学工具，也深刻揭示了 $\vec{\nabla} \cdot \vec{B} = 0$ 的结构性根源 [@problem_id:1807904]。任何可写成一个矢量场旋度的场，其散度必然为零。反之，任何散度处处为零的场，都可以表示为某个矢量势的旋度。

考虑一个[静态磁场](@entry_id:195560)构型 [@problem_id:1807936]，$\vec{B}(x, y, z) = B_0 (x\hat{i} + y\hat{j} - 2z\hat{k})$。为了判断其物理可能性，我们需检验它是否满足静态真空方程：
- **散度**: $\vec{\nabla} \cdot \vec{B} = \frac{\partial}{\partial x}(B_0 x) + \frac{\partial}{\partial y}(B_0 y) + \frac{\partial}{\partial z}(-2B_0 z) = B_0 + B_0 - 2B_0 = 0$。该条件满足。
- **旋度**: 通过计算可以发现，该场的各个旋度分量均为零，即 $\vec{\nabla} \times \vec{B} = \vec{0}$。

由于这个静态场同时满足了[散度和旋度](@entry_id:270881)条件，因此它是在真空中一个物理上可能的局部[磁场](@entry_id:153296)[分布](@entry_id:182848)，尽管它可能需要由区域外的电流源来产生。

### 动态场的相互作用：[电磁感应](@entry_id:181154)与位移电流

[麦克斯韦方程组](@entry_id:150940)最引人入胜的部分在于两个旋度方程，它们描述了[电场和磁场](@entry_id:261347)如何相互创生，形成一个不可分割的动态整体。

**法拉第[电磁感应](@entry_id:181154)定律** $\vec{\nabla} \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$ 表明，一个时变的[磁场](@entry_id:153296)必然伴随着一个空间变化的[电场](@entry_id:194326)（具体来说，是一个有旋的[电场](@entry_id:194326)）。即使在[磁场](@entry_id:153296)[空间分布](@entry_id:188271)均匀的情况下，只要其强度随时间变化，就会感生出[电场](@entry_id:194326)。例如，考虑一个空间均匀但时间上正弦[振荡](@entry_id:267781)的[磁场](@entry_id:153296) $\vec{B}(t) = B_0 \cos(\omega t) \hat{k}$ [@problem_id:1807935]。根据法拉第定律，感应[电场的旋度](@entry_id:182875)为：
$$ \vec{\nabla} \times \vec{E} = -\frac{\partial}{\partial t} (B_0 \cos(\omega t) \hat{k}) = B_0 \omega \sin(\omega t) \hat{k} $$
这个结果表明，变化的[磁场](@entry_id:153296)在其周围激发出涡旋状的[电场](@entry_id:194326)。正是这种[感应电场](@entry_id:267314)驱动了变压器和发电机中的电流。

**[安培-麦克斯韦定律](@entry_id:266368)** $\vec{\nabla} \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$ 提供了另一半图景。麦克斯韦的天才洞见在于，变化的[电场](@entry_id:194326)也应该扮演类似电流的角色，产生[磁场](@entry_id:153296)。他将 $\vec{J}_D = \epsilon_0 \frac{\partial \vec{E}}{\partial t}$ 命名为**[位移电流](@entry_id:190231)密度 (displacement current density)**。虽然它不涉及[电荷](@entry_id:275494)的真实运动，但在产生[磁场](@entry_id:153296)方面，其效果与真实电流无异。

我们可以通过一个思想实验来体会[位移电流](@entry_id:190231)的物理效应 [@problem_id:1807921]。设想真空中有一个均匀但[线性增长](@entry_id:157553)的[电场](@entry_id:194326) $\vec{E}(t) = \alpha t \hat{z}$。我们来计算环绕z轴的一个半径为 $R$ 的圆形回路的[磁场](@entry_id:153296)环流 $\oint \vec{B} \cdot d\vec{l}$。根据[安培-麦克斯韦定律](@entry_id:266368)的积分形式：
$$ \oint \vec{B} \cdot d\vec{l} = \mu_0 I_{\text{enc}} + \mu_0 \epsilon_0 \frac{d\Phi_E}{dt} $$
在真空中，[传导电流](@entry_id:265343) $I_{\text{enc}} = 0$。[电通量](@entry_id:266049) $\Phi_E$ 为 $\int \vec{E} \cdot d\vec{A} = (\alpha t) (\pi R^2)$。因此，其时间变化率为：
$$ \frac{d\Phi_E}{dt} = \alpha \pi R^2 $$
代入[安培-麦克斯韦定律](@entry_id:266368)，我们得到[磁场](@entry_id:153296)的环流：
$$ \oint \vec{B} \cdot d\vec{l} = \mu_0 \epsilon_0 (\alpha \pi R^2) $$
这个非零的结果明确显示，一个变化的[电通量](@entry_id:266049)确实在空间中产生了环绕的[磁场](@entry_id:153296)。正是这种对称的相[互感应](@entry_id:180602)机制，使得电磁扰动能够脱离源而独立存在。

### 终极推论：[电磁波](@entry_id:269629)

[电场和磁场](@entry_id:261347)之间的动态耦合导致了麦克斯韦理论最辉煌的成果：预言了以光速传播的[电磁波](@entry_id:269629)的存在。

#### **波动方程的推导**

我们可以从麦克斯韦的两个旋度方程出发，推导出关于电场和磁场的[波动方程](@entry_id:139839)。首先，对[法拉第定律](@entry_id:149836) $\vec{\nabla} \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$ 两边取旋度：
$$ \vec{\nabla} \times (\vec{\nabla} \times \vec{E}) = \vec{\nabla} \times \left(-\frac{\partial \vec{B}}{\partial t}\right) = -\frac{\partial}{\partial t}(\vec{\nabla} \times \vec{B}) $$
利用矢量恒等式 $\vec{\nabla} \times (\vec{\nabla} \times \vec{A}) = \vec{\nabla}(\vec{\nabla} \cdot \vec{A}) - \nabla^2 \vec{A}$，上式左边变为：
$$ \vec{\nabla}(\vec{\nabla} \cdot \vec{E}) - \nabla^2 \vec{E} $$
现在，我们将另外两个麦克斯韦方程代入。在真空中，$\vec{\nabla} \cdot \vec{E} = 0$，同时[安培-麦克斯韦定律](@entry_id:266368)给出 $\vec{\nabla} \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$。代入后得到：
$$ \vec{\nabla}(0) - \nabla^2 \vec{E} = -\frac{\partial}{\partial t}\left(\mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}\right) $$
整理后，我们得到了[电场](@entry_id:194326)的**[三维波动方程](@entry_id:162663)**:
$$ \nabla^2 \vec{E} = \mu_0 \epsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2} $$
通过完全类似的步骤（对[安培-麦克斯韦定律](@entry_id:266368)取旋度），可以得到关于[磁场](@entry_id:153296)的完全相同的波动方程：
$$ \nabla^2 \vec{B} = \mu_0 \epsilon_0 \frac{\partial^2 \vec{B}}{\partial t^2} $$
为了更具体地理解这个过程，我们可以考虑一个沿z轴传播的[线偏振](@entry_id:273116)波，其[电场](@entry_id:194326)只有x分量，且只依赖于 $z$ 和 $t$，即 $\vec{E}(z, t) = E_x(z, t) \hat{i}$ [@problem_id:1807910]。通过上述推导过程，可以得到其**[一维波动方程](@entry_id:164824)**：
$$ \frac{\partial^2 E_x}{\partial z^2} = \mu_0 \epsilon_0 \frac{\partial^2 E_x}{\partial t^2} $$

#### **光速的预言**

标准的[波动方程](@entry_id:139839)形式为 $\nabla^2 f = \frac{1}{v^2} \frac{\partial^2 f}{\partial t^2}$，其中 $v$ 是[波的传播](@entry_id:144063)速度。通过与我们推导出的电磁[波动方程](@entry_id:139839)进行比对，可以立刻确定[电磁波](@entry_id:269629)在真空中的[传播速度](@entry_id:189384)为：
$$ v = \frac{1}{\sqrt{\mu_0 \epsilon_0}} $$
代入当时已知的[真空磁导率](@entry_id:186031) $\mu_0$ 和[介电常数](@entry_id:146714) $\epsilon_0$ 的实验值，计算出的速度约为 $3.00 \times 10^8$ 米/秒，这与当时测得的光速惊人地一致。麦克斯韦由此断定，光本身就是一种[电磁波](@entry_id:269629)。这一发现是[物理学史](@entry_id:168682)上最伟大的综合之一。

我们可以通过一个思想实验进一步理解速度与定律本身的关系 [@problem_id:1592457]。如果在一个假想宇宙中，[安培-麦克斯韦定律](@entry_id:266368)的形式变为 $\vec{\nabla} \times \vec{B} = \alpha \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$，其中 $\alpha$ 是一个无量纲常数，那么重复上述推导，波动方程将变为 $\nabla^2 \vec{E} = \alpha \mu_0 \epsilon_0 \frac{\partial^2 \vec{E}}{\partial t^2}$。这将导致波速为 $v = \frac{1}{\sqrt{\alpha \mu_0 \epsilon_0}}$。这表明，电磁[波的传播](@entry_id:144063)速度直接由电场和磁场相互耦合的强度（由 $\mu_0, \epsilon_0$ 和任何其他因子决定）所决定。

#### **[电磁波](@entry_id:269629)的性质**

麦克斯韦方程不仅预言了[电磁波](@entry_id:269629)的存在和速度，还揭示了它们的内在属性。对于在真空中传播的平面[电磁波](@entry_id:269629)，其形式可以写作 $\vec{E}(\vec{r}, t) = \vec{E}_0 \exp(i(\vec{k} \cdot \vec{r} - \omega t))$，其中 $\vec{k}$ 是波矢，指向传播方向。
- **横波性 (Transversality)**: 将此[平面波解](@entry_id:195230)代入[高斯定律](@entry_id:141493) $\vec{\nabla} \cdot \vec{E} = 0$ [@problem_id:1807927]，我们得到：
$$ \vec{\nabla} \cdot \vec{E} = i \vec{k} \cdot \vec{E}_0 \exp(i(\vec{k} \cdot \vec{r} - \omega t)) = 0 $$
这意味着 $\vec{k} \cdot \vec{E}_0 = 0$。同理，从 $\vec{\nabla} \cdot \vec{B} = 0$ 可以得到 $\vec{k} \cdot \vec{B}_0 = 0$。这两个结果表明，[电磁波](@entry_id:269629)的[电场和磁场](@entry_id:261347)分量都垂直于传播方向 $\vec{k}$。因此，[电磁波](@entry_id:269629)是**[横波](@entry_id:269527)**。
- **正交性 (Orthogonality)**: 将[平面波解](@entry_id:195230)代入法拉第定律 $\vec{\nabla} \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$，我们得到 $i\vec{k} \times \vec{E} = -(-i\omega)\vec{B}$，即 $\vec{k} \times \vec{E} = \omega \vec{B}$。这个关系式表明，$\vec{B}$ 垂直于 $\vec{E}$ 和 $\vec{k}$ 构成的平面，因此 $\vec{E}$ 和 $\vec{B}$ 相互垂直。
综上，在真空中传播的[电磁波](@entry_id:269629)，其[电场](@entry_id:194326) $\vec{E}$、[磁场](@entry_id:153296) $\vec{B}$ 和传播方向 $\vec{k}$ 三者构成一个右手[正交系](@entry_id:184795)。

### 高等表述与对称性

为了更深入地理解麦克斯韦理论，物理学家发展了更为抽象和普适的数学框架，这些框架揭示了理论背后深刻的对称性原理。

#### **规范不变性**

我们之前引入了标量势 $V$ 和矢量势 $\vec{A}$ 来表示电场和磁场：
$$ \vec{B} = \vec{\nabla} \times \vec{A} $$
$$ \vec{E} = -\vec{\nabla} V - \frac{\partial \vec{A}}{\partial t} $$
然而，给定的[电磁场](@entry_id:265881) $(\vec{E}, \vec{B})$ 所对应的势 $(V, \vec{A})$ 并不是唯一的。我们可以对势进行如下的**[规范变换](@entry_id:176521) (gauge transformation)**：
$$ V' = V - \frac{\partial \chi}{\partial t} $$
$$ \vec{A}' = \vec{A} + \vec{\nabla} \chi $$
其中 $\chi(\vec{r}, t)$ 是任意一个标量函数，称为[规范函数](@entry_id:749731)。一个惊人的结果是，在这样的变换下，物理的[电场和磁场](@entry_id:261347)保持不变。这一性质被称为**规范不变性 (gauge invariance)**。我们可以通过直接计算来验证这一点 [@problem_id:1592422]。变换后的[电场](@entry_id:194326) $\vec{E}'$ 为：
$$ \vec{E}' = -\vec{\nabla} V' - \frac{\partial \vec{A}'}{\partial t} = -\vec{\nabla}\left(V - \frac{\partial \chi}{\partial t}\right) - \frac{\partial}{\partial t}(\vec{A} + \vec{\nabla} \chi) = \left(-\vec{\nabla}V - \frac{\partial \vec{A}}{\partial t}\right) + \vec{\nabla}\frac{\partial \chi}{\partial t} - \frac{\partial}{\partial t}\vec{\nabla}\chi $$
由于空间和时间导数可以交换次序，后两项相互抵消，因此 $\vec{E}' = \vec{E}$。同样可以证明 $\vec{B}' = \vec{B}$。[规范不变性](@entry_id:137857)是现代物理学（包括[量子场论](@entry_id:138177)和广义相对论）中的一个核心指导原则。它表明我们理论中的某些数学自由度并不对应于[物理可观测量](@entry_id:154692)。

#### **洛伦兹不变量**

麦克斯韦方程组的结构与爱因斯坦的[狭义相对论](@entry_id:275552)完美契合。在相对论的四维时空框架下，电场和磁场不再是独立的概念，而是被统一为一个单一的物理实体——**[电磁场张量](@entry_id:158921) (electromagnetic field strength tensor)** $F^{\mu\nu}$。这个反对称的二阶张量将 $\vec{E}$ 和 $\vec{B}$ 的六个分量整合在一起。

从这个张量出发，我们可以构造出在**[洛伦兹变换](@entry_id:176827)**（即在不同惯性参考系之间切换）下保持不变的量，称为**[洛伦兹标量](@entry_id:275319) (Lorentz scalars)**。这些量反映了[电磁场](@entry_id:265881)不依赖于观测者运动状态的内在属性。有两个基本的[洛伦兹标量](@entry_id:275319) [@problem_id:1592433]：

1.  $\mathcal{S}_1 \propto F_{\mu\nu}F^{\mu\nu} = 2\left(B^2 - \frac{E^2}{c^2}\right)$
2.  $\mathcal{S}_2 \propto \tilde{F}_{\mu\nu}F^{\mu\nu} \propto \vec{E} \cdot \vec{B}$

其中 $\tilde{F}^{\mu\nu}$ 是 $F^{\mu\nu}$ 的对偶张量。这两个组合，$E^2 - c^2 B^2$ 和 $\vec{E} \cdot \vec{B}$，对于任何惯性参考系中的观测者来说，其值都是相同的。例如，如果在一个[参考系](@entry_id:169232)中观测到纯[电场](@entry_id:194326)（$\vec{B}=\vec{0}$），那么在任何其他以不同速度运动的[参考系](@entry_id:169232)中，观测者可能会测到非零的[磁场](@entry_id:153296)，但 $E^2 - c^2 B^2$ 的值将保持不变。同样，如果 $\vec{E}$ 和 $\vec{B}$ 在一个[参考系](@entry_id:169232)中是正交的，那么它们在所有[参考系](@entry_id:169232)中都将是正交的。这深刻地揭示了[电场和磁场](@entry_id:261347)是如何作为同一个四维时空实体的不同侧面而呈现出来的。

本章我们从[麦克斯韦方程组](@entry_id:150940)的基本形式出发，系统地探索了它在真空中的物理机制，从静态场的约束到动态场的相[互感应](@entry_id:180602)，再到[电磁波](@entry_id:269629)的诞生及其性质，最后触及了支撑这一宏伟理论的更深层次的对称性原理。这些原理不仅统一了电、磁、光现象，也为20世纪物理学的两大革命——相对论和量子力学——铺平了道路。