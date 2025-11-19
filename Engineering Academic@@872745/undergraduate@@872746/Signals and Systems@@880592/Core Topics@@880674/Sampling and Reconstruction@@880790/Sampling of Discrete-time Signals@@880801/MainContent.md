## Introduction
In the world of digital technology, signals are constantly being passed between systems that operate at different speeds. The ability to change a signal's sampling rate is therefore not just a theoretical curiosity but a practical necessity. This process, known as [multirate signal processing](@entry_id:196803), forms the foundation for [interoperability](@entry_id:750761) in fields like [digital audio](@entry_id:261136) and telecommunications. However, altering the [sampling rate](@entry_id:264884) is a delicate operation; done incorrectly, it can introduce irreversible distortion, but done correctly, it enables highly efficient and powerful signal processing techniques. This article addresses the challenge of how to modify a signal's sampling rate without corrupting its information.

Across the following chapters, you will gain a comprehensive understanding of [discrete-time signal sampling](@entry_id:266385). The journey begins in "Principles and Mechanisms," where we will deconstruct the core operations of decimation (downsampling) and interpolation ([upsampling](@entry_id:275608)), analyzing their effects in both the time and frequency domains. Next, "Applications and Interdisciplinary Connections" will bridge theory and practice, showcasing how these concepts are implemented in real-world systems, from converting audio formats to enabling efficient filter designs and advanced [time-frequency analysis](@entry_id:186268). Finally, "Hands-On Practices" will provide targeted exercises to solidify your grasp of these essential techniques, empowering you to apply them with confidence.

## Principles and Mechanisms

In the domain of [discrete-time signal](@entry_id:275390) processing, it is often necessary to change the [sampling rate](@entry_id:264884) of a signal. This process, known as [multirate signal processing](@entry_id:196803), involves two fundamental operations: decreasing the [sampling rate](@entry_id:264884), or **decimation**, and increasing the [sampling rate](@entry_id:264884), or **interpolation**. While these operations may seem straightforward in the time domain, their effects in the frequency domain are profound and form the basis for a wide array of powerful techniques. This chapter elucidates the principles and mechanisms of these core operations, examining their properties, their spectral consequences, and their application in constructing practical sample-rate conversion systems.

### Core Operations in the Time Domain

We begin by defining the two foundational operations for altering the [sampling rate](@entry_id:264884) of a [discrete-time signal](@entry_id:275390) $x[n]$.

#### Downsampling

Downsampling, also known as decimation, is the process of reducing a signal's [sampling rate](@entry_id:264884) by an integer factor $M$. The operation, performed by a system component often called a **decimator**, produces an output signal $y[n]$ by retaining only every $M$-th sample of the input signal $x[n]$. The mathematical relationship is:

$y[n] = x[nM]$

Here, $n$ is the time index of the new, lower-rate signal. It is clear from this definition that $M-1$ samples are discarded for every one sample that is kept. This is an inherently lossy operation, as information contained in the discarded samples may be lost permanently.

Consider, for example, the downsampling of the discrete-time [unit step function](@entry_id:268807), $u[n]$, by an integer factor $M \ge 2$ [@problem_id:1750367]. The input signal is $x[n] = u[n]$, defined as $1$ for $n \ge 0$ and $0$ otherwise. The output signal is $y[n] = x[nM] = u[nM]$. By the definition of the unit step, $u[nM]$ is $1$ if the index $nM \ge 0$, and $0$ if $nM  0$. Since the factor $M$ is positive, the condition $nM \ge 0$ is equivalent to $n \ge 0$. Consequently, the output signal $y[n]$ is $1$ for $n \ge 0$ and $0$ for $n  0$, which is precisely the definition of the [unit step function](@entry_id:268807) $u[n]$. In this particular case, the downsampled signal is identical to the original: $y[n] = u[n]$. This illustrates that the effect of downsampling is highly signal-dependent.

#### Upsampling

Upsampling, or expansion, is the process of increasing a signal's sampling rate by an integer factor $L$. The most common method, and the one we will focus on, is **[upsampling](@entry_id:275608) by zero-insertion**. This operation, performed by a component called an **expander**, creates the output signal $y[n]$ by inserting $L-1$ zero-valued samples between each consecutive pair of samples from the input signal $x[n]$. The formal definition is:

$$
y[n] = \begin{cases} x[n/L]  \text{if } n \text{ is an integer multiple of } L \\ 0  \text{otherwise} \end{cases}
$$

Unlike downsampling, this operation does not discard any of the original signal's samples. The original information from $x[n]$ is preserved in the samples of $y[n]$ at indices that are multiples of $L$.

A key property of this operation relates to [signal energy](@entry_id:264743). The total energy of a [discrete-time signal](@entry_id:275390) $g[n]$ is defined as $E_g = \sum_{n=-\infty}^{\infty} |g[n]|^2$. If we upsample a signal $x[n]$ to produce $y[n]$, the energy of $y[n]$ consists only of the contributions from its non-zero samples. These non-zero samples occur at indices $n=kL$ for integer $k$, where $y[kL] = x[k]$. Therefore, the energy of the upsampled signal is:

$$
E_y = \sum_{n=-\infty}^{\infty} |y[n]|^2 = \sum_{k=-\infty}^{\infty} |y[kL]|^2 = \sum_{k=-\infty}^{\infty} |x[k]|^2 = E_x
$$

This demonstrates that [upsampling](@entry_id:275608) by zero-insertion preserves the total energy of the signal [@problem_id:1750405]. The energy is simply redistributed over a greater number of time indices in the output signal.

### Fundamental System Properties

When analyzing signal processing operations, it is crucial to characterize them as systems and determine if they possess fundamental properties such as linearity and time-invariance. Let us examine the upsampler as a system $T$ where $y[n] = T\{x[n]\}$.

An upsampler is a **linear** system. To verify this, we must check if it satisfies the [superposition principle](@entry_id:144649): $T\{a_1 x_1[n] + a_2 x_2[n]\} = a_1 T\{x_1[n]\} + a_2 T\{x_2[n]\}$. The output for a combined input $a_1 x_1[n] + a_2 x_2[n]$ is non-zero only at multiples of $L$, where it takes the value $a_1 x_1[n/L] + a_2 x_2[n/L]$. This is identical to computing the upsampled outputs for $x_1[n]$ and $x_2[n]$ separately and then forming the linear combination $a_1 y_1[n] + a_2 y_2[n]$. The property holds.

However, an upsampler is **not a time-invariant** system; it is **time-varying**. A system is time-invariant if a shift in the input, $x[n-n_0]$, causes an identical shift in the output, $y[n-n_0]$. Let's test this [@problem_id:1750354] [@problem_id:1750369].
The output for a shifted input $x[n-n_0]$ is:
$$
T\{x[n-n_0]\} = \begin{cases} x[n/L - n_0]  \text{if } n \text{ is a multiple of } L \\ 0  \text{otherwise} \end{cases}
$$
The shifted original output is:
$$
y[n-n_0] = \begin{cases} x[(n-n_0)/L]  \text{if } n-n_0 \text{ is a multiple of } L \\ 0  \text{otherwise} \end{cases}
$$
These two expressions are clearly not the same. For a simple counterexample, consider $L=2$, $n_0=1$, and the input $x[n] = \delta[n]$. The output for the shifted input $x[n-1]=\delta[n-1]$ is $T\{\delta[n-1]\}$, which has a non-zero value of $\delta[2/2 - 1] = \delta[0] = 1$ at index $n=2$. The shifted original output is $y[n-1]$, where $y[n]=T\{\delta[n]\}=\delta[n]$. Thus, $y[n-1] = \delta[n-1]$, which is non-zero at index $n=1$. Since the outputs are different, the system is not time-invariant. The same conclusion holds for the downsampler. This time-varying nature is a critical characteristic of [multirate systems](@entry_id:264982).

### Frequency Domain Analysis of Rate Changing Operations

The true power and potential pitfalls of [upsampling and downsampling](@entry_id:186158) are revealed in the frequency domain. We use the Discrete-Time Fourier Transform (DTFT), $X(e^{j\omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j\omega n}$, to analyze these effects.

#### The Spectrum of an Upsampled Signal

Let $x[n]$ have a DTFT $X(e^{j\omega})$, and let $y[n]$ be the result of [upsampling](@entry_id:275608) $x[n]$ by a factor $L$. The DTFT of $y[n]$ is:

$$
Y(e^{j\omega}) = \sum_{n=-\infty}^{\infty} y[n] e^{-j\omega n}
$$

Since $y[n]$ is non-zero only for $n=kL$, we can substitute $n=kL$ and $y[kL]=x[k]$:

$$
Y(e^{j\omega}) = \sum_{k=-\infty}^{\infty} y[kL] e^{-j\omega kL} = \sum_{k=-\infty}^{\infty} x[k] e^{-j(L\omega)k}
$$

Recognizing the final summation as the definition of the DTFT of $x[k]$ evaluated at frequency $L\omega$, we arrive at a remarkably simple and important relationship [@problem_id:1750368]:

$$
Y(e^{j\omega}) = X(e^{jL\omega})
$$

This equation signifies that the spectrum of the upsampled signal is a **frequency-compressed** version of the original signal's spectrum. The frequency axis $\omega$ is effectively scaled by $L$. Because the DTFT is $2\pi$-periodic, the original spectrum $X(e^{j\omega})$ from the interval $[-\pi, \pi]$ is compressed into the smaller interval $[-\pi/L, \pi/L]$. This compression causes $L-1$ additional copies, or **images**, of the baseband spectrum to appear within the $[-\pi, \pi]$ interval.

To create a smoothly interpolated signal, these unwanted spectral images must be removed. This is achieved by passing the upsampled signal through a low-pass filter, often called an **[anti-imaging filter](@entry_id:273602)**. To perfectly recover the baseband spectral shape, this filter must pass frequencies up to the edge of the compressed original spectrum and reject everything above it. Therefore, an [ideal low-pass filter](@entry_id:266159) for this purpose would have a [cutoff frequency](@entry_id:276383) of $\omega_c = \pi/L$ [@problem_id:1750387]. To restore the amplitude of the time-domain signal, which was diminished by the insertion of zeros, the filter is typically designed with a [passband](@entry_id:276907) gain of $L$. The combination of an expander and an [anti-imaging filter](@entry_id:273602) constitutes an **interpolator**.

#### The Spectrum of a Downsampled Signal

Now consider downsampling $y[n] = x[nM]$. The derivation of its DTFT, $Y(e^{j\omega})$, is more involved but yields an equally critical result:

$$
Y(e^{j\omega}) = \frac{1}{M} \sum_{k=0}^{M-1} X\left(e^{j\frac{\omega - 2\pi k}{M}}\right)
$$

This expression shows that the spectrum of the downsampled signal is the sum of $M$ frequency-scaled and shifted versions of the original spectrum. The term for $k=0$, which is $\frac{1}{M}X(e^{j\omega/M})$, represents a **frequency-expanded** version of the original spectrum. The frequency axis is stretched by a factor of $M$. The remaining terms for $k=1, \dots, M-1$ represent shifted copies of this expanded spectrum.

If the original signal $x[n]$ is not sufficiently bandlimited, these $M$ spectral components will overlap, causing a distortion known as **aliasing**. Once [aliasing](@entry_id:146322) occurs, the overlapping spectral information is irrevocably mixed, and the original signal cannot be recovered from its downsampled version.

To prevent [aliasing](@entry_id:146322), the input signal must be bandlimited before downsampling. Specifically, the spectral replicas must not overlap. This is guaranteed if the original signal's spectrum $X(e^{j\omega})$ is zero for all frequencies $|\omega| \ge \pi/M$. This is the **Nyquist criterion for decimation**. If this condition holds, then for frequencies in the principal interval $-\pi \lt \omega \le \pi$, only the $k=0$ term in the summation is non-zero, and the relationship simplifies to:

$$
Y(e^{j\omega}) = \frac{1}{M} X\left(e^{j\frac{\omega}{M}}\right) \quad (\text{for } | \omega_{original} | \lt \pi/M)
$$

This principle defines the conditions for perfect [signal recovery](@entry_id:185977) in [multirate systems](@entry_id:264982). For a system that downsamples by a factor $M$ and then upsamples by the same factor, the original signal can be recovered (up to a scaling factor) only if its frequency content is strictly confined to the range $|\omega| \lt \pi/M$ [@problem_id:1750389]. Any frequency components at or above $\pi/M$ in the original signal will be aliased into lower frequencies, corrupting the result. A practical decimator system therefore consists of an **anti-aliasing filter** (a [low-pass filter](@entry_id:145200) with cutoff $\pi/M$) followed by the downsampler.

### Cascaded Systems and Applications

By combining the elementary operations of [upsampling](@entry_id:275608), downsampling, and filtering, we can construct sophisticated systems for [sample rate conversion](@entry_id:276968).

#### Commutativity of Operations

A crucial design consideration is the order of operations. Are [upsampling and downsampling](@entry_id:186158) commutative? That is, does downsampling followed by [upsampling](@entry_id:275608) yield the same result as [upsampling](@entry_id:275608) followed by downsampling? A simple example demonstrates that they are **not commutative** [@problem_id:1750382].

Consider the signal $x[n] = \{1, 2, 3, 4\}$ for $n=0, 1, 2, 3$.
- **Pipeline A (Downsample then Upsample):** Downsampling by $M=2$ yields an intermediate signal $\{x[0], x[2]\} = \{1, 3\}$. Upsampling this by $L=2$ yields the final output $y_A[n] = \{1, 0, 3, 0\}$.
- **Pipeline B (Upsample then Downsample):** Upsampling by $L=2$ yields an intermediate signal $\{1, 0, 2, 0, 3, 0, 4, 0\}$. Downsampling this by $M=2$ by taking every second sample gives $y_B[n] = \{1, 2, 3, 4\}$.

Clearly, $y_A[n] \neq y_B[n]$. Pipeline B, which performs [upsampling](@entry_id:275608) first, results in perfect reconstruction of the original signal ($y_B[n] = x[n]$). In contrast, Pipeline A results in a loss of information, as the samples $x[1]$ and $x[3]$ are discarded in the initial downsampling step and can never be recovered. This illustrates a general principle: a downsampler followed by an upsampler with the same factor $M$ effectively sets samples to zero, while an upsampler followed by a downsampler is an identity operation. For this reason, systems for rational [sample rate conversion](@entry_id:276968) almost always place the upsampler first.

#### Sample Rate Conversion by a Rational Factor

To change a signal's [sampling rate](@entry_id:264884) by a rational factor $L/M$, we can cascade an upsampler, a filter, and a downsampler. The standard and most efficient configuration is:

1.  **Upsample** by a factor of $L$.
2.  Pass the result through a **Low-Pass Filter**.
3.  **Downsample** the filtered signal by a factor of $M$.

The [low-pass filter](@entry_id:145200) serves a dual purpose: it is an [anti-imaging filter](@entry_id:273602) for the upsampler and an anti-aliasing filter for the downsampler. To satisfy both roles, its [cutoff frequency](@entry_id:276383) $\omega_c$ must be the more restrictive of the two individual requirements: $\omega_c = \min(\pi/L, \pi/M)$.

A complete numerical example can solidify this process [@problem_id:1750380]. Let's change the rate of a signal by a factor of $2/3$, meaning $L=2$ and $M=3$. The input signal is $x[n] = \cos(\frac{\pi n}{2})$ for $0 \le n \le 4$, which is the sequence $\{1, 0, -1, 0, 1\}$.
1.  **Upsample by $L=2$:** We insert one zero between each sample to get the expanded signal $x_u[n] = \{1, 0, 0, 0, -1, 0, 0, 0, 1\}$.
2.  **Filter:** We apply a simple linear interpolation filter with impulse response $h[n] = \{1/2, 1, 1/2\}$ centered at $n=0$. The output is $v[n] = x_u[n] * h[n]$. The convolution gives $v[n] = \frac{1}{2}x_u[n+1] + x_u[n] + \frac{1}{2}x_u[n-1]$. This "fills in" the zeros, producing the sequence $v[n] = \{\dots, \frac{1}{2}, 1, \frac{1}{2}, 0, -\frac{1}{2}, -1, -\frac{1}{2}, 0, \frac{1}{2}, 1, \frac{1}{2}, \dots\}$.
3.  **Downsample by $M=3$:** We take every third sample of $v[n]$ to get the final output $y[m] = v[3m]$.
    - $y[0] = v[0] = 1$
    - $y[1] = v[3] = -1/2$
    - $y[2] = v[6] = 0$
    - $y[3] = v[9] = 1/2$
The final output sequence is $\{1, -1/2, 0, 1/2\}$.

This process of [upsampling](@entry_id:275608), filtering, and downsampling forms the backbone of digital [sample rate conversion](@entry_id:276968). When the filters are designed correctly, this cascade can act as a near-perfect identity system for signals that meet the appropriate bandlimiting criteria. For instance, a system with [upsampling](@entry_id:275608) factor $M$, an ideal LPF with gain $M$ and cutoff $\pi/M$, and a downsampling factor $M$ will perfectly reconstruct any input signal $x[n]$ that is bandlimited to $|\omega| \lt \pi/M$. The frequency domain analysis confirms this: $X(e^{j\omega}) \to X(e^{jM\omega}) \to M \cdot X(e^{jM\omega}) \to \frac{1}{M}[M \cdot X(e^{jM(\omega/M)})] = X(e^{j\omega})$ [@problem_id:1750377]. This demonstrates the theoretical elegance and practical power of [multirate signal processing](@entry_id:196803) principles.