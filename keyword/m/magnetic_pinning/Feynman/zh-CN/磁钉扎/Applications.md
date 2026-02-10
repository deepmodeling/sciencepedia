## 应用与跨学科联系

现在我们已经探讨了[磁钉扎](@keyword=magnetic_pinning|lang=zh-CN|style=Feynman)的基本物理原理——材料中的缺陷如何抓住磁畴壁并将其固定在位——你可能会留下这样的印象：我们作为科学家和工程师的主要目标是创造尽可能原始和完美的材料，让这些磁畴壁自由滑行。有时确实如此。但正如自然界中常见的那样，真正的魔力，最强大和最令人惊讶的技术，在我们学会掌控不完美时才会涌现。现代磁性工程的艺术，在很大程度上，就是有意创造和控制这些钉扎中心的艺术。

最初只是对磁性材料中一种微妙“粘性”的描述，现已发展成为一项强大的设计原则，贯穿了广阔的科学领域。随心所欲地增强或抑制钉扎的能力，使我们能够用相同的基本成分锻造出性质截然不同的材料。在本章中，我们将穿越这些应用领域，你将看到这一个单一的概念——[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)被卡住——是如何成为从电动汽车的强大电机到你电脑中的存储器，再到未来聚变能源的希望等一切事物的关键。

### 两种磁体的故事：硬磁与软磁

想象你有一块铁。你希望它成为一块能永远记住其磁化状态、抵抗任何改变尝试的磁铁吗？还是希望它成为一块能毫不费力地每秒改变主意十亿次的磁铁？材料是相同的，但目的却截然相反。这个谜题的答案，能够将材料从一种特性切换到另一种特性的开关，就是对磁[畴壁钉扎](@keyword=domain_wall_pinning|lang=zh-CN|style=Feynman)的控制。

材料抵抗磁化状态改变的能力由一种叫做[矫顽力](@keyword=coercivity|lang=zh-CN|style=Feynman)的特性来衡量。高[矫顽力](@keyword=coercivity|lang=zh-CN|style=Feynman)意味着它在磁性上是“硬”的——需要很大的力气才能将其退磁。低矫顽力意味着它在磁性上是“软”的——容易磁化和退磁。两者都非常有用，只是用途不同。

对于[永磁体](@keyword=permanent_magnets|lang=zh-CN|style=Feynman)，比如电动马达或风力发电机所需的那些，我们需要尽可能高的[矫顽力](@keyword=coercivity|lang=zh-CN|style=Feynman)。我们需要将磁化锁定在位，并使磁畴壁极难移动。我们如何做到这一点？我们构建一个微观的障碍赛。一个绝妙的策略是使材料的内部结构成为一个由墙壁和栅栏组成的密集迷宫。通过制造具有极小晶粒（小至纳米尺度）的合金，我们极大地增加了晶界的密度。每个[晶界](@keyword=grain_boundary|lang=zh-CN|style=Feynman)都是一个能量上的扰动，充当钉扎中心，阻碍磁畴壁的移动，使材料在磁性上变得“顽固”[@problem_id:1802623]。这种方法在机械工程中有一个美好的类比，即更小的晶粒也会阻碍晶体[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)的运动，使金属在机械上更硬。实际上，简单的物理模型表明，磁矫顽力可以与[晶粒尺寸](@keyword=grain_size|lang=zh-CN|style=Feynman)成反比，这个结果被称为[霍尔-佩奇关系](@keyword=hall_petch_relationship|lang=zh-CN|style=Feynman) (Hall-Petch relation) 的磁性类似物 [@problem_id:1337602]。

另一种同样强大的方法是，在磁性材料中故意[散布](@keyword=dispersal|lang=zh-CN|style=Feynman)微小的非磁性杂质或“析出物”。这些通过精心热处理工程化出的颗粒，就像移动[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)路径上的微观巨石，将其牢固地锚定在位，从而显著增加[矫顽力](@keyword=coercivity|lang=zh-CN|style=Feynman) [@problem_id:1802614]。

但如果你需要完全相反的效果呢？在电力[变压器](@keyword=transformers|lang=zh-CN|style=Feynman)中，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)每秒来回翻转50或60次。如果[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)被钉扎中心卡住，每次循环都必须强行将它们撕开。这个过程以热量的形式耗散能量，这种现象称为[磁滞损耗](@keyword=hysteresis_loss|lang=zh-CN|style=Feynman)。为了制造高效的变压器，我们需要让[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)的移动尽可能平滑。我们需要消除钉扎中心。

所以，我们反其道而行之。我们不是制造微小的晶粒，而是对材料进行[退火](@keyword=annealing|lang=zh-CN|style=Feynman)——一个加热和缓慢冷却的过程——以促使晶粒尽可能长大。具有巨大晶粒的材料每单位体积的[晶界](@keyword=grain_boundary|lang=zh-CN|style=Feynman)非常少，创造了一个广阔、开放的景观，磁畴壁可以在其中以最小的努力和最小的能量损失来回滑行。这正是高效[变压器磁芯](@keyword=transformer_cores|lang=zh-CN|style=Feynman)由大晶粒硅钢制成的原因 [@problem_id:1287645]。

我们甚至可以将这种理念推向其逻辑上的极致。如果我们能完全消除[晶界](@keyword=grain_boundary|lang=zh-CN|style=Feynman)呢？这就是[非晶态](@keyword=amorphous_state|lang=zh-CN|style=Feynman)或“玻璃态”金属背后的想法。通过极快地冷却熔融合金，我们可以在原子有时间[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)之前将其冻结在原位。由此产生的固体没有晶体，因此也没有[晶界](@keyword=grain_boundary|lang=zh-CN|style=Feynman)。虽然在无序结构中仍存在一些由短程涨落引起的次要钉扎，但由于没有强大的晶界钉扎中心，这些材料在磁性上异常柔软。它们表现出极低的[磁滞损耗](@keyword=hysteresis_loss|lang=zh-CN|style=Feynman)，尤其是在高频下，使其成为先进电力电子和高频变压器的首选材料 [@problem_id:1767174]。

### 量子世界中的钉扎

钉扎的重要性并不仅限于电机和变压器的日常世界。同样的基本思想在奇异而美丽的量子力学世界中再次出现，并在那里催生了一些我们最先进的技术。

在[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)中，强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)不会被完全排出。相反，它以微小的、离散的磁通管形式穿透材料。这些“[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)”或“涡旋”就像微观的磁性旋风，每个都携带一个量子化的磁通。现在，如果我们试图让电流通过这个[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，电流会对这些量子旋风施加[洛伦兹力](@keyword=lorentz_force|lang=zh-CN|style=Feynman)。如果这些旋风可以自由移动，它们的运动会产生耗散，我们将其感知为电阻。一个充满可移动[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)不再是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。这是为 MRI 设备或[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)制造高场[超导磁体](@keyword=superconducting_magnets|lang=zh-CN|style=Feynman)所面临的巨大挑战。

解决方案？我们钉扎这些量子旋风。通过在超导基体中有意引入微观缺陷——例如，微小的非超导相颗粒——我们可以创建一个充满“黏性”点的[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)。磁通量子被困在这些钉扎中心。由于[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)被固定，它们无法漂移并引起耗散。这使得材料即使在极强的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中也能无电阻地承载巨大的电流。因此，衡量[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)能承载多少电流的[临界电流密度](@keyword=critical_current_density|lang=zh-CN|style=Feynman)，直接由这些钉扎中心的强度和密度决定 [@problem_id:2257703]。

一种不同但同样关键的量子钉扎形式是数字时代的核心：自旋电子学。像硬盘驱动器中的读头和磁性随机存取存储器（MRAM）中的单元这样的设备，都是由“[自旋阀](@keyword=spin_valve|lang=zh-CN|style=Feynman)”构成的。[自旋阀](@keyword=spin_valve|lang=zh-CN|style=Feynman)由两个被薄势垒隔开的铁磁层组成。该器件的电阻取决于两层磁化方向是平行还是反平行。为了使其能作为传感器或存储位工作，其中一层必须能够在一个小的外[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中“自由”翻转其磁化方向，而另一层则必须被“钉扎”住，将其磁化方向固定以作为稳定的参考。

这种钉扎是通过界面处一种非凡的量子力学效应实现的，即[交换偏置](@keyword=exchange_bias|lang=zh-CN|style=Feynman)。通过将铁磁层放置在一种称为[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)的特殊磁性材料旁边，在边界两侧的电子自旋之间会产生相互作用。这种界面[交换耦合](@keyword=exchange_coupling|lang=zh-CN|style=Feynman)就像一个强大的锚，产生一个有效的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，将铁[磁层](@keyword=magnetosphere|lang=zh-CN|style=Feynman)的取向锁定在位。这就好像你把其中一块磁铁粘住了，从而可以可靠地测量另一块磁铁的取向 [@problem_id:1301693] [@problem_id:1825675]。这种对界面钉扎的巧妙运用是诺贝尔奖获奖发现——[巨磁阻效应](@keyword=giant_magnetoresistance|lang=zh-CN|style=Feynman)（GMR）的基石，并且对于下一代[计算机存储器](@keyword=computer_memory|lang=zh-CN|style=Feynman)的发展仍然至关重要。

### 作为窗口和开关的钉扎

到目前为止，我们已经看到如何通过工程化钉扎来创造所需的宏观性能。但这种关系也可以反过来利用。钉扎的存在可以作为一个灵敏的探针，揭示材料的隐藏特性，甚至可以作为一个把手，将完全不同的物理现象联系起来。

想象一下未来聚变反应堆内部的严酷环境。结构材料，如特种钢，将不断受到高能中子的猛烈轰击。这种无情的辐照会将原子从其[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)位置上敲出，产生一系列诸如[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)和[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)环之类的微观缺陷。监测这种不断累积的损伤对于安全至关重要，但是你如何能从内部无损地检查反应堆壁的完整性呢？

答案依然是[磁钉扎](@keyword=magnetic_pinning|lang=zh-CN|style=Feynman)。这些由辐射引起的缺陷是[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)的完美钉扎中心。随着材料累积损伤，钉扎中心的密度增加，其磁性变得更硬——矫顽力上升。因此，只需在部件外部进行磁性测量，我们就能直接读出内部原子尺度的损伤程度。[磁钉扎](@keyword=magnetic_pinning|lang=zh-CN|style=Feynman)成为一种强大的诊断工具，一个“晴雨表”，为我们提供了一个窥视材料在最极端环境下健康状况的窗口 [@problem_id:315266]。

也许钉扎最未来的应用在于不同物理领域的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点，即蓬勃发展的多[铁性材料](@keyword=ferroic_materials|lang=zh-CN|style=Feynman)领域。在这里，目标是创造出不同序（如磁性与电性）相互耦合的材料。想象一种复合材料，其中一层[磁致伸缩材料](@keyword=magnetostrictive_materials|lang=zh-CN|style=Feynman)（在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中改变形状）与一层[压电材料](@keyword=piezoelectric_materials|lang=zh-CN|style=Feynman)（受应变时产生电压）结合在一起。电性材料中的畴壁可以产生局部应变，而这种应变反过来又可以作为相邻层中[磁畴壁](@keyword=magnetic_domain_wall|lang=zh-CN|style=Feynman)的钉扎中心。

现在是真正令人兴奋的部分。通过施加外部*电场*，你可以操纵电畴及其相关应变。这样做，你就改变了磁畴壁所经历的钉扎势。你刚刚实现了对[磁钉扎](@keyword=magnetic_pinning|lang=zh-CN|style=Feynman)的电学控制 [@problem_id:2510580]。这为一类革命性的新型电子设备打开了大门，其中信息的磁性比特可能不再由电流产生的高功耗[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)来写入，而是由低功耗的电场来写入。

从[永磁体](@keyword=permanent_magnets|lang=zh-CN|style=Feynman)的蛮力到[量子涡旋](@keyword=quantum_vortices|lang=zh-CN|style=Feynman)的空灵之舞，从计算机的存储器到清洁能源的希望，[磁钉扎](@keyword=magnetic_pinning|lang=zh-CN|style=Feynman)的原理提供了一条统一的线索。它教给我们一个深刻的教训：在物理世界中，瑕疵并非总是缺陷。通过理解和掌握自然界自身的不完美，我们可以引导物质展现出惊人的力量、精妙和实用性。