## Applications and Interdisciplinary Connections

Having understood the machinery of the Local Average Treatment Effect (LATE), we can now embark on a journey to see it in action. You might be surprised to find that the logic we’ve developed is not some esoteric concept confined to textbooks. It is a powerful lens through which scientists, doctors, and policymakers look at the world to answer some of the most pressing causal questions. The beauty of LATE lies in its versatility; its core idea appears in wildly different fields, unifying them in the quest to separate correlation from causation. We will see how a simple “nudge,” a rule in a handbook, a doctor's habit, or even the genetic lottery of our birth can serve as a key to unlock causal truths.

### The Gentle Nudge: Encouragement and Compliance

Perhaps the most intuitive application of LATE comes from what we call “encouragement designs.” Imagine a public health department wants to know if a text-message reminder system *causes* more adolescents to get vaccinated. They can't just compare those who use the reminders to those who don't—the people who sign up might be more health-conscious to begin with!

So, what can they do? They can randomly *encourage* half the families to sign up for the reminders. This random encouragement is our instrument, $Z$. Not everyone encouraged will sign up (non-compliance), and a few might sign up even without the encouragement (also non-compliance). But now we can ask a brilliant question: what is the effect of the reminders on the very people whose decision to enroll was changed by our encouragement? This is precisely the LATE. We estimate it by taking the effect of the encouragement on vaccination rates (the "Intention-to-Treat" or ITT effect) and adjusting for the fact that not everyone complied [@problem_id:4550162].

This ITT effect is a "diluted" version of the true effect of the treatment on the people it sways (the compliers). The relationship is beautifully simple: the observed ITT effect is just the LATE multiplied by the proportion of the population who are compliers.

$$
\text{ITT} = p \times \text{LATE}
$$

where $p$ is the compliance rate, which is the proportion of people who take up the treatment because of the encouragement [@problem_id:4603203]. This formula is our "magnifying glass." We can measure the ITT effect directly from our randomized groups and we can measure the compliance rate $p$. With those two numbers, we can calculate the LATE—the undiluted effect of the treatment on the compliers [@problem_id:4603125] [@problem_id:4852282].

This "encouragement" doesn't even have to be part of a formal experiment. In another scenario, public health officials noticed that people living closer to a vaccination clinic were more likely to get a flu shot. Is it just that these people are different, or does proximity *cause* vaccination? Here, proximity to the clinic acts as a natural encouragement. By treating proximity as an instrument, we can estimate the causal effect of the vaccine on preventing influenza, but specifically for the group of people who get vaccinated simply because it's convenient—the compliers [@problem_id:4525690].

### The Bright Line: Finding Experiments in Rules

Sometimes, a [natural experiment](@entry_id:143099) is hiding in plain sight within a rulebook. Consider a government program like Medicaid, where eligibility is determined by a sharp income cutoff relative to the Federal Poverty Level. For instance, people with income just below 138% of the FPL are eligible, and those just above are not.

Of course, people on either side of this line are, on average, very similar. Yet, one group gets a powerful "push"—eligibility—while the other does not. This setup is known as a Regression Discontinuity design. But we know that not everyone who becomes eligible will actually enroll in Medicaid. The program has imperfect compliance. This is what we call a "fuzzy" regression discontinuity, and it is a perfect job for LATE!

Here, the instrument $Z$ is being eligible (i.e., being just below the income threshold). The treatment $D$ is actual enrollment in Medicaid. The LATE then tells us the causal effect of enrolling in Medicaid on, say, having health insurance coverage, but specifically for the population of individuals at the threshold whose enrollment decision is tipped by gaining eligibility [@problem_id:4384322]. It's a wonderfully clever way to use a program's own rules to evaluate its true impact.

### Human Nature as an Instrument: The Habits of Physicians

The source of our "instrument" can be even more subtle, rooted in human behavior itself. Imagine we want to compare a new drug, a DOAC, to an older drug, warfarin, for preventing strokes. A simple comparison is fraught with peril; doctors may prescribe the new drug to healthier or sicker patients, hopelessly confounding the results.

Here, researchers found a clever instrument: the prescribing preference of the physician. Some doctors have a habit of preferring the new drug, while others stick to the old one. We can argue that for many patients, the particular doctor they see is somewhat random (after accounting for factors like geography and specialty). A doctor's preference, therefore, acts as a "push" or "nudge" toward one drug over the other.

By using the physician’s preference as an instrument, we can estimate the causal effect of DOAC versus warfarin. The LATE we uncover is not the effect for all patients, but the effect for a very specific and policy-relevant group: the "compliers." In this case, compliers are the patients who would receive warfarin from a doctor with a low-preference for DOAC, but would be switched to DOAC if they saw a high-preference doctor. This is a powerful technique in health services research, leveraging the natural variation in clinical practice to get at causal answers [@problem_id:4597360].

### The Ultimate Lottery: Mendelian Randomization

Perhaps the most profound application of the LATE framework comes from a field that connects us all: genetics. For decades, epidemiologists have struggled to determine whether risk factors like high cholesterol truly *cause* heart disease, or are merely correlated with it through lifestyle and other behaviors.

Enter Mendelian Randomization (MR). The core idea is that nature conducts its own randomized trial at our conception. We are all dealt a random hand of genetic variants from our parents. Some of these variants are known to slightly increase or decrease levels of certain exposures, like cholesterol, throughout our lives.

This genetic variant becomes our instrument, $G$. It's randomly assigned (satisfying the independence assumption). It influences an exposure, like cholesterol ($X$). And, crucially, it should not affect the outcome, heart disease ($Y$), through any other pathway (the exclusion restriction).

When we apply the IV machinery here, the Wald ratio gives us a LATE. It is the causal effect of the exposure (cholesterol) on the outcome (heart disease) for the subpopulation of individuals whose cholesterol level is influenced by that specific genetic variant [@problem_id:5211224] [@problem_id:5058912]. This has been a revolutionary tool, allowing scientists to confirm causal relationships for many risk factors and to debunk others, all by exploiting "nature's RCT." It is a stunning example of the unity of scientific ideas, linking genetics, epidemiology, and causal inference.

### A Universal Lens

The power of LATE extends far beyond medicine and public health. Economists and policy experts use this tool constantly. Imagine evaluating a national reform aimed at making essential medicines more affordable. The reform might be rolled out unevenly across different districts based on some eligibility index. This index can serve as an instrument to evaluate the causal effect of the reform on drug prices, but specifically for the districts that were induced to comply by the new eligibility rule [@problem_id:5003589]. The same logic applies to evaluating the effect of smaller class sizes on student learning (using enrollment caps as an instrument), the effect of job training programs on employment (using random offers as an instrument), and countless other questions across the social and biological sciences.

What all these examples share is a certain intellectual honesty. The LATE does not pretend to give us *the* single, universal causal effect for everyone. Instead, it provides something much more valuable: a valid, believable causal effect for a specific, well-defined, and often policy-relevant subpopulation—the compliers. It tells us the effect of a treatment on the very people who can be moved. In doing so, it doesn’t just give us a number; it gives us a deeper understanding of how the world works.