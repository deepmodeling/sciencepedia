## Introduction
The [root locus method](@entry_id:273543), developed by Walter R. Evans, is a cornerstone of classical control theory, offering a powerful graphical technique for analyzing and designing [feedback systems](@entry_id:268816). It provides profound insight into how a system's stability and dynamic performance change as a key parameter, typically a [controller gain](@entry_id:262009), is varied. Without a systematic approach, predicting the movement of a system's closed-loop poles can be a daunting task requiring repetitive algebraic calculations. The [root locus method](@entry_id:273543) addresses this gap by providing a set of well-defined rules that allow an engineer to sketch the trajectory of these poles by hand, transforming abstract [polynomial roots](@entry_id:150265) into an intuitive visual map.

This article provides a comprehensive guide to this essential technique. The first chapter, "Principles and Mechanisms," will detail the fundamental rules for constructing a [root locus plot](@entry_id:264447), from identifying real-axis segments to calculating asymptotes and [breakaway points](@entry_id:265082). The following chapter, "Applications and Interdisciplinary Connections," will explore how to interpret the finished plot to assess system performance and design controllers, while also highlighting its connections to other engineering domains. Finally, "Hands-On Practices" will offer opportunities to apply these concepts to practical problems. We begin by deriving the fundamental principles and step-by-step rules that govern the construction of the [root locus](@entry_id:272958).

## Principles and Mechanisms

This chapter builds upon the foundational concept of the root locus by systematically detailing the principles and rules that govern its construction. Understanding these rules enables the engineer to sketch the [root locus](@entry_id:272958) of a system by hand, providing invaluable insight into system stability and transient response without requiring computational software. We will derive each rule from the fundamental properties of the closed-loop system and illustrate its application through concrete examples.

### The Fundamental Locus Conditions

A typical negative feedback control system has a closed-[loop transfer function](@entry_id:274447) $T(s)$ given by:
$T(s) = \frac{L(s)}{1 + L(s)}$
where $L(s)$ is the [open-loop transfer function](@entry_id:276280). For the common case of a proportional controller with gain $K > 0$ and a plant $G(s)$, the [open-loop transfer function](@entry_id:276280) is $L(s) = KG(s)$. The stability and dynamic characteristics of the closed-loop system are determined by the locations of the poles of $T(s)$, which are the roots of the **characteristic equation**:
$1 + KG(s) = 0$

The **[root locus](@entry_id:272958)** is the set of all points $s$ in the complex plane that satisfy this characteristic equation as the gain $K$ is varied from $0$ to $\infty$. The equation can be rearranged as:
$G(s) = -\frac{1}{K}$

Since $K$ is a positive real number, the right side of this equation is always a negative real number. This single complex equation can be decomposed into two separate real conditions:

1.  **The Angle Condition**: The phase angle of $G(s)$ must be an odd multiple of $\pi$ (or $180^\circ$).
    $\angle G(s) = (2k + 1)\pi$, for any integer $k$.

2.  **The Magnitude Condition**: The magnitude of $G(s)$ must be equal to $1/K$.
    $|G(s)| = \frac{1}{K}$

The angle condition is the primary criterion for determining the shape of the locus; a point $s$ is on the root locus if and only if it satisfies this condition. The magnitude condition is then used to find the specific value of gain $K$ corresponding to that point on the locus.

For example, to determine if a specific point, say $s_0 = -2 + j2$, is on the root locus for a system with an [open-loop transfer function](@entry_id:276280) $G(s) = \frac{s+3}{s(s+4)}$, we must test the angle condition [@problem_id:1607667]. Let's express $G(s)$ in terms of its poles and zeros: $G(s) = \frac{s - z_1}{(s - p_1)(s - p_2)}$, where $z_1 = -3$, $p_1 = 0$, and $p_2 = -4$. The angle of $G(s_0)$ is:
$\angle G(s_0) = \angle(s_0 - z_1) - \angle(s_0 - p_1) - \angle(s_0 - p_2)$
$\angle G(-2+j2) = \angle(-2+j2 - (-3)) - \angle(-2+j2 - 0) - \angle(-2+j2 - (-4))$
$\angle G(-2+j2) = \angle(1+j2) - \angle(-2+j2) - \angle(2+j2)$
The vectors are $1+j2$ (in quadrant I), $-2+j2$ (in quadrant II), and $2+j2$ (in quadrant I). Their angles are $\arctan(\frac{2}{1})$, $180^\circ - \arctan(\frac{2}{2}) = 135^\circ$, and $\arctan(\frac{2}{2}) = 45^\circ$, respectively. The total angle is:
$\angle G(-2+j2) = \arctan(2) - 135^\circ - 45^\circ = \arctan(2) - 180^\circ$
Since $\arctan(2) \approx 63.4^\circ$, the net angle is approximately $-116.6^\circ$. This is not an odd multiple of $180^\circ$, so the point $s_0 = -2+j2$ is not on the root locus.

### General Rules for Constructing a Root Locus

Based on the fundamental conditions, we can establish a set of rules that form a systematic procedure for sketching the [root locus](@entry_id:272958).

#### Rule 1: Number of Branches

The [characteristic equation](@entry_id:149057) $1+KG(s)=0$ can be written as $D(s) + KN(s) = 0$, where $D(s)$ and $N(s)$ are the denominator and numerator polynomials of $G(s)$, respectively. The degree of this polynomial equation is equal to the degree of $D(s)$, which is the number of [open-loop poles](@entry_id:272301), denoted by $n$. Therefore, there are $n$ closed-loop poles for any given $K$. Each of these $n$ poles traces a path as $K$ varies, and each path is called a **branch** of the [root locus](@entry_id:272958). Thus, the [root locus](@entry_id:272958) has exactly $n$ branches.

#### Rule 2: Starting Points ($K \to 0$) and Ending Points ($K \to \infty$)

The starting and ending points of the locus branches are fundamental to the sketch.

*   **Starting Points ($K=0$):** As the gain $K$ approaches zero, the characteristic equation $D(s) + KN(s) = 0$ simplifies to $D(s) = 0$. The roots of this equation are the [open-loop poles](@entry_id:272301). Therefore, the $n$ branches of the root locus **start** at the $n$ [open-loop poles](@entry_id:272301) of $G(s)$ [@problem_id:1607701]. For instance, for a system with $G(s) = \frac{s+4}{(s+1)(s+8)(s^2+2s+5)}$, the locus branches will begin at the [open-loop poles](@entry_id:272301) $s = -1$, $s = -8$, and $s = -1 \pm 2j$.

*   **Ending Points ($K \to \infty$):** As the gain $K$ becomes very large, we can divide the [characteristic equation](@entry_id:149057) by $K$ to get $\frac{1}{K}D(s) + N(s) = 0$. In the limit as $K \to \infty$, this equation simplifies to $N(s) = 0$. The roots of this equation are the open-loop zeros. If $G(s)$ has $m$ finite open-loop zeros, then $m$ of the locus branches will **terminate** on these $m$ finite zeros. The remaining $n-m$ branches must go elsewhere. As $|s| \to \infty$, these branches approach infinity in the [s-plane](@entry_id:271584).

A clear example is the system with $G_p(s) = \frac{s+3}{(s+1)(s+2)}$, which has two poles ($n=2$) at $s=-1, -2$ and one zero ($m=1$) at $s=-3$. The two locus branches start at $s=-1$ and $s=-2$. As $K \to \infty$, one branch terminates at the zero $s=-3$, and the other ($n-m = 2-1=1$) branch goes to infinity [@problem_id:1607695].

#### Rule 3: Symmetry of the Locus

For any physical system, the coefficients of the polynomials $N(s)$ and $D(s)$ that form the transfer function $G(s)$ are real numbers. This means that if a complex number is a pole or zero, its complex conjugate must also be a pole or zero. This property extends to the [characteristic equation](@entry_id:149057) $D(s) + KN(s) = 0$. Since $K$ is also real, the [characteristic polynomial](@entry_id:150909) has real coefficients. A [fundamental theorem of algebra](@entry_id:152321) states that the roots of a polynomial with real coefficients must either be real or occur in complex conjugate pairs.

Therefore, the [root locus](@entry_id:272958) is always **symmetric with respect to the real axis**. If a point $s_1 = \sigma + j\omega$ is on the [root locus](@entry_id:272958) for a certain gain $K$, then its conjugate $s_2 = \sigma - j\omega$ must also be on the locus for the same value of $K$ [@problem_id:1607689]. Conversely, if a plotted locus is found to be not symmetric about the real axis, it implies that the underlying [open-loop transfer function](@entry_id:276280) does not have real coefficients, meaning its set of poles and zeros is not closed under [complex conjugation](@entry_id:174690) [@problem_id:1607698].

#### Rule 4: Root Locus on the Real Axis

To determine which parts of the real axis belong to the [root locus](@entry_id:272958), we apply the angle condition. For any point $\sigma$ on the real axis, the angle contribution from a pair of [complex conjugate poles](@entry_id:269243) or zeros is zero. A real pole or zero to the left of $\sigma$ contributes an angle of $0^\circ$. A real pole to the right of $\sigma$ contributes an angle of $-180^\circ$, and a real zero to the right contributes $+180^\circ$.

The total angle is $\angle G(\sigma) = (\text{number of zeros to the right}) \times 180^\circ - (\text{number of poles to the right}) \times 180^\circ$. For this angle to be an odd multiple of $180^\circ$, the term $(\text{zeros to the right}) - (\text{poles to the right})$ must be odd. This is equivalent to the total number of real poles and zeros to the right of $\sigma$ being odd.

Thus, a point on the real axis lies on the [root locus](@entry_id:272958) if and only if **the total number of real poles and real zeros to its right is odd**.

Consider a system with [open-loop poles](@entry_id:272301) at $s = 1, -2, -4$ and a zero at $s = -3$. We can determine the real-axis segments of the locus [@problem_id:1607685]:

*   For $\sigma > 1$: 0 poles/zeros to the right (even). Not on locus.
*   For $-2  \sigma  1$: 1 pole at $s=1$ to the right (odd). **On locus**.
*   For $-3  \sigma  -2$: 2 poles at $s=1, -2$ to the right (even). Not on locus.
*   For $-4  \sigma  -3$: 2 poles at $s=1, -2$ and 1 zero at $s=-3$ to the right. Total 3 (odd). **On locus**.
*   For $\sigma  -4$: 3 poles and 1 zero to the right. Total 4 (even). Not on locus.

The segments of the real axis that are part of the root locus are therefore $(-4, -3)$ and $(-2, 1)$.

### Asymptotic Behavior for Large Gain

The $n-m$ branches that tend to infinity as $K \to \infty$ do so along straight-line asymptotes. The properties of these asymptotes are crucial for sketching the overall shape of the locus.

#### Rule 5: Asymptotes of the Locus

*   **Number of Asymptotes**: The number of asymptotes is equal to the number of branches that go to infinity, which is $n-m$.

*   **Angles of Asymptotes**: The angles that these asymptotes make with the positive real axis are given by the formula:
    $\phi_k = \frac{(2k + 1)180^\circ}{n-m}$ for $k = 0, 1, \dots, n-m-1$.
    
    For example, a system with $G(s) = \frac{K}{s(s+1)(s+2)}$ has $n=3$ poles and $m=0$ zeros. It will have $n-m=3$ asymptotes. The angles are [@problem_id:1607712]:
    For $k=0: \phi_0 = \frac{180^\circ}{3} = 60^\circ$
    For $k=1: \phi_1 = \frac{3 \times 180^\circ}{3} = 180^\circ$
    For $k=2: \phi_2 = \frac{5 \times 180^\circ}{3} = 300^\circ$

*   **Centroid of Asymptotes**: All $n-m$ asymptotes intersect at a single point on the real axis, known as the **[centroid](@entry_id:265015)** or center of asymptotes, denoted by $\sigma_a$. This point is calculated as the sum of the pole locations minus the sum of the zero locations, divided by the number of asymptotes:
    $\sigma_a = \frac{\sum_{i=1}^n p_i - \sum_{j=1}^m z_j}{n-m}$
    where $p_i$ are the [open-loop poles](@entry_id:272301) and $z_j$ are the open-loop zeros.
    
    For a system with $G(s) = \frac{s+2}{(s+1)(s+3)(s+5)}$, we have poles at $-1, -3, -5$ and a zero at $-2$. Here $n=3$ and $m=1$. The [centroid](@entry_id:265015) is [@problem_id:1607665]:
    $\sigma_a = \frac{(-1 - 3 - 5) - (-2)}{3 - 1} = \frac{-9 + 2}{2} = -3.5$
    
    The calculation includes all poles, even complex ones. For a system with $G(s) = \frac{1}{s(s+1)(s^2+2s+2)}$, the poles are at $0, -1, -1+j, -1-j$ and there are no zeros ($n=4, m=0$). The sum of poles is $0 + (-1) + (-1+j) + (-1-j) = -3$. The centroid is [@problem_id:1607681]:
    $\sigma_a = \frac{-3 - 0}{4-0} = -0.75$

### Fine Details of the Locus

To add precision to the sketch, we need to determine where the locus leaves the real axis and the specific angles at which it departs from or arrives at complex singularities.

#### Rule 6: Breakaway and Break-in Points

**Breakaway points** are locations on the real axis where two or more branches of the locus, moving towards each other from opposite directions, meet and depart into the complex plane. **Break-in points** are where [complex conjugate](@entry_id:174888) branches meet the real axis and then move along it. These points correspond to multiple roots of the characteristic equation and represent a [local maximum](@entry_id:137813) (for breakaway) or minimum (for break-in) of the gain $K$ along the real axis.

To find these points, we use the characteristic equation $1+KG(s)=0$ to express $K$ as a function of $s$:
$K(s) = -\frac{1}{G(s)}$
The breakaway and [break-in points](@entry_id:273410) are among the real roots of the equation $\frac{dK(s)}{ds} = 0$. After solving this equation, we must verify which solutions are valid by checking if they lie on a segment of the real axis that is part of the [root locus](@entry_id:272958) (Rule 4).

For a system with $G(s) = \frac{1}{s(s+2)(s+5)}$, we have $K(s) = -s(s+2)(s+5) = -s^3 - 7s^2 - 10s$. We find the [extrema](@entry_id:271659) by differentiating [@problem_id:1607678]:
$\frac{dK}{ds} = -3s^2 - 14s - 10 = 0 \implies 3s^2 + 14s + 10 = 0$
The solutions are $s = \frac{-7 \pm \sqrt{19}}{3}$. The real-axis locus exists on $(-2, 0)$ and $(-\infty, -5)$.
*   $s_1 = \frac{-7 + \sqrt{19}}{3} \approx -0.880$. This point is in the interval $(-2, 0)$, which is on the locus. This is a valid [breakaway point](@entry_id:276550).
*   $s_2 = \frac{-7 - \sqrt{19}}{3} \approx -3.786$. This point is in the interval $(-5, -2)$, which is not on the locus. This is not a valid point.
Thus, the locus breaks away from the real axis at $s = \frac{-7 + \sqrt{19}}{3}$.

#### Rule 7: Angle of Departure and Angle of Arrival

*   **Angle of Departure**: The angle at which a locus branch leaves a complex open-loop pole is called the [angle of departure](@entry_id:264341), $\theta_d$. It is found by applying the angle condition to a point infinitesimally close to the pole in question. The formula is derived as:
    $\theta_d = 180^\circ - (\sum \text{angles from other poles}) + (\sum \text{angles from zeros})$
    More formally, for a departure from pole $p_k$:
    $\theta_d = (2r+1)180^\circ - \sum_{j \neq k} \angle(p_k - p_j) + \sum_i \angle(p_k - z_i)$ for some integer $r$.
    
    Consider a system with a zero at $s=0$ and [complex poles](@entry_id:274945) at $p_{1,2} = -1 \pm j$. To find the [angle of departure](@entry_id:264341) from the pole $p_1 = -1+j$ [@problem_id:1607707]:
    The angle contribution from the zero $z_1=0$ to $p_1$ is $\angle(p_1 - z_1) = \angle(-1+j) = 135^\circ$.
    The angle contribution from the other pole $p_2=-1-j$ to $p_1$ is $\angle(p_1 - p_2) = \angle(2j) = 90^\circ$.
    The angle condition near $p_1$ requires that $\sum \angle(\text{vectors from zeros}) - \sum \angle(\text{vectors from poles}) = (2r+1)180^\circ$.
    This becomes $135^\circ - (\theta_d + 90^\circ) = (2r+1)180^\circ$.
    Choosing $r=0$ for the [principal value](@entry_id:192761), we get:
    $\theta_d = 135^\circ - 90^\circ - 180^\circ = -135^\circ$.
    The branch leaves the pole at $-1+j$ at an angle of $-135^\circ$.

*   **Angle of Arrival**: Similarly, the angle at which a locus branch arrives at a complex open-loop zero is the **[angle of arrival](@entry_id:265527)**, $\theta_a$. The calculation is analogous and applies the angle condition to a point infinitesimally close to the zero in question. The formula becomes:
    $\theta_a = (2r+1)180^\circ - \sum_j \angle(z_k - p_j) + \sum_{i \neq k} \angle(z_k - z_i)$

By systematically applying these rules, one can generate an accurate sketch of the [root locus](@entry_id:272958), providing a powerful graphical tool for analyzing and designing [feedback control systems](@entry_id:274717).