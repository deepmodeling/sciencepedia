## 引言
在[量子光学](@entry_id:140582)的领域中，理解强[激光](@entry_id:194225)场与单个原子的相互作用是探索光与物质深层次联系的基石。当一个原子被强[相干光](@entry_id:170661)场驱动时，其能级结构会发生根本性的重塑，形成新的[能量本征态](@entry_id:152154)——“缀饰态”（dressed states）。这个简洁的图像为解释高强度场下的原子响应提供了强大的物理直觉。然而，一个孤立的、仅由[哈密顿量](@entry_id:172864)描述的系统是一个理想化的模型。真实的原子系统是开放的，它不可避免地与周围环境（如真空[电磁场](@entry_id:265881)）发生耦合，从而引发自发辐射等耗散过程。这就提出了一个核心问题：我们如何建立一个统一的理论框架，既能包含强场驱动下的相干“缀饰”效应，又能精确描述耗散带来的非相干动力学？

本文旨在系统性地解答这一问题，通过构建和应用“[缀饰原子](@entry_id:202812)主方程”这一核心工具。在接下来的内容中，读者将深入学习：首先，在“原理和机制”一章中，我们将详细推导[缀饰原子](@entry_id:202812)主方程，并阐明其如何揭示[共振荧光](@entry_id:195107)（莫洛三线谱）和[AC斯塔克位移](@entry_id:161492)等基本现象的物理根源。接着，在“应用与跨学科关联”一章，我们将展示该理论如何应用于激光冷却、[非经典光](@entry_id:190601)源制备等前沿技术，并探索其在凝聚态物理、天体物理等领域的广泛联系。最后，通过“动手实践”部分，读者将有机会将理论知识应用于解决具体的物理问题。让我们从建立[缀饰原子](@entry_id:202812)主方程的基本原理开始，一步步揭开这个强驱动[开放量子系统](@entry_id:138632)的神秘面纱。

## 原理和机制

在上一章中，我们介绍了在[激光](@entry_id:194225)场驱动下的二能级原子模型，并通过[旋转波近似](@entry_id:204016)，得到了描述原子与[激光](@entry_id:194225)相互作用的[哈密顿量](@entry_id:172864)。该[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)，即缀饰态（dressed states），为我们提供了一个强有力的物理图像，用以理解强场驱动下的原子行为。然而，一个真实的原子系统并非孤立存在，它不可避免地会与环境，特别是真空[电磁场](@entry_id:265881)，发生相互作用。这种相互作用导致了[自发辐射](@entry_id:140032)等耗散过程。本章的核心任务是建立描述这种[开放量子系统](@entry_id:138632)动力学的理论框架——[缀饰原子](@entry_id:202812)[主方程](@entry_id:142959)，并运用它来阐释一系列关键的[量子光学](@entry_id:140582)现象。

### [缀饰原子](@entry_id:202812)[主方程](@entry_id:142959)

描述一个与环境耦合的量子系统，其密度矩阵 $\rho$ 的演化由林德布拉德（Lindblad）[主方程](@entry_id:142959)给出。对于一个经历自发辐射的二能级原子，其[主方程](@entry_id:142959)在裸态[基矢](@entry_id:199546)（bare-state basis）$\{|g\rangle, |e\rangle\}$ 下写作：
$$
\frac{d\rho}{dt} = -\frac{i}{\hbar}[H, \rho] + \mathcal{L}[\rho]
$$
其中 $H$ 是系统的[哈密顿量](@entry_id:172864)，而 $\mathcal{L}[\rho]$ 是描述耗散的林德布拉德超算符（Liouvillian）。对于自发辐射过程，跃迁算符是原子降低算符 $\sigma_- = |g\rangle\langle e|$，衰减率为 $\Gamma$，对应的耗散项为：
$$
\mathcal{L}[\rho] = \frac{\Gamma}{2}(2\sigma_-\rho\sigma_+ - \sigma_+\sigma_-\rho - \rho\sigma_+\sigma_-)
$$
为了在缀饰态图像下理解系统的动力学，我们需要将整个[主方程](@entry_id:142959)转换到[缀饰态](@entry_id:143646)[基矢](@entry_id:199546)中。

#### [缀饰态](@entry_id:143646)与混合角

首先，我们回顾在频率为 $\omega_L$ 的[激光](@entry_id:194225)驱动下，原子与[激光](@entry_id:194225)相互作用的[哈密顿量](@entry_id:172864)，在以 $\omega_L$ 旋转的[参考系](@entry_id:169232)中为：
$$
H = -\frac{\hbar\Delta}{2}\sigma_z + \frac{\hbar\Omega}{2}\sigma_x
$$
其中，$\Delta = \omega_L - \omega_a$ 是[激光](@entry_id:194225)频率与原子跃迁频率 $\omega_a$ 之间的[失谐](@entry_id:148084)，$\Omega$ 是[拉比频率](@entry_id:154019)，$\sigma_x = |e\rangle\langle g| + |g\rangle\langle e|$ 和 $\sigma_z = |e\rangle\langle e| - |g\rangle\langle g|$ 是泡利算符。

该[哈密顿量](@entry_id:172864)的本征态是[缀饰态](@entry_id:143646)，记为 $|1\rangle$ 和 $|2\rangle$（或 $|+\rangle$ 和 $|-\rangle$，取决于约定），其能量为 $E_{1,2} = \pm \frac{\hbar\Omega'}{2}$，其中 $\Omega' = \sqrt{\Omega^2 + \Delta^2}$ 是广义[拉比频率](@entry_id:154019)。这两个[缀饰态](@entry_id:143646)是裸态的线性叠加：
$$
|1\rangle = \cos(\theta/2)|e\rangle - \sin(\theta/2)|g\rangle \\
|2\rangle = \sin(\theta/2)|e\rangle + \cos(\theta/2)|g\rangle
$$
这里的混合角 $\theta$ 由驱动参数决定，满足关系 $\cos\theta = -\Delta/\Omega'$ 和 $\sin\theta = \Omega/\Omega'$。这个角度 $\theta$ 表征了[激光](@entry_id:194225)场将裸态 $|g\rangle$ 和 $|e\rangle$ “混合”成新的[能量本征态](@entry_id:152154)（[缀饰态](@entry_id:143646)）的程度。

#### 跃迁算符的分解

理解耗散过程在[缀饰态](@entry_id:143646)[基矢](@entry_id:199546)中如何作用的关键，在于将裸态的跃迁算符 $\sigma_-$ 分解到缀饰态[基矢](@entry_id:199546)上。任何作用于此二维空间的算符都可以写成[缀饰态](@entry_id:143646)[投影算符](@entry_id:154142) $|j\rangle\langle k|$（其中 $j, k \in \{1, 2\}$）的线性组合：
$$
\sigma_- = \sum_{j,k \in \{1,2\}} c_{jk} |j\rangle\langle k| \quad \text{其中} \quad c_{jk} = \langle j|\sigma_-|k\rangle
$$
通过将[缀饰态](@entry_id:143646)的表达式代入，我们可以计算出这些系数 $c_{jk}$：
$$
c_{11} = \langle 1|g\rangle\langle e|1\rangle = (-\sin(\theta/2))(\cos(\theta/2)) = -\frac{1}{2}\sin\theta \\
c_{22} = \langle 2|g\rangle\langle e|2\rangle = (\cos(\theta/2))(\sin(\theta/2)) = \frac{1}{2}\sin\theta \\
c_{12} = \langle 1|g\rangle\langle e|2\rangle = (-\sin(\theta/2))(\sin(\theta/2)) = -\sin^2(\theta/2) \\
c_{21} = \langle 2|g\rangle\langle e|1\rangle = (\cos(\theta/2))(\cos(\theta/2)) = \cos^2(\theta/2)
$$
这些系数所代表的物理过程可以分为两类：
1.  **“垂直”跃迁** (Vertical Transitions)：对应 $j=k$ 的项，如 $c_{11}|1\rangle\langle 1|$ 和 $c_{22}|2\rangle\langle 2|$。这些算符描述了系统与真空相互作用后，仍处于同一缀饰态能级阶梯内的过程。它们与相干瑞利散射有关。
2.  **“[交叉](@entry_id:147634)”跃迁** (Cross Transitions)：对应 $j \neq k$ 的项，如 $c_{12}|1\rangle\langle 2|$ 和 $c_{21}|2\rangle\langle 1|$。这些算符描述了系统因自发辐射而从一个[缀饰态](@entry_id:143646)能级阶梯跃迁到另一个的过程。它们是[非弹性散射](@entry_id:138624)过程，是产生[共振荧光](@entry_id:195107)（如莫洛三线谱）的根源。

我们可以通过计算这些分量的“强度”来量化它们的相对重要性。定义垂直（或弹性）分量的总强度为 $S_{el} = |c_{11}|^2 + |c_{22}|^2$，[交叉](@entry_id:147634)（或非弹性）分量的总强度为 $S_{inel} = |c_{12}|^2 + |c_{21}|^2$。通过简单的代数计算 [@problem_id:690873]，我们得到：
$$
S_{el} = 2 \left(\frac{1}{2}\sin\theta\right)^2 = \frac{1}{2}\sin^2\theta \\
S_{inel} = \sin^4(\theta/2) + \cos^4(\theta/2) = 1 - 2\sin^2(\theta/2)\cos^2(\theta/2) = 1 - \frac{1}{2}\sin^2\theta
$$
它们的比值 $\mathcal{F} = S_{inel}/S_{el}$ 揭示了一个深刻的物理洞察：
$$
\mathcal{F} = \frac{1 - \frac{1}{2}\sin^2\theta}{\frac{1}{2}\sin^2\theta} = \frac{2}{\sin^2\theta} - 1
$$
利用 $\sin^2\theta = \Omega^2 / (\Omega^2 + \Delta^2)$, 我们最终得到：
$$
\mathcal{F} = \frac{S_{inel}}{S_{el}} = 1 + \frac{2\Delta^2}{\Omega^2}
$$
这个结果表明，当驱动场与原子共振时（$\Delta=0$），非弹性散射的强度与[弹性散射](@entry_id:152152)的强度相等。而当驱动场远离共振时（$|\Delta| \gg \Omega$），[非弹性散射](@entry_id:138624)过程占据主导地位。这解释了为什么在远失谐驱动下，原子散射的[光子](@entry_id:145192)频率会与入射[光子](@entry_id:145192)频率有显著差异。

### 非相干动力学与[稳态](@entry_id:182458)

[自发辐射](@entry_id:140032)在[缀饰态](@entry_id:143646)表象下诱导的[交叉](@entry_id:147634)跃迁，驱动系统产生非相干的布居数转移，并最终达到一个非[热平衡](@entry_id:141693)的[稳态](@entry_id:182458)。

#### 非相干跃迁速率

从一个[缀饰态](@entry_id:143646) $|i\rangle$ 到另一个 $|f\rangle$ 的非相干跃迁速率 $R_{f \leftarrow i}$ 正比于相应跃迁矩阵元模的平方，即 $R_{f \leftarrow i} \propto |\langle f|\sigma_-|i\rangle|^2$。使用上一节计算的系数 $c_{jk}$，我们可以直接写出[缀饰态](@entry_id:143646)之间的跃迁速率 [@problem_id:690748]。

为明确起见，我们定义上能级缀饰态为 $|u\rangle$ (能量 $E_u$)，下能级为 $|l\rangle$ (能量 $E_l$)。从上能级 $|u\rangle$ 到下能级 $|l\rangle$ 的衰变速率 $R_{decay}$ 和从下能级 $|l\rangle$ 到上能级 $|u\rangle$ 的激发速率 $R_{excite}$ 分别为：
$$
R_{decay} = \Gamma |\langle l|\sigma_-|u\rangle|^2 = \Gamma \cos^4(\theta/2) \\
R_{excite} = \Gamma |\langle u|\sigma_-|l\rangle|^2 = \Gamma \sin^4(\theta/2)
$$
值得注意的是，自发辐射这一纯粹的“衰减”过程，在[缀饰态](@entry_id:143646)图像中竟然可以导致系统从低能态“激发”到高能态。这并非[能量不守恒](@entry_id:276143)，而是因为缀饰态本身就包含了驱动场的作用，能量的交换发生在整个“原子+[激光](@entry_id:194225)场”系统中。

这两个速率的比值给出了一个至关重要的结果：
$$
\frac{R_{decay}}{R_{excite}} = \frac{\cos^4(\theta/2)}{\sin^4(\theta/2)} = \cot^4(\theta/2) = \left(\frac{1+\cos\theta}{1-\cos\theta}\right)^2 = \left(\frac{1-\Delta/\Omega'}{1+\Delta/\Omega'}\right)^2 = \left(\frac{\Omega'-\Delta}{\Omega'+\Delta}\right)^2
$$
这个比率强烈依赖于失谐 $\Delta$。当[激光](@entry_id:194225)为[红失谐](@entry_id:160023)（$\Delta  0$）时，分子 $\Omega'-\Delta$ 较大，而分母 $\Omega'+\Delta$ 较小，导致 $R_{decay} \gg R_{excite}$。这意味着系统倾向于从高能[缀饰态](@entry_id:143646)衰变到低能[缀饰态](@entry_id:143646)，每次跃迁都从系统中净移除了能量。这是多种激光冷却机制（如[西西弗斯冷却](@entry_id:162161)）的微观物理基础。相反，当[激光](@entry_id:194225)为蓝失谐（$\Delta > 0$）时，$R_{excite}$ 相对更大，导致净加热效应。

#### [稳态](@entry_id:182458)布居与[AC斯塔克位移](@entry_id:161492)

在长[时间演化](@entry_id:153943)后，系统将达到一个[稳态](@entry_id:182458)，此时从 $|u\rangle$ 到 $|l\rangle$ 的总跃迁流与从 $|l\rangle$ 到 $|u\rangle$ 的总跃迁流相等。设[稳态](@entry_id:182458)时 $|u\rangle$ 和 $|l\rangle$ 的布居数分别为 $\pi_u$ 和 $\pi_l$，则[细致平衡条件](@entry_id:265158)为：
$$
\pi_u R_{decay} = \pi_l R_{excite}
$$
结合[归一化条件](@entry_id:156486) $\pi_u + \pi_l = 1$，我们可以解出[稳态](@entry_id:182458)布居数 [@problem_id:690944]。

由驱动光场引起的[原子能级](@entry_id:148255)位移被称为[AC斯塔克位移](@entry_id:161492)（AC Stark Shift）。在远失谐极限下（$|\Delta| \gg \Omega$），缀饰态近似于裸态，此时可以通过[二阶微扰理论](@entry_id:192858)证明，裸[基态](@entry_id:150928) $|g\rangle$ 的能量位移 $\delta E_g$ 恰好是 [@problem_id:690730]：
$$
\delta E_g \approx \frac{\hbar\Omega^2}{4\Delta}
$$
这个结果通常被称为光学偶极力的[势能](@entry_id:748988)，它描述了原子因与非共振光场相互作用（可以看作是虚光子的吸收和发射）而获得的能量。

### [共振荧光](@entry_id:195107)：莫洛三线谱

[缀饰态](@entry_id:143646)图像最著名的成功之一是它对[共振荧光](@entry_id:195107)[光谱](@entry_id:185632)的完美解释。一个被强[激光](@entry_id:194225)场驱动的原子散射的[光谱](@entry_id:185632)并非单色的，而是呈现出三明治般的结构，即莫洛三线谱（Mollow Triplet）。

#### [光谱](@entry_id:185632)的物理来源

莫洛三线谱的三个峰对应于[缀饰态](@entry_id:143646)能级阶梯之间的四种可能跃迁。假设原子-[激光](@entry_id:194225)系统吸收了驱动场的一个[光子](@entry_id:145192)，从 $|j, n\rangle$ 跃迁到 $|j, n+1\rangle$（这里 $n$ 是驱动[场模](@entry_id:189270)式中的[光子](@entry_id:145192)数，只是一个记号）。随后，原子自发辐射一个[光子](@entry_id:145192)并回到某个缀饰态。发射[光子](@entry_id:145192)的频率由跃迁前后的能量差决定。
1.  **中央峰**：由“垂直”跃迁 $|u, n+1\rangle \to |u, n\rangle$ 和 $|l, n+1\rangle \to |l, n\rangle$ 产生。发射[光子](@entry_id:145192)的能量恰好等于驱动[光子](@entry_id:145192)的能量，因此[谱线](@entry_id:193408)位于驱动频率 $\omega_L$ 处。
2.  **[边带](@entry_id:261079)**：由“[交叉](@entry_id:147634)”跃迁产生。
    *   衰变跃迁 $|u, n+1\rangle \to |l, n\rangle$ 发射的[光子](@entry_id:145192)频率为 $\omega_L - \Omega'$。这形成了一个[红失谐](@entry_id:160023)的[边带](@entry_id:261079)。
    *   激发跃迁 $|l, n+1\rangle \to |u, n\rangle$ 发射的[光子](@entry_id:145192)频率为 $\omega_L + \Omega'$。这形成了一个蓝[失谐](@entry_id:148084)的[边带](@entry_id:261079)。

#### [谱线宽度](@entry_id:168313)

根据[量子回归定理](@entry_id:186216)，荧光[光谱](@entry_id:185632)的形状是原子偶极矩关联函数 $\langle\sigma^+(t)\sigma^-(0)\rangle$ 的[傅里叶变换](@entry_id:142120)。该关联函数的动力学演化与[密度矩阵](@entry_id:139892)元的演化遵循相同的规律。因此，[谱线](@entry_id:193408)的宽度由缀饰态布居数和[相干性](@entry_id:268953)的衰减率决定。

为了简化分析，我们考虑共振驱动（$\Delta=0, \Omega'=\Omega$）和强驱动（$\Omega \gg \Gamma$）的极限情况。描述缀饰态布居数差和相干[性的演化](@entry_id:163338)矩阵的[本征值](@entry_id:154894)决定了衰减率。分析表明，系统存在三个主要的衰减模式 [@problem_id:417138]：
*   一个慢衰减模式，其衰减率（即[谱线](@entry_id:193408)半宽）为 $\Gamma_0 = \Gamma/2$。这个纯实数的[本征值](@entry_id:154894)对应于[缀饰态](@entry_id:143646)布居数的衰减，它决定了中央峰的宽度。
*   两个快衰减模式，它们是共轭复数，其实部给出的衰减率为 $\Gamma_\pm = 3\Gamma/4$。这两个模式对应缀饰态[相干性](@entry_id:268953)的衰减，并决定了两个边带的宽度。

因此，[边带](@entry_id:261079)的宽度是中央峰宽度的 $3/2$ 倍：
$$
\frac{\Gamma_\pm}{\Gamma_0} = \frac{3}{2}
$$
这是一个反直觉但被实验精确验证的著名结果。它深刻地揭示了不同物理量（布居数和相干性）在[开放系统](@entry_id:147845)中有不同的衰减时间。对于更精确的分析，可以发现中央峰的宽度实际上也依赖于驱动强度。在强场下，其半宽度的修正项为 [@problem_id:690938]：
$$
\text{HWHM}_{\text{central}} \approx \frac{\Gamma}{2} - \frac{\Gamma^3}{32\Omega^2}
$$
这表明在极强的驱动下，中央峰会变得比通常认为的 $\Gamma/2$ 更窄。

#### 相干与[非相干散射](@entry_id:190180)

原子散射的总光强可以分为两个部分：相干（弹性）散射和非相干（非弹性）散射。
*   **[相干散射](@entry_id:267724)**：其强度正比于[稳态](@entry_id:182458)偶极矩的平方 $|\langle\sigma_-\rangle_{ss}|^2$。它对应于一个频率严格等于 $\omega_L$ 的无限窄的[谱线](@entry_id:193408)（$\delta$-函数），物理上是原子作为一个[经典偶极子](@entry_id:151120)被驱动场极化后辐射的结果。
*   **[非相干散射](@entry_id:190180)**：其强度正比于偶极矩的[方差](@entry_id:200758) $\langle\sigma_+\sigma_-\rangle_{ss} - |\langle\sigma_-\rangle_{ss}|^2$。这部分光强[分布](@entry_id:182848)在整个莫洛三线谱中，来源于与[自发辐射](@entry_id:140032)相关的[量子涨落](@entry_id:154889)。

这两个分量的积分强度之比为 [@problem_id:690831]：
$$
\frac{A_{coh}}{A_{incoh}} = \frac{2(\Delta^2+\Gamma^2/4)}{\Omega^2}
$$
该比值告诉我们，当驱动较弱（$\Omega$ 小）或远[失谐](@entry_id:148084)（$|\Delta|$ 大）时，相干瑞利散射占主导。而在强驱动或近共振条件下，大部分[光子](@entry_id:145192)都以非相干的莫洛三线谱形式被散射出来。

### 高阶效应与其他耗散通道

[缀饰原子](@entry_id:202812)主方程还可以用于分析更精细的物理效应和更复杂的环境相互作用。

#### 非久期效应：[稳态](@entry_id:182458)相干性

在推导许多结果时，我们常常使用“[久期近似](@entry_id:189746)”（secular approximation），即忽略在[主方程](@entry_id:142959)中以高频 $\Omega'$ [振荡](@entry_id:267781)的项。然而，这些非[久期项](@entry_id:167483)可以导致一些有趣的效应。一个显著的例子是，它们可以在缀饰态之间诱导出一个非零的[稳态](@entry_id:182458)[相干性](@entry_id:268953) $\pi_{+-} = \langle +|\rho_{ss}|-\rangle$。

通常我们认为，不同能量本征态之间的相干性在[稳态](@entry_id:182458)时会衰减为零。但对于[缀饰原子](@entry_id:202812)系统，驱动和耗散的持续作用可以维持一个非零的相干性。对于共振驱动的情况，可以精确求解得到其虚部为 [@problem_id:690838]：
$$
\text{Im}(\pi_{+-}) = \frac{\Gamma\Omega}{2\Omega^2+\Gamma^2}
$$
这个[稳态](@entry_id:182458)相 coherent性的存在，是原子内部动力学与外部驱动和耗散之间复杂协同作用的直接证据。

#### [纯退相干](@entry_id:204036)通道的影响

除了自发辐射（[能量弛豫](@entry_id:136820)），原子还可能经历[纯退相干](@entry_id:204036)过程（例如由环境涨落或碰撞引起的相位随机化），其跃迁算符为 $\sigma_z$。对应的耗散项为 $\mathcal{L}_\phi \rho = \gamma_\phi(\sigma_z\rho\sigma_z - \rho)$。

当我们将这个耗散项转换到缀饰态[基矢](@entry_id:199546)时，会发现一个有趣的现象。因为裸态算符 $\sigma_z$ 在[缀饰态](@entry_id:143646)[基矢](@entry_id:199546)中可以分解为：
$$
\sigma_z = \cos\theta\,\tilde{\sigma}_z - \sin\theta\,\tilde{\sigma}_x
$$
其中 $\tilde{\sigma}_z$ 和 $\tilde{\sigma}_x$ 是[缀饰态](@entry_id:143646)[基矢](@entry_id:199546)中的泡利算符。这意味着，一个在裸态[基矢](@entry_id:199546)中纯粹的“横向”[退相干](@entry_id:145157)过程，在[缀饰态](@entry_id:143646)[基矢](@entry_id:199546)中会同时引起“纵向”的布居数弛豫和“横向”的[相干性](@entry_id:268953)衰减 [@problem_id:690733]。

在[久期近似](@entry_id:189746)下，我们可以定义缀饰态的有效纵向[弛豫率](@entry_id:150136) $\gamma_L$（布居数差衰减率）和横向[弛豫率](@entry_id:150136) $\gamma_T$（相干性衰减率）。它们分别由 $\sigma_z$ 分解式中的 $\tilde{\sigma}_x$ 和 $\tilde{\sigma}_z$ 部分贡献。其比值为：
$$
\frac{\gamma_L}{\gamma_T} = \frac{2\sin^2\theta}{2\cos^2\theta+\sin^2\theta} = \frac{2\Omega^2}{2\Delta^2+\Omega^2}
$$
这个结果表明，通过调节[激光](@entry_id:194225)的参数（$\Omega$ 和 $\Delta$），我们可以控制一个给定的噪声源（[纯退相干](@entry_id:204036)）在[缀饰态](@entry_id:143646)表象下表现为弛豫还是退相干。例如，在共振时（$\Delta=0$），$\gamma_L/\gamma_T = 2$，退相干过程主要引起缀饰态的布居数弛豫。

类似地，在[腔量子电动力学](@entry_id:149422)（Cavity QED）的杰恩斯-卡明斯（Jaynes-Cummings）模型中，原子的[纯退相干](@entry_id:204036)也会导致杰恩斯-卡明斯[缀饰态](@entry_id:143646) $|n, \pm\rangle$ 之间[相干性](@entry_id:268953)的衰减。在强[退相干](@entry_id:145157)（或[过阻尼](@entry_id:167953)）极限 $\gamma_\phi > \Omega_n$（其中 $\Omega_n = 2g\sqrt{n+1}$ 是能级劈裂）下，[相干性](@entry_id:268953)会以两个实指数率衰减，其中较慢的那个衰减率为 [@problem_id:670496]：
$$
\lambda_{slow} = \gamma_\phi - \sqrt{\gamma_\phi^2 - 4g^2(n+1)}
$$
这展示了[缀饰态](@entry_id:143646)方法在分析不同物理系统中的耗散过程时的普适性和强大功能。