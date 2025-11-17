## Introduction
The ability to describe and constrain quantities is fundamental to mathematics and its applications. From defining the safe operating temperature of an engine to determining the [domain of a function](@entry_id:162002), we rely on the language of inequalities. While simple comparisons like $x < 5$ are intuitive, real-world problems often present complex conditions that require a systematic approach. This article addresses the need for a robust framework for solving a wide variety of inequalities and understanding their solutions as intervals on the [real number line](@entry_id:147286).

This guide is structured to build your expertise from the ground up. In the first chapter, **Principles and Mechanisms**, we will establish the foundational rules for manipulating inequalities, explore the geometric power of [absolute values](@entry_id:197463), and introduce the methodical process for solving complex polynomial and rational inequalities. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, discovering how intervals and inequalities are used to model constraints in engineering, analyze system stability in control theory, and underpin core concepts in calculus and mathematical logic. Finally, the **Hands-On Practices** section provides carefully selected problems to help you solidify your understanding and apply these techniques to challenging scenarios involving radicals, exponentials, and [composite functions](@entry_id:147347).

## Principles and Mechanisms

The study of inequalities and the intervals that represent their solutions is a foundational element of [mathematical analysis](@entry_id:139664). It provides the language to describe ranges, tolerances, and domains of functions, which are concepts essential across science and engineering. This chapter will systematically develop the principles for manipulating inequalities and understanding the structure of their solution sets on the real number line.

### From Linear Inequalities to Intervals

The simplest relationship between an inequality and an interval is demonstrated by linear inequalities. A [linear inequality](@entry_id:174297) in one variable, $x$, can be manipulated using the fundamental properties of inequalities: adding or subtracting any real number, or multiplying or dividing by a positive real number, preserves the direction of the inequality. Multiplying or dividing by a negative number reverses it. The solution to such an inequality is typically a half-infinite interval.

More complex conditions often lead to **compound inequalities**, which constrain a variable from both above and below. Consider a geometric problem: finding the possible x-coordinates of a point $B(x, -1)$ such that the x-coordinate of the midpoint $M$ between $A(3, 5)$ and $B$ lies strictly between $-5$ and $1$. The x-coordinate of the midpoint $M$ is given by $\frac{3+x}{2}$. The condition is expressed as the compound inequality:

$$ -5 \lt \frac{3+x}{2} \lt 1 $$

To solve for $x$, we apply operations to all three parts of the inequality simultaneously. Multiplying by $2$ (a positive number) yields:

$$ -10 \lt 3+x \lt 2 $$

Subtracting $3$ from all parts isolates $x$:

$$ -13 \lt x \lt -1 $$

The solution set is the set of all real numbers strictly greater than $-13$ and strictly less than $-1$. This is the **open interval** $(-13, -1)$ [@problem_id:2139306]. This example illustrates how a bounded interval naturally arises as the solution to a set of simultaneous [linear constraints](@entry_id:636966).

### The Geometric Interpretation of Absolute Value

A powerful tool for describing intervals is the **absolute value**, which provides a geometric interpretation of distance on the number line. The expression $|x - k|$ represents the distance between a point $x$ and a fixed point $k$. This single insight allows us to translate geometric statements about distance into algebraic inequalities.

Let us explore the fundamental types of absolute value inequalities, where $R$ is a positive real number representing a radius or tolerance.

1.  **Bounded Intervals:** The inequality $|x - k| \lt R$ describes all points $x$ whose distance from the center $k$ is *less than* $R$. This corresponds precisely to the [open interval](@entry_id:144029) $(k - R, k + R)$. If the inequality is non-strict, $|x - k| \le R$, it includes the endpoints, resulting in the **closed interval** $[k - R, k + R]$.

2.  **Unbounded Intervals:** Conversely, the inequality $|x - k| \gt R$ describes all points $x$ whose distance from $k$ is *greater than* $R$. These points lie "outside" the interval of radius $R$ around $k$. This solution set is a **union** of two disjoint, half-infinite intervals: $(-\infty, k - R) \cup (k + R, \infty)$. The non-strict version, $|x - k| \ge R$, includes the endpoints: $(-\infty, k - R] \cup [k + R, \infty]$.

This [dual representation](@entry_id:146263) is invaluable. For instance, the condition for a frequency $f$ to be within $40$ kHz of a central frequency of $150$ kHz can be written concisely as $|f - 150| \le 40$. This immediately translates to the interval $[150 - 40, 150 + 40]$, which is $[110, 190]$ kHz [@problem_id:2139294].

### Operations on Solution Sets: Intersection, Union, and Complement

Often, a variable must satisfy multiple conditions simultaneously, or satisfy at least one of several conditions. These logical structures correspond to [set operations](@entry_id:143311) on the intervals that represent the solutions to each individual condition.

#### Intersection: The "AND" Condition

The **intersection** of two sets, denoted $A \cap B$, contains all elements that are in *both* set $A$ and set $B$. In the context of inequalities, this arises when multiple constraints must be met simultaneously.

For example, a quality control process for a manufactured rod might require its diameter $D$ to satisfy two criteria. First, its absolute difference from a target $D_0=15.0$ mm must be less than a tolerance $\delta=0.4$ mm. This gives $|D - 15.0| \lt 0.4$, which is the interval $(14.6, 15.4)$. Second, its relative error with respect to a reference $D_{ref}=15.5$ mm must be less than $\epsilon=0.02$. This is $|\frac{D - 15.5}{15.5}| \lt 0.02$, which simplifies to $|D - 15.5| \lt 0.31$, or the interval $(15.19, 15.81)$ [@problem_id:2139327].

An acceptable diameter must satisfy *both* conditions. The set of acceptable diameters is the intersection of these two intervals:
$$ (14.6, 15.4) \cap (15.19, 15.81) $$
To find this intersection, we find the most restrictive bounds: the lower bound must be the maximum of the individual lower bounds ($\max(14.6, 15.19) = 15.19$), and the upper bound must be the minimum of the individual [upper bounds](@entry_id:274738) ($\min(15.4, 15.81) = 15.4$). The resulting interval is $(15.19, 15.4)$.

#### Union and Complement: The "OR" and "NOT" Conditions

The **union** of two sets, $A \cup B$, contains all elements that are in set $A$ *or* in set $B$ (or in both). We have already seen this in the solution to inequalities like $|x-k| > R$, which results in the union of two intervals.

The **complement** of a set $S$, denoted $\mathbb{R} \setminus S$ or $S^c$, contains all elements in the [universal set](@entry_id:264200) (here, $\mathbb{R}$) that are *not* in $S$. This operation is useful in problems where it is easier to characterize the "rejected" or "failing" cases and then find all other cases by taking the complement.

Consider a [digital filter](@entry_id:265006) that passes a frequency $f$ if it is *not* rejected. A frequency is rejected if it meets two conditions: (1) $|f-3| \ge 2$ and (2) $0 \lt f \lt 8$. Let's find the rejected set, $R$.
Condition (1) gives $f \in (-\infty, 1] \cup [5, \infty)$.
Condition (2) gives $f \in (0, 8)$.
The rejected set $R$ is the intersection of these two solution sets:
$$ R = \big( (-\infty, 1] \cup [5, \infty) \big) \cap (0, 8) = (0, 1] \cup [5, 8) $$
The set of passed frequencies, $P$, is the complement of $R$ in the real numbers, $P = \mathbb{R} \setminus R$. Taking the complement of this union of two intervals leaves us with the gaps on the number line:
$$ P = (-\infty, 0] \cup (1, 5) \cup [8, \infty) $$
This set represents all frequencies that are passed by the filter [@problem_id:2139311].

### Solving Polynomial and Rational Inequalities

For inequalities involving polynomials of degree two or higher, or rational functions, a more systematic approach is required. The **Method of Critical Points** is a robust algorithm for solving such inequalities.

The central idea is that a continuous function can only change its sign (from positive to negative or vice versa) by passing through zero. For a [rational function](@entry_id:270841) $f(x) = \frac{P(x)}{Q(x)}$, the sign can change at points where the numerator is zero (since $f(x)=0$) or where the denominator is zero (since $f(x)$ is undefined and may change sign across the vertical asymptote). These points are the **[critical points](@entry_id:144653)**.

The method proceeds as follows:
1.  **Standard Form:** Rearrange the inequality so that one side is $0$, e.g., $f(x) \ge 0$.
2.  **Find Critical Points:** Determine all real numbers $x$ for which the numerator or the denominator of $f(x)$ is zero.
3.  **Partition the Number Line:** The [critical points](@entry_id:144653) divide the [real number line](@entry_id:147286) into a finite number of test intervals.
4.  **Test Each Interval:** Choose a convenient test value within each interval and evaluate the sign of $f(x)$ at that point. Since the sign of $f(x)$ is constant throughout each interval, the sign at the test point applies to the entire interval.
5.  **Construct the Solution:** Collect the intervals that satisfy the inequality. Be meticulous about the endpoints: if the inequality is non-strict ($\ge$ or $\le$), include critical points from the numerator's roots. Critical points from the denominator's roots are *never* included, as the function is undefined there.

Let's apply this to find the domain of the function $F(x) = \sqrt{\frac{x^2 + x - 6}{x - 5}}$. For the square root to be defined, its argument must be non-negative:
$$ \frac{x^2 + x - 6}{x - 5} \ge 0 $$
Factoring the numerator gives $\frac{(x+3)(x-2)}{x-5} \ge 0$. The [critical points](@entry_id:144653) are $x=-3$, $x=2$ (from the numerator), and $x=5$ (from the denominator). These partition the line into $(-\infty, -3)$, $(-3, 2)$, $(2, 5)$, and $(5, \infty)$. A sign analysis reveals the expression is non-negative on $(-3, 2)$ and $(5, \infty)$. We now check the endpoints. At $x=-3$ and $x=2$, the expression is $0$, so these points are included. At $x=5$, the expression is undefined, so it is excluded. The final domain is $[-3, 2] \cup (5, \infty)$ [@problem_id:2139280].

This method is powerful. It can handle complex rational expressions, such as determining the temperature range for which a material is stable based on an index $\sigma(T) = \frac{T^2 - 4T + 53}{T^2 - 20T - 96} \le 0$. By noting the numerator $(T-2)^2 + 49$ is always positive, the problem reduces to solving just the denominator inequality $T^2 - 20T - 96 \lt 0$, which yields the interval $(-4, 24)$ [@problem_id:2139320]. It can also be applied to inequalities that arise from comparing functions, like finding where the cost $(x+3)^2$ is less than the cost $4(x-9)^2$. This simplifies to the quadratic inequality $(x-5)(x-21) > 0$, whose solution is $(-\infty, 5) \cup (21, \infty)$ [@problem_id:2139297].

### Bridging Concepts: Quadratic and Absolute Value Forms

There is an elegant connection between quadratic inequalities and absolute value inequalities. Consider the solution to a quadratic inequality $ax^2 + bx + c \le 0$, where the parabola opens upwards ($a > 0$) and has two distinct real roots, $r_1$ and $r_2$. The solution is the closed interval $[r_1, r_2]$.

Any closed interval $[r_1, r_2]$ can be characterized by its **center**, $k$, and its **radius**, $R$.
$$ k = \frac{r_1 + r_2}{2} \quad \text{and} \quad R = \frac{r_2 - r_1}{2} $$
In terms of $k$ and $R$, the interval is described by the [absolute value inequality](@entry_id:175124) $|x - k| \le R$. We can express $k$ and $R$ directly in terms of the quadratic coefficients $a, b, c$. The roots are $r_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2a}$. Summing the roots gives $r_1+r_2 = -\frac{b}{a}$, and their difference is $r_2-r_1 = \frac{\sqrt{b^2-4ac}}{a}$.

Substituting these into the formulas for $k$ and $R$ yields:
$$ k = \frac{1}{2} \left(-\frac{b}{a}\right) = -\frac{b}{2a} $$
$$ R = \frac{1}{2} \left(\frac{\sqrt{b^2-4ac}}{a}\right) = \frac{\sqrt{b^2-4ac}}{2a} $$
This shows that the solution to $ax^2 + bx + c \le 0$ (for $a>0$) is equivalent to the inequality $|x - (-\frac{b}{2a})| \le \frac{\sqrt{b^2-4ac}}{2a}$ [@problem_id:2139290]. The center of the solution interval, $k = -\frac{b}{2a}$, is precisely the x-coordinate of the vertex of the parabola, the [axis of symmetry](@entry_id:177299) for the roots.

### An Excursion into Discontinuous Functions

The principles of solving inequalities can be extended to more exotic functions, such as those that are not continuous. A prime example is the **[floor function](@entry_id:265373)**, $\lfloor x \rfloor$, which gives the greatest integer less than or equal to $x$.

Consider the inequality:
$$ \frac{\lfloor x \rfloor^2 - 5\lfloor x \rfloor + 4}{\lfloor x \rfloor - 2} \ge 0 $$
The key to solving this is to recognize that $\lfloor x \rfloor$ always produces an integer. Let us make the substitution $n = \lfloor x \rfloor$, where $n$ is an integer. The inequality becomes a rational inequality in the integer variable $n$:
$$ \frac{n^2 - 5n + 4}{n - 2} \ge 0 \quad \implies \quad \frac{(n-1)(n-4)}{n-2} \ge 0 $$
We can analyze this inequality for integer values of $n$. The critical integer values are $1, 2, 4$.
-   For $n=1$, the expression is $0$, which satisfies the inequality.
-   For $n=2$, the denominator is zero, so this integer is disallowed.
-   For $n=3$, the expression is $\frac{(2)(-1)}{1} = -2 \lt 0$, which fails.
-   For $n=4$, the expression is $0$, which satisfies the inequality.
-   For integers $n \ge 5$, all factors are positive, so the expression is positive.
-   For integers $n \le 0$, the expression is negative.

The set of integers $n$ that satisfy the inequality is $\{1\} \cup \{4, 5, 6, \dots\}$. Now, we must translate this solution in terms of $n$ back to a solution in terms of $x$.
-   If $\lfloor x \rfloor = 1$, then by definition $1 \le x \lt 2$. This gives the interval $[1, 2)$.
-   If $\lfloor x \rfloor \in \{4, 5, 6, \dots\}$, this means $\lfloor x \rfloor \ge 4$. By definition, this implies $x \ge 4$. This gives the interval $[4, \infty)$.

The complete solution is the union of these sets: $[1, 2) \cup [4, \infty)$ [@problem_id:2139317]. This example demonstrates a powerful technique: transforming a problem involving a complex function into a simpler algebraic problem by a judicious substitution, and then carefully translating the solution back into the original domain.