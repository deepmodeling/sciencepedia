## Introduction
Quadrature Mirror Filter (QMF) banks are a cornerstone of modern [digital signal processing](@entry_id:263660), providing a powerful framework for decomposing a signal into frequency subbands and subsequently reconstructing it. Their importance spans numerous fields, from audio compression to telecommunications, where efficient [signal representation](@entry_id:266189) is paramount. However, the process of splitting, downsampling, and recombining signals introduces significant challenges, namely aliasing and other forms of distortion. This article addresses the fundamental question of how to design a [filter bank](@entry_id:271554) that perfectly cancels these artifacts to achieve high-fidelity reconstruction.

Throughout the following chapters, you will gain a comprehensive understanding of this critical technology. We will begin in **Principles and Mechanisms** by dissecting the two-channel analysis-synthesis architecture, analyzing the mathematical origins of [aliasing](@entry_id:146322), and establishing the conditions for [perfect reconstruction](@entry_id:194472). Then, in **Applications and Interdisciplinary Connections**, we will explore how these theoretical concepts are leveraged in practical subband coding systems and how they provide the computational engine for the Discrete Wavelet Transform. Finally, you will apply this knowledge in **Hands-On Practices**, working through exercises to design and analyze the core components of a QMF system. This structured journey will equip you with the foundational knowledge to understand and utilize multirate [filter banks](@entry_id:266441) in advanced signal processing applications.

## Principles and Mechanisms

A Quadrature Mirror Filter (QMF) bank is a fundamental [multirate signal processing](@entry_id:196803) structure designed to decompose a signal into multiple frequency bands, known as subbands, and subsequently reconstruct the original signal from them. This process of decomposition and reconstruction is central to a vast array of applications, from audio and [image compression](@entry_id:156609) to communications and [feature extraction](@entry_id:164394). This chapter elucidates the core principles governing the behavior of the most common configuration: the [two-channel filter bank](@entry_id:186662). We will dissect its architecture, analyze the artifacts introduced by rate changes, and establish the precise conditions required for perfect [signal reconstruction](@entry_id:261122).

### The Two-Channel Analysis-Synthesis Framework

The canonical [two-channel filter bank](@entry_id:186662) consists of two primary stages: an **analysis stage** and a **synthesis stage**.

In the analysis stage, the input signal $x[n]$ is split into two paths. In the upper path, it is processed by a [low-pass filter](@entry_id:145200) with impulse response $h_0[n]$ and transfer function $H_0(z)$. In the lower path, it is processed by a high-pass filter with impulse response $h_1[n]$ and transfer function $H_1(z)$. The filtered signals are then **downsampled** by a factor of two. Downsampling, also known as decimation, is the process of retaining only every $M$-th sample of a sequence; here, $M=2$. The resulting signals, $v_0[n]$ and $v_1[n]$, represent the low-frequency and high-frequency content of the input, respectively, but at half the original sampling rate.

The synthesis stage is designed to reverse this process. The subband signals $v_0[n]$ and $v_1[n]$ are first **upsampled** by a factor of two. Upsampling, or interpolation, involves inserting $M-1$ zero-valued samples between each sample of the sequence. The upsampled signals are then passed through synthesis filters, $G_0(z)$ for the low-pass channel and $G_1(z)$ for the high-pass channel. Finally, the outputs of these filters are summed to produce the reconstructed signal, $\hat{x}[n]$.

A critical design consideration is the ordering of operations. One might question why the signal is filtered *before* being downsampled in the analysis stage. The operations of filtering and downsampling are not, in general, commutative. Interchanging them produces a different result. Consider a system where an input is first downsampled by two and then filtered, versus a system where it is first filtered and then downsampled. As demonstrated in a direct calculation [@problem_id:1746330], the outputs of these two configurations are not identical. The standard filter-then-downsample structure is chosen because it allows for the removal of high-frequency content that would otherwise cause [aliasing](@entry_id:146322) upon downsampling.

To understand the system's behavior, we must analyze it in the frequency domain. Let $X(z)$ be the Z-transform of the input signal $x[n]$. The output of the analysis stage, after downsampling by two, can be expressed in the Z-domain as:
$$V_k(z) = \frac{1}{2} \left[ H_k(z^{1/2})X(z^{1/2}) + H_k(-z^{1/2})X(-z^{1/2}) \right], \quad k \in \{0, 1\}$$

Subsequently, [upsampling](@entry_id:275608) and filtering in the synthesis stage leads to the Z-transform of the final reconstructed signal, $\hat{X}(z)$:
$$\hat{X}(z) = G_0(z)V_0(z^2) + G_1(z)V_1(z^2)$$

Substituting the expressions for $V_0(z^2)$ and $V_1(z^2)$ and rearranging terms yields the fundamental equation of the [two-channel filter bank](@entry_id:186662):
$$\hat{X}(z) = \frac{1}{2} \left[ G_0(z)H_0(z) + G_1(z)H_1(z) \right] X(z) + \frac{1}{2} \left[ G_0(z)H_0(-z) + G_1(z)H_1(-z) \right] X(-z)$$

This equation reveals that the output $\hat{x}[n]$ is composed of two components. The first term, proportional to $X(z)$, represents a linearly distorted version of the original signal. The second term, proportional to $X(-z)$, represents an aliased version of the signal. The term $X(-z)$ corresponds to modulating the time-domain signal $x[n]$ by $(-1)^n$, which reflects the spectrum around $\omega = \pi/2$. We can write this relationship more compactly as:
$$\hat{X}(z) = T(z)X(z) + A(z)X(-z)$$
where $T(z)$ is the **distortion transfer function** and $A(z)$ is the **[aliasing](@entry_id:146322) transfer function** [@problem_id:1746329].

An immediate consequence of this structure is that the overall system from $x[n]$ to $\hat{x}[n]$ is not, in general, Linear Time-Invariant (LTI). The presence of the $X(-z)$ term, arising from the multirate operations, makes the system Linear Periodically Time-Varying (LPTV) with a period of 2. However, if the filters are designed such that the aliasing transfer function is identically zero, i.e., $A(z) = 0$, the relationship simplifies to $\hat{X}(z) = T(z)X(z)$. In this case, and only in this case, the entire system behaves as a single LTI system [@problem_id:1746374]. This is a primary goal of [filter bank](@entry_id:271554) design.

### Designing the Analysis Filters: The Quadrature Mirror Property

The first step toward a functional [filter bank](@entry_id:271554) is the design of the analysis filters, $H_0(z)$ and $H_1(z)$. A simple yet powerful method for creating the [high-pass filter](@entry_id:274953) $H_1(z)$ from a low-pass prototype $H_0(z)$ is the **quadrature mirror** relationship.

In the time domain, this relationship is defined by modulating the low-pass impulse response $h_0[n]$ by the sequence $(-1)^n$:
$$h_1[n] = (-1)^n h_0[n]$$
Since $(-1)^n = e^{j\pi n}$, this [modulation](@entry_id:260640) corresponds to a frequency shift in the Discrete-Time Fourier Transform (DTFT). Specifically, if $H_0(e^{j\omega})$ is the DTFT of $h_0[n]$, the DTFT of $h_1[n]$ is given by:
$$H_1(e^{j\omega}) = H_0(e^{j(\omega-\pi)})$$
In the Z-domain, this corresponds to the substitution $z \to -z$, yielding the compact relationship:
$$H_1(z) = H_0(-z)$$
This transformation effectively shifts the [frequency response](@entry_id:183149) of the low-pass filter by $\pi$ radians, converting it into a [high-pass filter](@entry_id:274953) [@problem_id:1746332].

This design gives the QMF bank its name. For a filter $H_0(z)$ with real coefficients, its magnitude response is an even function, i.e., $|H_0(e^{j\omega})| = |H_0(e^{-j\omega})|$. The magnitude response of the [high-pass filter](@entry_id:274953) is then:
$$|H_1(e^{j\omega})| = |H_0(e^{j(\omega-\pi)})| = |H_0(e^{-j(\omega-\pi)})| = |H_0(e^{j(\pi-\omega)})|$$
This equation [@problem_id:1746343] shows that the magnitude response $|H_1(e^{j\omega})|$ for $\omega \in [0, \pi]$ is a mirror image of the magnitude response $|H_0(e^{j\omega})|$ reflected about the **quadrature frequency** $\omega = \pi/2$.

For instance, if a low-pass prototype $H_0(z)$ has a [passband](@entry_id:276907) edge at $\omega_{p,0}$ and a [stopband](@entry_id:262648) edge at $\omega_{s,0}$, the corresponding high-pass filter $H_1(z) = H_0(-z)$ will have its critical frequencies mirrored. Its stopband will begin at $\pi - \omega_{s,0}$ and its passband will begin at $\pi - \omega_{p,0}$. If $H_0(z)$ had a [passband](@entry_id:276907) edge of $\omega_{p,0} = \pi/4$ and a stopband edge of $\omega_{s,0} = \pi/3$, the derived high-pass filter $H_1(z)$ would have a stopband edge of $\omega_{s,1} = \pi - \pi/3 = 2\pi/3$ and a passband edge of $\omega_{p,1} = \pi - \pi/4 = 3\pi/4$ [@problem_id:1746384].

The necessity for careful [filter design](@entry_id:266363) becomes apparent when considering the effect of downsampling on signals whose frequencies are not confined to the low-pass band. If a pure sinusoid with frequency $\omega_0 > \pi/2$ (the folding frequency for downsampling by 2) enters the low-pass branch, the non-ideal nature of the filter means some of this signal will pass through. Upon downsampling, this component will be aliased into the baseband $[0, \pi/2]$. For example, an input signal $x[n] = \cos(\frac{2\pi}{3}n)$ entering the low-pass branch and then being downsampled by 2 will result in a component at frequency $2 \times \frac{2\pi}{3} = \frac{4\pi}{3}$, which is aliased to $\frac{4\pi}{3} - 2\pi = -\frac{2\pi}{3}$. Due to the symmetry of the cosine, this appears as an undesired [sinusoid](@entry_id:274998) at frequency $2\pi/3$ at the output of the low-pass channel [@problem_id:1746333]. It is precisely this type of [aliasing](@entry_id:146322) that the full QMF synthesis stage is designed to cancel.

### Conditions for Reconstruction

The ultimate goal of a [filter bank](@entry_id:271554) is often **perfect reconstruction (PR)**, where the output is simply a scaled and delayed version of the input, i.e., $\hat{x}[n] = c \cdot x[n-d]$ for some constant gain $c$ and integer delay $d$. This requires satisfying two conditions:
1.  **Aliasing Cancellation**: The aliasing transfer function must be zero, $A(z) = 0$.
2.  **Distortion Elimination**: The distortion transfer function must be a simple delay, $T(z) = c \cdot z^{-d}$.

#### Aliasing Cancellation

The general condition for [aliasing cancellation](@entry_id:262830) is:
$$A(z) = \frac{1}{2} \left[ G_0(z)H_0(-z) + G_1(z)H_1(-z) \right] = 0$$
Let's adopt the QMF analysis filter choice, $H_1(z) = H_0(-z)$. A common selection for the synthesis filters that satisfies the [aliasing cancellation](@entry_id:262830) condition is:
$$G_0(z) = 2H_0(z), \quad G_1(z) = -2H_1(z) = -2H_0(-z)$$
Substituting these into the expression for $A(z)$ gives:
$$A(z) = \frac{1}{2} \left[ (2H_0(z))H_0(-z) + (-2H_0(-z))H_0(z) \right] = H_0(z)H_0(-z) - H_0(-z)H_0(z) = 0$$
This choice of filters elegantly cancels all [aliasing](@entry_id:146322) artifacts, making the overall system LTI [@problem_id:1746367].

#### The Challenge of Distortion

With aliasing removed, we are left with an LTI system whose transfer function is $T(z)$. Using the same filter choices, the distortion transfer function becomes:
$$T(z) = \frac{1}{2} \left[ G_0(z)H_0(z) + G_1(z)H_1(z) \right] = \frac{1}{2} \left[ (2H_0(z))H_0(z) + (-2H_0(-z))H_0(-z) \right]$$
$$T(z) = H_0(z)^2 - H_0(-z)^2$$
For [perfect reconstruction](@entry_id:194472), we would require $T(z) = c z^{-d}$. Unfortunately, for any real, causal, non-trivial FIR filter $H_0(z)$, this condition cannot be met. This represents the fundamental limitation of the classic QMF design.

To see why, consider the hypothetical case where $H_0(z)$ is an ideal zero-phase "brick-wall" low-pass filter with a cutoff at $\pi/2$. Its [frequency response](@entry_id:183149) $H_0(e^{j\omega})$ is 1 for $|\omega|  \pi/2$ and 0 for $|\omega| > \pi/2$. The response of the high-pass filter, $H_0(e^{j(\omega-\pi)})$, would be 0 for $|\omega|  \pi/2$ and 1 for $|\omega| > \pi/2$. The overall distortion [frequency response](@entry_id:183149) $T(e^{j\omega}) = (H_0(e^{j\omega}))^2 - (H_0(e^{j(\omega-\pi)}))^2$ would then be:
$$T(e^{j\omega}) = \begin{cases} 1^2 - 0^2 = 1,  |\omega|  \frac{\pi}{2} \\ 0^2 - 1^2 = -1,  \frac{\pi}{2}  |\omega| \le \pi \end{cases}$$
This response is far from a constant gain; it introduces severe magnitude distortion, passing low frequencies with gain 1 and high frequencies with gain -1 (a phase shift) [@problem_id:1746363]. While ideal filters are not realizable, this thought experiment shows that even in the best-case scenario for frequency separation, this QMF structure inherently introduces distortion. Practical QMF designs seek to find a filter $H_0(z)$ that minimizes this distortion, but they cannot eliminate it entirely.

#### Achieving Perfect Reconstruction (PR)

To achieve true [perfect reconstruction](@entry_id:194472), we must abandon the simple QMF filter choices and select all four filters to simultaneously satisfy both PR conditions. This leads to the field of **Perfect Reconstruction Filter Banks**.

Let's examine the conditions with a simple, concrete example. Consider a 2-tap FIR filter prototype $H_0(z) = \alpha + \beta z^{-1}$. We use the standard analysis high-pass filter $h_1[n]=(-1)^n h_0[n]$, so $H_1(z) = \alpha - \beta z^{-1}$. For the synthesis stage, let's choose the filters $G_0(z) = \beta + \alpha z^{-1}$ and $G_1(z) = -\beta + \alpha z^{-1}$. By substituting these into the [aliasing](@entry_id:146322) and distortion transfer functions, we find that aliasing is cancelled if $\alpha^2 = \beta^2$, and the distortion term becomes $T(z) = (\alpha^2 + \beta^2)z^{-1}$. To achieve PR with unity gain, we must have $\alpha^2 + \beta^2 = 1$. Solving these two conditions simultaneously gives $\alpha^2 = 1/2$. A valid solution is $\alpha = \beta = 1/\sqrt{2}$, which defines the Haar analysis filter, a cornerstone of [wavelet theory](@entry_id:197867) [@problem_id:1746375].

This example reveals that perfect reconstruction is indeed possible with a more sophisticated set of filter relationships. A general class of PR [filter banks](@entry_id:266441) can be constructed using the following relations for an FIR filter $H_0(z)$ of length $N$:
- $H_1(z) = c z^{-(N-1)} H_0(-z^{-1})$ (High-pass analysis)
- $G_0(z) = z^{-(N-1)} H_0(z^{-1})$ (Low-pass synthesis)
- $G_1(z) = z^{-(N-1)} H_1(z^{-1})$ (High-pass synthesis)

Substituting these into the PR conditions reveals that aliasing is automatically cancelled. The distortion condition simplifies to a requirement on the prototype filter $H_0(z)$ alone, known as the **power-complementary condition**:
$$H_0(z)H_0(z^{-1}) + H_0(-z)H_0(-z^{-1}) = K$$
where $K$ is a constant. The term $P(z) = H_0(z)H_0(z^{-1})$ is the Z-transform of the autocorrelation of the filter's impulse response. The condition states that the sum of this function and its spectrally-flipped version must be constant. This condition is the key to designing a wide variety of practical PR [filter banks](@entry_id:266441). For example, by imposing this condition, along with constraints on the DC gain, one can uniquely determine the coefficients for filters of a given length, such as the 3-tap FIR [filter design](@entry_id:266363) explored in [@problem_id:1731862], which also leads to a Haar basis filter.

In summary, the design of a Quadrature Mirror Filter bank is a study in trade-offs. The multirate nature of the system introduces aliasing, which can be elegantly canceled by defining the [high-pass filter](@entry_id:274953) as a modulated version of the low-pass prototype. However, this classic QMF design is fundamentally unable to achieve perfect reconstruction with FIR filters due to residual amplitude and [phase distortion](@entry_id:184482). By employing more intricate relationships between the four filters in the bank, it is possible to create Perfect Reconstruction systems that cancel all [aliasing](@entry_id:146322) and distortion, paving the way for high-fidelity [signal analysis](@entry_id:266450) and compression.