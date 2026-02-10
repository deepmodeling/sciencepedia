## 引言
我们的日常经验告诉我们，热量会缓慢地扩散和耗散。这个被称为扩散的过程是经典[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)的基石，但它描绘的图景并不完整。在量子世界的极端条件下，这种我们所熟知的行为可能被彻底颠覆。热，作为随机运动的本质，可以自我组织成一种有序的、集体的行进，以相干波的形式传播。这种看似矛盾的现象被称为“第二声”——一种温度自身的波。

本文旨在探讨经典热学理论的根本局限性，并探索那些允许波状热能传输的非凡物理学。它将揭示为何这种典型的无序形式能够实现波的有序运动。

首先，在“原理与机制”部分，我们将审视预测热波的理论框架，并探索观测到[热波](@keyword=thermal_waves|lang=zh-CN|style=Feynman)的两个主要物理系统：[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)中的量子芭蕾，以及晶体固体中如同流体般运动的原子[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)气体。随后，在“应用与跨学科联系”部分，我们将深入探讨[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)的深远影响，从探测奇特的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)，到管理下一代电子设备中的热量，甚至理解遥远[中子星](@keyword=neutron_stars|lang=zh-CN|style=Feynman)的物理学。

## 原理与机制

你了解热是什么。你从太阳、火炉、剧烈运动中感受到它。你对它的运动方式有着深刻的直觉。如果你将一根烧热的拨火棍放入一桶冷水中，热量并不会瞬间温暖整桶水。它会[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)开来。它会*[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)*。一个热的区域会逐渐将其热量[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)到周围较冷的区域，并在此过程中被稀释。我们有一个优美的数学描述来形容这个缓慢、蔓延的过程，即**傅里叶定律**，它对我们日常经验中的几乎所有事物都适用得非常好。

但如果我告诉你，这幅图景并不完整呢？如果我说，在某些非凡的条件下，热量可以停止“爬行”，开始“行进”呢？它能够停止扩散，开始像空气中传播的声音一样，以一种纯净、相干的波的形式传播。这种奇异的现象被称为 **[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman) (second sound)**，这个名字暗示了它的奇特性。它不是普通意义上的声音；它是一种温度自身的波。这个想法本身似乎就充满矛盾。热是无数原子随机碰撞的运动。这种典型的无序形式怎么可能自我组织成一种有序的、集体的波的运动呢？这正是我们即将解开的谜团。正如我们将看到的，答案将我们从抽象的数学修正引向奇异的量子世界——超流体，以及晶体中[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的隐藏的类流体行为。

### 修正傅里叶定律：热波的普适理论

我们首先来看一下我们熟悉并喜爱的理论——[傅里叶定律](@keyword=fourier_s_law|lang=zh-CN|style=Feynman)，$\mathbf{q} = -k \nabla T$。它指出热通量 $\mathbf{q}$ 与温度梯度 $\nabla T$ 的负值成正比。施加一个梯度，你就会立即得到一个通量。但“立即”这个词应该让物理学家感到不安。它意味着，如果你在宇宙的一个角落点燃一个打火机，宇宙遥远的另一端的温度计应该*在那一瞬间*就记录到变化。这违反了任何物体的传播速度都不能超过光速的基本原理。

当然，对于大多数实际应用来说，这个“无限速度”问题只是学术上的。其影响微乎其微，我们可以忽略不计。但如果我们处理的是极快的过程，比如说，用仅持续飞秒（$10^{-15}$秒）的[激光脉冲](@keyword=laser_pulses|lang=zh-CN|style=Feynman)轰击一种材料呢？在这些极端情况下，瞬时响应的假设会彻底失效[@problem_id:2489782]。我们需要一个更好的定律。

修正这个问题最简单的方法是给热量一点迟滞性，一种**[热惯性](@keyword=thermal_inertia|lang=zh-CN|style=Feynman)**。想象一下，热通量就像一辆沉重的推车。当你开始推它（通过施加[温度梯度](@keyword=temperature_gradient|lang=zh-CN|style=Feynman)），它不会立即达到全速。它需要一点时间才能启动。这个“时间”被称为[热弛豫时间](@keyword=thermal_relaxation_time|lang=zh-CN|style=Feynman)，$\tau$。这个思想的数学体现就是**[卡塔内奥-韦尔诺特方程](@keyword=cattaneo_vernotte_equation|lang=zh-CN|style=Feynman) (Cattaneo-Vernotte equation)**：

$$
\mathbf{q} + \tau \frac{\partial \mathbf{q}}{\partial t} = -k \nabla T
$$

看看这个方程在说什么。热通量 $\mathbf{q}$ 仍然*倾向于*等于 $-k\nabla T$，正如[傅里叶定律](@keyword=fourier_s_law|lang=zh-CN|style=Feynman)所规定的那样。但是，如果通量变化很快（如果 $\partial\mathbf{q}/\partial t$ 很大），就会有一个阻力项 $\tau \partial\mathbf{q}/\partial t$ 拖住它。通量无法跟上[温度梯度](@keyword=temperature_gradient|lang=zh-CN|style=Feynman)的瞬时变化 [@problem_id:2776852]。

当我们将这个对热通量更仔细的描述与基本的[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)定律结合起来时，奇妙的事情发生了。最终得到的温度方程不再是傅里叶定律的[简单扩散](@keyword=simple_diffusion|lang=zh-CN|style=Feynman)方程。它是一个更复杂且内涵更丰富的方程，称为**[电报方程](@keyword=telegrapher_s_equations|lang=zh-CN|style=Feynman) (Telegrapher's Equation)** [@problem_id:526133]。对于一维系统，它看起来是这样的：

$$
\tau \frac{\partial^2 T}{\partial t^2} + \frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}
$$

这里，$\alpha = k/(\rho c_v)$ 是热扩散率。注意这个方程有两部分。$\partial T/\partial t$ 这一项是旧的[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)项。但新的项 $\tau \partial^2 T/\partial t^2$ 是一个波动项！它与你在振动弦或光波的方程中找到的项是同一种类型。这个方程告诉我们，热扰动既有波的成分，也有[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)的成分。它像波一样向外传播，但同时也像一缕烟一样衰减和[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)。这种“[热波](@keyword=thermal_waves|lang=zh-CN|style=Feynman)”的速度是有限的，由 $c_s = \sqrt{\alpha/\tau} = \sqrt{k/(\rho c_v \tau)}$ 给出 [@problem_id:2776852] [@problem_id:526133]。我们已经解决了无限速度的难题！

然而，这并不意味着你每天都能看到热波。这个方程也告诉我们存在一种竞争。对于长距离上的缓慢、温和的变化，[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)项占主导地位，我们又回到了熟悉的傅里叶世界。为了让波真正“胜出”并传播，扰动必须非常迅速且波长很短。事实上，存在一个临界波长 $\lambda_c = 4 \pi \sqrt{\alpha \tau}$。波长短于 $\lambda_c$ 的扰动表现得像波，而波长较长的扰动则是纯粹的扩散 [@problem_id:2151643]。这个理论框架很强大，但它引出了一个问题：这种[热惯性](@keyword=thermal_inertia|lang=zh-CN|style=Feynman)，这个 $\tau$，是真实存在的吗？是否存在任何真实系统，其中这种类波行为不仅仅是理论上的奇想，而是一种主导的、可观测的现象？答案是肯定的。

### 首次发现：[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)中的量子芭蕾

第二声的第一个也是最引人注目的证实来自宇宙中最奇特的物质之一：冷却到约 $2.17$ [开尔文](@keyword=kelvin|lang=zh-CN|style=Feynman)以下的液氦。在这个温度下，它转变为一种[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，一种具有惊人特性的[量子液体](@keyword=quantum_liquids|lang=zh-CN|style=Feynman)。为了理解它，物理学家们发展了**[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman) (two-fluid model)**。该模型要求你想象[超流氦](@keyword=superfluid_helium|lang=zh-CN|style=Feynman)是两种可相互[渗透](@keyword=permeation|lang=zh-CN|style=Feynman)的流体的紧密混合物 [@problem_id:1994370]：
1.  一种**超流体组分**，其黏度恰好为零，并且至关重要的是，它携带零熵。它是“量子力学纯净”的，不携带任何热量。
2.  一种**正常流体组分**，其行为像普通的黏性流体。它携带系统的*全部*熵和热量。

有了这个奇异的图景，当你试图制造[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)时会发生什么呢？嗯，这两种流体有两种运动方式。

第一种方式是，超流体和[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)组分*同相*来回晃动。它们一起运动。这会产生更高和更低密度的区域，就像普通的[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)一样。这被称为**[第一声](@keyword=first_sound|lang=zh-CN|style=Feynman)**，它实际上只是通过这种奇特液体传播的普通声音。

但还有另一种更奇怪的可能性。如果两种流体*异相*运动呢？想象一下，超流体组分向右冲，而[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)组分向左冲，然后它们反向运动。在这场量子芭蕾中，液体的总密度在任何地方都保持恒定，因为无论[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)涌入何处，正常流体都会涌出以填补其空间。没有密度变化，就没有压力变化。压力麦克风将听不到任何声音！但请记住，[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)携带所有热量。因此，这种[逆流](@keyword=counterflow|lang=zh-CN|style=Feynman)，即[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)与[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的晃动，实际上是一种[热波](@keyword=thermal_waves|lang=zh-CN|style=Feynman)。一个暂时富含正常流体的区域变热，一个贫乏[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)的区域变冷。这就是第二声：一种温度的波 [@problem_id:1994370]。

这种波的速度 $u_2$ 可以从[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)方程中推导出来。结果是物理学中的一颗瑰宝：

$$
u_2^2 = \frac{\rho_s s^2 T}{\rho_n c_p}
$$

不要被这些符号吓到。这个公式讲述了一个美丽的故事 [@problem_id:464736]。速度取决于超流体密度 ($\rho_s$) 与正常流体密度 ($\rho_n$) 的比值。它还取决于[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)性质：温度 $T$、熵 $s$ 和比热 $c_p$。它具体地表明了这种宏观波动现象如何深深植根于流体的量子力学状态。

### 不可见的流体：固体中的[声子[流体动力](@keyword=phonon_hydrodynamics|lang=zh-CN|style=Feynman)学](@article_id:319275)

很长一段时间里，[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)被认为是[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的专属派对。但物理学中最深刻的见解往往来自于在看似迥异的现象中发现统一性。事实证明，一种非常相似的[热波](@keyword=thermal_waves|lang=zh-CN|style=Feynman)可以在某些固体晶体中传播，其原因与[双流体模型](@keyword=two_fluid_model|lang=zh-CN|style=Feynman)有着奇妙的类比。

非金属晶体内部的“流体”是**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**的气体——[声子](@keyword=phonons|lang=zh-CN|style=Feynman)是振动能的量子化包，即[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)。晶体中的热量不过是这种[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体的能量。正如气体中的粒子可以碰撞一样，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)也可以。这些碰撞的性质是解开一切的关键。

[声子](@keyword=phonons|lang=zh-CN|style=Feynman)碰撞有两种类型 [@problem_id:2849431]：
1.  **[正常过程](@keyword=normal_process|lang=zh-CN|style=Feynman) (N-processes)**：两个或多个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)碰撞并产生新的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)，但[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的总动量是守恒的。可以把它想象成在无摩擦的台球桌上碰撞的台球。这些碰撞不会[对流](@keyword=convection|lang=zh-CN|style=Feynman)动产生任何阻力。相反，通过不断地重新分配动量，它们使得[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体能够作为一个集体行动，建立局部平衡，并赋予气体“黏性”。它们是[声子](@keyword=phonons|lang=zh-CN|style=Feynman)流体的“社会粘合剂”。
2.  **阻抗过程 (R-processes)**：在这些碰撞中，总的[声子动量](@keyword=phonon_momentum|lang=zh-CN|style=Feynman)*不*守恒。其中最重要的是**[倒逆散射](@keyword=umklapp_scattering|lang=zh-CN|style=Feynman) (Umklapp scattering, U-processes)**，动量被倾倒到整个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中。这是完美晶体中热阻的来源。其他的 R 过程包括在杂质或晶体缺陷上的散射。这些碰撞就像摩擦力；它们会抑制[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体的任何[集体流动](@keyword=bulk_flow|lang=zh-CN|style=Feynman)。

现在类比变得清晰了。保持[动量守恒](@keyword=conservation_of_momentum|lang=zh-CN|style=Feynman)的[正常过程](@keyword=normal_process|lang=zh-CN|style=Feynman)，就像无摩擦的[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)。它们允许[集体流动](@keyword=bulk_flow|lang=zh-CN|style=Feynman)。破坏动量的阻抗过程，就像产生阻力并耗散热量的黏性[正常流体](@keyword=normal_fluid|lang=zh-CN|style=Feynman)。

为了使[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体展现出[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)行为并支持像第二声这样的波，必须满足一个特殊条件：[声子](@keyword=phonons|lang=zh-CN|style=Feynman)必须通过[正常过程](@keyword=normal_process|lang=zh-CN|style=Feynman)频繁地相互碰撞以建立集体的、类流体的流动，并且这种流动必须在被阻抗过程消除之前持续足够长的时间以进行传播。这转化为一个明确的[散射时间](@keyword=scattering_time|lang=zh-CN|style=Feynman)层级：正常碰撞之间的时间 ($\tau_N$) 必须远短于阻抗碰撞之间的时间 ($\tau_R$)。

$$
\tau_N \ll \tau_R
$$

当这个条件满足时，[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体的行为就像流体，热量以波的形式传播。这就是**[声子流体动力学](@keyword=phonon_hydrodynamics|lang=zh-CN|style=Feynman)** [@problem_id:2514900]。在这些条件下，从[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)出发，使用[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的[玻尔兹曼输运方程](@keyword=boltzmann_transport_equation|lang=zh-CN|style=Feynman)在一个简单晶体中进行推导，得到了一个惊人地简单而优雅的第二声速度结果 [@problem_id:2803315]：

$$
c_{II} = \frac{v_s}{\sqrt{3}}
$$

这里，$v_s$ 是晶体中声速（[第一声](@keyword=first_sound|lang=zh-CN|style=Feynman)）的平均值。这太不可思议了！这种奇特[热波](@keyword=thermal_waves|lang=zh-CN|style=Feynman)的速度不是某个任意的参数；它与普通声速成正比。这个优美的公式揭示了晶体的弹性特性与其在这个特殊区域的热输运行为之间深刻的统一性。

### “[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)窗口”：制造波状热的秘诀

那么，我们如何制造一个满足关键条件 $\tau_N \ll \tau_R$ 的晶体呢？我们需要找到“[第二声](@keyword=second_sound|lang=zh-CN|style=Feynman)窗口”——一套关于温度、纯度甚至样品尺寸的特殊条件 [@problem_id:2514900]。

-   **温度**：这是最重要的调节旋钮。在非常高的温度下，[倒逆散射](@keyword=umklapp_scattering|lang=zh-CN|style=Feynman)非常强，所以 $\tau_R$ 很短，热传输是纯粹的[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)。在非常、非常低的温度下，即使是正常散射也变得稀少，所以[声子](@keyword=phonons|lang=zh-CN|style=Feynman)只是从晶体的一端飞到另一端而不相互作用（这是“弹道”输运区域）。最佳点是在一个**中等偏低的温度**（通常是材料[德拜温度](@keyword=debye_temperature|lang=zh-CN|style=Feynman)的百分之几）。在这里，[倒逆过程](@keyword=umklapp_process|lang=zh-CN|style=Feynman)被“冻结”，使得 $\tau_R$ 呈指数级增长，而[正常过程](@keyword=normal_process|lang=zh-CN|style=Feynman)仍然足够频繁，使得 $\tau_N$ 很短。

-   **纯度**：晶体中的任何杂质或同位素都会充当散射中心，这些中心会促成弛豫动量的阻抗过程。为了最大化 $\tau_R$，需要**超纯、同位素纯净的晶体**。

-   **几何形状**：你还必须考虑样品尺寸 $L$。为了使[声子气](@keyword=phonon_gas|lang=zh-CN|style=Feynman)体表现得像一个体流体，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)在撞到边界墙壁之前必须发生许多次正常碰撞。这意味着正常散射的[平均自由程](@keyword=mean_free_path|lang=zh-CN|style=Feynman) $l_N = v_s \tau_N$ 必须远小于样品尺寸（$l_N \ll L$）。与此同时，我们需要体内的阻抗散射在样品内部是罕见的，这意味着 $L$ 应该远小于阻抗[平均自由程](@keyword=mean_free_path|lang=zh-CN|style=Feynman) $l_R = v_s \tau_R$。这就给了我们著名的[声子流体动力学](@keyword=phonon_hydrodynamics|lang=zh-CN|style=Feynman) Gurzhi 条件 [@problem_id:2849431]：

    $$
    l_N \ll L \ll l_R
    $$

当所有这些条件都吻合时，一个窗口就打开了，在一个近乎完美的晶体的寒冷纯净中，热量在短暂的瞬间发生了转变。它自我组织，它[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)行进，它成为一种波。

当然，这种波并非完美。它会衰减。正是那些必须被抑制以允许波存在的[倒逆过程](@keyword=umklapp_process|lang=zh-CN|style=Feynman)，仍然提供少量阻尼。而且，奇妙的是，创造[声子](@keyword=phonons|lang=zh-CN|style=Feynman)“流体”的[正常过程](@keyword=normal_process|lang=zh-CN|style=Feynman)也赋予了它黏性，这本身也有助于衰减波，尤其是在高频时 [@problem_id:34310]。物理学的美妙之处很少没有其精微的复杂性。

从经典定律的一个缺陷，到[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)中的量子芭蕾，再到固体中不可见的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)流体，第二声的故事证明了支配我们世界的隐藏的、统一的结构。它向我们展示，即使是像热这样看似简单和无序的东西，在正确的规则下，也能参与自然界最优雅的运动形式之一：波。