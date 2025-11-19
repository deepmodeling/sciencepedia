## Introduction
The Dedekind eta function, η(τ), stands as a central object in the landscape of [special functions](@entry_id:143234), weaving together complex analysis, number theory, and modern physics. At first glance, it is a simple [infinite product](@entry_id:173356) defined on the complex upper half-plane. However, its true significance is revealed through its intricate and elegant behavior under [modular transformations](@entry_id:184910). Understanding these properties is the key to unlocking its power, yet the underlying mechanisms and the sheer breadth of its applications can appear disparate and complex. This article aims to demystify the eta function by providing a structured journey through its theoretical foundations and its most significant roles across science.

This exploration is divided into three comprehensive chapters. First, in **"Principles and Mechanisms,"** we will dissect the function's core properties, from its q-[series expansion](@entry_id:142878) to its transformation laws under the [modular group](@entry_id:146452), introducing the crucial concepts of multiplier systems and Dedekind sums. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the remarkable utility of these principles, showing how the eta function provides solutions and insights in fields as varied as the theory of [integer partitions](@entry_id:139302), the geometry of [elliptic curves](@entry_id:152409), string theory, and the "Monstrous Moonshine" conjectures. Finally, the **"Hands-On Practices"** section offers a set of targeted problems, allowing readers to engage directly with the material and solidify their understanding of the calculations and concepts discussed. By the end of this article, the reader will have a robust framework for appreciating the Dedekind eta function not just as a mathematical formula, but as a powerful and unifying tool in the mathematical sciences.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the Dedekind eta function. We begin with its definition and its representation as both an infinite product and a series. We then explore its central feature: the elegant and intricate transformation properties under the action of the [modular group](@entry_id:146452), which form the bedrock of its utility in number theory, complex analysis, and modern physics.

### The Dedekind Eta Function: Definition and q-Expansion

The **Dedekind eta function**, denoted $\eta(\tau)$, is a [holomorphic function](@entry_id:164375) defined on the complex [upper half-plane](@entry_id:199119), $\mathbb{H} = \{ \tau \in \mathbb{C} \mid \text{Im}(\tau) > 0 \}$. Its [canonical representation](@entry_id:146693) is an [infinite product](@entry_id:173356), given by:
$$ \eta(\tau) = q^{1/24} \prod_{n=1}^{\infty} (1 - q^n) $$
Here, $q$ is the **nome**, defined as $q = \exp(2\pi i \tau)$. Since $|\exp(2\pi i \tau)| = \exp(-2\pi \, \text{Im}(\tau))$, the condition $\text{Im}(\tau) > 0$ ensures that $|q|  1$, which guarantees the absolute and [uniform convergence](@entry_id:146084) of the [infinite product](@entry_id:173356) on any compact subset of $\mathbb{H}$. This convergence ensures that $\eta(\tau)$ is a well-defined [holomorphic function](@entry_id:164375). Furthermore, since each term $(1-q^n)$ is non-zero for $\tau \in \mathbb{H}$, the eta function itself is non-zero throughout the upper half-plane.

The product part of the eta function, $\prod_{n=1}^{\infty} (1 - q^n)$, is often denoted as Euler's function, $\phi(q)$. A remarkable result established by Leonhard Euler, known as the **Pentagonal Number Theorem**, provides the series expansion for this product:
$$ \phi(q) = \prod_{n=1}^{\infty} (1 - q^n) = \sum_{k=-\infty}^{\infty} (-1)^k q^{k(3k-1)/2} $$
The exponents $n_k = k(3k-1)/2$ for $k \in \mathbb{Z}$ are known as the generalized **pentagonal numbers**. This identity connects the product definition of $\eta(\tau)$ to a sparsely populated [power series](@entry_id:146836), which is exceptionally useful for computational purposes.

To illustrate the practical use of this [series representation](@entry_id:175860), consider the function $F(\tau) = \eta(\tau)^3$. This function plays a significant role in the theory of modular forms and is related to the Jacobi [theta functions](@entry_id:202912). Its $q$-expansion can be written as $F(\tau) = q^{1/8} \sum_{n=0}^{\infty} a_n q^n$. Let us compute the coefficient $a_{10}$ [@problem_id:650896].
First, we express $F(\tau)$ using Euler's function:
$$ F(\tau) = \eta(\tau)^3 = \left( q^{1/24} \phi(q) \right)^3 = q^{1/8} \phi(q)^3 $$
The coefficient $a_{10}$ is the coefficient of $q^{10}$ in the series expansion of $\phi(q)^3$. The pentagonal numbers are $0, 1, 2, 5, 7, 12, \dots$. The series for $\phi(q)$ is therefore:
$$ \phi(q) = 1 - q - q^2 + q^5 + q^7 - q^{12} - \dots $$
To find the coefficient of $q^{10}$ in $\phi(q)^3$, we need to find combinations of three terms from this series whose exponents sum to 10. Let the expansion be $\phi(q) = \sum b_m q^m$. We seek the coefficient of $q^{10}$ in $(\sum b_m q^m)^3$, which is $\sum_{i+j+k=10} b_i b_j b_k$. The non-zero coefficients up to this order are $b_0=1, b_1=-1, b_2=-1, b_5=1, b_7=1$.
The possible partitions of 10 into these exponents are:
1.  $\{7, 2, 1\}$: The corresponding coefficients are $b_7=1, b_2=-1, b_1=-1$. There are $3! = 6$ [permutations](@entry_id:147130) of these distinct indices, so the contribution is $6 \times (1)(-1)(-1) = 6$.
2.  $\{5, 5, 0\}$: The coefficients are $b_5=1, b_5=1, b_0=1$. There are $\frac{3!}{2!1!} = 3$ permutations of this multiset, giving a contribution of $3 \times (1)(1)(1) = 3$.
Summing these contributions, we find that the coefficient of $q^{10}$ in $\phi(q)^3$ is $6+3=9$. Thus, $a_{10} = 9$.

### The Modular Group and Fundamental Transformations

The true power of the eta function is revealed through its behavior under transformations by the **[modular group](@entry_id:146452)**, $SL(2, \mathbb{Z})$. This is the group of $2 \times 2$ matrices with integer entries and determinant 1:
$$ SL(2, \mathbb{Z}) = \left\{ \gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \mid a,b,c,d \in \mathbb{Z}, ad-bc=1 \right\} $$
This group acts on the [upper half-plane](@entry_id:199119) $\mathbb{H}$ via **Möbius transformations** (or fractional linear transformations):
$$ \tau \mapsto \gamma\tau = \frac{a\tau+b}{c\tau+d} $$
The [modular group](@entry_id:146452) is generated by two fundamental transformations:
1.  **Translation**, $T = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$, which maps $\tau \mapsto \tau+1$.
2.  **Inversion**, $S = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$, which maps $\tau \mapsto -1/\tau$.

The Dedekind eta function transforms neatly under these generators. The transformation under $T$ follows directly from the definition. Since $q \to \exp(2\pi i (\tau+1)) = \exp(2\pi i)\exp(2\pi i \tau) = q$, the product term remains unchanged. The leading factor becomes $\exp(2\pi i (\tau+1)/24) = \exp(\pi i/12) \exp(\pi i \tau/12)$. This gives the **T-transformation law**:
$$ \eta(\tau+1) = e^{\pi i/12} \eta(\tau) $$

The transformation under $S$ is far more profound and non-obvious. It is given by the **S-transformation law**:
$$ \eta(-1/\tau) = \sqrt{-i\tau} \, \eta(\tau) $$
Here, $\sqrt{z}$ denotes the [principal branch](@entry_id:164844) of the square root, where the argument is taken in $(-\pi, \pi]$. This remarkable identity can be derived by relating $\eta(\tau)$ to the **Jacobi [theta functions](@entry_id:202912)** [@problem_id:650904]. The three fundamental [theta functions](@entry_id:202912) are defined as:
$$ \vartheta_2(\tau) = \sum_{n=-\infty}^{\infty} q^{(n+1/2)^2/2}, \quad \vartheta_3(\tau) = \sum_{n=-\infty}^{\infty} q^{n^2/2}, \quad \vartheta_4(\tau) = \sum_{n=-\infty}^{\infty} (-1)^n q^{n^2/2} $$
A deep result known as **Jacobi's identity** connects these functions to the eta function:
$$ \vartheta_2(\tau) \vartheta_3(\tau) \vartheta_4(\tau) = 2 \eta(\tau)^3 $$
The [theta functions](@entry_id:202912) have known S-transformations:
$$ \vartheta_2(-1/\tau) = \sqrt{-i\tau} \, \vartheta_4(\tau), \quad \vartheta_3(-1/\tau) = \sqrt{-i\tau} \, \vartheta_3(\tau), \quad \vartheta_4(-1/\tau) = \sqrt{-i\tau} \, \vartheta_2(\tau) $$
To derive the law for $\eta(\tau)$, we apply Jacobi's identity at $-1/\tau$:
$$ 2 \eta(-1/\tau)^3 = \vartheta_2(-1/\tau) \vartheta_3(-1/\tau) \vartheta_4(-1/\tau) $$
Substituting the transformation laws for the [theta functions](@entry_id:202912), we get:
$$ 2 \eta(-1/\tau)^3 = (\sqrt{-i\tau})^3 \vartheta_4(\tau) \vartheta_3(\tau) \vartheta_2(\tau) $$
Recognizing the product on the right as $2\eta(\tau)^3$ via Jacobi's identity, we have:
$$ 2 \eta(-1/\tau)^3 = (\sqrt{-i\tau})^3 (2 \eta(\tau)^3) $$
Canceling the common factor of 2 and taking the cube root of both sides yields the desired result: $\eta(-1/\tau) = \sqrt{-i\tau} \eta(\tau)$.

### The Multiplier System and the Cocycle Condition

The transformation properties under $S$ and $T$ can be extended to any element $\gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in SL(2, \mathbb{Z})$. The eta function is said to be a **[modular form](@entry_id:184897) of weight 1/2 with a multiplier system**. Its general transformation law is:
$$ \eta(\gamma\tau) = \epsilon(\gamma) (c\tau+d)^{1/2} \eta(\tau) $$
Here, $(c\tau+d)^{1/2}$ is the automorphy factor for weight $1/2$, and $\epsilon(\gamma)$ is a complex number of unit modulus, specifically a 24th root of unity, which depends on the matrix $\gamma$. This $\epsilon(\gamma)$ is the **multiplier**. The collection of these multipliers for all $\gamma \in SL(2, \mathbb{Z})$ is the **multiplier system**.

The multiplier system must satisfy a consistency relation known as the **[cocycle condition](@entry_id:262034)**. For any two transformations $\gamma_1, \gamma_2 \in SL(2, \mathbb{Z})$, applying them successively must be consistent with applying their product $\gamma_1\gamma_2$. Let $v_\eta(\gamma, \tau) = \epsilon(\gamma) (c\tau+d)^{1/2}$ be the full multiplier. Then $\eta(\gamma_1\gamma_2\tau) = v_\eta(\gamma_1\gamma_2, \tau)\eta(\tau)$. Alternatively, we can evaluate it step-by-step:
$$ \eta(\gamma_1(\gamma_2\tau)) = v_\eta(\gamma_1, \gamma_2\tau) \eta(\gamma_2\tau) = v_\eta(\gamma_1, \gamma_2\tau) v_\eta(\gamma_2, \tau) \eta(\tau) $$
This implies the [cocycle condition](@entry_id:262034): $v_\eta(\gamma_1\gamma_2, \tau) = v_\eta(\gamma_1, \gamma_2\tau) v_\eta(\gamma_2, \tau)$.

A powerful way to check this consistency is to use known relations between the generators. For instance, it is a fundamental fact that $(ST)^3 = -I$ in $SL(2, \mathbb{Z})$. The matrix $-I$ acts as the identity on $\mathbb{H}$, so $\eta((-I)\tau) = \eta(\tau)$. Let's verify that the multiplier for $(ST)^3$ is indeed 1 [@problem_id:886075]. We compute the transformation for $ST\tau = -1/(\tau+1)$:
$$ \eta(ST\tau) = \eta(S(\tau+1)) = \sqrt{-i(\tau+1)} \, \eta(\tau+1) = \sqrt{-i(\tau+1)} e^{\pi i/12} \eta(\tau) $$
Now we apply $ST$ again to the point $ST\tau$:
$$ \eta((ST)^2\tau) = \eta(ST(ST\tau)) = \sqrt{-i(ST\tau+1)} e^{\pi i/12} \eta(ST\tau) $$
Substituting $ST\tau = -1/(\tau+1)$ and the expression for $\eta(ST\tau)$:
$$ \eta((ST)^2\tau) = \sqrt{-i\left(-\frac{1}{\tau+1}+1\right)} e^{\pi i/12} \left(\sqrt{-i(\tau+1)} e^{\pi i/12} \eta(\tau)\right) = \sqrt{-i\frac{\tau}{\tau+1}} \sqrt{-i(\tau+1)} e^{2\pi i/12} \eta(\tau) $$
Applying $ST$ a third time to $(ST)^2\tau = \frac{-\tau-1}{\tau}$:
$$ \eta((ST)^3\tau) = \sqrt{-i((ST)^2\tau+1)} e^{\pi i/12} \eta((ST)^2\tau) $$
Substituting the expressions for $(ST)^2\tau$ and $\eta((ST)^2\tau)$:
$$ \eta((ST)^3\tau) = \sqrt{-i\left(\frac{-\tau-1}{\tau}+1\right)} e^{\pi i/12} \left(\sqrt{-i\frac{\tau}{\tau+1}} \sqrt{-i(\tau+1)} e^{2\pi i/12} \eta(\tau)\right) $$
Simplifying the terms:
$$ \eta((ST)^3\tau) = \sqrt{-i\frac{-1}{\tau}} \sqrt{-i\frac{\tau}{\tau+1}} \sqrt{-i(\tau+1)} e^{3\pi i/12} \eta(\tau) $$
The arguments of the square roots multiply to $(-i/\tau)( -i\tau/(\tau+1))(-i(\tau+1)) = -i$. Using the property $\sqrt{z_1}\sqrt{z_2} = \sqrt{z_1z_2}$ (which holds carefully for principal branches with $\tau \in \mathbb{H}$), the product of the square roots is $\sqrt{-i} = e^{-i\pi/4}$. The total multiplier is thus:
$$ \chi = e^{-\pi i/4} e^{3\pi i/12} = e^{-\pi i/4} e^{\pi i/4} = 1 $$
This confirms that $\eta((ST)^3\tau) = \eta(\tau)$, perfectly matching the group theory. This example not only confirms the consistency of the multiplier system but also showcases its predictive power [@problem_id:651006] [@problem_id:886075].

These transformation laws are also the foundation for understanding related functions. For example, the **Weber [modular functions](@entry_id:155728)** are defined as ratios of eta functions. Consider $\mathfrak{f}(\tau) = e^{-\pi i/24} \frac{\eta\left((\tau+1)/2\right)}{\eta(\tau)}$ and $\mathfrak{f}_1(\tau) = \frac{\eta\left(\tau/2\right)}{\eta(\tau)}$. The transformation of these functions under modular maps can be deduced directly from the eta transformations. As a simple exercise, let's examine the ratio $C(\tau) = \frac{\mathfrak{f}(\tau+1)}{\mathfrak{f}_1(\tau)}$ [@problem_id:651037].
$$ \mathfrak{f}(\tau+1) = e^{-\pi i/24} \frac{\eta\left(\frac{(\tau+1)+1}{2}\right)}{\eta(\tau+1)} = e^{-\pi i/24} \frac{\eta\left(\frac{\tau}{2}+1\right)}{\eta(\tau+1)} $$
Using $\eta(z+1) = e^{\pi i/12}\eta(z)$, we get:
$$ \mathfrak{f}(\tau+1) = e^{-\pi i/24} \frac{e^{\pi i/12}\eta(\tau/2)}{e^{\pi i/12}\eta(\tau)} = e^{-\pi i/24} \frac{\eta(\tau/2)}{\eta(\tau)} = e^{-\pi i/24} \mathfrak{f}_1(\tau) $$
Therefore, the ratio $C(\tau)$ is the constant $e^{-\pi i/24}$.

### Dedekind Sums and the Explicit Multiplier Formula

While the [cocycle condition](@entry_id:262034) provides a structural constraint, Rademacher provided an explicit formula for the multiplier $\epsilon(\gamma)$ that involves a fascinating arithmetic object: the **Dedekind sum**. For coprime integers $d$ and $c$ with $c0$, the Dedekind sum $s(d,c)$ is defined as:
$$ s(d,c) = \sum_{k=1}^{c-1} \left(\left(\frac{k}{c}\right)\right) \left(\left(\frac{dk}{c}\right)\right) $$
where $((x))$ is the "sawtooth" function:
$$ ((x)) = \begin{cases} x - \lfloor x \rfloor - 1/2  \text{if } x \notin \mathbb{Z} \\ 0  \text{if } x \in \mathbb{Z} \end{cases} $$
With this definition, the multiplier for $\gamma=\begin{pmatrix} a  b \\ c  d \end{pmatrix}$ with $c0$ is given by:
$$ \epsilon(\gamma) = \exp\left(\pi i \left( \frac{a+d}{12c} - s(d,c) \right)\right) $$
This formula provides a direct route to calculating the multiplier for any given transformation. For example, consider the matrix $\gamma = \begin{pmatrix} 8  5 \\ 3  2 \end{pmatrix}$ [@problem_id:650866]. Here, $a=8, c=3, d=2$. First, we compute the Dedekind sum $s(2,3)$:
$$ s(2,3) = \sum_{k=1}^{2} \left(\left(\frac{k}{3}\right)\right) \left(\left(\frac{2k}{3}\right)\right) $$
The terms are:
- For $k=1$: $((1/3)) = 1/3 - 1/2 = -1/6$. $((2/3)) = 2/3 - 1/2 = 1/6$. The product is $(-1/6)(1/6) = -1/36$.
- For $k=2$: $((2/3)) = 1/6$. $((4/3)) = ((1+1/3)) = 1/3 - 1/2 = -1/6$. The product is $(1/6)(-1/6) = -1/36$.
So, $s(2,3) = -1/36 - 1/36 = -2/36 = -1/18$.
The term in the exponent of the multiplier formula is $\frac{a+d}{12c} - s(d,c) = \frac{8+2}{12 \cdot 3} - (-\frac{1}{18}) = \frac{10}{36} + \frac{1}{18} = \frac{5}{18} + \frac{1}{18} = \frac{6}{18} = \frac{1}{3}$.
Similarly, for $\gamma = \begin{pmatrix} 4  3 \\ 5  4 \end{pmatrix}$, one finds $s(4,5) = -1/5$ and the multiplier is $\epsilon(\gamma) = \exp(\pi i/3)$ [@problem_id:650900].

A cornerstone of the theory of Dedekind sums is the **Dedekind Reciprocity Law**. For any two coprime positive integers $h$ and $k$, it states:
$$ s(h,k) + s(k,h) = \frac{h^2 + k^2 + 1}{12hk} - \frac{1}{4} $$
This theorem is not just a theoretical curiosity; it provides a powerful algorithm, analogous to the Euclidean algorithm, for rapidly computing Dedekind sums. It also reveals a deep symmetry. For example, to find the value of $s(7,11) + s(11,7)$, one does not need to compute each sum individually [@problem_id:651033]. We can directly apply the [reciprocity law](@entry_id:185655):
$$ s(7,11) + s(11,7) = \frac{7^2 + 11^2 + 1}{12 \cdot 7 \cdot 11} - \frac{1}{4} = \frac{49+121+1}{924} - \frac{1}{4} = \frac{171}{924} - \frac{231}{924} = -\frac{60}{924} = -\frac{5}{77} $$

### Connections to Modular Forms Theory

The Dedekind eta function is a gateway to the richer theory of modular forms. A **meromorphic modular form of weight $k$** for a group $\Gamma \subseteq SL(2, \mathbb{Z})$ is a function $f$ meromorphic on $\mathbb{H}$ (and at the cusps) that transforms as:
$$ f(\gamma\tau) = (c\tau+d)^k f(\tau) \quad \text{for all } \gamma = \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in \Gamma $$
The eta function, with its non-trivial multiplier $\epsilon(\gamma)$, is not strictly a [modular form](@entry_id:184897) in this sense. However, certain powers of $\eta$ are. The multiplier $\epsilon(\gamma)$ is a 24th root of unity. Therefore, for $\eta(\tau)^{24}$, the transformation becomes:
$$ \eta(\gamma\tau)^{24} = (\epsilon(\gamma))^{24} ((c\tau+d)^{1/2})^{24} \eta(\tau)^{24} = 1 \cdot (c\tau+d)^{12} \eta(\tau)^{24} $$
Thus, the function $\Delta(\tau) = (2\pi)^{12}\eta(\tau)^{24}$ is a true [modular form](@entry_id:184897) of weight 12 for the full [modular group](@entry_id:146452) $SL(2, \mathbb{Z})$. This is the celebrated **[modular discriminant](@entry_id:191288)**. Since $\eta(\tau)$ has a $q$-expansion starting with $q^{1/24}$, $\Delta(\tau)$ has a $q$-expansion starting with $(2\pi)^{12}q$, meaning it vanishes as $\tau \to i\infty$. This makes it a **cusp form**.

The distribution of [zeros and poles](@entry_id:177073) of a modular form is tightly constrained by the **valence formula**. For any non-zero meromorphic modular form $f$ of weight $k$ for $SL(2, \mathbb{Z})$, this formula states:
$$ \text{ord}_{i\infty}(f) + \frac{1}{2}\text{ord}_{i}(f) + \frac{1}{3}\text{ord}_{\rho}(f) + \sum_{p \in \mathcal{F}^*} \text{ord}_p(f) = \frac{k}{12} $$
Here, $i$ and $\rho = e^{2i\pi/3}$ are the elliptic fixed points of the standard [fundamental domain](@entry_id:201756) $\mathcal{F}$, and $\text{ord}_p(f)$ is the order of the zero or pole at $p$. This formula provides a powerful accounting tool. For instance, consider the Eisenstein series $E_4$ (weight 4) and $E_6$ (weight 6), and the [modular discriminant](@entry_id:191288) $\Delta$ (weight 12). $E_4$ has a simple zero at $\rho$, $E_6$ has a simple zero at $i$, and $\Delta$ is non-zero everywhere in $\mathbb{H}$. Let's determine the order at the cusp of the function $F(\tau) = \frac{E_4(\tau) \Delta(\tau)}{E_6(\tau)}$ [@problem_id:650905].
The weight of $F(\tau)$ is $k = 4 + 12 - 6 = 10$. The orders of its [zeros and poles](@entry_id:177073) in the [fundamental domain](@entry_id:201756) are:
-   At $\tau = \rho$, $E_4$ has a simple zero, so $\text{ord}_{\rho}(F)=1$.
-   At $\tau = i$, $E_6$ has a simple zero, so $F$ has a simple pole: $\text{ord}_{i}(F)=-1$.
-   Since $\Delta$ is non-zero in $\mathbb{H}$ and $E_4, E_6$ have no other zeros in $\mathcal{F}^*$, the sum over other points is zero.
Plugging these into the valence formula:
$$ \text{ord}_{i\infty}(F) + \frac{1}{2}(-1) + \frac{1}{3}(1) = \frac{10}{12} $$
$$ \text{ord}_{i\infty}(F) - \frac{1}{6} = \frac{5}{6} \implies \text{ord}_{i\infty}(F) = 1 $$
This means $F(\tau)$ has a simple zero at the cusp, i.e., its $q$-expansion begins with $q$.

Finally, the eta function is key to understanding **quasi-modular forms**. The Eisenstein series $E_2(\tau)$ is defined via the [logarithmic derivative](@entry_id:169238) of $\eta$:
$$ E_2(\tau) = \frac{12}{\pi i} \frac{d}{d\tau} \log \eta(\tau) = 1 - 24 \sum_{n=1}^\infty \frac{nq^n}{1-q^n} $$
Its modular transformation is anomalous. We can derive this from the transformation of $\log\eta(\tau)$. Taking the logarithm of the general transformation law for $\eta$ gives:
$$ \log\eta(\gamma\tau) = \log \epsilon(\gamma) + \frac{1}{2}\log(c\tau+d) + \log\eta(\tau) $$
Differentiating with respect to $\tau$ (and using $\frac{d(\gamma\tau)}{d\tau} = (c\tau+d)^{-2}$) yields:
$$ \frac{1}{(c\tau+d)^2} \frac{d}{d(\gamma\tau)}\log\eta(\gamma\tau) = \frac{c}{2(c\tau+d)} + \frac{d}{d\tau}\log\eta(\tau) $$
Multiplying by $\frac{12}{\pi i}(c\tau+d)^2$ and identifying the definition of $E_2$:
$$ \frac{12}{\pi i} \frac{d}{d(\gamma\tau)}\log\eta(\gamma\tau) = (c\tau+d)^2 \left(\frac{12}{\pi i} \frac{d}{d\tau}\log\eta(\tau)\right) + \frac{12(c\tau+d)^2}{\pi i} \frac{c}{2(c\tau+d)} $$
This simplifies to the transformation law for $E_2(\tau)$ [@problem_id:886095]:
$$ E_2(\gamma\tau) = (c\tau+d)^2 E_2(\tau) + \frac{6c}{\pi i}(c\tau+d) $$
The extra term $\frac{6c}{\pi i}(c\tau+d)$ prevents $E_2$ from being a true modular form. This "anomaly" is a direct consequence of the logarithmic nature of the eta transformation and makes $E_2$ a prime example of a quasi-[modular form](@entry_id:184897), a class of functions with rich algebraic structure and wide-ranging applications.