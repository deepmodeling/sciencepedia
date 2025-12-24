## Introduction
How do we know if a weather forecast is any good? When predicting events that either happen or don't—like rainfall exceeding a critical threshold or a storm forming—we need a rigorous way to measure model performance. This is the domain of [categorical verification](@entry_id:1122129). While simple metrics like accuracy can be misleading, especially for rare events, the atmospheric sciences have developed sophisticated tools to quantify true predictive skill. This article addresses the need for robust evaluation by focusing on a cornerstone metric: the Equitable Threat Score (ETS).

This guide will equip you with a graduate-level understanding of [categorical verification](@entry_id:1122129). In the "Principles and Mechanisms" chapter, you will learn to build and interpret the foundational [contingency table](@entry_id:164487) and understand why equitable skill scores are essential, culminating in a deep dive into the derivation of the ETS. The "Applications and Interdisciplinary Connections" chapter will demonstrate how ETS is used in real-world scenarios, from evaluating precipitation forecasts and model upgrades to tackling challenges like spatial errors and ensemble predictions. Finally, the "Hands-On Practices" section provides targeted problems to solidify your ability to apply these concepts and calculate skill scores in practical situations.

## Principles and Mechanisms

In the evaluation of [numerical weather prediction](@entry_id:191656) (NWP) and climate models, a fundamental task is to quantify the correspondence between a model’s forecasts and the corresponding observations. When the event of interest is dichotomous—either it occurs or it does not (e.g., precipitation exceeding a certain threshold, a temperature dropping below freezing)—the process of evaluation is known as **[categorical verification](@entry_id:1122129)**. This chapter elucidates the core principles and mechanisms of [categorical verification](@entry_id:1122129), with a focus on developing a robust understanding of skill scores, particularly the widely used Equitable Threat Score (ETS).

### The Contingency Table: A Foundation for Categorical Verification

The cornerstone of [categorical verification](@entry_id:1122129) is the **$2 \times 2$ [contingency table](@entry_id:164487)**. For a set of $N$ forecast-observation pairs, each outcome can be classified into one of four mutually exclusive categories. These categories quantify the four possible outcomes of a binary forecast :

*   **Hits ($H$)**: The event was forecast to occur, and it did occur.
*   **Misses ($M$)**: The event was not forecast to occur, but it did occur.
*   **False Alarms ($F$)**: The event was forecast to occur, but it did not occur.
*   **Correct Negatives ($C$)**: The event was not forecast to occur, and it did not occur.

The total number of forecast-observation pairs is the sum of these four counts: $N = H + M + F + C$. These counts can be organized into a table that summarizes the [joint distribution](@entry_id:204390) of the forecast and observation outcomes:

|                    | Observed: Yes | Observed: No | **Forecast Total** |
| :----------------- | :-----------: | :----------: | :----------------: |
| **Forecast: Yes**  |      $H$      |     $F$      |       $H+F$        |
| **Forecast: No**   |      $M$      |     $C$      |       $M+C$        |
| **Observed Total** |     $H+M$     |    $F+C$     |        $N$         |

The row and column totals are known as the **marginal totals** or **marginals**. The sum of the first row, $H+F$, represents the total number of times the event was forecast. The sum of the first column, $H+M$, represents the total number of times the event was observed.

Under the common statistical assumption that the $N$ forecast-observation pairs are **[independent and identically distributed](@entry_id:169067) (IID)**, the vector of counts $(H, M, F, C)$ serves as a **[sufficient statistic](@entry_id:173645)** for the underlying joint probabilities of the four outcomes. This means that these four counts capture all the information available in the sample about the model's performance, assuming the IID model holds. Most standard verification scores, including the ETS, are functions of these counts precisely because of this property . It is important to acknowledge, however, that assumptions of IID may be violated in practice due to spatial or temporal correlations, or if the forecast system or event climatology changes across the sample (heterogeneity). In such cases, aggregating all data into a single [contingency table](@entry_id:164487) can obscure important details.

### Elementary Verification Metrics: A First Look at Performance

From the [contingency table](@entry_id:164487), we can derive several elementary metrics that provide an initial assessment of forecast quality.

A fundamental characteristic of the verification sample is the **observed base rate**, or climatology, which is the relative frequency of the event's occurrence. It is estimated as:
$$ p_o = \frac{H+M}{N} $$
Similarly, the **forecast base rate** is the relative frequency with which the model predicted the event:
$$ p_f = \frac{H+F}{N} $$

The relationship between these two base rates is captured by the **Frequency Bias**, or simply **Bias**, score :
$$ B = \frac{H+F}{H+M} = \frac{p_f}{p_o} $$
This score indicates whether the model tends to forecast the event more or less frequently than it is observed. A value of $B > 1$ indicates **overforecasting**, $B  1$ indicates **underforecasting**, and $B = 1$ means the forecast is **unbiased** in its frequency. It is crucial to understand that an unbiased forecast ($B=1$) is not necessarily a skillful one; a model can have the correct frequency of events but place them in all the wrong locations or times.

Other key metrics focus on conditional performance. The **Probability of Detection (POD)**, also known as the hit rate, measures what fraction of the observed events were correctly forecast:
$$ \mathrm{POD} = \frac{H}{H+M} $$
This is equivalent to the conditional probability $P(\text{forecast event} \mid \text{observed event})$. A high POD is desirable, but it can often be achieved at the expense of issuing many false alarms .

A complementary metric is the **Threat Score (TS)**, also known as the **Critical Success Index (CSI)**. It measures the fraction of correct event forecasts relative to the set of all cases where the event was either forecast *or* observed. This set is the union of the forecast-yes and observed-yes sets, and its size is $H+M+F$ .
$$ \mathrm{CSI} = \frac{H}{H+M+F} $$
The CSI is particularly useful as it penalizes both misses and false alarms, providing a more balanced view than POD alone.

### The Imperative for Skill: Why Basic Metrics Can Mislead

While the elementary metrics provide useful diagnostics, they can be misleading if interpreted in isolation, especially when dealing with rare or very common events. Consider the metric of **Accuracy**, defined as the proportion of all forecasts that were correct: $ACC = (H+C)/N$.

For a rare event, the number of correct negatives ($C$) will be overwhelmingly large. A trivial forecast that always predicts "no event" will have $H=0$ and $F=0$. Its accuracy will be $ACC = C/N = (N-M)/N$. If the event is rare, $M$ will be small relative to $N$, and the accuracy will be very close to 1, suggesting excellent performance. However, this forecast has zero ability to predict the event of interest. For example, in a sample of $N=10,000$ where an event occurs only 100 times ($H+M=100$), a "never-forecast" strategy would miss all 100 events ($M=100$) and correctly predict the 9,900 non-events ($C=9900$). The accuracy would be $9900/10000 = 0.99$, a deceptively high value for a useless forecast .

This illustrates the need for **skill scores**. A skill score measures the accuracy of a forecast relative to a baseline or reference forecast, such as random chance or [climatology](@entry_id:1122484). A skillful forecast is one that performs better than this reference.

Furthermore, a good skill score should be **equitable**. An equitable score assigns the same "no-skill" value (typically zero) to any non-informative forecast strategy, regardless of the event's base rate. For instance, the "always forecast yes" and "always forecast no" strategies should both receive a score of zero, irrespective of how common or rare the event is . This property prevents a score from being inflated purely due to the climatological frequency of the event.

### The Equitable Threat Score (ETS): A Rigorous Measure of Skill

The Equitable Threat Score (ETS), also known as the Gilbert Skill Score (GSS), is an equitable [skill score](@entry_id:1131731) based on the CSI. It is designed to measure the forecast skill in predicting the event above and beyond what would be expected from random chance.

The first step is to define the "random chance" reference. We consider a random forecast that is statistically independent of the observations but is constrained to have the same marginal frequencies—that is, the same forecast base rate ($p_f$) and observed base rate ($p_o$) as the actual data.

Under [statistical independence](@entry_id:150300), the probability of a joint event is the product of the marginal probabilities. Therefore, the probability of a hit occurring by chance is $p_o \times p_f$. The expected number of hits in $N$ trials due to random chance, denoted $H_r$, is:
$$ H_r = N \times p_o \times p_f = N \left( \frac{H+M}{N} \right) \left( \frac{H+F}{N} \right) = \frac{(H+M)(H+F)}{N} $$
This derivation is a cornerstone of constructing equitable scores  .

The ETS is constructed by subtracting these chance-expected hits from the actual hits in the numerator, and from the total "threatened" events in the denominator of the CSI formula :
$$ \mathrm{ETS} = \frac{H - H_r}{H + M + F - H_r} $$
This formulation ensures that the ETS has the essential properties of an equitable [skill score](@entry_id:1131731):

1.  **Zero Skill for Random Forecasts**: If the forecast performs no better than random chance, the number of observed hits will, on average, equal the number of hits expected by chance ($H = H_r$). In this case, the numerator becomes zero, and thus $\mathrm{ETS} = 0$, correctly indicating no skill .

2.  **Perfect Score of One**: For a perfect forecast, there are no misses or false alarms ($M=0, F=0$). In this scenario, the ETS formula simplifies to 1 (assuming a non-trivial case where $H0$ and $C0$).

3.  **Equitability**: The ETS assigns a score of 0 to constant forecasts (always-yes or always-no). For an always-yes forecast, $p_f=1$, which leads to $H_r = H$, making the ETS numerator zero. For an always-no forecast, $H=0$ and $p_f=0$, which leads to $H_r=0$, again making the ETS numerator zero. This holds regardless of the observed base rate $p_o$, satisfying the equitability criterion .

Let's consider an application. Suppose we are comparing two models, A and B, which both have a high Probability of Detection ($\mathrm{POD} = 0.7$). Model A, however, is more discerning and issues fewer false alarms than Model B.
- Model A: $H=84, M=36, F=180, C=700$ ($N=1000$)
- Model B: $H=84, M=36, F=360, C=520$ ($N=1000$)

Both have $\mathrm{POD} = 84/(84+36) = 0.7$. However, their ETS scores differ significantly. For Model A, $H_r = (120)(264)/1000 = 31.68$, giving $\mathrm{ETS}_A \approx 0.195$. For Model B, which has far more false alarms, $H_r = (120)(444)/1000 = 53.28$, giving a much lower $\mathrm{ETS}_B \approx 0.072$ . This illustrates how the ETS effectively penalizes the lower-quality forecast, even when a simpler metric like POD shows no difference.

The magnitude of the chance correction, $H_r$, determines how much the ETS will differ from the uncorrected CSI. The scores diverge substantially when $H_r$ is large, which occurs when events are common (high $H+M$) or when the model has a strong positive bias (high $H+F$). For rare events and unbiased forecasts, $H_r$ is small, and $\mathrm{ETS} \approx \mathrm{CSI}$ .

### Contextualizing ETS: Comparisons with Other Skill Scores

The ETS is a powerful and widely used tool, but its properties are best understood in comparison with other skill scores.

#### Heidke Skill Score (HSS)

The **Heidke Skill Score (HSS)** is another equitable score, but it is based on overall accuracy rather than the threat score. It measures the fractional improvement in accuracy over a random forecast. Its formula is:
$$ \mathrm{HSS} = \frac{(H+C) - E_{correct}}{N - E_{correct}} $$
where $E_{correct}$ is the number of correct forecasts (hits plus correct negatives) expected by chance, calculated from the marginals: $E_{correct} = \frac{(H+M)(H+F) + (F+C)(M+C)}{N}$.

The crucial difference between HSS and ETS lies in their treatment of correct negatives ($C$). The HSS explicitly includes $C$ in its measure of success ($H+C$), whereas the ETS formula does not explicitly contain $C$. For rare-event verification, this distinction is paramount. As we have seen, the large number of correct negatives can inflate accuracy-based scores. While HSS is chance-corrected, its reliance on $H+C$ makes it sensitive to the large magnitude of $C$. The ETS, by focusing only on event-relevant counts ($H, M, F$), provides a measure of skill that is not inflated by the large number of easy-to-predict non-events, making it a preferred score for rare-event verification .

#### Peirce Skill Score (PSS)

The **Peirce Skill Score (PSS)**, also known as the True Skill Statistic or Hanssen-Kuipers Discriminant, is defined based on conditional probabilities:
$$ \mathrm{PSS} = \mathrm{POD} - \mathrm{POFD} = \frac{H}{H+M} - \frac{F}{F+C} $$
where $\mathrm{POFD}$ is the Probability of False Detection (the false alarm rate). The PSS measures the forecast's ability to separate the "yes" cases from the "no" cases.

A key property of PSS is its **independence from the base rate**, assuming the model's underlying discrimination characteristics (POD and POFD) are constant. The ETS, in contrast, is sensitive to the base rate. In a scenario with a very rare event ($p_o \to 0$), a forecast with good discrimination ($POD  POFD$) will see its ETS approach zero, because the number of hits ($H$) becomes vanishingly small compared to the number of false alarms ($F$). The PSS, however, remains constant at $POD - POFD$. This means that for extremely rare events, ETS may suggest no skill, while PSS indicates that the model retains its ability to discriminate between events and non-events .

This does not invalidate ETS, but rather highlights that different skill scores measure different aspects of performance. The ETS measures skill in successfully predicting the location and timing of events in a way that is useful for practical applications (minimizing misses and false alarms), a task that becomes inherently harder as events become rarer. The PSS measures the more abstract quality of statistical discrimination. Both provide valuable, and complementary, insights into model performance.

In summary, the journey from the simple counts of a [contingency table](@entry_id:164487) to the nuanced interpretation of equitable skill scores like the ETS represents a progression toward a more rigorous and meaningful evaluation of forecast quality. By understanding the principles of chance correction and equitability, and by appreciating the distinct properties of different scores, we can develop a comprehensive and robust framework for the verification of NWP and climate models.