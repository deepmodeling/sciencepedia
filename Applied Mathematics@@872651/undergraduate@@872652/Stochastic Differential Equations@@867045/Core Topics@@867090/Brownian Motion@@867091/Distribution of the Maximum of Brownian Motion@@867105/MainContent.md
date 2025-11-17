## Introduction
Brownian motion is a cornerstone of stochastic theory, providing a mathematical model for a wide range of random phenomena, from the jittery motion of particles in a fluid to the unpredictable fluctuations of financial markets. While the position of a Brownian particle at any given time is well-understood as a [normal distribution](@entry_id:137477), a more complex and practical question arises: What is the highest point this erratic path will reach over a given period? Characterizing this path-dependent property—the running maximum—is not straightforward, yet it is essential for solving problems involving thresholds, barriers, and extreme events.

This article systematically demystifies the distribution of the maximum of a standard Brownian motion. It addresses the challenge of analyzing a property of the entire path by introducing a powerful and elegant tool that simplifies the problem immensely. Across three chapters, you will gain a comprehensive understanding of this fundamental topic. The journey begins with the core theory in "Principles and Mechanisms," where we derive the distribution of the maximum using the celebrated [reflection principle](@entry_id:148504). Next, in "Applications and Interdisciplinary Connections," we explore how this theory becomes a practical tool in fields like [quantitative finance](@entry_id:139120), materials science, and [mathematical statistics](@entry_id:170687). Finally, the "Hands-On Practices" section provides targeted problems to reinforce the concepts and build your problem-solving skills in stochastic calculus.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the distribution of the running maximum of a standard Brownian motion. We will build from the foundational properties of Brownian motion to derive its key distributional characteristics, chief among them the celebrated [reflection principle](@entry_id:148504). This will allow us to obtain explicit formulas for the probability distribution, density, and expectation of the maximum, revealing a surprising and elegant connection to the absolute value of the Brownian motion itself.

For the entirety of this chapter, we consider a standard one-dimensional Brownian motion $(B_t)_{t \ge 0}$, which is a [stochastic process](@entry_id:159502) characterized by the following properties:
1.  It starts at the origin: $B_0 = 0$.
2.  Its [sample paths](@entry_id:184367) are continuous with probability one.
3.  It has stationary and [independent increments](@entry_id:262163).
4.  For any $0 \le s \lt t$, the increment $B_t - B_s$ is a Gaussian random variable with mean $0$ and variance $t-s$. Consequently, for any fixed time $t > 0$, the random variable $B_t$ is distributed as a normal distribution with mean $0$ and variance $t$, denoted $B_t \sim \mathcal{N}(0, t)$.

We are interested in the behavior of its **running maximum**, a process defined as:
$$ M_t := \sup_{0 \le s \le t} B_s $$
This random variable, $M_t$, represents the highest level reached by the Brownian path over the time interval $[0, t]$.

A first, simple observation follows directly from the definition. Since the process starts at $B_0=0$ and the supremum is taken over an interval including time $s=0$, we must have $M_t \ge B_0 = 0$. This holds for every continuous path starting at zero. Therefore, the event that $M_t$ is less than some negative value $a \lt 0$ is an impossible event. The probability $\mathbb{P}(M_t \le a)$ for $a \lt 0$ is thus zero [@problem_id:3049932]. The distribution of $M_t$ is supported on the non-negative real numbers $[0, \infty)$.

### The Reflection Principle: A Consequence of Symmetry

The key to unlocking the distribution of $M_t$ lies in a powerful tool known as the **reflection principle**. This principle is a direct consequence of the inherent symmetry of Brownian motion.

Let's first formalize this symmetry. For any fixed $t > 0$, the random variable $B_t \sim \mathcal{N}(0, t)$ has a probability density function that is symmetric about the origin. This implies that the random variables $B_t$ and $-B_t$ are equal in distribution, a property we denote as $B_t \stackrel{d}{=} -B_t$. This is because if $B_t \sim \mathcal{N}(0,t)$, then $-B_t \sim \mathcal{N}(-1 \cdot 0, (-1)^2 t) = \mathcal{N}(0,t)$ [@problem_id:3049908]. Consequently, for any $a \ge 0$, the probability of the process being above $a$ is the same as the probability of it being below $-a$:
$$ \mathbb{P}(B_t \ge a) = \mathbb{P}(-B_t \ge a) = \mathbb{P}(B_t \le -a) $$

The [reflection principle](@entry_id:148504) extends this static symmetry to a dynamic context. Consider a level $a > 0$. The event $\{M_t \ge a\}$ is equivalent to the event that the process hits the level $a$ at or before time $t$. Let us denote the [first hitting time](@entry_id:266306) of level $a$ by $\tau_a = \inf\{s \ge 0: B_s = a\}$. Then $\{M_t \ge a\} = \{\tau_a \le t\}$. We can partition this event based on the final position of the process at time $t$:
$$ \mathbb{P}(M_t \ge a) = \mathbb{P}(\tau_a \le t, B_t \ge a) + \mathbb{P}(\tau_a \le t, B_t  a) $$

Due to path continuity, if $B_t \ge a$ (and $B_0=0$), the path must have crossed level $a$ at some point. Thus, the event $\{B_t \ge a\}$ is a subset of $\{\tau_a \le t\}$, which simplifies the first term:
$$ \mathbb{P}(\tau_a \le t, B_t \ge a) = \mathbb{P}(B_t \ge a) $$

The second term, $\mathbb{P}(\tau_a \le t, B_t  a)$, is where the [reflection principle](@entry_id:148504) applies. By the **strong Markov property** of Brownian motion, the process "restarts" at the [stopping time](@entry_id:270297) $\tau_a$. The process $B'_{u} = B_{\tau_a+u} - B_{\tau_a}$ for $u \ge 0$ is a new standard Brownian motion, independent of the path history up to $\tau_a$. On the event $\{\tau_a \le t\}$, we have $B_t = B_{\tau_a} + (B_t-B_{\tau_a}) = a + B'_{t-\tau_a}$. The condition $B_t  a$ is thus equivalent to $B'_{t-\tau_a}  0$. By the symmetry of the new Brownian motion $B'$, it is equally likely to be positive or negative at time $t-\tau_a$. This means that, conditional on hitting $a$, the path is equally likely to end up above or below $a$. This leads to the remarkable equality:
$$ \mathbb{P}(\tau_a \le t, B_t  a) = \mathbb{P}(\tau_a \le t, B_t > a) $$
Since we can ignore the zero-probability event $\{B_t = a\}$, and noting that $\{\tau_a \le t, B_t > a\}$ is the same as $\{B_t > a\}$, we get:
$$ \mathbb{P}(\tau_a \le t, B_t  a) = \mathbb{P}(B_t > a) = \mathbb{P}(B_t \ge a) $$

Substituting these findings back into our original equation, we arrive at the classic [reflection principle](@entry_id:148504) formula [@problem_id:3049928] [@problem_id:3049908]:
$$ \mathbb{P}(M_t \ge a) = \mathbb{P}(B_t \ge a) + \mathbb{P}(B_t \ge a) = 2\mathbb{P}(B_t \ge a) $$
This elegant result states that for $a \ge 0$, the probability of the maximum reaching level $a$ is exactly twice the probability of the process itself being at or above level $a$ at the end of the interval.

A more general version of the [reflection principle](@entry_id:148504) can be stated for the [joint distribution](@entry_id:204390) of the maximum and the terminal value [@problem_id:3049931]. For any $x \le a$ and $a \ge 0$, the same logic of reflecting the post-hitting-time path yields:
$$ \mathbb{P}(M_t \ge a, B_t \le x) = \mathbb{P}(B_t \ge 2a - x) $$
Here, the event that the path hits $a$ but ends below $x$ is mapped to an event where an unconstrained Brownian motion ends up above the "reflected" level $2a-x$. The simpler formula can be recovered by letting $x \to a$ and noting that $\mathbb{P}(M_t \ge a, B_t \gt a) = \mathbb{P}(B_t \gt a)$.

### Distribution and Properties of the Maximum

With the [reflection principle](@entry_id:148504) in hand, we can now fully characterize the distribution of $M_t$.

#### Cumulative Distribution Function (CDF) and Tail Probability

We know that for $a \ge 0$, $\mathbb{P}(M_t \ge a) = 2\mathbb{P}(B_t \ge a)$. To get an explicit formula, we standardize the random variable $B_t \sim \mathcal{N}(0, t)$. Let $Z = B_t / \sqrt{t}$, where $Z \sim \mathcal{N}(0, 1)$ is a standard normal variable. Let $\Phi(z)$ denote the CDF of $Z$.
$$ \mathbb{P}(B_t \ge a) = \mathbb{P}\left(\frac{B_t}{\sqrt{t}} \ge \frac{a}{\sqrt{t}}\right) = \mathbb{P}\left(Z \ge \frac{a}{\sqrt{t}}\right) = 1 - \Phi\left(\frac{a}{\sqrt{t}}\right) $$
Therefore, the [tail probability](@entry_id:266795) of the maximum is [@problem_id:3049930]:
$$ \mathbb{P}(M_t \ge a) = 2\left(1 - \Phi\left(\frac{a}{\sqrt{t}}\right)\right) $$
From this, we find the CDF of $M_t$ for $a \ge 0$:
$$ F_{M_t}(a) = \mathbb{P}(M_t \le a) = 1 - \mathbb{P}(M_t > a) = 1 - \mathbb{P}(M_t \ge a) = 1 - 2\left(1 - \Phi\left(\frac{a}{\sqrt{t}}\right)\right) = 2\Phi\left(\frac{a}{\sqrt{t}}\right) - 1 $$
This formula provides the complete distribution of the running maximum [@problem_id:3049911]. As a quick check on this result, we can examine its behavior in the limits. As $a \to 0^+$, the argument $a/\sqrt{t} \to 0$, and $\Phi(0) = 1/2$. The probability $\mathbb{P}(M_t \ge a)$ approaches $2(1-1/2) = 1$, which makes sense as the maximum is almost surely non-negative. As $a \to \infty$, the argument $a/\sqrt{t} \to \infty$, and $\Phi(a/\sqrt{t}) \to 1$. The probability $\mathbb{P}(M_t \ge a)$ approaches $2(1-1) = 0$, correctly stating that it is impossible to reach an infinite height in finite time [@problem_id:3049930].

#### Probability Density Function (PDF)

By differentiating the CDF with respect to $a$ (for $a  0$), we obtain the probability density function (PDF) of $M_t$. Let $\varphi(z) = \frac{d}{dz}\Phi(z) = \frac{1}{\sqrt{2\pi}}\exp(-z^2/2)$ be the PDF of the standard normal distribution.
$$ f_{M_t}(a) = \frac{d}{da}\left( 2\Phi\left(\frac{a}{\sqrt{t}}\right) - 1 \right) = 2\varphi\left(\frac{a}{\sqrt{t}}\right) \cdot \frac{1}{\sqrt{t}} $$
Substituting the expression for $\varphi(z)$, we find for $a  0$:
$$ f_{M_t}(a) = \frac{2}{\sqrt{t}} \cdot \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{1}{2}\left(\frac{a}{\sqrt{t}}\right)^2\right) = \frac{2}{\sqrt{2\pi t}} \exp\left(-\frac{a^2}{2t}\right) $$
This density is that of a **folded normal distribution**. It is the distribution of the absolute value of a normal random variable with mean $0$ and variance $t$, multiplied by a factor of 2 on its positive domain [@problem_id:3049911, @problem_id:3049954].

### A Surprising Equivalence: Maximum and Absolute Value

The form of the CDF for $M_t$ is highly suggestive. Let us compare it with the distribution of another simple random variable derived from Brownian motion: the absolute value of its terminal position, $|B_t|$.

For $x \ge 0$, the CDF of $|B_t|$ is:
$$ \mathbb{P}(|B_t| \le x) = \mathbb{P}(-x \le B_t \le x) $$
Standardizing the variable $B_t$ gives:
$$ \mathbb{P}\left(-\frac{x}{\sqrt{t}} \le \frac{B_t}{\sqrt{t}} \le \frac{x}{\sqrt{t}}\right) = \mathbb{P}\left(-\frac{x}{\sqrt{t}} \le Z \le \frac{x}{\sqrt{t}}\right) $$
In terms of the standard normal CDF $\Phi$, this is:
$$ \Phi\left(\frac{x}{\sqrt{t}}\right) - \Phi\left(-\frac{x}{\sqrt{t}}\right) $$
Using the symmetry property $\Phi(-z) = 1 - \Phi(z)$, this becomes:
$$ \Phi\left(\frac{x}{\sqrt{t}}\right) - \left(1 - \Phi\left(\frac{x}{\sqrt{t}}\right)\right) = 2\Phi\left(\frac{x}{\sqrt{t}}\right) - 1 $$
This is exactly the same expression we found for the CDF of $M_t$. Since both random variables are non-negative and their CDFs are identical for all $x \ge 0$, we have established the remarkable identity in distribution [@problem_id:3049954] [@problem_id:3049956]:
$$ M_t \stackrel{d}{=} |B_t| $$
This result is deeply counter-intuitive. It states that the maximum value attained by the process over the *entire path* from $0$ to $t$ has the same probability distribution as the absolute value of the process at the *single endpoint* $t$.

### Moments and Scaling

This identity in law, $M_t \stackrel{d}{=} |B_t|$, provides a powerful shortcut for calculating moments of the maximum. For instance, the expected value of the maximum is:
$$ \mathbb{E}[M_t] = \mathbb{E}[|B_t|] $$
Since $B_t \sim \mathcal{N}(0,t)$, we can calculate this expectation by integrating against the PDF of $B_t$:
$$ \mathbb{E}[|B_t|] = \int_{-\infty}^{\infty} |x| \frac{1}{\sqrt{2\pi t}} \exp\left(-\frac{x^2}{2t}\right) dx = 2 \int_{0}^{\infty} x \frac{1}{\sqrt{2\pi t}} \exp\left(-\frac{x^2}{2t}\right) dx $$
This integral evaluates to $\sqrt{2t/\pi}$. Thus, the expectation of the running maximum is [@problem_id:3049911] [@problem_id:3049954]:
$$ \mathbb{E}[M_t] = \sqrt{\frac{2t}{\pi}} $$
The running maximum also inherits the scaling properties of Brownian motion. Recall that for any constant $c  0$, the process $X_t = B_{ct}/\sqrt{c}$ is also a standard Brownian motion. Applying this to the maximum:
$$ \frac{M_{ct}}{\sqrt{c}} = \frac{1}{\sqrt{c}} \sup_{0 \le s \le ct} B_s = \sup_{0 \le s \le ct} \frac{B_s}{\sqrt{c}} $$
With a change of variables $u = s/c$, this becomes:
$$ \sup_{0 \le u \le t} \frac{B_{cu}}{\sqrt{c}} = \sup_{0 \le u \le t} X_u $$
Since $(X_u)_{u \ge 0}$ is a standard Brownian motion, its running maximum has the same distribution as the maximum of $(B_u)_{u \ge 0}$. Therefore, we have the scaling relation [@problem_id:3049911]:
$$ \frac{M_{ct}}{\sqrt{c}} \stackrel{d}{=} M_t $$

### Advanced Structural Properties

#### The Markov Property

A common question is whether the running maximum process, $(M_t)_{t\ge 0}$, is itself a Markov process. A process is Markov if its future evolution depends only on its present state, not on its past history. For $(M_t)$, this is not the case.

To see why, consider the probability that the maximum increases in a small future time interval, say from $t$ to $t+h$. This means we want to evaluate $\mathbb{P}(M_{t+h}  M_t | \mathcal{F}_t)$, where $\mathcal{F}_t$ is the history of the process up to time $t$. Let's assume we know the state at time $t$ to be $(B_t, M_t) = (b, m)$, where $b \le m$. For the maximum to increase, the underlying process $B$ must exceed the current maximum $m$. The future evolution $B_{t+s} - B_t$ for $s0$ is an independent Brownian motion. So, the probability of an increase depends on the probability that this new Brownian motion, starting from $B_t = b$, will exceed level $m$ within time $h$. This is the probability that $\sup_{0 \le s \le h} (B_{t+s}-b)$ exceeds the "gap" $m-b$.

Using the reflection principle for this new increment, this probability is $2(1-\Phi(\frac{m-b}{\sqrt{h}}))$. Crucially, this probability depends not only on the current maximum $m=M_t$ but also on the current position $b=B_t$ through the gap $m-b$. If $B_t$ is far below $M_t$ (a large gap), it is less likely to create a new maximum soon. If $B_t = M_t$ (zero gap), the process is at its current peak, and the law of the iterated logarithm ensures it will immediately cross this level, making the probability of a new maximum 1 [@problem_id:3049952]. Since the future evolution of $M_t$ depends on more past information than just its current value, **the process $(M_t)_{t \ge 0}$ is not a Markov process**.

However, the two-dimensional process $(B_t, M_t)_{t \ge 0}$ *is* a Markov process. Given the current state $(B_t, M_t)$, the future evolution is fully determined by an independent Brownian increment, making the pair $(B_t, M_t)$ a [sufficient statistic](@entry_id:173645) for its own future [@problem_id:3049952].

#### The Uniqueness of the Reflection Principle

Finally, it is essential to recognize that the [reflection principle](@entry_id:148504), and all the elegant results that flow from it, are not universal truths for all stochastic processes. The argument relies critically on the unique features of Brownian motion: the **strong Markov property** combined with the **independence and symmetry of its increments** [@problem_id:3049916].

For a general [continuous martingale](@entry_id:185466) that is not a Brownian motion (for example, a stochastic integral of the form $X_t = \int_0^t \sigma_s dB_s$ where the volatility $\sigma_s$ depends on the path), the post-hitting-time process is no longer independent of the past, nor is its distribution necessarily symmetric. For instance, if the volatility $\sigma_s$ increases after the process has crossed some level, the process will be more "unstable" and might be pushed further away from the level it just crossed, breaking the symmetric reflection. This demonstrates that the beautiful relationship between the maximum and the endpoint, $M_t \stackrel{d}{=} |B_t|$, is a special and profound consequence of the very specific structure of Brownian motion [@problem_id:3049916].