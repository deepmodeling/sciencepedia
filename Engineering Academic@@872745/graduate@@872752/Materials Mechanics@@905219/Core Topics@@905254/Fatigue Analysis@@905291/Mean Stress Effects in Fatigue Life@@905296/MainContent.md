## Introduction
In the field of [materials mechanics](@entry_id:189503), predicting the fatigue life of a component is a critical task for ensuring [structural integrity](@entry_id:165319) and reliability. While the amplitude of cyclic stress is a primary driver of fatigue damage, it alone is insufficient for an accurate assessment. The mean stress, or the static level about which the stress fluctuates, plays a profound and often decisive role. A tensile [mean stress](@entry_id:751819) can drastically reduce a component's life, whereas a compressive [mean stress](@entry_id:751819) can significantly extend it. This article addresses the crucial knowledge gap that exists between simplified [fatigue analysis](@entry_id:191624) and the reality of complex service loads by providing a comprehensive framework for understanding and quantifying [mean stress effects](@entry_id:202195).

Across the following chapters, you will gain a deep, practical understanding of this vital topic. The journey begins in **Principles and Mechanisms**, where we will decompose [stress cycles](@entry_id:200486) and introduce the classical [mean stress correction](@entry_id:181000) models—Goodman, Gerber, and Soderberg—visualizing them on the Haigh diagram and exploring the underlying physical mechanisms like [crack closure](@entry_id:191482) that explain their effects. Next, **Applications and Interdisciplinary Connections** will demonstrate how these theories are applied to solve real-world engineering problems, from analyzing complex load histories and surface-treated components to accounting for thermal and environmental factors. Finally, **Hands-On Practices** will provide an opportunity to solidify your knowledge by working through practical problems that mirror the challenges faced by design engineers.

## Principles and Mechanisms

In the study of [material fatigue](@entry_id:260667), the simple magnitude of cyclic stress is seldom sufficient to predict component life. Decades of empirical observation and theoretical development have demonstrated that the *mean* level about which the stress fluctuates plays a crucial role, particularly in the [high-cycle fatigue](@entry_id:159534) (HCF) regime. A positive (tensile) [mean stress](@entry_id:751819) is generally detrimental, reducing the fatigue life for a given [stress amplitude](@entry_id:191678), while a negative (compressive) mean stress is often beneficial. This chapter elucidates the fundamental principles used to quantify these effects and explores the underlying physical mechanisms that govern them.

### Decomposition of Cyclic Stress: Mean and Alternating Components

A steady-state cyclic stress history, regardless of its complexity, can be characterized for [fatigue analysis](@entry_id:191624) by its extreme values within a representative cycle: a maximum stress, $\sigma_{\max}$, and a minimum stress, $\sigma_{\min}$. While the peak stress $\sigma_{\max}$ is critical for assessing failure by static overload (i.e., whether the component will fail on the first application of the load), it does not, by itself, fully characterize the fatigue damage potential of the cycle. Fatigue is a process driven by cyclic [plastic deformation](@entry_id:139726) and damage accumulation, which is sensitive to both the range of the stress excursion and its mean level.

To properly account for these influences, the stress cycle is decomposed into two more fundamental quantities: the **mean stress**, $\sigma_m$, and the **alternating stress** (or [stress amplitude](@entry_id:191678)), $\sigma_a$. These are defined as:

$$ \sigma_{m} = \frac{\sigma_{\max} + \sigma_{\min}}{2} $$
$$ \sigma_{a} = \frac{\sigma_{\max} - \sigma_{\min}}{2} $$

The [mean stress](@entry_id:751819) represents the static component of the load, while the alternating stress represents the magnitude of the cyclic fluctuation about that mean. For instance, a loading cycle with $\sigma_{\min} = -80\,\text{MPa}$ and $\sigma_{\max} = 520\,\text{MPa}$ has a [mean stress](@entry_id:751819) of $\sigma_m = 220\,\text{MPa}$ and an alternating stress of $\sigma_a = 300\,\text{MPa}$ [@problem_id:2900912]. Two different loading cycles can have the same $\sigma_{\max}$ but vastly different fatigue lives if their $\sigma_{\min}$ values, and thus their $\sigma_m$ and $\sigma_a$ values, differ. The assertion that simply keeping $\sigma_{\max}$ below the material's [yield strength](@entry_id:162154) ($S_y$) guarantees infinite life is incorrect; [fatigue failure](@entry_id:202922) can and does occur at stress levels well below those required for macroscopic yielding [@problem_id:2900912]. The central task of mean [stress analysis](@entry_id:168804) is to predict the combinations of $\sigma_m$ and $\sigma_a$ that a component can safely withstand.

### Visualizing Mean Stress Effects: The Haigh Diagram

A powerful tool for visualizing the interplay between mean and alternating stress is the **Haigh diagram**. By convention, the [mean stress](@entry_id:751819) $\sigma_m$ is plotted on the horizontal axis (abscissa) and the alternating stress $\sigma_a$ is plotted on the vertical axis (ordinate). On this plane, any specific cyclic loading condition can be represented as a single point $(\sigma_m, \sigma_a)$.

The purpose of a [fatigue analysis](@entry_id:191624) considering [mean stress](@entry_id:751819) is to draw a boundary, or **failure locus**, on this diagram. This locus separates the plane into two regions: a "safe" region of infinite life and an "unsafe" region where failure is expected after a finite number of cycles. For any given mean stress $\sigma_m$, any alternating stress $\sigma_a$ that falls on or below this failure locus is considered safe for infinite life. Any combination above the locus is predicted to lead to failure [@problem_id:2659731].

The failure locus must be anchored by two physically meaningful endpoints.
1.  **The $\sigma_a$-axis intercept ($\sigma_m = 0$):** This corresponds to a fully reversed loading condition. The highest alternating stress a material can withstand for infinite life under these conditions is its **[endurance limit](@entry_id:159045)**, denoted $S_e$ (or $\sigma_e$). Thus, the failure locus must pass through the point $(0, S_e)$.
2.  **The $\sigma_m$-axis intercept ($\sigma_a = 0$):** This corresponds to a purely static load. Here, failure is governed by the material's static strength. Depending on the design philosophy, this could be the **[ultimate tensile strength](@entry_id:161506)**, $S_u$ (or $\sigma_u$), representing fracture, or the **tensile [yield strength](@entry_id:162154)**, $S_y$ (or $\sigma_y$), representing the onset of macroscopic [plastic deformation](@entry_id:139726).

The various [mean stress correction](@entry_id:181000) models are, in essence, different proposed functions for interpolating the failure locus between these two intercepts.

### Phenomenological Models for Infinite-Life Design

Several classical models have been developed to describe the failure locus in the Haigh diagram for tensile mean stresses ($\sigma_m \ge 0$). They are phenomenological, meaning they are formulated to fit experimental data rather than being derived entirely from first principles, but they embody distinct assumptions about material behavior.

#### The Goodman Criterion: A Linear Model Based on Ultimate Strength

The simplest non-trivial interpolation between the two fundamental intercepts is a straight line. The **modified Goodman criterion** (often simply called the Goodman criterion) defines the failure locus as a straight line connecting the endurance limit on the $\sigma_a$-axis to the [ultimate tensile strength](@entry_id:161506) on the $\sigma_m$-axis. The equation for this line is:

$$ \frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_u} = 1 $$

This relationship can be interpreted as a linear superposition of "utilizations". The term $\sigma_a / S_e$ represents the fraction of the material's fatigue life capacity consumed by the alternating stress, while $\sigma_m / S_u$ represents the fraction of its static strength capacity consumed by the [mean stress](@entry_id:751819). The Goodman criterion posits that failure occurs when the sum of these fractions equals unity [@problem_id:2659702]. It implicitly assumes that the degradation of fatigue strength due to [mean stress](@entry_id:751819) is a linear process terminating at the point of ultimate static fracture.

#### The Gerber Criterion: A Parabolic Refinement for Ductile Materials

While the Goodman criterion is simple and widely used, extensive experimental data for ductile metals, such as steels, show that their fatigue strength is somewhat less sensitive to mean stress than the linear model suggests. The failure data points often trace a curve that lies above the Goodman line. To better capture this behavior, the **Gerber criterion** proposes a [parabolic interpolation](@entry_id:173774) between the same two endpoints, $(0, S_e)$ and $(S_u, 0)$:

$$ \frac{\sigma_a}{S_e} + \left(\frac{\sigma_m}{S_u}\right)^2 = 1 $$

This equation defines a parabola that is tangent to the horizontal at the $\sigma_a$-axis and curves downward to meet the $\sigma_m$-axis at $S_u$. For any tensile [mean stress](@entry_id:751819) $0 \lt \sigma_m \lt S_u$, the Gerber criterion predicts a higher allowable alternating stress than the Goodman criterion, making it less conservative. Its motivation is purely empirical: it provides a more accurate fit to the observed "convex downward" shape of constant-life loci for many ductile materials [@problem_id:2659744].

#### The Soderberg Criterion: A Conservative Model Based on Yield Strength

In some engineering applications, any macroscopic [plastic deformation](@entry_id:139726) is unacceptable, as it can lead to a loss of dimensional tolerances, invalidate assumptions of elasticity in design, or compromise the function of components like bearings or precision gears. For such cases, a more conservative design philosophy is required. The **Soderberg criterion** provides this by constructing a failure locus that guards against yielding.

Like the Goodman criterion, it is a linear model, but it anchors the static failure point at the material's [yield strength](@entry_id:162154), $S_y$, instead of its ultimate strength. The equation is:

$$ \frac{\sigma_a}{S_e} + \frac{\sigma_m}{S_y} = 1 $$

This criterion's primary purpose is to ensure that the maximum stress in a cycle, $\sigma_{\max} = \sigma_m + \sigma_a$, never exceeds the yield strength. This strict requirement makes it the most conservative of the three classical models [@problem_id:2900949]. Its use is warranted in applications where maintaining geometric integrity is paramount, such as in aircraft primary structures, or where yielding could relax beneficial compressive residual stresses, for instance at the root of a notch in a rotating shaft [@problem_id:2900924].

### A Comparative Analysis of Classical Criteria

The differences between the Goodman, Gerber, and Soderberg criteria can be clearly understood by comparing their predictions for a given loading condition. For any material where $S_y  S_u$ (which is true for all ductile metals), and for any tensile mean stress $\sigma_m > 0$, the following hierarchy of allowable alternating stress holds:

$$ \sigma_a^{\text{Soderberg}}  \sigma_a^{\text{Goodman}}  \sigma_a^{\text{Gerber}} $$

This means that for predicting infinite life, **Soderberg is the most conservative criterion**, **Gerber is the least conservative**, and Goodman is intermediate.

Consider a steel with $S_u = 950\,\text{MPa}$, $S_y = 700\,\text{MPa}$, and $S_e = 400\,\text{MPa}$, subjected to a [mean stress](@entry_id:751819) of $\sigma_m = 300\,\text{MPa}$. The maximum allowable alternating stresses predicted by each criterion would be [@problem_id:2900894]:

*   **Soderberg:** $\sigma_a = 400 \left(1 - \frac{300}{700}\right) \approx 229\,\text{MPa}$
*   **Goodman:** $\sigma_a = 400 \left(1 - \frac{300}{950}\right) \approx 274\,\text{MPa}$
*   **Gerber:** $\sigma_a = 400 \left(1 - \left(\frac{300}{950}\right)^2\right) \approx 360\,\text{MPa}$

The choice of which criterion to use is a design decision that depends on the material, the application, and the acceptable level of risk. For brittle materials where $S_y \approx S_u$, the difference between the Soderberg and Goodman criteria becomes negligible [@problem_id:2900924]. For ductile materials, Gerber often best represents the actual fatigue behavior, while Goodman offers a simpler, more conservative linear approximation, and Soderberg provides a safeguard against any yielding.

### Physical Mechanisms of Mean Stress Effects

While the classical criteria provide useful design rules, they do not explain *why* [mean stress](@entry_id:751819) affects fatigue life. The underlying answer lies in the mechanics of crack initiation and propagation at the microstructural level.

#### The Role of Crack Closure and Effective Driving Force

Fatigue failure is fundamentally a process of crack growth, even from microscopic, pre-existing flaws. In the framework of Linear Elastic Fracture Mechanics (LEFM), the driving force for [crack propagation](@entry_id:160116) is the range of the [stress intensity factor](@entry_id:157604), $\Delta K = K_{\max} - K_{\min}$. However, this simple range is often an overestimation of the true driving force.

A key phenomenon known as **[crack closure](@entry_id:191482)** occurs where the crack faces make physical contact with each other even when the component is under a net tensile load. This can be caused by the [plastic deformation](@entry_id:139726) "wake" left behind a growing crack, the roughness of the fracture surfaces, or the formation of oxides within the crack. As a result, the crack does not become fully "open" at its tip until the applied stress exceeds a certain **opening stress**, $\sigma_{op}$. The portion of the loading cycle below $\sigma_{op}$ is ineffective at driving the crack forward.

This leads to the concept of an **[effective stress intensity factor](@entry_id:201687) range**, $\Delta K_{\text{eff}} = K_{\max} - K_{\text{op}}$ (where $K_{\text{op}}$ is the stress intensity at $\sigma_{op}$). Mean stress exerts its influence primarily by altering this effective driving force. A positive (tensile) mean stress $\sigma_m > 0$ helps to pull the crack faces apart, lowering the opening stress $\sigma_{op}$ and making a larger portion of the stress cycle effective in driving crack growth. This increases $\Delta K_{\text{eff}}$ for a given $\sigma_a$, accelerating crack growth and reducing fatigue life [@problem_id:2900909].

#### The Beneficial Influence of Compressive Mean Stress

Conversely, a negative (compressive) mean stress $\sigma_m  0$ has a strongly beneficial effect. The compressive [mean stress](@entry_id:751819) pushes the crack faces firmly together. A larger portion of the tensile alternating [stress amplitude](@entry_id:191678) is "used up" just to overcome this clamping force and open the crack. This significantly reduces the effective stress range $\Delta K_{\text{eff}}$ for a given $\sigma_a$, thereby slowing crack growth and increasing [fatigue life](@entry_id:182388).

This physical reasoning allows us to formulate a defensible criterion for the compressive mean stress regime. For a cycle where the crack is closed during the compressive portion, a reasonable approximation is that the crack opens as soon as the applied stress becomes tensile ($\sigma_{op} \approx 0$). In this scenario, the effective driving force, $\Delta K_{\text{eff}}$, becomes approximately equal to $K_{\max}$. The threshold for infinite life is met when this driving force is no greater than the threshold established by the fully reversed [endurance limit](@entry_id:159045), where $\sigma_{\max} = S_e$. Thus, the [fatigue limit](@entry_id:159178) criterion for $\sigma_m \le 0$ becomes [@problem_id:2659727]:

$$ \sigma_{\max} \le S_e \implies \sigma_a + \sigma_m \le S_e \implies \sigma_a \le S_e - \sigma_m $$

This equation describes a line with a slope of $-1$ extending into the compressive regime from the point $(0, S_e)$. It correctly captures the beneficial effect of compressive mean stress, predicting that the allowable alternating stress can be increased as the [mean stress](@entry_id:751819) becomes more compressive, until another failure mode, such as [buckling](@entry_id:162815) or compressive yielding, becomes dominant. This physically-based extension is generally preferred over simply assuming no benefit (i.e., clipping the Haigh diagram horizontally at $\sigma_a=S_e$ for all $\sigma_m  0$).

### Connecting Models to Microstructure and Surface Treatments

The relative accuracy of the phenomenological models (Goodman, Gerber, Soderberg) can be understood by considering how real-world conditions align with the physical mechanism of [crack closure](@entry_id:191482). Surface treatments, in particular, can drastically alter the local [mean stress](@entry_id:751819) and closure behavior.

Consider a high-strength steel component in two conditions: one mirror-polished and one shot-peened [@problem_id:2659708].
*   The **polished** specimen, tested in an inert environment, has minimal roughness- or oxide-induced closure. It is highly sensitive to the applied [mean stress](@entry_id:751819), as the [crack tip](@entry_id:182807) experiences the full effect of the loading cycle. For such high-strength, low-ductility materials, the linear, more aggressive penalty of the **Goodman** criterion often provides a better (or at least safer) fit than the less conservative Gerber parabola.
*   The **shot-peened** specimen has two critical differences. First, the peening process induces a deep layer of high-magnitude compressive [residual stress](@entry_id:138788) at the surface. This acts as a significant negative local mean stress, shielding the material from the applied tensile mean stress. Second, the increased surface roughness enhances closure. Both mechanisms make the component much less sensitive to the *applied* $\sigma_m$. The failure locus on the Haigh diagram becomes much flatter. The **Gerber** criterion, with its parabolic shape and zero slope at $\sigma_m=0$, provides a much better mathematical approximation for this muted sensitivity than the steeper [linear models](@entry_id:178302).

This comparison demonstrates that there is no single "best" model. The choice of an appropriate [mean stress](@entry_id:751819) criterion depends on a deep understanding of the material's [ductility](@entry_id:160108), the component's surface condition, the presence of residual stresses, and the governing design philosophy. The classical models serve as invaluable tools, but their application must be guided by an appreciation for the underlying physical principles of fatigue and fracture.