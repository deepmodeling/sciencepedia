## 引言
在量子世界中，[量子比特](@entry_id:137928)是信息的基本单元，但其状态存在于抽象的[希尔伯特空间](@entry_id:261193)中，难以直观理解。为了克服这一挑战，物理学家们发展出了一种强大的几何工具——[布洛赫矢量](@entry_id:144181)表示法，它将任意单[量子比特](@entry_id:137928)的状态映射到我们熟悉的三维空间中。这种表示法不仅提供了一个优美的视觉图像，更深刻地揭示了[量子态](@entry_id:146142)的性质、其动力学演化以及与测量的关系，成为连接[量子理论](@entry_id:145435)与实验物理不可或缺的桥梁。本文将系统地引导读者深入探索[布洛赫矢量](@entry_id:144181)的世界。在“原理和机制”一章中，我们将奠定其数学基础，揭示纯态、混合态与布洛赫球几何的对应关系。接着，在“应用与跨学科联系”一章中，我们将展示该工具如何在量子光学、[量子计算](@entry_id:142712)乃至广义相对论等前沿领域中发挥作用。最后，通过“动手实践”部分，读者将有机会运用所学知识解决具体物理问题。

## 原理和机制

在量子信息和量子光学领域，最基本的系统是[两能级量子系统](@entry_id:190799)，也就是我们熟知的**[量子比特](@entry_id:137928) (qubit)**。尽管它的[希尔伯特空间](@entry_id:261193)仅有二维，但其[状态和](@entry_id:193625)动力学的丰富性为我们提供了一个理解更复杂量子现象的窗口。为了直观地把握和分析单个[量子比特](@entry_id:137928)的状态，我们引入一个强大的几何工具：**[布洛赫矢量](@entry_id:144181) (Bloch vector)**。本章将详细阐述[布洛赫矢量](@entry_id:144181)的定义、其与[量子态](@entry_id:146142)（纯态和[混合态](@entry_id:141568)）的几何对应关系，以及它在[幺正演化](@entry_id:145020)、退相干过程和[量子测量](@entry_id:272490)中的动力学行为。

### [布洛赫矢量](@entry_id:144181)表示

任何作用于二维希尔伯特空间 $\mathbb{C}^2$ 上的算符都可以由[泡利矩阵](@entry_id:139493) $\sigma_x, \sigma_y, \sigma_z$ 和单位矩阵 $I$ 的[线性组合](@entry_id:154743)来表示。对于一个[量子比特](@entry_id:137928)的状态，其可以用一个 $2 \times 2$ 的**[密度矩阵](@entry_id:139892)** $\rho$ 来描述。[密度矩阵](@entry_id:139892)必须满足三个基本性质：[厄米性](@entry_id:141899) ($\rho^\dagger = \rho$)、正半定性 (所有[本征值](@entry_id:154894)非负) 以及单位迹 ($\text{Tr}(\rho) = 1$)。

基于这些性质，任何单[量子比特](@entry_id:137928)的[密度矩阵](@entry_id:139892) $\rho$ 都可以被唯一地表示为：
$$
\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma}) = \frac{1}{2}(I + r_x \sigma_x + r_y \sigma_y + r_z \sigma_z)
$$
其中 $I$ 是 $2 \times 2$ 的单位矩阵，$\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 是由泡利矩阵组成的矢量。系数 $\vec{r} = (r_x, r_y, r_z)$ 是一个三维实矢量，被称为**[布洛赫矢量](@entry_id:144181)**。

[布洛赫矢量](@entry_id:144181)的物理意义极其重要。它的各个分量直接对应于相应[泡利算符](@entry_id:144061)的[期望值](@entry_id:153208)。我们可以通过计算[期望值](@entry_id:153208)的定义来验证这一点 [@problem_id:2912024]：
$$
\langle \sigma_k \rangle = \text{Tr}(\rho \sigma_k) = \text{Tr}\left(\frac{1}{2}(I + \sum_{j=x,y,z} r_j \sigma_j) \sigma_k\right)
$$
利用[迹的线性](@entry_id:199170)和泡利矩阵的性质 $\text{Tr}(\sigma_k)=0$ 以及 $\text{Tr}(\sigma_j \sigma_k) = 2 \delta_{jk}$ (其中 $\delta_{jk}$ 是克罗内克符号)，我们得到：
$$
\langle \sigma_k \rangle = \frac{1}{2} \left( \text{Tr}(\sigma_k) + \sum_{j} r_j \text{Tr}(\sigma_j \sigma_k) \right) = \frac{1}{2} \left( 0 + \sum_{j} r_j (2 \delta_{jk}) \right) = r_k
$$
因此，[布洛赫矢量](@entry_id:144181) $\vec{r}$ 的分量 $(r_x, r_y, r_z)$ 正是[泡利算符](@entry_id:144061)的[期望值](@entry_id:153208) $(\langle \sigma_x \rangle, \langle \sigma_y \rangle, \langle \sigma_z \rangle)$。这个简单的关系为我们提供了一种通过[可观测量](@entry_id:267133)来刻画[量子态](@entry_id:146142)的途径。

### [量子态](@entry_id:146142)的几何：布洛赫球

[布洛赫矢量](@entry_id:144181) $\vec{r}$ 并不能取遍整个 $\mathbb{R}^3$ 空间。[密度矩阵](@entry_id:139892)的正半定性要求其所有[本征值](@entry_id:154894)必须是非负的，这给 $\vec{r}$ 的长度施加了一个重要的约束。$\rho$ 的[本征值](@entry_id:154894)可以通过求解特征方程得到。注意到泡利矢量 $\vec{r} \cdot \vec{\sigma}$ 的一个重要性质是 $(\vec{r} \cdot \vec{\sigma})^2 = |\vec{r}|^2 I$。由此可知，$\vec{r} \cdot \vec{\sigma}$ 的[本征值](@entry_id:154894)为 $\pm |\vec{r}|$。因此，$\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})$ 的[本征值](@entry_id:154894)为：
$$
\lambda_{\pm} = \frac{1}{2}(1 \pm |\vec{r}|)
$$
正半定性要求 $\lambda_{\pm} \ge 0$，这直接导出 $1 \pm |\vec{r}| \ge 0$，即 $|\vec{r}| \le 1$ [@problem_id:1988528]。这意味着所有物理上允许的单[量子比特](@entry_id:137928)态都对应于一个半径为 1、中心在原点的三维实心球内的点。这个实心球被称为**布洛赫球 (Bloch ball)**。

#### 纯态与[混合态](@entry_id:141568)

布洛赫球的几何结构完美地区分了[量子态](@entry_id:146142)的两种基本类型：[纯态](@entry_id:141688)和混合态。

一个[量子态](@entry_id:146142)是**[纯态](@entry_id:141688) (pure state)**，当且仅当它可以用一个单独的态矢量 $|\psi\rangle$ 来描述，其[密度矩阵](@entry_id:139892)为 $\rho = |\psi\rangle\langle\psi|$。纯态的一个等价代数定义是 $\rho^2 = \rho$。我们将这个条件应用于布洛赫表示：
$$
\rho^2 = \frac{1}{4} (I + 2(\vec{r} \cdot \vec{\sigma}) + (\vec{r} \cdot \vec{\sigma})^2) = \frac{1}{4} ((1 + |\vec{r}|^2)I + 2(\vec{r} \cdot \vec{\sigma}))
$$
令 $\rho^2 = \rho$，即 $\frac{1}{4} ((1 + |\vec{r}|^2)I + 2(\vec{r} \cdot \vec{\sigma})) = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})$。比较系数可得 $1 + |\vec{r}|^2 = 2$，即 $|\vec{r}|^2 = 1$。

这个结果表明，**所有[纯态](@entry_id:141688)都对应于布洛赫球的表面上的点**，即[布洛赫矢量](@entry_id:144181)长度为 1 的态。这个[单位球](@entry_id:142558)面通常被称为**[布洛赫球面](@entry_id:138823) (Bloch sphere)**。反之，所有非纯态被称为**混合态 (mixed states)**，它们对应于布洛赫球内部的点，即 $|\vec{r}|  1$ [@problem_id:1988528]。特别地，位于球心的点 $\vec{r} = \vec{0}$ 对应于[密度矩阵](@entry_id:139892) $\rho = \frac{1}{2}I$，它被称为**[最大混合态](@entry_id:137775) (maximally mixed state)**，代表了对[量子比特](@entry_id:137928)状态信息的最完全无知。

#### [态的纯度](@entry_id:185476)

我们可以用一个标量来量化一个态的“混合程度”，即**纯度 (purity)** $\gamma$，其定义为 $\gamma = \text{Tr}(\rho^2)$。对于纯态，$\gamma=1$；对于[混合态](@entry_id:141568)，$\gamma  1$。对于一个 $d$ 维系统，最小纯度为 $1/d$，对应于[最大混合态](@entry_id:137775)。

利用我们之前计算的 $\rho^2$ 表达式，我们可以直接计算纯度 [@problem_id:744496]：
$$
\gamma = \text{Tr}(\rho^2) = \text{Tr}\left[ \frac{1}{4} \left( (1 + |\vec{r}|^2)I + 2(\vec{r} \cdot \vec{\sigma}) \right) \right]
$$
利用 $\text{Tr}(I) = 2$ 和 $\text{Tr}(\vec{r} \cdot \vec{\sigma}) = 0$，我们得到一个优美的关系：
$$
\gamma = \frac{1}{4} ( (1 + |\vec{r}|^2) \cdot 2 + 0 ) = \frac{1}{2}(1 + |\vec{r}|^2)
$$
这个公式清晰地揭示了纯度与[布洛赫矢量](@entry_id:144181)长度的直接联系。当态是[纯态](@entry_id:141688)时， $|\vec{r}| = 1$，纯度 $\gamma = \frac{1}{2}(1+1) = 1$。当态是[最大混合态](@entry_id:137775)时， $|\vec{r}| = 0$，纯度 $\gamma = \frac{1}{2}(1+0) = \frac{1}{2}$，这与二维系统 ($d=2$) 的最小纯度相符。

#### 物理实例：[热平衡](@entry_id:141693)态

一个与大型热库弱耦合的[两能级系统](@entry_id:196082)，在达到[热平衡](@entry_id:141693)时，其状态由吉布斯态 (Gibbs state) 描述。这是一个典型的[混合态](@entry_id:141568)。假设系统[哈密顿量](@entry_id:172864)为 $H = \frac{1}{2} \hbar \omega \sigma_z$，处在[逆温](@entry_id:140086)度为 $\beta = 1/(k_B T)$ 的环境中。其[密度矩阵](@entry_id:139892)为 [@problem_id:2912024]：
$$
\rho_{\beta} = \frac{\exp(-\beta H)}{\text{Tr}[\exp(-\beta H)]}
$$
利用算符指数的[泰勒展开](@entry_id:145057)以及 $\sigma_z^2 = I$ 的性质，可以得到 $\exp(-a \sigma_z) = \cosh(a) I - \sinh(a) \sigma_z$。令 $a = \frac{1}{2}\beta\hbar\omega$，我们有：
$$
\exp(-\beta H) = \cosh\left(\frac{\beta\hbar\omega}{2}\right) I - \sinh\left(\frac{\beta\hbar\omega}{2}\right) \sigma_z
$$
其迹（[配分函数](@entry_id:193625)）为 $Z = 2\cosh\left(\frac{\beta\hbar\omega}{2}\right)$。因此，热平衡态的密度矩阵为：
$$
\rho_{\beta} = \frac{1}{2} \left[ I - \tanh\left(\frac{\beta\hbar\omega}{2}\right) \sigma_z \right]
$$
与标准布洛赫形式 $\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})$ 比较，我们立刻读出其[布洛赫矢量](@entry_id:144181)为：
$$
\vec{r}_\beta = (0, 0, -\tanh\left(\frac{\beta\hbar\omega}{2}\right))^T
$$
这个结果非常直观。在高温极限下 ($T \to \infty, \beta \to 0$)，$\tanh(\cdot) \to 0$，于是 $\vec{r}_\beta \to \vec{0}$，系统处于[最大混合态](@entry_id:137775)。在低温极限下 ($T \to 0, \beta \to \infty$)，$\tanh(\cdot) \to 1$，于是 $\vec{r}_\beta \to (0, 0, -1)$，系统趋于能量最低的[基态](@entry_id:150928) $|g\rangle$，这是一个[纯态](@entry_id:141688)。这清晰地描绘了一个态如何随着与环境的相互作用（由温度 $T$ 体现）在布洛赫球内部从中心移动到表面的过程。

### [布洛赫矢量](@entry_id:144181)的动力学

[布洛赫矢量](@entry_id:144181)不仅能静态地描述[量子态](@entry_id:146142)，还能生动地描绘其随时间的演化。

#### [幺正演化](@entry_id:145020)：进动

对于一个孤立的量子系统，其演化是幺正的，由刘维尔-冯诺依曼方程描述：
$$
i\hbar \frac{d\rho}{dt} = [H, \rho]
$$
考虑一个一般的[哈密顿量](@entry_id:172864) $H = \frac{\hbar}{2}\vec{\omega} \cdot \vec{\sigma}$，其中 $\vec{\omega}$ 是一个具有角频率量纲的实矢量。将 $\rho$ 的布洛赫表示代入方程，我们得到：
$$
i\hbar \frac{d}{dt}\left(\frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})\right) = \left[\frac{\hbar}{2}\vec{\omega} \cdot \vec{\sigma}, \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})\right]
$$
利用[泡利矩阵](@entry_id:139493)的[对易关系](@entry_id:136780) $[\sigma_i, \sigma_j] = 2i \sum_k \epsilon_{ijk} \sigma_k$，其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)，对易子可以化简为 $[\vec{\omega} \cdot \vec{\sigma}, \vec{r} \cdot \vec{\sigma}] = 2i (\vec{\omega} \times \vec{r}) \cdot \vec{\sigma}$。代入原方程并化简，我们得到一个经典的矢量方程：
$$
\frac{d\vec{r}}{dt} = \vec{\omega} \times \vec{r}
$$
这个方程描述了一个矢量 $\vec{r}$ 绕着一个固定的轴 $\vec{\omega}$ 以角速度 $|\vec{\omega}|$ 进行**进动 (precession)**。这揭示了一个深刻的联系：**单[量子比特](@entry_id:137928)的[幺正演化](@entry_id:145020)在几何上等价于其[布洛赫矢量](@entry_id:144181)的刚性旋转。**

例如，考虑一个[量子比特](@entry_id:137928)处在沿 z 轴的静[磁场](@entry_id:153296)中，其[哈密顿量](@entry_id:172864)为 $H = \frac{\hbar\omega}{2}\sigma_z$。此时，进动矢量为 $\vec{\omega}=(0,0,\omega)$。如果系统初始处于[布洛赫矢量](@entry_id:144181)为 $\vec{r}(0) = (1, 0, 0)$ 的状态（即 $|+\rangle_x$ 态），它的演化方程为 $\dot{r}_x = -\omega r_y$, $\dot{r}_y = \omega r_x$, $\dot{r}_z = 0$。解得 $\vec{r}(t) = (\cos(\omega t), \sin(\omega t), 0)$。这正是[布洛赫矢量](@entry_id:144181)在 x-y 平面内绕 z 轴的匀速旋转 [@problem_id:744404]。

#### 驱动系统与[旋转坐标系](@entry_id:170324)

在[量子光学](@entry_id:140582)和[磁共振](@entry_id:143712)中，系统常受到外部场的驱动。例如，一个固有频率为 $\omega_0$ 的[量子比特](@entry_id:137928)被频率为 $\omega_d$ 的驱动场驱动。在驱动频率 $\omega_d$ 的旋转坐标系中，并采用[旋转波近似 (RWA)](@entry_id:198719)，系统的演化由一个时间无关的[有效哈密顿量](@entry_id:748813) $H'$ 描述 [@problem_id:744429]：
$$
H' = \frac{\hbar\Omega}{2}\sigma_x + \frac{\hbar\Delta}{2}\sigma_z
$$
其中 $\Omega$ 是[拉比频率](@entry_id:154019) (Rabi frequency)，表征驱动场强度，$\Delta = \omega_0 - \omega_d$ 是失谐 (detuning)。在这个旋转坐标系中，[布洛赫矢量](@entry_id:144181) $\vec{r}$ 的动力学遵循同样的进动规则，但围绕的是一个**有效场矢量** $\vec{\Omega}_{\text{eff}} = (\Omega, 0, \Delta)$：
$$
\frac{d\vec{r}}{dt} = \vec{\Omega}_{\text{eff}} \times \vec{r}
$$
这意味着[布洛赫矢量](@entry_id:144181)将绕着由驱动强度和[失谐](@entry_id:148084)共同决定的轴进行进动，进动频率为广义[拉比频率](@entry_id:154019) $\Omega_R = |\vec{\Omega}_{\text{eff}}| = \sqrt{\Omega^2 + \Delta^2}$。例如，一个从[基态](@entry_id:150928) $\vec{r}(0) = (0,0,-1)$ 开始演化的系统，其[布洛赫矢量](@entry_id:144181)会绕 $\vec{\Omega}_{\text{eff}}$ 描绘出一个圆锥面。这种运动的 $z$ 分量 $w(t) = \langle\sigma_z\rangle(t)$ 会以频率 $\Omega_R$ [振荡](@entry_id:267781)，这就是著名的**[拉比振荡](@entry_id:137940)**。其长时间平均的布居数反转 $\bar{w}$ 会收敛到一个依赖于 $\Omega$ 和 $\Delta$ 的[稳态](@entry_id:182458)值 $\bar{w} = -\frac{\Delta^2}{\Omega^2+\Delta^2}$ [@problem_id:744429]。

#### 非[幺正演化](@entry_id:145020)：[退相干](@entry_id:145157)

当[量子比特](@entry_id:137928)与环境发生相互作用时，其演化不再是幺正的，[态的纯度](@entry_id:185476)会降低，这个过程称为**退相干 (decoherence)**。这种演化可以用**量子通道 (quantum channel)** 来描述，它是一个作用在密度矩阵上的[线性映射](@entry_id:185132) $\mathcal{E}$。在布洛赫球图像中，[退相干](@entry_id:145157)过程通常表现为[布洛赫矢量](@entry_id:144181)的收缩。

考虑一个**广义退极化通道 (generalized depolarizing channel)**，它以概率 $p$ 将[量子比特](@entry_id:137928)重置到一个固定的态 $\rho_0$（[布洛赫矢量](@entry_id:144181)为 $\vec{r}_0$），以概率 $1-p$ 保持原态不变 [@problem_id:744474]。其作用为：
$$
\mathcal{E}(\rho) = (1-p)\rho + p \rho_0
$$
将布洛赫表示代入，我们发现输出态的[布洛赫矢量](@entry_id:144181) $\vec{r}'$ 与输入态的 $\vec{r}$ 之间存在一个简单的仿射变换关系：
$$
\vec{r}' = (1-p)\vec{r} + p\vec{r}_0
$$
这个变换将整个布洛赫球线性地收缩了因子 $1-p$，并平移到以 $\vec{r}_0$ 为中心。所有初始态构成的布洛赫球，经过此通道后，会变成一个半径为 $1-p$ 的小球，球心位于 $p\vec{r}_0$。整个[状态空间](@entry_id:177074)的体积收缩了 $(1-p)^3$ 倍。如果 $\rho_0$ 是[最大混合态](@entry_id:137775) ($\vec{r}_0 = \vec{0}$)，则布洛赫球向着原点均匀收缩。

另一种重要的[退相干](@entry_id:145157)模型是**退相（或[相位阻尼](@entry_id:147888)）通道 (dephasing channel)**。它描述了[量子比特](@entry_id:137928)沿某个特定方向 $\hat{n}$ 的相位信息逐渐丢失的过程。其映射形式为 [@problem_id:744499]：
$$
\mathcal{E}(\rho) = \left(1-\frac{\lambda}{2}\right)\rho + \frac{\lambda}{2} (\hat{n} \cdot \vec{\sigma}) \rho (\hat{n} \cdot \vec{\sigma})
$$
其中 $\lambda \in [0,1]$ 是退相强度。通过代数运算，可以导出[布洛赫矢量](@entry_id:144181)的变换规则：
$$
\vec{r}' = (1-\lambda)\vec{r} + \lambda(\hat{n} \cdot \vec{r})\hat{n}
$$
这个变换可以被分解为沿 $\hat{n}$ 方向的投影和垂直于 $\hat{n}$ 的投影。令 $\vec{r} = \vec{r}_\parallel + \vec{r}_\perp$，其中 $\vec{r}_\parallel = (\hat{n}\cdot\vec{r})\hat{n}$。变换可以写作 $\vec{r}' = \vec{r}_\parallel + (1-\lambda)\vec{r}_\perp$。这表明，[布洛赫矢量](@entry_id:144181)平行于 $\hat{n}$ 的分量保持不变，而垂直于 $\hat{n}$ 的分量被因子 $1-\lambda$ 压缩。几何上，这意味着布洛赫球被“压扁”成一个沿 $\hat{n}$ 轴的旋转[椭球体](@entry_id:165811)。这个过程的体积收缩因子是 $(1-\lambda)^2$。

### [布洛赫矢量](@entry_id:144181)与量子测量

[布洛赫矢量](@entry_id:144181)表示法也为理解量子测量提供了直观的几何图像。

#### [期望值](@entry_id:153208)与[方差](@entry_id:200758)

考虑一个对应于可观测量 $\hat{M} = \hat{n} \cdot \vec{\sigma}$ 的投影测量，其中 $\hat{n}$ 是一个单位矢量，定义了[布洛赫球面](@entry_id:138823)上的一个测量轴。该测量的可能结果是其[本征值](@entry_id:154894) $\pm 1$。对于处在态 $\rho$ ([布洛赫矢量](@entry_id:144181)为 $\vec{r}$) 的[量子比特](@entry_id:137928)，测量的[期望值](@entry_id:153208)为 [@problem_id:744572]：
$$
\langle \hat{M} \rangle = \text{Tr}(\rho \hat{M}) = \text{Tr}\left(\frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})(\hat{n} \cdot \vec{\sigma})\right)
$$
利用[泡利矩阵](@entry_id:139493)的恒等式 $(\vec{a} \cdot \vec{\sigma})(\vec{b} \cdot \vec{\sigma}) = (\vec{a} \cdot \vec{b})I + i(\vec{a} \times \vec{b}) \cdot \vec{\sigma}$，我们得到：
$$
\langle \hat{M} \rangle = \frac{1}{2} \text{Tr}((\vec{r} \cdot \hat{n})I + i(\vec{r} \times \hat{n})\cdot\vec{\sigma}) = \vec{r} \cdot \hat{n}
$$
这个结果极其优雅：**任意泡利测量 $\hat{n} \cdot \vec{\sigma}$ 的[期望值](@entry_id:153208)就是[布洛赫矢量](@entry_id:144181) $\vec{r}$ 在测量轴 $\hat{n}$ 上的投影。**

测量结果的概率也由此确定。得到 $+1$ 的概率是 $P(+1) = \frac{1}{2}(1 + \langle \hat{M} \rangle) = \frac{1}{2}(1 + \vec{r} \cdot \hat{n})$，得到 $-1$ 的概率是 $P(-1) = \frac{1}{2}(1 - \langle \hat{M} \rangle) = \frac{1}{2}(1 - \vec{r} \cdot \hat{n})$。

测量结果的不确定性可以用[方差](@entry_id:200758) $(\Delta M)^2 = \langle \hat{M}^2 \rangle - \langle \hat{M} \rangle^2$ 来量化。由于 $\hat{M}^2 = (\hat{n} \cdot \vec{\sigma})^2 = |\hat{n}|^2 I = I$，我们有 $\langle \hat{M}^2 \rangle = \text{Tr}(\rho I) = \text{Tr}(\rho) = 1$。因此，[方差](@entry_id:200758)为 [@problem_id:744572]：
$$
(\Delta M)^2 = 1 - (\vec{r} \cdot \hat{n})^2
$$
这个公式的几何意义非常清晰：当态矢量 $\vec{r}$ 与测量轴 $\hat{n}$ 平行或反平行时（即 $\vec{r} \cdot \hat{n} = \pm 1$），[方差](@entry_id:200758)为零，测量结果是确定的。当 $\vec{r}$ 与 $\hat{n}$ 正交时 ($\vec{r} \cdot \hat{n} = 0$)，[方差](@entry_id:200758)达到最大值 1，测量结果具有最大的不确定性。

#### 态的可区分性：[迹距离](@entry_id:142668)

布洛赫球的几何距离是否具有操作意义？答案是肯定的，它与[量子态](@entry_id:146142)的可区分性直接相关。两个[量子态](@entry_id:146142) $\rho_1$ 和 $\rho_2$ 的可区分性由**[迹距离](@entry_id:142668) (trace distance)** $D(\rho_1, \rho_2)$ 来量化，定义为：
$$
D(\rho_1, \rho_2) = \frac{1}{2} \text{Tr}\left|\rho_1 - \rho_2\right| = \frac{1}{2} \text{Tr}\left(\sqrt{(\rho_1 - \rho_2)^\dagger (\rho_1 - \rho_2)}\right)
$$
[迹距离](@entry_id:142668)的取值范围为 $[0, 1]$，其中 $D=0$ 表示两态相同，$D=1$ 表示两态可以通过单次测量被完美区分。

现在，我们来考察两个[纯态](@entry_id:141688) $\rho_1$ 和 $\rho_2$ 的[迹距离](@entry_id:142668)，它们的[布洛赫矢量](@entry_id:144181)分别为 $\vec{r}_1$ 和 $\vec{r}_2$ ($|\vec{r}_1| = |\vec{r}_2| = 1$)。它们密度矩阵的差为：
$$
\rho_1 - \rho_2 = \frac{1}{2}((\vec{r}_1 - \vec{r}_2) \cdot \vec{\sigma})
$$
计算 $(\rho_1 - \rho_2)^2$：
$$
(\rho_1 - \rho_2)^2 = \frac{1}{4} ((\vec{r}_1 - \vec{r}_2) \cdot \vec{\sigma})^2 = \frac{1}{4} |\vec{r}_1 - \vec{r}_2|^2 I
$$
因此，$|\rho_1 - \rho_2| = \sqrt{(\rho_1 - \rho_2)^2} = \frac{1}{2} |\vec{r}_1 - \vec{r}_2| I$。代入[迹距离](@entry_id:142668)的定义 [@problem_id:2126156]：
$$
D(\rho_1, \rho_2) = \frac{1}{2} \text{Tr}\left(\frac{1}{2} |\vec{r}_1 - \vec{r}_2| I\right) = \frac{1}{4} |\vec{r}_1 - \vec{r}_2| \text{Tr}(I) = \frac{1}{2} |\vec{r}_1 - \vec{r}_2|
$$
这个简洁的结果表明，**两个[纯态](@entry_id:141688)之间的[迹距离](@entry_id:142668)恰好是它们在[布洛赫球面](@entry_id:138823)上对应点之间[欧几里得距离](@entry_id:143990)的一半。** 这为布洛赫球的几何赋予了深刻的操作意义。球面上距离最远的两个点是对跖点，它们的欧几里得距离为 2，对应的[迹距离](@entry_id:142668)为 1。这正好对应于两个正交的纯态，它们是完全可以区分的。

综上所述，[布洛赫矢量](@entry_id:144181)表示法不仅为单[量子比特](@entry_id:137928)态提供了一个优雅的几何图像，还将[态的纯度](@entry_id:185476)、幺正与非幺正动力学、以及测量的统计性质与这个几何空间的结构紧密地联系在一起，是研究量子信息与[量子光学](@entry_id:140582)不可或缺的基础工具。