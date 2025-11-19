## Introduction
The explosion of population-scale sequencing has revealed that a single [linear reference genome](@entry_id:164850) is inadequate to capture the full spectrum of human and species-wide [genetic diversity](@entry_id:201444). Complex structural variations, insertions, and deletions are difficult to represent and analyze in a linear coordinate system, leading to [reference bias](@entry_id:173084) and missed discoveries. To address this, the field of [bioinformatics](@entry_id:146759) has shifted towards pangenome graphs—a powerful [data structure](@entry_id:634264) that compactly represents the genomes of an entire population, including all their variations, within a single, unified network. This approach moves beyond a single point of reference to embrace [genetic diversity](@entry_id:201444) as a core feature of the model.

This article serves as a comprehensive guide to understanding and utilizing these complex but powerful representations. It bridges the gap between the traditional concept of a linear sequence and the dynamic reality of a variable, branching [pangenome](@entry_id:149997). The journey begins with the first chapter, **"Principles and Mechanisms,"** which deconstructs the foundational theory behind variation graphs, exploring how they are built, navigated, and used to model everything from simple SNPs to complex [chromosomal rearrangements](@entry_id:268124). The second chapter, **"Applications and Interdisciplinary Connections,"** showcases the transformative impact of pangenome graphs across genomics, evolutionary biology, and medicine, and even reveals surprising connections to fields like digital humanities and [game theory](@entry_id:140730). Finally, the **"Hands-On Practices"** section provides an opportunity to engage directly with core computational problems in [pangenomics](@entry_id:173769), solidifying theoretical knowledge through practical implementation.

## Principles and Mechanisms

The limitations of a single [linear reference genome](@entry_id:164850) have become increasingly apparent as population-scale sequencing has revealed the vast extent of [genetic variation](@entry_id:141964), including complex [structural variants](@entry_id:270335), that are difficult to represent in a linear coordinate system. Pangenome graphs have emerged as a powerful alternative, providing a data structure that can compactly represent the genomes of an entire population or species, including all their variations. This chapter elucidates the fundamental principles of pangenome [graph representations](@entry_id:273102) and the mechanisms by which they encode and enable the analysis of genomic diversity.

### From Linear Sequences to Variation Graphs

A [linear reference genome](@entry_id:164850) represents a chromosome as a single, contiguous string of nucleotides. A genetic locus is identified by an integer coordinate, representing its offset from the start of the sequence. While simple and effective for many applications, this model struggles to accommodate structural variations such as insertions, deletions, and rearrangements. An insertion on an alternate haplotype, for instance, disrupts the coordinate system for all downstream loci on that [haplotype](@entry_id:268358) relative to the reference. Similarly, a deletion in a sample means that a range of reference coordinates has no corresponding position in that sample's genome.

Pangenome variation graphs address these issues by abstracting the genome into a more flexible structure. In its most common form, a **variation graph** is a **[directed graph](@entry_id:265535)** where nodes are labeled with DNA sequences and edges represent observed adjacencies between these sequences. A complete chromosome or [haplotype](@entry_id:268358) is no longer a single string but an **embedded path**—a specific walk through the graph that concatenates the sequences of the nodes it visits.

Consider a simple example involving a single-nucleotide polymorphism (SNP), a small insertion, and a small deletion [@problem_id:2818225].
- A **SNP** where an adenine (A) in the reference is a guanine (G) in an alternate [haplotype](@entry_id:268358) can be represented by a "bubble" structure. A node containing the sequence upstream of the SNP connects to two parallel nodes—one containing 'A' and the other 'G'—which both then connect to a single node containing the downstream sequence. The reference path traverses the 'A' node, while the alternate path traverses the 'G' node.
- An **insertion** is represented by a bubble where one path is a direct edge between two nodes, while the alternate path traverses an additional node containing the inserted sequence.
- A **deletion** is represented by a bubble where the reference path traverses a node containing the deleted sequence, while the alternate path is a direct edge that bypasses this node.

In all these cases, genetic variation is encoded as alternative paths that diverge and reconverge, maintaining the **colinearity** of the shared flanking sequences. This structure naturally represents the idea that different alleles occupy the same "locus," which is defined by the branching and merging points of the bubble [@problem_id:2818225].

### Formalizing the Graph Model and Its Construction

To handle the full complexity of genomes, including inversions and reverse-complementary sequences, the simple [directed graph](@entry_id:265535) model is extended to a **bidirected [sequence graph](@entry_id:165947)**. In a bidirected graph, each node has two ends, or "sides" (e.g., representing the $5'$ and $3'$ ends of the DNA segment). Edges connect specific ends of nodes, allowing the graph to encode not just adjacency but also the relative orientation of segments. This is essential for representing DNA, which can be traversed on either its forward or reverse-complement strand.

In this model, nodes typically represent maximal, non-branching homologous sequence segments, sometimes called **unitigs**. Each individual genome from the source population is then represented as an embedded path that traces the specific order and orientation of these segments in that genome [@problem_id:2476523]. This formal structure is superior to other representations for capturing both sequence content and [synteny](@entry_id:270224):
- It is more semantically rich than a **de Bruijn graph**, which atomizes sequences into short $k$-mers and loses long-range information.
- It explicitly models adjacency, unlike **string-based methods** like suffix arrays, which are powerful for finding substring occurrences but cannot represent structural rearrangements.
- It is a direct representation of DNA sequence, unlike **functional networks** (e.g., co-expression graphs) which model relationships between genes based on their activity, not their physical structure [@problem_id:2476523].

One popular implementation of this model is the **Graphical Fragment Assembly (GFA)** format. GFA uses `S` lines for Segments (nodes), `L` lines for Links (edges, specifying the connected node ends and their orientations), and `P` lines for Paths (embedded haplotypes) [@problem_id:2412180].

While graphs built from aligning and merging homologous segments are common, another paradigm for graph construction is based on **de Bruijn graphs (DBGs)**. In a DBG, nodes are all unique $k$-mers (sequences of length $k$) present in the input genomes, and an edge connects two nodes if they represent overlapping $(k-1)$-mers. The choice of $k$ is critical and involves a fundamental trade-off [@problem_id:2412185].
- A **large $k$** increases specificity. Longer $k$-mers are more likely to be unique, helping to resolve short repeats and isolate sequencing errors into simple, identifiable motifs (like "tips" or small bubbles). However, this high specificity makes the graph fragile; a single [polymorphism](@entry_id:159475) can break the $(k-1)$ overlap requirement, fragmenting the graph into disconnected components, especially in highly variable or low-coverage regions.
- A **small $k$** increases connectivity. With shorter required overlaps, it's easier to connect across polymorphic sites, resulting in a more contiguous graph. However, this comes at the cost of specificity. Short $k$-mers are more likely to be shared by chance or to occur in multiple, unrelated genomic regions (e.g., paralogous genes, repeats). This collapses distinct sequences into the same nodes and paths, creating a highly complex and tangled graph with many spurious bubbles that do not represent true allelic variation [@problem_id:2412185].

### Navigating the Pangenome: Coordinate Systems

A key challenge in using [pangenome](@entry_id:149997) graphs is defining and translating genomic positions. A single integer coordinate is no longer sufficient. Several [coordinate systems](@entry_id:149266) are used:
1.  **Path-based Coordinates**: A position can be specified as a pair $(P, t)$, where $P$ is a specific embedded path and $t$ is the cumulative $1$-based offset along that path. This is intuitive but specific to one [haplotype](@entry_id:268358).
2.  **Node-relative Coordinates**: A position can be given as a pair $(v, o)$, where $v$ is a node identifier and $o$ is the $1$-based offset within that node's sequence.

Translating coordinates between haplotypes is a core operation. If two paths, $P_1$ and $P_2$, differ only by SNPs, they have the same length, and there is a simple one-to-one mapping between their coordinates. Homologous bases share the same cumulative offset [@problem_id:2818225].

However, if the paths differ by insertions or deletions (indels), the relationship becomes a **[piecewise affine](@entry_id:638052) function**. Consider mapping from a reference path $R$ to an alternate [haplotype](@entry_id:268358) $H$.
- In regions where $R$ and $H$ are identical, the [coordinate mapping](@entry_id:156506) is $t_H = t_R$.
- If $H$ has an insertion of length $L$ relative to $R$, then for all positions downstream of the insertion, the coordinates on $H$ will be shifted: $t_H = t_R + L$.
- If $H$ has a [deletion](@entry_id:149110) of length $L$ relative to $R$, the coordinates downstream will be shifted: $t_H = t_R - L$. The positions on $R$ that were deleted have no homologous coordinate on $H$.

This demonstrates that a coordinate on one path may not have a counterpart on another. A single node-relative coordinate $(v, o)$ is also insufficient to uniquely identify a comparative locus across all alleles, because homologous positions can reside in different nodes (e.g., the 'A' and 'G' nodes in a SNP bubble) [@problem_id:2818225].

### Representing Genomic Diversity and Structure

Pangenome graphs provide a unified framework for representing many facets of genomic variation, from population diversity to complex structural events.

#### Core and Accessory Genomes

The concepts of a **core genome** (sequences shared by all or nearly all individuals) and an **[accessory genome](@entry_id:195062)** (sequences present in only a subset) can be quantified directly on the graph. By defining a **coverage** or **support** function $c(v)$ for each node $v$ as the number of embedded haplotype paths that traverse it, we can classify nodes. Nodes with high coverage (e.g., $c(v) = N$ for $N$ total samples) belong to the core genome, while nodes with low coverage ($c(v) \lt N$) belong to the [accessory genome](@entry_id:195062) [@problem_id:2476523].

#### Structural Variation and Complex Events

The graph model excels at representing complex structural variations.
- **Gene Fusions**: An interchromosomal gene fusion creates a novel adjacency between two previously unlinked segments. To represent this in a GFA-based graph, the two nodes containing the fusion breakpoints must first be split. This creates new node ends at the exact breakpoint locations. A new `L` (Link) record is then added to connect the appropriate ends of the newly created nodes, explicitly representing the fusion adjacency. Finally, a new `P` (Path) record is defined for the sample carrying the fusion, which traces the path across this new interchromosomal link [@problem_id:2412180].
- **Circular Genomes**: Genomes like plasmids or bacterial chromosomes are circular. A [directed graph](@entry_id:265535) can only represent this as a directed cycle. However, many [graph algorithms](@entry_id:148535) require a **Directed Acyclic Graph (DAG)**. To represent a circular genome in a DAG, the cycle must be broken by removing the "wrap-around" edge. This linearizes the genome, creating an artificial [source and sink](@entry_id:265703). This action has consequences: it destroys the symmetric [reachability](@entry_id:271693) of the cycle and loses the adjacency information at the break point. To preserve all sequence context, it is necessary to duplicate at least one segment from the beginning of the linearized path and append it to the end, connected by an edge. This allows any read or substring spanning the original breakpoint to be mapped to a contiguous path in the DAG [@problem_id:2412192].

#### Repetitive and Symmetric Structures

Repeats pose a major challenge. A long [palindromic sequence](@entry_id:170244)—one that equals its own reverse complement—is particularly problematic. In a bidirected graph that merges identical sequences, all occurrences of a palindrome, regardless of their orientation (forward or inverted), will be collapsed into a **single node with reverse-complement symmetry**. Traversing this node from head-to-tail yields the same sequence string as traversing it from tail-to-head [@problem_id:2412196].

This symmetry has profound consequences for [read mapping](@entry_id:168099). A read mapper that uses **canonical $k$-mers** (treating a $k$-mer and its reverse complement as equivalent) will find that seeds from within the palindrome match identically to both orientations of the node. Thus, for any read shorter than the palindrome, its orientation cannot be determined. Furthermore, if the palindrome exists at multiple genomic loci, the read will **multi-map** to all of them. Unique mapping can only be achieved if the read is long enough to span into the unique, non-palindromic flanking sequence of a specific locus [@problem_id:2412196].

#### Relating Graph Topology to Evolutionary Dynamics

The structure of a [pangenome graph](@entry_id:165320) is a direct reflection of the evolutionary processes acting on the population. A comparison between two extreme scenarios is illustrative [@problem_id:2412215]:
- **Rapidly Evolving RNA Viruses**: These populations are characterized by high mutation rates and frequent recombination. Their [pangenome graph](@entry_id:165320) will be highly complex and reticulated. We expect a high **bubble density** (from many SNPs and short indels), a high **branching factor** at variant nodes, and a significant **cycle count** due to recombination shuffling segments. The high haplotypic diversity results in a large number of distinct paths through any given region.
- **Conserved Mammalian Genes**: These are under strong **[purifying selection](@entry_id:170615)**, which removes most new mutations. Recombination within gene bodies is also often suppressed. Their [pangenome graph](@entry_id:165320) will be structurally simple and nearly linear. It will have a very low bubble density, minimal branching, and virtually no cycles. The vast majority of sampled haplotypes will trace the same, highly conserved path.

### Advanced Representations and Interpretations

The basic variation graph model can be extended to handle more complex biological realities and to incorporate statistical uncertainty.

#### Polyploidy and Allele Dosage

In [diploid](@entry_id:268054) organisms, a sample contributes two haplotype paths to the [pangenome](@entry_id:149997). In polyploid organisms with [ploidy](@entry_id:140594) $p$, a sample contributes $p$ paths. It is possible for multiple of these paths to traverse the same branch of a variant bubble, a phenomenon known as **allele dosage**. To represent this without violating the principle of a shared graph topology, the model can be augmented with per-sample edge multiplicities. For each sample $S$, a function $c_S: E \to \{0, 1, \dots, p\}$ is defined on the edges $E$ of the graph. The value $c_S(e)$ records how many of the sample's $p$ haplotypes traverse edge $e$. This can be viewed as a **conserved, integral flow** of value $p$ through the graph for that sample. This is a compact and powerful way to represent copy number and allele dosage without duplicating subgraphs for each sample [@problem_id:2412205].

#### Deriving Consensus and Core Genome Paths

A common task is to extract a single representative "core genome" sequence from the graph. A simple definition might be a path that visits all nodes classified as "core" (e.g., present in $\ge \tau N$ samples). However, due to recombination or complex [structural variation](@entry_id:173359), it is often the case that **no single path visits all core nodes**. The core genome itself may be fragmented across incompatible paths [@problem_id:2412220].

In this situation, the problem must be reframed as an optimization. A principled approach is to define the "core genome path" as the path $P^\star$ that maximizes the number of core nodes it visits. This can be formulated as finding the longest path in a DAG where core nodes have a weight of $1$ and non-core nodes have a weight of $0$. This problem is efficiently solvable using [dynamic programming](@entry_id:141107). A greedy approach, such as always choosing the next node with the highest support, is not guaranteed to find the optimal path and is not a principled solution [@problem_id:2412220].

#### Probabilistic Pangenome Graphs

The standard graph model is deterministic. However, there is often uncertainty in the graph assembly or ambiguity in [haplotype](@entry_id:268358) paths. This can be represented by converting the graph into a probabilistic model. A common approach is to model path traversal as a Markov process [@problem_id:2412160].

At each vertex $v$, the choice of an outgoing edge is treated as a categorical random variable. This means we assign a probability $P(e)$ to each outgoing edge $e \in \mathrm{Out}(v)$, subject to the constraint that the probabilities sum to one locally:
$$
\sum_{e \in \mathrm{Out}(v)} P(e) = 1
$$
This local normalization is crucial; a global normalization across all edges in the graph is conceptually incorrect for modeling sequential choices.

These edge probabilities can be estimated from data, such as read alignments that span across nodes. Using a Bayesian framework, one can place a **Dirichlet prior** on the probability vector for each vertex's outgoing edges. Given observed counts $c(e)$ of reads supporting each edge $e$, the [posterior distribution](@entry_id:145605) over the probabilities is also a Dirichlet distribution. From this posterior, we can compute [point estimates](@entry_id:753543) for the probabilities, such as the **[posterior mean](@entry_id:173826)** or the **maximum a posteriori (MAP)** estimate [@problem_id:2412160]. For an edge $e \in \mathrm{Out}(v)$ with prior hyperparameter $\alpha(e)$ and count $c(e)$, the posterior mean is:
$$
\mathbb{E}[P(e) \mid \mathbf{c}] = \frac{c(e) + \alpha(e)}{\sum_{e' \in \mathrm{Out}(v)} (c(e') + \alpha(e'))}
$$
Once these probabilities are estimated, the probability of any given haplotype path can be calculated as the product of the probabilities of the edges it traverses. This allows for a likelihood-based ranking and quantification of paths, transforming the [pangenome graph](@entry_id:165320) from a purely structural object into a generative statistical model.