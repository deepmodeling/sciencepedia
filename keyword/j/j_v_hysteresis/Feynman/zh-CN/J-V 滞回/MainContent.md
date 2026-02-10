## 引言
有些材料，就像人一样，会记住它们的过去。它们当前的状态不仅取决于现时条件，还取决于其历史。这种被称为滞回的现象是一项基本原理，它解释了从[硬盘](@keyword=hard_disk_drive|lang=zh-CN|style=Feynman)如何存储数据到下一代[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)的奇特行为等各种现象。尤其是在高效[钙钛矿太阳能电池](@keyword=perovskite_solar_cells|lang=zh-CN|style=Feynman)中出现的 J-V（[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)-[电压](@keyword=voltage|lang=zh-CN|style=Feynman)）滞回现象，一直是一个主要的难题，它使评估这些电池的真实性能和稳定性变得复杂。本文旨在通过揭开这些先进材料核心的[记忆效应](@keyword=memory_effect|lang=zh-CN|style=Feynman)之谜来解决这一难题。

我们将首先探索滞回现象背后的核心“原理与机制”，揭示[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)内离子缓慢而从容的“舞蹈”如何创造出一种[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)于我们实验测量的记忆。在此基础上，我们将踏上一段旅程，穿越“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”的广阔领域，揭示滞回现象的两面性。您将发现，它在[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中表现为不受欢迎的客人，在[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)中是可控的特性，在[数据存储](@keyword=data_storage|lang=zh-CN|style=Feynman)中是英雄法则，甚至在生命本身中也是一种关键的调节机制。

## 原理与机制

### 记忆问题

您是否曾试过拉伸一块口香糖或面团然后放手？它并不会立即恢复原状。如果您在拉伸和释放时追踪其长度，会发现它遵循两条不同的路径。这种材料似乎“记住”了它曾被拉伸过。这[种系](@keyword=germ_line|lang=zh-CN|style=Feynman)统状态取决于其历史的现象被称为**滞回**（hysteresis，源自希腊语“[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)”之意）。这不仅仅是[粘性](@keyword=viscosity|lang=zh-CN|style=Feynman)材料的一种奇特现象，而是自然界中一个深刻而普遍的原理。您可以在铁的[磁化](@keyword=magnetization|lang=zh-CN|style=Feynman)过程中看到它，这是计算机[硬盘](@keyword=hard_disk_drive|lang=zh-CN|style=Feynman)的基础；也可以在正在塑造我们未来技术的先进材料的行为中看到它。理解滞回就是理解过去可以对现在留下挥之不去的痕迹。

我们关于滞回的故事始于现代科学中最令人兴奋的材料之一：[钙钛矿](@keyword=perovskite|lang=zh-CN|style=Feynman)。这些[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)在制造高效、低成本的[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)方面展现了惊人的潜力。但它们带有一个奇特且常常令人沮丧的怪癖——它们的性能似乎取决于您的测量方式。如果您在向上扫描[电压](@keyword=voltage|lang=zh-CN|style=Feynman)时测量[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)，会得到一条曲线。而向下扫描[电压](@keyword=voltage|lang=zh-CN|style=Feynman)时，则会得到另一条。这种 J-V（[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)-[电压](@keyword=voltage|lang=zh-CN|style=Feynman)）滞回现象一直是一个主要的难题，使得确定这些器件的“真实”效率变得困难。解开这个谜题的关键不在于某种深奥的[量子效应](@keyword=quantum_effects|lang=zh-CN|style=Feynman)，而在于一些更具体的东西：[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)内部离子缓慢而从容的“舞蹈”。

### 游离离子的案例

想象一下[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中的[钙钛矿](@keyword=perovskite|lang=zh-CN|style=Feynman)[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)，它并非一个完全刚性且有序的支架，而更像一个有些柔性的结构，有点像一家有些客人可以自由在走廊里闲逛的旅馆。在许多[卤化物钙钛矿](@keyword=halide_perovskites|lang=zh-CN|style=Feynman)中，某些离子（如[碘](@keyword=iodine|lang=zh-CN|style=Feynman)离子）并未被紧紧锁在[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)位置上。它们是可移动的。当[钙钛矿太阳能电池](@keyword=perovskite_solar_cells|lang=zh-CN|style=Feynman)工作或被测量时，其内部存在[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)。那么，[带电粒子](@keyword=charged_particles|lang=zh-CN|style=Feynman)——我们这些游离的离子——在[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)中会做什么？它们会移动。

在[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)的影响下，这些正离子缓慢漂移并开始在[负极](@keyword=cathode|lang=zh-CN|style=Feynman)界面积累，在正极附近留下一个正[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)耗尽（等效于净负[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)）的区域。这种离子[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)的[分离](@keyword=fractionation|lang=zh-CN|style=Feynman)会产生一个与外加[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)方向相反的内建[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)。这种现象被称为**屏蔽**；可移动的离子有效地“屏蔽”或削弱了器件内部的[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman) [@problem_id:1334748]。

现在，关键点来了：这种离子移动不是瞬时的。与[电子](@keyword=electrons|lang=zh-CN|style=Feynman)相比，这些离子非常笨重，它们必须在[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)中艰难地移动。这是一项缓慢的工作。这个过程可以用一个**[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)** $\tau_{\text{ion}}$ 来表征，它代表了离子[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)重新适应新[电场](@keyword=electric_fields|lang=zh-CN|style=Feynman)所需要的典型时间 [@problem_id:23769]。正是这种迟缓，这种外加[电压](@keyword=voltage|lang=zh-CN|style=Feynman)变化与离子完全响应之间的时间延迟，赋予了器件对其近期历史的记忆 [@problem_id:1322622]。

### 伟大的竞赛：[扫描速率](@keyword=scan_rate|lang=zh-CN|style=Feynman) vs. [弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)

滞回现象源于两种竞争时间尺度之间的一场伟大竞赛：测量的**[扫描速率](@keyword=scan_rate|lang=zh-CN|style=Feynman)**（实验者改变外加[电压](@keyword=voltage|lang=zh-CN|style=Feynman)的[速度](@keyword=velocity|lang=zh-CN|style=Feynman)）和离子的内部**[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)**。

为了感受这一点，想象您是一艘巨大而沉重的货船的船长。船的方向是[钙钛矿](@keyword=perovskite|lang=zh-CN|style=Feynman)的内部状态（离子[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)），而船舵是您控制的外部[电压](@keyword=voltage|lang=zh-CN|style=Feynman)。

-   **慢速扫描**：如果您非常缓慢且逐渐地[转动](@keyword=rotational_motion|lang=zh-CN|style=Feynman)船舵，这艘巨大的船有足够的时间响应，其航向会忠实地跟随船舵的位置。在我们的[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中，这对应于非常慢的[电压](@keyword=voltage|lang=zh-CN|style=Feynman)扫描。离子有时间在每个[电压](@keyword=voltage|lang=zh-CN|style=Feynman)[步长](@keyword=step_size|lang=zh-CN|style=Feynman)下达到其[平衡位置](@keyword=equilibrium_position|lang=zh-CN|style=Feynman)，正向和反向 J-V 曲线会完全重合。没有滞回。

-   **快速扫描**：现在，如果您把船舵猛地向右打，然后立即猛地向左打，会怎么样？这艘船凭借其巨大的[惯性](@keyword=inertia|lang=zh-CN|style=Feynman)，完全无法跟上。它会划出一个宽阔而迟缓的弧线，向右转弯的路径与向左转回的路径完全不同。这正是在[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中进行快速[电压](@keyword=voltage|lang=zh-CN|style=Feynman)扫描时发生的情况。[扫描速率](@keyword=scan_rate|lang=zh-CN|style=Feynman)太快，以至于缓慢移动的离子无法跟上。外部[电压](@keyword=voltage|lang=zh-CN|style=Feynman)改变了，但来自离子的内部屏蔽场却[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)了，仍然反映着前一个[电压](@keyword=voltage|lang=zh-CN|style=Feynman)。外部场和内部状态之间的这种不匹配正是产生两条不同[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)-[电压](@keyword=voltage|lang=zh-CN|style=Feynman)曲线的原因 [@problem_id:2846456] [@problem_id:23819]。

我们甚至可以为此提供一些数字。基于原子[量子[力](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)学](@article_id:312082)的理论计算可以估算出单个卤化物离子在[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)中从一个位置跳到另一个位置的[能垒](@keyword=energy_barrier|lang=zh-CN|style=Feynman)。一个典型的[能垒](@keyword=energy_barrier|lang=zh-CN|style=Feynman)可能在 $0.5$ [电子伏特](@keyword=electron_volt|lang=zh-CN|style=Feynman)（$eV$）左右。这听起来极小，但利用[统计力学](@keyword=statistical_mechanics|lang=zh-CN|style=Feynman)的工具，我们可以将这个微观[能垒](@keyword=energy_barrier|lang=zh-CN|style=Feynman)转化为宏观的时间尺度。在室温下，一个 $0.5$ $eV$ 的[能垒](@keyword=energy_barrier|lang=zh-CN|style=Feynman)意味着一个离子可能需要**几秒钟**才能漂移穿过[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)的整个活性层 [@problem_id:2498997]。而研究实验室中一次典型的 J-V 测量需要多长时间？通常只有几秒钟。这场竞赛势均力敌！测量时间与离子[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)相当，这正是观察到显著滞回现象的绝佳条件。这种美妙的联系表明，一个原子尺度的性质如何直接决定了器件的宏观行为。

### 我们如何知道？科学家的工具箱

然而，一个好的科学家是一个专业的怀疑论者。我们如何能确定这些游离的离子是真正的元凶呢？毕竟，[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)中的其他过程也存在时间延迟。例如，[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)中的缺陷可以充当“[电子](@keyword=electrons|lang=zh-CN|style=Feynman)陷阱”，暂时捕获[电子](@keyword=electrons|lang=zh-CN|style=Feynman)然后再释放它们。这难道不会也引起滞回吗？

为了区分这些可能性，科学家们采用了一系列巧妙的实验技术，它们就像一个用于探究材料的工具箱 [@problem_id:2850491]。目标是找到离子运动独有的“指纹”。

-   **温度测试**：离子在[晶体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)中的移动是一个物理过程，很像试图把一颗弹珠推过粘稠的蜂蜜。如果你加热蜂蜜，它的[粘度](@keyword=viscosity|lang=zh-CN|style=Feynman)会降低，弹珠移动起来就更容易。类似地，如果我们加热[钙钛矿太阳能电池](@keyword=perovskite_solar_cells|lang=zh-CN|style=Feynman)，离子可以更快地迁移，它们的[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman) $\tau_{\text{ion}}$ 就会变短。$\tau_{\text{ion}}$ 随温度的这种变化遵循一个非常特定的数学形式（[阿伦尼乌斯定律](@keyword=arrhenius_law|lang=zh-CN|style=Feynman)），这是[热激](@keyword=heat_shock|lang=zh-CN|style=Feynman)活物理过程的一个明确标志。而[电子](@keyword=electrons|lang=zh-CN|style=Feynman)陷阱效应通常表现出对温度弱得多或不同的依赖性。通过在不同温度下测量滞回，我们可以判断其行为更像离子还是其他东西。

-   **频率探针**：另一个强大的工具是**[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)抗谱 (EIS)**。该技术不是采用缓慢、稳定的[电压](@keyword=voltage|lang=zh-CN|style=Feynman)扫描，而是向器件施加一个微小的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[电压](@keyword=voltage|lang=zh-CN|style=Feynman)，并测量其在极大频率范围内的[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)响应——从每秒不到一次[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)（低频）到每秒数百万次[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)（高频）。笨重、移动缓慢的离子只能跟上非常低频的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。而[电子](@keyword=electrons|lang=zh-CN|style=Feynman)由于极轻且灵活，可以响应高得多的频率。通过分析器件在不同频率下的响应，我们可以清晰地将离子的缓慢笨重的贡献与[电子](@keyword=electrons|lang=zh-CN|style=Feynman)的快速高频响应[分离](@keyword=fractionation|lang=zh-CN|style=Feynman)开来。

这些方法以及其他类似的方法，已经为在许多[钙钛矿](@keyword=perovskite|lang=zh-CN|style=Feynman)器件中，离子的缓慢迁移确实是神秘 J-V 滞回现象背后的主要角色提供了压倒性的证据。

### 一个普适的故事：从[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)到[超导体](@keyword=superconductors|lang=zh-CN|style=Feynman)

现在，让我们退后一步，欣赏这个想法的广度。滞回作为外部驱动与内部弛豫之间竞赛的故事，并不仅限于[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)。它是物理学中的一个普适主题，出现在最意想不到的地方。

让我们从阳光普照的光伏世界，走向超导和[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)的超冷领域。这些技术中的一个基本构建单元是**[约瑟夫森结](@keyword=josephson_junctions|lang=zh-CN|style=Feynman)**，它由一层极薄的绝缘势垒隔开的两个[超导体](@keyword=superconductors|lang=zh-CN|style=Feynman)组成。如果您测量它的[电流-电压特性](@keyword=i_v_characteristics|lang=zh-CN|style=Feynman)，您通常会发现——您猜对了——

