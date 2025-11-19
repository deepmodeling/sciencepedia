## Introduction
When an electric field is applied to an [electrolyte solution](@entry_id:263636), the resulting current is a collective effort, carried by the movement of ions. However, not all ions are created equal in their ability to transport charge. The fundamental concept that quantifies this difference is the **[transport number](@entry_id:267968)**, also known as the **[transference number](@entry_id:262367)**. This crucial parameter addresses the core question of how the total current is divided among the various ionic species present. Understanding the [transport number](@entry_id:267968) is indispensable for anyone studying electrochemistry, as it forms the bridge between microscopic ionic properties and macroscopic phenomena observed in batteries, analytical instruments, and even biological systems.

This article provides a comprehensive exploration of the [transport number](@entry_id:267968), designed to build your understanding from first principles to practical applications. We will address the knowledge gap between simply knowing that ions move and appreciating the specific factors that dictate their contribution to conductivity. Across three chapters, you will gain a robust understanding of this topic. The chapter on **Principles and Mechanisms** will lay the theoretical groundwork, defining the [transport number](@entry_id:267968) and linking it to [ionic mobility](@entry_id:263897), conductivity, and the physical factors that govern them. The **Applications and Interdisciplinary Connections** chapter will highlight the real-world relevance of transport numbers in fields ranging from materials science to biology. Finally, **Hands-On Practices** will allow you to apply these concepts to solve practical problems, solidifying your knowledge. To begin, we will delve into the fundamental principles that define the [transport number](@entry_id:267968) and the mechanisms governing its behavior.

## Principles and Mechanisms

In the study of electrochemistry, it is a fundamental observation that when an electric potential is applied across an [electrolyte solution](@entry_id:263636), the resulting flow of current is constituted by the movement of ions. However, not all ions contribute equally to this charge transport. The **[transport number](@entry_id:267968)**, also known as the **[transference number](@entry_id:262367)**, is a dimensionless quantity that quantifies the fraction of the total electrical current carried by a particular ionic species. Understanding the principles that govern transport numbers is crucial for analyzing a wide range of electrochemical phenomena, from the efficiency of batteries and fuel cells to the design of [electrophoretic separation](@entry_id:175043) techniques.

### Defining the Transport Number: The Fraction of Current Carried by an Ion

When a direct current, $I$, passes through an electrolyte, it is the sum of the partial currents carried by all the individual ionic species present in the solution. The partial current carried by ion $i$, denoted as $I_i$, depends on its ability to move through the solvent under the influence of the applied electric field. The [transport number](@entry_id:267968) of ion $i$, represented by the symbol $t_i$, is formally defined as the ratio of the partial current it carries to the total current:

$$
t_i = \frac{I_i}{I_{total}} = \frac{I_i}{\sum_j I_j}
$$

By definition, the sum of the transport numbers of all ions in the solution must equal unity: $\sum_i t_i = 1$.

The current carried by an ion is a function of its molar concentration ($c_i$), the magnitude of its charge number ($|z_i|$), and its **[ionic mobility](@entry_id:263897)** ($u_i$), which is a measure of the terminal velocity the ion attains per unit electric field strength. The [current density](@entry_id:190690) contributed by ion $i$ is $J_i = |z_i| F u_i c_i E$, where $F$ is the Faraday constant and $E$ is the magnitude of the electric field. Since the current $I_i$ is proportional to the [current density](@entry_id:190690) $J_i$, we can express the [transport number](@entry_id:267968) in terms of these fundamental ionic properties. The factors of field strength $E$ and the cross-sectional area cancel, yielding a more practical expression:

$$
t_i = \frac{|z_i| c_i u_i}{\sum_j |z_j| c_j u_j}
$$

This equation reveals that the [transport number](@entry_id:267968) is not an [intrinsic property](@entry_id:273674) of an ion alone but depends on the properties and concentrations of all other ions present in the solution.

### Relationship to Ionic Conductivity

The concept of [transport number](@entry_id:267968) is intimately linked to that of **molar [ionic conductivity](@entry_id:156401)**, $\lambda_i$. Molar [ionic conductivity](@entry_id:156401) relates the charge-[carrying capacity](@entry_id:138018) of an ion to its mobility through the equation $\lambda_i = |z_i| F u_i$. By substituting this relationship into the expression for the [transport number](@entry_id:267968), we arrive at a widely used formulation in terms of conductivities:

$$
t_i = \frac{c_i \lambda_i}{\sum_j c_j \lambda_j} = \frac{c_i \lambda_i}{\Lambda_m}
$$

Here, the denominator $\Lambda_m$ is the [molar conductivity](@entry_id:272691) of the entire solution. At the limit of infinite dilution, where ion-ion interactions are negligible, this relationship is expressed using **limiting molar ionic conductivities**, $\lambda_i^\circ$. This condition corresponds to **Kohlrausch's law of independent migration**, which states that the [limiting molar conductivity](@entry_id:266276) of an electrolyte is the sum of the limiting molar ionic conductivities of its constituent ions.

For a simple 1:1 electrolyte (e.g., NaCl), which dissociates into one cation ($+$) and one anion ($-$), the concentrations are equal ($c_+ = c_- = c$), and the expressions simplify significantly. At infinite dilution, the transport numbers for the cation ($t_+^\circ$) and anion ($t_-^\circ$) become:

$$
t_+^\circ = \frac{\lambda_+^\circ}{\lambda_+^\circ + \lambda_-^\circ} = \frac{\lambda_+^\circ}{\Lambda_m^\circ} \quad \text{and} \quad t_-^\circ = \frac{\lambda_-^\circ}{\lambda_+^\circ + \lambda_-^\circ} = \frac{\lambda_-^\circ}{\Lambda_m^\circ}
$$

These simple relationships are powerful. For instance, if the [limiting molar conductivity](@entry_id:266276) of a salt solution, $\Lambda_m^\circ$, and the [transport number](@entry_id:267968) of one of its ions are known from experiments, the limiting molar ionic conductivity of the other ion can be readily calculated. Imagine a hypothetical 1:1 electrolyte XY for which $\Lambda_m^\circ$ is $148.2 \text{ S cm}^2 \text{ mol}^{-1}$ and the cation [transport number](@entry_id:267968) $t_+^\circ$ is $0.385$. The anion [transport number](@entry_id:267968) must be $t_-^\circ = 1 - t_+^\circ = 1 - 0.385 = 0.615$. Consequently, the limiting molar [ionic conductivity](@entry_id:156401) of the anion, $\lambda_-^\circ$, is simply $t_-^\circ \Lambda_m^\circ = 0.615 \times 148.2 \text{ S cm}^2 \text{ mol}^{-1} = 91.1 \text{ S cm}^2 \text{ mol}^{-1}$ [@problem_id:1599667].

For electrolytes with higher valencies, the [stoichiometry](@entry_id:140916) of dissociation must be taken into account. Consider a salt of the type M$_{\nu_+}$X$_{\nu_-}$, which dissociates into $\nu_+$ cations and $\nu_-$ anions. The total conductivity contribution from each ion type depends on both its individual ionic conductivity and its [stoichiometric number](@entry_id:144772). For example, in a solution of magnesium chloride (MgCl$_2$), which dissociates into one Mg$^{2+}$ ion and two Cl$^-$ ions, Kohlrausch's law is written as $\Lambda_m^\circ(\text{MgCl}_2) = \lambda^\circ(\text{Mg}^{2+}) + 2\lambda^\circ(\text{Cl}^-)$. The fraction of current carried by the chloride ions is therefore:

$$
t_{\text{Cl}^-}^\circ = \frac{2 \lambda^\circ(\text{Cl}^-)}{\lambda^\circ(\text{Mg}^{2+}) + 2 \lambda^\circ(\text{Cl}^-)}
$$

Given that $\Lambda_m^\circ(\text{MgCl}_2) = 258.6 \times 10^{-4} \text{ S m}^2 \text{ mol}^{-1}$ and $\lambda^\circ(\text{Mg}^{2+}) = 106.0 \times 10^{-4} \text{ S m}^2 \text{ mol}^{-1}$, we can first find the conductivity of the chloride ion: $\lambda^\circ(\text{Cl}^-) = (\Lambda_m^\circ - \lambda^\circ(\text{Mg}^{2+}))/2 = 76.3 \times 10^{-4} \text{ S m}^2 \text{ mol}^{-1}$. Using this value, the [transport number](@entry_id:267968) of chloride is calculated as $t_{\text{Cl}^-}^\circ = \frac{2 \times 76.3}{106.0 + (2 \times 76.3)} \approx 0.590$ [@problem_id:1599679]. This illustrates that despite there being two chloride ions for every magnesium ion, the substantial charge-[carrying capacity](@entry_id:138018) of the Mg$^{2+}$ ion (as reflected in its large $\lambda^\circ$ value) prevents the [transport number](@entry_id:267968) of Cl$^-$ from being simply $2/3$.

### Physical Factors Governing Ionic Mobility and Transport Numbers

The [transport number](@entry_id:267968) is fundamentally determined by an ion's mobility, which in turn is governed by a complex interplay of physical factors.

#### Ion Size, Charge, and Solvation

A simple picture of ionic motion might suggest that smaller, lighter ions should move faster. However, this is rarely the case in solution. Ions in a [polar solvent](@entry_id:201332) are not bare entities; they are surrounded by a shell of solvent molecules, a phenomenon known as **[solvation](@entry_id:146105)** (or **hydration** in water). The strength of this interaction depends on the ion's charge density. Small ions with high charge (e.g., Li$^+$, Mg$^{2+}$) are powerful electric field sources and organize solvent molecules into a relatively large and tightly bound [solvation shell](@entry_id:170646). This entire solvated complex moves as a single kinetic unit. Therefore, the resistance to motion is determined not by the bare [ionic radius](@entry_id:139997) but by the **effective solvated radius** (or [hydrodynamic radius](@entry_id:273011)).

A simplified model can illuminate the interplay between charge and solvated radius [@problem_id:1599680]. Let's assume [ionic mobility](@entry_id:263897) is proportional to charge magnitude and inversely proportional to the solvated radius, $r_h$, so that $u_i \propto \frac{|z_i|}{r_{h,i}}$. The current carried by an ion is then proportional to $|z_i| c_i u_i$, which becomes proportional to $c_i \frac{|z_i|^2}{r_{h,i}}$. The [transport number](@entry_id:267968) of a cation in a solution of salt M$_{\nu_+}$X$_{\nu_-}$ is:

$$
t_+ = \frac{\nu_+ \frac{|z_+|^2}{r_{h,+}}}{\nu_+ \frac{|z_+|^2}{r_{h,+}} + \nu_- \frac{|z_-|^2}{r_{h,-}}}
$$

Using this model to compare Na$^+$ in NaCl ($z=1, \nu=1$) and Ca$^{2+}$ in CaCl$_2$ ($z=2, \nu=1$ for cation, $\nu=2$ for anion), we can see how both charge and [stoichiometry](@entry_id:140916) affect the result. Despite Ca$^{2+}$ having a larger [hydrated radius](@entry_id:273088) than Na$^+$, its higher charge ($z^2=4$) significantly boosts its contribution to conductivity, resulting in a [transport number](@entry_id:267968) for Ca$^{2+}$ that is surprisingly comparable to, or even larger than, that for Na$^+$ in their respective chloride solutions.

#### Anomalous Mobility: The Grotthuss Mechanism

Certain ions, most notably the hydrogen ion (H$^+$) and the hydroxide ion (OH$^-$) in water, exhibit exceptionally high molar ionic conductivities and, consequently, high transport numbers. For instance, in a dilute HCl solution, the [transport number](@entry_id:267968) of H$^+$ is approximately $0.82$, meaning it carries over 80% of the current. This cannot be explained by a simple model of a solvated ion moving through a fluid. The bare proton is tiny, but in water, it exists as a solvated complex, often represented as the hydronium ion (H$_3$O$^+$).

The true explanation lies in a unique transport mechanism known as the **Grotthuss mechanism** or structural diffusion [@problem_id:1599707]. Instead of the entire H$_3$O$^+$ complex moving through the water (a vehicular mechanism), a proton can effectively "hop" from one water molecule to the next through the network of hydrogen bonds. A covalent O-H bond in an H$_3$O$^+$ ion breaks, and a new one forms with an adjacent H$_2$O molecule. This relay race of bond-forming and bond-breaking results in the net [translocation](@entry_id:145848) of positive charge over a long distance much more rapidly than any single ion could physically move. A similar, though slightly less efficient, mechanism exists for the hydroxide ion, where a proton is transferred from a neutral water molecule to an OH$^-$, effectively moving the negative charge. This structural diffusion is why H$^+$ and OH$^-$ have mobilities that are several times larger than those of other simple ions like K$^+$ or Cl$^-$.

#### The Influence of Temperature and Solvent

Transport numbers are sensitive to both temperature and the nature of the solvent.

**Temperature** affects [ionic mobility](@entry_id:263897) in two primary ways [@problem_id:1599684]. First, increasing the temperature decreases the viscosity of the solvent, which reduces the hydrodynamic drag on all ions, increasing their mobilities. If this were the only effect, the ratio of mobilities, and thus the transport numbers, would remain relatively constant. However, a second, more subtle effect is the change in the [solvation shell](@entry_id:170646). For ions with highly structured [solvation](@entry_id:146105) shells, like the small, high-charge-density Li$^+$ ion, increasing temperature provides the thermal energy to disrupt this ordered structure. This "melting" of the [hydration shell](@entry_id:269646) causes a significant decrease in the effective [hydrodynamic radius](@entry_id:273011). This effect is less pronounced for larger ions with weaker solvation, like Cl$^-$. As a result, the mobility of Li$^+$ increases *disproportionately* more than that of Cl$^-$ as temperature rises. Consequently, the [transport number](@entry_id:267968) of Li$^+$ in an aqueous LiCl solution is observed to increase with temperature.

The choice of **solvent** has a profound impact on solvation and mobility [@problem_id:1599689]. Consider the difference between water, a [polar protic solvent](@entry_id:201676), and acetonitrile (CH$_3$CN), a polar [aprotic solvent](@entry_id:188199). Protic solvents have H atoms bonded to electronegative atoms (like oxygen in H$_2$O) and are excellent [hydrogen bond](@entry_id:136659) donors. They can effectively solvate both cations (via lone pairs on the oxygen) and [anions](@entry_id:166728) (via [hydrogen bonding](@entry_id:142832)). Aprotic solvents lack this hydrogen-bonding ability.

In an [aprotic solvent](@entry_id:188199) like acetonitrile, a cation like Li$^+$ can still be well-solvated by coordination with the nitrogen [lone pairs](@entry_id:188362). An anion like Cl$^-$, however, is very poorly solvated because acetonitrile cannot act as a [hydrogen bond donor](@entry_id:141108). This "bare" anion experiences much less drag and has a dramatically higher mobility in acetonitrile compared to its mobility in water. The mobility of Li$^+$ does not change as drastically. Since the [transport number](@entry_id:267968) of the cation is $t_{Li^+} = u_{Li^+}/(u_{Li^+} + u_{Cl^-})$, the large increase in the anion's mobility ($u_{Cl^-}$) leads to a decrease in the cation's [transport number](@entry_id:267968). Therefore, one would predict that $t_{\text{Li}^+, \text{ACN}}  t_{\text{Li}^+, \text{H}_2\text{O}}$.

### Concentration Dependence of Transport Numbers

While we often discuss transport numbers at infinite dilution, in practice they exhibit a dependence on concentration. This arises from ion-ion interactions (e.g., electrophoretic and relaxation effects described by Debye-Hückel-Onsager theory). A particularly illustrative case of concentration dependence is that of a [weak electrolyte](@entry_id:266880), such as acetic acid (CH$_3$COOH) in water [@problem_id:1599701].

In a moderately concentrated [acetic acid](@entry_id:154041) solution, the primary charge carriers are H$^+$ and acetate ions (CH$_3$COO$^-$), from the acid's dissociation, and the [transport number](@entry_id:267968) of H$^+$ is given by $t_{H^+} \approx \frac{u_{H^+}}{u_{H^+} + u_{\text{CH}_3\text{COO}^-}}$. Now, as this solution is progressively diluted, two things happen: the [degree of dissociation](@entry_id:141012) increases, but more importantly, the concentrations of ions from the acid dissociation eventually become comparable to and then smaller than the concentrations of H$^+$ and OH$^-$ from the [autoionization of water](@entry_id:137837).

In the limit of infinite dilution, the solution is essentially pure water. The only ions present are H$^+$ and OH$^-$, both at a concentration of $10^{-7}$ M (at 25 °C). The current is carried exclusively by these two ions. The [transport number](@entry_id:267968) of H$^+$ in this limit is therefore $t_{H^+} = \frac{u_{H^+}}{u_{H^+} + u_{OH^-}}$. Since the acetate ion has a significantly lower mobility than the hydroxide ion ($u_{\text{CH}_3\text{COO}^-}  u_{\text{OH}^-}$), the denominator in the expression for $t_{H^+}$ increases as the counter-ion transitions from acetate to hydroxide upon dilution. This means that the [transport number](@entry_id:267968) of H$^+$ in an acetic acid solution *decreases* as the concentration approaches zero, settling at a non-zero value characteristic of pure water.

### Experimental Determination of Transport Numbers

Several experimental methods have been developed to measure transport numbers, each with its own principles and limitations.

#### The Hittorf Method and Apparent Transport Numbers

The **Hittorf method** is a classical technique that relies on measuring the changes in the amount of electrolyte in the compartments surrounding the electrodes after a known quantity of charge has passed through the cell. A Hittorf cell is typically divided into three compartments: an anode compartment, a cathode compartment, and a central compartment. The central compartment's concentration should remain unchanged, confirming that measurement is not affected by diffusion from the electrode regions.

Consider the anode compartment. The concentration of cations in this compartment changes due to two processes: cations migrate *out* of the compartment toward the cathode, and cations may be produced by the oxidation of the anode. Anions migrate *into* the compartment from the central region. By carefully analyzing the number of moles of the ion in the compartment before and after [electrolysis](@entry_id:146038) and accounting for the amount produced or consumed at the electrode (calculable via Faraday's laws), one can determine the number of moles that migrated.

A crucial complication in the Hittorf method is the phenomenon of solvent transport. Because ions are solvated, their migration drags a certain number of solvent molecules along with them. The Hittorf method, by measuring concentration changes in a fixed laboratory frame, cannot distinguish between the movement of ions relative to the solvent and the bulk flow of the solvent itself. The value measured is therefore an **apparent [transport number](@entry_id:267968)**, often denoted $t'$. To determine the **true [transport number](@entry_id:267968)**, which represents [ion migration](@entry_id:260704) relative to the stationary solvent, the movement of the solvent must be quantified. This is accomplished by adding a neutral, non-migrating tracer substance (like urea or a sugar) to the solution [@problem_id:1599697]. Any change in the amount of the tracer in an electrode compartment is attributed solely to the bulk flow of the solvent. By measuring the initial and final amounts of the tracer, one can calculate the net moles of solvent that were transported, allowing a correction to be made to find the true [transport number](@entry_id:267968).

#### The Moving Boundary Method

The **[moving boundary method](@entry_id:276813)** offers a more direct and often more accurate way to determine transport numbers. In this technique, a sharp boundary is formed between two [electrolyte solutions](@entry_id:143425) that share a common ion. The "leading electrolyte" contains the ion whose [transport number](@entry_id:267968) is to be measured (e.g., H$^+$ in HCl), while the "indicator electrolyte" contains a cation with a *lower* mobility (e.g., Cd$^{2+}$ in CdCl$_2$).

The electrodes are arranged such that the cation of the leading electrolyte migrates away from the boundary. For instance, to measure $t_{H^+}$ in HCl, the cathode is placed in the HCl solution and the anode in the CdCl$_2$ solution. When current flows, the H$^+$ ions move toward the cathode, and the boundary between HCl and CdCl$_2$ moves with them.

For the boundary to remain sharp and stable, two conditions must be met [@problem_id:1599677]. First, the indicator ion must not overtake the leading ion, meaning the mobility of the indicator cation must be less than that of the leading cation ($u_{\text{indicator}}  u_{\text{leading}}$). For measuring the [transport number](@entry_id:267968) of Na$^+$ in NaCl ($u_{Na^+}^\circ \approx 5.19 \times 10^{-8} \text{ m}^2 \text{ s}^{-1} \text{ V}^{-1}$), a suitable indicator cation would be Li$^+$ ($u_{Li^+}^\circ \approx 4.01 \times 10^{-8}$) but not K$^+$ ($u_{K^+}^\circ \approx 7.62 \times 10^{-8}$). Second, to avoid having two different moving boundaries, both [electrolytes](@entry_id:137202) should share a common counter-ion (e.g., Cl$^-$ in the HCl/CdCl$_2$ example).

The [transport number](@entry_id:267968) can be calculated by measuring the distance the boundary moves, or more commonly, the volume $V$ it sweeps out in a channel of uniform cross-section, after a constant current $I$ has been passed for a time $t$. All the charge that passes a stationary plane in the leading solution is carried by both cations and [anions](@entry_id:166728). However, the charge that crosses the moving boundary itself is carried *only* by the cations. The total charge passed through the solution is $Q = I \times t$. The fraction of this charge carried by the cations is $t_+ Q$. This [charge transport](@entry_id:194535) is accomplished by all the cations contained within the volume $V$ that the boundary has swept. For a 1:1 electrolyte of concentration $c$, the number of moles of cations in this volume is $c \times V$. The charge they represent is $F \times c \times V$. Equating these gives:

$$
t_+ (I \times t) = F c V
$$

This can be rearranged to give the [transport number](@entry_id:267968) of the cation directly from the experimental measurements [@problem_id:1599669]:

$$
t_+ = \frac{F c V}{I t}
$$

This method provides the true [transport number](@entry_id:267968) directly, as the measurement is inherently made relative to the boundary, which delineates the extent of ionic migration.