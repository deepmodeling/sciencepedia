## Introduction
Power series represent a fundamental bridge between the algebraic world of infinite sums and the analytic world of calculus. In complex analysis, they provide the means to represent [analytic functions](@entry_id:139584), encoding their intricate properties within a sequence of coefficients. However, a key question arises: how do the fundamental operations of calculus, differentiation and integration, interact with these infinite structures? This article addresses this question, demonstrating that the relationship is remarkably straightforward and powerful. It provides the theoretical justification and practical methodology for applying calculus to power series, transforming complex analytical problems into more manageable algebraic manipulations.

Across the following chapters, you will gain a comprehensive understanding of this essential technique. The journey begins in **Principles and Mechanisms**, which lays the theoretical groundwork for term-by-term differentiation and integration, establishing the core rules and proving the crucial invariance of the radius of convergence. Next, **Applications and Interdisciplinary Connections** showcases the immense utility of these methods, exploring how they are used to solve differential equations, evaluate integrals, and serve as a foundation for the theory of generating functions in fields like probability and number theory. Finally, **Hands-On Practices** will offer opportunities to apply and solidify your understanding through targeted exercises, building your proficiency with this indispensable tool of mathematical analysis.

## Principles and Mechanisms

A [power series](@entry_id:146836) is not merely a formal sequence of terms; within its [disk of convergence](@entry_id:177284), it defines an analytic function, inheriting the rich properties of [differentiability](@entry_id:140863) and integrability. The profound connection between the algebraic structure of a series and the analytic properties of the function it represents is governed by a set of powerful yet elegant principles. This chapter elucidates these principles, focusing on how the fundamental operations of calculus—differentiation and integration—can be applied directly to power series representations.

### The Calculus of Power Series: Term-by-Term Operations

The central principle that unlocks the calculus of [power series](@entry_id:146836) is that both [differentiation and integration](@entry_id:141565) can be performed **term-by-term**. This remarkable property states that to find the series for the derivative of a function, one can simply differentiate its [power series](@entry_id:146836) term by term, as if it were a finite polynomial. The same holds for integration.

Let a function $f(z)$ be defined by a power series centered at $z_0$ with a non-zero radius of convergence $R$:
$$f(z) = \sum_{n=0}^{\infty} a_n (z-z_0)^n, \quad \text{for } |z-z_0|  R$$
This series converges to an [analytic function](@entry_id:143459) inside this disk. The derivative, $f'(z)$, is also analytic in the same disk and its [power series](@entry_id:146836) is given by:
$$f'(z) = \frac{d}{dz} \left( \sum_{n=0}^{\infty} a_n (z-z_0)^n \right) = \sum_{n=1}^{\infty} n a_n (z-z_0)^{n-1}$$
Notice that the summation now naturally starts from $n=1$, as the derivative of the constant term $a_0$ is zero.

Similarly, we can find an [antiderivative](@entry_id:140521) of $f(z)$ by integrating the series term-by-term. If $F(z)$ is an [antiderivative](@entry_id:140521) of $f(z)$, so that $F'(z) = f(z)$, its [series representation](@entry_id:175860) is:
$$F(z) = \int f(z) dz = C + \sum_{n=0}^{\infty} \frac{a_n}{n+1} (z-z_0)^{n+1}$$
where $C$ is the constant of integration. Typically, we define a unique antiderivative by imposing an initial condition, such as $F(z_0)=0$. This condition forces $C=0$, yielding the [definite integral](@entry_id:142493) form:
$$F(z) = \int_{z_0}^z f(w) dw = \sum_{n=0}^{\infty} \frac{a_n}{n+1} (z-z_0)^{n+1}$$

To see this mechanism in action, consider a function $f(z) = \sum_{n=0}^{\infty} a_n z^n$ where the coefficients are $a_n = \frac{2n+5}{n!}$. Let us find the fourth coefficient, $b_4$, of the [power series](@entry_id:146836) for its [antiderivative](@entry_id:140521) $F(z) = \int_0^z f(w) dw = \sum_{k=0}^{\infty} b_k z^k$. Applying the [term-by-term integration](@entry_id:138696) rule, we have:
$$F(z) = \sum_{n=0}^{\infty} \frac{a_n}{n+1} z^{n+1} = \sum_{n=0}^{\infty} \frac{2n+5}{n!(n+1)} z^{n+1} = \sum_{n=0}^{\infty} \frac{2n+5}{(n+1)!} z^{n+1}$$
To identify the coefficients $b_k$, we re-index the summation by setting $k = n+1$. Thus, $n = k-1$ and the sum begins at $k=1$:
$$F(z) = \sum_{k=1}^{\infty} \frac{2(k-1)+5}{k!} z^k = \sum_{k=1}^{\infty} \frac{2k+3}{k!} z^k$$
The coefficients of the series for $F(z)$ are therefore $b_0=0$ (consistent with $F(0)=0$) and $b_k = \frac{2k+3}{k!}$ for $k \ge 1$. For the specific coefficient $b_4$, we substitute $k=4$:
$$b_4 = \frac{2(4)+3}{4!} = \frac{11}{24}$$
This calculation [@problem_id:2247155] directly illustrates the mechanical relationship between the coefficients of a function's series and that of its antiderivative.

### Invariance of the Radius of Convergence

A crucial question arises: what happens to the radius of convergence when we differentiate or integrate a power series? The coefficients are altered—multiplied by $n$ for differentiation and divided by $n+1$ for integration. One might worry that this could change the convergence properties. Remarkably, it does not.

**Theorem:** If the [power series](@entry_id:146836) $\sum a_n (z-z_0)^n$ has a radius of convergence $R$, then the series obtained by term-by-term [differentiation and integration](@entry_id:141565),
$$\sum_{n=1}^{\infty} n a_n (z-z_0)^{n-1} \quad \text{and} \quad \sum_{n=0}^{\infty} \frac{a_n}{n+1} (z-z_0)^{n+1}$$
also have the same radius of convergence $R$.

The intuitive reason lies in the asymptotic behavior of the factors $n$ and $n+1$. The [radius of convergence](@entry_id:143138) is determined by the large-$n$ behavior of $|a_n|^{1/n}$. The new coefficients are $n a_n$ and $a_n/(n+1)$. According to the [root test](@entry_id:138735), the new radius would depend on $\lim_{n \to \infty} |n a_n|^{1/n}$ and $\lim_{n \to \infty} |a_n/(n+1)|^{1/n}$. Since $\lim_{n \to \infty} n^{1/n} = 1$ and $\lim_{n \to \infty} (n+1)^{-1/n} = 1$, the asymptotic behavior is unchanged, and the [radius of convergence](@entry_id:143138) remains the same.

For example, consider a series $S(z) = \sum_{n=2}^{\infty} \frac{n(n-1)}{k^n} z^{n-2}$ for some real constant $k \neq 0$. This series can be recognized as the second derivative of the [geometric series](@entry_id:158490) $\sum_{n=0}^\infty (\frac{z}{k})^n$. The [geometric series](@entry_id:158490) converges for $|z/k|  1$, meaning its [radius of convergence](@entry_id:143138) is $|k|$. Our theorem predicts that its second derivative, $S(z)$, must also have a radius of convergence of $|k|$ [@problem_id:2247150].

This principle extends to combinations of series. If we have two functions $f(x) = \sum a_n x^n$ with radius of convergence $R_f=3$ and $g(x) = \sum b_n x^n$ with $R_g=5/2$, the series for their sum, $h(x) = f(x)+g(x)$, will converge only when both series converge. Therefore, the radius of convergence for $h(x)$ is $R_h = \min(R_f, R_g) = 5/2$. If we then consider the integral $H(x) = \int_0^x h(t) dt$, the theorem on invariance ensures that the [radius of convergence](@entry_id:143138) for the resulting [power series](@entry_id:146836) for $H(x)$ is also $5/2$ [@problem_id:2317645].

### Uniqueness of Representation and its Consequences

The ability to manipulate power series with calculus is fortified by the **Uniqueness Theorem for Power Series**. This theorem states that if a function can be represented by a [power series](@entry_id:146836) centered at $z_0$, that representation is unique. In other words, if $\sum a_n (z-z_0)^n = \sum b_n (z-z_0)^n$ for all $z$ in some open disk around $z_0$, then it must be that $a_n = b_n$ for all $n$. The coefficients are uniquely determined by the function's derivatives at the center point: $a_n = f^{(n)}(z_0)/n!$.

This uniqueness guarantees that the series we obtain by [term-by-term differentiation](@entry_id:142985) is not just *a* series for the derivative, but *the* Taylor series for the derivative. This principle provides the theoretical confidence behind many of our manipulations [@problem_id:2285631].

Consider two [analytic functions](@entry_id:139584), $f(z)$ and $g(z)$, on the [unit disk](@entry_id:172324). Suppose we know that $g(0)=0$ and that its derivative is given by the geometric series $g'(z) = \sum_{k=0}^{\infty} (-1)^k z^k$. We also know that the function $f(z) = \ln(1+z)$ has the [series representation](@entry_id:175860) $\sum_{n=1}^{\infty} \frac{(-1)^{n-1}}{n} z^n$. If we differentiate $f(z)$, we find $f'(z) = \frac{1}{1+z}$, whose series is precisely $\sum_{k=0}^{\infty} (-1)^k z^k$. So, we have $f'(z) = g'(z)$. Since their derivatives are identical, the functions $f(z)$ and $g(z)$ can only differ by a constant. But we are given that $f(0) = \ln(1) = 0$ and $g(0) = 0$. Since they agree at one point, the constant must be zero, and thus $f(z) = g(z)$ throughout the disk. By the [uniqueness of power series](@entry_id:139951), their coefficients must be identical. Therefore, the coefficients $b_n$ of $g(z)$ must be $b_n = \frac{(-1)^{n-1}}{n}$ for $n \ge 1$, and $b_0=0$ [@problem_id:2247146].

### A Toolkit for Series Manipulation

The true power of these principles is revealed when they are used as a toolkit to generate new series representations and to find the closed-form sums of unfamiliar series.

#### Generating New Series from Known Ones

We can begin with a small collection of known "base" series, such as the geometric, exponential, and trigonometric series, and derive a vast array of others.

The [geometric series](@entry_id:158490) is a particularly fertile starting point:
$$\frac{1}{1-z} = \sum_{n=0}^{\infty} z^n, \quad |z|  1$$
Differentiating term-by-term yields the series for its derivative:
$$\frac{1}{(1-z)^2} = \sum_{n=1}^{\infty} n z^{n-1} = \sum_{k=0}^{\infty} (k+1) z^k, \quad |z|  1$$
By substituting $-z$ for $z$ in the original [geometric series](@entry_id:158490), we get:
$$\frac{1}{1+z} = \sum_{n=0}^{\infty} (-z)^n = \sum_{n=0}^{\infty} (-1)^n z^n, \quad |z|  1$$
Integrating this series from $0$ to $z$ gives us the series for the [principal branch](@entry_id:164844) of the logarithm:
$$\ln(1+z) = \int_0^z \frac{1}{1+w} dw = \sum_{n=0}^{\infty} (-1)^n \int_0^z w^n dw = \sum_{n=0}^{\infty} \frac{(-1)^n}{n+1} z^{n+1}, \quad |z|  1$$
As a check of consistency, if we now differentiate the series for $\ln(1+z)$ term-by-term, we obtain $\sum_{n=0}^{\infty} (-1)^n z^n$, which is indeed the series for $\frac{1}{1+z}$. This circular journey confirms that differentiation and integration act as inverse operations on power series, just as they do on the functions they represent [@problem_id:2247181].

This method is broadly applicable. Knowing the series for $\cos(z) = \sum_{k=0}^{\infty} \frac{(-1)^k}{(2k)!} z^{2k}$, we can find a series for a related function like $g(z) = \frac{\cos(z)-1}{z}$. First, we manipulate the series for the numerator:
$$\cos(z) - 1 = \left(1 - \frac{z^2}{2!} + \frac{z^4}{4!} - \dots\right) - 1 = \sum_{k=1}^{\infty} \frac{(-1)^k}{(2k)!} z^{2k}$$
Then, for $z \neq 0$, we divide by $z$:
$$g(z) = \frac{\cos(z)-1}{z} = \sum_{k=1}^{\infty} \frac{(-1)^k}{(2k)!} z^{2k-1} = -\frac{z}{2!} + \frac{z^3}{4!} - \dots$$
This series defines an [entire function](@entry_id:178769) (it converges for all $z$). We can now differentiate it term-by-term to find the series for $g'(z)$ [@problem_id:2247180].

Similarly, the known relationship between [hyperbolic functions](@entry_id:165175), $\frac{d}{dz}\sinh(z) = \cosh(z)$, is beautifully reflected in their series. Starting with the series for $f(z) = \cosh(z) = \sum_{n=0}^{\infty} \frac{z^{2n}}{(2n)!}$, [term-by-term integration](@entry_id:138696) yields:
$$\int_0^z \cosh(w) dw = \sum_{n=0}^{\infty} \frac{1}{(2n)!} \int_0^z w^{2n} dw = \sum_{n=0}^{\infty} \frac{z^{2n+1}}{(2n+1)!}$$
We immediately recognize this as the Maclaurin series for $\sinh(z)$, providing a series-level confirmation of the calculus identity [@problem_id:2247137].

#### Finding Closed-Form Sums

The reverse process—identifying the closed-form function that a given series sums to—is a more creative art that relies on recognizing series as derivatives or integrals of simpler, known series.

Consider the problem of finding the sum of the series $f(z) = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n)!} (n+1) z^{2n}$. The key is to break the coefficient $(n+1)$ into more manageable parts: $n+1 = 1+n$. This allows us to split the series into two:
$$f(z) = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n)!} z^{2n} + \sum_{n=0}^{\infty} \frac{(-1)^n n}{(2n)!} z^{2n}$$
The first sum is immediately recognizable as the Maclaurin series for $\cos(z)$. The second sum is more challenging. Let's call it $S_2(z)$. Note the factor of $n$ in the numerator. This often hints at a derivative. Let's start with a known series whose derivative might produce terms like this. The series for $\sin(z)$ is $\sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)!} z^{2n+1}$. Let's see what happens when we manipulate it:
$$z \sin(z) = \sum_{n=0}^{\infty} \frac{(-1)^n}{(2n+1)!} z^{2n+2}$$
Now, differentiate with respect to $z$:
$$\frac{d}{dz} (z \sin(z)) = \sin(z) + z \cos(z) = \sum_{n=0}^{\infty} \frac{(-1)^n (2n+2)}{(2n+1)!} z^{2n+1}$$
This doesn't seem to lead directly to $S_2(z)$. Let's try a different manipulation. A more direct path involves relating the coefficients. Notice that $\frac{n}{(2n)!} = \frac{n}{2n(2n-1)!} = \frac{1}{2(2n-1)!}$ for $n \ge 1$. This suggests a connection to a series with $(2n-1)!$ in the denominator. Let's return to our target $S_2(z) = \sum_{n=1}^{\infty} \frac{(-1)^n n}{(2n)!} z^{2n}$ (the $n=0$ term is zero). Consider the series for $z\sin(z)$, but re-indexed.
Let's try to construct $S_2(z)$ from a known function. Perhaps differentiating $\sin(z)$ or $\cos(z)$ is involved.
Let's try to relate $S_2(z)$ to something involving $z$ times a derivative. Let's try differentiating $\cos(z)$:
$$\frac{d}{dz} \cos(z) = -\sin(z) = \sum_{n=1}^{\infty} \frac{(-1)^n (2n)}{(2n)!} z^{2n-1}$$
Multiplying by $z$ is a common trick:
$$-z\sin(z) = \sum_{n=1}^{\infty} \frac{(-1)^n (2n)}{(2n)!} z^{2n} = 2 \sum_{n=1}^{\infty} \frac{(-1)^n n}{(2n)!} z^{2n} = 2 S_2(z)$$
So, we have found that $S_2(z) = -\frac{z}{2}\sin(z)$.
Combining our two parts, the [closed form](@entry_id:271343) of the original series is:
$$f(z) = \cos(z) - \frac{z}{2}\sin(z)$$
This example [@problem_id:2247178] showcases how a combination of algebraic splitting and recognizing patterns related to differentiation can be used to evaluate [complex series](@entry_id:191035).

### Symmetry and Differentiation

Finally, [term-by-term differentiation](@entry_id:142985) provides a clear window into how functional symmetries, such as being even or odd, behave under differentiation.

An **even function** is one for which $f(-z) = f(z)$. Its Maclaurin series contains only even powers of $z$: $f(z) = \sum_{k=0}^{\infty} c_{2k} z^{2k}$. An **odd function** satisfies $g(-z) = -g(z)$ and its series contains only odd powers of $z$: $g(z) = \sum_{k=0}^{\infty} d_{2k+1} z^{2k+1}$.

What happens when we differentiate an even function $f(z)$? We can see this in two ways.
First, by differentiating the identity $f(-z) = f(z)$ using the chain rule, we get:
$$\frac{d}{dz} f(-z) = f'(-z) \cdot (-1) = -f'(-z)$$
$$\frac{d}{dz} f(z) = f'(z)$$
Since the original functions were equal, their derivatives must be equal: $f'(z) = -f'(-z)$. This is the definition of an odd function.

Second, we can see this at the series level. Differentiating the series for an even function gives:
$$f'(z) = \frac{d}{dz} \sum_{k=0}^{\infty} c_{2k} z^{2k} = \sum_{k=1}^{\infty} c_{2k} (2k) z^{2k-1}$$
The resulting series consists entirely of odd powers ($2k-1$), which is the [series representation](@entry_id:175860) of an [odd function](@entry_id:175940). Thus, the derivative of an even analytic function is always an odd function [@problem_id:2247167]. A similar argument shows that the derivative of an odd function is an [even function](@entry_id:164802). This interplay between symmetry and calculus is a recurring theme in analysis, and [power series](@entry_id:146836) provide a particularly transparent framework for understanding it.