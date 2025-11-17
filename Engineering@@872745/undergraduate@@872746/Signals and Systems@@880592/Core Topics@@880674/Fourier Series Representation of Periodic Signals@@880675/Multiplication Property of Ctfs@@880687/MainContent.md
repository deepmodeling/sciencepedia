## Introduction
The multiplication of signals is a fundamental operation in signals and systems, from modulating a carrier wave in communications to analyzing the effects of non-linear components. While simple in the time domain, this operation has profound and non-intuitive consequences in the frequency domain. This article demystifies the relationship between [time-domain multiplication](@entry_id:275182) and its frequency-domain counterpart for continuous-time [periodic signals](@entry_id:266688), addressing the crucial question: what happens to the spectrum when two signals are multiplied?

This article will guide you through the multiplication property of the Continuous-Time Fourier Series (CTFS). In "Principles and Mechanisms," we will derive the core theorem that [time-domain multiplication](@entry_id:275182) corresponds to [frequency-domain convolution](@entry_id:265059) and establish the preconditions for its application. Following that, "Applications and Interdisciplinary Connections" will demonstrate the property's power in real-world scenarios, including [amplitude modulation](@entry_id:266006), signal analysis, and understanding [non-linear systems](@entry_id:276789). Finally, "Hands-On Practices" will provide opportunities to solidify your understanding through targeted problems, bridging theory with practical application.

## Principles and Mechanisms

In our study of [signals and systems](@entry_id:274453), we frequently encounter operations that combine or modify signals. One of the most fundamental of these operations is multiplication. Whether it is a message signal being modulated by a [carrier wave](@entry_id:261646) or a signal being passed through a time-varying filter, the multiplication of two signals is a ubiquitous phenomenon. This chapter delves into the frequency-domain consequences of multiplying two continuous-time [periodic signals](@entry_id:266688). We will establish the core principle that [time-domain multiplication](@entry_id:275182) corresponds to [frequency-domain convolution](@entry_id:265059) and explore the profound implications of this relationship for [signal analysis](@entry_id:266450) and system design.

### Prerequisites: Periodicity of Product Signals

Before we can apply the Continuous-Time Fourier Series (CTFS), the resulting signal must be periodic. A natural first question, therefore, is: if we multiply two [periodic signals](@entry_id:266688), is the product also guaranteed to be periodic?

Consider two [periodic signals](@entry_id:266688), $x_1(t)$ and $x_2(t)$, with fundamental periods $T_1$ and $T_2$, respectively. Their product is $z(t) = x_1(t)x_2(t)$. For $z(t)$ to be periodic with some period $T$, it must satisfy $z(t+T) = z(t)$ for all $t$. This means $x_1(t+T)x_2(t+T) = x_1(t)x_2(t)$. A sufficient condition for this to hold is that $T$ is a common period for both $x_1(t)$ and $x_2(t)$. This requires that $T$ be an integer multiple of both $T_1$ and $T_2$. That is, there must exist positive integers $n_1$ and $n_2$ such that:
$T = n_1 T_1 = n_2 T_2$

This equality can be rearranged to reveal a critical condition on the ratio of the periods:
$$
\frac{T_1}{T_2} = \frac{n_2}{n_1}
$$
This demonstrates that a common period $T$ can only exist if the ratio of the fundamental periods $T_1/T_2$ is a rational number. This condition is both necessary and sufficient to guarantee that the product of two [periodic signals](@entry_id:266688) is also periodic [@problem_id:1736945]. If the ratio is irrational, the product signal will not be periodic, and a Fourier [series representation](@entry_id:175860) is not applicable.

Once we establish that the product signal is periodic, we must determine its **[fundamental period](@entry_id:267619)**, $T_0$. The [fundamental period](@entry_id:267619) is the *smallest* positive value $T$ for which $z(t+T) = z(t)$. This corresponds to the least common multiple (LCM) of the individual fundamental periods, $T_0 = \operatorname{lcm}(T_1, T_2)$. Equivalently, in the frequency domain, the new [fundamental frequency](@entry_id:268182) $f_0 = 1/T_0$ is the greatest common divisor (GCD) of the individual fundamental frequencies, $f_0 = \gcd(f_1, f_2)$.

For instance, if a signal $x_1(t)$ has a fundamental frequency $f_1 = 20$ Hz ($T_1 = 1/20$ s) and it is multiplied by a signal $x_2(t)$ with a fundamental frequency $f_2 = 12.5$ Hz ($T_2 = 1/12.5 = 2/25$ s), the ratio of periods is $T_1/T_2 = (1/20) / (2/25) = 25/40 = 5/8$, which is rational. The product signal is therefore periodic. Its [fundamental frequency](@entry_id:268182) is $f_0 = \gcd(20, 12.5) = \gcd(40/2, 25/2) = \frac{\gcd(40,25)}{2} = 5/2 = 2.5$ Hz. The corresponding [fundamental period](@entry_id:267619) is $T_0 = 1/f_0 = 1/2.5 = 2/5 = 0.4$ seconds [@problem_id:1736962]. This new [fundamental period](@entry_id:267619) $T_0$ (and its corresponding fundamental frequency $\omega_0 = 2\pi/T_0$) forms the basis for the Fourier series analysis of the product signal.

### The Multiplication Property: Time Multiplication, Frequency Convolution

Having established the conditions for periodicity, we can now derive one of the most elegant and powerful properties of the Fourier series. Let $x(t)$ and $w(t)$ be two signals that are periodic with a common [fundamental period](@entry_id:267619) $T$, and let their CTFS coefficient sequences be $\{X_k\}$ and $\{W_k\}$, respectively. We define a new signal $y(t)$ as their product:
$$
y(t) = x(t)w(t)
$$
To find the Fourier series coefficients $Y_k$ of $y(t)$, we apply the analysis formula:
$$
Y_k = \frac{1}{T} \int_{T} y(t) e^{-j k \omega_0 t} dt = \frac{1}{T} \int_{T} x(t)w(t) e^{-j k \omega_0 t} dt
$$
The key step is to substitute the synthesis formula for one of the signals, say $x(t) = \sum_{m=-\infty}^{\infty} X_m e^{j m \omega_0 t}$, into this integral:
$$
Y_k = \frac{1}{T} \int_{T} \left( \sum_{m=-\infty}^{\infty} X_m e^{j m \omega_0 t} \right) w(t) e^{-j k \omega_0 t} dt
$$
Assuming uniform convergence, we can interchange the order of integration and summation:
$$
Y_k = \sum_{m=-\infty}^{\infty} X_m \left( \frac{1}{T} \int_{T} w(t) e^{j m \omega_0 t} e^{-j k \omega_0 t} dt \right)
$$
Combining the exponential terms inside the integral gives:
$$
Y_k = \sum_{m=-\infty}^{\infty} X_m \left( \frac{1}{T} \int_{T} w(t) e^{-j (k-m) \omega_0 t} dt \right)
$$
We immediately recognize the expression within the parentheses. It is nothing more than the CTFS analysis formula for the coefficient of $w(t)$ at the harmonic index $(k-m)$. Thus, this expression is equal to $W_{k-m}$.

Substituting this back, we arrive at the final, fundamental result [@problem_id:2895806]:
$$
Y_k = \sum_{m=-\infty}^{\infty} X_m W_{k-m}
$$
This equation defines the **[discrete convolution](@entry_id:160939)** of the sequences $\{X_k\}$ and $\{W_k\}$. Symbolically, we write $Y_k = (X * W)[k]$. This reveals a profound duality: while time-domain convolution corresponds to frequency-domain multiplication, **[time-domain multiplication](@entry_id:275182) corresponds to [frequency-domain convolution](@entry_id:265059)**.

### Applications and Interpretations

The convolution relationship is not merely a mathematical curiosity; it provides deep insights into the behavior of [signals and systems](@entry_id:274453).

#### Amplitude Modulation

One of the most direct applications of the multiplication property is in understanding **[amplitude modulation](@entry_id:266006) (AM)**. In AM, a lower-frequency message signal $x(t)$ is multiplied by a high-frequency sinusoidal carrier signal to shift the message's spectral content to a higher frequency band.

Let's consider modulating a signal $x(t)$ with coefficients $a_k$ by a simple cosine carrier, $w(t) = \cos(M\omega_0 t)$, where $M$ is an integer. First, we find the Fourier coefficients of the carrier. Using Euler's formula, $w(t) = \frac{1}{2} e^{jM\omega_0 t} + \frac{1}{2} e^{-jM\omega_0 t}$. By inspection, the only non-zero coefficients, which we'll call $W_k$, are:
$$
W_M = \frac{1}{2} \quad \text{and} \quad W_{-M} = \frac{1}{2}
$$
Now, let $y(t) = x(t)\cos(M\omega_0 t)$. The coefficients of $y(t)$, denoted $b_k$, are given by the convolution $b_k = \sum_{m=-\infty}^{\infty} a_m W_{k-m}$. Since $W_l$ is non-zero only for $l = \pm M$, the infinite sum collapses to just two terms, corresponding to when $k-m = M$ (so $m=k-M$) and when $k-m=-M$ (so $m=k+M$):
$$
b_k = a_{k-M}W_M + a_{k+M}W_{-M} = a_{k-M} \left(\frac{1}{2}\right) + a_{k+M} \left(\frac{1}{2}\right)
$$
So, for $y(t) = x(t)\cos(7\omega_0t)$, the resulting coefficients are $b_k = \frac{1}{2}(a_{k-7} + a_{k+7})$ [@problem_id:1736965]. This elegant result shows that the spectrum of the modulated signal is composed of two copies of the original signal's spectrum, each scaled by $1/2$ and shifted to be centered at frequencies $\pm M\omega_0$.

#### Bandwidth Expansion

The convolution property also dictates how the "bandwidth" of signals combines. In the context of the Fourier series, we can consider the bandwidth to be the highest harmonic index $N$ for which the coefficient $a_k$ is non-zero. A signal is **band-limited** if its coefficients are zero for all $|k| > N$.

Suppose we multiply two [band-limited signals](@entry_id:269973): $x(t)$ with highest harmonic $N$ (i.e., $a_k=0$ for $|k|>N$) and $y(t)$ with highest harmonic $M$ (i.e., $b_l=0$ for $|l|>M$). Let the product be $z(t)$ with coefficients $c_k = (a*b)[k]$. The coefficient $c_k$ can be non-zero only if there is an index $m$ where $a_m \neq 0$ and $b_{k-m} \neq 0$. This requires $|m| \le N$ and $|k-m| \le M$. The maximum possible value for the index $k$ occurs when we add the maximum possible values of the indices $m$ and $k-m$. By the [triangle inequality](@entry_id:143750), $|k| = |m + (k-m)| \le |m| + |k-m|$. Therefore, the maximum value for $|k|$ is $N+M$.

This means the highest possible non-zero harmonic of the product signal is $K_{max} = N+M$. For example, if a signal $x(t)$ with highest harmonic $5$ is multiplied by a signal $y(t)$ with highest harmonic $12$, the resulting signal $z(t)$ will have a highest possible harmonic of $5+12=17$ [@problem_id:1736949]. This principle is fundamental: **multiplication in the time domain generally leads to an expansion of bandwidth in the frequency domain**.

#### Symmetry Properties

The multiplication property also preserves the deep connection between time-domain symmetry and frequency-domain properties. Consider the product of a real, even signal $x(t)$ and a real, odd signal $y(t)$. Their product, $z(t) = x(t)y(t)$, is a real, odd signal, since $z(-t) = x(-t)y(-t) = x(t)[-y(t)] = -z(t)$.

We know that the CTFS coefficients of a real and odd signal must be purely imaginary. Furthermore, for any real signal, the coefficients must exhibit [conjugate symmetry](@entry_id:144131): $D_{-k} = D_k^*$. If $D_k$ is purely imaginary, then $D_k^* = -D_k$. Combining these facts, we find that the coefficients must satisfy $D_{-k} = -D_k$, which is the definition of an odd sequence. Therefore, the coefficients $D_k$ of the product signal $z(t)$ are a purely imaginary and odd sequence [@problem_id:1736955].

### Worked Examples and Advanced Cases

Let's solidify our understanding with a few examples that showcase the application of the multiplication property in various scenarios.

#### Example 1: Direct Convolution with a Pulse Train

Consider finding the CTFS coefficients $c_k$ of the signal $y(t) = x_1(t)x_2(t)$, where $x_1(t) = C_1\cos(\omega_0 t) + C_2\cos(3\omega_0 t)$ and $x_2(t)$ is a periodic square wave that is 1 for the first half of the period and 0 for the second.
The coefficients of $x_1(t)$, denoted $a_m$, are sparse: $a_{\pm 1} = C_1/2$ and $a_{\pm 3} = C_2/2$. The coefficients of the square wave, $b_k$, are $b_0 = 1/2$ and $b_k = \frac{1}{j\pi k}$ for odd $k$, and zero for other non-zero even $k$.
The coefficients of the product are $c_k = \sum_m a_m b_{k-m}$. Due to the sparsity of $\{a_m\}$, this sum becomes:
$$
c_k = a_{-3}b_{k+3} + a_{-1}b_{k+1} + a_1 b_{k-1} + a_3 b_{k-3}
$$
$$
c_k = \frac{C_2}{2}b_{k+3} + \frac{C_1}{2}b_{k+1} + \frac{C_1}{2}b_{k-1} + \frac{C_2}{2}b_{k-3}
$$
This expression can then be evaluated for different cases of $k$ (e.g., even, odd) by substituting the appropriate values for the $b_k$ coefficients, demonstrating a direct application of the convolution formula [@problem_id:1736940].

#### Example 2: Harmonically Related Periods

What if the signals have periods that are harmonically related but not equal? Suppose $x_1(t)$ has period $T$ (frequency $\omega_0$) and $x_2(t)$ has period $T/2$ (frequency $2\omega_0$). The product $z(t) = x_1(t)x_2(t)$ has a [fundamental period](@entry_id:267619) of $T$. We use $\omega_0$ as the [fundamental frequency](@entry_id:268182) for the analysis. The series are:
$$
x_1(t) = \sum_{k=-\infty}^{\infty} a_k e^{jk\omega_0 t} \quad \text{and} \quad x_2(t) = \sum_{l=-\infty}^{\infty} b_l e^{jl(2\omega_0) t}
$$
The product is:
$$
z(t) = \left( \sum_{k} a_k e^{jk\omega_0 t} \right) \left( \sum_{l} b_l e^{j2l\omega_0 t} \right) = \sum_{k,l} a_k b_l e^{j(k+2l)\omega_0 t}
$$
To find the coefficient $c_n$ of $z(t)$, we collect all terms where the harmonic index is $n$. This occurs when $n = k+2l$, or $k = n-2l$. Summing over all possible combinations (i.e., summing over all $l$), we get:
$$
c_n = \sum_{l=-\infty}^{\infty} a_{n-2l} b_l
$$
This is a modified [convolution sum](@entry_id:263238) where the indices of the first sequence are "skipped" by a factor of 2, reflecting the harmonic relationship between the two original signals [@problem_id:1736923].

#### Example 3: Combining Properties

The true power of Fourier analysis lies in combining properties to solve complex problems. Consider finding the coefficients $c_k$ of the signal $z(t) = x(t) \frac{dx(t)}{dt}$, where $x(t) = \cos^2(\omega_0 t)$.
This is a two-step problem.
1.  **Differentiation Property**: First, find the coefficients of $y(t) = \frac{dx(t)}{dt}$. If $x(t) \leftrightarrow a_k$, then $y(t) \leftrightarrow b_k = j k \omega_0 a_k$.
2.  **Multiplication Property**: Second, find the coefficients of the product $z(t) = x(t)y(t)$, which are given by the convolution $c_k = \sum_l a_l b_{k-l}$.

For $x(t) = \cos^2(\omega_0 t) = \frac{1}{2} + \frac{1}{2}\cos(2\omega_0 t)$, the non-zero coefficients are $a_0 = 1/2$ and $a_{\pm 2} = 1/4$.
The non-zero coefficients of the derivative are $b_0 = 0$ and $b_{\pm 2} = j(\pm 2)\omega_0 a_{\pm 2} = \pm j \frac{\omega_0}{2}$.
The [convolution sum](@entry_id:263238) $c_k = a_{-2}b_{k+2} + a_0 b_k + a_2 b_{k-2}$ can then be evaluated. For example, the DC coefficient $c_0$ is $c_0 = a_{-2}b_2 + a_0 b_0 + a_2 b_{-2} = \frac{1}{4}(j\frac{\omega_0}{2}) + 0 + \frac{1}{4}(-j\frac{\omega_0}{2}) = 0$. This makes physical sense, as $z(t) = \frac{1}{2}\frac{d}{dt}[x(t)^2]$. The integral of the derivative of any periodic function over one full period is zero, which confirms that the DC component $c_0$ must be zero. By evaluating the convolution for all $k$, we can find the complete spectrum of the product signal [@problem_id:1736918].

In summary, the multiplication property is a cornerstone of Fourier analysis. It provides the essential link between the time-domain operation of multiplication and the frequency-domain operation of convolution. This principle is indispensable for understanding phenomena ranging from [amplitude modulation](@entry_id:266006) and [signal sampling](@entry_id:261929) to the interaction of signals in nonlinear systems.