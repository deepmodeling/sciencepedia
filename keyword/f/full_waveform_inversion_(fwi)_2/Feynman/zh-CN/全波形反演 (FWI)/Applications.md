## 应用与跨学科联系

在了解了[全波形反演](@keyword=full_waveform_inversion|lang=zh-CN|style=Feynman)的复杂原理之后，人们可能很容易将其视为一种用于单一目的的专业工具：窥探地球表面之下。但这样做就像看一个宏伟的交响乐团却只看到小提琴部分。FWI 的真正美妙之处，就像物理学本身的美妙之处一样，不在于其孤立性，而在于其与广阔科学思想景观的深刻联系。FWI 是一个交汇点，一个十字路口，物理学、高等数学、计算机科学和工程学的思想在这里汇聚，以解决一个极其复杂的问题。在探索其应用时，我们不只是在列举用途；我们正在揭示一种非凡的科学原理的统一性。

### 从理想物理到现实图像

FWI 首要且最引人注目的应用当然是在[地球物理学](@keyword=geophysics|lang=zh-CN|style=Feynman)领域。几十年来，科学家们一直试图创造出地球的“CT扫描”图像，而 FWI 是实现这一梦想最大胆的尝试。它被用来生成地下结构的高分辨率图像，以前所未有的清晰度揭示潜在的油气藏，监测[封存](@keyword=sequestration|lang=zh-CN|style=Feynman)的二氧化碳在地下[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)的情况，并帮助我们理解引发地震的复杂断层系统。

但是，将 FWI 从物理学家的黑板上变成一个实用的工具是一项艰巨的努力，一项挑战着[计算极限](@keyword=limits_of_computation|lang=zh-CN|style=Feynman)的挑战。一个单一的 3D FWI 项目可能涉及在数十亿个网格点上模拟数千个时间步的波传播。存储整个正向传播波场的历史以与[反向传播](@keyword=backward_pass|lang=zh-CN|style=Feynman)的伴随波场进行[互相关](@keyword=cross_correlation|lang=zh-CN|style=Feynman)——这是伴随状态法的核心要求——将需要 PB 级的内存，远远超出了即使是最大型超级计算机的容量。这不是一个小麻烦；这是一个根本性的障碍。

解决方案来自计算机科学中的一个绝妙思想：**检查点 (checkpointing)**。我们不保存所有东西，只在稀疏的时间间隔保存几个完整的波场快照。在反向时间运行的伴随计算期间，我们只需通过从最近的前一个检查点重新开始模拟，即可“即时”重新计算必要的前向波场片段。这将一个不可能的内存问题转变为一个可管理的计算问题，用存储换取了额外的浮点运算。这是一个优雅的折衷方案，使大规模 3D FWI 成为可能，证明了[数值算法](@keyword=numerical_algorithms|lang=zh-CN|style=Feynman)和高性能计算架构之间的协同作用 [@problem_id:3593127]。

挑战不止于计算。现实世界的地震数据，不像模拟中的干净信号，是杂乱的。它们被[噪声污染](@keyword=noise_pollution|lang=zh-CN|style=Feynman)，被海面的复杂回波（一种称为**鬼波 (ghosting)** 的现象）扭曲，并且带有声源本身的未知特征。在我们甚至开始反演之前，这些原始数据必须经过细致的预处理。每一步——**去鬼波 (deghosting)**、**震源反褶积 (source deconvolution)**、**滤波 (filtering)** 和**平衡 (balancing)**——都是应用于数据的算子。为了保持伴随法数学上的纯粹性，我们应用于观测数据的每个算子也必须在反演循环内应用于我们的合成数据。此外，梯度计算必须修改为包含这些算子的*伴随*，并以相反的顺序应用。这确保了我们正在最小化一个有意义的物理失配，并且我们的梯度正确地指向“下山”方向 [@problem_id:3598839]。这种在数据处理和算法完整性之间的谨慎平衡，正是抽象的反演理论与现场工程的严酷现实相遇的地方。

### 与其他科学的对话

也许 FWI 最迷人的方面是它作为与其他学科思想交流的枢纽的角色。FWI 中遇到的挑战常常是伪装起来的普遍性问题，而解决方案则常常借鉴于或与乍看之下完全不相关的领域共享。

#### 优化的语言

从本质上讲，FWI 是一个[优化问题](@keyword=optimization_problem|lang=zh-CN|style=Feynman)：我们正在寻找能最好地解释我们数据的地球模型。然而，FWI 目标函数的“地形”是出了名的险恶，充满了无数的[局部极小值](@keyword=local_minimum|lang=zh-CN|style=Feynman)。这些挑战中最臭名昭著的是“周波跳跃”。如果我们对地球模型的初始猜测太差，以至于预测的[地震波](@keyword=seismic_waves|lang=zh-CN|style=Feynman)与真实数据相比，时间上相差超过半个波长，算法就会感到困惑。局部梯度将指向地形中一个邻近但错误的山谷，从而被困住。

一个源自[数值优化](@keyword=numerical_optimization|lang=zh-CN|style=Feynman)通用理论的、非常直观的解决方案是多尺度方法。波的相位误差与频率成正比（$ \Delta\phi = 2\pi f \Delta t $）。因此，即使我们初始的时间误差 $ \Delta t $ 很大，我们总能选择一个足够低的频率 $ f $ 来使[相位误差](@keyword=phase_error|lang=zh-CN|style=Feynman)变小，确保 $ \Delta\phi \lt \pi $。我们仅使用非常低频的数据开始反演。由此产生的平滑、低分辨率图像并不完美，但它为下一阶段提供了更好的猜测，在下一阶段我们引入稍高一些的频率。通过逐步扩大频带，我们逐步引导自己走向高分辨率解，小心翼翼地从其大尺度特征到其精细细节导航优化地形 [@problem_id:3599254]。

即使有好的策略，下降的效率也至关重要。FWI 目标函数的原始梯度通常尺度不佳。在模型的照明良好部分（如震源附近）可能巨大，而在更深、更暗的区域则很小。纯粹沿着梯度方向迈出一步，就像试图通过在某些地方大步跳跃而在另一些地方蹑手蹑脚来下山一样——效率低下且不稳定。在这里，我们可以利用物理洞察力来设计一个**预条件子**。通过推导高斯-牛顿[海森矩阵](@keyword=hessian_matrix|lang=zh-CN|style=Feynman)（一个捕捉目标函数曲率的算子）的[对角近似](@keyword=diagonal_approximation|lang=zh-CN|style=Feynman)，我们可以创建一个缩放图来补偿这些照明效应。这个[基于物理的预条件子](@keyword=physics_based_preconditioners|lang=zh-CN|style=Feynman)平衡了梯度，导致更均匀、更快速的收敛，将一次跌跌撞撞的下降变成一次稳健的迈进 [@problem_id:3601013]。这些策略，连同使用诸如 Wolfe 条件等标准来确保每一步都富有成效的详细机制 [@problem_id:3392092]，都展示了 FWI 作为丰富的[数值优化](@keyword=numerical_optimization|lang=zh-CN|style=Feynman)理论的复杂应用。

#### 来自统计学、[稀疏性](@keyword=sparsity|lang=zh-CN|style=Feynman)和传输理论的启示

标准的 FWI [目标函数](@keyword=objective_function|lang=zh-CN|style=Feynman)基于平方 $ L^2 $ 范数，这相当于假设误差是简单的、不相关的、[高斯分布](@keyword=gaussian_distribution|lang=zh-CN|style=Feynman)的噪声。但如果误差不那么简单呢？如果主导误差是复杂的时间偏移，恰恰是导致周波跳跃的那种呢？这就是 FWI 与统计学和信息论进行深入对话的地方。

通过改变我们对数据提出的问题——也就是说，通过改变[失配函数](@keyword=misfit_function|lang=zh-CN|style=Feynman)——我们可以深刻地改变优化地形。一个革命性的想法是使用来自**最优传输**理论的**Wasserstein 距离**。Wasserstein 距离不是逐点比较两个地震图，而是测量将一个信号重排成另一个信号所需的最小“功”，就好像它们是质量的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)一样。对于简单的[时移](@keyword=time_shifting|lang=zh-CN|style=Feynman)，这种[时移](@keyword=time_shifting|lang=zh-CN|style=Feynman)会导致 $ L^2 $ 范数有许多局部极小值，而平方 Wasserstein 距离则非常简单：一个单一的、凸的抛物线。将其用作[失配函数](@keyword=misfit_function|lang=zh-CN|style=Feynman)可以有效消除周波跳跃，为[优化算法](@keyword=optimization_algorithms|lang=zh-CN|style=Feynman)创造一条更平滑的路径 [@problem_id:3411497] [@problem_id:3607334]。

另一个强大的思想来自信号处理和机器学习领域：**稀疏性**原则。地球的地下通常以相对均一地层之间的清晰边界为特征。我们可以通过寻求拟[合数](@keyword=composite_numbers|lang=zh-CN|style=Feynman)据的最简单模型来表达这一先验知识。这通常通过向[目标函数](@keyword=objective_function|lang=zh-CN|style=Feynman)添加一个 $ L_1 $ 范数正则化项 $ \lambda \|m\|_1 $ 来实现。与平滑的 $ L^2 $ 范数不同，$ L_1 $ 范数促进稀疏性——它鼓励许多模型参数（或其梯度）恰好为零。这可以通过**[近端梯度法](@keyword=proximal_gradient_methods|lang=zh-CN|style=Feynman)**优雅地处理，这种方法将每次迭代分为两部分：对[数据失配](@keyword=data_misfit|lang=zh-CN|style=Feynman)项进行标准的[梯度下降](@keyword=gradient_descent|lang=zh-CN|style=Feynman)步骤，然后应用一个**[近端算子](@keyword=proximal_operators|lang=zh-CN|style=Feynman)**。对于 $ L_1 $ 范数，此算子是一个简单的**[软阈值](@keyword=soft_thresholding|lang=zh-CN|style=Feynman)**函数，它将小值收缩为零，从而在每一步中有效地强制稀疏性 [@problem_id:3392029]。

#### 用数学绘画

有时，FWI 的挑战不是找到一个平滑的模型，而是找到一个尖锐边界的精确位置，比如嵌入在沉积物中的巨大的、高速盐体的边缘。在这里，模型的标准逐像素表示是低效的。在如此强烈的对比度附近，波散射的物理过程变得高度[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)，标准的 FWI 线性化方法失效。

解决方案可以在一个完全不同的领域找到：[计算机图形学](@keyword=computer_graphics|lang=zh-CN|style=Feynman)和[图像处理](@keyword=image_processing|lang=zh-CN|style=Feynman)。我们不将模型描述为值的网格，而是通过盐体的*形状*来描述它。**[水平集方法](@keyword=level_set_method_2|lang=zh-CN|style=Feynman)**正是这样做的。一个平滑的函数，即“水平集”，在整个域上定义，其零等值线隐式地表示盐体的边界。然后，反演求解最优的[水平集](@keyword=level_set_2|lang=zh-CN|style=Feynman)函数，本质上是使边界变形，直到预测数据与观测数据匹配。模型更新不再是每个像素的微小变化，而是界面本身的运动，使用形状微积分的优雅数学来计算。这种重新[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)的方法将反演的力量集中在主导数据的几何特征上，使问题变得更加稳定和易于处理 [@problem_id:3599275]。

### [反问题](@keyword=inverse_problems|lang=zh-CN|style=Feynman)的普适性

FWI 所编织的联系之网揭示了一个普遍的真理：[反问题](@keyword=inverse_problems|lang=zh-CN|style=Feynman)的基本特征由连接其参数与数据的物理学所决定。我们可以通过一个优美的类比来看待这一点。想象一个简单的大气[遥感](@keyword=remote_sensing|lang=zh-CN|style=Feynman)问题，我们测量穿过气体的光，以确定两种不同化学物质的浓度。每种化学物质在自己独特的频率通道吸收光，而不影响另一种。正演模型是[解耦](@keyword=disentanglement|lang=zh-CN|style=Feynman)的。结果，由高斯-牛顿[海森矩阵](@keyword=hessian_matrix|lang=zh-CN|style=Feynman)描述的问题的数学曲率是对角的。对一种化学物质浓度的敏感性与另一种无关 [@problem_id:3603038]。

地震 FWI 则恰恰相反。参数——比如 P 波和 S [波速](@keyword=wave_speed|lang=zh-CN|style=Feynman)度——由[弹性波方程](@keyword=elastic_wave_equation|lang=zh-CN|style=Feynman)的物理学内在耦合。空间中单个点的单个参数变化会影响整个波场，进而影响所有接收器上的信号。这种物理耦合表现为一个稠密的、非对角的海森矩阵，充满了代表参数之间**串扰 (cross-talk)** 的非对角块。这种结构上的差异不仅仅是一个细节；它是问题复杂性的数学体现。

这种洞察力使我们能够将 FWI 不仅仅看作一个自成一类的问题，而是看作一个庞大的、复杂、多物理场耦合反演问题家族中的一员。为 FWI 开发的技术和直觉——从多尺度方法和最优传输[失配函数](@keyword=misfit_function|lang=zh-CN|style=Feynman)到水平集[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)和先进的计算策略——不仅仅是为地球物理学家准备的。它们是强大的思想，适用于任何试图利用波来成像物体内部的领域，无论是在[医学超声](@keyword=medical_ultrasound|lang=zh-CN|style=Feynman)断层成像、材料的[无损检测](@keyword=non_destructive_testing|lang=zh-CN|style=Feynman)，还是[日震学](@keyword=helioseismology|lang=zh-CN|style=Feynman)（研究我们太阳内部的学科）。[全波形反演](@keyword=full_waveform_inversion|lang=zh-CN|style=Feynman)，在它探求照亮地球的过程中，最终也照亮了科学本身美丽而相互关联的本质。