## 应用和跨学科联系

现在我们已经了解了支配量子世界中[动量输运](@keyword=momentum_transport|lang=zh-CN|style=Feynman)的奇特规则，接下来是有趣的部分。让我们把这些想法付诸实践，看看它们能做什么。黏度的量子性质在哪里显现出来？你会欣喜地发现，答案无处不在，从我们电脑中的硅片到[中子星](@keyword=neutron_stars|lang=zh-CN|style=Feynman)的核心，再到早期宇宙的火热汤羹。量子黏度的研究不仅仅是一项学术活动；它是一个强大的透镜，通过它我们可以探索一些科学已知的最迷人和最极端的物质状态。它是一个绝佳的例子，说明一个单一的物理概念，当通过量子透镜观察时，如何绽放成一幅丰富的跨学科联系的织锦。

### 固体中电子的滑移逻辑

让我们从一些看似普通的东西开始：一层电子片，就像在现代晶体管内部或在像石墨烯这样的非凡材料中流动的那样。经典地看，你会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)这种电子流体的行为与任何其他气体一样——加热它，粒子运动得更快，碰撞更多，流体变得更黏稠，或者说“更黏”。但在量子世界里，事情并非如此简单。

想象一下一个非常冷、非常纯净的二维电子气。在这里，[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)是至高无上的法则。它规定没有两个电子可以占据同一个状态。在接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的温度下，电子填满了所有可用的低能级态，形成一个“[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)”。要让两个电子碰撞并交换动量，它们必须散射到当前空着的状态中。但空着的状态在哪里？只有在费米海“表面”之上的高处才有。要到达那里需要显著的能量提升，这在低温下是罕见的。

结果是一个美丽的悖论：当你冷却系统时，你正在“冻结”碰撞的可能性。电子发现彼此之间越来越难以散射。它们的[平均自由程](@keyword=mean_free_path|lang=zh-CN|style=Feynman)——即两次碰撞之间行进的平均距离——变得越来越长。由于黏度与这个平均自由程成正比，电子气随着温度的降低而变得*更*黏稠！这与经典气体中黏度随温度升高而增加的情况形成鲜明对比。对高纯度二维电子系统的实验证实了这种奇怪的行为，其中黏度在低温下遵循 $T^{-2}$ 定律，这是[泡利阻塞](@keyword=pauli_blocking|lang=zh-CN|style=Feynman)施加的量子交通规则的直接后果 [@problem_id:2015763]。这是一个惊人的例子，说明了量子力学如何颠覆我们的经典直觉。

### 用[冷原子](@keyword=cold_atoms|lang=zh-CN|style=Feynman)工程构筑[完美流体](@keyword=perfect_fluid|lang=zh-CN|style=Feynman)

如果固体中的电子对我们的口味来说有点受限，那么让我们转向一个我们完全掌控的系统：[超冷原子气体](@keyword=ultracold_atomic_gases|lang=zh-CN|style=Feynman)。在这些系统中，物理学家可以扮演“[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)师”的角色，使用激光和[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)来[囚禁原子](@keyword=trapped_atoms|lang=zh-CN|style=Feynman)，并且最值得注意的是，可以调节它们之间相互作用的强度。

实现这一魔术的关键工具是“费什巴赫共振”。通过调节外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，我们可以引导原子跨越一个共振点，在这个共振点上，它们的[散射截面](@keyword=scattering_cross_section|lang=zh-CN|style=Feynman)——衡量它们碰撞可能性的一个量——可以改变几个[数量级](@keyword=powers_of_ten|lang=zh-CN|style=Feynman)。现在，回想一下我们的动理论洞见：黏度大致与[散射截面](@keyword=scattering_cross_section|lang=zh-CN|style=Feynman)成反比 ($\eta \propto 1/\sigma$)。因此，通过调节相互作用，我们实际上在直接调节我们量子气体的黏度！

想象一下，我们从一个相互作用非常弱的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)气体开始（这被称为BCS侧）。原子很少见到彼此，[散射截面](@keyword=scattering_cross_section|lang=zh-CN|style=Feynman) $\sigma$ 很小，黏度 $\eta$ 很高。气体像蜂蜜一样流动。现在，我们慢慢地向[费什巴赫共振](@keyword=feshbach_resonance|lang=zh-CN|style=Feynman)点调节[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。原子开始越来越强烈地相互作用。[散射截面](@keyword=scattering_cross_section|lang=zh-CN|style=Feynman)增大，黏度开始下降。

就在共振点上，发生了令人惊奇的事情。[散射截面](@keyword=scattering_cross_section|lang=zh-CN|style=Feynman)变得和量子力学所允许的一样大，仅受粒子波长的限制。相互作用如此之强，以至于原子不断碰撞，平均自由程短至它们之间的距离。这就是“[幺正极限](@keyword=unitary_limit|lang=zh-CN|style=Feynman)”。在这里，黏度达到了一个深刻的最小值 [@problem_id:2093385]。这种[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)相互作用如此之强，流动时相对阻力如此之小，以至于它被誉为“近[完美流体](@keyword=perfect_fluid|lang=zh-CN|style=Feynman)”。据推测，其剪切黏度与熵密度之比接近于一个普适下限 $\eta/s \ge \hbar/(4\pi k_B)$，这是由弦理论预测的。

真正令人难以置信的是，在另一个完全不同的系统中也观察到了同样“[完美流体](@keyword=perfect_fluid|lang=zh-CN|style=Feynman)”的行为：在大型强子对撞机等粒子加速器中产生的夸克-胶子等离子体。这是一种温度高达数万亿度的基本粒子汤，但它流动的黏度却与仅比绝对零度高几十亿分之一度的原子气体一样，低得破了纪录。这证明了物理学统一的力量，即[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)的相同原理适用于如此巨大的能量尺度范围。这种通过在共振点附近调节来调谐黏度的能力，是对微观散射物理的直接探测，将宏观[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)与碰撞原子的量子[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)联系起来 [@problem_id:1227896] [@problem_id:305015]。

### 无黏度的[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)：超流体的幽灵之舞

还有什么比[完美流体](@keyword=perfect_fluid|lang=zh-CN|style=Feynman)更奇怪的呢？一个黏度完全为*零*的流体怎么样？这就是[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，比如低于约2.17[开尔文](@keyword=kelvin|lang=zh-CN|style=Feynman)的[液氦-4](@keyword=liquid_helium_4|lang=zh-CN|style=Feynman)。如果你让它在一个桶里旋转，理论上它永远不会停止。但这是否意味着[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)中的流动总是平滑有序的呢？完全不是！超过某个[临界速度](@keyword=critical_velocity|lang=zh-CN|style=Feynman)，流动会爆发成一种混乱、无序的状态，看起来和经典[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)一模一样。但是，没有黏度来将能量耗散成[涡流](@keyword=vortex_flow|lang=zh-CN|style=Feynman)，你怎么能有[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)呢？

答案在于“[量子化涡旋](@keyword=quantized_vortices|lang=zh-CN|style=Feynman)”。超流体的旋转运动受到量子力学的约束，只能以微小的、相同的龙卷风形式存在，每个龙卷风都携带一个固定的、不可分割的环量，$\kappa = h/m$。在[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)状态下，流体充满了这些涡旋线的密集、缠结的混乱状态，即“[量子涡旋](@keyword=quantum_vortices|lang=zh-CN|style=Feynman)缠结”。

这就提出了一个绝妙的问题：如果使用黏度来预测[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)起始的经典[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman)在这里无用，那么什么可以取而代之呢？物理学家发现可以构造一个新的、类似的[无量纲数](@keyword=dimensionless_numbers|lang=zh-CN|style=Feynman)：一个“量子[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman)”，$\mathrm{Re}_q = VD/\kappa$，其中 $V$ 是速度，$D$ 是管道直径，而黏度 $\nu$ 已被[环流量子](@keyword=quantum_of_circulation|lang=zh-CN|style=Feynman) $\kappa$ 所取代 [@problem_id:1742091]。再一次，一个经典概念以一颗量子的心重生。

此外，虽然[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)本身是无黏的，但涡旋缠结的混沌之舞——涡旋的拉伸、碰撞和重联——是耗散能量的一种方式。在宏观尺度上，这种缠结表现得*好像*它具有一个有效黏度！美妙的结果是，这种有效的[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)黏度并非某个任意参数，而是与基本的[环流量子](@keyword=quantum_of_circulation|lang=zh-CN|style=Feynman) $\kappa$ 直接成正比 [@problem_id:564077]。黏度的幽灵再次出现，但它的值是由普朗克常数决定的。这个框架使我们能够将[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)的强大工具（如计算移动物体上的表面摩擦力）应用于这些奇特的量子系统，前提是我们正确地考虑了它们奇特的、源于量子的性质 [@problem_id:493284]。

### 奇异动物园：体黏度和[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman)

到目前为止，我们一直在讨论剪切黏度——对剪切流的阻力，就像在吐司上抹蜂蜜一样。但量子世界在其[输运系数](@keyword=transport_coefficients|lang=zh-CN|style=Feynman)的动物园里还有更多惊喜。

考虑一个正在经历均匀压缩或膨胀的[玻色-爱因斯坦凝聚](@keyword=bose_einstein_condensation|lang=zh-CN|style=Feynman)体。这不涉及剪切，但它仍然可以是一个耗散过程。为什么？一个BEC不仅仅是一个平静的凝聚原子海洋；它还充满了基本激发或“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”的气体——在这种情况下，是[声子](@keyword=phonons|lang=zh-CN|style=Feynman)，即声音的量子。当你压缩凝聚体时，你扰乱了这个[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)的平衡。系统通过产生或消灭[声子](@keyword=phonons|lang=zh-CN|style=Feynman)来缓慢地回到平衡状态的挣扎，产生了一种类似摩擦的效应。这就是体黏度 $\zeta$，一种对压缩而非剪切的阻力 [@problem_id:623231]。它是一种并非源于粒子相互碰撞，而是源于量子流体自身激发的生与死的黏度。

也许这个动物园中最奇特的生物是[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman) $\eta_H$。它出现在强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下的二维电子系统中，这是量子霍尔效应的背景。与剪切或体黏度不同，[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman)是完全*非耗散*的。它不会将能量转化为热量。相反，它产生一个与速度梯度方向*垂直*的力。

想象一下搅动一种经典流体；剪切黏度会产生一个抵抗你勺子运动的阻力。如果你能搅动一个量子霍尔流体，[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman)会产生一个*侧向*推动你勺子的力！这种奇怪的行为是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)破坏时间反演对称性的一个深刻结果。[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman)的值不仅仅是某个随机数；它是量子化的，并由多体量子波函数本身的一个深刻的几何性质——“平均轨道自旋”——所决定 [@problem_id:818015]。在某种意义上，它既是一个[输运系数](@keyword=transport_coefficients|lang=zh-CN|style=Feynman)，也是一个[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)。这不仅仅是一个理论上的好奇心；它具有真实的力学后果。例如，一个放置在流动的量子霍尔流体中的旋转物体将会体验到一个横向[升力](@keyword=lift_force|lang=zh-CN|style=Feynman)，部分原因就是这种奇异的[霍尔黏度](@keyword=hall_viscosity|lang=zh-CN|style=Feynman) [@problem_id:682865]。

从平凡到奇异，量子气体中黏度的概念就像一根线，连接着不同的领域。它将芯片中电子的行为与[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)的物理学联系起来，将[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)的混沌与量子力学的基础联系起来，将流体力学与[量子物质](@keyword=quantum_matter|lang=zh-CN|style=Feynman)的深刻拓扑学联系起来。这是一个惊人的提醒，即便是最简单的经典思想，当用量子的眼光重新审视时，也[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)领我们踏上一段不可思议的发现之旅。