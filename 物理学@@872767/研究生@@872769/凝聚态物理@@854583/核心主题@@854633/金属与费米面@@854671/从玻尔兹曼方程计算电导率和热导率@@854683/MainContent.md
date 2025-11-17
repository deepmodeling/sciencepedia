## 引言
在固态物理与[材料科学](@entry_id:152226)领域，理解[电荷](@entry_id:275494)与热量如何在材料[内部流动](@entry_id:155636)是探索物质基本属性和推动技术创新的核心。从计算机芯片的散热到温差发电器件的效率，宏观的输运性质——如电导率和热导率——直接决定了材料的应用前景。然而，这些宏观可测的量源于微观世界中电子与[晶格](@entry_id:196752)、杂质之间复杂的相互作用。如何在微观的量子力学行为与宏观的经典输运现象之间建立一座定量的桥梁？这正是[凝聚态理论](@entry_id:141958)长期以来致力于解决的核心问题。[玻尔兹曼输运方程](@entry_id:140472)（Boltzmann Transport Equation, BTE）正是为应对这一挑战而生的强大理论工具。

本篇文章将系统地引导读者深入玻尔兹曼方程的世界，揭示其如何成为理解固体电热输运现象的基石。我们将从第一章“原则与机制”开始，建立玻尔兹曼方程的基本形式，阐明关键的[弛豫时间近似](@entry_id:138429)，并用它来推导基本的[电导](@entry_id:177131)、磁输运和[温差电效应](@entry_id:141235)。接着，在第二章“应用与跨学科联系”中，我们将视野扩展到更广阔的领域，探讨BTE如何解释介观尺寸效应、复杂材料中的集体行为（如电子[流体力学](@entry_id:136788)）、[非线性响应](@entry_id:188175)以及其在自旋电子学、超导和天体物理中的前沿应用。最后，通过第三章“动手实践”中的具体计算问题，读者将有机会亲手运用这些理论，将抽象的公式转化为对物理世界可量化的洞察。通过这一系列的学习，你将掌握一个贯穿凝聚态物理多个分支的统一分析框架。

## 原则与机制

在本章中，我们将深入探讨描述固体中电子输运现象的核心理论框架——[玻尔兹曼输运方程](@entry_id:140472)（Boltzmann Transport Equation, BTE）。作为连接微观[量子态](@entry_id:146142)与宏观[输运系数](@entry_id:136790)的桥梁，BTE 在半经典图像下为我们理解和计算[电导率](@entry_id:137481)、热导率、[霍尔系数](@entry_id:145549)等关键物理量提供了强有力的工具。我们将首先建立 BTE 的基本形式，特别是在[弛豫时间近似](@entry_id:138429)下的应用，然后系统地运用它来解析各种重要的[输运现象](@entry_id:147655)，从基本的直流和交流[电导](@entry_id:177131)，到[磁场](@entry_id:153296)下的霍尔效应与磁阻，再到更为复杂的[温差电效应](@entry_id:141235)和电子[流体力学](@entry_id:136788)行为。

### [玻尔兹曼输运方程 (BTE)](@entry_id:156362)

在固体的半经典模型中，电子的状态由其在相空间中的[分布函数](@entry_id:145626) $f(\mathbf{r}, \mathbf{k}, t)$ 完整描述。该函数给出了在时刻 $t$，位于空间位置 $\mathbf{r}$ 附近、具有波矢 $\mathbf{k}$ 的电子态被占据的概率。在没有碰撞或散射的情况下，相空间中的“粒子流”是守恒的，这可以用[刘维尔定理](@entry_id:191167)来表述：分布函数的[全时间导数](@entry_id:172646)为零。

$$
\frac{df}{dt} = \frac{\partial f}{\partial t} + \dot{\mathbf{r}} \cdot \nabla_{\mathbf{r}} f + \dot{\mathbf{k}} \cdot \nabla_{\mathbf{k}} f = 0
$$

这里，$\dot{\mathbf{r}} = \mathbf{v}_{\mathbf{k}} = \frac{1}{\hbar}\nabla_{\mathbf{k}}\epsilon_{\mathbf{k}}$ 是电子的群速度，$\dot{\mathbf{k}} = \frac{\mathbf{F}}{\hbar}$ 是作用在电子上的外力（如电场和磁场引起的洛伦兹力）所导致的[波矢](@entry_id:178620)变化率。然而，在真实的晶体中，电子会与[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）、杂质、缺陷等发生碰撞，这些碰撞过程会改变电子的动量和能量，从而使分布函数趋向于[热平衡](@entry_id:141693)态。我们将这些复杂的碰撞过程的影响归结为一项碰撞项，记为 $\left( \frac{\partial f}{\partial t} \right)_{\text{coll}}$。于是，完整的[玻尔兹曼输运方程](@entry_id:140472)写为：

$$
\frac{\partial f}{\partial t} + \mathbf{v}_{\mathbf{k}} \cdot \nabla_{\mathbf{r}} f + \frac{\mathbf{F}}{\hbar} \cdot \nabla_{\mathbf{k}} f = \left( \frac{\partial f}{\partial t} \right)_{\text{coll}}
$$

**[弛豫时间近似 (RTA)](@entry_id:754231)**

直接处理碰撞项是极其复杂的。一个极为有效且广泛应用的简化是**[弛豫时间近似](@entry_id:138429)** (Relaxation Time Approximation, RTA)。该近似的核心思想是，任何由外场引起的对[平衡分布](@entry_id:263943) $f_0$（通常是[费米-狄拉克分布](@entry_id:138909)）的偏离，都会以一个特征时间尺度 $\tau$ 指数衰减回[平衡态](@entry_id:168134)。数学上，这表示为：

$$
\left( \frac{\partial f}{\partial t} \right)_{\text{coll}} = -\frac{f - f_0}{\tau} = -\frac{g}{\tau}
$$

其中 $g = f - f_0$ 是分布函数对平衡态的偏离，$\tau$ 被称为**[弛豫时间](@entry_id:191572)**或**[散射时间](@entry_id:272979)**。这个时间通常依赖于电子的能量 $\epsilon$ 和具体的[散射机制](@entry_id:136443)。

**线性化 BTE**

在大多数实验条件下，外场（如[电场](@entry_id:194326)）是微扰，它引起的分布函数偏离 $g$ 是一个小量。因此，我们可以对 BTE 进行线性化。假设体系在空间上是均匀的（$\nabla_{\mathbf{r}} f = 0$），且外力 $\mathbf{F}$ 很小，我们可以忽略包含 $g$ 的高阶项，例如 $\mathbf{F} \cdot \nabla_{\mathbf{k}} g$。于是，BTE 中的力学项变为：

$$
\frac{\mathbf{F}}{\hbar} \cdot \nabla_{\mathbf{k}} f \approx \frac{\mathbf{F}}{\hbar} \cdot \nabla_{\mathbf{k}} f_0
$$

利用链式法则，$\nabla_{\mathbf{k}} f_0 = \frac{\partial f_0}{\partial \epsilon} \nabla_{\mathbf{k}} \epsilon = \frac{\partial f_0}{\partial \epsilon} \hbar \mathbf{v}_{\mathbf{k}}$，线性化的 BTE 最终写为：

$$
\frac{\partial g}{\partial t} + \mathbf{v}_{\mathbf{k}} \cdot \nabla_{\mathbf{r}} g + \mathbf{v}_{\mathbf{k}} \cdot \mathbf{F} \frac{\partial f_0}{\partial \epsilon} = -\frac{g}{\tau}
$$

在金属等简并电子系统中，在低温下，导数项 $(-\frac{\partial f_0}{\partial \epsilon})$ 表现为一个在费米能 $\epsilon_F$ 处达到峰值的尖锐函数，近似于一个狄拉克 $\delta(\epsilon - \epsilon_F)$ 函数。这意味着只有费米面附近的电子才对输运过程有显著贡献，这正是 BTE 框架下所得结果的深刻物理内涵。

### 电导率

电导率描述了材料在[电场](@entry_id:194326)作用下传导电流的能力。利用 BTE，我们可以从微观[散射机制](@entry_id:136443)和能带结构出发，推导出[电导率](@entry_id:137481)。

**直流 (DC) 电导率**

考虑一个处于均匀静态[电场](@entry_id:194326) $\mathbf{E}$ 中的电子系统。此时，外力为 $\mathbf{F} = -e\mathbf{E}$，分布函数不随时间变化（$\frac{\partial g}{\partial t}=0$），且体系均匀（$\nabla_{\mathbf{r}} g=0$）。线性化的 BTE 简化为：

$$
-e\mathbf{E} \cdot \mathbf{v}_{\mathbf{k}} \frac{\partial f_0}{\partial \epsilon} = -\frac{g}{\tau}
$$

解出[分布函数](@entry_id:145626)的偏离 $g = e\tau (\mathbf{E} \cdot \mathbf{v}_{\mathbf{k}}) (-\frac{\partial f_0}{\partial \epsilon})$。总的电流密度 $\mathbf{j}$ 是所有电子速度的加权平均（权重为[电荷](@entry_id:275494) $-e$ 和[分布函数](@entry_id:145626) $g$）：

$$
\mathbf{j} = \int 2 \frac{d^dk}{(2\pi)^d} (-e) \mathbf{v}_{\mathbf{k}} g(\mathbf{k}) = e^2 \int 2 \frac{d^dk}{(2\pi)^d} \tau (\mathbf{E} \cdot \mathbf{v}_{\mathbf{k}}) \mathbf{v}_{\mathbf{k}} \left(-\frac{\partial f_0}{\partial \epsilon}\right)
$$

其中因子 2 来自自旋简并，$d$ 是体系维度。这可以写成 $\mathbf{j} = \sigma \mathbf{E}$，其中[电导率张量](@entry_id:155827) $\sigma_{\alpha\beta}$ 为：

$$
\sigma_{\alpha\beta} = e^2 \int 2 \frac{d^dk}{(2\pi)^d} \tau v_{\alpha} v_{\beta} \left(-\frac{\partial f_0}{\partial \epsilon}\right)
$$

对于各向同性的三维系统，能带为抛物线型 $\epsilon = \frac{\hbar^2 k^2}{2m}$，在低温极限下 $(-\frac{\partial f_0}{\partial \epsilon}) \approx \delta(\epsilon - \epsilon_F)$，上式可以被求出，最终得到经典的**德鲁德 (Drude) 公式** $\sigma = \frac{ne^2\tau}{m}$，其中 $n$ 是电子密度。这表明 BTE 包含了早期唯象理论的结果。

BTE 的强大之处在于它可以处理更复杂的能带结构。例如，考虑一个二维材料，其色散关系为更一般的[幂律](@entry_id:143404)形式 $\epsilon(\mathbf{k}) = A |\mathbf{k}|^\alpha$ [@problem_id:83212]。通过在二维 $k$ 空间中进行积分，并利用[群速度](@entry_id:147686) $v = \frac{1}{\hbar}\frac{d\epsilon}{dk}$ 和[费米波矢](@entry_id:140713) $k_F$ 与[载流子浓度](@entry_id:143028) $n$ 的关系，我们可以推导出其[直流电导率](@entry_id:273370)。这一过程展示了如何将具体的[能带结构](@entry_id:139379)参数（如 $A$ 和 $\alpha$）与宏观可测量的电导率联系起来，超越了简单抛物线模型的限制。

**交流 (AC) 电导率**

当外[电场](@entry_id:194326)随时间谐振变化，$\mathbf{E}(t) = \text{Re}[\mathbf{E}_0 e^{-i\omega t}]$ 时，分布函数的偏离也会以相同频率[振荡](@entry_id:267781)，$g(\mathbf{k}, t) = \text{Re}[g_1(\mathbf{k}) e^{-i\omega t}]$。将此形式代入时变 BTE [@problem_id:83318]：

$$
\frac{\partial g}{\partial t} + \mathbf{v}_{\mathbf{k}} \cdot \mathbf{F} \frac{\partial f_0}{\partial \epsilon} = -\frac{g}{\tau} \quad \implies \quad -i\omega g_1 + \mathbf{v}_{\mathbf{k}} \cdot (-e\mathbf{E}_0) \frac{\partial f_0}{\partial \epsilon} = -\frac{g_1}{\tau}
$$

解出 $g_1$：
$$
g_1 = \frac{e\tau}{1 - i\omega\tau} (\mathbf{E}_0 \cdot \mathbf{v}_{\mathbf{k}}) \left(-\frac{\partial f_0}{\partial \epsilon}\right)
$$

与直流情况类似地计算电流密度，我们得到频率依赖的复数[电导率](@entry_id:137481) $\sigma(\omega) = \frac{\sigma_0}{1 - i\omega\tau}$，其中 $\sigma_0 = \frac{ne^2\tau}{m}$ 是[直流电导率](@entry_id:273370)。其实部，即耗散部分，为：

$$
\text{Re}[\sigma(\omega)] = \frac{\sigma_0}{1 + (\omega\tau)^2} = \frac{ne^2\tau/m}{1 + (\omega\tau)^2}
$$

这个结果被称为**德鲁德-洛伦兹 (Drude-Lorentz) 型**电导率。它描述了在低频时 ($\omega\tau \ll 1$) 电导率接近直流值，而在高频时 ($\omega\tau \gg 1$) [电导率](@entry_id:137481)随频率以 $\omega^{-2}$ 的形式衰减。这反映了电子的惯性：在高频[电场](@entry_id:194326)下，电子来不及在[电场](@entry_id:194326)反向前充分加速，导致电流响应减弱。

**复合[散射机制](@entry_id:136443)与[马西森定则](@entry_id:141203)**

在真实材料中，电子可能同时经历多种散射过程，例如与静态杂质的散射和与[声子](@entry_id:140728)的散射。如果这些散射过程是[相互独立](@entry_id:273670)的，那么总的[散射率](@entry_id:143589)就是各个散射率之和：

$$
\frac{1}{\tau_{\text{total}}(\epsilon)} = \sum_i \frac{1}{\tau_i(\epsilon)}
$$

这是一个基本的结论，被称为**[马西森定则](@entry_id:141203) (Matthiessen's Rule)**。它直观地意味着不同的散射渠道共同阻碍电子的运动。在弛豫时间不依赖于能量的简化情况下，总[电阻率](@entry_id:266481) $\rho_{\text{total}}$ 等于各分立电阻率 $\rho_i = m/(ne^2\tau_i)$ 之和。

然而，当不同[散射机制](@entry_id:136443)的弛豫时间具有不同的能量依赖性时，情况会变得更加复杂 [@problem_id:83184]。例如，考虑[杂质散射](@entry_id:267814)（$\tau_1 \propto \text{const}$）和简化的[声子散射](@entry_id:140674)（$\tau_2 \propto 1/\epsilon$）并存的情况。总的能量依赖[弛豫时间](@entry_id:191572)为 $\tau_{\text{total}}(\epsilon) = \frac{c_1 c_2}{c_2 + c_1\epsilon}$。为了计算电导率，需要对包含 $\tau_{\text{total}}(\epsilon)$ 的表达式进行[能量积分](@entry_id:166228)。在低温下，可利用**[索末菲展开](@entry_id:149655) (Sommerfeld expansion)** 来处理此积分，从而不仅能得到零温下的[电阻率](@entry_id:266481)，还能得到温度依赖的修正项（通常为 $T^2$ 项）。这揭示了[电阻率的温度依赖性](@entry_id:266964)源于费米面附近电子[分布](@entry_id:182848)的展宽以及[散射时间](@entry_id:272979)的能量依赖性的共同作用。

### [磁场](@entry_id:153296)中的输运

当施加[磁场](@entry_id:153296)时，洛伦兹力会使电子运动轨迹弯曲，从而产生一系列新的输运现象。

**霍尔效应**

考虑一个导体，电流 $j_x$ 沿 $x$ 方向流动，同时一个[磁场](@entry_id:153296) $\mathbf{B} = B_z \hat{z}$ 沿 $z$ 方向施加。洛伦兹力 $e(\mathbf{v} \times \mathbf{B})$ 会使电子向 $y$ 方向偏转。在开路边界条件下，[电荷](@entry_id:275494)会在样品侧面积累，形成一个横向的**霍尔[电场](@entry_id:194326)** $E_y$，这个[电场](@entry_id:194326)产生的[静电力](@entry_id:203379)会精确地平衡洛伦兹力，使得净的横向电流 $j_y$ 为零。[霍尔系数](@entry_id:145549) $R_H$ 定义为 $R_H = E_y / (j_x B_z)$。

通过求解包含洛伦兹力项的[稳态](@entry_id:182458) BTE，我们可以推导出[霍尔系数](@entry_id:145549)。一个非常重要的结果是，对于单能带模型，即使能带结构是各向异性的（例如，[有效质量](@entry_id:142879)是一个张量，$\epsilon(\mathbf{k}) = \frac{\hbar^2}{2} (\frac{k_x^2}{m_x} + \frac{k_y^2}{m_y} + \frac{k_z^2}{m_z})$），只要弛豫时间是各向同性的，最终得到的[霍尔系数](@entry_id:145549)仍然是 $R_H = -1/(ne)$ [@problem_id:83237]。这个结果令人惊讶，它表明霍尔效应在很大程度上不受能带细节的影响，而是直接测量了载流子的浓度 $n$ 和[电荷](@entry_id:275494)符号（负号表示电子）。这使其成为表征[半导体](@entry_id:141536)和金属中载流子性质的最基本和最强大的工具之一。

**[磁阻](@entry_id:260621)**

[磁阻](@entry_id:260621)是指材料电阻率随外[磁场](@entry_id:153296)变化的现象。根据[磁场](@entry_id:153296)和电流的相对方向，分为横向磁阻（$\mathbf{B} \perp \mathbf{j}$）和纵向[磁阻](@entry_id:260621)（$\mathbf{B} \parallel \mathbf{j}$）。

一个同样基础且重要的结果是，对于具有球形费米面（各向同性有效质量）和能量无关[弛豫时间](@entry_id:191572)的简单金属，**纵向磁阻为零** [@problem_id:83232]。这是因为当电场和磁场都沿 $z$ 方向时，洛伦兹力 $\mathbf{v} \times \mathbf{B}$ 位于 $xy$ 平面，对电子沿 $z$ 方向的加速度没有影响。因此，沿 $z$ 方向的电导率 $\sigma_{zz}$ 与[磁场](@entry_id:153296)无关。实验中观察到的非零纵向[磁阻](@entry_id:260621)，表明真实的金属要么具有复杂的、非球形的费米面，要么存在多能带输运，要么散射过程更为复杂。

### [温差电](@entry_id:142802)输运

[温差电效应](@entry_id:141235)研究的是电学和热学现象之间的耦合。当材料两端存在温差时，会产生电势差（[塞贝克效应](@entry_id:141489)）；反之，当电流通过不同材料的结时，会产生吸热或放热（帕尔帖效应）。

**塞贝克效应与[莫特公式](@entry_id:147321)**

**塞贝克系数** $S$ (也称[温差电动势](@entry_id:201717)) 定义为在零电流条件下（开路），由单位[温度梯度](@entry_id:136845) $(-\nabla T)$ 所感生的[电场](@entry_id:194326) $\mathbf{E}$，即 $\mathbf{E} = S(-\nabla T)$。物理上，热端的电子比冷端的电子具有更高的动能，这驱动了一个从热端到冷端的电子流。在开路条件下，电子在冷端堆积，形成一个反向的[电场](@entry_id:194326)，直到该[电场](@entry_id:194326)力与热扩散“力”平衡为止。

对于低温下的简并金属，[塞贝克系数](@entry_id:142873)可以用著名的**[莫特公式](@entry_id:147321) (Mott formula)** 精确描述：

$$
S = -\frac{\pi^2 k_B^2 T}{3e} \left[ \frac{d}{d\epsilon} \ln(\sigma(\epsilon)) \right]_{\epsilon=\epsilon_F}
$$

这里的 $\sigma(\epsilon) \propto D(\epsilon) v(\epsilon)^2 \tau(\epsilon)$ 是一个“能量依赖的电导率”，它正比于能量为 $\epsilon$ 的电子对总[电导](@entry_id:177131)的贡献，其中 $D(\epsilon)$ 是[态密度](@entry_id:147894)，$v(\epsilon)$ 是速率，$\tau(\epsilon)$ 是弛豫时间。[莫特公式](@entry_id:147321)的精髓在于，塞贝克效应的大小和符号取决于电导率函数在[费米能级](@entry_id:143215)处的[能量导数](@entry_id:170468)。换言之，它探测的是费米面附近电子输运性质的**不对称性**。如果 $\sigma(\epsilon)$ 在 $\epsilon_F$ 附近是对称的，则导数为零，塞贝克效应也为零。

这种不对称性的主要来源是[散射时间](@entry_id:272979) $\tau(\epsilon)$ 的能量依赖性。例如，对于由未屏蔽的离子化杂质主导的散射，理论预测 $\tau(\epsilon) \propto \epsilon^{3/2}$。将此依赖关系，以及[自由电子气](@entry_id:145649)的态密度 $D(\epsilon) \propto \epsilon^{1/2}$ 和速度平方 $v^2(\epsilon) \propto \epsilon$ 代入[莫特公式](@entry_id:147321)，可以计算出塞贝克系数 [@problem_id:83338]。这个例子清晰地展示了微观[散射机制](@entry_id:136443)如何直接决定宏观的[温差电](@entry_id:142802)响应。

**维德曼-弗朗茨定律及其破缺**

**维德曼-弗朗茨 (Wiedemann-Franz, WF) 定律**指出，金属的[电子热导率](@entry_id:262860) $\kappa$ 与[电导率](@entry_id:137481) $\sigma$ 之比正比于温度 $T$，其比例系数是一个普适常数，即洛伦兹数 $L = \frac{\kappa}{\sigma T} = L_0 = \frac{\pi^2}{3}(\frac{k_B}{e})^2$。这个定律是[费米液体理论](@entry_id:144069)的基石之一，它成立的条件是热流和电流由相同的弹性散射过程所弛豫。

然而，在某些条件下，此定律会显著破缺：

1.  **非[简并系统](@entry_id:203460)与能量依赖散射**：在[非简并半导体](@entry_id:203941)中，电子遵循[麦克斯韦-玻尔兹曼分布](@entry_id:144245)。若其弛豫时间具有能量依赖性，例如 $\tau(\epsilon) \propto \epsilon^p$，则通过求解BTE得到的[电导率](@entry_id:137481)和[热导率](@entry_id:147276)积分，可以证明洛伦兹数变为 $L = (p + \frac{5}{2})(\frac{k_B}{e})^2$ [@problem_id:83335]。这通常不等于 $L_0$，表明 WF 定律的普适性依赖于电子系统的[统计分布](@entry_id:182030)。

2.  **电子[流体力学](@entry_id:136788)**：在超纯净材料的特定温度区间，电子-电子 (e-e) 碰撞可能成为最主要的散射事件 ($\tau_{ee}$ 极短)，而使动量弛豫的杂质或[声子散射](@entry_id:140674)则弱得多 ($\tau_{imp} \gg \tau_{ee}$)。在这种**电子[流体力学](@entry_id:136788)**区域，WF 定律会被严重破坏 [@problem_id:83308]。其物理根源在于不同[守恒量](@entry_id:150267)的弛豫机制不同：
    *   **[电导](@entry_id:177131)**：电流与系统[总动量](@entry_id:173071)成正比。e-e 碰撞**守恒[总动量](@entry_id:173071)**，因此不能使电流弛豫。电流的弛豫由动量非守恒的杂质/[声子散射](@entry_id:140674)决定，故有效[弛豫时间](@entry_id:191572)为 $\tau_{charge} = \tau_{imp}$。
    *   **[热导](@entry_id:189019)**：热流不守恒。e-e 碰撞能高效地在电子间重新分配能量，从而剧烈地促使热流弛豫。因此，热流的弛豫由最快的 e-e 碰撞主导，$\tau_{heat} = \tau_{ee}$。
    将这两个不同的[弛豫时间](@entry_id:191572)代入各自的[电导](@entry_id:177131)和热导公式，最终得到的洛伦兹数为 $L = L_0 \frac{\tau_{ee}}{\tau_{imp}}$。由于 $\tau_{ee} \ll \tau_{imp}$，此时的洛伦兹数远小于标准值 $L_0$，标志着 WF 定律的强烈破坏，也揭示了电子系统进入了一种类似粘滞流体的集体行为模式。

### 屏蔽与集体行为

导体中的自由电子会对外部[电荷](@entry_id:275494)或[电势](@entry_id:267554)做出响应，重新排布自身以减弱（或**屏蔽**）该外部扰动在导体内部的影响。BTE 也可以用来描述这种集体行为。

考虑一个静态的、空间调制的微弱外部势场 $\phi_{\text{ext}}(\mathbf{r})$。它会在[电子气](@entry_id:140692)中产生一个总的自洽势场 $\phi(\mathbf{r})$，这个[势场](@entry_id:143025)反过来通过力 $\mathbf{F} = e\nabla\phi$ 驱动电子[分布函数](@entry_id:145626)偏离平衡，形成一个非均匀的[分布](@entry_id:182848)偏离 $g(\mathbf{r}, \mathbf{k})$。这个非均匀的电子[分布](@entry_id:182848)又会产生一个感生电荷密度 $\rho_{\text{ind}}(\mathbf{r})$。

利用线性化的静态 BTE，我们可以求解出由[势场](@entry_id:143025) $\phi(\mathbf{q})$（势场的傅里叶分量）引起的感生[电荷密度](@entry_id:144672) $\rho_{\text{ind}}(\mathbf{q})$ [@problem_id:83283]。这个感生电荷密度与总[势场](@entry_id:143025)之间的关系定义了材料的**介电函数** $\epsilon(\mathbf{q})$：

$$
\epsilon(\mathbf{q}) = 1 - \frac{\rho_{\text{ind}}(\mathbf{q})}{\epsilon_0 q^2 \phi(\mathbf{q})}
$$

在静态、长波（$q \to 0$）且无碰撞（$\tau \to \infty$）的极限下，对三维[自由电子气](@entry_id:145649)求解 BTE，可以得到介电函数的形式为：

$$
\epsilon(q) = 1 + \frac{q_{TF}^2}{q^2}
$$

这就是著名的**托马斯-费米 (Thomas-Fermi) 介电函数**。其中 $q_{TF}$ 被称为**[托马斯-费米屏蔽](@entry_id:145372)[波矢](@entry_id:178620)**，其平方为：

$$
q_{TF}^2 = \frac{3ne^2}{2\epsilon_0\epsilon_F}
$$

这个结果的物理意义是，一个点电荷在导体中产生的库仑势 $1/r$ 会被屏蔽为短程的[汤川势](@entry_id:139645) $e^{-q_{TF}r}/r$，其特征[屏蔽长度](@entry_id:143797)为 $1/q_{TF}$。这一分析将[输运理论](@entry_id:143989)与[静电屏蔽](@entry_id:192260)这一核心的[多体效应](@entry_id:173569)联系起来，展示了 BTE 在描述电子气集体响应方面的能力。