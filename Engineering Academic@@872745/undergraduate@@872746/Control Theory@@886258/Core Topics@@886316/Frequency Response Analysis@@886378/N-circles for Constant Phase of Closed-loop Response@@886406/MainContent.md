## Introduction
In the design and analysis of [feedback control systems](@entry_id:274717), a central challenge is understanding how the [open-loop frequency response](@entry_id:267477), represented by a Nyquist plot, translates into the behavior of the final closed-loop system. While the Nyquist plot of $G(j\omega)$ is a powerful tool for assessing stability, it does not inherently reveal quantitative performance metrics like the phase of the closed-loop response, $T(j\omega)$. This article introduces N-circles, a fundamental graphical method designed to bridge this gap by providing contours of constant closed-loop phase directly on the open-loop G-plane.

This article is structured to build a complete understanding of N-circles, from theory to practice. The first chapter, **Principles and Mechanisms**, will delve into the mathematical derivation of the N-circle equations and explore their distinct geometric properties. Following this theoretical foundation, the **Applications and Interdisciplinary Connections** chapter will demonstrate how N-circles are used for direct graphical analysis, [controller synthesis](@entry_id:261816), and how they relate to broader topics like robust and [digital control](@entry_id:275588). Finally, the **Hands-On Practices** section provides targeted exercises to reinforce these concepts and develop practical skills in applying N-circles to control problems.

## Principles and Mechanisms

In the analysis and design of [feedback control systems](@entry_id:274717), understanding the relationship between the [open-loop frequency response](@entry_id:267477), $G(j\omega)$, and the [closed-loop frequency response](@entry_id:273935), $T(j\omega)$, is paramount. For a canonical unity-feedback system, this relationship is given by:

$$T(j\omega) = \frac{G(j\omega)}{1+G(j\omega)}$$

While the Nyquist plot provides a complete graphical representation of the open-loop response $G(j\omega)$, it does not directly reveal the characteristics of the closed-loop response, such as its magnitude or phase. To bridge this gap, graphical aids known as M-circles and N-circles are employed. These are contours plotted on the same complex plane as $G(j\omega)$ (the **G-plane**) that represent loci of constant closed-loop magnitude and phase, respectively. This chapter focuses on the principles and mechanisms underlying the N-circles, which correspond to a constant phase of the closed-loop response.

### Derivation of the N-Circle Equation

Our primary goal is to find the set of all points $G(j\omega)$ in the complex G-plane that result in a closed-loop response $T(j\omega)$ with a constant phase angle, $\phi$. Let us represent the open-loop response in Cartesian coordinates as $G(j\omega) = x + iy$. Substituting this into the expression for $T(j\omega)$:

$$T(j\omega) = \frac{x + iy}{1 + (x + iy)} = \frac{x + iy}{(1+x) + iy}$$

To separate the real and imaginary parts of $T(j\omega)$, we multiply the numerator and denominator by the [complex conjugate](@entry_id:174888) of the denominator, $(1+x) - iy$:

$$T(j\omega) = \frac{(x + iy)((1+x) - iy)}{((1+x) + iy)((1+x) - iy)} = \frac{x(1+x) - ixy + iy(1+x) - i^2y^2}{(1+x)^2 + y^2}$$

Simplifying the numerator by grouping real and imaginary terms, and using $i^2 = -1$:

$$T(j\omega) = \frac{(x + x^2 + y^2) + i(y + xy - xy)}{(1+x)^2 + y^2} = \frac{x + x^2 + y^2}{(1+x)^2 + y^2} + i \frac{y}{(1+x)^2 + y^2}$$

The [phase angle](@entry_id:274491) of the closed-loop response is $\phi = \arg[T(j\omega)]$. The tangent of this angle is the ratio of the imaginary part to the real part of $T(j\omega)$:

$$\tan(\phi) = \frac{\Im\{T(j\omega)\}}{\Re\{T(j\omega)\}} = \frac{\frac{y}{(1+x)^2 + y^2}}{\frac{x + x^2 + y^2}{(1+x)^2 + y^2}} = \frac{y}{x^2 + x + y^2}$$

It is conventional to define a parameter $N = \tan(\phi)$. With this definition, the condition for a constant closed-loop phase becomes:

$$N = \frac{y}{x^2 + x + y^2}$$

Rearranging this expression gives the general equation for the locus of points $(x,y)$ corresponding to a constant $N$:

$$N(x^2 + x + y^2) = y$$

For $N \neq 0$, we can rearrange this into a more familiar form:

$$x^2 + x + y^2 - \frac{1}{N}y = 0$$

This equation is the fundamental equation for the family of N-circles.

### Geometric Properties of N-Circles

The equation $x^2 + x + y^2 - \frac{1}{N}y = 0$ is a quadratic in both $x$ and $y$ with equal coefficients for the $x^2$ and $y^2$ terms, which is characteristic of a circle. To determine the geometric properties of this circle, we complete the square for the $x$ and $y$ terms:

$$(x^2 + x) + (y^2 - \frac{1}{N}y) = 0$$

$$(x^2 + x + \frac{1}{4}) - \frac{1}{4} + (y^2 - \frac{1}{N}y + \frac{1}{4N^2}) - \frac{1}{4N^2} = 0$$

$$(x + \frac{1}{2})^2 + (y - \frac{1}{2N})^2 = \frac{1}{4} + \frac{1}{4N^2}$$

This is the [standard equation of a circle](@entry_id:164169), $(x-x_c)^2 + (y-y_c)^2 = R^2$. By inspection, we can identify the center and radius of the N-circle:

- **Center:** $(x_c, y_c) = \left(-\frac{1}{2}, \frac{1}{2N}\right)$
- **Radius:** $R = \sqrt{\frac{1}{4} + \frac{1}{4N^2}} = \frac{1}{2}\sqrt{1 + \frac{1}{N^2}}$

#### Illustrative Examples

Let's consider two specific cases to build intuition.

- Suppose we are interested in the locus for a closed-loop phase of $\phi = -45^\circ$. The corresponding parameter is $N = \tan(-45^\circ) = -1$. The center of this N-circle is at $(-\frac{1}{2}, \frac{1}{2(-1)}) = (-\frac{1}{2}, -\frac{1}{2})$, and its radius is $R = \frac{1}{2}\sqrt{1 + \frac{1}{(-1)^2}} = \frac{\sqrt{2}}{2}$ [@problem_id:1594796].

- For a closed-loop phase of $\phi = -30^\circ$, the parameter is $N = \tan(-30^\circ) = -1/\sqrt{3}$. The center is at $(-\frac{1}{2}, \frac{1}{2(-1/\sqrt{3})}) = (-\frac{1}{2}, -\frac{\sqrt{3}}{2})$, and the radius is $R = \frac{1}{2}\sqrt{1 + \frac{1}{(-1/\sqrt{3})^2}} = \frac{1}{2}\sqrt{1+3} = 1$ [@problem_id:1594775].

#### Locus of Centers and Behavior of Radius

The formula for the center, $(-\frac{1}{2}, \frac{1}{2N})$, reveals a remarkable property: the x-coordinate of the center of every N-circle is fixed at $x_c = -1/2$. As the phase angle $\phi$ (and thus $N$) varies, the y-coordinate $y_c = 1/(2N)$ sweeps through all real values. Therefore, **the locus of the centers of all N-circles is the vertical line $x = -1/2$** in the G-plane [@problem_id:1594819].

The radius, $R = \frac{1}{2}\sqrt{1 + 1/N^2}$, also exhibits a systematic behavior [@problem_id:1594783]:
- As $|N| \to \infty$ (corresponding to $\phi \to \pm 90^\circ$), the term $1/N^2 \to 0$, and the radius approaches its minimum value: $R \to 1/2$.
- As $|N| \to 0$ (corresponding to $\phi \to 0^\circ$ or $\phi \to \pm 180^\circ$), the term $1/N^2 \to \infty$, and the radius $R \to \infty$. This limiting case corresponds to a degenerate circle—a straight line.

### Key Features and Special Cases

The family of N-circles possesses several important structural features.

#### Common Intersection Points

A key property is that all N-circles, for any non-zero real value of $N$, intersect at two common points. We can find these points by observing the general equation $x^2 + x + y^2 - y/N = 0$. We seek solutions $(x, y)$ that are independent of $N$. This can only happen if the term containing $N$ vanishes, which requires $y=0$. Substituting $y=0$ into the equation gives:

$$x^2 + x = 0 \implies x(x+1) = 0$$

This yields two solutions: $x=0$ and $x=-1$. Therefore, **all N-circles pass through the origin $(0,0)$ and the critical point $(-1,0)$** in the G-plane [@problem_id:1594777]. These points correspond to $G(j\omega)=0$ and $G(j\omega)=-1$, respectively.

#### Degenerate Cases: The Real Axis

The case $N=0$ corresponds to a closed-loop phase of $\phi=0^\circ$ or $\phi=\pm 180^\circ$. As noted, the radius of the N-circle becomes infinite, and the locus degenerates into a straight line. The equation $N(x^2 + x + y^2) = y$ simplifies to $y=0$, which is the real axis of the G-plane.

To distinguish between $0^\circ$ and $180^\circ$ phase, we must examine the sign of $T(j\omega)$ when $G(j\omega) = x$ is purely real:

$$T = \frac{x}{1+x}$$

- A phase of $\phi = 0^\circ$ requires $T > 0$. This occurs when $x$ and $1+x$ have the same sign, which is true for the intervals $(-\infty, -1)$ and $(0, \infty)$.
- A phase of $\phi = 180^\circ$ requires $T  0$. This occurs when $x$ and $1+x$ have opposite signs, which is true for the interval $(-1, 0)$ [@problem_id:1594831].

Thus, the real axis is partitioned into three segments, corresponding to different closed-loop phases.

#### Symmetry

Consider two phase angles that are equal in magnitude but opposite in sign, $\phi = \alpha$ and $\phi = -\alpha$. The corresponding parameters are $N_+ = \tan(\alpha)$ and $N_- = \tan(-\alpha) = -N_+$. The centers of the respective N-circles are:

- Center for $+\alpha$: $(-\frac{1}{2}, \frac{1}{2\tan(\alpha)})$
- Center for $-\alpha$: $(-\frac{1}{2}, -\frac{1}{2\tan(\alpha)})$

The radii are identical since $R$ depends on $N^2$. This shows that the N-circles for $\pm \alpha$ are mirror images of each other with respect to the real axis ($y=0$) [@problem_id:1594820].

### Application in Frequency Response Analysis

N-circles provide a powerful graphical method to determine the closed-loop phase response directly from the open-loop Nyquist plot.

When the Nyquist plot of $G(j\omega)$ is superimposed on a chart of N-circles, **any intersection between the Nyquist plot and an N-circle for a parameter $N$ indicates a frequency $\omega$ at which the closed-loop phase is $\phi = \arctan(N)$**.

For instance, if at a frequency $\omega_p$, the open-loop response is found to be $G(j\omega_p) = -0.800 - j0.900$, this point lies on a specific N-circle. To find the corresponding closed-loop phase, we can directly compute $T(j\omega_p)$:

$$T(j\omega_p) = \frac{-0.800 - j0.900}{1 + (-0.800 - j0.900)} = \frac{-0.800 - j0.900}{0.200 - j0.900} \approx 0.765 - j1.059$$

The phase is $\arg[T(j\omega_p)] = \arctan(\frac{-1.059}{0.765}) \approx -54.2^\circ$. This means the point $(-0.800, -0.900)$ lies on the N-circle for $\phi=-54.2^\circ$ [@problem_id:1594839].

Conversely, to identify which N-circle a given point $G(j\omega_k) = x+iy$ lies upon, one can compute the value of $N$ directly from its definition. For a point $G(j\omega_k) = -1.2 + j0.9$, we have $x=-1.2$ and $y=0.9$. Using the derived formula:

$$N = \frac{y}{x^2 + x + y^2} = \frac{0.9}{(-1.2)^2 + (-1.2) + (0.9)^2} = \frac{0.9}{1.44 - 1.2 + 0.81} = \frac{0.9}{1.05} \approx 0.857$$

This point lies on the N-circle corresponding to a closed-loop phase of $\phi = \arctan(0.857)$ [@problem_id:1594778].

Finally, it is worth noting that the family of N-circles is intrinsically related to the family of **M-circles**, which are loci of constant closed-loop magnitude $|T(j\omega)| = M$. Together, these two families of circles form a curvilinear coordinate system on the G-plane. A fundamental property of these families is that they are **mutually orthogonal**: at every intersection point, the tangent to the M-circle is perpendicular to the tangent to the N-circle. This orthogonality is a consequence of the analytic properties of the mapping $T(G)$ and is extremely useful in graphical design methods using tools like the Hall chart [@problem_id:1594804].