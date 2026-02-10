## 应用与跨学科联系

我们花了一些时间来了解[流体旋转](@keyword=fluid_rotation|lang=zh-CN|style=Feynman)、涡度和环量的机制。你可能会认为这是一个相当专业的话题，是那些喜欢看水流入排水管的人的数学奇趣。但事实远非如此！事实证明，这种局部涡旋的想法是所有科学中最强大和最统一的概念之一。它是一把秘密钥匙，解开了从微观到宇宙尺度的现象的运作方式。涡旋之舞发生在我们周围，我们体内，以及浩瀚的宇宙中。那么，让我们踏上一段旅程，看看这个想法会引向何方。我们会发现，不起眼的涡旋是一条连接天气、飞行、量子力学甚至[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的线索。

### 行星与海洋的宏伟机器

让我们从大舞台开始：我们自己旋转的地球。为什么[天气预报](@keyword=weather_forecasting|lang=zh-CN|style=Feynman)不总是各处都“晴朗平静”？为什么海洋被雕刻成如墨西哥湾流这样巨大的旋转洋流？答案在很大程度上是[涡度](@keyword=vorticity|lang=zh-CN|style=Feynman)。地球本身就是一个巨大的旋转参考系。任何在其表面上移动的流体——无论是空气还是水——都在玩一场由[位涡守恒](@keyword=potential_vorticity_conservation|lang=zh-CN|style=Feynman)支配的游戏。

想象一下大气中的一个气柱。当这个气柱被垂直拉伸时，也许是由于流过一座山脉，它必须加速旋转以保持其[位涡守恒](@keyword=potential_vorticity_conservation|lang=zh-CN|style=Feynman)，从而形成一个旋转的涡旋 [@problem_id:1780100]。相反，如果气柱被挤压，比如在山的另一侧下降时，它将开始向相反方向旋转。用一个简单的旋转水箱进行的实验室实验完美地展示了这一原理：如果你拉伸一个水柱，它会产生“[气旋](@keyword=cyclones|lang=zh-CN|style=Feynman)式”旋转（像低压系统），如果你挤压它，它会产生“反[气旋](@keyword=cyclones|lang=zh-CN|style=Feynman)式”旋转（像高压系统） [@problem_id:1780146]。这不仅仅是一个可爱的类比；它是产生主导我们星球气候的巨大、旋转天气系统的基本机制。你在天气图上看到的山脊和低谷，本质上就是[涡度](@keyword=vorticity|lang=zh-CN|style=Feynman)图。

同样的原理也解释了为什么北半球的飓风是逆时针旋转的，以及为什么主要的[洋流](@keyword=ocean_currents|lang=zh-CN|style=Feynman)会那样运动。考虑一列在赤道完全静止的海水。在赤道，水感受到的背景“行星”旋转为零。现在，想象你慢慢地将这列水向北推。当它移动到更高的纬度时，其下方的地球背景旋转增加。为了保持其总[位涡守恒](@keyword=potential_vorticity_conservation|lang=zh-CN|style=Feynman)，水柱必须开始相对于地球向相反方向旋转 [@problem_id:596385]。这种由纬度变化产生的相对[涡度](@keyword=vorticity|lang=zh-CN|style=Feynman)是[地球物理流体动力学](@keyword=geophysical_fluid_dynamics|lang=zh-CN|style=Feynman)的基石，驱动着世界海洋巨大的环流状循环。大气和海洋复杂、不断变化的舞蹈，正是由这个简单的守恒定律编排的。流动总是在试图平衡自身的自旋与它所居住的行星的自旋。

运动、温度和旋转之间的这种相互作用可以导致极其复杂的行为。大气[对流](@keyword=convection|lang=zh-CN|style=Feynman)的简化模型，如著名的 Lorenz 系统，表明流体的旋转与加热产生的[浮力](@keyword=buoyant_force|lang=zh-CN|style=Feynman)之间的相互作用，可以从一套看似简单的规则中产生混沌、不可预测的天气模式 [@problem_id:1717894]。

### 飞行艺术与涡旋驾驭

几个世纪以来，[航空工程](@keyword=aeronautical_engineering|lang=zh-CN|style=Feynman)师一直将[流动分离](@keyword=flow_separation|lang=zh-CN|style=Feynman)——即气流从机翼表面脱离的点——视为必须不惜一切代价战胜的敌人，因为它通常会导致升力的灾难性损失。但是大自然，以及后来的聪明工程师，不仅学会了与分离共存，还学会了利用它的力量。

考虑一架拥有锐利[三角翼](@keyword=delta_wing|lang=zh-CN|style=Feynman)的现代战斗机，甚至是昆虫或蝙蝠的翅膀。在一个高[攻角](@keyword=angle_of_attack|lang=zh-CN|style=Feynman)下，空气根本无法跟随锐利的前缘而发生分离。但它并没有产生一个混乱的尾流，而是卷起成一个非常稳定、紧凑且快速旋转的涡旋，恰好位于机翼上方。为什么这是件好事？嗯，记住[伯努利原理](@keyword=bernoulli_s_principle|lang=zh-CN|style=Feynman)：流体速度高的地方，压力就低。在这个前缘涡的核心内部，空气以极高的速度旋转。这在机翼上表面产生了一个强烈的低压区，有效地以巨大的力量向上“吸”动机翼 [@problem_id:1738016]。这种“[涡升力](@keyword=vortex_lift|lang=zh-CN|style=Feynman)”使得飞机能够实现常规翼型不可能达到的机动性和飞行[攻角](@keyword=angle_of_attack|lang=zh-CN|style=Feynman)。这是通过掌握旋转物理学将“问题”转化为解决方案的一个美丽例子。

### 更深层的转折：[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)与量子领域

到目前为止，我们研究的都是像空气和水这样熟悉的流体。但是旋转的概念在[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)和量子力学的世界中找到了更奇特的表现形式。

想象一种“[铁磁流体](@keyword=ferrofluid|lang=zh-CN|style=Feynman)”，这是一种充满微小磁性纳米颗粒的液体。当你施加一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，这些颗粒会试图与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)对齐。现在，如果流体本身开始局部涡旋（即它有[涡度](@keyword=vorticity|lang=zh-CN|style=Feynman)），流体会试图拖动纳米颗粒一起运动，迫使它们旋转。然而，这些颗粒被[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)固定在位。流体的旋转与磁性对齐之间的这种微观拉锯战产生了一种额外的摩擦，或者说一种有效的“[旋转粘度](@keyword=rotational_viscosity|lang=zh-CN|style=Feynman)”，它可以通过[拨动开关](@keyword=toggle_switch|lang=zh-CN|style=Feynman)来开启和关闭 [@problem_id:464713]。这只是“[复杂流体](@keyword=complex_fluids|lang=zh-CN|style=Feynman)”的一个例子，其中材料的内部微观结构直接与宏观流动耦合，导致了迷人而有用的新特性。

当我们把某些流体，如[氦-4](@keyword=helium_4|lang=zh-CN|style=Feynman)，冷却到接近绝对零度时，故事变得更加离奇。它们进入一种被称为[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的奇异物质状态，这本质上是一个宏观的量子物体。它可以由一个单一的、巨大的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)来描述。当你试图旋转一桶这种东西时会发生什么？普通流体会平稳地旋转起来。但超流体不会。在量子世界里，事物是量子化的——它们以离散的包的形式出现。事实证明，超流体中的环量也是量子化的！[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)必须是单值的这一要求意味着，流体中的任何环量都必须是一个[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman)的整数倍：$\frac{2\pi\hbar}{m}$，其中 $m$ 是单个氦原子的质量 [@problem_id:1235024]。你可以有一个量[子环](@keyword=subring|lang=zh-CN|style=Feynman)量，或两个，或十个，但你*永远*不能有一个半。旋转不再是连续的。它以一系列细得不可思议的、离散的涡线形式存在。

这些[量子化涡旋](@keyword=quantized_vortices|lang=zh-CN|style=Feynman)不仅仅是理论上的奇趣。在[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)中，也就是[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)的电学表亲，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)只能以这些量子化涡线（通常称为磁通管）的形式穿透材料。这些涡旋的集合本身可以被视为一种奇怪的、二维的“涡旋流体”。这种缺陷流体有其自己奇特的[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)，表现出像“霍尔粘度”这样的现象，这是一种非耗散的、侧向的[粘性力](@keyword=viscous_forces|lang=zh-CN|style=Feynman)，源于作用在涡旋上的基本力 [@problem-id:259010]。甚至这些涡旋之一在其环境中移动时所经历的阻力，也可以用我们用于飞机机翼的相同[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)原​​理来建模，但应用于量子领域 [@problem_id:1219930]。

### 浴缸中的宇宙回响

也许[流体旋转](@keyword=fluid_rotation|lang=zh-CN|style=Feynman)最令人费解的应用来自一个名为“[模拟引力](@keyword=analogue_gravity|lang=zh-CN|style=Feynman)”的领域。控制波在运动流体中传播的定律与控制光和物质在[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)周围弯曲时空中传播的定律在数学上惊人地相似。

考虑一个简单的排水浴缸涡旋，其中[流体旋转](@keyword=fluid_rotation|lang=zh-CN|style=Feynman)着流入中央排水口。会存在一个特定的半径，在该半径处，向内流的水速恰好等于水中的声速。这是一个“声学视界”。就像任何东西，甚至光，都无法从[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)内部逃脱一样，任何东西，甚至[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)，都无法从这个声学视界内部逃脱。它在所有意图和目的上都是一个“哑洞”——一个声音的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)。

这是令人惊奇的部分。[Stephen Hawking](@keyword=stephen_hawking|lang=zh-CN|style=Feynman) 曾著名地预测，真正的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)并非完全是黑的；它们有温度并缓慢地辐射能量。事实证明，同样的数学推理预测，流体涡旋中的这些声学视界也应该有温度，并发出[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)或“[声子](@keyword=phonons|lang=zh-CN|style=Feynman)”的热谱 [@problem_id:359784]。一个简单的水涡旋可以模仿理论物理学中最深刻的现象之一。这告诉我们一些关于现实本质的极其深刻的东西：支配广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)和量子力学的数学结构并非孤立存在，而是在我们熟悉的[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)方程中找到了回响。

从窗外肆虐的龙卷风，到支撑飞机在空中的[升力](@keyword=lift_force|lang=zh-CN|style=Feynman)，到超流体的量子低语，再到水槽中[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的回响，[流体旋转](@keyword=fluid_rotation|lang=zh-CN|style=Feynman)的原理是一条金线。它是物理学统一性的一个壮观展示，显示了一个单一、优雅的思想如何能够阐明世界在所有尺度上的运作方式，揭示了自然法则内在的美丽和相互关联性。