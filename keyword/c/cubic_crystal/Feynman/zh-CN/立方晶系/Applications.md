## 应用与跨学科联系

在我们之前的讨论中，我们惊叹于[立方晶体](@keyword=cubic_crystals|lang=zh-CN|style=Feynman)的朴素之美，一个由[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)简单重复构建而成的完美对称物体。这是一个优雅几何学的世界，由诸如密勒[指数和](@keyword=exponential_sums|lang=zh-CN|style=Feynman)布拉维[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)等抽象概念所描述。但物理学家从不满足于仅仅欣赏抽象的形式；我们必须问，“那又怎样？” 这个隐藏的[原子结构](@keyword=atomic_structure|lang=zh-CN|style=Feynman)——这个微观的原子之城——如何在我们可以触摸、测量和使用的宏观世界中显现出来？将原子放置在立方体的顶点或面心的简单规则，是如何产生构成我们世界的材料的性质的？

本章就是对这个问题的探索之旅。我们将看到，晶体的内部对称性不仅仅是[晶体学](@keyword=crystallography|lang=zh-CN|style=Feynman)家的一个好[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)。它是一种材料强度、电学行为、对[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)的响应，甚至是其外形的根本来源。[立方晶系](@keyword=cubic_systems|lang=zh-CN|style=Feynman)的简单几何学具有深刻而常常令人惊讶的后果，其影响横跨化学、工程学和物理学。

### 窥探内部：晶体的指纹

在我们能够理解[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)如何决定其性质之前，我们首先必须有一种方法来确认这种结构。你不能仅仅看着一块铁或盐，就看到里面的[体心立方](@keyword=body_centered_cubic_(bcc)|lang=zh-CN|style=Feynman)或[面心立方结构](@keyword=face_centered_cubic_structure|lang=zh-CN|style=Feynman)。我们需要一种能够解析原子尺度距离的探针。这个探针就是[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)，而这项技术就是[X射线衍射 (XRD)](@keyword=x_ray_diffraction_(xrd)|lang=zh-CN|style=Feynman)。

想象一下对着峡谷大喊并聆听回声。回声的时间和质量会告诉你一些关于峡谷壁形状的信息。XRD的工作原理类似，但细节要精细得多。当一束[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)照射到晶体上时，波会从有序的原子平面上散射。如果原子平面的间距相对于[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)的波长恰到好处，散射波就会发生[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)，在特定的角度产生一束强烈的反射光束，这一现象由[布拉格定律](@keyword=bragg_s_law|lang=zh-CN|style=Feynman)所支配。通过旋转晶体并测量这些明亮反射出现的角度，我们可以绘制出内部原子平面的间距图。

这张平面间距图是[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)的决定性“指纹”。对于任何立方晶体，具有密勒指数 $(h,k,l)$ 的[晶面](@keyword=crystal_planes|lang=zh-CN|style=Feynman)之间的间距 $d_{hkl}$ 与[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)尺寸，即晶格常数 $a$，通过一个简单的几何公式相关联：$d_{hkl} = \frac{a}{\sqrt{h^2 + k^2 + l^2}}$。请注意，[晶格常数](@keyword=lattice_constant|lang=zh-CN|style=Feynman) $a$ 是给定晶体中所有晶面的一个公因子。这意味着不同[晶面间距](@keyword=interplanar_spacing|lang=zh-CN|style=Feynman)的*比率*与材料的具体晶格常数 $a$ 无关，只与[晶格类型](@keyword=crystal_lattice_types|lang=zh-CN|style=Feynman)有关。