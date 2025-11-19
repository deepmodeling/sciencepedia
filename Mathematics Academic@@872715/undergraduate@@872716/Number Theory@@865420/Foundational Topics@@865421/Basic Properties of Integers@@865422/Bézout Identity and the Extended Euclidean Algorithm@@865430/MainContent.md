## Introduction
The concept of the [greatest common divisor](@entry_id:142947) (GCD) is a fundamental building block in number theory, yet its significance extends far beyond simple arithmetic. Bézout's Identity reveals a deeper truth: the GCD of two integers is not just their largest shared factor, but is also the smallest positive value that can be formed by a [linear combination](@entry_id:155091) of them. While this identity guarantees the existence of such a combination, it raises a crucial question: how do we systematically find these integer coefficients? This knowledge gap is bridged by the Extended Euclidean Algorithm, an elegant and powerful computational method that serves as a cornerstone for modern mathematics and computer science.

This article will guide you through this foundational topic in three parts. First, the chapter on **Principles and Mechanisms** will rigorously establish the theory, from the formal definition of the GCD to the [constructive proof](@entry_id:157587) of Bézout's Identity and the mechanics of the algorithms used to find its coefficients. Next, in **Applications and Interdisciplinary Connections**, we will explore the algorithm's far-reaching impact, solving linear Diophantine equations, enabling modern cryptography, and revealing its connections to abstract algebra. Finally, the **Hands-On Practices** will provide an opportunity to solidify your understanding by implementing the algorithm and solving practical problems. We begin by laying the theoretical groundwork upon which these powerful applications are built.

## Principles and Mechanisms

The previous chapter introduced the foundational concepts of divisibility and modular arithmetic. We now build upon this foundation to explore one of the most powerful and elegant results in elementary number theory: Bézout's Identity. This identity reveals a profound structural property of integers and provides the theoretical underpinning for the Extended Euclidean Algorithm, a computational tool of immense practical importance in fields ranging from cryptography to computer science. This chapter will rigorously define the [greatest common divisor](@entry_id:142947), establish Bézout's identity from first principles, detail the mechanisms of the algorithms used to find it, and explore its numerous applications and generalizations.

### The Greatest Common Divisor, Redefined

Our intuitive understanding of the **[greatest common divisor](@entry_id:142947)** (GCD) of two integers $a$ and $b$, denoted $\gcd(a,b)$, is that it is the largest positive integer that divides both $a$ and $b$. While this definition is serviceable for basic arithmetic, a more robust and abstract definition provides deeper insight and generalizes more effectively. The modern definition is based on the [partial order](@entry_id:145467) imposed by divisibility.

**Definition.** For two integers $a$ and $b$, not both zero, an integer $d$ is a **greatest common divisor** if it satisfies two conditions:
1.  $d$ is a common divisor: $d \mid a$ and $d \mid b$.
2.  $d$ is the "greatest" in terms of [divisibility](@entry_id:190902): for any other common [divisor](@entry_id:188452) $c$ (i.e., if $c \mid a$ and $c \mid b$), it must be that $c \mid d$.

This definition reveals that the GCD is a common divisor that is divisible by every other common [divisor](@entry_id:188452). An immediate consequence is that the GCD is not necessarily unique. If $d$ is a GCD of $a$ and $b$, then its negative, $-d$, also satisfies both conditions. In the ring of integers $\mathbb{Z}$, these two values, $d$ and $-d$, are called **associates**. To make the function $\gcd(a,b)$ single-valued, we adopt the standard convention of choosing the non-negative result. Thus, $\gcd(a,b)$ is defined as the unique non-negative integer satisfying the two conditions.

The special cases involving zero are handled consistently by this definition [@problem_id:3082259]. For any non-zero integer $a$, the common divisors of $a$ and $0$ are simply the divisors of $a$. The largest positive [divisor](@entry_id:188452) of $a$ is $|a|$, and every other [divisor](@entry_id:188452) of $a$ indeed divides $|a|$. Thus, $\gcd(a,0) = |a|$. For the case of $\gcd(0,0)$, every integer $c \in \mathbb{Z}$ is a [divisor](@entry_id:188452) of $0$. The only integer that is divisible by every integer $c$ is $0$ itself. Therefore, the only consistent definition is $\gcd(0,0) = 0$.

### Bézout's Identity: The Fundamental Theorem

The formal definition of the GCD sets the stage for a remarkable theorem that links the GCD to a [linear combination](@entry_id:155091) of the original numbers.

**Theorem (Bézout's Identity).** For any integers $a$ and $b$, not both zero, there exist integers $x$ and $y$ such that:
$$ax + by = \gcd(a,b)$$

The integers $x$ and $y$ are known as the **Bézout coefficients**. This identity asserts that the [greatest common divisor](@entry_id:142947) of $a$ and $b$ is precisely the smallest positive integer that can be expressed as a [linear combination](@entry_id:155091) of $a$ and $b$.

The existence of such integers $x$ and $y$ is not immediately obvious but can be proven elegantly using the **Well-Ordering Principle**, which states that any non-[empty set](@entry_id:261946) of non-negative integers has a [least element](@entry_id:265018) [@problem_id:3082259]. Consider the set $S$ of all positive integer linear combinations of $a$ and $b$:
$$ S = \{ax' + by' \mid x', y' \in \mathbb{Z} \text{ and } ax' + by' > 0 \} $$
Since $a$ and $b$ are not both zero, this set is non-empty (for instance, if $a \neq 0$, then $a(1) + b(0) = a$ or $a(-1) + b(0) = -a$ is in $S$, depending on the sign of $a$). By the Well-Ordering Principle, $S$ must contain a [least element](@entry_id:265018); let's call it $d$. By its definition, $d = ax + by$ for some integers $x$ and $y$.

We claim this $d$ is the $\gcd(a,b)$. We must show it satisfies the two conditions of our formal definition.
1.  First, we show $d$ divides $a$. By the [division algorithm](@entry_id:156013), we can write $a = dq + r$, where $0 \le r  d$. We can express the remainder $r$ as $r = a - dq = a - (ax+by)q = a(1-xq) + b(-yq)$. This shows that $r$ is also a linear combination of $a$ and $b$. If $r$ were positive, it would be an element of $S$. However, $r  d$, and $d$ is the *least* element of $S$. This is a contradiction. Therefore, the remainder $r$ must be $0$. This implies $a = dq$, so $d \mid a$. A similar argument shows $d \mid b$. Thus, $d$ is a common [divisor](@entry_id:188452).
2.  Second, let $c$ be any other common divisor of $a$ and $b$. Then $a=ca'$ and $b=cb'$ for some integers $a'$ and $b'$. Substituting these into the expression for $d$ gives $d = (ca')x + (cb')y = c(a'x + b'y)$. This shows that $c \mid d$.

Since $d$ satisfies both conditions and is positive by construction, it is the unique non-negative [greatest common divisor](@entry_id:142947). This [constructive proof](@entry_id:157587) not only guarantees the existence of Bézout coefficients but also provides the theoretical basis for an algorithm to find them.

From a more abstract algebraic perspective, the set of all integer linear combinations $\{ax' + by' \mid x', y' \in \mathbb{Z}\}$ forms what is known as an **ideal** in the [ring of integers](@entry_id:155711), denoted $(a,b)$ or $a\mathbb{Z} + b\mathbb{Z}$. The proof above shows that this ideal is precisely the set of all multiples of $d = \gcd(a,b)$, which is the [principal ideal](@entry_id:152760) $(d)$. Thus, Bézout's identity is equivalent to the statement that every ideal in $\mathbb{Z}$ generated by two elements can be generated by a single element: $a\mathbb{Z} + b\mathbb{Z} = \gcd(a,b)\mathbb{Z}$ [@problem_id:3082264].

### The Euclidean Algorithm: Finding the GCD

While Bézout's identity guarantees the existence of coefficients $x$ and $y$, it does not immediately provide a method for finding them. The key is the **Euclidean Algorithm**, a simple yet powerful procedure for computing the GCD that dates back to antiquity. The algorithm is based on a single, crucial property: if $a = bq + r$, then $\gcd(a,b) = \gcd(b,r)$.

This property holds because the set of common divisors of $(a,b)$ is identical to the set of common divisors of $(b,r)$. Any common [divisor](@entry_id:188452) of $b$ and $r$ must also divide $bq+r=a$, making it a common divisor of $a$ and $b$. Conversely, any common [divisor](@entry_id:188452) of $a$ and $b$ must also divide $a-bq=r$, making it a common divisor of $b$ and $r$.

The algorithm proceeds as follows:
Given two integers $a$ and $b$ (assume non-negative without loss of generality), apply the [division algorithm](@entry_id:156013) repeatedly:
\begin{align*}
a = b q_1 + r_1  (0 \le r_1  b) \\
b = r_1 q_2 + r_2  (0 \le r_2  r_1) \\
r_1 = r_2 q_3 + r_3  (0 \le r_3  r_2) \\
\vdots \\
r_{k-2} = r_{k-1} q_k + r_k  (0 \le r_k  r_{k-1}) \\
r_{k-1} = r_k q_{k+1} + 0
\end{align*}
Since the remainders form a strictly decreasing sequence of non-negative integers ($b > r_1 > r_2 > \dots \ge 0$), the process must terminate with a remainder of $0$ in a finite number of steps [@problem_id:3082278]. The last non-zero remainder, $r_k$, is the [greatest common divisor](@entry_id:142947).

**Example.** Let's compute $\gcd(141, 96)$ [@problem_id:3082270].
\begin{align*}
141 = 96 \cdot 1 + 45 \\
96 = 45 \cdot 2 + 6 \\
45 = 6 \cdot 7 + 3 \\
6 = 3 \cdot 2 + 0
\end{align*}
The algorithm terminates. The last non-zero remainder is $3$, so $\gcd(141, 96) = 3$.

### The Extended Euclidean Algorithm: Finding the Bézout Coefficients

The Euclidean algorithm can be "extended" to keep track of the Bézout coefficients. There are two common approaches to this.

#### Method 1: Back-Substitution

This method involves working backward through the steps of the Euclidean algorithm to express the GCD as a linear combination of the original numbers. We start with the equation that produced the GCD and substitute previous remainders one by one.

Let's continue our example with $\gcd(141, 96) = 3$ [@problem_id:3082270].
From the third equation, we express the GCD, $3$:
$$ 3 = 45 - 6 \cdot 7 $$
From the second equation, we express the previous remainder, $6$, as $6 = 96 - 45 \cdot 2$. Substitute this into our expression for $3$:
$$ 3 = 45 - (96 - 45 \cdot 2) \cdot 7 = 45 - 7 \cdot 96 + 14 \cdot 45 = 15 \cdot 45 - 7 \cdot 96 $$
Finally, from the first equation, we express $45$ as $45 = 141 - 96 \cdot 1$. Substitute this in:
$$ 3 = 15 \cdot (141 - 96 \cdot 1) - 7 \cdot 96 = 15 \cdot 141 - 15 \cdot 96 - 7 \cdot 96 $$
Combining terms gives the Bézout identity:
$$ 3 = 15 \cdot 141 - 22 \cdot 96 $$
Thus, we have found the coefficients $x=15$ and $y=-22$.

#### Method 2: The Forward Algorithm

While back-substitution is intuitive, it requires storing all the steps of the algorithm. A more efficient "forward" method calculates the coefficients iteratively. This is the standard implementation of the **Extended Euclidean Algorithm (EEA)**. The goal is to maintain, at each step $i$, not only the remainder $r_i$ but also two coefficients $s_i$ and $t_i$ such that the invariant $r_i = s_i a + t_i b$ always holds [@problem_id:3082246].

The algorithm is initialized with two rows corresponding to $a$ and $b$:
$r_0 = a$, $s_0 = 1$, $t_0 = 0$ (since $a = 1 \cdot a + 0 \cdot b$)
$r_1 = b$, $s_1 = 0$, $t_1 = 1$ (since $b = 0 \cdot a + 1 \cdot b$)

For each subsequent step $i+1$, we have $r_{i+1} = r_{i-1} - q_i r_i$. To maintain the invariant, the coefficients must follow the same recurrence:
$s_{i+1} = s_{i-1} - q_i s_i$
$t_{i+1} = t_{i-1} - q_i t_i$

The algorithm stops when $r_{k+1} = 0$. The previous row contains the final answer: the GCD is $d=r_k$, and the coefficients are $x=s_k$ and $y=t_k$.

**Example.** Let's compute $\gcd(420, 378)$ and its Bézout coefficients using the forward method [@problem_id:3082264]. Let $a=420, b=378$.

| $i$ | $r_i$ | $q_i$ | $s_i$ | $t_i$ |
|---|---|---|---|---|
| 0 | 420 | - | 1 | 0 |
| 1 | 378 | - | 0 | 1 |
| 2 | 42 | $q_1=1$ | $s_2=1-1\cdot 0=1$ | $t_2=0-1\cdot 1=-1$ |
| 3 | 0 | $q_2=9$ | | |

Here, $420 = 1 \cdot 378 + 42$, so $q_1=1$. The next remainder is $r_2=42$. The coefficients are $s_2 = s_0 - q_1 s_1 = 1-1(0)=1$ and $t_2 = t_0 - q_1 t_1 = 0-1(1)=-1$.
In the next step, $378 = 9 \cdot 42 + 0$, so $q_2=9$ and the remainder is $0$. The algorithm stops.
The last non-zero remainder is $d=r_2=42$. The corresponding coefficients are $x=s_2=1$ and $y=t_2=-1$.
The identity is $420(1) + 378(-1) = 42$.

### The Family of Solutions

The Bézout coefficients found by the Extended Euclidean Algorithm are not unique. If $(x_0, y_0)$ is one integer solution to the linear Diophantine equation $ax + by = d$, where $d = \gcd(a,b)$, then there are infinitely many solutions.

We can find the general solution by noting that $a(x_0 + \Delta x) + b(y_0 + \Delta y) = d$. Subtracting $ax_0+by_0=d$ leaves $a(\Delta x) + b(\Delta y) = 0$. Dividing by $d$, we get $\frac{a}{d}(\Delta x) = -\frac{b}{d}(\Delta y)$. Since $\frac{a}{d}$ and $\frac{b}{d}$ are coprime, $\frac{b}{d}$ must divide $\Delta x$. So, $\Delta x = k \frac{b}{d}$ for some integer $k$. Substituting this back gives $\frac{a}{d}(k \frac{b}{d}) = -\frac{b}{d}(\Delta y)$, which simplifies to $\Delta y = -k \frac{a}{d}$.

Thus, the general solution is:
$$ x = x_0 + k \frac{b}{d}, \quad y = y_0 - k \frac{a}{d} \quad \text{for any } k \in \mathbb{Z} $$

**Example.** For $899x + 493y = \gcd(899, 493)$, the EEA yields $\gcd(899,493)=29$ and a particular solution $(x_0, y_0) = (-6, 11)$. The general solution is:
$$ x = -6 + k \frac{493}{29} = -6 + 17k $$
$$ y = 11 - k \frac{899}{29} = 11 - 31k $$
For $k=0$, we get the particular solution $(-6, 11)$. For $k=1$, we get another valid solution: $x=11, y=-20$ [@problem_id:3082250].

This general form allows us to find solutions with specific properties. For instance, to find the smallest non-negative integer $x$ satisfying $420x + 378y = 42$, we use our particular solution $(1, -1)$ and the general form $x(k) = 1 + k \frac{378}{42} = 1 + 9k$. We need $1+9k \ge 0$, which implies $k \ge -1/9$. The smallest integer $k$ is $0$, giving the smallest non-negative solution $x=1$ [@problem_id:3082264].

### Applications and Extensions

#### Modular Multiplicative Inverses

One of the most important applications of the EEA is computing modular multiplicative inverses. An integer $a$ has an inverse modulo $n$ if and only if $\gcd(a,n)=1$. Bézout's identity provides the construction. If $\gcd(a,n)=1$, the EEA finds integers $x$ and $y$ such that:
$$ ax + ny = 1 $$
Taking this equation modulo $n$, the term $ny$ becomes $0 \pmod n$, leaving:
$$ ax \equiv 1 \pmod n $$
By definition, this means $x$ is the [multiplicative inverse](@entry_id:137949) of $a$ modulo $n$. The unique inverse in $\{0, 1, \dots, n-1\}$ is then $x \pmod n$.

**Example.** To find the inverse of $143$ modulo $256$ [@problem_id:3087476], we first confirm $\gcd(143, 256) = 1$. Then, applying the EEA to $(256, 143)$ yields the identity:
$$ 111 \cdot 143 - 62 \cdot 256 = 1 $$
Reducing this modulo $256$ gives $111 \cdot 143 \equiv 1 \pmod{256}$. Thus, $143^{-1} \equiv 111 \pmod{256}$.

#### Practical Considerations: Handling Negative Inputs

The Euclidean algorithm is typically defined for non-negative integers. To handle arbitrary integers $a$ and $b$, we can use the property $\gcd(a,b) = \gcd(|a|,|b|)$. We run the EEA on $(|a|, |b|)$ to find $(g, x, y)$ such that $|a|x + |b|y = g$. To find the correct coefficients $(x', y')$ for the original inputs, we use the relations $|a| = a \cdot \operatorname{sgn}(a)$ and $|b| = b \cdot \operatorname{sgn}(b)$.
Substituting these into the identity gives:
$$ (a \cdot \operatorname{sgn}(a))x + (b \cdot \operatorname{sgn}(b))y = g $$
Rearranging, we get:
$$ a(x \cdot \operatorname{sgn}(a)) + b(y \cdot \operatorname{sgn}(b)) = g $$
Thus, the correct coefficients for the original inputs are $x' = x \cdot \operatorname{sgn}(a)$ and $y' = y \cdot \operatorname{sgn}(b)$ [@problem_id:3082276]. For example, running the EEA on $(126, 45)$ gives $9 = (-1) \cdot 126 + 3 \cdot 45$. To find the solution for $(-126, -45)$, we calculate $x' = (-1) \cdot \operatorname{sgn}(-126) = (-1)(-1) = 1$ and $y' = 3 \cdot \operatorname{sgn}(-45) = 3(-1) = -3$. The identity is $9 = (1) \cdot (-126) + (-3) \cdot (-45)$.

#### Algorithmic Variants

The classical Euclidean algorithm uses the least non-negative remainder $r$ satisfying $0 \le r  |b|$. An alternative uses the remainder closest to zero, the **symmetric remainder**, which satisfies $-|b|/2 \le r \le |b|/2$. This often accelerates the algorithm because the remainders decrease in magnitude more rapidly.

**Example.** For $(a,b)=(1000, 64)$, the classical algorithm takes 5 steps. The symmetric variant proceeds as [@problem_id:3082285]:
\begin{align*}
1000 = 16 \cdot 64 - 24  (\text{note } 1000/64=15.625, \text{nearest integer is } 16) \\
64 = 3 \cdot 24 - 8  (\text{note } 64/24 \approx 2.67, \text{nearest integer is } 3) \\
24 = 3 \cdot 8 + 0
\end{align*}
This variant takes only 3 steps. The EEA can be adapted to this method, yielding a valid Bézout identity.

### Generalizations to Other Domains

The principles we have discussed are not limited to the integers. They apply broadly to a class of algebraic structures known as **Euclidean domains**. A Euclidean domain is an integral domain $R$ equipped with a norm function $N: R \setminus \{0\} \to \mathbb{N}$ such that for any $a, b \in R$ with $b \neq 0$, there exist $q, r \in R$ satisfying $a = bq + r$, where either $r=0$ or $N(r)  N(b)$ [@problem_id:3082278].

The [ring of integers](@entry_id:155711) $\mathbb{Z}$ with the norm $N(n) = |n|$ is the canonical example. The argument that the Euclidean algorithm must terminate, based on the well-ordering of $\mathbb{N}$, holds in any Euclidean domain. Furthermore, the argument that the ideal $(a,b)$ is generated by the last non-zero remainder also holds. This leads to a fundamental result in abstract algebra: **every Euclidean domain is a Principal Ideal Domain (PID)**, meaning every ideal can be generated by a single element.

A prime example of another Euclidean domain is the ring of polynomials with rational coefficients, $\mathbb{Q}[x]$. The norm function is the degree of the polynomial, $N(p(x)) = \deg(p(x))$. The [division algorithm for polynomials](@entry_id:150372) always produces a remainder that is either the zero polynomial or has a degree strictly less than the [divisor](@entry_id:188452)'s degree.

In $\mathbb{Q}[x]$, the **units** (elements with multiplicative inverses) are the non-zero constant polynomials. This means that if $d(x)$ is a GCD, then any $c \cdot d(x)$ where $c \in \mathbb{Q} \setminus \{0\}$ is an associate and also a GCD. To enforce uniqueness, we typically normalize the GCD to be **monic** (having a leading coefficient of 1) [@problem_id:3082271].

Bézout's identity holds just as it does for integers. For polynomials $a(x), b(x) \in \mathbb{Q}[x]$, there exist polynomials $u(x), v(x) \in \mathbb{Q}[x]$ such that:
$$ a(x)u(x) + b(x)v(x) = \gcd(a(x), b(x)) $$

**Example.** Let $a(x) = 2x^3 - 2x = 2x(x^2-1)$ and $b(x) = 3x^2-3 = 3(x^2-1)$. A common divisor is clearly $x^2-1$, which is monic, so we take it as the normalized GCD. A simple Bézout representation is found by observing that $b(x)$ is a multiple of the GCD:
$$ (2x^3 - 2x) \cdot 0 + (3x^2 - 3) \cdot \frac{1}{3} = x^2-1 $$
This shows that $u(x) = 0$ and $v(x) = \frac{1}{3}$ are valid Bézout coefficients [@problem_id:3082271]. Just as with integers, these coefficients are not unique. If one has a solution $(u_0(x), v_0(x))$, the general solution is $u(x) = u_0(x) + k(x) \frac{b(x)}{d(x)}$, $v(x) = v_0(x) - k(x) \frac{a(x)}{d(x)}$ for any $k(x) \in \mathbb{Q}[x]$. This demonstrates the universality of the structure first revealed by Bézout and Euclid in the familiar setting of the integers.