## 引言
在物理学和工程学中，对自然现象的描述必须是客观的，不应依赖于我们碰巧选择的测量[坐标系](@entry_id:156346)。一个力的作用效果，或一个点上的应力状态，是独立于我们如何架设x-y-z轴的物理现实。为了精确地用数学语言捕捉这种[坐标无关性](@entry_id:159715)，我们需要引入标量、向量以及它们的一般化形式——张量的概念。这些工具不仅仅是方便的记号，它们构成了描述物理世界的基本语法，解决了如何区分真实物理属性和[坐标系](@entry_id:156346)人为效应的根本问题。

本文将系统地引导你穿越[张量分析](@entry_id:161423)的核心地带。在“原理与机制”一章中，我们将从坐标变换这一第一性原理出发，严格定义张量，区分[协变与逆变](@entry_id:189600)分量，并探讨在力学中至关重要的正交变换、[张量不变量](@entry_id:203254)及[主值](@entry_id:189577)问题。随后，在“应用与跨学科联系”一章中，我们将展示这些抽象的原理如何成为表述物理定律（如[本构关系](@entry_id:186508)）的通用语言，并应用于固体力学、[材料科学](@entry_id:152226)甚至广义相对论等多个领域。最后，“动手实践”部分将通过具体的计算问题，让你亲手应用这些理论，将抽象的数学转化为解决实际工程问题的强大工具。

## 原理与机制

在[固体力学](@entry_id:164042)的研究中，物理量（如力、位移、应力、应变）的数学描述必须独立于观察者选择的[坐标系](@entry_id:156346)。一个物理状态的内在属性不应因我们如何度量它而改变。标量、向量和张量的概念为我们提供了精确描述这些与坐标无关的量的框架。本章旨在从第一性原理出发，系统地阐述这些基本概念及其变换规律，并展示它们在描述材料行为中的核心作用。

### 张量的现代定义：变换规律

我们从熟悉的向量概念开始。在几何上，向量是一个具有大小和方向的箭头，一个独立于任何[坐标系](@entry_id:156346)存在的实体。然而，为了进行计算，我们必须在选定的[基矢](@entry_id:199546)（坐标轴）上表示它。例如，向量 $\mathbf{v}$ 可以表示为其分量和[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)，$\mathbf{v} = v^i \mathbf{e}_i$（此处及下文，重复的指标表示根据爱因斯坦求和约定进行求和）。

关键问题是：当[基矢](@entry_id:199546)发生变化时，向量的分量会如何变化？这正是张量定义的核心。

考虑一个从旧[基矢](@entry_id:199546) $\{\mathbf{e}_i\}$ 到新[基矢](@entry_id:199546) $\{\mathbf{e}'_i\}$ 的一般线性变换，其关系可以写为 $\mathbf{e}'_i = P^j{}_i \mathbf{e}_j$，其中 $P^j{}_i$ 是一个可逆的变换矩阵 $\mathbf{P}$ 的元素。由于向量 $\mathbf{v}$ 本身是[几何不变量](@entry_id:178611)，它在新旧[坐标系](@entry_id:156346)下的表示必须相等：
$$ \mathbf{v} = v^j \mathbf{e}_j = v'^i \mathbf{e}'_i $$
将[基矢](@entry_id:199546)的变换关系代入上式，我们得到：
$$ v^j \mathbf{e}_j = v'^i (P^j{}_i \mathbf{e}_j) = (v'^i P^j{}_i) \mathbf{e}_j $$
由于[基矢](@entry_id:199546) $\mathbf{e}_j$ 是线性无关的，两边的系数必须相等，即 $v^j = v'^i P^j{}_i$。为了求解新分量 $v'^i$，我们用 $\mathbf{P}$ 的逆矩阵 $(\mathbf{P}^{-1})^k{}_j$ 乘以上式两边，得到 $v'^k = (\mathbf{P}^{-1})^k{}_j v^j$。

这种“逆着”[基矢](@entry_id:199546)变换矩阵 $\mathbf{P}$ 进行变换的分量，被称为**[逆变分量](@entry_id:185440) (contravariant components)**。按照惯例，[逆变分量](@entry_id:185440)的指标写在上标位置，如 $v^i$。

现在，我们引入[向量空间](@entry_id:151108)的**对偶空间 (dual space)** $V^*$。[对偶空间](@entry_id:146945)由作用于原[向量空间](@entry_id:151108) $V$ 的所有线性函数（称为**协向量 (covectors)** 或[对偶向量](@entry_id:161217)）构成。对于每个[基矢](@entry_id:199546) $\{\mathbf{e}_i\}$，都存在一个唯一的对偶[基矢](@entry_id:199546) $\{\mathbf{e}^i\}$，其定义满足关系 $\mathbf{e}^i(\mathbf{e}_j) = \delta^i_j$，其中 $\delta^i_j$ 是克罗内克符号。

可以证明，当[基矢](@entry_id:199546)按 $\mathbf{e}'_i = P^j{}_i \mathbf{e}_j$ 变换时，对偶[基矢](@entry_id:199546)的变换规律为 $\mathbf{e}'^i = (\mathbf{P}^{-1})^i{}_j \mathbf{e}^j$。一个协向量 $\mathbf{w}$ 同样是[几何不变量](@entry_id:178611)，$\mathbf{w} = w_j \mathbf{e}^j = w'_i \mathbf{e}'^i$。通过类似的推导，可以得到其分量的变换规律：$w'_i = P^j{}_i w_j$。

这种“随着”[基矢](@entry_id:199546)变换矩阵 $\mathbf{P}$ 进行变换的分量，被称为**[协变](@entry_id:634097)分量 (covariant components)**，其指标写在下标位置，如 $w_i$ [@problem_id:2683613]。梯度就是一个典型的[协变向量](@entry_id:263917)。

这个概念可以推广到更高阶的张量。从最根本的数学角度看，一个 $(r,s)$ 型张量 $\mathbf{T}$ 是一个[多重线性映射](@entry_id:274221)，它将 $r$ 个协向量和 $s$ 个向量映射到一个标量（实数）[@problem_id:2683613]：
$$ \mathbf{T}: \underbrace{V^* \times \dots \times V^*}_{r \text{ times}} \times \underbrace{V \times \dots \times V}_{s \text{ times}} \to \mathbb{R} $$
其分量 $T^{i_1 \dots i_r}{}_{j_1 \dots j_s}$ 是通过将张量作用于相应的[基矢](@entry_id:199546)和对偶[基矢](@entry_id:199546)得到的。基于这一定义，可以推导出 $(r,s)$ 型张量分量的一般变换规律：
$$ T'^{i_1 \dots i_r}{}_{j_1 \dots j_s} = (\mathbf{P}^{-1})^{i_1}{}_{a_1} \dots (\mathbf{P}^{-1})^{i_r}{}_{a_r} P^{b_1}{}_{j_1} \dots P^{b_s}{}_{j_s} T^{a_1 \dots a_r}{}_{b_1 \dots b_s} $$
这个公式是[张量分析](@entry_id:161423)的基石。它表明，一个张量的分量变换规律由其类型 $(r,s)$ 唯一确定：每个[逆变](@entry_id:192290)指标（上标）都伴随着一个逆[变换矩阵](@entry_id:151616) $\mathbf{P}^{-1}$，而每个[协变](@entry_id:634097)指标（下标）都伴随着一个原[变换矩阵](@entry_id:151616) $\mathbf{P}$。一个标量是 $(0,0)$ 型张量，它没有指标，因此其值在任何坐标变换下都保持不变。

### [欧几里得空间](@entry_id:138052)中的张量：正交变换

在固体力学中，我们通常处理的是欧几里得空间，并使用**标准正交基矢 (orthonormal bases)**。在这种特殊情况下，从一个[标准正交基](@entry_id:147779) $\{\mathbf{e}_i\}$ 到另一个[标准正交基](@entry_id:147779) $\{\mathbf{e}'_i\}$ 的变换由一个**[正交矩阵](@entry_id:169220) (orthogonal matrix)** $\mathbf{Q}$ 描述。正交矩阵最重要的特性是其[逆矩阵](@entry_id:140380)等于其转置矩阵，即 $\mathbf{Q}^{-1} = \mathbf{Q}^T$。此外，如果两个基都保持相同的“手性”（例如，都是[右手系](@entry_id:166669)），则该变换是一个纯旋转，且 $\det(\mathbf{Q}) = +1$。

在正交变换下，张量的变换规律得到简化。由于 $\mathbf{P} = \mathbf{Q}^T$（若定义 $\mathbf{e}'_i=Q_{ji}\mathbf{e}_j$）且 $\mathbf{P}^{-1} = \mathbf{Q}$, [逆变和协变分量](@entry_id:268728)的变换分别由 $\mathbf{Q}$ 和 $\mathbf{Q}^T$ 决定。然而，在工程应用中，更常见的做法是直接定义[变换矩阵](@entry_id:151616) $Q_{ij} = \mathbf{e}'_i \cdot \mathbf{e}_j$，这样向量分量的变换就可以统一写为矩阵形式 $[\mathbf{v}'] = \mathbf{Q}[\mathbf{v}]$ [@problem_id:2683609]。

对于二阶张量 $\mathbf{T}$（如应力或[应变张量](@entry_id:193332)），其分量的变换规律为：
$$ T'_{ij} = Q_{ip} Q_{jq} T_{pq} $$
这在矩阵形式下等价于一个非常重要的关系式——**相似变换 (similarity transformation)**：
$$ [\mathbf{T}'] = \mathbf{Q} [\mathbf{T}] \mathbf{Q}^T $$
这个变换规律保证了张量的内在物理属性与[坐标系](@entry_id:156346)无关。例如，对称性就是一个内在属性。如果一个二阶张量 $\mathbf{S}$ 在一个[坐标系](@entry_id:156346)中是对称的，即 $[\mathbf{S}] = [\mathbf{S}]^T$，那么在任何旋转后的新[坐标系](@entry_id:156346)中，它仍然是对称的。我们可以通过对变换公式取[转置](@entry_id:142115)来证明这一点：
$$ [\mathbf{S}']^T = (\mathbf{Q} [\mathbf{S}] \mathbf{Q}^T)^T = (\mathbf{Q}^T)^T [\mathbf{S}]^T \mathbf{Q}^T = \mathbf{Q} [\mathbf{S}] \mathbf{Q}^T = [\mathbf{S}'] $$
这表明对称性是张量固有的、坐标无关的性质 [@problem_id:2683609]。

### [标量不变量](@entry_id:193787)：与旋转无关的量

在物理上，最有意义的量往往是在[坐标旋转](@entry_id:164444)下保持不变的**[标量不变量](@entry_id:193787) (scalar invariants)**。它们捕捉了张量所描述的物理状态的内在特征，而不依赖于观察者的视角。

最基本的[不变量](@entry_id:148850)是向量的欧几里得范数（或其平方），即向量的长度。如果向量分量在旋转下变换为 $[\mathbf{v}'] = \mathbf{Q}[\mathbf{v}]$，其范数的平方变换为：
$$ \|\mathbf{v}'\|^2 = [\mathbf{v}']^T [\mathbf{v}'] = (\mathbf{Q}[\mathbf{v}])^T (\mathbf{Q}[\mathbf{v}]) = [\mathbf{v}]^T \mathbf{Q}^T \mathbf{Q} [\mathbf{v}] $$
由于 $\mathbf{Q}$ 是正交矩阵，$\mathbf{Q}^T \mathbf{Q} = \mathbf{I}$（单位矩阵），因此：
$$ \|\mathbf{v}'\|^2 = [\mathbf{v}]^T \mathbf{I} [\mathbf{v}] = [\mathbf{v}]^T [\mathbf{v}] = \|\mathbf{v}\|^2 $$
这从第一性原理证明了向量的长度在旋转下是不变的 [@problem_id:2683629]。

对于二阶张量 $\mathbf{T}$，也存在一组不随[坐标旋转](@entry_id:164444)而改变的标量，称为**[主不变量](@entry_id:193522) (principal invariants)**。其中最常用的是**迹 (trace)** 和**[行列式](@entry_id:142978) (determinant)**。迹的[不变性](@entry_id:140168)可以利用[矩阵乘法](@entry_id:156035)[迹的循环性质](@entry_id:153103)（$\mathrm{tr}(\mathbf{ABC}) = \mathrm{tr}(\mathbf{BCA})$）轻松证明：
$$ \mathrm{tr}([\mathbf{T}']) = \mathrm{tr}(\mathbf{Q}[\mathbf{T}]\mathbf{Q}^T) = \mathrm{tr}([\mathbf{T}]\mathbf{Q}^T\mathbf{Q}) = \mathrm{tr}([\mathbf{T}]\mathbf{I}) = \mathrm{tr}([\mathbf{T}]) $$
这一性质在连续介质力学中至关重要。例如，对于柯西应力张量 $\boldsymbol{\sigma}$，其迹的一阶[不变量](@entry_id:148850) $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$ 与材料的体积变化紧密相关。我们定义**[静水压力](@entry_id:275365) (hydrostatic pressure)** 为 $p = -\frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$。由于迹是[标量不变量](@entry_id:193787)，静水压力也是一个不依赖于[坐标系](@entry_id:156346)选择的物理量 [@problem_id:2683634]。

为了区分引起体积变化和形状变化（剪切）的应力部分，通常将应力张量分解为球量部分和偏量部分。**应力[偏张量](@entry_id:185837) (stress deviator tensor)** 定义为 $\mathbf{s} = \boldsymbol{\sigma} + p\mathbf{I} = \boldsymbol{\sigma} - \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})\mathbf{I}$。可以轻易验证，应力偏[张量的迹](@entry_id:190669)恒为零。

描述[材料屈服](@entry_id:751736)和塑性行为的理论（如 von Mises 屈服准则）依赖于应力[偏张量](@entry_id:185837)的[不变量](@entry_id:148850)。其中最重要的是第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$，它与 von Mises [等效应力](@entry_id:749064) $\sigma_{\mathrm{vM}}$ 直接相关：
$$ J_2 = \frac{1}{2} \mathbf{s}:\mathbf{s} = \frac{1}{2} \mathrm{tr}(\mathbf{s}^2) \quad \text{and} \quad \sigma_{\mathrm{vM}} = \sqrt{3J_2} $$
其中“:”表示张量的[双点积](@entry_id:748648)。我们可以证明 $\mathbf{s}:\mathbf{s}$ 是一个[标量不变量](@entry_id:193787)。因为 $\mathbf{s}$ 的变换规律与 $\boldsymbol{\sigma}$ 相同，即 $[\mathbf{s}'] = \mathbf{Q}[\mathbf{s}]\mathbf{Q}^T$，所以：
$$ \mathbf{s}':\mathbf{s}' = \mathrm{tr}([\mathbf{s}']^T[\mathbf{s}']) = \mathrm{tr}((\mathbf{Q}[\mathbf{s}]\mathbf{Q}^T)^T (\mathbf{Q}[\mathbf{s}]\mathbf{Q}^T)) = \mathrm{tr}(\mathbf{Q}[\mathbf{s}]^T\mathbf{Q}^T \mathbf{Q}[\mathbf{s}]\mathbf{Q}^T) = \mathrm{tr}(\mathbf{Q}[\mathbf{s}]^T[\mathbf{s}]\mathbf{Q}^T) = \mathrm{tr}([\mathbf{s}]^T[\mathbf{s}]) = \mathbf{s}:\mathbf{s} $$
因此，$J_2$ 和 $\sigma_{\mathrm{vM}}$ 都是客观的物理量，它们表征了材料内部的[剪切应力](@entry_id:137139)状态，而与我们如何设置[坐标系](@entry_id:156346)无关 [@problem_id:2683634]。

### 主值与[主方向](@entry_id:276187)：一个特殊的基

尽管[张量不变量](@entry_id:203254)为了解其内在属性提供了便捷途径，但有时我们希望找到一个最能简化张量描述的特殊[坐标系](@entry_id:156346)。对于对称的二阶张量（如应力张量 $\boldsymbol{\sigma}$ 或[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$），这个特殊的[坐标系](@entry_id:156346)由其**[主方向](@entry_id:276187) (principal directions)** 构成。

在物理上，[主方向](@entry_id:276187)是指应力张量作用在该方向上只产生纯拉伸或压缩而没有剪切的方向。数学上，这是一个本征值问题 (eigenvalue problem)：
$$ \boldsymbol{\sigma} \mathbf{n} = \sigma_p \mathbf{n} $$
其中，标量 $\sigma_p$ 是**[主应力](@entry_id:176761) (principal stress)**，即[本征值](@entry_id:154894)；向量 $\mathbf{n}$ 是对应的主方向，即[本征向量](@entry_id:151813) [@problem_id:2683612]。对于三维空间中的对称[二阶张量](@entry_id:199780)，总可以找到三个实数主应力，以及一组相互正交的[主方向](@entry_id:276187)。

如果我们选择这组标准正交的[主方向](@entry_id:276187)作为新的[坐标基](@entry_id:270149)，那么在该[坐标系](@entry_id:156346)下，[应力张量](@entry_id:148973)的[矩阵表示](@entry_id:146025)将变成一个[对角矩阵](@entry_id:637782)，其对角[线元](@entry_id:196833)素就是三个[主应力](@entry_id:176761)：
$$ [\boldsymbol{\sigma}'] = \begin{pmatrix} \sigma_1 & 0 & 0 \\ 0 & \sigma_2 & 0 \\ 0 & 0 & \sigma_3 \end{pmatrix} $$
将原始[坐标系](@entry_id:156346)下的应力张量变换到[主方向](@entry_id:276187)[坐标系](@entry_id:156346)的[变换矩阵](@entry_id:151616) $\mathbf{Q}$，正是由[标准化](@entry_id:637219)的主[方向向量](@entry_id:169562)作为其列向量构成的。根据二阶张量的[相似变换](@entry_id:152935)法则，我们有 $[\boldsymbol{\sigma}'] = \mathbf{Q}^T[\boldsymbol{\sigma}]\mathbf{Q}$（假设 $\mathbf{Q}$ 的列是主方向）。这个过程称为张量的**[对角化](@entry_id:147016)**，它极大地简化了对复杂应力状态的分析 [@problem_id:2683612]。

### [高阶张量](@entry_id:200122)及其在力学中的映射

许多物理关系，尤其是材料的[本构关系](@entry_id:186508)，需要用到更高阶的张量。例如，在线[弹性理论](@entry_id:184142)中，（二阶）应力张量 $\boldsymbol{\sigma}$ 与（二阶）[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 之间的线性关系由一个四阶的**[弹性张量](@entry_id:170728) (elasticity tensor)** $\mathbf{C}$ 描述：
$$ \sigma_{ij} = C_{ijkl} \varepsilon_{kl} $$
这个[四阶张量](@entry_id:181350) $\mathbf{C}$ 本身也必须遵循[张量变换法则](@entry_id:185176)。根据物理定律形式不变的[客观性原理](@entry_id:185412)，[本构关系](@entry_id:186508)在旋转后的[坐标系](@entry_id:156346)中必须具有完全相同的形式：$\sigma'_{ij} = C'_{ijkl} \varepsilon'_{kl}$。结合二阶张量的变换规律 $\sigma'_{ij} = Q_{ip}Q_{jq}\sigma_{pq}$ 和 $\varepsilon'_{kl} = Q_{kr}Q_{ls}\varepsilon_{rs}$，可以推导出[四阶张量](@entry_id:181350) $\mathbf{C}$ 的变换规律为 [@problem_id:2683603]：
$$ C'_{ijkl} = Q_{ip} Q_{jq} Q_{kr} Q_{ls} C_{pqrs} $$
每个指标都受到一次正交变换。

材料的对称性直接体现在其[弹性张量](@entry_id:170728) $\mathbf{C}$ 的性质上。如果一种材料是**各向同性 (isotropic)** 的，意味着其物理性质在所有方向上都相同。数学上，这表示其[弹性张量](@entry_id:170728) $\mathbf{C}$ 在任意[坐标旋转](@entry_id:164444)下都保持不变，即 $C'_{ijkl} = C_{ijkl}$。对于[各向同性线弹性](@entry_id:185899)材料，其81个分量的[弹性张量](@entry_id:170728)可以被简化，仅由两个独立的材料常数——拉梅参数 $\lambda$ 和 $\mu$——完全确定 [@problem_id:2683605]：
$$ C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk}) $$

在处理大变形问题时，张量也扮演着连接不同构形（configuration）的角色。**变形梯度 (deformation gradient)** $\mathbf{F}$ 是一个关键的二阶张量，它是一个**两点张量 (two-point tensor)**，因为它将变形前参考构形中的[切向量](@entry_id:265494) $d\mathbf{X}$ 映射到变形后当前构形中的切向量 $d\mathbf{x}$：$d\mathbf{x} = \mathbf{F} d\mathbf{X}$。这个操作称为**推前 (push-forward)** [@problem_id:2683623]。

相应地，也存在将当前构形中的量“[拉回](@entry_id:160816)”到参考构形的操作。协向量的**[拉回](@entry_id:160816) (pull-back)** 遵循不同的变换法则。如果一个空间协向量场为 $\boldsymbol{\alpha}$，其[拉回](@entry_id:160816)到材料构形中的协向量场 $\mathbf{A}$ 由 $A_I = \alpha_i F^i_I$ 或 $[\mathbf{A}] = \mathbf{F}^T[\boldsymbol{\alpha}]$ 定义。推前和[拉回](@entry_id:160816)操作的定义保证了向量与协向量的作用（对偶[内积](@entry_id:158127)）在不同构形间的[不变性](@entry_id:140168)，即 $\boldsymbol{\alpha}(\mathbf{v}) = \mathbf{A}(\mathbf{V})$，这是皮奥拉恒等式 (Piola's identity) 的体现 [@problem_id:2683623]。[标量场的梯度](@entry_id:270765)作为一个协向量场，其在不同构形间的变换也遵循协向量的[拉回](@entry_id:160816)法则。

### [曲线坐标系](@entry_id:172561)中的张量

尽管笛卡尔坐标系在理论推导中很方便，但许多实际问题（如圆柱壳或球形[压力容器](@entry_id:191906)）具有几何上的对称性，使用**[曲线坐标系](@entry_id:172561) (curvilinear coordinates)**（如[柱坐标](@entry_id:271645)或球坐标）会更加自然。然而，这也引入了一些新的复杂性。

在[曲线坐标系](@entry_id:172561)中，我们必须区分两种[基矢](@entry_id:199546)。**[协变基](@entry_id:198968)矢 (covariant basis vectors)** $\mathbf{e}_i$ 定义为沿坐标线 $x^i$ 的[切线](@entry_id:268870)方向，$\mathbf{e}_i = \partial\mathbf{x}/\partial x^i$。通常情况下，这些[基矢](@entry_id:199546)既非单位长度，也非相互正交。它们的[内积](@entry_id:158127)定义了**[度规张量](@entry_id:160222) (metric tensor)** 的协变分量 $g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j$。度规张量包含了[曲线坐标系](@entry_id:172561)局部几何的所有信息，例如，空间中微小线段的长度平方为 $ds^2 = g_{ij} dx^i dx^j$。

以[柱坐标](@entry_id:271645) $(r, \theta, z)$ 为例，其度规张量是 $g_{ij} = \mathrm{diag}(1, r^2, 1)$。这意味着 $\mathbf{e}_r$ 和 $\mathbf{e}_z$ 是[单位向量](@entry_id:165907)，而 $\mathbf{e}_\theta$ 的长度为 $r$ [@problem_id:2683614]。

由于[协变基](@entry_id:198968)矢通常不正交，一个向量 $\mathbf{v}$ 的分量表示也变得更加微妙。我们可以将其表示为[协变基](@entry_id:198968)矢的[线性组合](@entry_id:154743)，$\mathbf{v} = v^i \mathbf{e}_i$，这里的 $v^i$ 是**[逆变分量](@entry_id:185440)**。我们也可以用对偶[基矢](@entry_id:199546) $\mathbf{e}^i$ 来表示，$\mathbf{v} = v_i \mathbf{e}^i$，这里的 $v_i$ 是**协变分量**。度规张量正是连接这两种分量的桥梁：$v_i = g_{ij} v^j$ 和 $v^i = g^{ij} v_j$，其中 $g^{ij}$ 是[度规张量](@entry_id:160222)的逆。

在工程实践中，我们更关心的是**物理分量 (physical components)**，即向量在与坐标线相切的局部*标准正交*基 $\hat{\mathbf{e}}_i$ 上的投影。对于[正交坐标](@entry_id:166074)系，[协变基](@entry_id:198968)矢和物理[基矢](@entry_id:199546)的关系很简单：$\mathbf{e}_i = \sqrt{g_{ii}} \hat{\mathbf{e}}_i$（无求和）。这使得我们可以在物理分量与张量分量（协变/[逆变](@entry_id:192290)）之间建立明确的换算关系 [@problem_id:2683614]。

在[曲线坐标系](@entry_id:172561)中对[张量场](@entry_id:190170)进行[微分](@entry_id:158718)时，我们不能再使用简单的偏导数，因为[基矢](@entry_id:199546)本身会随空间位置的变化而变化。为了正确地描述[张量场](@entry_id:190170)的变化率，必须引入**协变导数 (covariant derivative)** $\nabla_j$。协变导数在普通偏导数的基础上增加了一项，用以修正[基矢](@entry_id:199546)变化带来的影响。这一修正项由**克氏符 (Christoffel symbols)** $\Gamma^k_{ij}$ 给出，它完全由度规张量及其导数决定。

例如，一个混合二阶张量 $\sigma^j{}_i$ 的[协变导数](@entry_id:152476)为：
$$ \nabla_k \sigma^j{}_i = \frac{\partial \sigma^j{}_i}{\partial x^k} + \Gamma^j_{kl} \sigma^l{}_i - \Gamma^l_{ki} \sigma^j{}_l $$
通过对指标进行缩并，我们可以得到张量的**[协变散度](@entry_id:275039) (covariant divergence)**，这在力[平衡方程](@entry_id:172166)中至关重要。例如，应力[张量的散度](@entry_id:191736)表示单位体积内的体力，其第 $i$ 个分量为 $f_i = \nabla_j \sigma^j{}_i$ [@problem_id:2683607]。

考虑一个各向同性应[力场](@entry_id:147325) $\sigma_{ij} = p(r) g_{ij}$ 的例子，在球坐标中，其混合形式为 $\sigma^j{}_i = p(r) \delta^j_i$。代入[协变散度](@entry_id:275039)的公式，经过计算会发现，包含克氏符的项会精确地相互抵消，最终得到一个极其简洁和直观的结果 [@problem_id:2683607]：
$$ f_i = \frac{\partial p(r)}{\partial x^i} $$
这表明，在这种情况下，单位体积内的[体力](@entry_id:174230)就是压[力场](@entry_id:147325) $p(r)$ 的梯度。这个例子完美地展示了[张量微积分](@entry_id:161423)这套看似复杂的工具如何揭示了深刻而简单的物理现实，并验证了其理论框架的自洽性与强大功能。