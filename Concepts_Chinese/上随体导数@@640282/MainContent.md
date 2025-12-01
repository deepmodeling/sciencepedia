## 引言
为了理解和预测[聚合物熔体](@entry_id:192068)或生物流体等复杂材料的行为，我们必须使用连续介质力学的语言。该领域的一个核心挑战在于，如何描述在一个不断流动、拉伸和翻滚的系统中材料属性的变化。标准的时间导数通常是不够的，因为它们可能被简单的旋转所“欺骗”，这违反了“自然法则不应依赖于观察者[参考系](@entry_id:169232)”这一基本物理原理。本文通过引入客观时间变化率的概念来填补这一知识空白。在接下来的章节中，您将了解客观导数背后的核心原理，并看到它们是如何构建的。文章最后将探讨其中最重要的导数之一——上[随体导数](@entry_id:204621)，如何成为模拟和理解[复杂流体](@entry_id:198415)真实世界行为的一把万能钥匙。

## 原理与机制

要真正理解[聚合物熔体](@entry_id:192068)、面包面团，乃至地球地幔等材料奇异而奇妙的世界，我们必须学会它们的语言。这就是[连续介质力学](@entry_id:155125)的语言，一种思考物质如何流动、拉伸和变形的方式。我们的核心挑战是在一个不断运动的世界中测量变化。当我们的实验室——材料本身——正在空间中流动和翻滚时，我们如何建立物理定律？

### 观察者问题：为什么你的手表是骗子

想象一下，你是一位科学家，坐在一只小筏上[顺流](@entry_id:149122)而下。你的工作是测量[水的性质](@entry_id:137983)，比如某个内部应力张量，我们称之为 $\boldsymbol{T}$。最自然的做法是将探测器放入筏旁的水中，观察仪表读数随时间的变化。你测量的是*跟随水体*时的变化。这种跟随一个物[质点](@entry_id:186768)的变化率，数学家称之为**物质导数**，记作 $\frac{D\boldsymbol{T}}{Dt}$。它是在一个固定位置发生的变化 ($\frac{\partial \boldsymbol{T}}{\partial t}$) 和由于你被带到一个具有不同 $\boldsymbol{T}$ 值的新位置而引起的变化（[对流](@entry_id:141806)项 $\boldsymbol{u}\cdot\nabla\boldsymbol{T}$）的总和 [@problem_id:3388261]。

现在，假设你的朋友在河岸上一个巨大的旋转木马上观察你。他们也用探测器测量你正在追踪的同一个[水质](@entry_id:180499)点的应力张量。他们测量的*变化率*应该和你的测量结果一致吗？根据物理学的一条基本原则——**物质[坐标无关性](@entry_id:159715)原理**（或**[客观性原理](@entry_id:185412)**），答案必须是肯定的。物理定律不能依赖于观察者的任意旋转或运动。

问题就在这里：简单的[物质导数](@entry_id:172646)不具有客观性 [@problem_id:3388261] [@problem_id:2905932]。如果一块果冻只是像陀螺一样刚性旋转，其内部状态在任何有意义的物理层面上都没有改变。然而，固定在实验室里的观察者会看到[应力张量](@entry_id:148973)的方向在变化，[物质导数](@entry_id:172646) $\frac{D\boldsymbol{T}}{Dt}$ 将不为零。物质导数是一个“骗子”；它将材料的简单旋转与内部真正的物理变化混为一谈。为了写出有意义的本构律——即支配材料行为的规则——我们需要一个“诚实”的“时间导数”，一个**客观时间变化率**。我们需要一个不会被旋转所迷惑的时钟。

### 两种运动的故事：[拉伸与旋转](@entry_id:150197)

要制造一个诚实的时钟，我们必须首先理解运动的本质。任何复杂的[流体运动](@entry_id:182721)，当你观察一个无穷小的邻域时，都是平移、旋转和变形的组合。描述这种局部运动的关键是**[速度梯度张量](@entry_id:270928)** $\boldsymbol{L} = \nabla\boldsymbol{u}$。这个张量是一本紧凑的字典，告诉我们速度如何从一点变化到相邻一点。

这里真正的美妙之处在于，我们可以将任何矩阵，包括 $\boldsymbol{L}$，分解为一个对称[部分和](@entry_id:162077)一个反对称部分。对于[速度梯度](@entry_id:261686)，这种分解揭示了[流体运动](@entry_id:182721)的两个基本特征 [@problem_id:3388285] [@problem_id:554275]：

$\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$

这里，$\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathrm{T}})$ 是对称部分，称为**[形变率张量](@entry_id:184787)**。它描述了一个小流体单元如何被拉伸、挤压或剪切。这是改变单元形状的运动部分。

另一部分，$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathrm{T}})$，是反对称部分，称为**自旋**或**[涡量张量](@entry_id:189621)**。它描述了流体单元如何像陀螺一样进行刚体旋转，而形状没有任何改变。

这个简单的数学分解意义深远。它告诉我们，任何局部流体运动都可以看作是纯拉伸/剪切和纯旋转的叠加。有了这一洞见，我们现在就有了修正我们那个说谎的时钟的工具。

### 构建一个诚实的时钟：客观导数

对“诚实”导数的第一次尝试可能是简单地减去由[流体旋转](@entry_id:273789)引起的表观变化。这就得到了**Jaumann导数**（或[共旋导数](@entry_id:203813)）：

$\overset{\circ}{\boldsymbol{T}} = \frac{D\boldsymbol{T}}{Dt} - (\boldsymbol{W}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{W})$

我们减去的这一项 $\boldsymbol{W}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{W}$，正是一个张量如果仅仅以 $\boldsymbol{W}$ 给定的自旋速率随流体被动旋转时所具有的变化率 [@problem_id:554275]。所以，Jaumann导数是从一个与流体单元一同旋转的观察者的角度来测量 $\boldsymbol{T}$ 的变化率。它成功地忽略了刚体旋转，并且确实是一个客观变化率 [@problem_id:2886962]。它比物质导数是一个诚实得多的时钟。但这是否就是全部呢？由 $\boldsymbol{D}$ 描述的拉伸又该如何处理？

### 上[随体导数](@entry_id:204621)：运动学的杰作

对于许多物理量，特别是那些与材料自身结构相关的量，即使是纯拉伸引起的变化也是一种我们希望忽略的“平凡”[对流](@entry_id:141806)。我们希望找到真正内禀于材料响应的变化率，剥离所有由宏观流动产生的影响。这就引出了我们故事的主角：**上[随体导数](@entry_id:204621)**。

乍一看，它的定义有点吓人：

$\overset{\triangledown}{\boldsymbol{T}} = \frac{D\boldsymbol{T}}{Dt} - \boldsymbol{L}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{L}^{\mathrm{T}}$

但让我们来解析它的含义。首先，我们可以使用我们的分解 $\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}$。一点代数运算揭示了一个非凡的结果 [@problem_id:3388285] [@problem_id:554275]：

$\overset{\triangledown}{\boldsymbol{T}} = \left( \frac{D\boldsymbol{T}}{Dt} - (\boldsymbol{W}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{W}) \right) - (\boldsymbol{D}\boldsymbol{T} + \boldsymbol{T}\boldsymbol{D})$

仔细看！括号中的第一部分正是 Jaumann 导数。上[随体导数](@entry_id:204621)做了 Jaumann 导数所做的事情——它减去了旋转——但它做得更多。它*还*减去了 $\boldsymbol{D}\boldsymbol{T} + \boldsymbol{T}\boldsymbol{D}$ 这一项，该项代表了仅仅因为定义张量的物质线被流动拉伸和剪切而发生的变化率。它是一个客观变化率，对于任何可压缩或不可压缩的运动都被证明是如此 [@problem_id:2905932] [@problem_id:2886962]。它回答了这样一个问题：“$\boldsymbol{T}$ 的变化率中，*不*因于物质单元被流动被动地旋转和拉伸的部分是多少？”

还有另一种可能更直观的方式来看待这个问题 [@problem_id:525293]。想象在时间 $t$ 时，流体上画了一张网。片刻之后，在 $t + \Delta t$ 时，流体已经流动，我们的网现在变形并处于一个新的位置。上[随体导数](@entry_id:204621)是一个概念性实验的结果：取在较晚时刻的变形网上测量的张量 $\boldsymbol{T}$，在数学上将其沿着流动路径“[拉回](@entry_id:160816)”并“反拉伸”，使网的形状与时间 $t$ 时相同，然后计算张量变化了多少。这个“[拉回](@entry_id:160816)”操作正是由 $-\boldsymbol{L}\boldsymbol{T} - \boldsymbol{T}\boldsymbol{L}^{\mathrm{T}}$ 这两项完成的。它是在一个与材料一同*随动*和*变形*的[坐标系](@entry_id:156346)中的导数。

### 禅意时刻：消失的导数

当我们用上[随体导数](@entry_id:204621)来测量一个非常特殊的张量的变化时，它的真正力量和优雅就显现出来了：**左 Cauchy-Green [应变张量](@entry_id:193332)** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathrm{T}}$。这个由变形梯度 $\boldsymbol{F}$ 构成的张量，是衡量材料从某个参考状态所经历的总有限变形的基本度量。它基本上承载了所有已发生的拉伸历史。

现在，让我们问一个简单的运动学问题：$\boldsymbol{B}$ 如何随时间变化？通过微积分和运动学法则，可以推导出一个优美而精确的恒等式 [@problem_id:522143]：

$\frac{D\boldsymbol{B}}{Dt} = \boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathrm{T}}$

这个方程告诉我们应变历史的物质导数如何与当前的速度梯度相关联。现在是见证奇迹的时刻。让我们计算 $\boldsymbol{B}$ 的上[随体导数](@entry_id:204621)：

$\overset{\triangledown}{\boldsymbol{B}} = \frac{D\boldsymbol{B}}{Dt} - \boldsymbol{L}\boldsymbol{B} - \boldsymbol{B}\boldsymbol{L}^{\mathrm{T}}$

将我们的恒等式代入这个定义，我们发现：

$\overset{\triangledown}{\boldsymbol{B}} = (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathrm{T}}) - (\boldsymbol{L}\boldsymbol{B} + \boldsymbol{B}\boldsymbol{L}^{\mathrm{T}}) = \boldsymbol{0}$

结果是零。恒为零。这是一个力学上的禅意时刻。左 Cauchy-Green [应变张量](@entry_id:193332)的上[随体导数](@entry_id:204621)恒等于零。这告诉我们，从上[随体导数](@entry_id:204621)的特殊视角来看，有限应变张量 $\boldsymbol{B}$ 根本没有变化。它纯粹地被流动所[对流](@entry_id:141806)，而这种[对流](@entry_id:141806)方式正是该导数被设计来忽略的。这证实了我们的直觉：上[随体导数](@entry_id:204621)是与材料变形结构内禀地交织在一起的物理量的自然变化率。

### 观察者家族

上[随体导数](@entry_id:204621)是一整个客观变化率家族中的一个关键成员。它的“对偶”是**下[随体导数](@entry_id:204621)**，由 $\overset{\triangle}{\boldsymbol{A}} = \frac{D\boldsymbol{A}}{Dt} + \boldsymbol{L}^{\mathrm{T}}\boldsymbol{A} + \boldsymbol{A}\boldsymbol{L}$ 给出。这个变化率天然适用于描述[协变张量](@entry_id:634493)（其变换方式与像 $\boldsymbol{B}$ 这样的[逆变张量](@entry_id:636697)不同）的演化 [@problem_id:555686]。其他的变化率，如 **Truesdell 变化率**，也是客观的，并且通过不同的应力度量（如 Kirchhoff 应力）与上随体变化率优雅地联系在一起 [@problem_id:2886962]。

这个客观变化率家族为描述变形介质的物理学提供了一个完整的工具包。然而，上[随体导数](@entry_id:204621)占有特殊地位。通过同时考虑旋转和拉伸，它提供了一个完美的[运动学](@entry_id:173318)参考，使我们能够将材料响应中真正有趣的部分——弛豫、纠缠和流动的物理学——从材料仅被被动携带的平凡背景中分离出来。它就是我们着手构建的那个诚实的时钟，一个[运动学](@entry_id:173318)推理的杰作。

