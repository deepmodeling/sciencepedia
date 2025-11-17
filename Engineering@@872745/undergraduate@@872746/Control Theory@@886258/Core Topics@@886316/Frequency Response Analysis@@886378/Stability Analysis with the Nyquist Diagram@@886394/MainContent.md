## Introduction
The stability of feedback systems is a central concern in control engineering. While methods like the Routh-Hurwitz criterion provide algebraic answers, they offer limited insight into design trade-offs or robustness against [model uncertainty](@entry_id:265539). The Nyquist stability criterion, a powerful graphical method, addresses this gap by analyzing the [frequency response](@entry_id:183149) of a system's [open-loop transfer function](@entry_id:276280). It provides not only a definitive yes-or-no answer to stability but also a deep, intuitive understanding of how close a system is to instability and how to improve its performance.

This article provides a comprehensive exploration of this essential tool. The first chapter, "Principles and Mechanisms," will unpack the theory behind the Nyquist plot, from its physical meaning based on Cauchy's Argument Principle to the formal stability criterion and its application to both stable and unstable plants. Following this, "Applications and Interdisciplinary Connections" will demonstrate the criterion's practical utility in calculating [stability margins](@entry_id:265259), designing controllers for systems with time delays, and its relevance in fields like [digital control](@entry_id:275588) and [robust control](@entry_id:260994). Finally, "Hands-On Practices" will allow you to solidify your understanding by solving targeted problems that bridge theory and application. By the end, you will be equipped to use the Nyquist diagram to analyze and design robust [control systems](@entry_id:155291).

## Principles and Mechanisms

The Nyquist stability criterion is a powerful graphical method used in control theory to determine the stability of a closed-loop system by examining the [frequency response](@entry_id:183149) of its [open-loop transfer function](@entry_id:276280). This chapter delves into the fundamental principles that underpin the Nyquist analysis, the mechanisms for constructing and interpreting the Nyquist plot, and its application to a wide range of systems.

### The Physical Meaning of the Nyquist Plot

Before delving into the mathematics of stability, it is crucial to understand what a Nyquist plot physically represents. A linear time-invariant (LTI) system, described by an [open-loop transfer function](@entry_id:276280) $G(s)$, processes [sinusoidal inputs](@entry_id:269486) in a characteristic way. When a sinusoidal signal, such as $v_{in}(t) = A \cos(\omega t)$, is applied to a stable LTI system, the steady-state output will also be a sinusoid of the same frequency, but with a potentially different amplitude and a phase shift.

The Nyquist plot is the locus of points in the complex plane representing the system's frequency response, $G(j\omega)$, as the [angular frequency](@entry_id:274516) $\omega$ is varied from $0$ to $\infty$. Each point on this plot is a complex number, $G(j\omega_0)$, corresponding to a specific frequency $\omega_0$. This complex number directly quantifies the change in the input [sinusoid](@entry_id:274998).

The magnitude of this complex number, $|G(j\omega_0)|$, is the gain of the system at that frequency; it is the factor by which the input amplitude is multiplied to get the output amplitude. The argument or angle of the complex number, $\arg(G(j\omega_0))$, is the phase shift introduced by the system at that frequency.

For instance, consider an audio preamplifier with transfer function $G(s)$. If a sinusoidal input $v_{in}(t) = 0.5 \cos(2000\pi t)$ is applied, and the Nyquist plot of $G(s)$ at the frequency $\omega_0 = 2000\pi$ rad/s is located at the complex coordinate $(-4.0, -3.0)$, this point represents the complex number $G(j\omega_0) = -4.0 - 3.0j$ [@problem_id:1613301]. The magnitude of this response is $|-4.0 - 3.0j| = \sqrt{(-4.0)^2 + (-3.0)^2} = 5.0$. The phase shift is $\arg(-4.0 - 3.0j) = \arctan(-3.0 / -4.0) - 180^\circ \approx -143^\circ$. Therefore, the steady-state output signal will be $v_{out,ss}(t) = (0.5 \times 5.0) \cos(2000\pi t - 143^\circ) = 2.5 \cos(2000\pi t - 143^\circ)$. Each point on the Nyquist plot thus provides a complete picture of the system's steady-state behavior at a particular frequency.

### Constructing the Full Nyquist Plot

While the plot of $G(j\omega)$ for $\omega \in [0, \infty)$ (often called the polar plot) holds physical meaning, stability analysis requires a complete, closed contour known as the **Nyquist plot**. This distinction is critical because the stability criterion is based on **Cauchy's Argument Principle**, which relates the number of times a function's plot encircles the origin to the number of [zeros and poles](@entry_id:177073) of that function inside a given contour in the input domain.

For a standard unity-feedback system, the closed-[loop transfer function](@entry_id:274447) is $T(s) = \frac{G(s)}{1+G(s)}$. The poles of this closed-loop system, which determine its stability, are the roots of the characteristic equation $1+G(s)=0$. These roots are the **zeros** of the function $F(s) = 1+G(s)$. The Nyquist criterion applies the Argument Principle to $F(s)$. The principle states that the number of counter-clockwise (CCW) encirclements of the origin by the plot of $F(s)$ is equal to the number of zeros of $F(s)$ minus the number of poles of $F(s)$ inside the chosen contour.

Notice that the plot of $F(s)=1+G(s)$ is simply the plot of $G(s)$ shifted one unit to the right. Therefore, the number of times the plot of $1+G(s)$ encircles the origin is identical to the number of times the plot of $G(s)$ encircles the point $(-1+j0)$. This is the fundamental reason why we analyze the Nyquist plot of $G(s)$ and focus on encirclements of the **critical point, -1**.

To apply the criterion, we must select a contour in the $s$-plane, known as the **Nyquist contour ($\Gamma_s$)**, that encloses the entire right-half plane (RHP), as any poles or zeros in this region lead to instability. The standard Nyquist contour consists of three parts [@problem_id:2888084]:

1.  The entire [imaginary axis](@entry_id:262618), from $s=-j\infty$ to $s=+j\infty$.
2.  A semicircle of infinite radius in the RHP, connecting $+j\infty$ back to $-j\infty$.

The full Nyquist plot is the image of this entire contour $\Gamma_s$ under the mapping $s \mapsto G(s)$. For systems with real coefficients, the transfer function has the property that $G(\bar{s}) = \overline{G(s)}$. This leads to a crucial simplification: the plot for negative frequencies ($s=-j\omega$) is the [complex conjugate](@entry_id:174888) of the plot for positive frequencies ($s=j\omega$). This means the Nyquist plot for $\omega \in (-\infty, 0)$ is a mirror image of the polar plot across the real axis.

Furthermore, for any **strictly proper** transfer function (where the degree of the denominator is greater than the degree of the numerator), as $|s| \to \infty$, $|G(s)| \to 0$. This means the entire infinite semicircle of the Nyquist contour maps to a single point: the origin $(0,0)$ in the $G(s)$-plane.

Consequently, for a strictly proper system with real coefficients, the full, closed Nyquist plot can be constructed by:
1.  Plotting $G(j\omega)$ for $\omega \in [0, \infty)$.
2.  Reflecting this curve across the real axis to obtain the plot for $\omega \in (-\infty, 0]$.
3.  The plot is automatically closed at the origin, as $G(j\infty)$ and $G(-j\infty)$ are both at $(0,0)$.

The concept of "encirclement" is only meaningful for such a closed curve. The polar plot alone is an open curve and is insufficient for determining stability.

### The Nyquist Stability Criterion

The Nyquist stability criterion provides a direct link between the encirclements on the Nyquist plot and the stability of the closed-loop system. The criterion is formally stated as:
$$Z = P + N_{ccw}$$
where:
-   $Z$ is the number of zeros of $1+G(s)$ in the [right-half plane](@entry_id:277010). These are the **unstable closed-loop poles**. For a system to be stable, we require $Z=0$.
-   $P$ is the number of poles of the [open-loop transfer function](@entry_id:276280) $G(s)$ in the right-half plane. These are the **unstable [open-loop poles](@entry_id:272301)**. This number is determined by inspecting the denominator of $G(s)$.
-   $N_{ccw}$ is the number of net **counter-clockwise** (CCW) encirclements of the critical point $(-1+j0)$ by the Nyquist plot of $G(s)$. Clockwise (CW) encirclements are counted as negative.

For a closed-loop system to be stable, we must have $Z=0$. Substituting this into the criterion gives the stability condition:
$$N_{ccw} = -P$$

This elegant equation forms the heart of Nyquist analysis. Let's explore its implications in two key scenarios.

#### Case 1: Open-Loop Stable Systems ($P=0$)

Many [control systems](@entry_id:155291) are designed around processes that are inherently stable on their own. In this case, the [open-loop transfer function](@entry_id:276280) $G(s)$ has no poles in the RHP, so $P=0$ [@problem_id:1613296]. The stability condition simplifies dramatically to:
$$N_{ccw} = 0$$
This means for a system that is open-loop stable, the closed-loop system is stable if and only if the Nyquist plot of $G(s)$ **does not encircle** the critical point $(-1, 0)$. This is the most commonly cited version of the criterion and is the basis for the related concepts of [gain and phase margin](@entry_id:166519).

#### Case 2: Open-Loop Unstable Systems ($P>0$)

The true power of the Nyquist criterion becomes evident when dealing with inherently unstable systems, such as magnetic levitation vehicles or inverted pendulums [@problem_id:1613324]. For these systems, $G(s)$ has one or more poles in the RHP, so $P > 0$. Bode plot analysis, which implicitly assumes $P=0$ for its simple stability rules, is insufficient here. The Nyquist criterion, however, handles this situation naturally.

For stability ($Z=0$), we require $N_{ccw} = -P$. This means the Nyquist plot **must encircle** the $-1$ point exactly $P$ times in the **clockwise** direction. The feedback controller must be designed to shape the Nyquist plot in such a way that it performs this precise "stabilizing dance" around the critical point.

As an example, consider a system with the [open-loop transfer function](@entry_id:276280) $G(s) = \frac{K(s+2)}{s(s-1)(s+10)}$ [@problem_id:1613345]. This system has a pole at $s=1$, so it is open-loop unstable with $P=1$. For the closed-loop system to be stable, the Nyquist plot must encircle the $-1$ point once in the clockwise direction ($N_{ccw}=-1$). Analysis shows that the Nyquist plot crosses the negative real axis at a point given by $-\frac{7K}{90}$. To achieve one CW encirclement, this crossing point must be to the left of $-1$.
$$-\frac{7K}{90}  -1 \implies \frac{7K}{90} > 1 \implies K > \frac{90}{7}$$
Thus, only for a gain $K$ greater than $90/7$ will the controller be strong enough to stabilize the inherently unstable plant. This demonstrates how the Nyquist criterion provides a quantitative tool for designing controllers for unstable systems.

### Handling Poles on the Imaginary Axis

The Argument Principle requires the function $G(s)$ to be analytic (i.e., have no poles or other singularities) on the chosen contour $\Gamma_s$. A problem arises if the [open-loop transfer function](@entry_id:276280) has poles directly on the [imaginary axis](@entry_id:262618), such as an integrator pole at $s=0$ or poles for an undamped resonant mode at $s = \pm j\omega_0$ [@problem_id:1613295]. The standard Nyquist contour, which traverses the [imaginary axis](@entry_id:262618), would pass directly through these poles, invalidating the procedure.

To resolve this, the contour $\Gamma_s$ must be modified. We create an infinitesimally small semicircular "detour" or **indentation** into the [right-half plane](@entry_id:277010) to bypass each pole on the [imaginary axis](@entry_id:262618). The Argument Principle remains valid as the poles are now outside the modified contour. However, we must now map these small indentations into the $G(s)$-plane.

Near a simple pole at $s_0$, the transfer function behaves as $G(s) \approx \frac{R}{s-s_0}$, where $R$ is the residue at that pole. A small semicircular path in the $s$-plane, $s-s_0 = \epsilon e^{j\theta}$ with $\epsilon \to 0$, gets mapped to a large arc in the $G(s)$-plane, $G(s) \approx \frac{R}{\epsilon}e^{-j\theta}$.
Specifically, a small CCW detour in the $s$-plane from $\theta = -\pi/2$ to $\theta = +\pi/2$ maps to a large **clockwise** semicircle in the $G(s)$-plane.

For example, a system with poles at $s = \pm j\omega_0$ requires two indentations [@problem_id:1613302]. Each of these small CCW detours in the $s$-plane will map to a large clockwise semicircle at infinity in the $G(s)$-plane. Correctly accounting for the mapping of these indentations is essential for constructing the proper closed Nyquist plot and accurately counting encirclements.

### Interpreting Plot Shape: Asymptotic Analysis

The shape of the Nyquist plot contains rich information about the underlying transfer function. By examining the plot's behavior at very low and very high frequencies, we can deduce key structural properties of the system.

#### Low-Frequency Behavior ($\omega \to 0^+$)

The behavior of the Nyquist plot as $\omega \to 0^+$ is determined by the number of pure integrators in the [open-loop transfer function](@entry_id:276280), i.e., poles at $s=0$. This is known as the **[system type](@entry_id:269068)**.

-   **Type 0 System (no integrators):** $G(s)$ has a finite DC gain, $G(0)$. The plot starts at a finite point on the real axis.
-   **Type 1 System (one integrator, $1/s$):** As $\omega \to 0^+$, $|G(j\omega)| \to \infty$. The plot approaches a vertical or horizontal asymptote. For example, for a system like an antenna tracker with $L(s) = \frac{2(s+10)}{s(s+1)}$, the low-frequency behavior is approximately $L(j\omega) \approx \frac{20}{j\omega} - 18 = -18 - j\frac{20}{\omega}$. This corresponds to a vertical asymptote at $\text{Re}(L) = -18$ [@problem_id:1613300]. The location of this asymptote is critical for determining stability.
-   **Type 2 System (two integrators, $1/s^2$):** As $\omega \to 0^+$, the plot approaches infinity along the negative real axis, since $G(j\omega) \approx K/(j\omega)^2 = -K/\omega^2$.

#### High-Frequency Behavior ($\omega \to \infty$)

The behavior of the plot as it approaches the origin for $\omega \to \infty$ is determined by the **[relative degree](@entry_id:171358)** of the transfer function, $r=n-m$, which is the difference between the degree of the denominator ($n$) and numerator ($m$). For large $s$, $G(s) \approx K s^{-r}$. On the [imaginary axis](@entry_id:262618), $G(j\omega) \approx K(j\omega)^{-r} = K\omega^{-r}e^{-j r\pi/2}$.

The angle at which the plot approaches the origin is therefore $\phi_\infty = -r \frac{\pi}{2}$.
-   $r=1$: Approaches the origin along the negative imaginary axis ($-90^\circ$).
-   $r=2$: Approaches the origin along the negative real axis ($-180^\circ$).
-   $r=3$: Approaches the origin along the positive [imaginary axis](@entry_id:262618) ($-270^\circ$, or $+90^\circ$).
-   $r=4$: Approaches the origin along the positive real axis ($-360^\circ$, or $0^\circ$).

If, for example, an experimental Nyquist plot is observed to approach the origin tangentially to the positive imaginary axis, we can immediately deduce that the system's [relative degree](@entry_id:171358) is most likely $r=3$ [@problem_id:1613318].

### An Advanced Consideration: Internal Stability

A critical caveat in applying the Nyquist criterion relates to **[pole-zero cancellation](@entry_id:261496)**. Suppose a controller $G_c(s)$ is designed with a zero that exactly cancels an [unstable pole](@entry_id:268855) of the plant $G_p(s)$. For example, if the plant has a pole at $s=p$ (with $p>0$) and the controller has a zero at $s=p$. The resulting [open-loop transfer function](@entry_id:276280) $L(s) = G_c(s)G_p(s)$ will no longer show the [unstable pole](@entry_id:268855) [@problem_id:1613292].

If an engineer performs a Nyquist analysis on this mathematically reduced $L(s)$, the number of open-loop [unstable poles](@entry_id:268645) $P$ would be incorrectly counted as zero. The analysis might then conclude the system is stable (e.g., if $N_{ccw}=0$). However, the actual physical system remains unstable. The unstable mode associated with the pole at $s=p$ has become "hidden" from the input-output transfer function, but it has not been eliminated from the system's internal dynamics. This mode can be excited by disturbances or initial conditions, causing internal signals to grow without bound, leading to **internal instability**.

The standard Nyquist criterion only guarantees the stability of the input-output relationship. To ensure the stability of the entire system, one must check for [internal stability](@entry_id:178518). The fundamental rule is that there must be **no cancellation of poles and zeros in the [right-half plane](@entry_id:277010)**. The Nyquist analysis must be performed on the complete, uncancelled [open-loop transfer function](@entry_id:276280) to correctly account for all unstable [open-loop poles](@entry_id:272301) and ensure true [system stability](@entry_id:148296).