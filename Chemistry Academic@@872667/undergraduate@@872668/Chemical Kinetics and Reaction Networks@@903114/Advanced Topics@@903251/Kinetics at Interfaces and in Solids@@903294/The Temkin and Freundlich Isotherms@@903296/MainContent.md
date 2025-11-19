## Introduction
Adsorption, the process by which molecules accumulate on a surface, is fundamental to countless natural and industrial processes. While simple models like the Langmuir isotherm provide a foundational understanding based on ideal, uniform surfaces, they often fall short when describing the complexity of real-world systems. Most materials used in practice, from industrial catalysts to environmental sorbents, possess heterogeneous surfaces with a wide spectrum of adsorption site energies and potential interactions between adsorbed molecules. This discrepancy creates a significant knowledge gap, necessitating more sophisticated models to accurately predict and engineer adsorption processes.

This article delves into two of the most important non-ideal [adsorption models](@entry_id:184889): the Temkin and Freundlich [isotherms](@entry_id:151893). By moving beyond ideal assumptions, these models provide a more realistic framework for understanding adsorption on complex surfaces. The following chapters will guide you through a comprehensive exploration of these powerful tools. In **Principles and Mechanisms**, you will learn the mathematical formulation and underlying physical assumptions of each isotherm, as well as their inherent limitations. Following that, **Applications and Interdisciplinary Connections** will demonstrate their practical utility in fields like [heterogeneous catalysis](@entry_id:139401), environmental science, and [materials engineering](@entry_id:162176). Finally, **Hands-On Practices** will provide opportunities to apply these concepts to analyze experimental data and solve practical problems.

## Principles and Mechanisms

The Langmuir isotherm, predicated on the ideal assumptions of a perfectly uniform surface and no interactions between adsorbed molecules, provides a fundamental starting point for understanding adsorption. However, real-world surfaces, particularly those of industrial catalysts, soils, and porous materials, are rarely uniform. They are characterized by a complex topography and chemical composition, leading to a spectrum of adsorption sites with varying affinities for adsorbate molecules. Furthermore, as surface coverage increases, interactions between neighboring adsorbates can become significant. To describe these more complex, non-ideal systems, alternative isotherm models have been developed. This chapter explores two of the most widely used models: the Freundlich isotherm and the Temkin isotherm.

### The Freundlich Isotherm: An Empirical Model for Heterogeneous Surfaces

The Freundlich isotherm is an early [empirical formula](@entry_id:137466) that has proven remarkably successful in fitting [adsorption](@entry_id:143659) data on heterogeneous surfaces over an intermediate range of pressures or concentrations.

#### Mathematical Formulation and Parameters

The Freundlich isotherm relates the [amount of substance](@entry_id:145418) adsorbed to the equilibrium pressure or concentration via a power-law relationship. For gas-phase [adsorption](@entry_id:143659), it is often written in terms of fractional surface coverage $\theta$ and partial pressure $P$:

$$ \theta = k P^{1/n} $$

For adsorption from a solution, the equation takes the form:

$$ q_e = K_F c_e^{1/n} $$

In these equations, $q_e$ represents the amount of adsorbate adsorbed per unit mass of the adsorbent (e.g., in mg/g), and $c_e$ is the equilibrium concentration of the adsorbate in the solution (e.g., in mg/L). The parameters are:
- **$K_F$ (or $k$)**: The **Freundlich capacity constant**, which is related to the adsorption capacity and the affinity of the adsorbate for the surface. A larger $K_F$ value generally indicates a greater adsorption capacity.
- **$1/n$**: The **heterogeneity index**, a dimensionless parameter that indicates the favorability of the adsorption process and the degree of [surface heterogeneity](@entry_id:180832). For most [physical adsorption](@entry_id:170714) systems, the value of $n$ is greater than 1, meaning $0  1/n  1$.

To determine these parameters from experimental data, the equation is typically linearized by taking the natural logarithm:

$$ \ln(q_e) = \ln(K_F) + \frac{1}{n} \ln(c_e) $$

This equation is in the form of a straight line, $y = m x + b$. By plotting $\ln(q_e)$ versus $\ln(c_e)$, one can obtain a straight line where the slope is the heterogeneity index $1/n$ and the y-intercept is $\ln(K_F)$.

For example, consider an experiment studying pesticide adsorption on soil [@problem_id:1525274]. If at an equilibrium concentration $c_{e1} = 0.50$ mg/L, the adsorbed amount is $q_{e1} = 1.20$ mg/g, and at $c_{e2} = 5.00$ mg/L, the adsorbed amount is $q_{e2} = 4.80$ mg/g, we can calculate the heterogeneity index without a full plot. By subtracting the linearized equations for two data points, we find:

$$ \frac{1}{n} = \frac{\ln(q_{e2}/q_{e1})}{\ln(c_{e2}/c_{e1})} = \frac{\ln(4.80/1.20)}{\ln(5.00/0.50)} = \frac{\ln(4)}{\ln(10)} \approx 0.602 $$

The value of the heterogeneity index $1/n$ provides insight into the nature of the adsorption. If $1/n = 1$, the equation reduces to a [linear relationship](@entry_id:267880), suggesting a highly uniform surface. As $1/n$ approaches 0, the surface is considered increasingly heterogeneous, with a wide distribution of site energies.

#### Theoretical Justification and Physical Interpretation

While originally empirical, the Freundlich isotherm can be theoretically justified by assuming that the [heat of adsorption](@entry_id:199302) decreases exponentially with increasing surface coverage. A more intuitive physical picture involves a surface with a distribution of [adsorption](@entry_id:143659) sites possessing different binding energies. The model assumes an exponential distribution of site energies, where there are many low-energy sites and progressively fewer high-energy sites. Adsorption proceeds by filling the highest-energy sites first. As pressure increases, molecules begin to occupy the more abundant, lower-energy sites.

A more sophisticated justification arises from modeling the adsorbent surface as a **fractal object** [@problem_id:1525240]. If we assume the number of sites with a given [adsorption energy](@entry_id:180281) $q$ follows an exponential distribution, $\rho(q) \propto \exp(-q/q_0)$, and that adsorption on each individual site follows a local Langmuir model, we can derive the Freundlich isotherm. By using an approximation where sites are either fully occupied ($\theta(q) \approx 1$) or empty ($\theta(q) \approx 0$), one can show that the overall coverage is a [power function](@entry_id:166538) of pressure. This derivation connects the empirical exponent $1/n$ to fundamental physical properties, such as the surface's fractal dimension $D_f$ and the absolute temperature $T$, yielding an expression like $1/n \propto T / (D_f - 2)$. This theoretical underpinning transforms the Freundlich equation from a mere curve-fitting tool into a model with a plausible physical basis rooted in [surface heterogeneity](@entry_id:180832).

#### Limitations of the Freundlich Model

Despite its utility, the Freundlich isotherm has significant theoretical limitations that make it physically unrealistic at very low and very high pressures [@problem_id:1525234].

1.  **Failure to Predict Saturation**: The model predicts that the amount adsorbed increases indefinitely with pressure or concentration. As $P \to \infty$, $\theta = k P^{1/n} \to \infty$. This violates the physical reality that any surface has a finite number of adsorption sites, and thus the coverage must approach a saturation limit (i.e., $\theta \le 1$ for a monolayer).

2.  **Violation of Henry's Law**: At sufficiently low pressures, where adsorbate-adsorbate interactions are negligible, the adsorption process should become directly proportional to pressure. This [linear relationship](@entry_id:267880) is known as **Henry's Law**, and a thermodynamically consistent model must exhibit $\theta \propto P$ as $P \to 0$. The Freundlich model fails this test. The ratio $\theta/P = kP^{(1/n)-1}$ does not approach a finite constant. Since $n>1$, the exponent $(1/n)-1$ is negative, causing the ratio to diverge to infinity as $P \to 0$ [@problem_id:1525297]. This thermodynamic inconsistency at low pressures means the Freundlich isotherm should only be applied over an intermediate pressure range where it has been experimentally validated.

### The Temkin Isotherm: A Model for Linear Decay in Adsorption Energy

Like the Freundlich model, the Temkin isotherm was developed to describe adsorption on heterogeneous surfaces. However, it is based on a different core assumption about the energetics of the process.

#### Core Assumption and Formulation

The fundamental premise of the Temkin model is that the **[heat of adsorption](@entry_id:199302) decreases linearly with increasing [surface coverage](@entry_id:202248)**. This can be expressed as:

$$ q_{st}(\theta) = q_0 - C\theta $$

where $q_{st}(\theta)$ is the [isosteric heat of adsorption](@entry_id:151208) at coverage $\theta$, $q_0$ is the [heat of adsorption](@entry_id:199302) on the bare surface ($\theta=0$), and $C$ is a positive constant characterizing the [surface heterogeneity](@entry_id:180832) or the strength of repulsive interactions between adsorbates. This assumption implies that the first molecules to adsorb occupy the most favorable, high-energy sites. Subsequent molecules are forced to occupy progressively weaker sites or experience repulsion from already adsorbed neighbors, leading to a lower [heat of adsorption](@entry_id:199302) [@problem_id:1525292].

This energetic assumption leads to an isotherm equation where the coverage varies logarithmically with pressure, typically expressed for an intermediate coverage range:

$$ \theta = \frac{RT}{b_T} \ln(A_T P) $$

Here, $R$ is the ideal gas constant, $T$ is the absolute temperature, and $A_T$ and $b_T$ are Temkin constants. The constant $b_T$ is directly related to the change in [adsorption energy](@entry_id:180281) with coverage (corresponding to the constant $C$ in the [heat of adsorption](@entry_id:199302) equation). The constant $A_T$ is related to the binding energy of the most energetic sites.

#### Thermodynamic Analysis and Application

The link between the Temkin isotherm's mathematical form and its underlying energetic assumption can be rigorously established using the Clausius-Clapeyron equation for adsorption, which defines the [isosteric heat of adsorption](@entry_id:151208) $q_{st}$:

$$ \left( \frac{\partial \ln P}{\partial T} \right)_{\theta} = \frac{q_{st}}{RT^2} $$

By rearranging the Temkin isotherm to solve for $\ln(P)$ and performing the [partial differentiation](@entry_id:194612) with respect to $T$ at constant $\theta$, one can derive the expression for $q_{st}$. This derivation confirms that the Temkin equation indeed corresponds to a [heat of adsorption](@entry_id:199302) that decreases linearly with coverage, as expressed by $q_{st} = q_0 - C\theta$ [@problem_id:15308].

This coverage-dependent enthalpy has direct consequences for the total heat released during an adsorption process. To find the total heat, $Q$, released as the coverage increases from 0 to a final value $\theta_f$, one must integrate the molar [enthalpy of adsorption](@entry_id:171774) over the number of moles adsorbed [@problem_id:1525299]. This yields:

$$ Q = -N_{\text{sites}} \int_{0}^{\theta_f} \Delta H_{ads}(\theta) \,d\theta = -N_{\text{sites}}\left[ \Delta H_{ads,0}\,\theta_{f} + \frac{\Delta H_{ads,1}-\Delta H_{ads,0}}{2}\,\theta_{f}^{2} \right] $$

where $\Delta H_{ads}$ is the molar [enthalpy of adsorption](@entry_id:171774) (note: $q_{st} = -\Delta H_{ads}$ for an ideal gas) and $N_{\text{sites}}$ is the total molar capacity of the surface.

In practice, the Temkin parameters can be found by plotting experimental data of $\theta$ versus $\ln(P)$. This should yield a straight line with a slope $S = RT/b_T$. This relationship reveals a key feature of the model: the slope of the linearized plot is directly proportional to the absolute temperature [@problem_id:1525269]. If experiments are run at two temperatures, $T_1$ and $T_2$, the corresponding slopes will be related by $S_2/S_1 = T_2/T_1$, assuming the parameter $b_T$ is temperature-independent.

#### Limitations of the Temkin Model

The Temkin isotherm shares a key limitation with the Freundlich model: it does not predict surface saturation. As $P \to \infty$, the logarithmic term grows without bound, leading to an infinite predicted coverage.

However, its most severe limitation occurs at low pressures [@problem_id:1525257]. As the pressure $P$ approaches zero, $\ln(P)$ approaches $-\infty$. Consequently, the model predicts a physically impossible negative [surface coverage](@entry_id:202248). This means the Temkin isotherm is fundamentally invalid at low pressures and, like the Freundlich model, should only be used to describe [adsorption](@entry_id:143659) over an intermediate range of coverages where the logarithmic relationship holds.

### Comparative Analysis and Application

The Freundlich and Temkin [isotherms](@entry_id:151893) both offer improvements over the Langmuir model for describing [adsorption](@entry_id:143659) on heterogeneous surfaces, but they do so based on different assumptions. The Freundlich isotherm implicitly models an [exponential distribution](@entry_id:273894) of site energies, while the Temkin isotherm explicitly assumes a [linear decay](@entry_id:198935) in [adsorption energy](@entry_id:180281) with coverage. The choice between them often depends on which model provides a better empirical fit to the experimental data over the pressure range of interest.

Consider a scenario where two different catalysts are being evaluated for adsorbing a gaseous impurity [@problem_id:1525280]. Catalyst A follows the Freundlich isotherm ($\theta_A = k P_A^{1/n}$) and Catalyst B follows the Temkin isotherm ($\theta_B = C \ln(K_0 P_B)$). To compare their performance, we might calculate the ratio of pressures ($P_A/P_B$) required to achieve a target fractional coverage of, say, $\theta = 0.40$.

For Catalyst A, we solve for $P_A$:
$$ P_A = \left(\frac{\theta}{k}\right)^n $$

For Catalyst B, we solve for $P_B$:
$$ \ln(K_0 P_B) = \frac{\theta}{C} \implies P_B = \frac{1}{K_0} \exp\left(\frac{\theta}{C}\right) $$

By substituting the experimentally determined constants for each catalyst, we can calculate the required pressures and their ratio. This type of analysis demonstrates how these distinct mathematical forms are used in practice to predict and compare the behavior of different adsorbent-adsorbate systems under specific operating conditions.

In conclusion, the Freundlich and Temkin [isotherms](@entry_id:151893) are indispensable tools in [surface science](@entry_id:155397) and [chemical engineering](@entry_id:143883). They provide mathematically convenient and physically plausible frameworks for describing adsorption on the non-ideal, heterogeneous surfaces commonly encountered in practical applications. However, it is crucial to recognize their empirical nature and their inherent limitations, particularly their failure to describe [adsorption](@entry_id:143659) accurately at the extremes of very low and very high pressures. Their strength lies in their ability to model complex behavior within a defined, intermediate range of conditions.