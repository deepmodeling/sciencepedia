## 引言
对核反应堆在非[稳态](@entry_id:139253)工况下的行为进行精确预测，是确保其安全运行与高效控制的基石。瞬态[中子扩散理论](@entry_id:160104)正是描述反应堆内部中子群体随时间动态演化的核心物理模型。然而，从[稳态分析](@entry_id:271474)过渡到[瞬态分析](@entry_id:262795)，意味着需要处理更为复杂的时空耦合现象以及中子产生与损失过程中的各种时间[延迟效应](@entry_id:199612)，这对理论理解和计算建模都提出了更高的要求。本文旨在系统性地剖析这一关键领域。在“原理与机制”章节中，我们将深入探讨[瞬态扩散](@entry_id:154656)方程的数学形式、物理基础及其内在局限性，并阐明[反应堆动力学](@entry_id:1130674)中的核心概念。随后的“应用与跨学科联系”章节将展示该理论在[反应堆瞬态分析](@entry_id:1130686)、敏感性研究等实际工程问题中的应用，并揭示其与[热传导](@entry_id:143509)、量子力学等其他学科的深刻联系。最后，通过“动手实践”部分，读者将有机会将理论知识应用于具体的计算问题中。现在，让我们首先进入理论的核心，详细考察瞬态[中子扩散](@entry_id:158469)的原理与机制。

## 原理与机制

本章旨在深入阐述瞬态[中子扩散理论](@entry_id:160104)的核心原理与机制。我们将从描述中子群体宏观行为的数学方程出发，探讨其物理基础、内在局限性，并进一步延伸至反应堆动力学分析中的关键概念，如反馈效应、[点动力学](@entry_id:1129859)近似及其适用范围，以及用于灵敏度分析的伴随理论。

### 瞬态[多群扩散方程](@entry_id:1128304)

描述反应堆内中子群体时空行为最常用的模型是**瞬态[多群扩散方程](@entry_id:1128304)** (time-dependent multigroup diffusion equation)。该模型基于中子[守恒原理](@entry_id:1122907)，将连续的中子能谱划分为有限数量（$G$个）的离散能群，并对每个能群建立中子[平衡方程](@entry_id:172166)。对于任意能群 $g$（$g=1, \dots, G$），其在中子通量密度 $\phi_g(\mathbf{r}, t)$ 的控制方程可以写作：

$$
\frac{1}{v_g}\frac{\partial \phi_g(\mathbf{r}, t)}{\partial t} = \nabla \cdot \big( D_g(\mathbf{r}) \nabla \phi_g(\mathbf{r}, t) \big) - \Sigma_{r,g}(\mathbf{r})\phi_g(\mathbf{r}, t) + \sum_{h=1}^{G}\Sigma_{s,h\to g}(\mathbf{r})\phi_h(\mathbf{r}, t) + \chi_g \sum_{h=1}^{G}\nu_h \Sigma_{f,h}(\mathbf{r})\phi_h(\mathbf{r}, t) + S_g(\mathbf{r}, t)
$$

这个方程精确地表达了在一个[微分](@entry_id:158422)[体积元](@entry_id:267802)内，单位时间能群 $g$ 中子密度的变化率（方程左侧）等于该能群中子的净增量（方程右侧）。我们来逐项解析这个[平衡方程](@entry_id:172166)：

*   **中子密度变化项**：$\frac{1}{v_g}\frac{\partial \phi_g}{\partial t}$ 代表能群 $g$ 中子[数密度](@entry_id:895657) $n_g = \phi_g/v_g$ 的时间变化率。其中，$v_g$ 是能群 $g$ 的平均中子速度 (单位: $\text{cm} \cdot \text{s}^{-1}$)，$\phi_g$ 是标量中子通量密度 (scalar neutron flux)，表示单位时间穿过单位面积的中子数量 (单位: $\text{neutrons} \cdot \text{cm}^{-2} \cdot \text{s}^{-1}$)。此项的单位是 $\text{neutrons} \cdot \text{cm}^{-3} \cdot \text{s}^{-1}$，与方程中所有其他项（反应率密度）的单位保持一致。

*   **泄漏项** (Leakage Term)：$\nabla \cdot ( D_g \nabla \phi_g )$ 代表由于空间不均匀性导致的中子净流出（泄漏）。它源于**[菲克定律](@entry_id:155177)** (Fick's Law)，该定律将[中子流](@entry_id:1128689)密度矢量 $\mathbf{J}_g$ 与通量密度的梯度关联起来：$\mathbf{J}_g = -D_g \nabla \phi_g$。$D_g$ 是能群 $g$ 的**扩散系数** (diffusion coefficient) (单位: $\text{cm}$)。方程中的负号被移到左侧（或在右侧带负号），表示泄漏是一种中子损失机制。

*   **移出项** (Removal Term)：$\Sigma_{r,g}\phi_g$ 代表由于核反应导致中子从能群 $g$ 中移出的总速率。**移出[截面](@entry_id:154995)** (removal cross section) $\Sigma_{r,g}$ (单位: $\text{cm}^{-1}$) 是一个关键的[复合截面](@entry_id:197270)，它包括了所有导致中子离开能群 $g$ 的相互作用。其标准定义为：
    $$
    \Sigma_{r,g} \equiv \Sigma_{a,g} + \sum_{h\neq g} \Sigma_{s,g\to h}
    $$
    其中 $\Sigma_{a,g}$ 是能群 $g$ 的宏观[吸收截面](@entry_id:172609)，$\sum_{h\neq g} \Sigma_{s,g\to h}$ 是中子从能群 $g$ 散射到所有其他能群 $h$（$h \neq g$）的**群外散射** (out-scattering) [截面](@entry_id:154995)之和。值得注意的是，移出[截面](@entry_id:154995)有时也被定义为总截面 $\Sigma_{t,g}$ 减去**群内散射** (in-group scattering) [截面](@entry_id:154995) $\Sigma_{s,g\to g}$，即 $\Sigma_{r,g} = \Sigma_{t,g} - \Sigma_{s,g\to g}$，这在数学上是等价的，因为它同样描述了除群内散射外的所有损失。

*   **源项** (Source Terms)：
    *   **散射源**：$\sum_{h=1}^{G}\Sigma_{s,h\to g}\phi_h$ 代表从中子与其他原子核发生散射反应，从其他所有能群 $h$（包括自身，即 $h=g$）进入能群 $g$ 的中子产生率。$\Sigma_{s,h\to g}$ 是从能群 $h$ 散射到能群 $g$ 的宏观[散射截面](@entry_id:140322)。当我们将所有能群的平衡方程相加时，总的散射源项 $\sum_g \sum_h \Sigma_{s,h\to g}\phi_h$ 与总的群外散射损失项 $\sum_g (\sum_{h\neq g} \Sigma_{s,g\to h})\phi_g$ 会精确抵消。这体现了散射过程仅重新分配中子能量（即在能群间移动中子），而不会改变中子总数的物理事实。在整个系统层面，唯一真正的材料吸收（中子消失）由吸收截面 $\Sigma_{a,g}$ 描述。
    *   **裂变源**：$\chi_g \sum_{h=1}^{G}\nu_h \Sigma_{f,h}\phi_h$ 代表裂变产生的中子对能群 $g$ 的贡献。其中，$\Sigma_{f,h}$ 是能群 $h$ 的宏观裂变[截面](@entry_id:154995)，$\nu_h$ 是由能群 $h$ 的中子引发的单次裂变所产生的平均中子数（无量纲），$\chi_g$ 是裂变中子出生在能群 $g$ 的份额或概率，称为**裂变谱** (fission spectrum)，满足[归一化条件](@entry_id:156486) $\sum_{g=1}^{G}\chi_g=1$。
    *   **外源**：$S_g(\mathbf{r}, t)$ 代表任何外部中子源（如启动中子源）向能群 $g$ 的贡献率 (单位: $\text{neutrons} \cdot \text{cm}^{-3} \cdot \text{s}^{-1}$)。

### [扩散方程](@entry_id:170713)的数学性质与物理启示

为了更清晰地理解[瞬态扩散](@entry_id:154656)方程的内在特性，我们考虑一个简化的单能群模型。通过组合中子数守恒定律 $\frac{\partial n}{\partial t} + \nabla \cdot \mathbf{J} = \text{源} - \text{损失}$、通量定义 $\phi = vn$ 以及[菲克定律](@entry_id:155177) $\mathbf{J} = -D\nabla\phi$，我们可以得到[单群](@entry_id:140851)[瞬态扩散](@entry_id:154656)方程：
$$
\frac{1}{v}\frac{\partial \phi}{\partial t} - \nabla \cdot (D\nabla\phi) = S(\mathbf{r}, t, \phi)
$$
其中 $S$ 代表所有净源项。此方程的数学类型由其最[高阶导数](@entry_id:140882)项（即[主部](@entry_id:168896)）$\frac{1}{v}\frac{\partial \phi}{\partial t} - \nabla \cdot (D\nabla\phi)$ 决定。该方程在时间上是一阶导数，在空间上是二阶导数。这种类型的[偏微分](@entry_id:194612)方程被归类为**[抛物型方程](@entry_id:144670)** (parabolic equation)，其原型是[热传导方程](@entry_id:194763)。

[抛物型方程](@entry_id:144670)的性质对我们理解[扩散模型](@entry_id:142185)的物理意义和局限性至关重要：

1.  **[无限传播速度](@entry_id:178332)** (Infinite Propagation Speed)：抛物型方程的一个显著数学特征是，在任意时刻 $t=0$ 位于某点 $\mathbf{r}_0$ 的一个局部扰动，其影响会在任何无穷小的时间增量 $\delta t > 0$ 后瞬间传播到整个求解域。这意味着信息（或中子存在的概率）以无限大的速度传播。这显然与物理现实相悖，因为中子以有限的速度 $v$ 运动。这是扩散近似的一个根本性理论缺陷，表明它无法精确描述依赖于有限中子速度的[波前](@entry_id:197956)传播现象。

2.  **平滑效应** (Smoothing Effect)：抛物型算子具有强大的[平滑性质](@entry_id:145455)。即使初始条件 $\phi(\mathbf{r}, 0)$ 包含不连续或不可导的尖锐特征（例如，一个脉冲源），在任何 $t>0$ 的时刻，解 $\phi(\mathbf{r}, t)$ 在空间上都会变得无限光滑（即 $C^\infty$）。这意味着[扩散模型](@entry_id:142185)无法维持或传播尖锐的中子波前；任何尖锐的扰动都会被迅速地“模糊”或衰减掉。

尽管存在这些理论上的局限，但在许多实际应用中，扩散理论仍然是一个非常有效且计算成本相对较低的工具，特别是当系统的特征尺度远大于中子平均自由程时。

### [扩散近似](@entry_id:147930)的来源与有效性条件

扩散方程并非基本物理定律，而是对更精确的**[玻尔兹曼输运方程](@entry_id:140472)** (Boltzmann Transport Equation) 的一种近似。理解其推导过程有助于我们明确其适用范围。单能群下的[中子输运方程](@entry_id:1128709)描述了角通量密度 $\psi(\mathbf{r}, \boldsymbol{\Omega}, t)$ 的演化，它不仅依赖于位置 $\mathbf{r}$ 和时间 $t$，还依赖于中子的运动方向 $\boldsymbol{\Omega}$。

扩散理论可以通过对[输运方程](@entry_id:174281)取角度矩并引入**[P1近似](@entry_id:152048)** (P1 approximation) 来导出。首先，我们将[标量通量](@entry_id:1131249)密度 $\phi$ 和中子流密度 $\mathbf{J}$ 定义为角通量 $\psi$ 的零阶和一阶角度矩：
$$
\phi(\mathbf{r},t) = \int_{4\pi} \psi(\mathbf{r},\boldsymbol{\Omega},t) d\boldsymbol{\Omega}
$$
$$
\mathbf{J}(\mathbf{r},t) = \int_{4\pi} \boldsymbol{\Omega} \psi(\mathbf{r},\boldsymbol{\Omega},t) d\boldsymbol{\Omega}
$$
[P1近似](@entry_id:152048)假设角通量 $\psi$ 的角度依赖性是弱的，可以近似为一个各向同性部分和一个小的线性各向异性部分的和：
$$
\psi(\mathbf{r}, \boldsymbol{\Omega}, t) \approx \frac{1}{4\pi}\phi(\mathbf{r}, t) + \frac{3}{4\pi}\boldsymbol{\Omega}\cdot\mathbf{J}(\mathbf{r}, t)
$$
将此近似代入[输运方程](@entry_id:174281)的一阶[矩方程](@entry_id:149666)，并在某些条件下（特别是瞬态变化相比于碰撞频率足够慢），可以推导出菲克定律 $\mathbf{J} = -D\nabla\phi$，其中扩散系数 $D$ 与材料的**[输运截面](@entry_id:1133392)** (transport cross section) $\Sigma_{tr}$ 相关：
$$
D = \frac{1}{3\Sigma_{tr}} = \frac{1}{3(\Sigma_t - \bar{\mu}_0\Sigma_s)}
$$
这里 $\bar{\mu}_0$ 是实验室坐标系下散射角的平均余弦，它量化了散射的各向异性程度。只有在各向同性散射（$\bar{\mu}_0=0$）的特殊情况下，$\Sigma_{tr}$ 才等于总截面 $\Sigma_t$。

这个推导过程揭示了扩散理论成立所必须满足的一系列物理条件 ：

1.  **介质[光学厚度](@entry_id:150612)大** (Optically Thick Medium)：系统尺寸 $L$ 必须远大于中子的**输运平均自由程** $\lambda_{tr} = 1/\Sigma_{tr}$，即 $L/\lambda_{tr} \gg 1$。这意味着中子在穿过系统或被吸收之前，会经历多次有效的方向[随机化](@entry_id:198186)散射。这保证了中子[角分布](@entry_id:193827)趋于各向同性。

2.  **散射主导** (Scattering-Dominated)：散射概率应远大于[吸收概率](@entry_id:265511)，即散射比 $c = \Sigma_s / \Sigma_t \approx 1$。强散射是驱动角通量趋于各向同性的基本机制。在吸收远大于散射的介质中，中子在被吸收前没有足够的机会通过散射来“忘记”其原始方向，导致角通量高度各向异性，[扩散近似](@entry_id:147930)失效。

3.  **通量梯度缓变** (Slowly Varying Flux)：通量密度的空间变化必须是缓慢的，其特征长度 $L_g \sim \phi/|\nabla\phi|$ 必须远大于输运平均自由程 $\lambda_{tr}$。即 $\frac{|\nabla\phi|}{\phi} \ll \Sigma_{tr}$。这是[P1近似](@entry_id:152048)（即角通量仅有微弱各向异性）成立的直接要求。

4.  **时间演化缓慢** (Slowly Varying in Time)：中子场的瞬态变化必须足够慢。具体来说，变化的特征时间尺度 $T$ 必须远大于中子两次碰撞之间的平均时间，即 $T \gg 1/(v\Sigma_t)$。这保证了在系统宏观状态发生显著变化之前，中子[角分布](@entry_id:193827)有足够的时间弛豫到准平衡的、接近各向同性的状态。

扩散理论不适用于强吸收区域、材料界面附近、真空边界附近以及远离中子源的[深穿透问题](@entry_id:1123478)，因为在这些情况下，上述一个或多个条件通常不被满足。

### 反应堆动力学与反馈机制

当我们将扩散方程应用于整个反应堆时，必须考虑[中子产生](@entry_id:1128705)和损失过程中的时间延迟和温度效应，这些是[反应堆动力学](@entry_id:1130674)的核心。

#### 缓发中子

裂变产生的中子并非全部瞬时释放。一小部分（通常小于1%）是由裂变产物（称为**缓发中子先驱核** (delayed neutron precursors)）在裂变发生后经由放射性衰变而释放的，这些中子称为**缓发中子** (delayed neutrons)。尽管份额很小，但它们的存在极大地延长了链式反应的有效[中子代时间](@entry_id:1128698)，使得反应堆控制成为可能。

为了在扩散方程中包含缓发中子，我们需要为每一类（共 $I$ 类）先驱核 $C_i(\mathbf{r}, t)$ 引入一个平衡方程：
$$
\frac{\partial C_i(\mathbf{r}, t)}{\partial t} = \beta_i \sum_{h=1}^{G} \nu_h \Sigma_{f,h}(\mathbf{r})\phi_h(\mathbf{r}, t) - \lambda_i C_i(\mathbf{r}, t), \quad i=1,\dots,I
$$
这里，$\beta_i$ 是第 $i$ 类缓发中子在总裂变中子中所占的份额，$\lambda_i$ 是其[衰变常数](@entry_id:149530)。总的缓发中子份额为 $\beta = \sum_i \beta_i$。缓发中子作为源项加入到中子扩散方程中，其贡献为 $\sum_{i=1}^{I} \lambda_i C_i(\mathbf{r}, t)$（假设缓发中子也遵循裂变谱 $\chi_g$）。同时，[瞬发中子](@entry_id:161367)源项需要乘以因子 $(1-\beta)$。

缓发中子系统的动态响应可以通过**传递函数** (transfer function) 来表征。例如，考虑一个单缓发中子群组的情况，我们可以通过对先驱核平衡方程进行线性化和拉普拉斯变换，推导出裂变源扰动 $\delta F(s)$ 与缓发中子源扰动 $\delta S_d(s)$ 之间的传递函数：
$$
G(s) = \frac{\delta S_d(s)}{\delta F(s)} = \frac{\lambda \beta}{s + \lambda}
$$
这表示缓发中子系统是一个一阶滞后环节，其时间常数由[衰变常数](@entry_id:149530) $\lambda$ 决定，其增益与[缓发中子份额](@entry_id:158691) $\beta$ 成正比。

#### 温度反馈与[多普勒效应](@entry_id:160624)

反应堆的核截面（特别是吸收和裂变[截面](@entry_id:154995)）依赖于材料的温度，这种依赖性构成了最重要的**[反应性反馈机制](@entry_id:1130663)** (reactivity feedback mechanisms)。其中，**[多普勒效应](@entry_id:160624)** (Doppler effect) 或多普勒展宽是轻水堆等[热中子](@entry_id:270226)反应堆中最关键的瞬发负反馈机制。

其物理原理如下：燃料（如 $^{238}\text{U}$）的吸收截面在特定能量处存在极高的峰值，称为**共振峰** (resonances)。当燃料温度升高时，燃料核的热运动加剧。对于一个向运动原子核飞来的中子，其感受到的相对能量会发生变化。这种效应导致原本尖锐的[共振峰](@entry_id:271281)在能量上被“展宽”。虽然峰值高度降低，但共振峰的总宽度增加，使得能量处于[共振峰](@entry_id:271281)“翼部”的中子有更高的概率被吸收。在存在**自屏效应** (self-shielding) 的燃料块中，共振峰中心的中子通量已经很低，因此展宽导致的翼部吸收增加效应超过了峰值降低的效应，净结果是总的[共振吸收](@entry_id:1130936)增加。

由于 $^{238}\text{U}$ 的[共振吸收](@entry_id:1130936)主要发生在超热能区，[多普勒效应](@entry_id:160624)导致中子被非裂变材料吸收的概率增加，从而引入负反应性，起到抑制功率上升的自稳定作用。

在扩散模型中，这种效应被表征为一个温度依赖的宏观[吸收截面](@entry_id:172609) $\Sigma_a(T)$。基于共振峰有效宽度与绝对温度 $T$ 的平方根成正比的物理原理，一个常用的、物理基础扎实的[多普勒反馈](@entry_id:1123930)模型为：
$$
\Sigma_{a}(T(t)) = \Sigma_{a,\mathrm{ref}} \left[ 1 + \beta_{D}\left( \sqrt{ \frac{T(t)}{T_{\mathrm{ref}}} } - 1 \right) \right]
$$
其中 $\Sigma_{a,\mathrm{ref}}$ 是在参考温度 $T_{\mathrm{ref}}$ 下的吸收截面，$\beta_D > 0$ 是一个无量纲的、量化多普勒效应强度的系数。这种温度依赖性使得[扩散方程](@entry_id:170713)变为[非线性](@entry_id:637147)，因为温度 $T(\mathbf{r}, t)$ 本身又由中子通量 $\phi(\mathbf{r}, t)$ 产生的裂变功率决定。

### 从[时空动力学](@entry_id:1132003)到[点动力学](@entry_id:1129859)

求解完整的时空[瞬态扩散](@entry_id:154656)方程组计算量巨大。在许多情况下，尤其是在分析整个反应堆系统的全局动态响应时，可以采用一个重要的简化模型——**[点动力学](@entry_id:1129859)近似** (point kinetics approximation)。

#### [点动力学](@entry_id:1129859)近似的理据与误差

[点动力学](@entry_id:1129859)近似的核心假设是，中子通量密度在瞬态过程中的空间形状保持不变，其时间行为可以与[空间分布](@entry_id:188271)分离，即**形状函数** (shape function) $\varphi(\mathbf{r})$ 和**幅度函数** (amplitude function) $P(t)$ 的乘积：
$$
\phi(\mathbf{r}, t) \approx P(t)\varphi(\mathbf{r})
$$
这个假设的合理性可以从[谱理论](@entry_id:275351)的角度来理解。对于一个均匀裸堆，[扩散算子](@entry_id:136699) $D\nabla^2 + (\nu\Sigma_f - \Sigma_a)$ 的[本征函数](@entry_id:154705)（或称模式）构成一个完备[正交基](@entry_id:264024)。任何初始通量分布 $\phi(\mathbf{r}, 0)$ 都可以展开为这些[本征模](@entry_id:174677)式的线性叠加。每个模式 $n$ 都对应一个时间演化的本征值 $\omega_n$。由于泄漏随着模式阶数 $n$ 的增加而急剧增加，高阶模式的时间本征值 $\omega_n$ 通常远小于基频模式的本征值 $\omega_1$（即 $\omega_1 > \omega_2 > \omega_3 > \dots$）。

因此，通量的精确解可以写成：
$$
\phi(\mathbf{r},t) = \sum_{n=1}^\infty c_n e^{\omega_n t} \varphi_n(\mathbf{r}) = e^{\omega_1 t} \left[ c_1 \varphi_1(\mathbf{r}) + \sum_{n=2}^\infty c_n e^{(\omega_n - \omega_1)t} \varphi_n(\mathbf{r}) \right]
$$
由于 $\omega_n - \omega_1  0$ 对所有 $n>1$ 成立，[高阶模](@entry_id:750331)式项 $e^{(\omega_n - \omega_1)t}$ 会随着时间的推移而指数衰减。只要初始通量分布中包含[基频](@entry_id:268182)模式的成分（即 $c_1 \neq 0$），在经过一段初始的形状弛豫时间后，[高阶模](@entry_id:750331)式的贡献将变得微不足道，通量的形状将趋近于基频模式 $\varphi_1(\mathbf{r})$。此时，$\phi(\mathbf{r}, t) \approx (c_1 e^{\omega_1 t})\varphi_1(\mathbf{r})$，形状[函数近似](@entry_id:141329)成立。

忽略形状变化引入的误差大小，取决于高阶模式的相对幅度和衰减速率。我们可以定义一个量化误差的度量，例如近似解与精确解之差的 $L^2$ 范数与精确解 $L^2$ 范数的比值。这个误差在初始时刻最大（如果初始形状不是纯[基频](@entry_id:268182)模式），并随着时间推移而减小。

#### [点动力学](@entry_id:1129859)近似的失效

然而，当存在空间依赖的反馈时，[点动力学](@entry_id:1129859)近似的根基——形状函数不变假设——会受到挑战。例如，在发生功率瞬态时，功率（因而温度）在堆芯中心的增加幅度远大于边缘。这导致多普勒效应在堆芯中心更强，[吸收截面](@entry_id:172609)的增加也更显著。这种空间非均匀的[截面](@entry_id:154995)变化 $\delta\Sigma(\mathbf{r}, t)$ 相当于在[扩散方程](@entry_id:170713)中引入了一个空间依赖的扰动算子。

当这个扰动算子作用于[基频](@entry_id:268182)模式 $\varphi_1(\mathbf{r})$ 时，其产生的“源项” $\delta\Sigma(\mathbf{r}, t)\varphi_1(\mathbf{r})$ 的空间形状通常不再是 $\varphi_1(\mathbf{r})$ 本身。这个新的源项会激发高阶空间模式，导致通量的实际形状发生畸变，从而破坏了通量形状与时间的可分离性。

尽管如此，[点动力学](@entry_id:1129859)在许多情况下仍然是一个足够好的近似。其适用性取决于两个关键因素的权衡：

1.  **时间尺度分离**：如果由反馈引起的扰动（如温度变化）演化得非常缓慢，而高阶中子通量模式的弛豫（衰减）速度非常快，那么[高阶模](@entry_id:750331)式就没有足够的时间增长到显著的幅度。即，形状[弛豫时间](@entry_id:191572) $\tau_s$ 远小于[热反馈](@entry_id:1132998)特征时间 $\tau_T$。

2.  **空间扰动幅度**：如果反应性扰动的空间非均匀性很小，那么其激发[高阶模](@entry_id:750331)式的能力就很弱。可以用反应性扰动分布的加[权空间](@entry_id:195741)方差来衡量这种非均匀性。如果方差相对于平均扰动值很小，那么通量形状的变化也相应很小。

因此，[点动力学](@entry_id:1129859)的有效性不仅仅取决于反应堆的固有属性（如本征值间隔），还取决于瞬态过程中扰动本身的性质（幅度、空间分布和时间尺度）。

### 高级主题：伴随方程

在[瞬态分析](@entry_id:262795)和灵敏度研究中，**伴随方程** (adjoint equation) 是一个极其强大的数学工具。对于一个由前向扩散方程描述的系统，我们可以定义一个相应的伴随[扩散方程](@entry_id:170713)，其解 $\phi^\dagger(\mathbf{r}, t)$ 具有特殊的物理意义。

考虑一个我们关心的物理量 $R$，它是在终端时刻 $t_R$ 对中子通量进行某种加权积分得到的结果（例如，某个探测器的总计数）：
$$
R = \int_V \Sigma_d(\mathbf{r}) \phi(\mathbf{r}, t_R) dV
$$
其中 $\Sigma_d(\mathbf{r})$ 是探测器[响应函数](@entry_id:142629)或权重。对应的[单群](@entry_id:140851)瞬态伴随[扩散方程](@entry_id:170713)可以推导为：
$$
-\frac{1}{v}\frac{\partial \phi^\dagger(\mathbf{r}, t)}{\partial t} - \nabla \cdot \big(D(\mathbf{r}) \nabla \phi^\dagger(\mathbf{r}, t)\big) + (\Sigma_a(\mathbf{r}) - \nu\Sigma_f(\mathbf{r}))\phi^\dagger(\mathbf{r}, t) = S^\dagger(\mathbf{r}, t)
$$
这个方程有几个显著特点：

*   **时间反演**：时间导数项的符号为负，表明伴随方程本质上是“向后”求解的，从终端时刻 $t_R$ 演化回初始时刻。
*   **[伴随算子](@entry_id:140236)**：空间算子部分与前向方程中的算子互为伴随（对于实数[截面](@entry_id:154995)，扩散和反应算子是自伴的）。
*   **伴随源与终端条件**：伴随源 $S^\dagger$ 由我们所关心的响应 $R$ 决定。对于上述终端响应 $R$，伴随方程的源项 $S^\dagger$ 为零，但需要在最终时刻 $t_R$ 施加一个“终端条件” $\phi^\dagger(\mathbf{r}, t_R) = \Sigma_d(\mathbf{r})$。