## Introduction
In fields from medicine to marketing, researchers often need to measure the effect of an intervention or compare two conditions. When the data involves paired observations—such as a patient's symptoms before and after treatment, or a user's preference for two different interfaces—and the outcome is a simple binary choice (e.g., 'Yes/No', 'Success/Failure'), standard statistical tests fall short. The inherent dependency between paired measurements violates the core assumptions of common methods like the Pearson's [chi-squared test](@entry_id:174175), creating a crucial knowledge gap in analysis.

This article introduces the McNemar test, an elegant and powerful tool specifically designed to navigate this challenge. It provides a robust framework for determining whether a statistically significant change has occurred between the two paired measurements. By reading this article, you will gain a comprehensive understanding of this essential statistical method. The **Principles and Mechanisms** section dissects the theoretical underpinnings of the test, revealing how it cleverly isolates change by focusing only on 'discordant' pairs. The **Applications and Interdisciplinary Connections** section showcases the test's versatility with real-world examples from public health, biomedical research, and even genomics. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through practical problems and applying the test to sample data.

## Principles and Mechanisms

In the analysis of experimental and observational data, we frequently encounter situations where measurements are taken on the same subject at two different points in time or under two different conditions. This study design, known as a **[paired design](@entry_id:176739)** or **repeated measures design**, is powerful because it controls for inter-subject variability. When the outcome of interest is a binary categorical variable, a specialized set of tools is required for analysis. The McNemar test is the canonical method for such scenarios.

### The Context of Paired Dichotomous Data

The McNemar test is specifically designed for analyzing **paired nominal data** where the outcome for each member of a pair is **dichotomous**, meaning it can take one of two possible values. Common examples of such data structures include:

*   **Pre-test/Post-test Studies:** A group of subjects is measured before and after an intervention. For instance, a panel of voters' preference for a candidate ("For" or "Against") is recorded before and after a debate [@problem_id:1933898], or public willingness to receive a vaccine ("Willing" or "Unwilling") is assessed before and after an educational campaign [@problem_id:1933876].

*   **Matched-Pair Studies:** Subjects are matched based on key characteristics (e.g., age, gender), and one member of each pair is assigned to a different treatment or condition. A classic example involves surveying married couples to see if spouses' preferences for a political candidate differ [@problem_id:1933869].

*   **Concurrent Comparisons:** The same subject is evaluated using two different methods or under two different conditions. For example, each participant in a study might use both an old and a new user interface, with task completion recorded as "Success" or "Failure" for each [@problem_id:1933905]. Similarly, every transaction in a dataset might be processed by two different fraud detection algorithms, with the outcome being "Flagged" or "Not Flagged" [@problem_id:1933884].

In all these cases, the two measurements for each pair (e.g., a single subject's before and after response) are not independent; they are linked by the common subject or pair. This intra-pair dependency is a fundamental feature of the data that must be accounted for in the statistical analysis.

To structure this data for analysis, we use a $2 \times 2$ [contingency table](@entry_id:164487). Let the two categorical outcomes be generically labeled as positive (+) and negative (-). The rows typically represent the outcome of the first measurement (or condition), and the columns represent the outcome of the second.

|                  | Measurement 2: +          | Measurement 2: -          | Row Total        |
|------------------|---------------------------|---------------------------|------------------|
| **Measurement 1: +** | $a$                       | $b$                       | $a+b$            |
| **Measurement 1: -** | $c$                       | $d$                       | $c+d$            |
| **Column Total**     | $a+c$                     | $b+d$                     | $N = a+b+c+d$    |

Here, the cell counts represent:
*   $a$: Number of pairs with a (+, +) outcome.
*   $b$: Number of pairs with a (+, -) outcome.
*   $c$: Number of pairs with a (-, +) outcome.
*   $d$: Number of pairs with a (-, -) outcome.
*   $N$: The total number of pairs.

### The Core Research Question: Testing for Marginal Homogeneity

The primary objective of the McNemar test is not to assess agreement or association, but to determine if there is a systematic change in the proportion of a specific outcome between the two paired measurements. This is known as a test of **marginal homogeneity**.

The "marginal" proportions refer to the overall proportion of positive outcomes for each measurement, which can be read from the margins of the table.
*   The proportion of positive outcomes for Measurement 1 is $P_1 = \frac{a+b}{N}$.
*   The proportion of positive outcomes for Measurement 2 is $P_2 = \frac{a+c}{N}$.

The fundamental research question that the McNemar test addresses is whether these two marginal proportions are equal in the population from which the sample was drawn [@problem_id:1933905]. The null hypothesis ($H_0$) and [alternative hypothesis](@entry_id:167270) ($H_1$) are therefore stated as:

$H_0: P_1 = P_2$
$H_1: P_1 \neq P_2$

This framework seeks to answer questions like: "Is there a significant difference between the proportion of participants who succeeded with the old UI and the proportion who succeeded with the new UI?" A simple comparison of these two proportions, however, would be misleading if it ignored the paired nature of the data.

### The Mechanism: Isolating Change with Discordant Pairs

The brilliance of the McNemar test lies in its mechanism for testing the hypothesis of marginal homogeneity. If we substitute the expressions for the marginal proportions into the null hypothesis, we get:

$H_0: \frac{a+b}{N} = \frac{a+c}{N}$

With simple algebra, this equation simplifies to:

$H_0: b = c$

This reveals a profound insight: the hypothesis of equal marginal proportions is mathematically equivalent to the hypothesis that the number of pairs that change from positive to negative ($b$) is equal to the number of pairs that change from negative to positive ($c$).

The cells $b$ and $c$ are known as the **[discordant pairs](@entry_id:166371)**, as they represent the pairs where the outcome changed between the two measurements [@problem_id:1933876]. For instance, in a vaccine sentiment study, these are the individuals who changed their minds, either from "Willing" to "Unwilling" ($b$) or from "Unwilling" to "Willing" ($c$).

Conversely, cells $a$ and $d$ are the **concordant pairs**. These are the pairs where the outcome remained the same (+,+ or -,-). As the algebraic simplification shows, these concordant pairs provide no information whatsoever about a change in the marginal proportions. Their responses were consistent across both measurements, so they cannot inform a question about systematic change. The test, therefore, logically and efficiently ignores them [@problem_id:1933894].

The entire inferential weight of the McNemar test rests on the comparison of the two types of discordance. The question of marginal homogeneity boils down to: "Among the pairs that showed a change, is the direction of change random, or is there a systematic shift in one direction over the other?"

### The Test Statistic

Under the [null hypothesis](@entry_id:265441) that there is no systematic difference between the two conditions, any observed change is due to random chance. This implies that for any pair that shows a change, the change from + to - is just as likely as a change from - to +. In other words, if we condition on the total number of [discordant pairs](@entry_id:166371), $b+c$, we would expect that $E(b) = E(c) = \frac{b+c}{2}$.

This framing allows us to view the problem as a simple binomial test. Out of $n_{discordant} = b+c$ total "changers", the count in cell $b$ (or $c$) can be tested against the null proportion of $0.5$. For a sufficiently large number of [discordant pairs](@entry_id:166371) (e.g., $b+c \ge 10$), this binomial test can be approximated using a [chi-squared distribution](@entry_id:165213).

The McNemar test statistic is the squared Z-score for the difference between the observed counts $b$ and $c$, and it is calculated using only the [discordant pairs](@entry_id:166371) [@problem_id:1933906]:

$\chi^2 = \frac{(b-c)^2}{b+c}$

This statistic is compared to a chi-squared ($\chi^2$) distribution with one degree of freedom. If the calculated $\chi^2$ value is large enough to exceed a critical threshold (corresponding to a small p-value, e.g., $p \lt 0.05$), we reject the [null hypothesis](@entry_id:265441) and conclude that there is a statistically significant difference in the marginal proportions.

For smaller sample sizes of [discordant pairs](@entry_id:166371), a **[continuity correction](@entry_id:263775)** is often applied to better approximate the discrete binomial distribution with the continuous chi-squared distribution:

$\chi^2_{corrected} = \frac{(|b-c|-1)^2}{b+c}$

If the number of [discordant pairs](@entry_id:166371) is very small, an **[exact binomial test](@entry_id:170573)** on the counts $b$ and $c$ is the most appropriate method.

### Key Assumptions and Proper Application

For the results of a McNemar test to be valid, certain assumptions must be met:

1.  **Paired Dichotomous Data:** The test is exclusively for designs with paired subjects or repeated measurements on a dichotomous nominal variable.
2.  **Independence of Pairs:** This is a critical and often misunderstood assumption. The test does *not* assume that the two measurements within a pair are independent. In fact, some level of correlation is expected. The crucial assumption is that the **pairs themselves are independent of one another**. The outcome for one subject or matched pair must not influence the outcome for any other subject or pair [@problem_id:1933862].
3.  **Sufficient Discordant Pairs:** For the chi-squared approximation to be reliable, the total number of [discordant pairs](@entry_id:166371), $b+c$, should not be too small. While there are varying rules of thumb, if $b+c \lt 10$, it is generally advisable to use an [exact binomial test](@entry_id:170573).

### Distinctions from Other Common Tests

Understanding what the McNemar test is requires understanding what it is not. Students often confuse it with other tests for [contingency tables](@entry_id:162738).

#### The McNemar Test vs. the Chi-Squared Test of Independence

A frequent error is to apply the standard Pearson's chi-squared [test of independence](@entry_id:165431) to paired data. This is fundamentally incorrect. The chi-squared [test of independence](@entry_id:165431) assumes that all observations in the table are independent. In a [paired design](@entry_id:176739), where each subject contributes two data points, this assumption is violated by definition [@problem_id:1933857]. For example, if analyzing satisfaction with two smartphone models rated by the same 250 users, constructing a table with 500 total observations and running a [chi-squared test](@entry_id:174175) would treat the data as if it came from 500 independent users, ignoring the fact that user-specific preferences link the ratings for the two phones. This inflates the sample size and leads to an invalid statistical conclusion. The McNemar test correctly handles the paired dependency.

#### The McNemar Test vs. Measures of Agreement (Cohen's Kappa)

Another important distinction is between testing for a systematic shift (McNemar) and measuring agreement (Cohen's Kappa). The McNemar test is designed to detect **asymmetric disagreement**. It answers the question: "When the two measurements disagree, does the disagreement tend to go in one direction more than the other?" A significant result indicates a directional shift.

Cohen's Kappa, on the other hand, measures the level of **agreement** between two raters or measurements, while correcting for agreement that would be expected by chance. It quantifies consistency. It is possible to have low agreement (low Kappa) but an insignificant McNemar test result if the disagreements are symmetric ($b \approx c$). Conversely, one could have high overall agreement but a significant McNemar test result if the relatively few disagreements are heavily skewed in one direction [@problem_id:1933898]. The two tests answer fundamentally different research questions.

### Statistical Power and Study Design

A final, crucial point concerns the [statistical power](@entry_id:197129) of the McNemar test. Since the [test statistic](@entry_id:167372) depends solely on the counts of [discordant pairs](@entry_id:166371), $b$ and $c$, the power of the test to detect an effect is driven primarily by the **number of [discordant pairs](@entry_id:166371)**, not the total sample size $N$.

Consider two studies comparing two machine learning models, both with a total sample size of $N=1000$ [@problem_id:1933912].
*   In Study 1, there are 45 items where the models disagree in one direction and 25 in the other ($b+c = 70$). The [test statistic](@entry_id:167372) is $\chi^2 = \frac{(45-25)^2}{70} \approx 5.71$.
*   In Study 2, there are 130 disagreements in one direction and 70 in the other ($b+c = 200$). The test statistic is $\chi^2 = \frac{(130-70)^2}{200} = 18.0$.

Despite having the same total sample size, the evidence for a difference between the models is far stronger in Study 2. This is because Study 2 contained many more instances of disagreement—the very data that provides information about a systematic difference. When designing a study that will be analyzed with the McNemar test, researchers must anticipate that only subjects who change their response will contribute to the test's power. A large study with very few changers may fail to detect a real effect.