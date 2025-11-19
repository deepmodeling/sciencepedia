## 引言
在我们对光的理解从经典波动到量子粒子的飞跃中，电[场算符](@entry_id:140269)的概念扮演了核心角色。它将经典电磁学中平滑连续的场，转变为一个描述[光子](@entry_id:145192)产生与湮灭、并蕴含着内在量子涨落的算符实体。经典理论无法解释[自发辐射](@entry_id:140032)、光的[散粒噪声](@entry_id:140025)以及[压缩光](@entry_id:166152)等纯粹的量子现象。为了搭建一个能够精确描述这些行为的框架，我们必须对[电磁场](@entry_id:265881)本身进行量子化。

本文将系统地引导您深入电[场算符](@entry_id:140269)的世界。在“原理与机制”一章中，我们将通过[二次量子化](@entry_id:137766)建立其数学形式，并探讨其在真空态、[光子](@entry_id:145192)数态和相干态等关键[量子态](@entry_id:146142)下的物理意义。接着，在“应用与跨学科联系”一章中，我们将展示该算符如何解释[光与物质的相互作用](@entry_id:268903)，并催生了[腔量子电动力学](@entry_id:149422)、[量子干涉](@entry_id:139127)和[非经典光](@entry_id:190601)场等前沿技术。最后，通过“动手实践”部分，您将有机会将这些理论应用于具体计算。让我们首先从构建电[场算符](@entry_id:140269)的基本原理开始。

## 原理与机制

在经典电磁学中，[电场](@entry_id:194326)被视为一个在时空中平滑变化的矢量场。然而，当量子力学原理应用于[电磁场](@entry_id:265881)时，这一图像发生了根本性的转变。[电场](@entry_id:194326)不再是一个简单的数值矢量，而是一个**算符**，作用于描述场[量子态](@entry_id:146142)的希尔伯特空间。本章旨在深入探讨量子化电[场算符](@entry_id:140269)的定义、基本性质及其在各种[量子态](@entry_id:146142)下的物理表现。

### 电[场算符](@entry_id:140269)的[二次量子化](@entry_id:137766)

将一个经典物理系统量子化的标准程序始于将其用[正则坐标](@entry_id:175654)和[正则动量](@entry_id:155151)表示。对于自由[电磁场](@entry_id:265881)，更便捷的方法是**[二次量子化](@entry_id:137766)**，该方法直接将描述经典场简正模式的振幅提升为[量子算符](@entry_id:137703)。

经典上，在没有源的区域，[电场](@entry_id:194326) $\mathbf{E}(\mathbf{r}, t)$ 可以通过模式展开写成一系列平面波的叠加。量子化后，每个模式的[复振幅](@entry_id:164138)被一对共轭的算符——**湮灭算符** $\hat{a}_{\mathbf{k},\lambda}$ 和**[产生算符](@entry_id:191512)** $\hat{a}_{\mathbf{k},\lambda}^\dagger$——所取代。这些算符分别对应于从模式 $(\mathbf{k}, \lambda)$ 中移除或添加一个能量量子（即[光子](@entry_id:145192)）。它们遵循[玻色子](@entry_id:138266)对易关系：
$$
[\hat{a}_{\mathbf{k},\lambda}, \hat{a}_{\mathbf{k}',\lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'} \delta_{\lambda\lambda'}
$$
$$
[\hat{a}_{\mathbf{k},\lambda}, \hat{a}_{\mathbf{k}',\lambda'}] = [\hat{a}_{\mathbf{k},\lambda}^\dagger, \hat{a}_{\mathbf{k}',\lambda'}^\dagger] = 0
$$
其中 $\mathbf{k}$ 是[波矢](@entry_id:178620)，$\lambda$ 是偏振指数。

在[海森堡绘景](@entry_id:141162)中，电[场算符](@entry_id:140269) $\hat{\mathbf{E}}(\mathbf{r}, t)$ 的一般形式是这些模式算符的线性叠加。对于一个体积为 $V$ 的量子化腔体内的自由场，其表达式为：
$$
\hat{\mathbf{E}}(\mathbf{r}, t) = \sum_{\mathbf{k}, \lambda} i \mathcal{E}_k \left( \boldsymbol{\epsilon}_{\mathbf{k},\lambda} \hat{a}_{\mathbf{k},\lambda} e^{i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)} - \boldsymbol{\epsilon}_{\mathbf{k},\lambda}^* \hat{a}_{\mathbf{k},\lambda}^\dagger e^{-i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)} \right)
$$
这个表达式包含了几个关键部分：
- $\boldsymbol{\epsilon}_{\mathbf{k},\lambda}$ 是模式的（可能为复数）偏振矢量。
- $e^{i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)}$ 是描述[平面波传播](@entry_id:753479)的模式函数。
- $\mathcal{E}_k$ 是一个重要的[归一化常数](@entry_id:752675)，称为**单[光子](@entry_id:145192)[电场](@entry_id:194326)振幅**。

这个振幅 $\mathcal{E}_k$ 的值并非随意设定，它确保了场的[哈密顿量](@entry_id:172864)具有正确的形式。场的总能量是所有模式谐振子能量的总和，其[哈密顿量](@entry_id:172864)为 $\hat{H} = \sum_{\mathbf{k},\lambda} \hbar\omega_k (\hat{a}_{\mathbf{k},\lambda}^\dagger \hat{a}_{\mathbf{k},\lambda} + 1/2)$。通过将量子[哈密顿量](@entry_id:172864)与经典[电磁场](@entry_id:265881)的总能量表达式 $U = \int_V \frac{1}{2}(\epsilon_0 E^2 + B^2/\mu_0) dV$ 相对应，可以确定该振幅。对于真空中的单个模式，其值为：
$$
\mathcal{E}_k = \sqrt{\frac{\hbar \omega_k}{2\epsilon_0 V}}
$$
这个常数的大小揭示了量子效应的尺度：它与普朗克常数 $\hbar$ 的平方根成正比，表明了其纯粹的量子来源。值得注意的是，如果场存在于[折射率](@entry_id:168910)为 $n$ 的介[电介质](@entry_id:147163)中，介质的极化会屏蔽[电场](@entry_id:194326)，导致单[光子](@entry_id:145192)场振幅减小，其归一化常数变为 $\mathcal{E}_k = \sqrt{\frac{\hbar\omega}{2n^2\epsilon_0 V}}$ [@problem_id:2110867]。

### 基本[对易关系](@entry_id:136780)

电[场算符](@entry_id:140269)的量子特性最深刻的体现是其分量之间以及与其他[场算符](@entry_id:140269)之间的非对易性。这些[对易关系](@entry_id:136780)是[量子光学](@entry_id:140582)现象的基础。

#### 场正交算符

对于单个[电磁场](@entry_id:265881)模式，我们可以定义一对**广义正交算符**，它们与[光子](@entry_id:145192)的产生和湮灭算符 $\hat{a}$ 和 $\hat{a}^\dagger$ [线性相关](@entry_id:185830)：
$$
\hat{X}(\theta) = \frac{1}{\sqrt{2}} \left(\hat{a} e^{-i\theta} + \hat{a}^\dagger e^{i\theta}\right)
$$
其中 $\theta$ 是一个可调的实数相位。这个算符对应于测量[电场](@entry_id:194326)[振荡](@entry_id:267781)的某个特定相位分量。例如，$\hat{X}(0)$ 和 $\hat{X}(\pi/2)$ 分别被称为场的“振幅”和“相位”正交分量。利用 $[\hat{a}, \hat{a}^\dagger] = 1$，我们可以直接计算不同相位下正交算符的对易子 [@problem_id:749829]：
$$
[\hat{X}(\theta_1), \hat{X}(\theta_2)] = \frac{1}{2} [ \hat{a}e^{-i\theta_1} + \hat{a}^\dagger e^{i\theta_1}, \hat{a}e^{-i\theta_2} + \hat{a}^\dagger e^{i\theta_2} ] = \frac{1}{2} (e^{i(\theta_2-\theta_1)} - e^{i(\theta_1-\theta_2)}) = i\sin(\theta_2-\theta_1)
$$
这个结果表明，除非 $\theta_2 - \theta_1$ 是 $\pi$ 的整数倍，否则测量两个不同相位的正交分量是不能同时精确进行的。这构成了光场的[海森堡不确定性原理](@entry_id:171099)，是[压缩光](@entry_id:166152)等非经典现象的理论基础。

#### [场算符](@entry_id:140269)的对易关系

更进一步，我们可以计算时空不同点上电场和磁场算符分量之间的对易关系。这是一个更为复杂的计算，需要用到[场的模式展开](@entry_id:196020)和偏振矢量的[完备性关系](@entry_id:139077) $\sum_{\lambda} (\epsilon_{\mathbf{k},\lambda})_i (\epsilon_{\mathbf{k},\lambda}^*)_j = \delta_{ij} - k_i k_j/|\mathbf{k}|^2$。一个基础且重要的结果是[电场](@entry_id:194326)的一个分量与[磁场](@entry_id:153296)的另一个分量之间的等时[对易关系](@entry_id:136780) [@problem_id:2110837]：
$$
[\hat{E}_x(\mathbf{r}), \hat{B}_y(\mathbf{r}')] = -\frac{i\hbar}{\epsilon_0} \frac{\partial}{\partial z} \delta^{(3)}(\mathbf{r}-\mathbf{r}')
$$
这个关系式与单粒子量子力学中的 $[x, p_x] = i\hbar$ 惊人地相似。它揭示了量子[电磁场](@entry_id:265881)的深刻结构：在某一点上精确测量[电场](@entry_id:194326)的 $x$ 分量，会不可避免地导致在该点附近[磁场](@entry_id:153296)的 $y$ 分量产生巨大的、快速变化的不确定性。右侧的狄拉克 $\delta$ 函数的导数表明这种影响是局域的。

在更形式化的层面上，场的算符可以分解为横向（无散度）和纵向（无旋度）部分。在[库仑规范](@entry_id:273044)或时间规范等特定规范选择下，这些分量扮演着不同的角色。例如，在时间规范中，可以证明横向电[场算符](@entry_id:140269) $E_i^T$ 与纵向矢量势算符 $A_j^L$ 在等时条件下是对易的，即 $[E_i^T(t, \mathbf{x}), A_j^L(t, \mathbf{y})] = 0$ [@problem_id:749966]。这反映了场自由度的独立性，是规范[场量子化](@entry_id:160906)理论的一个精细特征。

此外，在[海森堡绘景](@entry_id:141162)中，电[场算符](@entry_id:140269)与系统的[哈密顿量](@entry_id:172864) $\hat{H}$ 和矢量势算符 $\hat{\mathbf{A}}_\perp$ 之间存在一个动力学关系。通过[海森堡运动方程](@entry_id:140445) $\dot{\hat{\mathbf{A}}}_\perp = \frac{i}{\hbar}[\hat{H}, \hat{\mathbf{A}}_\perp]$ 以及经典关系 $\mathbf{E}_\perp = -\dot{\mathbf{A}}_\perp$，我们可以直接将电[场算符](@entry_id:140269)表示为对易子的形式 [@problem_id:756340]：
$$
\hat{E}_{\perp i}(\mathbf{x},t) = -\frac{i}{\hbar} [\hat{H}, \hat{A}_{\perp i}(\mathbf{x},t)]
$$
这强调了[电场](@entry_id:194326)作为矢量势“[共轭动量](@entry_id:172203)”的动力学角色。

### 关键[量子态](@entry_id:146142)中的[电场](@entry_id:194326)

电[场算符](@entry_id:140269)的抽象定义可以通过计算其在各种重要[量子态](@entry_id:146142)下的[期望值](@entry_id:153208)来获得具体的物理意义。

#### 真空态 $|0\rangle$

真空态是场的[基态](@entry_id:150928)，不包含任何[光子](@entry_id:145192)，即对所有模式 $(\mathbf{k}, \lambda)$ 都有 $\hat{a}_{\mathbf{k},\lambda} |0\rangle = 0$。由于电[场算符](@entry_id:140269)是 $\hat{a}$ 和 $\hat{a}^\dagger$ 的[线性组合](@entry_id:154743)，其在真空态下的[期望值](@entry_id:153208)显然为零：
$$
\langle 0 | \hat{\mathbf{E}}(\mathbf{r}, t) | 0 \rangle = 0
$$
这意味着在真空中，平均[电场](@entry_id:194326)为零。然而，这并不意味着真空是“空”的。如果我们计算电[场算符](@entry_id:140269)平方的[期望值](@entry_id:153208)，会得到一个非零结果。考虑一个简化情形，即单个模式的[场算符](@entry_id:140269)在某个特定时空点可以写成 $\hat{E} = \mathcal{E}_0 (\hat{a} + \hat{a}^\dagger)$ [@problem_id:2107523]。其平方的[真空期望值](@entry_id:146340)为：
$$
\langle 0 | \hat{E}^2 | 0 \rangle = \mathcal{E}_0^2 \langle 0 | (\hat{a} + \hat{a}^\dagger)^2 | 0 \rangle = \mathcal{E}_0^2 \langle 0 | \hat{a}\hat{a}^\dagger | 0 \rangle = \mathcal{E}_0^2 \langle 0 | [\hat{a}, \hat{a}^\dagger] | 0 \rangle = \mathcal{E}_0^2
$$
代入 $\mathcal{E}_0^2 = \frac{\hbar\omega}{2\epsilon_0 V}$，我们得到：
$$
\langle 0 | \hat{E}^2 | 0 \rangle = \frac{\hbar\omega}{2\epsilon_0 V}
$$
这个非零结果被称为**真空涨落**或**零点能**。它意味着即使在没有[光子](@entry_id:145192)的情况下，[电场](@entry_id:194326)本身也在不断地涨落。这种涨落是许多物理现象的根源，如自发辐射和[卡西米尔效应](@entry_id:148651)。

#### [福克态](@entry_id:155105)（[光子](@entry_id:145192)数态）$|n\rangle$

[福克态](@entry_id:155105) $|n\rangle$ 是具有确定[光子](@entry_id:145192)数的态。与真空态类似，由于相位不确定，电[场算符](@entry_id:140269)在[福克态](@entry_id:155105)的[期望值](@entry_id:153208)也为零：$\langle n | \hat{\mathbf{E}} | n \rangle = 0$。然而，场的涨落（以 $\langle \hat{E}^2 \rangle$ 度量）则依赖于[光子](@entry_id:145192)数 $n$。对于一个单模[驻波](@entry_id:148648)场 $\hat{E}(z,t) = i \mathcal{E}_{0} ( \hat{a} e^{-i\omega t} - \hat{a}^{\dagger} e^{i\omega t} ) \sin(kz)$，在其波腹处（$\sin(kz)=1$），我们有 [@problem_id:2107494]：
$$
\langle n | \hat{E}^2 | n \rangle = -\mathcal{E}_0^2 \langle n | (\hat{a} - \hat{a}^\dagger)^2 | n \rangle = \mathcal{E}_0^2 \langle n | \hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a} | n \rangle = \mathcal{E}_0^2 ( (n+1) + n ) = \mathcal{E}_0^2 (2n+1)
$$
代入 $\mathcal{E}_0^2$，得到：
$$
\langle \hat{E}^2 \rangle = \frac{\hbar\omega}{\epsilon_0 V} \left(n + \frac{1}{2}\right)
$$
这个结果非常富有启发性。场的总涨落包含两部分：一部分与[光子](@entry_id:145192)数 $n$ 成正比，这可以看作是[光子](@entry_id:145192)到达探测器的随机性所引起的**[散粒噪声](@entry_id:140025)**；另一部分是常数项 $1/2$，它正是我们之前看到的**[真空涨落](@entry_id:154889)**。这表明真空涨落是所有[量子态](@entry_id:146142)固有的背景噪声。

#### [相干态](@entry_id:154533) $|\alpha\rangle$

相干态是[激光](@entry_id:194225)器发出的光的良好近似。它被定义为湮灭算符的[本征态](@entry_id:149904)：$\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$，其中 $\alpha$ 是一个复数。与[福克态](@entry_id:155105)不同，[相干态](@entry_id:154533)的[电场](@entry_id:194326)[期望值](@entry_id:153208)不为零。以一个双模[相干态](@entry_id:154533) $|\Psi\rangle = |\alpha_{\mathbf{k},1}\rangle \otimes |\beta_{\mathbf{k},2}\rangle$ 为例，其中 $\alpha = A$ 和 $\beta = iB$（$A, B$为实数），[电场](@entry_id:194326)的[期望值](@entry_id:153208)计算如下 [@problem_id:360458]：
$$
\langle \Psi | \hat{\mathbf{E}}(\mathbf{r}, t) | \Psi \rangle = -2\sqrt{\frac{\hbar\omega_k}{2\epsilon_0V}} \left( A\sin(\theta) \boldsymbol{\epsilon}_1 + B\cos(\theta) \boldsymbol{\epsilon}_2 \right)
$$
其中 $\theta = \mathbf{k}\cdot\mathbf{r} - \omega_k t$。这个结果是一个行为完全类似于经典[电磁波](@entry_id:269629)的矢量场。其振幅由复数 $\alpha$ 和 $\beta$ 的模决定，而其相位则由它们的辐角决定。这解释了为什么[相干态](@entry_id:154533)被认为是“最经典”的[量子态](@entry_id:146142)。

#### 叠加态与[纠缠态](@entry_id:152310)

电[场算符](@entry_id:140269)还能够揭示叠加态和[纠缠态](@entry_id:152310)中的[量子干涉](@entry_id:139127)和关联。考虑一个单[光子](@entry_id:145192)处于两个[反向传播](@entry_id:199535)模式 $(k, -k)$ 的路径[纠缠态](@entry_id:152310) [@problem_id:749844]：
$$
|\psi\rangle = \frac{1}{\sqrt{2}} \left( |1\rangle_1 |0\rangle_{-1} + e^{i\phi} |0\rangle_1 |1\rangle_{-1} \right)
$$
这是一个单[光子](@entry_id:145192)的“薛定谔的猫”态，它同时处于顺时针和逆时针传播的叠加。计算该状态下[电场](@entry_id:194326)平方的[期望值](@entry_id:153208)，我们会发现一个依赖于空间位置 $z$ 和相对相位 $\phi$ 的[干涉图样](@entry_id:181379)：
$$
\langle \psi | \hat{E}(z,t)^2 | \psi \rangle \propto 2 + \cos(2kz - \phi)
$$
这个结果表明，即使只有一个[光子](@entry_id:145192)，其能量在空间中的[概率分布](@entry_id:146404)（正比于 $\langle \hat{E}^2 \rangle$）也会形成[干涉条纹](@entry_id:176719)。条纹的位置取决于叠加态中的相对相位 $\phi$，这正是量子干涉仪的工作原理。

类似地，通过计算多[光子](@entry_id:145192)态下的多点场关联函数，可以揭示更深层次的[量子关联](@entry_id:136327)。例如，在一个包含一个左旋和一个[右旋圆偏振](@entry_id:267955)[光子](@entry_id:145192)的双光子态 $|\psi\rangle = \hat{a}_{\mathbf{k}_0, R}^\dagger \hat{a}_{\mathbf{k}_0, L}^\dagger |0\rangle$ 中，二阶（正常序）关联函数 $\langle \psi | : \hat{E}_x(\mathbf{r}_1) \hat{E}_x(\mathbf{r}_2) : | \psi \rangle$ 显示出随两点间距变化的余弦调制 [@problem_id:711717]。这表明[光子](@entry_id:145192)场的存在诱导了不同空间点之间场的涨落的关联。

总之，电[场算符](@entry_id:140269)是量子光学中的核心概念。它的定义、对易关系以及在不同[量子态](@entry_id:146142)下的[期望值](@entry_id:153208)，不仅为我们提供了描述和理解光的量子行为的数学工具，也揭示了[真空涨落](@entry_id:154889)、[不确定性原理](@entry_id:141278)和量子干涉等一系列深刻的物理图像。