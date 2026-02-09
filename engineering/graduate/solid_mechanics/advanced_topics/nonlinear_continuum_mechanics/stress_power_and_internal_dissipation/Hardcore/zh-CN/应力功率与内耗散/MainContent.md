## 引言
在现代工程科学与材料研究中，准确预测材料在复杂载荷下的行为是设计的核心。无论是承受循环载荷的聚合物，发生塑性变形的金属构件，还是逐渐开裂的混凝土结构，其内部都在发生着复杂的能量转换过程。应力功率与内耗散正是理解这些过程的关键概念，它们构成了从宏观力学变形到微观热力学耗散的桥梁，揭示了材料不可逆行为的本质。然而，如何在严格的理论框架下定义、分解和应用这些能量相关的量，从而建立物理上一致且具有预测能力的本构模型，是连续介质力学面临的一个核心问题。

本文旨在系统地阐明应力功率与内耗散的理论和应用。读者将通过本文学习到：
- **原理与机制**: 从第一性原理出发，推导应力功率的表达式，并基于热力学第二定律（克劳修斯-杜亥姆不等式）建立内耗散的基本概念，理解其与材料非弹性行为的深刻联系。
- **应用与交叉学科联系**: 探索这些原理在粘弹性、塑性、损伤及断裂力学等领域的具体应用，了解耗散如何量化滞回、塑性流动和材料退化，并触及其在摩擦学、孔隙介质力学等交叉学科中的作用。
- **动手实践**: 通过一系列精心设计的练习，从基本概念推导到高级计算分析，巩固对应力功率与内耗散的理解，并体会其在理论分析与数值模拟中的实际价值。

通过这三个层面的学习，本文将为读者构建一个关于材料能量转换与耗散的完整知识体系，为深入研究非弹性材料行为和高级计算力学奠定坚实的基础。

## 原理与机制

在连续介质力学中，理解材料内部能量的转换和耗散对于建立准确的本构模型和预测结构行为至关重要。应力功率和内耗散是连接力学变形与热力学过程的核心概念。本章旨在从第一性原理出发，系统地阐述这些概念，并探讨它们在不同材料模型和理论框架中的应用。

### 经典连续介质中的应力功率

我们首先考虑一个经典的、非极性的连续介质。在这种介质中，描述材料行为的基本物理量是应力场和运动场。

#### 内应力[功率密度](@entry_id:194407)的推导

应力功率密度，记为 $p$，定义为单位体积内应力在材料变形上做功的速率。为了推导其表达式，我们考虑一个占据空间区域 $\Omega(t)$ 的物体中的任意物质子区域 $V$。作用在该子区域上的力的总功率 $\mathcal{P}$ 来自于体积力 $\mathbf{b}$ 和面力 $\mathbf{t}$：

$$
\mathcal{P} = \int_V \mathbf{b} \cdot \mathbf{v} \, dV + \int_{\partial V} \mathbf{t} \cdot \mathbf{v} \, dS
$$

其中 $\mathbf{v}$ 是速度场，$\partial V$ 是子区域的边界。根据柯西公式，面力 $\mathbf{t}$ 与柯西应力张量 $\boldsymbol{\sigma}$ 的关系为 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$，其中 $\mathbf{n}$ 是边界的外法线向量。利用散度定理，表面积分可以转换成体积分：

$$
\int_{\partial V} \mathbf{t} \cdot \mathbf{v} \, dS = \int_V \nabla \cdot (\boldsymbol{\sigma}^{\mathsf{T}}\mathbf{v}) \, dV = \int_V \left( (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{v} + \boldsymbol{\sigma} : \nabla\mathbf{v} \right) dV
$$

这里，“$:$”表示张量的双点积，即 $\boldsymbol{\sigma} : \nabla\mathbf{v} = \sigma_{ij} (\nabla\mathbf{v})_{ji} = \sigma_{ij} v_{j,i}$。将此结果代入总功率表达式，我们得到：

$$
\mathcal{P} = \int_V \left( (\nabla \cdot \boldsymbol{\sigma} + \mathbf{b}) \cdot \mathbf{v} + \boldsymbol{\sigma} : \nabla\mathbf{v} \right) dV
$$

根据线性动量守恒定律（柯西第一运动定律），我们有 $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}$，其中 $\rho$ 是质量密度，$\mathbf{a}$ 是物质加速度。因此，总功率为：

$$
\mathcal{P} = \int_V \left( \rho \mathbf{a} \cdot \mathbf{v} + \boldsymbol{\sigma} : \nabla\mathbf{v} \right) dV
$$

总功率 $\mathcal{P}$ 用于两个方面：增加物体的动能和内部功。动能的变化率为 $\dot{K} = \int_V \rho \mathbf{a} \cdot \mathbf{v} \, dV$。因此，总的内功率 $P_{\text{int}}$ 为：

$$
P_{\text{int}} = \mathcal{P} - \dot{K} = \int_V \boldsymbol{\sigma} : \nabla\mathbf{v} \, dV
$$

由此，我们确定了**内应力[功率密度](@entry_id:194407)**的普适表达式为 $p = \boldsymbol{\sigma} : \nabla\mathbf{v}$。这个表达式是在没有对应力张量 $\boldsymbol{\sigma}$ 的对称性做任何假设的情况下得出的，因此它具有普遍性 [@problem_id:2691165]。

#### 运动学分解与应力对称性的作用

为了更深入地理解应力功率的物理意义，我们将速度梯度张量 $\mathbf{L} = \nabla\mathbf{v}$ 分解为其对称部分和反对称部分：

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

其中，$\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ 是**变形率张量**，描述了材料微元的拉伸和剪切；$\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$ 是**自旋张量**，描述了材料微元的刚性转动 [@problem_id:2691168]。

应力功率密度相应地可以写成：

$$
p = \boldsymbol{\sigma} : (\mathbf{D} + \mathbf{W}) = \boldsymbol{\sigma} : \mathbf{D} + \boldsymbol{\sigma} : \mathbf{W}
$$

在经典（非极性）连续介质中，角动量守恒定律要求柯西应力张量是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。一个基本的张量代数结论是，一个对称张量与一个反对称张量的双点积恒为零。因此，对于经典连续介质：

$$
\boldsymbol{\sigma} : \mathbf{W} = 0
$$

这意味着应力功率密度完全由应力在变形率上所做的功决定：

$$
p = \boldsymbol{\sigma} : \mathbf{D}
$$

这个重要的结论表明，在经典连续介质中，材料微元的纯刚性转动（由自旋张量 $\mathbf{W}$ 描述）不做功，只有变形（由变形率张量 $\mathbf{D}$ 描述）才与应力功相关 [@problem_id:2691165]。一个直观的例子是，当一个物体只进行刚体运动时，其内部没有任何形状或尺寸的改变，因此变形率张量 $\mathbf{D} = \mathbf{0}$。在这种情况下，即使物体内部存在应力，内应力[功率密度](@entry_id:194407)也必然为零 [@problem_id:2691193] [@problem_id:2691168]。

另一个有启发性的例子是静水压力状态，即 $\boldsymbol{\sigma} = -P\mathbf{I}$，其中 $P$ 是压力，$ \mathbf{I} $ 是单位张量。此时，应力功率为 $p = (-P\mathbf{I}) : \mathbf{D} = -P (\mathbf{I} : \mathbf{D}) = -P \operatorname{tr}(\mathbf{D})$。由于 $\operatorname{tr}(\mathbf{D})$ 代表了体积的相对变化率，这个表达式清晰地表明，静水压力只在体积发生变化时才做功 [@problem_id:2691168]。

### 热力学框架：从功率到耗散

机械功可以被可逆地储存为能量，也可以被不可逆地转化为热量。为了区分这两种情况，我们需要引入热力学第二定律。

#### 克劳修斯-杜亥姆不等式

我们将力学第一定律（能量守恒）和第二定律（熵增）结合，可以推导出对本构关系的核心约束——克劳修斯-杜亥姆不等式。对于在恒定均匀温度下发生的等温过程，该不等式（也称为耗散不等式）的局部空间形式为：

$$
\mathcal{D}_{\text{int}} = \boldsymbol{\sigma} : \mathbf{D} - \rho \dot{\psi} \ge 0
$$

其中，$\psi$ 是单位质量的亥姆霍兹自由能（$e - \theta\eta$，其中 $e$ 是内能，$\theta$ 是温度，$\eta$ 是熵），$\dot{\psi}$ 是其物质时间导数，$\rho\dot{\psi}$ 是单位体积自由能的储存率 [@problem_id:2887014]。

这个不等式具有深刻的物理意义：应力所做的总功率（$\boldsymbol{\sigma} : \mathbf{D}$）被分成了两部分。一部分是以自由能形式可逆地储存在材料中的功率（$\rho\dot{\psi}$），通常与弹性变形相关。另一部分，即它们的差值 $\mathcal{D}_{\text{int}}$，是**内耗散率**，它代表了因材料内部不可逆过程（如黏性流动、塑性变形或损伤）而转化为热的能量速率。热力学第二定律要求这个耗散率必须是非负的。

#### 耗散的实例：黏弹性与滞回

我们可以通过一个简单的黏弹性模型——开尔文-沃伊特（Kelvin-Voigt）模型——来具体说明耗散的概念 [@problem_id:2691192]。在一维情况下，该模型的应力-应变关系为：

$$
\sigma(t) = E\varepsilon(t) + \eta\dot{\varepsilon}(t)
$$

其中 $E$ 是弹性模量，$\eta$ 是黏度。对于这个模型，一个自然的选择是将亥姆霍兹自由能定义为纯弹性的部分，即 $\psi = \frac{1}{2\rho} E \varepsilon^2$。其储存率为 $\rho\dot{\psi} = E\varepsilon\dot{\varepsilon}$。

总应力功率为 $\sigma\dot{\varepsilon} = (E\varepsilon + \eta\dot{\varepsilon})\dot{\varepsilon} = E\varepsilon\dot{\varepsilon} + \eta\dot{\varepsilon}^2$。根据耗散不等式，内耗散率为：

$$
\mathcal{D}_{\text{int}} = \sigma\dot{\varepsilon} - \rho\dot{\psi} = (E\varepsilon\dot{\varepsilon} + \eta\dot{\varepsilon}^2) - E\varepsilon\dot{\varepsilon} = \eta\dot{\varepsilon}^2
$$

由于黏度 $\eta$ 和应变率的平方 $\dot{\varepsilon}^2$ 都是非负的，热力学第二定律得到满足。

如果我们对该材料施加一个闭合的应变循环（例如，从零加载到最大应变，再卸载回零），在一个循环内所做的总功为 $\oint \sigma d\varepsilon$。由于应变路径是闭合的，储存的弹性自由能的净变化为零，即 $\oint d\psi = 0$。因此，在一个循环中所做的总功完全等于总耗散：

$$
W_{\text{diss}} = \oint \sigma d\varepsilon = \oint \mathcal{D}_{\text{int}} dt = \oint \eta \dot{\varepsilon}^2 dt > 0
$$

这个非零的循环功在应力-应变图上表现为滞回环的面积。这一特性是区分耗散材料与纯弹性（或**超弹性**）材料的根本标志。对于超弹性材料，应力可以由一个应变能势函数导出，因此在任何闭合应变路径上所做的功都必须为零。开尔文-沃伊特模型由于其应力对应变率的依赖性（路径依赖性），显然不是超弹性的 [@problem_id:2691192]。

### 高级主题与现代理论

应力功率和内耗散的基本原理可以推广到更复杂和更现代的理论框架中，这些框架对于处理大变形和复杂的材料行为至关重要。

#### 大变形中的客观性

在有限变形理论中，一个核心挑战是如何定义应力的“变化率”。物质时间导数 $\dot{\boldsymbol{\tau}}$（其中 $\boldsymbol{\tau}$ 是柯西应力或基尔霍夫应力）并不是一个**客观的**（即与观察者无关的）张量率。这意味着在不同的刚性旋转坐标系下，$\dot{\boldsymbol{\tau}}$ 的变换规律与张量本身的变换规律不同 [@problem_id:2691194]。

如果在弹塑性或黏弹性本构关系中（例如，形式为“应力率 = $\mathbb{C}:\mathbf{D}$”的下弹性模型）错误地使用了非客观的应力率，将会导致物理上荒谬的结论。例如，一个受应力的物体在进行纯刚性转动时（$\mathbf{D}=\mathbf{0}$），这样的模型会错误地预测应力不发生变化（$\dot{\boldsymbol{\tau}}=\mathbf{0}$），而实际上应力张量应该随着物体一起旋转。这违反了**物质坐标无关性原理**。

为了确保本构定律的物理真实性，必须使用客观应力率，例如 Jaumann 率或 Truesdell 率。这些应力率通过引入自旋张量 $\mathbf{W}$ 来修正物质时间导数，从而消除了由观察者旋转引起的非客观项。只有这样，才能保证应力功率和内耗散的计算是独立于观察者的，从而正确地建立了应力与变形率之间的功共轭关系 [@problem_id:2691194]。

#### 非经典连续介质中的耗散

经典柯西理论并非唯一的连续介质模型。当材料具有显著的微观结构（如晶粒、纤维或颗粒）时，可能需要引入额外的运动学自由度。

一个重要的例子是**微极（Cosserat）介质**。该理论除了宏观位移场外，还引入了一个独立的微观转动场 $\boldsymbol{\varphi}$。这导致了非对称的柯西应力张量 $\boldsymbol{\sigma}$ 和一种新的广义应力——**力偶应力张量** $\boldsymbol{\mu}$ 的出现 [@problem_id:2691161]。

在这种更广义的框架下，内应力[功率密度](@entry_id:194407)的表达式也必须相应修正以保证客观性。正确的表达式为：

$$
p_{\text{int}} = \boldsymbol{\sigma} : (\nabla\mathbf{v} - \mathbf{W}(\boldsymbol{\omega})) + \boldsymbol{\mu} : \nabla\boldsymbol{\omega}
$$

其中 $\boldsymbol{\omega} = \dot{\boldsymbol{\varphi}}$ 是微观转动速率，$\mathbf{W}(\boldsymbol{\omega})$ 是其对应的反对称张量。这里，应力功率由两部分组成：一部分是非对称应力 $\boldsymbol{\sigma}$ 与相对变形率 $(\nabla\mathbf{v} - \mathbf{W}(\boldsymbol{\omega}))$ 之间的功共轭；另一部分是力偶应力 $\boldsymbol{\mu}$ 与微观转动速率梯度 $\nabla\boldsymbol{\omega}$ 之间的功共轭 [@problem_id:2691161]。这个例子表明，在非经典介质中，反对称应力确实可以做功，其功共轭对象是宏观运动与微观转动之间的相对转动速率。这也呼应了我们最初的分解，即当应力非对称时，$\boldsymbol{\sigma} : \mathbf{W}$ 项通常不为零 [@problem_id:2691165]。

#### 能量和变分方法

现代理论力学倾向于使用更抽象但功能强大的能量和变分框架来描述材料行为，特别是对于塑性等率无关过程。

**广义标准材料（GSM）** 框架是一个典范。它假设材料状态由应变 $\varepsilon$ 和一组内变量 $\alpha$ 描述。自由能 $\psi(\varepsilon, \alpha)$ 和耗散势 $\phi(\dot{\alpha})$ 是两个核心函数。通过公设化的本构关系（应力 $\sigma = \partial_{\varepsilon}\psi$）和演化法则（热力学力 $A = -\partial_{\alpha}\psi \in \partial_{\dot{\alpha}}\phi$），可以系统地构建热力学一致的模型。这个框架的优美之处在于，只要耗散势 $\phi$ 是凸函数且在 $\dot{\alpha}=0$ 处取最小值0，那么耗散非负性 ($A \cdot \dot{\alpha} \ge 0$) 就被自动满足。此外，自由能 $\psi$ 关于 $\varepsilon$ 的凸性保证了材料的稳定性（即切线刚度算子的椭圆性），而耗散势 $\phi$ 的严格凸性则保证了给定热力学力时内变量演化路径的唯一性，这对问题的适定性至关重要 [@problem_id:2691184]。

在**有限应变塑性**中，乘法分解 $\mathbf{F} = \mathbf{F}^{\text{e}}\mathbf{F}^{\text{p}}$ 是一个标准方法。其中一个关键的微妙之处在于，中间构型可以任意叠加一个刚性转动，而物理定律不应依赖于这个任意选择。为了使塑性耗散与这个中间构型的选择无关（即满足规范不变性），需要确定正确的功共轭对。研究表明，在各向同性材料的假设下，正确的应力措施是**Mandel应力** $\mathbf{M} = \mathbf{C}^{\text{e}}\mathbf{S}^{\text{e}}$，它与中间构型中的塑性变形率 $\mathbf{D}^{\text{p}}$ 共轭 [@problem_id:2691156]。这揭示了热力学、不变性原理与高级本构理论中应力-应变措施选择之间的深刻联系。

最后，最抽象的**能量表述**将整个问题提升到全局层面。它将系统的演化描述为两个基本原理的组合：一个**稳定性准则**和一个**能量平衡方程** [@problem_id:2691154]。稳定性准则要求系统在任一时刻都处于一个稳定的状态，即任何向邻近状态的虚拟转变所需的耗散代价都不能小于其可能带来的能量降低。能量平衡方程则精确地追踪了在整个加载历史中，外力功是如何分配给储存能和耗散能的。这个强大的框架为模拟断裂、损伤和塑性等复杂的率无关现象提供了坚实的数学基础，统一了本章所探讨的力学和热力学原理。