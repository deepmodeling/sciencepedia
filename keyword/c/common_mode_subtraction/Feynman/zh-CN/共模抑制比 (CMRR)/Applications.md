## 应用与跨学科联系

在我们上次的讨论中，我们探索了[共模抑制](@keyword=common_mode_rejection|lang=zh-CN|style=Feynman)的优雅原理。我们看到，自然界以及我们自己的技术，往往充满着压倒性的噪声。我们真正关心的信号——遥远恒星的微弱低语、心跳的微妙[颤动](@keyword=zitterbewegung|lang=zh-CN|style=Feynman)、材料电阻的微小变化——常常被埋没在一座共模“喋喋不休”的大山之下，这种噪声影响着周围的一切。因此，测量的艺术，往往就是减法的艺术：巧妙地忽略共通的部分，以揭示不同之处。

现在，让我们踏上一段旅程，看看这个强大的理念将我们带向何方。你可能会感到惊讶。这不仅仅是电子工程师的技巧；它是一种生命和物理学用以理解世界的基本策略。我们将在浴室体重秤、我们数字世界的核心、未来聚变反应堆的炽[热核](@keyword=heat_kernel|lang=zh-CN|style=Feynman)心，甚至在检验时空结构本身的实验中，看到它的身影。

### 精密测量的世界

让我们从熟悉的事物开始。想象你正在设计一个现代数字秤。重量由一个应变片测量，这是一种当被拉伸时电阻会发生微小变化的传感器。为了测量这个微小的变化，我们将其置于一个称为[惠斯通电桥](@keyword=wheatstone_bridge|lang=zh-CN|style=Feynman)的电路中。但有一个问题。整个电桥电路可能相对于系统地线处于，比如说，2.5伏的电压。这个2.5伏的偏置是一个[共模电压](@keyword=common_mode_voltage|lang=zh-CN|style=Feynman)。它存在于电桥的两条输出线上。我们想要的实际信号——那个对应于重量的信号——是这两条线之间一个微小的电压*差*，可能只有几百万分之一伏。

你如何放大这个微伏级的差异，而不去同时放大那个巨大的2.5伏偏置呢？你使用一个[差分放大器](@keyword=differential_amplifier|lang=zh-CN|style=Feynman)。它的全部目的就是观察它的两个输入，用一个减去另一个，然后放大结果。但没有放大器是完美的。一小部分[共模电压](@keyword=common_mode_voltage|lang=zh-CN|style=Feynman)总是会泄漏过去。一个好的放大器可能具有86分贝的[共模抑制比](@keyword=common_mode_rejection_ratio|lang=zh-CN|style=Feynman)（CMRR），这意味着它对[共模电压](@keyword=common_mode_voltage|lang=zh-CN|style=Feynman)的抑制能力是[差模信号](@keyword=differential_mode_signal|lang=zh-CN|style=Feynman)的约20,000倍。即便如此，对于2.5V的共模输入，一个小的误差电压仍然会出现在输出端，设计者必须考虑到这一点，以确保你的秤在没有东西时读数为零（[@problem_id:1293347]）。

这个问题不仅限于[直流偏置](@keyword=dc_offset|lang=zh-CN|style=Feynman)。我们的世界充满了电磁噪声，最著名的就是来自我们[电力](@keyword=electric_forces|lang=zh-CN|style=Feynman)线的50或60赫兹的嗡嗡声。想象你是一位电化学家，正在研究一个液体电池中精密的反应（[@problem_id:1562342]）。连接到你电池的电极引线就像小天线一样，会接收到这种嗡嗡声。工作电极和[参比电极](@keyword=reference_electrodes|lang=zh-CN|style=Feynman)都会在这个它们真实[电位](@keyword=electric_potential|lang=zh-CN|style=Feynman)之上叠加一个不希望有的50赫兹[正弦波](@keyword=sinusoid|lang=zh-CN|style=Feynman)。这是一个[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)信号。一个高质量的[恒电位仪](@keyword=potentiostat|lang=zh-CN|style=Feynman)——控制电化学过程的仪器——必须使用具有优异CMRR的[差分放大器](@keyword=differential_amplifier|lang=zh-CN|style=Feynman)来忽略这种嗡嗡声，只测量决定[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的真实电位差。没有它，仪器将试图控制一个大部分是噪声的信号，实验也将毫无意义。这是所有精密仪器面临的普遍挑战：放大所需的[差模信号](@keyword=differential_mode_signal|lang=zh-CN|style=Feynman)，同时抑制不可避免的[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)，无论是直流偏置还是交流嗡嗡声（[@problem_id:1340795]）。

### 从模拟纯净到数字保真

好了，我们现在有了一个干净的[模拟信号](@keyword=analog_signals|lang=zh-CN|style=Feynman)。我们如何将它带入计算机的数字世界？我们使用[模数转换器](@keyword=analog_to_digital_converter_2|lang=zh-CN|style=Feynman)，或称[ADC](@keyword=antibody–drug_conjugates|lang=zh-CN|style=Feynman)。[ADC](@keyword=antibody–drug_conjugates|lang=zh-CN|style=Feynman)测量一个电压并将其表示为一个数字。假设你有一个16位的ADC。这意味着它可以将输入电压范围分解为$2^{16} = 65,536$个不同的级别。对于5伏的范围，最小的电压步长，或称最低有效位（LSB），仅为76微伏。

现在，如果该[ADC](@keyword=antibody–drug_conjugates|lang=zh-CN|style=Feynman)内部的放大器具有有限的CMRR，并且受到例如1.5伏的[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)影响，会发生什么？就像应变片一样，这些噪声的一部分将被转换成误差电压。如果这个误差超过半个LSB——在我们的例子中约为38微伏——ADC就不能再被信任了。它可能输出数字`45132`，而本应是`45131`。你的16位[ADC](@keyword=antibody–drug_conjugates|lang=zh-CN|style=Feynman)的最后一位已经丢失在噪声中了！为了保持所宣传的全部分辨率，工程师必须选择一个具有足够高CMRR的放大器，以将该[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)抑制到远低于LSB水平（[@problem_id:1300333]）。在这里我们看到了一个优美而直接的联系：一个模拟特性，CMRR，决定了一个数字系统的有效精度。

这个原理对于传输数字数据本身也同样至关重要。一个代表“1”或“0”的信号是如何从一个电路板传输到另一个，或者沿着长长的以太网电缆传输到你的电脑，而不会被损坏的？如果你用单根导线发送它，那根导线就像一根天线，会拾取噪声。解决方案是[差分信号传输](@keyword=differential_signaling|lang=zh-CN|style=Feynman)。我们不用一根线，而是用两根，通常绞合成“双绞线”。我们将信号沿着一根线发送，同时将其精确的反相信号沿着另一根线发送。远端的接收器对任何一根线上的绝对电压不感兴趣；它只关心它们之间的*差值*。

来[自环](@keyword=self_loop|lang=zh-CN|style=Feynman)境的噪声，比如附近的[电动机](@keyword=electric_motor|lang=zh-CN|style=Feynman)，会在两根导线上同时感应出几乎相同的电压尖峰。这是一个共模干扰。当差分接收器将两个信号相减时，这个[共模噪声](@keyword=common_mode_noise|lang=zh-CN|style=Feynman)就消失了！这就是为什么像USB、HDMI和以太网这样的高速数据链路都依赖于[差分对](@keyword=differential_pair|lang=zh-CN|style=Feynman)的根本原因。发射极耦合逻辑（ECL）是一种非常快速的[数字电路](@keyword=digital_circuits|lang=zh-CN|style=Feynman)，它的天才之处在于它能自然地提供一个信号及其[补码](@keyword=twos__complement|lang=zh-CN|style=Feynman)，使其非常适合驱动双绞线并实现这种卓越的噪声抗扰性（[@problem_id:1932363]）。

这一切的关键是构建一个好的减法器。在流行的三[运放](@keyword=op_amp|lang=zh-CN|style=Feynman)[仪表放大器](@keyword=instrumentation_amplifier|lang=zh-CN|style=Feynman)中，第一级巧妙地放大了[差模信号](@keyword=differential_mode_signal|lang=zh-CN|style=Feynman)，同时让[共模信号](@keyword=common_mode_signal|lang=zh-CN|style=Feynman)以单位增益通过。执行关键减法操作的是最后的第二级——一个经典的[差分放大器](@keyword=differential_amplifier|lang=zh-CN|style=Feynman)，它消除了第一级在其两个输出上精心保留的共模分量（[@problem_id:1293331]）。

### 高风险与高科技

在追求清洁能源的过程中，对[共模抑制](@keyword=common_mode_rejection|lang=zh-CN|style=Feynman)的需求成为了一个关乎机器生死存亡的问题。考虑一个[托卡马克](@keyword=tokamaks|lang=zh-CN|style=Feynman)（tokamak），一种旨在实现核聚变的装置。它使用巨大的[超导磁体](@keyword=superconducting_magnets|lang=zh-CN|style=Feynman)，承载着数万安培的电流，来约束比太阳还热的等离子体。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)电阻为零，但如果磁体的任何部分稍微升温并失去其超导性——这种事件被称为“失超”（quench）——它会突然变得有电阻。这个小的电阻段会迅速[过热](@keyword=superheating|lang=zh-CN|style=Feynman)，并对价值数百万美元的磁体造成灾难性损害。

为了防止这种情况，工程师必须检测出新产生的电阻段上出现的微小电压（$V = IR$）。问题在哪里？在操作过程中，这些巨大线圈中的电流会上升和下降，在线圈上感应出巨大的电压——数百甚至数千伏。当你将两个电压抽头连接到线圈的一小段时，它们都承载着这个巨大且快速变化的[共模电压](@keyword=common_mode_voltage|lang=zh-CN|style=Feynman)。失超信号就是一个微小的差模电压，埋藏在[共模电压](@keyword=common_mode_voltage|lang=zh-CN|style=Feynman)的滔天巨浪之中。

一个具有有限CMRR的检测系统会把一小部分大的共模感应尖峰误认为差模失超信号。这可能导致“误报”，触发反应堆的紧急停堆，浪费时间和资源。为了防止这种情况，工程师必须要求其电子设备具有极高的性能。一个系统要可靠地忽略100V的共模摆幅，同时寻找毫伏级的信号，可能需要$10^5$或100分贝的CMRR（[@problem_id:3716175]）。在这个极端环境中，[共模抑制](@keyword=common_mode_rejection|lang=zh-CN|style=Feynman)不仅仅关乎[数据质量](@keyword=data_quality|lang=zh-CN|style=Feynman)；它是整个机器安全和保护系统的基石。

### 原理的普适性

这种抑制共同背景以观察差异特征的思想是如此基本，以至于我们在远离电子学的领域也能找到它。想想测量地球[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。如果你正在寻找一个微小的异常——也许来自一艘潜艇或一个矿藏——你面临的挑战是你正处在地球更大的背景[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)之中。

你如何抵消它？你可以建造一个磁梯度计。一个简单的设计使用两个相同的线圈，反向绕制并[串联](@keyword=catenation|lang=zh-CN|style=Feynman)连接（[@problem_id:3018021]）。如果你把这个装置放在一个完全均匀的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，穿过第一个线圈的磁通量会被穿过第二个线圈的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)完全抵消。净输出为零。均匀场是“共模”，装置会抑制它。然而，如果场有梯度——如果它在一个线圈处比另一个稍强——抵消就不再完美，从而产生一个净信号。该装置对梯度（[差模信号](@keyword=differential_mode_signal|lang=zh-CN|style=Feynman)）敏感，但对均匀背景“视而不见”。当然，“完美”是一个难以企及的词。两个线圈面积的微小不匹配，比如百分之几，会限制共模场被抑制的程度，从而给仪器一个有限的“CMRR”。这与[差分放大器](@keyword=differential_amplifier|lang=zh-CN|style=Feynman)中电阻不匹配的原理完全相同，只不过现在应用于磁通量。

也许这个原理最美丽和深刻的应用是在基础物理学的前沿——原子干涉测量法中找到的。科学家们可以使用[激光](@keyword=laser|lang=zh-CN|style=Feynman)来分裂、重定向和重组超冷原子云，使它们像[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)中的光波一样行事。通过构建两个这样的[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)，一个在另一个之上，他们可以测量[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)拉力的微小差异——从而创建一个[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)梯度计。“信号”是两个原子云之间的差分相移，它取决于[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)梯度。

但是用来操纵原子的[激光](@keyword=laser|lang=zh-CN|style=Feynman)并不完全稳定；它们的相位会随机[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)。由于*同一束*[激光](@keyword=laser|lang=zh-CN|style=Feynman)被用来驱动两个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)，这种[激光](@keyword=laser|lang=zh-CN|style=Feynman)[相位噪声](@keyword=phase_noise|lang=zh-CN|style=Feynman)应该是一种共模扰动，在比较两个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)的相位时会相互抵消。它几乎做到了。它不完美的原因是物理学中最优雅的事实之一：光的有限速度。击中顶部[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)的[激光](@keyword=laser|lang=zh-CN|style=Feynman)光在片刻之后，经过 $\tau = L/c$ 的延迟，才到达底部的[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)，其中 $L$ 是分离距离， $c$ 是光速。由于这个微小的延迟，第二个[干涉仪](@keyword=interferometer|lang=zh-CN|style=Feynman)看到的噪声与第一个看到的噪声并非完全相关。这种基本的时间延迟产生了一个残留的差分噪声，限制了最终的灵敏度。限制[共模抑制](@keyword=common_mode_rejection|lang=zh-CN|style=Feynman)的“不完美”之处，不是制造缺陷，而是宇宙的一个基本常数（[@problem_id:646279]）。

从简陋的浴室体重秤到地球上的恒星之心，从流经电缆的比特到检验[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的[原子量](@keyword=atomic_weight|lang=zh-CN|style=Feynman)子之舞，共模减法的原理始终如一。它证明了一个简单而巧妙思想的统一力量：要找到信号，你必须首先学会忽略什么。