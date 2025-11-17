## Introduction
While the hyperbolic functions are familiar from real calculus, their inverses take on a new level of depth and complexity in the complex plane. Inverse [hyperbolic functions](@entry_id:165175) are fundamental constructs in complex analysis, providing elegant solutions to a wide range of problems. However, their transition from the real line to the complex plane introduces a critical challenge: they are inherently multi-valued. This article addresses this complexity, providing a clear framework for understanding and applying these powerful functions.

This article will guide you through the theoretical and practical landscape of complex inverse hyperbolic functions. In "Principles and Mechanisms," you will learn how these functions are defined via the [complex logarithm](@entry_id:174857), leading to their multi-valued nature, and how to manage this using the concepts of [branch points](@entry_id:166575), [branch cuts](@entry_id:163934), and [principal values](@entry_id:189577). The next chapter, "Applications and Interdisciplinary Connections," will showcase the versatility of these functions as indispensable tools for [integral calculus](@entry_id:146293), [conformal mapping](@entry_id:144027), and even in describing the non-Euclidean geometries of modern physics. Finally, "Hands-On Practices" will provide you with the opportunity to apply these concepts and solidify your understanding through a series of guided problems.

## Principles and Mechanisms

The hyperbolic functions, defined in terms of the exponential function, extend naturally into the complex plane. Their inverses—the inverse hyperbolic functions—are consequently fundamental tools in complex analysis, finding applications in [conformal mapping](@entry_id:144027), the evaluation of integrals, and the solution of differential equations. Unlike their real-valued counterparts, complex inverse [hyperbolic functions](@entry_id:165175) are inherently multi-valued, a direct consequence of the periodic nature of the [complex exponential function](@entry_id:169796). This chapter elucidates the principles governing these functions, from their definition and logarithmic representation to their analytic structure, including branch points, [branch cuts](@entry_id:163934), and derivatives.

### From Inversion to Logarithmic Representation

The inverse hyperbolic functions are defined, as their name suggests, by inverting the standard [hyperbolic functions](@entry_id:165175). For a given complex number $z$, if $w = \operatorname{arcsinh}(z)$, then $z = \sinh(w)$. To find an explicit expression for $w$ in terms of $z$, we leverage the exponential definitions of the hyperbolic functions.

Let us consider the inverse hyperbolic tangent, $w = \operatorname{arctanh}(z)$. By definition, $z = \tanh(w)$. Using the exponential form of the hyperbolic tangent, we have:
$$
z = \frac{\sinh(w)}{\cosh(w)} = \frac{(e^w - e^{-w})/2}{(e^w + e^{-w})/2} = \frac{e^{2w} - 1}{e^{2w} + 1}
$$
Our goal is to solve this algebraic equation for $w$. Rearranging the terms to isolate $e^{2w}$ yields:
$$
z(e^{2w} + 1) = e^{2w} - 1 \\
z e^{2w} + z = e^{2w} - 1 \\
z + 1 = e^{2w}(1 - z) \\
e^{2w} = \frac{1+z}{1-z}
$$
To solve for $w$, we take the [complex logarithm](@entry_id:174857) of both sides. The [complex logarithm](@entry_id:174857) is a multi-valued function, which is the source of the multi-valued nature of the inverse hyperbolic functions. Denoting the multi-valued logarithm as $\ln(\cdot)$, we have:
$$
2w = \ln\left(\frac{1+z}{1-z}\right)
$$
Thus, the complete set of values for $\operatorname{arctanh}(z)$ is given by:
$$
\operatorname{arctanh}(z) = \frac{1}{2} \ln\left(\frac{1+z}{1-z}\right)
$$
Here, for any non-zero complex number $\zeta$, the logarithm is $\ln(\zeta) = \text{Log}(\zeta) + 2k\pi i$, where $\text{Log}(\zeta)$ is the [principal value](@entry_id:192761), defined as $\text{Log}(\zeta) = \ln|\zeta| + i \text{Arg}(\zeta)$ with the [principal argument](@entry_id:171517) $\text{Arg}(\zeta)$ typically in the interval $(-\pi, \pi]$, and $k$ is any integer.

A similar procedure can be applied to derive the logarithmic forms for all six inverse [hyperbolic functions](@entry_id:165175). For example, to find the expression for $w = \operatorname{arccsch}(z)$, we start with $z = \text{csch}(w) = \frac{2}{e^w - e^{-w}}$. Letting $y = e^w$, this equation becomes a quadratic in $y$:
$$
zy - zy^{-1} = 2 \implies zy^2 - 2y - z = 0
$$
The solutions for $y$ are given by the quadratic formula:
$$
y = e^w = \frac{2 \pm \sqrt{4+4z^2}}{2z} = \frac{1 \pm \sqrt{1+z^2}}{z}
$$
Taking the logarithm gives $w = \ln\left(\frac{1 \pm \sqrt{1+z^2}}{z}\right)$. In this expression, both the square root and the logarithm are multi-valued. A careful analysis [@problem_id:2247672] shows that the two signs $(\pm)$ and the multiple branches of the logarithm can be elegantly combined into a single expression involving an integer parameter $n$.

The general logarithmic representations are:
- $\operatorname{arcsinh}(z) = \ln(z + \sqrt{z^2+1})$
- $\operatorname{arccosh}(z) = \ln(z + \sqrt{z^2-1})$
- $\operatorname{arctanh}(z) = \frac{1}{2}\ln\left(\frac{1+z}{1-z}\right)$
- $\operatorname{arccoth}(z) = \frac{1}{2}\ln\left(\frac{z+1}{z-1}\right)$
- $\operatorname{arcsech}(z) = \ln\left(\frac{1+\sqrt{1-z^2}}{z}\right)$
- $\operatorname{arccsch}(z) = \ln\left(\frac{1+\sqrt{1+z^2}}{z}\right)$

To see these definitions in practice, let's find all possible values of $\operatorname{arctanh}(1+i)$ [@problem_id:2247696]. We first compute the argument of the logarithm:
$$
\frac{1+z}{1-z} = \frac{1+(1+i)}{1-(1+i)} = \frac{2+i}{-i} = \frac{(2+i)i}{(-i)i} = -1+2i
$$
Now we must find $\frac{1}{2}\ln(-1+2i)$. For the complex number $-1+2i$, the modulus is $|-1+2i| = \sqrt{(-1)^2 + 2^2} = \sqrt{5}$, and its [principal argument](@entry_id:171517) is $\text{Arg}(-1+2i) = \pi - \arctan(2)$. Therefore, the multi-valued logarithm is:
$$
\ln(-1+2i) = \ln(\sqrt{5}) + i(\pi - \arctan(2) + 2k\pi) = \frac{1}{2}\ln(5) + i(\pi(1+2k) - \arctan(2))
$$
for any integer $k$. The set of values for $\operatorname{arctanh}(1+i)$ is then:
$$
\operatorname{arctanh}(1+i) = \frac{1}{2} \left[ \frac{1}{2}\ln(5) + i(\pi - \arctan(2) + 2k\pi) \right] = \frac{1}{4}\ln(5) + i\left(\frac{\pi}{2} - \frac{1}{2}\arctan(2) + k\pi\right)
$$
This calculation demonstrates that for a single input $z$, there is an infinite, discrete set of output values for the inverse hyperbolic function.

### Branch Points, Branch Cuts, and Principal Values

The multi-valued nature of these functions necessitates the concepts of **branch points** and **[branch cuts](@entry_id:163934)**. A [branch point](@entry_id:169747) is a singularity in the complex plane where the multiple values of a function converge. If we trace a small closed loop around a [branch point](@entry_id:169747), the function's value does not return to its starting value.

A powerful method for locating the finite branch points of an [inverse function](@entry_id:152416), say $w=f^{-1}(z)$, is to find the **[critical points](@entry_id:144653)** of the original function, $z=f(w)$. These are the points where the derivative $f'(w)$ vanishes. The images of these critical points, $z_c = f(w_c)$ where $f'(w_c)=0$, are the branch points of $f^{-1}(z)$.

Let's apply this to $w=\operatorname{arccosh}(z)$. The direct function is $z=\cosh(w)$. Its derivative is $\frac{dz}{dw} = \sinh(w)$. Setting the derivative to zero gives $\sinh(w)=0$, which occurs for $w_n = n\pi i$ where $n$ is an integer. The corresponding values of $z$ are the critical values:
$$
z_n = \cosh(w_n) = \cosh(n\pi i) = \cos(n\pi) = (-1)^n
$$
Thus, the critical values are $z=1$ (for even $n$) and $z=-1$ (for odd $n$). These are the finite branch points of $\operatorname{arccosh}(z)$ [@problem_id:2247704].

To work with these functions in a single-valued context, we introduce **[branch cuts](@entry_id:163934)**, which are curves in the complex plane that we define as "off-limits". By preventing paths from encircling branch points, we can restrict the function to a single, continuous sheet of its domain, creating a single-valued and analytic function known as a **branch** of the original function. The most common choice is the **[principal branch](@entry_id:164844)**, typically denoted with a capital letter (e.g., $\operatorname{Arcsinh}(z)$), which is obtained by selecting the [principal value](@entry_id:192761) of the underlying logarithm and/or square root.

The location of the [branch cuts](@entry_id:163934) for a [principal branch](@entry_id:164844) is determined by the arguments of the logarithms and square roots in its definition. For the [principal value](@entry_id:192761) of the logarithm, $\text{Log}(\zeta)$, the [branch cut](@entry_id:174657) is conventionally placed along the non-positive real axis, $(-\infty, 0]$.
Consider the [principal branch](@entry_id:164844) of the inverse hyperbolic tangent, $\operatorname{Artanh}(z)$:
$$
\operatorname{Artanh}(z) = \frac{1}{2}[\text{Log}(1+z) - \text{Log}(1-z)]
$$
This function is discontinuous where the arguments of the logarithms are on the non-positive real axis [@problem_id:2247654].
1.  $1+z \in (-\infty, 0]$ implies $\text{Im}(z)=0$ and $\text{Re}(1+z) \le 0$, which means $z=x$ with $x \le -1$. This gives the [branch cut](@entry_id:174657) $(-\infty, -1]$.
2.  $1-z \in (-\infty, 0]$ implies $\text{Im}(z)=0$ and $\text{Re}(1-z) \le 0$, which means $z=x$ with $x \ge 1$. This gives the branch cut $[1, \infty)$.
Combining these, the [principal branch](@entry_id:164844) $\operatorname{Artanh}(z)$ has [branch cuts](@entry_id:163934) on the real axis along $(-\infty, -1] \cup [1, \infty)$.

The [branch cuts](@entry_id:163934) for other functions can be similarly determined. For $\operatorname{Arcsinh}(z) = \text{Log}(z+\sqrt{z^2+1})$, the analysis is slightly more complex as it involves the [branch cuts](@entry_id:163934) of both the square root and the logarithm [@problem_id:2247681]. The [principal square root](@entry_id:180892) $\sqrt{\zeta}$ has a cut on $(-\infty, 0)$. Thus, $\sqrt{z^2+1}$ has cuts where $z^2+1$ is real and negative, which occurs for $z=iy$ where $|y| \ge 1$. A further analysis shows that the argument of the logarithm, $z+\sqrt{z^2+1}$, does not fall on the non-positive real axis for any $z$ not on these cuts. Therefore, the function $\operatorname{Arcsinh}(z)$ is analytic on the entire complex plane except for two cuts along the [imaginary axis](@entry_id:262618): $\{iy : y \in (-\infty, -1] \cup [1, \infty)\}$.

Branch points can also arise from composition. For a function $f(z) = \operatorname{arcsinh}(\operatorname{arctanh}(z))$ [@problem_id:2247678]:
- The inner function $\operatorname{arctanh}(z)$ has branch points at $z=\pm 1$.
- The outer function $\operatorname{arcsinh}(w)$ has branch points at $w=\pm i$.
- We must therefore find the values of $z$ for which $\operatorname{arctanh}(z) = \pm i$. This gives $z = \tanh(\pm i) = \pm i \tan(1)$.
The complete set of finite branch points for $\operatorname{arcsinh}(\operatorname{arctanh}(z))$ is therefore $\{1, -1, i\tan(1), -i\tan(1)\}$.

### Derivatives of Principal Branches

Once a [principal branch](@entry_id:164844) is defined by specifying its [branch cuts](@entry_id:163934), it becomes an [analytic function](@entry_id:143459) on its domain. We can then compute its derivative using standard rules. One method is [implicit differentiation](@entry_id:137929). If $w = \operatorname{Arccosh}(z)$, then $z = \cosh(w)$. Differentiating with respect to $z$ gives $1 = \sinh(w) \frac{dw}{dz}$, so $\frac{dw}{dz} = \frac{1}{\sinh(w)}$. Since $\cosh^2(w) - \sinh^2(w) = 1$, we have $\sinh(w) = \sqrt{\cosh^2(w)-1} = \sqrt{z^2-1}$. The choice of sign for the square root must be consistent with the chosen branch. For the [principal branch](@entry_id:164844), this leads to:
$$
\frac{d}{dz}\operatorname{Arccosh}(z) = \frac{1}{\sqrt{z^2-1}}
$$
This formula is valid on $\mathbb{C} \setminus (-\infty, 1]$.

Alternatively, we can use the [chain rule](@entry_id:147422) on definitions involving other functions. For instance, the [principal branch](@entry_id:164844) $\operatorname{Arcsech}(z)$ can be defined as $\operatorname{Arccosh}(1/z)$. Using the chain rule [@problem_id:2247694]:
$$
\frac{d}{dz}\operatorname{Arcsech}(z) = \frac{d}{dz}\operatorname{Arccosh}\left(\frac{1}{z}\right) = \frac{1}{\sqrt{(1/z)^2-1}} \cdot \left(-\frac{1}{z^2}\right) = \frac{-1}{z^2 \sqrt{\frac{1-z^2}{z^2}}} = \frac{-1}{z^2 \frac{\sqrt{1-z^2}}{z}} = \frac{-1}{z\sqrt{1-z^2}}
$$
This derivative is valid on the domain where $\operatorname{Arcsech}(z)$ is analytic, which is $\mathbb{C} \setminus ((-\infty, 0] \cup [1, \infty))$.

### Identities in the Complex Plane

The rich structure of complex inverse hyperbolic functions gives rise to numerous identities. These identities must often be interpreted in the context of multi-valuedness, meaning they relate sets of values rather than single numbers.

A fundamental property is symmetry. For example, $\operatorname{arcsinh}(z)$ is an [odd function](@entry_id:175940). In the multi-valued sense, this means that the set of values for $\operatorname{arcsinh}(-z)$ is the negative of the set for $\operatorname{arcsinh}(z)$. What is the value of $\operatorname{arcsinh}(z) + \operatorname{arcsinh}(-z)$? Let us consider $z=i$ [@problem_id:2247687].
We have $z^2+1 = i^2+1 = 0$, so $\sqrt{z^2+1} = 0$.
$$
\operatorname{arcsinh}(i) = \ln(i) = \left\{ i\left(\frac{\pi}{2} + 2k\pi\right) : k \in \mathbb{Z} \right\}
$$
Similarly, for $z=-i$, we have $(-i)^2+1=0$.
$$
\operatorname{arcsinh}(-i) = \ln(-i) = \left\{ i\left(-\frac{\pi}{2} + 2m\pi\right) : m \in \mathbb{Z} \right\}
$$
The sum $\operatorname{arcsinh}(i) + \operatorname{arcsinh}(-i)$ is the set of all possible sums of an element from each set:
$$
\left\{ i\left(\frac{\pi}{2} + 2k\pi\right) + i\left(-\frac{\pi}{2} + 2m\pi\right) \right\} = \{ 2\pi i (k+m) : k, m \in \mathbb{Z} \} = \{ 2n\pi i : n \in \mathbb{Z} \}
$$
This shows that while the function is odd, the sum $\operatorname{arcsinh}(z) + \operatorname{arcsinh}(-z)$ is not simply zero, but the set of all even integer multiples of $\pi i$.

Another crucial class of identities connects the inverse [hyperbolic functions](@entry_id:165175) to the [inverse trigonometric functions](@entry_id:170957). The identity $\sinh(iw) = i\sin(w)$ has a direct analogue for the [inverse functions](@entry_id:141256): $\operatorname{arcsinh}(iz) = i\arcsin(z)$. To prove this as a multi-valued identity [@problem_id:2247697], we must show that the set of values on the left is identical to the set of values on the right.
Let $S_1 = \operatorname{arcsinh}(iz)$ and $S_2 = i \cdot \arcsin(z)$.
Using the logarithmic definitions:
$$
S_1 = \ln\left(iz + \sqrt{(iz)^2+1}\right) = \ln\left(iz + \sqrt{1-z^2}\right)
$$
And for the inverse sine:
$$
\arcsin(z) = -i \ln\left(iz + \sqrt{1-z^2}\right)
$$
Multiplying by $i$:
$$
S_2 = i \cdot \left(-i \ln\left(iz + \sqrt{1-z^2}\right)\right) = \ln\left(iz + \sqrt{1-z^2}\right)
$$
The expressions for the sets $S_1$ and $S_2$ are identical. Since all branches of the square root and logarithm are included, the sets themselves are identical, confirming the identity $\operatorname{arcsinh}(iz) = i\arcsin(z)$.

### Analytic Continuation and Riemann Surfaces

The multi-valued nature of these functions is best understood through the geometric concept of a Riemann surface. For $w = \operatorname{arccosh}(z)$, the Riemann surface consists of infinitely many sheets (the branches) connected at the [branch points](@entry_id:166575) $z=\pm 1$. Analytic continuation is the process of extending a function along a path, and it allows us to move from one branch to another.

Let's explore what happens to a value of $\operatorname{arccosh}(z)$ when it is analytically continued along a closed path $\gamma$ that starts and ends at a point $z_0$, encircling the [branch point](@entry_id:169747) $z=1$ once counter-clockwise but not encircling $z=-1$ [@problem_id:2247660].
Let $W(z)$ be a specific branch of $\operatorname{arccosh}(z)$, defined by $W(z) = \text{Log}(z + \sqrt{z^2-1})$, with a specific choice of branch for the square root. The term $\sqrt{z^2-1}$ can be factored as $\sqrt{z-1}\sqrt{z+1}$. As we traverse the loop $\gamma$ around $z=1$, the argument of $(z-1)$ increases by $2\pi$. This causes the value of $\sqrt{z-1}$ to be multiplied by $e^{i\pi}=-1$. The term $\sqrt{z+1}$ returns to its original value, as its argument's change is zero.
Therefore, after one full loop, the term $\sqrt{z^2-1}$ changes sign: $\sqrt{z^2-1} \to -\sqrt{z^2-1}$.
Let the initial value at $z_0$ be $W_i = \text{Log}(z_0 + \sqrt{z_0^2-1})$. The final value, $W_f$, is obtained by replacing $\sqrt{z_0^2-1}$ with $-\sqrt{z_0^2-1}$:
$$
W_f = \text{Log}(z_0 - \sqrt{z_0^2-1})
$$
We can relate this to the initial value. Note that $(z_0 + \sqrt{z_0^2-1})(z_0 - \sqrt{z_0^2-1}) = z_0^2 - (z_0^2-1) = 1$.
So, $z_0 - \sqrt{z_0^2-1} = \frac{1}{z_0 + \sqrt{z_0^2-1}}$.
This means:
$$
W_f = \text{Log}\left(\frac{1}{z_0 + \sqrt{z_0^2-1}}\right) = -\text{Log}(z_0 + \sqrt{z_0^2-1}) = -W_i
$$
The value on the new branch is the negative of the value on the original branch. The total change upon traversing the contour is $\Delta W = W_f - W_i = -2W_i$. This remarkable result shows precisely how the different branches of $\operatorname{arccosh}(z)$ are interconnected. Traversing a loop around a [branch point](@entry_id:169747) transitions us from one branch, $W$, to another, $-W$. This behavior is the essence of the function's multi-valued structure, visualized by its Riemann surface.