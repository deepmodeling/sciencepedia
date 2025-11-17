## Introduction
In the study of combinatorics, we often seek to count the ways of selecting items from a set. While basic combinations deal with selecting distinct items, many real-world problems—from allocating computational resources to modeling quantum particles—require us to select items with repetition. This common scenario demands a unique and powerful approach that goes beyond standard combinatorial formulas. This article serves as a comprehensive guide to mastering combinations with repetition. The first chapter, "Principles and Mechanisms," will introduce the foundational "[stars and bars](@entry_id:153651)" method, derive its formula, and demonstrate how to adapt it for various constraints. The second chapter, "Applications and Interdisciplinary Connections," will explore the surprising ubiquity of this concept, showcasing its role in fields ranging from computer science and finance to statistical physics and abstract algebra. Finally, "Hands-On Practices" will provide an opportunity to solidify your understanding by tackling a curated set of problems. We will begin by exploring the fundamental principles and mechanisms that govern these types of selections.

## Principles and Mechanisms

In [combinatorial mathematics](@entry_id:267925), we are often concerned with counting the number of ways to select objects from a set. A foundational concept is the **combination**, which counts the number of ways to choose a subset of a specific size from a larger set of distinct elements, where the order of selection does not matter. However, many real-world and theoretical scenarios require a different approach—one where we are allowed to select the same element multiple times. This is known as a **combination with repetition**. This chapter elucidates the fundamental principles governing such selections and the primary mechanism for solving these problems, a powerful technique commonly known as "[stars and bars](@entry_id:153651)".

### The Core Problem: Distributing Identical Items into Distinct Bins

Imagine a scenario where we need to distribute a number of identical items into a set of distinct containers or categories. For instance, consider distributing 12 identical computational jobs to 4 distinct processing cores [@problem_id:1349415]. Since the jobs are identical, the only thing that distinguishes one assignment configuration from another is the number of jobs assigned to each core. A core could receive zero jobs, all 12 jobs, or any number in between.

Let's denote the number of jobs assigned to the $i$-th core as $x_i$, where $i \in \{1, 2, 3, 4\}$. Since the total number of jobs is 12, we are looking for the number of integer solutions to the equation:
$x_1 + x_2 + x_3 + x_4 = 12$

The constraint is that each $x_i$ must be a non-negative integer ($x_i \ge 0$). This type of problem is the canonical form for combinations with repetition. It is equivalent to choosing 12 items from a set of 4 types (the cores), where repetition is allowed, and the order of choice does not matter. For example, selecting "core 1" three times and "core 2" nine times corresponds to the solution $x_1=3, x_2=9, x_3=0, x_4=0$.

To solve this, we can visualize the problem using a simple but profound model.

### The Stars and Bars Method

Let's represent the $n$ identical items to be distributed as $n$ "stars" ($\star$). To partition these stars among $k$ distinct bins, we can use $k-1$ "bars" ($|$) as separators. For example, if we have $n=12$ jobs (stars) and $k=4$ cores (bins), we need $k-1=3$ bars. An arrangement of these [stars and bars](@entry_id:153651) could look like this:

$\star\star\star | \star\star\star\star\star | | \star\star\star\star$

This arrangement corresponds to a specific distribution:
- The 3 stars to the left of the first bar mean $x_1 = 3$ jobs for the first core.
- The 5 stars between the first and second bars mean $x_2 = 5$ jobs for the second core.
- The zero stars between the second and third bars mean $x_3 = 0$ jobs for the third core.
- The 4 stars to the right of the third bar mean $x_4 = 4$ jobs for the fourth core.

Note that $3+5+0+4=12$, which is our total number of jobs. Every possible arrangement of these [stars and bars](@entry_id:153651) corresponds to exactly one unique non-negative integer solution to our equation, and vice versa.

The problem has now been transformed into a question of arrangements: In how many ways can we arrange $n$ stars and $k-1$ bars? We have a total of $n + k - 1$ positions to fill. The number of ways to do this is equivalent to choosing which of these $n + k - 1$ positions will be occupied by the $k-1$ bars. The remaining $n$ positions will automatically be filled by stars. This is a standard combination problem.

The number of combinations with repetition is given by the [binomial coefficient](@entry_id:156066):
$$ \binom{n+k-1}{k-1} $$

Due to the symmetry of [binomial coefficients](@entry_id:261706), $\binom{N}{K} = \binom{N}{N-K}$, this is equivalent to choosing the $n$ positions for the stars:
$$ \binom{n+k-1}{n} $$

Applying this formula to the computational jobs problem [@problem_id:1349415], we have $n=12$ identical jobs and $k=4$ distinct cores. The number of distinct assignment configurations is:
$$ \binom{12+4-1}{4-1} = \binom{15}{3} = \frac{15 \times 14 \times 13}{3 \times 2 \times 1} = 455 $$

This demonstrates that there are 455 possible ways to distribute the 12 jobs.

This method is broadly applicable. Consider a robotic barista creating a 4-scoop coffee blend from 8 distinct types of beans [@problem_id:1349441]. This is equivalent to distributing $n=4$ identical "scoops" into $k=8$ distinct "bean types". The number of different blends is:
$$ \binom{4+8-1}{4} = \binom{11}{4} = \frac{11 \times 10 \times 9 \times 8}{4 \times 3 \times 2 \times 1} = 330 $$

### Equivalent Formulations and Diverse Applications

The true power of the [stars and bars](@entry_id:153651) model lies in its ability to solve a wide variety of problems that may not, at first glance, appear related to distributing items. The key is to reframe the problem into the form of finding [non-negative integer solutions](@entry_id:261624) to a linear equation.

#### Polynomial Expansions
Consider the expansion of a multinomial expression like $(w+x+y+z)^9$. When fully expanded, each term will be of the form $C \cdot w^{n_1} x^{n_2} y^{n_3} z^{n_4}$, where $n_1, n_2, n_3, n_4$ are non-negative integers. The sum of the exponents in any given term must be equal to the power of the expansion, so $n_1 + n_2 + n_3 + n_4 = 9$. The number of distinct terms in the expansion is therefore equal to the number of [non-negative integer solutions](@entry_id:261624) to this equation. This is a [stars and bars problem](@entry_id:148883) with $n=9$ and $k=4$. The context could be modeling a quantum system where 9 [energy quanta](@entry_id:145536) are distributed among 4 distinct oscillator modes [@problem_id:1356388]. The number of distinct states is:
$$ \binom{9+4-1}{4-1} = \binom{12}{3} = \frac{12 \times 11 \times 10}{3 \times 2 \times 1} = 220 $$

#### Non-Decreasing Sequences
Another application arises when counting non-decreasing sequences. Suppose we need to form a sequence of length 7 by choosing from the set of integers $\{1, 2, 3, 4, 5\}$, with the condition that the sequence must be non-decreasing (e.g., $1, 1, 2, 4, 4, 4, 5$) [@problem_id:1356394]. A [non-decreasing sequence](@entry_id:139501) is uniquely defined not by the order of selection, but by the *count* of each element selected. Let $x_j$ be the number of times the integer $j$ appears in the sequence. Since the total length of the sequence is 7, we must have:
$x_1 + x_2 + x_3 + x_4 + x_5 = 7$
This is a [stars and bars problem](@entry_id:148883) with $n=7$ and $k=5$. The number of such sequences is:
$$ \binom{7+5-1}{5-1} = \binom{11}{4} = 330 $$

#### Higher-Order Partial Derivatives
In calculus, for a sufficiently smooth multivariable function $\Phi(x_1, x_2, \dots, x_k)$, Clairaut's theorem guarantees that the order of differentiation does not affect the result of [mixed partial derivatives](@entry_id:139334). For example, $\frac{\partial^2 \Phi}{\partial x_1 \partial x_2} = \frac{\partial^2 \Phi}{\partial x_2 \partial x_1}$. Consequently, a distinct $n$-th order partial derivative is uniquely defined by the number of times differentiation is performed with respect to each variable. For a scalar field $\Phi(x, y, z, t)$, the number of distinct third-order [partial derivatives](@entry_id:146280) corresponds to the number of [non-negative integer solutions](@entry_id:261624) to $a_x + a_y + a_z + a_t = 3$, where $a_v$ is the number of times we differentiate with respect to variable $v$ [@problem_id:1349417]. This is a problem with $n=3$ and $k=4$:
$$ \binom{3+4-1}{4-1} = \binom{6}{3} = 20 $$

### Handling Constraints

The basic [stars and bars](@entry_id:153651) formula assumes we are seeking [non-negative integer solutions](@entry_id:261624) ($x_i \ge 0$). Many problems, however, impose additional constraints on the variables. These can often be handled with clever transformations.

#### Lower Bound Constraints
A common constraint is that each category must contain a minimum number of items. For example, a gift box must contain at least one cookie of each of three available colors, with a total of 18 cookies [@problem_id:1349418]. This translates to the equation $x_1 + x_2 + x_3 = 18$, with the constraint $x_i \ge 1$ for all $i$.

To solve this, we can first satisfy the minimum requirement. We "pre-assign" one cookie to each color. This uses up $3 \times 1 = 3$ cookies. We now have $18 - 3 = 15$ cookies left to distribute among the three colors without any further restrictions. This can be modeled with a [change of variables](@entry_id:141386). Let $y_i = x_i - 1$. Since $x_i \ge 1$, we have $y_i \ge 0$. Substituting this into the original equation:
$(y_1 + 1) + (y_2 + 1) + (y_3 + 1) = 18$
$y_1 + y_2 + y_3 = 15$
This is now a standard [stars and bars problem](@entry_id:148883) with $n=15$ and $k=3$. The number of solutions is:
$$ \binom{15+3-1}{3-1} = \binom{17}{2} = 136 $$

This technique generalizes to any set of lower bounds. For an equation $\sum_{i=1}^{k} x_i = n$ with constraints $x_i \ge c_i$ for each $i$, we define new variables $y_i = x_i - c_i$, where $y_i \ge 0$. The total number of pre-assigned items is $C = \sum_{i=1}^{k} c_i$. The equation transforms to:
$\sum_{i=1}^{k} (y_i + c_i) = n \implies \sum_{i=1}^{k} y_i = n - C$
This can then be solved for the $y_i$ variables using the standard formula. This method is applicable to problems like finding stable particle configurations in energy levels with minimum occupancy requirements [@problem_id:1365546] or designing DNA segments with a minimum count of each nucleotide base [@problem_id:1356357].

#### Inequality Constraints
Sometimes we need to solve an inequality, such as distributing *at most* 7 cookies among 4 community centers [@problem_id:1349422]. This corresponds to finding the number of [non-negative integer solutions](@entry_id:261624) to:
$x_1 + x_2 + x_3 + x_4 \le 7$

We can convert this inequality into an equality by introducing a **[slack variable](@entry_id:270695)**. Let $x_5$ represent the number of cookies *not* given away. The number of cookies not given away can be any integer from 0 (if all 7 are distributed) to 7 (if none are distributed). Therefore, $x_5 \ge 0$. The problem is now equivalent to finding the number of [non-negative integer solutions](@entry_id:261624) to:
$x_1 + x_2 + x_3 + x_4 + x_5 = 7$

This is a standard [stars and bars problem](@entry_id:148883) with $n=7$ items and $k=5$ bins (the 4 centers plus the "slack" bin for leftovers). The number of ways is:
$$ \binom{7+5-1}{5-1} = \binom{11}{4} = 330 $$

#### Upper Bound Constraints
Handling upper bounds ($x_i \le M$) is generally more complex and often requires the Principle of Inclusion-Exclusion. However, for certain problems, an elegant [change of variables](@entry_id:141386) can be used. Consider a problem where $n$ items are distributed into $k$ bins, with the constraint that no bin can contain more than $M$ items, i.e., $x_1 + \dots + x_k = n$ with $0 \le x_i \le M$.

An example is distributing $G=15$ identical gates among $Q=4$ distinct qubits, with a hardware limit of $L=5$ gates per qubit [@problem_id:1349414]. The equation is $x_1 + x_2 + x_3 + x_4 = 15$, with the constraint $0 \le x_i \le 5$.

Here, we can define new "slack" variables representing the unused capacity of each bin: $y_i = 5 - x_i$. Since $x_i \le 5$, our new variables are non-negative, $y_i \ge 0$. Substituting $x_i = 5 - y_i$ into the equation:
$\sum_{i=1}^{4} (5 - y_i) = 15$
$20 - \sum_{i=1}^{4} y_i = 15$
$\sum_{i=1}^{4} y_i = 5$

We now have a simple [stars and bars problem](@entry_id:148883): distribute 5 "unused capacity units" among the 4 qubits. The number of ways to do this is:
$$ \binom{5+4-1}{4-1} = \binom{8}{3} = 56 $$
This powerful technique provides a shortcut for problems with uniform upper bounds where the total number of items is relatively high compared to the total capacity.

In summary, the principle of combinations with repetition is governed by a single, powerful mechanism. By modeling problems as the distribution of identical items into distinct bins and applying the [stars and bars method](@entry_id:152143), we can derive a simple formula. The true art of combinatorial problem-solving lies in identifying this underlying structure in diverse scenarios and skillfully adapting the model to handle various constraints through algebraic manipulation and clever changes of variables.