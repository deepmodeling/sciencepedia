## 引言
某些流体在极低温度下能够无粘性地流动，这种被称为超流性的状态，挑战了我们关于液体的经典直觉。传统的单个分子混乱海洋模型无法解释像[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)这样的物质如何能够爬上壁面并穿过极其微小的裂缝。本文旨在通过介绍由 Lev Landau 开创的革命性视角来弥补这一认知空白：即不通过其粒子，而是通过其被称为[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)的集体量子化运动来理解流体。在接下来的章节中，我们将首先深入“原理与机制”，认识其中的关键角色——[声子和旋子](@keyword=phonons_and_rotons|lang=zh-CN|style=Feynman)，并学习它们独特的能量-动量关系如何决定了[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)的规则。随后，“应用与跨学科联系”一章将揭示这些微观[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)如何表现为惊人的宏观效应，从温度波到壮观的喷泉，以及它们的核心概念如何在其他奇异的量子系统中得到体现。

## 原理与机制

要理解[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)这个奇特而美丽的世界，我们必须改变对液体的思考方式。对于像水一样的普通流体，我们想象的是一个由单个分子组成的混乱群体，它们相互碰撞、推挤，从而产生了粘性等性质。但在寒冷的[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)所处的量子领域，这幅图景失效了。伟大的物理学家 Lev Landau 教导我们，应该转而关注整个流体的集体、有序的运动。这些运动并非随机的[抖动](@keyword=dither|lang=zh-CN|style=Feynman)，而是量子化的[运动波](@keyword=kinematic_wave|lang=zh-CN|style=Feynman)，我们可以将其视为独立的粒子。我们称之为**[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)**或**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**。它们是这种[量子液体](@keyword=quantum_liquids|lang=zh-CN|style=Feynman)的真正居民，而[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)的故事就是它们的故事。

### 无阻力流动的秘密：[朗道临界速度](@keyword=landau_critical_velocity|lang=zh-CN|style=Feynman)

流体如何能完全无摩擦地流动？想象一下，在一片完全静止的池塘中非常缓慢地拖动一把勺子。如果移动得足够慢，就不会产生涟漪，勺子几乎感觉不到因产生波浪而带来的阻力。要产生一个波，勺子必须为其提供一定的能量 $E$ 和动量 $p$。Landau 的关键洞见在于，这种能量和动量的传递只有在勺子的速度 $v$ 大于波的能量动量比 $E/p$ 时才可能发生。

[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)就是一个量子池塘，而“涟漪”就是它的[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)。一个物体在氦中移动要经历阻力，就必须通过产生一个[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)来损失能量和动量。如果物体的速度 $v$ 太低，这个过程在能量上是被禁止的。发生这一过程的阈值由最“容易产生”的激发决定——即 $E/p$ 比值最小的那个激发。这个最小值是流体的一个决定性属性，被称为**[朗道临界速度](@keyword=landau_critical_velocity|lang=zh-CN|style=Feynman)**，$v_c$：

$$
v_c = \min_{p \gt 0} \left( \frac{E(p)}{p} \right)
$$

如果一种流体的临界速度 $v_c$ 大于零，那么它就能在任何低于 $v_c$ 的速度下无耗散地流动。这就是超流性的秘密。一个流体是否能成为[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的全部问题，归结于其能量-动量曲线 $E(p)$ 的形状，物理学家称之为**色散关系**。

还有另一种非常直观的方式来看待这个问题。想象你正随着超流体以速度 $\vec{v}_s$ 一起流动。从你的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)看，一个激发的能量会发生[多普勒频移](@keyword=doppler_shift|lang=zh-CN|style=Feynman)。一个在[静止流体](@keyword=fluid_at_rest|lang=zh-CN|style=Feynman)中能量为 $E(p)$、动量为 $\vec{p}$ 的激发，现在的能量变为 $E'(\vec{p}) = E(p) + \vec{p} \cdot \vec{v}_s$。当一个激发可能从真空中自发产生时，流动就变得不稳定，这意味着它的能量 $E'$ 可能降至零。这种情况发生的最低速度 $v_s$——即动量与流动方向相反的激发能量首次达到零时的速度——正是[朗道临界速度](@keyword=landau_critical_velocity|lang=zh-CN|style=Feynman) [@problem_id:240686]。因此，要理解[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)，我们必须认识一下存在于色散曲线上的那些角色。

### 角色阵容：[声子](@keyword=phonons|lang=zh-CN|style=Feynman)与[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)

[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)的[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)是物理学中最著名的图表之一，它最初由 Landau 勾勒，后来被[中子散射](@keyword=neutron_scattering|lang=zh-CN|style=Feynman)实验所证实。它不是一条简单的单一曲线；根据动量的不同，它表现出两种截然不同的特性。

#### [声子](@keyword=phonons|lang=zh-CN|style=Feynman)：流体的低语

在非常小的动量下（对应非常长的波长），[元激发](@keyword=elementary_excitations|lang=zh-CN|style=Feynman)正如你所预料的：[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)。但这些是量子[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)，所以我们称之为**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**。就像普通声音一样，它们的能量与动量成正比：

$$
E_{ph}(p) = c_s p
$$

这里，$c_s$ 是液体中的声速。对于这些[声子激发](@keyword=phonon_excitations|lang=zh-CN|style=Feynman)，比值 $E(p)/p$ 就是一个常数 $c_s$。如果[声子](@keyword=phonons|lang=zh-CN|style=Feynman)是唯一的激发类型，那么[临界速度](@keyword=critical_velocity|lang=zh-CN|style=Feynman)将是声速，一个高达约 240 m/s 的值 [@problem_id:504952]。但随着我们增加动量，故事发生了戏剧性的转折。

#### [旋子](@keyword=rotons|lang=zh-CN|style=Feynman)：微观的漩涡

随着动量的增加，一些真正奇异的事情发生了。能量曲线没有继续上升，而是向下凹陷，在一个特定的有限动量 $p_0$ 处形成一个局部极小值。这个极小值附近的激发是一种完全不同的东西：**[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)**。

什么是[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)？Richard Feynman 提出了一个优美的物理图像。他将[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)想象成一个由氦原子组成的微小“烟圈”，一个微型涡旋环，其中有几个原子在绕着自身旋转。这种微观的旋转运动是“roton”（[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)）这个名字的由来，并为其为何具有特征动量 $p_0$ 提供了一个直观的理由。正如晶体中最高动量[声子](@keyword=phonons|lang=zh-CN|style=Feynman)与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的原子间距相关一样，[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)动量 $p_0$ 从根本上与[液氦](@keyword=liquid_helium|lang=zh-CN|style=Feynman)中的平均原子间距 $d$ 相联系。一个简单的模型是 $p_0 \approx h/d$，其中 $h$ 是普朗克常数。这告诉我们，[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)是一种原子尺度的现象，是液体[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)的遗迹在其集体行为中的体现 [@problem_id:1794755]。

与[声子](@keyword=phonons|lang=zh-CN|style=Feynman)不同，产生[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)不能用任意小的能量。即使是产生能量最低的[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)，也需要一个有限的能量块，称为**[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)** $\Delta$。在极小值附近，[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)可以近似为一个简单的抛物线形式，就像一个经典粒子一样：

$$
E_{rot}(p) \approx \Delta + \frac{(p - p_0)^2}{2\mu}
$$

这里，$\mu$ 是一个“有效质量”，描述了当动量偏离 $p_0$ 时能量增加的程度 [@problem_id:1994389]。

[色散曲线](@keyword=dispersion_curves|lang=zh-CN|style=Feynman)中的这个凹陷，即[旋子极小值](@keyword=roton_minimum|lang=zh-CN|style=Feynman)，是决定超[流体[流](@keyword=fluid_flow|lang=zh-CN|style=Feynman)动稳定性](@article_id:380735)的关键特征。如果你从原点画一条线到 $E(p)$ 曲线上的一个点，这条线的斜率就是 $E(p)/p$。[朗道临界速度](@keyword=landau_critical_velocity|lang=zh-CN|style=Feynman)就是你能画出的所有这类线中*最平缓*的那条线的斜率——即刚好与曲线相切的那条线。由于[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)的凹陷，与[旋子极小值](@keyword=roton_minimum|lang=zh-CN|style=Feynman)相切的切线要比[声子](@keyword=phonons|lang=zh-CN|style=Feynman)对应的线平缓得多。

通过一个直接的计算，可以找到由产生[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)设定的[临界速度](@keyword=critical_velocity|lang=zh-CN|style=Feynman) [@problem_id:1994389] [@problem_id:232665]。这个速度依赖于 $\Delta$、$p_0$ 和 $\mu$，结果远低于声速，大约在 60 m/s 左右 [@problem_id:1893269]。这意味着在能量上产生一个[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)比产生一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)更“便宜”。[旋子极小值](@keyword=roton_minimum|lang=zh-CN|style=Feynman)是超[流态](@keyword=flow_regimes|lang=zh-CN|style=Feynman)的“阿喀琉斯之踵”；它决定了[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)的真正速度极限。

### 双流体探戈

这两种[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的存在直接导致了著名的**[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)**，这是一种描述[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)宏观行为的强大方法。在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)以上的任何温度下，该液体的行为都像两种完全相互[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)的流体的混合物：

1.  **超流体组分**：这是液体的纯量子[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，是没有任何[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)存在的“真空”。它具有[零粘度](@keyword=zero_viscosity|lang=zh-CN|style=Feynman)和至关重要的零熵。它是一种完美的理想流体。

2.  **正常流体组分**：这只不过是所有热激发的[声子和旋子](@keyword=phonons_and_rotons|lang=zh-CN|style=Feynman)组成的“气体”。由于这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)携带能量和动量，[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)具有普通液体的所有性质。它携带了系统的全部熵（热量），并且是粘性的，其粘性源于[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)和[声子](@keyword=phonons|lang=zh-CN|style=Feynman)之间的相互散射 [@problem_id:1921364]。

这不仅仅是一个方便的数学技巧，它在物理上是真实的。一个惊人的证据是**[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)**现象。在普通流体中，声音是压力和密度的波。但在超流体中，你可以有一种波，其中[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)（热的，携带熵）和超流体（冷的，无熵）向相反方向移动，从而使总密度保持不变。结果是一种在流体中传播的温度波。发现这种“温度波”是对双流体图像的壮观证实 [@problem_id:574426]。

该模型的核心原理——所有熵都存在于正常流体中——也优雅地解释了其他观测结果。例如，如果将少量较轻的同位素氦-3原子溶解到[超流氦-4](@keyword=superfluid_helium_4|lang=zh-CN|style=Feynman)中，可以观察到它们与正常流体一起运动，而不是与[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)一起运动。为什么呢？随机放置的氦-3原子引入了一种称为混合熵的无序形式。根据[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)的基本假设，任何对系统熵有贡献的物理实体都必须是[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)的一部分。因此，氦-3原子被迫加入了[声子和旋子](@keyword=phonons_and_rotons|lang=zh-CN|style=Feynman)的舞蹈 [@problem_id:1886069]。

或许对整个理论最明确的定量检验来自于测量液体的**[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)**——即提高其温度需要多少能量。[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)曲线的形状是色散关系的直接写照。
*   在极低温度下（$k_B T \ll \Delta$），没有足够的热能来产生昂贵的[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)。只有低能量的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)被激发。这导致[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)随温度的立方增长，$C_V \propto T^3$，这是[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体的普适特征 [@problem_id:2643852]。
*   随着温度升高并接近[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的尺度（$\Delta/k_B$），激发[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)突然变得可能。因为每个[旋子](@keyword=rotons|lang=zh-CN|style=Feynman)都需要一大块能量 $\Delta$，这为液体吸收热量开辟了一个新通道。这导致[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)中出现一个指数级上升的贡献，正比于 $\exp(-\Delta / (k_B T))$ [@problem_id:107999]。

测得的总[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)是这两部分之和。它与理论预测的完美一致，为[声子和旋子](@keyword=phonons_and_rotons|lang=zh-CN|style=Feynman)的存在，以及支配[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)量子世界的深刻而优美的物理学提供了响亮的证明。