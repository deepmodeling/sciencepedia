## Introduction
In mathematics, the ambition to assign a notion of "size" or "length" to a wide variety of sets on the real line is the central goal of [measure theory](@entry_id:139744). Before we can measure a set, however, we must first answer a more fundamental question: which sets are "measurable"? This article tackles the very first step in this journey, focusing on the measurability of the most basic geometric objects: intervals. While it may seem intuitive that an interval should have a measurable length, establishing this fact with mathematical rigor is a non-trivial process that unlocks the entire framework of Lebesgue measure.

This article will guide you through the elegant logic that confirms the measurability of intervals and explores the profound consequences of this single fact. In "Principles and Mechanisms," you will learn how the abstract properties of a σ-algebra and the Carathéodory criterion are used to construct all types of measurable intervals from a simple starting point, leading to the creation of the vital Borel σ-algebra. Subsequently, "Applications and Interdisciplinary Connections" will demonstrate the utility of these concepts, showing how they enable the measurement of complex sets and serve as the bedrock for modern [mathematical analysis](@entry_id:139664), probability theory, and dynamical systems. Finally, you will apply your knowledge in "Hands-On Practices," engaging with problems that reinforce the theoretical bridge between simple intervals and their powerful applications.

## Principles and Mechanisms

In the preceding chapter, we introduced the ambition of measure theory: to assign a notion of "size"—such as length, area, or volume—to a vast collection of subsets of a given space. For the real line $\mathbb{R}$, this "size" is the Lebesgue measure. The foundational challenge is to rigorously define which sets are "measurable" and to do so in a way that aligns with our intuition about length while also possessing powerful [closure properties](@entry_id:265485). This collection of measurable sets must form a **σ-algebra**, a structure closed under complements, countable unions, and countable intersections.

The formal definition of a Lebesgue [measurable set](@entry_id:263324) hinges on the **Carathéodory criterion**. A set $E \subseteq \mathbb{R}$ is deemed Lebesgue measurable if, for any arbitrary "test" set $A \subseteq \mathbb{R}$, it partitions the outer measure additively:

$$ \lambda^*(A) = \lambda^*(A \cap E) + \lambda^*(A \cap E^c) $$

Here, $\lambda^*$ represents the Lebesgue outer measure. While this definition is abstract, its power lies in guaranteeing that the resulting collection of [measurable sets](@entry_id:159173), $\mathcal{M}$, indeed forms a [σ-algebra](@entry_id:141463). Our first task is to use this powerful framework to confirm that the most elementary geometric objects—intervals—are themselves measurable.

### From Half-Infinite Rays to All Intervals

The construction of the Lebesgue measure often begins by proving that a simple class of sets is measurable. A common starting point is to establish the measurability of all half-infinite intervals of the form $(c, \infty)$ for any $c \in \mathbb{R}$. While the proof of this initial step is technical and relies on the definition of [outer measure](@entry_id:157827), we can take it as a given premise to demonstrate the power of the σ-algebra properties. If we know that all sets $(c, \infty)$ are in the σ-algebra $\mathcal{M}$, how can we deduce that a simple open interval $(a, b)$ is also measurable?

The process is a beautiful exercise in logical construction, relying on the three pillars of a [σ-algebra](@entry_id:141463) [@problem_id:1411594]:

1.  **Closure under Complements:** Since $(c, \infty)$ is measurable for any $c$, its complement must also be measurable. The complement of $(c, \infty)$ is the closed, left-unbounded interval $(-\infty, c]$. Thus, we have established that all sets of the form $(-\infty, c]$ are members of $\mathcal{M}$.

2.  **Closure under Countable Unions:** Our goal is to obtain an [open interval](@entry_id:144029), but we currently only have access to closed ones on the left side. We can, however, construct an [open interval](@entry_id:144029) from closed ones. Consider the open interval $(-\infty, b)$. Any point $x$ in this interval satisfies $x  b$. By the Archimedean property of the real numbers, we can always find a positive integer $n$ such that $x \le b - \frac{1}{n}$. This observation allows us to express the [open interval](@entry_id:144029) as a countable union of closed intervals:
    $$ (-\infty, b) = \bigcup_{n=1}^{\infty} \left(-\infty, b - \frac{1}{n}\right] $$
    Since each set $(-\infty, b - \frac{1}{n}]$ is measurable from step 1, and $\mathcal{M}$ is closed under countable unions, it follows that the open interval $(-\infty, b)$ is also measurable.

3.  **Closure under (Countable) Intersections:** A [σ-algebra](@entry_id:141463) is closed under countable intersections (which can be derived from [closure under complements](@entry_id:183838) and countable unions via De Morgan's laws). We can now express our target interval $(a, b)$ as the intersection of two measurable sets we have just constructed:
    $$ (a, b) = (a, \infty) \cap (-\infty, b) $$
    The set $(a, \infty)$ is measurable by our premise, and $(-\infty, b)$ is measurable by step 2. Therefore, their intersection, the open interval $(a, b)$, is Lebesgue measurable.

This [constructive proof](@entry_id:157587) illustrates a core theme in measure theory: starting from a simple class of measurable sets, we can systematically build up to a much richer collection. Once open intervals are known to be measurable, it is straightforward to show that all other types of intervals—closed, half-open—are also measurable. For instance, a closed interval $[a, b]$ is the complement of the [measurable set](@entry_id:263324) $(-\infty, a) \cup (b, \infty)$. The union of two [measurable sets](@entry_id:159173) is measurable, and the complement of a measurable set is measurable, so $[a, b]$ must be measurable. Simple applications of the σ-algebra axioms, such as showing that the set $(-\infty, a] \cup [b, \infty)$ is measurable given that its constituent parts are, become elementary exercises in this framework [@problem_id:1430774].

### The Borel σ-Algebra: The Offspring of Intervals

The fact that all intervals are Lebesgue measurable is of paramount importance. They form the basis for the most significant [σ-algebra](@entry_id:141463) on the real line used in analysis and probability theory: the **Borel σ-algebra**.

The Borel σ-algebra on $\mathbb{R}$, denoted $\mathcal{B}(\mathbb{R})$, is defined as the **smallest [σ-algebra](@entry_id:141463) containing all open sets** in $\mathbb{R}$. However, since any open set in $\mathbb{R}$ can be written as a countable union of disjoint [open intervals](@entry_id:157577), this is equivalent to defining $\mathcal{B}(\mathbb{R})$ as the σ-algebra **generated by the collection of all [open intervals](@entry_id:157577)**. We write this as $\mathcal{B}(\mathbb{R}) = \sigma(\mathcal{O})$, where $\mathcal{O}$ is the collection of all [open intervals](@entry_id:157577) $(a, b)$ with $a, b \in \mathbb{R}$.

This raises a profound question: do we truly need the uncountable collection of *all* open intervals to generate the Borel sets? Or could a smaller, perhaps even countable, collection of [generating sets](@entry_id:190106) suffice? The answer is not only yes, but this fact is fundamental to many theoretical results.

Consider the collection $\mathcal{O}_{\mathbb{Q}}$ of all open intervals $(q_1, q_2)$ whose endpoints $q_1$ and $q_2$ are rational numbers. Since the set of rational numbers $\mathbb{Q}$ is countable, the set of pairs of rational numbers $\mathbb{Q} \times \mathbb{Q}$ is also countable, which means $\mathcal{O}_{\mathbb{Q}}$ is a countable collection of sets. We can demonstrate that this countable collection generates the exact same Borel [σ-algebra](@entry_id:141463), i.e., $\sigma(\mathcal{O}_{\mathbb{Q}}) = \mathcal{B}(\mathbb{R})$ [@problem_id:1430781].

The proof of this equality proceeds in two steps:
1.  **Show $\sigma(\mathcal{O}_{\mathbb{Q}}) \subseteq \mathcal{B}(\mathbb{R})$:** This direction is straightforward. Every interval with rational endpoints is, by definition, an [open interval](@entry_id:144029). Therefore, the generating collection $\mathcal{O}_{\mathbb{Q}}$ is a subset of the collection $\mathcal{O}$. Since $\mathcal{B}(\mathbb{R}) = \sigma(\mathcal{O})$ is a σ-algebra that contains $\mathcal{O}_{\mathbb{Q}}$, it must also contain the smallest [σ-algebra](@entry_id:141463) generated by $\mathcal{O}_{\mathbb{Q}}$.

2.  **Show $\mathcal{B}(\mathbb{R}) \subseteq \sigma(\mathcal{O}_{\mathbb{Q}})$:** To show this, we need to prove that every set in the generating collection for $\mathcal{B}(\mathbb{R})$—that is, every open interval $(a, b)$ with real endpoints—can be found in $\sigma(\mathcal{O}_{\mathbb{Q}})$. This is achieved by leveraging the **density of the rational numbers in the reals**. For any open interval $(a, b)$, we can find a sequence of rational-endpoint intervals that "fill it up". Specifically, any point $x \in (a, b)$ can be contained within a rational-endpoint interval $(q_1, q_2)$ which itself is contained within $(a, b)$. By taking the union of all such possible rational-endpoint intervals inside $(a,b)$, we can reconstruct the original interval:
    $$ (a, b) = \bigcup \left\{ (q_1, q_2) \mid q_1, q_2 \in \mathbb{Q}, a  q_1  q_2  b \right\} $$
    Because this union is indexed by a subset of the countable set $\mathbb{Q} \times \mathbb{Q}$, it is a countable union. Each interval $(q_1, q_2)$ is in $\mathcal{O}_{\mathbb{Q}}$ by definition. Since $\sigma(\mathcal{O}_{\mathbb{Q}})$ is closed under countable unions, the set $(a, b)$ must belong to $\sigma(\mathcal{O}_{\mathbb{Q}})$.

Because the generators of $\mathcal{B}(\mathbb{R})$ are contained in $\sigma(\mathcal{O}_{\mathbb{Q}})$, the entire [σ-algebra](@entry_id:141463) must be contained within it as well. Together, these two inclusions prove that $\sigma(\mathcal{O}_{\mathbb{Q}}) = \mathcal{B}(\mathbb{R})$. This powerful result shows that the immensely [complex structure](@entry_id:269128) of the Borel sets can be built up from a humble, countable collection of rational intervals. This has far-reaching consequences, for example, in defining measures by specifying their values only on this countable [generating set](@entry_id:145520).

### Measure Calculations and Limiting Properties

With the measurability of intervals established, we can perform concrete calculations. The Lebesgue measure of any interval is simply its length. Two fundamental properties of the measure are indispensable for calculations.

First is the **[continuity of measure](@entry_id:159818)**. For a nested, decreasing sequence of measurable sets $E_1 \supseteq E_2 \supseteq \dots$ with $\lambda(E_1)  \infty$, the measure of the intersection is the limit of the measures:
$$ \lambda\left(\bigcap_{n=1}^{\infty} E_n\right) = \lim_{n \to \infty} \lambda(E_n) $$
Consider, for instance, a set $S$ defined as the intersection of a sequence of nested closed intervals $I_n = [a_n, b_n]$. If the endpoint sequences $\{a_n\}$ and $\{b_n\}$ are monotonic and converge to limits $a$ and $b$ respectively, then the intersection is simply the interval $[a, b]$, and its measure is $b-a$ [@problem_id:1430765].

Second is **[countable additivity](@entry_id:141665)**. For any countable collection of pairwise disjoint [measurable sets](@entry_id:159173) $\{E_n\}$, the measure of their union is the sum of their measures:
$$ \lambda\left(\bigcup_{n=1}^{\infty} E_n\right) = \sum_{n=1}^{\infty} \lambda(E_n) $$
This property is the cornerstone of integration theory. We can use it in concert with other basic properties, such as the fact that if $B \subseteq A$ are [measurable sets](@entry_id:159173) with [finite measure](@entry_id:204764), then $\lambda(A \setminus B) = \lambda(A) - \lambda(B)$.

For example, imagine a set $S$ constructed as a disjoint union $S = \bigcup_{n=1}^{\infty} (I_n \setminus C_n)$, where $\{I_n\}$ are disjoint open intervals and each $C_n$ is a measurable subset of $I_n$. By [countable additivity](@entry_id:141665), the measure of $S$ is $\lambda(S) = \sum_{n=1}^{\infty} \lambda(I_n \setminus C_n)$. Applying the difference rule, we get $\lambda(S) = \sum_{n=1}^{\infty} (\lambda(I_n) - \lambda(C_n))$. If the measures of $I_n$ and $C_n$ are known (e.g., given by terms of a [geometric series](@entry_id:158490)), this sum can be calculated directly [@problem_id:1430777].

### The Subtleties of Measurability

The Carathéodory criterion is precisely formulated for a reason. Its structure is deeply connected to the properties of the length function itself. A natural question to ask is: why this definition? What would happen if we tried to build a measure from a different notion of "length"?

Let's explore this by defining a hypothetical [pre-measure](@entry_id:192696) on half-open intervals $(a, b]$ not by their length $b-a$, but by the square root of their length, $\lambda_{\text{sqrt}}((a,b]) = \sqrt{b-a}$. We can then generate an [outer measure](@entry_id:157827) $\mu_{\text{sqrt}}^*$ in the standard way. Is an interval like $S=(5, 17]$ measurable with respect to this new outer measure? To check, we use the Carathéodory criterion with a test set, say $T = (1, 10]$. For $S$ to be measurable, we would need $\mu_{\text{sqrt}}^*(T) = \mu_{\text{sqrt}}^*(T \cap S) + \mu_{\text{sqrt}}^*(T \cap S^c)$.

Let's perform the calculation [@problem_id:1430778]:
*   $T = (1, 10]$, so $\mu_{\text{sqrt}}^*(T) = \sqrt{10-1} = \sqrt{9} = 3$.
*   $T \cap S = (5, 10]$, so $\mu_{\text{sqrt}}^*(T \cap S) = \sqrt{10-5} = \sqrt{5}$.
*   $T \cap S^c = (1, 5]$, so $\mu_{\text{sqrt}}^*(T \cap S^c) = \sqrt{5-1} = \sqrt{4} = 2$.

Now, we check the criterion:
$$ \mu_{\text{sqrt}}^*(T \cap S) + \mu_{\text{sqrt}}^*(T \cap S^c) = \sqrt{5} + 2 \approx 4.236 $$
This value is clearly not equal to $\mu_{\text{sqrt}}^*(T) = 3$. The additivity fails. The "additivity defect" is $\sqrt{5} + 2 - 3 = \sqrt{5} - 1 > 0$. The reason for this failure is the concavity of the square root function: for any positive lengths $L_1, L_2$, we have $\sqrt{L_1} + \sqrt{L_2} \ge \sqrt{L_1 + L_2}$. In contrast, the standard length function is additive: $L_1 + L_2 = L_1 + L_2$. It is precisely this simple additivity of length that ensures intervals satisfy the Carathéodory criterion for the Lebesgue measure.

Another crucial subtlety of the criterion is the requirement that it must hold for *any* [test set](@entry_id:637546) $A \subseteq \mathbb{R}$. One might wonder if it would be sufficient to check the criterion only for a simpler class of test sets, such as open intervals. While this simplification is sufficient for the Lebesgue measure (a non-trivial result known as Carathéodory's Lemma), it is not true in general for other measures. There exist measures, like the Lebesgue-Stieltjes measure $\mu_F$ induced by the Cantor-Lebesgue function $F$, for which a set can satisfy the criterion for all interval test sets but fail it for a more complex [test set](@entry_id:637546) (like the Cantor set itself), proving the set is not $\mu_F$-measurable [@problem_id:1430776]. This advanced example serves as a critical warning: the [quantifier](@entry_id:151296) "for any set A" in the Carathéodory definition is indispensable for its full power and generality.

### Advanced Topics in Measurability

The concept of measurability extends to sets defined in more abstract ways, often leading to surprising and enlightening results.

#### Measurability of Level Sets

A powerful technique for establishing the measurability of a set is to show that it is a **level set** of a measurable function. A function $f: \mathbb{R} \to \mathbb{R}$ is said to be measurable if for every real number $c$, the set $\{x \in \mathbb{R} \mid f(x) > c\}$ is a measurable set. It follows from the properties of a [σ-algebra](@entry_id:141463) that other types of [level sets](@entry_id:151155) (e.g., $\{x \mid f(x) \le c\}$, $\{x \mid f(x) = c\}$) are also measurable.

Consider a set $E$ defined by a condition involving the measure of other sets, for instance:
$$ E = \left\{ x \in [0,1] \;\middle|\; m\left(\bigcup_{n: x \in I_n} J_n\right) > c \right\} $$
where $\{I_n\}$ and $\{J_n\}$ are given sequences of intervals and $c$ is a constant [@problem_id:1430770]. At first glance, the [measurability](@entry_id:199191) of $E$ is not obvious. The path forward is to define a function $f(x) = m\left(\bigcup_{n: x \in I_n} J_n\right)$ and analyze its properties. If $f(x)$ can be shown to be a measurable function, then the set $E = \{x \mid f(x) > c\}$ is, by definition, measurable. In many practical cases, the function $f(x)$ turns out to be a [step function](@entry_id:158924) or a [pointwise limit](@entry_id:193549) of [step functions](@entry_id:159192), which are known to be measurable. This transforms a question about set structure into a question about function properties, often providing a clearer route to the solution.

#### Measurability and Uncountable Unions

Intuition can sometimes mislead when dealing with the infinite, particularly with [non-measurable sets](@entry_id:161390). For example, if we take a union of sets indexed by a [non-measurable set](@entry_id:138132), we might expect the resulting union to be non-measurable as well. This is not necessarily true. The geometric properties of the sets in the union can override the "badness" of the [index set](@entry_id:268489).

Consider a [non-measurable set](@entry_id:138132) $V \subset [0,1]$. For each $x \in V$, let's define an [open interval](@entry_id:144029) $I_x$ centered at $x$ whose radius is determined by the distance to its nearest neighbor in $V$. Let $d_x = \inf \{ |x-y| : y \in V, y \neq x \}$. We define $I_x = (x - d_x/2, x + d_x/2)$. Now form the union $U = \bigcup_{x \in V} I_x$. Is $U$ measurable?

The answer, perhaps surprisingly, is yes. The key insight lies in the relationship between the intervals $I_x$. For any two distinct points $x, z \in V$, the intervals $I_x$ and $I_z$ are **pairwise disjoint**. If they were to overlap, the distance between their centers, $|x-z|$, would have to be less than the sum of their radii, $d_x/2 + d_z/2$. However, by definition of $d_x$ and $d_z$, we know that $d_x \le |x-z|$ and $d_z \le |x-z|$. This leads to the contradiction $|x-z|  (d_x+d_z)/2 \le (|x-z|+|x-z|)/2 = |x-z|$.

Therefore, the set $U$ is a union of pairwise disjoint open intervals. A union of any collection of open sets is always an open set. And in $\mathbb{R}$, every open set is Lebesgue measurable (in fact, it can be written as a countable union of disjoint open intervals). Thus, $U$ is always measurable, regardless of the non-measurable nature of the indexing set $V$ [@problem_id:1430771]. This elegant example demonstrates that geometric structure can impose regularity, yielding a "well-behaved" [measurable set](@entry_id:263324) from a process involving a "pathological" non-measurable one. It is a powerful reminder that in [measure theory](@entry_id:139744), our finite intuition must be constantly tested and refined against the rigorous logic of its axioms.