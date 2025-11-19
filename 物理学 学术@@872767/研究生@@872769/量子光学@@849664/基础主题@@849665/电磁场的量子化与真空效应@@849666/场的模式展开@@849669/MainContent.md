## 引言
场的模式展开（Mode Expansion）是量子光学乃至整个[量子场论](@entry_id:138177)的基石之一。它是一套强有力的理论工具，成功地将经典电磁学中连续的场，与量子力学中分立的[光子](@entry_id:145192)概念联系起来，为我们理解和操控光的量子行为提供了数学框架。面对一个连续的、在时空中处处定义的[电磁场](@entry_id:265881)，如何将其量子化并揭示其粒子性的难题，正是模式展开方法所要解决的核心问题。

本文将系统地引导读者深入理解场的模式展开。在“原理与机制”一章中，我们将从[正则量子化](@entry_id:148501)出发，详细阐述如何将场分解为一系列独立的谐振子模式，并由此推导出[零点能](@entry_id:142176)、[场算符](@entry_id:140269)关系等基本概念。随后，在“应用与跨学科联系”一章中，我们将展示这一框架的巨大威力，探索其在量子工程、凝聚态物理、先进材料乃至广义相对论和宇宙学等前沿领域的广泛应用，揭示其作为统一物理语言的深刻内涵。最后，“动手实践”部分将通过具体计算问题，帮助读者将抽象理论应用于实际分析，巩固对[光子](@entry_id:145192)、模式和场之间关系的理解。

## 原理与机制

继前一章对电磁[场量子化](@entry_id:160906)的基本概念进行介绍之后，本章将深入探讨其核心技术——模式展开（Mode Expansion）。场的模式展开是量子光学中一个极其强大的工具，它将一个看似复杂的[连续场论](@entry_id:154108)问题，转化为一组无限但离散（或连续）且[相互独立](@entry_id:273670)的[量子谐振子](@entry_id:140678)问题。这种类比不仅极大地简化了数学处理，更深刻地揭示了[光量子](@entry_id:173025)的概念——[光子](@entry_id:145192)——正是这些[谐振子](@entry_id:155622)模式的能量量子。本章将系统地阐述模式展开的原理，展示如何通过它来确定[场算符](@entry_id:140269)的形式，并探讨其在自由空间、[电介质](@entry_id:147163)、以及各种边界条件下的具体应用。

### 场的[正则量子化](@entry_id:148501)

量子化[电磁场](@entry_id:265881)的标准方法始于其经典哈密顿形式。在没有[电荷](@entry_id:275494)和[电流源](@entry_id:275668)的自由空间中，[电磁场](@entry_id:265881)的总能量（[哈密顿量](@entry_id:172864)）是[电场能量](@entry_id:193072)和[磁场能量](@entry_id:267501)在整个空间中的积分。为了建立一个具有[正则坐标](@entry_id:175654)和[正则动量](@entry_id:155151)的哈密顿体系，我们通常采用[库仑规范](@entry_id:273044)（$\nabla \cdot \mathbf{A} = 0$），在该规范下，标量势为零，矢量势 $\mathbf{A}(\mathbf{r}, t)$ 完全描述了横向[电磁场](@entry_id:265881)。

在这种情况下，矢量势 $\mathbf{A}(\mathbf{r})$ 可以被视为[广义坐标](@entry_id:156576)，而其[共轭动量](@entry_id:172203)场 $\mathbf{\Pi}(\mathbf{r})$ 被定义为 $\mathbf{\Pi}(\mathbf{r}) = -\epsilon_0 \mathbf{E}_{\perp}(\mathbf{r})$，其中 $\mathbf{E}_{\perp}$ 是横向[电场](@entry_id:194326)。于是，场的[哈密顿量](@entry_id:172864)可以写作：
$$
\hat{H} = \int d^3\mathbf{r} \left( \frac{1}{2\epsilon_0} |\hat{\mathbf{\Pi}}(\mathbf{r})|^2 + \frac{1}{2\mu_0} |\nabla \times \hat{\mathbf{A}}(\mathbf{r})|^2 \right)
$$
量子化的关键步骤是将这些场量提升为算符，并对它们施加[正则对易关系](@entry_id:185041)。对于任意两个空间点 $\mathbf{r}$ 和 $\mathbf{r}'$ 的场分量，其等时[对易关系](@entry_id:136780)为：
$$
[\hat{A}_i(\mathbf{r}), \hat{\Pi}_j(\mathbf{r}')] = i\hbar \delta_{ij}^{\perp}(\mathbf{r} - \mathbf{r}')
$$
其中 $i, j$ 代表笛卡尔坐标分量（$x, y, z$），$\delta_{ij}^{\perp}(\mathbf{r} - \mathbf{r}')$ 是横向德尔塔函数，它保证了[场算符](@entry_id:140269)的横[向性](@entry_id:144651)。同一类型的[场算符](@entry_id:140269)在不同空间点的对易子为零：$[\hat{A}_i(\mathbf{r}), \hat{A}_j(\mathbf{r}')]=0$ 以及 $[\hat{\Pi}_i(\mathbf{r}), \hat{\Pi}_j(\mathbf{r}')]=0$。

这些基本的对易关系是整个理论的基石。它们决定了[场算符](@entry_id:140269)之间的相互作用和系统的动力学演化。例如，我们可以利用这些关系来推导[海森堡运动方程](@entry_id:140445)。考虑[哈密顿算符](@entry_id:144286)与矢量势算符在某点 $\mathbf{r}_0$ 的对易子 $[\hat{H}, \hat{\mathbf{A}}(\mathbf{r}_0)]$。由于 $\hat{\mathbf{A}}(\mathbf{r}_0)$ 与 $\hat{\mathbf{A}}(\mathbf{r}')$ 对易，也与 $\nabla' \times \hat{\mathbf{A}}(\mathbf{r}')$ 对易，因此只有[哈密顿量](@entry_id:172864)中的[共轭动量](@entry_id:172203)项（[电场](@entry_id:194326)项）会产生非零贡献。经过计算可以得到一个简洁而深刻的结果 [@problem_id:694017]：
$$
[\hat{H}, \hat{A}_i(\mathbf{r}_0)] = \frac{1}{2\epsilon_0} \int d^3\mathbf{r}' \sum_j [\hat{\Pi}_j(\mathbf{r}')^2, \hat{A}_i(\mathbf{r}_0)] = -\frac{i\hbar}{\epsilon_0} \hat{\Pi}_i(\mathbf{r}_0)
$$
将 $\hat{\mathbf{\Pi}}(\mathbf{r}_0) = -\epsilon_0 \hat{\mathbf{E}}_{\perp}(\mathbf{r}_0)$ 代入，我们得到：
$$
[\hat{H}, \hat{\mathbf{A}}(\mathbf{r}_0)] = i\hbar \hat{\mathbf{E}}_{\perp}(\mathbf{r}_0)
$$
这个关系式与[海森堡运动方程](@entry_id:140445) $\frac{d\hat{\mathbf{A}}}{dt} = \frac{1}{i\hbar}[\hat{\mathbf{A}}, \hat{H}]$ 相结合，便得到了算符形式的麦克斯韦方程 $\frac{\partial \hat{\mathbf{A}}}{\partial t} = -\hat{\mathbf{E}}_{\perp}$，这表明我们的量子化方案与[经典电动力学](@entry_id:270496)是自洽的。

### 场的模式展开

尽管[正则量子化](@entry_id:148501)为我们提供了理论框架，但直接处理连续的[场算符](@entry_id:140269)及其对易关系在实践中非常困难。模式展开的思想就是将[场算符](@entry_id:140269)分解到一组完备正交的函[数基](@entry_id:634389)上，这些[基函数](@entry_id:170178)被称为“模式”。每一种模式都具有简单的时空演化特性。通过这种方式，场的动力学问题被转化为求解每个模式的演化系数的动力学问题。

对于一个给定的物理系统（例如自由空间、[谐振腔](@entry_id:274488)或[波导](@entry_id:198471)），我们总可以找到一组满足[亥姆霍兹方程](@entry_id:149977)和相应边界条件的矢量模式函数 $\mathbf{u}_{\mathbf{k},\lambda}(\mathbf{r})$。于是，矢量势算符 $\hat{\mathbf{A}}(\mathbf{r})$ 可以展开为：
$$
\hat{\mathbf{A}}(\mathbf{r}) = \sum_{\mathbf{k},\lambda} \left[ C_k \mathbf{u}_{\mathbf{k},\lambda}(\mathbf{r}) \hat{a}_{\mathbf{k},\lambda} + C_k^* \mathbf{u}_{\mathbf{k},\lambda}^*(\mathbf{r}) \hat{a}_{\mathbf{k},\lambda}^\dagger \right]
$$
这里，${\mathbf{k},\lambda}$ 是模式的索引（例如波矢和偏振），$\hat{a}_{\mathbf{k},\lambda}$ 和 $\hat{a}_{\mathbf{k},\lambda}^\dagger$ 是该模式对应的湮灭和创生算符，它们是算符性质的来源。$C_k$ 是一个归一化常数。我们要求 $\hat{a}$ 和 $\hat{a}^\dagger$ 满足[玻色子](@entry_id:138266)[对易关系](@entry_id:136780)：$[\hat{a}_{\mathbf{k},\lambda}, \hat{a}_{\mathbf{k}',\lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'} \delta_{\lambda\lambda'}$。

这个展开式的美妙之处在于，通过恰当地选择归一化常数 $C_k$，场的[哈密顿量](@entry_id:172864)可以被[对角化](@entry_id:147016)，呈现为所有模式的[谐振子](@entry_id:155622)[哈密顿量](@entry_id:172864)之和：
$$
\hat{H} = \sum_{\mathbf{k},\lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k},\lambda}^\dagger \hat{a}_{\mathbf{k},\lambda} + \frac{1}{2} \right)
$$
这个过程是模式展开方法的核心。我们可以通过一个具体的例子来演示如何确定归一化常数。考虑一个充满了[折射率](@entry_id:168910)为 $n$ 的均匀、无损耗[电介质](@entry_id:147163)的体积为 $V$ 的空间。场的能量密度为 $\frac{1}{2}(\hat{\mathbf{D}} \cdot \hat{\mathbf{E}} + \hat{\mathbf{B}} \cdot \hat{\mathbf{H}}) = \frac{1}{2}(\epsilon \hat{\mathbf{E}}^2 + \frac{1}{\mu_0} \hat{\mathbf{B}}^2)$，其中 $\epsilon = \epsilon_0 n^2$。我们采用[平面波](@entry_id:189798)模式 $\mathbf{u}_{\mathbf{k},\lambda}(\mathbf{r}) = \vec{\epsilon}_{\mathbf{k},\lambda} e^{i\mathbf{k}\cdot\mathbf{r}}$，其中 $\vec{\epsilon}_{\mathbf{k},\lambda}$ 是偏振矢量。将对应的[场算符](@entry_id:140269)展开式代入[哈密顿量](@entry_id:172864)积分中，利用平面波的正交性 $\int_V e^{i(\mathbf{k}-\mathbf{k}')\cdot\mathbf{r}} d^3r = V \delta_{\mathbf{k}\mathbf{k}'}$，并利用色散关系 $\omega_k = kc/n$ (即 $\epsilon\omega_k^2 = k^2/\mu_0$)，经过一系列代数运算后，我们发现[电场和磁场](@entry_id:261347)对能量的贡献是相等的 [@problem_id:694043]。最终得到的[哈密顿量](@entry_id:172864)为：
$$
\hat{H} = V \sum_{\mathbf{k},\lambda} \epsilon \omega_k^2 C_k^2 (\hat{a}_{\mathbf{k},\lambda}\hat{a}^\dagger_{\mathbf{k},\lambda} + \hat{a}^\dagger_{\mathbf{k},\lambda}\hat{a}_{\mathbf{k},\lambda}) = V \sum_{\mathbf{k},\lambda} \epsilon \omega_k^2 C_k^2 (2\hat{a}^\dagger_{\mathbf{k},\lambda}\hat{a}_{\mathbf{k},\lambda} + 1)
$$
将此表达式与目标[谐振子](@entry_id:155622)形式 $\sum_{\mathbf{k},\lambda} \hbar \omega_k ( \hat{a}^\dagger_{\mathbf{k},\lambda} \hat{a}_{\mathbf{k},\lambda} + 1/2 )$ 进行比较，我们可以立刻确定归一化常数 $C_k$ 必须满足：
$$
2V \epsilon \omega_k^2 C_k^2 = \hbar \omega_k
$$
由此解得：
$$
C_k = \sqrt{\frac{\hbar}{2V \epsilon \omega_k}} = \sqrt{\frac{\hbar}{2V \epsilon_0 n^2 \omega_k}}
$$
这个结果至关重要，它将[场算符](@entry_id:140269)的振幅与基本常数 $\hbar$、模式频率 $\omega_k$、以及系统的宏观属性（体积 $V$ 和[介电常数](@entry_id:146714) $\epsilon$）联系在一起。对于任何给定的几何结构和介质，确定模式[归一化常数](@entry_id:752675)的步骤都是类似的。

### [量子真空](@entry_id:155581)与[零点能](@entry_id:142176)

将场分解为一系列独立的谐振子后，我们可以定义系统的[基态](@entry_id:150928)，即**量子真空态** $|0\rangle$。这个状态的特征是它不包含任何[光子](@entry_id:145192)，即对于所有模式 $(\mathbf{k}, \lambda)$，都有 $\hat{a}_{\mathbf{k},\lambda} |0\rangle = 0$。

然而，真空并非一无所有。将真空态的定义代入[哈密顿量](@entry_id:172864)，我们发现它的能量并非为零：
$$
E_{ZPE} = \langle 0 | \hat{H} | 0 \rangle = \sum_{\mathbf{k},\lambda} \frac{1}{2} \hbar \omega_k
$$
这便是著名的**零点能**（Zero-Point Energy, ZPE）。由于模式的总数是无限的，且频率 $\omega_k$ 可以任意高，这个总和是发散的。这是[量子场论](@entry_id:138177)中遇到的第一个臭名昭著的发散问题。尽管总能量无限，但在大多数物理情境下，我们关心的是能量的*变化*或能量*密度*。

我们可以计算单位体积的零点能，即**[真空能](@entry_id:155067)量密度**。在一个大的量化体积 $V$ 中，模式求和可以近似为积分：$\frac{1}{V}\sum_{\mathbf{k}} \to \int \frac{d^3k}{(2\pi)^3}$。考虑到两种偏振，真空能量密度为：
$$
\langle \mathcal{H} \rangle_0 = \frac{E_{ZPE}}{V} = \frac{1}{V} \sum_{\mathbf{k},\lambda} \frac{\hbar\omega_k}{2} \approx \int \frac{d^3k}{(2\pi)^3} \cdot 2 \cdot \frac{\hbar\omega_k}{2} = \frac{\hbar c}{2\pi^2} \int_0^\infty k^3 dk
$$
这个积分仍然是发散的。为了得到一个有限的结果，物理学家引入了**正则化**（regularization）方案。一个简单的方法是引入一个尖锐的高频截断 $\Omega_c$，即只考虑角频率 $\omega_k \le \Omega_c$（或[波数](@entry_id:172452) $k \le k_{\text{max}} = \Omega_c/c$）的模式。在这种情况下，积分变为 [@problem_id:693835]：
$$
\langle \mathcal{H} \rangle_0^{\text{reg}} = \frac{\hbar c}{2\pi^2} \int_0^{\Omega_c/c} k^3 dk = \frac{\hbar c}{2\pi^2} \frac{(\Omega_c/c)^4}{4} = \frac{\hbar \Omega_c^4}{8\pi^2 c^3}
$$
这个结果表明，[真空能](@entry_id:155067)量密度对截断频率极为敏感，随 $\Omega_c^4$ 增长。虽然这个截断在物理上是人为的，但它揭示了真空涨落的能量主要由[高频模式](@entry_id:750297)贡献。[卡西米尔效应](@entry_id:148651)等物理现象证实了[零点能](@entry_id:142176)的真实存在及其可测量的宏观效应。

我们也可以考察零点能的**谱密度**，即单位[角频率](@entry_id:261565)间隔内的零点能量密度。通过对能量密度表达式进行变量替换 $k = \omega \sqrt{\epsilon\mu}$，我们可以直接读出谱密度函数 [@problem_id:694006]。在一般的均匀介质中，其零点能谱密度为：
$$
\frac{dU_{ZPE}}{d\omega} = \frac{\hbar(\epsilon\mu)^{3/2}}{2\pi^2}\,\omega^3
$$
这个 $\omega^3$ 依赖关系是[真空能](@entry_id:155067)谱的一个普适特征，与著名的普朗克[黑体辐射谱](@entry_id:158574)的低频部分（[瑞利-金斯定律](@entry_id:156467)）在频率依赖性上有所不同（[黑体辐射](@entry_id:137223)为 $\omega^2$）。

### [场算符](@entry_id:140269)的[对易关系](@entry_id:136780)

模式展开不仅简化了[哈密顿量](@entry_id:172864)，它也为计算物理可观测量（如[电场和磁场](@entry_id:261347)）之间的对易关系提供了强有力的工具。这些对易关系反映了[量子涨落](@entry_id:154889)的基本限制，类似于位置和动量的[不确定性原理](@entry_id:141278)。

例如，我们考虑一个沿 $z$ 轴传播的单模一维场。[电场算符](@entry_id:196320) $\hat{E}_x(z)$ 和磁[场算符](@entry_id:140269) $\hat{B}_y(z')$ 的模式展开式可以写出。通过代入展开式并利用创生/湮灭算符的[对易关系](@entry_id:136780) $[\hat{a}_{k,\lambda}, \hat{a}_{k',\lambda'}^\dagger] = 2\pi \delta(k-k') \delta_{\lambda\lambda'}$（这里使用[连续谱](@entry_id:155477)的归一化），我们可以直接计算它们的等时对易子 [@problem_id:693973]。经过一番计算，涉及到一个关键的积分 $\int_0^\infty k \sin(kx) dk = -\pi \delta'(x)$，我们得到：
$$
[\hat{E}_x(z), \hat{B}_y(z')] = -\frac{i\hbar}{\mathcal{A} \epsilon_0} \delta'(z-z')
$$
其中 $\mathcal{A}$ 是模式的有效[截面](@entry_id:154995)积，$\delta'(z-z')$ 是狄拉克-[德尔塔函数](@entry_id:273429)的导数。这个结果表明，电场和磁场算符在同一点并不对易，测量其中一个会不可避免地影响另一个。对易子中出现[德尔塔函数](@entry_id:273429)的导数，反映了[场论](@entry_id:155241)中算符的局域但又相互关联的复杂性质。

### 特定几何构型中的模式

模式展开的威力在处理有边界的物理系统时表现得淋漓尽致。在这些系统中，模式函数不再是简单的[平面波](@entry_id:189798)，而必须适应特定的边界条件，例如在完美[导体表面[电](@entry_id:267665)场](@entry_id:194326)的切向分量为零。

#### 矩形谐振腔

考虑一个尺寸为 $a \times b \times L$ 的矩形金属谐振腔。腔内的[电磁场](@entry_id:265881)模式被离散化。例如，对于横电（TE）模式，其模式函数 $\vec{u}_{mnp}(\vec{r})$ 是由正弦和余弦函数构成的驻波，其中整数 $m, n, p$ 标记了在三个方向上的半[波数](@entry_id:172452)目。

利用这些模式函数，我们可以将腔内的[电场算符](@entry_id:196320)展开。这个 formalism 允许我们计算具体的物理量。例如，我们可以考察当腔内从真空态 $|0\rangle$ 变为包含一个 TE$_{121}$ 模式[光子](@entry_id:145192)的单[光子](@entry_id:145192)态 $|1_{121}\rangle = \hat{a}_{121}^{\dagger}|0\rangle$ 时，腔体中心点 $\vec{r}_0 = (a/2, b/2, L/2)$ 的[电场](@entry_id:194326)强度平方的[期望值](@entry_id:153208)会发生怎样的变化 [@problem_id:694039]。

计算过程包括：
1.  写出特定模式 TE$_{121}$ 在[中心点](@entry_id:636820) $\vec{r}_0$ 的模式函数值 $\vec{u}_{121}(\vec{r}_0)$。由于三角函数的对称性，该矢量可能只沿某个特定方向。
2.  计算 $\langle 0 | \hat{\vec{E}}(\vec{r}_0)^2 | 0 \rangle$ 和 $\langle 1_{121} | \hat{\vec{E}}(\vec{r}_0)^2 | 1_{121} \rangle$。这需要用到算符 $(a-a^\dagger)^2$ 在真空态和单[光子](@entry_id:145192)态下的[矩阵元](@entry_id:186505)，即 $\langle 0 |(a-a^\dagger)^2|0\rangle = -1$ 和 $\langle 1 |(a-a^\dagger)^2|1\rangle = -3$，由于[电场算符](@entry_id:196320)包含因子 $i$, [电场](@entry_id:194326)平方的[期望值](@entry_id:153208)是正的，其真空态和单[光子](@entry_id:145192)态的[期望值](@entry_id:153208)之比为 $1:3$。
3.  两者相减得到变化量 $\Delta E^2$。

最终结果表明，增加一个[光子](@entry_id:145192)使得中心点的[电场](@entry_id:194326)平方[期望值](@entry_id:153208)增加了一个确定的、依赖于腔体几何尺寸和模式频率的量。这清晰地展示了“[光子](@entry_id:145192)”这个量子概念如何与一个可测量的经典量（[电场](@entry_id:194326)强度）联系起来。

#### [波导](@entry_id:198471)

波导是另一种常见的结构，它在两个维度上受限，在一个维度上无限延伸。例如，考虑两块间距为 $a$ 的无限大平行[完美导体](@entry_id:273420)板。其中的横磁（TM）模式的模式函数会包含在受限方向（比如 $y$ 方向）上的正弦函数 $\sin(m\pi y/a)$，以满足边界条件，同时在传播方向（$z$ 方向）上是[行波](@entry_id:185008)形式。

对这些模式进行归一化时，我们遵循与之前相同的原则：要求每个模式对总能量的贡献等于一个[谐振子](@entry_id:155622)的能量。通过对模式函数的平方在量化体积[内积](@entry_id:158127)分，并令其等于 $\frac{\hbar}{2\epsilon_0 \omega}$，我们可以解出归一化系数 [@problem_id:694070]。这个过程再次强调了模式展开方法的普适性，它适用于各种不同的物理边界和几何构型。

### 超越[平面波](@entry_id:189798)：[结构光](@entry_id:163306)与傍轴近似

虽然[平面波](@entry_id:189798)构成了理论的基石，但在许多现代光学应用中，例如[激光](@entry_id:194225)物理，我们处理的是具有复杂横向结构的光束。此时，采用更符合光束几何特征的模式基会更加高效。

#### 傍轴近似

对于沿 $z$ 轴传播的准直光束，其[波矢](@entry_id:178620)量的横向分量 $|\mathbf{k}_T| = \sqrt{k_x^2+k_y^2}$ 通常远小于总波数 $k$。在这种情况下，我们可以对精确的[色散关系](@entry_id:140395) $k_z = \sqrt{k^2 - |\mathbf{k}_T|^2}$ 进行[泰勒展开](@entry_id:145057)，这便是**傍轴近似**（Paraxial Approximation）：
$$
k_z(\mathbf{k}_T) = k\sqrt{1-\frac{|\mathbf{k}_T|^2}{k^2}} \approx k \left( 1 - \frac{|\mathbf{k}_T|^2}{2k^2} \right) = k - \frac{|\mathbf{k}_T|^2}{2k}
$$
这个近似将亥姆霍兹方程简化为了傍轴波动方程，其形式类似于二维空间中的薛定谔方程，其中传播距离 $z$ 扮演了时间的角色，$|\mathbf{k}_T|^2/(2k)$ 则扮演了动能的角色。

我们可以系统地考虑更高阶的修正，即**非傍轴修正**。展开中的下一项是 [@problem_id:693868]：
$$
\Delta k_{z,\text{np}} = k_z - k_{z,\text{par}} \approx -k \frac{1}{8} \left(\frac{|\mathbf{k}_T|^2}{k^2}\right)^2 = -\frac{|\mathbf{k}_T|^4}{8k^3}
$$
对于一个给定的光束轮廓，例如[束腰](@entry_id:267007)半径为 $w_0$ 的[高斯光束](@entry_id:182900)，我们可以计算其在空间频率域的[功率谱](@entry_id:159996)，并据此求出非傍轴修正的平均效应。计算表明，对于[高斯光束](@entry_id:182900)，该平均修正值为 $\langle \Delta k_{z,\text{np}} \rangle = -\frac{1}{k^3w_0^4}$。这个结果显示，光束越窄（$w_0$ 越小），发散角越大（横向频率分量越大），非傍轴效应就越显著。

#### 厄米-高斯模式

在傍轴近似下，厄米-高斯（Hermite-Gaussian）函数族构成了描述光束横向[分布](@entry_id:182848)的一组完备[正交基](@entry_id:264024)。这些模式是傍轴波动方程的精确解，在实验上被广泛用于描述[激光](@entry_id:194225)器的输出模式。

我们可以将[场算符](@entry_id:140269)从[平面波基](@entry_id:140187)变换到厄米-高斯模式基。例如，一个具有特定纵向[波矢](@entry_id:178620) $k_z$ 的[平面波](@entry_id:189798)算符可以展开为该 $k_z$ 对应的所有横向厄米-高斯模式算符的叠加。一个有趣的问题是，傍轴[哈密顿量](@entry_id:172864)在厄米-高斯基下是否是对角化的。将傍轴[哈密顿量](@entry_id:172864) $H \propto (k_z + \frac{k_x^2+k_y^2}{2k_z})$ 和[基变换](@entry_id:189626)关系代入，我们会发现，由于 $k_x^2+k_y^2$ 项的存在，[哈密顿量](@entry_id:172864)矩阵会出现非对角元 [@problem_id:693901]。例如，基模（0,0）和[高阶模](@entry_id:750331)（2,0）之间的[耦合矩阵](@entry_id:191757)元 $H_{00,20}^{(k_z)}$ 不为零，其值为 $-\frac{\hbar c}{2\sqrt{2}\,k_z\,w_0^2}$。这说明，在此特定[哈密顿量](@entry_id:172864)的描述下，纯的厄米-高斯模式并非其本征传播模式，因此会与其他模式发生耦合。这揭示了模式展开中基底选择的微妙之处：一个方便描述某个平面（如[束腰](@entry_id:267007)）上场的基底，不一定是传播算符的本征基底。

### [光子](@entry_id:145192)属性：模式的量子

最后，我们必须将抽象的模式与可观测的[光子](@entry_id:145192)属性联系起来。每个模式 $(\mathbf{k}, \lambda)$ 不仅定义了[光子](@entry_id:145192)的能量和动量，还定义了其内部自由度，如偏振。

偏振可以用一个二维希尔伯特空间来描述。常用的基底有[线偏振](@entry_id:273116)基 $\{|1_x\rangle, |1_y\rangle\}$ 和圆偏振（或[螺旋性](@entry_id:157633)）基 $\{|1_+\rangle, |1_-\rangle\}$，分别对应右旋和左旋圆偏振。它们之间的关系为：
$$
|1_x\rangle = \frac{1}{\sqrt{2}} (|1_+\rangle + |1_-\rangle) \quad , \quad |1_y\rangle = \frac{i}{\sqrt{2}} (-|1_+\rangle + |1_-\rangle)
$$
[螺旋性](@entry_id:157633)是一个可观测量，其对应的算符为 $\hat{S}_z$，本征态是[圆偏振](@entry_id:261702)态：$\hat{S}_z |1_\pm\rangle = \pm\hbar |1_\pm\rangle$。

我们可以利用这个 formalism 来分析任意偏振态的单[光子](@entry_id:145192)。考虑一个由x[线偏振光](@entry_id:165445)和[右旋圆偏振](@entry_id:267955)光叠加而成的单[光子](@entry_id:145192)态 $|\tilde{\psi}\rangle = |1_x\rangle + i \gamma |1_+\rangle$，其中 $\gamma$ 是一个实常数。为了计算其物理属性，我们首先需要将其归一化，然后计算算符在该归一化态下的[期望值](@entry_id:153208) [@problem_id:693949]。

首先，我们将整个态在[圆偏振](@entry_id:261702)基下展开：
$$
|\tilde{\psi}\rangle = \left(\frac{1}{\sqrt{2}} + i \gamma\right) |1_+\rangle + \frac{1}{\sqrt{2}} |1_-\rangle
$$
其模方为 $\langle\tilde{\psi}|\tilde{\psi}\rangle = 1 + \gamma^2$。归一化后，该态的螺旋性[期望值](@entry_id:153208)为：
$$
\langle\hat{S}_z\rangle = \langle\psi|\hat{S}_z|\psi\rangle = \frac{1}{1+\gamma^2} \left[ \left|\frac{1}{\sqrt{2}} + i\gamma\right|^2 (+\hbar) + \left|\frac{1}{\sqrt{2}}\right|^2 (-\hbar) \right] = \frac{\hbar \gamma^2}{1+\gamma^2}
$$
这个结果直观地表明，该[光子](@entry_id:145192)的平均[螺旋性](@entry_id:157633)是右旋和左旋成分的加权平均，权重由叠加系数决定。这个简单的例子完美地诠释了量子力学中的叠加原理，并展示了如何从模式展开的框架中提取单个[光子](@entry_id:145192)的可测量属性。

综上所述，模式展开是连接经典[电磁场](@entry_id:265881)论与[光子](@entry_id:145192)量子力学的桥梁。它通过将场分解为独立的[谐振子](@entry_id:155622)，不仅使问题得以简化，还自然地引出了[光子](@entry_id:145192)的概念，并为计算真空效应、场间关联以及在各种实际物理系统中的量子现象提供了坚实的理论基础。