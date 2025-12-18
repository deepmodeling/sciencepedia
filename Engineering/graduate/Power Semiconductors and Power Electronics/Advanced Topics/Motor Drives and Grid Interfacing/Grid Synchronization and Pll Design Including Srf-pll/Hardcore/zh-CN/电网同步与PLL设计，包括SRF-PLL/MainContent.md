## 引言
随着可再生能源和分布式发电的快速发展，大量的[电力](@entry_id:264587)电子变流器正以前所未有的规模并入电网。确保这些设备与电网精确、可靠地同步，是维持[电力](@entry_id:264587)系统稳定、高效运行的基石。[电网同步](@entry_id:1125807)技术，特别是锁相环（PLL），正是实现这一关键任务的核心。然而，真实的电网并非理想的正弦波源，它充满了电压不平衡、[谐波](@entry_id:181533)畸变、频率波动等各种扰动。设计一个能够在这些复杂多变的非理想条件下依然保持高性能的[同步系统](@entry_id:172214)，对[电力](@entry_id:264587)电子工程师构成了重大挑战。

本文旨在系统性地阐述现代[电网同步](@entry_id:1125807)技术，重点聚焦于工业界和学术界广泛应用的[同步参考系锁相环](@entry_id:1132249)（[SRF-PLL](@entry_id:1132249)）。文章分为三个核心章节：**“原理与机制”** 将深入剖析[SRF-PLL](@entry_id:1132249)的数学基础、控制结构和基本设计方法，为您构建坚实的理论基础。**“应用与跨学科连接”** 将视野扩展到真实世界的复杂性，探讨如何增强[锁相环](@entry_id:271717)在非理想电网下的鲁棒性，介绍DD[SRF-PLL](@entry_id:1132249)等高级结构，并讨论其与控制理论、信号处理及整个[电力](@entry_id:264587)系统的动态交互。最后，**“动手实践”** 提供了一系列精心设计的问题，旨在将理论知识转化为解决实际工程问题的能力。通过本文的学习，读者将不仅掌握[SRF-PLL](@entry_id:1132249)的设计与实现，更能深刻理解在现代[电力](@entry_id:264587)电子化电网中设计一个高性能[同步系统](@entry_id:172214)所需面临的挑战与权衡。

## 原理与机制

在将逆变器等[电力](@entry_id:264587)电子设备连接到电网时，精确的同步是一个基本要求。同步涉及到使变流器的内部时序与电网电压的振荡精确对准。本章深入探讨了实现这一目标所依据的原理和机制，重点关注在三相和单相系统中广泛使用的[同步参考系锁相环](@entry_id:1132249)（[SRF-PLL](@entry_id:1132249)）。我们将从基本定义开始，构建数学和控制框架，讨论实际的设计和实现考虑，并分析在非理想电网条件下的性能。

### [电网同步](@entry_id:1125807)的核心原理

从根本上说，**[电网同步](@entry_id:1125807)**（grid synchronization）是变流器的内部参考系与电网电压基波分量的相位和频率进行动态对准的过程。更精确地说，同步包含两个主要目标 ：

1.  **锁相（Phase Tracking）**：变流器的内部振荡器产生的估计相位角 $\hat{\theta}(t)$ 必须实时跟踪电网电压基波正序分量的实际相位角 $\theta_g(t)$。由于相位是周期性的，这种跟踪是在模 $2\pi$ 的意义上实现的，即 $\hat{\theta}(t) \equiv \theta_g(t) \pmod{2\pi}$。[相位误差](@entry_id:162993)可以定义为 $e_\theta(t) = \operatorname{wrap}_{(-\pi,\pi]}\big(\theta_g(t) - \hat{\theta}(t)\big)$，其中 $\operatorname{wrap}$ 函数将角度包装在 $(-\pi, \pi]$ 区间内，以处理 $2\pi$ 的不连续性。

2.  **[锁频](@entry_id:262107)（Frequency Tracking）**：变流器的估计[角频率](@entry_id:261565) $\hat{\omega}(t) = \frac{d}{dt}\hat{\theta}(t)$ 必须与电网的瞬时[角频率](@entry_id:261565) $\omega_g(t) = \frac{d}{dt}\theta_g(t)$ 相匹配。频率误差定义为 $e_\omega(t) = \omega_g(t) - \hat{\omega}(t)$。在相位误差 $e_\theta(t)$ 连续的区间内，这两个误差通过[微分](@entry_id:158422)关系相互关联：$\frac{d}{dt}e_\theta(t) = e_\omega(t)$。

值得注意的是，同步不应与**幅值估计**（amplitude estimation）相混淆。虽然许多高级控制方案也需要估计电网电压的幅值 $V_1(t)$，但这被认为是与相位和频率跟踪不同的一个独立任务。[锁相环](@entry_id:271717)（PLL）的核心功能是同步相位和频率，而不是估计幅值。

### 数学框架：从三相到[旋转坐标系](@entry_id:170324)

为了以一种可控的方式处理三相交流电压，我们采用了一系列数学变换，将三个时间变化的交流信号转换为直流信号。这个过程是[SRF-PLL](@entry_id:1132249)方法的核心。

#### Clarke 变换：从 ABC 到固定的 $\alpha\beta$ 坐标系

三相系统（a, b, c）中的瞬时电压，如 $v_a(t)$, $v_b(t)$, $v_c(t)$，可以被视为三维空间中的一个向量 $v_{abc}(t) = [v_a(t), v_b(t), v_c(t)]^\top$。对于一个平衡系统（即三个相位幅值相等，相位相差 $120^\circ$ 且没有零序分量），这个向量的轨迹实际上位于一个二维平面上。**[Clarke变换](@entry_id:1122422)**（Clarke transform）是一种[线性映射](@entry_id:185132)，它将 $abc$ 坐标系中的[向量投影](@entry_id:147046)到一个正交的二维固定坐标系（$\alpha\beta$ 坐标系）和一个零序分量上。

为了保持变换前后的[瞬时功率](@entry_id:174754)不变，即满足**功率不变性**（power invariance），[Clarke变换](@entry_id:1122422)矩阵 $T_\alpha$ 必须是正交的 。一个功率不变的[Clarke变换](@entry_id:1122422)定义为：
$$
v_{\alpha\beta 0} = T_\alpha v_{abc} \quad \text{其中} \quad T_\alpha = \sqrt{\frac{2}{3}}\begin{pmatrix}
1  & -\frac{1}{2}  & -\frac{1}{2} \\
0  & \frac{\sqrt{3}}{2}  & -\frac{\sqrt{3}}{2} \\
\frac{1}{\sqrt{2}}  & \frac{1}{\sqrt{2}}  & \frac{1}{\sqrt{2}}
\end{pmatrix}
$$
其中 $v_{\alpha\beta 0} = [v_\alpha, v_\beta, v_0]^\top$。$v_\alpha$ 和 $v_\beta$ 分量构成了所谓的**[空间矢量](@entry_id:1132014)**（space vector），在复平面中表示为 $v_\alpha(t) + jv_\beta(t)$。对于平衡的正序系统，这个空间矢量以电网角频率 $\omega_g$ 匀速旋转，其幅值等于相电压的峰值。零序分量 $v_0$ 则与[三相电](@entry_id:185866)压之和成正比，在平衡系统中为零。

#### Park 变换：从固定的 $\alpha\beta$ 坐标系到旋转的 $dq$ 坐标系

尽管[Clarke变换](@entry_id:1122422)将问题简化为二维，但 $\alpha$ 和 $\beta$ 分量仍然是正弦变化的。下一步是通过**[Park变换](@entry_id:1129357)**（Park transform）将固定的 $\alpha\beta$ [坐标系转换](@entry_id:263003)为一个以PLL估计的角频率 $\hat{\omega}$ 旋转的同步参考系（$dq$ 坐标系）。这个变换的本质是一次坐标系的旋转，其角度为PLL估计的相位角 $\hat{\theta}(t)$。

[Park变换](@entry_id:1129357)的目标是将旋转的电压空间矢量“固定”下来。当旋转的 $dq$ 坐标系与电网电压空间矢量同步旋转时，该矢量在 $dq$ 坐标系中的投影将变为直流（DC）分量。[变换矩阵](@entry_id:151616) $T_{dq}(\hat{\theta})$ 定义如下 ：
$$
v_{dq0} = T_{dq}(\hat{\theta}) v_{\alpha\beta 0} \quad \text{其中} \quad T_{dq}(\hat{\theta}) = \begin{pmatrix}
\cos\hat{\theta}  & \sin\hat{\theta}  & 0 \\
-\sin\hat{\theta}  & \cos\hat{\theta}  & 0 \\
0  & 0  & 1
\end{pmatrix}
$$
将 $\alpha\beta$ 坐标系中的电压分量 $v_\alpha = V \cos\theta_g$ 和 $v_\beta = V \sin\theta_g$（其中 $V$ 是峰值幅值，$\theta_g$ 是真实电网相位）代入，我们得到 $d$ 轴和 $q$ 轴的电压：
$$
v_d = v_\alpha \cos\hat{\theta} + v_\beta \sin\hat{\theta} = V(\cos\theta_g \cos\hat{\theta} + \sin\theta_g \sin\hat{\theta}) = V \cos(\theta_g - \hat{\theta})
$$
$$
v_q = -v_\alpha \sin\hat{\theta} + v_\beta \cos\hat{\theta} = V(-\cos\theta_g \sin\hat{\theta} + \sin\theta_g \cos\hat{\theta}) = V \sin(\theta_g - \hat{\theta})
$$
这些关系是[SRF-PLL](@entry_id:1132249)的核心。当PLL锁相时，相位误差 $\Delta\theta = \theta_g - \hat{\theta}$ 接近于零。此时，$v_d \approx V$ 且 $v_q \approx V \Delta\theta$。$q$ 轴电压 $v_q$ 因此成为一个与相位误差成正比的信号，是驱动[闭环控制系统](@entry_id:269635)实现同步的理想误差信号。

### [SRF-PLL](@entry_id:1132249)：一个[闭环控制系统](@entry_id:269635)

[SRF-PLL](@entry_id:1132249)的本质是一个负反馈控制系统，其目标是将 $v_q$ 分量调节到零，从而迫使[相位误差](@entry_id:162993) $\Delta\theta$ 趋于零。

#### [系统架构](@entry_id:1132820)

一个典型的[SRF-PLL](@entry_id:1132249)由三个关键部分组成 ：

1.  **[相位检测器](@entry_id:266236) (Phase Detector, PD)**：这部分由Clarke和[Park变换](@entry_id:1129357)组成。如上所述，它将三相AC输入电压转换为[旋转坐标系](@entry_id:170324)中的 $v_d$ 和 $v_q$ 分量。$q$ 轴电压 $v_q$ 直接用作相位误差的度量。

2.  **环路滤波器 (Loop Filter, LF)**：[相位误差](@entry_id:162993)信号 $v_q$ 被送入一个[环路滤波器](@entry_id:275178)，通常是一个**比例积分（PI）控制器**。[PI控制器](@entry_id:268031)的输出是对电网频率的修正量。
    -   **比例项 ($K_p$)**：提供对当前相位误差的快速响应，主要影响系统的动态响应速度和阻尼。
    -   **积分项 ($K_i$)**：对累积的[相位误差](@entry_id:162993)进行积分。它的关键作用是消除[稳态](@entry_id:139253)[相位误差](@entry_id:162993)。例如，如果电网频率与PLL的中心频率有一个微小的恒定偏差，积分作用将调整PLL的估计频率，直至[稳态](@entry_id:139253)相位误差为零。

3.  **压控/数控振荡器 (Voltage/Numerically Controlled Oscillator, VCO/NCO)**：环路滤波器的输出（频率修正量）与一个标称的电网频率（如 $2\pi \cdot 50$ rad/s）相加，得到最终的频率估计值 $\hat{\omega}(t)$。NCO通过对这个频率估计值进行积分来生成相位角估计值 $\hat{\theta}(t)$，即 $\frac{d\hat{\theta}}{dt} = \hat{\omega}$。这个更新后的相位角 $\hat{\theta}$ 再反馈给[Park变换](@entry_id:1129357)，形成闭环。

其信号流可以概括为：测量 $v_{abc}$ $\rightarrow$ [Clarke变换](@entry_id:1122422)得 $v_{\alpha\beta}$ $\rightarrow$ [Park变换](@entry_id:1129357)得 $v_q$ ([误差信号](@entry_id:271594)) $\rightarrow$ [PI控制器](@entry_id:268031)处理 $v_q$ 得 $\Delta\hat{\omega}$ $\rightarrow$ $\hat{\omega} = \omega_{\text{nom}} + \Delta\hat{\omega}$ $\rightarrow$ NCO积分 $\hat{\omega}$ 得 $\hat{\theta}$ $\rightarrow$ $\hat{\theta}$ 用于下一次[Park变换](@entry_id:1129357)。

#### 线性化[小信号模型](@entry_id:270703)

为了系统地设计[PI控制器](@entry_id:268031)参数，我们需要一个[线性模型](@entry_id:178302)来描述PLL的动态行为。这通过在[锁相](@entry_id:268892)点（$\Delta\theta \approx 0$）附近对系统进行线性化来实现。

我们已经知道，对于小的[相位误差](@entry_id:162993)，$v_q \approx V \Delta\theta$。这表明相位检测过程可以被建模为一个增益为 $K_{\mathrm{pd}}$ 的环节。这个**相位检测器增益**（phase detector gain）可以通过求导得到 ：
$$
K_{\mathrm{pd}} \triangleq \left.\frac{\partial v_{q}}{\partial \Delta \theta}\right|_{\Delta \theta=0}
$$
由于 $v_q = V \sin(\Delta\theta)$，其导数为 $V \cos(\Delta\theta)$。在 $\Delta\theta = 0$ 处求值，我们得到：
$$
K_{\mathrm{pd}} = V \cos(0) = V
$$
其中 $V$ 是电网的相电压峰值。这个简单的结果——相位检测器的增益就是电网电压的峰值幅值——是PLL设计的关键参数。

因此，整个[SRF-PLL](@entry_id:1132249)的[开环传递函数](@entry_id:276280) $L(s)$ 可以表示为[相位检测器](@entry_id:266236)、环路滤波器和NCO（一个积分器）的串联：
$$
L(s) = K_{\mathrm{pd}} \cdot C(s) \cdot P_{\mathrm{nco}}(s) = V \left( K_p + \frac{K_i}{s} \right) \frac{1}{s} = V \frac{K_p s + K_i}{s^2}
$$
这个[二阶系统](@entry_id:276555)模型是所有后续频率域设计和分析的基础。

### [SRF-PLL](@entry_id:1132249)的设计与调谐

有了线性模型，我们就可以采用标准的控制理论方法来设计[PI控制器](@entry_id:268031)的增益 $K_p$ 和 $K_i$，以满足特定的性能要求，如带宽和相位裕度 。

一个典型的设计流程如下：

1.  **确定系统参数**：首先，计算[相位检测器](@entry_id:266236)增益 $K_{\mathrm{pd}} = V$。例如，对于一个线电压有效值为 $400 \, \mathrm{V}$ 的三相系统，相电压有效值为 $V_{\mathrm{LN,rms}} = 400 / \sqrt{3} \approx 230.9 \, \mathrm{V}$。因此，相电压峰值 $V = V_{\mathrm{LN,rms}} \cdot \sqrt{2} \approx 326.6 \, \mathrm{V}$。

2.  **设定性能指标**：根据应用需求，确定期望的闭环**带宽**（通常以单位增益穿越频率 $\omega_c$ 表示）和**相位裕度**（$\phi_m$）。带宽决定了PLL对电网相位/频率变化的响应速度，而相位裕度则关系到系统的稳定性和阻尼。例如，我们可以设定 $\omega_c = 100 \, \mathrm{rad/s}$ 和 $\phi_m = 60^\circ$。

3.  **求解[控制器增益](@entry_id:262009)**：利用[开环传递函数](@entry_id:276280) $L(s)$ 和性能指标建立方程。
    -   **[相位裕度](@entry_id:264609)条件**：在穿越频率 $\omega_c$ 处，开环相角应为 $\arg(L(j\omega_c)) = \phi_m - 180^\circ$。
        $$
        \arg\left(V \frac{K_p (j\omega_c) + K_i}{-\omega_c^2}\right) = \arctan\left(\frac{\omega_c K_p}{K_i}\right) - 180^\circ = 60^\circ - 180^\circ = -120^\circ
        $$
        由此可得 $\arctan\left(\frac{\omega_c K_p}{K_i}\right) = 60^\circ$，即 $\frac{\omega_c K_p}{K_i} = \sqrt{3}$。
    -   **幅值条件**：在穿越频率 $\omega_c$ 处，开环幅值应为1，即 $|L(j\omega_c)| = 1$。
        $$
        \left|V \frac{K_p (j\omega_c) + K_i}{-\omega_c^2}\right| = \frac{V}{\omega_c^2}\sqrt{(\omega_c K_p)^2 + K_i^2} = 1
        $$
    -   联立求解这两个方程，可以得到 $K_p$ 和 $K_i$ 的表达式：
        $$
        K_i = \frac{\omega_c^2}{2 V} \quad \text{and} \quad K_p = \frac{\sqrt{3}}{\omega_c} K_i = \frac{\sqrt{3} \omega_c}{2 V}
        $$

4.  **计算与验证**：代入数值（$V \approx 326.6 \, \mathrm{V}$, $\omega_c = 100 \, \mathrm{rad/s}$），可得 $K_i \approx 15.3 \, \mathrm{(rad/s^2)/V}$ 和 $K_p \approx 0.265 \, \mathrm{(rad/s)/V}$。设计完成后，必须通过线性模型的[Bode图](@entry_id:268389)和[非线性系统](@entry_id:168347)的[时域仿真](@entry_id:755983)来验证设计是否满足所有性能要求。

### 实际实现中的考虑

从连续时间模型到离散时间数字实现的转变引入了新的挑战和考虑。

#### 数控振荡器（NCO）的实现

NCO在数字控制器中通过一个离散时间积分器来实现，其相位[更新方程](@entry_id:264802)为 ：
$$
\hat{\theta}[k] = \hat{\theta}[k-1] + \hat{\omega}[k] T_s
$$
其中 $T_s$ 是采样周期。在定点数实现中，必须仔细处理相位[累加器](@entry_id:175215) $\hat{\theta}[k]$ 和频率输入 $\hat{\omega}[k]$。

-   **相位[累加器](@entry_id:175215)的回绕 (Wrap-around)**：由于相位角是周期性的，[累加器](@entry_id:175215) $\hat{\theta}[k]$ 不需要无限增长。当其值超出 $[0, 2\pi)$ 或 $[-\pi, \pi)$ 的范围时，它应该“回绕”。例如，一个从 $2\pi - \epsilon$ 增加一个小步长的相位应该变为 $\epsilon$ 附近的一个小值。对相位进行**饱和**（即钳位在 $2\pi$）是**错误**的，因为这会使振荡器停止，导致PLL失锁。正确的做法是执行模 $2\pi$ 运算。在定点数实现中，这通常可以通过利用整数寄存器的自然溢出行为来高效实现。

-   **频率输入的约束**：频率估计值 $\hat{\omega}[k]$ 也需要约束。
    1.  **物理约束**：电网频率总是在一个已知的有限范围内变化（例如，50 Hz $\pm$ 1 Hz）。将 $\hat{\omega}[k]$ 饱和到一个合理的物理区间（如 $2\pi \cdot 45 \, \mathrm{rad/s}$ 到 $2\pi \cdot 55 \, \mathrm{rad/s}$）可以防止[环路滤波器](@entry_id:275178)[积分饱和](@entry_id:275065)（anti-windup），提高系统在暂态过程中的鲁棒性。
    2.  **奈奎斯特约束**：为了避免离散时间振荡器产生[混叠](@entry_id:146322)，相位在单个采样周期内的增量 $|\hat{\omega}[k] T_s|$ 必须小于 $\pi$。这意味着频率必须被约束在 $| \hat{\omega}[k] | \le \pi/T_s$ 的范围内。虽然物理电网频率远低于此限制，但在控制器发生不稳定或剧烈暂态时，此约束对于维持[数值稳定性](@entry_id:175146)至关重要。

#### 对传感器误差的鲁棒性

标准[SRF-PLL](@entry_id:1132249)的一个缺点是其动态性能依赖于电网电压的幅值 $V$，因为 $K_{\mathrm{pd}} = V$。这意味着如果电压传感器存在[增益误差](@entry_id:263104)，或者电网电压本身发生跌落或升高，PLL的带宽和[相位裕度](@entry_id:264609)都会发生变化，可能导致性能下降甚至不稳定。

一种有效的改进方法是使用**归一化**（normalization）的PLL 。在这种结构中，[相位检测器](@entry_id:266236)的输出不是 $v_q$，而是归一化的量 $v_q / |v|$，其中 $|v| = \sqrt{v_d^2 + v_q^2}$ 是从测量的 $dq$ 分量计算出的瞬时电压幅值。

让我们分析一下这种方法的好处。假设传感器有一个[增益误差](@entry_id:263104) $g$，测得的电压是真实值的 $g$ 倍。那么：
$$
v_d = gV \cos(\Delta\theta) \quad \text{and} \quad v_q = gV \sin(\Delta\theta)
$$
瞬时幅值为 $|v| = \sqrt{(gV \cos\Delta\theta)^2 + (gV \sin\Delta\theta)^2} = gV$。
归一化的[误差信号](@entry_id:271594)为：
$$
y_{\text{norm}} = \frac{v_q}{|v|} = \frac{gV \sin(\Delta\theta)}{gV} = \sin(\Delta\theta)
$$
对于小的[相位误差](@entry_id:162993)， $y_{\text{norm}} \approx \Delta\theta$。这意味着归一化PLL的相位检测器增益 $K_{\mathrm{pd,norm}} = 1$。这个增益既不依赖于电网电压幅值 $V$，也不依赖于传感器增益 $g$。因此，归一化PLL的闭环动力学与电压幅值和传感器增益完全[解耦](@entry_id:160890)，从而获得了极高的鲁棒性。其对传感器[增益误差](@entry_id:263104)的对数灵敏度为零，而未归一化PLL的灵敏度为1。

### 在非理想电网条件下的性能

实际电网电压并非完美的正弦波，可能存在不平衡和背景谐波。[SRF-PLL](@entry_id:1132249)对这些非理想因素的响应是评估其性能的关键。

#### 电网不平衡：负序分量的影响

电网不平衡意味着[三相电](@entry_id:185866)压的幅值不相等或相位间隔不完全是 $120^\circ$。任何不平衡的三相系统都可以分解为一个平衡的正序分量和一个平衡的**负序分量**（以及一个零序分量）。正序分量以角频率 $+\omega$ 旋转，而负序分量以 $-\omega$ 旋转。

当一个包含正序矢量 $V^+ e^{j\omega t}$ 和负序矢量 $V^- e^{-j\omega t}$ 的电压被转换到一个以 $+\omega$ 旋转的同步参考系时，其 $dq$ 分量为 ：
$$
\mathbf{v}_{dq}(t) = (V^+ e^{j\omega t} + V^- e^{-j\omega t}) e^{-j\omega t} = V^+ + V^- e^{-j2\omega t}
$$
这表明，正序分量 $V^+$ 成为一个DC量，而负序分量 $V^-$ 则表现为一个以角频率 $-2\omega$ 旋转的矢量，即在 $v_d$ 和 $v_q$ 上产生频率为 $2\omega$ 的**二[次谐波](@entry_id:171489)纹波**。例如，如果负序分量的幅值是正序的5%（$|V^-| = 0.05|V^+|$），并且PLL的d轴与正序电压对齐（$V^+$为实数），则：
$$
v_d(t) = |V^+| + 0.05|V^+| \cos(2\omega t - \phi_-)
$$
$$
v_q(t) = -0.05|V^+| \sin(2\omega t - \phi_-)
$$
其中 $\phi_-$ 是负序分量的初始相位。这个 $2\omega$ 的纹波会扰乱 $v_q$ [误差信号](@entry_id:271594)，导致PLL的相位和频率估计出现振荡，并最终影响变流器注入电网的电流质量。

#### [谐波](@entry_id:181533)畸变的影响

电网电压通常也包含背景谐波。在三相系统中，最常见的[谐波](@entry_id:181533)是5次、7次、11次、13次等。这些[谐波](@entry_id:181533)也具有序的特性。通常，$h=3k-1$ 次谐波（如5次、11次）是负序的，而 $h=3k+1$ [次谐波](@entry_id:171489)（如7次、13次）是正序的。

一个序为 $s$（$s=+1$ 表示正序, $s=-1$ 表示负序）、次数为 $h$ 的谐波，在固定坐标系中以 $s \cdot h\omega$ 的频率旋转。当通过[Park变换](@entry_id:1129357)进入以 $+\omega$ 旋转的同步参考系时，其频率会变为 $(sh - 1)\omega$ 。

-   对于**5[次谐波](@entry_id:171489)**（负序）：$h=5, s=-1$。它在 $dq$ 坐标系中的频率为 $(-1 \cdot 5 - 1)\omega = -6\omega$。
-   对于**7[次谐波](@entry_id:171489)**（正序）：$h=7, s=+1$。它在 $dq$ 坐标系中的频率为 $(+1 \cdot 7 - 1)\omega = +6\omega$。

有趣的是，5次和7次谐波在 $dq$ 坐标系中都表现为**六[次谐波](@entry_id:171489)纹波**。这两个纹波分量会叠加在 $v_q$ 信号上。其总幅值取决于两个谐波分量的幅值以及它们之间的[相对相位](@entry_id:148120)。这个 $6\omega$ 的纹波同样会干扰PLL的正常工作，导致相位估计产生高频[抖动](@entry_id:200248)。为了应对不平衡和谐波问题，需要设计更高级的PLL结构，例如双同步参考系PLL（D[SRF-PLL](@entry_id:1132249)）或使用[陷波滤波器](@entry_id:261721)来滤除特定的纹波频率。

### 单相系统的扩展

[SRF-PLL](@entry_id:1132249)的原理是基于二维旋转矢量的概念，这天然适用于三相系统。然而，在**单相系统**中，我们只有一个测量信号 $v(t)$。为了应用[SRF-PLL](@entry_id:1132249)框架，必须人工生成一个与原始信号正交的虚拟信号，从而构建一个二维的 $\alpha\beta$ 矢量。这个过程由**[正交信号发生器](@entry_id:172425)（Quadrature Signal Generator, QSG）**完成 。

一种广泛使用的QSG是**二阶广义积分器（Second-Order Generalized Integrator, SOGI）**。SOGI是一个线性滤波器，它接收单相输入信号 $v(t)$，并产生两个输出：一个与输入同相的信号 $v_\alpha(t)$ 和一个与输入正交（相差 $90^\circ$）的信号 $v_\beta(t)$。

SOGI的关键特性是：
-   它在其[谐振频率](@entry_id:265742) $\hat{\omega}$ 处具有单位增益和零相移（对于 $v_\alpha$ 输出），以及单位增益和 $-90^\circ$ 相移（对于 $v_\beta$ 输出）。
-   为了使SOGI能够为任意输入频率 $\omega$ 生成完美的[正交信号](@entry_id:193351)（即 $v_\alpha$ 和 $v_\beta$ 幅值相等且相位相差 $90^\circ$），SOGI的谐振频率 $\hat{\omega}$ 必须精确地等于输入信号的频率 $\omega$。

因此，在单相PLL中，SOGI和[SRF-PLL](@entry_id:1132249)通常是耦合在一起的。PLL估计出的电网频率 $\hat{\omega}$ 会被反馈给SOGI，以实时调整其谐振频率，确保能够持续准确地生成[正交信号](@entry_id:193351)。这种SOGI-PLL结构使得强大的[SRF-PLL](@entry_id:1132249)技术能够成功地应用于单相[电网同步](@entry_id:1125807)任务中。