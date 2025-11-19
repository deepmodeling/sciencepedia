## 引言
[最小作用量原理](@entry_id:138921)是理论物理学中最深刻、最强大的基石之一。它提供了一个优雅而统一的框架，用以预测从单个粒子到整个宇宙的各类物理系统的动力学演化。这一原理的非凡之处在于，它将物理定律的探寻从寻找瞬时作用的“力”，转化为寻找一条使某个全局量——“作用量”——取极值的“最优”路径。本文旨在系统性地阐明这一原理，解决如何从一个单一的变分原则出发，推导出不同物理系统的[运动方程](@entry_id:170720)，并揭示其背后更深层次的结构。

在接下来的章节中，读者将踏上一段从基础到前沿的旅程。第一章“原理与机制”将奠定理论基础，详细阐述如何从作用量推导出欧拉-拉格朗日方程，探讨诺特定理如何连接[对称性与守恒律](@entry_id:160300)，并介绍处理高级理论（如规范理论）所必需的哈密顿形式和约束分析。第二章“应用与跨学科联系”将展示该原理的惊人普适性，探索其在广义相对论、粒子物理、凝聚态物理乃至宇宙学中的具体应用，彰显其作为统一物理学语言的角色。最后，第三章“动手实践”将通过一系列具体问题，巩固读者对核心概念的理解和计算能力。

让我们首先深入探讨[最小作用量原理](@entry_id:138921)的核心机制，看看它是如何将一个抽象的变分思想转化为描述我们宇宙动力学规律的精确数学方程的。

## 原理与机制

物理学的核心目标之一是预测系统如何随时间演化。在经典力学和[场论](@entry_id:155241)中，[作用量原理](@entry_id:154742)（Principle of Action），尤其是最小作用量原理，为此提供了一个极其深刻而强大的框架。该原理断言，一个物理系统所遵循的动力学轨迹，是在所有可能的轨迹中，使其“作用量”这一标量泛函取驻值的那个。本章旨在系统地阐述这一原理及其在[经典场论](@entry_id:149475)中的应用，从推导运动方程到揭示[对称性与守恒律](@entry_id:160300)之间的深刻联系，再到处理更高级的[约束系统](@entry_id:164587)和[引力](@entry_id:175476)理论中的边界效应。

### [欧拉-拉格朗日方程](@entry_id:137827)：从作用量到动力学

[理论物理学](@entry_id:154070)的核心构造是**作用量 (Action)** $S$，它是一个依赖于系统场构型 $\phi(x)$ 及其时空导数 $\partial_\mu \phi(x)$ 的泛函。作用量通常被写成拉格朗日密度 $\mathcal{L}$ 在整个时空 $\mathcal{M}$ 上的积分：
$$
S[\phi] = \int_{\mathcal{M}} d^D x \, \mathcal{L}(\phi(x), \partial_\mu \phi(x))
$$
其中 $d^D x$ 是 $D$ 维时空的[体积元](@entry_id:267802)。拉格朗日密度 $\mathcal{L}$ 封装了系统的全部动力学信息，包括其动能、[势能](@entry_id:748988)以及场之间的相互作用。

**[最小作用量原理](@entry_id:138921) (Principle of Least Action)** 指出，物理系统所实现的真实演化路径是使作用量 $S$ 取驻值（通常是最小值）的路径。数学上，这意味着对于场的任意微小变分 $\phi(x) \to \phi(x) + \delta\phi(x)$，作用量的一阶变分 $\delta S$ 为零，前提是变分在时空边界上为零。
$$
\delta S = 0
$$
通过对[作用量泛函](@entry_id:169216)进行变分并应用[分部积分](@entry_id:136350)，我们便能得到描述场演化的[微分方程](@entry_id:264184)，即**欧拉-拉格朗日方程 (Euler-Lagrange equation)**。对于单个[标量场](@entry_id:151443) $\phi$，其方程形式为：
$$
\frac{\partial \mathcal{L}}{\partial \phi} - \partial_\mu \left( \frac{\partial \mathcal{L}}{\partial (\partial_\mu \phi)} \right) = 0
$$
这个方程是[经典场论](@entry_id:149475)的基石。它将一个抽象的[变分原理](@entry_id:198028)转化为一个具体的、可解的动力学方程。

这个框架可以自然地推广到包含多种相互作用场的理论。例如，考虑一个将质量为 $m$ 的实标量场 $\phi$ 与质量为 $M$ 的[狄拉克费米子](@entry_id:161484)场 $\psi$ 耦合的汤川理论 (Yukawa theory)。其拉格朗日密度为 [@problem_id:420504]：
$$
\mathcal{L} = \frac{1}{2}(\partial_\mu \phi)(\partial^\mu \phi) - \frac{1}{2}m^2 \phi^2 + \bar{\psi}(i\gamma^\mu \partial_\mu - M)\psi - g\phi\bar{\psi}\psi
$$
这里， $g$ 是耦合常数，$\gamma^\mu$ 是[狄拉克矩阵](@entry_id:155614)，$\bar{\psi} = \psi^\dagger \gamma^0$。为了推导[狄拉克场](@entry_id:156753)的[运动方程](@entry_id:170720)，我们将 $\psi$ 和 $\bar{\psi}$ 视为独立的场变量。

对标量场 $\phi$ 应用欧拉-拉格朗日方程，我们得到带有[源项](@entry_id:269111)的[克莱因-戈登方程](@entry_id:153831) (Klein-Gordon equation)：
$$
(\partial_\nu \partial^\nu + m^2)\phi = -g\bar{\psi}\psi
$$
而对 $\bar{\psi}$ 进行变分（等价于对 $\bar{\psi}$ 应用[欧拉-拉格朗日方程](@entry_id:137827) $\frac{\partial\mathcal{L}}{\partial\bar{\psi}} = 0$），我们得到带有相互作用项的狄拉克方程 (Dirac equation)：
$$
(i\gamma^\mu \partial_\mu - M)\psi = g\phi\psi
$$
这些结果清晰地展示了[作用量原理](@entry_id:154742)如何系统地生成描述相互作用场系的耦合运动方程。场之间的相互作用在拉格朗日密度中表现为耦合项（如 $-g\phi\bar{\psi}\psi$），而在运动方程中则体现为源项或势能项。

### 几何作用量与扩展对象

[作用量原理](@entry_id:154742)的应用远不止于描述定义在平直时空背景上的场。它同样可以用来描述扩展对象（如弦或膜）的动力学，此时的作用量通常与这些对象在时空中扫过的“世界体积”的几何性质相关。

一个典型的例子是描述相对论性弦运动的**[南部-后藤作用量](@entry_id:157897) (Nambu-Goto action)** [@problem_id:420545]。弦在 $D$ 维闵可夫斯基时空中的运动轨迹形成一个二维[曲面](@entry_id:267450)，称为**世界面 (worldsheet)**。该作用量正比于世界面的面积：
$$
S[X^\mu] = -T_0 \int d\tau d\sigma \sqrt{-h}
$$
其中，$T_0$ 是[弦张力](@entry_id:141324)，$(\tau, \sigma)$ 是世界面参数，$X^\mu(\tau, \sigma)$ 是描述世界面如何嵌入到目标时空的嵌入函数。$h$ 是世界面上[诱导度规](@entry_id:160616) $h_{\alpha\beta}$ 的[行列式](@entry_id:142978)，其定义为：
$$
h_{\alpha\beta} = \eta_{\mu\nu} (\partial_\alpha X^\mu) (\partial_\beta X^\nu)
$$
这里 $\eta_{\mu\nu}$ 是背景时空的[闵可夫斯基度规](@entry_id:154660)。

与标准的[场论](@entry_id:155241)拉格朗日密度相比，[南部-后藤作用量](@entry_id:157897)的形式更为复杂，因为它包含一个平方根，使得它对导数 $\partial_\alpha X^\mu$ 的依赖是高度[非线性](@entry_id:637147)的。尽管如此，我们依然可以应用[最小作用量原理](@entry_id:138921)。对 $X^\mu$ 进行变分 $\delta X^\mu$，并执行一系列计算，包括[行列式](@entry_id:142978)的[变分法](@entry_id:163656)则 $\delta h = h h^{\alpha\beta} \delta h_{\alpha\beta}$ 和分部积分，最终可以得到弦的经典运动方程：
$$
\partial_\alpha \left( \sqrt{-h} \, h^{\alpha\beta} \partial_\beta X^\mu \right) = 0
$$
这个方程具有深刻的几何意义。它表明，经典弦的世界面是在目标时空中的一个极小曲面。这一结果展示了[作用量原理](@entry_id:154742)的普适性，它能够从一个纯粹的几何假设（作用量是世界面面积）出发，导出具体的物理运动定律。

### [从拉格朗日到哈密顿](@entry_id:164887)：正则形式

虽然[拉格朗日形式](@entry_id:145697)在彰显对称性和建立协变理论方面非常优雅，但哈密顿形式在量子化、相[空间分析](@entry_id:183208)和[约束系统](@entry_id:164587)研究中则更为根本。从[拉格朗日形式](@entry_id:145697)到**哈密顿形式 (Hamiltonian formalism)** 的转换通过**勒让德变换 (Legendre transformation)** 完成。

对于一个场 $\phi$，其**[正则动量](@entry_id:155151)密度 (canonical momentum density)** $\pi$ 定义为拉格朗日密度对场的时间导数 $\dot{\phi} \equiv \partial_0 \phi$ 的偏导数：
$$
\pi = \frac{\partial \mathcal{L}}{\partial \dot{\phi}}
$$
**哈密顿密度 (Hamiltonian density)** $\mathcal{H}$ 则是：
$$
\mathcal{H} = \pi \dot{\phi} - \mathcal{L}
$$
关键步骤是，我们必须通过求解 $\pi$ 的定义式来将 $\dot{\phi}$ 表示为 $\pi$、$\phi$ 及其空间导数 $\nabla\phi$ 的函数，从而使得最终的哈密顿密度 $\mathcal{H}$ 完全由相空间变量 $(\phi, \pi)$ 和空间导数 $\nabla\phi$ 描述。

对于一个标准的实标量场，$\mathcal{L} = \frac{1}{2}\dot{\phi}^2 - \frac{1}{2}(\nabla\phi)^2 - V(\phi)$，这个过程很简单：$\pi = \dot{\phi}$，因此 $\mathcal{H} = \frac{1}{2}\pi^2 + \frac{1}{2}(\nabla\phi)^2 + V(\phi)$。然而，对于动能项非标准的理论，这个过程会更加复杂。

考虑一个由**狄拉克-玻恩-英费尔德 (Dirac-Born-Infeld, DBI)** 类型拉格朗日密度描述的标量场 [@problem_id:420608]：
$$
\mathcal{L} = -V(\phi) \sqrt{1 - \partial_\mu \phi \, \partial^\mu \phi} = -V(\phi) \sqrt{1 - \dot{\phi}^2 + (\nabla \phi)^2}
$$
这种形式的[拉格朗日量](@entry_id:174593)出现在[弦理论](@entry_id:145688)的 [D-膜](@entry_id:147530)动力学中。其[正则动量](@entry_id:155151)为：
$$
\pi = \frac{\partial \mathcal{L}}{\partial \dot{\phi}} = \frac{V(\phi) \dot{\phi}}{\sqrt{1 - \dot{\phi}^2 + (\nabla \phi)^2}}
$$
这个关系式是[非线性](@entry_id:637147)的，但我们仍可以将其反解，得到 $\dot{\phi}$ 关于 $\pi$ 的表达式。经过代数运算，我们可以将 $\dot{\phi}$ 和 $\mathcal{L}$ 都用 $(\phi, \pi, \nabla\phi)$ 表示，并最终推导出哈密顿密度：
$$
\mathcal{H} = \sqrt{\left(V(\phi)^2 + \pi^2\right)\left(1 + (\nabla \phi)^2\right)}
$$
这个非平凡的结果展示了勒让德变换作为一个系统性程序，能够处理具有高度[非线性](@entry_id:637147)动能项的理论。总[哈密顿量](@entry_id:172864) $H = \int d^3x \, \mathcal{H}$ 代表系统的总能量，它的守恒性是[时间平移对称性](@entry_id:261093)的直接结果 [@problem_id:420407]。

### 对称性、[诺特定理](@entry_id:145690)与守恒律

物理学中最深刻的见解之一是**[诺特定理](@entry_id:145690) (Noether's Theorem)**，它建立了作用量的**连续对称性 (continuous symmetry)** 与**守恒律 (conservation law)** 之间的[一一对应](@entry_id:143935)关系。

如果一个作用量在某个连续变换下保持不变（例如，场的相位旋转或时空平移），那么理论中就必定存在一个守恒量。这个守恒量由一个[守恒流](@entry_id:148966) $j^\mu$ 给出，它满足[连续性方程](@entry_id:195013) $\partial_\mu j^\mu = 0$。对应的[守恒荷](@entry_id:145660) $Q = \int d^{D-1}x \, j^0$ 在时间上是恒定的，即 $\frac{dQ}{dt}=0$。

#### [时空对称性](@entry_id:179029)与能量-动量张量

时空平移不变性，即拉格朗日密度不显含时空坐标 $x^\mu$，导致了能量和动量的守恒。与之对应的[守恒流](@entry_id:148966)是**能量-动量张量 (stress-energy tensor)** $T^{\mu\nu}$。通过诺特程序得到的正则[能量-动量张量](@entry_id:203902)为：
$$
T_c^{\mu\nu} = \frac{\partial\mathcal{L}}{\partial(\partial_\mu \phi_\alpha)}\partial^\nu \phi_\alpha - \eta^{\mu\nu}\mathcal{L}
$$
其中 $\phi_\alpha$ 代表系统中的所有场。守恒的[四动量](@entry_id:264378) $P^\mu = \int d^3x \, T^{0\mu}$ 就是总能量 ($P^0$) 和总动量 ($P^i$)。

然而，这个正则张量 $T_c^{\mu\nu}$ 通常不是对称的，这在与广义相对论耦合时会产生问题。幸运的是，我们可以对其进行改进。**贝尔凡特-罗森菲尔德 (Belinfante-Rosenfeld)** 程序提供了一种系统性的方法，通过在 $T_c^{\mu\nu}$ 上增加一个散度为零的项，来构造一个新的、对称的能量-动量张量 $T_{BR}^{\mu\nu}$，它给出相同的[守恒荷](@entry_id:145660)。

以描述大质量矢量[玻色子](@entry_id:138266)的**[普罗卡理论](@entry_id:191071) (Proca theory)** 为例 [@problem_id:420466]，其拉格朗日密度为 $\mathcal{L} = -\frac{1}{4} F_{\mu\nu}F^{\mu\nu} + \frac{1}{2}m^2 A_\mu A^\mu$。人们可以计算出其对称的贝尔凡特-罗森菲尔德[张量的迹](@entry_id:190669)。在满足普罗卡运动方程（$\partial_\mu F^{\mu\nu} = -m^2 A^\nu$）的条件下，我们发现：
$$
T^\mu_{\mu,BR} = -m^2 A_\mu A^\mu
$$
这个结果意义深远。对于无质量的场（如[电磁场](@entry_id:265881)），[能量-动量张量](@entry_id:203902)的迹为零，这对应于经典理论的**标度不变性 (scale invariance)**。而对于有质量的[普罗卡场](@entry_id:173172)，其迹不为零，且正比于 $m^2$。这表明质量项 $m^2 A_\mu A^\mu$ 明确地破坏了标度不变性。

#### 内部[对称性与守恒](@entry_id:154858)荷作为生成元

除了[时空对称性](@entry_id:179029)，[场论](@entry_id:155241)还常常具有**内部对称性 (internal symmetry)**。一个典型的例子是描述[复标量场](@entry_id:159799)的拉格朗日密度 $\mathcal{L} = (\partial_\mu \phi^*)(\partial^\mu \phi) - m^2 \phi^* \phi$ 所具有的全局 $U(1)$ 相位[旋转对称](@entry_id:137077)性：$\phi \to e^{i\alpha}\phi$。

根据[诺特定理](@entry_id:145690)，这个对称性对应一个守恒的[诺特荷](@entry_id:138226) $Q$。在哈密顿形式下，这个荷表示为：
$$
Q = i \int d^d z \, \left( \phi(\vec{z}) \pi(\vec{z}) - \phi^*(\vec{z}) \pi^*(\vec{z}) \right)
$$
在[哈密顿力学](@entry_id:146202)中，守恒量扮演着双重角色：它们不仅是[演化过程](@entry_id:175749)中的[不变量](@entry_id:148850)，还是[对称变换](@entry_id:144406)的**生成元 (generator)**。一个[可观测量](@entry_id:267133) $F$ 在由参数 $\epsilon$ 和生成元 $G$ 描述的无穷小变换下的变化由**[泊松括号](@entry_id:151133) (Poisson bracket)** 给出：$\delta F = \epsilon \{F, G\}$。

对于 $U(1)$ 对称性，场的无穷小变换是 $\delta\phi = i\alpha\phi$。我们可以验证，[守恒荷](@entry_id:145660) $Q$ 确实是这个[变换的生成元](@entry_id:172031)。通过使用场的正则[泊松括号](@entry_id:151133)关系，如 $\{\phi(t, \vec{x}), \pi(t, \vec{y})\} = \delta^{(d)}(\vec{x}-\vec{y})$，我们可以直接计算 [@problem_id:420403]：
$$
\{\phi(t, \vec{x}), Q\} = i \phi(t, \vec{x})
$$
这个结果精确地表明，[守恒荷](@entry_id:145660) $Q$ 通过泊松括号作用在场 $\phi$ 上，重现了其无穷小变换的形式。这建立了对称性、守恒律和[哈密顿动力学](@entry_id:156273)之间的深刻联系。

### [约束哈密顿系统](@entry_id:169165)

在某些理论中，特别是规范理论（如电磁学和[杨-米尔斯理论](@entry_id:137401)）和[引力](@entry_id:175476)理论中，拉格朗日是“奇异的”(singular)。这意味着[正则动量](@entry_id:155151)的定义式 $\pi_a = \partial\mathcal{L}/\partial\dot{q}_a$ 无法对所有的速度 $\dot{q}_a$ 进行反解。其后果是在相空间中出现了一些**约束 (constraints)**，即一些只依赖于[广义坐标](@entry_id:156576)和动量的关系式 $\Phi(\phi, \pi) \approx 0$。这里的 "$\approx$" 符号表示“弱等于”，意味着这个等式只在被称为约束[曲面](@entry_id:267450)的相空间[子空间](@entry_id:150286)上成立。

由 Paul Dirac 和 Peter Bergmann 发展的**狄拉克-贝尔格曼程序 (Dirac-Bergmann procedure)** 提供了一套处理这类[约束系统](@entry_id:164587)的系统方法。
1.  **主约束 (Primary Constraints)**：直接从[正则动量](@entry_id:155151)的定义中产生的约束。例如，对于[电磁场](@entry_id:265881) $A_\mu$，由于拉格朗日密度不含 $\partial_0 A_0$，我们立即得到主约束 $\pi^0 \approx 0$。
2.  **总[哈密顿量](@entry_id:172864) (Total Hamiltonian)**：系统的演化由总[哈密顿量](@entry_id:172864) $H_T = H_c + \sum_i u_i \Phi_i$ 生成，其中 $H_c$ 是正则[哈密顿量](@entry_id:172864)，$\Phi_i$ 是主约束，$u_i$ 是[拉格朗日乘子](@entry_id:142696)。
3.  **[次级约束](@entry_id:165897) (Secondary Constraints)**：约束必须在时间演化中保持。要求主约束的时间导数（即其与总[哈密顿量](@entry_id:172864)的[泊松括号](@entry_id:151133)）弱等于零，$\dot{\Phi}_i = \{\Phi_i, H_T\} \approx 0$，这可能会产生新的、不依赖于拉格朗日乘子的约束，称为[次级约束](@entry_id:165897)。这个过程需要迭代，直到不再产生新的约束为止。
4.  **第一类与[第二类约束](@entry_id:175584) (First- and Second-Class Constraints)**：所有约束（主约束和[次级约束](@entry_id:165897)）可以分为两类。如果一个约束 $\Phi_A$ 与所有其他约束的[泊松括号](@entry_id:151133)都在约束[曲面](@entry_id:267450)上为零（即 $\{\Phi_A, \Phi_B\} \approx 0$ for all $B$），则称其为**[第一类约束](@entry_id:168143)**。否则，它就是**[第二类约束](@entry_id:175584)**。[第一类约束](@entry_id:168143)与[规范对称性](@entry_id:136438)密切相关，而[第二类约束](@entry_id:175584)则对应于相空间中的冗余、非物理的自由度。

例如，在一个 U(1) 规范理论的[一阶表述](@entry_id:265920)中 [@problem_id:420603]，通过完整的约束分析，可以发现系统存在两个局域的[第一类约束](@entry_id:168143)：$\pi^0 \approx 0$ 和[次级约束](@entry_id:165897) $\partial_i \pi^i \approx 0$（高斯定律）。这两个约束正是 U(1) 规范对称性的生成元。

为了处理[第二类约束](@entry_id:175584)并进行量子化，Dirac 引入了**[狄拉克括号](@entry_id:178441) (Dirac bracket)**。对于任意两个相空间函数 $F$ 和 $G$，其[狄拉克括号](@entry_id:178441)定义为：
$$
\{F, G\}_D = \{F, G\} - \sum_{a,b} \{F, \chi_a\} C_{ab}^{-1} \{\chi_b, G\}
$$
其中 $\chi_a$ 是[第二类约束](@entry_id:175584)的集合，$C_{ab} = \{\chi_a, \chi_b\}$ 是它们[泊松括号](@entry_id:151133)构成的矩阵。[狄拉克括号](@entry_id:178441)的优点在于，它与任何[第二类约束](@entry_id:175584)的括号都恒等于零，$\{\cdot, \chi_a\}_D = 0$。这意味着我们可以在计算完[狄拉克括号](@entry_id:178441)之后，将[第二类约束](@entry_id:175584)作为强等式（即 "="）代入方程中，从而将理论限制在一个更小的、物理的相空间上。

一个引人注目的例子是 (2+1) 维时空中的拓扑质量电动力学，其拉格朗日中包含一个陈-西蒙斯项 [@problem_id:420487]。在选择了特定的[规范固定](@entry_id:142821)条件（如[库仑规范](@entry_id:273044) $\partial_i A^i \approx 0$）后，系统会出现一系列[第二类约束](@entry_id:175584)。计算这些约束之间的[狄拉克括号](@entry_id:178441)会得到一个惊人的结果：[正则动量](@entry_id:155151)分量之间的[狄拉克括号](@entry_id:178441)不再为零！
$$
\{\pi^i(\mathbf{x}), \pi^j(\mathbf{y})\}_D = m \epsilon^{ij} \delta^2(\mathbf{x}-\mathbf{y})
$$
这个非零的结果表明，即使在经典层面上，相空间的几何结构也因拓扑质量项的存在而发生了根本性的改变。

### 边界项与变分原理的修正

在应用[作用量原理](@entry_id:154742)时，我们通常假设场在时空边界上的变分为零。然而，在某些情况下，例如在有边界的[流形](@entry_id:153038)上研究[引力](@entry_id:175476)时，作用量本身的变分就会在边界上产生不希望出现的项。为了得到一个定义良好的（well-posed）[变分问题](@entry_id:756445)，即从[作用量原理](@entry_id:154742)可以推导出正确的体[运动方程](@entry_id:170720)，这些边界项必须被消除。

最著名的例子是广义相对论中的**爱因斯坦-[希尔伯特作用量](@entry_id:204075) (Einstein-Hilbert action)**。由于其拉格朗日密度（[里奇标量](@entry_id:158934) $R$）包含度规的[二阶导数](@entry_id:144508)，对其进行变分时，分部积分会产生一个边界项，该项依赖于度规变分 $\delta g_{\mu\nu}$ 在边界上的值。为了抵消这个项，必须在原作用量上额外增加一个**吉本斯-霍金-约克 (Gibbons-Hawking-York, GHY)** 边界项。
$$
S_{GHY} = \frac{1}{8\pi G} \int_{\partial\mathcal{M}} d^{D-1}x \sqrt{|h|} K
$$
其中 $\partial\mathcal{M}$ 是时空边界，$h$ 是边界上的[诱导度规](@entry_id:160616)，$K$ 是边界的**[外在曲率](@entry_id:160405) (extrinsic curvature)** 的迹。外在曲率描述了边界是如何嵌入到周围的时空中的。

计算[外在曲率](@entry_id:160405)是[引力](@entry_id:175476)理论中的一项基本技术，尤其在[黑洞热力学](@entry_id:136383)和 AdS/CFT 对偶中至关重要。例如，我们可以考虑一个位于 $r=r_0$ 的球形边界，它包围着一个 $D=4$ 维反德西特 (AdS) 时空的一部分 [@problem_id:420514]。通过计算该边界超曲面的[单位法向量](@entry_id:178851) $n^\mu$ 及其[协变散度](@entry_id:275039) $\nabla_\mu n^\mu$，我们可以得到[外在曲率](@entry_id:160405)的迹 $K$。对于一个度规为 $ds^2 = -(1+k^2 r^2)dt^2 + \frac{dr^2}{1+k^2 r^2} + r^2 d\Omega^2$ 的AdS时空，在半径为 $r_0$ 的边界上，其值为：
$$
K(r_0) = \frac{2 + 3k^2 r_0^2}{r_0 \sqrt{1 + k^2 r_0^2}}
$$
这个 GHY 项的加入，确保了爱因斯坦-[希尔伯特作用量](@entry_id:204075)的[变分原理](@entry_id:198028)是自洽的，并为研究时空本身的动力学提供了一个坚实的理论基础。它再次彰显了[作用量原理](@entry_id:154742)的深刻性——即使是理论的边界条件和一致性要求，也可以被优雅地纳入这个统一的框架之内。