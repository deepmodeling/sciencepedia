## Introduction
In the study of complex analysis, understanding the behavior of functions near points where they are not analytic—their singularities—is of fundamental importance. While the Laurent series provides a complete local description, it is often overwhelmingly detailed. The central challenge addressed in this article is the extraction of the most vital piece of information from this series, a single coefficient that unlocks the function's integral properties: the residue.

This article provides a comprehensive guide to the theory and calculation of residues at [isolated singularities](@entry_id:166795). In **Principles and Mechanisms**, you will learn the formal definition of the residue and master the essential techniques for its calculation, from direct [series expansion](@entry_id:142878) for [essential singularities](@entry_id:178894) to powerful formulas for simple and higher-order poles. Following this, **Applications and Interdisciplinary Connections** will demonstrate the remarkable utility of [residue calculus](@entry_id:171988) in solving complex [contour integrals](@entry_id:177264), evaluating real [improper integrals](@entry_id:138794), and analyzing systems in fields ranging from signal processing to physics. Finally, **Hands-On Practices** will allow you to solidify your understanding by tackling a series of curated problems. By navigating these chapters, you will gain a deep appreciation for the residue as a cornerstone concept in complex analysis.

## Principles and Mechanisms

The Laurent series provides a complete description of a function's behavior near an [isolated singularity](@entry_id:178349). However, for many applications, particularly in the evaluation of [complex integrals](@entry_id:202758), this representation contains far more information than is necessary. It turns out that a single coefficient from this series, the **residue**, holds the key to understanding the function's most essential singular properties and its integral behavior. This chapter will define the residue and establish the principal mechanisms for its calculation.

### The Definition of the Residue

Let a function $f(z)$ have an [isolated singularity](@entry_id:178349) at a point $z_0$. In a punctured neighborhood of this point, $0 \lt |z-z_0| \lt R$, $f(z)$ can be uniquely represented by its Laurent series:
$$
f(z) = \sum_{n=-\infty}^{\infty} c_n (z-z_0)^n = \cdots + \frac{c_{-2}}{(z-z_0)^2} + \frac{c_{-1}}{z-z_0} + c_0 + c_1(z-z_0) + \cdots
$$
The **residue** of $f(z)$ at $z_0$, denoted $\operatorname{Res}(f, z_0)$ or $\operatorname{Res}(f(z), z_0)$, is defined as the coefficient $c_{-1}$ of the $(z-z_0)^{-1}$ term in this expansion.

The uniqueness of the Laurent [series expansion](@entry_id:142878) ensures that the residue is a well-defined complex number for any [isolated singularity](@entry_id:178349). The special role of the $c_{-1}$ term stems from its integration properties. When integrating term-by-term around a [simple closed contour](@entry_id:176484) $\gamma$ enclosing $z_0$, every term of the form $(z-z_0)^n$ for $n \neq -1$ integrates to zero. Only the term with $n=-1$ yields a non-zero result:
$$
\oint_\gamma c_n (z-z_0)^n \,dz = \begin{cases} 2\pi i \, c_{-1}  \text{if } n=-1 \\ 0  \text{if } n \neq -1 \end{cases}
$$
This leads to the foundational result of the Residue Theorem, which states that $\oint_\gamma f(z) \,dz = 2\pi i \, \operatorname{Res}(f, z_0)$. Consequently, the ability to calculate the residue $c_{-1}$ is of paramount practical importance.

### Direct Calculation from Laurent Series

The definition of the residue itself provides the most fundamental method of calculation: determine the Laurent series for the function about the singularity and identify the coefficient $c_{-1}$. This method is universally applicable to any type of [isolated singularity](@entry_id:178349)—removable, pole, or essential.

For **[essential singularities](@entry_id:178894)**, direct expansion into a Laurent series is often the only viable method. Consider the function $f(z) = z^2 \sin\left(\frac{1}{z}\right)$, which has an [essential singularity](@entry_id:173860) at $z_0=0$. We can find its residue by using the well-known Maclaurin series for the sine function, $\sin(u) = u - u^3/3! + u^5/5! - \cdots$. By substituting $u = 1/z$, we obtain the Laurent series for $\sin(1/z)$:
$$
\sin\left(\frac{1}{z}\right) = \frac{1}{z} - \frac{1}{3! z^3} + \frac{1}{5! z^5} - \cdots
$$
Multiplying by $z^2$ gives the series for $f(z)$:
$$
f(z) = z^2\left(\frac{1}{z} - \frac{1}{6 z^3} + \frac{1}{120 z^5} - \cdots\right) = z - \frac{1}{6z} + \frac{1}{120 z^3} - \cdots
$$
By inspection, the coefficient of the $z^{-1}$ term is $c_{-1} = -1/6$. Therefore, $\operatorname{Res}(f, 0) = -1/6$ [@problem_id:2285598]. A similar procedure can be applied to functions like $f(z) = z^3 \cos(1/z)$. Using the series for cosine, $\cos(u) = 1 - u^2/2! + u^4/4! - \cdots$, we find:
$$
f(z) = z^3\left(1 - \frac{1}{2! z^2} + \frac{1}{4! z^4} - \frac{1}{6! z^6} + \cdots\right) = z^3 - \frac{z}{2} + \frac{1}{24z} - \frac{1}{720z^3} + \cdots
$$
The residue at $z=0$ is the coefficient of $z^{-1}$, which is $c_{-1} = 1/24$ [@problem_id:2263581].

This [series expansion](@entry_id:142878) method is also highly effective for some **poles**, especially when the function involves familiar analytic components. For instance, to find the residue of $f(z) = \frac{1 - \cosh(az)}{z^3}$ at $z=0$, we can expand the numerator. The Maclaurin series for $\cosh(w)$ is $1 + w^2/2! + w^4/4! + \cdots$.
$$
1 - \cosh(az) = 1 - \left(1 + \frac{(az)^2}{2!} + \frac{(az)^4}{4!} + \cdots\right) = -\frac{a^2z^2}{2} - \frac{a^4z^4}{24} - \cdots
$$
Dividing by $z^3$ gives the Laurent series for $f(z)$ about $z=0$:
$$
f(z) = \frac{1}{z^3}\left(-\frac{a^2z^2}{2} - \frac{a^4z^4}{24} - \cdots\right) = -\frac{a^2}{2z} - \frac{a^4z}{24} - \cdots
$$
From this expansion, we can immediately identify the residue as $c_{-1} = -a^2/2$. We also see that the [principal part](@entry_id:168896) of the series starts with $z^{-1}$, confirming that the singularity at $z=0$ is a [simple pole](@entry_id:164416), despite the $z^3$ in the denominator [@problem_id:2263598].

### Formulas for Calculating Residues at Poles

While the Laurent series method is always valid, computing the full series is often inefficient when we only need a single coefficient. For poles, a set of powerful formulas allows for a more direct computation of the residue.

#### Simple Poles

A singularity $z_0$ is a **[simple pole](@entry_id:164416)** (a pole of order 1) if the principal part of the Laurent series is simply $c_{-1}/(z-z_0)$. In this case, the function $\phi(z) = (z-z_0)f(z)$ is analytic (more precisely, has a [removable singularity](@entry_id:175597)) at $z_0$. The value of $\phi(z_0)$ is precisely $c_{-1}$. This leads to the first formula for [simple poles](@entry_id:175768):
$$
\operatorname{Res}(f, z_0) = \lim_{z \to z_0} (z-z_0)f(z)
$$
For example, consider the function $f(z) = \frac{\cosh(kz)}{z(z-a)^2}$, which has a [simple pole](@entry_id:164416) at $z=0$ (assuming $a \neq 0$). Applying the formula:
$$
\operatorname{Res}(f, 0) = \lim_{z \to 0} z \cdot \frac{\cosh(kz)}{z(z-a)^2} = \lim_{z \to 0} \frac{\cosh(kz)}{(z-a)^2} = \frac{\cosh(0)}{(-a)^2} = \frac{1}{a^2}
$$
[@problem_id:2263607].

A particularly useful specialization of this rule exists for functions expressed as a quotient $f(z) = P(z)/Q(z)$, where $P(z)$ and $Q(z)$ are analytic at $z_0$. If $P(z_0) \neq 0$ and $Q(z)$ has a simple zero at $z_0$ (i.e., $Q(z_0)=0$ and $Q'(z_0) \neq 0$), then $f(z)$ has a [simple pole](@entry_id:164416) at $z_0$. The residue can be computed as:
$$
\operatorname{Res}(f, z_0) = \frac{P(z_0)}{Q'(z_0)}
$$
This elegant formula can be derived by applying L'Hôpital's rule to the limit formula: $\lim_{z \to z_0} \frac{(z-z_0)P(z)}{Q(z)} = \lim_{z \to z_0} \frac{P(z) + (z-z_0)P'(z)}{Q'(z)} = \frac{P(z_0)}{Q'(z_0)}$.

As an illustration, let's find the residue of $f(z) = \frac{z^2 + 2z + i}{z^3 + z^2 - 5z + 3}$ at the simple pole $z_0 = -3$. Here, $P(z) = z^2+2z+i$ and $Q(z) = z^3+z^2-5z+3$. First, we verify the conditions: $P(-3) = (-3)^2 + 2(-3) + i = 3+i \neq 0$, and $Q(-3) = -27+9+15+3 = 0$. The derivative is $Q'(z) = 3z^2+2z-5$, so $Q'(-3) = 3(9) - 6 - 5 = 16 \neq 0$. Since the conditions hold, we can apply the formula directly:
$$
\operatorname{Res}(f, -3) = \frac{P(-3)}{Q'(-3)} = \frac{3+i}{16} = \frac{3}{16} + \frac{1}{16}i
$$
[@problem_id:2263593].

#### Poles of Order m

If $f(z)$ has a pole of order $m \gt 1$ at $z_0$, its Laurent series begins with the term $c_{-m}/(z-z_0)^m$. To isolate $c_{-1}$, we can first multiply $f(z)$ by $(z-z_0)^m$. This clears the pole, resulting in a function $\phi(z) = (z-z_0)^m f(z)$ that is analytic at $z_0$:
$$
\phi(z) = c_{-m} + c_{-m+1}(z-z_0) + \cdots + c_{-1}(z-z_0)^{m-1} + c_0(z-z_0)^m + \cdots
$$
This is now the Taylor series for $\phi(z)$ around $z_0$. The coefficient we seek, $c_{-1}$, is the coefficient of the $(z-z_0)^{m-1}$ term. From the formula for Taylor coefficients, we know that this coefficient is given by $\frac{\phi^{(m-1)}(z_0)}{(m-1)!}$. This gives us the general formula for the residue at a pole of order $m$:
$$
\operatorname{Res}(f, z_0) = \frac{1}{(m-1)!} \lim_{z \to z_0} \frac{d^{m-1}}{dz^{m-1}}\left[ (z-z_0)^m f(z) \right]
$$
For a **double pole** ($m=2$), this simplifies to:
$$
\operatorname{Res}(f, z_0) = \lim_{z \to z_0} \frac{d}{dz}\left[ (z-z_0)^2 f(z) \right]
$$
For instance, the function $f(z) = \frac{z\exp(z)}{(z-i)^2}$ has a double pole at $z_0=i$. Here, $(z-i)^2f(z) = z\exp(z)$. The residue is:
$$
\operatorname{Res}(f, i) = \lim_{z \to i} \frac{d}{dz}[z\exp(z)] = \lim_{z \to i} [\exp(z) + z\exp(z)] = (1+i)\exp(i)
$$
Using Euler's formula, $\exp(i) = \cos(1) + i\sin(1)$, we can write the final result as $(\cos(1)-\sin(1)) + i(\cos(1)+\sin(1))$ [@problem_id:2263621]. This same formula for a double pole can be used for the singularity at $z=a$ of the function $f(z) = \frac{\cosh(kz)}{z(z-a)^2}$ from our earlier example [@problem_id:2263607].

For **higher-order poles**, the calculation can become algebraically intensive due to the repeated differentiations. Consider $f(z) = \frac{\exp(z)\cos(z)}{z^4}$, which has a pole of order 4 at $z_0=0$. Using the general formula with $m=4$:
$$
\operatorname{Res}(f, 0) = \frac{1}{3!} \lim_{z \to 0} \frac{d^3}{dz^3}\left[ z^4 \frac{\exp(z)\cos(z)}{z^4} \right] = \frac{1}{6} \left[ \frac{d^3}{dz^3} (\exp(z)\cos(z)) \right]_{z=0}
$$
The third derivative of $g(z) = \exp(z)\cos(z)$ evaluated at $z=0$ is required. While this can be done with the [product rule](@entry_id:144424), a clever use of Euler's identity for $\cos(z)$ simplifies the work. Letting $g(z) = \frac{1}{2}(\exp((1+i)z) + \exp((1-i)z))$, the third derivative is easily found to be $g'''(z) = \frac{1}{2}((1+i)^3\exp((1+i)z) + (1-i)^3\exp((1-i)z))$. Evaluating at $z=0$ gives $g'''(0) = \frac{1}{2}((1+i)^3+(1-i)^3) = \frac{1}{2}((-2+2i)+(-2-2i)) = \frac{1}{2}(-4) = -2$. The residue is therefore $\frac{1}{6}(-2) = -1/3$ [@problem_id:2263620].

### Advanced Topics and Generalizations

The principles of [residue calculation](@entry_id:174587) can be extended to more abstract scenarios and to the entire complex plane.

#### Residues from Functional Properties

Sometimes we can determine a residue based on the general properties of the functions involved, without knowing their explicit forms. Suppose a function $h(z)$ is analytic near $z_0$ and has a simple zero at that point, meaning $h(z_0)=0$ and $h'(z_0) \neq 0$. What is the residue of $g(z) = \frac{1}{[h(z)]^2}$ at $z_0$?

Since $h(z)$ has a simple zero at $z_0$, its Taylor series starts as $h(z) = h'(z_0)(z-z_0) + \frac{h''(z_0)}{2}(z-z_0)^2 + \cdots$. Therefore, $[h(z)]^2$ has a zero of order 2, and $g(z)$ has a pole of order 2 at $z_0$. We can find the residue by expanding $g(z)$ in a Laurent series:
$$
g(z) = \frac{1}{\left( h'(z_0)(z-z_0) + \frac{h''(z_0)}{2}(z-z_0)^2 + \cdots \right)^2}
$$
$$
= \frac{1}{[h'(z_0)]^2(z-z_0)^2} \left( 1 + \frac{h''(z_0)}{2h'(z_0)}(z-z_0) + \cdots \right)^{-2}
$$
Using the [binomial expansion](@entry_id:269603) $(1+u)^{-2} = 1 - 2u + \cdots$, with $u = \frac{h''(z_0)}{2h'(z_0)}(z-z_0)$, the term we are interested in is:
$$
g(z) = \frac{1}{[h'(z_0)]^2(z-z_0)^2} \left( 1 - 2\frac{h''(z_0)}{2h'(z_0)}(z-z_0) + \cdots \right) = \frac{1}{[h'(z_0)]^2(z-z_0)^2} - \frac{h''(z_0)}{[h'(z_0)]^3(z-z_0)} + \cdots
$$
The residue, which is the coefficient of $(z-z_0)^{-1}$, is thus found to be $-\frac{h''(z_0)}{[h'(z_0)]^3}$. This remarkable result connects the residue to the local geometric properties of the function $h(z)$: its rate of change $h'(z_0)$ and its [concavity](@entry_id:139843) $h''(z_0)$ at the zero [@problem_id:2263611].

#### The Residue at Infinity

It is often useful to consider the behavior of a function "at infinity." The **point at infinity** can be treated as a single point, compactifying the complex plane into the Riemann sphere. The behavior of $f(z)$ for large $|z|$ is analyzed by the transformation $z = 1/w$, which maps the [point at infinity](@entry_id:154537) to the origin $w=0$. The residue of $f(z)$ at $z=\infty$ is defined in terms of the residue of a transformed function at $w=0$:
$$
\operatorname{Res}(f, \infty) = \operatorname{Res}\left(-\frac{1}{w^2}f\left(\frac{1}{w}\right), 0\right)
$$
The factor $-1/w^2$ is the Jacobian of the transformation, arising from $dz = -1/w^2 dw$.

An equivalent and often more practical definition is that $\operatorname{Res}(f, \infty) = -c_{-1}$, where $c_{-1}$ is the coefficient of the $z^{-1}$ term in the Laurent series of $f(z)$ that is valid for large $|z|$ (i.e., outside a large circle containing all finite singularities). The negative sign is a crucial convention; it arises because a counter-clockwise contour enclosing the origin and all finite singularities corresponds to a clockwise-oriented contour with respect to the [point at infinity](@entry_id:154537).

For example, let's calculate the [residue at infinity](@entry_id:178509) for the function $f(z) = \frac{5z^4 + 2z^2 - 8}{2z^5 - z^3 + 9} + \frac{z^2 - 3}{z^4 + 1}$. For large $|z|$, we can analyze the leading terms:
$$
f(z) \approx \frac{5z^4}{2z^5} + \frac{z^2}{z^4} = \frac{5}{2z} + \frac{1}{z^2}
$$
This suggests that the $z^{-1}$ coefficient in the Laurent series at infinity is $c_{-1} = 5/2$. To be more rigorous, we can find $c_{-1} = \lim_{z \to \infty} z f(z)$ when the limit exists. In this case, the second term vanishes in the limit: $\lim_{z \to \infty} z \frac{z^2-3}{z^4+1} = 0$. The limit of the first term is:
$$
\lim_{z \to \infty} z \frac{5z^4 + 2z^2 - 8}{2z^5 - z^3 + 9} = \lim_{z \to \infty} \frac{5z^5 + 2z^3 - 8z}{2z^5 - z^3 + 9} = \frac{5}{2}
$$
Thus, the full Laurent series for $f(z)$ at infinity begins $f(z) = \frac{5}{2}z^{-1} + O(z^{-2})$. The coefficient is $c_{-1} = 5/2$. Therefore, the [residue at infinity](@entry_id:178509) is $\operatorname{Res}(f, \infty) = -c_{-1} = -5/2$ [@problem_id:2263583].

The concept of the [residue at infinity](@entry_id:178509) culminates in a powerful statement: for any function with a finite number of [isolated singularities](@entry_id:166795) in the [extended complex plane](@entry_id:165233), the sum of all its residues (including the one at infinity) is zero. This theorem provides a useful check on calculations and can be an alternative method for finding a particularly difficult residue if all others are easier to compute.

#### Residues of Composite Functions

Calculating the residue of a composite function, $h(z) = f(g(z))$, requires careful analysis. A singularity can arise at $z_0$ if $g(z_0)$ is a singularity of $f(w)$. Consider the case where $f(w) = \frac{\exp(w)}{(w-i)^2}$ and $g(z) = \frac{2z+i}{1-z}$. We want to find the residue of $h(z) = f(g(z))$ at $z=0$.

First, we observe that $g(0) = i$, which is a double pole for $f(w)$. Thus, $z=0$ is a singularity for $h(z)$. What is its order? We examine the derivative of the inner function: $g'(z) = \frac{2+i}{(1-z)^2}$, so $g'(0) = 2+i \neq 0$. Because the mapping $w=g(z)$ is locally conformal and non-degenerate at $z=0$, it preserves the order of the pole. Therefore, $h(z)$ has a double pole at $z=0$.

To find the residue, we apply the formula for a double pole to $h(z)$ directly. We need to compute the derivative of $z^2 h(z)$ at $z=0$.
$$
h(z) = f(g(z)) = \frac{\exp(g(z))}{(g(z)-i)^2}
$$
The denominator term is $g(z)-i = \frac{2z+i}{1-z} - i = \frac{z(2+i)}{1-z}$. Substituting this in, we get:
$$
z^2 h(z) = z^2 \frac{\exp(g(z))}{\left(\frac{z(2+i)}{1-z}\right)^2} = \frac{(1-z)^2 \exp(g(z))}{(2+i)^2}
$$
Now we differentiate this expression with respect to $z$ and evaluate at $z=0$. After applying the product and chain rules, the calculation yields $\operatorname{Res}(h, 0) = \frac{i \exp(i)}{(2+i)^2}$, which simplifies to $\frac{(4+3i)\exp(i)}{25}$ [@problem_id:2263584]. This example illustrates that while no simple "chain rule" for residues exists, a direct application of the fundamental formulas to the composite function is the correct path forward.