## 引言
在许多工程和科学领域，尤其是在[计算燃烧学](@entry_id:1122776)和航空航天等涉及高温环境的学科中，热辐射是一种主导的能量传递模式。准确预测[辐射传热](@entry_id:149271)对于模拟火焰结构、[污染物形成](@entry_id:1129911)以及高超声速飞行器的热防护至关重要。然而，描述辐射现象的物理模型——辐射传输方程(RTE)，是一个复杂的积分-[偏微分](@entry_id:194612)方程，直接求解极为困难。这催生了多种数值方法，其中，离散坐标法(DOM)因其通用性和在复杂几何中的适用性，已成为[计算流体动力学](@entry_id:142614)(CFD)中应用最广泛的辐射求解器之一。

本文旨在为研究生及相关领域的研究人员提供一份关于[气体辐射](@entry_id:150797)离散坐标法的全面指南。我们将系统性地解决从理论构建到实际应用的完整学习路径，帮助读者不仅理解“是什么”，更掌握“如何用”。

- 在**第一章：原理与机制**中，我们将深入剖析辐射传输方程的物理内涵，详细阐述离散坐标法的核心思想——角向离散化，并解释其如何与能量方程耦合，形成封闭的数值求解框架。
- 接着，在**第二章：应用与交叉学科联系**中，我们将通过燃烧模拟、[高超声速再入](@entry_id:1126302)等具体案例，展示DOM在解决前沿工程问题中的强大能力，并揭示其与[化学动力学](@entry_id:144961)、等离子体物理和高性能计算等领域的深刻联系。
- 最后，在**第三章：动手实践**中，您将通过一系列精心设计的编程练习，亲手实现和评估DOM的关键方面，将理论知识转化为解决实际问题的技能。

通过这一结构化的学习过程，读者将建立对离散坐标法的坚实理解。现在，让我们从[辐射传热](@entry_id:149271)最基本的控制方程开始，进入第一章的学习。

## 原理与机制

在深入探讨离散坐标法（Discrete Ordinates Method, DOM）在[气体辐射](@entry_id:150797)计算中的具体应用之前，我们必须首先建立对辐射传输物理过程及其数学描述的坚实理解。本章旨在系统性地阐述控制辐射强度的基本方程、DOM的核心原理，以及将这些理论应用于实际燃烧问题时所涉及的关键机制与简化模型。

### 辐射传输方程 (RTE)

辐射传热的核心是描述辐射强度在参与性介质中传播时如何变化的**辐射传输方程 (Radiative Transfer Equation, RTE)**。**[辐射强度](@entry_id:150179)** $I_\nu(\boldsymbol{x}, \boldsymbol{s})$ 是一个基本量，定义为在位置 $\boldsymbol{x}$、沿单位[方向矢量](@entry_id:1132366) $\boldsymbol{s}$ 传播的、单位频率间隔内、单位投影面积上、单位[立体角](@entry_id:154756)内的[辐射功率](@entry_id:267187)。

对于一个[稳态](@entry_id:139253)、可吸收、发射和散射的参与性介质，RTE 源于沿射线路径的能量守恒。考虑一段沿方向 $\boldsymbol{s}$ 的[微分](@entry_id:158422)路径 $ds$，[辐射强度](@entry_id:150179)的变化 $dI_\nu$ 来自于介质的吸收（损失）、发射（增益）和散射（增益与损失）过程。这可以写成如下的[微分](@entry_id:158422)[平衡方程](@entry_id:172166) ：

$$
\boldsymbol{s} \cdot \nabla I_\nu(\boldsymbol{x}, \boldsymbol{s}) = \underbrace{-\kappa_{a,\nu} I_\nu(\boldsymbol{x}, \boldsymbol{s})}_{\text{吸收}} + \underbrace{\kappa_{a,\nu} I_{b,\nu}(T)}_{\text{发射}} \underbrace{-\sigma_{s,\nu} I_\nu(\boldsymbol{x}, \boldsymbol{s})}_{\text{外散射}} + \underbrace{\sigma_{s,\nu} \int_{4\pi} \Phi(\boldsymbol{s}' \cdot \boldsymbol{s}) I_\nu(\boldsymbol{x}, \boldsymbol{s}') d\Omega'}_{\text{内散射}}
$$

我们来逐项解析这个方程：

*   **流变项 (Streaming Term)**：左侧的 $\boldsymbol{s} \cdot \nabla I_\nu$ 表示强度 $I_\nu$ 沿着方向 $\boldsymbol{s}$ 的空间变化率，描述了辐射能量在没有与介质发生相互作用时的直线传播。

*   **吸收项 (Absorption Term)**：$-\kappa_{a,\nu} I_\nu$ 代表辐射束因被介质吸收而造成的强度衰减。$\kappa_{a,\nu}$ 是**光谱[吸收系数](@entry_id:156541)**，表示单位路径长度上辐射被吸收的概率。

*   **发射项 (Emission Term)**：$\kappa_{a,\nu} I_{b,\nu}(T)$ 代表介质由于其自身温度 $T$ 而发射的热辐射。根据[基尔霍夫热辐射定律](@entry_id:144588)，在局部热力学平衡（LTE）下，介质的[光谱发射率](@entry_id:1132091)等于其光谱[吸收率](@entry_id:144520)。$I_{b,\nu}(T)$ 是**普朗克[黑体辐射](@entry_id:137223)[强度函数](@entry_id:755508)**，它给出了在温度 $T$ 下黑体发射的[辐射强度](@entry_id:150179)的光[谱分布](@entry_id:158779)。

*   **散射项 (Scattering Terms)**：散射过程将辐射从一个方向重新分配到另一个方向。**外散射**（$-\sigma_{s,\nu} I_\nu$）是沿 $\boldsymbol{s}$ 方向的强度因被散射到其他方向而造成的损失。$\sigma_{s,\nu}$ 是**光谱散射系数**。**内散射**（积分项）是来自所有其他方向 $\boldsymbol{s}'$ 的辐射被散射到当前方向 $\boldsymbol{s}$ 的增益。$\Phi(\boldsymbol{s}' \cdot \boldsymbol{s})$ 是**[散射相函数](@entry_id:1131288)**，描述了辐射能量从 $\boldsymbol{s}'$ 方向散射到 $\boldsymbol{s}$ 方向的概率分布。

在许多高温燃烧应用中，例如不含烟尘的天然气燃烧，辐射主要由气相分子（如 $\text{H}_2\text{O}$ 和 $\text{CO}_2$）的振动-转动谱带主导。在这些条件下，分子散射（[瑞利散射](@entry_id:178255)）相比于吸收和发射通常可以忽略不计 。是否可以忽略散射，可以通过两个[无量纲参数](@entry_id:169335)进行判断：

1.  **[单次散射反照率](@entry_id:1131707) (Single-Scattering Albedo)**：$\omega_\nu = \sigma_{s,\nu} / (\kappa_{a,\nu} + \sigma_{s,\nu})$，表示一次光子-介质相互作用中，散射事件相对于总消光（吸收+散射）事件的概率。
2.  **散射[光学厚度](@entry_id:150612) (Scattering Optical Thickness)**：$\tau_{s,\nu} = \sigma_{s,\nu} L$，表示光子在穿过特征长度为 $L$ 的介质时发生散射的期望次数。

当 $\omega_\nu \ll 1$ 且 $\tau_{s,\nu} \ll 1$ 时，表明介质是强吸收性的，并且光子在整个路径中几乎不会发生散射。例如，在一个特征尺度为 $0.5\,\mathrm{m}$、温度为 $1800\,\mathrm{K}$ 的无烟尘燃烧产物中，某个红外谱带处的[吸收系数](@entry_id:156541)可能为 $\kappa_{a,\nu} = 0.5\,\mathrm{m}^{-1}$，而散射系数可能低至 $\sigma_{s,\nu} = 10^{-6}\,\mathrm{m}^{-1}$。此时，$\omega_\nu \approx 2 \times 10^{-6}$，$\tau_{s,\nu} = 5 \times 10^{-7}$，这两个条件都充分满足，因此可以安全地忽略散射项 。

在这种常见的**非散射**介质近似下，RTE 显著简化为 ：

$$
\boldsymbol{s} \cdot \nabla I_\nu(\boldsymbol{x}, \boldsymbol{s}) = \kappa_\nu(\boldsymbol{x}) \left[ I_{b,\nu}(T(\boldsymbol{x})) - I_\nu(\boldsymbol{x}, \boldsymbol{s}) \right]
$$

这个方程构成了许多工程辐射计算的基础。它平衡了强度的空间变化（左侧）与介质的发射增益和吸收损失（右侧）。

### 与能量方程的耦合：辐射源项

在[计算流体动力学](@entry_id:142614)（CFD）模拟中，辐射通过能量守恒方程影响温度场。能量方程中的辐射贡献项是**辐射热流矢量** $\boldsymbol{q}_r$ 的散度，通常记为**辐射源项** $Q_{rad} = -\nabla \cdot \boldsymbol{q}_r$。注意，这里的符号约定是 $Q_{rad}$ 为介质获得的净能量；在某些文献中，它可能被定义为 $\nabla \cdot \boldsymbol{q}_r$，即介质损失的净能量。

辐射热流矢量 $\boldsymbol{q}_r$ 定义为[辐射强度](@entry_id:150179)在所有方向上的第一矩：

$$
\boldsymbol{q}_r(\boldsymbol{x}) = \int_{4\pi} I(\boldsymbol{x}, \boldsymbol{s}) \boldsymbol{s} \,d\Omega
$$

为了推导辐射源项，我们对简化的非散射 RTE 在整个 $4\pi$ 立体角上进行积分。为简化推导，我们暂时考虑一个**灰体介质**（即吸收系数 $\kappa$ 与频率无关）：

$$
\int_{4\pi} (\boldsymbol{s} \cdot \nabla I) \,d\Omega = \int_{4\pi} \kappa (I_b - I) \,d\Omega
$$

利用[散度定理](@entry_id:143110)，并注意到 $\boldsymbol{s}$ 与 $\boldsymbol{x}$ 无关，左侧变为 $\nabla \cdot \left(\int_{4\pi} I \boldsymbol{s} \,d\Omega\right) = \nabla \cdot \boldsymbol{q}_r$。右侧的 $I_b$ 和 $\kappa$ 是各向同性的，可以移到积分外：

$$
\nabla \cdot \boldsymbol{q}_r = \kappa I_b \int_{4\pi} d\Omega - \kappa \int_{4\pi} I \,d\Omega
$$

定义**入射辐射** $G(\boldsymbol{x}) = \int_{4\pi} I(\boldsymbol{x}, \boldsymbol{s}) \,d\Omega$，它是到达某一点的[总辐射功率](@entry_id:756065)。同时，$\int_{4\pi} d\Omega = 4\pi$。因此，我们得到：

$$
\nabla \cdot \boldsymbol{q}_r = \kappa (4\pi I_b - G)
$$

引入**平均[辐射强度](@entry_id:150179)** $J(\boldsymbol{x}) = G(\boldsymbol{x}) / (4\pi)$，上式可以写成更紧凑的形式 ：

$$
\nabla \cdot \boldsymbol{q}_r = 4\pi \kappa (I_b - J)
$$

这个表达式清楚地揭示了辐射与介质的能量交换机制：当局部黑体发射强度 $I_b$ 大于周围环境的平均强度 $J$ 时，净能量流出该微元（$\nabla \cdot \boldsymbol{q}_r > 0$），导致介质冷却；反之亦然。然而，这也带来了一个**封闭性问题**：能量方程依赖于 $J$，而 $J$ 本身是通过对未知的辐射强度场 $I$ 积分得到的。为了求解 $I$，我们需要求解 RTE。离散坐标法（DOM）正是为解决这个耦合问题而设计的。

### 离散坐标法 (DOM)

#### 角向离散化

DOM 的核心思想是将辐射强度对方向 $\boldsymbol{s}$ 的连续依赖性替换为一组有限的、离散的**坐标**（ordinates）或方向，记为 $\{\boldsymbol{s}_m\}_{m=1}^M$。每个方向 $\boldsymbol{s}_m$ 都关联一个**积分权重** $w_m$，它们共同构成一个**角向[求积组](@entry_id:156430)**。这个[求积组](@entry_id:156430)用于将任何关于方向的函数 $f(\boldsymbol{s})$ 的积分近似为一个加权和：

$$
\int_{4\pi} f(\boldsymbol{s}) \,d\Omega \approx \sum_{m=1}^M w_m f(\boldsymbol{s}_m)
$$

通过这种离散化，原本单一的、包含积分项的 RTE 被转化为一个包含 $M$ 个耦合的偏微分方程组。对于每个离散方向 $\boldsymbol{s}_m$，我们求解其对应的强度 $I_{\nu,m}(\boldsymbol{x}) \equiv I_\nu(\boldsymbol{x}, \boldsymbol{s}_m)$。对于非散射介质，第 $m$ 个 DOM 方程为 ：

$$
\boldsymbol{s}_m \cdot \nabla I_{\nu,m}(\boldsymbol{x}) = \kappa_\nu(\boldsymbol{x}) \left[ I_{b,\nu}(T(\boldsymbol{x})) - I_{\nu,m}(\boldsymbol{x}) \right]
$$

值得注意的是，积分权重 $w_m$ 不会出现在单个方向的[输运方程](@entry_id:174281)中，它们仅在计算角度积分量（如辐射源项）时使用。

#### 辐射源项的封闭

一旦通过求解上述方程组得到了所有离散方向的强度 $\{I_m\}_{m=1}^M$，我们就可以使用角向求积来计算平均[辐射强度](@entry_id:150179) $J$，从而封闭能量方程。对于灰体介质：

$$
J(\boldsymbol{x}) = \frac{1}{4\pi} \int_{4\pi} I(\boldsymbol{x}, \boldsymbol{s}) \,d\Omega \approx \frac{1}{4\pi} \sum_{m=1}^M w_m I_m(\boldsymbol{x})
$$

为了使这个近似有效，[求积组](@entry_id:156430) $\{\boldsymbol{s}_m, w_m\}$ 必须满足特定的**[矩条件](@entry_id:136365)**，最基本的一条是它必须能精确积分[常数函数](@entry_id:152060)，即 $\sum_{m=1}^M w_m = \int_{4\pi} 1 \,d\Omega = 4\pi$ 。

综上所述，DOM 的工作流程是：
1.  求解 $M$ 个关于离散强度 $I_m$ 的[偏微分](@entry_id:194612)方程。
2.  利用[求积组](@entry_id:156430)将求解得到的 $\{I_m\}$ 合成为平均强度 $J$。
3.  将 $J$ 代入辐射源项表达式 $4\pi \kappa (I_b - J)$，为能量方程提供封闭。
这个过程在每个 CFD 迭代步中重复，以确保辐射场和温度场的完全耦合。

### 物理机制与边界条件

#### 光学厚度与渐近极限

介质与辐射相互作用的强度可以用**[光学厚度](@entry_id:150612)** $\tau_\nu$ 来表征。对于沿法线方向穿过厚度为 $L$ 的平板介质，其定义为[吸收系数](@entry_id:156541)沿路径的积分 $\tau_\nu(L) = \int_0^L \kappa_\nu(x) dx$ 。光学厚度是一个无量纲量，它决定了辐射场的行为。

*   **[光学薄极限](@entry_id:1129155) ($\tau_\nu \ll 1$)**：介质几乎是透明的。辐射可以几乎无衰减地穿过介质。在这种情况下，内部任一点的[辐射场](@entry_id:164265)主要由边界条件（如壁面发射或外部入射辐射）决定。局部的气体发射对总[辐射场](@entry_id:164265)的贡献很小，量级为 $\mathcal{O}(\tau_\nu)$。由于辐射场保留了很强的方向性（继承自边界条件），因此需要较高阶的角向离散（即更多的坐标）来准确捕捉角度分布的细节 。

*   **光学厚极限 ($\tau_\nu \gg 1$)**：介质是高度不透明的。来自边界的辐射在深入介质不远后就被完全吸收。在远离边界的内部区域，辐射场与物质达到局部热力学平衡，即[辐射强度](@entry_id:150179)在所有方向上都趋近于当地的普朗克函数，$I_\nu \approx I_{b,\nu}(T)$。[辐射场](@entry_id:164265)变得几乎各向同性。在这种情况下，辐射传输可以用更简单的**扩散近似**来描述，并且 DOM 只需要很少的坐标就能准确表示平滑的角度分布。边界的影响仅限于一个物理厚度约为 $\mathcal{O}(1/\kappa_\nu)$ 的薄层内 。

一个重要的考虑是，沿斜向路径的有效光学厚度会增加。对于以与[法线](@entry_id:167651)夹角 $\theta$（[方向余弦](@entry_id:170591)为 $\mu = \cos\theta$）传播的射线，其穿过的几何路径是法向距离的 $1/|\mu|$ 倍。因此，其经历的**光学路径长度**为 $\tau_\nu/|\mu|$。这意味着即使对于法向光学薄的介质，对于掠射角（$|\mu| \to 0$）的辐射，介质也可能表现为光学厚。这个效应是理解边界层现象和 DOM 中角度分辨率要求的关键 。

#### DOM 中的边界条件

在 DOM 中，必须为每个指向计算域内的离散方向（即入射方向）规定边界强度。

*   **黑[体壁](@entry_id:272571)面**：一个温度为 $T_w$ 的黑[体壁](@entry_id:272571)面是完美的吸收体和发射体。它吸收所有入射辐射，并以各向同性的黑体强度 $I_{b,\nu}(T_w)$ 向外发射。因此，对于所有满足 $\boldsymbol{s}_m \cdot \boldsymbol{n}_w  0$ 的入射方向（其中 $\boldsymbol{n}_w$ 是壁面的外法线），边界强度被设定为 ：
    $$
    I_{\nu,m}(\boldsymbol{x}_w) = I_{b,\nu}(T_w) \quad (\text{for } \boldsymbol{s}_m \cdot \boldsymbol{n}_w  0)
    $$

*   **镜面反射壁面**：一个理想的镜面反射壁面不吸收也不发射辐射，而是将入射辐射根据[反射定律](@entry_id:175197)反射回计算域。对于给定的入射方向 $\boldsymbol{s}_i$，反射方向 $\boldsymbol{s}_r$ 由下式给出：
    $$
    \boldsymbol{s}_r = \boldsymbol{s}_i - 2(\boldsymbol{s}_i \cdot \boldsymbol{n}_w) \boldsymbol{n}_w
    $$
    能量守恒要求反射光线的强度等于入射光线的强度。因此，边界条件将一个出射方向的强度与另一个入射方向的强度联系起来 ：
    $$
    I(\boldsymbol{x}_w, \boldsymbol{s}_r) = I(\boldsymbol{x}_w, \boldsymbol{s}_i)
    $$
    在 DOM 中，这意味着某个出射坐标 $I_m$ 的边界值由另一个入射坐标 $I_j$ 在同一位置的值决定，其中 $\boldsymbol{s}_m$ 是 $\boldsymbol{s}_j$ 的[镜面反射](@entry_id:270785)方向。

### DOM 的高级主题

#### [求积组](@entry_id:156430)与矩守恒

DOM 的准确性在很大程度上取决于角向[求积组](@entry_id:156430) $\{\boldsymbol{s}_m, w_m\}$ 的选择。一个好的[求积组](@entry_id:156430)必须能够精确地积分低阶球谐函数，这等价于保持辐射强度场的各阶角度矩。对于一个各向同性的[辐射场](@entry_id:164265) $I = I_0$，我们期望计算得到的物理量与理论值完全一致：

1.  **零阶矩（入射辐射）**：$\sum_m w_m I_0 = I_0 \int_{4\pi} d\Omega = 4\pi I_0 \implies \sum_m w_m = 4\pi$。
2.  **一阶矩（辐射热流）**：$\sum_m w_m I_0 \boldsymbol{s}_m = I_0 \int_{4\pi} \boldsymbol{s} d\Omega = \boldsymbol{0} \implies \sum_m w_m \boldsymbol{s}_m = \boldsymbol{0}$。
3.  **二阶矩（[辐射压力](@entry_id:165366)张量）**：$\sum_m w_m I_0 s_{m,i} s_{m,j} = I_0 \int_{4\pi} s_i s_j d\Omega = \frac{4\pi}{3} I_0 \delta_{ij} \implies \sum_m w_m s_{m,i} s_{m,j} = \frac{4\pi}{3} \delta_{ij}$。

标准的高阶 $S_N$ [求积组](@entry_id:156430)（如[水平对称求积](@entry_id:1127172)组）通过精心构造方向和权重的对称性来自动满足这些[矩条件](@entry_id:136365) 。这种矩守恒特性对于确保数值解的物理真实性至关重要。当考虑[各向异性散射](@entry_id:148372)时，为了精确计算散射源项，对[求积组](@entry_id:156430)的要求会更高。如果强度和相函数都可以用最高 $L$ 阶的[球谐函数展开](@entry_id:188485)，那么[求积组](@entry_id:156430)必须能精确积分最高 $2L$ 阶的所有球谐函数，以精确计算它们的乘积 。

#### 光谱模型：灰体近似

[真实气体](@entry_id:136821)的吸收系数 $\kappa_\nu$ 具有极其复杂的随频率变化的结构，直接进行光谱积分计算成本极高。因此，发展了各种**光谱模型**（或称灰体近似）来简化问题。

*   **普朗克平均吸收系数 ($\kappa_P$)**：此系数定义为 $\kappa_\nu$ 以普朗克函数 $B_\nu(T)$ 为权重的平均值。它被设计用于在**[光学薄极限](@entry_id:1129155)**下，精确保持气体的总发射功率。
    $$
    \kappa_P = \frac{\int_0^\infty \kappa_\nu B_\nu(T) d\nu}{\int_0^\infty B_\nu(T) d\nu}
    $$

*   **[罗斯兰平均吸收系数](@entry_id:754423) ($\kappa_R$)**：此系数是一个谐波平均，其权重函数为普朗克函数对温度的导数 $\partial B_\nu / \partial T$。它被设计用于在**光学厚极限**下，当辐射传输表现为[扩散过程](@entry_id:268015)时，精确保持总辐射热流。
    $$
    \frac{1}{\kappa_R} = \frac{\int_0^\infty \frac{1}{\kappa_\nu} \frac{\partial B_\nu}{\partial T} d\nu}{\int_0^\infty \frac{\partial B_\nu}{\partial T} d\nu}
    $$
    选择哪种平均系数取决于问题的物理特性。$\kappa_P$ 适用于发射主导的场景，而 $\kappa_R$ 适用于扩散主导的场景 。

*   **加权灰体和模型 (WSGG)**：这是一种更精确的光谱模型，它将真实气体的总发射率拟合成若干个（通常是4-5个）具有不同吸收系数 $\kappa_i$ 的假想灰体和一个透明气体（$\kappa_0=0$）的加权和。权重因子 $a_i(T,p,y)$ 代表了在温度 $T$、压力 $p$ 和组分 $y$ 下，被第 $i$ 个灰体所代表的光谱带所包含的黑体辐射能量的份额，且满足 $\sum a_i=1$。该模型将复杂的频率依赖性转化为求解一组并行的[灰体辐射](@entry_id:142501)传输方程，每个方程对应一个灰体组分，其发射项被相应地缩放为 $\kappa_i a_i I_b$。最终的总[辐射场](@entry_id:164265)是所有灰体组分贡献的总和。WSGG 模型在工程计算中，尤其是在 $\text{H}_2\text{O}$–$\text{CO}_2$ 混合物的辐射计算中，取得了巨大成功 。

#### 射线效应伪影

DOM 的一个固有缺陷是**射线效应 (Ray Effect)**。由于角度空间被离散化为有限数量的方向，辐射能量只能沿着这些离散的路径传播。当辐射源是局部的（例如一个小的热点或火焰锋面），能量会像手电筒光束一样沿着离散的坐标方向射出，而在这些方向之间留下未被辐射照亮的“阴影区”。这导致计算出的辐射场（如入射辐射 $G$）出现非物理的波纹和条纹 。

射线效应在[光学薄介质](@entry_id:1129156)中、存在强烈的局部辐射源或温度梯度时最为显著。减轻射线效应的主要方法是增加离散坐标的数量（即使用更高阶的 $S_N$ [求积组](@entry_id:156430)），但这会直接增加计算成本。通过比较粗糙角向网格（如 $S_4$，12个方向）和精细角向网格（如 $S_{12}$，96个方向）下的解，可以量化射线效应的严重程度。其差异的均方根和最大值等指标，可以评估角向离散的收敛性和解的质量 。理解并识别射线效应对于正确解释 DOM 的计算结果至关重要。