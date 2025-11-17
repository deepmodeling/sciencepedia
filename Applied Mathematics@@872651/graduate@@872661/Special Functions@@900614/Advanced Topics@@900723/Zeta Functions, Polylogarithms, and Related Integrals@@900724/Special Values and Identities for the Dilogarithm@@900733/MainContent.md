## Introduction
The [dilogarithm](@entry_id:202722), denoted as Li₂(z), is a special function that, despite its simple definition as a power series, holds a surprisingly deep and [complex structure](@entry_id:269128). First studied by Leonhard Euler, it appears in a remarkable variety of contexts, from pure mathematics to theoretical physics, often serving as a bridge between seemingly unrelated fields. The central challenge and allure of the [dilogarithm](@entry_id:202722) lie in its intricate web of functional identities. These equations are the key to unlocking its secrets, allowing for the calculation of specific values, the evaluation of challenging integrals, and the discovery of profound connections that are otherwise hidden from view.

This article provides a comprehensive journey into the world of the [dilogarithm](@entry_id:202722). It is structured to build your understanding from the ground up, starting with fundamental definitions and moving toward advanced, research-level applications. You will learn not only what the [dilogarithm](@entry_id:202722) is but, more importantly, what it *does* and why it is an indispensable tool for mathematicians and physicists.

Our exploration unfolds across three chapters. The first chapter, **Principles and Mechanisms**, establishes the theoretical foundation, introducing the formal definitions of the [dilogarithm](@entry_id:202722) and systematically deriving its most important [functional equations](@entry_id:199663). The second chapter, **Applications and Interdisciplinary Connections**, showcases the power of these principles, revealing how the [dilogarithm](@entry_id:202722) is applied to solve concrete problems in number theory, hyperbolic geometry, and quantum field theory. Finally, the **Hands-On Practices** chapter provides an opportunity to solidify your knowledge by working through guided problems that require the strategic application of the identities and concepts you have learned.

## Principles and Mechanisms

Following the introduction to the [dilogarithm function](@entry_id:181405), this chapter delves into the core principles and mechanisms that govern its behavior. We will begin by formalizing its definitions and exploring its most fundamental properties. We will then systematically uncover the rich algebraic structure of the [dilogarithm](@entry_id:202722), manifest in a web of [functional equations](@entry_id:199663). These identities are not mere mathematical curiosities; they are powerful tools that allow for the computation of specific values of the function, the evaluation of [definite integrals](@entry_id:147612), and the discovery of profound connections to other areas of mathematics and physics.

### Definitions and Fundamental Values

The [dilogarithm](@entry_id:202722) is the special case $s=2$ of a more general class of functions known as polylogarithms, $\text{Li}_s(z)$. Throughout this text, the **[dilogarithm function](@entry_id:181405)**, $\text{Li}_2(z)$, is defined for any complex number $z$ with $|z| \le 1$ by the power series:

$$
\text{Li}_2(z) = \sum_{k=1}^{\infty} \frac{z^k}{k^2}
$$

This [series representation](@entry_id:175860) is the most direct definition, but its utility is limited to the unit disk. A more broadly applicable definition is given by the integral representation:

$$
\text{Li}_2(z) = - \int_0^z \frac{\ln(1-t)}{t} dt
$$

Here, $\ln(1-t)$ denotes the [principal branch](@entry_id:164844) of the [complex logarithm](@entry_id:174857). This integral form defines an [analytic function](@entry_id:143459) in the complex plane with a [branch cut](@entry_id:174657), conventionally placed along the real axis from $1$ to $\infty$. The equivalence of these two definitions within the [unit disk](@entry_id:172324) can be demonstrated by expanding the integrand's logarithm into its Maclaurin series, $\ln(1-t) = -\sum_{k=1}^{\infty} t^k/k$, and integrating term-by-term.

From the series definition, several special values can be determined directly. For $z=1$, the [dilogarithm](@entry_id:202722) coincides with a famous value of the Riemann zeta function, a result first established by Leonhard Euler in the resolution of the Basel problem:

$$
\text{Li}_2(1) = \sum_{k=1}^{\infty} \frac{1}{k^2} = \zeta(2) = \frac{\pi^2}{6}
$$

For $z=-1$, we obtain the sum of the [alternating series](@entry_id:143758), which is related to the Dirichlet eta function $\eta(2)$:

$$
\text{Li}_2(-1) = \sum_{k=1}^{\infty} \frac{(-1)^k}{k^2} = -\sum_{k=1}^{\infty} \frac{(-1)^{k-1}}{k^2} = -\eta(2)
$$

Knowing that $\eta(s) = (1-2^{1-s})\zeta(s)$, we find $\eta(2) = (1-2^{-1})\zeta(2) = \frac{1}{2}\zeta(2) = \frac{\pi^2}{12}$. Therefore, we have the fundamental value:

$$
\text{Li}_2(-1) = -\frac{\pi^2}{12}
$$

The integral representation is particularly powerful for evaluating certain classes of [definite integrals](@entry_id:147612). Consider, for example, the integral $I = \int_0^1 \frac{\ln(1-x^2)}{x} dx$ [@problem_id:771587]. A substitution of $u=x^2$ yields $du = 2x dx$, so that $dx/x = du/(2u)$. The integral becomes:

$$
I = \int_0^1 \frac{\ln(1-u)}{2u} du = \frac{1}{2} \int_0^1 \frac{\ln(1-u)}{u} du = \frac{1}{2} \left[ - \text{Li}_2(u) \right]_0^1 = -\frac{1}{2} \text{Li}_2(1) = -\frac{\pi^2}{12}
$$

This elegantly demonstrates the intimate connection between the integral form of the [dilogarithm](@entry_id:202722) and specific values of the Riemann zeta function.

### The Major Two-Term Functional Equations

The true power of the [dilogarithm](@entry_id:202722) is unlocked through its [functional equations](@entry_id:199663). These identities relate the value of the [dilogarithm](@entry_id:202722) at different arguments. The most fundamental of these relate two [dilogarithm](@entry_id:202722) terms.

#### Euler's Reflection Formula

One of the most celebrated identities is **Euler's [reflection formula](@entry_id:198841)**, which connects $\text{Li}_2(z)$ and $\text{Li}_2(1-z)$:

$$
\text{Li}_2(z) + \text{Li}_2(1-z) = \frac{\pi^2}{6} - \ln(z)\ln(1-z)
$$

This identity is valid for complex $z$, with care taken for the [branch cuts](@entry_id:163934) of the logarithms. Its proof typically involves showing that the derivative of the left-hand side with respect to $z$ is equal to the derivative of the right-hand side. This identity is exceptionally useful for relating values within the interval $(0,1)$.

As an elegant application, consider the evaluation of $\text{Li}_2\left(\frac{3-\sqrt{5}}{2}\right)$ given the known value of the [dilogarithm](@entry_id:202722) at an argument related to the golden ratio, $\phi = \frac{1+\sqrt{5}}{2}$ [@problem_id:771650]. Let $z = \frac{\sqrt{5}-1}{2}$. We note that $z = \phi^{-1}$. Then, $1-z = 1 - \frac{\sqrt{5}-1}{2} = \frac{3-\sqrt{5}}{2}$. Interestingly, $\left(\frac{\sqrt{5}-1}{2}\right)^2 = \frac{5 - 2\sqrt{5} + 1}{4} = \frac{3-\sqrt{5}}{2}$, so $1-z=z^2$. We are asked to find $\text{Li}_2(1-z)$ given the value of $\text{Li}_2(z) = \frac{\pi^2}{10} - \ln^2\left(\frac{\sqrt{5}-1}{2}\right)$.

Applying the [reflection formula](@entry_id:198841):
$$
\text{Li}_2(z) + \text{Li}_2(1-z) = \frac{\pi^2}{6} - \ln(z)\ln(1-z)
$$
$$
\text{Li}_2\left(\frac{3-\sqrt{5}}{2}\right) = \frac{\pi^2}{6} - \ln(z)\ln(1-z) - \text{Li}_2(z)
$$
Substituting the given value for $\text{Li}_2(z)$:
$$
\text{Li}_2\left(\frac{3-\sqrt{5}}{2}\right) = \frac{\pi^2}{6} - \ln(z)\ln(1-z) - \left[ \frac{\pi^2}{10} - \ln^2(z) \right] = \frac{\pi^2}{15} + \ln^2(z) - \ln(z)\ln(1-z)
$$
The logarithmic part can be factored:
$$
\ln(z)[\ln(z) - \ln(1-z)] = \ln(z)\ln\left(\frac{z}{1-z}\right)
$$
Since $z = \phi^{-1}$ and $1-z=z^2=\phi^{-2}$, we have $\frac{z}{1-z} = \frac{\phi^{-1}}{\phi^{-2}} = \phi$. The logarithmic term becomes $\ln(\phi^{-1})\ln(\phi) = -\ln(\phi)\ln(\phi) = -\ln^2(\phi)$. Thus, the final value is:
$$
\text{Li}_2\left(\frac{3-\sqrt{5}}{2}\right) = \frac{\pi^2}{15} - \ln^2\left(\frac{1+\sqrt{5}}{2}\right)
$$

#### The Inversion Formula

The **inversion formula** relates the [dilogarithm](@entry_id:202722) of an argument $z$ to that of its reciprocal $1/z$:

$$
\text{Li}_2(z) + \text{Li}_2(1/z) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(-z)
$$

This identity is valid for $z \in \mathbb{C} \setminus [0,1]$. It is particularly important for evaluating the [dilogarithm](@entry_id:202722) outside the unit circle, where the defining [power series](@entry_id:146836) diverges, by relating it to a value inside the unit circle. The term $\ln(-z)$ requires careful handling of the [principal branch](@entry_id:164844) of the logarithm, where $\ln(-z) = \ln|z| + i \arg(-z)$.

A straightforward application of this formula is the evaluation of the sum $S = \text{Li}_2(-2) + \text{Li}_2(-1/2)$ [@problem_id:771581]. We can immediately recognize this as being of the form $\text{Li}_2(z) + \text{Li}_2(1/z)$ with $z=-2$. Since $z=-2$ is not in the excluded interval $[0,1]$, the formula applies directly:

$$
S = \text{Li}_2(-2) + \text{Li}_2(-1/2) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(-(-2)) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(2)
$$

### Further Functional Equations and Symmetries

Beyond the fundamental two-term relations, the [dilogarithm](@entry_id:202722) satisfies a host of other identities that reveal deeper symmetries.

#### Legendre's Duplication Formula

One such identity is **Legendre's [duplication formula](@entry_id:173961)**, which provides a relationship between arguments $z$, $-z$, and $z^2$:

$$
\text{Li}_2(z) + \text{Li}_2(-z) = \frac{1}{2} \text{Li}_2(z^2)
$$

This identity can be readily understood from the [power series](@entry_id:146836) definition: the sum of the series for $\text{Li}_2(z)$ and $\text{Li}_2(-z)$ causes all the odd power terms to cancel, leaving only the even power terms, which can then be related to the series for $\text{Li}_2(z^2)$.

We can verify this identity for the complex argument $z=i$ [@problem_id:771733]. The left-hand side (LHS) becomes $\text{Li}_2(i) + \text{Li}_2(-i)$, while the right-hand side (RHS) becomes $\frac{1}{2}\text{Li}_2(i^2) = \frac{1}{2}\text{Li}_2(-1)$. Using the known values $\text{Li}_2(-1) = -\frac{\pi^2}{12}$ and the complex value $\text{Li}_2(i) = -\frac{\pi^2}{48} + iG$ (where $G$ is Catalan's constant, which we will discuss shortly), we can evaluate both sides. Note that $\text{Li}_2(-i) = \overline{\text{Li}_2(i)} = -\frac{\pi^2}{48} - iG$.

LHS: $\text{Li}_2(i) + \text{Li}_2(-i) = \left(-\frac{\pi^2}{48} + iG\right) + \left(-\frac{\pi^2}{48} - iG\right) = -2 \times \frac{\pi^2}{48} = -\frac{\pi^2}{24}$.

RHS: $\frac{1}{2}\text{Li}_2(-1) = \frac{1}{2} \left(-\frac{\pi^2}{12}\right) = -\frac{\pi^2}{24}$.

The equality holds, demonstrating the consistency of the known special values with the [duplication formula](@entry_id:173961).

#### Landen's Identity

Another powerful relation, known as one of **Landen's identities**, connects the arguments $z$ and $z/(z-1)$:

$$
\text{Li}_2(z) + \text{Li}_2\left(\frac{z}{z-1}\right) = -\frac{1}{2}\ln^2(1-z)
$$

This identity is particularly useful because the transformation $z \mapsto z/(z-1)$ has order two, meaning applying it twice returns the original argument. It provides an alternative pathway for relating [dilogarithm](@entry_id:202722) values. For instance, we can derive the value of $\text{Li}_2(-1)$ from the known special value $\text{Li}_2(1/2) = \frac{\pi^2}{12} - \frac{1}{2}\ln^2(2)$ [@problem_id:771730]. By setting $z=1/2$, the argument $\frac{z}{z-1}$ becomes $\frac{1/2}{1/2-1} = \frac{1/2}{-1/2} = -1$. Substituting $z=1/2$ into Landen's identity gives:

$$
\text{Li}_2(1/2) + \text{Li}_2(-1) = -\frac{1}{2}\ln^2(1 - 1/2) = -\frac{1}{2}\ln^2(1/2) = -\frac{1}{2}(-\ln(2))^2 = -\frac{1}{2}\ln^2(2)
$$

Solving for $\text{Li}_2(-1)$:
$$
\text{Li}_2(-1) = -\frac{1}{2}\ln^2(2) - \text{Li}_2(1/2) = -\frac{1}{2}\ln^2(2) - \left( \frac{\pi^2}{12} - \frac{1}{2}\ln^2(2) \right) = -\frac{\pi^2}{12}
$$
This provides a beautiful alternative derivation for one of our fundamental constants.

#### The Distribution Identity

The **distribution** or **multiplication identity** generalizes the [duplication formula](@entry_id:173961). It relates $\text{Li}_2(z^N)$ to a sum of dilogarithms whose arguments are $z$ multiplied by the $N$-th [roots of unity](@entry_id:142597):

$$
\sum_{k=0}^{N-1} \text{Li}_2(z e^{2\pi i k/N}) = N^{1-2}\text{Li}_2(z^N) = \frac{1}{N} \text{Li}_2(z^N)
$$

This identity is a manifestation of a deep symmetry related to [cyclotomic polynomials](@entry_id:155668). It can be used to evaluate certain trigonometric series. For example, let's find the value of the series $S = \sum_{n=1}^\infty \frac{\cos(2n\pi/3)}{n^2}$ [@problem_id:771582]. We recognize this series as the real part of a [dilogarithm](@entry_id:202722) evaluated on the unit circle:

$$
S = \Re\left[ \sum_{n=1}^\infty \frac{(e^{2\pi i/3})^n}{n^2} \right] = \Re[\text{Li}_2(e^{2\pi i/3})]
$$

We apply the distribution identity with $N=3$ and $z=1$. The roots of unity are $1$, $e^{2\pi i/3}$, and $e^{4\pi i/3}$.
$$
\text{Li}_2(1) + \text{Li}_2(e^{2\pi i/3}) + \text{Li}_2(e^{4\pi i/3}) = \frac{1}{3}\text{Li}_2(1^3) = \frac{1}{3}\text{Li}_2(1)
$$
Since the series coefficients are real, $\text{Li}_2(\bar{z}) = \overline{\text{Li}_2(z)}$. Noting that $e^{4\pi i/3}$ is the complex conjugate of $e^{2\pi i/3}$, we have $\text{Li}_2(e^{4\pi i/3}) = \overline{\text{Li}_2(e^{2\pi i/3})}$. The sum becomes:
$$
\text{Li}_2(1) + \text{Li}_2(e^{2\pi i/3}) + \overline{\text{Li}_2(e^{2\pi i/3})} = \frac{1}{3}\text{Li}_2(1)
$$
$$
\text{Li}_2(1) + 2\Re[\text{Li}_2(e^{2\pi i/3})] = \frac{1}{3}\text{Li}_2(1)
$$
Solving for the real part, which is our series $S$:
$$
2S = \frac{1}{3}\text{Li}_2(1) - \text{Li}_2(1) = -\frac{2}{3}\text{Li}_2(1) = -\frac{2}{3}\frac{\pi^2}{6} = -\frac{\pi^2}{9} \implies S = -\frac{\pi^2}{18}
$$

### Connections to Related Functions and Constants

The study of the [dilogarithm](@entry_id:202722) is not an isolated pursuit; it is deeply connected with other important special functions and mathematical constants.

#### The Clausen Function and Catalan's Constant

When the argument of the [dilogarithm](@entry_id:202722) lies on the unit circle, its imaginary part defines the **Clausen function** of order 2:

$$
\text{Cl}_2(\theta) = \Im[\text{Li}_2(e^{i\theta})] = \sum_{k=1}^{\infty} \frac{\sin(k\theta)}{k^2}
$$

A particularly important value arises when we evaluate $\text{Li}_2(i) = \text{Li}_2(e^{i\pi/2})$ [@problem_id:771753]. By separating its defining series into real and imaginary parts:

$$
\text{Li}_2(i) = \sum_{k=1}^{\infty} \frac{i^k}{k^2} = \left( \frac{i^2}{2^2} + \frac{i^4}{4^2} + \dots \right) + \left( \frac{i^1}{1^2} + \frac{i^3}{3^2} + \dots \right)
$$

The real part consists of even terms ($k=2m$): $\sum_{m=1}^{\infty} \frac{i^{2m}}{(2m)^2} = \sum_{m=1}^{\infty} \frac{(-1)^m}{4m^2} = \frac{1}{4} \sum_{m=1}^{\infty} \frac{(-1)^m}{m^2} = \frac{1}{4}\text{Li}_2(-1) = -\frac{\pi^2}{48}$.

The imaginary part consists of odd terms ($k=2n+1$, for $n \ge 0$):
$$
\Im[\text{Li}_2(i)] = \sum_{n=0}^{\infty} \frac{\sin((2n+1)\pi/2)}{(2n+1)^2} = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)^2}
$$
This famous series defines **Catalan's constant**, $G$. Thus, we have the landmark value:
$$
\text{Li}_2(i) = -\frac{\pi^2}{48} + iG
$$
This also implies that $G = \text{Cl}_2(\pi/2)$. The [functional equations](@entry_id:199663) for the [dilogarithm](@entry_id:202722) can be translated into identities for the Clausen function. For example, taking the imaginary part of Legendre's [duplication formula](@entry_id:173961) at $z=e^{i\pi/4}$ gives a relation between Clausen function values and Catalan's constant [@problem_id:771580]:

$$
\Im[\text{Li}_2(e^{i\pi/4})] + \Im[\text{Li}_2(-e^{i\pi/4})] = \frac{1}{2}\Im[\text{Li}_2(i)]
$$
Recognizing that $-e^{i\pi/4} = e^{i\pi}e^{i\pi/4} = e^{i5\pi/4}$, this becomes:
$$
\text{Cl}_2(\pi/4) + \text{Cl}_2(5\pi/4) = \frac{1}{2}G
$$
Using the property $\text{Cl}_2(\pi+\theta) = -\text{Cl}_2(\pi-\theta)$, we have $\text{Cl}_2(5\pi/4) = \text{Cl}_2(\pi+\pi/4) = -\text{Cl}_2(\pi-\pi/4) = -\text{Cl}_2(3\pi/4)$. The identity simplifies to $\text{Cl}_2(\pi/4) - \text{Cl}_2(3\pi/4) = \frac{1}{2}G$.

#### The Rogers L-Function

Another closely related function is the **Rogers L-function**, defined as:

$$
L(z) = \text{Li}_2(z) + \frac{1}{2}\ln(z)\ln(1-z)
$$

Substituting this definition into Euler's [reflection formula](@entry_id:198841), $\text{Li}_2(z) + \text{Li}_2(1-z) = \frac{\pi^2}{6} - \ln(z)\ln(1-z)$, yields a remarkably simple identity for the Rogers function, $L(z) + L(1-z) = \frac{\pi^2}{6}$, which is valid for real $z \in (0,1)$.

It is an instructive exercise to investigate what happens to this relation outside of $(0,1)$, where the complex logarithms introduce additional phases. Let's test the value of $\Re[L(x) + L(1-x)]$ for $x=-1$ [@problem_id:771707]. We need to compute $L(-1) + L(2)$. This requires the values $\text{Li}_2(-1)$ and $\text{Li}_2(2)$, as well as careful evaluation of logs.
We know $\text{Li}_2(-1) = -\pi^2/12$. We can find $\text{Li}_2(2)$ using the inversion formula with $z=2$:
$\text{Li}_2(2) + \text{Li}_2(1/2) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(-2)$. Using $\ln(-2) = \ln(2)+i\pi$ and $\text{Li}_2(1/2)=\frac{\pi^2}{12}-\frac{1}{2}\ln^2(2)$, a detailed calculation yields $\text{Li}_2(2) = \frac{\pi^2}{4} - i\pi\ln(2)$.

Now we assemble the L-functions:
$$
L(-1) = \text{Li}_2(-1) + \frac{1}{2}\ln(-1)\ln(1-(-1)) = -\frac{\pi^2}{12} + \frac{1}{2}(i\pi)\ln(2)
$$
$$
L(2) = \text{Li}_2(2) + \frac{1}{2}\ln(2)\ln(1-2) = \left(\frac{\pi^2}{4} - i\pi\ln(2)\right) + \frac{1}{2}\ln(2)(i\pi) = \frac{\pi^2}{4} - \frac{i\pi}{2}\ln(2)
$$
Summing these two expressions:
$$
L(-1) + L(2) = \left(-\frac{\pi^2}{12} + \frac{\pi^2}{4}\right) + i\left(\frac{\pi}{2}\ln(2) - \frac{\pi}{2}\ln(2)\right) = \frac{2\pi^2}{12} = \frac{\pi^2}{6}
$$
Remarkably, the imaginary parts cancel perfectly, and the real part of the sum is still $\pi^2/6$. This demonstrates how the identities persist in the complex plane, provided the multi-valued nature of the logarithm is handled with care.

### Advanced Applications: Chaining Identities

The true mastery of the [dilogarithm](@entry_id:202722) comes from the ability to combine these [functional equations](@entry_id:199663) strategically, forming a "chain" of transformations to relate seemingly disparate arguments. Such calculations highlight the intricate and beautiful web of relationships that the identities encode.

As a capstone illustration, let us compute the value of the combination $\text{Li}_2(-3) + \text{Li}_2(3/4)$ [@problem_id:771588]. There is no single identity that connects these two arguments. Instead, we must construct a path using multiple steps:

1.  The argument $-3$ is outside the unit circle. Our first step is to use the **inversion formula** with $z=-3$ to relate it to $\text{Li}_2(-1/3)$:
    $$ \text{Li}_2(-3) + \text{Li}_2(-1/3) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(3) \quad (1)$$

2.  Now we have terms with arguments $-1/3$ and $3/4$. We can attempt to relate them. Let's subtract the value of $\text{Li}_2(-1/3)$ from $\text{Li}_2(3/4)$. We can create a path from $-1/3$ to $3/4$ via the argument $4/3$. First, use the **[reflection formula](@entry_id:198841)** for $z'=-1/3$:
    $$ \text{Li}_2(-1/3) + \text{Li}_2(4/3) = \frac{\pi^2}{6} - \ln(-1/3)\ln(4/3) \quad (2)$$
    Next, use the **inversion formula** for $z''=4/3$:
    $$ \text{Li}_2(4/3) + \text{Li}_2(3/4) = -\frac{\pi^2}{6} - \frac{1}{2}\ln^2(-4/3) \quad (3)$$

3.  We can now find an expression for $\text{Li}_2(3/4) - \text{Li}_2(-1/3)$ by subtracting equation (2) from equation (3):
    $$ (\text{Li}_2(4/3) + \text{Li}_2(3/4)) - (\text{Li}_2(-1/3) + \text{Li}_2(4/3)) = \left(-\frac{\pi^2}{6} - \frac{1}{2}\ln^2(-4/3)\right) - \left(\frac{\pi^2}{6} - \ln(-1/3)\ln(4/3)\right) $$
    $$ \text{Li}_2(3/4) - \text{Li}_2(-1/3) = -\frac{\pi^2}{3} - \frac{1}{2}\ln^2(-4/3) + \ln(-1/3)\ln(4/3) \quad (4)$$

4.  The final step is to evaluate the logarithmic terms and combine the results. Let the target sum be $S = \text{Li}_2(-3) + \text{Li}_2(3/4)$. From (1), we can write $\text{Li}_2(-3) = -\text{Li}_2(-1/3) - \frac{\pi^2}{6} - \frac{1}{2}\ln^2(3)$. Therefore,
    $$ S = (\text{Li}_2(3/4) - \text{Li}_2(-1/3)) - \frac{\pi^2}{6} - \frac{1}{2}\ln^2(3) $$
    Substituting our expression (4) for the difference:
    $$ S = \left( -\frac{\pi^2}{3} - \frac{1}{2}\ln^2(-4/3) + \ln(-1/3)\ln(4/3) \right) - \frac{\pi^2}{6} - \frac{1}{2}\ln^2(3) $$
    Using the [principal branch](@entry_id:164844) logarithms $\ln(-x) = \ln(x) + i\pi$ for $x>0$:
    $$ S = -\frac{\pi^2}{3} - \frac{1}{2}(\ln(4/3)+i\pi)^2 + (\ln(1/3)+i\pi)\ln(4/3) - \frac{\pi^2}{6} - \frac{1}{2}\ln^2(3) $$
    Expanding and collecting the real part (the imaginary parts can be shown to cancel):
    $$ \Re(S) = -\frac{\pi^2}{3} - \frac{1}{2}(\ln^2(4/3)-\pi^2) - \ln(3)\ln(4/3) - \frac{\pi^2}{6} - \frac{1}{2}\ln^2(3) $$
    The $\pi^2$ terms sum to $-\frac{\pi^2}{3} + \frac{\pi^2}{2} - \frac{\pi^2}{6} = 0$. The remaining logarithmic terms are:
    $$ S = -\frac{1}{2}\ln^2(4/3) - \ln(3)\ln(4/3) - \frac{1}{2}\ln^2(3) = -\frac{1}{2}\left[ \ln^2(4/3) + 2\ln(3)\ln(4/3) + \ln^2(3) \right] $$
    This is a [perfect square](@entry_id:635622):
    $$ S = -\frac{1}{2}\left[ \ln(4/3) + \ln(3) \right]^2 = -\frac{1}{2}\left[ \ln(4/3 \cdot 3) \right]^2 = -\frac{1}{2}[\ln(4)]^2 = -\frac{1}{2}(2\ln(2))^2 = -2\ln^2(2) $$
This calculation, while intricate, showcases the deep structural coherence of the [dilogarithm function](@entry_id:181405). The seemingly arbitrary [functional equations](@entry_id:199663) are precisely the tools needed to simplify complex expressions into elegant, closed-form results.