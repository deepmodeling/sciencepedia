## Introduction
Electron affinity stands as a cornerstone concept in chemistry, quantifying an atom's fundamental tendency to accept an electron. This property is not just a numerical value on a chart; it is the energetic driver behind anion formation, a key determinant in the nature of chemical bonds, and a predictor of reactivity. While general [periodic trends](@entry_id:139783) offer a useful starting point, they often fail to capture the full picture, leaving students puzzled by numerous 'exceptions.' This article addresses that knowledge gap by delving into the quantum mechanical principles that govern not only the trends but also the critical anomalies that provide a deeper insight into atomic structure.

Throughout this exploration, you will first master the foundational concepts in **Principles and Mechanisms**, where we define electron affinity, explain its [periodic trends](@entry_id:139783), and dissect the crucial role of electron configuration in creating exceptions. Next, in **Applications and Interdisciplinary Connections**, we will bridge theory and practice, demonstrating how [electron affinity](@entry_id:147520) is applied to understand everything from the [stability of ionic compounds](@entry_id:148945) to the design of modern semiconductor materials. Finally, the **Hands-On Practices** section will challenge you to apply these principles to solve complex chemical problems, solidifying your understanding. We begin by examining the core principles that define electron affinity and the mechanisms that dictate its behavior across the periodic table.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental periodic properties of atoms. We now turn our attention to a property of profound chemical importance: **electron affinity**. This property quantifies an atom's propensity to accept an electron, a process central to anion formation, [redox chemistry](@entry_id:151541), and the nature of [chemical bonding](@entry_id:138216). Unlike [ionization energy](@entry_id:136678), which measures the ease of electron removal, [electron affinity](@entry_id:147520) probes the energetics of electron gain. Understanding its principles and the apparent exceptions to its trends provides deep insight into the quantum mechanical structure of the atom.

### Defining Electron Affinity: Energy, Stability, and Sign Conventions

The **[first electron affinity](@entry_id:156805)** ($EA_1$) of an element is formally defined as the energy released when a neutral atom in the gaseous state gains an electron to form a gaseous anion. This process is represented by the equation:

$$
X(g) + e^{-} \to X^{-}(g)
$$

By convention in [inorganic chemistry](@entry_id:153145), electron affinity is defined such that a positive value indicates that energy is *released* during this process. Therefore, an [exothermic process](@entry_id:147168) corresponds to a positive electron affinity ($EA > 0$). This energy release signifies that the resulting anion, $X^{-}(g)$, is thermodynamically more stable than the separated neutral atom and a free electron.

Conversely, a process that requires an input of energy is endothermic. In such cases, the [electron affinity](@entry_id:147520) is negative ($EA  0$), and the resulting anion is thermodynamically unstable relative to the neutral atom and a free electron; it would spontaneously decay by ejecting the electron.

It is crucial to distinguish this convention from the thermodynamic quantity, the **change in enthalpy** ($\Delta H$) or **change in internal energy** ($\Delta E$) for the process. These quantities are negative for an [exothermic process](@entry_id:147168) and positive for an endothermic one. The relationship is therefore:

$$
\Delta E \approx \Delta H = -EA
$$

For example, chlorine has a large, positive [electron affinity](@entry_id:147520) ($EA(\text{Cl}) = +349 \text{ kJ/mol}$), meaning the process $Cl(g) + e^{-} \to Cl^{-}(g)$ is highly exothermic ($\Delta E = -349 \text{ kJ/mol}$). The resulting chloride ion, $Cl^{-}$, is stable. In contrast, neon has a negative [electron affinity](@entry_id:147520) ($EA(\text{Ne}) \approx -116 \text{ kJ/mol}$), meaning the process $Ne(g) + e^{-} \to Ne^{-}(g)$ is endothermic ($\Delta E \approx +116 \text{ kJ/mol}$). The neonide anion, $Ne^{-}$, is unstable and does not form spontaneously in the gas phase [@problem_id:2278737].

It is also vital to differentiate [electron affinity](@entry_id:147520) from **electronegativity**. While both relate to an atom's attraction for electrons, their contexts are distinct. Electron affinity is a quantifiable energy change for an isolated, gaseous atom. Electronegativity, conversely, is a relative, dimensionless measure of an atom's ability to attract shared electrons *within a chemical bond*. For instance, fluorine's high [electronegativity](@entry_id:147633) describes its strong pull on the electrons in a molecule like HF, whereas its electron affinity quantifies the energy released when an isolated F atom captures an electron [@problem_id:2278745].

### The Physical Basis of Electron Affinity: A Balance of Forces

The magnitude and sign of an element's electron affinity are determined by a delicate balance between electrostatic attraction and repulsion, governed by quantum mechanics.

The primary stabilizing factor is the **electron-nucleus attraction**. An incoming electron is attracted to the positive charge of the nucleus. The strength of this attraction depends on the **effective nuclear charge ($Z_{eff}$)** experienced by the electron in its destination orbital. $Z_{eff}$ is the net positive charge "felt" by an electron, which is the actual nuclear charge ($Z$) minus a [shielding constant](@entry_id:152583) ($\sigma$) that accounts for the screening effect of other electrons. A higher $Z_{eff}$ leads to a stronger attraction and, all else being equal, a more exothermic [electron affinity](@entry_id:147520).

The primary destabilizing factor is **electron-electron repulsion**. The incoming electron is repelled by the electrons already present in the atom. This repulsion counteracts the nuclear attraction.

The net energy change, or electron affinity, is the result of the competition between these forces. An element will have a positive (exothermic) [electron affinity](@entry_id:147520) if the stabilization from the electron-nucleus attraction outweighs the destabilization from [electron-electron repulsion](@entry_id:154978). This is observed for [alkali metals](@entry_id:139133) like lithium. Although highly electropositive, a neutral lithium atom ($[\text{He}] 2s^1$) readily accepts an electron to form a stable $Li^{-}$ anion. The incoming electron enters the 2s orbital, where it is primarily shielded only by the two core 1s electrons. The resulting $Z_{eff}$ is sufficiently high that the attraction to the lithium nucleus is strong enough to overcome the repulsion from the other 2s electron, leading to a net release of energy [@problem_id:2278741].

### General Periodic Trends

The interplay of effective nuclear charge, [atomic size](@entry_id:151650), and [electron configuration](@entry_id:147395) gives rise to predictable trends in electron affinity across the periodic table.

#### Trend Across a Period

As one moves from left to right across a period, the [electron affinity](@entry_id:147520) generally becomes more exothermic (i.e., the value of $EA$ becomes more positive). The underlying reason is the steady increase in **effective nuclear charge**. Across a period, protons are added to the nucleus, increasing $Z$. The corresponding electrons are added to the same principal energy shell, where they are relatively ineffective at shielding one another. Consequently, $Z_{eff}$ increases significantly. This stronger effective nuclear pull attracts the incoming electron more powerfully, leading to a greater release of energy. A simplified model shows that for many elements, the electron affinity is nearly linearly dependent on the [effective nuclear charge](@entry_id:143648) experienced by the valence electrons [@problem_id:2278726].

#### Trend Down a Group

As one moves down a group, the electron affinity generally becomes less exothermic (i.e., the value of $EA$ decreases). The dominant factor here is the increase in [atomic size](@entry_id:151650). The incoming electron must occupy a valence shell with a progressively higher **principal quantum number ($n$)**. Orbitals with higher $n$ are, on average, significantly farther from the nucleus. According to Coulomb's law, the force of attraction diminishes with the square of the distance. This increased distance weakens the electrostatic attraction between the nucleus and the incoming electron. Although the total nuclear charge increases down a group, this effect is largely offset by the shielding from a greater number of core [electron shells](@entry_id:270981). The dominant effect is the increasing orbital radius, which results in a smaller energy release upon [electron capture](@entry_id:158629). This trend is clearly observed in the [alkali metals](@entry_id:139133), where electron affinity decreases steadily from lithium down to cesium [@problem_id:2278704].

### Key Exceptions: The Decisive Role of Electron Configuration

The general trends for [electron affinity](@entry_id:147520) are punctuated by several important and highly instructive exceptions. These anomalies are not random; they are direct consequences of the unique stability associated with certain [electron configurations](@entry_id:191556).

#### Groups 2 and 18: The Cost of Disrupting Stability

Elements in Group 2 ([alkaline earth metals](@entry_id:142937)) and Group 18 ([noble gases](@entry_id:141583)) exhibit endothermic or near-zero electron affinities. This is because they possess particularly stable [electron configurations](@entry_id:191556): a completely filled **s-subshell** ($ns^2$) for Group 2 and a completely filled **valence shell** ($ns^2np^6$) for Group 18.

For a Group 2 element like Beryllium ($[\text{He}] 2s^2$), the incoming electron cannot enter the filled 2s subshell. It is forced to occupy a vacant orbital in the next, higher-energy subshell, the 2p subshell. For a Group 18 element like Neon ($[\text{He}] 2s^22p^6$) or Argon ($[\text{Ne}] 3s^23p^6$), the situation is even more energetically costly: the incoming electron must occupy the [s-orbital](@entry_id:151164) of the next principal energy level (the 3s for Ne, the 4s for Ar) [@problem_id:2278756]. In both cases, the significant energy penalty required to place an electron in a higher-energy orbital is not compensated by the nuclear attraction, making the overall process endothermic [@problem_id:2278703, @problem_id:2010506].

#### Group 15: The Penalty for Pairing

Another significant anomaly occurs in Group 15. These elements typically have a less exothermic [electron affinity](@entry_id:147520) than their neighbors in Group 14 and Group 16. For example, nitrogen's [electron affinity](@entry_id:147520) is endothermic, while those of carbon and oxygen are exothermic [@problem_id:2278767].

The reason lies in the special stability of a **half-filled p-subshell**. According to Hund's rule, the $np^3$ configuration of Group 15 elements, with one electron in each p-orbital and all spins parallel, is particularly stable due to maximized exchange energy. When an element from Group 14 (with an $np^2$ configuration) accepts an electron, it achieves this stable $np^3$ configuration. However, when a Group 15 element accepts an electron, it must place this new electron into a p-orbital that is already occupied. This has two negative energetic consequences:
1.  It disrupts the special stability of the half-filled subshell.
2.  It introduces significant electron-electron repulsion, known as **pairing energy**, between the two electrons forced to occupy the same orbital space.

This energetic penalty makes the [electron affinity](@entry_id:147520) of Group 15 elements anomalously low [@problem_id:2278700, @problem_id:2278723]. Some elements, like nitrogen, have a combination of a stable half-filled subshell and a compact valence shell, making the process of adding an electron endothermic [@problem_id:2278746].

#### The Halogens and the Second-Period Anomaly

The [periodic trends](@entry_id:139783) culminate in Group 17, the **halogens**. With a valence configuration of $ns^2np^5$, they are one electron short of a stable [noble gas configuration](@entry_id:138350). This, combined with their high [effective nuclear charge](@entry_id:143648), results in the most exothermic electron affinities in their respective periods. The addition of an electron completes the valence shell, leading to a large release of energy [@problem_id:2278754].

However, within the [halogens](@entry_id:145512) (and other p-block groups), an important anomaly appears: the [electron affinity](@entry_id:147520) of the second-period element is often less exothermic than that of the third-period element below it. For instance, chlorine has a more exothermic [electron affinity](@entry_id:147520) ($+349 \text{ kJ/mol}$) than fluorine ($+328 \text{ kJ/mol}$) [@problem_id:2010497]. The same is true for sulfur relative to oxygen [@problem_id:2278727].

This counterintuitive result arises from the extremely high electron density in the compact valence shell of the second-period elements. The 2p orbitals of fluorine are much smaller than the 3p orbitals of chlorine. While the incoming electron is closer to the fluorine nucleus, it is also forced into a much more crowded region of space. The resulting inter-[electron repulsion](@entry_id:260827) is exceptionally large, and this destabilizing effect significantly offsets the strong nuclear attraction. In chlorine, the incoming electron enters a larger, more diffuse 3p orbital, where the [electron-electron repulsion](@entry_id:154978) is substantially less severe. This reduction in repulsion is significant enough to make the overall process more exothermic for chlorine than for fluorine, despite chlorine's larger size [@problem_id:2278715].

### Successive Electron Affinities and Advanced Topics

The principles of electron affinity extend beyond the addition of a single electron and can be influenced by more complex atomic phenomena.

#### Second and Higher Electron Affinities

While the [first electron affinity](@entry_id:156805) can be exothermic or endothermic, the **[second electron affinity](@entry_id:138138)** ($EA_2$), which describes the addition of an electron to a gaseous anion, is *always* a strongly [endothermic process](@entry_id:141358).

$$
X^{-}(g) + e^{-} \to X^{2-}(g) \quad \Delta E = -EA_2 > 0
$$

The fundamental reason is **electrostatic repulsion**. The incoming electron, which is negatively charged, is strongly repelled by the net negative charge of the anion it is approaching. An enormous amount of energy is required to overcome this Coulombic repulsion and force the second electron onto the ion. This universal principle holds true even when the addition of the electron would result in a stable closed-shell configuration, such as in the formation of $O^{2-}(g)$ or $S^{2-}(g)$ [@problem_id:2278708, @problem_id:2278719, @problem_id:2278746]. Such polyanions are only stable when stabilized by the [electrostatic field](@entry_id:268546) of surrounding counter-ions in an ionic crystal lattice.

#### Anomalies in Heavier Elements: d-Block Contraction and Relativistic Effects

For heavier elements, additional factors come into play. A notable anomaly occurs between aluminum and gallium in Group 13. Contrary to the expected trend, gallium's electron affinity is nearly identical to aluminum's. This is a consequence of the **[d-block contraction](@entry_id:140104)**. Gallium's electronic configuration includes a filled 3d subshell. Electrons in [d-orbitals](@entry_id:261792) are notoriously poor at shielding the nuclear charge from the outer valence electrons. This inefficient shielding causes the valence electrons of gallium to experience a much higher effective nuclear charge than would otherwise be expected, enhancing its attraction for an incoming electron and counteracting the effect of its larger size [@problem_id:2278750].

In the heaviest elements, **[relativistic effects](@entry_id:150245)** become significant. For an element like gold, the electrons near its massive nucleus travel at speeds that are a substantial fraction of the speed of light. This leads to a [relativistic contraction](@entry_id:154351) and stabilization of its s-orbitals. The 6s orbital of gold contracts, drawing the electron closer to the nucleus. Furthermore, the inner d and f orbitals expand relativistically, making them even poorer at shielding. Both effects dramatically increase the effective nuclear charge felt by the 6s electron. This enhanced attraction explains gold's remarkably high [electron affinity](@entry_id:147520), which is comparable to that of the halogens and is responsible for much of its unique chemistry [@problem_id:2278729]. These advanced concepts demonstrate that the simple [periodic trends](@entry_id:139783) taught in introductory courses are built upon a deep and complex foundation of physics.