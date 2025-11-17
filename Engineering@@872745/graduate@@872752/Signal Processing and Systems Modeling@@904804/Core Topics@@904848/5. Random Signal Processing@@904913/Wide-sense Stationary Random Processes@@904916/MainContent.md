## Introduction
Random processes provide a powerful framework for modeling [signals and systems](@entry_id:274453) whose behavior is not deterministic. However, the full complexity of a process whose statistical properties can change at every moment is often analytically intractable. A crucial simplification arises when these properties are invariant over time, a concept formalized by [stationarity](@entry_id:143776). This article delves into a cornerstone of this theory: the Wide-Sense Stationary (WSS) random process, a model whose utility spans countless areas of science and engineering. We will bridge the gap between abstract theory and practical application, showing how this elegant mathematical construct enables the analysis of real-world phenomena.

Throughout this exploration, you will first master the foundational **Principles and Mechanisms** of WSS processes. This includes their formal definition via constant mean and [time-invariant autocorrelation](@entry_id:267923), the critical distinction from [strict-sense stationarity](@entry_id:260987), and their powerful representation in the frequency domain through the power spectral density (PSD). Next, we will uncover the widespread **Applications and Interdisciplinary Connections**, demonstrating how WSS theory is used to analyze signals in LTI systems, identify unknown system characteristics, and design optimal Wiener filters for signal estimation. Finally, a series of **Hands-On Practices** will allow you to apply this knowledge directly, solidifying your understanding through targeted problem-solving. This journey will equip you with the theoretical and practical tools to leverage WSS processes in your own work.

## Principles and Mechanisms

Having established the foundational role of [random processes](@entry_id:268487) in modeling [signals and systems](@entry_id:274453), we now delve into a cornerstone concept: stationarity. In many applications, from communications to control theory, the statistical characteristics of a signal or noise source do not change over time. This invariance is formalized by the notion of [stationarity](@entry_id:143776). This chapter will focus on a particularly useful and widespread form of [stationarity](@entry_id:143776) known as [wide-sense stationarity](@entry_id:173765), exploring its definition, its relationship to stricter forms of stationarity, its representation in the frequency domain, and its deeper mathematical structure.

### Defining Wide-Sense Stationarity

A random process can be a formidable object, with its statistical properties potentially varying at every instant. Wide-sense [stationarity](@entry_id:143776) (WSS), also known as weak-sense [stationarity](@entry_id:143776), imposes a crucial simplification: it requires that the first and second moments of the process be invariant under time shifts. For a continuous-time real or complex-valued [random process](@entry_id:269605) $X(t)$ with finite second moments, i.e., $\mathbb{E}[|X(t)|^2] < \infty$ for all $t$, this translates to two specific conditions.

First, the **mean function** of the process must be constant for all time.
$$
\mu_X(t) = \mathbb{E}[X(t)] = \mu_X \quad (\text{a constant})
$$

Second, the **autocorrelation function**, which describes the correlation between the process values at two time instants, must depend only on the [time lag](@entry_id:267112) $\tau$ between them. Throughout this article, we will consistently use the following definition, where $t$ is an arbitrary time and $\tau$ is the lag:
$$
R_X(\tau) = \mathbb{E}[X(t+\tau)X^*(t)]
$$
This implies that the two-variable function $R_X(t_1, t_2) = \mathbb{E}[X(t_1)X^*(t_2)]$ depends only on the difference $t_1-t_2$, i.e., $R_X(t_1, t_2) = R_X(t_1-t_2)$. While other conventions exist (for example, defining the function in terms of $t_2-t_1$), this one will be used throughout for consistency.

Closely related to the [autocorrelation function](@entry_id:138327) is the **[autocovariance function](@entry_id:262114)**, which measures the correlation of the centered process:
$$
C_X(t_1, t_2) = \mathbb{E}[(X(t_1) - \mu_X(t_1))(X(t_2) - \mu_X(t_2))^*]
$$
By expanding this definition, we find the relationship between the two functions:
$$
C_X(t_1, t_2) = R_X(t_1, t_2) - \mu_X(t_1)\mu_X^*(t_2)
$$
For a WSS process, using the fact that $R_X(t_1, t_2) = R_X(t_1-t_2)$, this relationship simplifies to:
$$
C_X(\tau) = R_X(\tau) - |\mu_X|^2
$$
where $\tau = t_1-t_2$. This shows that if the mean is constant and the [autocorrelation](@entry_id:138991) depends only on the time lag, the [autocovariance](@entry_id:270483) must also depend only on the [time lag](@entry_id:267112). Conversely, if the mean is constant and the [autocovariance](@entry_id:270483) is shift-invariant, the [autocorrelation](@entry_id:138991) must also be shift-invariant. Therefore, the WSS conditions can be stated equivalently using the [autocovariance function](@entry_id:262114) [@problem_id:2916945].

**Example: The Ornstein-Uhlenbeck Process**

To make these definitions concrete, consider a real-valued [random process](@entry_id:269605) $X(t)$ whose mean is given as $\mathbb{E}[X(t)] = \mu$ and whose [autocovariance function](@entry_id:262114) is specified as:
$$
C_X(t_1, t_2) = \mathbb{E}[(X(t_1) - \mu)(X(t_2) - \mu)] = \sigma^2 \exp(-\alpha|t_1 - t_2|)
$$
where $\sigma^2 > 0$ and $\alpha > 0$ are constants. Let us verify if this process is WSS [@problem_id:2916982].

1.  **Mean:** The mean is given as $\mathbb{E}[X(t)] = \mu$, a constant. The first condition is satisfied.
2.  **Autocorrelation:** We find the [autocorrelation function](@entry_id:138327) using the relation $R_X(t_1, t_2) = C_X(t_1, t_2) + \mu_X(t_1)\mu_X(t_2)$.
    $$
    R_X(t_1, t_2) = \sigma^2 \exp(-\alpha|t_1 - t_2|) + \mu^2
    $$
    This expression depends only on the [time lag](@entry_id:267112) $\tau = t_1 - t_2$. Therefore, the second condition is also satisfied. The process is WSS. Its autocorrelation and [autocovariance](@entry_id:270483) functions, written in terms of the lag $\tau$, are:
    $$
    R_X(\tau) = \sigma^2 \exp(-\alpha|\tau|) + \mu^2
    $$
    $$
    C_X(\tau) = \sigma^2 \exp(-\alpha|\tau|)
    $$
    This process, known as the Ornstein-Uhlenbeck process, is a fundamental model for noisy systems with memory, where the correlation between two points decays exponentially with their temporal separation.

### Strict-Sense vs. Wide-Sense Stationarity

Wide-sense [stationarity](@entry_id:143776) constrains only the first two moments of a process. A much stronger condition is **[strict-sense stationarity](@entry_id:260987) (SSS)**. A process $X(t)$ is SSS if all its finite-dimensional [joint probability](@entry_id:266356) distributions are invariant to shifts in time. That is, for any integer $n$, any set of time indices $t_1, \dots, t_n$, and any time shift $\tau$, the [joint distribution](@entry_id:204390) of the vector $(X(t_1), \dots, X(t_n))$ is identical to that of $(X(t_1+\tau), \dots, X(t_n+\tau))$ [@problem_id:2916946].

Invariance of the entire probability distribution implies invariance of all moments that exist. Therefore, if a process is SSS and its first two moments are finite, it is automatically WSS.

The converse, however, is not true: **WSS does not imply SSS**. This is a critical distinction. A process can have a constant mean and a shift-invariant [autocorrelation function](@entry_id:138327) while its [higher-order statistics](@entry_id:193349) or the very shape of its probability distributions change with time.

Let's construct an example to illustrate this [@problem_id:2916979]. Consider a [discrete-time process](@entry_id:261851) $\{X[n]\}_{n \in \mathbb{Z}}$ that is independent across time, with [zero mean](@entry_id:271600) for all $n$. The variance is also constant, $\mathbb{E}[X[n]^2] = a^2$ for all $n$. Because the samples are independent and zero-mean, the [autocovariance function](@entry_id:262114) is $C_X[n_1, n_2] = \mathbb{E}[X[n_1]X[n_2]] = a^2 \delta[n_1 - n_2]$, where $\delta[\cdot]$ is the Kronecker delta. This function depends only on the lag $k = n_1 - n_2$, so the process is WSS.

Now, let's specify the distributions. For even time indices $n$, let $X[n]$ be a [discrete random variable](@entry_id:263460) taking values $\pm a$ with equal probability. For odd time indices $n$, let $X[n]$ be a [continuous random variable](@entry_id:261218) uniformly distributed on $[-\sqrt{3}a, \sqrt{3}a]$. As shown in the solution to [@problem_id:2916979], both distributions have a mean of zero and a variance of $a^2$. However, the first-order distribution of the process is clearly not time-invariant; the distribution of $X[0]$ is discrete, while the distribution of $X[1]$ is continuous. Since the first-order distribution is not shift-invariant, the process cannot be SSS. We can further show that [higher-order statistics](@entry_id:193349) are time-varying by computing, for instance, the fourth-order cumulants, which are different for even and odd time indices.

There is one exceptionally important case where the two forms of [stationarity](@entry_id:143776) coincide: the **Gaussian process**. A process is Gaussian if any [finite set](@entry_id:152247) of samples $(X(t_1), \dots, X(t_n))$ has a multivariate Gaussian distribution. A Gaussian distribution is completely determined by its [mean vector](@entry_id:266544) and covariance matrix. If a Gaussian process is WSS, its mean is constant and its [autocovariance function](@entry_id:262114) is shift-invariant. This implies that the [mean vector](@entry_id:266544) and covariance matrix of any time-shifted sample vector are identical to those of the original vector. Since the distributions are Gaussian, and they are defined by these moments, the distributions themselves must be identical. Thus, for a Gaussian process, WSS implies SSS [@problem_id:2916946].

### The Frequency Domain and Power Spectral Density

Since the [autocorrelation function](@entry_id:138327) $R_X(\tau)$ of a WSS process depends on a single variable, it is natural to analyze it in the frequency domain using the Fourier transform. This leads to one of the most powerful tools in signal processing: the **Power Spectral Density (PSD)**.

Why is the PSD so important? One might be tempted to analyze the frequency content of a random process by taking a single, finite-time realization of the process, say $x(t)$ over $[0, T]$, and computing its Fourier transform magnitude squared, $|X_T(f)|^2$. However, $x(t)$ is just one outcome from an entire ensemble of possibilities. The resulting spectrum is itself a random function and is not a stable, reliable characterization of the underlying process. In fact, for a broadband process, the variance of this spectral estimate (known as a [periodogram](@entry_id:194101)) is typically on the same order as its mean value, making it a very noisy estimator [@problem_id:1736135].

The **Wiener-Khinchin theorem** provides the correct, robust approach. It states that the PSD, denoted $S_X(f)$, is the Fourier transform of the ensemble [autocorrelation function](@entry_id:138327) $R_X(\tau)$:
$$
S_X(f) = \int_{-\infty}^{\infty} R_X(\tau) e^{-j2\pi f \tau} d\tau
$$
The inverse relationship also holds:
$$
R_X(\tau) = \int_{-\infty}^{\infty} S_X(f) e^{j2\pi f \tau} df
$$
The PSD $S_X(f)$ describes how the [average power](@entry_id:271791) of the process is distributed across frequency. It is a deterministic function that characterizes the entire WSS ensemble, not just one realization. From these definitions, two key properties emerge:
1.  **Non-negativity:** $S_X(f) \ge 0$ for all $f$. This must be true for the PSD to represent power.
2.  **Reality:** For a real-valued process $X(t)$, $R_X(\tau)$ is a real and even function, which implies that its Fourier transform, $S_X(f)$, is also real and even.

Furthermore, the total average power of the process can be found by evaluating the [autocorrelation](@entry_id:138991) at zero lag, which is equivalent to integrating the PSD over all frequencies:
$$
\text{Average Power} = \mathbb{E}[|X(t)|^2] = R_X(0) = \int_{-\infty}^{\infty} S_X(f) df
$$

### Spectral Representation Theorems

The Wiener-Khinchin theorem connects the second-moment description ($R_X(\tau)$) to the frequency domain ($S_X(f)$). Deeper results, known as [spectral representation](@entry_id:153219) theorems, provide a way to represent the process $X(t)$ itself as a synthesis of random frequency components. These theorems are central to the theory of [stationary processes](@entry_id:196130).

#### Characterization of the Autocorrelation Function

For a function to be a valid autocorrelation function of a discrete-time WSS process, it must satisfy a property called **[positive semidefiniteness](@entry_id:147720)**. For a discrete-time ACF $r[k]$, this means that for any [finite set](@entry_id:152247) of complex coefficients $\{c_i\}$, the following holds:
$$
\sum_{i=0}^{N}\sum_{j=0}^{N}c_{i}c_{j}^{*}r[i-j] \ge 0
$$
**Bochner's theorem** (sometimes called Herglotz's theorem in the discrete-time context) provides a complete and elegant characterization: a sequence $r[k]$ is a valid ACF if and only if it is the set of Fourier coefficients of a finite, non-negative measure $\mu$ on the frequency interval $[-\pi, \pi)$ [@problem_id:2916925].
$$
r[k] = \int_{[-\pi, \pi)} e^{ik\omega} d\mu(\omega)
$$
This [spectral measure](@entry_id:201693) $\mu$ may be composed of two parts:
1.  An **absolutely continuous part**, which can be described by a density function $S(\omega)$, the PSD. In this case, $d\mu(\omega) = S(\omega) d\omega$. An example is the ACF $r[k] = \rho^{|k|}$ for $0  \rho  1$, which corresponds to a smooth PSD.
2.  A **singular part**, consisting of discrete point masses (Dirac delta functions). This corresponds to discrete [spectral lines](@entry_id:157575). For instance, the ACF $r[k] = \cos(\omega_0 k)$ corresponds to two point masses at frequencies $\pm \omega_0$ [@problem_id:2916925].

#### Cramér's Spectral Representation

Bochner's theorem describes the ACF. The **Cramér [representation theorem](@entry_id:275118)** goes further and describes the process $X(t)$ itself. It states that any zero-mean, continuous-time WSS process can be written as a stochastic integral:
$$
X(t) = \int_{-\infty}^{\infty} e^{j2\pi ft} dZ(f)
$$
Here, $Z(f)$ is a random process in frequency with **orthogonal increments**. This means that the random increments of $Z(f)$ over any two disjoint frequency bands are uncorrelated (orthogonal) [@problem_id:2916934]:
$$
\mathbb{E}[dZ(f_1) dZ^*(f_2)] = 0 \quad \text{for} \quad f_1 \neq f_2
$$
The crucial link back to the PSD is that the variance of an infinitesimal increment $dZ(f)$ is precisely the power in that frequency band:
$$
\mathbb{E}[|dZ(f)|^2] = dF_X(f) = S_X(f) df
$$
where $dF_X(f)$ is the [spectral measure](@entry_id:201693) from Bochner's theorem.

This powerful representation formalizes the intuition of a [stationary process](@entry_id:147592) as a superposition of sinusoids with random amplitudes and phases. The interpretation becomes particularly clear when the PSD contains both continuous and discrete parts [@problem_id:2916957]:
*   A **continuous PSD component**, $S_c(f)$, corresponds to a broadband, noise-like process component $X_c(t)$ whose power is spread over a range of frequencies.
*   A **discrete [spectral line](@entry_id:193408)** (a Dirac delta function) at a frequency $f_k \neq 0$, say $p_k \delta(f-f_k)$, paired with a line at $-f_k$, corresponds to a deterministic sinusoidal component with a *random phase*: $A_k \cos(2\pi f_k t + \Theta_k)$. The phase $\Theta_k$ must be random (typically uniform on $[0, 2\pi)$) to ensure the component is zero-mean and stationary. The power of this component, $\mathbb{E}[A_k^2 \cos^2(\cdot)] = A_k^2/2$, is related to the mass $p_k$ of the spectral line.

### Advanced Topics in Stationarity

#### Ergodicity

Stationarity is an ensemble property, defined over the collection of all possible realizations of a process. In practice, we often have access to only a single, long realization. **Ergodicity** is the property that allows us to substitute time averages for [ensemble averages](@entry_id:197763). A WSS process is **[mean-ergodic](@entry_id:180206)** if the time average of any single realization converges to the ensemble mean $\mu_X$:
$$
\lim_{T\to\infty} \frac{1}{T} \int_0^T X(t) dt = \mathbb{E}[X(t)] = \mu_X
$$
It is important to understand that stationarity does not imply [ergodicity](@entry_id:146461). Consider the process $X(t) = A$, where $A$ is a random variable with mean zero and non-zero variance. This process is WSS. However, the time average for any single realization is simply $A$, which is a random variable, not the constant ensemble mean of 0.

A more subtle point is that a process can be ergodic in some statistics but not others. Consider the process $X(t) = A \cos(\omega_0 t + \Theta)$, where $\Theta$ is a uniform random phase and $A$ is an independent random amplitude with $\text{Var}(A)  0$. This process is WSS and can be shown to be [mean-ergodic](@entry_id:180206). However, it is not **[autocorrelation](@entry_id:138991)-ergodic** [@problem_id:2916969]. The ensemble autocorrelation is $R_X(\tau) = \frac{1}{2}\mathbb{E}[A^2]\cos(\omega_0\tau)$. The time-averaged [autocorrelation](@entry_id:138991) for a single realization converges to $\frac{1}{2}A^2\cos(\omega_0\tau)$. Since this limit depends on the random variable $A$, it is not equal to the deterministic [ensemble average](@entry_id:154225). The process fails to be ergodic in [autocorrelation](@entry_id:138991) because the [time average](@entry_id:151381) depends on the specific random amplitude of the single path being observed.

#### Complex WSS Processes and Circularity

The concept of stationarity extends naturally to complex-valued processes, which are essential in fields like communications and modern signal processing. For a complex WSS process $X(t)$, we must consider two second-order moment functions:
1.  The **autocorrelation function**: $R_X(\tau) = \mathbb{E}[X(t+\tau)X^*(t)]$
2.  The **pseudo-autocorrelation function**: $P_X(\tau) = \mathbb{E}[X(t+\tau)X(t)]$

For a complex WSS process, $R_X(\tau)$ exhibits Hermitian symmetry, $R_X(\tau) = R_X^*(-\tau)$, while $P_X(\tau)$ is an [even function](@entry_id:164802), $P_X(\tau) = P_X(-\tau)$.

A special and important class of complex WSS processes are those that are **circular** or **proper**. A process is circular if its statistics are invariant to a phase rotation, i.e., the process $Y(t) = X(t)e^{j\phi}$ has the same statistics as $X(t)$ for any phase $\phi$. For a WSS process, this leads to two [necessary and sufficient conditions](@entry_id:635428) [@problem_id:2916978]:
1.  The mean must be zero: $\mathbb{E}[X(t)] = 0$.
2.  The pseudo-autocorrelation must be identically zero: $P_X(\tau) \equiv 0$ for all $\tau$.

The condition $P_X(\tau) = 0$ implies that the process is uncorrelated with its [complex conjugate](@entry_id:174888), $X^*(t)$. Such processes are rotationally symmetric in the complex plane, which greatly simplifies many theoretical and practical calculations. Most physical noise sources modeled as complex processes (e.g., [thermal noise](@entry_id:139193) in I/Q channels) are assumed to be circular.