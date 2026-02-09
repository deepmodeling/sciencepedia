## 引言
在工程与科学领域，准确描述材料在受力与温度变化下的行为至关重要。从桥梁设计到生物组织工程，我们依赖于能够预测材料变形、强度和失效的数学模型，即本构关系。然而，如何确保这些数学模型不仅仅是经验曲线的拟合，而是真正遵循宇宙的基本物理定律？这正是可变形固体热力学所要解决的核心问题。其关键在于，任何有效的本构理论都必须服从能量守恒（热力学第一定律）和熵增原理（热力学第二定律）的严格约束。

本文旨在系统地介绍现代连续介质力学中用于构建物理上自洽本构模型的强大框架。我们将聚焦于热力学第二定律的局部表达——克劳修斯-杜亥姆不等式，并展示它如何从一个看似抽象的物理约束，转变为推导具体材料模型的生成性工具。通过本文的学习，您将掌握连接基础物理与前沿材料建模的理论桥梁。

- 在第一章 **“原理与机制”** 中，我们将奠定理论基础，从连续介质的热力学定律出发，引入亥姆霍兹自由能等关键概念。您将学习如何运用科尔曼-诺尔程序，系统地从克劳修斯-杜亥姆不等式中分离出材料的弹性响应和耗散行为，并了解如何通过内变量理论将其推广至塑性等非弹性现象。

- 随后的 **“应用与跨学科联系”** 章节将展示该理论框架的广阔应用。我们将看到它如何自然地解释热弹性、各向异性、黏弹性和损伤等复杂行为，并探讨其在多孔介质力学、多尺度模拟和实验验证等交叉学科前沿中的核心作用。

- 最后，在 **“动手实践”** 部分，您将通过三个精心设计的计算问题，将抽象理论付诸实践。这些练习将引导您计算应力功率、验证超弹性材料的零耗散特性，并量化塑性变形中的能量耗散与温升，从而巩固您对核心概念的理解。

## 原理与机制

本章旨在系统性地阐述可变形固体的热力学理论框架。我们将从连续介质力学中的热力学第一和第二定律出发，建立一个严格的数学框架，用于推导材料的本构关系。这一框架的核心是 **克劳修斯-杜亥姆不等式 (Clausius-Duhem inequality)**，它为所有物理上可接受的材料行为设定了热力学约束。我们将详细介绍如何利用 **科尔曼-诺尔程序 (Coleman-Noll procedure)** 从该不等式中系统地推导出弹性和非弹性材料的本构方程，包括应力-应变关系和熵的表达式。最后，我们会探讨该框架在描述复杂材料行为（如塑性）时的应用，并讨论其理论边界与推广。

### 热力学基本定律的局部形式

在连续介质力学中，热力学定律以场的形式在物体中的每一点上都成立。这些局部形式的定律是我们构建本构理论的基石。

#### 能量守恒：第一定律

热力学第一定律即能量守恒定律。对于一个正在变形的连续体中的任意物质区域，其总能量（内能与动能之和）的变化率等于外力对该区域所做的功率与外界传入该区域的热量之和。通过应用雷诺输运定理和高斯散度定理，可以从其全局形式推导出适用于任意物质点的局部形式。

在现时构型（欧拉描述）下，忽略动能变化对内能演化的影响，能量守恒定律的局部形式可以写作一个关于比内能（单位质量的内能）$e$ 的演化方程 [@problem_id:2925263]：
$$
\rho \dot{e} = \boldsymbol{\sigma}:\mathbf{D} - \nabla\cdot\mathbf{q} + \rho r
$$
这里，每个符号都具有明确的物理意义：
- $\rho$ 是材料在现时构型下的质量密度。
- $\dot{e}$ 是比内能 $e$ 的**物质时间导数**，表示跟随一个特定物质点测量的内能变化率。
- $\boldsymbol{\sigma}$ 是 **柯西应力张量 (Cauchy stress tensor)**，它描述了物体内部的接触力状态。根据动量矩守恒，对于非极性材料，该张量是对称的。
- $\mathbf{D}$ 是**变形率张量 (rate of deformation tensor)**，定义为空间速度梯度 $\mathbf{L} = \nabla\mathbf{v}$ 的对称部分，即 $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$。它描述了物质点的变形速率。
- $\boldsymbol{\sigma}:\mathbf{D}$ 项是**应力功率密度 (stress power density)**，表示单位体积内，应力做功的速率。这是机械能转化为内能或从内能中释放出来的关键项。
- $\mathbf{q}$ 是**热流矢量 (heat flux vector)**，描述了通过单位面积的热量传输速率。
- $\nabla\cdot\mathbf{q}$ 是热流的散度，代表由于热传导导致的单位体积能量变化率。
- $r$ 是单位质量的**体积热源 (volumetric heat source)**，代表由辐射、化学反应等内部或外部源直接提供的热量。

这个方程明确指出，一个物质点的内能变化由三个因素贡献：应力做功、热量传导和内部热源。

#### 熵产不等式：第二定律

热力学第二定律为自然界中过程的方向性提供了基本约束，即孤立系统的总熵永不减少。在连续介质热力学中，这表现为一个关于熵产率的局部不等式，即 **克劳修斯-杜亥姆不等式**。它规定，在任何物理过程中，熵的产生率必须是非负的。其局部形式可写为：
$$
\rho \dot{s} + \nabla\cdot\left(\frac{\mathbf{q}}{\theta}\right) - \frac{\rho r}{\theta} \ge 0
$$
其中：
- $s$ 是比熵（单位质量的熵）。
- $\theta$ 是绝对温度，必须为正值 ($\theta > 0$)。
- $\rho\dot{s}$ 是单位体积的熵变化率。
- $\nabla\cdot(\mathbf{q}/\theta)$ 是熵流的散度。
- $\rho r/\theta$ 是由热源提供的熵。

这个不等式是本构理论的核心约束。任何描述材料行为的数学模型都必须保证在所有可能的热力学过程中，这个不等式都得到满足。我们的任务就是利用这个强大的约束来揭示材料本构关系的内在结构。

### 应力功率与共轭量：力学与热力学的桥梁

在能量守恒方程中，应力功率项 $\boldsymbol{\sigma}:\mathbf{D}$ 是连接力学变形与热力学状态的桥梁。为了在不同的运动学描述下（例如，参考构型与现时构型）都能正确地表达能量转换，我们需要引入不同的应力张量和与之共轭的应变率度量。

描述有限变形时，物体的运动由映射 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 定义，其中 $\mathbf{X}$ 是参考构型中的位置，$\mathbf{x}$ 是现时构型中的位置。**变形梯度 (deformation gradient)** $\mathbf{F} = \nabla_{\mathbf{X}}\boldsymbol{\chi}$ 是这一映射的局部线性近似。基于 $\mathbf{F}$，我们可以定义多种应力张量 [@problem_id:2925255]：

1.  **柯西应力张量 ($\boldsymbol{\sigma}$)**：这是一个空间张量，定义在现时构型上。它将现时构型中的单位法向量 $\mathbf{n}$ 映射为作用在该面上的真实牵引力（单位真实面积上的力）$\mathbf{t}$，即 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。由于动量矩守恒，$\boldsymbol{\sigma}$ 是对称的。

2.  **第一皮奥拉-基尔霍夫应力张量 ($\mathbf{P}$)**：这是一个两点张量，它将参考构型中的单位法向量 $\mathbf{N}$ 映射为现时构型中的力矢量。具体来说，它定义的“名义”牵引力 $\mathbf{T}_R$ 是作用在变形后物体上的力除以未变形时的参考面积。它与柯西应力的关系为：
    $$
    \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
    $$
    其中 $J = \det(\mathbf{F})$ 是体积变化率。$\mathbf{P}$ 通常不是对称的。

3.  **第二皮奥拉-基尔霍夫应力张量 ($\mathbf{S}$)**：这是一个物质张量，完全定义在参考构型上。它在能量和本构关系中扮演着核心角色。它与 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系为：
    $$
    \mathbf{S} = \mathbf{F}^{-1}\mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathsf{T}}
    $$
    如果 $\boldsymbol{\sigma}$ 是对称的，那么 $\mathbf{S}$ 也是对称的。

这些不同的应力度量之所以重要，是因为它们与不同的应变率度量在应力功率表达式中形成“能量共轭”对。应力功率，作为一个标量物理量，其值不应依赖于观察者的选择（即必须是**客观的**），也不应依赖于所使用的运动学描述。这导致了以下关键的等价关系 [@problem_id:2925234]：

$$
\mathcal{P}_0 = \mathbf{P}:\dot{\mathbf{F}} = \mathbf{S}:\dot{\mathbf{E}} = J(\boldsymbol{\sigma}:\mathbf{D})
$$

这里，$\mathcal{P}_0$ 是单位参考体积的应力功率。每个等式都揭示了一对能量共轭的量：
- $(\mathbf{P}, \dot{\mathbf{F}})$：第一皮奥拉-基尔霍夫应力与变形梯度的时间导数共轭。
- $(\mathbf{S}, \dot{\mathbf{E}})$：第二皮奥拉-基尔霍夫应力与**格林-拉格朗日应变张量 (Green-Lagrange strain tensor)** $\mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})$ 的时间导数共轭。
- $(\boldsymbol{\sigma}, \mathbf{D})$：柯西应力与变形率张量共轭。

这种共轭关系是建立本构理论的基础。例如，在参考构型中分析问题时，使用 $(\mathbf{S}, \mathbf{E})$ 对通常最为方便，因为它们都是物质张量，并且在刚体转动下不变（客观的），这极大地简化了本构方程的构建 [@problem_id:2925255]。

### 热力学势与克劳修斯-杜亥姆不等式

为了有效地利用克劳修斯-杜亥姆不等式，标准做法是引入一个**热力学势 (thermodynamic potential)**，最常用的是**亥姆霍兹自由能 (Helmholtz free energy)**。自由能的引入可以将不等式转化为一个更直接的形式，从而揭示本构关系。

我们首先将第一和第二定律合并。从第二定律出发，将第一定律代入以消去热源项 $r$，可以得到如下形式的不等式，称为**克劳修斯-普朗克不等式 (Clausius-Planck inequality)**：
$$
\boldsymbol{\sigma}:\mathbf{D} - \rho(\dot{e} - \theta\dot{s}) - \frac{1}{\theta}\mathbf{q}\cdot\nabla\theta \ge 0
$$
这个不等式依然包含了难以直接使用的内能变化率 $\dot{e}$ 和熵变率 $\dot{s}$。为了解决这个问题，我们定义比亥姆霍兹自由能 $\psi$：
$$
\psi = e - \theta s
$$
其物质时间导数为 $\dot{\psi} = \dot{e} - \dot{\theta}s - \theta\dot{s}$。通过这个定义，我们可以用 $\dot{\psi}$ 来替换 $\dot{e}$ 和 $\theta\dot{s}$ 的组合：$\rho(\dot{e} - \theta\dot{s}) = \rho(\dot{\psi} + s\dot{\theta})$。将此代入克劳修斯-普朗克不等式，我们得到一个只包含自由能变化率的最终形式：
$$
\boldsymbol{\sigma}:\mathbf{D} - \rho(\dot{\psi} + s\dot{\theta}) - \frac{1}{\theta}\mathbf{q}\cdot\nabla\theta \ge 0
$$
这个不等式是后续所有本构推导的出发点。它的优越性在于，如果我们将自由能 $\psi$ 视为一组**状态变量 (state variables)**（如应变和温度）的函数，那么 $\dot{\psi}$ 就可以通过链式法则表示为这些状态变量变化率的线性组合。这为我们系统地分离和约束本构关系提供了可能。

除了亥姆霍兹自由能，其他热力学势在特定条件下也很有用。例如，通过**勒让德变换 (Legendre transformation)**，我们可以定义不同的势，其自然变量也不同 [@problem_id:2925254]：
- **比内能 $u(\boldsymbol{\varepsilon}, s)$**：以应变和熵为自然变量。其导数给出应力和温度：$\boldsymbol{\sigma} = \rho \frac{\partial u}{\partial \boldsymbol{\varepsilon}}$ 和 $\theta = \frac{\partial u}{\partial s}$。
- **比亥姆霍兹自由能 $\psi(\boldsymbol{\varepsilon}, \theta)$**：以应变和温度为自然变量。其导数给出应力和熵：$\boldsymbol{\sigma} = \rho \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}$ 和 $s = -\frac{\partial \psi}{\partial \theta}$。
- **比吉布斯自由能 $g(p, \theta)$**：在静水压力 $p$ 条件下，以压力和温度为自然变量。其导数给出比容和熵：$1/\rho = \frac{\partial g}{\partial p}$ 和 $s = -\frac{\partial g}{\partial \theta}$。

选择哪个势函数取决于实验中更容易控制或测量的变量。对于固体力学，应变和温度通常是实验的输入，因此亥姆霍兹自由能是最常用的工具。

### 科尔曼-诺尔程序：从热力学推导本构律

科尔曼-诺尔程序是一种系统性的方法，它利用克劳修斯-杜亥姆不等式来推导材料的本构关系。这个程序的核心思想是：一个正确的本构理论必须保证热力学第二定律对于该材料**所有可能经历的物理过程**都成立。

让我们以一个有限变形的**热弹性材料 (thermoelastic material)** 为例，来演示这个程序的步骤 [@problem_id:2925267] [@problem_id:2925221]。对于这类材料，我们假设其热力学状态完全由应变（通过右柯西-格林张量 $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 度量）和温度 $\theta$ 决定。因此，单位参考体积的亥姆霍兹自由能可以写成函数 $\Psi = \hat{\Psi}(\mathbf{C}, \theta)$。

1.  **写出耗散不等式**：在参考构型中，使用共轭对应力 $(\mathbf{S}, \mathbf{E})$，并将自由能对时间的导数用链式法则展开，克劳修斯-杜亥姆不等式最终可以写成：
    $$
    \left(\frac{1}{2}\mathbf{S} - \frac{\partial\Psi}{\partial\mathbf{C}}\right):\dot{\mathbf{C}} - \left(\eta + \frac{\partial\Psi}{\partial\theta}\right)\dot{\theta} - \frac{1}{\theta}\mathbf{Q}\cdot\nabla_X\theta \ge 0
    $$
    其中 $\eta$ 是单位参考体积的熵，$\mathbf{Q}$ 是参考构型中的热流矢量。

2.  **应用独立性假设**：科尔曼-诺尔程序的关键假设是，在任意给定的状态 $(\mathbf{C}, \theta)$下，我们可以设计一个实验过程，使得该点的变化率 $\dot{\mathbf{C}}$ 和 $\dot{\theta}$ 可以被**独立地、任意地**指定。

3.  **分离可逆与不可逆部分**：观察上述不等式，它在率 $\dot{\mathbf{C}}$ 和 $\dot{\theta}$ 上是线性的。如果括号中的系数（例如 $\eta + \frac{\partial\Psi}{\partial\theta}$）不为零，我们总可以选择一个 $\dot{\theta}$（足够大且符号合适），使得整个不等式的左边变为负值，从而违反第二定律。为了确保不等式对所有可能的 $\dot{\mathbf{C}}$ 和 $\dot{\theta}$ 都成立，这些线性项的系数必须恒等于零。这就给出了材料的**无耗散**或**弹性**部分的本构关系：
    - **应力本构关系**：
      $$
      \mathbf{S} = 2\frac{\partial\Psi}{\partial\mathbf{C}}
      $$
      这一定义了**超弹性 (hyperelasticity)**：应力可以从一个标量势函数（自由能）的导数得到。
    - **熵本构关系**：
      $$
      \eta = -\frac{\partial\Psi}{\partial\theta}
      $$
      这表明熵也可以由自由能函数确定。

4.  **得到剩余耗散不等式**：将上述本构关系代入总的不等式后，与率相关的项消失了，只剩下与不可逆过程相关的部分，即**剩余耗散不等式 (residual dissipation inequality)**：
    $$
    -\frac{1}{\theta}\mathbf{Q}\cdot\nabla_X\theta \ge 0
    $$
    这个不等式约束了材料的耗散行为，这里是热传导。它要求热量必须从高温区流向低温区。一个满足此条件的充分条件是傅里叶热传导定律 $\mathbf{Q} = -\mathbf{K}\nabla_X\theta$，其中热传导张量 $\mathbf{K}$ 是半正定的。

在**小应变理论**中，上述框架得到极大简化 [@problem_id:2925245]。当位移梯度 $\|\nabla\mathbf{u}\| \ll 1$ 时，我们可以做如下近似：
- 运动学线性化：格林-拉格朗日应变 $\mathbf{E}$ 近似为无穷小应变张量 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathsf{T}})$。
- 体积变化忽略不计：$J \approx 1$，因此参考构型和现时构型中的密度和体积测度可以不加区分，$\rho \approx \rho_0$。
- 应变率近似：变形率张量等于应变张量的时间导数，$\mathbf{D} \approx \dot{\boldsymbol{\varepsilon}}$。
- 应力张量近似：不同应力张量之间的区别可以忽略，$\boldsymbol{\sigma} \approx \mathbf{P} \approx \mathbf{S}$。

在这些近似下，自由能可以视为 $\Psi = \hat{\Psi}(\boldsymbol{\varepsilon}, \theta)$，而应力本构关系简化为我们更熟悉的形式 [@problem_id:2925254]：
$$
\boldsymbol{\sigma} = \frac{\partial\Psi}{\partial\boldsymbol{\varepsilon}}
$$

### 内变量框架与非弹性材料

科尔曼-诺尔程序的美妙之处在于它可以被推广到描述具有内部耗散机制的**非弹性材料**，如粘塑性、塑性和损伤材料。其关键是引入一组**内状态变量 (internal state variables)**，记为 $\boldsymbol{\alpha}$。这些变量不是直接可控的宏观量（如应变或温度），而是描述了材料内部微观结构的状态，例如位错密度、塑性应变、损伤程度等 [@problem_id:2925222]。

在这种框架下，我们假设亥姆霍兹自由能不仅依赖于应变和温度，还依赖于这些内变量：$\Psi = \hat{\Psi}(\boldsymbol{\varepsilon}, \theta, \boldsymbol{\alpha})$。自由能的时间导数现在包含内变量的变化率：
$$
\dot{\Psi} = \frac{\partial\Psi}{\partial\boldsymbol{\varepsilon}}:\dot{\boldsymbol{\varepsilon}} + \frac{\partial\Psi}{\partial\theta}\dot{\theta} + \frac{\partial\Psi}{\partial\boldsymbol{\alpha}}\cdot\dot{\boldsymbol{\alpha}}
$$
将此代入耗散不等式并再次应用科尔曼-诺尔程序，我们发现：
- 弹性本构关系 $\boldsymbol{\sigma} = \frac{\partial\Psi}{\partial\boldsymbol{\varepsilon}}$ 和 $\eta = -\frac{\partial\Psi}{\partial\theta}$ 的形式保持不变。
- 剩余耗散不等式现在包含了一个由内变量演化引起的额外项：
  $$
  \mathbf{A}\cdot\dot{\boldsymbol{\alpha}} - \frac{1}{\theta}\mathbf{q}\cdot\nabla\theta \ge 0
  $$
  其中，我们定义了**热力学力 (thermodynamic force)** $\mathbf{A} = -\frac{\partial\Psi}{\partial\boldsymbol{\alpha}}$，它是与内变量 $\boldsymbol{\alpha}$ 共轭的广义力。

不等式的第一项 $\mathcal{D}_{int} = \mathbf{A}\cdot\dot{\boldsymbol{\alpha}}$ 代表了由材料内部微观结构重排所导致的**内在耗散 (intrinsic dissipation)**。第二定律要求这个耗散率必须是非负的（通常假设机械耗散和热耗散可以分开约束，即 $\mathcal{D}_{int} \ge 0$）。这个条件为内变量的**演化方程**（即 $\dot{\boldsymbol{\alpha}}$ 如何随加载和状态变化）提供了热力学约束。

作为一个重要的例子，考虑一个在等温条件下的**弹塑性材料** [@problem_id:2925220]。我们可以将弹性应变 $\boldsymbol{\varepsilon}^e$ 和一个描述加工硬化的标量内变量（如等效塑性应变）$\alpha_p$ 作为状态变量。总应变率为 $\mathbf{D} = \mathbf{D}^e + \mathbf{D}^p$。自由能为 $\Psi = \hat{\Psi}(\boldsymbol{\varepsilon}^e, \alpha_p)$。通过上述推导，可以证明在等温条件下，耗散不等式简化为：
$$
\mathcal{D}_{pl} = \boldsymbol{\sigma}:\mathbf{D}^p - \frac{\partial\Psi}{\partial\alpha_p}\dot{\alpha}_p \ge 0
$$
这个表达式具有清晰的物理意义：
- $\boldsymbol{\sigma}:\mathbf{D}^p$ 是**塑性功率**，即应力在塑性变形上所做的功。
- $\frac{\partial\Psi}{\partial\alpha_p}\dot{\alpha}_p$ 是由于材料硬化而储存在微观结构中的能量（**冷作硬化能**）的变化率。
- 因此，**塑性耗散** $\mathcal{D}_{pl}$ 等于总的塑性功率减去其中被储存起来作为微观结构能量的部分。耗散的能量最终以热的形式释放。

对于理想塑性材料（无硬化），自由能不依赖于 $\alpha_p$，因此 $\frac{\partial\Psi}{\partial\alpha_p}=0$。耗散就简化为塑性功率本身，$\mathcal{D}_{pl} = \boldsymbol{\sigma}:\mathbf{D}^p \ge 0$。例如，对于满足 von Mises (J2) 屈服准则的理想塑性材料，可以证明其耗散等于屈服应力 $\sigma_y$ 与等效塑性应变率 $\dot{\varepsilon}_p^{eq}$ 的乘积 [@problem_id:2925220]：
$$
\mathcal{D}_{pl} = \sigma_y \dot{\varepsilon}_p^{eq} \ge 0
$$

### 高级议题：理论的边界与推广

尽管科尔曼-诺尔程序功能强大，但其核心的“率的独立性”假设在某些情况下过于理想化，尤其是在处理非光滑、率无关的非弹性过程时 [@problem_id:2925262]。

例如，在率无关塑性理论中，塑性流动（即 $\dot{\boldsymbol{\alpha}} \ne 0$）仅当应力状态达到并停留在屈服面上时才会发生，并且其演化方向由流动法则（通常是屈服面的法线方向）确定。这意味着 $\dot{\boldsymbol{\alpha}}$ 既不是任意的，也不是独立于应变率 $\dot{\boldsymbol{\varepsilon}}$ 的。因此，科尔曼-诺尔程序的原始假设在此失效。

为了在数学上更严格地处理这些情况，发展了更通用的方法：
- **刘氏程序 (Liu's procedure)**：该方法使用拉格朗日乘子将能量平衡等其他平衡方程作为约束条件引入到熵不等式中。它不要求所有率都是独立的，因此更适合处理具有内部约束的系统。
- **广义标准材料 (Generalized Standard Materials, GSM)** 框架：这是一个现代的、功能强大的框架，它假设存在一个**耗散势 (dissipation potential)** $\phi$，该势是耗散率的函数。材料的演化法则通过该势的（次）梯度来定义。例如，热力学力 $\mathbf{A}$ 属于耗散势 $\phi(\dot{\boldsymbol{\alpha}})$ 在 $\dot{\boldsymbol{\alpha}}$ 点的次梯度，即 $\mathbf{A} \in \partial\phi(\dot{\boldsymbol{\alpha}})$。这种基于凸分析的方法能够自然地处理屈服面上的角点等非光滑问题，为率无关塑性等复杂行为提供了坚实的理论基础。

本章介绍的基于克劳修斯-杜亥姆不等式和科尔曼-诺尔程序的框架，是理解现代固体本构理论的基石。它不仅为弹性行为提供了严格的热力学基础，而且通过内变量的概念，为模拟各种复杂的非弹性现象（如塑性、粘弹性、损伤）开辟了系统性的途径。