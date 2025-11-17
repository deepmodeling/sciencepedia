## 引言
经典麦克斯韦理论在描述电磁现象方面取得了非凡的成功，但其传统的三维矢量形式在狭义相对论的框架下显得格格不入。一个核心的矛盾在于，物理定律应在所有[惯性参考系](@entry_id:276742)中保持形式不变，而[麦克斯韦方程组](@entry_id:150940)在[洛伦兹变换](@entry_id:176827)下的不变性并非显而易见。为了解决这一理论上的不协调，并揭示电磁学与[时空几何](@entry_id:139497)之间更深层次的联系，我们需要一种新的数学语言——电动力学的协变表述。

本文旨在系统地构建并应用这一强大的理论框架。读者将踏上一段从基本原理到前沿应用的旅程。在“原理与机制”章节中，我们将学习如何使用[四维矢量](@entry_id:275085)和张量将[电场](@entry_id:194326)、[磁场](@entry_id:153296)、源和势统一起来，从而将复杂的麦克斯韦方程组压缩为优美简洁的协变形式。接着，在“应用与跨学科联系”章节中，我们将见证这一理论在简化[相对论动力学](@entry_id:264218)问题、分析场的基本性质以及连接凝聚态物理、量子引力等多个学科方面的强大威力。最后，“动手实践”部分将提供具体问题，巩固所学知识。

现在，让我们首先进入“原理与机制”章节，深入探讨构建这一协变理论的核心原理与内在机制。

## 原理与机制

在“导论”章节中，我们已经认识到，经典[麦克斯韦方程组](@entry_id:150940)虽然在描述电磁现象方面取得了巨大成功，但其形式在洛伦兹变换下并非显性[协变](@entry_id:634097)。为了使[电动力学](@entry_id:158759)与[狭义相对论](@entry_id:275552)的基本原理——所有惯性系中物理定律形式相同——完全协调，我们需要一种新的数学语言。本章旨在系统地建立这种语言，即电磁理论的协变形式，并深入探讨其核心原理与内在机制。我们将看到，通过引入四维矢量和张量，麦克斯韦理论的深刻对称性和内在统一性将以一种前所未有的优美形式展现出来。

### 电磁学中的[四维矢量](@entry_id:275085)

[狭义相对论](@entry_id:275552)的核心舞台是四维[闵可夫斯基时空](@entry_id:156421)，其时空坐标由一个**[四维矢量](@entry_id:275085) (four-vector)** $x^\mu = (ct, x, y, z)$ 描述。在这种框架下，物理定律的协变性要求我们将物理量组织成四维标量、四维矢量或更高阶的张量。

电磁理论中的基本量——[电势](@entry_id:267554)与磁矢势，以及[电荷密度](@entry_id:144672)与[电流密度](@entry_id:190690)——也必须遵循这一要求。我们定义**[四维势](@entry_id:188407) (four-potential)** $A^\mu$ 和**[四维电流密度](@entry_id:262568) (four-current density)** $J^\mu$ 如下：
$$
A^\mu = (\phi/c, \vec{A}) = (\phi/c, A_x, A_y, A_z)
$$
$$
J^\mu = (c\rho, \vec{J}) = (c\rho, J_x, J_y, J_z)
$$
其中 $\phi$ 是标量势，$\vec{A}$ 是矢量势，$\rho$ 是[电荷密度](@entry_id:144672)，$\vec{J}$ 是电流密度。电荷守恒定律 $\frac{\partial \rho}{\partial t} + \nabla \cdot \vec{J} = 0$ 在四维形式下具有一个极为简洁的表达：$\partial_\mu J^\mu = 0$，其中 $\partial_\mu = \frac{\partial}{\partial x^\mu} = (\frac{1}{c}\frac{\partial}{\partial t}, \vec{\nabla})$ 是四维梯度算符。这清晰地表明，[四维电流密度](@entry_id:262568)的四维散度是一个[洛伦兹标量](@entry_id:275319)，且其值为零。

在规范变换理论中，**[洛伦兹规范](@entry_id:153650)条件 (Lorenz gauge condition)** $\frac{1}{c^2}\frac{\partial \phi}{\partial t} + \nabla \cdot \vec{A} = 0$ 起着至关重要的作用。在四维语言中，它可以被写为 $\partial_\mu A^\mu = 0$。一个深刻的问题是：这个条件本身是否是洛伦兹协变的？也就是说，如果在一个惯性系中成立，它在所有惯性系中都成立吗？答案是肯定的，因为 $\partial_\mu A^\mu$ 是一个**[洛伦兹标量](@entry_id:275319) (Lorentz scalar)**。

我们可以通过一个具体的例子来验证这一点 [@problem_id:380210]。考虑一个在 $S$ 系中给定的[四维势](@entry_id:188407) $A^\mu(x) = (K_0 x^0, K_1 x^1, 0, 0)$，其中 $K_0$ 和 $K_1$ 为常数。其四维散度为：
$$
\partial_\mu A^\mu = \frac{\partial A^0}{\partial x^0} + \frac{\partial A^1}{\partial x^1} + \frac{\partial A^2}{\partial x^2} + \frac{\partial A^3}{\partial x^3} = K_0 + K_1
$$
现在，我们变换到一个沿 $x^1$ 方向以速度 $v$ 运动的 $S'$ 系。[四维矢量](@entry_id:275085)（包括梯度算符 $\partial'_\mu$ 和[四维势](@entry_id:188407) $A'^\mu$）的变换法则会使计算变得复杂。然而，由于我们已经断言 $\partial_\mu A^\mu$ 是一个标量，它的值在 $S'$ 系中应该保持不变。也就是说，$\partial'_\mu A'^\mu$ 的值应该直接就是 $K_0 + K_1$。直接计算可以验证，尽管 $A'^\mu$ 和 $\partial'_\mu$ 的各个分量都发生了变化，但它们的[内积](@entry_id:158127)组合 $\partial'_\mu A'^\mu$ 最终确实等于 $K_0+K_1$。这有力地证明了[洛伦兹规范](@entry_id:153650)条件的[洛伦兹不变性](@entry_id:155152)，为我们在任意[惯性系](@entry_id:266190)中使用它提供了理论保障。

### 电磁场张量

虽然[四维势](@entry_id:188407) $A^\mu$ 是理论的基础，但物理上可直接测量的量是[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$。在[协变](@entry_id:634097)理论中，这两个三维矢量场被统一为一个单一的、二阶反对称的**电磁场张量 (electromagnetic field tensor)** $F^{\mu\nu}$：
$$
F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu
$$
其中 $\partial^\mu = \eta^{\mu\sigma}\partial_\sigma = (\frac{1}{c}\frac{\partial}{\partial t}, -\vec{\nabla})$。将 $A^\mu$ 的分量代入，我们可以得到 $F^{\mu\nu}$ 矩阵：
$$
F^{\mu\nu} = \begin{pmatrix}
0  -E_x/c  -E_y/c  -E_z/c \\
E_x/c  0  -B_z  B_y \\
E_y/c  -B_z  0  -B_x \\
E_z/c  B_y  -B_x  0
\end{pmatrix}
$$
这个张量优美地将[电场和磁场](@entry_id:261347)的所有六个分量容纳其中。它的[反对称性](@entry_id:261893)（$F^{\mu\nu} = -F^{\nu\mu}$）是其定义式的直接推论。

电场和磁场在不同惯性系之间的变换关系是[狭义相对论](@entry_id:275552)的经典结果。在张量语言中，这个复杂的变换可以被一个简单的公式所取代。作为一个二阶张量，$F^{\mu\nu}$ 的变换规律是：
$$
F'^{\alpha\beta} = \Lambda^\alpha_{\ \mu} \Lambda^\beta_{\ \nu} F^{\mu\nu}
$$
其中 $\Lambda^\alpha_{\ \mu}$ 是[洛伦兹变换](@entry_id:176827)矩阵。这个公式自动地、无一遗漏地再现了 $\vec{E}$ 和 $\vec{B}$ 的所有变换规则。

例如，考虑一个在静止系 $S$ 中位于 $z=0$ 平面、带有均匀面[电荷密度](@entry_id:144672) $\sigma_0$ 的无限大薄板 [@problem_id:380207]。在 $S$ 系中，只有垂直于板面的[电场](@entry_id:194326) $E_z = \frac{\sigma_0}{2\epsilon_0} \mathrm{sgn}(z)$，而[磁场](@entry_id:153296) $\vec{B}=0$。现在，在一个相对于 $S$ 系以速度 $\vec{v} = v\hat{x}$ 运动的 $S'$ 系中，通过应用上述[张量变换法则](@entry_id:185176)（或等价的 $\vec{E}, \vec{B}$ 变换法则），我们会发现 $S'$ 系中的场为：
$$
E'_z = \gamma E_z \quad , \quad B'_y = \gamma \frac{v}{c^2} E_z
$$
其他分量为零。一个纯[电场](@entry_id:194326)在另一个参照系中“变”出了一部分[磁场](@entry_id:153296)，这正是电场和磁场作为同一个实体——电磁场张量——不同侧面的体现。

### [麦克斯韦方程组的协变形式](@entry_id:197529)

麦克斯韦的四个[方程组](@entry_id:193238)在四维时空 formalism 中可以被压缩成两个极其简洁的张量方程。

#### [齐次方程](@entry_id:163650)与[比安基恒等式](@entry_id:261685)

无磁单极的[高斯磁定律](@entry_id:182942)（$\nabla \cdot \vec{B} = 0$）和法拉第电磁感应定律（$\nabla \times \vec{E} + \frac{\partial \vec{B}}{\partial t} = 0$）被统称为齐次麦克斯韦方程组。它们源于[场张量](@entry_id:186486) $F^{\mu\nu}$ 由[四维势](@entry_id:188407) $A^\mu$ 导出的定义。这个几何事实可以用**比安基恒等式 (Bianchi identity)** 来表达：
$$
\partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0
$$
这个恒等式对任意由势场导出的旋度形式的场都成立。以 $(\lambda, \mu, \nu) = (1, 2, 3)$ 为例，该恒等式变为 $\partial_1 F_{23} + \partial_2 F_{31} + \partial_3 F_{12} = 0$。回顾 $F_{\mu\nu}$ 的分量，$F_{23} = -B_x, F_{31} = -B_y, F_{12} = -B_z$ (注意 $F_{\mu\nu}$ 和 $F^{\mu\nu}$ 的分量符号差异)，代入后即得到 $\frac{\partial B_x}{\partial x} + \frac{\partial B_y}{\partial y} + \frac{\partial B_z}{\partial z} = 0$，这正是 $\nabla \cdot \vec{B} = 0$。如果这个等式不为零，其结果就对应于磁荷密度 [@problem_id:380233]。类似地，选取其他指标组合可以重现法拉第定律。

[齐次方程组](@entry_id:150411)还有另一种等价的协变形式。我们引入**对偶张量 (dual tensor)** $G^{\mu\nu}$：
$$
G^{\mu\nu} = \frac{1}{2}\epsilon^{\mu\nu\alpha\beta}F_{\alpha\beta} = \begin{pmatrix}
0  -B_x  -B_y  -B_z \\
B_x  0  E_z/c  -E_y/c \\
B_y  -E_z/c  0  E_x/c \\
B_z  E_y/c  -E_x/c  0
\end{pmatrix}
$$
其中 $\epsilon^{\mu\nu\alpha\beta}$ 是全反对称的[列维-奇维塔符号](@entry_id:193594)。对偶张量是通过将原始张量中的 $\vec{E}/c$ 和 $-\vec{B}$ 进行互换得到的。齐次[麦克斯韦方程组](@entry_id:150940)可以统一表示为：
$$
\partial_\mu G^{\mu\nu} = 0
$$
我们可以通过一个具体例子来验证这个方程的正确性 [@problem_id:380221]。考虑一个以恒定速度 $\vec{v}=(v, 0, 0)$ 运动的[点电荷](@entry_id:263616)。它产生的电场和磁场是时空坐标的复杂函数。然而，如果我们计算 $\partial_\mu G^{\mu\nu}$ 的任意一个分量，例如 $\nu=2$ 分量，即 $\partial_\mu G^{\mu 2} = \partial_0 G^{02} + \partial_1 G^{12} + \partial_2 G^{22} + \partial_3 G^{32}$。将 $G^{\mu\nu}$ 的分量 $G^{02}=-B_y$, $G^{12}=E_z/c$, $G^{32}=-E_x/c$ 代入，再将[移动点电荷](@entry_id:273707)的场表达式代入并进行[偏导数](@entry_id:146280)运算，经过一番计算，所有项将精确地相互抵消，结果为零。这明确地展示了协变形式如何巧妙地编码了场的时空演化规律。

#### 非[齐次方程](@entry_id:163650)

包含源（[电荷](@entry_id:275494)和电流）的高斯定律（$\nabla \cdot \vec{E} = \rho/\epsilon_0$）和[安培-麦克斯韦定律](@entry_id:266368)（$\nabla \times \vec{B} = \mu_0 \vec{J} + \mu_0\epsilon_0 \frac{\partial \vec{E}}{\partial t}$）被统称为非[齐次方程](@entry_id:163650)。它们在协变框架下也统一为一个方程：
$$
\partial_\mu F^{\mu\nu} = \mu_0 J^\nu
$$
这个方程优雅地将场的时空变化（左侧）与源的[分布](@entry_id:182848)（右侧）联系起来。方程的 $\nu=0$ 分量对应[高斯定律](@entry_id:141493)，而 $\nu=1,2,3$ 空间分量则对应[安培-麦克斯韦定律](@entry_id:266368)。

### 波动方程与协变性验证

将场的定义 $F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu$ 代入非齐次方程 $\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$，我们得到：
$$
\partial_\mu (\partial^\mu A^\nu - \partial^\nu A^\mu) = \mu_0 J^\nu
$$
这可以写作 $\Box A^\nu - \partial^\nu (\partial_\mu A^\mu) = \mu_0 J^\nu$，其中 $\Box \equiv \partial_\mu \partial^\mu = \frac{1}{c^2}\frac{\partial^2}{\partial t^2} - \nabla^2$ 是**[达朗贝尔算符](@entry_id:275913) ([d'](@entry_id:189153)Alembertian operator)**，它是一个[洛伦兹标量](@entry_id:275319)。

这个方程形式还不够简洁。但如果我们采用之前提到的[洛伦兹规范](@entry_id:153650) $\partial_\mu A^\mu = 0$，方程立刻简化为：
$$
\Box A^\mu = \mu_0 J^\mu
$$
这是一个四维[波动方程](@entry_id:139839)，它明确指出[四维电流](@entry_id:199021)是[四维势](@entry_id:188407)的源。这个方程是显性[协变](@entry_id:634097)的，意味着它在所有惯性系中都具有完全相同的形式。

我们可以通过具体物理系统来检验这个核心方程。考虑一个半径为 $R_0$ 的无限长静态导线，内部有均匀的电荷密度 $\sigma$ 和电流密度 $\mathcal{J}$ [@problem_id:380227]。在导线内部，[四维势](@entry_id:188407) $A^\mu$ 和[四维电流](@entry_id:199021) $J^\mu$ 具有特定的形式。通过对给定的 $A^\mu(r)$ 分量直接计算 $\Box A^\mu = -\nabla^2 A^\mu$（因为系统是静态的），可以发现计算结果与 $\mu_0 J^\mu$ 的相应分量完全匹配。例如，对于 $\mu=0$ 分量，计算表明 $\Box A^0 = \sigma/(\epsilon_0 c)$。根据波动方程，这应等于 $\mu_0 J^0 = \mu_0 (c\rho) = \mu_0 c \sigma$。利用 $c^2 = 1/(\mu_0\epsilon_0)$，我们发现等式成立。对 $\mu=3$ 分量进行同样的操作，也能验证其正确性。

为了更深刻地理解[协变](@entry_id:634097)性的含义，我们可以考察一个运动的系统 [@problem_id:380192]。设一根带[电荷密度](@entry_id:144672)为 $\lambda$ 的无限长直导线静止在 $S$ 系。在 $S$ 系中，它只产生[电场](@entry_id:194326)，其[四维势](@entry_id:188407)为 $A^\mu = (A^0, 0, 0, 0)$。在一个以速度 $v$ 运动的 $S'$ 系中，根据洛伦兹变换，$A'^\mu$ 和 $J'^\mu$ 都会有新的、更复杂的分量，并且坐标也发生了变换。物理定律的协变性要求 $\Box' A'^\mu = \mu_0 J'^\mu$ 在 $S'$ 系中依然成立。这是一项非常繁琐但极具启发性的验证：对变换后的 $A'^\mu$ 在 $S'$ 系的坐标下计算[达朗贝尔算符](@entry_id:275913) $\Box'$，其结果精确地等于[洛伦兹变换](@entry_id:176827)后的源 $\mu_0 J'^\mu$。这表明，物理定律的形式确实独立于观测者的惯性运动状态。

从另一个角度，我们也可以探究势与场之间的关系。对于一个以匀速 $\vec{v}$ 运动的点电荷，其产生的[电场](@entry_id:194326)可以看作是[标量势](@entry_id:276177) $V$ 和矢量势 $\vec{A}$ 共同作用的结果：$\vec{E} = -\nabla V - \frac{\partial \vec{A}}{\partial t}$ [@problem_id:380234]。一个有趣的问题是，这两部分贡献的相对大小如何？通过计算可以发现，沿[电荷](@entry_id:275494)运动方向，来自矢量势的贡献 $\vec{E}_A \cdot \vec{v}$ 与来自[标量势](@entry_id:276177)的贡献 $\vec{E}_V \cdot \vec{v}$ 之比恰好为 $-\frac{v^2}{c^2}$。这个简洁的结果揭示了在相对论性运动中，磁矢势的时间变化对[电场](@entry_id:194326)的贡献变得不可忽略，且其相对重要性随速度的增加而增加。

### 场的洛伦兹[不变量与对称性](@entry_id:143276)

尽管 $\vec{E}$ 和 $\vec{B}$ 的分量依赖于[参考系](@entry_id:169232)，但我们可以从中构造出不依赖于[参考系](@entry_id:169232)的量，即**洛伦兹不变量 (Lorentz invariants)**。对于[电磁场](@entry_id:265881)，存在两个基本的[标量不变量](@entry_id:193787)：
$$
I_1 = F_{\mu\nu}F^{\mu\nu} = 2\left(|\vec{B}|^2 - \frac{|\vec{E}|^2}{c^2}\right)
$$
$$
I_2 = \frac{1}{4}\epsilon_{\mu\nu\alpha\beta}F^{\mu\nu}F^{\alpha\beta} = -\frac{1}{c}(\vec{E} \cdot \vec{B})
$$
任何由[场张量](@entry_id:186486)构造的[洛伦兹标量](@entry_id:275319)都可以表示为这两个[不变量](@entry_id:148850)的函数。它们的物理意义在于，所有惯性观测者对于同一个时空点的这两个[不变量](@entry_id:148850)的测量值都是相同的。

利用洛伦兹不变量的特性，可以巧妙地解决一些看似复杂的问题。例如，考虑两个相同的[点电荷](@entry_id:263616)，它们以相同的速度 $\vec{v}$ 平行运动，保持间距不变 [@problem_id:380204]。要计算它们连线中点的 $F^{\mu\nu}F_{\mu\nu}$ 值。在实验室坐标系中，计算该点的 $\vec{E}$ 和 $\vec{B}$ 场是一个非常复杂的过程。但是，我们可以利用 $F^{\mu\nu}F_{\mu\nu}$ 是洛伦兹不变量这一事实。我们切换到与[电荷](@entry_id:275494)一起运动的[参考系](@entry_id:169232) $S'$。在这个[参考系](@entry_id:169232)中，两个[电荷](@entry_id:275494)是静止的，因此它们只产生[静电场](@entry_id:268546)，[磁场](@entry_id:153296) $\vec{B}'=0$。在两[电荷](@entry_id:275494)的几何中心点，根据对称性，来自两个[电荷](@entry_id:275494)的[电场](@entry_id:194326) $\vec{E}'$ 大小相等、方向相反，因此总[电场](@entry_id:194326)为零。所以，在 $S'$ 系的中点，$\vec{E}'=0$ 且 $\vec{B}'=0$。那么，[不变量](@entry_id:148850)的值为 $I_1' = 2(0^2 - 0^2/c^2) = 0$。因为该值为[不变量](@entry_id:148850)，所以在[实验室参考系](@entry_id:166991) $S$ 中，该点的 $F^{\mu\nu}F_{\mu\nu}$ 值也必然为零。我们无需任何复杂计算就得到了答案。

除了洛伦兹变换下的[不变性](@entry_id:140168)，无源麦克斯韦理论还具有一种被称为**[对偶对称性](@entry_id:273545) (duality symmetry)** 的内在对称性。这种对称性表现为在如下变换下，方程形式保持不变：
$$
F'^{\mu\nu} = F^{\mu\nu} \cos\alpha + G^{\mu\nu} \sin\alpha
$$
$$
G'^{\mu\nu} = G^{\mu\nu} \cos\alpha - F^{\mu\nu} \sin\alpha
$$
这本质上是在由 $F^{\mu\nu}$ 和 $G^{\mu\nu}$ 张成的“平面”内进行旋转。标准麦克斯韦理论的[拉格朗日量](@entry_id:174593) $\mathcal{L} = -\frac{1}{4}F_{\mu\nu}F^{\mu\nu} = -\frac{1}{4}I_1$ 在此变换下并非严格不变。然而，无源麦克斯韦方程本身是[协变](@entry_id:634097)的。这种对称性在更高级的理论中具有重要意义。例如，我们可以考察一个假设的[非线性电动力学](@entry_id:275004)理论，其拉格朗日量包含[不变量](@entry_id:148850)的高次项，如 $\mathcal{L}_{NL} \propto (F_{\mu\nu}F^{\mu\nu})^2 + \lambda (F_{\mu\nu}G^{\mu\nu})^2 = I_1^2 + \lambda I_2^2$ [@problem_id:380236]。通过分析 $I_1$ 和 $I_2$ 在对偶旋转下的变换规律，可以证明，只有当 $\lambda=1$ 时，这个[非线性](@entry_id:637147)项才是对偶对称的。这表明，组合 $I_1^2 + I_2^2$ 具有特殊的对称性。

### 应力-能量张量与[守恒定律](@entry_id:269268)

[电磁场](@entry_id:265881)不仅在时空中传播，还携带能量和动量。这些物理量被统一在对称的二阶**[电磁应力-能量张量](@entry_id:267456) (electromagnetic stress-energy tensor)** $T^{\mu\nu}$ 中。其分量与我们熟悉的能量密度 $u_{EM}$、[坡印廷矢量](@entry_id:269386) $\vec{S}$ 和[麦克斯韦应力张量](@entry_id:153513) $\sigma^{ij}$ 相关：
$$
T^{\mu\nu} = \begin{pmatrix}
u_{EM}  S_x/c  S_y/c  S_z/c \\
S_x/c  -\sigma^{xx}  -\sigma^{xy}  -\sigma^{xz} \\
S_y/c  -\sigma^{yx}  -\sigma^{yy}  -\sigma^{yz} \\
S_z/c  -\sigma^{zx}  -\sigma^{zy}  -\sigma^{zz}
\end{pmatrix}
$$
能量和动量守恒定律可以用一个简洁的四维方程来表述：
$$
\partial_\mu T^{\mu\nu} = -f^\nu
$$
其中 $f^\nu = F^{\nu\lambda}J_\lambda$ 是[电磁场](@entry_id:265881)施加于[电荷](@entry_id:275494)和电流上的**洛伦兹力密度 (Lorentz force density)** 的四维形式。如果在一个区域内没有[电荷](@entry_id:275494)和电流（$J_\lambda=0$），则 $f^\nu = 0$，我们得到 $\partial_\mu T^{\mu\nu} = 0$，这表达了[电磁场](@entry_id:265881)自身能量和动量的[局域守恒](@entry_id:751393)。

这个强大的工具可以将抽象的场论与具体的物理力学效应联系起来。一个经典的例子是导线中的**[箍缩效应](@entry_id:267341) (pinch effect)** [@problem_id:380209]。考虑一根载有均匀[稳恒电流](@entry_id:271551) $\vec{J} = J_z \hat{z}$ 的中性导线。导线内部的[电流元](@entry_id:188466)会受到其他部分电流产生的[磁场](@entry_id:153296)的作用力，趋向于向中心轴线压缩。这个力密度可以通过计算[应力-能量张量](@entry_id:146544)的散度得到。

对于这个静态系统（$\partial/\partial t = 0$），空间力密度为 $\vec{f} = -\vec{\nabla} \cdot \mathbf{T}$，其中 $\mathbf{T}$ 是 $T^{ij}$ 构成的三维张量。导线内部的[磁场](@entry_id:153296)为 $B_\phi(r) = \frac{\mu_0 J_z r}{2}$（$r \le R_0$）。由于是中性导线，[电场](@entry_id:194326)为零。将[磁场](@entry_id:153296)代入 $T^{ij}$ 的表达式，并计算其在柱坐标下的散度，我们可以得到径向力密度 $f_r$。经过计算，我们发现：
$$
f_r = -\frac{\mu_0 J_z^2 r}{2}
$$
负号表示力指向中心，即压缩力。力的大小与到轴心距离 $r$ 成正比。这个结果不仅与使用[洛伦兹力定律](@entry_id:270735) $\vec{f} = \vec{J} \times \vec{B}$ 直接计算的结果一致，而且展示了如何从更基本的[守恒定律](@entry_id:269268)出发，将力理解为场自身动量流的变化。

通过本章的学习，我们完成了从传统三维矢量表述到四维张量表述的过渡。这种新的表述不仅使麦克斯韦理论的[洛伦兹协变性](@entry_id:161987)一目了然，更揭示了电与磁、场与势、时与空之间不可分割的深刻联系。这种[协变](@entry_id:634097)思想是现代物理学，从广义相对论到[量子场论](@entry_id:138177)的基石。