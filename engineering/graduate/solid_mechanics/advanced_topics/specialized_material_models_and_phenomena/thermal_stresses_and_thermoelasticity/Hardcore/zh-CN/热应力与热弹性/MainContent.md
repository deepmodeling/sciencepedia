## 引言
温度变化与力学响应之间的相互作用是工程与科学领域中一个普遍存在且至关重要的问题。从宏伟桥梁的季节性伸缩，到微电子芯片中因散热产生的应力，再到先进制造过程中材料内部残余应力的形成，理解和预测“热应力”是确保结构完整性、功能性和可靠性的关键。然而，这种热-力学耦合行为背后的物理机制复杂多样，需要一个严谨的理论框架来描述。本文旨在系统性地阐述热应力与热弹性理论，填补基础理论与工程应用之间的知识鸿沟。

为实现这一目标，本文分为三个循序渐进的章节。首先，在“原理与机制”一章中，我们将从连续介质热力学的基础出发，构建热弹性本构关系，并深入剖析热应力产生的两种根本机制：外部约束和内部不协调性。接着，在“应用与跨学科联系”一章中，我们将通过一系列来自土木、机械、材料科学及失效分析领域的实际案例，展示这些理论原理如何解决现实世界中的复杂问题，揭示该学科的广泛影响力。最后，“动手实践”部分将引导读者通过具体的计算练习，包括解析推导和有限元建模，将抽象的理论知识转化为解决问题的实践能力。通过这一结构化的学习路径，读者将建立起对热弹性力学全面而深刻的理解。

## 原理与机制

本章旨在系统阐述热应力与热弹性理论的核心原理和内在机制。我们将从连续介质热力学的基本定律出发，构建描述材料热-力学行为的本构关系，并深入探讨温度变化在固体中激发出应力的两种主要方式：外部约束和内部不协调性。本章内容将为后续章节中更复杂的应用问题提供坚实的理论基础。

### 热弹性的热力学基础

为了严谨地描述温度变化与力学响应之间的相互作用，我们必须从热力学第一和第二定律出发。对于一个经历可逆过程的均匀、小应变热弹性体，其单位质量内能 $u$ 的微分形式（也称为吉布斯关系）可以写作：

$$
du = T ds + \frac{1}{\rho} \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}
$$

其中，$T$ 是绝对温度，$s$ 是单位质量熵，$\rho$ 是材料密度，$\boldsymbol{\sigma}$ 是柯西应力张量，而 $\boldsymbol{\varepsilon}$ 是小应变张量。冒号“$:$”表示张量的双点积，因此 $\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$ 代表了单位体积的机械功。这个基本方程揭示了内能 $u$ 的自然变量是熵 $s$ 和应变 $\boldsymbol{\varepsilon}$，即 $u = u(s, \boldsymbol{\varepsilon})$。

然而，在实际工程问题中，我们更容易控制和测量温度 $T$ 而非熵 $s$。因此，通过勒让德变换（Legendre transform）引入更方便的热力学势函数是至关重要的。

**亥姆霍兹自由能 (Helmholtz Free Energy)**, $\psi$, 定义为：

$$
\psi = u - Ts
$$

这个变换将自变量从 $(s, \boldsymbol{\varepsilon})$ 切换为 $(T, \boldsymbol{\varepsilon})$。通过计算其全微分 $d\psi = du - Tds - s dT$，并代入上述吉布斯关系，我们得到：

$$
d\psi = -s dT + \frac{1}{\rho} \boldsymbol{\sigma} : d\boldsymbol{\varepsilon}
$$

这个方程表明，对于一个选定的亥姆霍兹自由能函数 $\psi(T, \boldsymbol{\varepsilon})$，熵和应力可以作为其偏导数直接导出：

$$
s = -\frac{\partial \psi}{\partial T}, \quad \boldsymbol{\sigma} = \rho \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$

这为构建基于能量函数的本构理论提供了坚实的基础。在恒温、恒应变的条件下，系统达到稳定平衡时，亥姆霍兹自由能 $\psi$ 取得最小值。[@problem_id:2701610]

类似地，我们还可以定义一个**吉布斯型自由能 (Gibbs-type Free Energy)**, $g$，其自然变量为 $(T, \boldsymbol{\sigma})$。这在应力为控制变量的实验条件下非常有用。通过对亥姆霍兹自由能再次进行勒让德变换来实现：

$$
g = \psi - \frac{1}{\rho}\boldsymbol{\sigma} : \boldsymbol{\varepsilon}
$$

其微分形式为：

$$
dg = -s dT - \frac{1}{\rho} \boldsymbol{\varepsilon} : d\boldsymbol{\sigma}
$$

由此可见，应变可以从吉布斯自由能中导出：$\boldsymbol{\varepsilon} = -\rho \frac{\partial g}{\partial \boldsymbol{\sigma}}$。值得注意的是，对于能够承受剪切应力的固体，其机械功必须由完整的应力张量 $\boldsymbol{\sigma}$ 和应变张量 $\boldsymbol{\varepsilon}$ 来描述，而不能像静水流体那样简化为仅与压力相关的项。[@problem_id:2701610]

### 热应变的运动学与本征应变的概念

理解热应力的关键在于应变分解的基本假设。在小应变理论框架下，我们假定总应变张量 $\boldsymbol{\varepsilon}$ 可以线性地分解为两部分：由机械载荷引起的**弹性应变** $\boldsymbol{\varepsilon}^e$ 和由温度变化引起的**热应变** $\boldsymbol{\varepsilon}^{th}$。[@problem_id:2701584]

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^{th}
$$

这是一个核心假设：材料的应力完全由其弹性应变 $\boldsymbol{\varepsilon}^e$ 决定，而热应变 $\boldsymbol{\varepsilon}^{th}$ 自身并不直接产生应力。如果一个物体可以不受任何阻碍地自由膨胀或收缩，那么其内部将只存在热应变而没有弹性应变，因此应力为零。

热应变 $\boldsymbol{\varepsilon}^{th}$ 是一种典型的**本征应变 (eigenstrain)**，即一种非因机械外力而产生的固有应变。它是由温度场 $\Delta T(\mathbf{x}) = T(\mathbf{x}) - T_0$ 决定的一个已知场，其中 $T_0$ 是材料处于无应力状态的**参考温度**。$T_0$ 是一个关键的材料参数，它定义了应变的零点，任意改变 $T_0$ 的取值将会改变热应变量，进而影响应力计算结果。然而，理论对于温度标度的零点选择是不变的，即若将 $T$ 和 $T_0$ 同时平移一个常数 $c$，热应变 $\alpha(T-T_0)$ 不变，因此应力场也不变。[@problem_id:2701584] [@problem_id:2701632]

对于线性热弹性体，热应变与温度变化 $\Delta T$ 成正比：

$$
\boldsymbol{\varepsilon}^{th} = \boldsymbol{\alpha} \Delta T
$$

这里的 $\boldsymbol{\alpha}$ 是一个二阶张量，称为**热膨胀系数张量**。由于应变张量 $\boldsymbol{\varepsilon}^{th}$ 必然是对称的，热膨胀系数张量 $\boldsymbol{\alpha}$ 也必须是对称的，即 $\alpha_{ij} = \alpha_{ji}$。[@problem_id:2701591]

对于**各向异性**材料，$\boldsymbol{\alpha}$ 的分量取决于材料的晶体取向。当坐标系从材料主轴系（以正交矩阵 $\mathbf{Q}$ 描述）旋转到实验室坐标系时，$\boldsymbol{\alpha}$ 的分量遵循二阶张量的变换法则：

$$
\alpha'_{ij} = Q_{ip} Q_{jq} \alpha_{pq} \quad \text{或矩阵形式} \quad \boldsymbol{\alpha}' = \mathbf{Q} \boldsymbol{\alpha} \mathbf{Q}^T
$$

例如，如果一个材料在主轴方向的热膨胀系数为对角阵 $\boldsymbol{\alpha}^{\mathrm{mat}} = \mathrm{diag}(\alpha_1, \alpha_2, \alpha_3)$，当坐标系绕 $\mathbf{e}_3$ 轴旋转 $\theta$ 角时，新的坐标系下会产生剪切-伸长耦合项，如 $\alpha'_{12} = (\alpha_1 - \alpha_2) \cos\theta \sin\theta$。这表明，对于各向异性材料，均匀加热也可能引起剪切变形。[@problem_id:2701591]

对于**各向同性**材料，材料属性不随方向改变，因此热膨胀张量必须是各向同性张量，即与单位张量 $\mathbf{I}$（或克罗内克符号 $\delta_{ij}$）成正比：

$$
\alpha_{ij} = \alpha \delta_{ij}
$$

这里的标量 $\alpha$ 就是我们通常所说的**线性热膨胀系数**。它定义为在无应力（自由膨胀）条件下，单位长度材料因单位温度变化而产生的伸长量，即 $\alpha = (\frac{1}{L}\frac{\partial L}{\partial T})_{\sigma=0}$。[@problem_id:2928399]

在这种情况下，热应变为纯体积应变：$\boldsymbol{\varepsilon}^{th} = \alpha \Delta T \mathbf{I}$。其迹，即热致体积应变 $\varepsilon_{vol}^{th}$，为：

$$
\varepsilon_{vol}^{th} = \mathrm{tr}(\boldsymbol{\varepsilon}^{th}) = \mathrm{tr}(\alpha \Delta T \mathbf{I}) = \alpha \Delta T (\delta_{11}+\delta_{22}+\delta_{33}) = 3\alpha \Delta T
$$

因此，在自由膨胀条件下，体积应变随温度的变化率是线性膨胀系数的三倍。这个系数 $3\alpha$ 有时被称为**体热膨胀系数**。[@problem_id:2928399]

### 线性各向同性热弹性本构关系

结合上述概念，我们可以推导出适用于小应变、各向同性材料的完整热弹性本构关系，即**杜哈梅-诺伊曼 (Duhamel-Neumann) 方程**。

我们从胡克定律出发，它将应力与弹性应变关联起来：

$$
\boldsymbol{\sigma} = \lambda \mathrm{tr}(\boldsymbol{\varepsilon}^e) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}^e
$$

其中 $\lambda$ 和 $\mu$ 是拉梅 (Lamé) 常数。将应变分解式 $\boldsymbol{\varepsilon}^e = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{th}$ 代入，并使用各向同性热应变 $\boldsymbol{\varepsilon}^{th} = \alpha \Delta T \mathbf{I}$，我们得到：

$$
\boldsymbol{\sigma} = \lambda \mathrm{tr}(\boldsymbol{\varepsilon} - \alpha \Delta T \mathbf{I}) \mathbf{I} + 2\mu (\boldsymbol{\varepsilon} - \alpha \Delta T \mathbf{I})
$$

由于 $\mathrm{tr}(\boldsymbol{\varepsilon} - \alpha \Delta T \mathbf{I}) = \mathrm{tr}(\boldsymbol{\varepsilon}) - 3\alpha \Delta T = \varepsilon_{kk} - 3\alpha \Delta T$，上式可以整理为：

$$
\sigma_{ij} = 2\mu (\varepsilon_{ij} - \alpha \Delta T \delta_{ij}) + \lambda (\varepsilon_{kk} - 3\alpha \Delta T) \delta_{ij}
$$

这便是以总应变 $\varepsilon_{ij}$ 和温度变化 $\Delta T$ 表示的应力。[@problem_id:2701587] 该关系式可以进一步整理，将与应变和温度相关的项分开：

$$
\boldsymbol{\sigma} = (\lambda \varepsilon_{kk} \mathbf{I} + 2\mu \boldsymbol{\varepsilon}) - (3\lambda + 2\mu)\alpha \Delta T \mathbf{I}
$$

引入体积模量 $K = \lambda + \frac{2}{3}\mu$，则 $(3\lambda + 2\mu) = 3K$。于是，本构方程可以写成一个更具物理洞察力的形式：

$$
\boldsymbol{\sigma} = \mathbf{C} : \boldsymbol{\varepsilon} - 3K\alpha \Delta T \mathbf{I}
$$

这里，$\mathbf{C}$ 是四阶弹性张量。第二项 $-3K\alpha \Delta T \mathbf{I}$ 代表一个由温度变化引起的**静水压力**。当 $\Delta T > 0$（升温）时，它是一个压缩性的静水应力（如果变形受约束）。这清晰地表明，热膨胀效应是通过体积模量 $K$ 和热膨胀系数 $\alpha$ 耦合到力学行为中的。[@problem_id:2701587]

### 热应力的产生机制

热应力产生的根本原因是材料的**自由热变形**受到了阻碍。这种阻碍可以来自两个方面：外部施加的边界约束，或材料内部由非均匀温度场引起的变形不协调。[@problem_id:2701584]

#### 外部约束

当物体的边界位移受到限制，使其无法实现自由热膨胀或收缩时，就会产生应力。这是一个非常直接且常见的机制。

考虑一个初始长度为 $L_0$、在参考温度 $T_0$ 时无应力的杆件。当其温度均匀升高 $\Delta T$ 时，若不受约束，其长度会变为 $L_0(1+\alpha\Delta T)$，对应的自由热应变为 $\varepsilon^{th} = \alpha\Delta T$。[@problem_id:2701632]

*   **完全约束情况**：如果杆的两端被完全固定，使其总长度不能改变，那么总应变 $\varepsilon_{xx}$ 必须为零。根据应变分解 $\varepsilon_{xx} = \varepsilon^e_{xx} + \varepsilon^{th}_{xx}$，我们有 $0 = \varepsilon^e_{xx} + \alpha\Delta T$。这要求一个负的弹性应变 $\varepsilon^e_{xx} = -\alpha\Delta T$ 出现，以抵消热膨胀。由此产生的轴向应力为 $\sigma_{xx} = E \varepsilon^e_{xx} = -E\alpha\Delta T$。对于升温（$\Delta T > 0$），这是一个压应力。该应力的大小与杆的长度 $L_0$ 和截面积 $A$ 无关。[@problem_id:2701632] [@problem_id:2701584]

*   **部分或零约束情况**：如果杆的边界位移恰好被设定为 $u(L_0) - u(0) = \alpha\Delta T L_0$，那么运动学所要求的总应变 $\varepsilon_{xx} = \frac{u(L_0)-u(0)}{L_0} = \alpha\Delta T$ 正好等于自由热应变。此时，弹性应变 $\varepsilon^e_{xx} = \varepsilon_{xx} - \varepsilon^{th}_{xx} = 0$，因此杆内应力为零。[@problem_id:2701632]

这个简单的例子揭示了一个普遍原理：热应力的大小正比于**运动学上允许的总应变**与**材料自由热应变**之间的**失配 (mismatch)**。

#### 内部约束（不协调性）

即使一个物体完全不受外部载荷和约束（即处于**自由状态**），只要其内部的温度场分布不均匀，也可能产生应力。这种应力被称为**残余应力**或**自平衡应力**。

其根源在于**应变协调性 (strain compatibility)**。一个连续的固体能够保持其完整性，要求其总应变场 $\boldsymbol{\varepsilon}(\mathbf{x})$ 必须是“协调的”，即该应变场可以由一个连续、单值的位移场 $\mathbf{u}(\mathbf{x})$ 导出（$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$）。在数学上，这等价于圣维南 (Saint-Venant) 协调方程 $\mathrm{inc}(\boldsymbol{\varepsilon}) = 0$，其中 $\mathrm{inc}$ 是一个包含应变分量二阶偏导数的微分算子。

将协调性条件应用于应变分解式，我们得到：

$$
\mathrm{inc}(\boldsymbol{\varepsilon}) = \mathrm{inc}(\boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^{th}) = 0
$$

由于算子的线性，这可以写成：

$$
\mathrm{inc}(\boldsymbol{\varepsilon}^e) = -\mathrm{inc}(\boldsymbol{\varepsilon}^{th})
$$

这个方程的物理意义极为深刻。它表明，如果由温度场 $\Delta T(\mathbf{x})$ 产生的热应变场 $\boldsymbol{\varepsilon}^{th}(\mathbf{x})$ 本身是**不协调的**（即 $\mathrm{inc}(\boldsymbol{\varepsilon}^{th}) \neq 0$），那么为了保证总应变场 $\boldsymbol{\varepsilon}$ 的协调性，物体内部必须自动产生一个同样不协调的弹性应变场 $\boldsymbol{\varepsilon}^e$，其不协调性恰好与热应变场的相反。既然存在一个非零的弹性应变场，那么必然会有一个非零的应力场 $\boldsymbol{\sigma} = \mathbf{C}:\boldsymbol{\varepsilon}^e$ 与之对应。[@problem_id:2701619]

一个关键问题是：什么样的温度场会产生不协调的热应变？对于各向同性材料，$\varepsilon^{th}_{ij} = \alpha \Delta T \delta_{ij}$。在二维平面问题中，其不协调性由下式衡量：

$$
\mathcal{I} = \frac{\partial^2 \varepsilon^{th}_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon^{th}_{yy}}{\partial x^2} - 2\frac{\partial^2 \varepsilon^{th}_{xy}}{\partial x \partial y} = \alpha \left( \frac{\partial^2 \Delta T}{\partial y^2} + \frac{\partial^2 \Delta T}{\partial x^2} \right) = \alpha \nabla^2 (\Delta T)
$$

因此，热应变场是协调的，当且仅当温度场是一个**谐和函数**（$\nabla^2 T = 0$）。任何非谐和的温度分布（例如，存在局部热源或瞬态热传导过程中的温度分布）都会导致不协调的热应变，从而在一个自由体中产生内部应力。[@problem_id:2701624] [@problem_id:2701619]

例如，一个二次温度场 $T(x,y) = T_{ref} + ax + by + cx^2 + dxy + ey^2$，其拉普拉斯值为 $\nabla^2 T = 2c + 2e$。只有当 $c+e=0$ 时，该温度场才是谐和的，对应的热应变场才是协调的。否则，即使板件完全自由，也会因该温度场而产生内部应力。[@problem_id:2701624] 同样，一个形如 $\Delta T(x,y) = T_0(1 - \cos(\frac{\pi x}{L})\cos(\frac{\pi y}{L}))$ 的温度场，其拉普拉斯值通常不为零，因此必然会在自由体中诱发残余应力。[@problem_id:2701619]

### 高等专题与推广

前述的原理构成了热弹性理论的基础。在此之上，我们可以进行若干重要的推广。

#### 耦合与非耦合热弹性理论

到目前为止，我们的讨论都基于**非耦合 (uncoupled)** 热弹性理论。该理论包含一个单向的因果链：
1.  求解独立的热传导方程以获得温度场 $T(\mathbf{x}, t)$。
2.  将得到的温度场作为已知输入，代入热弹性力学方程中求解位移和应力。

在这种模型下，热传导方程不包含任何力学项：
$$
\rho c \dot{T} = k \nabla^2 T + r
$$
其中 $c$ 是比热，$k$ 是热导率，$r$ 是内热源。这种简化在大多数静态或准静态工程问题中是足够精确的。[@problem_id:2701601]

然而，物理现实是双向耦合的。力学变形也会影响温度，这种现象称为**热弹性效应**或压卡效应 (piezocaloric effect)：材料在快速压缩时会升温，快速膨胀时会降温。**全耦合 (fully coupled)** 理论将此效应纳入考虑。其力学平衡方程和本构关系与非耦合理论相同，但热传导方程中增加了一个耦合项：

$$
\rho c \dot{T} + 3K\alpha T_0 \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}) = k \nabla^2 T + r
$$

新增的项 $3K\alpha T_0 \mathrm{tr}(\dot{\boldsymbol{\varepsilon}})$ 代表了由体积应变率 $\mathrm{tr}(\dot{\boldsymbol{\varepsilon}})$ 引起的温度变化。当材料膨胀时（$\mathrm{tr}(\dot{\boldsymbol{\varepsilon}})>0$），该项为正，对 $\dot{T}$ 产生负贡献，导致降温，反之亦然。这个耦合项在高速变形或振动问题（如超声波传播）中变得十分重要。[@problem_id:2701601]

#### 有限应变热弹性理论

当变形不再微小时，小应变理论的假设不再成立，必须采用**有限应变 (finite strain)** 框架。此时，运动学描述变得更加复杂。

*   **运动学**：变形由变形梯度 $\mathbf{F} = \nabla_X \boldsymbol{\chi}$ 描述，应变通常使用格林-拉格朗日应变张量 $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$。
*   **动力学**：与 $\mathbf{E}$ 共轭的应力度量是第二皮奥拉-基尔霍夫 (Second Piola-Kirchhoff) 应力张量 $\mathbf{S}$。
*   **本构关系**：与小应变情况类似，本构关系同样可以从一个亥姆霍兹自由能函数 $\psi(\mathbf{E}, T)$ 导出，其形式为 $S = \partial\psi/\partial E$。

一个能够推广线性理论的合理有限应变自由能函数形式为：

$$
\psi(\mathbf{E},T) = \underbrace{\tfrac{1}{2}\lambda(\mathrm{tr}\mathbf{E})^2 + \mu \mathbf{E}:\mathbf{E}}_{\text{机械能 (St. Venant-Kirchhoff)}} - \underbrace{3K\alpha_T (T-T_0) \mathrm{tr}\mathbf{E}}_{\text{耦合项}} + \underbrace{c\Big[(T-T_0)-T\ln\Big(\tfrac{T}{T_0}\Big)\Big]}_{\text{热能}}
$$

这个势函数在应变为零、温度为参考温度 $T_0$ 时应力为零，并且能够正确地描述各向同性热膨胀。它清晰地展示了，即使在复杂的非线性框架下，通过热力学势函数构建本构关系的基本原理依然适用。[@problem_id:2701614]