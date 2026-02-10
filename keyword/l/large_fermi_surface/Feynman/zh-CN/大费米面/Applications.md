## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

我们花了一些时间讨论这样一个相当抽象的想法：在适当的条件下，顽固的、局域的电子可以被说服加入集体之舞，从而壮大移动电子的海洋。你可能会说，这想法很美，但它仅仅是理论家的白日梦吗？我们怎么可能*知道*这个无形的海洋是否已经变大了？有没有办法对巡游电子的数量进行一次“普查”？

事实证明，大自然以其无穷的精妙，为我们提供了非常聪明的工具来做到这一点。这种[电子计数](@keyword=electron_counting|lang=zh-CN|style=Feynman)的后果是深远的，其回响从奇异磁性材料的研究，一直延伸到高温超导这个宏大而未解的谜团。这段从一个简单的计数规则到物理学前沿的旅程，揭示了量子世界深层次的内在统一性。

### 进行普查：探测费米面大小

核心原理非常简单：如果[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子的数量发生变化，任何依赖于这个数量的宏观性质也必须随之改变。诀窍在于找到一个既对这个数量敏感又易于测量的性质。幸运的是，我们至少有两种精妙的技术。

#### 量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)：费米面的指纹

想象一下，将一块纯净的金属晶体置于非常强的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，并将其冷却到接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)。曾经随机漫游的自由电子现在被迫进入量子化的圆形轨道。整个电子海的能级会聚集成离散的“朗道能级”。当你调高或调低[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，这些能级会扫过费米能级，导致各种物理性质——磁化强度、[电阻率](@keyword=electrical_resistivity|lang=zh-CN|style=Feynman)、比热——以一种周期性的方式[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这种现象被称为 de Haas-van Alphen (dHvA) 效应。

其魔力在于这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的*频率*。事实证明，当振荡频率对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的倒数 $1/B$ 作图时，其值与费米面的[极值截面](@keyword=extremal_cross_section|lang=zh-CN|style=Feynman)积成正比。就好像[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)让我们能够直接拍摄到[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的轮廓。

现在，我们可以检验我们的“[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)”假说。在高温下，[近藤晶格](@keyword=kondo_lattice|lang=zh-CN|style=Feynman)中的 f-电子是[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)，只有传导电子形成一个“小”[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)。当我们将系统冷却到远低于[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman)时，f-电子变得巡游，加入费米海。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子的密度增加——在最简单的情况下，它会加倍。更大的密度意味着更大的[费米动量](@keyword=fermi_momentum|lang=zh-CN|style=Feynman) $k_F$，这又意味着更大的费米面面积 $A \propto k_F^2$。因此，dHvA 频率 $F$ 必须跃升到一个更高的值！对于一个[载流子密度](@keyword=charge_carrier_density|lang=zh-CN|style=Feynman)加倍的简单三维金属，一个简单的计算表明，频率应该增加 $2^{2/3}$ 倍 [@problem_id:118474]。通过用温度或压力调控系统，并观察到 dHvA 频率的跃变，实验学家可以直接见证[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)的诞生 [@problem_id:2862015] [@problem_id:2998355]。

#### [霍尔效应](@keyword=hall_effect|lang=zh-CN|style=Feynman)：被宏大真理偏转的简单电流

还有另一种，也许更熟悉的方法来计数载流子：霍尔效应。如果你让电流通过一种材料，并施加一个垂直于电流方向的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，移动的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)（电子）会因[洛伦兹力](@keyword=lorentz_force|lang=zh-CN|style=Feynman) $q(\mathbf{v} \times \mathbf{B})$ 而偏向一侧。这种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的积累会产生一个横向的“[霍尔电压](@keyword=hall_voltage|lang=zh-CN|style=Feynman)”。这个电压的大小信息量非常大。对于一个简单的金属，[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman) $R_H$ 仅仅与[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[载流子密度](@keyword=charge_carrier_density|lang=zh-CN|style=Feynman)成反比，即 $R_H \approx -1/(ne)$。

这为我们的普查提供了第二个独立的工具。设想一个系统处于一个量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的边缘，近藤效应在此处崩塌。当我们调控一个像[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)这样的参数时，系统可能会从一个“[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)”态（高[载流子密度](@keyword=charge_carrier_density|lang=zh-CN|style=Feynman) $n_L$）突然切换到一个 f-电子突然局域化的“小[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)”态（低[载流子密度](@keyword=charge_carrier_density|lang=zh-CN|style=Feynman) $n_S$）。[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)应该发生什么变化？它必须*跃变*！由于 $n_S$ 小于 $n_L$，[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)的[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman) $|R_H|$ 应该会不连续地增加。观察到 $R_H$ 作为[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)函数的这种急剧跃变，被认为是[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)重构与近藤崩塌[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)相关的强有力证据 [@problem_id:3018895] [@problem_id:2833084]。

### 作为诊断工具的[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)

有了这些工具，我们就可以超越仅仅证实一个理论的范畴，开始像量子侦探一样行事。我们可以利用[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)的特征——或其缺失——来区分关于物质本质的深刻而相互竞争的观点。

一个典型的例子是对量子临界点（QCPs）的研究。这些是发生在绝对零度的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，不是由热量驱动，而是由量子涨落驱动，因为像压力或[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)这样的参数被调控。在 QCP 附近，材料常常表现出奇怪的、“[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)”的行为，这 defying 常规描述。

在许多[重费米子材料](@keyword=heavy_fermion_materials|lang=zh-CN|style=Feynman)中，一个核心问题是：QCP 的本质是什么？一个流行的理论是我们刚刚讨论的“近藤崩塌”模型，其中[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)本身在 QCP 处被摧毁。这种情况预示着一些标志性的信号：[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)的跃变和 dHvA 频率的急剧变化 [@problem_id:2833084]。

但还有另一种可能性。QCP 可能是一个更常规的磁性[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，比如[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)（SDW）的出现。在这种情况下，重[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)一直持续到[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，而正是*这个[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)*的不稳定性驱动了[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。这种不稳定性通常是由费米面的一个几何特性“嵌套（nesting）”引起的——即费米面上的大片平坦区域可以被一个单一的波矢 $\mathbf{Q}$ 完美地相互映射。这就像湖上有两条平行的海岸线；它使得它们之间的水特别容易形成驻波。[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)的这种“驻波”就是[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)，其波矢就是嵌套矢量 $\mathbf{Q}$ [@problem_id:2806239]。

那么，我们如何决定呢？我们看证据。材料 CeCoIn$_5$ 是一个著名的例子。它显示出 QCP 的所有特征。但当物理学家进行精细的量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)和[霍尔效应](@keyword=hall_effect|lang=zh-CN|style=Feynman)测量时，他们发现了一个惊喜：对应于[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)的 dHvA 频率平滑地穿过了[临界场](@keyword=critical_fields|lang=zh-CN|style=Feynman)，而[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)没有显示出跃变。结论是明确的。在 CeCoIn$_5$ 中，[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)是稳健的；[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)不是近藤崩塌，而是[重费米子](@keyword=heavy_fermion|lang=zh-CN|style=Feynman)液体的 SDW 不稳定性。[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)的概念，以及对其稳定性的检验，是解开这个谜题的关键线索 [@problem_id:3011760]。

### 普适原理：铜氧化物之谜

以免你认为这种[电子计数](@keyword=electron_counting|lang=zh-CN|style=Feynman)的事情仅限于[重费米子化合物](@keyword=heavy_fermion_compounds|lang=zh-CN|style=Feynman)的奇异领域，完全相同的原理和问题也出现在物理学一个完全不同且以困惑著称的角落：高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)。

这些材料是“掺杂的 Mott 绝缘体”。在其母体状态下，强烈的电子-电子排斥将每个铜位点上的一个[电子局域化](@keyword=electron_localization|lang=zh-CN|style=Feynman)，阻止了导电。当我们引入一小部分浓度为 $p$ 的“空穴”（电子的缺失）时，材料变成金属，并在低温下成为具有前所未有高转变温度 $T_c$ 的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。高于 $T_c$ 的金属态，即所谓的“[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)”相的本质，是科学界最大的未解之谜之一。

在这里，Luttinger 定理同样是我们的指路明灯。对于一个电子密度为 $n=1-p$ 的简单金属，该定理预测一个“大”的空穴型[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，其体积对应于 $1+p$ 的载流子数。但当实验学家使用角分辨光电子能谱（[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)）来绘制[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)时，他们没有看到一个闭合的轮廓。相反，他们看到了不连续的“[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)”。

这意味着什么？争论仍在继续，但主要的理论情景都是由 Luttinger 定理的推论构建的 [@problem_id:2842819]：

1.  **[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)被隐藏：** 一种可能性是，底层的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)*确实*有一个与 $1+p$ 计数相符的[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)。然而，[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)相中的[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)导致这个费米面部分区域（“反节点”）上的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)变得非相干或“打开[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”，使它们对 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 来说是不可见的。观察到的[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)仅仅是完整的、大的费米面中幸存的、相干的部分。在这种观点下，Luttinger 定理得到遵守，但我们的实验存在盲点 [@problem_id:2828402]。

2.  **[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)重构：** 另一个想法是，一种隐藏的序，也许是某种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)或自旋模式，在[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)相中出现。这种序会破坏[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)，折叠[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)，并将[大费米面](@keyword=large_fermi_surface|lang=zh-CN|style=Feynman)重构成小的、闭合的“口袋”。我们看到的[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)将是这些口袋明亮、可见的一侧。在这里，Luttinger 定理也得到遵守，但它必须应用于对称性破缺态的新的、更小的[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)。口袋中的载流子数将与掺杂浓度 $p$ 成正比，而不是 $1+p$ [@problem_id:2828402] [@problem_id:2842819]。

3.  **物态是真正奇异的（[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)的）：** 最激进的提议是，Luttinger 定理的前提本身被违反了。在这种观点下，电子[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)本身已经解体，或“分数化”，成为分别携带其自旋和[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的更基本的激发。我们看到的费米面将由这些分数化粒子构成。这样一个“拓扑有序”态不会破坏任何常规对称性，但会拥有一个体积与 $p$ 成正比的小[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，直接违反了标准的 Luttinger 计数。这将标志着一种真正全新的量子物质态，超出了我们教科书的描述 [@problem_id:3020773] [@problem_id:2842819]。

因此，从一个“有多少电子可以自由移动？”的简单问题出发，我们被带入了一个充满量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)、对称性破缺、甚至分数化粒子的兔子洞。这是一个美丽的证明，展示了物理学的力量和统一性，即一个如此简单的计数规则可以作为我们穿越科学中一些最复杂、最神秘景观的坚定向导。