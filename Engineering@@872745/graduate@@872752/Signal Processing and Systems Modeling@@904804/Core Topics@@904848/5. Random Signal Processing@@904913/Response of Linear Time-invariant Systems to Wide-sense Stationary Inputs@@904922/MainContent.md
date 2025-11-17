## Introduction
In the study of signal processing and systems, we often begin with [deterministic signals](@entry_id:272873) whose behavior is perfectly predictable. However, the real world is inherently stochastic, filled with random noise, unpredictable information streams, and complex environmental phenomena. A fundamental challenge, therefore, is to understand how these [random signals](@entry_id:262745) behave when processed by standard engineering systems. This article addresses this challenge by focusing on the interaction between two foundational concepts: [wide-sense stationary](@entry_id:144146) (WSS) random processes, which model a vast class of statistically stable signals, and linear time-invariant (LTI) systems, the building blocks of modern signal processing.

The central question we explore is: how does an LTI system transform the statistical character of a WSS input? Answering this provides the key to designing effective noise filters, modeling complex signals, and identifying unknown system dynamics from observed data. This article is structured to guide you from theoretical foundations to practical mastery. The first chapter, **Principles and Mechanisms**, derives the cornerstone mathematical relationships that govern the output's [power spectrum](@entry_id:159996) and [autocorrelation](@entry_id:138991). We will then explore the broad utility of these principles in **Applications and Interdisciplinary Connections**, demonstrating their use in fields ranging from communications to control theory. Finally, **Hands-On Practices** will offer a chance to solidify your understanding by working through concrete design and analysis problems.

We begin our investigation by delving into the core principles that dictate the statistical relationship between a system's input and its output.

## Principles and Mechanisms

Having established the foundational concepts of [wide-sense stationary](@entry_id:144146) (WSS) processes in the previous chapter, we now investigate their interaction with a cornerstone of signal processing: the Linear Time-Invariant (LTI) system. This chapter delves into the principles and mechanisms that govern the statistical properties of a system's output when its input is a WSS [random process](@entry_id:269605). Our primary objective is to develop a quantitative framework for understanding how an LTI system transforms the spectral and temporal characteristics of [random signals](@entry_id:262745).

### The Fundamental Input-Output Relationship for Power Spectra

The most crucial result in the analysis of [random signals](@entry_id:262745) in LTI systems is the relationship between the [power spectral density](@entry_id:141002) (PSD) of the input and output signals. Let us consider a continuous-time LTI system with a deterministic, stable impulse response $h(t)$. The system's output, $y(t)$, in response to an input signal $x(t)$, is given by the convolution integral:

$y(t) = \int_{-\infty}^{\infty} h(\alpha) x(t - \alpha) \, d\alpha$

Now, let the input $x(t)$ be a zero-mean, [wide-sense stationary process](@entry_id:204592). A natural question arises: what are the statistical properties of the output $y(t)$? We can begin to answer this by examining the output's [autocorrelation function](@entry_id:138327), $R_{y}(\tau) = \mathbb{E}[y(t+\tau)y^{*}(t)]$. By substituting the convolution integral and assuming that the expectation and integration operators can be interchanged (a condition guaranteed by system stability), we can derive the relationship from first principles [@problem_id:2901260].

$R_{y}(\tau) = \mathbb{E}\left[ \left( \int_{-\infty}^{\infty} h(\alpha) x(t+\tau-\alpha) \, d\alpha \right) \left( \int_{-\infty}^{\infty} h^{*}(\beta) x^{*}(t-\beta) \, d\beta \right) \right]$

$R_{y}(\tau) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} h(\alpha) h^{*}(\beta) \mathbb{E}[x(t+\tau-\alpha)x^{*}(t-\beta)] \, d\alpha \, d\beta$

Since $x(t)$ is WSS, the expectation term is simply the input autocorrelation function evaluated at the time lag $(\tau - \alpha + \beta)$.
$\mathbb{E}[x(t+\tau-\alpha)x^{*}(t-\beta)] = R_{x}(\tau - \alpha + \beta)$.

This gives the output autocorrelation as a double convolution involving the system's impulse response and the input's [autocorrelation](@entry_id:138991). While correct, this expression is cumbersome. A more insightful relationship emerges in the frequency domain. By applying the Wiener-Khinchin theorem, which equates the PSD with the Fourier transform of the autocorrelation function, we find a remarkably simple and powerful result. The Fourier transform of this complex convolutional expression yields:

$S_{y}(\omega) = S_{x}(\omega) H(\omega) H^{*}(\omega) = S_{x}(\omega) |H(\omega)|^{2}$

where $S_{x}(\omega)$ and $S_{y}(\omega)$ are the power spectral densities of the input and output, respectively, and $H(\omega)$ is the frequency response of the LTI system. This equation is the cornerstone of our analysis. It states that the **output power spectral density is the product of the input power spectral density and the magnitude-squared of the system's frequency response**. The term $|H(\omega)|^{2}$ is often called the system's **power transfer function** or **power gain**, as it describes how the system scales the power of the input signal at each frequency.

### The Decisive Role of Magnitude Response

A profound implication of the fundamental PSD relationship is that the second-[order statistics](@entry_id:266649) of the output process—its PSD and, by extension, its [autocorrelation function](@entry_id:138327)—depend *only* on the **magnitude response** $|H(\omega)|$ of the filter. The phase of the frequency response, $\arg\{H(\omega)\}$, plays no role in shaping the output's power spectrum.

To illustrate this, consider a thought experiment involving two distinct LTI filters, $H_{1}(\omega)$ and $H_{2}(\omega)$, designed such that their magnitude responses are identical, $|H_{1}(\omega)| = |H_{2}(\omega)|$, but their phase responses differ. If the same WSS process $x(t)$ is passed through both filters, the resulting output processes, $y_{1}(t)$ and $y_{2}(t)$, will have identical power spectral densities:

$S_{y_{1}}(\omega) = S_{x}(\omega) |H_{1}(\omega)|^{2} = S_{x}(\omega) |H_{2}(\omega)|^{2} = S_{y_{2}}(\omega)$

Since the [autocorrelation function](@entry_id:138327) is the inverse Fourier transform of the PSD, it follows that their [autocorrelation](@entry_id:138991) functions, $R_{y_{1}}(\tau)$ and $R_{y_{2}}(\tau)$, must also be identical. If the input is a Gaussian process, this means the two output processes have identical second-[order statistics](@entry_id:266649). However, it is crucial to recognize that the output *[sample paths](@entry_id:184367)* $y_{1}(t)$ and $y_{2}(t)$ will generally be different, because the different phase responses correspond to different impulse responses, $h_{1}(t) \neq h_{2}(t)$ [@problem_id:2901266]. This highlights a critical distinction between the statistical (ensemble) properties of a process and its individual realizations.

### Computing Output Power and the Effect of Filtering

The average power of a zero-mean WSS process is given by its variance, which is equal to the value of its autocorrelation function at zero lag, $R_{y}(0)$. Using the inverse Wiener-Khinchin relation, this can be expressed as an integral of the PSD over all frequencies:

$P_{y} = \sigma_{y}^{2} = R_{y}(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_{y}(\omega) \, d\omega = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_{x}(\omega) |H(\omega)|^{2} \, d\omega$

This formula allows us to compute the total power of the output signal by examining how the filter's power gain $|H(\omega)|^{2}$ reshapes the input's power distribution $S_{x}(\omega)$.

#### Example: Filtering a First-Order Markov Process

A common model for a [random process](@entry_id:269605) with memory is one whose autocorrelation function decays exponentially, a characteristic of a continuous-time first-order Markov process. Let's consider a real, zero-mean WSS process $x(t)$ with $R_{x}(\tau) = \sigma_{x}^{2}\exp(-\alpha|\tau|)$ for $\alpha > 0$. By taking the Fourier transform, we find its PSD to be a Lorentzian function [@problem_id:2901250]:

$S_{x}(\omega) = \frac{2\alpha\sigma_{x}^{2}}{\alpha^{2} + \omega^{2}}$

The parameter $\alpha$ dictates the "memory" of the process. A large $\alpha$ corresponds to a rapidly decaying [autocorrelation](@entry_id:138991) in the time domain and, consequently, a broad spectrum in the frequency domain. The half-power bandwidth of this spectrum, defined as the frequency $\omega_{3\text{dB}}$ where $S_{x}(\omega_{3\text{dB}}) = \frac{1}{2}S_{x}(0)$, is found to be precisely $\alpha$.

Now, suppose this process is passed through a simple first-order [low-pass filter](@entry_id:145200) with frequency response $H(\omega) = \frac{1}{1+j\omega/\beta}$. The output power $\sigma_{y}^{2}$ can be calculated by integrating the product of the input PSD and the filter's power gain $|H(\omega)|^{2} = \frac{\beta^{2}}{\beta^{2}+\omega^{2}}$. The integral is tractable and yields:

$\sigma_{y}^{2} = \frac{1}{2\pi} \int_{-\infty}^{\infty} \left( \frac{2\alpha\sigma_{x}^{2}}{\alpha^{2} + \omega^{2}} \right) \left( \frac{\beta^{2}}{\beta^{2} + \omega^{2}} \right) d\omega = \frac{\sigma_{x}^{2}\beta}{\alpha + \beta}$

This result elegantly shows how the output power depends on both the input signal's bandwidth ($\alpha$) and the filter's bandwidth ($\beta$).

#### Example: Filtering White Noise

A foundational, albeit idealized, input is **white noise**, defined as a WSS process with a constant PSD across all frequencies: $S_{x}(\omega) = S_{0}$. While such a process would have infinite power and is not physically realizable, it serves as an excellent model for disturbances whose bandwidth is much larger than the bandwidth of the system under consideration. When white noise is the input, the output PSD takes the shape of the filter's power gain:

$S_{y}(\omega) = S_{0} |H(\omega)|^{2}$

The output power is then proportional to the area under the filter's power gain curve, a quantity sometimes referred to as the **noise equivalent bandwidth**. For instance, if [white noise](@entry_id:145248) with PSD $\sigma_{w}^{2}$ is passed through a [second-order filter](@entry_id:265113) with $H(\omega) = \frac{1}{(1+j\omega/\omega_{1})(1+j\omega/\omega_{2})}$, the output variance can be found by integrating $|H(\omega)|^{2}$, which after evaluation using partial fractions yields $\sigma_{y}^{2} = \frac{\sigma_{w}^{2}\omega_{1}\omega_{2}}{2(\omega_{1}+\omega_{2})}$ [@problem_id:2901260].

This principle can be used to analyze the effect of spectral shaping. If a process with a flat, bandlimited spectrum (a more physically plausible model) is passed through an ideal [notch filter](@entry_id:261721) that has zero gain over a specific frequency band, the output will have zero power in that band. The total power removed from the signal is directly proportional to the width of the notch, assuming the input PSD is constant over that region [@problem_id:2901265]. Crucially, no manipulation of the filter's phase can restore power in a band where the magnitude gain is zero.

### Beyond the Power Spectrum: Phase, Transients, and Higher-Order Statistics

While the filter's [phase response](@entry_id:275122) does not affect the steady-state output power spectrum, it has significant consequences for the temporal structure of the output signal, particularly during transient periods.

Consider two FIR filters, one **[minimum-phase](@entry_id:273619)** (all zeros of its transfer function $H(z)$ inside the unit circle) and one **maximum-phase** (all zeros outside the unit circle), both having the same magnitude response. The [minimum-phase filter](@entry_id:197412) is known to have the minimum possible group delay and "minimum energy delay" among all filters with the same magnitude response. This means its impulse response is maximally concentrated at its beginning. When a WSS process is switched on as an input at time $n=0$, the output of the [minimum-phase filter](@entry_id:197412) will converge in mean-square to its steady-state behavior more rapidly than the output of the maximum-phase filter. Its transient response is faster because its impulse response is more front-loaded [@problem_id:2901270].

The effect of phase is also central to the behavior of **all-pass filters**, which are defined by the property $|H(e^{j\omega})| = 1$. Such a filter does not alter the [power spectrum](@entry_id:159996) of any input signal; thus, $S_{y}(e^{j\omega}) = S_{x}(e^{j\omega})$ and $R_{y}[k] = R_{x}[k]$. For a general WSS input, the output process has the same second-[order statistics](@entry_id:266649) as the input. However, if the input $x[n]$ is specifically a **Gaussian process**, the consequences are much stronger. A zero-mean Gaussian process is completely defined by its [autocorrelation function](@entry_id:138327). Since an [all-pass filter](@entry_id:199836) preserves the [autocorrelation](@entry_id:138991), the output $y[n]$ is not just statistically similar to the input; it has the exact same [finite-dimensional distributions](@entry_id:197042). It is, for all statistical purposes, the same process [@problem_id:2901275]. This property does not hold for non-Gaussian inputs, where preserving the second moments does not guarantee preservation of the full distribution. It is also important to note that while the autocorrelation is preserved, the [cross-correlation](@entry_id:143353) between input and output, $R_{xy}[k]$, depends directly on the filter's phase response.

A related concept for complex-valued signals is that of a **proper** (or circularly-symmetric) process, for which the pseudo-autocorrelation $C_{xx}(\tau) = \mathbb{E}[x(t)x(t+\tau)]$ is identically zero. This property of having no correlation between the process and its non-conjugated version is invariant under LTI filtering. If an input $x(t)$ is proper, the output $y(t) = h(t)*x(t)$ will also be proper, regardless of the filter's characteristics [@problem_id:2901268].

### Practical Considerations and Extensions

#### Finite Data and Matrix Formulation

In practice, we often work with finite-length segments of [discrete-time signals](@entry_id:272771). The [continuous convolution](@entry_id:173896) operation can be translated into a discrete [matrix-vector multiplication](@entry_id:140544). If we collect an $N$-length input segment into a vector $\mathbf{x}$ and the resulting output into a vector $\mathbf{y}$, their relationship can be expressed as $\mathbf{y} = \mathbf{H}\mathbf{x}$. Here, $\mathbf{H}$ is a rectangular **convolution matrix** whose entries are determined by the system's impulse response $h[n]$. This matrix has a special, highly structured form known as a **Toeplitz matrix**, where all elements on any given diagonal are the same [@problem_id:2901257].

This formulation allows us to relate the input and output covariance matrices, $\mathbf{R}_{x} = \mathbb{E}[\mathbf{x}\mathbf{x}^{*}]$ and $\mathbf{R}_{y} = \mathbb{E}[\mathbf{y}\mathbf{y}^{*}]$, through a simple and elegant quadratic form:

$\mathbf{R}_{y} = \mathbf{H} \mathbf{R}_{x} \mathbf{H}^{*}$

If the input process is WSS, its covariance matrix $\mathbf{R}_{x}$ is also a Toeplitz matrix. This [matrix representation](@entry_id:143451) is fundamental to many algorithms in statistical signal processing, system identification, and [adaptive filtering](@entry_id:185698).

#### Non-Zero Means and Detrending

Our analysis has so far assumed zero-mean processes. If the input has a non-zero constant mean, $x[n] = \mu_x + w[n]$, where $w[n]$ is zero-mean WSS, the output mean is given by the convolution of the input mean with the impulse response. For a stable LTI system, the output mean converges to a constant value $\mu_y = \mu_x H(0)$, where $H(0)$ is the filter's DC gain. The output process $y[n]$ is still WSS, but with a shifted mean. The stochastic part of the output, $y[n] - \mu_y$, remains a zero-mean WSS process with PSD $|H(e^{j\omega})|^2 S_{ww}(e^{j\omega})$ [@problem_id:2901274].

If a system has zero DC gain, $H(0) = 0$, it will completely suppress any constant input mean, resulting in a zero-mean output. This is a common strategy for removing DC offsets. Conversely, if a system is unstable and has infinite DC gain, such as a discrete-time accumulator ($h[n]=u[n]$), a constant input mean will produce a non-stationary trend (e.g., a linear ramp) in the output mean. In such cases, operations like differencing can be used to remove the trend and recover a WSS process. For more general, slowly drifting trends, high-pass filtering serves as an effective detrending technique.

#### On the Existence of the Output

A final, more theoretical point concerns the very existence of the output process $y(t) = \int h(\tau)x(t-\tau)d\tau$. When $x(t)$ is a [random process](@entry_id:269605), this is a [stochastic integral](@entry_id:195087), and its convergence must be established. Two primary [modes of convergence](@entry_id:189917) are relevant [@problem_id:2901281].

1.  **Mean-Square Convergence**: The output is said to exist in the mean-square sense if the output power is finite. This provides a necessary and sufficient condition: $\int_{-\infty}^{\infty} |H(\omega)|^2 S_x(\omega) d\omega  \infty$. This is the most common criterion used in engineering contexts.

2.  **Almost-Sure Convergence**: This is a stronger, sample-path-wise convergence. A widely used sufficient (but not necessary) condition for almost-sure convergence is that the system is Bounded-Input, Bounded-Output (BIBO) stable, i.e., its impulse response is absolutely integrable: $\int_{-\infty}^{\infty} |h(t)| dt  \infty$.

These conditions ensure that the mathematical operations central to this chapter are well-defined and rigorously grounded.