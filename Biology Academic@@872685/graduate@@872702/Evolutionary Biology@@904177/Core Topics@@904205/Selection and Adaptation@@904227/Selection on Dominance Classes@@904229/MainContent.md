## Introduction
In [diploid](@entry_id:268054) organisms, the phenotypic expression of an allele is often conditional on its partner at the same locus. This interaction, known as dominance, is a cornerstone of genetics, yet its full impact on the evolutionary process is profoundly complex. While introductory genetics defines dominant and recessive traits, it often overlooks the crucial question of how these relationships shape the dynamics of natural selection. This article bridges that gap by providing a comprehensive framework for understanding selection on different dominance classes. We will begin in the first chapter, **Principles and Mechanisms**, by establishing the mathematical models that quantify dominance and examining its powerful influence on [allele frequency](@entry_id:146872) change, the fixation of new mutations, and the maintenance of [genetic variation](@entry_id:141964). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the far-reaching relevance of these principles, showing how they explain patterns in human [genetic disease](@entry_id:273195), [cancer evolution](@entry_id:155845), and even the formation of new species. Finally, the **Hands-On Practices** section offers an opportunity to apply these theoretical concepts to solve classic problems in population genetics, solidifying your understanding of this central evolutionary principle.

## Principles and Mechanisms

In diploid organisms, the expression of an allele's effect on the phenotype, and consequently on fitness, is contingent upon the identity of the second allele at the same locus. This interaction, known as **dominance**, is a fundamental determinant of how natural selection operates. It governs the visibility of new mutations to selection, shapes the trajectory of [allele frequency](@entry_id:146872) change, and influences the maintenance of genetic variation within populations. This chapter explores the principles and mechanisms of selection on different dominance classes, establishing a formal framework and examining its dynamic consequences.

### Parameterizing Dominance in Fitness Models

To quantitatively analyze the effects of dominance, we must first establish a mathematical model that links genotype to fitness. Consider a single autosomal locus with two alleles, a [wild-type allele](@entry_id:162987) $a$ and a variant allele $A$. In a diploid organism, three genotypes are possible: $AA$, $Aa$, and $aa$. Let us assume that selection acts on a quantitative phenotype, $z$, such that higher values of $z$ confer greater fitness. The phenotypic values for the three genotypes are $z_{AA}$, $z_{Aa}$, and $z_{aa}$.

The concept of dominance is fundamentally a description of the heterozygote's phenotype relative to the two homozygotes [@problem_id:2750035].
-   If allele $A$ is **completely dominant**, the heterozygote expresses the same phenotype as the $AA$ homozygote: $z_{Aa} = z_{AA}$.
-   If allele $A$ is **completely recessive**, it has no effect in the [heterozygous](@entry_id:276964) state, and the phenotype matches that of the other homozygote: $z_{Aa} = z_{aa}$.
-   If the alleles are **codominant** (or show **additivity**), the heterozygote's phenotype is exactly intermediate between the two homozygotes: $z_{Aa} = \frac{z_{AA} + z_{aa}}{2}$.

Since fitness is a function of the phenotype, these phenotypic relationships translate directly into fitness relationships. Let's consider [directional selection](@entry_id:136267) where allele $A$ is beneficial. We can establish a [relative fitness](@entry_id:153028) scale by setting the fitness of the less-fit homozygote, $w_{aa}$, to a baseline of $1$. The more-fit homozygote, $w_{AA}$, will have a fitness of $1+s$, where $s > 0$ is the **[selection coefficient](@entry_id:155033)** representing the selective advantage of the $AA$ genotype.

The fitness of the heterozygote, $w_{Aa}$, is determined by its degree of dominance. We introduce a **[dominance coefficient](@entry_id:183265)**, $h$, which scales the selective advantage expressed in the heterozygote. The standard [parameterization](@entry_id:265163) is:
$$
w_{AA} = 1+s, \quad w_{Aa} = 1+hs, \quad w_{aa} = 1
$$
Here, $h$ represents the fraction of the total fitness difference between homozygotes ($s$) that is expressed by the heterozygote. This single parameter elegantly captures the spectrum of [dominance relationships](@entry_id:156670) [@problem_id:2750035] [@problem_id:2750073]:
-   **$h=1$ (Complete Dominance of A):** $w_{Aa} = 1+s = w_{AA}$. The beneficial effect of allele $A$ is fully expressed in heterozygotes.
-   **$h=0$ (Complete Recessiveness of A):** $w_{Aa} = 1 = w_{aa}$. The beneficial allele $A$ is completely masked in heterozygotes; selection cannot "see" it unless it is homozygous.
-   **$h=1/2$ (Codominance or Additivity):** $w_{Aa} = 1 + s/2$. The heterozygote fitness is the [arithmetic mean](@entry_id:165355) of the two homozygote fitnesses, implying that each copy of allele $A$ contributes an equal fitness benefit of $s/2$. This is also referred to as genic selection or semidominance.

The parameter $h$ can also describe cases outside this range. If $h > 1$, then $w_{Aa} > w_{AA} > w_{aa}$, a condition known as **[overdominance](@entry_id:268017)** or [heterozygote advantage](@entry_id:143056). Conversely, if $h  0$, then $w_{Aa}  w_{aa}  w_{AA}$, a condition of **[underdominance](@entry_id:175739)** or [heterozygote disadvantage](@entry_id:166229) [@problem_id:2750073].

It is critical to distinguish between dominance at the level of a visible phenotype and dominance at the level of fitness. While they are often correlated, they are not necessarily identical, especially when selection operates across heterogeneous environments. Consider a hypothetical scenario where an allele $A$ confers a protective phenotype (e.g., camouflage) that is phenotypically dominant, meaning both $AA$ and $Aa$ individuals are equally protected from predators. In an environment with predators, their fitness would be identical: $w_{AA}^{(1)} = w_{Aa}^{(1)}$. However, if this protective structure carries a metabolic cost in an environment without predators, and this cost is dosage-dependent (higher for $AA$ than for $Aa$), their fitnesses in the safe environment would differ: $w_{AA}^{(2)}  w_{Aa}^{(2)}$. The overall fitness of each genotype, averaged across both environments, would then be different ($\bar{w}_{AA} \neq \bar{w}_{Aa}$), meaning the allele is not dominant with respect to fitness. This illustrates that fitness dominance is an emergent property of the [genotype-phenotype map](@entry_id:164408) and the selective environment, not solely an intrinsic property of gene expression [@problem_id:2750079].

### The Influence of Dominance on Allele Frequency Dynamics

The dominance relationship profoundly affects the rate and pattern of [allele frequency](@entry_id:146872) change under selection. We can analyze these dynamics by deriving the change in the frequency of a beneficial allele $A$, denoted $p$, over a single generation ($\Delta p$). For a large, randomly mating population at Hardy-Weinberg equilibrium before selection, the genotype frequencies are $p^2$ for $AA$, $2p(1-p)$ for $Aa$, and $(1-p)^2$ for $aa$. With fitnesses $w_{AA}=1+s$, $w_{Aa}=1+hs$, and $w_{aa}=1$, the exact change in [allele frequency](@entry_id:146872) is given by:
$$
\Delta p = \frac{p(1-p)s[h + p(1-2h)]}{1 + 2p(1-p)hs + p^2s}
$$
While this equation describes the full trajectory, the most revealing insights come from examining the dynamics when the allele is either very rare ($p \to 0$) or very common ($p \to 1$) [@problem_id:2750047]. We can define boundary selection gradients that measure the initial rate of increase and the final rate of approach to fixation.

The initial rate of increase of a rare beneficial allele is governed by the gradient $G_0 = \lim_{p \to 0^+} \frac{\Delta p}{p}$. When $p$ is small, $\Delta p \approx G_0 p$, indicating exponential growth. From the general formula for $\Delta p$, we find:
$$
G_0 = hs
$$
The rate at which the alternative allele, $a$, is eliminated from the population when it is rare (i.e., as $p \to 1$) is governed by the gradient $G_1 = \lim_{p \to 1^-} \frac{\Delta p}{1-p}$. Letting $q=1-p$, this is equivalent to $\lim_{q \to 0^+} \frac{-\Delta q}{q}$. From the formula for $\Delta p$, we find:
$$
G_1 = \frac{s(1-h)}{1+s}
$$
Evaluating these gradients for our key dominance classes reveals the fundamental character of their evolutionary trajectories [@problem_id:2750047]:

1.  **Beneficial Dominant Allele ($h=1$):** We find $(G_0, G_1) = (s, 0)$. The initial growth is rapid ($\Delta p \approx sp$), as the benefit is immediately expressed in heterozygotes. However, as the allele approaches fixation ($p \to 1$), the rate of change plummets ($G_1=0$). The now-deleterious [recessive allele](@entry_id:274167) $a$ can "hide" from selection in heterozygotes ($Aa$), which have the same fitness as the optimal $AA$ genotype. Purging the last copies of a recessive allele is notoriously inefficient, leading to a long tail of [polymorphism](@entry_id:159475).

2.  **Beneficial Recessive Allele ($h=0$):** We find $(G_0, G_1) = (0, s/(1+s))$. The initial increase is extremely slow ($G_0=0$). The allele is shielded from selection when rare because it exists almost exclusively in heterozygotes that have no fitness advantage ($w_{Aa}=w_{aa}$). Selection only acts on the exceedingly rare $AA$ homozygotes, so the allele must first drift to a sufficient frequency before selection can drive its increase. In this case, the change is not exponential, but follows $\Delta p \propto p^2$. In stark contrast, the final approach to fixation is highly efficient ($G_1 > 0$), as the [deleterious allele](@entry_id:271628) $a$ is now dominant in its effect and cannot hide in heterozygotes.

3.  **Codominant Allele ($h=1/2$):** We find $(G_0, G_1) = (s/2, s/(2(1+s)))$. Both gradients are positive. Selection is effective at both ends of the frequency spectrum. The allele is never fully expressed nor fully hidden in heterozygotes, allowing selection to act consistently across all frequencies. This leads to a symmetric, efficient trajectory of substitution.

The rate of adaptation, measured by the change in the population's mean fitness ($\Delta \bar{w}$), is also dependent on dominance. Consistent with **Fisher's Fundamental Theorem of Natural Selection**, mean fitness increases over time, and the rate of increase is proportional to the [additive genetic variance](@entry_id:154158) in fitness. For a rare beneficial allele ($p$ is small), a dominant allele ($h=1$) generates more additive variance in fitness than a [recessive allele](@entry_id:274167) ($h=0$), because the fitness difference is expressed in the relatively common heterozygotes. Consequently, a population with a rare, dominant beneficial allele will show a faster increase in mean fitness than a population with a rare, recessive one, even if the ultimate selective advantage ($s$) is the same [@problem_id:2750071].

### Dominance and the Fate of New Mutations: Haldane's Sieve

The deterministic dynamics described above assume the allele is already present at a sufficient frequency for selection to act upon. However, most new mutations arise as a single copy in a population and are subject to the vagaries of genetic drift. The vast majority are lost by chance, even if they are beneficial. The probability that a new [beneficial mutation](@entry_id:177699) ultimately reaches fixation is a critical parameter in adaptation, and it is strongly influenced by dominance.

This principle is known as **Haldane's sieve**. It states that beneficial mutations that are dominant or codominant are far more likely to survive the initial stochastic loss and contribute to adaptation than are beneficial [recessive mutations](@entry_id:266872) [@problem_id:2750068]. The reason lies in the mutation's initial visibility to selection. A new mutation exists as a single copy in a heterozygote.
- If the mutation is dominant ($h=1$) or codominant ($h=1/2$), the heterozygote has a fitness advantage ($1+s$ or $1+s/2$) over the wild-type. This advantage, however small, gives it a better-than-random chance of leaving more offspring.
- If the mutation is recessive ($h=0$), the heterozygote has no fitness advantage ($w_{Aa}=w_{aa}=1$). Its fate is determined purely by genetic drift, just like a [neutral mutation](@entry_id:176508).

Using a branching process approximation, one can derive the [fixation probability](@entry_id:178551), $u$, for a new mutation with a small selective advantage. For a diploid population of effective size $N_e$, the result is remarkably simple:
$$
u \approx 2h s_{het}
$$
where $s_{het}$ is the selective advantage of the heterozygote. In our standard model, $s_{het}=hs$, but this can be misleading. A more intuitive formulation based on the fitness of the heterozygote carrier ($1+s_{het}$) is $u \approx 2s_{het}$. For our [parameterization](@entry_id:265163), the fitness advantage of the heterozygote over the wild-type population average (which is close to 1) is $hs$. Thus, the [fixation probability](@entry_id:178551) is approximately:
$$
u \approx 2hs
$$
This simple formula encapsulates Haldane's sieve [@problem_id:2750068]:
- For a dominant beneficial allele ($h=1$), $u \approx 2s$.
- For a codominant allele ($h=1/2$), $u \approx s$.
- For a [recessive allele](@entry_id:274167) ($h=0$), this approximation gives $u \approx 0$.

The result $u \approx 0$ for a recessive allele highlights a limitation of this simple approximation. It correctly indicates that the probability is much smaller, but it is not zero. A more advanced analysis using diffusion theory is required [@problem_id:2750062]. In the case of a strictly recessive beneficial allele, selection is ineffective when the allele is rare because the mean change in [allele frequency](@entry_id:146872) is proportional to $p^2$, not $p$. The allele must first drift to a higher frequency by chance before selection can act effectively on the newly formed homozygotes. The [fixation probability](@entry_id:178551) for a new recessive beneficial mutation is approximately $u \approx \sqrt{2s / (\pi N_e)}$, which is substantially smaller than $s$ or $2s$ for large $N_e$, but greater than the neutral [fixation probability](@entry_id:178551) of $1/(2N_e)$. The key point is that the limit of the general [fixation probability](@entry_id:178551) formula as $h \to 0^{+}$ is $0$, which does not equal the [fixation probability](@entry_id:178551) at $h=0$. This "singular" behavior underscores the profound qualitative difference in the dynamics of recessive alleles when rare [@problem_id:2750062].

Haldane's sieve implies that the raw material for adaptation is filtered by dominance. The mutations that are most likely to drive evolutionary change are those with at least some beneficial effect in the [heterozygous](@entry_id:276964) state.

### Consequences and Extensions of Dominance Effects

The [principles of dominance](@entry_id:273418) extend to numerous other areas of population genetics, including the balance between mutation and selection, the concept of [genetic load](@entry_id:183134), the architecture of [quantitative traits](@entry_id:144946), and the effects of [non-random mating](@entry_id:145055).

#### Mutation-Selection Balance

Deleterious alleles are constantly introduced into populations by mutation. Selection acts to remove them, leading to an [equilibrium frequency](@entry_id:275072) known as the **[mutation-selection balance](@entry_id:138540)**. Dominance is a crucial determinant of this [equilibrium frequency](@entry_id:275072) because it controls how efficiently selection can purge the [deleterious allele](@entry_id:271628).

Consider a [deleterious allele](@entry_id:271628) $a$ that arises by mutation from the [wild-type allele](@entry_id:162987) $A$ at a rate $\mu$. The fitnesses are $w_{AA}=1$, $w_{Aa}=1-hs$, and $w_{aa}=1-s$. At equilibrium, the rate of removal of the allele by selection is balanced by its introduction via mutation. The derived equilibrium frequencies, $\hat{q}$, for [lethal alleles](@entry_id:141780) ($s=1$) are particularly illustrative [@problem_id:2750081]:
-   **Recessive Lethal ($h=0$):** The allele is shielded from selection in heterozygotes. Selection only acts on the $aa$ homozygotes, which have frequency $q^2$. The balance between the creation of new alleles ($\approx \mu$) and their removal ($\approx q^2s$) leads to an [equilibrium frequency](@entry_id:275072) of $\hat{q} \approx \sqrt{\mu/s}$. For a lethal allele ($s=1$), this is $\hat{q} \approx \sqrt{\mu}$.
-   **Dominant Lethal ($h=1$):** The allele is lethal in heterozygotes. Every new mutation that arises is immediately eliminated by selection. The only copies that exist in the population are those that arose in the current generation. Thus, the [equilibrium frequency](@entry_id:275072) is simply the mutation rate: $\hat{q} = \mu$.
-   **Codominant Lethal ($h=1/2$):** Heterozygotes have reduced fitness ($w_{Aa}=1/2$). Selection is more efficient than in the recessive case but less absolute than in the dominant case. The [equilibrium frequency](@entry_id:275072) is $\hat{q} \approx 2\mu$.

For a typical mutation rate of $\mu = 10^{-6}$ and a lethal allele ($s=1$), the [equilibrium frequency](@entry_id:275072) of a [recessive lethal allele](@entry_id:272654) would be $\hat{q} \approx \sqrt{10^{-6}} = 10^{-3}$, whereas for a dominant lethal, it would be $\hat{q} = 10^{-6}$. The recessive lethal can persist at a frequency 1000 times higher than the dominant lethal, a direct consequence of its ability to "hide" in heterozygotes [@problem_id:2750081]. This explains the persistence of many severe recessive genetic diseases in human populations.

#### Genetic Load

The presence of deleterious alleles or suboptimal genotypes means that the average fitness of a population is lower than that of the fittest possible genotype. This reduction in mean fitness is called **[genetic load](@entry_id:183134)**. The nature of this load depends on the form of selection.

**Substitutional load** is the fitness cost incurred by a population during the process of replacing an old allele with a new, superior one. It is defined relative to the fitness of the ultimately fixed genotype (e.g., $w_{AA}=1+s$). The instantaneous load, defined as the reduction from the optimal fitness ($L_{\text{sub}} = w_{AA}-\bar{w}$), becomes $L_{\text{sub}} = s(q^2 + 2pq(1-h))$. This shows that the load is composed of a contribution from less-fit homozygotes and a contribution from heterozygotes [@problem_id:2750080].

**Segregational load** is a permanent feature of populations with a stable polymorphism maintained by [overdominance](@entry_id:268017) ($h>1$). Here, the heterozygote is the fittest genotype, but due to Mendelian segregation, matings between heterozygotes continually produce less-fit [homozygous](@entry_id:265358) offspring. The load is defined relative to the optimal heterozygote's fitness, $L_{\text{seg}} = 1 - \bar{w}/w_{Aa}$. This load is borne entirely by the production of inferior homozygotes and persists as long as the [polymorphism](@entry_id:159475) is maintained [@problem_id:2750080].

#### Dominance in Quantitative Genetics: Additive and Dominance Variance

The concepts of dominance in selection and [quantitative genetics](@entry_id:154685) are linked but distinct. For a quantitative trait, we define an additive effect ($a$) and a dominance deviation ($d$). The total [genetic variance](@entry_id:151205) at a locus ($V_G$) can be partitioned into **[additive genetic variance](@entry_id:154158)** ($V_A$) and **[dominance variance](@entry_id:184256)** ($V_D$). These statistical components are not intrinsic properties of the gene but depend on [allele frequencies](@entry_id:165920):
$$
V_A = 2pq[a + d(q-p)]^2
$$
$$
V_D = (2pqd)^2
$$
Even if the underlying genotypic effects ($a, d$) and the fitness [dominance coefficient](@entry_id:183265) ($h$) are constant, the [variance components](@entry_id:267561) $V_A$ and $V_D$ will change as selection alters the allele frequency $p$ [@problem_id:2750032]. For example, for a trait with dominance ($d \neq 0$), when the allele $A$ is rare ($p \to 0$), nearly all the [genetic variance](@entry_id:151205) is additive ($V_A \gg V_D$). As the allele frequency increases towards the middle of the range, the contribution of [dominance variance](@entry_id:184256) becomes more significant. As the allele approaches fixation ($p \to 1$), both [variance components](@entry_id:267561) decline to zero as variation is eliminated. This dynamic relationship is crucial because the [response to selection](@entry_id:267049) is primarily determined by the [additive genetic variance](@entry_id:154158). The dominance of an allele, by influencing its frequency trajectory, thereby indirectly shapes the evolution of the very [variance components](@entry_id:267561) that govern its [response to selection](@entry_id:267049).

#### The Effect of Non-Random Mating

The principles discussed so far assume [random mating](@entry_id:149892), leading to Hardy-Weinberg genotype proportions. Departures from this assumption, such as **[inbreeding](@entry_id:263386)**, alter the evolutionary dynamics. Inbreeding increases the frequency of homozygotes and decreases the frequency of heterozygotes relative to HWE expectations. For a locus with alleles $A$ and $a$ at frequencies $p$ and $q$, the genotype frequencies under [inbreeding coefficient](@entry_id:190186) $F$ are $p^2+Fpq$ for $AA$, $2pq(1-F)$ for $Aa$, and $q^2+Fpq$ for $aa$ [@problem_id:2750019].

This shift in genotype frequencies has profound consequences for [selection on dominance](@entry_id:189440) classes:
-   For a **recessive [deleterious allele](@entry_id:271628)** ($h=0$), inbreeding increases the frequency of the $aa$ homozygotes upon which selection acts. This "exposes" the hidden recessive alleles to selection more frequently, increasing the efficiency of their removal (purging).
-   For a **dominant [deleterious allele](@entry_id:271628)** ($h=1$), most rare copies are already exposed to selection in heterozygotes under [random mating](@entry_id:149892). Inbreeding has a negligible effect on its rate of removal when the allele is rare, because it primarily shifts very rare heterozygotes to even rarer homozygotes, both of which are strongly selected against.
-   For a **codominant allele** ($h=1/2$), inbreeding also increases the efficiency of selection. By converting heterozygotes (with fitness $1-s/2$) to homozygotes (with fitness $1-s$), it increases the average selection pressure against the [deleterious allele](@entry_id:271628).

In summary, the interaction between alleles at a locus is not a minor detail but a central organizing principle of evolution. Dominance determines whether an allele's effect is expressed or masked, which in turn dictates its visibility to selection, its probability of fixation, its [equilibrium frequency](@entry_id:275072) under mutation, and its contribution to the genetic architecture of [complex traits](@entry_id:265688). Understanding [selection on dominance](@entry_id:189440) classes is therefore essential for a complete picture of the [evolutionary process](@entry_id:175749).