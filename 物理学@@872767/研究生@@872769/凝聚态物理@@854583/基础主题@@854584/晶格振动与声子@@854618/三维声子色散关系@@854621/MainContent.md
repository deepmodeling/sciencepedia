## 引言
晶体中的原子并非静止不动，而是在其[平衡位置](@entry_id:272392)附近不停[振动](@entry_id:267781)。这些集体[振动](@entry_id:267781)的量子化形式被称为“[声子](@entry_id:140728)”，是理解固体宏观物理性质的微观基石。描述[声子](@entry_id:140728)能量（频率）与其动量（[波矢](@entry_id:178620)）之间依赖关系的[声子色散关系](@entry_id:182841)，是[晶格动力学](@entry_id:145448)理论的核心，它如同一张“指纹图谱”，蕴含了关于材料结构、成键和稳定性的丰富信息。

然而，如何从微观的原子间相互作用出发，系统地推导出这张复杂的图谱，并将其与可测量的宏观现象如[热容](@entry_id:137594)、[热导率](@entry_id:147276)、光学响应等精确联系起来，是凝聚态物理学中的一个基本问题。

本文旨在为读者搭建起这座从微观理论到宏观应用的桥梁。在“原理与机制”一章中，我们将建立动力学矩阵的数学框架，详细推导单原子和多原[子基](@entry_id:151637)元晶体的色散关系，并探讨[声子模式](@entry_id:201212)的分类与物理内涵。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[声子谱](@entry_id:753408)如何决定材料的[热力学性质](@entry_id:146047)，如何与其他[准粒子相互作用](@entry_id:146832)，并揭示其与力学、拓扑物理乃至天体物理等领域的深刻联系。最后，“动手实践”部分将通过具体计算问题，巩固读者对核心概念的理解和应用能力。

让我们首先深入[晶格振动](@entry_id:140970)的核心，从其普适的[动力学方程](@entry_id:751029)出发，揭示[声子色散关系](@entry_id:182841)的奥秘。

## 原理与机制

在上一章中，我们介绍了[晶格振动](@entry_id:140970)的概念，并将其量子化为[声子](@entry_id:140728)。本章将深入探讨描述这些[振动](@entry_id:267781)行为的核心数学框架和物理原理。我们将从一般理论出发，推导出三维晶体中[声子频率](@entry_id:753407)与波矢之间的关系——即**[声子色散关系](@entry_id:182841)**——并利用具体的晶格结构实例来阐释其丰富的物理内涵。

### 动力学矩阵：晶格振动的通用框架

为了描述晶体中任意原子的运动，我们从其平衡位置附近的微小位移出发。在**[谐振子近似](@entry_id:268588)** (harmonic approximation) 下，晶体的总势能 $U$ 可以展开为原子位移的二次函数。考虑一个包含 $p$ 个原[子基](@entry_id:151637)元的[晶体结构](@entry_id:140373)，每个[原胞](@entry_id:159354)由格点矢量 $\mathbf{R}$ 标记。[原胞](@entry_id:159354)内第 $\kappa$ 个原子（$\kappa=1, \dots, p$）的质量为 $M_\kappa$，其相对于平衡位置 $\mathbf{R} + \mathbf{d}_\kappa$ 的位移为 $\mathbf{u}(\mathbf{R}, \kappa)$。

该原子所受的力可以表示为：
$$
F_\alpha(\mathbf{R}, \kappa) = - \sum_{\mathbf{R}', \kappa', \beta} \Phi_{\alpha\beta}(\mathbf{R}, \kappa; \mathbf{R}', \kappa') u_\beta(\mathbf{R}', \kappa')
$$
其中，$\alpha, \beta$ 代表笛卡尔坐标分量（$x, y, z$），而 $\Phi_{\alpha\beta}(\mathbf{R}, \kappa; \mathbf{R}', \kappa')$ 是**[力常数](@entry_id:156420)张量** (force-constant tensor)，它描述了在 $(\mathbf{R}', \kappa')$ 位置的原子沿 $\beta$ 方向产生单位位移时，在 $(\mathbf{R}, \kappa)$ 位置的原子沿 $\alpha$ 方向受到的力的负值。

根据牛顿第二定律，运动方程为：
$$
M_\kappa \ddot{u}_\alpha(\mathbf{R}, \kappa) = - \sum_{\mathbf{R}', \kappa', \beta} \Phi_{\alpha\beta}(\mathbf{R}, \kappa; \mathbf{R}', \kappa') u_\beta(\mathbf{R}', \kappa')
$$
由于[晶格](@entry_id:196752)的[平移对称性](@entry_id:171614)，[力常数](@entry_id:156420)仅依赖于[原胞](@entry_id:159354)间的相对位置，即 $\Phi(\mathbf{R}, \kappa; \mathbf{R}', \kappa') = \Phi(\mathbf{0}, \kappa; \mathbf{R}'-\mathbf{R}, \kappa')$。根据布洛赫定理，格波解的形式为行波：
$$
\mathbf{u}(\mathbf{R}, \kappa) = \frac{1}{\sqrt{M_\kappa}} \boldsymbol{\epsilon}(\kappa, \mathbf{k}) \exp[i(\mathbf{k} \cdot (\mathbf{R} + \mathbf{d}_\kappa) - \omega t)]
$$
其中 $\boldsymbol{\epsilon}(\kappa, \mathbf{k})$ 是一个三维的**[极化矢量](@entry_id:269389)** (polarization vector)，描述了[原胞](@entry_id:159354)内第 $\kappa$ 个原子在一个特定模式下的[振动](@entry_id:267781)方向和相对振幅。将此解代入运动方程，经过化简，我们得到一个关于频率 $\omega$ 的[本征值方程](@entry_id:192306)：
$$
\omega^2 \epsilon_\alpha(\kappa) = \sum_{\kappa', \beta} D_{\alpha\beta}(\kappa, \kappa'; \mathbf{k}) \epsilon_\beta(\kappa')
$$
这里的 $D_{\alpha\beta}(\kappa, \kappa'; \mathbf{k})$ 是**动力学矩阵** (Dynamical Matrix) 的[矩阵元](@entry_id:186505)，其定义为：
$$
D_{\alpha\beta}(\kappa, \kappa'; \mathbf{k}) = \frac{1}{\sqrt{M_\kappa M_{\kappa'}}} \sum_{\mathbf{R}'} \Phi_{\alpha\beta}(\mathbf{0}, \kappa; \mathbf{R}', \kappa') \exp[i\mathbf{k} \cdot (\mathbf{R}' + \mathbf{d}_{\kappa'} - \mathbf{d}_\kappa)]
$$
对于一个包含 $p$ 个基元原子的三维晶体，动力学矩阵是一个 $3p \times 3p$ 的厄米矩阵。求解该矩阵的[本征值](@entry_id:154894)，即可得到 $3p$ 个 $\omega^2(\mathbf{k})$ 的值，它们对应 $3p$ 个[声子](@entry_id:140728)**[色散](@entry_id:263750)支** (dispersion branches)。其对应的本征矢量则给出了每个模式的极化特性。

### 单原子布拉伐格子：[声学声子](@entry_id:141298)

对于最简单的情况，即每个原胞只有一个原子（$p=1$）的**布拉伐格子** (Bravais lattice)，动力学矩阵简化为一个 $3 \times 3$ 的矩阵 $D_{\alpha\beta}(\mathbf{k})$。此时，不存在下标 $\kappa$，所有原子质量相同，记为 $M$。$3 \times 1 = 3$ 个[色散](@entry_id:263750)支全部为**[声学支](@entry_id:138762)** (acoustic branches)，其特点是在布里渊区中心（$\mathbf{k} \to 0$）时，频率趋于零。

为了获得更具体的物理图像，我们常常采用简化的**[中心力](@entry_id:267832)模型** (central force model)，即原子间的相互作用力沿着连接它们的直线上，如同弹簧一样。在这种模型下，只考虑最近邻和次近邻的相互作用，动力学矩阵的矩阵元可以表示为：
$$
D_{\alpha\beta}(\mathbf{k}) = \frac{1}{M} \sum_{\mathbf{\delta}} C_{\mathbf{\delta}} (1 - \cos(\mathbf{k} \cdot \mathbf{\delta})) \frac{\delta_\alpha \delta_\beta}{|\mathbf{\delta}|^2}
$$
其中，求和遍历所有邻居矢量 $\mathbf{\delta}$，而 $C_{\mathbf{\delta}}$ 是连接中心原子与位于 $\mathbf{\delta}$ 处的邻居原子之间的等效[弹簧常数](@entry_id:167197)。

#### 实例分析：简单立方（SC）[晶格](@entry_id:196752)

让我们以晶格常数为 $a$ 的单原子简单立方（SC）[晶格](@entry_id:196752)为例。

首先，只考虑连接**最近邻**（Nearest Neighbors, NN）的力，其[力常数](@entry_id:156420)为 $C_1$。最近邻位于 $(\pm a, 0, 0)$, $(0, \pm a, 0)$, $(0, 0, \pm a)$。在一个仅考虑沿坐标轴方向相互作用的简化模型中，动力学矩阵的对角元形如：
$$
D_{xx}(\mathbf{k}) = \frac{2C_1}{M}(1-\cos(k_x a))
$$
且所有非对角元 $D_{xy}(\mathbf{k})$ 等均为零。因此，动力学矩阵是完全对角的。其三个[本征值](@entry_id:154894)可以直接读出，给出三个独立的、分别沿x, y, z方向极化的[声子模式](@entry_id:201212)，它们的色散关系为：
$$
\omega_x^2(\mathbf{k}) = \frac{2C_1}{M}(1-\cos(k_x a)) \\
\omega_y^2(\mathbf{k}) = \frac{2C_1}{M}(1-\cos(k_y a)) \\
\omega_z^2(\mathbf{k}) = \frac{2C_1}{M}(1-\cos(k_z a))
$$
对于一个通用的[波矢](@entry_id:178620) $\mathbf{k}$，这三个模式的频率通常是不同的（非简并的）。

现在，我们让模型更真实一些，引入**次近邻**（Next-Nearest Neighbors, NNN）相互作用，其力常数为 $C_2$。次近邻位于 $(\pm a, \pm a, 0)$ 等位置，距离为 $a\sqrt{2}$。在[计算动力学](@entry_id:204520)矩阵时，需要将这些邻居的贡献也加进去。例如，在[布里渊区](@entry_id:142395)的R点，波矢为 $\mathbf{k}_R = (\pi/a, \pi/a, \pi/a)$，此时 $\mathbf{k}_R \cdot \mathbf{\delta}$ 对于所有最近邻矢量 $\mathbf{\delta} = (\pm a, 0, 0), \dots$ 都会得到 $\pm\pi$。因此 $1-\cos(\mathbf{k}_R \cdot \mathbf{\delta}) = 1 - (-1) = 2$。最近邻贡献使 $D_{xx}$ 增加了 $\frac{2C_1}{M}(1-\cos(\pi)) = \frac{4C_1}{M}$。有趣的是，对于次近邻矢量，如 $\mathbf{\delta}' = (a, a, 0)$，$\mathbf{k}_R \cdot \mathbf{\delta}' = \pi+\pi=2\pi$，导致 $\cos(\mathbf{k}_R \cdot \mathbf{\delta}') = 1$，所以次近邻的贡献项 $(1 - \cos(\mathbf{k}_R \cdot \mathbf{\delta}'))$ 为零。因此在R点，[声子频率](@entry_id:753407)完全由最近邻相互作用决定，即使存在次近邻力。此时动力学矩阵是对角的，且三个对角元相等，$D_{xx}=D_{yy}=D_{zz}=\frac{4C_1}{M}$。这导致在R点有一个三重简并的模式，其频率为 $\omega_R = \sqrt{4C_1/M} = 2\sqrt{C_1/M}$ [@problem_id:180700]。

在其他高[对称点](@entry_id:174836)，情况则有所不同。例如在M点，$\mathbf{k}_M = (\pi/a, \pi/a, 0)$，对于一个沿 $z$ 方向极化的[声子模式](@entry_id:201212)，最近邻 $(\pm a, 0, 0)$ 和 $(0, \pm a, 0)$ 的位移方向与极化方向垂直，不产生贡献。而最近邻 $(0, 0, \pm a)$ 的 $\mathbf{k}_M \cdot \mathbf{\delta} = 0$，贡献也为零。因此，该特定模式的频率完全由次近邻相互作用决定。经过计算，其频率为 $\omega = \sqrt{8C_2/M}$ [@problem_id:180599]。这些例子表明，[声子频率](@entry_id:753407)不仅依赖于[波矢](@entry_id:178620)的大小和方向，还强烈依赖于其极化方式以及[晶格](@entry_id:196752)的几何结构。

### [声子](@entry_id:140728)属性及其物理诠释

#### 长波极限与声速

[声子色散关系](@entry_id:182841)蕴含着丰富的宏观[物理信息](@entry_id:152556)。特别地，在**长波极限** (long-wavelength limit) 下，即[波矢](@entry_id:178620) $\mathbf{k} \to 0$ 时（靠近布里渊区中心Γ点），[声学声子](@entry_id:141298)的色散关系呈现线性特征。我们可以对 $\cos(ka)$ 项进行[泰勒展开](@entry_id:145057)：$1-\cos(ka) \approx \frac{1}{2}(ka)^2$。

以沿 [100] 方向传播的[声子](@entry_id:140728)为例，$\mathbf{k}=(k,0,0)$。对于前面提到的SC[晶格模型](@entry_id:184345)，$\omega_x^2 \approx \frac{2C_1}{M} (\frac{1}{2}(ka)^2) = \frac{C_1 a^2}{M} k^2$。因此，$\omega_x = \sqrt{C_1/M} a k$。这种 $\omega = v_s k$ 的线性关系正是宏观连续介质中声[波的色散](@entry_id:275520)关系，其中 $v_s$ 就是**声速** (speed of sound)。

我们可以将这个思想应用于更复杂的[晶格](@entry_id:196752)，例如面心立方（FCC）[晶格](@entry_id:196752)。考虑一个只含最近邻相互作用（[力常数](@entry_id:156420) $K$）的单原子FCC[晶格](@entry_id:196752)。通过在长波极限下展开动力学矩阵，可以计算沿 [100] 方向传播的声速。计算结果表明，存在三种不同速度的模式。其中，极化方向平行于传播方向 [100] 的**纵向[声学](@entry_id:265335)** (Longitudinal Acoustic, LA) 模式，其声速为 $v_L = a\sqrt{K/(2M)}$。而另外两个极化方向垂直于 [100] 的**横向声学** (Transverse Acoustic, TA) 模式，其声速为 $v_T = a\sqrt{K/(4M)}$ [@problem_id:180699]。这清晰地揭示了微观的[原子间作用力](@entry_id:158182)常数 $K$ 和晶格常数 $a$ 如何决定了宏观的材料[声学](@entry_id:265335)特性。

#### [群速度](@entry_id:147686)

[声子](@entry_id:140728)的**[群速度](@entry_id:147686)** (group velocity) 定义为 $\mathbf{v}_g = \nabla_\mathbf{k} \omega(\mathbf{k})$，即频率 $\omega$ 在 $\mathbf{k}$ 空间的梯度。它描述了携带能量的[声子](@entry_id:140728)波包在晶体中的传播速度。从[色散曲线](@entry_id:197598)来看，[群速度](@entry_id:147686)就是曲线的斜率。

在Γ点附近，[色散关系](@entry_id:140395)是线性的（$\omega = v_s k$），[群速度](@entry_id:147686) $\mathbf{v}_g$ 是一个常数，等于声速 $v_s$。然而，当 $k$ 增大时，色散曲线开始弯曲，[群速度](@entry_id:147686)也随之改变。特别地，在布里渊区的边界上，例如X点，[色散曲线](@entry_id:197598)通常是平坦的，这意味着 $\mathbf{v}_g = 0$。这对应于一种[驻波](@entry_id:148648)状态，[声子](@entry_id:140728)[波包](@entry_id:154698)无法在晶体中传播。我们可以通过对给定的色散关系求导来直接计算群速度。例如，在一个各向异性的SC[晶格](@entry_id:196752)中，其[色散关系](@entry_id:140395)为 $\omega^2(\mathbf{k}) = \frac{2}{M} [ K_x (1 - \cos(k_x a)) + K_y (1 - \cos(k_y a)) + K_z (1 - \cos(k_z a)) ]$。在[波矢](@entry_id:178620) $\mathbf{k} = (0, \pi/(2a), 0)$ 处，通过计算梯度可以得到群速度矢量为 $\mathbf{v}_g = (0, a\sqrt{K_y/(2M)}, 0)$ [@problem_id:180717]，这表明能量仅沿 $y$ 方向传播。

#### [纵模](@entry_id:164178)与[横模](@entry_id:163265)

如前所述，[声子](@entry_id:140728)的[极化矢量](@entry_id:269389) $\boldsymbol{\epsilon}$ 描述了原子的[振动](@entry_id:267781)方向。根据 $\boldsymbol{\epsilon}$ 与波矢 $\mathbf{k}$ 的相对方向，[声子模式](@entry_id:201212)可分为：
- **[纵模](@entry_id:164178) (Longitudinal Mode, L):** [极化矢量](@entry_id:269389)平行于波矢，$\boldsymbol{\epsilon} \parallel \mathbf{k}$。原子[振动](@entry_id:267781)方向与波的传播方向一致，形成疏密波。
- **[横模](@entry_id:163265) (Transverse Mode, T):** [极化矢量](@entry_id:269389)垂直于波矢，$\boldsymbol{\epsilon} \perp \mathbf{k}$。原子[振动](@entry_id:267781)方向垂直于[波的传播](@entry_id:144063)方向，形成剪切波。

在三维空间中，对于给定的 $\mathbf{k}$，总有一个[纵模](@entry_id:164178)和两个相互正交的[横模](@entry_id:163265)。在具有高对称性的方向上（例如[立方晶格](@entry_id:148452)的 [100], [110], [111] 方向），[本征模](@entry_id:174677)式可以严格地分为纯[纵模](@entry_id:164178)和纯[横模](@entry_id:163265)。在一般方向上，本征模式则是纵向和横向位移的混合。

由于[晶格](@entry_id:196752)的各向异性，[纵模](@entry_id:164178)和[横模](@entry_id:163265)的原子位移会“感受”到不同的恢复力，因此它们的频率通常是不同的，这种现象称为**L-T劈裂** (longitudinal-transverse splitting)。例如，在FCC[晶格](@entry_id:196752)的X点，$\mathbf{k}_X = (2\pi/a, 0, 0)$，[纵模](@entry_id:164178)（沿x方向[振动](@entry_id:267781)）和[横模](@entry_id:163265)（沿y或z方向[振动](@entry_id:267781)）的频率平方比为 $\omega_L^2 / \omega_T^2 = 2$ [@problem_id:180695]。同样，在L点，$\mathbf{k}_L = (\pi/a, \pi/a, \pi/a)$，尽管动力学矩阵变得更加复杂，但我们依然可以找到平行于 $\mathbf{k}_L$ 的纵向本征矢和垂直于 $\mathbf{k}_L}$ 的两个简并的横向本征矢。计算表明，[频率比](@entry_id:202730)为 $\omega_L / \omega_T = 2$ [@problem_id:180718]。对不同晶格结构（如BCC [@problem_id:180668]）和不同高对称点的分析，揭示了晶体微观对称性与其[振动](@entry_id:267781)谱之间的深刻联系。

### 含基元晶体：[声学](@entry_id:265335)与[光学声子](@entry_id:136993)

当晶体[原胞](@entry_id:159354)中包含多个原子（$p>1$）时，动力学矩阵的维度增加到 $3p \times 3p$，从而产生 $3p$ 个[声子色散](@entry_id:142059)支。这些[色散](@entry_id:263750)支可以分为两类：
- **3个[声学支](@entry_id:138762) (Acoustic branches):** 其行为与单原子[晶格](@entry_id:196752)的[声子](@entry_id:140728)类似，在 $\mathbf{k} \to 0$ 时 $\omega \to 0$。在长波极限下，这些模式对应于整个[原胞](@entry_id:159354)作为一个整体的平移运动，就像宏观声波一样。
- **$3p-3$个[光学支](@entry_id:137810) (Optical branches):** 即使在 $\mathbf{k} \to 0$ 时，这些模式也具有非零的有限频率。它们对应于原胞内部原子之间的相对运动。

#### 实例分析：NaCl 晶体

NaCl 结构是典型的含双原[子基](@entry_id:151637)元的晶体，可以看作是FCC布拉伐格子，每个格点上附加两个不同类型的离子（如Na$^+$和Cl$^-$）。我们用 $m_1$ 和 $m_2$ 表示它们的质量。假设只存在最近邻间的相互作用（[力常数](@entry_id:156420) $K$），每个原子都有6个不同类型的最近邻。

我们特别关注 $\mathbf{k}=0$ (Γ点) 的情况。此时，所有原胞的运动都是同相位的。我们只需分析一个原胞内两个原子的[相对运动](@entry_id:169798)。设它们的位移分别为 $\mathbf{u}_1$ 和 $\mathbf{u}_2$。运动方程为：
$$
m_1 \ddot{\mathbf{u}}_1 = 6K (\mathbf{u}_2 - \mathbf{u}_1)
$$
$$
m_2 \ddot{\mathbf{u}}_2 = 6K (\mathbf{u}_1 - \mathbf{u}_2)
$$
求解这个[方程组](@entry_id:193238)可以得到两个频率解。一个解是 $\omega^2 = 0$，对应于 $\mathbf{u}_1 = \mathbf{u}_2$，即两个原子一起运动，这是[声学模](@entry_id:263916)式在Γ点的行为。另一个解是 $\omega_O^2 = 6K \frac{m_1+m_2}{m_1 m_2}$ [@problem_id:180719]。这就是**光学声子** (optical phonon) 的频率。在这个模式中，$\mathbf{u}_1$ 和 $\mathbf{u}_2$ 方向相反，即两个子[晶格](@entry_id:196752)在相互“摩擦”。如果原[子带](@entry_id:154462)电（如NaCl），这种[振动](@entry_id:267781)会产生一个[振荡](@entry_id:267781)的[电偶极矩](@entry_id:178520)，从而可以与[电磁波](@entry_id:269629)（光）发生强烈耦合，这便是“光学”[声子](@entry_id:140728)名称的由来。

#### 实例分析：[金刚石结构](@entry_id:199042)

[金刚石结构](@entry_id:199042)是另一种重要的双原[子基](@entry_id:151637)元结构（FCC格子，基元为 $(0,0,0)$ 和 $\frac{a}{4}(1,1,1)$），但基元中的两个原子是相同的。这导致了3个[声学支](@entry_id:138762)和3个[光学支](@entry_id:137810)。其[色散关系](@entry_id:140395)比NaCl更复杂，但在高对称点上仍可进行分析。例如，在X点，可以计算出所有六个[声子模式](@entry_id:201212)的频率，其中最高频率的模式为 $\omega = \sqrt{8\mathcal{K}/(3M)}$，其中 $\mathcal{K}$ 为最近邻[力常数](@entry_id:156420) [@problem_id:180644]。

### 超越简单模型：极性晶体中的[长程力](@entry_id:181779)

上述基于“弹簧”的[短程力](@entry_id:142823)模型对于共价晶体（如硅、金刚石）和金属晶体是很好的近似。但对于离子晶体（如NaCl），原[子带](@entry_id:154462)有效电荷，必须考虑它们之间的长程库仑相互作用。

在极性晶体的[光学模式](@entry_id:188043)中，正负离子的相对运动会产生一个宏观的[电极化强度](@entry_id:141475) $\mathbf{P}$。根据电磁学理论，这个[极化强度](@entry_id:188176)会诱导一个[宏观电场](@entry_id:196409) $\mathbf{E}^{mac}$。对于一个波矢为 $\mathbf{q}$ 的格波，这个[电场](@entry_id:194326)由下式给出：
$$
\mathbf{E}^{mac} = -4\pi \frac{\mathbf{q}(\mathbf{q}\cdot \mathbf{P})}{q^2}
$$
这个[宏观电场](@entry_id:196409)会反过来作用在离子上，提供一个额外的恢复力。这个力的大小和方向依赖于[波矢](@entry_id:178620) $\mathbf{q}$ 的方向，即使在 $\mathbf{q} \to 0$ 的极限下也是如此。这种依赖性导致动力学矩阵中出现一个**非解析** (non-analytic) 的贡献项。

通过将[电场](@entry_id:194326)力 $\mathbf{F}(\kappa) = Z_\kappa e \mathbf{E}^{mac}$ 的表达式与力常数的定义相联系，可以推导出动力学矩阵的非解析部分 [@problem_id:180580]：
$$
D^{NA}_{\alpha\beta}(\kappa\kappa'; \mathbf{q}) = \frac{4\pi e^2}{v_c} \frac{Z_\kappa Z_{\kappa'}}{\sqrt{M_\kappa M_{\kappa'}}} \frac{q_\alpha q_\beta}{q^2}
$$
其中 $Z_\kappa e$ 是离子的有效电荷，$v_c$ 是[原胞](@entry_id:159354)体积。

这个非解析项的物理后果是显著的。
- 对于**纵向光学** (Longitudinal Optical, LO) [声子](@entry_id:140728)，其极化方向 $\boldsymbol{\epsilon}$ 平行于 $\mathbf{q}$。此时 $q_\alpha q_\beta / q^2$ 项不为零，[宏观电场](@entry_id:196409)提供了强大的恢复力，显著提高了[LO声子](@entry_id:140641)的频率 $\omega_{LO}$。
- 对于**横向光学** (Transverse Optical, TO) [声子](@entry_id:140728)，其极化方向 $\boldsymbol{\epsilon}$ 垂直于 $\mathbf{q}$。此时 $\mathbf{q} \cdot \boldsymbol{\epsilon} = 0$，[宏观电场](@entry_id:196409)效应消失。TO[声子](@entry_id:140728)的频率 $\omega_{TO}$ 主要由[短程力](@entry_id:142823)决定。

因此，在极性晶体的Γ点（$\mathbf{q} \to 0$），[纵向光学声子](@entry_id:140641)和[横向光学声子](@entry_id:139212)的频率不再简并，而是发生劈裂，使得 $\omega_{LO} > \omega_{TO}$。这就是著名的**[LO-TO劈裂](@entry_id:138758)**，它是极性晶体一个标志性的特征，其大小直接反映了晶体中长程库仑相互作用的强度。这一现象最终由著名的**Lyddane-Sachs-Teller (LST) 关系**所定量描述。