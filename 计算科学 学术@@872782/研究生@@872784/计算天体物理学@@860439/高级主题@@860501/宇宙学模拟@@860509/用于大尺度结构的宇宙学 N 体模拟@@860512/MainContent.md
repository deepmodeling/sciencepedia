## 引言
宇宙是如何从早期近乎均匀的状态演化成我们今天观测到的由星系、[星系团](@entry_id:160919)和巨大空洞构成的宏伟“宇宙网”的？这是[现代宇宙学](@entry_id:752086)的核心问题之一。[宇宙学N体模拟](@entry_id:747920)是回答这一问题的最强大工具。通过在超级计算机中追踪数万亿虚拟粒子的[引力](@entry_id:175476)相互作用，这些模拟能够以前所未有的保真度重现宇宙大尺度结构的形成和演化过程，为我们提供了一个检验宇宙学理论和解释天文观测的“虚拟实验室”。

本文旨在为计算天体物理领域的研究生提供一份关于[宇宙学N体模拟](@entry_id:747920)的全面指南，弥合理论概念与计算实践之间的鸿沟。我们将系统地剖析这些复杂模拟背后的物理原理、关键算法及其在前沿科学研究中的应用。读者将学到如何从第一性原理出发，构建一个能够模拟宇宙演化的计算框架，并理解如何利用模拟结果来探索宇宙的奥秘。

为实现这一目标，文章组织如下：第一章“原理与机制”将深入探讨描述粒子在[膨胀宇宙](@entry_id:161442)中运动的方程、用于生成[初始条件](@entry_id:152863)和高效计算[引力](@entry_id:175476)的核心算法，以及确保模拟精度的数值技术。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示[N体模拟](@entry_id:157492)如何被用来识别[暗物质晕](@entry_id:147523)、构建模拟观测星表以直接与巡天数据对比，以及如何作为平台来检验[修正引力](@entry_id:158859)等基础物理理论。最后，第三章“动手实践”部分提供了一系列精心设计的问题，旨在引导读者亲手实现和分析[N体模拟](@entry_id:157492)的关键组成部分，从而将理论知识转化为实践技能。

## 原理与机制

本章旨在系统阐述宇宙学 N 体模拟的核心物理原理与数值机制。我们将从描述粒子在[膨胀宇宙](@entry_id:161442)中运动的基本方程出发，探讨这些方程如何在离散的[粒子系统](@entry_id:180557)中求解，并介绍用于建立[初始条件](@entry_id:152863)、计算[引力](@entry_id:175476)、以及随时间演化系统的关键算法。最后，我们将讨论如何设计模拟参数以达成特定的科学目标，以及如何检验模拟的[数值精度](@entry_id:173145)。

### [膨胀宇宙](@entry_id:161442)中的[运动方程](@entry_id:170720)

宇宙学 N 体模拟的基石是在一个膨胀的背景时空中描述物质（主要是[冷暗物质](@entry_id:158219)）的动力学演化。描述这一过程最自然的方式是采用与宇宙背景膨胀“一同运动”的[坐标系](@entry_id:156346)，即**[共动坐标](@entry_id:271238)（comoving coordinates）**。

一个粒子在物理空间中的位置 $\mathbf{r}$ 可以通过一个随时间变化的**[尺度因子](@entry_id:266678)（scale factor）** $a(t)$ 和其共动位置 $\mathbf{x}$ 联系起来：

$$
\mathbf{r}(t) = a(t) \mathbf{x}(t)
$$

尺度因子 $a(t)$ 描述了宇宙的整体膨胀，通常我们约定当前宇宙的[尺度因子](@entry_id:266678)为 $a_0 = 1$。粒子的物理速度 $\mathbf{v} = \dot{\mathbf{r}}$ 可以通过对上式求时间导数得到：

$$
\mathbf{v} = \dot{a}\mathbf{x} + a\dot{\mathbf{x}}
$$

引入**哈勃参数（Hubble parameter）** $H(t) = \dot{a}/a$，我们可以将上式重写为：

$$
\mathbf{v} = H a \mathbf{x} + a\dot{\mathbf{x}} = H\mathbf{r} + \mathbf{u}
$$

这里，我们定义了**奇特速度（peculiar velocity）** $\mathbf{u} = a\dot{\mathbf{x}}$。这个关系式 [@problem_id:3507099] 明确地将粒子的总速度分解为两部分：由[宇宙膨胀](@entry_id:161474)引起的**哈勃流（Hubble flow）**速度 $H\mathbf{r}$，以及粒子相对于哈勃流的运动速度 $\mathbf{u}$。在宇宙大尺度结构形成中，我们主要关心的是由[引力不稳定性](@entry_id:160721)驱动的奇特速度。

为了在模拟中演化粒子的状态 $(\mathbf{x}, \mathbf{u})$，我们需要推导它们的运动方程。这始于牛顿第二定律，$\ddot{\mathbf{r}} = -\nabla_r \Phi$，其中 $\Phi$ 是物理引力势。通过对 $\mathbf{v}$ 再次求导，我们得到物理加速度 $\ddot{\mathbf{r}}$：

$$
\ddot{\mathbf{r}} = \frac{d}{dt}(H\mathbf{r} + a\dot{\mathbf{x}}) = \dot{H}\mathbf{r} + H\dot{\mathbf{r}} + \dot{a}\dot{\mathbf{x}} + a\ddot{\mathbf{x}}
$$

将 $\dot{\mathbf{r}} = H\mathbf{r} + a\dot{\mathbf{x}}$ 和 $\dot{a} = Ha$ 代入，经过整理可得：

$$
\ddot{\mathbf{r}} = (\dot{H} + H^2) \mathbf{r} + 2H a\dot{\mathbf{x}} + a\ddot{\mathbf{x}}
$$

在广义相对论框架下，对于一个均匀物质[分布](@entry_id:182848)的宇宙，背景时空的演化由弗里德曼方程描述，其中之一是 $\ddot{a}/a = \dot{H} + H^2 = - \frac{4\pi G}{3}(\bar{\rho} + 3p/c^2)$。这表明，即使在没有[密度扰动](@entry_id:159546)的均匀宇宙中，粒子也会因宇宙的减速或加速而感受到一个“加速度”，$\ddot{\mathbf{r}} = (\ddot{a}/a)\mathbf{r}$。

[引力势](@entry_id:160378) $\Phi$ 可以分解为来自均匀背景的部分和来自[密度扰动](@entry_id:159546) $\delta = (\rho - \bar{\rho})/\bar{\rho}$ 的**奇特引力势（peculiar potential）** $\phi$。总的[引力](@entry_id:175476)加速度可以写成 $\ddot{\mathbf{r}} = (\ddot{a}/a)\mathbf{r} - \frac{1}{a}\nabla_x\phi$，其中 $\nabla_r = (1/a)\nabla_x$。将此式与运动学推导的 $\ddot{\mathbf{r}}$ 相等，背景项相互抵消，我们得到描述奇特运动的方程：

$$
a\ddot{\mathbf{x}} + 2\dot{a}\dot{\mathbf{x}} = -\frac{1}{a}\nabla_x \phi
$$

或者写成关于共动加速度 $\ddot{\mathbf{x}}$ 的形式：

$$
\ddot{\mathbf{x}} + 2H\dot{\mathbf{x}} = -\frac{1}{a^2}\nabla_x \phi
$$

这个方程中的 $2H\dot{\mathbf{x}}$ 项被称为**哈勃阻尼（Hubble drag）**，它反映了在膨胀[坐标系](@entry_id:156346)中粒子运动受到的“摩擦”效应。为了得到关于奇特速度 $\mathbf{u}=a\dot{\mathbf{x}}$ 的[演化方程](@entry_id:268137)，我们对其求导：

$$
\dot{\mathbf{u}} = \dot{a}\dot{\mathbf{x}} + a\ddot{\mathbf{x}} = H(a\dot{\mathbf{x}}) + a\ddot{\mathbf{x}} = H\mathbf{u} + a\ddot{\mathbf{x}}
$$

将 $\ddot{\mathbf{x}}$ 的表达式代入，我们发现：

$$
\dot{\mathbf{u}} + H\mathbf{u} = -\frac{1}{a}\nabla_x \phi
$$

这组方程，$\dot{\mathbf{x}} = \mathbf{u}/a$ 和 $\dot{\mathbf{u}} + H\mathbf{u} = -\frac{1}{a}\nabla_x \phi$，构成了 N 体模拟的核心演化方程 [@problem_id:3507099]。值得注意的是，奇特速度 $\mathbf{u}$ 方程中的阻尼项系数是 $H$，而共动速度 $\dot{\mathbf{x}}$ 方程中的系数是 $2H$。

采用[共动坐标系](@entry_id:266800) $(\mathbf{x}, \mathbf{u})$ 进行模拟具有巨大的数值优势。首先，它将宏大的、均匀的哈勃流从演化变量中分离出去，使得模拟器只需处理幅度小得多的奇特运动，这极大地提高了[数值精度](@entry_id:173145)和稳定性。其次，模拟的计算域（通常是一个周期性盒子）在[共动坐标](@entry_id:271238)下具有固定的尺寸，这极大地简化了边界条件和力计算的实现 [@problem_id:3507099]。

### 宇宙学框架：时间与增长

为了求解上述运动方程，我们必须知道宇宙的膨胀历史，即[尺度因子](@entry_id:266678) $a$ 和哈勃参数 $H$ 如何随[时间演化](@entry_id:153943)。这由**弗里德曼方程（Friedmann equations）** 决定。在一个空间平直、由无压物质（[密度参数](@entry_id:265044) $\Omega_m$）和[宇宙学常数](@entry_id:159297)（[密度参数](@entry_id:265044) $\Omega_\Lambda$）主导的 $\Lambda$CDM 宇宙中，第一个弗里德曼方程可以写为：

$$
H^2(a) = H_0^2 \left( \Omega_{m,0} a^{-3} + \Omega_{\Lambda,0} a^{-2(1+w)} \right)
$$

对于[宇宙学常数](@entry_id:159297)，[状态方程](@entry_id:274378)参数 $w=-1$，因此其能量密度不随[宇宙膨胀](@entry_id:161474)而改变。对于无压物质（“尘埃”），其密度随[体积膨胀](@entry_id:144241)而稀释，$\rho_m \propto a^{-3}$。因此，对于一个空间平直 ($\Omega_{m,0} + \Omega_{\Lambda,0} = 1$) 的宇宙，哈勃参数随[尺度因子](@entry_id:266678)的演化关系为 [@problem_id:3507104]：

$$
H(a) = H_0 \sqrt{\Omega_{m,0} a^{-3} + \Omega_{\Lambda,0}}
$$

其中 $H_0$、$\Omega_{m,0}$ 和 $\Omega_{\Lambda,0}$ 分别是今天的哈勃常数、物质密度参数和暗能量[密度参数](@entry_id:265044)。

从 $H = \dot{a}/a = (1/a) da/dt$ 的定义，我们可以建立宇宙时 $t$ 和[尺度因子](@entry_id:266678) $a$ 之间的关系：$dt = da / (aH(a))$。通过积分，我们可以得到从大爆炸 ($a=0$) 到任意时刻 $a$ 的[宇宙年龄](@entry_id:159794)：

$$
t(a) = \int_0^a \frac{da'}{a' H(a')}
$$

将 $H(a')$ 的表达式代入并进行积分，可以得到一个解析解 [@problem_id:3507104]：

$$
t(a) = \frac{2}{3 H_0 \sqrt{\Omega_{\Lambda,0}}} \arcsinh\left(\sqrt{\frac{\Omega_{\Lambda,0}}{\Omega_{m,0}}} a^{3/2}\right)
$$

这个关系式是模拟的“时钟”，它将积分步长中自然出现的尺度因子 $a$ 与物理时间 $t$ 联系起来。

### N体离散化及其有效性

N 体模拟用有限数量的离散粒子来近似一个连续的、无碰撞的暗物质流体。这个近似的有效性是[计算宇宙学](@entry_id:747605)的核心问题。在理论上，[无碰撞系统](@entry_id:158088)的演化由[相空间分布](@entry_id:151304)函数 $f(\mathbf{x}, \mathbf{u}, a)$ 遵循的**[弗拉索夫-泊松方程组](@entry_id:756544)（Vlasov-Poisson system）** 描述。N 体模拟本质上是对这个[分布函数](@entry_id:145626)的一次**[蒙特卡洛采样](@entry_id:752171)** [@problem_id:3507109]。

一个模拟的有效性，即其结果在粒子数 $N \to \infty$ 时是否收敛于[弗拉索夫-泊松方程](@entry_id:756543)的解，取决于几个关键条件：

1.  **[质量分辨率](@entry_id:197946)**：为了模拟一个总质量固定的宇宙区域，当粒子数 $N$ 趋于无穷时，单个粒子的质量 $m_p$ 必须趋于零。保持[粒子质量](@entry_id:156313)不变而增加粒子数，会错误地改变所模拟宇宙的平均密度 [@problem_id:3507109]。

2.  **抑制离散效应**：在真实的 N 体系统中，两个粒子间的近距离相互作用（[二体散射](@entry_id:144358)）会导致其[轨道](@entry_id:137151)发生偏转。然而，[冷暗物质](@entry_id:158219)被认为是**无碰撞的（collisionless）**，这种散射是数值模拟带来的非物理效应。为了抑制这种效应，必须引入**[引力软化](@entry_id:146273)（gravitational softening）**。即在距离小于[软化长度](@entry_id:755011) $\epsilon$ 时，将[牛顿引力](@entry_id:159796) $1/r^2$ 修改为一个更平缓的形式（例如，Plummer 软化势 $\Phi \propto 1/\sqrt{r^2+\epsilon^2}$）。

    严格的[数学证明](@entry_id:137161)要求，[软化长度](@entry_id:755011) $\epsilon_N$ 随粒子数 $N$ 的变化需满足 $\epsilon_N \to 0$ 但 $N\epsilon_N^3 \to \infty$。这保证了在任何一个粒子的软化半径内总有足够多的其他粒子，使得[引力场](@entry_id:169425)更接近于平滑的平均场。在实践中，通常选择[软化长度](@entry_id:755011)与平均粒子间距 $\ell_N$ 成正比，即 $\epsilon_N \sim \ell_N / N_{ngb}^{1/3}$，其中 $N_{ngb}$ 是一个几十的数值，这在实践中被证明是有效的 [@problem_id:3507109]。采取让 $\epsilon_N$ 比粒子间距更快地趋于零的策略反而会增强非物理的[二体散射](@entry_id:144358)，使模拟结果偏离无碰撞的极限 [@problem_id:3507109]。

3.  **初始采样噪声**：如果初始粒子位置是随机[分布](@entry_id:182848)的，会引入与粒子数相关的**散粒噪声（shot noise）**。为了减少这种非物理的初始噪声，高精度模拟通常采用“宁静启动（quiet start）”方法，即将粒子放置在规则的格点上，然后根据初始密度场施加微小的位移 [@problem_id:3507109]。

### 设置舞台：初始条件

模拟的起始状态——即初始粒子位置和速度——必须精确地反映由宇宙微波背景辐射观测所确定的早期宇宙的密度涨落。这通常通过**[拉格朗日微扰理论](@entry_id:751116)（Lagrangian Perturbation Theory）**，特别是其一阶近似，即**[泽尔多维奇近似](@entry_id:139227)（Zel'dovich Approximation）** 来实现 [@problem_id:3507148]。

[泽尔多维奇近似](@entry_id:139227)将粒子的初始（拉格朗日）共动位置 $\mathbf{q}$ 映射到稍后时刻（欧拉）的位置 $\mathbf{x}$：

$$
\mathbf{x}(\mathbf{q}, a) = \mathbf{q} + \mathbf{s}(\mathbf{q}, a)
$$

其中 $\mathbf{s}$ 是**[位移场](@entry_id:141476)（displacement field）**。在线性理论中，[质量守恒](@entry_id:204015)要求密度涨落 $\delta$ 与位移场的散度相关：$\delta = -\nabla \cdot \mathbf{s}$。在傅里叶空间中，这变成了代数关系 $\tilde{\delta} = -i\mathbf{k} \cdot \tilde{\mathbf{s}}$。由于[引力不稳定性](@entry_id:160721)导致的位移是无旋的，[位移矢量](@entry_id:262782) $\tilde{\mathbf{s}}(\mathbf{k})$ 必须平行于[波矢](@entry_id:178620) $\mathbf{k}$。综合这两个条件，我们可以唯一地确定[位移场](@entry_id:141476)与密度场的关系 [@problem_id:3507148]：

$$
\tilde{\mathbf{s}}(\mathbf{k}) = i \frac{\mathbf{k}}{k^2} \tilde{\delta}(\mathbf{k})
$$

[密度涨落](@entry_id:143540)的增长由**[线性增长因子](@entry_id:751309)（linear growth factor）** $D(a)$ 描述，它只依赖于[宇宙学参数](@entry_id:161338)和[尺度因子](@entry_id:266678)。因此，[位移场](@entry_id:141476)可以写成一个时间无关的空间部分 $\boldsymbol{\psi}(\mathbf{q})$ 和[时间演化](@entry_id:153943)部分 $D(a)$ 的乘积：

$$
\mathbf{s}(\mathbf{q}, a) = D(a) \boldsymbol{\psi}(\mathbf{q})
$$

粒子的奇特速度是位移的时间导数乘以尺度因子，$\mathbf{v} = a \dot{\mathbf{s}}$。利用增长因子，这可以表示为：

$$
\mathbf{v}(\mathbf{q}, a) = a \dot{D}(a) \boldsymbol{\psi}(\mathbf{q}) = a H(a) f(a) D(a) \boldsymbol{\psi}(\mathbf{q})
$$

其中 $f(a) = d\ln D / d\ln a$ 是**[线性增长](@entry_id:157553)率（linear growth rate）**。因此，生成初始条件的算法流程如下：首先在傅里叶空间中生成一个符合理论幂谱的随机[高斯密度](@entry_id:199706)场 $\tilde{\delta}(\mathbf{k})$，然后利用上述关系计算出[位移场](@entry_id:141476) $\boldsymbol{\psi}(\mathbf{q})$，最后结合在初始红移 $z_{\text{init}}$ 处的增长因子 $D(a_{\text{init}})$ 和增长率 $f(a_{\text{init}})$，计算出每个粒子的初始位置和速度 [@problem_id:3507148]。

### 计算[引力](@entry_id:175476)

在 N 体模拟中，计算所有粒子间的[引力](@entry_id:175476)是计算量最大的部分。为此发展了多种算法，以平衡计算速度和精度。

#### 粒子-网格（Particle-Mesh, PM）方法

PM 方法是一种高效计算长程[引力](@entry_id:175476)的方法 [@problem_id:3507182]。其核心思想是在一个规则的网格上求解泊松方程。步骤如下：

1.  **[质量分配](@entry_id:751704)（Mass Assignment）**：将每个粒子的[质量分配](@entry_id:751704)到其周围的网格点上，形成一个离散的密度场 $\rho_{\mathbf{j}}$。常用的方法包括最近邻网格点法（NGP）和云-in-元胞法（CIC）。
2.  **求解[泊松方程](@entry_id:143763)**：奇特[引力势](@entry_id:160378) $\phi$ 满足的[泊松方程](@entry_id:143763)为 $\nabla^2 \phi = 4\pi G a^2 (\rho - \bar{\rho})$。在周期性边界条件的立方体中，我们可以利用**[快速傅里叶变换](@entry_id:143432)（FFT）** 来求解。在傅里叶空间，拉普拉斯算子 $\nabla^2$ 变为乘以 $-k^2$，因此泊松方程变成一个简单的[代数方程](@entry_id:272665)：
    $$
    -k^2 \phi(\mathbf{k}) = 4\pi G a^2 \delta(\mathbf{k}) \implies \phi(\mathbf{k}) = -\frac{4\pi G a^2}{k^2} \delta(\mathbf{k})
    $$
    在离散网格上，[拉普拉斯算子](@entry_id:146319)的[傅里叶表示](@entry_id:749544)不再是精确的 $-k^2$，而是一个**有效[波矢](@entry_id:178620)（effective wavenumber）** $k_{\text{eff}}^2(\mathbf{k})$，其具体形式取决于所用的[有限差分格式](@entry_id:749361)。对于[二阶中心差分](@entry_id:170774)，我们有 [@problem_id:3507182] [@problem_id:3507183]：
    $$
    k_{\text{eff}}^2(\mathbf{k}) = \sum_{i \in \{x,y,z\}} \left( \frac{2}{\Delta x} \sin\left(\frac{k_i \Delta x}{2}\right) \right)^2
    $$
    其中 $\Delta x$ 是网格间距。只有在长波极限下（$k \Delta x \ll 1$），$k_{\text{eff}}^2$ 才趋近于 $k^2$。
    对于 $\mathbf{k}=\mathbf{0}$ 模式（直流分量），由于周期性盒子里的总[质量守恒](@entry_id:204015)，[密度涨落](@entry_id:143540)的平均值 $\delta(\mathbf{k}=\mathbf{0})$ 恒为零。此时泊松方程变为 $0 \cdot \phi(\mathbf{0}) = 0$，$\phi(\mathbf{0})$ 不确定。这对应于引力势可以任意添加一个常数而不影响[引力](@entry_id:175476)。通常我们约定 $\phi(\mathbf{0})=0$ [@problem_id:3507182]。
3.  **计算[引力](@entry_id:175476)与力插值**：在傅里叶空间计算出势 $\phi(\mathbf{k})$ 后，通过逆 FFT 变换回[实空间](@entry_id:754128)得到网格上的势 $\phi_{\mathbf{j}}$。然后通过[有限差分](@entry_id:167874)[计算网格](@entry_id:168560)上的[引力场](@entry_id:169425)，最后将[引力](@entry_id:175476)从网格点**插值（Interpolation）** 回每个粒子的位置。

为了提高精度，还可以在傅里叶空间对[质量分配方案](@entry_id:751705)引入的平滑效应进行**[反卷积](@entry_id:141233)（deconvolution）** [@problem_id:3507182]。

#### TreePM [混合方法](@entry_id:163463)

PM 方法在[长程力](@entry_id:181779)计算上高效，但在[短程力](@entry_id:142823)上精度不足（受网格尺寸限制）。为了克服这一缺点，现代高精度模拟广泛采用 TreePM [混合方法](@entry_id:163463) [@problem_id:3507172]。这种方法将[引力](@entry_id:175476)分解为两部分：

$$
\mathbf{F} = \mathbf{F}_{\text{long-range}} + \mathbf{F}_{\text{short-range}}
$$

- **长程力（Long-range force）**：变化平滑，适合用 PM 方法在网格上高效计算。
- **[短程力](@entry_id:142823)（Short-range force）**：在小尺度上剧烈变化，但在大尺度上迅速衰减为零，适合用**树形码（Tree code）** 或直接求和的方式精确计算。

这种分解通常通过在傅里叶空间将[引力势](@entry_id:160378)的格林函数（$ -4\pi G/k^2$）乘以一个滤波器来实现。例如，使用一个高斯滤波器 [@problem_id:3507172]：

- 长程部分：$\tilde{G}_{\text{LR}}(k) = -\frac{4\pi G}{k^2} \exp(-k^2 r_s^2)$
- 短程部分：$\tilde{G}_{\text{SR}}(k) = -\frac{4\pi G}{k^2} \left(1 - \exp(-k^2 r_s^2)\right)$

其中 $r_s$ 是分解尺度。长程部分通过 PM 方法计算，而短程部分的力需要通过[傅里叶逆变换](@entry_id:178300)得到其实[空间形式](@entry_id:186145)，然后用树形码计算。对于高斯分解，[短程力](@entry_id:142823)具有一个包含[互补误差函数](@entry_id:190973) $\operatorname{erfc}$ 和一个指数衰减项的复杂形式。为了保证整个计算的自洽性，必须仔细处理 PM 部分的 CIC [反卷积](@entry_id:141233)和在两个分量上一致地施加[引力软化](@entry_id:146273) [@problem_id:3507172]。

### 时间积分

得到粒子在任意时刻的加速度后，我们需要一个[数值积分](@entry_id:136578)方案来更新它们的位置和速度。由于模拟需要跨越数十亿年，保持长期[数值稳定性](@entry_id:146550)和[能量守恒](@entry_id:140514)至关重要。

标准的积分方案是**蛙跳积分（Leapfrog integrator）**，也称 KDK（Kick-Drift-Kick）格式。它是一种**辛积分器（symplectic integrator）**，能很好地保持系统的相空间结构和长期[能量守恒](@entry_id:140514)。一个典型的蛙跳步包含：

1.  **Kick (半步)**：用当前加速度更新速度半个时间步：$\mathbf{v}_{i+1/2} = \mathbf{v}_i + \mathbf{a}_i \frac{\Delta t}{2}$。
2.  **Drift (整步)**：用新的速度更新位置一个完整时间步：$\mathbf{x}_{i+1} = \mathbf{x}_i + \mathbf{v}_{i+1/2} \Delta t$。
3.  **Kick (半步)**：计算新位置上的加速度 $\mathbf{a}_{i+1}$，并完成速度更新：$\mathbf{v}_{i+1} = \mathbf{v}_{i+1/2} + \mathbf{a}_{i+1} \frac{\Delta t}{2}$。

[宇宙学模拟](@entry_id:747928)中，密度范围跨越多个[数量级](@entry_id:264888)。在致密的星系[晕核](@entry_id:160438)中，粒子的[轨道周期](@entry_id:182572)很短，需要极小的时间步长才能精确积分；而在稀疏的宇宙空洞中，动力学时标很长，可以使用大得多的时间步长。因此，采用**[自适应时间步长](@entry_id:261403)（adaptive time-stepping）**至关重要。

一个普遍的[自适应时间步长](@entry_id:261403)判据基于**局域动力学时标（local dynamical time）** $t_{\text{dyn}}$ [@problem_id:3507183]。对于一个局域密度为 $\rho$ 的区域，其特征[轨道](@entry_id:137151)频率近似为 $\omega \sim \sqrt{G\rho}$。动力学时标即为 $t_{\text{dyn}} \sim 1/\omega \propto (G\rho)^{-1/2}$。为了保证[数值积分](@entry_id:136578)的稳定性，时间步长 $\Delta t$ 必须是动力学时标的一个小部分：

$$
\Delta t = \eta \cdot t_{\text{dyn}} = \frac{\eta}{\sqrt{4\pi G \rho}}
$$

其中 $\eta$ 是一个无量纲的控制参数，通常取值为 $0.01 - 0.05$。例如，在一个典型的星系晕中心，其过密度 $\Delta = \rho / \rho_{\text{crit}} \approx 200$，对于 $H_0 = 67.4 \ \text{km/s/Mpc}$ 和 $\eta=0.02$ 的参数，所需的时间步长约为 16.8 兆年（Myr）[@problem_id:3507183]。

### 模拟设计与诊断

设计一个 N 体模拟需要在多个参数之间进行权衡，以匹配科学目标。

#### 分辨率与模拟盒尺寸

- **[质量分辨率](@entry_id:197946)（Mass Resolution）**：模拟能分辨的最小天体质量由[粒子质量](@entry_id:156313) $m_p$ 决定。一个质量为 $M$ 的暗晕至少需要由上百个粒子构成才能被认为是可靠解析的。粒子质量由模拟盒尺寸 $L$、粒子总数 $N$ 和[宇宙学参数](@entry_id:161338)共同决定：$m_p = \bar{\rho}_{m,0} L^3 / N$。因此，要解析一个质量为 $M$ 的暗晕，需要的最小粒子数 $N_{\text{min}}$ 为 [@problem_id:3507116]：
  $$
  N_{\text{min}} = \frac{100 \cdot \bar{\rho}_{m,0} L^3}{M} = \frac{75 \Omega_{m,0} H_0^2 L^3}{2\pi G M}
  $$

- **空间分辨率（Spatial Resolution）**：模拟的力分辨率由[引力软化](@entry_id:146273)长度 $\epsilon$ 决定。通常 $\epsilon$ 被选为平均粒子间距的一个小分数。

- **大尺度覆盖范围（Large-Scale Coverage）**：模拟盒的尺寸 $L$ 决定了能探测的最大尺度模式。傅里叶空间中的最[小波](@entry_id:636492)矢（**[基频](@entry_id:268182)**）为 $k_f = 2\pi/L$。为了精确测量大尺度上的统计量，如[功率谱](@entry_id:159996)中的**[重子声学振荡](@entry_id:158848)（Baryon Acoustic Oscillations, BAO）**，模拟盒必须足够大，以包含多个 BAO 波长。BAO 在[功率谱](@entry_id:159996)上表现为间隔约 $\Delta k_{\text{BAO}} \approx \pi / r_s \approx 0.021 \, h\,\text{Mpc}^{-1}$ 的[振荡](@entry_id:267781)。为了分辨这些[振荡](@entry_id:267781)，必须要求 $k_f \ll \Delta k_{\text{BAO}}$，这意味着需要一个非常大的模拟盒（$L \gg 300 \, h^{-1}\,\text{Mpc}$）[@problem_id:3507122]。

- **傅里叶空间分辨率**：在使用网格进行分析时（如计算[功率谱](@entry_id:159996)），网格尺寸 $N_g$ 决定了能分辨的最小尺度。根据[奈奎斯特采样定理](@entry_id:268107)，最大可信[波矢](@entry_id:178620)（**[奈奎斯特频率](@entry_id:276417)**）为 $k_N = \pi N_g / L$。要测量[功率谱](@entry_id:159996)直至 $k_{\text{max}}$，必须满足 $k_N > k_{\text{max}}$ [@problem_id:3507122]。

#### 模拟精度检验：Layzer-Irvine 方程

检验模拟代码的正确性和[数值积分](@entry_id:136578)的精度的一个强有力工具是检查某个[守恒量](@entry_id:150267)的守恒情况。在静态宇宙中，总能量 $E = K+W$（动能加势能）是守恒的。然而，在膨胀宇宙中，由于哈勃阻尼的存在，这个量不再守恒。

通过对系统的总动能 $K$ 和总势能 $W$ 求导，可以推导出**Layzer-Irvine 方程** [@problem_id:3507175]：

$$
\frac{d(K+W)}{dt} + H(2K+W) = 0
$$

这个方程描述了在[宇宙膨胀](@entry_id:161474)背景下，系统能量的演化规律。通过变量代换 $d/dt = aH \cdot d/da$，可以进一步证明存在一个守恒量 $C(a)$：

$$
C(a) = a(K(a) + W(a)) + \int_{a_0}^a K(a') da' = \text{const.}
$$

这个量在理想的[无碰撞系统](@entry_id:158088)中是严格守恒的。在 N 体模拟中，我们可以通过计算每个输出快照的 $K$ 和 $W$，并用数值方法（如梯形法则）估计积分项，来检验 $C(a)$ 是否在整个模拟过程中保持不变。$C(a)$ 的偏离程度直接反映了时间积分方案和力计算的累积误差，是衡量模拟精度的重要指标 [@problem_id:3507175]。