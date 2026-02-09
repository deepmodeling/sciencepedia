## 引言
在工程与科学的广阔天地中，[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)因其简洁的[叠加原理](@keyword=linearity_principle|lang=zh-CN|style=Feynman)而易于分析。然而，从[机械振动](@keyword=mechanical_vibrations|lang=zh-CN|style=Feynman)到生命节律，真实世界充满了复杂且难以预测的[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)现象。这些系统不遵循[叠加原理](@keyword=linearity_principle|lang=zh-CN|style=Feynman)，常常展现出独特的“[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)”——一种自我维持的稳定[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，对它的分析是传统[线性](@keyword=linearity|lang=zh-CN|style=Feynman)工具无法企及的难题。面对这一挑战，[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)应运而生，它提供了一种强大而直观的[近似分析](@keyword=proximate_analysis|lang=zh-CN|style=Feynman)技术。本文旨在系统阐述这一方法。我们将首先深入剖析[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)的**原理与机制**，理解其如何通过[谐波平衡](@keyword=harmonic_balance|lang=zh-CN|style=Feynman)来预测[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。接着，我们将探索其在**应用与跨学科[连接](@keyword=concatenation|lang=zh-CN|style=Feynman)**中的具体实例，从工程设计到[生物模型](@keyword=biological_models|lang=zh-CN|style=Feynman)。最后，通过一系列**动手实践**来巩固所学。现在，就让我们开始探索[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)的核心概念。

## 原理与机制

在[物理学](@keyword=physics|lang=zh-CN|style=Feynman)和工程学的世界里，我们钟爱[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)。它们举止优雅、彬彬有礼。如果你把两个输入加在一起送进一个[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)，得到的输出就是两个输入单独产生的输出之和。这种“[叠加原理](@keyword=linearity_principle|lang=zh-CN|style=Feynman)”让分析变得异常简单，就像用乐高积木搭建一样，一切都清晰明了。然而，真实的世界却很少如此“守规矩”。从吉他音箱中刺耳的反馈啸叫，到飞机机翼在特定[速度](@keyword=velocity|lang=zh-CN|style=Feynman)下发生的危险颤振，再到我们心脏有节奏的搏动，这些现象的背后都潜藏着一种更普遍、也更狂野的力量——**[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)**。

[非线性系统](@keyword=nonlinear_systems|lang=zh-CN|style=Feynman)常常让我们头疼，因为[叠加原理](@keyword=linearity_principle|lang=zh-CN|style=Feynman)在这里完全失效。它们的行为难以预测，充满了各种惊奇，比如“[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)”（limit cycles）——一种不依赖于初始状态的、自我维持的稳定[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。面对这些“不守规矩”的系统，我们该如何是好？难道只能在复杂的数学公式中迷失方向吗？不。伟大的科学思想往往不是用更复杂的锤子去砸碎坚果，而是找到一种巧妙的视角，让坚果自己裂开。[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)（Describing Function method）正是这样一种闪耀着智慧光芒的近似方法。

### 核心思想：用“近似的[线性](@keyword=linearity|lang=zh-CN|style=Feynman)”来驯服[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)

[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)的核心思想是一种优雅的妥协。它没有试图去完全征服[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)的所有复杂细节，而是问了一个更聪明的问题：在一个[持续振荡](@keyword=sustained_oscillations|lang=zh-CN|style=Feynman)的系统中，[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)环节对于“主导”[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的那个频率分量，到底起到了什么样的作用？

想象一下，一个[反馈回路](@keyword=feedback_loops|lang=zh-CN|style=Feynman)中存在一个[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件。如果系统正在发生一种稳定的、[周期性](@keyword=periodicity|lang=zh-CN|style=Feynman)的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)（[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)），那么在回路中流动的信号，其最主要的成分很可能是一个特定频率的[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)。我们可以大胆地做出一个“[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)猜想”：假设输入到[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件的信号就是一个纯净的[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)，形如 $x(t) = A\sin(\omega t)$。

当然，[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件会“[扭曲](@keyword=distortion|lang=zh-CN|style=Feynman)”这个[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)，输出一个同样[周期性](@keyword=periodicity|lang=zh-CN|style=Feynman)但外形复杂的波形 $y(t)$。根据[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)的伟大思想，任何一个周期波都可以被看作是无穷多个不同频率、不同[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)的[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)（[谐波](@keyword=harmonics|lang=zh-CN|style=Feynman)）的[叠加](@keyword=superposition|lang=zh-CN|style=Feynman)。也就是说，输出信号 $y(t)$ 中除了包含与输入同频率的“基波”外，还包含了频率为 $2\omega$, $3\omega$, $4\omega$… 的“高[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)”。

这时，奇迹发生了。在大多数[控制系统](@keyword=control_systems|lang=zh-CN|style=Feynman)中，[线性](@keyword=linearity|lang=zh-CN|style=Feynman)部分 $G(s)$ 都扮演着一个天然的“[滤波器](@keyword=frequency_filter|lang=zh-CN|style=Feynman)”角色。它就像一个严谨的“音乐品鉴师”，对不同频率的信号有着不同的“偏好”。通常，它对低频信号“青睐有加”，而对高频信号则“拒之门外”。这种特性被称为**低通滤波**。

因此，当包含着丰富[谐波](@keyword=harmonics|lang=zh-CN|style=Feynman)的信号 $y(t)$ 流经[线性](@keyword=linearity|lang=zh-CN|style=Feynman)环节 $G(s)$ 时，那些高[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)（$2\omega$, $3\omega$…）会被大幅削弱，而基波（$\omega$）则能相对轻松地通过。最终，流回[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件输入端的信号，又变回了一个近似纯净的[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)。这使得我们最初的“[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)猜想”形成了一个自洽的闭环。这个至关重要的假设，我们称之为“**[滤波器](@keyword=frequency_filter|lang=zh-CN|style=Feynman)假设**” ([@problem_id:1569538])。

这个假设有多可靠？我们可以定量地检验它。比如，对于一个由[理想](@keyword=ideals|lang=zh-CN|style=Feynman)继电器（一种简单的开关式[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件）和一个一阶[低通滤波器](@keyword=low_pass_filter|lang=zh-CN|style=Feynman) $G(s) = K/(Ts+1)$ 组成的系统，我们可以精确计算出在[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件输入端，三[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)与基波的[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)之比。这个比值是 $\frac{1}{3} \frac{\sqrt{1+(T\omega)^2}}{\sqrt{1+(3T\omega)^2}}$ ([@problem_id:1569533])。你会发现，当频率 $\omega$ 较高或者[时间常数](@keyword=time_constant|lang=zh-CN|style=Feynman) $T$ 较大时，这个比值会远小于1，说明高[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)被有效地“[过滤](@keyword=filtrations|lang=zh-CN|style=Feynman)”掉了，[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)此时会相当准确。

反之，如果[线性](@keyword=linearity|lang=zh-CN|style=Feynman)环节 $G(s)$ 不是一个好的[低通滤波器](@keyword=low_pass_filter|lang=zh-CN|style=Feynman)，[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)就可能失效。一个典型的例子是带​​有[谐振峰](@keyword=resonant_peak|lang=zh-CN|style=Feynman)的轻[阻尼](@keyword=damping|lang=zh-CN|style=Feynman)[二阶系统](@keyword=second_order_systems|lang=zh-CN|style=Feynman) ([@problem_id:1569539])。如果某个高[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)的频率恰好落在了这个系统的[谐振频率](@keyword=resonant_frequency|lang=zh-CN|style=Feynman)附近，它不仅不会被[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)，反而会被放大！这样一来，反馈回来的信号就会严重偏离[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)，我们最初的假设就土崩瓦解了。这提醒我们，任何强大的工具都有其适用边界。

### 描述函数 $N(A)$：[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)的“身份证”

在确认了[滤波器](@keyword=frequency_filter|lang=zh-CN|style=Feynman)假设的合理性之后，我们就可以专注于基波了。我们忽略所有高[次谐波](@keyword=subharmonic|lang=zh-CN|style=Feynman)，只关心[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件是如何“改造”输入信号的基波分量的。描述函数 $N(A)$ 就是用来描述这种“改造”的数学工具。它被定义为一个[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)，其**模** $|N(A)|$ 表示输出信号中基波分量的[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)与输入信号[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)的比值（一种“[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)增益”）；其**[相角](@keyword=phase_angle|lang=zh-CN|style=Feynman)** $\arg(N(A))$ 表示输出基波相对于输入的[相位移](@keyword=phase_shift|lang=zh-CN|style=Feynman)动。

$$
N(A) = \frac{\text{输出信号中基波分量的[相量](@keyword=phasors|lang=zh-CN|style=Feynman)}}{\text{输入信号的[相量](@keyword=phasors|lang=zh-CN|style=Feynman)}}
$$

为什么是[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)？因为它需要同时捕捉增益和相位这两个信息。想象一下，一个[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)在[极坐标](@keyword=polar_coordinates|lang=zh-CN|style=Feynman)下既有长度（模），又有角度（[相角](@keyword=phase_angle|lang=zh-CN|style=Feynman)）。这完美地对应了我们的需求。

描述函数的具体形式完全取决于[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件自身的特性，它就像是每个[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件独一无二的“身份证”。

-   **当 $N(A)$ 是纯[实数](@keyword=real_numbers|lang=zh-CN|style=Feynman)时**：这意味着什么？一个纯[实数](@keyword=real_numbers|lang=zh-CN|style=Feynman)（非零）的[相角](@keyword=phase_angle|lang=zh-CN|style=Feynman)是 $0^\circ$ 或 $180^\circ$。这说明输出的基波与输入要么完全同相，要么完全反相，不存在时间上的延迟。这种情况通常发生在“无记忆”的[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件中，比如一个[理想](@keyword=ideals|lang=zh-CN|style=Feynman)的饱和放大器或具有奇[对称性](@keyword=symmetry|lang=zh-CN|style=Feynman)（$f(-x) = -f(x)$）的元件。它们的输出在任何时刻都只取决于同一时刻的输入，没有任何“历史包袱”。因此，输出波形虽然被[扭曲](@keyword=distortion|lang=zh-CN|style=Feynman)，但其基波的过[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)、峰值点都与输入保持[同步](@keyword=synchronization|lang=zh-CN|style=Feynman)，没有产生[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman) ([@problem_id:1569509])。

-   **当 $N(A)$ 是[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)时**：一个非纯[实数](@keyword=real_numbers|lang=zh-CN|style=Feynman)的[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)意味着[相角](@keyword=phase_angle|lang=zh-CN|style=Feynman)不为零。这说明输出基波相对于输入产生了[相位滞后](@keyword=phase_lag|lang=zh-CN|style=Feynman)或超前。这通常发生在具有“[记忆效应](@keyword=memory_effect|lang=zh-CN|style=Feynman)”或“迟滞”（hysteresis）的[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)环节中。一个绝佳的例子是机械系统中的**[齿隙](@keyword=backlash|lang=zh-CN|style=Feynman)**（backlash）。当你[转动](@keyword=rotational_motion|lang=zh-CN|style=Feynman)一个有[间隙](@keyword=backlash|lang=zh-CN|style=Feynman)的齿轮组时，在改变方向的瞬间，主动轮需要空转一小段距离才能重新带动从动轮。这个“空转”的过程就是一个时间延迟。这个时间延迟反映在[频域](@keyword=frequency_space|lang=zh-CN|style=Feynman)上，就是[相位滞后](@keyword=phase_lag|lang=zh-CN|style=Feynman)。因此，[齿隙](@keyword=backlash|lang=zh-CN|style=Feynman)的描述函数必然是一个[复数](@keyword=complex_numbers|lang=zh-CN|style=Feynman)，其[虚部](@keyword=imaginary_part|lang=zh-CN|style=Feynman)就代表了这种由物理延迟所导致的[相位变化](@keyword=phase_variation|lang=zh-CN|style=Feynman) ([@problem_gpid_1569525])。

-   **当 $N(A)$ 是纯虚数时**：这意味着[相位移](@keyword=phase_shift|lang=zh-CN|style=Feynman)动恰好是 $\pm 90^\circ$ ([@problem_id:1569527])。这种关系在物理世界中也很有趣，类似于[理想](@keyword=ideals|lang=zh-CN|style=Feynman)[电感](@keyword=inductance|lang=zh-CN|style=Feynman)或[电容](@keyword=capacitance|lang=zh-CN|style=Feynman)中[电压](@keyword=voltage|lang=zh-CN|style=Feynman)与[电流](@keyword=electric_current|lang=zh-CN|style=Feynman)的关系，暗示了一种纯粹的能量存储与释放过程，而不是简单的增益或延迟。

### [谐波平衡](@keyword=harmonic_balance|lang=zh-CN|style=Feynman)：一场精妙的“共舞”

现在，我们有了描述[线性](@keyword=linearity|lang=zh-CN|style=Feynman)部分的 $G(j\omega)$ 和近似描述[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)部分的 $N(A)$。[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)，这个自我维持的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，是如何诞生的呢？

在一个[负反馈回路](@keyword=negative_feedback_loops|lang=zh-CN|style=Feynman)中，信号从某一点出发，经过[线性](@keyword=linearity|lang=zh-CN|style=Feynman)环节 $G(s)$，其[幅度和相位](@keyword=magnitude_and_phase|lang=zh-CN|style=Feynman)会根据 $G(j\omega)$ 发生改变；接着，它穿过[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)环节，其基波分量又根据 $N(A)$ 再次被改变。为了形成一个稳定的、周而复始的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，这个信号在绕行一圈回到起点时，必须与它出发时一模一样。

用数学的语言来说，整个环路的总增益必须为 1，总[相移](@keyword=phase_shifts|lang=zh-CN|style=Feynman)必须是 $360^\circ$ 的整数倍。对于一个标准的负[反馈系统](@keyword=feedback_systems|lang=zh-CN|style=Feynman)，这意味着[环路增益](@keyword=loop_gain|lang=zh-CN|style=Feynman) $G(j\omega)N(A)$ 必须等于 $-1$。

$$
G(j\omega)N(A) = -1 \quad \text{或者} \quad G(j\omega) = -\frac{1}{N(A)}
$$

这个简洁的方程被称为“**[谐波平衡方程](@keyword=harmonic_balance_equation|lang=zh-CN|style=Feynman)**”，它是[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)的灵魂。这个方程美妙地将两个看似无关的世界联系在了一起：
-   方程的左边，$G(j\omega)$，只与**频率 $\omega$** 有关，它由系统的[线性](@keyword=linearity|lang=zh-CN|style=Feynman)部分决定。
-   方程的右边，$-1/N(A)$，只与**[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) $A$** 有关，它由系统的[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)部分决定。

一个[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)的存在，就是这两个世界达成“共识”的时刻。它意味着，系统能够找到一个特定的频率 $\omega_0$ 和一个特定的[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) $A_0$，使得上述等式精确成立。

这个方程不仅能预测，还能进行“推理”。想象我们是系统侦探，在现场发现了一个稳定的[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)，并测得其[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)为 $A_0=2$, 频率为 $\omega_0=5$ rad/s。我们还知道[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)环节是一个具有特定参数的[磁滞](@keyword=magnetic_hysteresis|lang=zh-CN|style=Feynman)继电器。那么，[线性](@keyword=linearity|lang=zh-CN|style=Feynman)部分 $G(j\omega_0)$ 在那个频率下的响应是什么样的呢？我们可以通过计算 $-1/N(A_0)$ 来“反推出”$G(j\omega_0)$ 的值，就好像根据现场的指纹来确定嫌疑人的身份一样 ([@problem_id:1569534])。

更普遍的应用是预测。我们可以在一个[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)上，画出两条曲线：一条是[线性](@keyword=linearity|lang=zh-CN|style=Feynman)环节的[奈奎斯特图](@keyword=nyquist_plot|lang=zh-CN|style=Feynman)（Nyquist plot），即 $G(j\omega)$ 随着 $\omega$ 从 0 到无穷大变化的[轨迹](@keyword=trajectory|lang=zh-CN|style=Feynman)；另一条是 $-1/N(A)$ 随着[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) $A$ 从 0 到无穷大变化的[轨迹](@keyword=trajectory|lang=zh-CN|style=Feynman)。**如果这两条曲线存在交点，那么这个交点就对应着一个可能的[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)！** 交点处的 $\omega$ 值就是[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)的频率，而对应的 $A$ 值就是其[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) ([@problem_id:1569526]) [@problem_id:1569562]。这是一种极为强大和直观的图形分析方法。

### 稳定还是不稳定：最后的审判

找到交点就万事大吉了吗？还没有。这个预测出的[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)是稳定的还是不稳定的？一个**稳定[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)**就像一个碗底的弹珠，系统会自发地趋向于这种[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)状态，即使受到轻微扰动也能恢复。而一个**不稳定[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)**则像铅笔尖上的[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)，理论上存在，但任何微小的扰动都会让系统远离它。显然，在实际工程中我们只关心那些能够稳定存在的[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)。

如何判断稳定性？我们可以借助奈奎斯特稳定判据的思想，进行一种巧妙的“局部”分析。直观地讲，我们观察 $-1/N(A)$ 曲线是如何“穿越”$G(j\omega)$ 曲线的。

-   如果当[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) $A$ 增大时，$-1/N(A)$ 曲线是从 $G(j\omega)$ 曲线所包围的“不[稳定区域](@keyword=stability_regions|lang=zh-CN|style=Feynman)”进入“[稳定区域](@keyword=stability_regions|lang=zh-CN|style=Feynman)”，那么这个[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)就是**稳定**的 ([@problem_id:1569553])。这背后的物理含义是：当[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)小于[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman) $A_0$ 时，系统等效于一个不稳定的[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)，[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)会自发增长，向 $A_0$ 靠近；当[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)大于 $A_0$ 时，系统等效于一个稳定的[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)，[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)会[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)，也向 $A_0$ 靠近。一增一减，系统就被“锁定”在了 $A_0$ 这个稳定的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)[幅度](@keyword=amplitude|lang=zh-CN|style=Feynman)上。

-   反之，如果穿越方向相反，[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)就是**不稳定**的。

至此，我们已经走过了[描述函数法](@keyword=describing_function_method|lang=zh-CN|style=Feynman)的整个思想旅程。从一个巧妙的近似出发，通过[滤波器](@keyword=frequency_filter|lang=zh-CN|style=Feynman)假设简化问题，用描述函数 $N(A)$ 给[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)元件建立数学模型，再利用[谐波平衡方程](@keyword=harmonic_balance_equation|lang=zh-CN|style=Feynman) $G(j\omega) = -1/N(A)$ 预测[极限环](@keyword=limit_cycles|lang=zh-CN|style=Feynman)的存在，最后通过[稳定性判据](@keyword=stability_criteria|lang=zh-CN|style=Feynman)来确认其物理意义。这套方法将一个原本棘手的[非线性](@keyword=nonlinearity|lang=zh-CN|style=Feynman)问题，转化成了一个我们熟悉的、可以在[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)上直观求解的图形问题，充分展现了工程与科学中化繁为简的艺术与智慧。

