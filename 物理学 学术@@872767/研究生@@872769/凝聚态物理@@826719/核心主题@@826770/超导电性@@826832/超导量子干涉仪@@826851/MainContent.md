## 引言
超导量子干涉器件（SQUID）是利用宏观量子效应实现测量的杰出典范，被公认为当今最灵敏的磁通探测器。其无与伦比的灵敏度为从探测人脑微弱的神经活动到搜寻宇宙中的暗物质等众多前沿科学探索打开了大门。然而，要真正驾驭SQUID的力量，必须深刻理解其工作背后精妙的量子物理原理，并将这些原理与多样化的实际应用场景联系起来。本文旨在弥合理论与实践之间的鸿沟，为读者提供一个关于SQUID的全面视角。

我们将分三章展开论述。第一章“原理与机制”将深入剖析SQUID的核心——约瑟夫森结，并阐明[磁通量子化](@entry_id:142518)如何导致[量子干涉](@entry_id:139127)，这是SQUID超高灵敏度的根源。第二章“应用与跨学科连接”将展示SQUID如何作为一种强大的工具，在[生物磁学](@entry_id:260845)、[材料科学](@entry_id:152226)、[量子计算](@entry_id:142712)乃至宇宙学等多个领域中发挥关键作用。最后，在“动手实践”部分，我们将通过具体的计算问题，巩固和深化对SQUID工作原理的理解。

通过本次学习，您不仅将掌握SQUID的理论基础，还将领略其在推动现代科技发展中的巨大潜力，准备好深入探索这个迷人的量子世界。

## 原理与机制

继前一章对超导量子干涉器件（SQUID）的背景和应用的概述之后，本章将深入探讨其运行所依据的基本物理原理和核心机制。我们将从构成SQUID的基本单元——[约瑟夫森结](@entry_id:263150)开始，逐步构建一个完整的[直流SQUID](@entry_id:144361)模型。通过分析理想和非理想情况下的行为，我们将揭示量子干涉如何使SQUID成为现有技术中最灵敏的磁通探测器，并讨论在实际器件设计中必须面对的关键权衡。

### [约瑟夫森结](@entry_id:263150)：SQUID的核心

SQUID的核心是一个或多个**[约瑟夫森结](@entry_id:263150)**（[Josephson junction](@entry_id:144457)），它是一种由薄绝缘层或非超导金属隔开的两个[超导体](@entry_id:191025)组成的“弱连接”结构。[库珀对](@entry_id:143370)（Cooper pairs）能够通过[量子隧穿效应](@entry_id:149523)穿过这个势垒，从而在没有电压的情况下形成超导电流。这种独特的行为由两个基本的[约瑟夫森关系](@entry_id:275232)式描述。

#### [约瑟夫森关系](@entry_id:275232)

考虑两个由弱连接相连的[超导体](@entry_id:191025)，每个[超导体](@entry_id:191025)都由一个宏观复数[序参量](@entry_id:144819) $\psi_i = |\psi_i| e^{i\theta_i}$ 来描述，其中 $|\psi_i|$ 是凝聚体的振幅，$\theta_i$ 是其宏观[量子相位](@entry_id:197087)。[库珀对](@entry_id:143370)的[相干隧穿](@entry_id:197725)在两个超导凝聚体之间产生了一个相位依赖的耦合能。微观理论表明，该耦合能的形式为：

$U(\varphi) = -E_J \cos(\varphi)$

其中，$E_J$ 是**[约瑟夫森能量](@entry_id:140409)**，表征了结的[耦合强度](@entry_id:275517)；$\varphi$ 是跨结的**规范不变相位差**。这个能量-相位关系是[约瑟夫森效应](@entry_id:141683)的根源。

首先，我们可以推导出**直流[约瑟夫森关系](@entry_id:275232)**。流经结的超导电流 $I$ 与耦合能 $U(\varphi)$ 之间存在一个基本关系。由于电流的载流子是[电荷](@entry_id:275494)为 $q=2e$ 的[库珀对](@entry_id:143370)，电流（单位时间的[电荷](@entry_id:275494)流量）与[哈密顿量](@entry_id:172864)（在此为耦合能）对相位的一阶导数成正比：

$I = \frac{2e}{\hbar} \frac{\partial U}{\partial \varphi} = \frac{2e}{\hbar} \frac{\partial}{\partial \varphi}(-E_J \cos \varphi) = \frac{2eE_J}{\hbar} \sin \varphi$

这个关系通常写作：

$I = I_0 \sin\varphi$

其中，$I_0 = \frac{2eE_J}{\hbar}$ 被定义为结的**[临界电流](@entry_id:136685)**，代表了在零电压下结所能承载的最大超导电流。当外加电压为零时，相位差 $\varphi$ 是一个常数，结可以支持一个大小在 $-I_0$ 和 $+I_0$ 之间的直流超导电流。这就是**[直流约瑟夫森效应](@entry_id:141944)**。[@problem_id:3017992]

其次，当在结两端施加一个非零的直流电压 $V$ 时，两侧库珀对的能量会产生一个 $2eV$ 的差异。根据薛定谔方程，一个能量为 $E$ 的[量子态](@entry_id:146142)的相位演化速率为 $\dot{\theta} = -E/\hbar$。因此，跨结的相位差 $\varphi$ 的[时间演化](@entry_id:153943)速率为：

$\dot{\varphi} = \dot{\theta}_2 - \dot{\theta}_1 = \frac{2e(V_1 - V_2)}{\hbar}$

习惯上，我们定义跨结的电压为 $V \equiv V_1 - V_2$，这便引出了**交流[约瑟夫森关系](@entry_id:275232)**：

$\frac{d\varphi}{dt} = \frac{2e}{\hbar} V$

这个关系式表明，一个恒定的直流电压 $V$ 会导致相位差随时间线性演化，$\varphi(t) = \varphi(0) + (2eV/\hbar)t$。将此代入直流[约瑟夫森关系](@entry_id:275232)，超导电流变为一个交流电：

$I(t) = I_0 \sin\left(\varphi(0) + \frac{2eV}{\hbar}t\right)$

该电流以**[约瑟夫森频率](@entry_id:158971)** $f_J = 2eV/h$ [振荡](@entry_id:267781)。更严格地，交流关系式的规范不变形式应写作 $\dot{\varphi} = (2e/\hbar) \int_{\mathcal{C}} \mathbf{E} \cdot d\boldsymbol{\ell}$，其中积分路径跨越势垒。当[电场](@entry_id:194326) $\mathbf{E}$ 局域在结内时，该积分就简化为电压降 $V$。[@problem_id:3017992]

这两个关系式构成了理解所有SQUID器件行为的基础。例如，考虑一个由理想交流[电流源](@entry_id:275668) $I(t) = I_a \sin(\omega t)$ 驱动的单个约瑟夫森结，其中电流幅度 $I_a$ 小于[临界电流](@entry_id:136685) $I_c$。在这种情况下，结始终处于超导状态，因此通过结的超导电流 $I_s$ 必须等于驱动电流，即 $I_c \sin(\delta(t)) = I_a \sin(\omega t)$。我们可以求解相位 $\delta(t)$，然后利用交流[约瑟夫森关系](@entry_id:275232) $V = (\hbar/2e) d\delta/dt$ 来计算结上的电压。通过计算可以发现，电压的最大幅值为 $|V|_{max} = \frac{\hbar\omega}{2e} \frac{I_a}{I_c}$。这个例子清晰地展示了在动态驱动下，电流、相位和电压之间紧密的相互联系。[@problem_id:1806340]

#### 结的动力学与[磁滞](@entry_id:145766)

实际的约瑟夫森结不仅具有超导电流通道，还存在固有的电容 $C$ 和一个等效的正常电阻 $R$。为了获得稳定的、非[磁滞](@entry_id:145766)的电压-电流特性，通常会在结上并联一个**分流电阻**（shunt resistor）$R_{\text{sh}}$。此时，结的行为可以用**阻性电容分流结（RCSJ）模型**来描述。总电流 $I$ 分为三个部分：超导电流、流过电阻的正常电流和流过电容的位移电流。结合交流[约瑟夫森关系](@entry_id:275232)，我们可以得到描述[相位动力学](@entry_id:274204)的方程：

$I = I_c \sin\varphi + \frac{\hbar}{2eR} \frac{d\varphi}{dt} + \frac{\hbar C}{2e} \frac{d^2\varphi}{dt^2}$

这个方程在形式上与一个受驱动的、有阻尼的摆的[运动方程](@entry_id:170720)相同。其动力学行为由一个无量纲的**斯图尔特-麦克म्बर参数**（Stewart-McCumber parameter）$\beta_c$ 决定：

$\beta_c = \frac{2e I_c R^2 C}{\hbar}$

这个参数衡量了系统的阻尼程度。当 $\beta_c > 1$ 时，系统是**欠阻尼**的，其电流-电压（$I-V$）特性会表现出**[磁滞](@entry_id:145766)**（hysteresis）：当[偏置电流](@entry_id:260952)从零增加并超过 $I_c$ 时，结会突然切换到一个有限电压状态；但当电流减小时，它会沿着另一条路径返回到零电压状态。相反，当 $\beta_c \le 1$ 时，系统是**[过阻尼](@entry_id:167953)**或**[临界阻尼](@entry_id:155459)**的，其$I-V$曲线是单值的、非[磁滞](@entry_id:145766)的。

对于大多数SQUID应用，[磁滞](@entry_id:145766)行为是不希望出现的，因为它会导致不明确的电压响应。因此，通过并联一个足够小的分流电阻 $R_{\text{sh}}$ 来确保 $\beta_c \le 1$ 是SQUID设计的标准做法。[@problem_id:3018039]

### [直流SQUID](@entry_id:144361)：环路中的量子干涉

SQUID有两种主要类型：**直流（DC）SQUID**和**射频（RF）SQUID**。它们在结构上的一个关键区别在于[约瑟夫森结](@entry_id:263150)的数量：[直流SQUID](@entry_id:144361)由一个包含**两个**约瑟夫森结的[超导环](@entry_id:142979)构成，而射频SQUID则包含一个只有一个结的环路。[@problem_id:1806317] 本章将重点讨论[直流SQUID](@entry_id:144361)。

#### [磁通量子化](@entry_id:142518)与相位约束

[直流SQUID](@entry_id:144361)的核心物理机制源于[超导环](@entry_id:142979)路中的**[磁通量子化](@entry_id:142518)**（fluxoid quantization）。由于超导[宏观波函数](@entry_id:143853)必须是单值的，沿着[环路积分](@entry_id:164828)一周，总的相位变化必须是 $2\pi$ 的整数倍。这个条件对穿过环路的总磁通量 $\Phi_{\text{tot}}$ 施加了严格的约束。

考虑一个包含两个结的环路。当我们在环路内沿着一个闭合路径积分时，相位变化包括了通过两个结的规范不变相位降 $\varphi_1$ 和 $\varphi_2$，以及由[磁矢量势](@entry_id:141246) $\mathbf{A}$ 贡献的[Aharonov-Bohm相位](@entry_id:158689)项。[单值性](@entry_id:174849)条件最终导致了以下关键的相位约束关系：

$\varphi_1 - \varphi_2 = 2\pi n - \frac{2\pi}{\Phi_0} \Phi_{\text{tot}}$

其中 $n$ 是一个整数，$\Phi_0 = h/(2e)$ 是**[磁通量子](@entry_id:136429)**。由于[约瑟夫森关系](@entry_id:275232)对于相位具有 $2\pi$ 的周期性，整数项 $2\pi n$ 可以被吸收到相位的定义中。因此，环路施加的核心约束是：

$\varphi_1 - \varphi_2 = - \frac{2\pi \Phi_{\text{tot}}}{\Phi_0} \pmod{2\pi}$

这个等式表明，穿过SQUID环路的总[磁通量](@entry_id:268943) $\Phi_{\text{tot}}$ 直接决定了两个结的相位差。正是这个关系将磁通输入与结的电学行为联系起来，并导致了量子干涉现象。[@problem_id:3018030]

#### [临界电流](@entry_id:136685)的调制（理想情况）

为了清晰地揭示干涉效应，我们首先考虑一个理想的对称[直流SQUID](@entry_id:144361)，其环路[电感](@entry_id:276031)可以忽略不计（$L \approx 0$），并且两个结的[临界电流](@entry_id:136685)相同，均为 $I_0$。在忽略[电感](@entry_id:276031)的情况下，环路中没有屏蔽电流，因此总[磁通](@entry_id:191239) $\Phi_{\text{tot}}$ 就等于外部施加的磁通 $\Phi_{\text{ext}}$。

通过SQUID的总超导电流 $I$ 是流过两个结的电流之和：

$I = I_1 + I_2 = I_0 \sin\varphi_1 + I_0 \sin\varphi_2$

利用三角和差化积公式，上式可以改写为：

$I = 2 I_0 \sin\left(\frac{\varphi_1+\varphi_2}{2}\right) \cos\left(\frac{\varphi_1-\varphi_2}{2}\right)$

现在，我们将[磁通量子化](@entry_id:142518)施加的相位约束 $\varphi_1 - \varphi_2 = -2\pi\Phi_{\text{ext}}/\Phi_0$ 代入上式：

$I = 2 I_0 \sin\left(\frac{\varphi_1+\varphi_2}{2}\right) \cos\left(\frac{-\pi\Phi_{\text{ext}}}{\Phi_0}\right) = 2 I_0 \sin\left(\frac{\varphi_1+\varphi_2}{2}\right) \cos\left(\frac{\pi\Phi_{\text{ext}}}{\Phi_0}\right)$

SQUID的[临界电流](@entry_id:136685) $I_c(\Phi_{\text{ext}})$ 定义为在给定外部磁通 $\Phi_{\text{ext}}$ 时，器件所能承载的最大超导电流。为了找到这个最大值，我们需要最大化上式。相位和 $\varphi_1+\varphi_2$ 是一个可自由调整的参数，以承载最大的电流。因此，我们可以让 $\sin((\varphi_1+\varphi_2)/2)$ 取其最大值1。由此，我们得到了SQUID[临界电流](@entry_id:136685)对外部[磁通](@entry_id:191239)的依赖关系：[@problem_id:3018086]

$I_c(\Phi_{\text{ext}}) = 2 I_0 \left|\cos\left(\frac{\pi\Phi_{\text{ext}}}{\Phi_0}\right)\right|$

这个结果是[直流SQUID](@entry_id:144361)工作的核心。它表明，SQUID的总[临界电流](@entry_id:136685)随外部磁通呈周期性变化，周期为**一个[磁通量子](@entry_id:136429) $\Phi_0$**。当外部[磁通](@entry_id:191239)是 $\Phi_0$ 的整数倍（$\Phi_{\text{ext}} = n\Phi_0$）时，[临界电流](@entry_id:136685)达到最大值 $2I_0$，这对应于两路电流的**相长干涉**。当外部[磁通](@entry_id:191239)是 $\Phi_0$ 的半整数倍（$\Phi_{\text{ext}} = (n+1/2)\Phi_0$）时，[临界电流](@entry_id:136685)降为零，对应于**[相消干涉](@entry_id:170966)**。[@problem_id:3018030]

这种[临界电流](@entry_id:136685)的调制效应是SQUID作为[磁通](@entry_id:191239)计的基础。例如，如果用一个恒定的[偏置电流](@entry_id:260952) $I_{\text{bias}}$ 来驱动SQUID，当 $I_{\text{bias}} > I_c(\Phi_{\text{ext}})$ 时，SQUID将从零电压的超导态切换到有电压的电阻态。考虑一个[偏置电流](@entry_id:260952)为 $I_{\text{bias}} = \frac{3}{2} I_c$ 的SQUID（其中$I_c$是单个结的[临界电流](@entry_id:136685)，即$2I_0$中的$I_0$）。SQUID保持超导态的条件是 $|I_{\text{bias}}| \le I_c(\Phi_{\text{ext}})$，即 $\frac{3}{2} I_c \le 2 I_c |\cos(\pi \Phi_{\text{ext}}/\Phi_0)|$，化简为 $|\cos(\pi \Phi_{\text{ext}}/\Phi_0)| \ge \frac{3}{4}$。在一个磁通量子周期内（从 $\Phi_{\text{ext}}=0$到$\Phi_0$），满足此条件的[磁通](@entry_id:191239)范围所占的比例为 $\frac{2 \arccos(3/4)}{\pi}$。这表明，通过监测SQUID的电压状态，我们可以精确地推断出穿过环路的[磁通](@entry_id:191239)变化。[@problem_id:1806316]

### SQUID的工作原理与性能指标

#### 从[临界电流](@entry_id:136685)到电压：传输函数

在实际操作中，通常将SQUID偏置在一个恒定的直流电流 $I_{\text{bias}}$ 下，该电流略大于其最大[临界电流](@entry_id:136685) $2I_0$。在这种**电压读出模式**下，$I_c(\Phi_{\text{ext}})$ 的周期性调制会转化为一个周期性的输出电压 $V(\Phi_{\text{ext}})$。这个电压信号通常呈近似三角形或锯齿形，周期同样为 $\Phi_0$。

SQUID作为[磁通](@entry_id:191239)计的灵敏度，由其**传输函数** $V_{\Phi}$ 来量化，定义为输出电压对输入磁通的变化率：

$V_{\Phi} = \frac{dV}{d\Phi_{\text{ext}}}$

为了达到最高的磁通探测灵敏度，SQUID必须被偏置在一个特定的[磁通](@entry_id:191239)点上，使得传输函数的[绝对值](@entry_id:147688) $|V_{\Phi}|$ 最大。这个点通常位于 $V-\Phi$ 曲线斜率最陡峭的位置，对应于 $\Phi_{\text{ext}} \approx (n \pm 1/4)\Phi_0$。为了直观理解，我们可以考虑一个简化的电压-磁通关系模型 $V(\Phi_{\text{ext}}) = V_{\text{amp}} \cos(2\pi \Phi_{\text{ext}}/\Phi_0)$。其传输函数为 $V_{\Phi} = -V_{\text{amp}} \frac{2\pi}{\Phi_0} \sin(2\pi \Phi_{\text{ext}}/\Phi_0)$。其最大幅值为 $|V_{\Phi}|_{\text{max}} = \frac{2\pi V_{\text{amp}}}{\Phi_0}$，出现在 $\sin$ 函数等于 $\pm 1$ 的点。对于一个具有 $V_{\text{amp}} = 47.5 \ \mu\text{V}$ 的SQUID，利用 $\Phi_0 = 2.068 \times 10^{-15} \ \text{Wb}$，其最大传输函数可达约 $1.44 \times 10^{11} \ \text{V/Wb}$，或 $1.44 \times 10^5 \ \text{MV/Wb}$。这个巨大的数值凸显了SQUID将微弱磁通变化转换为可测量电压信号的卓越能力。[@problem_id:1806312]

#### 环路[电感](@entry_id:276031)的作用：屏蔽参数

前面我们忽略了环路电感 $L$ 的影响。在实际器件中，[电感](@entry_id:276031)是不可避免的，它会引入**屏蔽效应**（screening effect）。环路中流动的电流 $I_{\text{circ}}$ 会产生一个自身磁通 $L I_{\text{circ}}$，它会反向作用于外部磁通。此时，总[磁通](@entry_id:191239)为 $\Phi_{\text{tot}} = \Phi_{\text{ext}} + L I_{\text{circ}}$。

这个效应的强度由一个无量纲的**屏蔽参数** $\beta_L$ 来表征：

$\beta_L = \frac{2 L I_0}{\Phi_0}$

该参数比较了SQUID能产生的最大屏蔽磁通（正比于 $L I_0$）与[磁通量子](@entry_id:136429) $\Phi_0$ 的大小。[@problem_id:3017988]

当 $\beta_L \ll 1$ 时，电感效应很弱，SQUID的行为接近于理想情况，[临界电流](@entry_id:136685)调制深度接近 $2I_0$。然而，随着 $\beta_L$ 的增加，屏蔽效应变得显著。SQUID会通过产生一个反向的屏蔽电流来抵消部分外部[磁通](@entry_id:191239)的变化，试图将环内的总[磁通](@entry_id:191239) $\Phi_{\text{tot}}$ 维持在一个恒定值。这导致 $I_c(\Phi_{\text{ext}})$ 的调制深度减小，即 $I_{c, \text{max}}$ 减小，$I_{c, \text{min}}$ 增加，从而降低了SQUID的响应。

更重要的是，当 $\beta_L$ 超过一个临界值（$\beta_L > 2/\pi \approx 0.64$）时，$\Phi_{\text{tot}}$ 与 $\Phi_{\text{ext}}$ 之间的关系将不再是单调的。这意味着对于某个给定的外部[磁通](@entry_id:191239) $\Phi_{\text{ext}}$，可能存在多个稳定的内部磁通状态 $\Phi_{\text{tot}}$。这种**[多稳态](@entry_id:180390)**（multistability）现象会导致SQUID的[磁通](@entry_id:191239)响应出现[磁滞](@entry_id:145766)，这对于需要线性响应的应用是不利的。因此，在SQUID设计中，通常要求 $\beta_L \lesssim 1$。[@problem_id:3017988]

#### 噪声与设计权衡

SQUID的最终灵敏度受到噪声的限制。一个主要的噪声来源就是之前提到的用于消除[磁滞](@entry_id:145766)的分流电阻 $R_{\text{sh}}$。这些电阻在有限温度 $T$ 下会产生**约翰逊-奈奎斯特[热噪声](@entry_id:139193)**（Johnson-Nyquist thermal noise）。

分流电阻的作用是双重的，这带来了一个关键的设计权衡：
1.  **抑制[磁滞](@entry_id:145766)**：为了获得非[磁滞](@entry_id:145766)的 $I-V$ 特性，需要选择足够小的 $R_{\text{sh}}$ 以确保斯图尔特-麦克म्बर参数 $\beta_c = 2e I_c R_{\text{sh}}^2 C/\hbar \le 1$。
2.  **引入噪声**：另一方面，每个电阻都会产生一个与其并联的、谱密度为 $S_I = 4k_B T/R_{\text{sh}}$ 的[热噪声](@entry_id:139193)电流。这个噪声电流会注入SQUID环路，产生[磁通](@entry_id:191239)噪声，从而直接降低器件的灵敏度。

从噪声公式可以看出，为了减小电流噪声，我们希望 $R_{\text{sh}}$ 越大越好。但这与抑制[磁滞](@entry_id:145766)的要求相矛盾。因此，SQUID的设计必须在这两者之间进行权衡。[最优策略](@entry_id:138495)是选择**在保证 $\beta_c \le 1$ 的前提下，尽可能大的分流电阻 $R_{\text{sh}}$**。

让我们通过一个具体的例子来说明。考虑一个工作在 $T=4.2\,\text{K}$ 的SQUID，其结参数为 $I_c = 5\,\mu\text{A}$ 和 $C = 100\,\text{fF}$。我们评估三个候选分流电阻：$R_{\text{sh}} \in \{2\,\Omega, 10\,\Omega, 50\,\Omega\}$。
- 计算可得，对于 $R_{\text{sh}} = 50\,\Omega$，$\beta_c \approx 3.80 > 1$，器件是[磁滞](@entry_id:145766)的。
- 对于 $R_{\text{sh}} = 10\,\Omega$，$\beta_c \approx 0.15  1$，非[磁滞](@entry_id:145766)。
- 对于 $R_{\text{sh}} = 2\,\Omega$，$\beta_c \approx 0.006  1$，非[磁滞](@entry_id:145766)。

在两个非[磁滞](@entry_id:145766)的选项中，$R_{\text{sh}} = 10\,\Omega$ 的电阻值更大，因此其产生的约翰逊电流噪声更低（具体来说，$S_I(2\,\Omega) = 5 \times S_I(10\,\Omega)$）。因此，对于这个特定的SQUID，$R_{\text{sh}} = 10\,\Omega$ 是实现无[磁滞](@entry_id:145766)操作和最小化热噪声之间的最佳折衷。[@problem_id:3018039] 这个例子完美地诠释了在设计高性能SQUID时，必须仔细考虑[量子动力学](@entry_id:138183)、电磁学和[热力学](@entry_id:141121)之间的相互作用。