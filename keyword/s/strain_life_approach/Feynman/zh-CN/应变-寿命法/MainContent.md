## 引言
为什么能够承受一次巨大作用力的构件，在承受数千次小得多的重复载荷后却会失效？这种被称为“疲劳”的现象是工程结构失效的主要原因之一，从飞机机翼到汽车悬架都概莫能外。几十年来，工程师们一直依赖基于应力的模型，这些模型在处理大量微[小振动](@keyword=small_oscillations|lang=zh-CN|style=Feynman)时效果很好。然而，这些模型无法解释由较少次数的较大变形引起的失效，在这些情况下，材料会弯曲并发生永久变形。本文深入探讨了[应变-寿命法](@keyword=strain_life_approach|lang=zh-CN|style=Feynman)——一个更全面的框架，它通过将应变视为疲劳损伤的真正驱动因素来解决这一悖论。在接下来的章节中，我们将首先揭示构成这一强大理论基础的基本原理和机制。随后，我们将探索其在现代工程设计中的多样化应用及其与其他科学学科的联系，揭示我们如何在一个复杂的世界中预测和预防[疲劳失效](@keyword=fatigue_failure|lang=zh-CN|style=Feynman)。

## 原理与机制

想象一下，你拿一个金属回形针来[回弯](@keyword=backbending|lang=zh-CN|style=Feynman)折。起初，你可以轻微地弯曲它，它会立刻弹回原状。然而，如果你弯得更厉害，它就会保持弯曲的状态。再经过几次这样的大幅弯折，伴随着一声令人失望的轻微“咔嗒”声，它断了。究竟是什么决定了它断裂的时刻？是你施加的力，还是你弯曲的程度？这个简单的问题是理解和预测[材料疲劳](@keyword=material_fatigue|lang=zh-CN|style=Feynman)的核心。这是一段旅程的开始，它将我们从简单的观察引向一个关于物体在重复载荷下如何断裂的优美统一理论。

### 根本问题：是什么主导失效，应力还是应变？

一个多世纪以来，工程师们一直依赖一个看似直接的理念来预测疲劳：**应力-寿命**或**S-N**法。“S”代表应力（单位面积上的[内力](@keyword=internal_forces|lang=zh-CN|style=Feynman)），“N”代表失效循环次数。其理念很简单：在每个循环中施加的应力越高，零件能承受的循环次数就越少。这在涉及巨大循环次数（数百万甚至数十亿次）的情况下非常有效，此时变形微小，几乎完全是弹性的。想象一下飞机机翼在飞行中几乎察觉不到的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，或是桥梁对交通的响应 [@problem_id:1299034]。在这个**[高周疲劳 (HCF)](@keyword=high_cycle_fatigue_(hcf)|lang=zh-CN|style=Feynman)** 的领域，材料表现为弹性行为，应力是寿命的一个极好预测指标。

但我们的回形针呢？或者车辆在硬着陆时关键悬架部件的情况呢？在这里，构件承受的是少数几次剧烈的载荷，导致其永久弯曲 [@problem_id:1299034]。这就是**[低周疲劳](@keyword=low_cycle_fatigue|lang=zh-CN|style=Feynman) (LCF)** 的世界。在这个世界里，应力失去了其预测能力。

考虑一个思想实验。我们取两个相同的钢制试样。在实验A中，我们控制*应变*——即拉伸量——并强制其在 $0.006$（或 $0.6\%$）的大幅值下循环。我们观察到材料以 $300 \, \mathrm{MPa}$ 的[应力幅](@keyword=stress_amplitude|lang=zh-CN|style=Feynman)值进行抵抗，并在大约 $3,000$ 次循环后失效。在实验B中，我们控制*应力*，强制其在相同的 $300 \, \mathrm{MPa}$ 幅值下循环。我们发现试样现在可以承受超过一百万次循环！[@problem_id:2920072]。

这怎么可能？相同的[应力幅](@keyword=stress_amplitude|lang=zh-CN|style=Feynman)值导致寿命相差一千倍！这个悖论迫使我们得出结论，应力不可能是故事的全部。当变形很大时，真正的罪魁祸首，真正主导失效的因素，必定是**应变**。**应变-寿命**法正是建立在这一基本洞见之上：[疲劳寿命](@keyword=fatigue_life|lang=zh-CN|style=Feynman)由材料所承受的循环应变决定。

### 解构变形：弹性与塑性

要理解为什么应变是更好的指标，我们必须审视其内部构成。当你使[材料变形](@keyword=material_deformation|lang=zh-CN|style=Feynman)时，总应变实际上是两种不同行为的总和 [@problem_id:2920149]。

首先是**弹性应变** $\epsilon_e$。这是“有弹性”的部分。就像一根被拉伸的橡皮筋，这种变形是暂时的，并且完全可以恢复。内部的原子键被拉伸但没有断裂。只要你保持在[弹性极限](@keyword=elastic_limit|lang=zh-CN|style=Feynman)内，当载荷移除时，材料就会恢复其原始形状。这里的关系非常简单：应力与弹性应变成正比，这是一个著名的规律，称为胡克定律 (Hooke's Law)，即 $\sigma = E \epsilon_e$，其中 $E$ 是材料的刚度，或称[杨氏模量](@keyword=young_s_modulus|lang=zh-CN|style=Feynman)。

其次，也是更具破坏性的是**塑性应变** $\epsilon_p$。这是“永久”的部分。当你把回形针弯曲到它保持弯曲状态时，你就引发了塑性应变。你迫使原子滑移到新的位置。这个过程是不可恢复的；它会产生微观损伤，以热量的形式耗散能量，并最终“消耗”掉材料的寿命。

总应变幅值 $\epsilon_a$ 仅仅是任一循环中弹性应变幅值和塑性应变幅值的总和：
$$
\epsilon_a = \epsilon_{a}^{e} + \epsilon_{a}^{p}
$$
在我们的思想实验中，LCF 测试（实验A）具有很大的总应变，其中大部分是破坏性的塑性应变。而 HCF 测试（实验B）尽管应力相同，但其总应变要小得多，几乎完全是无害的弹性应变 [@problem_id:2920072] [@problem_id:2647190]。这一区别是关键。塑性应变是[低周疲劳](@keyword=low_cycle_fatigue|lang=zh-CN|style=Feynman)中损伤的主要驱动力。

### 两大定律的统一：统一[应变-寿命方程](@keyword=strain_life_equation|lang=zh-CN|style=Feynman)

如果总应变由两部分组成，那么每一部分如何对总寿命做出贡献？[应变-寿命法](@keyword=strain_life_approach|lang=zh-CN|style=Feynman)的美妙之处在于它为每个分量都指定了一个独立的“定律”，然后将它们相加。

**[弹性应变](@keyword=elastic_strain|lang=zh-CN|style=Feynman)**分量与寿命的关系由**Basquin定律**描述。它看起来很像旧的[S-N曲线](@keyword=s_n_curve|lang=zh-CN|style=Feynman)，但用应变来表示。它指出，弹性应变幅值 $\epsilon_a^e$ 与失效反向次数（$2N_f$，其中一个循环有两次反向，即拉伸和压缩）通过一个[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)关系相关联：
$$
\epsilon_{a}^{e} = \frac{\sigma_f'}{E}(2N_f)^b
$$
在这里，$\sigma_f'$ 是**疲劳强度系数**，可以看作是材料的固有疲劳强度，而 $b$ 是**疲劳强度指数**，一个负数，决定了随着弹性应变的增加，寿命下降的陡峭程度 [@problem_id:2920135]。这部分方程在[高周疲劳](@keyword=high_cycle_fatigue|lang=zh-CN|style=Feynman)（HCF）区域占主导地位。

**塑性应变**分量由**Coffin-Manson定律**控制，这是LCF分析的真正核心。它也采用幂律形式：
$$
\epsilon_{a}^{p} = \epsilon_f'(2N_f)^c
$$
在这里，$\epsilon_f'$ 是**疲劳[延性](@keyword=ductility|lang=zh-CN|style=Feynman)系数**，衡量材料承受塑性变形的能力，而 $c$ 是**疲劳[延性](@keyword=ductility|lang=zh-CN|style=Feynman)指数**。该项捕捉了由原子面不可逆滑移造成的损伤，并在[低周疲劳](@keyword=low_cycle_fatigue|lang=zh-CN|style=Feynman)（LCF）区域占主导地位。

最后的点睛之笔是简单地将它们相加。这便得到了统一的**[Manson-Coffin-Basquin方程](@keyword=manson_coffin_basquin_equation|lang=zh-CN|style=Feynman)**，这是一个单一、优美的关系式，描述了从短寿命到长寿命整个范围内的疲劳行为 [@problem_id:2647171]：
$$
\epsilon_a = \epsilon_{a}^{e} + \epsilon_{a}^{p} = \frac{\sigma_f'}{E}(2N_f)^b + \epsilon_f'(2N_f)^c
$$
这是一项了不起的成就。它将两个看似不同的疲劳区域——HCF和LCF——统一在一个连贯的数学和物理框架之下。

### [交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点：连接两个世界的桥梁

如果你在对数[坐标图](@keyword=coordinate_map|lang=zh-CN|style=Feynman)上绘制弹性和塑性应变-寿命关系，你会得到两条斜率不同的直线。弹性线较平缓，而塑性线较陡峭。这两条线必然会在某个点相交。这个点被称为**过渡寿命**或**[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)寿命** [@problem_id:2647171]。

过渡寿命是弹性应变和塑性应变对总损伤的贡献相等的循环次数。它不是一个清晰的边界，而是一个标志着HCF和LCF之间[分界线](@keyword=separatrix|lang=zh-CN|style=Feynman)的区域。
-   对于**短于**过渡寿命的情况，塑性应变占主导。材料的行为由其延性决定，就像粘土被反复塑形一样。
-   对于**长于**过渡寿命的情况，[弹性应变](@keyword=elastic_strain|lang=zh-CN|style=Feynman)占主导。材料的行为由其强度和刚度决定，就像一个耐用的弹簧。

这个[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点是材料的一个基本属性，代表了其强度驱动和[延性](@keyword=ductility|lang=zh-CN|style=Feynman)驱动的疲劳抗性之间的[平衡点](@keyword=equilibrium_points|lang=zh-CN|style=Feynman)。

### 材料的循环特性

当我们测试材料的性能时，我们通常进行简单的[拉伸试验](@keyword=tensile_testing|lang=zh-CN|style=Feynman)——一次性将其拉断。但是，材料对一次性突发事件的响应与其对数千次重复循环的响应相同吗？对大多数材料来说，答案是响亮的“不”。

想象一下，让一种材料经受重复的应变循环。一些材料，如许多钢材，实际上会变得更强。每一次循环，微观[位错](@keyword=dislocations|lang=zh-CN|style=Feynman)会堆积和缠结，使得进一步的变形更加困难。这被称为**循环硬化**。而其他材料，如一些[铝合金](@keyword=aluminum_alloys|lang=zh-CN|style=Feynman)，可能会随着循环应变将其[微观结构](@keyword=microstructure|lang=zh-CN|style=Feynman)重组为更软的状态而变弱。这被称为**循环软化**。

这意味着材料在[循环过程](@keyword=cyclic_process|lang=zh-CN|style=Feynman)中遵循的[应力-应变曲线](@keyword=stress_strain_curve|lang=zh-CN|style=Feynman)——其**循环应力-应变曲线**——通常与在单次[拉伸试验](@keyword=tensile_testing|lang=zh-CN|style=Feynman)中测得的曲线不同 [@problem_id:2920146]。为了准确预测疲劳，我们必须表征这种循环特性。这是通过将几次稳定疲劳试验的应力和应变幅值拟合到另一个幂律关系来完成的：
$$
\epsilon_a = \frac{\sigma_a}{E} + \left( \frac{\sigma_a}{K'} \right)^{1/n'}
$$
在这里，$K'$ 和 $n'$ 分别是**循环强度系数**和**循环[应变硬化指数](@keyword=strain_hardening_exponent|lang=zh-CN|style=Feynman)**。这些是材料在*疲劳过程中的*真实属性，而必须使用这些属性来在应变-寿命框架内关联应力和应变。忽略这种循环行为而使用单调数据，就好像根据马拉松运动员的百米冲刺时间来评判他一样——你没有测量适合该项目的正确指标。

### 现实世界的复杂性：平均应力的危害

到目前为止，我们一直想象我们的回形针是对称地来[回弯](@keyword=backbending|lang=zh-CN|style=Feynman)曲。但如果循环是有偏置的呢？如果我们把它从“直”弯到“很弯”，再回到“直”，而从不进入压缩状态呢？这个循环有一个**拉伸平均应力**。

拉伸平均应力对疲劳寿命极其有害。你可以把它想象成一个持续的背景拉力，它有助于撬开微裂纹，阻止它们在循环的压缩部分闭合，从而加速其扩展。相反，压缩平均应力可以挤压裂纹使其闭合，从而延长寿命。

有几种模型可以解释这一点。**[Morrow平均应力修正](@keyword=morrow_mean_stress_correction|lang=zh-CN|style=Feynman)**提供了一个非常简单的想法：一个拉伸平均应力 $\sigma_m$ 只是减少了材料的“强度预算”。它只修改了[应变-寿命方程](@keyword=strain_life_equation|lang=zh-CN|style=Feynman)的弹性部分 [@problem_id:2920046]：
$$
\epsilon_a = \frac{\sigma_f' - \sigma_m}{E}(2N_f)^b + \epsilon_f'(2N_f)^c
$$
另一种流行的方法是**Smith-Watson-Topper (SWT) 参数**，它将最大应力和应变幅值结合成一个单一的损伤参数 $P = \sigma_{\max}\epsilon_a$，直观上与循环[应变能](@keyword=strain_energy|lang=zh-CN|style=Feynman)有关 [@problem_id:2920120]。

但[循环塑性](@keyword=cyclic_plasticity|lang=zh-CN|style=Feynman)的世界还给我们带来了最后一个美妙的惊喜。在LCF条件下，当我们控制应变时，一个带有初始平均应力的材料实际上可以发生松弛！在最初几十或几百个循环中，[滞后回线](@keyword=hysteresis_loop|lang=zh-CN|style=Feynman)会慢慢移动，直到平均应力几乎为零。材料会自己“找到”一个更稳定、对称的应力状态 [@problem_id:2900899]。这种**[平均应力松弛](@keyword=mean_stress_relaxation|lang=zh-CN|style=Feynman)**是材料自组织的一个深刻例子。这也意味着，对于LCF分析，初始平均应力可能不如稳定后的（通常为零的）平均应力那么重要。然而，在HCF中，我们控制应力，机器会强制保持平均应力，因此不会发生松弛。

这最后的精妙之处揭示了我们所发现的物理原理的真正力量和优雅。预测疲劳不仅仅是把数字代入方程。它是关于理解弹性和塑性变形之间的舞蹈，理解材料在[循环加载](@keyword=cyclic_loading|lang=zh-CN|style=Feynman)下特性的演变，以及它对其所经历的力和位移历史的微妙响应方式。