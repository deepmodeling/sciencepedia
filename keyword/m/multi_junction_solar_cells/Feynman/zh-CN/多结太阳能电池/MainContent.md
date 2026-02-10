## 引言
追求更高效的[太阳能转换](@keyword=solar_energy_conversion|lang=zh-CN|style=Feynman)是我们这个时代决定性的技术挑战之一。虽然传统的[硅太阳能电池](@keyword=silicon_solar_cells|lang=zh-CN|style=Feynman)已经无处不在，但它们的效率面临一个被称为 [Shockley-Queisser 极限](@keyword=shockley_queisser_limit|lang=zh-CN|style=Feynman)的基本天花板。这个限制源于单一[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)材料器件中一个不可避免的折衷：如何用单一的能量阈值，即[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，来有效捕获太阳的宽广光谱。本文深入探讨了针对这一问题的优雅解决方案：[多结太阳能电池](@keyword=multi_junction_solar_cells|lang=zh-CN|style=Feynman)。通过巧妙地堆叠不同材料，这些先进的器件可以克服其单结同类产品固有的损失，并实现创纪录的效率。

本文将引导您进入多结光伏的复杂世界。首先，在“原理与机制”部分，我们将探讨使这些电池工作的核心物理学，从最小化能量损失的叠层设计，到电流匹配的关键工程约束，再到发光耦合令人惊讶的有益作用。然后，在“应用与跨学科联系”部分，我们将考察这些高性能器件的应用领域，例如聚光光伏 (CPV)，并揭示这项前沿技术与自然界自身的太阳能解决方案——光合作用过程之间的迷人相似之处。

## 原理与机制

要真正领会[多结太阳能电池](@keyword=multi_junction_solar_cells|lang=zh-CN|style=Feynman)的精妙之处，我们必须首先理解其结构更简单的“表亲”——单结电池所处的困境。这是一个关于根本性且颇为令人沮丧的权衡的故事。这有点像试图用一张网同时捕捉雨滴、炮弹和保龄球。如果网太脆弱，重球会直接穿破它。如果网太结实，雨滴几乎察觉不到它的存在。没有一张网能完美地捕捉所有这些东西。对于太阳能电池来说，这张“网”就是[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)材料的一个基本属性，称为**[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。

### [带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的束缚

[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，记为 $E_g$，是激发一个电子从其[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)跃迁到可以自由移动并产生电流的状态所需的最小能量。它是一个能量阈值。太阳光是由具有各种能量的[光子](@keyword=photon|lang=zh-CN|style=Feynman)组成的连续光谱，就像一个由不同大小能量包组成的彩虹。

当这个光谱照射到单结太阳能电池上时，会发生两种情况：

1.  一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量可能*小于*[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) ($E_{photon}  E_g$)。材料对这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)是透明的。它会直接穿过，仿佛什么都没发生，其能量完全损失。这被称为**透射损失**。

2.  一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量可能*大于或等于*[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) ($E_{photon} \ge E_g$)。成功了！[光子](@keyword=photon|lang=zh-CN|style=Feynman)被吸收，一个电子被激发越过[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，产生一个可以发电的[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)。但问题来了，而且是个大问题：你能从这个事件中提取的电能*仅仅*是[带隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman) $E_g$。多余的能量，即差值 $E_{photon} - E_g$，会很快以热量的形式损失掉。这被称为**热弛豫损失**。被激发到“导带山丘”高处的电子，在被收集之前，会迅速滚落到山丘的底部边缘（$E_g$），[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，使你的太阳能电池板升温。

所以，你面临一个两难的境地。想象一个简化的世界，太阳只发出两种“颜色”的[光子](@keyword=photon|lang=zh-CN|style=Feynman)：高能量的蓝色[光子](@keyword=photon|lang=zh-CN|style=Feynman) ($E_H = 2.40 \text{ eV}$) 和低能量的红色[光子](@keyword=photon|lang=zh-CN|style=Feynman) ($E_L = 1.20 \text{ eV}$) [@problem_id:1334756]。如果你用低[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)材料（比如 $E_g = 1.20 \text{ eV}$）制造电池，你可以同时捕获红色和蓝色[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这很棒！但每捕获一个蓝色[光子](@keyword=photon|lang=zh-CN|style=Feynman)，你就会将其一半的能量（$2.40 \text{ eV} - 1.20 \text{ eV} = 1.20 \text{ eV}$）以热量的形式浪费掉。如果你转而选择高[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)材料（比如 $E_g = 2.40 \text{ eV}$），你就能非常高效地转换蓝色[光子](@keyword=photon|lang=zh-CN|style=Feynman)，没有热弛豫损失。但现在，所有的红色[光子](@keyword=photon|lang=zh-CN|style=Feynman)都直接穿过，毫无贡献！无论你选择哪种单一[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，你都必须做出妥协，将太阳能的很大一部分弃之不用。这种根本性的权衡就是著名的 **[Shockley-Queisser 极限](@keyword=shockley_queisser_limit|lang=zh-CN|style=Feynman)**的核心，它将单结[硅太阳能电池](@keyword=silicon_solar_cells|lang=zh-CN|style=Feynman)的最高理论效率限制在 $33\%$ 左右。我们怎样才能做得更好呢？

### 叠层解决方案：[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的交响曲

如果一张网无法完成任务，为什么不使用一叠按强度分类的网呢？这正是[多结太阳能电池](@keyword=multi_junction_solar_cells|lang=zh-CN|style=Feynman)（或称**叠层**太阳能电池）背后的理念。我们不再使用一种材料，而是将两个或多个具有不同[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的不同[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)层堆叠在一起。

让我们看看这是如何巧妙地解决我们的困境的。想象一个双结电池，处在一个简化的太阳下，该太阳发出三种类型的[光子](@keyword=photon|lang=zh-CN|style=Feynman)：高能量的紫外光 ($E_1 = 2.50 \text{ eV}$)，中等能量的绿光 ($E_2 = 1.70 \text{ eV}$)，和低能量的红外光 ($E_3 = 1.10 \text{ eV}$) [@problem_id:1322632]。

顶部电池由高[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)材料制成，例如 $E_{g,top} = 2.05 \text{ eV}$。它充当一个选择性滤光片。当太阳光照射到它时，高能量的紫外[光子](@keyword=photon|lang=zh-CN|style=Feynman) ($2.50 \text{ eV}$) 被吸收，因为它们的能量远高于顶部电池的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。关键是，现在的热弛豫损失小得多（$2.50 \text{ eV} - 2.05 \text{ eV} = 0.45 \text{ eV}$），这与使用低[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)材料相比是一个巨大的进步。而能量低于 $E_{g,top}$ 的绿光和红外[光子](@keyword=photon|lang=zh-CN|style=Feynman)则会毫发无损地穿过。

在下面，我们放置底部电池，它由[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)较低的材料制成，比如 $E_{g,bot} = 1.25 \text{ eV}$。它接收被顶部电池过滤后的光。绿光[光子](@keyword=photon|lang=zh-CN|style=Feynman) ($1.70 \text{ eV}$) 的能量足以在这里被吸收，同样热弛豫损失也相对较小。红外[光子](@keyword=photon|lang=zh-CN|style=Feynman) ($1.10 \text{ eV}$) 的能量仍然不足以被第二层吸收，所以它们穿过并损失掉了。

通过分工吸收太阳光谱，每个结都在更适合自己的光谱部分工作。总发[电功率](@keyword=electrical_power|lang=zh-CN|style=Feynman)是每个电池功率的总和。总体结果是热弛豫损失的显著减少 [@problem_id:1803213]。在一个比较优化单结电池和简单双结叠层电池的理想化场景中，叠层结构可以将功率输出惊人地提高 $50\%$ [@problem_id:1334756]。这不是一个微小的改进；这是[能量转换](@keyword=energy_conversion|lang=zh-CN|style=Feynman)游戏规则的根本性改变，让我们能够突破 [Shockley-Queisser 极限](@keyword=shockley_queisser_limit|lang=zh-CN|style=Feynman)所设定的天花板。

### 交易的艺术：电流匹配

当然，大自然不会免费赠送如此大奖。堆叠电池引入了一个新的、艰巨的工程挑战。在大多数实际器件中，这些子电池是单片集成生长的——一个长在另一个上面——并且在电学上是**串联**的。

任何摆弄过电子产品的人都知道[串联电路](@keyword=series_circuits|lang=zh-CN|style=Feynman)的第一条规则，即[基尔霍夫电流定律](@keyword=kirchhoff_s_current_law|lang=zh-CN|style=Feynman)：流经回路中每个元件的电流必须相同。把它想象成一根有几个狭窄部分的水管。整根水管的总流速是由*最窄*的部分决定的。

对于我们的[叠层太阳能电池](@keyword=tandem_solar_cells|lang=zh-CN|style=Feynman)来说，这意味着该器件产生的总电流受限于产生电流*最少*的子电池 [@problem_id:2510066]。这就是**电流匹配**的关键约束。如果你的底部电池跟不上，即使你的顶部电池能产生巨大的电流也无济于事。底部电池成为瓶颈，而顶部电池的额外潜力就被浪费了。

实现电流匹配是一个精细的平衡过程。一个电池产生的电流量取决于它吸收的[光子](@keyword=photon|lang=zh-CN|style=Feynman)数量。工程师必须精心选择具有合适[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的材料，然后调整每一层的厚度。顶部电池必须足够厚，以吸收其目标的大部分高能[光子](@keyword=photon|lang=zh-CN|style=Feynman)，但又不能太厚，以至于意外吸收了下面电池所需的低能[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这是一场[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)和光学工程的精确舞蹈，所有这些都是为了确保在标准太阳光谱下，叠层中的每一层都能产生完全相同的电流。

### 意外的转折：发光耦合

就在你认为已经考虑了所有主要物理过程时，大自然揭示了另一个更微妙的相互作用层面，它既优美又出人意料地有帮助。当一个电子和一个空穴在顶部电池中复合时会发生什么？在非常高质量的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中——也就是用于这些创纪录电池的那种——这种复合过程是高度**辐射性**的，这意味着它会发出一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这与发光二极管 (LED) 的原理相同。

这个发射出的[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量非常接近顶部电池的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $E_{g,top}$。现在，这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)可以做两件事之一。它可能在顶部电池内部被重新吸收，这个过程称为**[光子](@keyword=photon|lang=zh-CN|style=Feynman)回收**，有助于提高该电池的电压。或者，它可以逸出并向下传播，进入底部电池。

美妙之处就在这里：由于叠层设计为 $E_{g,top} > E_{g,bottom}$，顶部电池发出的[光子能量](@keyword=photon_energy|lang=zh-CN|style=Feynman)绰绰有余，可以被底部电池吸收！这种顶部电池实际上成为底部电池光源的现象，被称为**发光耦合** [@problem_id:2510074]。

这不仅仅是一个学术上的好奇心；它具有深远而有益的影响。假设我们的器件存在电流失配，底部电池是“薄弱环节”或瓶颈。来自顶部电池发光的额外[光子](@keyword=photon|lang=zh-CN|style=Feynman)流为底部电池提供了额外的生成功率，从而提升了其电流！这有助于“修复”失配，增加整个器件的总短路电流。描述这种效应的方程表明，最终电流成为两个子电池电流的[加权平均](@keyword=weighted_average|lang=zh-CN|style=Feynman)值，从限制值向上拉高 [@problem_id:2510074]。

那么电压呢？这个过程涉及一个权衡。一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)从顶部电池逸出被底部电池吸收，对顶部电池来说是一种损失，所以其单个[开路电压](@keyword=open_circuit_voltage|lang=zh-CN|style=Feynman) $V_{oc,top}$ 实际上会略有下降。然而，那个[光子](@keyword=photon|lang=zh-CN|style=Feynman)对底部电池来说是一种增益，所以其电压 $V_{oc,bot}$ 会增加。值得注意的是，在理想的辐射极限下，底部[电池电压](@keyword=cell_voltage|lang=zh-CN|style=Feynman)的增益足以补偿顶部[电池电压](@keyword=cell_voltage|lang=zh-CN|style=Feynman)的微小损失，从而导致总叠层[开路电压](@keyword=open_circuit_voltage|lang=zh-CN|style=Feynman) $V_{oc} = V_{oc,top} + V_{oc,bot}$ 的净*增加* [@problem_id:2510074] [@problem_id:2850599]。这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)没有被浪费；它在器件的另一部分被智能地回收，将一个潜在的损失转化为净增益。

从热弛豫这个棘手的问题到光谱分割的优雅解决方案，从电流匹配的刚性约束到发光耦合的巧妙援手，[多结太阳能电池](@keyword=multi_junction_solar_cells|lang=zh-CN|style=Feynman)的物理学是一段引人入胜的旅程。它展示了我们如何通过巧妙地组合材料和理解光与物质相互作用的最深层原理，来设计出接近[能量转换](@keyword=energy_conversion|lang=zh-CN|style=Feynman)[热力学极限](@keyword=thermodynamic_limit|lang=zh-CN|style=Feynman)的器件。