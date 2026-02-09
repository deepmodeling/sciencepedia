## 引言
在我们对光的理解从经典波动到量子粒子的飞跃中，电场算符的概念扮演了核心角色。它将经典电磁学中平滑连续的场，转变为一个描述光子产生与湮灭、并蕴含着内在量子涨落的算符实体。经典理论无法解释自发辐射、光的散粒噪声以及压缩光等纯粹的量子现象。为了搭建一个能够精确描述这些行为的框架，我们必须对电磁场本身进行量子化。

本文将系统地引导您深入电场算符的世界。在“原理与机制”一章中，我们将通过二次量子化建立其数学形式，并探讨其在真空态、光子数态和相干态等关键量子态下的物理意义。接着，在“应用与跨学科联系”一章中，我们将展示该算符如何解释光与物质的相互作用，并催生了腔量子电动力学、量子干涉和非经典光场等前沿技术。最后，通过“动手实践”部分，您将有机会将这些理论应用于具体计算。让我们首先从构建电场算符的基本原理开始。

## 原理与机制

在经典电磁学中，电场被视为一个在时空中平滑变化的矢量场。然而，当量子力学原理应用于电磁场时，这一图像发生了根本性的转变。电场不再是一个简单的数值矢量，而是一个**算符**，作用于描述场量子态的希尔伯特空间。本章旨在深入探讨量子化电场算符的定义、基本性质及其在各种量子态下的物理表现。

### 电场算符的二次量子化

将一个经典物理系统量子化的标准程序始于将其用正则坐标和正则动量表示。对于自由电磁场，更便捷的方法是**二次量子化**，该方法直接将描述经典场简正模式的振幅提升为量子算符。

经典上，在没有源的区域，电场 $\mathbf{E}(\mathbf{r}, t)$ 可以通过模式展开写成一系列平面波的叠加。量子化后，每个模式的复振幅被一对共轭的算符——**湮灭算符** $\hat{a}_{\mathbf{k},\lambda}$ 和**产生算符** $\hat{a}_{\mathbf{k},\lambda}^\dagger$——所取代。这些算符分别对应于从模式 $(\mathbf{k}, \lambda)$ 中移除或添加一个能量量子（即光子）。它们遵循玻色子对易关系：
$$
[\hat{a}_{\mathbf{k},\lambda}, \hat{a}_{\mathbf{k}',\lambda'}^\dagger] = \delta_{\mathbf{k}\mathbf{k}'} \delta_{\lambda\lambda'}
$$
$$
[\hat{a}_{\mathbf{k},\lambda}, \hat{a}_{\mathbf{k}',\lambda'}] = [\hat{a}_{\mathbf{k},\lambda}^\dagger, \hat{a}_{\mathbf{k}',\lambda'}^\dagger] = 0
$$
其中 $\mathbf{k}$ 是波矢，$\lambda$ 是偏振指数。

在海森堡绘景中，电场算符 $\hat{\mathbf{E}}(\mathbf{r}, t)$ 的一般形式是这些模式算符的线性叠加。对于一个体积为 $V$ 的量子化腔体内的自由场，其表达式为：
$$
\hat{\mathbf{E}}(\mathbf{r}, t) = \sum_{\mathbf{k}, \lambda} i \mathcal{E}_k \left( \boldsymbol{\epsilon}_{\mathbf{k},\lambda} \hat{a}_{\mathbf{k},\lambda} e^{i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)} - \boldsymbol{\epsilon}_{\mathbf{k},\lambda}^* \hat{a}_{\mathbf{k},\lambda}^\dagger e^{-i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)} \right)
$$
这个表达式包含了几个关键部分：
- $\boldsymbol{\epsilon}_{\mathbf{k},\lambda}$ 是模式的（可能为复数）偏振矢量。
- $e^{i(\mathbf{k}\cdot\mathbf{r} - \omega_k t)}$ 是描述平面波传播的模式函数。
- $\mathcal{E}_k$ 是一个重要的归一化常数，称为**单光子电场振幅**。

这个振幅 $\mathcal{E}_k$ 的值并非随意设定，它确保了场的哈密顿量具有正确的形式。场的总能量是所有模式谐振子能量的总和，其哈密顿量为 $\hat{H} = \sum_{\mathbf{k},\lambda} \hbar\omega_k (\hat{a}_{\mathbf{k},\lambda}^\dagger \hat{a}_{\mathbf{k},\lambda} + 1/2)$。通过将量子哈密顿量与经典电磁场的总能量表达式 $U = \int_V \frac{1}{2}(\epsilon_0 E^2 + B^2/\mu_0) dV$ 相对应，可以确定该振幅。对于真空中的单个模式，其值为：
$$
\mathcal{E}_k = \sqrt{\frac{\hbar \omega_k}{2\epsilon_0 V}}
$$
这个常数的大小揭示了量子效应的尺度：它与普朗克常数 $\hbar$ 的平方根成正比，表明了其纯粹的量子来源。值得注意的是，如果场存在于折射率为 $n$ 的介电介质中，介质的极化会屏蔽电场，导致单光子场振幅减小，其归一化常数变为 $\mathcal{E}_k = \sqrt{\frac{\hbar\omega}{2n^2\epsilon_0 V}}$ [@problem_id:2110867]。

### 基本对易关系

电场算符的量子特性最深刻的体现是其分量之间以及与其他场算符之间的非对易性。这些对易关系是量子光学现象的基础。

#### 场正交算符

对于单个电磁场模式，我们可以定义一对**广义正交算符**，它们与光子的产生和湮灭算符 $\hat{a}$ 和 $\hat{a}^\dagger$ 线性相关：
$$
\hat{X}(\theta) = \frac{1}{\sqrt{2}} \left(\hat{a} e^{-i\theta} + \hat{a}^\dagger e^{i\theta}\right)
$$
其中 $\theta$ 是一个可调的实数相位。这个算符对应于测量电场振荡的某个特定相位分量。例如，$\hat{X}(0)$ 和 $\hat{X}(\pi/2)$ 分别被称为场的“振幅”和“相位”正交分量。利用 $[\hat{a}, \hat{a}^\dagger] = 1$，我们可以直接计算不同相位下正交算符的对易子 [@problem_id:749829]：
$$
[\hat{X}(\theta_1), \hat{X}(\theta_2)] = \frac{1}{2} [ \hat{a}e^{-i\theta_1} + \hat{a}^\dagger e^{i\theta_1}, \hat{a}e^{-i\theta_2} + \hat{a}^\dagger e^{i\theta_2} ] = \frac{1}{2} (e^{i(\theta_2-\theta_1)} - e^{i(\theta_1-\theta_2)}) = i\sin(\theta_2-\theta_1)
$$
这个结果表明，除非 $\theta_2 - \theta_1$ 是 $\pi$ 的整数倍，否则测量两个不同相位的正交分量是不能同时精确进行的。这构成了光场的海森堡不确定性原理，是压缩光等非经典现象的理论基础。

#### 场算符的对易关系

更进一步，我们可以计算时空不同点上电场和磁场算符分量之间的对易关系。这是一个更为复杂的计算，需要用到场的模式展开和偏振矢量的完备性关系 $\sum_{\lambda} (\epsilon_{\mathbf{k},\lambda})_i (\epsilon_{\mathbf{k},\lambda}^*)_j = \delta_{ij} - k_i k_j/|\mathbf{k}|^2$。一个基础且重要的结果是电场的一个分量与磁场的另一个分量之间的等时对易关系 [@problem_id:2110837]：
$$
[\hat{E}_x(\mathbf{r}), \hat{B}_y(\mathbf{r}')] = -\frac{i\hbar}{\epsilon_0} \frac{\partial}{\partial z} \delta^{(3)}(\mathbf{r}-\mathbf{r}')
$$
这个关系式与单粒子量子力学中的 $[x, p_x] = i\hbar$ 惊人地相似。它揭示了量子电磁场的深刻结构：在某一点上精确测量电场的 $x$ 分量，会不可避免地导致在该点附近磁场的 $y$ 分量产生巨大的、快速变化的不确定性。右侧的狄拉克 $\delta$ 函数的导数表明这种影响是局域的。

在更形式化的层面上，场的算符可以分解为横向（无散度）和纵向（无旋度）部分。在库仑规范或时间规范等特定规范选择下，这些分量扮演着不同的角色。例如，在时间规范中，可以证明横向电场算符 $E_i^T$ 与纵向矢量势算符 $A_j^L$ 在等时条件下是对易的，即 $[E_i^T(t, \mathbf{x}), A_j^L(t, \mathbf{y})] = 0$ [@problem_id:749966]。这反映了场自由度的独立性，是规范场量子化理论的一个精细特征。

此外，在海森堡绘景中，电场算符与系统的哈密顿量 $\hat{H}$ 和矢量势算符 $\hat{\mathbf{A}}_\perp$ 之间存在一个动力学关系。通过海森堡运动方程 $\dot{\hat{\mathbf{A}}}_\perp = \frac{i}{\hbar}[\hat{H}, \hat{\mathbf{A}}_\perp]$ 以及经典关系 $\mathbf{E}_\perp = -\dot{\mathbf{A}}_\perp$，我们可以直接将电场算符表示为对易子的形式 [@problem_id:756340]：
$$
\hat{E}_{\perp i}(\mathbf{x},t) = -\frac{i}{\hbar} [\hat{H}, \hat{A}_{\perp i}(\mathbf{x},t)]
$$
这强调了电场作为矢量势“共轭动量”的动力学角色。

### 关键量子态中的电场

电场算符的抽象定义可以通过计算其在各种重要量子态下的期望值来获得具体的物理意义。

#### 真空态 $|0\rangle$

真空态是场的基态，不包含任何光子，即对所有模式 $(\mathbf{k}, \lambda)$ 都有 $\hat{a}_{\mathbf{k},\lambda} |0\rangle = 0$。由于电场算符是 $\hat{a}$ 和 $\hat{a}^\dagger$ 的线性组合，其在真空态下的期望值显然为零：
$$
\langle 0 | \hat{\mathbf{E}}(\mathbf{r}, t) | 0 \rangle = 0
$$
这意味着在真空中，平均电场为零。然而，这并不意味着真空是“空”的。如果我们计算电场算符平方的期望值，会得到一个非零结果。考虑一个简化情形，即单个模式的场算符在某个特定时空点可以写成 $\hat{E} = \mathcal{E}_0 (\hat{a} + \hat{a}^\dagger)$ [@problem_id:2107523]。其平方的真空期望值为：
$$
\langle 0 | \hat{E}^2 | 0 \rangle = \mathcal{E}_0^2 \langle 0 | (\hat{a} + \hat{a}^\dagger)^2 | 0 \rangle = \mathcal{E}_0^2 \langle 0 | \hat{a}\hat{a}^\dagger | 0 \rangle = \mathcal{E}_0^2 \langle 0 | [\hat{a}, \hat{a}^\dagger] | 0 \rangle = \mathcal{E}_0^2
$$
代入 $\mathcal{E}_0^2 = \frac{\hbar\omega}{2\epsilon_0 V}$，我们得到：
$$
\langle 0 | \hat{E}^2 | 0 \rangle = \frac{\hbar\omega}{2\epsilon_0 V}
$$
这个非零结果被称为**真空涨落**或**零点能**。它意味着即使在没有光子的情况下，电场本身也在不断地涨落。这种涨落是许多物理现象的根源，如自发辐射和卡西米尔效应。

#### 福克态（光子数态）$|n\rangle$

福克态 $|n\rangle$ 是具有确定光子数的态。与真空态类似，由于相位不确定，电场算符在福克态的期望值也为零：$\langle n | \hat{\mathbf{E}} | n \rangle = 0$。然而，场的涨落（以 $\langle \hat{E}^2 \rangle$ 度量）则依赖于光子数 $n$。对于一个单模驻波场 $\hat{E}(z,t) = i \mathcal{E}_{0} ( \hat{a} e^{-i\omega t} - \hat{a}^{\dagger} e^{i\omega t} ) \sin(kz)$，在其波腹处（$\sin(kz)=1$），我们有 [@problem_id:2107494]：
$$
\langle n | \hat{E}^2 | n \rangle = -\mathcal{E}_0^2 \langle n | (\hat{a} - \hat{a}^\dagger)^2 | n \rangle = \mathcal{E}_0^2 \langle n | \hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a} | n \rangle = \mathcal{E}_0^2 ( (n+1) + n ) = \mathcal{E}_0^2 (2n+1)
$$
代入 $\mathcal{E}_0^2$，得到：
$$
\langle \hat{E}^2 \rangle = \frac{\hbar\omega}{\epsilon_0 V} \left(n + \frac{1}{2}\right)
$$
这个结果非常富有启发性。场的总涨落包含两部分：一部分与光子数 $n$ 成正比，这可以看作是光子到达探测器的随机性所引起的**散粒噪声**；另一部分是常数项 $1/2$，它正是我们之前看到的**真空涨落**。这表明真空涨落是所有量子态固有的背景噪声。

#### 相干态 $|\alpha\rangle$

相干态是激光器发出的光的良好近似。它被定义为湮灭算符的本征态：$\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$，其中 $\alpha$ 是一个复数。与福克态不同，相干态的电场期望值不为零。以一个双模相干态 $|\Psi\rangle = |\alpha_{\mathbf{k},1}\rangle \otimes |\beta_{\mathbf{k},2}\rangle$ 为例，其中 $\alpha = A$ 和 $\beta = iB$（$A, B$为实数），电场的期望值计算如下 [@problem_id:360458]：
$$
\langle \Psi | \hat{\mathbf{E}}(\mathbf{r}, t) | \Psi \rangle = -2\sqrt{\frac{\hbar\omega_k}{2\epsilon_0V}} \left( A\sin(\theta) \boldsymbol{\epsilon}_1 + B\cos(\theta) \boldsymbol{\epsilon}_2 \right)
$$
其中 $\theta = \mathbf{k}\cdot\mathbf{r} - \omega_k t$。这个结果是一个行为完全类似于经典电磁波的矢量场。其振幅由复数 $\alpha$ 和 $\beta$ 的模决定，而其相位则由它们的辐角决定。这解释了为什么相干态被认为是“最经典”的量子态。

#### 叠加态与纠缠态

电场算符还能够揭示叠加态和纠缠态中的量子干涉和关联。考虑一个单光子处于两个反向传播模式 $(k, -k)$ 的路径纠缠态 [@problem_id:749844]：
$$
|\psi\rangle = \frac{1}{\sqrt{2}} \left( |1\rangle_1 |0\rangle_{-1} + e^{i\phi} |0\rangle_1 |1\rangle_{-1} \right)
$$
这是一个单光子的“薛定谔的猫”态，它同时处于顺时针和逆时针传播的叠加。计算该状态下电场平方的期望值，我们会发现一个依赖于空间位置 $z$ 和相对相位 $\phi$ 的干涉图样：
$$
\langle \psi | \hat{E}(z,t)^2 | \psi \rangle \propto 2 + \cos(2kz - \phi)
$$
这个结果表明，即使只有一个光子，其能量在空间中的概率分布（正比于 $\langle \hat{E}^2 \rangle$）也会形成干涉条纹。条纹的位置取决于叠加态中的相对相位 $\phi$，这正是量子干涉仪的工作原理。

类似地，通过计算多光子态下的多点场关联函数，可以揭示更深层次的量子关联。例如，在一个包含一个左旋和一个右旋圆偏振光子的双光子态 $|\psi\rangle = \hat{a}_{\mathbf{k}_0, R}^\dagger \hat{a}_{\mathbf{k}_0, L}^\dagger |0\rangle$ 中，二阶（正常序）关联函数 $\langle \psi | : \hat{E}_x(\mathbf{r}_1) \hat{E}_x(\mathbf{r}_2) : | \psi \rangle$ 显示出随两点间距变化的余弦调制 [@problem_id:711717]。这表明光子场的存在诱导了不同空间点之间场的涨落的关联。

总之，电场算符是量子光学中的核心概念。它的定义、对易关系以及在不同量子态下的期望值，不仅为我们提供了描述和理解光的量子行为的数学工具，也揭示了真空涨落、不确定性原理和量子干涉等一系列深刻的物理图像。