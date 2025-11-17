## Introduction
The root locus technique is a cornerstone of classical control theory, offering a powerful graphical perspective on how a system's stability and performance evolve as a parameter, typically a controller gain $K$, is varied. While the angle condition masterfully sketches the possible paths of the closed-loop poles, it leaves a critical design question unanswered: once we identify a desirable [pole location](@entry_id:271565) on this path, what specific value of the gain $K$ will place it there?

This is the knowledge gap that the **magnitude condition** fills. It transforms the root locus from a qualitative map into a precise quantitative design tool. By satisfying the condition $|L(s)|=1$, we can pinpoint the exact gain needed to achieve target performance metrics like [damping ratio](@entry_id:262264) and settling time. This article provides a comprehensive exploration of the magnitude condition, demonstrating its essential role in the design and analysis of [feedback control systems](@entry_id:274717).

Across the following chapters, you will gain a thorough understanding of this fundamental concept.
- **Principles and Mechanisms** will delve into the mathematical foundation of the magnitude condition, derived from the system's characteristic equation. It will present both the intuitive geometric method and robust algebraic techniques for calculating gain.
- **Applications and Interdisciplinary Connections** will showcase the magnitude condition's practical utility in diverse scenarios, from tuning simple controllers and designing advanced compensators to analyzing physical systems and addressing hardware constraints.
- **Hands-On Practices** will offer a series of guided problems to apply these principles, reinforcing your ability to solve real-world control engineering challenges.

By mastering the magnitude condition, you will be equipped to move beyond theoretical analysis and perform quantitative, specification-driven [control system design](@entry_id:262002).

## Principles and Mechanisms

The [root locus](@entry_id:272958) technique provides a powerful graphical method for analyzing how the closed-loop [poles of a system](@entry_id:261618) migrate in the [s-plane](@entry_id:271584) as a system parameter, typically a controller gain $K$, is varied. While the angle condition determines the path, or locus, of these poles, the **magnitude condition** provides the quantitative tool to determine the specific value of the parameter $K$ that corresponds to any given point on that locus. This chapter delves into the principles and mechanisms of the magnitude condition, demonstrating its application in [controller design](@entry_id:274982) and [system analysis](@entry_id:263805).

### The Characteristic Equation and its Conditions

The foundation of [root locus analysis](@entry_id:261770) lies in the closed-loop [characteristic equation](@entry_id:149057). For a standard unity [negative feedback](@entry_id:138619) system with an [open-loop transfer function](@entry_id:276280) $L(s)$, the closed-[loop transfer function](@entry_id:274447) $T(s)$ is given by $T(s) = \frac{L(s)}{1+L(s)}$. The closed-loop poles are the roots of the denominator, which are the values of $s$ that satisfy the [characteristic equation](@entry_id:149057):

$$1 + L(s) = 0$$

This can be rewritten as:

$$L(s) = -1$$

For any specific point $s_p$ in the complex plane to be a closed-loop pole, it must satisfy this equation. Since this is an equation of complex numbers, it can be decomposed into two independent conditions by considering its magnitude and [phase angle](@entry_id:274491) separately:

1.  **The Angle Condition**: The phase angle of $L(s_p)$ must be equal to the [phase angle](@entry_id:274491) of $-1$.
    $$\angle L(s_p) = \angle(-1) = (2n+1)\pi \text{ radians, for any integer } n$$
    This condition determines the set of all possible locations for closed-loop poles, which form the branches of the [root locus plot](@entry_id:264447).

2.  **The Magnitude Condition**: The magnitude of $L(s_p)$ must be equal to the magnitude of $-1$.
    $$|L(s_p)| = |-1| = 1$$
    This condition allows us to calculate the specific value of the gain $K$ required to place a closed-loop pole at a desired location $s_p$ that is known to lie on the root locus.

This chapter focuses on the application of the magnitude condition as a critical tool in [control system design](@entry_id:262002).

### Using the Magnitude Condition for Gain Calculation

In the most common scenario, the [open-loop transfer function](@entry_id:276280) $L(s)$ is composed of a variable [proportional gain](@entry_id:272008) $K$ and a plant transfer function $G(s)$, such that $L(s) = K G(s)$. Substituting this into the magnitude condition, we have:

$$|K G(s_p)| = 1$$

Assuming the gain $K$ is a positive real number ($K > 0$), we can write $|K| = K$. The equation then becomes $K|G(s_p)|=1$, which can be rearranged to solve for $K$:

$$K = \frac{1}{|G(s_p)|}$$

This simple but powerful formula is the cornerstone of gain calculation using the [root locus method](@entry_id:273543). It states that the gain required to place a pole at a location $s_p$ is the reciprocal of the magnitude of the open-loop plant's transfer function evaluated at that point.

### Method 1: The Geometric Interpretation

The magnitude condition has an elegant and intuitive geometric interpretation. Let the plant transfer function $G(s)$ be expressed in terms of its $m$ zeros ($z_i$) and $n$ poles ($p_j$):

$$G(s) = \frac{\prod_{i=1}^{m} (s - z_i)}{\prod_{j=1}^{n} (s - p_j)}$$

The magnitude of $G(s)$ evaluated at the desired [pole location](@entry_id:271565) $s_p$ is:

$$|G(s_p)| = \frac{|\prod_{i=1}^{m} (s_p - z_i)|}{|\prod_{j=1}^{n} (s_p - p_j)|} = \frac{\prod_{i=1}^{m} |s_p - z_i|}{\prod_{j=1}^{n} |s_p - p_j|}$$

The term $|s_p - z_i|$ represents the magnitude of the vector drawn from the zero $z_i$ to the point $s_p$, which is simply the Euclidean distance between these two points in the s-plane. Similarly, $|s_p - p_j|$ is the distance from the open-loop pole $p_j$ to $s_p$. Substituting this back into our formula for $K$:

$$K = \frac{1}{|G(s_p)|} = \frac{\prod_{j=1}^{n} |s_p - p_j|}{\prod_{i=1}^{m} |s_p - z_i|} = \frac{\text{Product of distances from open-loop poles to } s_p}{\text{Product of distances from open-loop zeros to } s_p}$$

This provides a graphical procedure for calculating the gain. Once a desired [pole location](@entry_id:271565) $s_p$ is identified on the root locus, one can measure the distances from all [open-loop poles and zeros](@entry_id:276317) to this point and use the formula above to find the corresponding gain $K$.

**Example:** Consider a magnetic levitation system where a lead compensator is used, resulting in an [open-loop transfer function](@entry_id:276280) $G(s) = \frac{K(s+8)}{s(s+4)}$. An engineer wishes to find the gain $K$ that places a dominant closed-loop pole at $s_p = -4 + j4$. The [open-loop poles](@entry_id:272301) are at $p_1 = 0$ and $p_2 = -4$, and the open-loop zero is at $z_1 = -8$.

Applying the geometric formula for $K$ [@problem_id:1618528]:

$$K = \frac{|s_p - p_1| |s_p - p_2|}{|s_p - z_1|} = \frac{|(-4 + j4) - 0| |(-4 + j4) - (-4)|}{|(-4 + j4) - (-8)|}$$

We calculate the magnitude of each vector:
-   Vector from pole at $0$: $|-4 + j4| = \sqrt{(-4)^2 + 4^2} = \sqrt{32}$
-   Vector from pole at $-4$: $|0 + j4| = \sqrt{0^2 + 4^2} = 4$
-   Vector from zero at $-8$: $|4 + j4| = \sqrt{4^2 + 4^2} = \sqrt{32}$

Substituting these values into the equation for $K$:

$$K = \frac{(\sqrt{32})(4)}{\sqrt{32}} = 4$$

Thus, a gain of $K=4$ is required to place a closed-loop pole at $s = -4 + j4$.

### Method 2: The Algebraic Approach

While the geometric method provides excellent intuition, it is often more direct to solve for $K$ algebraically, especially when the [pole location](@entry_id:271565) is specified numerically.

#### Direct Substitution

The most straightforward algebraic method is to return to the [characteristic equation](@entry_id:149057) $1 + L(s) = 0$. For $L(s)=KG(s)$, this can be written as $D(s) + K N(s) = 0$, where $G(s) = N(s)/D(s)$. Since the desired pole $s_p$ must be a root of this polynomial, we can substitute $s=s_p$ and solve the resulting linear equation for $K$.

**Example 1:** For a magnetic levitation model with [loop transfer function](@entry_id:274447) $L(s) = K \frac{s+3}{s^2}$, let's find the gain $K$ required to place a pole at $s = -5$ [@problem_id:1618556]. The [characteristic equation](@entry_id:149057) is:

$$1 + K \frac{s+3}{s^2} = 0 \implies s^2 + K(s+3) = 0$$

Substituting the desired [pole location](@entry_id:271565) $s = -5$:

$$(-5)^2 + K(-5+3) = 0$$
$$25 - 2K = 0 \implies K = \frac{25}{2}$$

This method is efficient and applies universally, even to systems with unstable [open-loop poles](@entry_id:272301). For instance, to stabilize a system with $L(s) = \frac{K(s+3)}{s(s-1)}$ and place a pole at $s = -3.5$, we follow the same procedure [@problem_id:1618559]. The characteristic equation is $s(s-1) + K(s+3) = 0$. Substituting $s = -3.5$ gives $(-3.5)(-4.5) + K(-0.5) = 0$, which yields $15.75 - 0.5K = 0$, and thus $K=31.5$. Note that $31.5$ can be written as $\frac{63}{2}$.

#### Coefficient Matching

An alternative algebraic technique is particularly useful for low-order systems when a pair of [complex conjugate poles](@entry_id:269243) is desired. If the target poles are $s_p = \sigma \pm j\omega_d$, they must be roots of a quadratic factor of the form $(s - s_p)(s - \bar{s}_p) = s^2 - 2\sigma s + (\sigma^2 + \omega_d^2)$. By equating the coefficients of this target polynomial with the actual [characteristic polynomial](@entry_id:150909) of the system (which will contain $K$), we can solve for the required gain.

**Example:** A robotic arm model has the characteristic equation $s^2 + 2s + 2 + K(s+2) = 0$, which simplifies to $s^2 + (2+K)s + (2+2K) = 0$. The goal is to place a pole at $s_p = -2 + j\sqrt{2}$ [@problem_id:1618518]. The conjugate pole must be at $\bar{s}_p = -2 - j\sqrt{2}$. The target quadratic polynomial is:

$$s^2 - (s_p + \bar{s}_p)s + s_p\bar{s}_p = s^2 - (-4)s + ((-2)^2 + (\sqrt{2})^2) = s^2 + 4s + 6$$

By comparing the coefficients of this target polynomial with the system's characteristic polynomial, $s^2 + (2+K)s + (2+2K) = 0$, we create a system of equations:

-   From the $s^1$ term: $2+K = 4 \implies K=2$
-   From the $s^0$ term: $2+2K = 6 \implies 2K=4 \implies K=2$

Both equations yield $K=2$, confirming that this gain achieves the desired [pole placement](@entry_id:155523). A variant of this method uses Vieta's formulas, which relate polynomial coefficients to the sums and products of their roots. For a second-order system $s^2+as+b=0$ with roots $r_1, r_2$, we know $r_1+r_2 = -a$. This can be used to quickly solve for $K$ if the real part of the desired poles is specified [@problem_id:1618542].

### Analysis of Special Cases

The magnitude condition is a robust tool that can be adapted to more complex scenarios.

#### Marginal Stability and Imaginary Axis Crossing

A critical aspect of [system analysis](@entry_id:263805) is determining the gain $K$ at which the system becomes marginally stable. This occurs when the root locus crosses the [imaginary axis](@entry_id:262618), meaning the closed-loop poles are of the form $s = \pm j\omega$. We can find this [critical gain](@entry_id:269026), often denoted $K_{mar}$, and the corresponding [oscillation frequency](@entry_id:269468) $\omega$ by substituting $s=j\omega$ into the characteristic equation and solving.

**Example:** A satellite control system has the [characteristic equation](@entry_id:149057) $s^3 + 4s^2 + 8s + K = 0$ [@problem_id:1618514]. To find the gain for [marginal stability](@entry_id:147657), we set $s = j\omega$:

$$(j\omega)^3 + 4(j\omega)^2 + 8(j\omega) + K = 0$$
$$-j\omega^3 - 4\omega^2 + j8\omega + K = 0$$

For this complex equation to be zero, both its real and imaginary parts must be zero:

-   Real Part: $K - 4\omega^2 = 0$
-   Imaginary Part: $8\omega - \omega^3 = 0 \implies \omega(8 - \omega^2) = 0$

For non-trivial oscillations, $\omega \neq 0$, so the imaginary part equation gives $\omega^2 = 8$. Substituting this into the real part equation gives the marginal gain:

$$K = K_{mar} = 4\omega^2 = 4(8) = 32$$

Thus, the system will exhibit [sustained oscillations](@entry_id:202570) at a frequency of $\omega = \sqrt{8}$ rad/s when the gain is set to $K=32$.

#### Systems Incorporating Time Delays

Process control systems often include time delays (or transport lags), represented by the term $e^{-\tau s}$ in the transfer function. The magnitude condition can be readily applied to such systems. The [characteristic equation](@entry_id:149057) becomes $1 + K G(s) e^{-\tau s} = 0$.

To find the gain $K$ for a pole at $s_p$, we can solve for $K$ algebraically:

$$K e^{-\tau s_p} = -\frac{1}{G(s_p)} \implies K = -\frac{1}{G(s_p) e^{-\tau s_p}} = -\frac{e^{\tau s_p}}{G(s_p)}$$

**Example:** Consider a process with [open-loop transfer function](@entry_id:276280) $G(s) = \frac{K e^{-0.2 s}}{s(s+5)}$. We want to find the gain $K$ that places a pole at $s = -2$ [@problem_id:1618554]. The characteristic equation is $1 + \frac{K e^{-0.2 s}}{s(s+5)} = 0$, or $s(s+5) + K e^{-0.2 s} = 0$. Substituting $s=-2$:

$$(-2)(-2+5) + K e^{-0.2(-2)} = 0$$
$$-6 + K e^{0.4} = 0 \implies K = 6 e^{-0.4}$$

Using the value $e^{-0.4} \approx 0.67032$, we find the required gain:

$$K \approx 6 \times 0.67032 \approx 4.02$$

### Generalization to Arbitrary System Parameters

The power of the [root locus method](@entry_id:273543) extends beyond simple [proportional gain](@entry_id:272008) $K$. Any system whose [characteristic equation](@entry_id:149057) can be expressed in terms of a single variable parameter $\alpha$ can be analyzed using this framework. The first step is to algebraically rearrange the characteristic equation into the canonical form $1 + \alpha F(s) = 0$. Here, $\alpha$ plays the role of the "gain," and $F(s)$ serves as the effective "plant."

**Example:** A system's behavior is described by the characteristic equation $s^2 + (4+\alpha)s + 8 = 0$. We want to find the value of $\alpha$ that places a pole at $s = -3$ [@problem_id:1618513].

The simplest method is direct substitution:
$$(-3)^2 + (4+\alpha)(-3) + 8 = 0$$
$$9 - 12 - 3\alpha + 8 = 0$$
$$5 - 3\alpha = 0 \implies \alpha = \frac{5}{3}$$

To view this through the lens of the [root locus method](@entry_id:273543), we rearrange the equation to isolate $\alpha$:
$$s^2 + 4s + 8 + \alpha s = 0$$
Dividing by the terms not multiplied by $\alpha$, we get the standard form:
$$1 + \frac{\alpha s}{s^2 + 4s + 8} = 0$$
Here, the parameter is $\alpha$ and the effective transfer function is $F(s) = \frac{s}{s^2 + 4s + 8}$. The magnitude condition is $|\alpha F(s_p)| = 1$, or $|\alpha| = \frac{1}{|F(s_p)|}$. For $s_p = -3$:

$$|\alpha| = \frac{1}{|F(-3)|} = \frac{|(-3)^2 + 4(-3) + 8|}{|-3|} = \frac{|9 - 12 + 8|}{3} = \frac{5}{3}$$

Assuming $\alpha$ must be positive to place the pole at this location (which would be confirmed by the angle condition), we find $\alpha = 5/3$, matching the simpler algebraic result. This demonstrates the generality of the magnitude condition principle.

### A Concluding Insight: Reciprocal Transfer Functions

The fundamental nature of the magnitude condition is rooted in the algebraic structure of the characteristic equation. A final example highlights this relationship. Suppose a system with plant $G_A(s)$ requires a gain $K_A = 75$ to place a pole at a location $s_0$ [@problem_id:1618517]. From the [characteristic equation](@entry_id:149057), we know:

$$1 + K_A G_A(s_0) = 0 \implies G_A(s_0) = -\frac{1}{K_A}$$

Now, consider a second system with a plant transfer function that is the reciprocal of the first, $G_B(s) = 1/G_A(s)$. We wish to find the gain $K_B$ that places a pole at the same location $s_0$. The characteristic equation for the second system is:

$$1 + K_B G_B(s_0) = 0 \implies 1 + K_B \frac{1}{G_A(s_0)} = 0 \implies G_A(s_0) = -K_B$$

By equating the two expressions for $G_A(s_0)$, we find a simple and elegant relationship between the two gains:

$$-\frac{1}{K_A} = -K_B \implies K_B = \frac{1}{K_A}$$

For $K_A=75$, the required gain for the second system is $K_B = 1/75 \approx 0.01333$. This result underscores that the magnitude condition is not merely a graphical tool but a direct consequence of the algebraic requirement that any point on the [root locus](@entry_id:272958) must satisfy the system's characteristic equation. Mastering its application is therefore essential for the quantitative design and analysis of [feedback control systems](@entry_id:274717).