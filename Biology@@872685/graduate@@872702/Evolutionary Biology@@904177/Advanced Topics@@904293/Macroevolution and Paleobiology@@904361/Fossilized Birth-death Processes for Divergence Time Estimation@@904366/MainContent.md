## Introduction
Accurately reconstructing the timeline of life's history is a central goal in evolutionary biology. Estimating the divergence times of species requires a robust synthesis of information from the genomes of living organisms and the physical remains of extinct ones found in the [fossil record](@entry_id:136693). However, integrating these disparate data sources presents significant challenges. Traditional methods often rely on subjective interpretations of fossil evidence to calibrate molecular clocks, introducing potential biases that can limit the reliability of time estimates. This creates a need for a unified framework that can coherently model both the diversification of lineages and the processes by which they are observed.

This article introduces the Fossilized Birth-Death (FBD) process, a powerful probabilistic model that directly addresses this challenge. Over the next three chapters, you will gain a comprehensive understanding of this cutting-edge method. We will begin by dissecting the fundamental **Principles and Mechanisms** of the FBD process, exploring the parameters that govern speciation, extinction, and fossilization. Next, we will examine its **Applications and Interdisciplinary Connections**, demonstrating how [total-evidence dating](@entry_id:163840) with the FBD model is used to test major macroevolutionary hypotheses. Finally, a series of **Hands-On Practices** will allow you to engage directly with the core concepts and solidify your knowledge. We will start by exploring the generative model at the heart of the FBD process.

## Principles and Mechanisms

The Fossilized Birth-Death (FBD) process provides a unified probabilistic framework for inferring [phylogenetic trees](@entry_id:140506) and divergence times by integrating molecular data from extant species with morphological and temporal data from the [fossil record](@entry_id:136693). It models the diversification of lineages and the sampling of these lineages—both as fossils through time and as living species at the present day—as a single, coherent generative process. This chapter elucidates the fundamental principles and mechanisms of the FBD process, explaining its parameters, the structure of the phylogenies it produces, and its statistical properties when used for inference.

### The Fossilized Birth-Death Process: A Generative Model

At its core, the **Fossilized Birth-Death (FBD) process** is a continuous-time branching process that describes the evolution of a [clade](@entry_id:171685) from its origin to the present. The model is defined by four key parameters that govern the rates at which fundamental evolutionary and sampling events occur [@problem_id:2714587].

*   **Speciation Rate ($\lambda$)**: This is the rate at which any given lineage splits into two distinct daughter lineages. In a constant-rate model, the waiting time until the next speciation event for a lineage is exponentially distributed with rate $\lambda$.

*   **Extinction Rate ($\mu$)**: This is the rate at which any given lineage goes extinct, leaving no descendants. The waiting [time to extinction](@entry_id:266064) is also exponentially distributed with rate $\mu$. The interplay between $\lambda$ and $\mu$ determines the net diversification dynamics of the clade.

*   **Fossil Sampling Rate ($\psi$)**: This parameter models the discovery of fossils. Along each extant lineage, fossil discoveries are modeled as a homogeneous Poisson point process with rate $\psi$. A critical feature of the FBD model is that a fossil sampling event is an observation that does not, by itself, terminate the lineage. The lineage can persist after a fossil is sampled, continuing to be subject to speciation, extinction, and further fossilization.

*   **Extant Sampling Probability ($\rho$)**: This parameter represents the probability that a lineage surviving to the present day ($t=0$) is included in the dataset of extant species. At the present, each surviving lineage is sampled independently in a Bernoulli trial with success probability $\rho$.

These four parameters—$\lambda, \mu, \psi, \rho$—together define a [generative model](@entry_id:167295) for a "sampled tree," which includes not only the sampled extant taxa but also the sampled fossil taxa, placed at their correct stratigraphic ages.

### The Parameters in Detail

A robust understanding of the FBD model requires a closer examination of the sampling parameters, $\psi$ and $\rho$, which mediate the connection between the underlying diversification process and the observed data.

#### The Fossil Sampling Rate, $\psi$

The parameter $\psi$ is a rate, not a probability, with units of events per lineage per unit of time (e.g., fossils per lineage per million years). As a rate, its value can be any non-negative real number, and a value of $\psi > 1$ is perfectly permissible; it would simply imply an expectation of more than one fossil discovery per lineage per unit of time [@problem_id:2714643].

Because fossil sampling along a lineage follows a Poisson process, we can precisely quantify the probability of fossil discovery. For a single lineage segment of duration $\Delta t$, the number of fossils found is Poisson distributed with a mean of $\psi \Delta t$. Consequently, the probability of finding at least one fossil on that segment is given by $1 - \exp(-\psi \Delta t)$.

The parameter $\psi$ can also be interpreted as a composite parameter representing a more complex geological reality. For instance, if fossil-bearing geological strata ("fossil beds") form as a Poisson process with rate $\beta$ and each extant lineage has an independent probability $p$ of being preserved and discovered in any given bed, then the resulting process of fossil discoveries along a single lineage is equivalent to a homogeneous Poisson process with an effective rate of $\psi = \beta p$ [@problem_id:2714643]. In a typical FBD analysis, it is this composite rate $\psi$ that is estimated, as the individual components $\beta$ and $p$ are generally non-identifiable.

Across an entire clade, the rate of fossil discovery at any time $t$ is the sum of the rates from all existing lineages. If there are $L(t)$ lineages at time $t$, the instantaneous rate of fossilization for the whole [clade](@entry_id:171685) is $L(t)\psi$. This implies that the total expected number of fossils for a given phylogeny is equal to $\psi$ multiplied by the total [branch length](@entry_id:177486) of the tree, which is the integral of $L(t)$ over time [@problem_id:2714643].

#### The Extant Sampling Probability, $\rho$

The parameter $\rho$ quantifies the completeness of sampling among species that are living at the present day. It models the reality that not all extant species in a [clade](@entry_id:171685) may be included in a phylogenetic study. The FBD model treats this as a series of independent Bernoulli trials at time $t=0$: each of the $N$ lineages that survive to the present is included in the final tree with probability $\rho$.

The inclusion of $\rho  1$ has two primary effects on the likelihood calculation for a given tree [@problem_id:2714546]. First, for the $n$ extant species that *are* observed in the tree, there is a direct contribution of $\rho^n$ to the probability of the data. Second, and more subtly, it affects the probability that any ancestral lineage leaves at least one sampled descendant. For a lineage existing in the past to be considered "unobserved" in the final dataset, it must not only produce no fossil samples along any of its descendant branches, but all of its descendant lineages that survive to the present must also be *missed* during the extant sampling phase. This latter possibility is accounted for by factors involving $(1-\rho)$. Thus, the likelihood calculation effectively integrates over all possible histories of unobserved extant survivors.

The case where $\rho = 1$ is a special, simplified scenario. It corresponds to a complete sampling of all extant species. In this case, there are no factors for missed extant sampling, and the probability of an ancestral lineage being unobserved simplifies to it having no fossil descendants and no descendants that survive to the present. The parameter $\rho$ effectively drops out of the likelihood terms related to [observability](@entry_id:152062) when sampling is complete [@problem_id:2714546].

### The Structure of FBD Trees: Sampled Ancestors

A key innovation of the FBD framework is its ability to model **sampled ancestors**. Because the act of fossil sampling is decoupled from speciation and extinction, a fossil can be an observation of an individual from a lineage that continues to evolve, speciate, and leave further descendants. This is in contrast to older models where fossils were often forced to be terminal side-branches.

The structure of the "reconstructed tree" under the FBD model can be understood by examining the different types of nodes it contains, which can be distinguished by their outdegree (the number of direct descendant branches) [@problem_id:2714553]:

*   **Speciation Node**: This is a true bifurcation event where an ancestral lineage splits into two daughter lineages. In the tree, this is represented by a node with an **outdegree of 2**.

*   **Terminal Fossil Tip**: This is a fossil sample from a lineage that has no other sampled descendants in the tree. This could be because the lineage went extinct shortly after the fossil was sampled, or because any subsequent descendants were simply not sampled (either as fossils or as extant species). In the tree, this is represented by a node with an **outdegree of 0**. It is a leaf of the tree.

*   **Sampled Ancestor**: This is a fossil sample from a lineage that continues to exist past the sampling event and gives rise to at least one other sampled descendant (either another fossil or an extant species). In the tree, this event is represented by a node that lies on an internal branch. It has one branch coming in from its ancestor and one branch continuing on to its descendant. Therefore, a [sampled ancestor](@entry_id:192502) is represented by a node with an **outdegree of 1**.

The ability to model sampled ancestors provides a more realistic representation of the fossil record and allows for the recovery of tree structures that are inaccessible to models that treat all fossils as terminal tips.

### The FBD Process in Phylogenetic Inference

The FBD process serves as a powerful tree prior in Bayesian [phylogenetic inference](@entry_id:182186), providing a mechanistic alternative to more traditional dating methods. Its role is best understood by contrasting it with node dating.

#### Context: Node Dating vs. Tip Dating

Phylogenetic dating methods can be broadly categorized by how they incorporate fossil information [@problem_id:2714511].

**Node Dating** is a widely used method where fossils are used *indirectly*. The analysis is typically performed on a molecular dataset for extant taxa only. A paleontologist assesses a fossil's age and its likely phylogenetic position, and this information is used to formulate a statistical probability distribution, called a **calibration prior** (e.g., a lognormal or [uniform distribution](@entry_id:261734)), on the age of a specific internal node ([clade](@entry_id:171685)) in the tree. The fossil itself is not part of the phylogenetic matrix or the tree. The tree prior in this case is often a simple birth-death or Yule model, which corresponds to an FBD process with the fossil sampling rate set to zero ($\psi = 0$).

**Tip Dating**, often implemented using the FBD process, uses fossils *directly*. Fossil specimens are included as terminal taxa (tips) in the phylogenetic matrix. Their ages, derived from stratigraphic data, are fixed as a property of the tip. Their phylogenetic position is not assumed a priori but is inferred from their character data (typically [morphology](@entry_id:273085), as ancient DNA is rare). The FBD process, with $\psi  0$, is used as a comprehensive tree prior that models the joint generation of the [tree topology](@entry_id:165290), divergence times, and fossil occurrences. When molecular data for extant species are analyzed simultaneously with morphological data for both extant and fossil taxa, this approach is often called **Total-Evidence Dating (TED)**.

#### The FBD as a Mechanistic Tree Prior

The primary conceptual advantage of using the FBD process in a tip-dating framework is that it replaces subjective, user-specified node calibrations with a single, mechanistic generative model [@problem_id:2714490]. In node dating, the choice of the shape and bounds of a calibration prior can be arbitrary and has been shown to strongly influence posterior time estimates.

The FBD prior, in contrast, generates a probability distribution for the entire tree, including both its topology and all of its node ages. The expected waiting times between speciation, extinction, and fossilization events are determined by the rates $\lambda$, $\mu$, and $\psi$. Consequently, the ages of the fossil tips probabilistically constrain the ages of the internal divergence nodes through the lens of this unified process. The constraints on divergence times emerge naturally from the data and the model dynamics rather than from externally imposed, ad-hoc distributions. This reduces a major source of subjectivity in [divergence time estimation](@entry_id:178959) [@problem_id:2714490].

### Statistical Properties and Identifiability

The statistical power of the FBD framework stems from its ability to jointly leverage information from different data sources, which helps resolve ambiguities that are intractable when using a single data type alone.

#### Breaking the Rate-Time Confounding

A fundamental challenge in [molecular phylogenetics](@entry_id:263990) is the confounding of [evolutionary rate](@entry_id:192837) and absolute time. The likelihood of a molecular sequence alignment depends on the branch lengths of the tree, which are measured in expected substitutions per site. The length of a branch $i$, $b_i$, is the product of the [substitution rate](@entry_id:150366) on that branch, $r_i$, and its duration in absolute time, $\Delta t_i$, such that $b_i = r_i \Delta t_i$.

With molecular data alone, one cannot uniquely disentangle the rate from the time. The data can be explained equally well by a combination of fast rates and short times or slow rates and long times. Specifically, the molecular likelihood is invariant under the transformation $(r_i, \Delta t_i) \mapsto (r_i/c, c \Delta t_i)$ for any positive scalar $c$ [@problem_id:2714604]. This means [absolute time](@entry_id:265046) is not identifiable from sequence data alone.

In node-dating analyses, this non-[identifiability](@entry_id:194150) means the sequence likelihood can be very "flat" or uninformative about absolute time. Consequently, the [posterior distribution](@entry_id:145605) for a node's age can be almost entirely determined by the user-specified calibration prior, a phenomenon known as **prior dominance** [@problem_id:2714582].

The FBD framework powerfully mitigates this issue. By including fossils with **absolute ages** as tips in the tree, the model is anchored to a real timescale. The [scaling invariance](@entry_id:180291) is broken because applying a scaling factor $c$ to all time durations would change the age of a fossil tip, contradicting its known stratigraphic age. This forces $c=1$. With the absolute timescale anchored by the fossils, the molecular data can then be used to more effectively estimate the substitution rates $r_i$. The FBD model thus moves fossil information from being an external, and potentially dominating, prior to being an integral part of the data that helps to deconvolve rate and time across the entire phylogeny [@problem_id:2714582]. It is crucial, however, that the fossils provide absolute age information; if fossils only provided relative ordering (e.g., fossil A is older than fossil B), the scaling non-identifiability would return in a more complex form involving all rate parameters [@problem_id:2714604].

#### Identifiability of FBD Parameters

While the FBD model is powerful, not all of its parameters are equally easy to estimate from all types of data. The ability to identify a parameter depends on the [information content](@entry_id:272315) of the data. For instance, consider a simplified dataset consisting only of the pooled occurrence times of fossils from a clade, without any phylogenetic information. Such data are primarily informative about the overall trajectory of lineage accumulation and the rate of sampling. The shape of the curve of fossil occurrences through time is mainly governed by the **[net diversification rate](@entry_id:162682)** ($r = \lambda - \mu$) and the fossil sampling rate $\psi$. The individual speciation ($\lambda$) and extinction ($\mu$) rates are very difficult to disentangle from such limited data. Any combination of $\lambda$ and $\mu$ that yields the same difference $r$ will produce a very similar likelihood, creating a "likelihood ridge" in the parameter space and indicating weak identifiability [@problem_id:2714493]. To better resolve individual speciation and extinction rates, information from the shape of a fully resolved phylogenetic tree is required, as the branching patterns contain a stronger signal about the underlying diversification dynamics.

### Advanced Topics: Conditioning the FBD Process

When using the FBD process as a prior, it is necessary to condition it on the observed outcome to ensure a valid probability distribution. We are analyzing a clade that, by definition, was successful enough to be discovered. We must therefore condition on the process not going extinct without leaving any trace. Two common conditioning schemes are used in practice [@problem_id:2714600].

**Stem Conditioning**: In this scheme, the analysis is conditioned on the process producing at least one sampled extant lineage. The tree is parameterized by its **origin time** ($t_{or}$), also known as the stem age. This is appropriate when the research question concerns the entire evolutionary history of a [clade](@entry_id:171685), including the lineage leading to its first major split. The tree prior is the FBD density divided by the probability of observing at least one extant sample given an origin at $t_{or}$.

**Crown Conditioning**: This scheme is used when the focus is on the diversification of the living members of a clade. The analysis is conditioned on the process producing at least two sampled extant lineages, which defines a "crown group". The tree is parameterized by the age of the [most recent common ancestor](@entry_id:136722) of these sampled extant species, the **crown age** ($t_c$). This involves a mathematical [reparameterization](@entry_id:270587) that integrates over the unknown duration of the stem lineage (from $t_{or}$ to $t_c$).

The choice between stem and crown conditioning depends on the data available and the specific hypothesis being tested, as it changes the [prior distribution](@entry_id:141376) on the age of the [clade](@entry_id:171685)'s root.