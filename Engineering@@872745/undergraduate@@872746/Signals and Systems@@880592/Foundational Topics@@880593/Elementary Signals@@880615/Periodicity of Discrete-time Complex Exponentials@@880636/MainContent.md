## Introduction
The [discrete-time complex exponential](@entry_id:264089), $x[n] = e^{j\omega_0 n}$, is one of the most important signals in digital signal processing (DSP). It serves as the fundamental building block for representing more complex signals through the powerful framework of Fourier analysis. However, unlike its always-periodic continuous-time counterpart, the discrete-time exponential exhibits a unique and conditional [periodicity](@entry_id:152486) that is central to understanding the behavior of digital systems. This article addresses the crucial principles that determine when these signals are periodic and what consequences arise from these properties. By exploring this topic, you will gain a deep understanding of the mathematical foundations that underpin many modern digital technologies.

The following chapters will guide you through this essential concept. First, **Principles and Mechanisms** will lay out the mathematical condition for [periodicity](@entry_id:152486), explain the surprising phenomenon of frequency [aliasing](@entry_id:146322), and show how to calculate the [fundamental period](@entry_id:267619) for single and composite signals. Next, **Applications and Interdisciplinary Connections** will bridge this theory to practice, demonstrating its impact on [signal synthesis](@entry_id:272649), [sampling rate conversion](@entry_id:274165), Fourier transforms, and even advanced fields like multidimensional signal processing and digital control. Finally, **Hands-On Practices** will offer a set of curated problems to help you solidify your knowledge and apply these principles to practical scenarios.

## Principles and Mechanisms

In our study of [discrete-time signals](@entry_id:272771), the complex exponential sequence, $x[n] = e^{j\omega_0 n}$, stands out as a fundamental building block. Its properties form the basis for understanding more complex signals through frameworks like the Fourier series and transform. A primary characteristic that governs the behavior of these signals is [periodicity](@entry_id:152486). This chapter delves into the principles that determine whether a [discrete-time complex exponential](@entry_id:264089) is periodic, the unique nature of discrete-time frequency, and how these properties extend to composite signals.

### The Periodicity Condition for Discrete-Time Exponentials

A [discrete-time signal](@entry_id:275390) $x[n]$ is defined as **periodic** if there exists a positive integer $N$ for which the signal repeats itself, meaning $x[n+N] = x[n]$ for all integers $n$. The smallest such positive integer $N$ is called the **[fundamental period](@entry_id:267619)**.

Let us apply this definition to the [complex exponential](@entry_id:265100) signal $x[n] = e^{j\omega_0 n}$, where $\omega_0$ is the discrete-time [angular frequency](@entry_id:274516) in [radians per sample](@entry_id:269535). For [periodicity](@entry_id:152486), we require:
$$ e^{j\omega_0 (n+N)} = e^{j\omega_0 n} $$
Using the law of exponents, we can write the left side as $e^{j\omega_0 n} e^{j\omega_0 N}$. The equality thus simplifies to:
$$ e^{j\omega_0 N} = 1 $$
This is a crucial result. It shows that the periodicity of the signal depends only on the frequency $\omega_0$ and the period $N$, not on the time index $n$. From Euler's formula, we know that $e^{j\theta} = 1$ if and only if $\theta$ is an integer multiple of $2\pi$. Therefore, the condition for [periodicity](@entry_id:152486) is:
$$ \omega_0 N = 2\pi k $$
for some non-zero integer $k$. Rearranging this equation gives:
$$ \frac{\omega_0}{2\pi} = \frac{k}{N} $$
This equation reveals the fundamental condition for the [periodicity](@entry_id:152486) of a [discrete-time complex exponential](@entry_id:264089): **a signal $x[n] = e^{j\omega_0 n}$ is periodic if and only if its angular frequency $\omega_0$ is a rational multiple of $2\pi$**.

This distinguishes discrete-time exponentials from their continuous-time counterparts, $x(t) = e^{j\Omega_0 t}$, which are *always* periodic for any non-zero frequency $\Omega_0$. In discrete time, if the ratio $\omega_0 / (2\pi)$ is irrational, no integer values for $k$ and $N$ can satisfy the condition, and the signal is **aperiodic**. For instance, a signal generated with a frequency of $\omega_0 = 3$ rad/sample is aperiodic because $\omega_0/(2\pi) = 3/(2\pi)$ is an irrational number [@problem_id:1741186]. In contrast, a signal with $\omega_0 = 3\pi/5$ is periodic because $\omega_0/(2\pi) = (3\pi/5)/(2\pi) = 3/10$, which is rational.

Once [periodicity](@entry_id:152486) is established, we can determine the [fundamental period](@entry_id:267619), $N_0$. This is the smallest positive integer $N$ that satisfies $\omega_0 N = 2\pi k$. To find it, we first express the ratio $\omega_0/(2\pi)$ as a fraction in lowest terms:
$$ \frac{\omega_0}{2\pi} = \frac{m}{p} $$
where $m$ and $p$ are integers with no common factors ($\text{gcd}(m, p) = 1$) and $p > 0$. The periodicity condition becomes $\frac{m}{p} N = k$. The smallest positive integer $N$ that makes $k$ an integer is $N = p$. Thus, the [fundamental period](@entry_id:267619) is $p$.

As an example from a digital oscillator design, consider the signal $x[n] = \exp(j \frac{5\pi}{9} n)$ [@problem_id:1711976]. To find its [fundamental period](@entry_id:267619), we compute the ratio:
$$ \frac{\omega_0}{2\pi} = \frac{5\pi/9}{2\pi} = \frac{5}{18} $$
Since this fraction is already in lowest terms ($\text{gcd}(5, 18) = 1$), we can directly identify the [fundamental period](@entry_id:267619) as the denominator, $N_0 = 18$. This means the sequence of values will take exactly 18 steps to repeat its pattern.

### Frequency Aliasing: A Unique Property of Discrete Time

A surprising and critically important property of [discrete-time signals](@entry_id:272771) is that distinct frequencies do not necessarily produce distinct signals. Consider two frequencies, $\omega_1$ and $\omega_2$, that differ by an integer multiple of $2\pi$:
$$ \omega_2 = \omega_1 + 2\pi k, \quad \text{for some integer } k $$
Let's examine the signal generated by $\omega_2$:
$$ x_2[n] = e^{j\omega_2 n} = e^{j(\omega_1 + 2\pi k)n} = e^{j\omega_1 n} e^{j2\pi kn} $$
Since $n$ and $k$ are both integers, their product $kn$ is also an integer. Therefore, $e^{j2\pi kn} = \cos(2\pi kn) + j\sin(2\pi kn) = 1$ for all $n$. This leads to a remarkable conclusion:
$$ e^{j(\omega_1 + 2\pi k)n} = e^{j\omega_1 n} $$
Frequencies separated by an integer multiple of $2\pi$ are indistinguishable in [discrete time](@entry_id:637509); they are **aliases** of one another. This implies that all unique complex exponential sequences are generated by frequencies within any single interval of length $2\pi$. By convention, this is often chosen as the **principal range** of $[0, 2\pi)$ or $[-\pi, \pi)$.

For example, a signal generated with a frequency $\omega_0 = 19\pi/6$ appears to have a high frequency. However, we can find its alias within the principal range $[0, 2\pi)$ by subtracting multiples of $2\pi$ [@problem_id:1741158].
$$ \frac{19\pi}{6} = \frac{12\pi + 7\pi}{6} = 2\pi + \frac{7\pi}{6} $$
The equivalent frequency in the principal range is $\omega_s = 7\pi/6$. The signals $e^{j(19\pi/6)n}$ and $e^{j(7\pi/6)n}$ are identical for all $n$. Similarly, a signal with frequency $\omega_0 = -3\pi/5$ is identical to signals with frequencies $\omega_A = -3\pi/5 + 2\pi = 7\pi/5$, $\omega_C = -3\pi/5 - 2\pi = -13\pi/5$, and $\omega_E = -3\pi/5 + 4\pi = 17\pi/5$, as they all differ from $-3\pi/5$ by an integer multiple of $2\pi$ [@problem_id:1741172].

### Fundamental Period and the Set of Distinct Periodic Exponentials

We can now connect the concepts of fundamental [period and frequency](@entry_id:173341) aliasing to answer more specific questions. For a given [fundamental period](@entry_id:267619) $N_0$, what are the possible frequencies $\omega_0$ that produce it?

Recall that for a frequency $\omega_0 = \frac{2\pi k}{N}$, the [fundamental period](@entry_id:267619) is $N_0 = \frac{N}{\text{gcd}(k, N)}$. If we require the [fundamental period](@entry_id:267619) to be exactly $N_0$, we must have:
$$ N_0 = \frac{N_0}{\text{gcd}(k, N_0)} \implies \text{gcd}(k, N_0) = 1 $$
This means the integer $k$ must be [relatively prime](@entry_id:143119) (coprime) to $N_0$. The valid frequencies that produce a [fundamental period](@entry_id:267619) of $N_0$ are therefore of the form $\omega_0 = \frac{2\pi k}{N_0}$ where $\text{gcd}(k, N_0) = 1$.

As a reverse-engineering problem, if we observe a sequence has a [fundamental period](@entry_id:267619) of $N_0=10$, we can determine the smallest positive frequency $\omega_0$ that could have generated it [@problem_id:1741139]. The possible frequencies are $\omega_0 = \frac{2\pi k}{10}$ with $\text{gcd}(k, 10)=1$. To find the smallest positive $\omega_0$, we choose the smallest positive integer $k$ coprime to 10, which is $k=1$. This gives $\omega_0 = \frac{2\pi}{10} = \frac{\pi}{5}$.

This principle also allows us to count how many distinct signals exist for a given [fundamental period](@entry_id:267619). By restricting the frequencies to the principal range $[0, 2\pi)$, we constrain $k$ to the range $0 \le k \lt N_0$. The number of distinct signals with [fundamental period](@entry_id:267619) $N_0$ is therefore the number of integers $k$ in the set $\{0, 1, \dots, N_0-1\}$ that are [relatively prime](@entry_id:143119) to $N_0$. This quantity is given by **Euler's totient function**, $\phi(N_0)$.

For instance, to design a generator that can produce all unique signals with a [fundamental period](@entry_id:267619) of exactly $N_0=12$, we need to find how many such signals exist [@problem_id:1741162]. We count the integers $k$ such that $0 \le k  12$ and $\text{gcd}(k, 12)=1$. The integers are $1, 5, 7, 11$. There are 4 such integers, so $\phi(12)=4$. This means there are exactly four distinct [complex exponential signals](@entry_id:273867) in the principal frequency range that have a [fundamental period](@entry_id:267619) of 12.

### Superposition and Periodicity of Composite Signals

When signals are combined, typically through addition, the [periodicity](@entry_id:152486) of the resulting composite signal depends on the periods of its components. Consider a signal $x[n]$ formed by the sum of two signals, $x[n] = x_1[n] + x_2[n]$. For $x[n]$ to be periodic with period $N$, we must have $x[n+N] = x[n]$. This requires:
$$ x_1[n+N] + x_2[n+N] = x_1[n] + x_2[n] $$
A sufficient condition for this to hold is that $N$ is a period for *both* $x_1[n]$ and $x_2[n]$ simultaneously (note that non-zero amplitudes or phase shifts do not affect periodicity [@problem_id:1741206]). If $x_1[n]$ has [fundamental period](@entry_id:267619) $N_1$ and $x_2[n]$ has [fundamental period](@entry_id:267619) $N_2$, then $N$ must be a common multiple of $N_1$ and $N_2$. The [fundamental period](@entry_id:267619) of the sum, $N_0$, will be the smallest such positive integer, which is the **[least common multiple](@entry_id:140942) (LCM)** of the individual fundamental periods.
$$ N_0 = \text{lcm}(N_1, N_2) $$
For example, if a musical tone is synthesized by combining two signals with frequencies $\omega_1 = 3\pi/5$ and $\omega_2 = 5\pi/6$, we first find their individual fundamental periods [@problem_id:1741138]:
-   For $\omega_1 = 3\pi/5$, we have $\frac{\omega_1}{2\pi} = \frac{3}{10}$. So, $N_1 = 10$.
-   For $\omega_2 = 5\pi/6$, we have $\frac{\omega_2}{2\pi} = \frac{5}{12}$. So, $N_2 = 12$.

The [fundamental period](@entry_id:267619) of the sum is $N_0 = \text{lcm}(10, 12) = 60$.

This rule has an important corollary: **the sum of a periodic signal and an aperiodic signal is always aperiodic**. If it were periodic, we could isolate the aperiodic component by subtracting the periodic component from the sum. The result would be a [periodic signal](@entry_id:261016) (since the difference of two [periodic signals](@entry_id:266688) is periodic), leading to a contradiction [@problem_id:1741177].

### Generalizing the Concept: Polynomial-Phase Signals

The definition of [periodicity](@entry_id:152486), $x[n+N] = x[n]$, is universal and can be applied to signals more complex than simple exponentials. A fascinating class of signals are **polynomial-phase signals**, of the form $x[n] = e^{jP(n)}$, where $P(n)$ is a polynomial in $n$. The simplest non-trivial example is a **quadratic-phase signal**, where the phase is a quadratic function, e.g., $\theta[n] = \alpha n^2$.

Let's investigate the [periodicity](@entry_id:152486) of such a signal, $x[n] = e^{j\alpha n^2}$. The condition $x[n+N] = x[n]$ implies:
$$ e^{j\alpha (n+N)^2} = e^{j\alpha n^2} \implies e^{j\alpha((n+N)^2 - n^2)} = 1 $$
This requires the phase difference to be an integer multiple of $2\pi$ for *all* integers $n$:
$$ \alpha((n+N)^2 - n^2) = \alpha(2nN + N^2) = 2\pi m(n) $$
where $m(n)$ must be an integer for every integer $n$. This is a much stricter requirement than for linear-phase signals. The expression $\alpha(2nN + N^2)$ is a linear function of $n$. For this to be a multiple of $2\pi$ for all $n$, both the "slope" term (proportional to $n$) and the "intercept" term must satisfy the condition independently. This leads to a system of two conditions:
1.  $\alpha(2N) = 2\pi k_1$ for some integer $k_1$.
2.  $\alpha(N^2) = 2\pi k_2$ for some integer $k_2$.

Consider a complex signal formed by the superposition of a linear-phase and a quadratic-phase component, such as $s[n] = \exp(j \frac{3\pi}{14} n) + \exp(j \frac{3\pi}{40} n^2)$ [@problem_id:1741151]. To find its [fundamental period](@entry_id:267619), we must find the fundamental periods of each component and then their LCM.
-   The first term, $s_1[n]$, is a standard [complex exponential](@entry_id:265100). Its frequency is $\omega_0 = \frac{3\pi}{14}$, so $\frac{\omega_0}{2\pi} = \frac{3}{28}$. Its [fundamental period](@entry_id:267619) is $N_1 = 28$.
-   For the second term, $s_2[n]$, with $\alpha = \frac{3\pi}{40}$, we apply the two conditions. Smallest positive integer $N_2$ must satisfy both:
    1. $\frac{3\pi}{40}(2N_2) = \frac{3\pi N_2}{20} = 2\pi k_1 \implies 3N_2$ is a multiple of 40.
    2. $\frac{3\pi}{40}(N_2^2) = 2\pi k_2 \implies 3N_2^2$ is a multiple of 80.
    From condition 1, since 3 and 40 are coprime, $N_2$ must be a multiple of 40. The smallest positive value is $N_2=40$. Let's check this in condition 2: $3(40^2) = 3(1600) = 4800$. Since $4800 = 80 \times 60$, condition 2 is also satisfied. Thus, the [fundamental period](@entry_id:267619) of the quadratic-phase term is $N_2 = 40$.

The [fundamental period](@entry_id:267619) of the composite signal $s[n]$ is then the [least common multiple](@entry_id:140942) of the individual periods: $N = \text{lcm}(N_1, N_2) = \text{lcm}(28, 40) = 280$. This example beautifully illustrates how the first principles of [periodicity](@entry_id:152486) can be applied to dissect and analyze even seemingly intricate signals.