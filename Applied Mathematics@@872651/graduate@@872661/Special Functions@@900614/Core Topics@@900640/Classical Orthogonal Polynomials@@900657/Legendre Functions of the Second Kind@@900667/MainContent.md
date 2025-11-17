## Introduction
The Legendre differential equation is a cornerstone of [mathematical physics](@entry_id:265403), and its complete solution requires two linearly independent sets of functions. While the Legendre polynomials, $P_n(x)$, provide the regular solutions familiar to many, a full understanding of the solution space necessitates an exploration of the second family: the Legendre functions of the second kind, $Q_n(x)$. These functions, characterized by their singular behavior at $x = \pm 1$, are often overlooked but are indispensable for solving physical problems where the domain of interest excludes these singular points. This article provides a comprehensive exploration of these vital functions. It will systematically derive $Q_n(x)$ and establish their fundamental properties, including recurrence relations and integral representations. Following this, it will demonstrate their crucial role in fields like [potential theory](@entry_id:141424) and hydrodynamics, and their deep connections within [mathematical analysis](@entry_id:139664). Finally, guided problems are provided to solidify computational fluency and theoretical understanding of Legendre functions of the second kind.

## Principles and Mechanisms

In the study of differential equations, particularly those arising in mathematical physics, a complete understanding of the solution space is paramount. The Legendre differential equation,
$$ (1-x^2)\frac{d^2y}{dx^2} - 2x\frac{dy}{dx} + n(n+1)y = 0 $$
is a cornerstone of this field. As a second-order linear [ordinary differential equation](@entry_id:168621), its general solution is a linear combination of two [linearly independent](@entry_id:148207) functions. For integer values of the parameter $n$, one family of solutions is the well-known Legendre polynomials, $P_n(x)$, which are distinguished by their regularity at the endpoints $x = \pm 1$. This chapter is dedicated to the systematic exploration of the second family of solutions: the **Legendre functions of the second kind**, denoted by $Q_n(x)$. These functions are indispensable for problems where the physical domain excludes the [singular points](@entry_id:266699) $x = \pm 1$, and they possess a rich mathematical structure that we will now unravel.

### Derivation via Reduction of Order

The most direct method for finding a second, [linearly independent solution](@entry_id:174476) to a second-order ODE when one solution is already known is the method of **[reduction of order](@entry_id:140559)**. Let $y_1(x)$ be a known solution to $y'' + p(x)y' + q(x)y = 0$. A second solution, $y_2(x)$, can be found using the formula:
$$ y_2(x) = y_1(x) \int \frac{\exp\left(-\int p(t) dt\right)}{[y_1(t)]^2} dt $$

Let us apply this powerful technique to the Legendre equation. In its standard form, the equation is $y'' - \frac{2x}{1-x^2}y' + \frac{n(n+1)}{1-x^2}y = 0$, so we identify $p(x) = -\frac{2x}{1-x^2}$. A straightforward integration gives:
$$ -\int p(x) dx = \int \frac{2x}{1-x^2} dx = -\ln(1-x^2) $$
Therefore, the exponential term in the [reduction of order formula](@entry_id:192210) simplifies to $\exp(-\ln(1-x^2)) = \frac{1}{1-x^2}$.

The simplest case is for $n=0$, where the Legendre equation becomes $(1-x^2)y'' - 2xy' = 0$. One solution is the Legendre polynomial $P_0(x) = 1$. Using this as $y_1(x)$, we can find the second solution, which we will call $Q_0(x)$. The Wronskian, $W(y_1, y_2) = y_1 y_2' - y_1' y_2$, provides a more direct path in this case. For any two solutions of the Legendre equation, Abel's identity implies their Wronskian $W(x)$ satisfies $W(x) = C \exp(-\int p(x) dx) = \frac{C}{1-x^2}$. By convention, the Legendre functions of the second kind are normalized such that the constant $C=1$. With $P_0(x)=1$ and $P_0'(x)=0$, the Wronskian becomes $W(P_0, Q_0) = (1)Q_0'(x) - (0)Q_0(x) = Q_0'(x)$. Setting this equal to the normalized Wronskian gives:
$$ Q_0'(x) = \frac{1}{1-x^2} $$
Integrating this expression with respect to $x$ for the domain $x \in (-1, 1)$ yields the explicit form of $Q_0(x)$ [@problem_id:778788].
$$ Q_0(x) = \int \frac{dx}{1-x^2} = \frac{1}{2} \int \left(\frac{1}{1+x} + \frac{1}{1-x}\right) dx = \frac{1}{2} \ln\left(\frac{1+x}{1-x}\right) $$
The constant of integration is chosen to be zero to make $Q_0(x)$ an odd function. This logarithmic form immediately reveals the singular nature of $Q_0(x)$ at $x = \pm 1$.

This process can be repeated for higher orders. For $n=1$, the Legendre equation is $(1-x^2)y'' - 2xy' + 2y = 0$, and a solution is $P_1(x)=x$. Applying the [reduction of order formula](@entry_id:192210) with $y_1(x) = x$, the second solution $Q_1(x)$ is found by evaluating the integral [@problem_id:2117620]:
$$ Q_1(x) = x \int \frac{1}{t^2(1-t^2)} dt $$
Using [partial fraction decomposition](@entry_id:159208), $\frac{1}{t^2(1-t^2)} = \frac{1}{t^2} + \frac{1}{1-t^2}$. Integrating this term by term gives:
$$ \int \left(\frac{1}{t^2} + \frac{1}{1-t^2}\right) dt = -\frac{1}{t} + \frac{1}{2}\ln\left(\frac{1+t}{1-t}\right) $$
Substituting back and multiplying by $y_1(x)=x$, we obtain:
$$ Q_1(x) = x \left(-\frac{1}{x} + \frac{1}{2}\ln\left(\frac{1+x}{1-x}\right)\right) = -1 + \frac{x}{2}\ln\left(\frac{1+x}{1-x}\right) = xQ_0(x) - 1 $$
This result not only provides the explicit form for $Q_1(x)$ but also reveals a fundamental structural relationship between $Q_1(x)$, $Q_0(x)$, and the corresponding Legendre polynomial $P_1(x)=x$.

### General Form and Recurrence Relations

The patterns observed for $n=0$ and $n=1$ generalize to any integer order $n$. For $x \in (-1, 1)$, the Legendre function of the second kind, $Q_n(x)$, can be expressed as:
$$ Q_n(x) = \frac{1}{2} P_n(x) \ln\left(\frac{1+x}{1-x}\right) - W_{n-1}(x) $$
Here, $P_n(x)$ is the Legendre polynomial of degree $n$, and $W_{n-1}(x)$ is a polynomial of degree $n-1$. This form elegantly separates the function into a part with the characteristic [logarithmic singularity](@entry_id:190437), modulated by $P_n(x)$, and a purely polynomial part. The polynomial $W_{n-1}(x)$ is given by the specific summation:
$$ W_{n-1}(x) = \sum_{k=0}^{\lfloor (n-1)/2 \rfloor} \frac{2n-4k-1}{(2k+1)(n-k)} P_{n-2k-1}(x) $$
For instance, for $n=2$, the sum has only a $k=0$ term, giving $W_1(x) = \frac{3}{2}P_1(x) = \frac{3}{2}x$. This allows for the direct calculation of functions like $Q_2(x)$ [@problem_id:710338]. Given $P_2(x) = \frac{1}{2}(3x^2-1)$, the expression for $Q_2(x)$ is:
$$ Q_2(x) = \frac{1}{2} \left(\frac{1}{2}(3x^2 - 1)\right) \ln\left(\frac{1+x}{1-x}\right) - \frac{3}{2}x = \frac{3x^2-1}{4}\ln\left(\frac{1+x}{1-x}\right) - \frac{3x}{2} $$
Evaluating this at $x=1/2$ gives $Q_2(1/2) = \frac{1}{2}P_2(1/2)\ln(3) - \frac{3}{4} = \frac{1}{2}(-\frac{1}{8})\ln(3) - \frac{3}{4} = -\frac{1}{16}\ln(3) - \frac{3}{4}$.

Furthermore, the Legendre functions of the second kind satisfy the same [three-term recurrence relation](@entry_id:176845) as the Legendre polynomials:
$$ (n+1)Q_{n+1}(x) = (2n+1)x Q_n(x) - n Q_{n-1}(x) $$
This relation is extremely powerful, as it allows for the algebraic generation of the entire sequence of $Q_n(x)$ functions starting from $Q_0(x)$ and $Q_1(x)$. Let's demonstrate this by deriving $Q_2(x)$ again, this time using the recurrence [@problem_id:1133295]. Setting $n=1$:
$$ 2Q_2(x) = (2(1)+1)x Q_1(x) - 1 \cdot Q_0(x) = 3x Q_1(x) - Q_0(x) $$
Substituting the known expressions $Q_1(x) = xQ_0(x)-1$, we get:
$$ 2Q_2(x) = 3x(xQ_0(x) - 1) - Q_0(x) = (3x^2 - 1)Q_0(x) - 3x $$
$$ Q_2(x) = \frac{3x^2 - 1}{2}Q_0(x) - \frac{3x}{2} $$
Substituting the definition of $Q_0(x)$ recovers the exact same expression for $Q_2(x)$ derived previously, confirming the consistency and utility of the [recurrence relation](@entry_id:141039).

### Linear Independence and the Wronskian

The linear independence of $P_n(x)$ and $Q_n(x)$ is formally established by their non-vanishing Wronskian, $W(P_n, Q_n)(x) = P_n(x)Q_n'(x) - P_n'(x)Q_n(x)$. As mentioned, Abel's identity dictates that the Wronskian must be of the form $C/(1-x^2)$. The standard normalization of $Q_n(x)$ fixes the constant $C=1$, leading to the fundamental identity:
$$ W(P_n(x), Q_n(x)) = \frac{1}{1-x^2} $$
This identity can be elegantly proven using [recurrence relations](@entry_id:276612) without resorting to the explicit, and often cumbersome, forms of the functions themselves [@problem_id:1119272]. The key is to use a derivative recurrence relation satisfied by both $P_n$ and $Q_n$, namely $(1-x^2)y_n' = n(y_{n-1} - xy_n)$, and a Wronskian-type identity connecting different orders, $P_n Q_{n-1} - P_{n-1} Q_n = \frac{1}{n}$. Substituting the derivative relations into the definition of the Wronskian gives:
\begin{align*}
W(P_n, Q_n) = P_n \left(\frac{n(Q_{n-1} - xQ_n)}{1-x^2}\right) - Q_n \left(\frac{n(P_{n-1} - xP_n)}{1-x^2}\right) \\
= \frac{n}{1-x^2} \left( P_n Q_{n-1} - x P_n Q_n - Q_n P_{n-1} + x Q_n P_n \right) \\
= \frac{n}{1-x^2} \left( P_n Q_{n-1} - P_{n-1} Q_n \right)
\end{align*}
Using the identity $P_n Q_{n-1} - P_{n-1} Q_n = \frac{1}{n}$, we immediately arrive at the desired result:
$$ W(P_n, Q_n) = \frac{n}{1-x^2} \left(\frac{1}{n}\right) = \frac{1}{1-x^2} $$
This result holds for any $x$ where the functions are defined. For example, one could undertake the laborious task of computing $W(P_3(x), Q_3(x))$ at a specific point, say $x=3$. The result would be $\frac{1}{1-3^2} = -\frac{1}{8}$ [@problem_id:710484], providing a concrete verification of this essential identity.

### Integral Representations

Integral representations provide alternative definitions for [special functions](@entry_id:143234) that are often more convenient for analysis, especially in the complex plane or for deriving asymptotic behaviors.

#### Neumann's Integral Representation

For a complex variable $z$ not on the real interval $[-1, 1]$, the Legendre function of the second kind is defined by **Neumann's integral representation**:
$$ Q_n(z) = \frac{1}{2} \int_{-1}^{1} \frac{P_n(x)}{z-x} dx $$
This definition elegantly constructs $Q_n(z)$ from the corresponding polynomial $P_n(x)$. The function defined this way is analytic in the complex plane with a [branch cut](@entry_id:174657) along the interval $[-1, 1]$. To see the power of this representation, let's re-derive $Q_0(z)$ [@problem_id:870436]. With $P_0(x)=1$, the integral becomes:
$$ Q_0(z) = \frac{1}{2} \int_{-1}^{1} \frac{1}{z-x} dx = \frac{1}{2} [-\ln(z-x)]_{-1}^{1} = \frac{1}{2} [-\ln(z-1) + \ln(z+1)] $$
$$ Q_0(z) = \frac{1}{2}\ln\left(\frac{z+1}{z-1}\right) $$
This result coincides perfectly with our previous findings for real $x$, but now naturally extends the function's domain to the complex plane.

#### Laplace's First Integral Representation

For real values of the argument $x > 1$, another powerful representation is **Laplace's [first integral](@entry_id:274642)**:
$$ Q_n(x) = \int_0^\infty \frac{du}{(x+\sqrt{x^2-1}\cosh u)^{n+1}} $$
This form is particularly useful for studying the behavior of $Q_n(x)$ for large $x$. Let us once again verify this representation for the [base case](@entry_id:146682) $n=0$ [@problem_id:710413]. The integral is $Q_0(x) = \int_0^\infty \frac{du}{x+\sqrt{x^2-1}\cosh u}$. This integral can be evaluated using the substitution $t = \tanh(u/2)$. The calculation confirms that the integral evaluates precisely to $\frac{1}{2}\ln(\frac{x+1}{x-1})$, confirming consistency across all three definitions presented. A direct numerical evaluation, for instance $Q_0(5/3)$, would yield $\frac{1}{2}\ln(\frac{5/3+1}{5/3-1}) = \frac{1}{2}\ln(4) = \ln(2)$ [@problem_id:710413].

### Analysis Near the Singular Points

The behavior of $Q_n(x)$ near its [singular points](@entry_id:266699) is of great theoretical and practical importance. The form $Q_n(x) = \frac{1}{2}P_n(x)\ln(\frac{1+x}{1-x}) - W_{n-1}(x)$ clearly shows the logarithmic singularities. For analysis near $x=1$, it is often beneficial to isolate the singular term. We can rewrite the logarithm as $\ln(\frac{x+1}{x-1}) = \ln(x+1) - \ln(x-1)$, which allows us to express $Q_n(x)$ as:
$$ Q_n(x) = -\frac{1}{2} P_n(x) \ln(x-1) + \left[ \frac{1}{2} P_n(x) \ln(x+1) - W_{n-1}(x) \right] $$
The term in the brackets is a function that is regular (analytic) at $x=1$. Let's call it $R_n(x)$. The value of this regular part at the [singular point](@entry_id:171198), $R_n(1)$, is a well-defined and important constant. We can find it by taking the limit as $x \to 1$:
$$ R_n(1) = \lim_{x\to 1} \left[ \frac{1}{2} P_n(x) \ln(x+1) - W_{n-1}(x) \right] = \frac{1}{2} P_n(1) \ln(2) - W_{n-1}(1) $$
Using the relation $P_n(1)=1$, this simplifies to:
$$ R_n(1) = \frac{1}{2}\ln(2) - W_{n-1}(1) $$
Let's apply this to find $R_2(1)$ [@problem_id:710489]. We previously found that $Q_2(x) = P_2(x)Q_0(x) - \frac{3}{2}x$. Comparing this with the general structure, we identify $W_1(x) = \frac{3}{2}x$. Thus, $W_1(1) = 3/2$. The regular part at $x=1$ can be found from the expression for $R_n(x)$:
$$ R_2(x) = \frac{1}{2} P_2(x) \ln(x+1) - W_1(x) = \frac{1}{2} \left(\frac{3x^2-1}{2}\right)\ln(x+1) - \frac{3x}{2} $$
Evaluating at $x=1$ (where $P_2(1)=1$):
$$ R_2(1) = \frac{1}{2} (1) \ln(1+1) - \frac{3(1)}{2} = \frac{1}{2}\ln(2) - \frac{3}{2} $$
This kind of analysis is crucial for matching solutions across [singular points](@entry_id:266699) in physical problems.

### Associated Legendre Functions of the Second Kind

Just as the Legendre polynomials $P_n(x)$ are generalized to the associated Legendre functions $P_n^m(x)$, the functions $Q_n(x)$ can be generalized to the **associated Legendre functions of the second kind**, $Q_n^m(x)$. For $|x|>1$, they are defined by a differentiation formula analogous to that for $P_n^m(x)$:
$$ Q_n^m(x) = (x^2-1)^{m/2} \frac{d^m}{dx^m} Q_n(x) $$
These functions are solutions to the associated Legendre differential equation and are required for solving problems in [spherical coordinates](@entry_id:146054) that lack [azimuthal symmetry](@entry_id:181872). As an example, let's find the value of $Q_2^1(2)$ [@problem_id:710491]. First, we need the derivative of $Q_2(x)$:
$$ Q_2(x) = \frac{3x^2-1}{4}\ln\left(\frac{x+1}{x-1}\right) - \frac{3x}{2} $$
$$ \frac{dQ_2}{dx} = \frac{3x}{2}\ln\left(\frac{x+1}{x-1}\right) + \frac{3x^2-1}{4}\left(\frac{-2}{x^2-1}\right) - \frac{3}{2} = \frac{3x}{2}\ln\left(\frac{x+1}{x-1}\right) - \frac{3x^2-2}{x^2-1} $$
Now we apply the definition of $Q_2^1(x)$:
$$ Q_2^1(x) = (x^2-1)^{1/2} \frac{dQ_2}{dx} = \sqrt{x^2-1} \left[ \frac{3x}{2}\ln\left(\frac{x+1}{x-1}\right) - \frac{3x^2-2}{x^2-1} \right] $$
Evaluating at $x=2$:
$$ Q_2^1(2) = \sqrt{3} \left[ \frac{3(2)}{2}\ln\left(\frac{3}{1}\right) - \frac{3(2^2)-2}{2^2-1} \right] = \sqrt{3} \left[ 3\ln(3) - \frac{10}{3} \right] = 3\sqrt{3}\ln(3) - \frac{10\sqrt{3}}{3} $$
This calculation demonstrates the direct application of the definition and provides a glimpse into the broader family of [special functions](@entry_id:143234) built upon the foundation of $Q_n(x)$.