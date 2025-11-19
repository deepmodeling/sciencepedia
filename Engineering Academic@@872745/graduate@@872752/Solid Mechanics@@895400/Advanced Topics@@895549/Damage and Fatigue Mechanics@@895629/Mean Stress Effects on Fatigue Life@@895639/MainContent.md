## Introduction
In the study of [structural integrity](@entry_id:165319), fatigue is a primary cause of failure, occurring under cyclic loading at stresses well below the material's static strength. While initial analyses often focus on simplified, fully reversed [stress cycles](@entry_id:200486), most engineering components operate under more complex conditions where the stress fluctuates about a non-zero average, or mean, stress. This [mean stress](@entry_id:751819) has a profound, and often detrimental, effect on fatigue life, a critical factor that cannot be ignored in reliable design. This article addresses the fundamental problem of how to predict [fatigue life](@entry_id:182388) when both a cyclic [stress amplitude](@entry_id:191678) and a static [mean stress](@entry_id:751819) are present, bridging the gap between baseline material data and real-world loading scenarios.

Over the next three chapters, you will gain a comprehensive understanding of [mean stress effects](@entry_id:202195). The first chapter, **Principles and Mechanisms**, will introduce the foundational concepts for characterizing [stress cycles](@entry_id:200486) and present the classical empirical models—Goodman, Gerber, and Soderberg—used to quantify the combined effects of mean and alternating stress. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are applied to solve practical engineering problems, including the analysis of residual stresses, variable amplitude loading, and multiaxial states, and explore connections to fields like materials science and reliability engineering. Finally, the **Hands-On Practices** chapter will provide guided exercises to solidify your ability to apply these critical analysis techniques.

## Principles and Mechanisms

The fatigue life of a structural component is profoundly influenced by the nature of the cyclic stresses it experiences. While the previous chapter introduced the fundamental concepts of fatigue under fully reversed loading, most real-world engineering components are subjected to [stress cycles](@entry_id:200486) that are not symmetric about zero. The presence of a non-zero **mean stress** superposed on the cyclic [stress amplitude](@entry_id:191678) can significantly alter [fatigue life](@entry_id:182388), with tensile mean stresses being generally detrimental and compressive mean stresses being beneficial. This chapter elucidates the principles and mechanisms governing these effects, moving from foundational definitions to the classical empirical models used in design and finally to more advanced, physically-based damage parameters.

### Characterizing Cyclic Stress

To analyze the effect of [mean stress](@entry_id:751819), a fluctuating stress history must first be decomposed into its fundamental components. For any stable, repeating stress cycle, the two most critical values are the maximum stress, $\sigma_{\max}$, and the minimum stress, $\sigma_{\min}$. From these, we define two parameters that are central to [fatigue analysis](@entry_id:191624): the **mean stress**, $\sigma_m$, and the **alternating stress** (or [stress amplitude](@entry_id:191678)), $\sigma_a$.

The mean stress is the arithmetic average of the extreme stresses, representing the static component of the load:
$$ \sigma_m = \frac{\sigma_{\max} + \sigma_{\min}}{2} $$

The alternating stress is one-half of the stress range, representing the magnitude of the cyclic fluctuation:
$$ \sigma_a = \frac{\sigma_{\max} - \sigma_{\min}}{2} $$

Another useful parameter is the **[stress ratio](@entry_id:195276)**, $R$, defined as:
$$ R = \frac{\sigma_{\min}}{\sigma_{\max}} $$

A fully reversed load, as discussed in the context of baseline [endurance limit](@entry_id:159045) testing, corresponds to $R = -1$, which implies $\sigma_m = 0$. A static load corresponds to $R = 1$, where $\sigma_a = 0$.

Consider, for example, a structural member subjected to a simple sinusoidal stress history given by $\sigma(t) = \sigma_{0} + \Delta\sigma \sin(\omega t)$, where $\sigma_0$ is a static offset and $\Delta\sigma$ is the amplitude of the [sinusoid](@entry_id:274998). The maximum stress occurs when $\sin(\omega t) = 1$, giving $\sigma_{\max} = \sigma_0 + \Delta\sigma$, and the minimum stress occurs when $\sin(\omega t) = -1$, giving $\sigma_{\min} = \sigma_0 - \Delta\sigma$. Applying the definitions above, we find that the mean stress $\sigma_m$ is precisely the static offset $\sigma_0$, and the alternating stress $\sigma_a$ is the sinusoidal amplitude $\Delta\sigma$ [@problem_id:2659766]. The [stress ratio](@entry_id:195276) for this cycle is $R = (\sigma_0 - \Delta\sigma) / (\sigma_0 + \Delta\sigma)$.

It is a common misconception in introductory mechanics to assume that preventing static failure is sufficient for ensuring structural integrity. For instance, one might believe that if the maximum stress in a cycle remains below the material's [yield strength](@entry_id:162154) ($S_y$), i.e., $\sigma_{\max}  S_y$, then infinite life is guaranteed. This is fundamentally incorrect. Fatigue is a process of cumulative damage initiated by [cyclic plasticity](@entry_id:176411), often on a microstructural scale, which can occur even when the macroscopic stresses are within the elastic range. The purpose of mean [stress analysis](@entry_id:168804) is precisely to quantify how the combination of $\sigma_m$ and $\sigma_a$ governs fatigue life, even when $\sigma_{\max}$ is well below $S_y$ [@problem_id:2900912]. Therefore, $\sigma_{\max}$ alone is an insufficient descriptor of the fatigue damage potential of a stress cycle; both $\sigma_m$ and $\sigma_a$ are essential.

### The Haigh Diagram: A Framework for Mean Stress Analysis

To visualize the combined effect of mean and alternating stress on [fatigue life](@entry_id:182388), engineers use a graphical tool known as the **Haigh diagram**. By convention, the [mean stress](@entry_id:751819), $\sigma_m$, is plotted on the horizontal axis (abscissa), and the alternating stress, $\sigma_a$, is plotted on the vertical axis (ordinate) [@problem_id:2659731].

On this diagram, a failure locus is drawn to represent the boundary between "safe" and "unsafe" combinations of $\sigma_m$ and $\sigma_a$ for a given design life (often infinite life in [high-cycle fatigue](@entry_id:159534)). Any stress state $(\sigma_m, \sigma_a)$ that falls on or below this line is predicted to be safe, while any point above the line is predicted to lead to failure. For any given [mean stress](@entry_id:751819), a smaller alternating stress corresponds to a longer life, hence the safe region lies below the failure curve [@problem_id:2659731].

The construction of any failure locus is anchored by two physically meaningful points corresponding to the limits of pure static and pure fatigue loading:

1.  **The $\sigma_a$-axis intercept**: This point corresponds to the case of zero [mean stress](@entry_id:751819) ($\sigma_m = 0$), which is a fully reversed loading condition. The maximum allowable alternating stress for infinite life in this case is, by definition, the material's **endurance limit**, denoted $S_e$. Thus, the failure locus must pass through the point $(0, S_e)$.

2.  **The $\sigma_m$-axis intercept**: This point corresponds to the case of zero alternating stress ($\sigma_a = 0$), which is a purely static load. Failure is governed by the material's static strength. The intercept is therefore a static strength property, typically either the **[ultimate tensile strength](@entry_id:161506)**, $S_u$, or the **[yield strength](@entry_id:162154)**, $S_y$.

The various [mean stress correction](@entry_id:181000) models discussed in the next section can be understood as different mathematical proposals for drawing the failure curve between these two fundamental intercepts.

### Empirical Models for Mean Stress Correction

The most widely used [mean stress](@entry_id:751819) criteria are empirical relationships that have been found to provide reasonable and often conservative predictions for many materials. They represent different assumptions about the shape of the failure locus on the Haigh diagram.

#### The Modified Goodman Criterion

The **modified Goodman criterion** assumes a linear relationship between the damaging effects of mean and alternating stresses. It proposes that the failure locus is a straight line connecting the [endurance limit](@entry_id:159045) on the $\sigma_a$-axis to the [ultimate tensile strength](@entry_id:161506) on the $\sigma_m$-axis [@problem_id:2659702]. The equation of this line is:
$$ \frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_u} = 1 $$

The underlying rationale for this [linear form](@entry_id:751308) can be interpreted as a superposition of normalized stress "utilizations." The term $\sigma_a/S_e$ represents the fraction of the material's fatigue strength consumed by the alternating stress, while $\sigma_m/S_u$ represents the fraction of its static ultimate strength consumed by the mean stress. Failure is predicted to occur when the sum of these fractions equals one [@problem_id:2659702]. The choice of $S_u$ as the [static limit](@entry_id:262480) makes this model suitable for describing failure by fracture.

#### The Gerber Criterion

Extensive experimental data, particularly for ductile steels, show that the Goodman line can be overly conservative. The actual failure locus is often a convex curve that lies above the Goodman line. The **Gerber criterion** accounts for this by proposing a parabolic failure locus that connects the same two endpoints, $(0, S_e)$ and $(S_u, 0)$ [@problem_id:2659744]. Its equation is:
$$ \frac{\sigma_a}{S_e} + \left(\frac{\sigma_m}{S_u}\right)^2 = 1 $$

The quadratic term in mean stress, $(\sigma_m/S_u)^2$, means that for small tensile mean stresses, the reduction in allowable alternating stress is less severe than that predicted by the linear Goodman model. Because the Gerber curve lies above the Goodman line for all tensile mean stresses $0  \sigma_m  S_u$, it is considered **less conservative** and often provides a more accurate fit to experimental data for ductile materials.

#### The Soderberg Criterion

In some applications, any amount of plastic deformation is unacceptable. To create a more conservative design that guards against yielding, the **Soderberg criterion** was proposed. Like the Goodman model, it assumes a linear failure locus. However, it conservatively uses the material's yield strength, $S_y$, as the static failure limit on the mean stress axis [@problem_id:2659764]. The equation is:
$$ \frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_y} = 1 $$

This relation ensures that the maximum stress in the cycle, $\sigma_{\max} = \sigma_m + \sigma_a$, will not exceed the [yield strength](@entry_id:162154) (a condition known as the Langer yield line). Since for all engineering metals $S_y  S_u$, the Soderberg line lies below the Goodman line on the Haigh diagram, making it the **most conservative** of the three classical criteria.

### A Comparative Analysis of Mean Stress Criteria

The choice of [mean stress](@entry_id:751819) criterion has significant implications for design. For any given tensile mean stress, the three models will predict different allowable alternating stresses. Because $S_y  S_u$, it is always true that for a positive $\sigma_m$, $\sigma_m/S_y > \sigma_m/S_u$. Furthermore, for any value $x$ between $0$ and $1$, $x^2 \le x$, which implies $(\sigma_m/S_u)^2 \le \sigma_m/S_u$. From these mathematical facts, the ordering of the allowable alternating stress, $\sigma_a^{\text{allowable}}$, predicted by the three models for any given tensile mean stress is:
$$ \sigma_a^{\text{Soderberg}} \le \sigma_a^{\text{Goodman}} \le \sigma_a^{\text{Gerber}} $$

This confirms the order of conservatism: Soderberg (most conservative), Goodman (intermediate), and Gerber (least conservative) [@problem_id:2900894].

To illustrate this, consider a high-strength steel with $S_u = 950 \text{ MPa}$, $S_y = 700 \text{ MPa}$, and a fully corrected [endurance limit](@entry_id:159045) $S_e = 400 \text{ MPa}$. If a component made from this material is subjected to a tensile mean stress of $\sigma_m = 300 \text{ MPa}$, we can calculate the maximum allowable alternating stress for infinite life according to each criterion:

-   **Soderberg:** $\sigma_a = S_e \left(1 - \frac{\sigma_m}{S_y}\right) = 400 \left(1 - \frac{300}{700}\right) \approx 229 \text{ MPa}$
-   **Goodman:** $\sigma_a = S_e \left(1 - \frac{\sigma_m}{S_u}\right) = 400 \left(1 - \frac{300}{950}\right) \approx 274 \text{ MPa}$
-   **Gerber:** $\sigma_a = S_e \left(1 - \left(\frac{\sigma_m}{S_u}\right)^2\right) = 400 \left(1 - \left(\frac{300}{950}\right)^2\right) \approx 360 \text{ MPa}$

The results clearly demonstrate that the choice of model can lead to vastly different design limits [@problem_id:2900894].

An alternative method for assessing safety is to calculate a **[factor of safety](@entry_id:174335)**, $n$, for a given loading condition $(\sigma_m, \sigma_a)$. The design equations are modified to include $n$:
$$ \frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_u} = \frac{1}{n_{\text{Goodman}}} \quad \quad \text{and} \quad \quad \frac{\sigma_a}{S_e} + \left(\frac{\sigma_m}{S_u}\right)^2 = \frac{1}{n_{\text{Gerber}}} \quad \quad \text{etc.} $$
A [factor of safety](@entry_id:174335) $n > 1$ indicates a safe design for infinite life. For a loading condition with $\sigma_a = 300 \text{ MPa}$ and $\sigma_m = 220 \text{ MPa}$ on a material with $S_u = 900 \text{ MPa}$, $S_y = 600 \text{ MPa}$, and $S_e = 400 \text{ MPa}$, the safety factors would be $n_{\text{Soderberg}} \approx 0.90$ (predicting failure), $n_{\text{Goodman}} \approx 1.01$ (predicting marginal safety), and $n_{\text{Gerber}} \approx 1.24$ (predicting safety with a larger margin) [@problem_id:2900912].

A third perspective is to define an **equivalent fully reversed stress**, $\sigma_{a, \text{eq}}$. This is the [stress amplitude](@entry_id:191678) of a fully reversed cycle ($R=-1$) that would be equally damaging as the actual cycle with non-zero [mean stress](@entry_id:751819). For the Goodman criterion, this is:
$$ \sigma_{a, \text{eq}} = \frac{\sigma_a}{1 - \sigma_m/S_u} $$
The design is considered safe if this [equivalent stress](@entry_id:749064) is less than the material's endurance limit, $\sigma_{a, \text{eq}} \le S_e$. Using the previous example, the [equivalent stress](@entry_id:749064) is $\sigma_{a, \text{eq}} \approx 397 \text{ MPa}$. Since this is less than $S_e=400 \text{ MPa}$, the Goodman criterion again predicts the design is safe [@problem_id:2900912].

### Advanced Considerations and Physical Mechanisms

The classical mean stress models are powerful design tools, but they are empirical simplifications. A deeper understanding requires examining the underlying physical mechanisms of fatigue damage and how they are influenced by mean stress.

#### The Role of Compressive Mean Stress and Crack Closure

What happens when the mean stress is compressive ($\sigma_m  0$)? If we were to extrapolate the unmodified Goodman or Gerber equations into this regime, they would predict that the allowable alternating stress $\sigma_a$ could be greater than the baseline [endurance limit](@entry_id:159045) $S_e$. While compressive mean stresses are indeed beneficial to fatigue life, relying on this predicted increase is often considered non-conservative in design practice [@problem_id:2659736].

The physical reason for the benefit of compressive [mean stress](@entry_id:751819) is linked to the phenomenon of **[crack closure](@entry_id:191482)**. Fatigue cracks propagate only when they are open, allowing the crack tip to experience tensile stresses. When a load cycle includes a compressive portion, the crack faces are pressed together. Even as the load becomes tensile again, a portion of the tensile cycle is spent just reopening the crack. This means the crack tip is shielded from the full applied stress range. The **effective stress intensity range**, which is what actually drives crack growth, is reduced. A compressive [mean stress](@entry_id:751819) keeps the crack closed for a larger portion of the cycle, thus strongly reducing the [effective stress](@entry_id:198048) range and retarding crack growth [@problem_id:2659736].

Due to uncertainties in quantifying this effect, a common and conservative design approach is to "clip" the Haigh diagram. For any compressive mean stress, the allowable alternating stress is simply capped at the baseline [endurance limit](@entry_id:159045), $\sigma_a \le S_e$. This is mathematically implemented by replacing $\sigma_m$ in the design equations with $\sigma_m^+ = \max(\sigma_m, 0)$. The clipped Goodman criterion, for example, becomes:
$$ \frac{\sigma_a}{S_e} + \frac{\max(\sigma_m, 0)}{S_u} \le 1 $$
Under this rule, a loading cycle with $\sigma_m = -120 \text{ MPa}$ would be treated as if $\sigma_m = 0$, and the allowable alternating stress would simply be $\sigma_a = S_e$ [@problem_id:2659736].

#### Mechanistic Basis for Model Selection

The relative accuracy of the Goodman, Gerber, and Soderberg models depends on the material's behavior and the specific loading environment, which in turn are linked to microstructural mechanisms like [crack closure](@entry_id:191482) [@problem_id:2659708].

For high-strength, low-ductility materials tested in inert environments where [crack closure](@entry_id:191482) is minimal, a tensile [mean stress](@entry_id:751819) is highly detrimental. The crack remains open for most of the cycle, and the crack tip experiences the full effect of the [mean stress](@entry_id:751819). In such cases, the linear and more punitive penalty of the **Goodman** model often provides a more realistic prediction than the less conservative Gerber parabola.

Conversely, for more ductile materials, or in conditions that promote [crack closure](@entry_id:191482) (e.g., [shot peening](@entry_id:272056) which induces compressive residual stress, or testing in ambient air which causes oxide formation on crack faces), the material becomes less sensitive to the applied mean stress. The compressive [residual stress](@entry_id:138788) effectively lowers the [mean stress](@entry_id:751819) experienced by the crack, and the closure mechanisms shield the [crack tip](@entry_id:182807). This "muted" sensitivity is better captured by the "flatter" curve of the **Gerber** model, which has a zero slope at $\sigma_m = 0$ and imposes a weaker penalty for small-to-moderate mean stresses [@problem_id:2659708].

#### Energy-Based Damage Parameters: The Smith-Watson-Topper Model

More modern [fatigue analysis](@entry_id:191624) methods move beyond simple empirical curve fits and attempt to formulate damage parameters based on [physical quantities](@entry_id:177395) like [strain energy](@entry_id:162699) or work. One of the most successful is the **Smith-Watson-Topper (SWT) parameter**, which was proposed based on the idea that fatigue damage on a critical plane is driven by a combination of the maximum tensile stress and the cyclic strain amplitude on that plane [@problem_id:2659747]. The parameter is defined as:
$$ P_{SWT} = \sigma_{\max} \epsilon_a $$
where $\epsilon_a$ is the strain amplitude. For a constant fatigue life, the value of $P_{SWT}$ must remain constant.

The SWT parameter naturally incorporates [mean stress effects](@entry_id:202195). In the elastic regime, where $\epsilon_a = \sigma_a/E$, the parameter becomes $P_{SWT} = (\sigma_m + \sigma_a)(\sigma_a/E)$. It is clear that a positive mean stress $\sigma_m$ increases the value of the parameter for a given $\sigma_a$, correctly indicating an increase in damage and a reduction in life. The constant-life criterion is found by equating the parameter to its value under fully reversed loading (where $\sigma_m=0$ and $\sigma_a$ equals the fatigue strength for a given life):
$$ (\sigma_m + \sigma_a)\sigma_a = \sigma_{a,R=-1}^2 $$
For infinite life, this becomes $(\sigma_m + \sigma_a)\sigma_a = S_e^2$.

This equation defines a hyperbolic-like failure locus on the Haigh diagram. A Taylor series expansion for small mean stress reveals that this curve can be approximated by a line with a slope of $-1/2$: $\sigma_a \approx S_e - \sigma_m/2$. This initial slope is comparable to the slope of the Goodman line, $-S_e/S_u$, under the common condition that $S_u \approx 2 S_e$ for [high-cycle fatigue](@entry_id:159534) [@problem_id:2659747].

The SWT model also makes a strong prediction for compressive mean stresses. If $\sigma_m$ is sufficiently negative such that $\sigma_{\max} = \sigma_m + \sigma_a \le 0$, the stress cycle is entirely compressive. The SWT parameter becomes zero or negative, implying zero fatigue damage and infinite life. This represents a much stronger beneficial effect than the simple "clipping" of the Goodman diagram and highlights the ability of physically-based models to capture more complex material responses [@problem_id:2659747].