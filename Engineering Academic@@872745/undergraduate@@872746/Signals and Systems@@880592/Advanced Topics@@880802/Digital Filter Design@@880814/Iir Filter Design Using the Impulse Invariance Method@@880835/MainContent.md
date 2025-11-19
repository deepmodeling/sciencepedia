## Introduction
The design of digital filters from analog prototypes is a fundamental technique in digital signal processing, allowing engineers to leverage a rich history of analog design theory in the digital domain. The core challenge lies in accurately translating the characteristics of a continuous-time system into a discrete-time equivalent. The [impulse invariance method](@entry_id:272647) offers a direct and intuitive solution to this problem by preserving the time-domain impulse response of the original [analog filter](@entry_id:194152). This article provides a comprehensive exploration of this powerful method. In the first chapter, **Principles and Mechanisms**, we will dissect the mathematical foundation of [impulse invariance](@entry_id:266308), from the core idea of sampling the impulse response to the crucial s-plane to [z-plane mapping](@entry_id:276475) and the inherent issue of aliasing. Following this, the chapter on **Applications and Interdisciplinary Connections** will showcase how the method is applied to design real-world IIR filters, discuss its practical limitations, and compare it to alternative techniques like the bilinear transform. Finally, the **Hands-On Practices** section will solidify your understanding through guided problems that bridge theory and practical implementation, allowing you to apply these concepts directly. By the end, you will have a thorough grasp of how to use, analyze, and critically evaluate the [impulse invariance method](@entry_id:272647) for your own [filter design](@entry_id:266363) tasks.

## Principles and Mechanisms

The design of digital filters from analog prototypes is a cornerstone of digital signal processing, providing a rich theoretical framework and practical design methodologies. The [impulse invariance method](@entry_id:272647) is a fundamental technique in this domain, distinguished by its direct and intuitive connection between the continuous-time and discrete-time domains. This chapter elucidates the core principles and underlying mechanisms of this method, exploring its procedural steps, mathematical properties, and practical limitations.

### The Fundamental Principle: Preserving the Impulse Response

The [impulse invariance method](@entry_id:272647) is founded on a simple yet powerful idea: to create a [digital filter](@entry_id:265006) whose impulse response is a sampled version of a corresponding [analog filter](@entry_id:194152)'s impulse response. Let $h_a(t)$ be the impulse response of a continuous-time analog filter. If we sample this response at uniform intervals of $T_s$ seconds, we generate a discrete-time sequence, $h[n]$. The most direct definition for this sequence is:

$$h[n] = h_a(nT_s)$$

where $n$ is an integer index. This definition ensures that the values of the digital impulse response are identical to the values of the analog impulse response at the sampling instants.

However, in practice, a scaling factor is often introduced. The standard definition for the impulse response in the **[impulse invariance](@entry_id:266308)** method is:

$$h[n] = T_s h_a(nT_s)$$

The inclusion of the sampling period $T_s$ as a scaling factor might seem arbitrary at first, but it serves a crucial purpose. Its primary role is to ensure that the low-frequency gain of the digital filter appropriately matches that of the analog prototype [@problem_id:1726532]. To understand why, consider the DC gain (the [frequency response](@entry_id:183149) at zero frequency) of both filters. The DC gain of the analog filter, $H_a(s)$, is given by its value at $s=0$:

$$H_a(0) = \int_{-\infty}^{\infty} h_a(t) dt$$

For a causal filter, this integral is over $[0, \infty)$. The DC gain of the digital filter, $H(z)$, is its value at $z=1$ (corresponding to a discrete-time frequency $\omega=0$):

$$H(1) = \sum_{n=-\infty}^{\infty} h[n]$$

If we substitute our scaled definition of $h[n]$, we get:

$$H(1) = \sum_{n=-\infty}^{\infty} T_s h_a(nT_s) = T_s \sum_{n=-\infty}^{\infty} h_a(nT_s)$$

This expression can be recognized as a Riemann sum approximation of the integral of $h_a(t)$. As the [sampling period](@entry_id:265475) $T_s$ becomes very small, this sum more closely approximates the integral:

$$T_s \sum_{n=0}^{\infty} h_a(nT_s) \approx \int_{0}^{\infty} h_a(t) dt = H_a(0)$$

Thus, the scaling by $T_s$ ensures that the DC gain of the [digital filter](@entry_id:265006) approximates the DC gain of the analog filter, with the approximation improving for smaller $T_s$. Without this factor, the digital filter's gain would be off by a factor of $T_s$.

### From Analog to Digital: The Design Procedure

With the time-domain relationship established, we can outline a systematic procedure for converting an analog transfer function, $H_a(s)$, into a digital transfer function, $H(z)$. This process is most straightforward when the analog transfer function is a rational function with simple (non-repeated) poles.

1.  **Partial Fraction Expansion**: Given the analog transfer function $H_a(s)$, the first step is to decompose it into a sum of first-order terms using [partial fraction expansion](@entry_id:265121). For a causal and stable filter with $N$ distinct poles $p_k$:
    $$H_a(s) = \sum_{k=1}^{N} \frac{R_k}{s - p_k}$$
    where $R_k$ are the residues corresponding to each pole $p_k$.

2.  **Inverse Laplace Transform**: The impulse response $h_a(t)$ of the analog filter is found by taking the inverse Laplace transform of each term. For a [causal system](@entry_id:267557), this yields:
    $$h_a(t) = \left( \sum_{k=1}^{N} R_k \exp(p_k t) \right) u(t)$$
    where $u(t)$ is the [continuous-time unit step function](@entry_id:272355).

3.  **Sampling**: The digital impulse response $h[n]$ is obtained by sampling $h_a(t)$ at intervals of $T_s$. Using the standard definition (without the $T_s$ scaling for now, as it only affects the numerator):
    $$h[n] = h_a(nT_s) = \left( \sum_{k=1}^{N} R_k \exp(p_k n T_s) \right) u[n] = \left( \sum_{k=1}^{N} R_k (\exp(p_k T_s))^n \right) u[n]$$
    where $u[n]$ is the [discrete-time unit step sequence](@entry_id:270300).

4.  **Z-Transform**: The final step is to find the digital transfer function $H(z)$ by taking the Z-transform of $h[n]$. Using the standard Z-transform pair $\mathcal{Z}\{a^n u[n]\} = \frac{1}{1 - a z^{-1}}$, we get:
    $$H(z) = \sum_{k=1}^{N} \frac{R_k}{1 - \exp(p_k T_s) z^{-1}}$$
    If the scaling factor $T_s$ is included in the definition of $h[n]$, the numerator of each term simply becomes $T_s R_k$.

As an illustrative example, consider the design of a digital filter from an analog prototype with the transfer function $H_a(s) = \frac{1}{(s+2)(s+5)}$ using a [sampling period](@entry_id:265475) of $T_s = 0.2$ s [@problem_id:1726554].

First, we perform a [partial fraction expansion](@entry_id:265121):
$$H_a(s) = \frac{1}{(s+2)(s+5)} = \frac{1/3}{s+2} - \frac{1/3}{s+5}$$
The analog impulse response is then:
$$h_a(t) = \frac{1}{3}(\exp(-2t) - \exp(-5t))u(t)$$
Sampling this response (we will omit the scaling factor $T_s$ for now and re-introduce it at the end if needed) gives:
$$h[n] = h_a(nT_s) = \frac{1}{3}(\exp(-2nT_s) - \exp(-5nT_s))u[n] = \frac{1}{3}((\exp(-2T_s))^n - (\exp(-5T_s))^n)u[n]$$
Taking the Z-transform yields the digital transfer function:
$$H(z) = \frac{1}{3} \left( \frac{1}{1 - \exp(-2T_s)z^{-1}} - \frac{1}{1 - \exp(-5T_s)z^{-1}} \right)$$
Combining the terms into a single rational function gives:
$$H(z) = \frac{\frac{1}{3}(\exp(-2T_s) - \exp(-5T_s))z^{-1}}{1 - (\exp(-2T_s) + \exp(-5T_s))z^{-1} + \exp(-7T_s)z^{-2}}$$
Substituting $T_s=0.2$, we obtain the final digital transfer function. This example encapsulates the entire workflow from an analog prototype to a functional [digital filter](@entry_id:265006).

### Mapping Properties: From the s-plane to the z-plane

The design procedure reveals a profound and direct relationship between the poles of the [analog filter](@entry_id:194152) and the poles of the resulting [digital filter](@entry_id:265006). An analog pole at $s = p_k$ is transformed into a digital pole at $z_k = \exp(p_k T_s)$. This exponential mapping, **$z = \exp(sT_s)$**, governs the fundamental properties of the [impulse invariance method](@entry_id:272647), including stability and [frequency response](@entry_id:183149) characteristics.

Let's explore this mapping by considering how key features of the [s-plane](@entry_id:271584) are transformed into the z-plane. Let the complex variable $s$ be written as $s = \sigma + j\Omega$, where $\sigma$ is the damping factor and $\Omega$ is the continuous-time frequency. The mapping becomes:
$$z = \exp((\sigma + j\Omega)T_s) = \exp(\sigma T_s) \exp(j\Omega T_s)$$
From this polar representation, we can see that the magnitude of $z$ is $|z| = \exp(\sigma T_s)$ and its angle is $\arg(z) = \Omega T_s$.

*   **Mapping the Frequency Axis**: The frequency response of an analog filter is found by evaluating $H_a(s)$ along the [imaginary axis](@entry_id:262618), where $s = j\Omega$ (i.e., $\sigma = 0$). Under the [impulse invariance](@entry_id:266308) mapping, this corresponds to $|z| = \exp(0 \cdot T_s) = 1$ and $\arg(z) = \Omega T_s$. This means the entire imaginary axis of the s-plane maps to the **unit circle** in the z-plane [@problem_id:1726555]. As the analog frequency $\Omega$ sweeps from $-\infty$ to $+\infty$, the angle $\Omega T_s$ also sweeps from $-\infty$ to $+\infty$, causing the point $z$ to traverse the unit circle infinitely many times. This repetitive mapping is the geometric origin of [aliasing](@entry_id:146322), a concept we will explore shortly.

*   **Mapping the Left Half-Plane and Stability**: A stable, causal analog filter has all its poles in the open left half of the [s-plane](@entry_id:271584), meaning $\text{Re}\{p_k\} = \sigma_k  0$ for all poles $p_k$. Consider a vertical line in the [s-plane](@entry_id:271584), $s = \sigma_0 + j\Omega$, where $\sigma_0  0$ is a fixed constant. Under the mapping, this line transforms to a locus in the z-plane with magnitude $|z| = \exp(\sigma_0 T_s)$ and varying angle $\Omega T_s$ [@problem_id:1726589]. Since $\sigma_0  0$ and $T_s > 0$, the magnitude is a constant satisfying $0  \exp(\sigma_0 T_s)  1$. Therefore, any vertical line in the left half of the s-plane maps to a circle centered at the origin within the unit circle.

This property has a critical consequence: **the [impulse invariance method](@entry_id:272647) preserves stability**. If an analog filter is stable, all its poles $p_k$ have a negative real part ($\text{Re}\{p_k\}  0$). The corresponding digital poles $z_k = \exp(p_k T_s)$ will have magnitudes $|z_k| = \exp(\text{Re}\{p_k\}T_s)  1$. Since all poles of the [digital filter](@entry_id:265006) lie strictly inside the unit circle, the resulting [digital filter](@entry_id:265006) is guaranteed to be stable, regardless of the specific analog filter or the choice of [sampling period](@entry_id:265475) $T_s$ [@problem_id:1726531] [@problem_id:1726530].

This direct pole mapping also provides a computational shortcut for finding the denominator of the [digital filter](@entry_id:265006)'s transfer function. Instead of performing the full impulse response transformation, one can find the analog poles $p_k$, compute the digital poles $z_k = \exp(p_k T_s)$, and construct the denominator directly from these poles [@problem_id:1726592]. For instance, for a [second-order filter](@entry_id:265113) with denominator $1 + a_1 z^{-1} + a_2 z^{-2}$, the coefficients are related to the digital poles $z_1, z_2$ by $a_1 = -(z_1 + z_2)$ and $a_2 = z_1 z_2$. Since $z_1 z_2 = \exp(p_1 T_s)\exp(p_2 T_s) = \exp((p_1 + p_2)T_s)$, the coefficient $a_2$ can be calculated directly from the sum of the analog poles.

### Frequency Response and the Inevitability of Aliasing

While the [impulse invariance method](@entry_id:272647) elegantly preserves the time-domain impulse response shape and guarantees stability, its behavior in the frequency domain reveals a significant limitation. The relationship between the digital [frequency response](@entry_id:183149) $H(e^{j\omega})$ and the analog [frequency response](@entry_id:183149) $H_a(j\Omega)$ is not a simple one-to-one mapping but is instead governed by [aliasing](@entry_id:146322).

This relationship can be derived formally using the Poisson summation formula. Starting from the definition $h[n] = T_s h_a(nT_s)$, taking the Discrete-Time Fourier Transform (DTFT) of both sides leads to the fundamental identity of [impulse invariance](@entry_id:266308) [@problem_id:1726573]:

$$H(e^{j\omega}) = \sum_{k=-\infty}^{\infty} H_a\left(j\frac{\omega - 2\pi k}{T_s}\right)$$

where $\omega$ is the normalized [digital frequency](@entry_id:263681) in [radians per sample](@entry_id:269535). This equation states that the frequency response of the digital filter is a periodic summation of infinitely many, frequency-shifted copies of the analog filter's frequency response. The analog frequency axis $\Omega$ is mapped to the digital baseband $\omega \in [-\pi, \pi]$ via the scaling $\Omega = \omega/T_s$. Simultaneously, high-frequency portions of the analog spectrum, centered at $\Omega_k = 2\pi k/T_s$, are shifted and added to this baseband response. This superposition of spectral copies is known as **[aliasing](@entry_id:146322)**.

The practical implication of this aliasing is profound and determines the suitability of the [impulse invariance method](@entry_id:272647) for different filter types [@problem_id:1726578].

*   **Suitability for Low-Pass Filters**: If the analog prototype is a [low-pass filter](@entry_id:145200) whose magnitude $|H_a(j\Omega)|$ is negligible for frequencies beyond the Nyquist frequency, $|\Omega| > \pi/T_s$, then the spectral copies in the summation (terms with $k \neq 0$) will not significantly overlap with the central copy ($k=0$) in the baseband $\omega \in [-\pi, \pi]$. In this scenario, aliasing is minimal, and the digital [frequency response](@entry_id:183149) is a good approximation of the analog response within the baseband:
    $$H(e^{j\omega}) \approx H_a\left(j\frac{\omega}{T_s}\right), \quad \text{for } |\omega| \le \pi$$
    Therefore, the [impulse invariance method](@entry_id:272647) is well-suited for designing low-pass (and some band-pass) filters, provided the [sampling rate](@entry_id:264884) is high enough relative to the filter's bandwidth.

*   **Unsuitability for High-Pass and Band-Stop Filters**: In stark contrast, analog high-pass and band-stop filters are, by definition, not band-limited. Their frequency responses have significant energy at high frequencies, often extending to infinity. When such a filter is converted using [impulse invariance](@entry_id:266308), the [aliasing](@entry_id:146322) effect is severe [@problem_id:1726547]. The high-frequency components of the analog response are "folded" or "aliased" down into the low-frequency range of the digital filter's spectrum. This [spectral folding](@entry_id:188628) catastrophically distorts the filter's characteristic, meaning a [digital filter](@entry_id:265006) designed from a high-pass analog prototype will not exhibit the desired high-pass behavior.

In summary, the [impulse invariance method](@entry_id:272647) provides a direct and stable means of converting an analog filter to a digital IIR filter. Its core strength lies in preserving the shape of the impulse response. However, this [time-domain fidelity](@entry_id:264778) comes at the cost of frequency-domain aliasing. This inherent [aliasing](@entry_id:146322) makes the method highly effective for low-pass filters whose bandwidth is well within the Nyquist limit but renders it fundamentally unsuitable for designing high-pass or band-stop filters.