## 引言
在航空航天、能源工程及诸多前沿科学领域，辐射传热是决定系统性能与安全性的关键物理过程。精确描述辐射能量在参与性介质中的吸收、发射和散射，依赖于求解复杂的积分-[微分](@entry_id:158422)方程——辐射传递方程（RTE）。然而，直接求解RTE在计算上极为昂贵，这催生了多种近似模型。工程师和研究者面临的核心挑战是：如何在计算成本和物理精度之间做出权衡，为特定问题选择最合适的辐射模型？这正是本文旨在解决的知识鸿沟。

本文将系统地引导您掌握两种主流的辐射计算方法：[P1近似](@entry_id:152048)模型和离散坐标法（DOM）。在“原理与机制”一章中，我们将从第一性原理出发，深入剖析这两种方法的数学推导、物理假设和内在局限性。随后，在“应用与跨学科联系”一章，我们将把理论付诸实践，探讨这些模型在解决高超声速热防护、燃烧火焰模拟等尖端工程问题中的具体应用，并建立一个实用的模型选择框架。最后，通过“动手实践”部分的系列练习，您将有机会亲手操作和验证所学概念，从而将理论知识内化为解决实际问题的能力。

## 原理与机制

本章深入探讨求解辐射传递方程（Radiative Transfer Equation, RTE）的两种核心方法——[P1近似](@entry_id:152048)模型和离散坐标法（Discrete Ordinates Method, DOM）的物理原理与数值机制。我们将从[辐射场](@entry_id:164265)的物理量定义出发，构建辐射传递的基本方程，随后详细推导并剖析这两种方法的数学形式、物理假设、适用范围及其在计算实践中面临的挑战与解决方案。

### 辐射传递方程（RTE）：理论基石

#### 辐射强度与辐射热流

[辐射场](@entry_id:164265)的描述始于一个最基本的物理量——**光[谱辐射强度](@entry_id:148916)** (spectral radiative intensity)，记为 $I(\mathbf{x}, \mathbf{s}, \lambda)$。它被定义为在空间位置 $\mathbf{x}$，沿特定方向 $\mathbf{s}$，单位时间内穿过垂直于 $\mathbf{s}$ 方向的单位投影面积，单位立体角内，以及单位波长间隔内的辐射能量。其单位为 $\mathrm{W} \cdot \mathrm{m}^{-2} \cdot \mathrm{sr}^{-1} \cdot \mathrm{m}^{-1}$。[辐射强度](@entry_id:150179)是描述[辐射场](@entry_id:164265)的方[向性](@entry_id:144651)和光谱依赖性的最完备的量，它包含了辐射场在某一点所有方向和所有波长的全部信息。

与辐射强度不同，**辐射热流矢量** (radiative heat flux vector) $\mathbf{q}_r(\mathbf{x})$ 是一个宏观的、积分性的物理量，代表在位置 $\mathbf{x}$ 处单位面积上的[净辐射](@entry_id:1128562)能流。它通过对光[谱辐射强度](@entry_id:148916)在所有方向（$4\pi$ 球面立体角）和所有波长上进行积分得到：

$$
\mathbf{q}_r(\mathbf{x}) = \int_{0}^{\infty} \int_{4\pi} I(\mathbf{x}, \mathbf{s}, \lambda) \mathbf{s} \, \mathrm{d}\Omega \, \mathrm{d}\lambda
$$

其中 $\mathrm{d}\Omega$ 是[立体角](@entry_id:154756)微元。此积分是强度的“一阶角矩”。从单位上看，$\mathbf{q}_r(\mathbf{x})$ 的单位是 $\mathrm{W} \cdot \mathrm{m}^{-2}$，这符合其作为能量通量的物理意义。通过某一个具有[单位法向量](@entry_id:178851) $\mathbf{n}$ 的表面的净标量热流，是辐射热流矢量在该法向上的投影，即 $\mathbf{n} \cdot \mathbf{q}_r(\mathbf{x})$，它由以下积分给出：

$$
\mathbf{n} \cdot \mathbf{q}_r(\mathbf{x}) = \int_{0}^{\infty} \int_{4\pi} I(\mathbf{x}, \mathbf{s}, \lambda) (\mathbf{s} \cdot \mathbf{n}) \, \mathrm{d}\Omega \, \mathrm{d}\lambda
$$

此表达式明确显示，辐射强度 $I$ 是方向性的，而热流是通过对所有方向的贡献进行加权（投影因子 $\mathbf{s} \cdot \mathbf{n}$）积分得到的。

#### RTE的建立与源项

辐射传递方程是[辐射强度](@entry_id:150179)沿光线路径的能量守恒方程。它描述了强度由于与介质的相互作用（吸收、发射和散射）而发生的变化。对于一个[稳态](@entry_id:139253)的、参与辐射的介质，单色RTE可以写作：

$$
\mathbf{s} \cdot \nabla I_\lambda(\mathbf{x}, \mathbf{s}) = j_\lambda - \kappa_\lambda I_\lambda(\mathbf{x}, \mathbf{s}) - \sigma_{s,\lambda} I_\lambda(\mathbf{x}, \mathbf{s}) + \frac{\sigma_{s,\lambda}}{4\pi} \int_{4\pi} I_\lambda(\mathbf{x}, \mathbf{s}') \Phi_\lambda(\mathbf{s}', \mathbf{s}) \, \mathrm{d}\Omega'
$$

其中，左侧的 $\mathbf{s} \cdot \nabla I_\lambda$ 是**流输项** (streaming term)，表示强度沿方向 $\mathbf{s}$ 的空间变化。右侧各项描述了与介质的相互作用：
- **发射 (Emission)**: $j_\lambda$ 是光谱发射系数。在**[局部热力学平衡](@entry_id:147993)** (Local Thermodynamic Equilibrium, LTE) 假设下，发射与吸收通过基尔霍夫定律联系起来，$j_\lambda = \kappa_\lambda I_{b,\lambda}(T)$。这里的 $\kappa_\lambda$ 是光谱[吸收系数](@entry_id:156541)，$I_{b,\lambda}(T)$ 是**普朗克黑体辐射强度** (Planck blackbody intensity)，由普朗克定律给出：
  $$
  I_{b,\lambda}(T) = \frac{2 h c^2}{\lambda^5} \left[ \exp\left(\frac{hc}{\lambda k_B T}\right) - 1 \right]^{-1}
  $$
  其中 $h$ 是普朗克常数，$c$ 是光速，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是介质的局部温度。这个函数描述了在温度 $T$ 下，一个理想黑体在波长 $\lambda$ 处所能发射的最大辐射强度。 在许多工程应用中，为了简化计算，会采用**灰体假设** (gray assumption)，即假定辐射物性（如吸收系数和发射率）在整个光谱上是常数。在这种情况下，我们可以使用积分后的总黑体强度 $I_b(T) = \int_0^\infty I_{b,\lambda}(T) d\lambda = \frac{\sigma T^4}{\pi}$，其中 $\sigma$ 是斯特藩-[玻尔兹曼常数](@entry_id:142384)。灰体假设在气体或表面的辐射物性在热辐射主要波段内变化不大时是合理的，例如在含有大量烟尘或烧蚀颗粒的火箭尾焰中，[连续谱](@entry_id:155477)辐射占主导。

- **吸收 (Absorption)**: $-\kappa_\lambda I_\lambda$ 表示辐射束由于被介质吸收而损失的能量。

- **外散射 (Out-scattering)**: $-\sigma_{s,\lambda} I_\lambda$ 表示辐射束由于被散射出当前方向 $\mathbf{s}$ 而损失的能量，其中 $\sigma_{s,\lambda}$ 是光谱散射系数。

- **内散射 (In-scattering)**: 最后一项表示从所有其他方向 $\mathbf{s}'$ 散射进入当前方向 $\mathbf{s}$ 的能量增益。$\Phi_\lambda(\mathbf{s}', \mathbf{s})$ 是**[散射相函数](@entry_id:1131288)**，描述了能量从方向 $\mathbf{s}'$ 散射到方向 $\mathbf{s}$ 的概率分布。对于最简单的**各向同性散射** (isotropic scattering)，$\Phi_\lambda = 1$。

#### 单次散射反照率与瞬态效应

我们可以将吸收和散射损失项合并，定义**[消光系数](@entry_id:270201)** (extinction coefficient) $\beta_\lambda = \kappa_\lambda + \sigma_{s,\lambda}$。同时，一个关键的无量纲参数是**[单次散射反照率](@entry_id:1131707)** (single-scattering albedo) $\omega_\lambda$：

$$
\omega_\lambda = \frac{\sigma_{s,\lambda}}{\kappa_\lambda + \sigma_{s,\lambda}}
$$

$\omega_\lambda$ 量化了消光过程中由散射所占的比例。$\omega_\lambda = 0$ 表示纯吸收介质，而 $\omega_\lambda = 1$ 表示纯散射介质。利用 $\omega_\lambda$，RTE可以重写为：

$$
\mathbf{s} \cdot \nabla I_\lambda = -\beta_\lambda I_\lambda + (1-\omega_\lambda)\beta_\lambda I_{b,\lambda} + \frac{\omega_\lambda \beta_\lambda}{4\pi} \int_{4\pi} I_\lambda(\mathbf{s}') \Phi_\lambda(\mathbf{s}', \mathbf{s}) \, \mathrm{d}\Omega'
$$

这个形式清楚地展示了 $\omega_\lambda$ 如何调控吸收/发射与散射之间的平衡。当 $\omega_\lambda \to 1$ 时，吸收和发射项消失，RTE变为一个纯粹的散射-[输运方程](@entry_id:174281)，辐射能量在介质中被重新分布，但不会与介质发生净能量交换。

在许多[高超声速CFD](@entry_id:750485)应用中，我们处理的是流场的[稳态](@entry_id:139253)或准[稳态](@entry_id:139253)演化。RTE的完整形式还应包含一个**瞬态项** $\frac{1}{c}\frac{\partial I_\lambda}{\partial t}$。通过[量纲分析](@entry_id:140259)可以判断该项的重要性。辐射场在长度为 $L$ 的区域内达到平衡所需的时间尺度 $t_{\text{rad}}$ 约为 $\max(L/c, \tau_\lambda L/c)$，其中 $\tau_\lambda = \beta_\lambda L$ 是光学厚度。而流场的特征时间尺度 $T_{\text{flow}}$（例如 $L/V_{\text{flow}}$）通常要大得多。由于光速 $c$ 极大，辐射场的建立（即使在[光学厚介质](@entry_id:752966)中，其扩散时间也远小于流场时间）相对于流场性质（如温度、密度）的变化几乎是瞬时的。因此，只要满足 $t_{\text{rad}} \ll T_{\text{flow}}$，即 $\frac{\tau_\lambda L}{c T_{\text{flow}}} \ll 1$，我们就可以忽略RTE中的瞬态项，采用**准稳态近似** (quasi-steady approximation)，这在绝大多数[航空航天CFD](@entry_id:746330)模拟中是成立的。

### P1[球谐函数](@entry_id:178380)模型：一种[扩散近似](@entry_id:147930)

求解包含复杂角度和光谱依赖性的RTE在计算上是极其昂贵的。P1球谐函数模型是一种[矩方法](@entry_id:277025)，它通过将[辐射强度](@entry_id:150179)的角度依赖性截断为线性函数来简化问题。

#### P1模型的推导

[P1近似](@entry_id:152048)假设辐射强度可以表示为：

$$
I(\mathbf{x}, \mathbf{s}, t) \approx \frac{1}{4\pi} \phi(\mathbf{x}, t) + \frac{3}{4\pi} \mathbf{q}_r(\mathbf{x}, t) \cdot \mathbf{s}
$$

其中，$\phi$ 是标量[辐射通量](@entry_id:151732)（即入射辐射 $G$），$\mathbf{q}_r$ 是辐射热流矢量。该近似的物理意义是辐射场是近各向同性的。

为了推导P1模型的主控方程，我们对瞬态RTE取零阶和一阶角矩。
1.  对RTE进行全角积分（零阶矩），得到辐射能量守恒方程：
    $$
    \frac{1}{c}\frac{\partial \phi}{\partial t} + \nabla \cdot \mathbf{q}_r + \kappa_a \phi = 4\pi\kappa_a I_b
    $$
2.  将RTE乘以 $\mathbf{s}$ 再进行全角积分（一阶矩），并利用[爱丁顿近似](@entry_id:161362)（Eddington approximation）进行封闭，即 $\int_{4\pi} I (\mathbf{s} \otimes \mathbf{s}) d\Omega \approx \frac{1}{3} \phi \boldsymbol{\delta}$（其中 $\boldsymbol{\delta}$ 是单位张量），得到动量方程。在忽略通量的时间导数项（[扩散近似](@entry_id:147930)）后，可得到**菲克辐射定律** (Fick's law of radiation)：
    $$
    \mathbf{q}_r = -\frac{1}{3\beta} \nabla\phi = -D \nabla\phi
    $$
    这里，$D = \frac{1}{3\beta} = \frac{1}{3(\kappa_a + \sigma_s)}$ 被称为**[辐射扩散](@entry_id:158401)系数** (radiation diffusion coefficient)。

将[菲克定律](@entry_id:155177)代入[能量守恒方程](@entry_id:748978)，便得到了P1模型的最终形式——一个关于标量通量 $\phi$ 的扩散型方程：
$$
\frac{1}{c}\frac{\partial \phi}{\partial t} - \nabla \cdot (D \nabla \phi) + \kappa_a \phi = 4\pi\kappa_a I_b
$$
这个方程在形式上类似于[热传导方程](@entry_id:194763)，将复杂的角度依赖问题转化为了一个相对简单的标量场求解问题。例如，在一个空间均匀、初始为零的介质中，温度瞬时升高，使 $I_b$ 变为常数 $I_{b,0}$。此时，空间梯度为零，上述方程简化为一个[常微分方程](@entry_id:147024)，其解为 $\phi(t) = \frac{4\pi\kappa_a I_{b,0}}{\kappa_a}(1 - \exp(-c\kappa_a t))$，描述了辐射场弛豫到新[平衡态](@entry_id:270364)的过程。

#### P1模型的局限性

P1模型的[计算效率](@entry_id:270255)很高，但在其基本假设（辐射场近各向同性）不成立时，会产生严重的物理偏差。这通常发生在**光学薄** ($\beta L \ll 1$) 或存在**强各向异性源**（如准直光束）的区域。

考虑一个典型的基准问题：一束准直光束 $I(0, \mu) = I_0 \delta(\mu-1)$ 垂直入射到一个纯吸收介质中。精确解是 $I(x, \mu) = I_0 \exp(-\beta x) \delta(\mu-1)$，即强度仅在 $\mu=1$ 方向存在，并按指数衰减。然而，P1模型试图用一个线性函数 $I_{P1}(x, \mu) = A(x) + B(x)\mu$ 来拟合这个由狄拉克 $\delta$ 函数描述的、高度各向异性的场。为了匹配精确解的零阶和一阶矩，[P1近似](@entry_id:152048)会得到 $I_{P1}(x, \mu) = \frac{I_0}{2}\exp(-\beta x)(1+3\mu)$。这个线性函数在某些后向方向（$\mu  -1/3$）会取负值，例如在 $\mu=-1$ 方向，P1预测的强度为 $I_{P1}(x, -1) = -I_0 \exp(-\beta x)$，这在物理上是荒谬的，因为辐射强度不能为负。在光学薄的情况下，例如[光学厚度](@entry_id:150612) $\tau = \beta L = 0.2$ 的平板中心 $x=L/2$ 处，P1模型在后向的相对误差可高达 $\exp(-0.1) \approx 0.9048$，即超过90%。这个例子鲜明地揭示了P1模型在处理强各向异性问题时的根本缺陷。

### 离散坐标法（DOM）：一种输运方法

离散坐标法（DOM或$S_N$方法）是求解RTE的另一种主流方法。它不改变RTE的物理形式，而是通过数值方法直接处理其角度依赖性。

#### 离散化原理

DOM的核心思想是将[辐射强度](@entry_id:150179)所依赖的连续角度空间（$4\pi$ 球面）用一组离散的方向（坐标）$\{\mathbf{s}_m\}_{m=1}^M$ 和相应的权重 $\{w_m\}_{m=1}^M$ 来代替。这样，RTE中的积分项就被替换为求积和：

$$
\int_{4\pi} f(\mathbf{s}) \, \mathrm{d}\Omega \approx \sum_{m=1}^{M} w_m f(\mathbf{s}_m)
$$

应用到RTE的散射源项中，原来的积分-[微分](@entry_id:158422)方程就转化为一个关于各个离散方向强度 $I_m(\mathbf{x}) = I(\mathbf{x}, \mathbf{s}_m)$ 的[耦合偏微分方程组](@entry_id:198181)。例如，在DOM中，辐射热流的计算也变为求和形式：

$$
\mathbf{q}_r(\mathbf{x}) \approx \int_0^\infty \sum_{m=1}^{M} w_m I(\mathbf{x}, \mathbf{s}_m, \lambda) \mathbf{s}_m \, \mathrm{d}\lambda
$$

#### [求积组](@entry_id:156430)的要求与$S_N$方法

为了保证数值解的物理一致性，[求积组](@entry_id:156430) $(\{\mathbf{s}_m\}, \{w_m\})$ 必须满足一些基本要求。最重要的是，它必须能精确积分低阶球谐函数，以保证对简单物理场的正确描述。例如，对于一个各向同性的辐射场 $I(\mathbf{x}, \mathbf{s}) = I_0$，求积必须能精确地给出其标量通量 $\phi = 4\pi I_0$ 和零热流 $\mathbf{q}_r = \mathbf{0}$。这导出了两个基本约束条件：
1.  **零阶矩守恒**: $\sum_{m=1}^{M} w_m = 4\pi$
2.  **一阶矩守恒**: $\sum_{m=1}^{M} w_m \mathbf{s}_m = \mathbf{0}$

$S_N$ 方法是一类广泛使用的、满足这些及更[高阶矩](@entry_id:266936)和对称性要求的**[水平对称求积](@entry_id:1127172)组** (level-symmetric quadrature sets)。在三维空间中，参数 $N$（一个偶数）决定了[求积组](@entry_id:156430)的阶数。总方向数 $M$ 通常由公式 $M = N(N+2)$ 给出。例如，$S_4$ [求积组](@entry_id:156430)包含 $4(4+2)=24$ 个方向，$S_8$ 包含 $8(8+2)=80$ 个方向。增加 $N$ 可以提供更精细的角度分辨率，从而更准确地描述复杂的各向异性[辐射场](@entry_id:164265)。

#### 数值实现与挑战

在DOM中，对于每个离散方向 $\mathbf{s}_m$，RTE变成一个双曲型（输运型）方程。在[有限体积法](@entry_id:141374)框架下，流输项 $\mathbf{s}_m \cdot \nabla I_m$ 的离散化是关键。通过高斯散度定理，体积积分可以转化为[面积分](@entry_id:275394)。为保证数值稳定性，必须采用**迎风格式** (upwind differencing)。这意味着在计算通过某个单元交界面的通量时，界面上的强度值应取自上游（或“[迎风](@entry_id:756372)”方向）的单元。这种处理方式尊重了[双曲型方程](@entry_id:145657)中信息沿特征线（即辐射方向 $\mathbf{s}_m$）传播的物理特性。这与P1模型中扩散项通常采用[中心差分](@entry_id:173198)形成鲜明对比，后者反映了椭圆型方程中信息向各个方向传播的特性。

尽管DOM比P1模型更具普适性，但它在实践中也面临挑战：
- **射线效应 (Ray Effects)**: 这是DOM最典型的数值伪影。由于角度空间被离散化，辐射能量只能沿有限的几个方向传播。在[光学薄介质](@entry_id:1129156)中，来自点源或小面源的辐射会沿着这些离散方向形成不真实的条纹，而在方向之间则出现虚假的“阴影区”。这是角度离散化误差的直接体现。
- **计算成本**: DOM的计算量与方向数 $M$ 和空间网格单元数成正比。提高 $S_N$ 的阶数 $N$ 是缓解射线效应最直接的方法，但这会导致计算成本显著增加（大约与 $N^2$ 成正比）。因此，需要在精度和成本之间进行权衡。
- **迭代收敛性**: 在散射占主导（即单次散射反照率 $\omega_\lambda \to 1$）的问题中，各个方向的[辐射场](@entry_id:164265)通过散射源项强耦合。标准的源迭代法（一种简单的迭代求解策略）的收敛速度会变得极其缓慢。这是因为信息通过散射在角度空间中的传播效率很低。在这种情况下，必须使用如**[扩散综合加速](@entry_id:1123717)** (Diffusion Synthetic Acceleration, DSA) 等高级加速技术来保证计算效率。

#### 射线效应的缓解策略

除了暴力增加 $S_N$ 阶数外，还存在一些更巧妙的策略来缓解射线效应，而无需承担过高的计算代价：
- **[旋转求积](@entry_id:1131113)组 (Rotating Quadrature Sets)**: 在求解[稳态](@entry_id:139253)问题的迭代过程中，可以在每次迭代（或伪时间步）之间对整个[求积组](@entry_id:156430)进行一次小的刚性旋转。这样，在整个求解过程中，辐射场实际上是在更多样化的方向上被采样的，相当于一种“角度[抖动](@entry_id:200248)”，可以有效地平滑掉由固定方向引起的[条纹伪影](@entry_id:917135)。由于每次迭代的计算量并未增加，这种方法能以很小的额外开销显著改善解的质量。
- **[混合方法](@entry_id:163463) (Hybrid Methods)**: 这种方法结合了P1和DOM的优点。在辐射场近各向同性的光学厚区域，使用计算成本低的P1模型；而在辐射场具有强方向性的光学薄区域，使用更精确但昂贵的$S_N$方法。通过对计算域进行分区，这种混合策略可以在保证关键区域精度的同时，大幅降低整体计算成本，并避免了全局使用P1可能导致的物理失真。

综上所述，P1模型和离散坐标法为辐射传递问题提供了从扩散近似到精确输运的不同层次的解决方案。深刻理解它们的物理假设、数学结构和数值特性，是选择和应用恰当辐射模型来解决复杂航空航天热流问题的关键。