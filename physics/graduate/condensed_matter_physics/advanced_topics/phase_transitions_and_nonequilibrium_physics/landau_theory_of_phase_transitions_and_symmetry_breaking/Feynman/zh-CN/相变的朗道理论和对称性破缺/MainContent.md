## 引言
物质世界充满了奇妙的转变：水结成冰，铁在加热后失去[磁性](@keyword=magnetism|lang=zh-CN|style=Feynman)。这些无处不在的“[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)”现象背后，是否隐藏着统一而深刻的支配法则？20世纪[物理学](@keyword=physics|lang=zh-CN|style=Feynman)巨匠列夫·朗道（Lev Landau）给出了一个非凡的答案：[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)的核心在于[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)的改变。这一洞见如同一把钥匙，为我们打开了理解物质[集体行为](@keyword=collective_behavior|lang=zh-CN|style=Feynman)的大门。本文旨在系统性地介绍[朗道相变理论](@keyword=landau_theory_of_phase_transitions|lang=zh-CN|style=Feynman)。我们将从其核心思想——[对称性破缺](@keyword=broken_symmetry|lang=zh-CN|style=Feynman)与[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)——出发，学习如何利用优美的[朗道自由能](@keyword=landau_free_energy|lang=zh-CN|style=Feynman)函数来描述和预测[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)的发生。随后，我们将见证该理论的巨大威力，看它如何统一解释从日常磁铁到量子[超导体](@keyword=superconductors|lang=zh-CN|style=Feynman)等迥然不同的物理现象。最后，我们还将探索该理论的适用边界，一窥现代凝聚态物理的更前沿图景。这趟旅程将从最基本的原理开始，揭示[物理学](@keyword=physics|lang=zh-CN|style=Feynman)如何将纷繁复杂的现象还原为简洁优美的普适规律。

## 原理与机制

在上一章中，我们已经对[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)现象有了初步的感性认识。我们看到，物质世界在温度或压力的变化下，会呈现出截然不同的“面貌”——水变成冰，铁失去[磁性](@keyword=magnetism|lang=zh-CN|style=Feynman)。现在，我们要像一位侦探，深入其内部，寻找支配这些戏剧性变化的底层逻辑。令人惊奇的是，我们将发现，这一切混乱与变化的背后，隐藏着一个极其深刻而优美的指导原则——**[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)**。

### [对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)：自然的组织法则

想象一下，你身处一个完全均匀的房间，四壁洁白，没有任何标记。你闭上眼睛，原地转任意一个角度，再睁开眼——你无法判断自己是否[转动](@keyword=rotational_motion|lang=zh-CN|style=Feynman)过。这个房间就具有**连续[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性**。现在，如果有人在墙上挂了一幅画，情况就不同了。除非你恰好转了360度，否则你总能发现房间变了样。这幅画的出现，**打破了**房间的[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性。

[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家列夫·朗道（Lev Landau）天才地指出，[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)的核心，正是物质[内部对称性](@keyword=internal_symmetry|lang=zh-CN|style=Feynman)的改变。

在一个高温的、无序的系统中，比如一块滚烫的铁，内部的微小磁体（[原子磁矩](@keyword=atomic_magnetic_moments|lang=zh-CN|style=Feynman)）像一群狂欢的人群，朝向四面八方，没有任何固定的指向。从任何方向看过去，这块铁的宏观[磁性](@keyword=magnetism|lang=zh-CN|style=Feynman)质都是一样的。它具有高度的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，就像那个空无一物的房间。

当我们冷却这块铁，低于一个特定的[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman) $T_c$（[居里温度](@keyword=curie_temperature|lang=zh-CN|style=Feynman)）时，奇妙的事情发生了。内部的微小磁体们仿佛听到了无声的号令，纷纷将自己的指向统一起来，形成一个宏观上可观测到的净[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)。它们“自发地”选择了一个方向。这个选择一旦做出，系统的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)就被打破了。现在，这个[磁化](@keyword=magnetization|lang=zh-CN|style=Feynman)方向和与之相反的方向就变得与所有其他方向不同了。系统从高度[对称](@keyword=symmetry|lang=zh-CN|style=Feynman)的“无序”态，跃迁到了[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)更低的“有序”态。

为了定量地描述这种[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)的变化，我们需要一个“指针”，它能在[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)完好的状态下指向零，而在[对称性破缺](@keyword=broken_symmetry|lang=zh-CN|style=Feynman)的状态下指向一个非零值。这个“指针”就是**[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)**（order parameter）。对于铁磁体，[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)就是宏观[磁化强度](@keyword=magnetization|lang=zh-CN|style=Feynman) $m$ [@problem_id:2999164]。在高温顺[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)，$m=0$；在低温铁[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)，$m\neq 0$。

[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的形式多种多样，它捕捉了特定系统“序”的本质。
- 对于只有“上”和“下”两种状态的[伊辛模型](@keyword=ising_model|lang=zh-CN|style=Feynman)（Ising model），[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)是一个简单的标量 $m$。
- 对于[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)或[超导体](@keyword=superconductors|lang=zh-CN|style=Feynman)，其中的粒子都凝聚到同一个[量子态](@keyword=quantum_states|lang=zh-CN|style=Feynman)，由一个统一的[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)描述。这个[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)具有相位，[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)便是一个[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman) $\psi = |\psi|e^{i\theta}$。它的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)是连续的 $U(1)$ 相位[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性 [@problem_id:2999164]。
- 对于[液晶](@keyword=liquid_crystals|lang=zh-CN|style=Feynman)，棒状分子在某一方向上择优[排列](@keyword=permutations|lang=zh-CN|style=Feynman)，但没有“头”和“尾”的区别（即 $\mathbf{n}$ 和 $-\mathbf{n}$ [等价](@keyword=biconditional|lang=zh-CN|style=Feynman)）。一个简单的矢量无法描述这种“[指向性](@keyword=directivity|lang=zh-CN|style=Feynman)”而非“[方向性](@keyword=directivity|lang=zh-CN|style=Feynman)”的序。[物理学](@keyword=physics|lang=zh-CN|style=Feynman)家构建了一个更为复杂的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)——一个[对称](@keyword=symmetry|lang=zh-CN|style=Feynman)无迹的[二阶张量](@keyword=second_rank_tensor|lang=zh-CN|style=Feynman) $Q_{ij}$ [@problem_id:2999164]。

### [朗道自由能](@keyword=landau_free_energy|lang=zh-CN|style=Feynman)：竞争的舞台

有了[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)这个“演员”，我们还需要一个“舞台”来上演[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)的戏剧。这个舞台就是**[朗道自由能](@keyword=landau_free_energy|lang=zh-CN|style=Feynman)** $F$。在[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)中，系统总是倾向于寻找使其[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)最小的状态。朗道的构想是，把[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)写成[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的函数，$F(m)$，然后通过最小化 $F(m)$ 来找到系统的[平衡态](@keyword=equilibrium_states|lang=zh-CN|style=Feynman)。

构建这个[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)函数，必须遵循一条铁律：**[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)函数本身的形式，必须尊重系统在高温相所具有的全部[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)**。

这条规则看似简单，却威力无穷。我们再次以铁磁体为例。它的高温顺[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)具有“自旋翻转”[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，即 $m \to -m$。这条规则要求[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)函数必须满足 $F(m) = F(-m)$。这意味着 $F(m)$ 必须是 $m$ 的一个[偶函数](@keyword=even_functions|lang=zh-CN|style=Feynman)！如果我们将其展开成 $m$ 的[幂级数](@keyword=power_series|lang=zh-CN|style=Feynman)，所有奇次方的项（如 $m, m^3, \dots$）都必须被禁止，因为它们会破坏这种[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman) [@problem_id:2999203] [@problem_id:2999165]。因此，最简单的形式（忽略空间变化）可以写成：

$$
F(m) = F_0 + \frac{a}{2}m^2 + \frac{b}{4}m^4
$$

这里，$F_0$ 是与 $m$ 无关的背景部分。系数 $a$ 和 $b$ 是依赖于温度和压力的参数。为了保证当 $m$ 很大时系统是稳定的（能量不能无限降低），我们必须要求 $b>0$。

现在，整出戏的关键落在了系数 $a$ 身上。朗道假设在[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman) $T_c$ 附近，$a$ 是温度 $T$ 的简单[线性](@keyword=linearity|lang=zh-CN|style=Feynman)函数，写作 $a(T) = \alpha(T-T_c)$，其中 $\alpha$ 是一个正的常数。

让我们看看这个简单的模型如何导演一出精彩的[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)大戏：

1.  **当 $T > T_c$ 时（高温相）**: $a>0$。此时，[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman) $F(m)$ 的图像是一个开口向上的、类似 $x^2$ 的碗，碗底在 $m=0$ 处（见下图a）。系统为了寻求最低能量，自然会待在碗底，所以[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)为零，$m=0$。这完美地描述了顺[磁相](@keyword=magnetic_phases|lang=zh-CN|style=Feynman)。

2.  **当 $T < T_c$ 时（低温相）**: $a<0$。现在，$m^2$ 项的系数为负，[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)的形状发生了根本性的变化。它不再是一个简单的碗，而是在 $m=0$ 处有一个小凸起，在两边形成了两个更低的“坑”。这著名的形状常被称为“墨西哥帽”势（见下图b）。$m=0$ 从一个稳定的最低点变成了一个不稳定的最高点。系统会滚入其中一个坑里，取一个非零的值 $m_0 = \pm\sqrt{-a/b}$。系统**自发地**选择了一个方向（“+”或“-”），打破了 $m \to -m$ 的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)。这就是**[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)**。

<center>
    <img src="https://i.imgur.com/G4i3wYy.png" alt="Landau Free Energy" width="600">
    <br>
    <small>图：[朗道自由能](@keyword=landau_free_energy|lang=zh-CN|style=Feynman)随温度的变化。(a) $T > T_c$ 时，[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)只有一个位于 $m=0$ 的极小值。(b) $T < T_c$ 时，[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)出现两个位于 $m \ne 0$ 的极小值，系统发生[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)。</small>
</center>

这个简单的理论甚至能做出可以被实验检验的定量预测。例如，它预言了在[临界点](@keyword=tipping_points|lang=zh-CN|style=Feynman)附近，[磁化率](@keyword=magnetic_susceptibility|lang=zh-CN|style=Feynman)（衡量系统对外[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)响应的敏感度）在低温相和高温相的[发散](@keyword=divergence|lang=zh-CN|style=Feynman)行为之间存在一个简单的整数比2 [@problem_id:2999165]。

如果我们施加一个外部[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman) $h$，它会给[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman)增加一项 $-hm$。这一项本身在 $m \to -m$ 变换下是不[对称](@keyword=symmetry|lang=zh-CN|style=Feynman)的，它“明确地”打破了[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，就像在房间里挂画一样。这称为**[显式对称性破缺](@keyword=explicit_symmetry_breaking|lang=zh-CN|style=Feynman)** [@problem_id:2999212]。此时，两个能量坑不再一样深，[磁场](@keyword=magnetic_fields|lang=zh-CN|style=Feynman)青睐的那个方向对应的坑会更深一些，系统会毫不犹豫地掉进那个坑里。

### [戈德斯通定理](@keyword=goldstone_s_theorem|lang=zh-CN|style=Feynman)：无代价的“摇摆”

从离散的 $m \to -m$ [对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)，我们更进一步，来思考[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)的情况，例如描述[超流体](@keyword=superfluid|lang=zh-CN|style=Feynman)或海森堡磁体的 $O(N)$ 模型 [@problem_id:2999167]。在这些模型中，[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)是一个矢量 $\vec{\phi}$，它可以指向 $N$ 维空间中的任何方向。[自由能](@keyword=free_energy|lang=zh-CN|style=Feynman) $F(\vec{\phi})$ 必须在所有 $O(N)$ 旋转下保持不变，这意味着它只能是[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)大小的函数，例如 $F(|\vec{\phi}|)$。

当 $T<T_c$ 时，系统同样会发生[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)。[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的大小被固定为某个非零值 $|\vec{\phi}|=\phi_0$，但它的*方向*是任意的。这意味着，所有满足 $|\vec{\phi}|=\phi_0$ 的状态都具有相同的最低能量。这些[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)的基态不再是两个孤立的点，而是形成了一个连续的“山谷”——在[三维空间](@keyword=3d_space|lang=zh-CN|style=Feynman)中，这个山谷就是一个[球面](@keyword=sphere|lang=zh-CN|style=Feynman) $S^2$ [@problem_id:2999145]。

想象一个弹珠在这个“墨西哥帽”形状的[势能面](@keyword=potential_energy_surfaces|lang=zh-CN|style=Feynman)上。要将弹珠从谷底沿径向推向山坡（改变[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的大小），需要克服势垒，这对应一个有能量代价（有质量）的激发模式。但是，如果让弹珠沿着圆形的谷底滑动（改变[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的方向），则完全不需要能量。这种沿着[对称性破缺](@keyword=broken_symmetry|lang=zh-CN|style=Feynman)后形成的[简并](@keyword=degeneracy|lang=zh-CN|style=Feynman)基态“山谷”的运动，对应的就是能量为零的激发模式。

这便是戈德斯通（Goldstone）定理的精髓：**当一个[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)被自发破缺时，系统必然会出现一种或多种能量为零（或称无质量、[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙）的激发模式，称为戈德斯-通模式（Goldstone modes）** [@problem_id:2999145] [@problem_id:2999167]。这些模式的数量等于被“破缺”的[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)生成元的数量。比如，从 $O(3)$ [对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)（空间旋转）破缺到一个选定方向的 $O(2)$ [对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)（绕该方向的旋转），破缺了两个[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性，于是就出现了两种[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)式 [@problem_id:2999212]。在磁体中，它们是[自旋波](@keyword=spin_waves|lang=zh-CN|style=Feynman)；在[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)中，它们是[声子](@keyword=phonon|lang=zh-CN|style=Feynman)。

### 空间与涨落：当指针开始摇摆

到目前为止，我们假设[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)在空间中是均匀的。但现实世界中，涨落无处不在。[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的值可以在空间中缓慢变化，$\phi(\mathbf{x})$。描述这种空间不均匀性的代价，最简单的形式就是[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)项 $\frac{c}{2}(\nabla\phi)^2$，它惩罚[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的剧烈变化 [$c>0$]。包含了[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)项的[朗道理论](@keyword=landau_theory|lang=zh-CN|style=Feynman)，被称为**[金兹堡-朗道理论](@keyword=ginzburg_landau_theory|lang=zh-CN|style=Feynman)**。

$$
F[\phi] = \int d^d x \left[ \frac{a}{2}\phi(\mathbf{x})^2 + \frac{b}{4}\phi(\mathbf{x})^4 + \frac{c}{2}|\nabla \phi(\mathbf{x})|^2 \right]
$$

[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)项的引入，带来了一个至关重要的物理量——**关联长度** $\xi$ [@problem_id:2999143]。在高温相，$a>0$，通过分析涨落可以发现，关联长度由 $\xi = \sqrt{c/a}$ 给出。它描述了空间中两点之间涨落的关联范围。当你拨动一处的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)，$\xi$ 就是这个扰[动能](@keyword=kinetic_energy|lang=zh-CN|style=Feynman)“感觉”到的距离。当温度 $T$ 趋近于 $T_c$ 时，$a \to 0$，导致 $\xi \to \infty$。关联长度的[发散](@keyword=divergence|lang=zh-CN|style=Feynman)是[临界现象](@keyword=critical_phenomena|lang=zh-CN|style=Feynman)的标志：在[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)点，一个局部的扰动可以影响到整个系统，整个系统变成一个紧密协作的整体。

### 涨落的复仇：低维世界的无序

[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)式的存在，虽然优美，却也为低维世界的有序性埋下了“祸根”。我们已经知道，激发一个[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)式的成本很低，尤其是那些[波长](@keyword=wavelength|lang=zh-CN|style=Feynman)极长（[动量](@keyword=momentum|lang=zh-CN|style=Feynman) $k \to 0$）的模式，成本趋近于零。在任何非零温度下，[热能](@keyword=thermal_energy|lang=zh-CN|style=Feynman)都会激发大量的这种“廉价”的涨落。

问题是，这些涨落的累积效应有多大？我们可以通过计算所有模式引起的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)方向的[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)（摇摆[幅度](@keyword=amplitude|lang=zh-CN|style=Feynman)） $\langle \boldsymbol{\pi}^2 \rangle$ 来衡量。一个粗略的计算表明，这个[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)正比于在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的积分 [@problem_id:2999150]：

$$
\langle \boldsymbol{\pi}^2 \rangle \propto \int d^d k \, \frac{T}{k^2}
$$

这里的 $d^d k$ 是 $d$ 维[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)的[体积元](@keyword=volume_element|lang=zh-CN|style=Feynman)，在低[动量](@keyword=momentum|lang=zh-CN|style=Feynman)区它正比于 $k^{d-1}dk$。因此，被积函数在 $k \to 0$（红外）处的行为像 $k^{d-3}$。
-   在 **$d=3$** 维空间，积分 $\int k^0 dk$ 是收敛的，涨落的总效应是有限的，长程有序得以存在。
-   在 **$d=2$** 维空间，积分 $\int k^{-1} dk \sim \ln(k)$，在 $k \to 0$ 时对数[发散](@keyword=divergence|lang=zh-CN|style=Feynman)。
-   在 **$d=1$** 维空间，积分 $\int k^{-2} dk \sim -1/k$，在 $k \to 0$ 时[线性](@keyword=linearity|lang=zh-CN|style=Feynman)[发散](@keyword=divergence|lang=zh-CN|style=Feynman)。

这个在低[动量](@keyword=momentum|lang=zh-CN|style=Feynman)区的[发散](@keyword=divergence|lang=zh-CN|style=Feynman)（称为**[红外发散](@keyword=infrared_divergence|lang=zh-CN|style=Feynman)**）意味着，在二维和一维空间中，长[波长](@keyword=wavelength|lang=zh-CN|style=Feynman)的、低能量的涨落是如此地泛滥，以至于它们的累积效应足以将任何试图建立的[宏观有序](@keyword=macroscopic_order|lang=zh-CN|style=Feynman)方向彻底“冲垮”。[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的指针在长距离上会完全迷失方向。这便是深刻的**默明-[瓦格纳定理](@keyword=wagner_s_theorem|lang=zh-CN|style=Feynman)（Mermin-Wagner Theorem）**：在低维（$d \le 2$）系统中，对于具有[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)的[短程相互作用](@keyword=short_range_interactions|lang=zh-CN|style=Feynman)，任何非零温度下都不可能存在自发的长程有序 [@problem_id:2999150]。

### [普适性](@keyword=universality|lang=zh-CN|style=Feynman)：[物理学](@keyword=physics|lang=zh-CN|style=Feynman)的“[趋同进化](@keyword=convergent_evolution|lang=zh-CN|style=Feynman)”

[朗道理论](@keyword=landau_theory|lang=zh-CN|style=Feynman)是一个美妙的唯象理论，但它本质上是一个**平均场理论**——它用一个平均的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)代替了所有微观[自由度](@keyword=degrees_of_freedom|lang=zh-CN|style=Feynman)的复杂相互作用，从而忽略了涨落的细节。正如我们刚刚看到的，涨落有时是决定性的。

然而，在[临界点](@keyword=tipping_points|lang=zh-CN|style=Feynman)附近，物理世界展现出了一个更为惊人的现象——**[普适性](@keyword=universality|lang=zh-CN|style=Feynman)（Universality）**。从水-气[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)到铁磁体的顺磁-铁[磁相变](@keyword=magnetic_phase_transitions|lang=zh-CN|style=Feynman)，尽管微观机制天差地别，它们在[临界点](@keyword=tipping_points|lang=zh-CN|style=Feynman)附近的行为（由一组称为“[临界指数](@keyword=critical_exponents|lang=zh-CN|style=Feynman)”的数字描述）却惊人地一致。

现代[物理学](@keyword=physics|lang=zh-CN|style=Feynman)通过**[重整化群](@keyword=renormalization_group|lang=zh-CN|style=Feynman)（Renormalization Group, RG）**的思想理解了这一现象 [@problem_id:2999140]。想象我们用一台“看不清”细节的相机来观察[临界点](@keyword=tipping_points|lang=zh-CN|style=Feynman)附近的系统。我们不断“放大”，忽略短距离的细节，只看长距离的宏观行为。在这个过程中，大部分微观细节（比如[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)的具体结构、相互作用力的精确形式）都变得“无关紧要”，被平均掉了。最终，唯一留存下来的、决定系统宏观行为的，只有最核心的要素：

1.  **空间的维度 $d$**
2.  **[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)**（例如，是标量、矢量还是[张量](@keyword=tensors|lang=zh-CN|style=Feynman)）

所有具有相同维度和[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)的系统，即使它们的“微观零件”完全不同，在[临界点](@keyword=tipping_points|lang=zh-CN|style=Feynman)附近也会表现出完全相同的行为，它们属于同一个**[普适类](@keyword=universality_classes|lang=zh-CN|style=Feynman)（universality class）** [@problem_id:2999148]。[朗道理论](@keyword=landau_theory|lang=zh-CN|style=Feynman)的成功与失败也可以在这个框架下被完美地理解。在高于某个“[上临界维度](@keyword=upper_critical_dimension|lang=zh-CN|style=Feynman)”（对我们讨论的模型是 $d_c=4$）的空间中，涨落是“无关紧要”的，朗道平均场理论的预测是精确的。而在我们生活的 $d<4$ 的世界里，涨落是“关键的”，它会修正[朗道理论](@keyword=landau_theory|lang=zh-CN|style=Feynman)的预测，产生新的、非平庸的[临界指数](@keyword=critical_exponents|lang=zh-CN|style=Feynman)，而这些[指数](@keyword=exponent|lang=zh-CN|style=Feynman)本身也是普适的 [@problem_id:2999140]。

从一个简单的[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)原则出发，我们构建了[朗道自由能](@keyword=landau_free_energy|lang=zh-CN|style=Feynman)，看到了[相变](@keyword=phase_transitions|lang=zh-CN|style=Feynman)的发生、[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)式的出现，也理解了涨落如何在低维世界摧毁秩序，并最终窥见了支配[临界现象](@keyword=critical_phenomena|lang=zh-CN|style=Feynman)的宏大[普适性](@keyword=universality|lang=zh-CN|style=Feynman)。这趟旅程，从一个简单的[对称性破缺](@keyword=broken_symmetry|lang=zh-CN|style=Feynman)思想开始，最终抵达了现代[凝聚态物理学](@keyword=condensed_matter_physics|lang=zh-CN|style=Feynman)的核心地带，淋漓尽致地展现了[物理学](@keyword=physics|lang=zh-CN|style=Feynman)将复杂现象还原为简单、优美基本原理的强大力量。

