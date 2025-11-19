## Introduction
The Gamma function, an extension of the factorial to the complex numbers, is a cornerstone of advanced analysis, defined by a rich network of identities that reveal deep mathematical structures. Among the most elegant and useful of these is the Legendre [duplication formula](@entry_id:173961), which establishes a precise relationship between the Gamma function at a value z, at z + 1/2, and at the doubled value 2z. This article aims to provide a thorough understanding of this powerful identity, bridging the gap between its abstract definition and its practical utility. In the following sections, we will first delve into the core **Principles and Mechanisms** of the formula, exploring its various proofs and verifying its consistency with the fundamental properties of the Gamma function. Subsequently, we will showcase its broad utility through a tour of its **Applications and Interdisciplinary Connections**, demonstrating how it simplifies calculations in fields ranging from combinatorics to theoretical physics. Finally, you will have the opportunity to solidify your understanding through a series of **Hands-On Practices** designed to build confidence and proficiency in applying the formula.

## Principles and Mechanisms

The Gamma function, $\Gamma(z)$, stands as a cornerstone of advanced analysis, extending the factorial concept to the complex plane. Its rich structure is described by a set of fundamental identities that reveal deep connections within mathematics. Among the most important of these is the **Legendre [duplication formula](@entry_id:173961)**, an elegant and powerful relation discovered by Adrien-Marie Legendre. This chapter elucidates the principles behind this formula, explores its various derivations, and demonstrates its consistency and application.

### The Legendre Duplication Formula: Statement and Significance

The Legendre [duplication formula](@entry_id:173961) establishes a precise relationship between the Gamma function evaluated at $z$, $z + \frac{1}{2}$, and $2z$. It is stated as follows:

$$ \Gamma(z) \Gamma\left(z + \frac{1}{2}\right) = 2^{1-2z} \sqrt{\pi} \Gamma(2z) $$

This identity holds for all complex numbers $z$ for which the Gamma functions are defined (i.e., $z$, $z+\frac{1}{2}$, and $2z$ are not zero or negative integers). The name "[duplication formula](@entry_id:173961)" arises from the presence of the $\Gamma(2z)$ term, which involves a doubling of the argument.

The formula's significance lies in its utility for both theoretical and practical purposes. It allows for the interconversion of Gamma functions with different arguments, which is invaluable in simplifying complex expressions and evaluating [definite integrals](@entry_id:147612). For instance, the formula can be readily rearranged to provide a compact expression for the ratio of $\Gamma(2z)$ to $\Gamma(z)$, a common requirement in series expansions and [asymptotic analysis](@entry_id:160416) [@problem_id:2250287]:

$$ \frac{\Gamma(2z)}{\Gamma(z)} = \frac{2^{2z-1}}{\sqrt{\pi}} \Gamma\left(z + \frac{1}{2}\right) $$

This rearranged form expresses $\Gamma(2z)$ not only in terms of $\Gamma(z)$ but also, more conveniently, in terms of $\Gamma(z + \frac{1}{2})$. Understanding the origins of this formula is key to appreciating its depth.

### Derivations of the Formula

The veracity of the Legendre [duplication formula](@entry_id:173961) can be established through several distinct mathematical routes. Each proof highlights a different facet of the Gamma function's character, drawing upon [integral calculus](@entry_id:146293), [functional analysis](@entry_id:146220), or [infinite product](@entry_id:173356) representations.

#### Derivation from the Beta Function Integral

A beautifully [direct proof](@entry_id:141172) of the [duplication formula](@entry_id:173961) emerges from the interplay between the Gamma function and the **Beta function**, $B(x,y)$. The Beta function is defined by its integral representation for $\Re(x) \gt 0$ and $\Re(y) \gt 0$:

$$ B(x,y) = \int_0^1 t^{x-1}(1-t)^{y-1} dt $$

It is linked to the Gamma function by the identity $B(x,y) = \frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)}$. The core of this proof lies in establishing an independent relationship between $B(z,z)$ and $B(z, \frac{1}{2})$ directly from their integral forms [@problem_id:2250283] [@problem_id:2250318].

Let's begin by considering the integral for $B(z,z)$:

$$ B(z,z) = \int_0^1 t^{z-1}(1-t)^{z-1} dt = \int_0^1 [t(1-t)]^{z-1} dt $$

We perform a trigonometric substitution $t = \sin^2\theta$. As $t$ ranges from $0$ to $1$, $\theta$ ranges from $0$ to $\frac{\pi}{2}$. The differential becomes $dt = 2\sin\theta\cos\theta \, d\theta$. The [integral transforms](@entry_id:186209) as follows:

$$ B(z,z) = \int_0^{\pi/2} [\sin^2\theta \cos^2\theta]^{z-1} (2\sin\theta\cos\theta) \, d\theta = 2 \int_0^{\pi/2} (\sin\theta\cos\theta)^{2z-1} d\theta $$

Using the double-angle identity $\sin(2\theta) = 2\sin\theta\cos\theta$, we get:

$$ B(z,z) = 2 \int_0^{\pi/2} \left(\frac{\sin(2\theta)}{2}\right)^{2z-1} d\theta = 2 \cdot 2^{1-2z} \int_0^{\pi/2} \sin^{2z-1}(2\theta) d\theta $$

Let $\phi = 2\theta$, so $d\theta = \frac{1}{2}d\phi$. The integration limits change from $[0, \pi/2]$ to $[0, \pi]$.

$$ B(z,z) = 2^{2-2z} \int_0^{\pi} \sin^{2z-1}(\phi) \frac{1}{2} d\phi = 2^{1-2z} \int_0^{\pi} \sin^{2z-1}(\phi) d\phi $$

Due to the symmetry of the sine function about $\phi = \pi/2$, we can write $\int_0^{\pi} \sin^{m}(\phi) d\phi = 2 \int_0^{\pi/2} \sin^{m}(\phi) d\phi$. Applying this gives:

$$ B(z,z) = 2^{1-2z} \cdot 2 \int_0^{\pi/2} \sin^{2z-1}(\phi) d\phi $$

Now, let's analyze $B(z, \frac{1}{2})$. Using the same substitution $t = \sin^2\theta$:

$$ B\left(z, \frac{1}{2}\right) = \int_0^1 t^{z-1}(1-t)^{-1/2} dt = \int_0^{\pi/2} (\sin^2\theta)^{z-1} (\cos^2\theta)^{-1/2} (2\sin\theta\cos\theta) d\theta $$
$$ B\left(z, \frac{1}{2}\right) = 2 \int_0^{\pi/2} \sin^{2z-2}\theta \cdot \frac{1}{\cos\theta} \cdot \sin\theta\cos\theta \, d\theta = 2 \int_0^{\pi/2} \sin^{2z-1}\theta \, d\theta $$

By comparing our expressions for $B(z,z)$ and $B(z, \frac{1}{2})$, we find the elegant relationship:

$$ B(z,z) = 2^{1-2z} B\left(z, \frac{1}{2}\right) $$

Finally, we translate this identity back into the language of Gamma functions:

$$ \frac{\Gamma(z)\Gamma(z)}{\Gamma(2z)} = 2^{1-2z} \frac{\Gamma(z)\Gamma(\frac{1}{2})}{\Gamma(z+\frac{1}{2})} $$

Assuming $\Gamma(z) \neq 0$, we can cancel one factor of $\Gamma(z)$ from both sides. Rearranging the terms and recalling the fundamental value $\Gamma(\frac{1}{2}) = \sqrt{\pi}$, we arrive at the Legendre [duplication formula](@entry_id:173961):

$$ \Gamma(z)\Gamma\left(z+\frac{1}{2}\right) = 2^{1-2z} \Gamma\left(\frac{1}{2}\right) \Gamma(2z) = 2^{1-2z} \sqrt{\pi} \Gamma(2z) $$
This derivation, initially valid for $\Re(z) > 0$, can be extended to the entire complex plane by the [principle of analytic continuation](@entry_id:187941).

#### Derivation from Functional Equations

An alternative and powerful method of proof relies on the principles of complex functions, particularly periodicity and [asymptotic behavior](@entry_id:160836) [@problem_id:2250322]. Let us define a function $H(z)$ as the ratio of the terms in the [duplication formula](@entry_id:173961):

$$ H(z) = \frac{\Gamma(z)\Gamma(z+1/2)}{\Gamma(2z)} $$

Our goal is to show that $H(z) = 2^{1-2z}\sqrt{\pi}$. We begin by finding a functional equation for $H(z)$. Let's examine $H(z+1/2)$:

$$ H\left(z+\frac{1}{2}\right) = \frac{\Gamma(z+1/2)\Gamma(z+1)}{\Gamma(2(z+1/2))} = \frac{\Gamma(z+1/2)\Gamma(z+1)}{\Gamma(2z+1)} $$

Using the fundamental recurrence relation $\Gamma(w+1) = w\Gamma(w)$, we substitute $\Gamma(z+1) = z\Gamma(z)$ and $\Gamma(2z+1) = 2z\Gamma(2z)$:

$$ H\left(z+\frac{1}{2}\right) = \frac{\Gamma(z+1/2) \cdot z\Gamma(z)}{2z\Gamma(2z)} = \frac{1}{2} \frac{\Gamma(z)\Gamma(z+1/2)}{\Gamma(2z)} = \frac{1}{2} H(z) $$

This gives us the simple recurrence $H(z+1/2) = \frac{1}{2} H(z)$. Now, let's define a new function $K(z) = \frac{2^{2z-1}}{\sqrt{\pi}}H(z)$. Let's see how it behaves under a shift of $1/2$:

$$ K\left(z+\frac{1}{2}\right) = \frac{2^{2(z+1/2)-1}}{\sqrt{\pi}} H\left(z+\frac{1}{2}\right) = \frac{2^{2z}}{\sqrt{\pi}} \left(\frac{1}{2}H(z)\right) = \frac{2^{2z-1}}{\sqrt{\pi}}H(z) = K(z) $$

This shows that $K(z)$ is a [periodic function](@entry_id:197949) with period $1/2$. As shown in the following section on [asymptotic consistency](@entry_id:176716), for large $z$, the ratio $H(z)$ has the [asymptotic behavior](@entry_id:160836) $H(z) \sim 2^{1-2z}\sqrt{\pi}$. Using this, we can find the asymptotic behavior of our periodic function $K(z)$:

$$ K(z) \sim \frac{2^{2z-1}}{\sqrt{\pi}} \left(2^{1-2z}\sqrt{\pi}\right) = \frac{2^{2z-1}}{2^{2z-1}} \cdot \frac{\sqrt{\pi}}{\sqrt{\pi}} = 1 $$

A periodic analytic function that tends to a constant (in this case, 1) as its argument goes to infinity in a strip must be that constant everywhere. Thus, $K(z) = 1$ for all $z$. From our definition of $K(z)$, this means:

$$ \frac{2^{2z-1}}{\sqrt{\pi}}H(z) = 1 \implies H(z) = \frac{\sqrt{\pi}}{2^{2z-1}} = 2^{1-2z}\sqrt{\pi} $$

Substituting the definition of $H(z)$ back in gives the Legendre [duplication formula](@entry_id:173961). This functional approach, while more abstract, powerfully demonstrates how the deep structural properties of the Gamma function (its recurrence and asymptotic behavior) are sufficient to determine the [duplication formula](@entry_id:173961) completely.

### Consistency and Verification

A hallmark of a fundamental mathematical identity is its consistency across different domains and with other known properties. The Legendre [duplication formula](@entry_id:173961) stands up to such scrutiny, whether tested at specific points, at its poles, or at infinity.

#### Verification at Specific Points

We can build confidence in the formula by testing it with simple values for $z$ where the Gamma function values are known [@problem_id:2250327] [@problem_id:2250313]. We use the facts that $\Gamma(n)=(n-1)!$ for positive integers $n$, $\Gamma(z+1)=z\Gamma(z)$, and $\Gamma(1/2)=\sqrt{\pi}$.

Let's test $z=1$:
-   Left-Hand Side (LHS): $\Gamma(1)\Gamma(1+1/2) = \Gamma(1)\Gamma(3/2) = 1 \cdot (\frac{1}{2}\Gamma(1/2)) = \frac{\sqrt{\pi}}{2}$.
-   Right-Hand Side (RHS): $2^{1-2(1)}\sqrt{\pi}\Gamma(2(1)) = 2^{-1}\sqrt{\pi}\Gamma(2) = \frac{\sqrt{\pi}}{2} \cdot 1! = \frac{\sqrt{\pi}}{2}$.
The sides match.

Let's test $z=3/2$:
-   LHS: $\Gamma(3/2)\Gamma(3/2+1/2) = \Gamma(3/2)\Gamma(2) = (\frac{1}{2}\Gamma(1/2)) \cdot 1! = \frac{\sqrt{\pi}}{2}$.
-   RHS: $2^{1-2(3/2)}\sqrt{\pi}\Gamma(2(3/2)) = 2^{-2}\sqrt{\pi}\Gamma(3) = \frac{\sqrt{\pi}}{4} \cdot 2! = \frac{\sqrt{\pi}}{4} \cdot 2 = \frac{\sqrt{\pi}}{2}$.
Again, the sides match perfectly. These checks confirm that the formula correctly links the values of the Gamma function at integer and half-integer arguments.

#### Consistency with Analytic Structure: Pole Analysis

A robust identity in complex analysis must respect the analytic structure of the functions involved, particularly the location and character of their singularities. The Gamma function $\Gamma(z)$ has [simple poles](@entry_id:175768) at all non-positive integers ($z=0, -1, -2, \dots$). The [duplication formula](@entry_id:173961) must ensure that the poles on both sides of the equation coincide perfectly.

Let's examine the behavior near $z=-1/2$, where the formula presents a non-trivial interplay of poles [@problem_id:2250290].
-   On the LHS, $\Gamma(z)\Gamma(z+1/2)$, the term $\Gamma(z) = \Gamma(-1/2)$ is analytic and finite, but the term $\Gamma(z+1/2)$ approaches $\Gamma(0)$, which has a simple pole. The residue of $\Gamma(w)$ at a simple pole $w=-n$ is $\frac{(-1)^n}{n!}$. For $w=0$ ($n=0$), the residue is $1$. Therefore, near $z=-1/2$, the LHS behaves like $\Gamma(-1/2) \cdot \frac{1}{z+1/2}$. The residue of the LHS at $z=-1/2$ is thus $\Gamma(-1/2)$. Using the recurrence, $\Gamma(1/2) = (-1/2)\Gamma(-1/2)$, so $\Gamma(-1/2) = -2\Gamma(1/2) = -2\sqrt{\pi}$.

-   On the RHS, $2^{1-2z}\sqrt{\pi}\Gamma(2z)$, the term $2^{1-2z}\sqrt{\pi}$ is analytic at $z=-1/2$. The singularity comes from $\Gamma(2z)$, which approaches $\Gamma(-1)$. The function $\Gamma(w)$ has a [simple pole](@entry_id:164416) at $w=-1$ with residue $\frac{(-1)^1}{1!} = -1$. To find the residue of $\Gamma(2z)$ at $z=-1/2$, we note that if $f(w)$ has a residue $r$ at $w_0$, then $g(z) = f(az)$ has a residue $r/a$ at $z_0 = w_0/a$. Here, the residue of $\Gamma(2z)$ at $z=-1/2$ is $\frac{\text{Res}(\Gamma, -1)}{2} = -1/2$.
The residue of the entire RHS is the value of the analytic part multiplied by the residue of the singular part:
$$ \text{Res}(\text{RHS}, -1/2) = \left(2^{1-2(-1/2)}\sqrt{\pi}\right) \cdot \text{Res}(\Gamma(2z), -1/2) = (2^2\sqrt{\pi}) \cdot \left(-\frac{1}{2}\right) = -2\sqrt{\pi} $$

The residues of both sides are identical. This remarkable consistency confirms that the [duplication formula](@entry_id:173961) correctly encodes the intricate pole structure of the Gamma function across the complex plane.

#### Consistency at Infinity: Asymptotic Behavior

Just as the formula holds for specific points and poles, it must also be consistent in the limit of large arguments. This can be verified using **Stirling's approximation** for the Gamma function, which for large positive real $z$ is given by:
$$ \Gamma(z) \sim \sqrt{2\pi} z^{z-1/2} \exp(-z) $$
We can check if the asymptotic forms of the LHS and RHS of the [duplication formula](@entry_id:173961) match [@problem_id:2250286].

-   Asymptotic form of the LHS, $L(z) = \Gamma(z)\Gamma(z+1/2)$:
$$ L(z) \sim (\sqrt{2\pi}z^{z-1/2}e^{-z}) \cdot (\sqrt{2\pi}(z+1/2)^{z}e^{-(z+1/2)}) = 2\pi e^{-1/2} z^{z-1/2} (z+1/2)^{z} e^{-2z} $$
Using the approximation $(z+1/2)^z = z^z(1+\frac{1}{2z})^z \sim z^z e^{1/2}$, we have:
$$ L(z) \sim 2\pi e^{-1/2} z^{z-1/2} (z^z e^{1/2}) e^{-2z} = 2\pi z^{2z-1/2}e^{-2z} $$

-   Asymptotic form of the RHS, $R(z) = 2^{1-2z}\sqrt{\pi}\Gamma(2z)$:
$$ R(z) \sim 2^{1-2z}\sqrt{\pi} \cdot (\sqrt{2\pi}(2z)^{2z-1/2}e^{-2z}) = 2^{1-2z}\sqrt{2}\pi \cdot 2^{2z-1/2}z^{2z-1/2} e^{-2z} $$
$$ R(z) \sim (2^{1-2z+2z-1/2})\sqrt{2}\pi z^{2z-1/2} e^{-2z} = 2^{1/2}\sqrt{2}\pi z^{2z-1/2}e^{-2z} = 2\pi z^{2z-1/2}e^{-2z} $$

The asymptotic behaviors of both sides match perfectly. To be more formal, we can examine their ratio:
$$ \frac{L(z)}{R(z)} \sim \frac{2\pi e^{-1/2} e^{-2z} z^{z-1/2} (z+1/2)^z}{2\pi z^{2z-1/2} e^{-2z}} = e^{-1/2} \frac{(z+1/2)^z}{z^z} = e^{-1/2} \left(1+\frac{1}{2z}\right)^z $$
We know that the limit of $(1+a/z)^z$ as $z \to \infty$ is $e^a$. Therefore:
$$ \lim_{z \to \infty} \frac{L(z)}{R(z)} = e^{-1/2} \cdot \lim_{z \to \infty} \left(1+\frac{1}{2z}\right)^z = e^{-1/2} \cdot e^{1/2} = 1 $$
The asymptotic behaviors of both sides match perfectly, confirming that the Legendre [duplication formula](@entry_id:173961) is consistent even in the limit of infinitely large arguments.

### Applications of the Duplication Formula

Beyond its theoretical importance, the Legendre [duplication formula](@entry_id:173961) is a workhorse in practical calculations involving special functions. It often serves as a key step in simplifying expressions that appear intractable at first glance. A prime example is the evaluation of products and ratios of Gamma functions at rational arguments.

Consider the task of finding a [closed-form expression](@entry_id:267458) for the constant $K = \frac{\Gamma(1/3)\Gamma(5/6)}{\Gamma(2/3)}$ [@problem_id:2250311]. This expression involves arguments that are not immediately related. The solution requires a clever combination of the [duplication formula](@entry_id:173961) and another fundamental identity, **Euler's [reflection formula](@entry_id:198841)**: $\Gamma(z)\Gamma(1-z) = \frac{\pi}{\sin(\pi z)}$.

1.  **Apply the Reflection Formula:** The term $\Gamma(5/6)$ can be related to $\Gamma(1-5/6) = \Gamma(1/6)$. With $z=1/6$, the [reflection formula](@entry_id:198841) gives:
    $$ \Gamma(1/6)\Gamma(5/6) = \frac{\pi}{\sin(\pi/6)} = \frac{\pi}{1/2} = 2\pi $$
    So, $\Gamma(5/6) = \frac{2\pi}{\Gamma(1/6)}$. Substituting this into the expression for $K$:
    $$ K = \frac{\Gamma(1/3)}{\Gamma(2/3)} \cdot \frac{2\pi}{\Gamma(1/6)} = \frac{2\pi \Gamma(1/3)}{\Gamma(2/3)\Gamma(1/6)} $$

2.  **Apply the Duplication Formula:** The denominator now contains $\Gamma(1/6)$ and $\Gamma(2/3)$. We can observe that $2/3 = 1/6 + 1/2$. This structure suggests using the [duplication formula](@entry_id:173961) with $z=1/6$:
    $$ \Gamma(1/6)\Gamma(1/6+1/2) = 2^{1-2(1/6)}\sqrt{\pi}\Gamma(2(1/6)) $$
    $$ \Gamma(1/6)\Gamma(2/3) = 2^{1-1/3}\sqrt{\pi}\Gamma(1/3) = 2^{2/3}\sqrt{\pi}\Gamma(1/3) $$
    This provides a direct link between the terms in the denominator and the term in the numerator.

3.  **Substitute and Simplify:** We can now substitute the result from step 2 into our expression for $K$:
    $$ K = \frac{2\pi \Gamma(1/3)}{2^{2/3}\sqrt{\pi}\Gamma(1/3)} = \frac{2\pi}{2^{2/3}\sqrt{\pi}} = 2^{1-2/3}\pi^{1-1/2} = 2^{1/3}\sqrt{\pi} $$
This example demonstrates the formula's power. By transforming arguments, it reveals hidden relationships, allowing for dramatic simplification and exact evaluation of complex-looking constants. The Legendre [duplication formula](@entry_id:173961), proven through multiple avenues and verified against the core properties of the Gamma function, is an indispensable tool in the analyst's repertoire.

Finally, we can also use the Weierstrass product representation for the Gamma function to prove the [duplication formula](@entry_id:173961). By substituting the [infinite product](@entry_id:173356) form for $\Gamma(z)$, $\Gamma(z+1/2)$, and $\Gamma(2z)$ into the formula, one can show through careful manipulation of the product terms that all dependence on $z$ cancels out, leaving only the constant pre-factors [@problem_id:2250297]. This advanced proof confirms that the formula is a deep consequence of the very definition of the Gamma function as an infinite product, tying together the integral, functional, and product-based perspectives on this remarkable function.