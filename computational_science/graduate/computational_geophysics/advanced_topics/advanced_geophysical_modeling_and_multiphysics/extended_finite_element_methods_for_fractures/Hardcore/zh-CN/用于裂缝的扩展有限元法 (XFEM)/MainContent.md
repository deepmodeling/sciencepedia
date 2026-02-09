## 引言
模拟裂缝和其他不连续性是计算地球物理学和工程力学中的一个关键挑战，因为这些特征往往决定了岩体等材料的力学和输运特性。标准数值方法，如有限元法（FEM），其内在设计适用于连续介质，在表示与裂缝相关的跳跃和奇异性时面临困难，这导致了严重的精度问题或因需要不断重新划分网格而产生高昂的计算成本。扩展有限元法（XFEM）正是为了解决这一根本性的知识鸿沟而出现的，它提供了一种优雅的方式，可以在不依赖于计算网格的情况下模拟不连续性。

本文对用于裂缝模拟的XFEM进行了全面探索，其结构旨在引导您从基础理论走向实际应用。第一章“原理与机制”深入探讨了XFEM的理论核心，解释了它如何利用单位分解框架和专门的富集函数来捕捉裂缝行为。第二章“应用与交叉学科联系”通过探讨该方法在高级断裂力学和如水力压裂等复杂多物理场问题中的应用，展示了其多功能性。最后，“动手实践”部分提供了一系列针对性的问题，以巩固您对关键实施概念的理解。通过学习这些章节，您将对应用XFEM解决具有挑战性的不连续性问题，获得关于“为什么”和“如何做”的坚实理解。

## 原理与机制

本章旨在深入探讨扩展有限元法（XFEM）的核心原理与关键机制。我们将从标准有限元法在处理不连续问题时遇到的根本局限性出发，系统阐述支撑XFEM的单位分解法（Partition of Unity Method）思想。随后，我们将详细介绍两种关键的富集技术：用于模拟位移跳跃的亥维赛（Heaviside）富集和用于捕捉裂尖应力奇异性的分支函数（branch function）富集。最后，本章将讨论在实际应用中保证XFEM精度、稳定性和收敛性所必须克服的几个高级问题，包括数值积分、系统矩阵的条件数以及混合单元（blending element）的处理。

### 标准有限元法处理不连续性问题的局限

在计算力学中，有限元法（FEM）是一种极为成功的数值工具，但其标准形式是为求解连续介质问题而设计的。标准有限元法的核心思想是利用分片连续的多项式基函数（即形函数）来逼近解。这些基函数，例如$C^0$拉格朗日多项式，在整个求解域$\Omega$上是连续的。因此，由这些基函数线性组合构成的任何有限元逼近解$u_h$也必然是全局连续的。从数学上看，标准有限元逼近空间$V_h$是索博列夫空间$H^1(\Omega)$的一个子空间，该空间中的所有函数都具有平方可积的一阶弱导数，且函数本身在域内是连续的。

然而，当地质体力学问题中涉及裂纹或断层时，物理场（如位移场）的性质发生了根本改变。一条内部裂纹$\Gamma_c$会将求解域$\Omega$分割成两个或多个子域（例如$\Omega^+$和$\Omega^-$），位移场$\boldsymbol{u}$在穿过裂纹面$\Gamma_c$时会产生跳跃，即$\llbracket \boldsymbol{u} \rrbracket \neq \boldsymbol{0}$。一个包含跳跃不连续的函数，其梯度在不连续面上表现为狄拉克$\delta$分布，因此其弱导数在整个域$\Omega$上不是平方可积的。这意味着真实的解$\boldsymbol{u}$不属于$H^1(\Omega)$空间，而是属于一个“破碎”的索博列夫空间，例如$H^1(\Omega \setminus \Gamma_c)$，该空间允许函数在子域$\Omega^+$和$\Omega^-$上分别为$H^1$函数，但在它们之间的界面$\Gamma_c$上不要求连续。

这种函数空间的根本不匹配，正是标准有限元法无法直接模拟裂纹的症结所在 [@problem_id:3590683]。用连续的逼近函数$u_h \in V_h \subset H^1(\Omega)$去逼近一个不连续的真实解$u \in H^1(\Omega \setminus \Gamma_c)$，本质上是“用连续的线去画一条断开的线”。尽管可以通过加密网格来模拟一个非常陡峭的梯度，但永远无法真正地、精确地捕捉到一个有限的跳跃。这会导致在裂纹附近产生巨大的逼近误差，并破坏有限元法应有的最优收敛率。

传统上，为了克服这一难题，工程师们采用**网格自动剖分（remeshing）**的方法。这种策略的核心是让有限元网格的边界与裂纹的几何边界完全重合，即**网格共形（mesh conformity）**。通过在裂纹面上创建重合但独立的节点（即所谓的“节点分离”），可以为裂纹两侧的单元赋予独立的自由度，从而自然地表达位移的不连续性。然而，对于动态扩展的裂纹问题，这种方法的代价极为高昂。每当裂纹扩展一小步，都必须对裂纹尖端周围的区域进行重新剖分网格，以维持网格共形。这一过程不仅计算成本高昂，还涉及复杂的几何操作、将历史状态变量（如应力、应变、塑性变形等）从旧网格投影到新网格时引入的投影误差，以及裂纹扩展路径可能受到网格结构影响而产生的网格偏向性等一系列难题 [@problem_id:3590683]。扩展有限元法的提出，正是为了摆脱这种对网格共形的依赖。

### 单位分解法：富集的理论框架

扩展有限元法的理论基石是**单位分解法（Partition of Unity Method, PUM）**。这一方法巧妙地利用了标准有限元形函数的一个基本性质——**单位分解性**。对于一个标准的有限元网格，其所有形函数$\{N_i(\boldsymbol{x})\}$在求解域$\Omega$内的任意一点$\boldsymbol{x}$处，其值之和恒为1。即：
$$
\sum_{i \in \mathcal{N}(\boldsymbol{x})} N_i(\boldsymbol{x}) = 1, \quad \forall \boldsymbol{x} \in \Omega
$$
其中，$\mathcal{N}(\boldsymbol{x})$是所有在点$\boldsymbol{x}$处支撑域非零的节点的集合。这个性质保证了标准有限元法能够精确地再现常数场。

PUM的核心思想是，既然标准的多项式基函数不足以描述复杂的解（如包含不连续或奇异性的解），我们可以在此基础上增加“信息”。具体做法是，将描述问题局部特性的**富集函数（enrichment function）** $\psi(\boldsymbol{x})$与单位分解的形函数相乘，从而构造出新的基函数。一个通用的PUM逼近可以写成：
$$
\boldsymbol{u}^h(\boldsymbol{x}) = \underbrace{\sum_{i \in \mathcal{N}} N_i(\boldsymbol{x}) \boldsymbol{u}_i}_{\text{标准有限元部分}} + \underbrace{\sum_{j \in \mathcal{N}_e} N_j(\boldsymbol{x}) \psi(\boldsymbol{x}) \boldsymbol{a}_j}_{\text{富集部分}}
$$
其中，$\boldsymbol{u}_i$是标准的节点自由度，$\mathcal{N}_e$是被选择进行富集的节点集合，$\boldsymbol{a}_j$是与富集函数相关联的额外自由度。

这种构造方式的精妙之处在于，它能在不破坏原有有限元框架连续性的前提下，将任意函数的性质“植入”到逼近空间中。考虑任意两个相邻但不被裂纹切割的单元，它们共享一个公共边界$e$。由于标准形函数$N_i(\boldsymbol{x})$是$C^0$连续的，即它们在$e$上的迹是唯一的。同时，如果我们选择的富集函数$\psi(\boldsymbol{x})$在远离其物理源（如裂纹）的区域是连续的，那么$\psi(\boldsymbol{x})$在边界$e$上也是单值的。因此，富集项$N_i(\boldsymbol{x}) \psi(\boldsymbol{x})$的乘积在$e$上也是连续的。这意味着，整个富集逼近$\boldsymbol{u}^h(\boldsymbol{x})$在所有未被裂纹切割的单元边界上，仍然保持$C^0$连续性。单位分解性确保了这种富集方式的相容性和局部性，使得我们可以在需要的地方（如裂纹周围）增强逼近能力，而在其他地方保持标准有限元的性质 [@problem_id:3590691]。

### 模拟强不连续性：亥维赛富集

为了模拟裂纹所代表的位移**强不连续性**（即跳跃），我们需要的富集函数$\psi(\boldsymbol{x})$本身必须是一个不连续函数。

#### 裂纹的几何表示：水平集方法

在XFEM中，裂纹的几何形状通常独立于网格，通过**水平集方法（Level Set Method）**进行隐式描述。我们定义一个光滑的标量函数$\phi(\boldsymbol{x})$，称为**水平集函数**，它通常是一个**符号距离函数**。该函数的定义如下 [@problem_id:3590682]：
-   裂纹面$\Gamma_c$由零等值线定义：$\Gamma_c = \{\boldsymbol{x} \mid \phi(\boldsymbol{x}) = 0\}$。
-   裂纹的两侧分别对应于$\phi(\boldsymbol{x}) > 0$和$\phi(\boldsymbol{x})  0$的区域。
-   在裂纹$\Gamma_c$的邻域内，$\phi(\boldsymbol{x})$的值等于点$\boldsymbol{x}$到$\Gamma_c$的最短欧氏距离，其符号由点位于裂纹的哪一侧决定。
-   水平集函数的梯度$\nabla\phi(\boldsymbol{x})$的方向垂直于等值线。因此，在裂纹面上，单位法向量$\boldsymbol{n}$可以由归一化的梯度得到：$\boldsymbol{n}(\boldsymbol{x}) = \nabla\phi(\boldsymbol{x}) / \|\nabla\phi(\boldsymbol{x})\|$。

这种表示方法非常灵活，可以方便地描述任意复杂的裂纹几何，并且在裂纹扩展时，只需更新$\phi$函数的值，而无需改变网格。

#### 亥维赛富集函数

有了裂纹的水平集表示，一个自然的选择是使用**亥维赛函数（Heaviside function）** $H(\cdot)$作为富集函数，来引入跳跃。亥维赛函数根据其参数的符号取不同的常数值。一个常用的定义是广义的符号函数 [@problem_id:3590682]：
$$
H(\phi(\boldsymbol{x})) = \text{sgn}(\phi(\boldsymbol{x})) = \begin{cases} +1  \text{if } \phi(\boldsymbol{x}) \ge 0 \\ -1  \text{if } \phi(\boldsymbol{x})  0 \end{cases}
$$
这个函数在$\phi(\boldsymbol{x}) = 0$（即裂纹面）上发生从-1到+1的跳跃，其跳跃值为2。

将亥维赛函数作为富集函数，XFEM位移逼近的强不连续部分可以写为 [@problem_id:3590761]：
$$
\boldsymbol{u}^h(\boldsymbol{x}) = \sum_{i \in \mathcal{N}} N_i(\boldsymbol{x}) \boldsymbol{u}_i + \sum_{j \in \mathcal{N}_H} N_j(\boldsymbol{x}) H(\phi(\boldsymbol{x})) \boldsymbol{a}_j
$$
其中，$\mathcal{N}_H$是其支撑域被裂纹切割的节点集合。对于任意点$\boldsymbol{x} \in \Gamma_c$，位移的跳跃值为：
$$
\llbracket \boldsymbol{u}^h(\boldsymbol{x}) \rrbracket = \boldsymbol{u}^h(\boldsymbol{x}^+) - \boldsymbol{u}^h(\boldsymbol{x}^-) = \sum_{j \in \mathcal{N}_H} N_j(\boldsymbol{x}) \boldsymbol{a}_j \big( H(\phi(\boldsymbol{x}^+)) - H(\phi(\boldsymbol{x}^-)) \big) = 2 \sum_{j \in \mathcal{N}_H} N_j(\boldsymbol{x}) \boldsymbol{a}_j
$$
这表明，通过求解额外的自由度$\boldsymbol{a}_j$，我们可以在裂纹上表示一个任意的、由形函数$N_j$插值出的位移跳跃场。这种构造方式使得位移逼近函数$\boldsymbol{u}^h$恰好属于所需的$H^1(\Omega \setminus \Gamma_c)$空间。

### 模拟裂尖奇异性：分支函数富集

裂纹尖端是另一个挑战。根据**线性弹性断裂力学（LEFM）**的理论，即使在远场施加有限的载荷，裂纹尖端附近的应力场也会呈现**奇异性**。通过求解弹性力学方程的特征值问题（即Williams渐近展开），可以证明，在二维问题中，裂纹尖端应力场和应变场具有$r^{-1/2}$的奇异性，而位移场则表现为$r^{1/2}$的行为，其中$r$是到裂尖的距离 [@problem_id:3590723]。
$$
\boldsymbol{\sigma} \sim \mathcal{O}(r^{-1/2}), \quad \boldsymbol{\varepsilon} \sim \mathcal{O}(r^{-1/2}), \quad \boldsymbol{u} \sim \mathcal{O}(r^{1/2})
$$
标准的多项式形函数无法有效地逼近这种根号形式的函数，会导致在裂尖附近计算应力强度因子（Stress Intensity Factor, SIF）时精度低下，并且收敛缓慢。

为了解决这个问题，XFEM引入了第二类富集——**分支函数（branch function）**富集。这些分支函数直接来自于LEFM的渐近解，能够精确地描述裂尖场的奇异性和角度依赖性。对于二维各向同性材料，一组完备的、用于富集裂尖周围节点的线性无关分支函数集为 [@problem_id:3590732]：
$$
\{F_\alpha(r, \theta)\} = \left\{ \sqrt{r}\sin(\tfrac{\theta}{2}),\ \sqrt{r}\cos(\tfrac{\theta}{2}),\ \sqrt{r}\sin(\tfrac{\theta}{2})\sin\theta,\ \sqrt{r}\cos(\tfrac{\theta}{2})\sin\theta \right\}
$$
其中$(r, \theta)$是以裂尖为原点的局部极坐标系。

包含两种富集的完整XFEM位移逼近形式为：
$$
\boldsymbol{u}^h(\boldsymbol{x}) = \sum_{i \in \mathcal{N}} N_i \boldsymbol{u}_i + \sum_{j \in \mathcal{N}_H} N_j H(\phi) \boldsymbol{a}_j + \sum_{k \in \mathcal{N}_T} N_k \sum_{\alpha=1}^{4} F_\alpha(r, \theta) \boldsymbol{b}_k^{(\alpha)}
$$
其中，$\mathcal{N}_T$是支撑域包含裂尖的节点集合，$\boldsymbol{b}_k^{(\alpha)}$是与分支函数相关的富集自由度。

为了在实际计算中使用分支函数，需要将全局坐标$\boldsymbol{x}$映射到裂尖的局部极坐标$(r, \theta)$。这可以通过**双水平集方法（dual level-set method）**实现 [@problem_id:3590759]。除了之前描述的法向水平集函数$\phi(\boldsymbol{x})$，我们还引入一个切向水平集函数$\psi(\boldsymbol{x})$。$\psi(\boldsymbol{x})$的值等于点$\boldsymbol{x}$在裂纹路径上的投影点到裂尖的弧长距离。这样，裂尖被唯一确定为$\phi(\boldsymbol{x})=0$和$\psi(\boldsymbol{x})=0$的点，而已存在的裂纹体则对应$\phi(\boldsymbol{x})=0, \psi(\boldsymbol{x}) \le 0$。在裂尖附近，$(\psi, \phi)$近似构成一个局部笛卡尔坐标系，从中可以方便地计算出所需的极坐标：
$$
r = \sqrt{\phi^2 + \psi^2}, \quad \theta = \operatorname{atan2}(\phi, \psi)
$$
这种双水平集表示法为精确捕捉裂尖奇异性提供了强大的几何工具。

### 实际应用中的关键机制与高级专题

仅仅定义富集函数并不足以构建一个稳健、精确的XFEM程序。本节将讨论几个在实际应用中至关重要的高级机制。

#### 切割单元的数值积分

当一个单元被裂纹切割时，其内部的被积函数（在组装刚度矩阵时出现）由于亥维赛函数或分支函数的存在而变得不连续或非多项式。标准的**高斯积分（Gaussian quadrature）**在这种情况下会失效，导致严重的积分误差，从而破坏整个方法的精度。为了解决这个问题，主要有两种策略 [@problem_id:3590720]：

1.  **共形子单元积分（Conformal Subcell Integration）**：该方法将每个被切割的单元沿裂纹几何边界精确地划分为多个子多边形（如三角形）。在每个子多边形内部，被积函数是光滑的，因此可以安全地使用标准高斯积分。最后将所有子单元的积分结果相加。这种方法的优点是概念直观，但缺点是实现起来非常复杂，需要稳健的几何求交、多边形裁剪和子三角剖分算法，尤其是在三维情况下。此外，如果裂纹是曲线，用直线段近似裂纹会引入几何误差。

2.  **矩匹配积分（Moment-Fitted Quadrature）**：该方法不改变积分区域，而是为每个切割单元构造一个特殊的积分法则（即积分点和权重）。该法则是通过求解一组“矩方程”得到的，旨在精确地积含有亥维赛富集函数的多项式。这种方法避免了复杂的几何剖分，并且对于曲线裂纹没有几何误差，因此能更好地保证XFEM的最优收敛率。虽然其背后的数学理论和矩的计算可能较为复杂，但通常认为它比实现一套通用的三维几何剖分算法要简单。

#### 系统条件数与基函数移位

XFEM的一个潜在问题是，富集后的线性方程组可能变得**病态（ill-conditioned）**，即系统矩阵的条件数过大。这主要是由于标准基函数$N_i$与其对应的富集基函数$N_i \psi$之间存在**近似线性相关**。例如，对于一个光滑的富集函数$\psi(\boldsymbol{x})$，在其节点$\boldsymbol{x}_i$附近，$\psi(\boldsymbol{x})$近似于一个常数$\psi(\boldsymbol{x}_i)$。此时，富集基函数$N_i \psi(\boldsymbol{x}) \approx \psi(\boldsymbol{x}_i) N_i(\boldsymbol{x})$，它几乎是标准基函数$N_i(\boldsymbol{x})$的一个倍数，从而导致线性相关。

为了改善系统条件数，一种非常有效的技术是**移位富集（shifted enrichment）** [@problem_id:3590697] [@problem_id:3590761]。其思想是将富集函数$\psi(\boldsymbol{x})$替换为$\psi(\boldsymbol{x}) - \psi(\boldsymbol{x}_i)$。修改后的富集逼近形式为：
$$
\boldsymbol{u}_h^{\text{shift}}(\boldsymbol{x}) = \sum_{i \in \mathcal{N}} N_i \boldsymbol{u}_i + \sum_{j \in \mathcal{N}_e} N_j \big(\psi(\boldsymbol{x}) - \psi(\boldsymbol{x}_j)\big) \boldsymbol{a}_j
$$
这种移位操作具有两个显著优点：
-   **恢复克罗内克（Kronecker-delta）性质**：在节点$\boldsymbol{x}_k$处，由于$N_j(\boldsymbol{x}_k)=\delta_{jk}$，移位富集项的贡献为$N_k(\psi(\boldsymbol{x}_k)-\psi(\boldsymbol{x}_k))\boldsymbol{a}_k = \boldsymbol{0}$。这意味着$\boldsymbol{u}_h^{\text{shift}}(\boldsymbol{x}_k) = \boldsymbol{u}_k$，使得标准自由度$\boldsymbol{u}_k$重新获得了其作为节点位移的明确物理意义 [@problem_id:3590697]。
-   **改善条件数**：移位操作从富集基函数中减去了导致线性相关的常数部分。这使得标准基函数与富集基函数更加“正交”，从而显著降低了系统矩阵的条件数，提高了数值求解的稳定性和精度 [@problem_id:3590697]。对于亥维赛富集，这种移位同样有效，它保留了正确的跳跃值，同时使富集基函数在节点处为零，有助于提高方法的稳健性。

#### 一致性与混合单元

当富集区域与标准有限元区域交接时，会产生一类特殊的单元，称为**混合单元（blending elements）**。这些单元同时包含富集节点和未富集节点。在这些单元中，XFEM会暴露出一个微妙的缺陷：丧失**一致性（consistency）**。这意味着，即使将一个已知的精确线性解（例如，均匀拉伸场）代入离散方程，方程也无法精确满足，即**单元检验（patch test）**失败 [@problem_id:3590758]。

这种不一致性的根源在于，在混合单元的富集侧和非富集侧之间，单位分解的性质被破坏。其直接后果是，方法的收敛率会从最优的$\mathcal{O}(h)$（对于能量范数）下降到次优的$\mathcal{O}(h^{1/2})$，其中$h$是网格尺寸。

为了修复这个问题并恢复最优收敛率，需要对混合单元中的富集函数进行特殊处理。标准做法是引入一个**混合函数（blending function）**，它是一个“斜坡”函数，乘以富集函数。该混合函数在富集节点处为1，并平滑地过渡到与未富集区域相邻的单元边界处为0。这样可以确保富集效应在交界面上平滑消失，从而恢复单位分解的性质和方法的一致性。通过这种修正，XFEM可以顺利通过单元检验，并恢复其理论上的最优收敛性能 [@problem_id:3590758]。