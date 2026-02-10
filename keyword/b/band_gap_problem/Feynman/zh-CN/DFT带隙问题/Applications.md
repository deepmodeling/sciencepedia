## 应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系

既然我们已经深入探讨了[带隙问题](@keyword=band_gap_problem|lang=zh-CN|style=Feynman)的根源——我们简单的模型与现实之间这个奇怪而持续的差异——那么我们有理由问：*所以呢？* 为什么要为区区几个[电子伏特](@keyword=electron_volt|lang=zh-CN|style=Feynman)大费周章？如果我们计算出一种材料的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)是$1\,\text{eV}$而实际上应该是$2\,\text{eV}$，这真的重要吗？

事实证明，答案是响亮的*“是”*。这个“小”误差，就是透明导体与无用绝缘体之间的区别，是明亮的[发光二极管](@keyword=light_emitting_diodes|lang=zh-CN|style=Feynman)（LED）与昏暗加热器之间的区别，是您电脑里的硅与一块沙子之间的区别。我们讨论的原理并非深奥的理论产物；它们是通往设计未来材料的大门。本章将带领我们走进科学家和工程师的工作坊，在那里，[带隙问题](@keyword=band_gap_problem|lang=zh-CN|style=Feynman)不是教科书上的练习，而是日常的障碍和创造性的挑战。

### 首要任务：确定正确的材料

对于任何电子应用而言，材料最基本的属性是它是金属、[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)还是绝缘体。这当然是由其[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)决定的。在设计新材料时，我们的首要任务就是正确预测这一属性。在这里，我们理论工具的选择——即[交换相关泛函](@keyword=exchange_correlation_functional|lang=zh-CN|style=Feynman)——至关重要。

作为一个简单的图景，想象一下，不同的[DFT泛函](@keyword=dft_functionals|lang=zh-CN|style=Feynman)就像是电子在晶体内部感受到的[有效势](@keyword=effective_potential|lang=zh-CN|style=Feynman)的不同配方。一个简单的配方，如[广义梯度近似](@keyword=generalized_gradient_approximation|lang=zh-CN|style=Feynman)（GGA）中的PBE，会产生一个相当平滑、温和的势场。这导致电子允许[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)之间的分离较小——即[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)较小。一个更复杂的“杂化”泛函配方则混入了一部分“尖锐”的、非局域的[Hartree-Fock交换](@keyword=hartree_fock_exchange|lang=zh-CN|style=Feynman)，这给势场带来了更强的“踢力”，倾向于将[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)分得更开，从而扩大了[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。例如，在一个氧化锌的玩具模型中，类似PBE的势可能只产生$0.8\,\text{eV}$的微小[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，而对于同一系统，类似杂化的势则会将其打开到更接近现实的$3.4\,\text{eV}$ ([@problem_id:2462509])。

这不仅仅是玩具模型的特征。让我们看看硅，这个定义了我们时代的元素。我们以极高的精度知道它的实验[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，约为$1.17\,\text{eV}$。这使得硅成为磨砺我们理论工具的完美磨刀石。如果我们用简单的[PBE泛函](@keyword=pbe_functional|lang=zh-CN|style=Feynman)进行计算，得到的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)约为$0.6\,\text{eV}$——误差接近$50\%$！该材料被预测为[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)，但性能很差。如果我们使用所谓的全局杂化泛函，它在各处都混合了固定百分比的[精确交换](@keyword=exact_exchange|lang=zh-CN|style=Feynman)呢？我们可能会发现[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)超出了目标，达到了$1.8\,\text{eV}$。