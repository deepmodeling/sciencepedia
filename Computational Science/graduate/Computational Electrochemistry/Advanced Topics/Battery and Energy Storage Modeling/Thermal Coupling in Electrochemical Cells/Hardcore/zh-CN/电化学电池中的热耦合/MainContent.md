## 引言
在现代能源存储技术中，电化学电池扮演着核心角色。然而，其性能、寿命和安全性都与一个关键的物理现象紧密相连——热效应。电池在运行过程中，电化学反应和电荷输运不可避免地伴随着热量的产生和转移，而温度的变化又反过来深刻地影响着电化学过程的速率和效率。这种复杂的双向作用，即热-电[化学耦合](@entry_id:138976)，是理解和优化电池系统的基础。忽视这种耦合不仅会导致性能预测的偏差，更可能引发灾难性的热失控事故。

本文旨在系统性地剖析电化学电池中的[热耦合](@entry_id:1132992)问题，填补基础理论与工程应用之间的知识鸿沟。我们将从最基本的物理化学原理出发，逐步构建一个全面的多物理场模型。通过阅读本文，您将深入理解电池内部热量的“前世今生”，掌握分析和预测电池热行为的核心工具。

文章将分为三个核心章节展开：第一章“原理与机制”，将详细阐述热量的来源（欧姆热、反应热、熵热），并建立描述热量产生与传递的数学模型，最终整合为完整的热-电[化学耦合](@entry_id:138976)方程组。第二章“应用与跨学科联系”，将展示这些原理如何应用于解决[电池热管理](@entry_id:148783)、安全评估、老化预测和状态诊断等实际工程问题，并探讨其与力学等其他学科的交叉。最后，第三章“动手实践”，将通过一系列计算练习，帮助您将理论知识转化为解决具体问题的实践能力。让我们首先进入第一章，探索[热耦合](@entry_id:1132992)现象背后的基本原理与机制。

## 原理与机制

在电化学电池的运行过程中，电能、化学能和热能之间发生着复杂的转换。理解这些[能量转换](@entry_id:165656)的原理及其相互耦合的机制，对于电池的设计、[性能优化](@entry_id:753341)和安全管理至关重要。本章将系统地阐述电化学电池内部热量产生的基本原理，并深入探讨温度如何反过来影响电化学过程，最终构建一个完整的热-电[化学耦合](@entry_id:138976)模型。

### 宏观热方程：均质化方法

在宏观尺度上，电化学电池（或其任何组成部分，如多孔电极）的温度分布 $T(\mathbf{x}, t)$ 可以通过求解一个[热传导方程](@entry_id:194763)来描述。该方程是能量守恒定律的数学表达，其一般形式为：

$$
\rho c_p \frac{\partial T}{\partial t} = \nabla \cdot (k \nabla T) + \dot{q}
$$

其中，$\rho$ 是材料的密度，$c_p$ 是比热容，$k$ 是[热导](@entry_id:189019)率。等式左边代表单位体积内热能随时间的变化率（蓄热项），等式右边第一项代表通过[热传导](@entry_id:143509)进出该体积的[净热通量](@entry_id:155652)（传导项），而 $\dot{q}$ 则是单位体积的 volumetric heat source（[体积热源](@entry_id:1133894)项），代表在内部产生的热量。

对于像电池电极这样的多孔复合材料，它由固相活性物质/导电剂（固相）和充满[电解质](@entry_id:261072)的孔隙（液相）组成，直接使用单一相的物性参数（$\rho, c_p, k$）是不合适的。我们需要采用**均质化 (homogenization)** 的方法，将微观上非均匀的复合材料处理为宏观上均匀的等效介质。这意味着方程中的物性参数都是**有效属性 (effective properties)**。

基于代表性单元体积 (Representative Elementary Volume, REV) 的[体积平均](@entry_id:1133895)法，我们可以定义这些有效属性 。假设固相的[体积分数](@entry_id:756566)为 $1-\varepsilon$，其物性为 $\rho_s, c_{p,s}, k_s$；[电解质](@entry_id:261072)相的孔隙率为 $\varepsilon$，其物性为 $\rho_e, c_{p,e}, k_e$。在两相达到**局部热平衡 (Local Thermal Equilibrium, LTE)** 的假设下（即在REV尺度上，固相和液相具有相同的温度 $T$），有效物性可以表示为：

- **有效密度 ($\rho^{\mathrm{eff}}$)**：为各相密度的[体积分数](@entry_id:756566)加权平均。
$$
\rho^{\mathrm{eff}} = (1-\varepsilon)\rho_s + \varepsilon\rho_e
$$

- **有效比热容 ($c_p^{\mathrm{eff}}$)**：为各相比热容的质量分数加权平均。这确保了有效体积热容 $(\rho c_p)^{\mathrm{eff}}$ 是各相体积热容的简单加权平均。
$$
(\rho c_p)^{\mathrm{eff}} = \rho^{\mathrm{eff}} c_p^{\mathrm{eff}} = (1-\varepsilon)\rho_s c_{p,s} + \varepsilon\rho_e c_{p,e}
$$
因此，
$$
c_p^{\mathrm{eff}} = \frac{(1-\varepsilon)\rho_s c_{p,s} + \varepsilon\rho_e c_{p,e}}{(1-\varepsilon)\rho_s + \varepsilon\rho_e}
$$

- **[有效热导率](@entry_id:152265) ($k^{\mathrm{eff}}$)**：其定义依赖于[多孔介质](@entry_id:154591)的微观结构。对于典型的电极结构，固相和液相通常形成相互贯通的网络（双连续相）。在这种情况下，可以近似认为热流在两相中并行传导，因此有效热导率是各相[热导](@entry_id:189019)率的[算术平均值](@entry_id:165355)（也称为Voigt上界）。
$$
k^{\mathrm{eff}} = (1-\varepsilon)k_s + \varepsilon k_e
$$
需要注意的是，对于其他微观结构，例如一个相作为分散颗粒分布在另一个连续相中，可能需要使用更复杂的模型，如Maxwell–Eucken模型或[谐波](@entry_id:181533)平均（串联模型）。

- **有效热源 ($\dot{q}^{\mathrm{eff}}$)**：同样，总的体积热源也是各相热源的体积加权平均。
$$
\dot{q}^{\mathrm{eff}} = (1-\varepsilon)\dot{q}_s + \varepsilon\dot{q}_e
$$

在建立了宏观[热方程](@entry_id:144435)的框架后，核心挑战转变为精确地识别和量化[体积热源](@entry_id:1133894)项 $\dot{q}$ 的各个物理来源。

### 电化学系统中的热源

电化学电池中的热量产生是一个复杂的过程，它源于电荷和物质传输的不可逆性以及电化学反应本身的[热力学](@entry_id:172368)特性。在[多孔电极理论](@entry_id:148271)中，总体积热源 $\dot{q}$ 通常被分解为四个主要部分：固相中的欧姆热、[电解质](@entry_id:261072)中的欧姆热、不可逆的[反应热](@entry_id:140993)和可逆的[反应热](@entry_id:140993) 。

$$
\dot{q} = \dot{q}_{\mathrm{ohm,s}} + \dot{q}_{\mathrm{ohm,l}} + \dot{q}_{\mathrm{irr,rxn}} + \dot{q}_{\mathrm{rev,rxn}}
$$

#### 欧姆热

**欧姆热 (Ohmic Heating)**，或称焦尔热，是由于电荷载流子（电子和离子）在具有电阻的介质中移动时，克服阻力做功而产生的不可逆热量。根据焦尔定律，其功率密度为电流密度与电场的点积，$\mathbf{J} \cdot \mathbf{E}$。

在多孔电极的两相模型中，欧姆热需要分别计算固相（电子导体）和液相（离子导体）的贡献 。

- **固相欧姆热 ($\dot{q}_{\mathrm{ohm,s}}$)**：电子在固相基体中流动产生的热量。设固相电势为 $\phi_s$，有效电导率为 $\sigma^{\mathrm{eff}}$，[宏观电流](@entry_id:203974)密度为 $\mathbf{i}_s$。根据欧姆定律，$\mathbf{i}_s = -\sigma^{\mathrm{eff}} \nabla \phi_s$。产生的热量为：
$$
\dot{q}_{\mathrm{ohm,s}} = \mathbf{i}_s \cdot (-\nabla \phi_s) = (-\sigma^{\mathrm{eff}} \nabla \phi_s) \cdot (-\nabla \phi_s) = \sigma^{\mathrm{eff}} |\nabla \phi_s|^2 = \frac{|\mathbf{i}_s|^2}{\sigma^{\mathrm{eff}}}
$$

- **[电解质](@entry_id:261072)相欧姆热 ($\dot{q}_{\mathrm{ohm,l}}$)**：离子在[电解质](@entry_id:261072)中迁移产生的热量。设液相电势为 $\phi_l$，有效离子电导率为 $\kappa^{\mathrm{eff}}$，[宏观电流](@entry_id:203974)密度为 $\mathbf{i}_l$。在忽略浓度梯度影响的简化情况下，$\mathbf{i}_l = -\kappa^{\mathrm{eff}} \nabla \phi_l$。产生的热量为：
$$
\dot{q}_{\mathrm{ohm,l}} = \mathbf{i}_l \cdot (-\nabla \phi_l) = \kappa^{\mathrm{eff}} |\nabla \phi_l|^2 = \frac{|\mathbf{i}_l|^2}{\kappa^{\mathrm{eff}}}
$$

由于电导率和平方项总是非负的，欧姆热永远是一个**产热项**（$\ge 0$），体现了其不可逆的耗散本质。

#### [反应热](@entry_id:140993)

**反应热 (Reaction Heat)** 是指在电极/[电解质](@entry_id:261072)界面上发生电化学反应时伴随的热效应。这部分热量可以进一步分解为不可逆和可逆两个部分。

**[不可逆反应](@entry_id:1126748)热 ($\dot{q}_{\mathrm{irr,rxn}}$)**

为了使电化学反应以一定的速率（即电流）发生，需要施加一个超出其平衡电势的驱动力，这个驱动力就是**过电势 (overpotential)**，记为 $\eta$。过电势的存在意味着一部分电能没有被用于化学能的转换，而是以热的形式耗散掉了。这部分热量就是[不可逆反应](@entry_id:1126748)热。

其大小等于过电势与反应电流的乘积。在多孔电极中，我们需要考虑单位体积内的总反应，因此表达式为：
$$
\dot{q}_{\mathrm{irr,rxn}} = a_s j \eta
$$
这里，$a_s$ 是单位体积内的比表面积（即反应界面的面积），$j$ 是界面上的电流密度（也称孔壁通量）。过电势 $\eta$ 定义为电极电势差 $(\phi_s - \phi_l)$ 与平衡电势 $U$ 的偏离：$\eta = \phi_s - \phi_l - U$。由于驱动反应的过电势 $\eta$ 和由此产生的电流 $j$ 始终同号，因此[不可逆反应](@entry_id:1126748)热也永远是一个**产热项**（$\ge 0$）。

**[可逆反应](@entry_id:202665)热 ($\dot{q}_{\mathrm{rev,rxn}}$)**

与不可逆耗散不同，**[可逆反应](@entry_id:202665)热 (Reversible Reaction Heat)**，也称**熵热 (Entropic Heat)**，源于反应物和产物之间熵值的差异。根据[热力学](@entry_id:172368)第二定律，在恒温恒压下的[可逆过程](@entry_id:276625)中，系统交换的热量等于[温度与熵](@entry_id:755836)变的乘积 ($Q_{\mathrm{rev}} = T \Delta S$)。

我们可以通过Gibbs-Helmholtz关系式将[熵变](@entry_id:138294) $\Delta S$ 与电化学测量值联系起来 。对于一个电化学反应，其[吉布斯自由能变](@entry_id:138324) $\Delta G$ 与平衡电势（或开路电压 $E_{\mathrm{oc}}$）的关系为 $\Delta G = -nFE_{\mathrm{oc}}$。而 $\Delta G$ 与 $\Delta S$ 的关系为 $(\partial \Delta G / \partial T)_p = -\Delta S$。联立这两个方程，可得：
$$
\Delta S = -\left( \frac{\partial (-nFE_{\mathrm{oc}})}{\partial T} \right)_p = nF \frac{\partial E_{\mathrm{oc}}}{\partial T}
$$
这里的 $\partial E_{\mathrm{oc}} / \partial T$ 被称为平衡电势的**温度系数**。

单位体积内的可逆热生成速率，就是单位体积内的[反应速率](@entry_id:185114)（$a_s j / (nF)$）乘以每个反应所对应的热量 $T \Delta S$：
$$
\dot{q}_{\mathrm{rev,rxn}} = \frac{a_s j}{nF} \cdot (T \Delta S) = \frac{a_s j}{nF} \cdot \left( T nF \frac{\partial U}{\partial T} \right) = a_s j T \frac{\partial U}{\partial T}
$$
（在多孔电极中，我们用局部平衡电势 $U$ 代替电池的开路电压 $E_{\mathrm{oc}}$）。

与欧姆热和[不可逆反应](@entry_id:1126748)热不同，[可逆反应](@entry_id:202665)热的符号取决于电流方向（$j$ 的符号）和反应的熵变特性（$\partial U / \partial T$ 的符号）。
- 如果 $\partial U / \partial T > 0$，则反应[熵增](@entry_id:138799)。在放电时（$j>0$，[自发反应](@entry_id:140874)），系统会**释放热量**（放热，exothermic）。充电时（$j0$）则会吸收热量（吸热，endothermic），起到冷却效果。
- 如果 $\partial U / \partial T  0$，则反应熵减。在放电时（$j>0$），系统会**吸收热量**（吸热，endothermic）。

因此，可逆热项是唯一可能为负的热源项，它在某些条件下（如低温、低倍率充电）可能导致电池的冷却现象。

### 温度与[电化学动力学](@entry_id:263644)的耦合

我们已经看到，电化学过程如何产生热量。反过来，温度的变化也会显著影响电化学反应的速率，从而形成一个紧密的**热-电[化学耦合](@entry_id:138976)**。这种耦合主要通过影响电化学反应动力学来实现，而反应动力学通常由**[Butler-Volmer方程](@entry_id:150187)**描述 。

Butler-Volmer方程给出了界面电流密度 $j$ 与过电势 $\eta$ 的关系：
$$
j = j_0(T) \left[ \exp\left(\frac{\alpha_a F \eta}{RT}\right) - \exp\left(-\frac{\alpha_c F \eta}{RT}\right) \right]
$$
其中，$\alpha_a$ 和 $\alpha_c$ 是[阳极和阴极](@entry_id:262146)的电荷[传递系数](@entry_id:264443)，$F$ 是[法拉第常数](@entry_id:262496)，$R$ 是[通用气体常数](@entry_id:136843)。温度 $T$ 通过两个关键参数进入该方程：

1.  **[交换电流密度](@entry_id:159311) $j_0(T)$**：$j_0$ 是在平衡状态下（$\eta=0$）正向和反向反应的速率，它衡量了电极的本征催化活性。作为一个[化学反应速率常数](@entry_id:184828)，它通常遵循**阿伦尼乌斯 (Arrhenius)** 关系式，即随温度[指数增长](@entry_id:141869)：
    $$
    j_0(T) \propto k^0(T) \propto \exp\left(-\frac{E_a}{RT}\right)
    $$
    其中 $E_a$ 是反应的活化能。温度升高，指数项变大，[交换电流密度](@entry_id:159311)增加，意味着在相同的过电势下可以获得更大的反应电流。这是温度对动力学最直接的加速效应。

2.  **指数项中的 $RT$ 和过电势 $\eta(T)$**：
    -   指数项的分母中包含 $RT$，这使得在固定过电势 $\eta$ 下，温度升高会减小指数项的绝对值，从而*减弱*过电势的驱动效果。
    -   过电势 $\eta = \phi_s - \phi_l - U_{\mathrm{eq}}(T)$ 本身也依赖于温度，因为平衡电势 $U_{\mathrm{eq}}(T)$ 是温度的函数。根据能斯特方程，平衡电势不仅显式地包含 $T$（在 $RT/nF$ 项中），其[标准电极电势](@entry_id:184074) $E^0$ 本身也是温度的函数。

这些复杂的依赖关系构成了热与电化学之间反馈回路的基础。温度升高会加速反应，产生更多的热量；而这些热量又会进一步影响温度和[反应速率](@entry_id:185114)。

### 热[失控反馈](@entry_id:1131145)机制

上述耦合关系可能导致一种危险的[正反馈](@entry_id:173061)循环，即**热失控 (thermal runaway)**。我们可以通过分析不[可逆热](@entry_id:1130995)源 $\dot{q}_{\mathrm{irr}} \approx a_s j \eta$ 对温度的敏感性来理解其机制 。热反馈的符号由 $\partial \dot{q}_{\mathrm{irr}} / \partial T$ 的符号决定。在固定过电势 $\eta$ 的条件下，这等价于分析 $\partial j / \partial T$ 的符号。

考虑大过电势下的单边Butler-Volmer近似（例如阳极反应，$\eta > 0$）：
$$
j \approx j_0(T) \exp\left(\frac{\alpha F \eta}{RT}\right)
$$
为了分析其随温度的变化，我们对 $\ln j$ 求导：
$$
\ln j \approx \ln j_0(T) + \frac{\alpha F \eta}{RT}
$$
代入 $j_0(T)$ 的阿伦尼乌斯形式 $\ln j_0 \approx \text{const} - E_a/(RT) + \ln f(c)$，其中 $f(c)$ 代表浓度依赖项，我们得到：
$$
\frac{\partial (\ln j)}{\partial T} \approx \frac{E_a}{RT^2} - \frac{\alpha F \eta}{RT^2} + \frac{\partial (\ln f)}{\partial T}
$$
正热反馈（$\partial j / \partial T > 0$）的条件是：
$$
\frac{E_a - \alpha F \eta}{RT^2} + \frac{\partial (\ln f)}{\partial T} > 0 \quad \implies \quad E_a + RT^2 \frac{\partial (\ln f)}{\partial T} > \alpha F \eta
$$
这个不等式揭示了控制[热稳定性](@entry_id:157474)的几个竞争因素：
- **活化能 ($E_a$)**：活化能项总是正的，它代表了[反应速率](@entry_id:185114)随温度升高的内在趋势，是**[正反馈](@entry_id:173061)**的来源。活化能越高，热失控风险越大。
- **过电势项 ($\alpha F \eta$)**：由于指数项中存在 $1/T$，在固定 $\eta$ 时，温度升高会削弱其驱动作用。这一项是**负反馈**的来源，有助于维持稳定。
- **浓度项 ($RT^2 \partial (\ln f) / \partial T$)**：此项反映了动态耦合。在快速反应中，温度升高会加速反应物消耗，导致界面浓度降低，从而减小 $j_0$（因为 $f(c)$ 减小）。这通常构成一个**负反馈**回路，有助于抑制热失控。

热失控是否发生，取决于这些正负反馈效应的综合平衡。

### 完整的耦合模型：热-电化学-[输运方程](@entry_id:174281)组

将上述所有原理整合在一起，我们就可以构建一个完整的热-电[化学耦合](@entry_id:138976)模型，例如广泛使用的**Doyle–Fuller–Newman (DFN)** 模型的[热耦合](@entry_id:1132992)版本。该模型通过一组[偏微分方程(PDEs)](@entry_id:169422)来描述电池内部的[物理化学](@entry_id:145220)过程 。在一个一维模型中，这些方程描述了五个主要未知量随空间位置 $x$ 和时间 $t$ 的演化：[电解质](@entry_id:261072)浓度 $c_e(x,t)$，固相电势 $\phi_s(x,t)$，液相电势 $\phi_e(x,t)$，固相颗粒内锂浓度 $c_s(x,r,t)$，以及温度 $T(x,t)$。

完整的方程组如下：

1.  **固相颗粒内物质守恒（[菲克第二定律](@entry_id:149792)）**:
    $$
    \frac{\partial c_s}{\partial t} = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 D_s(T) \frac{\partial c_s}{\partial r} \right)
    $$

2.  **[电解质](@entry_id:261072)相物质守恒**:
    $$
    \frac{\partial(\varepsilon_e c_e)}{\partial t} = \frac{\partial}{\partial x}\left( D_e^{\mathrm{eff}}(T,c_e) \frac{\partial c_e}{\partial x} \right) + \frac{(1 - t_+^0) a_s(x)}{F} j(x,t)
    $$

3.  **固相电荷守恒（欧姆定律）**:
    $$
    \frac{\partial i_s}{\partial x} = a_s j \quad \text{其中} \quad i_s = -\sigma^{\mathrm{eff}}(T) \frac{\partial \phi_s}{\partial x}
    $$

4.  **[电解质](@entry_id:261072)相电荷守恒（[浓溶液理论](@entry_id:1122829)）**:
    $$
    \frac{\partial i_e}{\partial x} = -a_s j \quad \text{其中} \quad i_e = -\kappa_e^{\mathrm{eff}}(T,c_e) \frac{\partial \phi_e}{\partial x} + \kappa_e^{\mathrm{eff}}(T,c_e) \frac{2 R T (1 - t_+^0)}{F} \frac{\partial \ln c_e}{\partial x}
    $$

5.  **界面反应动力学（[Butler-Volmer方程](@entry_id:150187)）**:
    $$
    j = j_0(T,c_e,c_{s,\mathrm{surf}}) \left[ \exp\left(\frac{\alpha_a F \eta}{RT}\right) - \exp\left(-\frac{\alpha_c F \eta}{RT}\right) \right]
    $$
    $$
    \eta = \phi_s - \phi_e - U(c_{s,\mathrm{surf}}, T)
    $$

6.  **能量守恒（热方程）**:
    $$
    \rho^{\mathrm{eff}} c_p^{\mathrm{eff}} \frac{\partial T}{\partial t} = \frac{\partial}{\partial x}\left( k^{\mathrm{eff}}(T) \frac{\partial T}{\partial x} \right) + \dot{q}
    $$
    其中热源 $\dot{q}$ 为：
    $$
    \dot{q} = \underbrace{\frac{i_s^2}{\sigma^{\mathrm{eff}}(T)}}_{\text{固相欧姆热}} + \underbrace{\frac{i_e^2}{\kappa_e^{\mathrm{eff}}(T,c_e)}}_{\text{液相欧姆热(近似)}} + \underbrace{a_s j \eta}_{\text{不可逆反应热}} + \underbrace{a_s j T \frac{\partial U}{\partial T}}_{\text{可逆反应热}}
    $$

这个方程组通过物性参数的[温度依赖性](@entry_id:147684)（如$D_s(T)$, $D_e^{\mathrm{eff}}(T)$, $\sigma^{\mathrm{eff}}(T)$, $\kappa_e^{\mathrm{eff}}(T)$）以及动力学和[热力学](@entry_id:172368)参数（$j_0(T)$, $U(T)$）实现了完全的耦合。求解这个方程组可以预测电池在各种工况下的电化学和热行为。

### 高等耦合效应

除了上述核心耦合机制外，在更精细的模型中还会考虑其他物理场的交叉耦合效应。

#### 热-质耦合：Soret与[Dufour效应](@entry_id:155524)

- **Soret效应（热扩散）**: 指在存在温度梯度时，即使没有浓度梯度，也会产生物质通量。这会导致混合物中的组分发生分离，较轻或较“热亲和”的组分向热端移动，反之则向冷端移动 。对于[二元混合物](@entry_id:168452)，物种 $i$ 的通量 $\mathbf{N}_i$ 修正为：
$$
\mathbf{N}_i = -D_i \nabla c_i - D_i c_i(1-c_i) S_T \nabla T
$$
其中 $S_T$ 是[Soret系数](@entry_id:151790)。

- **[Dufour效应](@entry_id:155524)**: 它是Soret效应的逆效应，指浓度梯度可以引起热通量。根据昂萨格 (Onsager) 倒易关系，Soret效应和[Dufour效应](@entry_id:155524)的交叉系数是相关的 。这意味着热通量 $\mathbf{q}$ 不仅遵循傅里叶定律，还包含一个与浓度梯度 $\nabla c_i$ 成正比的项。这些效应在液体中通常较小，但在某些特定条件下可能对传质和传热产生不可忽略的影响。

#### 力-热-电[化学耦合](@entry_id:138976)

在[锂离子电池](@entry_id:150991)中，锂的嵌入和脱出伴随着活性材料颗粒的体积变化，这会在电极内部产生显著的**机械应力 (mechanical stress)**。这些应力可以与电化学和热过程发生强烈的耦合 。

- **应力对输运和动力学的影响**:
    1.  **应力影响扩散**: 机械应力（特别是静水压力 $\sigma_h$）会改变原子扩散的活化能，从而影响[固相扩散](@entry_id:1131915)系数 $D_s$。例如，压应力可能促进或阻碍锂离子的扩散。
    2.  **应力影响平衡电势**: 嵌入一个锂离子到[晶格](@entry_id:148274)中所需做的机械功（$p dV = -\sigma_h \Omega$，其中 $\Omega$ 是锂的[偏摩尔体积](@entry_id:143502)）会改变反应的吉布斯自由能，从而改变平衡电势 $U_{\mathrm{eq}}$。通常，压应力会使嵌入更加困难，从而降低平衡电势。

- **应力对产热的反馈**:
    -   通过影响 $D_s$ 和 $U_{\mathrm{eq}}$，应力改变了浓度分布和过电势，进而改变了反应电流 $j$，最终影响了[反应热](@entry_id:140993)（$j\eta$ 和 $j T \partial U/\partial T$）的生成。
    -   如果材料发生塑性变形或断裂，[机械能](@entry_id:162989)的耗散也会直接转化为**[机械耗散](@entry_id:169843)热**（$\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^{\text{inelastic}}$），成为额外的热源。

将这些力学效应纳入模型，就构成了更为复杂的**力-热-电化学**多物理场耦合问题，这对于理解电池的长期衰退和机械失效至关重要。