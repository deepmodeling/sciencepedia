## 引言
我们如何研究一个微小到无法看见的世界？原子、分子以及它们构成的材料的秘密，是用一种能量和[量子跃迁](@keyword=quantum_transitions|lang=zh-CN|style=Feynman)的语言书写的，这种语言肉眼无法看见。光子[光谱学](@keyword=optical_spectroscopy|lang=zh-CN|style=Feynman)为翻译这种语言提供了钥匙。作为精确的探针，单个光包——光子——以可预测的方式与物质相互作用，带走关于其结构、组成和动力学的宝贵信息。本文旨在引导读者理解和利用这套强大的技术。它回答了一个基本问题：我们如何系统地揭示物质在量子层面的性质。在接下来的章节中，我们将首先探讨[光与物质相互作用](@keyword=light_matter_interaction|lang=zh-CN|style=Feynman)的基本原理，深入研究分子的[量子化能级](@keyword=quantized_energy_levels|lang=zh-CN|style=Feynman)阶梯以及光子可能遇到的各种命运。然后，我们将遍览其应用的广阔前景，看看这些原理如何在科学和工程领域被付诸实践，以解决现实世界的问题。

## 原理与机理

想象你是一名侦探，而你的嫌疑人是原子和分子，它们小得不可思议且难以捉摸。你看不见它们，也摸不着它们，那么你如何揭开它们的秘密呢？你的主要工具是光。你发射一个光子——光的单个量子——然后观察发生了什么。分子是吞噬了它？还是把它弹开了？或是把它撞得粉碎？每一个结果都是一条线索。光子[光谱学](@keyword=optical_spectroscopy|lang=zh-CN|style=Feynman)就是解读这些线索的科学。其核心在于，它讲述了能量以光子的形式如何与[物质的量](@keyword=molar_quantity|lang=zh-CN|style=Feynman)子化世界相互作用的故事。

### 一个由能级阶梯构成的宇宙

量子力学的第一个伟大原理，也是其基石之一，是原子或分子内的能量不是连续的。它是量子化的。一个原子不能拥有*任意*数量的能量；它必须存在于特定的、分立的能级上。我们可以将这些能级想象成能量阶梯上的梯级。为了改变能量，分子必须从一个梯级[量子跃迁](@keyword=quantum_transitions|lang=zh-CN|style=Feynman)到另一个梯级。它不能在两者之间悬停。

但情况比单个阶梯更复杂。分子是一个复杂的实体，它有多种不同的方式来储存能量。

首先，是**电子能级**，它对应于电子在[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)中不同的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)方式。这就像一栋建筑的不同楼层。楼层之间的能量跃迁是巨大的。要让一个电子跳到更高的楼层，你需要一个能量非常高的光子，通常来自[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)中的紫外或可见光（UV-Vis）区域 [@problem_id:2465201]。

在每一个电子“楼层”上，都有更精细的结构：一个由**振动能级**组成的阶梯。这些对应于将分子维系在一起的化学键的伸缩和弯曲。这个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)阶梯的梯级比电子楼层要密集得多。激发一次[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)所需的能量较少——通常，一个来自红外区域的光子就足够了。

最后，在每一个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)“台阶”上，还有更精细的层次：一组**转动能级**，对应于分子在空间中的翻滚。这些是所有能级跃迁中最小的，它们可以被来自微波区域的低能光子激发。

这些能量尺度究竟有多大差异？对于一个典型的双原子分子，如[一氧化碳](@keyword=carbon_monoxide_(co)|lang=zh-CN|style=Feynman)（$\text{CO}$），使其发生第一次[振动跃迁](@keyword=vibrational_transitions|lang=zh-CN|style=Feynman)（从 $v=0$ 到 $v=1$）所需的能量，比第一次转动跃迁（从 $J=0$ 到 $J=1$）所需的能量大500倍以上 [@problem_id:1990770]。这种巨大的[尺度分离](@keyword=separation_of_scales|lang=zh-CN|style=Feynman)是大自然给予我们的奇妙礼物。它使我们能够几乎独立地研究这些不同的运动——电子、[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和转动——只需选择正确种类的光即可。

### 光子的三种命运

当一个具有恰当能量的光子遇到一个分子时，接下来会发生什么？这种相互作用大致可分为三种基本过程：吸收、发射和散射。每一种都构成了一个强大的[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)技术家族的基础。

#### 吸收：向上的跃迁

最直观的相互作用是**吸收**。分子完全吸收光子，其能量被用来将分子提升到其某个能量阶梯上更高的梯级。光子消失，分子处于[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。

但这里有一个关键点：并非所有跃迁都是可能的，即使光子具有完全正确的能量。一个跃迁要成为“允许的”，分子必须有办法与光波的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)相互作用。这便引出了**[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)**，它们充当了跃迁的量子力学“通行证”。

一个分子要拥有纯[转动光谱](@keyword=rotational_spectra|lang=zh-CN|style=Feynman)——即吸收一个微波光子并开始更快地翻滚——它必须具有**[永久电偶极矩](@keyword=permanent_electric_dipole_moment|lang=zh-CN|style=Feynman)** [@problem_id:2020862]。可以把偶极矩想象成一个把手。光的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)需要抓住这个把手来施加扭转。像氮气（$\text{N}_2$）或二氧化碳（$\text{CO}_2$）这样的对称分子没有[永久偶极矩](@keyword=permanent_dipole_moment|lang=zh-CN|style=Feynman)，所以它们是“微波非活性的”——它们不吸收微波。相比之下，像水（$\text{H}_2\text{O}$）或[一氧化碳](@keyword=carbon_monoxide_(co)|lang=zh-CN|style=Feynman)（$\text{CO}$）这样的非对称分子，拥有[永久偶极矩](@keyword=permanent_dipole_moment|lang=zh-CN|style=Feynman)，并具有丰富而美丽的[转动光谱](@keyword=rotational_spectra|lang=zh-CN|style=Feynman)。

对于[振动跃迁](@keyword=vibrational_transitions|lang=zh-CN|style=Feynman)要成为“红外活性的”，规则略有不同。[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)本身必须引起[分子偶极矩](@keyword=molecular_dipole_moment|lang=zh-CN|style=Feynman)的*变化*。在 $\text{CO}_2$（O=C=O）中，当两个氧原子同时远离碳原子时发生的[对称伸缩](@keyword=symmetric_stretch|lang=zh-CN|style=Feynman)[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，不会改变偶极矩（它保持为零），所以这个模式是红外非活性的。但一个非[对称伸缩](@keyword=symmetric_stretch|lang=zh-CN|style=Feynman)[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，即一个键缩短而另一个键伸长，会产生一个临时的、[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的偶极矩，使其在红外[光谱仪](@keyword=spectrometer|lang=zh-CN|style=Feynman)中清晰可见。

当我们使用高能的紫外-可见光子引发电子跃迁时，事情变得更加有趣。电子跃迁是如此突然，以至于比电子重得多的分子核在跃迁期间实际上是冻结不动的。这就是**Franck-Condon 原理**。分子到达[激发电子态](@keyword=excited_electronic_states|lang=zh-CN|style=Feynman)时，其[键长](@keyword=bond_length|lang=zh-CN|style=Feynman)与[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)时相同。然而，[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的*理想*或平衡键长可能不同。如果[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)偏好更长的键，分子会发现自己处于一个被压缩的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)状态。因此，最强烈的跃迁不一定是指向新电子态的最低[振动能级](@keyword=vibrational_energy_levels|lang=zh-CN|style=Feynman)（$v'=0$），而是指向一个更高的[振动能级](@keyword=vibrational_energy_levels|lang=zh-CN|style=Feynman)（例如 $v'=4$），其波函数与[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)波函数的重叠最大 [@problem_id:2031445]。由此产生的[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)，即一系列[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)峰，是这种量子力学重叠的直接映射，告诉我们分子在激发后其几何形状如何变化。

#### 发射：优雅的坠落

有升必有降。处于[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的分子可以通过发射光子来弛豫。最重要的发射过程之一是**荧光**。通常，分子吸收一个紫外光子，跃迁到激发电子和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)状态。它迅速以热量（非辐射地）形式释放一些振动能，沿[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)阶梯滑到[激发电子态](@keyword=excited_electronic_states|lang=zh-CN|style=Feynman)的最低梯级（$v'=0$）。从那里，它完成回到基电子态的大跳跃，并在此过程中发射一个光子。

因为在[振动弛豫](@keyword=vibrational_relaxation|lang=zh-CN|style=Feynman)过程中部分能量以热量形式损失掉了，所以发射的[光子能量](@keyword=photon_energy|lang=zh-CN|style=Feynman)比吸收的光子能量低（因此波长更长）。这种能量差异被称为**[斯托克斯位移](@keyword=stokes_shift|lang=zh-CN|style=Feynman)** (Stokes shift)。

[荧光光谱学](@keyword=fluorescence_spectroscopy|lang=zh-CN|style=Feynman)以其非凡的灵敏度而闻名。原因非常深刻，与测量的本质有关 [@problem_id:2149594]。[吸收光谱学](@keyword=absorption_spectroscopy|lang=zh-CN|style=Feynman)就像试图探测一束非常明亮的光的微弱变暗；你在测量两个大信号（$I_0$ 和 $I_t$）之间的小差异。这在技术上是困难的。而荧光通常在与激发光束成90度角的位置进行测量。你是在漆黑的背景下测量微弱的光辉。在一个零背景上检测小信号远比在一个大信号中检测小变化要容易。这就像在一个灯火通明的体育场里注意到一根蜡烛熄灭了，和在一片漆黑的森林里发现一只萤火虫的区别。

#### 散射：光子的反弹

有时，光子不是被吸收，而只是从分子上“散射”开。大多数情况下，这是**瑞利散射** (Rayleigh scattering)，一个弹性过程，光子离开时能量与来时相同。这就是天空是蓝色的原因。

但大约百万分之一的情况下，会发生一些更有趣的事情：**拉曼散射** (Raman scattering)。这是一个*非弹性*过程，光子和分子可以交换一个振动能量量子。在短暂的相互作用中，光子可以诱导分子振动，并在此过程中放弃自己的一些能量。散射出的光子能量减少；这被称为**[斯托克斯散射](@keyword=stokes_scattering|lang=zh-CN|style=Feynman)** (Stokes scattering)。或者，如果分子已经在[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，它可以将其[振动能](@keyword=vibrational_energy|lang=zh-CN|style=Feynman)转移给光子，光子随后以*更高*的能量出现。这被称为**[反斯托克斯散射](@keyword=anti_stokes_scattering|lang=zh-CN|style=Feynman)** (anti-Stokes scattering) [@problem_id:2016393] [@problem_id:1467121]。

[拉曼散射的选择定则](@keyword=selection_rules_for_raman_scattering|lang=zh-CN|style=Feynman)为我们提供了一个窥见光与物质相互作用双重性质的美妙视角。[拉曼散射](@keyword=raman_scattering|lang=zh-CN|style=Feynman)不关心偶极矩。它关心**极化率**——即分子的电子云被[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)扭曲的难易程度 [@problem_id:2006898]。一个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)要想成为拉曼活性的，它必须引起[分子极化率](@keyword=molecular_polarizability|lang=zh-CN|style=Feynman)的变化。

这与红外[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)形成了绝佳的互补。想想我们的老朋友 $\text{N}_2$。作为[同核双原子分子](@keyword=homonuclear_diatomics|lang=zh-CN|style=Feynman)，它的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)不会引起偶极矩的变化，使其在红外[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)中完全不可见。但当键伸长时，电子云也会伸长，从而改变其[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman)。这使得 $\text{N}_2$（以及 $\text{O}_2$，我们空气的主要成分）的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)非常适合用拉曼[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)研究 [@problem_id:1467121]。红外和拉曼[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)共同为我们提供了[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)生命更完整的图景。

### 终极一击：光[电子能谱](@keyword=electron_energy_spectrum|lang=zh-CN|style=Feynman)

如果我们使用一个能量如此之高的光子，它不仅能把一个电子推到更高的能级，而是把它完全从分子中踢出去，会怎么样？这就是光电效应，也是**光[电子能谱](@keyword=electron_energy_spectrum|lang=zh-CN|style=Feynman) (PES)** 的基础。

这里的物理原理简单得令人耳目一新。它是一个[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)的表述 [@problem_id:2950566]。入射光子 ($h\nu$) 的能量花在两件事上：解放电子的代价（其**结合能**，$IE$），以及剩下的部分，成为电子的动能 ($KE$)。

$$h\nu = IE + KE$$

在 PES 实验中，我们控制光子的能量 ($h\nu$)，并建造一个精密的探测器来测量[逸出](@keyword=effusion|lang=zh-CN|style=Feynman)电子的动能 ($KE$)。有了这两个已知量，我们就可以直接计算出分子中每个电子的结合能。PES [光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)不是对能级间跃迁的间接观察；它是能级本身的直接映射图。这是一种极其强大的技术，证实了这些结合能是原子的内在属性，与用于探测它们的[光子能量](@keyword=photon_energy|lang=zh-CN|style=Feynman)无关 [@problem_id:2950566]。

就像一把多功能工具，PES 有不同的类型。通过使用能量相对较低的紫外光子（**UPS**），我们可以轻柔地剥离最外层、束缚最弱的**价电子**。这些是参与[化学键合](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)并决定材料电子性质（如导电性）的电子。因此，UPS 是研究[有机半导体](@keyword=organic_semiconductors|lang=zh-CN|style=Feynman)前沿[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的完美工具，例如 [@problem_id:2045543]。

如果我们换用能量更强的 X 射线光子（**XPS**），我们就可以轰出深层、束缚紧密的**芯层电子**。这些芯层电子的[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)高度特征性地反映了它们所属的元素。来自碳 1s [轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的电子的[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)与氧 1s [轨道](@keyword=orbit|lang=zh-CN|style=Feynman)的电子的结合能有很大不同。因此，XPS [光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)可作为元素的指纹，不仅告诉我们材料中存在哪些元素，还提供了关于它们化学环境的微妙线索。

从微波的轻柔推动到 X 射线的猛烈一击，光子[光谱学](@keyword=optical_spectroscopy|lang=zh-CN|style=Feynman)使我们能够探测分子存在的方方面面。通过仔细聆听这些光子讲述的故事，我们揭示了支配量子世界的基本原理。

