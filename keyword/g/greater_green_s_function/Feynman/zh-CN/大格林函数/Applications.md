## 应用与跨学科联系

在上一章中，我们深入探讨了Keldysh形式主义的形式机制，介绍了其中的角色：推迟、超前、小和巨格林函数。你可能感觉有点像一个刚刚学会所有国际象棋规则——各种棋子的走法、吃子规则和特殊情况——但还未见过一盘真实对局的学生。所有这些复杂的框架究竟是*为了什么*？它能解决什么问题？它揭示了什么新的物理学？

现在，让我们开始对弈吧。本章是一次穿越这种强大形式主义应用领域的旅程。我们将看到，这些[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)不仅仅是抽象的数学对象；它们是我们窥探量子粒子熙攘动态世界的最直接窗口。它们是我们用来理解当我们通过向系统照射光、施加电压或加热其一端来扰动它，使其脱离宁静平衡时会发生什么的工具。我们将发现，这种语言具有惊人的普适性，能描述从纳米晶体管中的电流到绝缘晶体中的热流等各种现象。

### 眼见为实：如何“测量”格林函数

我们新工具最直接、最令人满意的应用或许是在理解我们如何*看见*[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。我们如何通过实验验证[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman)（$G^<$）和巨[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)（$G^>$）所描述的粒子和空穴态的存在？答案在于现代谱学的强大技术。

想象一个晶体，一个由占据不同能级的电子组成的广阔城市。我们想为这个城市绘制一幅地图——哪些房子有人住，哪些是空的？一种方法是挨家挨户地敲出一个电子。这就是**[角分辨光电子能谱](@keyword=arpes|lang=zh-CN|style=Feynman)（[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)）**的精髓。在ARPES实验中，我们用高能[光子](@keyword=photon|lang=zh-CN|style=Feynman)轰击材料。当[光子](@keyword=photon|lang=zh-CN|style=Feynman)击中一个电子时，可以给它足够的能量，使其完全从材料中被弹出。然后我们捕捉这个被弹出的电子，并测量它的能量和动量。由此，我们可以推断出它在晶体*内部*所具有的能量和动量。

那么，这个过程发生的概率是多少？这取决于两件事：首先，那里要有一个电子可以被敲出；其次，量子力学定律允许存在具有该特定能量和动量的电子态。第一个条件——初始态的占据情况——正是[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman) $G^<(\mathbf{k}, \omega)$ 所描述的！事实上，在标准近似下，[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)实验中测得的强度与占据[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)成正比，对于热平衡系统，这由 $I_{\mathrm{PES}}(\mathbf{k},\omega) \propto f(\omega) A(\mathbf{k},\omega)$ 给出，其中 $A(\mathbf{k},\omega) = i[G^>(\mathbf{k},\omega) - G^<(\mathbf{k},\omega)]$ 是总谱函数，$f(\omega)$ 是我们熟悉的[费米-狄拉克分布](@keyword=fermi_dirac_distribution|lang=zh-CN|style=Feynman)。本质上，ARPES直接测量了电子能谱的占据部分，为 $iG^<(\mathbf{k},\omega)$ 提供了令人惊叹的实验可视化。

那么空房子呢？要绘制那些，我们不能敲出任何人。相反，我们必须尝试把某人*放进去*。这就是**反光[电子能谱](@keyword=electron_energy_spectrum|lang=zh-CN|style=Feynman)（IPES）**背后的思想。在这里，我们向材料发射一束电子。如果一个电子找到了一个可以跃入的空态，它就会这样做，并在此过程中发射一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。通过测量这个发射[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量，我们可以计算出电子刚刚填充的空态的能量。这种情况发生的几率取决于空态的可用性，这正是巨格林函数 $G^>(\mathbf{k}, \omega)$ 所携带的信息。测得的IPES强度与*未占据*态的密度成正比，由 $I_{\mathrm{IPES}}(\mathbf{k},\omega) \propto [1-f(\omega)] A(\mathbf{k},\omega)$ 给出。

总而言之，[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)和IPES为我们提供了材料中单粒子激发的完整图像。它们是[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman)和巨[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)的实验体现，将这些理论概念转化为有形的、可测量的谱。一个简单但富有启发性的理论模型是单点[Hubbard模型](@keyword=hubbard_model|lang=zh-CN|style=Feynman)，我们可以用它来显式计算 $G^>(\omega)$，并看到它由对应于向系统添加一个电子所需的不同能量的尖锐峰组成，从而从[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)揭示了谱的起源。

### 纳米世界的心跳：[量子输运](@keyword=quantum_transport|lang=zh-CN|style=Feynman)

虽然谱学是关于被动观察的，但Keldysh形式主义的真正威力在于我们主动将系统驱动到非平衡状态时。这方面的典型例子是[量子输运](@keyword=quantum_transport|lang=zh-CN|style=Feynman)——研究电子如何流过纳米级结构。

思考一下量子物理学家最喜欢的玩具：**量子点**，一个如此之小的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)材料岛，以至于只能容纳少数几个电子。让我们把这个点放在两个大的金属接触（一个“源极”和一个“漏极”）之间，并在它们之间施加一个电压。电子现在将从源极流经量子点，进入漏极。这实际上是世界上最小的晶体管。我们如何计算电流呢？

这是一个经典的非平衡问题。源极和漏极各自处于自身的[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)，但化学势不同，从而产生稳定的粒子流。[Meir-Wingreen公式](@keyword=meir_wingreen_formula|lang=zh-CN|style=Feynman)是[非平衡物理学](@keyword=non_equilibrium_physics|lang=zh-CN|style=Feynman)的一个基石性成果，它直接用[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)的语言给出了答案。它指出，从一个电极流入[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)的电流是粒子进入和粒子离开之间微妙平衡的结果，表示为：
$$
I_\alpha \propto \int d\omega \, \text{Tr}\left[ \mathbf{\Sigma}_\alpha^<(\omega) \mathbf{G}^>(\omega) - \mathbf{\Sigma}_\alpha^>(\omega) \mathbf{G}^<(\omega) \right]
$$
这里有非常优美的物理直觉。项 $\mathbf{\Sigma}_\alpha^<(\omega)$ 代表电极试图向[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)注入电子的速率，而 $\mathbf{G}^>(\omega)$ 代表量子点上可用于接收它们的空态的可用性。第二项 $\mathbf{\Sigma}_\alpha^>(\omega)\mathbf{G}^<(\omega)$ 代表逆过程：[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)上的电子（由 $\mathbf{G}^<$ 描述）试图逃逸到电极中的空态（由 $\mathbf{\Sigma}_\alpha^>$ 描述）。净电流是这场微观拔河比赛的结果，在所有能量上积分得到。使用这种形式主义，我们可以推导出著名的Landauer[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)公式，它将宏观属性（电流）与[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)的微观量子透射特性联系起来。

我们可以问更详细的问题。例如，在给定的电压下，驻留在量子点上的平均电子数是多少？这也可以通过对[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman)积分得到，$N = -i \int (d\omega/2\pi) G^<(\omega)$。这引出了一个更深的概念：**非[平衡分布](@keyword=equilibrium_distribution|lang=zh-CN|style=Feynman)函数**。在平衡状态下，能级的占据由普适的费米-狄拉克函数给出。但在非平衡状态下，情况要复杂得多。我们可以定义一个有效的、依赖于能量的占据函数 $f_d(\omega)$，作为占据态密度与总[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)的比率，$f_d(\omega) = i G^<(\omega) / A(\omega)$。这个函数不再是一个简单的[阶跃函数](@keyword=staircase_function|lang=zh-CN|style=Feynman)；它是一个由偏压以及，至关重要的，[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)上的[电子-电子相互作用](@keyword=electron_electron_interactions|lang=zh-CN|style=Feynman)所塑造的复杂景观。它显示了[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)内部的[非弹性散射](@keyword=inelastic_scattering|lang=zh-CN|style=Feynman)过程如何重新分布电子，创造出一个独特的[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)布居，这是非平衡状态的标志。

### 超越平均：涨落的交响曲

平均电流并不是故事的全部。因为电子是分立的粒子，它们的流动不是完全平滑的；它是有“散粒”性的。在平均值周围存在随机波动，这种现象被称为**[散粒噪声](@keyword=shot_noise|lang=zh-CN|style=Feynman)**。这种噪声不仅仅是实验上的麻烦；它包含了关于[电荷输运](@keyword=charge_transport|lang=zh-CN|style=Feynman)性质的深刻信息，例如载流子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)（如在分数量子霍尔效应中）以及它们之间的关联。

我们的形式主义能描述这些涨落吗？绝对可以。量子点上[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的[双时关联函数](@keyword=two_time_correlation_function|lang=zh-CN|style=Feynman) $\langle \delta\hat{n}(t) \delta\hat{n}(0) \rangle$ 量化了噪声，可以直接用格林函数表示。噪声[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)，即其傅里叶变换，结果是[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman)和巨格林[函数的卷积](@keyword=convolution_of_functions|lang=zh-CN|style=Feynman)：$S(\omega) \propto \int dE \, [G^<(E)G^>(E+\omega) + G^>(E)G^<(E-\omega)]$。这是一个优美的结果。它告诉我们，噪声源于电子到达[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)（与 $G^<$ 相关）和有一个空态可供其离开（与 $G^>$ 相关）的关联事件序列，反之亦然。不仅能计算平均值，还能计算其涨落，这是[非平衡格林函数](@keyword=non_equilibrium_green_s_functions|lang=zh-CN|style=Feynman)方法的一大胜利。

### 一种普适语言：从电子到[声子](@keyword=phonons|lang=zh-CN|style=Feynman)及更广领域

到目前为止，我们的讨论都集中在电子上。但正是在这里，该形式主义真正的美丽和力量得以彰显。我们刚刚讲述的故事并*不只*是关于电子的。这是一个关于量子粒子在非平衡状态下输运的普适故事。

考虑热输运。在许多材料中，特别是绝缘体，热量不是由电子携带，而是由**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**——[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的量子化[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)——携带。想象我们通过一个中心散射区域连接两个保持在不同温度 $T_L$ 和 $T_R$ 的材料，从而构建一个“[声子](@keyword=phonons|lang=zh-CN|style=Feynman)”器件。热流将从较热的一端流向较冷的一端。

我们如何描述这个过程？我们只需用[声子](@keyword=phonons|lang=zh-CN|style=Feynman)算符替换我们的电子算符，用[声子](@keyword=phonons|lang=zh-CN|style=Feynman)格林函数替换我们的电子[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)。整个Keldysh机制可以无缝转换。[稳态热流](@keyword=steady_state_heat_flow|lang=zh-CN|style=Feynman)的表达式，即Caroli-[Landauer公式](@keyword=landauer_formula|lang=zh-CN|style=Feynman)，看起来与Meir-Wingreen[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)公式惊人地相似：
$$
J_Q = \int_0^\infty \frac{d\omega}{2\pi} \hbar\omega \, \mathcal{T}(\omega) [n_B(\omega, T_L) - n_B(\omega, T_R)]
$$
在这里，$\mathcal{T}(\omega)$ 是[声子](@keyword=phonons|lang=zh-CN|style=Feynman)透射函数，$n_B(\omega, T)$ 是[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的[玻色-爱因斯坦分布](@keyword=bose_einstein_distribution|lang=zh-CN|style=Feynman)函数。透射函数本身由[声子](@keyword=phonons|lang=zh-CN|style=Feynman)格林函数和[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)的迹给出，$\mathcal{T}(\omega) = \text{Tr}[\Gamma_L D^R \Gamma_R D^A]$，这与电子的情况完全类似。这揭示了输运物理学深层次的统一性：由偏压（无论是化学势还是温度）驱动的粒子流动的基本逻辑是相同的，无论粒子是像电子这样的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)还是像[声子](@keyword=phonons|lang=zh-CN|style=Feynman)这样的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)。

该形式主义不仅孤立地描述不同类型的粒子；它还擅长描述它们的相互作用。例如，在金属中，流动的电子可以与[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)发生散射，传递能量和动量。这个过程会阻尼[声子](@keyword=phonons|lang=zh-CN|style=Feynman)，限制它们的寿命。我们可以通过计算[声子](@keyword=phonons|lang=zh-CN|style=Feynman)自能来计算这个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)阻尼率，这涉及到电子的[小格林函数](@keyword=lesser_green_s_function|lang=zh-CN|style=Feynman)和巨[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)的“气泡”图。这为我们提供了对[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)由于周围电子海洋而经历的摩擦的定量理解。[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)分量本身也获得了直接的物理意义：例如，小自能 $\Sigma^<(\omega)$ 与由于相互作用，粒子被散射*到*能量为 $\omega$ 的态的速率成正比，为形式理论与[系统动力学](@keyword=phylodynamics|lang=zh-CN|style=Feynman)之间提供了生动的联系。

从谱学到[纳米电子学](@keyword=nanoelectronics|lang=zh-CN|style=Feynman)，从电流到热流，从[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)噪声到[声子](@keyword=phonons|lang=zh-CN|style=Feynman)阻尼——巨格林函数及其Keldysh伙伴们提供了一个单一、连贯且极其优美的框架。它们是我们希望理解在一个远离平衡静谧沉睡的世界里，粒子丰富、动态且奇妙复杂的舞蹈时所使用的语言。