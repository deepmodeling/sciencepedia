## 引言
[韦尔定律](@entry_id:188635)（Weyl's Law）是[谱几何](@entry_id:186460)学的基石之一，深刻地揭示了黎曼流形上的“声音”（由[拉普拉斯-贝尔特拉米算子](@entry_id:267002)的[特征值](@entry_id:154894)谱决定）与其“形状”（由体积等[几何不变量](@entry_id:178611)刻画）之间的定量关系。对于一个给定的[流形](@entry_id:153038)，其拉普拉斯算子拥有一系列离散的[特征值](@entry_id:154894)，但这些数值是如何[分布](@entry_id:182848)的？它们的密度随着能量的增高如何变化？[韦尔定律](@entry_id:188635)正是为了回答这一根本问题而生，它提供了一个优美的[渐近公式](@entry_id:189846)，将[特征值](@entry_id:154894)的宏观[分布](@entry_id:182848)与[流形](@entry_id:153038)的体积联系起来。本文将系统地引导读者深入理解这一定律。在“原理与机制”一章中，我们将阐明[韦尔定律](@entry_id:188635)的精确表述，并通过半[经典相空间](@entry_id:195767)分析与热[核方法](@entry_id:276706)两种视角揭示其背后的物理与数学机制。接着，在“应用与跨学科联系”一章，我们将探讨该定律如何被精化以提取更多几何信息，并展示其在物理学、工程学等领域的广泛应用。最后，通过“动手实践”部分，读者将有机会通过具体的计算来巩固和应用所学知识，从而真正掌握这一连接分析与几何的强大工具。

## 原理与机制

本章深入探讨[韦尔定律](@entry_id:188635)（Weyl's Law）背后的核心原理与关键机制。我们将从作为研究对象的[拉普拉斯-贝尔特拉米算子](@entry_id:267002)（Laplace-Beltrami operator）及其谱的基本性质出发，逐步揭示[韦尔定律](@entry_id:188635)的精确表述。随后，我们将通过两种互补的视角——半[经典相空间](@entry_id:195767)分析与热[核方法](@entry_id:276706)——来阐释该定律的由来。最后，本章将讨论[韦尔定律](@entry_id:188635)在一些重要情形下的推广，包括[带边流形](@entry_id:159788)上的二项展开以及“局部”形式的[韦尔定律](@entry_id:188635)。

### [拉普拉斯-贝尔特拉米算子](@entry_id:267002)及其谱

在[黎曼几何](@entry_id:160508)中，[拉普拉斯-贝尔特拉米算子](@entry_id:267002)是研究[流形](@entry_id:153038)上函数性质的核心工具，它将[欧氏空间](@entry_id:138052)中的[拉普拉斯算子](@entry_id:146319)推广到了弯曲空间。对于一个紧致的 $n$ 维黎曼流形 $(M,g)$，我们关注其上的谱问题，即寻找该算子的[特征值与特征函数](@entry_id:167055)。

#### 定义与基本性质

对于定义在 $M$ 上的[光滑函数](@entry_id:267124) $u \in C^\infty(M)$，其梯度 $\nabla u$ 是一个向量场，由[微分](@entry_id:158718) $du$ 通过度量 $g$ 对偶得到。[向量场的散度](@entry_id:136342) $\operatorname{div}(X)$ 定义为向量场 $X$ 的[协变导数](@entry_id:152476) $\nabla X$ 的迹。分析学中通常采用的[拉普拉斯-贝尔特拉米算子](@entry_id:267002)定义为：
$$
\Delta u = -\operatorname{div}(\nabla u)
$$
这个定义中的负号使得该算子成为一个**非负算子**（non-negative operator）。通过[格林第一恒等式](@entry_id:170345)（Green's first identity），我们可以看到这一点。对于一个无边[流形](@entry_id:153038)，我们有：
$$
\langle \Delta u, u \rangle_{L^2} = \int_M (-\operatorname{div}(\nabla u)) u \, dV_g = \int_M g(\nabla u, \nabla u) \, dV_g = \int_M |\nabla u|_g^2 \, dV_g \ge 0
$$
其中 $dV_g$ 是由度量 $g$ 诱导的[体积元](@entry_id:267802)。这个积分表达式 $\int_M |\nabla u|_g^2 \, dV_g$ 通常被称为函数的**[狄利克雷能量](@entry_id:276589)**（Dirichlet energy）。由于度量 $g$ 是正定的，该积分值恒为非负。

#### 谱问题与谱的性质

谱问题是在[函数空间](@entry_id:143478) $L^2(M)$ 中求解[特征方程](@entry_id:265849) $\Delta \varphi = \lambda \varphi$，其中 $\varphi$ 是非零函数。满足该方程的 $\lambda$ 称为**[特征值](@entry_id:154894)**（eigenvalue），对应的 $\varphi$ 称为**[特征函数](@entry_id:186820)**（eigenfunction）。

对于一个紧致[黎曼流形](@entry_id:261160)，[拉普拉斯-贝尔特拉米算子](@entry_id:267002)的谱具有一系列优良的性质 [@problem_id:3006772] [@problem_id:3006811]。

1.  **[谱的离散性](@entry_id:636233)**：谱是由一列趋向于无穷大的离散实数构成的，我们可以将其从小到大[排列](@entry_id:136432)（计入重数）：
    $$
    0 = \lambda_0 \le \lambda_1 \le \lambda_2 \le \cdots \to \infty
    $$
    这一性质的根源在于[流形](@entry_id:153038) $M$ 的**紧致性**。紧致性保证了算子的[预解式](@entry_id:199555) $(\Delta + I)^{-1}$ 是 $L^2(M)$ 上的一个紧算子。根据希尔伯特-施密特理论（Hilbert-Schmidt theory），[紧自伴算子](@entry_id:147701)的谱是离散的。具体而言，[椭圆正则性理论](@entry_id:203755)保证了 $(\Delta + I)^{-1}$ 是一个从 $L^2(M)$ 到索博列夫空间 $H^2(M)$ 的[有界算子](@entry_id:264879)。而对于[紧致流形](@entry_id:158804)，**雷利希-康德拉绍夫[嵌入定理](@entry_id:150872)**（[Rellich-Kondrachov](@entry_id:140267) theorem）指出，嵌入映射 $H^2(M) \hookrightarrow L^2(M)$ 是一个紧算子。因此，作为[有界算子](@entry_id:264879)和紧[算子复合](@entry_id:268772)的[预解式](@entry_id:199555) $(\Delta + I)^{-1}$ 也是紧的。

2.  **[特征函数](@entry_id:186820)的完备性与正交性**：与[特征值](@entry_id:154894)序列对应的[特征函数](@entry_id:186820) $\{\varphi_j\}_{j=0}^\infty$ 可以被选取为 $L^2(M)$ 空间中的一个**完备[正交基](@entry_id:264024)**。这意味着：
    -   **正交性**：若 $\lambda_j \neq \lambda_k$，则 $\langle \varphi_j, \varphi_k \rangle_{L^2} = 0$。对于[重根](@entry_id:151486)[特征值](@entry_id:154894)，其特征[子空间](@entry_id:150286)内的函数可以通过格拉姆-施密特（Gram-Schmidt）方法[正交化](@entry_id:149208)。
    -   **完备性**：任何 $L^2(M)$ 中的函数 $f$ 都可以展开为[傅里叶级数](@entry_id:139455) $f = \sum_{j=0}^\infty c_j \varphi_j$（其中 $c_j = \langle f, \varphi_j \rangle_{L^2}$），该级数在 $L^2$ 范数下收敛于 $f$。
    -   **[光滑性](@entry_id:634843)**：[椭圆正则性](@entry_id:177548)进一步保证了所有特征函数都是光滑的，即 $\varphi_j \in C^\infty(M)$。

3.  **零[特征值](@entry_id:154894)**：最小的[特征值](@entry_id:154894) $\lambda_0 = 0$ 有着特殊的几何意义。由于 $\langle \Delta u, u \rangle_{L^2} = \int_M |\nabla u|_g^2 \, dV_g = 0$ 当且仅当 $\nabla u = 0$，这意味着 $u$ 在[流形](@entry_id:153038)的每个连通分支上都是常数。对于一个连通的[流形](@entry_id:153038) $M$，[特征值](@entry_id:154894) $\lambda_0=0$ 的特征[子空间](@entry_id:150286)由常函数构成，因此其重数为1。此外，任何与非零[特征值](@entry_id:154894) $\lambda_j \neq 0$ 对应的特征函数 $\varphi_j$ 都与常函数正交，这意味着其在[流形上的积分](@entry_id:156150)为零：$\int_M \varphi_j \, dV_g = 0$。

### [韦尔定律](@entry_id:188635)：[特征值](@entry_id:154894)的[渐近分布](@entry_id:272575)

我们已经知道，紧致[流形上的[拉普拉斯算](@entry_id:184243)子](@entry_id:146319)有无穷多个[特征值](@entry_id:154894)。一个自然的问题是：这些[特征值](@entry_id:154894)是如何[分布](@entry_id:182848)的？或者说，随着能量的增加，[特征值](@entry_id:154894)的“密度”如何变化？[韦尔定律](@entry_id:188635)精确地回答了这个问题。

首先，我们定义**[特征值计数函数](@entry_id:198458)**（eigenvalue counting function）$N(\lambda)$，它计算了所有不大于给定值 $\lambda$ 的[特征值](@entry_id:154894)的数量：
$$
N(\lambda) = \#\{j : \lambda_j \le \lambda\}
$$
[韦尔定律](@entry_id:188635)描述了当 $\lambda \to \infty$ 时，$N(\lambda)$ 的[渐近行为](@entry_id:160836)。

**[韦尔定律](@entry_id:188635) (Weyl's Law)**：对于一个紧致的 $n$ 维[黎曼流形](@entry_id:261160) $(M,g)$，其[特征值计数函数](@entry_id:198458) $N(\lambda)$ 满足如下渐近关系：
$$
N(\lambda) \sim \frac{\omega_n \operatorname{Vol}(M)}{(2\pi)^n} \lambda^{n/2} \quad \text{as } \lambda \to \infty
$$
其中：
- $n = \dim(M)$ 是[流形](@entry_id:153038)的维数。
- $\operatorname{Vol}(M)$ 是[流形](@entry_id:153038) $M$ 的黎曼体积。
- $\omega_n$ 是 $\mathbb{R}^n$ 中单位球体的体积，其值为 $\omega_n = \frac{\pi^{n/2}}{\Gamma(n/2+1)}$。

[韦尔定律](@entry_id:188635)是一个深刻的结果，它在分析（谱）与几何（体积）之间建立了一座宏伟的桥梁。公式表明，[特征值](@entry_id:154894)的[渐近分布](@entry_id:272575)在主阶上仅由[流形](@entry_id:153038)的两个最基本的[几何不变量](@entry_id:178611)——维数和体积——所决定。

一个核心的洞察是，[韦尔定律](@entry_id:188635)描述的是**高频**（即大[特征值](@entry_id:154894)）现象，而高频现象本质上是**局部的** [@problem_id:3006774]。具有非常大[特征值](@entry_id:154894) $\lambda_j$ 的特征函数 $\varphi_j$ 会在空间中剧烈[振荡](@entry_id:267781)，其波长近似为 $1/\sqrt{\lambda_j}$。当波长远小于[流形](@entry_id:153038)的[曲率半径](@entry_id:274690)时，这些波“感觉”不到[流形](@entry_id:153038)的宏观弯曲或拓扑结构，它们的行为非常接近于在平坦的欧氏空间中的表现。因此，[特征值](@entry_id:154894)的整体[渐近分布](@entry_id:272575)可以通过将[流形](@entry_id:153038)视为由许多微小的、近似平坦的区域拼接而成来理解。最终的结果是对这些局部贡献的积分，这自然地导出了[流形](@entry_id:153038)的总 体积 $\operatorname{Vol}(M)$。[流形](@entry_id:153038)的曲率、拓扑等更精细的几何信息只会影响到 $N(\lambda)$ [渐近展开](@entry_id:173196)的低阶项。

### 机制一：半[经典相空间](@entry_id:195767)视角

理解[韦尔定律](@entry_id:188635)的第一个强大机制源于物理学中的[半经典近似](@entry_id:147497)思想。该方法将量子系统的能谱问题（由算子[特征值](@entry_id:154894)描述）与经典力学系统的相空间几何联系起来。

#### 从[量子态](@entry_id:146142)到相空间

在经典力学中，一个系统的状态由其位置 $x$ 和动量 $p$ 共同决定，所有可能状态的集合构成**相空间**。对于在[流形](@entry_id:153038) $M$ 上运动的粒子，其相空间是[余切丛](@entry_id:185138) $T^*M$。每个点 $(x, \xi) \in T^*M$ 代表粒子在位置 $x \in M$ 时具有动量（余向量）$\xi \in T_x^*M$。

[量子力学中的算子](@entry_id:262952)，如 $-\Delta$，对应于相空间上的一个经典函数，称为其**主象征**（principal symbol）。对于拉普拉斯算子，其主象征正是经典动能函数。在[局部坐标](@entry_id:181200)下，$-\Delta$ 的最高阶部分形如 $\sum_{i,j} g^{ij}(x) \frac{\partial^2}{\partial x^i \partial x^j}$，其主象征通过将 $\frac{\partial}{\partial x^i}$ 替换为动量分量 $\xi_i$ 得到：
$$
p(x, \xi) = \sum_{i,j=1}^n g^{ij}(x) \xi_i \xi_j = |\xi|_g^2
$$
这里的 $|\xi|_g^2$ 是动量余向量 $\xi$ 在点 $x$ 处由度量 $g$ 诱导的范数平方。

#### 半经典启发式计数

半经典[对应原理](@entry_id:155778)启发我们：能量不大于 $\lambda$ 的[量子态](@entry_id:146142)（即[特征值](@entry_id:154894) $\lambda_j \le \lambda$）的数量，约等于相空间中经典能量不大于 $\lambda$ 的区域的体积，再除以每个[量子态](@entry_id:146142)所占据的“最小”相空间体积。根据不确定性原理，这个最小体积在每个自由度上是 $2\pi\hbar$。在我们的数学设定中，取 $\hbar=1$，则每个[量子态](@entry_id:146142)占据的相空间体积为 $(2\pi)^n$ [@problem_id:3006773] [@problem_id:3006788]。

因此，[特征值计数函数](@entry_id:198458) $N(\lambda)$ 可以被近似为：
$$
N(\lambda) \approx \frac{1}{(2\pi)^n} \operatorname{Vol}\left(\left\{ (x,\xi) \in T^*M \mid |\xi|_g^2 \le \lambda \right\}\right)
$$
这里的体积是在 $T^*M$ 上由标准刘维尔测度（Liouville measure）定义的。

#### 推导[韦尔定律](@entry_id:188635)

现在我们来计算这个相空间区域的体积。该体积可以表示为[对流](@entry_id:141806)形 $M$ 的积分，其中在每个点 $x$ 处，我们计算满足[能量条件](@entry_id:158507)的[动量空间](@entry_id:148936)的体积：
$$
\operatorname{Vol}\left(\left\{ |\xi|_g^2 \le \lambda \right\}\right) = \int_M \left( \int_{\xi \in T_x^*M, |\xi|_g^2 \le \lambda} d^n\xi \right) dV_g(x)
$$
对于固定的点 $x$，条件 $|\xi|_g^2 \le \lambda$ 在该点的[余切空间](@entry_id:270516) $T_x^*M \cong \mathbb{R}^n$ 中定义了一个 $n$ 维实心椭球。该椭球的体积等于一个半径为 $\sqrt{\lambda}$ 的标准 $n$ 维球体的体积，即 $\omega_n (\sqrt{\lambda})^n = \omega_n \lambda^{n/2}$。因此，动量空间的积分为一个不依赖于 $x$ 的常数 $\omega_n \lambda^{n/2}$。

将此结果代回原积分，我们得到：
$$
\operatorname{Vol}\left(\left\{ |\xi|_g^2 \le \lambda \right\}\right) = \int_M \omega_n \lambda^{n/2} \, dV_g(x) = \omega_n \lambda^{n/2} \int_M dV_g(x) = \omega_n \operatorname{Vol}(M) \lambda^{n/2}
$$
最后，根据半经典[启发式](@entry_id:261307)计数法则，除以 $(2\pi)^n$，我们便得到了[韦尔定律](@entry_id:188635)的表达式：
$$
N(\lambda) \approx \frac{\omega_n \operatorname{Vol}(M)}{(2\pi)^n} \lambda^{n/2}
$$
这个推导清晰地展示了公式中各项的来源：$\lambda^{n/2}$ 来自于动能与动量的二次关系，$\omega_n$ 来自于 $n$ 维动量空间的球体体积，$\operatorname{Vol}(M)$ 来自于对整个位置[空间的积](@entry_id:151742)分。

其中的通用因子 $(2\pi)^{-n}$ 深刻地根植于[傅里叶分析](@entry_id:137640)的归一化约定 [@problem_id:3006790]。在[伪微分算子](@entry_id:192996)（pseudodifferential operator）理论中，[算子的迹](@entry_id:185149)可以通过对其象征在相空间上积分得到，而这个积分恰好就带有 $(2\pi)^{-n}$ 这个因子。这正是“每个[量子态](@entry_id:146142)占据 $(2\pi)^n$ 相空间体积”这一物理直觉的严格数学体现。

### 机制二：热[核方法](@entry_id:276706)

第二种理解和严格证明[韦尔定律](@entry_id:188635)的方法是热[核方法](@entry_id:276706)。这是一种强大的分析工具，它将谱问题转化为研究[流形上的热传导方程](@entry_id:272321)。

#### [热迹](@entry_id:200414)与谱的关系

考虑[流形](@entry_id:153038) $M$ 上的热传导方程 $\frac{\partial u}{\partial t} = -\Delta u$。其解可以由热算子 $e^{-t\Delta}$ 给出。对于 $t>0$，热算子的**迹**（trace），称为**[热迹](@entry_id:200414)**（heat trace），可以写成所有[特征值](@entry_id:154894)的玻尔兹曼因子之和：
$$
Z(t) = \operatorname{Tr}(e^{-t\Delta}) = \sum_{j=0}^{\infty} e^{-t\lambda_j}
$$
这个函数可以看作是谱的生成函数：它编码了关于所有[特征值](@entry_id:154894)的信息。同时，[热迹](@entry_id:200414)也可以表示为[特征值计数函数](@entry_id:198458) $N(\lambda)$ 的拉普拉斯-斯蒂尔切斯变换（Laplace-Stieltjes transform）：
$$
Z(t) = \int_0^\infty e^{-t\lambda} \, dN(\lambda)
$$

#### [热迹](@entry_id:200414)的小时间[渐近展开](@entry_id:173196)

热[核方法](@entry_id:276706)的核心是研究当时间 $t \to 0^+$ 时[热迹](@entry_id:200414)的行为。对于一个紧致无边[流形](@entry_id:153038)，[热迹](@entry_id:200414)有一个著名的[渐近展开](@entry_id:173196)式（Minakshisundaram-Pleijel expansion）：
$$
Z(t) \sim \frac{1}{(4\pi t)^{n/2}} \sum_{k=0}^{\infty} a_k t^k = \frac{1}{(4\pi t)^{n/2}}(a_0 + a_1 t + a_2 t^2 + \cdots)
$$
其中系数 $a_k$ 是[流形](@entry_id:153038)的[几何不变量](@entry_id:178611)，称为**热[不变量](@entry_id:148850)**（heat invariants）。最重要的前两个系数为：
- $a_0 = \operatorname{Vol}(M)$
- $a_1 = \frac{1}{6} \int_M R \, dV_g$，其中 $R$ 是[流形](@entry_id:153038)的数量曲率。

[热迹](@entry_id:200414)的主项 $\frac{\operatorname{Vol}(M)}{(4\pi t)^{n/2}}$ 再次体现了高频现象的局部性：当时间极短时，热量没有足够时间传播到远处，其行为主要由局部的欧氏[热核](@entry_id:172041)决定。

#### 陶伯定理之桥

我们现在有两个关于谱的信息：一个是 $N(\lambda)$ 在 $\lambda \to \infty$ 时的行为（我们想求的），另一个是其拉普拉斯变换 $Z(t)$ 在 $t \to 0^+$ 时的行为。**陶伯定理**（Tauberian theorems）正是连接一个函数与其[拉普拉斯变换](@entry_id:159339)在不同极限下行为的桥梁。

具体来说，**卡拉马塔陶伯定理**（Karamata's Tauberian Theorem）的一个版本是 [@problem_id:3006777]：
> 假设 $N(\lambda)$ 是一个非减函数，其拉普拉斯-斯蒂尔切斯变换 $L(t) = \int_0^\infty e^{-t\lambda} dN(\lambda)$。若当 $t \to 0^+$ 时，$L(t) \sim A t^{-\alpha}$（其中 $A>0, \alpha>0$），则当 $\lambda \to \infty$ 时，$N(\lambda) \sim \frac{A}{\Gamma(\alpha+1)} \lambda^\alpha$。

#### 再次推导[韦尔定律](@entry_id:188635)

现在我们可以将陶伯定理应用于[热迹](@entry_id:200414) $Z(t)$。其主项行为是：
$$
Z(t) \sim \frac{\operatorname{Vol}(M)}{(4\pi)^{n/2}} t^{-n/2}
$$
这对应于陶伯定理中的 $A = \frac{\operatorname{Vol}(M)}{(4\pi)^{n/2}}$ 和 $\alpha = n/2$。根据定理，我们立即得到 $N(\lambda)$ 的[渐近行为](@entry_id:160836)：
$$
N(\lambda) \sim \frac{A}{\Gamma(\alpha+1)} \lambda^\alpha = \frac{\operatorname{Vol}(M)}{(4\pi)^{n/2}\Gamma(n/2+1)} \lambda^{n/2}
$$
为了将系数与之前的形式统一，我们使用 $\omega_n$ 的定义 $\omega_n = \frac{\pi^{n/2}}{\Gamma(n/2+1)}$。替换 $\Gamma(n/2+1)$，我们得到系数为：
$$
\frac{\operatorname{Vol}(M)}{(4\pi)^{n/2}} \frac{\omega_n}{\pi^{n/2}} = \frac{\operatorname{Vol}(M)}{2^n \pi^{n/2}} \frac{\omega_n}{\pi^{n/2}} = \frac{\omega_n \operatorname{Vol}(M)}{2^n \pi^n} = \frac{\omega_n \operatorname{Vol}(M)}{(2\pi)^n}
$$
这与我们通过[半经典方法](@entry_id:181818)得到的结果完全一致 [@problem_id:3006798]。热[核方法](@entry_id:276706)为[韦尔定律](@entry_id:188635)提供了坚实的分析基础，并揭示了两种推导方式内在的一致性。

### [韦尔定律](@entry_id:188635)的推广与精化

[韦尔定律](@entry_id:188635)不仅仅局限于紧致无边[流形](@entry_id:153038)，它可以被推广和精化，以适应更广泛的几何情境。

#### 边界的角色：二项[韦尔定律](@entry_id:188635)

当[流形](@entry_id:153038) $(M,g)$ 具有光滑边界 $\partial M$ 时，谱问题需要指定边界条件，最常见的是**狄利克雷边界条件**（Dirichlet boundary condition，即函数在边界上为零）和**[诺伊曼边界条件](@entry_id:142124)**（Neumann boundary condition，即函数在边界上的[法向导数](@entry_id:169511)为零）。

在这种情况下，[韦尔定律](@entry_id:188635)的主项依然成立，但[渐近展开](@entry_id:173196)中会出现一个与边界相关的次阶项。这就是**二项[韦尔定律](@entry_id:188635)**（two-term Weyl law）。对于狄利克雷（$D$）或诺伊曼（$N$）问题，其计数函数 $N_B(\lambda)$ 的[渐近行为](@entry_id:160836)是 [@problem_id:3006800] [@problem_id:3006792]：
$$
N_B(\lambda) = \frac{\omega_n \operatorname{Vol}(M)}{(2\pi)^n} \lambda^{n/2} \pm \frac{\omega_{n-1} \operatorname{Vol}(\partial M)}{4(2\pi)^{n-1}} \lambda^{(n-1)/2} + o(\lambda^{(n-1)/2})
$$
其中 $\operatorname{Vol}(\partial M)$ 是 $(n-1)$ 维边界的体积。

关键在于次阶项的符号：
- 对于**[诺伊曼条件](@entry_id:165471)**，取**正号** ($+$)。
- 对于**[狄利克雷条件](@entry_id:137096)**，取**负号** ($-$)。

这个符号差异有直观的物理解释。[狄利克雷条件](@entry_id:137096)（将函数“钉死”在边界上）比[诺伊曼条件](@entry_id:165471)（只限制其法向变化率）的约束更强。更强的约束会“推高”所有[特征值](@entry_id:154894)。因此，在任何给定的能量阈值 $\lambda$ 以下，[狄利克雷问题](@entry_id:274408)包含的特征态数量会比[诺伊曼问题](@entry_id:176713)少。这个差异正体现在次阶修正项的符号上。负号修正意味着狄利克雷谱的[态密度](@entry_id:147894)比仅由体积决定的主项要稀疏一些，而正号修正则意味着诺伊曼谱更密集。

#### 局部[韦尔定律](@entry_id:188635)

[韦尔定律](@entry_id:188635)描述的是整个谱的全局[渐近行为](@entry_id:160836)。一个自然的问题是：我们能否描述[特征函数](@entry_id:186820)在空间中的能量[分布](@entry_id:182848)？这就是**局部[韦尔定律](@entry_id:188635)**（local Weyl law）要回答的问题。

我们定义**[谱函数](@entry_id:147628)**（spectral function）$e(\lambda, x)$：
$$
e(\lambda, x) = \sum_{\lambda_j \le \lambda} |\varphi_j(x)|^2
$$
这个函数可以理解为在点 $x$ 处，所有能量不大于 $\lambda$ 的[特征模](@entry_id:174677)态的能量密度之和。它是[谱投影算子](@entry_id:755184)积分核的对角线值。

对于[流形](@entry_id:153038)内部的点 $x \in \operatorname{int}(M)$，局部[韦尔定律](@entry_id:188635)表明 [@problem_id:3006814]：
$$
e(\lambda, x) = \frac{\omega_n}{(2\pi)^n} \lambda^{n/2} + O(\lambda^{(n-1)/2})
$$
这个公式在 $M$ 的任何紧致[子集](@entry_id:261956)上是一致成立的。令人惊讶的是，其主项是一个不依赖于点 $x$ 的常数！这表明，在高频极限下，特征函数的能量在[流形](@entry_id:153038)内部是[均匀分布](@entry_id:194597)的。

我们可以通过对局部[韦尔定律](@entry_id:188635)在整个[流形](@entry_id:153038)上积分来验证其与全局定律的自洽性。利用[特征函数](@entry_id:186820)的[归一化条件](@entry_id:156486) $\int_M |\varphi_j(x)|^2 dV_g = 1$，我们有：
$$
\int_M e(\lambda, x) \, dV_g = \int_M \sum_{\lambda_j \le \lambda} |\varphi_j(x)|^2 \, dV_g = \sum_{\lambda_j \le \lambda} \int_M |\varphi_j(x)|^2 \, dV_g = \sum_{\lambda_j \le \lambda} 1 = N(\lambda)
$$
对局部[韦尔定律](@entry_id:188635)的主项积分，$\int_M \frac{\omega_n}{(2\pi)^n} \lambda^{n/2} dV_g = \frac{\omega_n \operatorname{Vol}(M)}{(2\pi)^n} \lambda^{n/2}$，我们完美地重现了全局[韦尔定律](@entry_id:188635)的主项。这揭示了全局定律是局部能量[均匀分布](@entry_id:194597)的宏观体现。对于边界点，或者在展开的次阶项中，局部几何（如曲率）和边界条件的影响才会显现出来。