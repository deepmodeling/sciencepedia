## Introduction
Random signals are ubiquitous, from the [thermal noise](@entry_id:139193) in electronic circuits to fluctuations in financial markets, yet their inherent unpredictability presents a challenge for traditional frequency analysis. How can we characterize the frequency content of a process that never truly repeats? This knowledge gap is bridged by the Wiener-Khinchin theorem, a cornerstone of signal processing that establishes a profound and elegant connection between a signal's time-domain correlation structure and its frequency-domain power distribution. This article provides a graduate-level exploration of this powerful theorem. The journey begins in **Principles and Mechanisms**, where we will establish the statistical prerequisites, formally state the theorem, and examine the properties of the resulting [power spectral density](@entry_id:141002) from both a practical and a rigorous measure-theoretic perspective. Building on this foundation, **Applications and Interdisciplinary Connections** will demonstrate how the theorem is leveraged to analyze linear systems, design [spectral estimation](@entry_id:262779) algorithms, and provide insights in diverse fields from optics to machine learning. To solidify your understanding, **Hands-On Practices** will guide you through concrete examples, translating theory into tangible analytical skills.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms underpinning the Wiener-Khinchin theorem. We will begin by establishing the statistical prerequisites for a spectral theory of [random processes](@entry_id:268487), namely [wide-sense stationarity](@entry_id:173765) and the properties of the autocorrelation function. We will then formally state the theorem, which forges the crucial link between the time-domain correlation structure of a process and its frequency-domain power distribution. The properties of the resulting [power spectral density](@entry_id:141002) will be examined, followed by a deeper, measure-theoretic treatment that provides a complete and rigorous framework. Finally, we will explore the practical implications for signal estimation and the consequences of relaxing the core assumption of stationarity.

### Wide-Sense Stationarity and the Autocorrelation Function

The concept of a power spectrum for a random process is only meaningful if the process exhibits a degree of statistical regularity over time. A sufficiently general and useful form of regularity is **[wide-sense stationarity](@entry_id:173765) (WSS)**. A continuous-time, complex-valued stochastic process $x(t)$ is defined as WSS if it meets two conditions:
1.  Its first moment (mean) is constant for all time $t$: $\mathbb{E}[x(t)] = m_x$.
2.  Its second moment, the autocorrelation, depends only on the time difference (or lag) $\tau = t_1 - t_2$: $\mathbb{E}[x(t_1)\overline{x(t_2)}] = R_x(t_1 - t_2)$.

For simplicity, we will often consider **zero-mean** WSS processes, where $m_x = 0$. The [autocorrelation function](@entry_id:138327) is then defined as $R_x(\tau) = \mathbb{E}[x(t+\tau)\overline{x(t)}]$. A parallel definition holds for a [discrete-time process](@entry_id:261851) $x[n]$, whose [autocorrelation](@entry_id:138991) sequence is $R_x[k] = \mathbb{E}[x[n+k]\overline{x[n]}]$ [@problem_id:2914583] [@problem_id:2914582].

The autocorrelation function of a WSS process possesses several fundamental properties that are essential for the development of [spectral theory](@entry_id:275351):

1.  **Maximum Value and Average Power**: The magnitude of the [autocorrelation](@entry_id:138991) is maximal at zero lag. By the Cauchy-Schwarz inequality, $|R_x(\tau)|^2 \le \mathbb{E}[|x(t+\tau)|^2] \mathbb{E}[|x(t)|^2] = R_x(0)^2$. Thus, $|R_x(\tau)| \le R_x(0)$. The value $R_x(0) = \mathbb{E}[|x(t)|^2]$ represents the [average power](@entry_id:271791) of the process, which is finite and constant for a WSS process.

2.  **Hermitian Symmetry**: The autocorrelation function exhibits [conjugate symmetry](@entry_id:144131): $R_x(-\tau) = \overline{R_x(\tau)}$. This follows directly from the definition: $R_x(-\tau) = \mathbb{E}[x(t-\tau)\overline{x(t)}] = \overline{\mathbb{E}[\overline{x(t-\tau)}x(t)]}$. By letting $s = t-\tau$, this becomes $\overline{\mathbb{E}[x(s)x(s+\tau)]}$, which is $\overline{R_x(\tau)}$. For a real-valued process, this property simplifies to even symmetry, $R_x(-\tau) = R_x(\tau)$.

3.  **Positive Definiteness**: This is the most profound property. A function $R_x(\tau)$ is a valid [autocorrelation function](@entry_id:138327) of a WSS process only if it is **positive-definite** (more precisely, non-[negative definite](@entry_id:154306)). This means that for any integer $N$, any set of times $t_1, \dots, t_N$, and any set of complex coefficients $a_1, \dots, a_N$, the following condition holds:
    $$ \sum_{k=1}^{N} \sum_{\ell=1}^{N} a_k \overline{a_\ell} R_x(t_k - t_\ell) \ge 0 $$
    This property is not arbitrary; it arises because this double summation represents the variance of the random variable $Y = \sum_{k=1}^{N} a_k x(t_k)$, which must be non-negative: $\mathbb{E}[|Y|^2] \ge 0$. As we will see, this time-domain property is what guarantees the non-negativity of the [power spectrum](@entry_id:159996) in the frequency domain.

### Energy Signals versus Power Signals: The Role of the PSD

Before stating the theorem, it is crucial to distinguish between two classes of signals. A deterministic signal $x(t)$ is an **[energy signal](@entry_id:273754)** if its total energy $E_x = \int_{-\infty}^{\infty} |x(t)|^2 dt$ is finite and non-zero. Such a signal must decay over time, and its time-averaged power is zero. The frequency content of an [energy signal](@entry_id:273754) is described by its **Energy Spectral Density (ESD)**, $E_x(\omega) = |X(\omega)|^2$, where $X(\omega)$ is the Fourier transform of $x(t)$. The ESD describes how the signal's finite energy is distributed across frequency.

In contrast, a WSS random process is a quintessential **[power signal](@entry_id:260807)**. Its average power $P_x = R_x(0)$ is finite and non-zero, which implies that the energy of any single realization is [almost surely](@entry_id:262518) infinite. For such signals, the ESD is not a meaningful concept. Instead, we use the **Power Spectral Density (PSD)**, denoted $S_x(\omega)$, to describe how the finite [average power](@entry_id:271791) of the process is distributed across frequency. The Wiener-Khinchin theorem is the bridge that connects the time-domain autocorrelation of a [power signal](@entry_id:260807) to its PSD [@problem_id:2914626]. A parallel relationship exists for deterministic [energy signals](@entry_id:190524), where the Fourier transform of the signal's *aperiodic* [autocorrelation](@entry_id:138991) yields the ESD; however, this is conceptually distinct from the theorem for random processes, which involves ensemble averaging and describes the distribution of power, not energy [@problem_id:2914626].

### The Wiener-Khinchin Theorem

The Wiener-Khinchin theorem states that for a WSS random process, the power spectral density $S_x(\omega)$ and the [autocorrelation function](@entry_id:138327) $R_x(\tau)$ form a Fourier transform pair. The precise form of this relationship depends on the chosen convention for the Fourier transform. Consistency is paramount.

Let's examine three common conventions [@problem_id:2914616]:

1.  **Continuous-Time, Asymmetric Angular Frequency ($\omega$) Convention**: This is common in physics and electrical engineering.
    *   Forward Transform: $X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} dt$
    *   Inverse Transform: $x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega) e^{j\omega t} d\omega$
    Under this convention, the Wiener-Khinchin relations are:
    $$ S_x(\omega) = \int_{-\infty}^{\infty} R_x(\tau) e^{-j\omega\tau} d\tau \quad \text{and} \quad R_x(\tau) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) e^{j\omega\tau} d\omega $$

2.  **Continuous-Time, Symmetric (Unitary) Ordinary Frequency ($f$) Convention**: This is common in signal processing and communications, where $f = \omega/(2\pi)$.
    *   Forward Transform: $X(f) = \int_{-\infty}^{\infty} x(t) e^{-j2\pi f t} dt$
    *   Inverse Transform: $x(t) = \int_{-\infty}^{\infty} X(f) e^{j2\pi f t} df$
    Here, the Wiener-Khinchin relations are symmetric:
    $$ S_x(f) = \int_{-\infty}^{\infty} R_x(\tau) e^{-j2\pi f\tau} d\tau \quad \text{and} \quad R_x(\tau) = \int_{-\infty}^{\infty} S_x(f) e^{j2\pi f\tau} df $$

3.  **Discrete-Time Fourier Transform (DTFT) Convention**: For a discrete-time WSS process $x[n]$.
    *   Forward Transform: $X(e^{j\Omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\Omega n}$
    *   Inverse Transform: $x[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\Omega}) e^{j\Omega n} d\Omega$
    The corresponding relations for the [autocorrelation](@entry_id:138991) sequence $R_x[k]$ and the PSD $S_x(e^{j\Omega})$ are:
    $$ S_x(e^{j\Omega}) = \sum_{k=-\infty}^{\infty} R_x[k] e^{-j\Omega k} \quad \text{and} \quad R_x[k] = \frac{1}{2\pi} \int_{-\pi}^{\pi} S_x(e^{j\Omega}) e^{j\Omega k} d\Omega $$
    A key feature of the discrete-time case is that the spectrum $S_x(e^{j\Omega})$ is always periodic with period $2\pi$, a direct consequence of the discrete nature of the time index $k$ [@problem_id:2914582].

### Properties and Interpretation of the Power Spectral Density

The fundamental properties of the autocorrelation function impart corresponding properties to the PSD.

**Real-Valued**: The Hermitian symmetry of $R_x(\tau)$ ensures that its Fourier transform, $S_x(\omega)$, is always a real-valued function.

**Non-Negativity**: The [positive-definiteness](@entry_id:149643) of $R_x(\tau)$ ensures that $S_x(\omega) \ge 0$ for all $\omega$. This is the central consequence of the theorem. A function whose Fourier transform takes on negative values cannot be a valid autocorrelation function, even if it is even and continuous. For example, consider the function $R(\tau) = \exp(-|\tau|) - 2\exp(-2|\tau|)$. Its Fourier transform can be calculated as $S(\omega) = \frac{2}{1+\omega^2} - \frac{8}{4+\omega^2} = \frac{-6\omega^2}{(1+\omega^2)(4+\omega^2)}$, which is negative for all $\omega \neq 0$. This violation of the non-negativity property proves that this $R(\tau)$ is not positive-definite and cannot represent the [autocorrelation](@entry_id:138991) of any WSS process [@problem_id:2914569]. The PSD represents power, and power cannot be negative.

**Total Power**: The [inverse relation](@entry_id:274206) allows us to recover the total [average power](@entry_id:271791) of the process by integrating the PSD. Setting $\tau=0$ in the inverse transform (using the first convention) gives a profoundly important result:
$$ R_x(0) = \frac{1}{2\pi} \int_{-\infty}^{\infty} S_x(\omega) d\omega $$
This equation states that the total [average power](@entry_id:271791) of the process, $R_x(0)$, is equal to the total area under the scaled PSD curve. This provides a powerful consistency check for candidate PSDs. For a WSS process with a known [average power](@entry_id:271791) $R_x(0)=3$, any valid PSD must integrate to $6\pi$ (i.e., $\int S_x(\omega) d\omega = 2\pi R_x(0)$). We can use this to validate or reject potential spectral models [@problem_id:2914566]. For example, a PSD of the form $S_x(\omega) = 3\pi \cdot \mathbb{1}_{\{|\omega|\le 1\}}$ is valid because $\int_{-1}^{1} 3\pi d\omega = 6\pi$, whereas $S_x(\omega) = \frac{2}{1+\omega^2}$ is not, because its integral is $2\pi$.

### A Rigorous View: Spectral Measures and Distributions

The simple Fourier transform integral $S_x(\omega) = \int_{-\infty}^{\infty} R_x(\tau)e^{-j\omega\tau}d\tau$ is only guaranteed to converge in the ordinary sense if $R_x(\tau)$ is absolutely integrable, i.e., $R_x \in L^1(\mathbb{R})$. However, many important WSS processes do not satisfy this condition. A simple [sinusoid](@entry_id:274998), $x(t) = A\cos(\omega_0 t + \Phi)$, has an autocorrelation function $R_x(\tau) = \frac{|A|^2}{2}\cos(\omega_0 \tau)$, which does not decay and is not in $L^1(\mathbb{R})$.

To handle all WSS processes, a more powerful mathematical framework is required. This is provided by **Bochner's theorem**, which states that any positive-definite, continuous function $R_x(\tau)$ can be represented as the Fourier-Stieltjes transform of a finite, non-negative measure $dF(\omega)$, called the **[spectral measure](@entry_id:201693)**:
$$ R_x(\tau) = \int_{-\infty}^{\infty} e^{j\omega\tau} dF(\omega) $$
This is the most general form of the Wiener-Khinchin theorem. The PSD is more properly understood not always as a function, but as this measure $dF(\omega)$ [@problem_id:2914583].

By the **Lebesgue Decomposition Theorem**, any such [spectral measure](@entry_id:201693) can be uniquely decomposed into three mutually singular components with respect to the standard Lebesgue measure $d\omega$ [@problem_id:2914603]:

1.  **The Absolutely Continuous Component**: This part can be written as $dF_{ac}(\omega) = S_x(\omega) d\omega$, where $S_x(\omega)$ is a non-negative, integrable function called the Radon-Nikodym derivative. This is the familiar PSD function, which exists when $R_x(\tau) \in L^1(\mathbb{R})$. It corresponds to processes whose correlation decays over time.

2.  **The Discrete (or Pure-Point) Component**: This part consists of a sum of Dirac delta functions at discrete frequencies, $dF_d(\omega) = \sum_k P_k \delta(\omega - \omega_k) d\omega$. Each [delta function](@entry_id:273429), or **[spectral line](@entry_id:193408)**, corresponds to a persistent periodic component in the random process, such as a sinusoid. This results in a non-decaying periodic term in the autocorrelation function, $R_d(\tau) = \sum_k P_k e^{j\omega_k \tau}$ [@problem_id:2914603].

3.  **The Singular Continuous Component**: This is a more exotic component, representing a measure that is concentrated on a set of Lebesgue [measure zero](@entry_id:137864) (like the discrete part) but which has no atoms or points of concentrated mass (unlike the discrete part). A classic example is a Cantor-type distribution. Such processes are aperiodic but exhibit a pathologically intricate structure.

A canonical example requiring a distributional interpretation is idealized **Gaussian [white noise](@entry_id:145248)**, $w(t)$. This process is a theoretical abstraction defined by an autocorrelation function $R_w(\tau) = \sigma^2 \delta(\tau)$ [@problem_id:2914586]. The Dirac delta function implies the process is completely uncorrelated at any non-zero lag, and it has infinite power at $\tau=0$. It is not a function in the classical sense. Its PSD is found by taking the Fourier transform of this distribution:
$$ S_w(\omega) = \mathcal{F}\{\sigma^2 \delta(\tau)\} = \sigma^2 $$
The PSD is a constant, or "flat," for all frequencies. This implies that the process has equal power at all frequencies, from zero to infinity. Consequently, its total power, $\frac{1}{2\pi} \int_{-\infty}^{\infty} \sigma^2 d\omega$, is infinite. Both $R_w(\tau)$ and $S_w(\omega)$ are not classical functions but are well-defined as [tempered distributions](@entry_id:193859), providing a powerful modeling tool for noise in systems that are band-limited.

### Estimation, Ergodicity, and Generalizations

The Wiener-Khinchin theorem is a statement about the *ensemble* properties of a process. It guarantees the existence of a PSD based on the WSS assumption alone. It does not, however, state how to find the PSD from data. This is the domain of estimation, where the concept of **[ergodicity](@entry_id:146461)** becomes crucial [@problem_id:2914568].

A WSS process is **ergodic** (in the second order) if time averages computed along a single, sufficiently long realization converge to the [ensemble averages](@entry_id:197763). For an ergodic process, we can estimate the [autocorrelation function](@entry_id:138327) $R_x(\tau)$ by computing a time-average from one [sample path](@entry_id:262599). If a process is WSS but not ergodic, one cannot learn its statistics from a single realization; one would need to average over an ensemble of multiple independent realizations. Therefore, WSS is required for the *existence* of a time-invariant PSD, while ergodicity is required for its *consistent estimation* from a single time series. It is a common mistake to assume that the raw [periodogram](@entry_id:194101) (the squared-magnitude of the Fourier transform of a finite data segment) is a [consistent estimator](@entry_id:266642) of the PSD. While asymptotically unbiased, its variance does not decrease as the length of the data record increases, making it an unreliable estimator [@problem_id:2914568].

Finally, what happens if a process is not WSS? The foundation of the theorem collapses. The autocorrelation, $R_x(t_1, t_2)$, will now depend on both the lag $\tau = t_1-t_2$ and the absolute time $u = (t_1+t_2)/2$. The elegant Fourier transform relationship to a single, time-invariant PSD is lost. The process's covariance matrix is no longer a simple Toeplitz matrix [@problem_id:2914609]. For such non-[stationary processes](@entry_id:196130), spectral analysis requires more advanced tools, such as time-frequency distributions (e.g., the Wigner-Ville distribution) or time-averaged spectra. An important special class of non-[stationary processes](@entry_id:196130) is **cyclostationary processes**, whose statistics are periodic in time. For these, the Wiener-Khinchin theorem is generalized to a two-dimensional [spectral theory](@entry_id:275351) that characterizes how power is correlated between different frequency bands [@problem_id:2914609].