## 引言
[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是质子和中子密集聚集的集合体，是物理学中最艰巨的[多体问题](@keyword=many_body_problem|lang=zh-CN|style=Feynman)之一。从第一性原理出发，通过追踪每一个组分来描述其结构和动力学，在计算上是难以处理的。玻尔-莫特森模型提供了一个革命性的解决方案，它将[焦点](@keyword=focal_point|lang=zh-CN|style=Feynman)从单个粒子转移到[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)作为一个整体的集体行为上。本文探讨了这个荣获诺贝尔奖的框架，它将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)描绘成一个可形变、转动的液滴。以下各节将首先详细介绍“原理与机制”，解释用于定义[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)形状的几何语言以及支配其[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和转动的动力学。随后，“应用与跨学科联系”一节将展示该模型深远的预测能力及其与凝聚态物理、[核裂变](@keyword=nuclear_fission|lang=zh-CN|style=Feynman)等不同领域的惊人联系。

## 原理与机制

想象一下，你试图描述一个摇晃的水气球的形状。你不会去追踪每一个水分子，那是一项不可能完成的任务。相反，你会谈论它的整体大小、拉伸了多少以及它如何翻滚。玻尔-莫特森模型正是邀请我们以完全相同的方式来看待[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)。它摒弃了数百个质子和中子令人难以置信的复杂性，转而描绘出[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)作为一个单一、统一的物体——一个可以[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)、拉伸和旋转的微小带电液滴。这种无数[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)协同运动的协调行为，正是**[集体运动](@keyword=collective_motions|lang=zh-CN|style=Feynman)**的精髓。我们的任务是发现支配这场优雅核舞蹈的语言和规律。

### [原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)形状的几何语言

我们如何用数学来描述这个核液滴的形状？一个完美的球体很简单，但现实更有趣。[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)偏离球形最常见的方式是获得**[四极形变](@keyword=quadrupole_deformation|lang=zh-CN|style=Feynman)**——它可以被拉伸成雪茄形状或压扁成烙饼形状。我们可以用一组称为[球谐函数](@keyword=y_l^m_functions|lang=zh-CN|style=Feynman)的数学函数，写出[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)在任意方向（$\theta, \phi$）上的半径 $R$ 相对于平均半径 $R_0$ 的微小偏离的公式。在[实验室参考系](@keyword=laboratory_frame|lang=zh-CN|style=Feynman)中，这种描述需要五个复数 $\alpha_{2\mu}$，这似乎相当复杂。

但模型的第一个美妙见解就在于此。就像一个橄榄球有一个天然的“长”轴一样，一个形变的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)也有定义其形状的主轴。为什么不在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)自身的体固[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)中描述它呢？通过旋转我们的数学[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)以与[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)自身的轴对齐，描述得到了极大的简化。与五个复参数 $\alpha_{2\mu}$ 相关联的十个[独立数](@keyword=independence_number|lang=zh-CN|style=Feynman)字，被优雅地换成了仅描述形状的两个内禀实数参数，以及描述该形状在空间中方向的三个[欧拉角](@keyword=euler_angles|lang=zh-CN|style=Feynman) [@problem_id:3595710]。这两个关键的[形状参数](@keyword=shape_parameters|lang=zh-CN|style=Feynman)是：

-   **$\beta$**：这是一个衡量总形变量的参数。$\beta=0$ 代表一个完美的球体。$\beta$ 的值越大，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)偏离球形的程度就越大。

-   **$\gamma$**：这个“三轴性”参数描述了[四极形变](@keyword=quadrupole_deformation|lang=zh-CN|style=Feynman)的*类型*，其常规范围为 $0^\circ$ 到 $60^\circ$。$\gamma=0^\circ$ 对应于[长椭球](@keyword=prolate_spheroid|lang=zh-CN|style=Feynman)形，或“雪茄形”。$\gamma=60^\circ$ 对应于扁椭球形，或“烙饼形”。对于介于两者之间的值 $0^\circ < \gamma < 60^\circ$，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是三轴的，具有三个不相等的轴，就像一个被轻微压扁的橄榄球 [@problem_id:3595770]。

这是一个巨大的简化。追踪所有[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)这个不可能完成的复杂问题，被简化为描述仅仅五个集体坐标的动力学：两个[形状参数](@keyword=shape_parameters|lang=zh-CN|style=Feynman)（$\beta, \gamma$）和三个[欧拉角](@keyword=euler_angles|lang=zh-CN|style=Feynman)。这些抽象参数不仅仅是数学构造；它们具有直接的物理后果。例如，内禀电四极矩，一个衡量核[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)偏离球形程度的物理量，与 $\beta \cos(\gamma)$ 成正比 [@problem_id:3595710]。[长椭球](@keyword=prolate_spheroid|lang=zh-CN|style=Feynman)形[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)具有正的四极矩，而扁椭球形[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)具有负的[四极矩](@keyword=quadrupole_moment|lang=zh-CN|style=Feynman)，这是我们可以在实验室中测量的。

### [原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)之舞：动能

定义了舞台和演员（$\beta, \gamma, \Omega$）之后，我们需要它们运动的脚本——动能。如果我们的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是一个液滴，它如何运动？一个强大而优美的物理假设是，将核流体处理为**无[旋流](@keyword=swirl_flow|lang=zh-CN|style=Feynman)**，就像一种完美的、无粘性的液体，没有任何内部涡旋。如果你搅拌一杯完美的咖啡，整个液体会像一个刚体一样旋转；而在无[旋流](@keyword=swirl_flow|lang=zh-CN|style=Feynman)中，流体元在滑过彼此时自身并不旋转。

从这个单一的假设出发，我们可以推导出集体运动的动能 [@problem_id:3595712]。值得注意的是，总[动能算符](@keyword=kinetic_energy_operator|lang=zh-CN|style=Feynman)可以通过一个称为 Laplace-Beltrami 算符的几何对象来表示，它自然地分离成两个不同的部分：一个与形状变化（即随时间变化的 $\beta$ 和 $\gamma$）相关的**[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)动能**，以及一个与形变体在空间中翻滚相关的**[转动动能](@keyword=rotational_kinetic_energy|lang=zh-CN|style=Feynman)** [@problem_id:3595742]。

[转动能](@keyword=rotational_energy|lang=zh-CN|style=Feynman)量的形式对于任何物理学生来说都非常熟悉：
$$
T_{\text{rot}} = \sum_{k=1}^{3} \frac{\hat{J}_k^2}{2\mathcal{I}_k}
$$
这是一个旋转陀螺的能量，其中 $\hat{J}_k$ 是体固[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)中沿三个[主轴](@keyword=principal_axes|lang=zh-CN|style=Feynman)的角动量分量的算符。但这里有一个深刻的转折。**[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)** $\mathcal{I}_k$ 不是常数。它们是动态量，取决于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)自身的形状！无[旋流](@keyword=swirl_flow|lang=zh-CN|style=Feynman)模型为它们给出了一个非常明确的预测 [@problem_id:3595735] [@problem_id:3595712]：
$$
\mathcal{I}_{k}(\beta,\gamma) = 4B\beta^{2}\sin^{2}\left(\gamma - \frac{2\pi k}{3}\right)
$$
其中 $B$ 是一个也从[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)图像中导出的“质量参数”。这个公式富含物理内涵。它告诉我们转动惯量与 $\beta^2$ 成正比，意味着形变越大的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)“越容易”转动，就像花样滑冰运动员通过收紧手臂来加快旋转速度一样。它还表明，三个[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)通常是不同的，并且取决于三轴性 $\gamma$。参数中循环的 $2\pi/3$ 位移仅仅反映了我们对三个轴（$k=1,2,3$）的标记是约定俗成的；底层的物理学具有一种[离散对称性](@keyword=discrete_symmetry|lang=zh-CN|style=Feynman)。

### 液滴之下的深层：微观起源

液滴图像是一个强大的类比，但[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)并*不是*真正的连续流体。它是一个由相互作用的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)——质子和中子——组成的量子系统。像转动惯量这样的集体性质到底从何而来？玻尔-莫特森模型通过在集体世界和微观单粒子世界之间架起桥梁，实现了其最深刻的预测能力。

**Inglis [摇摆模型](@keyword=cranking_model|lang=zh-CN|style=Feynman)**是一种实现这一目标的绝妙方法 [@problem_id:3595746]。想象你有一个由壳模型描述的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，其[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)占据离散的能级。现在，你“摇动”整个系统，迫使其以一个非常小的恒定[角速度](@keyword=angular_velocity|lang=zh-CN|style=Feynman) $\omega$ 旋转。处于各自量子[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)上的单个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)将抵抗这种强制旋转。你成功在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)中感生出的[总角动量](@keyword=total_angular_momentum|lang=zh-CN|style=Feynman)将与你摇动的速度成正比：$\langle \hat{J} \rangle = \mathcal{I} \omega$。那个比例常数 $\mathcal{I}$ 就是[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)。

由此产生的公式，称为 Inglis 摇摆公式，用单个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的性质来表示集体转动惯量：
$$
\mathcal{I} = 2 \hbar^2 \sum_{p,h} \frac{|\langle p|\hat{J}_x|h\rangle|^2}{\varepsilon_p - \varepsilon_h}
$$
在这里，求和遍及将一个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)从已占据态（“空穴”态，$h$）激发到未占据态（“粒子”态，$p$）的所有可能激发。分子中的项是旋转引起这种跃迁的[量子力学概率](@keyword=quantum_mechanics_probability|lang=zh-CN|style=Feynman)，分母是该跃迁的能量代价。这个公式是一个深刻的陈述：像转动惯量这样的宏观属性，源于所有单个粒子量子力学响应的总和。这是演生现象和不同物理描述统一性的一个美丽例子。

### [原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的肖像：可解极限

有了完整的量子[哈密顿量](@keyword=hamiltonian_function|lang=zh-CN|style=Feynman)，我们原则上可以预测[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的整个能谱。虽然通解异常复杂，但该模型的真正威力在于它能够解决某些极限情况，这些情况直接对应于我们在自然界中观察到的不同“类型”的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)。

-   **[轴对称](@keyword=axial_symmetry|lang=zh-CN|style=Feynman)[刚性转子](@keyword=rigid_rotor|lang=zh-CN|style=Feynman)**：许多重核拥有一个稳定的、明确的[长椭球](@keyword=prolate_spheroid|lang=zh-CN|style=Feynman)形状（$\gamma=0$）。如果我们假设形变 $\beta$ 也固定在某个平衡值 $\beta_0$，那么唯一可用的集体运动就是转动。模型随后预测[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)将有一个能级“[转动带](@keyword=rotational_bands|lang=zh-CN|style=Feynman)” [@problem_id:3595736]。对于[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)带（角动量在[对称轴](@keyword=axis_of_symmetry|lang=zh-CN|style=Feynman)上的投影 $K=0$），能量遵循标志性的公式：
    $$
    E_J = \frac{\hbar^2}{2\mathcal{I}}J(J+1)
    $$
    其中 $J$ 取值为 $0, 2, 4, \dots$。这种简单的二次方间距是核物理学中最著名且得到充分验证的预测之一，以惊人的准确性解释了[形变核](@keyword=deformed_nucleus|lang=zh-CN|style=Feynman)的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)。

-   **$\gamma$-不稳定核**：如果[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是形变的但没有首选的三轴性会怎样？它的势能依赖于 $\beta$ 但相对于 $\gamma$ 是“软”的或平坦的。这种情况揭示了一种被称为 O(5) 对称性的隐藏的、更高层次的对称性。由此产生的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)与[转动带](@keyword=rotational_bands|lang=zh-CN|style=Feynman)完全不同。能级被分组成由量子数 $\tau$（与“高阶数（seniority）”相关）标记的[多重态](@keyword=multiplets|lang=zh-CN|style=Feynman)，它们的能量遵循不同的模式，例如当 $\beta$ 是刚性时 $E \propto \tau(\tau+3)$ [@problem_id:3595724]，或者当 $\beta$ 可以谐振时 $E \propto 2n+\tau+5/2$ [@problem_id:3595753]。这种独特的模式是那些对其三轴形状呈“软性”的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的指纹。

-   **[三轴转子](@keyword=triaxial_rotor|lang=zh-CN|style=Feynman)**：在最一般的情况下，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)可能有一个稳定的、刚性的三轴形状（$0^\circ < \gamma < 60^\circ$）。在这里，所有三个[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)都不同。量子数的清晰分离被打破；特别是，投影 $K$ 不再是一个[好量子数](@keyword=good_quantum_numbers|lang=zh-CN|style=Feynman)。由此产生的能谱更加丰富和复杂，具有诸如在被称为 $\gamma$-带的激发带中能级的“奇偶蹒跚”等特征现象 [@problem_id:3595770]。

### 当舞蹈与摇摆混合：耦合效应

到目前为止，我们的故事将转动和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)视为基本上分离的现象。但在现实世界中，它们是耦合的。想象一团旋转的面团。离心力会使其拉伸和变平。类似地，旋转的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)会伸展，这意味着其形变 $\beta$ 随着角动量的增加而增加。这是一个**转动-[振动耦合](@keyword=vibrational_coupling|lang=zh-CN|style=Feynman)**的例子。

[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)取决于 $\beta^2$，所以当[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)伸展时，其[转动惯量](@keyword=rotational_inertia|lang=zh-CN|style=Feynman)增加。这意味着随着[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)旋转得更快，[转动能级](@keyword=rotational_energy_levels|lang=zh-CN|style=Feynman)之间的间距会缩小。玻尔-莫特森模型允许我们计算这种效应。通过对核形状的零点量子[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)进行平均 rotational energy，我们可以推导出对简单[刚性转子](@keyword=rigid_rotor|lang=zh-CN|style=Feynman)公式的修正项 [@problem_id:3595776]。这个项同时取决于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的转动和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)性质，使得模型能够解释高精度实验中观察到的与简单 $J(J+1)$ 模式的细微偏差。这证明了该模型的精妙之处，它不仅捕捉了核结构的宏观特征，还为理解其错综复杂舞蹈的精细细节提供了一个框架。

