## Introduction
The statistical nature of photon arrivals in a beam of light holds profound clues about its origin and fundamental properties. While simple interference experiments reveal a light field's wave-like character, they fail to capture the subtler, and often quantum, correlations in its intensity fluctuations. This article addresses this gap by focusing on the temporal statistics of photons, providing the tools to distinguish between classical phenomena, like the bunched emission from a star, and uniquely quantum effects, like the antibunched, orderly emission from a single atom. We will explore how the [second-order coherence function](@entry_id:175172), $g^{(2)}(\tau)$, serves as the definitive metric for this classification.

Through the following chapters, you will gain a comprehensive understanding of this critical area of [quantum optics](@entry_id:140582). The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, defining $g^{(2)}(\tau)$ and deriving the key criteria for bunching, [antibunching](@entry_id:194774), and [coherent light](@entry_id:170661). The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the power of these concepts by exploring their use in fields ranging from quantum communication and [single-molecule spectroscopy](@entry_id:169444) to [stellar interferometry](@entry_id:159528). Finally, **"Hands-On Practices"** will allow you to solidify your knowledge by working through practical problems related to the measurement and interpretation of photon correlations.

## Principles and Mechanisms

The statistical distribution of photons in time is a fundamental property of a light field, revealing profound insights into its generation mechanism. While the [first-order coherence function](@entry_id:181466), $g^{(1)}(\tau)$, characterizes the interference properties of a field, it is the [second-order coherence function](@entry_id:175172), $g^{(2)}(\tau)$, that quantifies the temporal correlations of intensity and provides the primary tool for distinguishing between classical and quantum states of light. This chapter will develop the theoretical framework for understanding [photon statistics](@entry_id:175965), focusing on the phenomena of photon [bunching and [antibunchin](@entry_id:194025)g](@entry_id:194774).

### The Second-Order Coherence Function

At its core, the [second-order coherence function](@entry_id:175172) addresses the question: if we detect a photon at a particular time $t$, what is the conditional probability of detecting another photon at a time $t+\tau$? The function $g^{(2)}(\tau)$ provides a normalized measure of this correlation. For a stationary light source with a mean photon detection rate of $\langle I \rangle$, this relationship is given by:

$P(\text{detection at } t+\tau | \text{detection at } t) = \langle I \rangle g^{(2)}(\tau)$

where the left-hand side is the [conditional probability](@entry_id:151013) per unit time. Thus, $g^{(2)}(\tau)$ directly compares the probability of detecting two photons separated by a time delay $\tau$ to the probability expected for purely random, uncorrelated events. [@problem_id:2247300]

In the quantum theory of photodetection, $g^{(2)}(\tau)$ is defined in terms of the field's [creation and annihilation operators](@entry_id:147121), $\hat{a}^\dagger$ and $\hat{a}$, which are related to the positive- and negative-frequency parts of [the electric field operator](@entry_id:196320), $\hat{E}^{(+)}$ and $\hat{E}^{(-)}$. For a single-mode field, the definition is:

$g^{(2)}(\tau) = \frac{\langle \hat{a}^\dagger(t) \hat{a}^\dagger(t+\tau) \hat{a}(t+\tau) \hat{a}(t) \rangle}{\langle \hat{a}^\dagger(t) \hat{a}(t) \rangle^2}$

The operators in the numerator are in **[normal order](@entry_id:190735)**, with all [creation operators](@entry_id:191512) to the left of all [annihilation operators](@entry_id:180957). This ordering is crucial because an ideal photodetector annihilates a photon to register a count; the expression thus corresponds directly to the rate of joint detection by two detectors at times $t$ and $t+\tau$.

The value at zero time delay, $g^{(2)}(0)$, is of particular importance as it characterizes the simultaneous emission properties of the source. By substituting $\tau=0$ and recalling that the photon [number operator](@entry_id:153568) is $\hat{n} = \hat{a}^\dagger \hat{a}$, the expression simplifies significantly:

$g^{(2)}(0) = \frac{\langle \hat{a}^\dagger \hat{a}^\dagger \hat{a} \hat{a} \rangle}{\langle \hat{a}^\dagger \hat{a} \rangle^2} = \frac{\langle \hat{n}(\hat{n}-1) \rangle}{\langle \hat{n} \rangle^2}$

This form provides a powerful connection between the abstract field correlation and the statistical distribution of photon number $P(n)$. The numerator, $\langle n(n-1) \rangle$, is the second [factorial](@entry_id:266637) moment of the photon number distribution. It represents the average rate of detecting photon *pairs* within a given time window. [@problem_id:2247308]

It is instructive to also consider the classical analogue of this function. In classical electromagnetic theory, light is a wave with a fluctuating but non-negative instantaneous intensity $I(t)$. The classical [second-order coherence](@entry_id:180621) is defined as:

$g^{(2)}(0) = \frac{\langle I(t)^2 \rangle}{\langle I(t) \rangle^2}$

This quantity measures the normalized variance of the intensity fluctuations. [@problem_id:2247289] The connection between the quantum and classical definitions forms the basis for distinguishing light sources.

### Classical Light: Coherence and Bunching

The classical description of light, powerful as it is, imposes a fundamental limit on the possible values of $g^{(2)}(0)$. For any fluctuating classical quantity $I(t)$, its variance must be non-negative:

$\text{Var}(I) = \langle (I - \langle I \rangle)^2 \rangle = \langle I^2 \rangle - \langle I \rangle^2 \ge 0$

Dividing by $\langle I \rangle^2$ (assuming a non-zero average intensity) immediately yields:

$\frac{\langle I^2 \rangle}{\langle I \rangle^2} \ge 1 \implies g^{(2)}(0) \ge 1$

This crucial result establishes that no classical light field can exhibit a [second-order coherence](@entry_id:180621) at zero delay of less than one. A measurement of $g^{(2)}(0)  1$ is therefore an unambiguous signature of the [quantum nature of light](@entry_id:270825). [@problem_id:2247289]

Based on this, classical light sources are categorized into two main groups:

1.  **Coherent Light ($g^{(2)}(0) = 1$):** This corresponds to the boundary case where the intensity variance is zero. An ideal, [single-mode laser](@entry_id:194328) produces a perfectly stable intensity, $I(t) = I_0$, for which $\langle I^2 \rangle = I_0^2$ and $\langle I \rangle^2 = I_0^2$, yielding $g^{(2)}(0) = 1$. In the quantum picture, this corresponds to a [coherent state](@entry_id:154869), whose photon number statistics follow a **Poisson distribution**, $P(n) = \frac{\lambda^n \exp(-\lambda)}{n!}$, where $\lambda = \langle n \rangle$ is the mean photon number. For a Poisson process, a key property is that $\langle n(n-1) \rangle = \lambda^2$. Substituting this into our quantum definition gives $g^{(2)}(0) = \frac{\lambda^2}{\lambda^2} = 1$, in perfect agreement with the classical result. [@problem_id:2247308] A value of $g^{(2)}(0)=1$ implies that photon arrivals are completely independent and uncorrelated events.

2.  **Thermal or Chaotic Light ($g^{(2)}(0)  1$):** This phenomenon is known as **[photon bunching](@entry_id:161039)**. Thermal sources, such as incandescent lamps, [gas discharge](@entry_id:198337) tubes, or starlight, consist of a vast number of independent atomic emitters. The superposition of their randomly phased emissions leads to large, rapid fluctuations in the total intensity. For a single-mode thermal field, the instantaneous intensity follows an exponential probability distribution. A standard calculation shows that for such a distribution, $\langle I^2 \rangle = 2 \langle I \rangle^2$. [@problem_id:2247295] This leads to the hallmark result for [thermal light](@entry_id:165211):

$g^{(2)}(0) = 2$

The physical interpretation of this value is profound. Recalling our conditional probability relationship, $g^{(2)}(0) = 2$ means that the immediate [conditional probability](@entry_id:151013) of detecting a second photon after a first has been detected is *twice* the average, unconditional probability. [@problem_id:2247300] Photons from a thermal source have a statistical tendency to arrive in "bunches." This can be directly observed in a **Hanbury Brown and Twiss (HBT) experiment**, where light from a source is split by a 50/50 beamsplitter and sent to two detectors. The rate of simultaneous "coincidence" counts is proportional to $g^{(2)}(0)$. If one were to measure a thermal source and an ideal laser with the same average intensity at each detector, the thermal source would produce exactly double the rate of coincidence counts, providing a stark demonstration of [photon bunching](@entry_id:161039). [@problem_id:2247277]

### Nonclassical Light: Photon Antibunching

The most striking departure from classical intuition occurs when $g^{(2)}(0)  1$, a phenomenon known as **[photon antibunching](@entry_id:165214)**. This condition is forbidden by classical wave theory and serves as a definitive marker for a "quantum" light source. It signifies that the detection of one photon *reduces* the probability of detecting a second photon immediately after. Consequently, photons in an antibunched stream are more regularly spaced in time than those in a random (coherent) stream. [@problem_id:2247274]

The archetypal antibunched source is an ideal **single-photon emitter**, such as a single atom, ion, or quantum dot. Such a system can only be in its excited state or ground state. After it emits a single photon, it transitions to the ground state and is incapable of emitting another until it has been re-excited. This period of inactivity is often called the "dead time." It is therefore physically impossible for an ideal single-emitter to emit two photons at the exact same time. This implies that the probability of finding two or more photons ($n \ge 2$) in an emission event is zero. In this case, the second [factorial](@entry_id:266637) moment $\langle n(n-1) \rangle = \sum_n n(n-1)P(n)$ is exactly zero, which leads to the ideal value for a [single-photon source](@entry_id:143467):

$g^{(2)}(0) = 0$

In practice, experimental measurements of $g^{(2)}(0)$ for single-photon sources rarely yield exactly zero. A common source of imperfection is contamination from background light, such as scattered laser light used for excitation. If a true [single-photon source](@entry_id:143467) of intensity $I_m$ (with $g^{(2)}_m(0)=0$) is mixed incoherently with a coherent background of intensity $I_b$ (with $g^{(2)}_b(0)=1$), the measured [second-order coherence](@entry_id:180621) of the total field is a weighted average. The total average intensity is $\langle I \rangle = I_m + I_b$, and the normally-ordered second moment is $\langle : \hat{I}^2 : \rangle = \langle : (\hat{I}_m + \hat{I}_b)^2 : \rangle = g^{(2)}_m(0)I_m^2 + g^{(2)}_b(0)I_b^2 + 2I_m I_b$. Substituting the known values, we find:

$g^{(2)}(0) = \frac{0 \cdot I_m^2 + 1 \cdot I_b^2 + 2 I_m I_b}{(I_m + I_b)^2} = \frac{I_b^2 + 2I_m I_b}{(I_m + I_b)^2} = 1 - \left(\frac{I_m}{I_m + I_b}\right)^2$

This important result [@problem_id:2247287] shows that as the signal-to-background ratio ($I_m/I_b$) increases, the measured $g^{(2)}(0)$ approaches 0. Conversely, even a small amount of background contamination will lift the measured value above zero. For this reason, a measurement of $g^{(2)}(0)  0.5$ is often considered a rigorous benchmark for confirming single-photon emission.

### Dynamics and Temporal Correlations: $g^{(2)}(\tau)$

While $g^{(2)}(0)$ classifies the source, the full function $g^{(2)}(\tau)$ describes the dynamics of the intensity correlations. For any stationary source with a finite memory (or correlation time), two detection events separated by a very long delay $\tau$ should be statistically independent. When the events at $t$ and $t+\tau$ are uncorrelated, the [joint probability](@entry_id:266356) becomes the product of the individual probabilities, which means $\langle I(t)I(t+\tau) \rangle \to \langle I(t) \rangle \langle I(t+\tau) \rangle = \langle I \rangle^2$. This leads to a universal [asymptotic behavior](@entry_id:160836):

$\lim_{\tau \to \infty} g^{(2)}(\tau) = 1$

This means that regardless of whether a source is bunched or antibunched at short time scales, its correlations will always decay to the uncorrelated Poissonian value of 1 for sufficiently long delays. The time scale over which this decay occurs is the **coherence time** of the intensity fluctuations, $T_c$. For instance, a pseudo-thermal source created by passing a laser through a rotating ground-glass disk might have intensity fluctuation correlations that decay exponentially. If the [autocorrelation](@entry_id:138991) of these fluctuations is $\langle \delta I(t) \delta I(t+\tau) \rangle = \langle I \rangle^2 \exp(-|\tau|/T_c)$, then the [second-order coherence function](@entry_id:175172) becomes:

$g^{(2)}(\tau) = 1 + \frac{\langle \delta I(t) \delta I(t+\tau) \rangle}{\langle I \rangle^2} = 1 + \exp(-|\tau|/T_c)$

This function correctly starts at $g^{(2)}(0)=2$ and decays to 1 with a [characteristic time](@entry_id:173472) $T_c$. [@problem_id:2247283] For an antibunched source, $g^{(2)}(\tau)$ starts at a value below 1, rises as the system recovers from its "[dead time](@entry_id:273487)" (often overshooting 1 in a phenomenon known as conditional bunching), and finally settles to 1 for large $\tau$. The characteristic "dip" at $\tau=0$ is the key experimental signature of [photon antibunching](@entry_id:165214).

### Characterizing Mixed and Composite Light Fields

Many practical light sources do not fall neatly into one of the three ideal categories but can be modeled as a mixture of them. Calculating the resulting $g^{(2)}(0)$ is essential for characterizing such systems. Consider a source that is an incoherent superposition of [thermal light](@entry_id:165211) and [coherent light](@entry_id:170661), where the thermal component contributes a fraction $\eta$ to the total average intensity, $\langle I_{th} \rangle = \eta \langle I \rangle$, and the coherent component contributes the rest, $I_{las} = (1-\eta)\langle I \rangle$. The total intensity is $I(t) = I_{th}(t) + I_{las}$. The second moment of the total intensity is $\langle I^2 \rangle = \langle (I_{th} + I_{las})^2 \rangle = \langle I_{th}^2 \rangle + 2 I_{las} \langle I_{th} \rangle + I_{las}^2$. Using $\langle I_{th}^2 \rangle = 2 \langle I_{th} \rangle^2$, we can express the total [second-order coherence](@entry_id:180621) as:

$g^{(2)}(0) = \frac{\langle I^2 \rangle}{\langle I \rangle^2} = \frac{2 \langle I_{th} \rangle^2 + 2 I_{las} \langle I_{th} \rangle + I_{las}^2}{(\langle I_{th} \rangle + I_{las})^2}$

Substituting the fractional intensities gives a remarkably simple result:

$g^{(2)}(0) = 2\eta^2 + 2(1-\eta)\eta + (1-\eta)^2 = 1 + \eta^2$

This formula shows that the [second-order coherence](@entry_id:180621) of the mixed field varies smoothly from $g^{(2)}(0)=1$ (for $\eta=0$, pure coherent) to $g^{(2)}(0)=2$ (for $\eta=1$, pure thermal). [@problem_id:2247295] A similar analysis can be performed for other types of mixtures, such as a source that rapidly switches in time between emitting coherent and [thermal light](@entry_id:165211) [@problem_id:2247257], confirming that the value of $g^{(2)}(0)$ is a sensitive probe of the statistical composition of a light field.