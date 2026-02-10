## 引言
在探索和理解世界的征程中，眼见为实通常是第一步。但当决定功能的结构比一根头发丝的宽度还要小上千倍时，我们该怎么办？我们需要一种全新的眼睛。[扫描电子显微镜 (SEM)](@keyword=scanning_electron_microscopy_(sem)|lang=zh-CN|style=Feynman) 是人类应对这一挑战的最强大工具之一，它能够揭示纳米世界中令人惊叹的复杂结构。当其他显微镜“穿透”样品以观察其内部工作原理时，SEM 却是[表面分析](@keyword=surface_analysis|lang=zh-CN|style=Feynman)的大师，提供细节惊人、栩栩如生的三维视图，真实得仿佛触手可及。它解决了一个根本性问题：当一个物体的行为正是由其表面决定时，我们如何才能将一个细胞复杂的形貌、一块金属的断裂面或一种新材料的[晶体结构](@keyword=crystal_structures|lang=zh-CN|style=Feynman)可视化？

本文将[引导](@keyword=bootstrapping|lang=zh-CN|style=Feynman)您进入SEM的世界。首先，在“原理与机制”一章中，我们将探索显微镜背后优雅的物理学原理，将其与它的“近亲”TEM进行对比，并解释SEM如何利用[电子](@keyword=electrons|lang=zh-CN|style=Feynman)信号逐个像素地“绘制”出图像。随后，在“应用与跨学科联系”一章中，我们将见证这项技术令人难以置信的多功能性，看它如何在生物学、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)和工程学中扮演建筑师之眼、侦探之镜以及[化学分析](@keyword=chemical_analysis|lang=zh-CN|style=Feynman)平台的角色。

## 原理与机制

想象一下，您想了解一台复杂的机器。您可以拍摄一张X光片来观察其内部的齿轮和线路，也可以拍摄一张其外壳的精细照片来研究它的形状、纹理和[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)。这两种视角都非常有用，但它们讲述的是截然不同的故事。这是理解[电子显微镜](@keyword=electron_microscope|lang=zh-CN|style=Feynman)世界的第一个也是最重要的原则。这是一个拥有两种截然不同观察方式的世界。

### 两种显微镜的故事：观察“表面”与“穿透”观察

一种[电子显微镜](@keyword=electron_microscope|lang=zh-CN|style=Feynman)是**[透射电子显微镜 (TEM)](@keyword=transmission_electron_microscopy_(tem)|lang=zh-CN|style=Feynman)**，它好比纳米世界的X光机。它将一束宽幅高能[电子](@keyword=electrons|lang=zh-CN|style=Feynman)束*穿透*一个极薄的材料切片——可能是一片只有90纳米厚的新型钢[合金](@keyword=alloys|lang=zh-CN|style=Feynman)薄片，或是一个单细胞的[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)。图像由成功穿过样品的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)形成。一些[电子](@keyword=electrons|lang=zh-CN|style=Feynman)会被致密的内部特征（如钢中形成的析出相或细胞内复杂的[细胞器](@keyword=organelles|lang=zh-CN|style=Feynman)）[散射](@keyword=scattering|lang=zh-CN|style=Feynman)或阻挡，从而在下方的探测器上形成一个类似阴影的投影。因此，TEM的本质决定了它揭示的是物体的内部结构 [@problem_id:1345351] [@problem_id:2303211]。

**[扫描电子显微镜 (SEM)](@keyword=scanning_electron_microscopy_(sem)|lang=zh-CN|style=Feynman)**，即我们在此讨论的[主角](@keyword=principal_angles|lang=zh-CN|style=Feynman)，是表面形貌的摄影大师。它对内部结构不感兴趣。它的使命是捕捉世界上错综复杂的形貌——细胞崎岖不平的外部、金属的断裂面、花粉粒的精巧结构。SEM并不*穿透*其对象；它通过“聆听”用一根极其精细的探针触碰表面时产生的微弱“私语”和“回声”来生成其非凡的图像。

### 用[电子](@keyword=electrons|lang=zh-CN|style=Feynman)作画：扫描的艺术

如何用[电子](@keyword=electrons|lang=zh-CN|style=Feynman)“触碰”一个表面并由此构建出一幅图像呢？这个过程是工程学上的一个奇迹。SEM并非试图一次性看到整个表面。相反，它使用一系列电[磁透镜](@keyword=magnetic_lens|lang=zh-CN|style=Feynman)将[电子](@keyword=electrons|lang=zh-CN|style=Feynman)聚焦成一束极其精细的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)束，形成一个比任何物理针尖都更加锐利的“探针”。然后，这束探针以精确的网格模式在样品上进行扫描，这个过程称为[光栅](@keyword=diffraction_grating|lang=zh-CN|style=Feynman)扫描，就像您的眼睛扫描本页的文字一样。在每一个点上，显微镜都会短暂停留并进行“聆听”。

但它在“聆听”什么呢？当探针中的高能[电子](@keyword=electrons|lang=zh-CN|style=Feynman)撞击表面时，它们会引发一场微小而局域化的相互作用风暴。其中，对于创造那些美丽、富有纹理的图像而言，最重要的是**[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)**的产生。您可以将这些[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)想象成从样品材料最表面的几纳米深度被“溅”出的一小撮低能[电子](@keyword=electrons|lang=zh-CN|style=Feynman)。它们是真正的表面信号。

一个通常放置在侧面的探测器负责收集这些[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)。巧妙之处在于：逃离表面并到达探测器的[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)数量，在很大程度上取决于局部的几何形状。如果[电子](@keyword=electrons|lang=zh-CN|style=Feynman)束击中一个平坦的区域，[电子](@keyword=electrons|lang=zh-CN|style=Feynman)会向四面八方飞溅，探测器只能捕捉到一小部分。但如果[电子](@keyword=electrons|lang=zh-CN|style=Feynman)束击中悬崖的边缘或山丘的斜坡，就会有更多的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)朝着探测器的方向飞溅出去。结果如何？在最终的图像中，边缘、脊线和凸起会显得异常明亮，而平坦的区域和凹陷则显得较暗。通过将屏幕上每个像素的[亮度](@keyword=luminance|lang=zh-CN|style=Feynman)与样品上相应点测得的[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)信号强度[同步](@keyword=synchronization|lang=zh-CN|style=Feynman)，显微镜逐个像素地绘制出一幅细节惊人的形貌图 [@problem_id:2087808]。

### 表面的两种声音：形貌与成分

故事并没有随着[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)的出现而结束。初级[电子](@keyword=electrons|lang=zh-CN|style=Feynman)束的撞击是一个信息丰富的事件，它还会产生另一种重要的信号——一种不同类型的回声。[二次电子](@keyword=secondary_electrons|lang=zh-CN|style=Feynman)是低能量的“飞溅物”，而一些入射的高能[电子](@keyword=electrons|lang=zh-CN|style=Feynman)则可以穿透到样品更深处，与重[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)发生近距离接触，然后反弹出来。这些就是**[背散射电子](@keyword=backscattered_electrons|lang=zh-CN|style=Feynman) (BSE)**。

因为它们被偏转

