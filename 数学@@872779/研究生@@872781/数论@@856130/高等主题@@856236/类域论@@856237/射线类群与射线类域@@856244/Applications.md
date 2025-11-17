## 应用与跨学科联系

在前面的章节中，我们已经建立了[射线类群](@entry_id:187052)和[射线类域](@entry_id:193459)的核心理论框架。这些概念虽然抽象，但它们为数论研究提供了极其强大的工具，使我们能够解决具体的算术问题，并与其他数学分支建立深刻的联系。本章旨在展示这些理论的应用，说明[射线类群](@entry_id:187052)的构造如何在不同的跨学科背景下发挥其威力。我们将从有理[数域](@entry_id:155558)上的显式[类域论](@entry_id:155687)开始，逐步探讨其如何控制素理想的分解、与[解析数论](@entry_id:158402)的定量结果相结合，并最终触及与[局部域](@entry_id:195717)理论、赫克特征理论以及椭圆曲线[复乘](@entry_id:168088)理论的深刻交汇。

### $\mathbb{Q}$上的显式[类域论](@entry_id:155687)

[类域论](@entry_id:155687)最辉煌的成就之一是在[数域](@entry_id:155558)上具体构造出其所有的[阿贝尔扩张](@entry_id:152984)。对于最基础的[数域](@entry_id:155558)——有理[数域](@entry_id:155558) $\mathbb{Q}$，[类域论](@entry_id:155687)给出了一个完全显式的描述，这本身就是其应用价值的集中体现。

#### 分圆域作为有理[数域](@entry_id:155558)的[射线类域](@entry_id:193459)

对于有理[数域](@entry_id:155558) $\mathbb{Q}$，其任意[阿贝尔扩张](@entry_id:152984)都可以由特定模数的[射线类域](@entry_id:193459)实现。一个根本性的结果，即Kronecker-Weber定理，断言 $\mathbb{Q}$ 的任意有限[阿贝尔扩张](@entry_id:152984)都包含在某个[分圆域](@entry_id:153828) $\mathbb{Q}(\zeta_n)$ 中。事实上，分圆域本身就是 $\mathbb{Q}$ 的[射线类域](@entry_id:193459)。具体而言，对于模 $\mathfrak{m} = n\infty$（其中 $n$ 是正整数，$\infty$ 代表唯一的实位），其对应的[射线类域](@entry_id:193459)正是[分圆域](@entry_id:153828) $\mathbb{Q}(\zeta_n)$。该扩张的伽罗瓦群通过[阿廷互反映射](@entry_id:189274)同构于[射线类群](@entry_id:187052)，即 $\operatorname{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q}) \cong (\mathbb{Z}/n\mathbb{Z})^\times$。这个同构关系是理解分圆域算术性质的基石。例如，著名的斯蒂克伯格定理（Stickelberger's Theorem）利用从伽罗瓦群 $\operatorname{Gal}(\mathbb{Q}(\zeta_n)/\mathbb{Q})$ 构造的斯蒂克伯格元素，给出了分圆域理想类群的显式湮灭子，这直接将伽罗瓦群的结构与类群这一重要的算术[不变量](@entry_id:148850)联系起来。[@problem_id:3027439]

#### 二次域作为[射线类域](@entry_id:193459)

除了分圆域，$\mathbb{Q}$ 的其他[阿贝尔扩张](@entry_id:152984)，如二次扩张，同样可以由[射线类域](@entry_id:193459)理论精确描述。每一个二次域 $K/\mathbb{Q}$ 都与一个唯一的本原二次[狄利克雷特征](@entry_id:151586) $\chi$ 相对应。该特征的导子 $N$ 定义了一个模 $\mathfrak{m} = N\infty$ 或 $\mathfrak{m}=N$（取决于 $\chi$ 的奇偶性）。与该模相关联的[射线类域](@entry_id:193459)包含一个唯一的二次[子域](@entry_id:155812)，这个[子域](@entry_id:155812)正是 $K$。换言之，$K$ 是由特征 $\chi$ 的核在全局[互反律](@entry_id:188215)下所固定的域。[类域论](@entry_id:155687)的一个重要推论是，一个素数 $p$ 在二次域 $K$ 中[分歧](@entry_id:193119)的充要条件是 $p$ 整除其对应[狄利克雷特征](@entry_id:151586)的导子 $N$。对于不[分歧](@entry_id:193119)的素数 $p$，$p$ 在 $K$ 中分裂或保持惯性，则由 $\chi(p)$ 的值决定：$\chi(p)=1$ 意味着 $p$ 分裂，而 $\chi(p)=-1$ 意味着 $p$ 保持惯性。[@problem_id:3021870]

### [希尔伯特类域](@entry_id:193523)与[主理想](@entry_id:152760)定理

[射线类域](@entry_id:193459)理论提供了一个灵活的框架，通过改变模 $\mathfrak{m}$ 来研究不同的[阿贝尔扩张](@entry_id:152984)。其中最简单也最重要的一种情形是取平凡模 $\mathfrak{m}=1$。

#### [理想类群](@entry_id:153974)作为伽罗瓦群

当模 $\mathfrak{m}=1$ 时，[射线类群](@entry_id:187052) $\mathrm{Cl}_1(K)$ 退化为（普通）理想类群 $\mathrm{Cl}(K) = I_K/P_K$。对应的[射线类域](@entry_id:193459) $K_1$ 被称为[希尔伯特类域](@entry_id:193523)，记作 $H$ 或 $H_K$。根据定义，$H_K$ 是 $K$ 的最大处处非分歧的[阿贝尔扩张](@entry_id:152984)。[阿廷互反律](@entry_id:194786)此时给出了一个深刻的同构关系：
$$
\operatorname{Gal}(H/K) \cong \mathrm{Cl}(K)
$$
这个同构将伽罗瓦群——一个描述域扩张对称性的对象——与[理想类群](@entry_id:153974)——一个衡量唯一因子分解失效程度的算术对象——等同起来。这一结果的直接推论是，[希尔伯特类域](@entry_id:193523)的扩张次数等于 $K$ 的[类数](@entry_id:156164)，即 $[H:K] = h_K = |\mathrm{Cl}(K)|$。[@problem_id:3024781]

#### 理想的本原化

[希尔伯特类域](@entry_id:193523)的一个惊人特性是所谓的“主理想定理”（Principal Ideal Theorem 或 Hauptidealsatz）。该定理断言，数域 $K$ 的任何一个理想，不论它在 $K$ 中是否是[主理想](@entry_id:152760)，当它被扩张到[希尔伯特类域](@entry_id:193523) $H$ 中时，都会变成一个主理想。换言之，对于任意 $K$ 的分数理想 $\mathfrak{a}$，其扩张理想 $\mathfrak{a}\mathcal{O}_H$ 都是 $H$ 的一个主理想。从群论的角度看，这意味着由理想扩张诱导的同态（称为投射映射）$j: \mathrm{Cl}(K) \to \mathrm{Cl}(H)$ 是一个零映射，即它将 $\mathrm{Cl}(K)$ 中的每一个元素都映到 $\mathrm{Cl}(H)$ 的单位元上。值得注意的是，这并不意味着 $H$ 本身的[类群](@entry_id:182524)是平凡的（即 $h_H=1$），事实上，$H$ 的[类数](@entry_id:156164)可以大于1，这引出了类[域塔](@entry_id:153606)的概念。[@problem_id:3030529]

### 掌控算术：素理想的分解

[类域论](@entry_id:155687)最强大的应用之一是它能够精确预测素理想在[阿贝尔扩张](@entry_id:152984)中的分解行为。给定一个模 $\mathfrak{m}$，一个未在对应[射线类域](@entry_id:193459) $K_{\mathfrak{m}}$ 中分歧的素理想 $\mathfrak{p}$ 的分解模式完全由其在[射线类群](@entry_id:187052) $\mathrm{Cl}_{\mathfrak{m}}(K)$ 中的位置决定。

根据[阿廷互反律](@entry_id:194786)，[素理想](@entry_id:154026) $\mathfrak{p}$ 在伽罗瓦扩张 $K_{\mathfrak{m}}/K$ 中完全分裂的充要条件是其[弗罗贝尼乌斯元](@entry_id:181102) $(\frac{K_{\mathfrak{m}}/K}{\mathfrak{p}})$ 是伽罗瓦群中的单位元。通过阿廷同构，这等价于 $\mathfrak{p}$ 的类在[射线类群](@entry_id:187052) $\mathrm{Cl}_{\mathfrak{m}}(K)$ 中是单位元。成为单位元意味着 $\mathfrak{p}$ 属于主射线 $P_{\mathfrak{m}}$，即 $\mathfrak{p}$ 必须是一个[主理想](@entry_id:152760) $(\alpha)$，并且其生成元 $\alpha$ 必须满足模 $\mathfrak{m}$ 所规定的全部条件：不仅要满足有限部分 $\mathfrak{m}_0$ 的同余条件（例如 $\alpha \equiv 1 \pmod{\mathfrak{m}_0}$），还要满足无限部分 $\mathfrak{m}_\infty$ 的符号条件（例如，对于 $\mathfrak{m}_\infty$ 中的每个实位 $\sigma$，都有 $\sigma(\alpha)0$）。[@problem_id:3010414]

模的无限部分是不可或缺的。即使一个主[理想的生成元](@entry_id:150082) $\alpha$ 满足了所有的有限[同余](@entry_id:143700)条件，但若其在某个指定的实位上的符号不正确，那么该理想的类在相应的[射线类群](@entry_id:187052)中就不是单位元，从而导致包含此理想的[素理想](@entry_id:154026)在[射线类域](@entry_id:193459)中不会完全分裂。这种对符号条件的精细控制，使得我们能够区分出那些仅靠有限[同余](@entry_id:143700)无法区分的算术行为。例如，通过在模中包含所有的实位，我们可以定义窄[类群](@entry_id:182524)（narrow class group）$\mathrm{Cl}^+(K)$ 及对应的窄[希尔伯特类域](@entry_id:193523) $H_K^+$。该域的伽罗瓦[群同构](@entry_id:147371)于窄类群 $\operatorname{Gal}(H_K^+/K) \cong \mathrm{Cl}^+(K)$，它通常是比（普通）[希尔伯特类域](@entry_id:193523)更大的扩张。[@problem_id:3022494] [@problem_id:3010414]

### 跨学科联系 I：[解析数论](@entry_id:158402)

[类域论](@entry_id:155687)为[解析数论](@entry_id:158402)中的核心定理——[切博塔廖夫密度定理](@entry_id:181202)（Chebotarev Density Theorem）——提供了完美的代数框架，使得我们能够对满足特定分解条件的[素理想](@entry_id:154026)进行计数。

该定理指出，在一个伽罗瓦扩张 $L/K$ 中，对于伽罗瓦群 $\operatorname{Gal}(L/K)$ 的任意一个[共轭类](@entry_id:143916) $C$，那些在 $L$ 中不分歧且其[弗罗贝尼乌斯元](@entry_id:181102)（作为一个共轭类）等于 $C$ 的 $K$ 的[素理想](@entry_id:154026)集合，其狄利克雷密度为 $\frac{|C|}{[L:K]}$。对于[射线类域](@entry_id:193459)这样的[阿贝尔扩张](@entry_id:152984)，伽罗瓦群是[交换群](@entry_id:145145)，因此每个共轭类都只包含一个元素。于是，对于任意给定的伽罗瓦[自同构](@entry_id:155390) $\sigma \in \operatorname{Gal}(K_{\mathfrak{m}}/K)$，其[弗罗贝尼乌斯元](@entry_id:181102)等于 $\sigma$ 的[素理想](@entry_id:154026)[集合的密度](@entry_id:136600)恰好是 $\frac{1}{[K_{\mathfrak{m}}:K]}$。

这使我们能够计算满足特定算术条件的[素理想](@entry_id:154026)的密度。例如，一个素理想在 $K_{\mathfrak{m}}$ 中完全分裂的密度就是 $\frac{1}{[K_{\mathfrak{m}}:K]}$。我们可以利用这个原理计算更复杂的问题。考虑由两个伽罗瓦扩张 $E_1$ 和 $E_2$ 复合而成的域 $L=E_1 E_2$。一个[素理想](@entry_id:154026)在 $L$ 中完全分裂，当且仅当它同时在 $E_1$ 和 $E_2$ 中完全分裂。通过分析 $E_1$ 和 $E_2$ 各自的[分歧素数](@entry_id:183288)，我们可以判断它们的交 $E_1 \cap E_2$ 的大小，进而计算出[复合域](@entry_id:151036)的次数 $[L:K] = \frac{[E_1:K][E_2:K]}{[E_1 \cap E_2:K]}$。这样，素理想在 $L$ 中完全分裂的密度 $\frac{1}{[L:K]}$ 就可以被精确计算出来。[@problem_id:3015319]

更进一步，我们可以计算[弗罗贝尼乌斯元](@entry_id:181102)落在伽罗瓦群的某个[子集](@entry_id:261956)（例如一个[子群](@entry_id:146164)的陪集）中的素理想的密度。这只需要将该[子集](@entry_id:261956)中每个元素的密度（均为 $\frac{1}{[K_{\mathfrak{m}}:K]}$）相加即可。例如，若 $H$ 是 $\operatorname{Gal}(K_{\mathfrak{m}}/K)$ 的一个[指数为2的子群](@entry_id:137534)，那么[弗罗贝尼乌斯元](@entry_id:181102)落在 $H$ 的非平凡[陪集](@entry_id:147145) $C$ 中的素理想密度就是 $\frac{|C|}{[K_{\mathfrak{m}}:K]} = \frac{|H|}{[K_{\mathfrak{m}}:K]} = \frac{1}{2}$。要完成这样的计算，关键在于确定伽罗瓦[群的阶](@entry_id:137115)，也就是[射线类群](@entry_id:187052)的阶，这可以通过标准公式 $h_{\mathfrak{m}} = \frac{h_K \cdot \phi(\mathfrak{m})}{[\mathcal{O}_K^\times : U_{K,\mathfrak{m}}^{(1)}]}$ 计算得出。[@problem_id:3022518]

### 跨学科联系 II：[局部-整体原则](@entry_id:183320)

[全局类域论](@entry_id:188026)的深刻之处在于它与[局部类域论](@entry_id:193658)的完美协调。定义全局[射线类群](@entry_id:187052)的模 $\mathfrak{m}$，其本质上是一系列局部条件的集合，而这些局部条件精确地反映在全局扩张的局部行为上，尤其是[分歧](@entry_id:193119)现象。

#### [分歧](@entry_id:193119)与导子

一个[阿贝尔扩张](@entry_id:152984) $L/K$ 的导子 $\mathfrak{f}(L/K)$ 是使得 $L$ 包含于模 $\mathfrak{f}$ 的[射线类域](@entry_id:193459)中的最小模。导子定理断言，一个素位（有限或无限）在 $L/K$ 中[分歧](@entry_id:193119)的充要条件是它整除导子 $\mathfrak{f}(L/K)$。因此，模的有限部分 $\mathfrak{m}_0$ 的素因子正是那些允许在对应[射线类域](@entry_id:193459)中发生[分歧](@entry_id:193119)的有限[素理想](@entry_id:154026)。[@problem_id:3010414]

#### 局部[互反律](@entry_id:188215)与[分歧](@entry_id:193119)群

[局部类域论](@entry_id:193658)为这种对应关系提供了更为精细的描述。对于 $K$ 的一个素位 $\mathfrak{p}$，扩张 $L/K$ 的局部行为由伽罗瓦群的分解[子群](@entry_id:146164) $D_{\mathfrak{P}} \cong \operatorname{Gal}(L_{\mathfrak{P}}/K_{\mathfrak{p}})$ 描述，其中 $L_{\mathfrak{P}}$ 和 $K_{\mathfrak{p}}$ 是相应的完备化。局部[互反律](@entry_id:188215)给出了一个同构 $\operatorname{rec}_{\mathfrak{p}}: K_{\mathfrak{p}}^\times / N(L_{\mathfrak{P}}^\times) \to \operatorname{Gal}(L_{\mathfrak{P}}/K_{\mathfrak{p}})$。

这个局部映射将[局部域](@entry_id:195717)的算术结构与伽罗瓦群的[分歧](@entry_id:193119)结构联系起来。具体而言，它将局部[单位群](@entry_id:184012) $\mathcal{O}_{\mathfrak{p}}^\times$ 映为惯性[子群](@entry_id:146164) $I_{\mathfrak{P}}$。更精细地，它将[主单位](@entry_id:188721)群的滤链 $U_{\mathfrak{p}}^{(j)} = 1+\mathfrak{p}^j\mathcal{O}_{\mathfrak{p}}$ 映为伽罗瓦群的高阶分歧群（在上标记下）$G_{\mathfrak{P}}^j$。即 $\operatorname{rec}_{\mathfrak{p}}(U_{\mathfrak{p}}^{(j)}) = G_{\mathfrak{P}}^j$。因为模 $\mathfrak{m}$ 在 $\mathfrak{p}$ 处的指数为 $n_{\mathfrak{p}}$ 意味着 $U_{\mathfrak{p}}^{(n_{\mathfrak{p}})}$ 包含在全局阿廷映射的核中，所以 $G_{\mathfrak{P}}^{n_{\mathfrak{p}}}$ 必然是平凡群。这精确地说明了模中的指数如何控制了[分歧](@entry_id:193119)的“深度”。[@problem_id:3022511] 对于[分圆扩张](@entry_id:155116) $\mathbb{Q}(\zeta_{p^n})/\mathbb{Q}$，它是模 $p^n\infty$ 的[射线类域](@entry_id:193459)，在 $p$ 处是[完全分歧的](@entry_id:189971)。其[惯性群](@entry_id:200010)就是整个伽罗瓦群，而[局部类域论](@entry_id:193658)表明这个[惯性群](@entry_id:200010)同构于 $\mathbb{Z}_p^\times / (1+p^n\mathbb{Z}_p)$，这再次印证了局部同余条件如何决定了[分歧](@entry_id:193119)结构。[@problem_id:3020346]

#### 导子-判别式公式

[分歧](@entry_id:193119)与导子的深刻联系最终体现在导子-判别式公式中。对于[阿贝尔扩张](@entry_id:152984) $L/K$，其相对[判别式理想](@entry_id:200833) $\mathfrak{D}_{L/K}$ 完全由其伽罗瓦群的特征 $\chi$ 的阿廷导子 $\mathfrak{f}(\chi)$ 的乘积决定：$\mathfrak{D}_{L/K} = \prod_{\chi} \mathfrak{f}(\chi)$。由于[射线类域](@entry_id:193459)的导子就是其模，这使得我们可以通过模来计算[判别式](@entry_id:174614)。例如，对于分圆域 $\mathbb{Q}(\zeta_n)$，其作为模 $n\infty$ 的[射线类域](@entry_id:193459)，[判别式](@entry_id:174614)可以通过一个涉及 $n$ 和 $\varphi(n)$ 的显式公式计算出来，从而可以比较不同[分圆域的判别式](@entry_id:203102)大小。[@problem_id:3022542]

### 跨学科联系 III：赫克特征与[自守形式](@entry_id:186448)

[射线类群](@entry_id:187052)上的特征（即射线类特征）是有限阶赫克特征（也称格罗森特征）的算术原型，后者在现代数论中，特别是在朗兰兹纲领的框架下，扮演着核心角色。

#### 从射线类特征到赫克特征

一个模为 $\mathfrak{m}$ 的[射线类群](@entry_id:187052) $\mathrm{Cl}_{\mathfrak{m}}(K)$ 是一个[有限阿贝尔群](@entry_id:136632)。其上的一个特征 $\chi: \mathrm{Cl}_{\mathfrak{m}}(K) \to \mathbb{C}^\times$ 是一个有限阶[群同态](@entry_id:140603)。[类域论](@entry_id:155687)的现代语言使用赋值向量环 $\mathbb{A}_K$ 和赋值向量群 $\mathbb{A}_K^\times$ 来表述。在此框架下，[射线类群](@entry_id:187052)同构于一个赋值向量类群的[商群](@entry_id:145113)：$\mathrm{Cl}_{\mathfrak{m}}(K) \cong \mathbb{A}_K^\times / (K^\times U_{\mathfrak{m}})$，其中 $U_{\mathfrak{m}}$ 是由模 $\mathfrak{m}$ 决定的一个开[子群](@entry_id:146164)。任何一个射线类特征 $\chi$ 都可以通过复合典范[商映射](@entry_id:140877) $\pi_{\mathfrak{m}}: \mathbb{A}_K^\times/K^\times \to \mathrm{Cl}_{\mathfrak{m}}(K)$ 被“提升”为一个定义在赋值向量[类群](@entry_id:182524) $\mathbb{A}_K^\times/K^\times$ 上的连续同态 $\tilde{\chi} = \chi \circ \pi_{\mathfrak{m}}$。这个 $\tilde{\chi}$ 就是一个有限阶赫克特征，其导子整除 $\mathfrak{m}$。[@problem_id:3022534]

#### 从赫克特征到伽罗瓦表示

反之，任何一个导子整除 $\mathfrak{m}$ 的有限阶赫克特征 $\chi: \mathbb{A}_K^\times/K^\times \to \mathbb{C}^\times$ 都可被看作一个定义在[射线类群](@entry_id:187052) $\mathrm{Cl}_{\mathfrak{m}}(K)$ 上的特征。通过阿廷互反同构 $\mathrm{Cl}_{\mathfrak{m}}(K) \cong \operatorname{Gal}(K_{\mathfrak{m}}/K)$，这个赫克特征就对应了一个伽罗瓦群 $\operatorname{Gal}(K_{\mathfrak{m}}/K)$ 的[一维表示](@entry_id:136509)（即一个特征）$\rho_\chi$。这个对应关系是典范的，并且满足弗罗贝尼乌斯相容性：对于不整除 $\mathfrak{m}$ 的[素理想](@entry_id:154026) $\mathfrak{p}$，表示 $\rho_\chi$ 在[弗罗贝尼乌斯元](@entry_id:181102) $\mathrm{Frob}_{\mathfrak{p}}$ 上的取值，等于赫克特征 $\chi$ 在对应于 $\mathfrak{p}$ 的赋值向量 $\varpi_{\mathfrak{p}}$ 上的取值。这种赫克特征与一维伽罗瓦表示之间的对偶性是[类域论](@entry_id:155687)的现代表述的核心，也是通向更高维伽罗瓦表示和[自守形式](@entry_id:186448)理论的桥梁。[@problem_id:3022540]

### 跨学科联系 IV：[复乘](@entry_id:168088)（CM）理论

[复乘](@entry_id:168088)理论为[虚二次域](@entry_id:197298)上的显式[类域论](@entry_id:155687)提供了最深刻和最具体的实例。它利用[椭圆曲线](@entry_id:152409)的丰富几何与算术性质来构造[阿贝尔扩张](@entry_id:152984)，其结果与[类域论](@entry_id:155687)的预测完全吻合。

#### 利用[CM椭圆曲线](@entry_id:197957)生成[阿贝尔扩张](@entry_id:152984)

[复乘](@entry_id:168088)理论的[主定理](@entry_id:267632)指出，具有[虚二次域](@entry_id:197298) $K$ 中某个序 $\mathcal{O}$ 作为其[自同态环](@entry_id:185357)的椭圆曲线（称为[CM椭圆曲线](@entry_id:197957)），其 $j$-[不变量](@entry_id:148850) $j(E)$ 是一个[代数整数](@entry_id:151672)，并且 $K(j(E))$ 恰好是对应于序 $\mathcal{O}$ 的环类域。更一般地，将 $j$-[不变量](@entry_id:148850)和[椭圆曲线](@entry_id:152409)上所有 $N$-[挠元](@entry_id:148301)点的坐标添加到 $K$ 中所生成的域，恰好是 $K$ 的某个[射线类域](@entry_id:193459)。这些由[模函数](@entry_id:155728)在CM点上的特殊值所生成的域，为我们提供了构造[阿贝尔扩张](@entry_id:152984)的具体解析工具。

#### [志村互反律](@entry_id:181462)

[志村互反律](@entry_id:181462)（Shimura's Reciprocity Law）精确地描述了这些特殊值上的伽罗瓦作用。它指出，一个赋值向量类 $x \in C_K$ 通过阿廷映射 $\mathrm{Art}_K(x)$ 作用在一个由[模函数](@entry_id:155728) $f$ 在CM点 $\tau$ 的取值 $f(\tau)$ 上，其效果等同于先让一个与 $x$ 关联的矩阵 $g_x \in \mathrm{GL}_2(\widehat{\mathbb{Z}})$ 作用在[模函数](@entry_id:155728) $f$ 自身上得到新函数 $f^{g_x}$，然后再在点 $\tau$ 取值。即：
$$
f(\tau)^{\mathrm{Art}_K(x)} = f^{g_x}(\tau)
$$
这个定律将抽象的伽罗瓦作用（左边）转化为具体的、可在模函数空间上计算的几何作用（右边），从而实现了对伽罗瓦[群作用](@entry_id:268812)的显式计算。[@problem_id:3010306]

#### 一个显式例子

我们可以利用C[M理论](@entry_id:161892)的这一思想来具体计算[阿廷符号](@entry_id:182144)。考虑一个具有CM的[椭圆曲线](@entry_id:152409) $E$，以及一个素理想 $\mathfrak{p}$。[弗罗贝尼乌斯自同态](@entry_id:148155)在 $E$ 的[挠元](@entry_id:148301)点上的作用，可以被显式计算。例如，对于[椭圆曲线](@entry_id:152409) $y^2 = x^3 - 1$，它具有 $\mathbb{Z}[\omega]$（其中 $\omega$ 是本原三次单位根）的[复乘](@entry_id:168088)。对于一个有理素数 $p=13$，其在 $\mathbb{Z}[\omega]$ 中分解为 $\mathfrak{p}\bar{\mathfrak{p}}$。我们可以通过计算 $E$ 在[有限域](@entry_id:142106) $\mathbb{F}_{13}$ 上的点数来确定[弗罗贝尼乌斯迹](@entry_id:197951) $a_{13}$，然后找到 $\mathbb{Z}[\omega]$ 中一个范为 $13$ 且迹为 $a_{13}$ 的元素 $\pi$。这个 $\pi$ 就是[弗罗贝尼乌斯元](@entry_id:181102)。它在 $E$ 的 $f$-[挠元](@entry_id:148301)点上的作用，就是 $\pi \pmod f$ 这个[同余类](@entry_id:635978)的作用。通过计算这个[同余类](@entry_id:635978)，我们就能确定[弗罗贝尼乌斯元](@entry_id:181102)在[挠元](@entry_id:148301)点上的具体作用，从而给出[阿廷符号](@entry_id:182144)的一个具体实现。这完美地展示了[复乘](@entry_id:168088)理论如何将[类域论](@entry_id:155687)从一个存在性理论转变为一个可计算的理论。[@problem_id:3024911]