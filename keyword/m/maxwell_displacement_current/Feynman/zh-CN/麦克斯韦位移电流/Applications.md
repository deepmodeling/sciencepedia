## 应用与跨学科联系

所以，我们“修正”了安培定律。我们添加了一个新项，一个涉及变化电场的修正因子，并称之为位移电流。你可能会倾向于认为这只是一个数学上的讲究，一点为使方程看起来更漂亮、更对称而做的深奥的记账工作。这样想就完全错失了重点。这个源于[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)充电这个简单思想谜题的小小补充，不仅仅是弥补了理论上的一个漏洞，它为通往宇宙的大门敞开了。

位移电流是完成电与磁宏大交织之舞的关键环节。它是将一套静态规则转变为充满活力、承载波动的电磁理论的缺失部分。正是因为这个项，光本身才得以存在。但其影响远比仅仅解释光要多样和深刻得多。让我们踏上一段旅程，看看这个思想是如何贯穿于物理学和工程学的广阔织锦，从平凡到真正奇特。

### [电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的完善

让我们回到一切开始的地方：[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)。当我们通过导线施加电流 $I_0$ 给[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)充电时，我们知道导线周围会产生[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。但是在极板*之间*，那个没有[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)流动的空间里呢？安培的原始定律会说那里应该没有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。一个荒谬的结论！麦克斯韦的补充拯救了局面：极板间变化的电场 $\mathbf{E}$ 就像真实电流一样，充当了[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的源。

现在，如果我们在[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)中填充[电介质材料](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)会发生什么？有人可能会天真地认为这会让事情变得非常复杂。材料会极化，产生自己的内部电场。对于极板上给定数量的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，电场 $\mathbf{E}$ 现在变弱了。这肯定会改变产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)吧？令人惊讶的答案是：不会！内部产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)仅取决于外部的充电电流 $I_0$，而与电介质材料完全无关。

为何有如此非凡的简洁性？这是因为[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)，在其最普遍的形式中，不仅仅关乎真空中变化的电场。它关乎变化的*[电位移矢量](@keyword=electric_displacement_vector|lang=zh-CN|style=Feynman)*，$\mathbf{D} = \varepsilon_0 \mathbf{E} + \mathbf{P}$，其中 $\mathbf{P}$ 是[材料的极化](@keyword=polarization_of_materials|lang=zh-CN|style=Feynman)强度。总的位移电流密度是 $\mathbf{J}_D = \frac{\partial \mathbf{D}}{\partial t}$。这可以分为两部分：$\varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}$，即使在真空中也存在的项；以及 $\frac{\partial \mathbf{P}}{\partial t}$，一个由材料中束缚电荷的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)引起的“[极化电流](@keyword=polarization_current|lang=zh-CN|style=Feynman)”。当我们在[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)中放入电介质时，$\mathbf{E}$ 的减弱减少了第一项。但材料变化的极化产生了一个[极化电流](@keyword=polarization_current|lang=zh-CN|style=Feynman)，正好弥补了差额！大自然把一切都安排得如此美妙。通过关注与我们控制的[自由电荷](@keyword=free_charge|lang=zh-CN|style=Feynman)直接相关的[位移矢量](@keyword=displacement_vector|lang=zh-CN|style=Feynman) $\mathbf{D}$，材料凌乱的内部细节从最终结果中消失了。这个表述不仅正确，而且优雅。

这种变化的极化产生[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的思想不仅仅是一个理论上的精妙之处。人们可以想象一个由特殊材料制成的圆柱体，其中感应出随时间变化的极化，比如沿其轴线的[方位角](@keyword=azimuthal_angle|lang=zh-CN|style=Feynman)方向。即使在任何地方都没有[自由电流](@keyword=free_currents|lang=zh-CN|style=Feynman)，这种变化的极化——这种“[极化电流](@keyword=polarization_current|lang=zh-CN|style=Feynman)”——也会沿圆柱体轴线产生[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，就像一个由取向[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的分子构成的[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)一样。

### 从火花到信号：波的诞生

[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)储存能量。但如果你想一想，天线只是一个被打开和展开的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)，其设计目的不是储存能量，而是将其投射到太空中。在一个简单的偶极子天线的馈电点，即两臂几乎相遇的地方，有一个小间隙。当来自发射机的交流电流入天线时，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)来回晃动。没有[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)穿过间隙。但就像我们的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)一样，一个快速变化的电场在那个间隙中产生。这个变化的场*就是*[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)。这个流过真空的电流确保了总电流的连续性。正是这最后的“推动”，将能量发射出去，脱离导线的束缚，以电磁波的形式穿越太空。每一次无线电广播，每一个Wi-Fi信号，每一比特从卫星发出的数据，都归功于位移电流跨越间隙并催生了波。

### 物质世界：电流的战场

到目前为止，我们谈论“导体”和“绝缘体”时，仿佛它们是两个完全不同的物种。这是一个方便的虚构。实际上，大多数材料两者兼备。它们可以像电介质一样维持电场，也可以传导一些电流，无论多么微弱。这就是我们所说的“有漏电的”电介质或不[完美导体](@keyword=perfect_conductor|lang=zh-CN|style=Feynman)。

当我们对这样的材料施加[时变电场](@keyword=time_varying_electric_field|lang=zh-CN|style=Feynman)时，一场战斗随之展开。两种类型的电流流动。首先是熟悉的传导电流，$\mathbf{J}_c = \sigma \mathbf{E}$，其中 $\sigma$ 是材料的[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)。这是[自由电荷](@keyword=free_charge|lang=zh-CN|style=Feynman)的流动。其次，是我们的新朋友，[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)，$\mathbf{J}_d = \epsilon \frac{\partial \mathbf{E}}{\partial t}$，其中 $\epsilon$ 是材料的[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)。这是变化电场和极化的效应。

哪种电流获胜？答案是理解现代世界中材料行为的关键：*这取决于频率*。对于角频率为 $\omega$ 的正弦场，这两种电流的幅度之比结果非常简单：

$$ \frac{|\mathbf{J}_c|}{|\mathbf{J}_d|} = \frac{\sigma}{\omega \epsilon} $$

这个小方程是一个强大的神谕。它告诉我们，材料的身份不是固定的。它是动态的，由我们探测它所用的场的频率定义。

考虑海水。由于含盐量高，它有可观的[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman) $\sigma$。在水下电缆的60赫兹低频下，比值 $\sigma/(\omega\epsilon)$ 是巨大的——大约在 $10^7$ 的量级！在这个频率下，位移电流在传导电流的咆哮声中只是微弱的耳语。海水实际上就是一个导体。对于像铜这样的金属，情况更为极端。在1兆赫的射频下，传导电流比[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)大一万亿倍。这就是为什么对于许多电路问题，我们可以忽略导线*内部*的[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)。“[良导体近似](@keyword=good_conductor_approximation|lang=zh-CN|style=Feynman)”正是建立在这一洞察之上。

但再看看这个比值。随着频率 $\omega$ 的增加，[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)获得力量。必然存在一个“[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)频率”，$\omega_c = \sigma/\epsilon$，在该频率下两种电流的幅度相等。低于这个频率，材料表现得像导体；高于它，材料开始更像[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)。这种频率依赖的行为支配着从无线电波如何穿透地面到高频[电路板设计](@keyword=circuit_board_design|lang=zh-CN|style=Feynman)的一切。

### 物理学前沿：旧思想，新应用

由麦克斯韦项揭示的电流竞争原理，远远超出了普通材料的范畴。它为理解即使是最奇特的物质状态也提供了一个框架。

- **[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)：** 在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的奇异量子世界中，出现了一种新型电流：[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)，即成对电子的[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)。当我们施加[时变电场](@keyword=time_varying_electric_field|lang=zh-CN|style=Feynman)时，战斗现在是在这种[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)和位移电流之间展开。我们同样可以找到一个特征频率，使它们的幅度相等。这个频率，被称为超导[等离子体频率](@keyword=plasma_frequency|lang=zh-CN|style=Feynman)，$\omega_p = \sqrt{n_s e^2 / (m \epsilon)}$，是材料的一个基本属性。低于它，[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)完美地屏蔽电场；高于它，[电磁波](@keyword=electromagnetic_waves|lang=zh-CN|style=Feynman)可以开始穿透。这场古老的斗争在一个新的量子舞台上上演。

- **[超材料](@keyword=metamaterials|lang=zh-CN|style=Feynman)：工程磁性：** 这也许是最令人费解的应用。源于[电子轨道](@keyword=electron_orbitals|lang=zh-CN|style=Feynman)运动和自旋的自然磁性是众所周知的弱，并且在可见光的高频下趋于消失。很长一段时间里，这似乎是自然界不可逾越的定律。

但如果我们能够构建我们自己的“磁性原子”呢？这就是超材料背后的革命性思想。该领域的主力是开口谐振环（SRR），一个带有小开口的微小导电环。当交变[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿过环路时，它会感应出电流。但电流无法穿过开口——至少，不能作为[传导电流](@keyword=conduction_current|lang=zh-CN|style=Feynman)。取而代之的是，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)在开口的两侧堆积，产生一个巨大的、局域化的电场。这个快速变化的电场*就是*[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)，它跃过间隙，完成了电路！

我们创造的是一个微小的[谐振电路](@keyword=resonant_circuit|lang=zh-CN|style=Feynman)，其循[环电流](@keyword=ring_current|lang=zh-CN|style=Feynman)（部分是[传导电流](@keyword=conduction_current|lang=zh-CN|style=Feynman)，部分是[位移电流](@keyword=displacement_current|lang=zh-CN|style=Feynman)）产生了一个强大的[磁偶极矩](@keyword=magnetic_dipole_moments|lang=zh-CN|style=Feynman)。通过将数十亿个这样的SRR[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，我们可以创造出一种体材料，其磁响应不是由其[化学成分](@keyword=chemical_composition|lang=zh-CN|style=Feynman)决定，而是由我们的设计决定。通过调整SRR的几何形状，我们可以使有效磁导率 $\mu$ 随心所欲。我们可以让它变得巨大，或为零，甚至在某个频带内为*负*——这是自然界中不存在的属性。

这种在自然界不提供磁响应的地方工程化磁响应的能力，完全依赖于每个谐振器间隙中的位移电流。它是解锁“[负折射率](@keyword=negative_refractive_index|lang=zh-CN|style=Feynman)”材料新世界的钥匙，这些材料具有实现[完美透镜](@keyword=superlens|lang=zh-CN|style=Feynman)和[隐形斗篷](@keyword=invisibility_cloak|lang=zh-CN|style=Feynman)的潜力。

从对安培定律的一个简单修补，我们发现了[无线电通信](@keyword=radio_communication|lang=zh-CN|style=Feynman)的秘密，一个对所有材料进行分类的工具，以及一种构建以前只存在于科幻小说中能弯曲光线的物质的蓝图。位移电流不是一个脚注。它是所有物理学中最富有成果和最具统一性的思想之一。