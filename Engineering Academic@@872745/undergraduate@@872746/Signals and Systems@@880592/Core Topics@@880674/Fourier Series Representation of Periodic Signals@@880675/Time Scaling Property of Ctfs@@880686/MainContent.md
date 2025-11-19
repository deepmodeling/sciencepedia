## Introduction
Time scaling, the act of compressing or expanding a signal along its time axis, is one of the most fundamental operations in signal processing. Whether speeding up an audio recording or stretching an image, this transformation has profound and often counter-intuitive effects on a signal's frequency content. Understanding this relationship is crucial for anyone working with signals, as it governs everything from the pitch of a sound to the constraints of [digital sampling](@entry_id:140476).

This article addresses a core question in the study of [periodic signals](@entry_id:266688): how does [time scaling](@entry_id:260603) precisely affect a signal's Continuous-Time Fourier Series (CTFS) representation? While we may intuitively guess that speeding up a signal increases its frequency, the CTFS provides a rigorous framework to quantify this change and uncover the elegant behavior of the signal's harmonic components.

Across the following chapters, you will gain a complete understanding of this essential property. The first chapter, **Principles and Mechanisms**, delves into the mathematical foundation, deriving the effects of [time scaling](@entry_id:260603) on a signal's period, frequency, and Fourier coefficients. Next, **Applications and Interdisciplinary Connections** demonstrates how this theoretical property is applied in advanced signal processing, [digital sampling](@entry_id:140476), and even in fields like image processing and neuroscience. Finally, the **Hands-On Practices** section provides targeted problems to solidify your knowledge and apply these concepts to practical scenarios.

## Principles and Mechanisms

In our study of signals, we frequently encounter transformations that alter a signal's characteristics. One of the most fundamental of these is **[time scaling](@entry_id:260603)**. This operation, represented by the transformation $y(t) = x(\alpha t)$, either compresses or expands the signal along the time axis. Understanding how [time scaling](@entry_id:260603) affects the frequency domain representation of a periodic signal is crucial for a wide range of applications, from [audio engineering](@entry_id:260890) and music synthesis to the analysis of physical oscillations.

The core of this chapter is to systematically investigate the consequences of [time scaling](@entry_id:260603) on the Continuous-Time Fourier Series (CTFS) of a [periodic signal](@entry_id:261016). We will determine its effect on the signal's fundamental [period and frequency](@entry_id:173341), and more importantly, uncover the elegant and somewhat surprising relationship between the Fourier series coefficients of the original and the scaled signals.

### The Effect of Time Scaling on Period and Frequency

Let us consider a periodic signal $x(t)$ with a [fundamental period](@entry_id:267619) $T_0$, and a corresponding fundamental [angular frequency](@entry_id:274516) $\omega_0 = 2\pi / T_0$. We now generate a new signal, $y(t)$, by scaling the time axis:

$$y(t) = x(\alpha t)$$

where $\alpha$ is a positive, real constant.

What is the nature of $y(t)$? If we think of $t$ as time, when $\alpha > 1$, the argument $\alpha t$ increases more rapidly than $t$. This means that the signal $x(t)$ is traversed "faster," leading to a **time compression**. Conversely, if $0  \alpha  1$, the argument $\alpha t$ progresses more slowly, resulting in a **time expansion**. For instance, in [audio processing](@entry_id:273289), time compression ($\alpha > 1$) corresponds to playing a sound back at a faster speed, which is perceived as an increase in pitch. This pitch increase is a direct manifestation of an increase in the signal's [fundamental frequency](@entry_id:268182) [@problem_id:1769558].

To formalize this, let's find the [fundamental period](@entry_id:267619) of $y(t)$, which we will denote as $T_y$. By definition, $y(t)$ is periodic if there exists a $T_y > 0$ such that $y(t + T_y) = y(t)$ for all $t$. Substituting the definition of $y(t)$:

$$x(\alpha (t + T_y)) = x(\alpha t)$$
$$x(\alpha t + \alpha T_y) = x(\alpha t)$$

Since $x(t)$ is periodic with [fundamental period](@entry_id:267619) $T_0$, its value repeats every time its argument changes by an integer multiple of $T_0$. For the equality above to hold for all $t$, the term $\alpha T_y$ must be equal to $T_0$ (for the [fundamental period](@entry_id:267619) of $y(t)$). This gives us a direct relationship:

$$\alpha T_y = T_0 \implies T_y = \frac{T_0}{\alpha}$$

The new fundamental angular frequency, $\omega_y$, is related to its period $T_y$ by $\omega_y = 2\pi / T_y$. Substituting our result for $T_y$:

$$\omega_y = \frac{2\pi}{T_0 / \alpha} = \alpha \left( \frac{2\pi}{T_0} \right) = \alpha \omega_0$$

These two results are fundamental: [time scaling](@entry_id:260603) a signal by a factor $\alpha$ scales its [fundamental period](@entry_id:267619) by $1/\alpha$ and its [fundamental frequency](@entry_id:268182) by $\alpha$. Time compression ($\alpha > 1$) shrinks the period and increases the frequency, while time expansion ($0  \alpha  1$) stretches the period and decreases the frequency.

This scaling applies not just to the fundamental frequency but to all harmonics as well. The $k$-th harmonic frequency of $x(t)$ is $k\omega_0$. The corresponding $k$-th harmonic frequency of $y(t)$ will be $k\omega_y = k(\alpha\omega_0)$. For example, if an audio signal $v(t)$ with a period of $50.0$ ms is time-compressed by a factor of $\beta = 2.50$ to create a new signal $w(t) = v(2.50 t)$, its original [fundamental frequency](@entry_id:268182) of $1/0.050 = 20$ Hz is increased to $2.50 \times 20 = 50$ Hz. Consequently, the frequency of its third harmonic component would shift from $3 \times 20 = 60$ Hz in the original signal to $3 \times 50 = 150$ Hz in the new signal [@problem_id:1769544].

The set of complex exponential basis functions used to represent the signal also transforms accordingly. The basis functions for $x(t)$ are $\{\exp(j k \omega_0 t)\}$. For the scaled signal $y(t)$, the basis functions become $\{\exp(j k \omega_y t)\}$, which can be expressed in terms of the original frequency as $\{\exp(j k \alpha \omega_0 t)\}$ [@problem_id:1769560].

### The Effect of Time Scaling on Fourier Series Coefficients

Having established how the temporal and frequency characteristics scale, we arrive at the central question: how does this transformation affect the Fourier series coefficients, which represent the harmonic "recipe" of the signal? Let the CTFS coefficients of $x(t)$ be $c_k^x$ and those of $y(t)=x(\alpha t)$ be $c_k^y$. We can determine the relationship between them through two different, yet complementary, perspectives.

#### The Synthesis Perspective

The [synthesis equation](@entry_id:260669) reconstructs the signal from its frequency components:
$$x(t) = \sum_{k=-\infty}^{\infty} c_k^x \exp(j k \omega_0 t)$$

We can construct the time-scaled signal $y(t)$ by simply replacing $t$ with $\alpha t$ in this equation:
$$y(t) = x(\alpha t) = \sum_{k=-\infty}^{\infty} c_k^x \exp(j k \omega_0 (\alpha t))$$

By regrouping the terms in the exponent, we can write this in terms of the new fundamental frequency, $\omega_y = \alpha \omega_0$:
$$y(t) = \sum_{k=-\infty}^{\infty} c_k^x \exp(j k (\alpha \omega_0) t) = \sum_{k=-\infty}^{\infty} c_k^x \exp(j k \omega_y t)$$

Now, let's write the standard [synthesis equation](@entry_id:260669) for $y(t)$ using its own coefficients, $c_k^y$:
$$y(t) = \sum_{k=-\infty}^{\infty} c_k^y \exp(j k \omega_y t)$$

By comparing these last two equations, and leveraging the uniqueness of the Fourier [series representation](@entry_id:175860), we arrive at a remarkably simple and powerful conclusion:

$$c_k^y = c_k^x$$

This means that the Fourier series coefficients themselves are invariant under [time scaling](@entry_id:260603) [@problem_id:1769502] [@problem_id:1769518]. Whether we are analyzing a signal from a function generator, an oscillation in a [magnetically confined plasma](@entry_id:202728), or any other periodic phenomenon, time-compressing or time-expanding the signal does not alter the set of coefficients that describe its harmonic structure [@problem_id:1769524] [@problem_id:1769558].

#### The Analysis Perspective

We can confirm this result through a more formal derivation using the analysis equation, which extracts the coefficients from the signal. The coefficient $c_k^y$ is defined as:

$$c_k^y = \frac{1}{T_y} \int_{T_y} y(t) \exp(-j k \omega_y t) dt$$

where the integral is over any interval of length $T_y$. Let's substitute $y(t) = x(\alpha t)$, $T_y = T_0/\alpha$, and $\omega_y = \alpha \omega_0$:

$$c_k^y = \frac{1}{T_0/\alpha} \int_0^{T_0/\alpha} x(\alpha t) \exp(-j k (\alpha \omega_0) t) dt$$

To evaluate this integral, we perform a change of variables. Let $\tau = \alpha t$. This implies that $t = \tau / \alpha$ and $dt = d\tau / \alpha$. The limits of integration also change: when $t$ goes from $0$ to $T_0/\alpha$, $\tau$ goes from $0$ to $T_0$. Substituting these into the integral:

$$c_k^y = \frac{\alpha}{T_0} \int_0^{T_0} x(\tau) \exp(-j k \omega_0 \tau) \frac{d\tau}{\alpha}$$

The scaling factor $\alpha$ in the numerator and the denominator cancels out:

$$c_k^y = \frac{1}{T_0} \int_0^{T_0} x(\tau) \exp(-j k \omega_0 \tau) d\tau$$

We immediately recognize this final expression as the definition of the original Fourier series coefficient, $c_k^x$. Therefore, we have rigorously proven that $c_k^y = c_k^x$.

The conceptual takeaway is this: [time scaling](@entry_id:260603) does not change the amount of each harmonic present in a signal, but it does change the frequencies at which those harmonics appear. Time compression spreads the same set of harmonic amplitudes over a wider frequency spectrum, while time expansion concentrates them within a narrower spectrum.

### Further Implications of the Time-Scaling Property

The invariance of the Fourier coefficients under [time scaling](@entry_id:260603) leads to several important consequences for other signal properties.

#### Average Power and Parseval's Relation

The average power $P_x$ of a [periodic signal](@entry_id:261016) $x(t)$ is defined as the total energy over one period, divided by the period duration:

$$P_x = \frac{1}{T_0} \int_{T_0} |x(t)|^2 dt$$

How does the average power of $y(t) = x(\alpha t)$, denoted $P_y$, relate to $P_x$?

$$P_y = \frac{1}{T_y} \int_{T_y} |y(t)|^2 dt = \frac{1}{T_0/\alpha} \int_0^{T_0/\alpha} |x(\alpha t)|^2 dt$$

Using the same change of variables, $\tau = \alpha t$, we find:

$$P_y = \frac{\alpha}{T_0} \int_0^{T_0} |x(\tau)|^2 \frac{d\tau}{\alpha} = \frac{1}{T_0} \int_0^{T_0} |x(\tau)|^2 d\tau = P_x$$

The **[average power](@entry_id:271791) of a periodic signal is invariant under [time scaling](@entry_id:260603)**. This makes intuitive sense: compressing a signal in time means you are averaging its squared magnitude over a shorter duration, but the integral of the squared magnitude over that shorter duration is also proportionally smaller.

This result is beautifully confirmed by **Parseval's relation**, which states that the average power is equal to the sum of the squared magnitudes of its Fourier series coefficients:

$$P = \sum_{k=-\infty}^{\infty} |c_k|^2$$

Since we have established that [time scaling](@entry_id:260603) does not change the coefficients ($c_k^y = c_k^x$), it must be true that $\sum |c_k^y|^2 = \sum |c_k^x|^2$. Therefore, $P_y = P_x$. This demonstrates the [self-consistency](@entry_id:160889) of the Fourier series framework [@problem_id:1769511].

It is critical, however, to distinguish average power from the **energy per period**, $E_{per} = P \times T$. While the average power remains constant, the energy per period does not:

$$E_{y,per} = P_y T_y = P_x \left(\frac{T_0}{\alpha}\right) = \frac{1}{\alpha} (P_x T_0) = \frac{1}{\alpha} E_{x,per}$$

The energy contained in one [fundamental period](@entry_id:267619) of a time-expanded signal ($0  \alpha  1$) is greater than that of the original signal, while it is less for a time-compressed signal ($\alpha > 1$).

#### Interaction with Other Signal Operations

The [time-scaling property](@entry_id:263340) can be combined with other elementary signal operations, such as [time shifting](@entry_id:270802) and amplitude scaling.

Consider a signal that is both scaled and shifted, such as $y(t) = x(\alpha t - t_0)$. This can be viewed as $y(t) = x(\alpha(t - t_0/\alpha))$. The Fourier coefficients of $z(t) = x(\alpha t)$ are $c_k^x$. The subsequent time shift by $t_0/\alpha$ introduces a linear phase term. The resulting coefficients for $y(t)$ are $c_k^y = c_k^x \exp(-j k \omega_y (t_0/\alpha))$. Since $\omega_y = \alpha \omega_0$, this simplifies to $c_k^y = c_k^x \exp(-j k \omega_0 t_0)$ [@problem_id:1769531].

Similarly, if a signal undergoes [time scaling](@entry_id:260603), amplitude scaling, and a DC shift, as in $v_{out}(t) = A v_{in}(t/\alpha) + B$, the effects on the Fourier coefficients can be determined systematically. The [time scaling](@entry_id:260603) $v_{in}(t/\alpha)$ leaves the coefficients of $v_{in}(t)$ unchanged. The amplitude scaling by $A$ multiplies all coefficients by $A$. The addition of a constant $B$ only affects the DC ($k=0$) component. If the coefficients of $v_{in}(t)$ are $c_k$, the coefficients of $v_{out}(t)$, let's call them $d_k$, are $d_k = A c_k$ for $k \ne 0$, and $d_0 = A c_0 + B$ [@problem_id:1769505].

#### Invariance of the Gibbs Phenomenon Overshoot

A more profound consequence of the [time-scaling property](@entry_id:263340) relates to the convergence of the Fourier series. For a signal with a jump discontinuity, the partial sum of its Fourier series exhibits an overshoot near the discontinuity, a phenomenon known as the **Gibbs phenomenon**. The peak overshoot, as a percentage of the jump size, is a universal constant of approximately 9% for a symmetric N-term partial sum.

One might wonder if compressing or expanding a signal could alter this behavior. Consider the N-term partial sum for $x(t)$:
$$x_N(t) = \sum_{k=-N}^{N} c_k^x \exp(j k \omega_0 t)$$

The N-term partial sum for the scaled signal $y(t)=x(\alpha t)$ is:
$$y_N(t) = \sum_{k=-N}^{N} c_k^y \exp(j k \omega_y t) = \sum_{k=-N}^{N} c_k^x \exp(j k (\alpha \omega_0) t) = x_N(\alpha t)$$

This shows that the partial sum approximation of the scaled signal is simply the scaled version of the original partial sum. Time scaling only acts on the time axis; it does not alter the amplitude values of the signal or its approximation. A discontinuity of height $\Delta$ in $x(t)$ becomes a discontinuity of the same height $\Delta$ in $y(t)$. The peak value of the overshoot in $y_N(t)$ will be identical to the peak value in $x_N(t)$. Since both the overshoot magnitude and the jump size are invariant under [time scaling](@entry_id:260603), their ratio—the overshoot percentage—must also be invariant [@problem_id:1769545]. This highlights that the Gibbs phenomenon is an [intrinsic property](@entry_id:273674) of representing a discontinuity with sinusoids, independent of the signal's period.

In summary, the [time-scaling property](@entry_id:263340) for the Continuous-Time Fourier Series can be stated as follows:

If a periodic signal $x(t)$ with [fundamental period](@entry_id:267619) $T_0$ and [fundamental frequency](@entry_id:268182) $\omega_0$ has CTFS coefficients $c_k$,
then the time-scaled signal $y(t) = x(\alpha t)$ (for $\alpha > 0$) is also periodic with:
- a new [fundamental period](@entry_id:267619) $T_y = T_0 / \alpha$,
- a new fundamental frequency $\omega_y = \alpha \omega_0$, and
- the **same** set of CTFS coefficients, $c_k$.

This simple, elegant property is a cornerstone of Fourier analysis, providing powerful predictive tools for understanding how temporal transformations manifest in the frequency domain.