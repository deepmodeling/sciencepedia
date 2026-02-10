## 应用与跨学科联系

在上一章中，我们拆解了GCaMP这个精美的小机器，理解了[蛋白质工程](@keyword=protein_engineering|lang=zh-CN|style=Feynman)如何将一种不起眼的水母蛋白和我们自身肌肉机制的一部分，转变成一个通过发光来报告钙离子情况的[分子探针](@keyword=molecular_probes|lang=zh-CN|style=Feynman)。我们了解了它的工作原理。现在，我们将看到它的回报。我们能用这样的工具*做*什么？它开启了哪些新世界？

这就像被赋予了一种新的感觉。想象一下，你突然能够*看见*电流的流动。你看着收音机，看到的将不仅仅是一个盒子，而是一场由电流和电场组成的充满活力的互动之舞。GCaMP赋予了我们类似的能力，但对象是活细胞的内部世界。它让我们能够观察由钙离子潮汐携带的秘密信息，这些信息调控着生命的进程。我们将从GCaMP一举成名的地方——错综复杂的大脑——开始我们的旅程，并由此发现，钙的语言是普适的，在生命界每个宁静的角落都被使用着。

### 照亮大脑的内部运作

大脑是一个密度惊人的网络，估计有八百六十亿个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)通过数万亿个突触相连。在很长一段时间里，神经科学家就像试图借助[烛光](@keyword=candela|lang=zh-CN|style=Feynman)绘制大陆地图的制图师，一次只能费力地追踪一条路径。GCaMP与另一项[生物工程](@keyword=biological_engineering|lang=zh-CN|style=Feynman)奇迹——[光遗传学](@keyword=optogenetics|lang=zh-CN|style=Feynman)——相结合，打开了探照灯。

通过[光遗传学](@keyword=optogenetics|lang=zh-CN|style=Feynman)，我们可以在特定[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中插入光敏通道，从而只需闪烁一下光脉冲，就能让选定的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)发放动作电位。现在，假设我们将这些光遗传学开关放入一个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)，并将我们的GCaMP探针放入其邻近的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)。然后我们可以玩一个简单的游戏：我们用光照射第一个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)，实际上是告诉它“说话”，然后用我们的GCaMP传感器观察第二个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)，看它是否在“倾听”。如果第二个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)出现一道绿光闪烁，就意味着钙离子涌入，这是它接收到信息的明确信号。我们刚刚证明了一个功能性的突触连接。通过在大脑中重复这个过程，我们就可以开始绘制神经环路的真实、功能性的布线图，而不仅仅是其静态的解剖结构 ([@problem_id:2336428])。

但这种全光学方法能做的不仅仅是绘制连接图。它还可以测量大脑运作的[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)。一条信息穿过[突触间隙](@keyword=synaptic_cleft|lang=zh-CN|style=Feynman)需要多长时间？通过将突触后细胞中的GCaMP与突触前末梢中另一种颜色的传感器——一种报告电压的传感器——相结合，我们可以为整个序列计时。我们可以看到电脉冲到达轴突末梢，然后片刻之后，看到间隙对面的树突中GCaMP信号开始上升。这两个事件之间的时间差就是突触延迟，这是一个以毫秒级精度测量的[神经通讯](@keyword=neural_communication|lang=zh-CN|style=Feynman)基本参数 ([@problem_id:2336435])。

当然，大脑的对话不是简单、单调的交流。连接的强度——突触“私语”的“音量”——会随着经验而改变。这种突触可塑性被认为是学习和[记忆的细胞基础](@keyword=cellular_basis_of_memory|lang=zh-CN|style=Feynman)。GCaMP为我们提供了一个前所未有的窗口来观察这些机制。一个经典的例子是“双脉冲易化”，即两个快速连续发放的脉冲导致第二个响应比第一个大得多。主流假说一直认为，第一个脉冲产生的一些钙离子残留在轴突末梢，与第二个脉冲产生的钙离子叠加，导致更大规模的[神经递质释放](@keyword=neurotransmitter_release|lang=zh-CN|style=Feynman)。通过在[突触前末梢](@keyword=presynaptic_terminal|lang=zh-CN|style=Feynman)表达GCaMP，我们现在可以直接观察到这一过程的发生。我们可以看到第一个脉冲产生的钙离子，看到它并未完全回到基线水平，然后看到第二个脉冲在这些残留钙离子的基础上达到一个更高的峰值，为这个长期存在的理论提供了直接证据 ([@problem_id:2336406])。

最深刻的可塑性形式，即那些持续数小时或数天并构成[长期记忆](@keyword=long_term_memory|lang=zh-CN|style=Feynman)基础的形式，被称为[长时程增强](@keyword=long_term_potentiation|lang=zh-CN|style=Feynman)（Long-Term Potentiation, LTP）和[长时程抑制](@keyword=long_term_depression|lang=zh-CN|style=Feynman)（Long-Term Depression, LTD）。一个著名的理论假设，一个突触的命运——是增强还是减弱——取决于钙离子流入一个称为[树突棘](@keyword=dendritic_spines|lang=zh-CN|style=Feynman)的微小突触后隔室的精确动力学。据信，大量而短暂的钙离子涌入会触发LTP，而较温和、持续的钙离子水平升高则会触发LTD。几十年来，这是一个优美但难以证明的想法。现在，借助能够将激光聚焦到单个[树突棘](@keyword=dendritic_spines|lang=zh-CN|style=Feynman)上的[双光子显微镜](@keyword=two_photon_microscopy|lang=zh-CN|style=Feynman)，科学家们可以进行一项几乎令人难以置信的精细实验。他们可以在一个突触上触发可塑性，同时使用GCaMP在小于一立方微米的体积内测量由此产生的钙信号。这些实验使我们能够将钙信号的数量和持续时间与突触强度的变化直接关联起来，最终在记忆诞生的终极物理尺度上检验“钙控制假说” ([@problem_id:2840049])。

到目前为止，我们一直在倾听个别的对话。但是群体的喧嚣呢？成千上万[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的集体活动意味着什么？这就是[神经编码](@keyword=neural_coding|lang=zh-CN|style=Feynman)的领域。通过构建[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中充满GCaMP的[基因工程](@keyword=genetic_engineering|lang=zh-CN|style=Feynman)小鼠，我们可以使用宽场显微镜观察大量脑细胞在动物看、闻或听的时候被点亮。想象一下，在小鼠嗅闻一种气味时观察其嗅球。一个特定而复杂的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)模式会闪烁。小鼠嗅闻另一种气味；另一个不同的模式出现。关于气味的信息就*在*那个模式中。我们可以更进一步，利用数学构建一个“解码器”。这个[算法分析](@keyword=analysis_of_algorithms|lang=zh-CN|style=Feynman)GCaMP的活动模式并做出预测：“小鼠正在闻香蕉。”通过检验我们的解码器是否正确，我们就能开始学习大脑的真正语言，这是理解感官体验如何在大脑中表征的关键一步 ([@problem_id:2336432])。

### 超越[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)：一种普适的信使

尽管[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)备受关注，但它们并非大脑中唯一的细胞。它们由大量的胶质细胞（如星形胶质细胞）支持。这些细胞曾被认为是单纯的被动支架，但我们现在知道它们是大脑功能的积极参与者。我们是怎么知道的？通过将我们的GCaMP工具包应用于它们。通过在活体动物的[星形胶质细胞](@keyword=astrocytes|lang=zh-CN|style=Feynman)中特异性表达GCaMP，我们可以在动物体验[世界时](@keyword=universal_time|lang=zh-CN|style=Feynman)观察它们。吹向胡须的一股气流不仅会使[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)放电，还会在周围的星形胶质细胞内触发可靠且空间局域化的[钙波](@keyword=calcium_waves|lang=zh-CN|style=Feynman) ([@problem_id:2337065])。大脑的“后勤人员”在交流，而我们第一次能够倾听。

钙的故事不仅仅是关于一个细胞是否放电；它是一个在细胞*内部*，在空间和时间上讲述的故事。一个发生在突触处、持续毫秒的短暂事件，如何导致像建立新记忆这样的永久性变化——一个需要在细胞核中制造新蛋白质的过程？信息必须传递。钙就是那个信息。通过创造靶向特定亚细胞位置的GCaMP版本，我们可以追踪它的旅程。我们可以观察到树突棘中的初始闪光，看到一个更广泛的波在树突中传播，最后，看到细胞核内部的钙浓度上升，在那里它激活了遗传机器以改变细胞的未来 ([@problem_id:2336438])。

这种[局部信号传导](@keyword=local_signaling|lang=zh-CN|style=Feynman)的原理无处不在。以[溶酶体](@keyword=lysosomes|lang=zh-CN|style=Feynman)为例，它们是细胞的回收中心。它们不仅仅是被动的酶囊；它们是活跃的信号中枢。当一个细胞需要加强其回收程序——一个称为[自噬](@keyword=autophagy|lang=zh-CN|style=Feynman)的过程——时，它是由从[溶酶体](@keyword=lysosomes|lang=zh-CN|style=Feynman)表面释放的局部钙离子“喷发”来协调的。这些微小、局部的离子云刚好足以激活附近的酶，如钙调磷酸酶（calcineurin），后者进而开启像TFEB这样的[主转录因子](@keyword=master_transcription_factors|lang=zh-CN|style=Feynman)。借助GCaMP，我们可以量化这些微妙的[细胞器](@keyword=organelles|lang=zh-CN|style=Feynman)特异性信号，模拟特定强度的整合钙信号如何触发下游的[分子开关](@keyword=molecular_switches|lang=zh-CN|style=Feynman)。这是[定量细胞生物学](@keyword=quantitative_cell_biology|lang=zh-CN|style=Feynman)的实践，将物理信号与细胞命运联系起来 ([@problem_id:2813375])。

### 跨越生命王国的旅程

科学中最深刻的发现常常揭示出一种潜在的统一性。支配[行星轨道](@keyword=planetary_orbits|lang=zh-CN|style=Feynman)的原理与支配下落苹果的原理是相同的。生物学也是如此，而GCaMP是我们揭示这种统一性的最佳工具之一。钙的语言是古老的。

思考一下生物学中最深的谜团之一：一个从完美对称的细胞球开始发育的胚胎，如何知道自己的左和右？在脊椎动物中，一个令人难以置信的机制涉及一个微小的流体涡旋。在一个称为左右组织者的结构中，特化的[纤毛](@keyword=cilia|lang=zh-CN|style=Feynman)以协调的方式摆动，产生一股温和的、向左流动的细胞外液。假说认为，周围“冠状”细胞上其他不动的纤毛能“感觉”到这种流动，从而仅在身体左侧触发钙信号，启动一系列基因表达级联反应，最终确定整个[身体蓝图](@keyword=body_plan|lang=zh-CN|style=Feynman)。你怎么可能证明如此微弱的力是原因所在？你可以将GCaMP与[光镊](@keyword=optical_tweezers|lang=zh-CN|style=Feynman)精巧的物理控制相结合。科学家可以用激[光捕获](@keyword=optical_trapping|lang=zh-CN|style=Feynman)一个微珠，并用它作为一个微小的“桨”，在一个表达GCaMP的冠状细胞旁边产生可控的、局部的流体剪切力。当他们这样做时，一道绿光闪现。细胞报告说它感觉到了推动 ([@problem_id:2647644])。这是一个激动人心的实验，是发育生物学、流[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)学和[生物物理学](@keyword=biological_physics|lang=zh-CN|style=Feynman)的完美结合，而所有这一切都得益于我们这个会发光的小小探针。

这种通过钙来感知物理世界的原理无处不在。鱼没有像我们一样的耳朵，但它通过其[侧线系统](@keyword=lateral_line_system|lang=zh-CN|style=Feynman)——一个由称为神经丘的[感觉器官](@keyword=sensory_organs|lang=zh-CN|style=Feynman)组成的阵列——来感知水中的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和压力波。每个神经丘都含有毛细胞，它们是我们内耳细胞的“亲戚”。通过在这些细胞中表达GCaMP，并从不同方向向它们喷射水流，我们可以观察到它们被点亮。我们可以绘制它们的方向调谐曲线，并理解在一个完全不同的感觉模式中机械感知的生物物理原理 ([@problem_id:2588930])。

作为最后一站，让我们冒险进入一个神经科学家很少涉足的领域：植物王国。植物的内部生命肯定是缓慢、平静和无声的吗？远非如此。思考一下一粒花粉落在花朵柱头上后的旅程。它必须长出一条细长的管子，穿过雌性组织，找到一个胚珠进行受精。这不是一个[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)；这是一个需要惊人精度的引导任务。而引导者是什么呢？又一次，是钙。利用[活细胞成像](@keyword=live_cell_imaging_2|lang=zh-CN|style=Feynman)，我们可以在生长的花粉管中表达GCaMP。我们所看到的是一幅美丽的景象：一个持续存在、常常[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的高钙浓度亮尖，像一个指导生长机器的灯塔。通过将GCaMP与用于检测pH或关键信号蛋白等其他[生物传感器](@keyword=biological_sensors|lang=zh-CN|style=Feynman)相结合，我们可以观察到协调这一[植物繁殖](@keyword=plant_reproduction|lang=zh-CN|style=Feynman)基本行为的分子间复杂而动态的对话 ([@problem_id:2662931])。同样的离子，利用与我们大脑中编码思想相同的局部、动态信号传导原理，也引导着[花粉管](@keyword=pollen_tube|lang=zh-CN|style=Feynman)到达其目标。

从绘制大脑环路到解码[神经编码](@keyword=neural_coding|lang=zh-CN|style=Feynman)，从记忆的生物物理学到植物的秘密生活，GCaMP的应用是革命性的。我们构建了一个分子来观察一种离子，并在此过程中获得了新的视野。我们现在可以观看那场无形的交响乐，它在真正意义上就是生命本身的音乐。而最激动人心的部分是，这场演出才刚刚开始。