# Part 2: Summary of Knowledge Graphs - Chapter 8 & 9

Chapter 8 provides conceptual foundations of instance matching and practical implementation of instance matching
Conceptual foundations encompasses instance matching, and formalism for instance matching. Practical implementation of instance matching includes two-step pipeline and post-similarity steps.

Chapter 9 outlines concetps in statistical relation learning which is incorporated into the KG process using useful frameworkds. The chapter consists of foundations of statistical relational learning and knowledge graph construction and inference.


### Conceptual Foundations of Instance Matching

- **Instance matching** is the challenge of grouping mentions of the same real-world entity within a knowledge graph (KG). This task is difficult for machines due to semantic ambiguity, which humans often resolve using context and domain knowledge. Without accurate ER, fundamental KG operations like counting unique entities become unreliable, and advanced analysis through aggregations and summarizations is hindered. Inconsistencies in KG creation, such as variations in citation details for the same publication, highlight the importance of contextual understanding in ER. Furthermore, ER is essential for consolidating information from different mentions of the same entity, preventing data inconsistencies. Despite five decades of research, achieving human-level ER performance across various domains remains an open AI problem, largely due to the necessity for significant tuning and training.


- **Formalism for instance matching**

Pairwise Linking Function<br>
Definition: A function that takes two entities (e.g., two nodes in a KG, such as citation 1 and citation 4) and determines whether they refer to the same real-world object. It outputs a binary decision based on features like shared attributes  or contextual embeddings. This function is crucial for the initial step of IM, enabling direct comparison between pairs of entities. It forms the foundation for identifying potential matches by evaluating similarity at a granular level. 

Clustering Linking Function<br>
Definition: A clustering linking function extends the pairwise approach by grouping multiple entities into clusters where all entities within a cluster are deemed to refer to the same real-world object. Instead of just comparing pairs, it considers transitive relationships This function often builds on pairwise similarity scores, using clustering algorithms to form these groups. The clustering linking function is vital for scaling IM to larger datasets, as it reduces redundancy by grouping all related entities together, not just pairs. 

The pairwise linking function directly tackles semantic ambiguity by providing a systematic way to compare entities, while the clustering linking function addresses broader inconsistencies by ensuring transitive matches are captured, despite the lack of human-level performance in AI systems.

### Practical implementation of instance matching

**Blocking**<br>
blocking mitigates the quadratic complexity of comparing all pairs of mention nodes in a knowledge graph (KG) by clustering similar entities into overlapping blocks using a blocking scheme. A key component of this scheme is the blocking key (K), defined as a many-many function that takes a mention node and returns a non-empty set of literals called blocking key values.

**Similarity**<br>
The second step to the two-step forumation is similarity in which the pairs must undergo similarty computations to filter out the subset of all that comprises the nonduplicate mention pairs after blocking. It behaves as a scoring mechanism where each pair receives a score between 0 and 1, with higher scores indicating greater likelihood of matching.

## Foundations of statistical relational learning 

statistical relational learning (SRL) is a key approach for working with knowledge graphs (KGs), which often contain complex relational dependencies that violate the i.i.d. assumption. SRL frameworks like Probabilistic Soft Logic (PSL) and Markov Logic Networks (MLNs) are of interest with this process for their ability to model and infer over these dependencies by integrating logic and probability theory. This chapter focuses on SRL's application to KGs, particularly in addressing the KG identification problem. 

Modeling dependencies in statistical relational learning (SRL) involve capturing the relational and structural connections between entities in a knowledge graph (KG), which do not follow the independent and identically distributed (i.i.d.) assumption. 

Statistical relational learning (SRL) frameworks are crucial for modeling dependencies in non-independently and identically distributed (i.i.d.) data, such as knowledge graphs. By integrating statistical and relational learning, SRL addresses uncertainty and dependencies, facilitating tasks like collective classification, link prediction, and link-based clustering.

A unified SRL framework should combine first-order logic with probabilistic graphical models, offer straightforward representations for typical SRL problems, and accommodate diverse inference methods (statistical, probabilistic, and logical). Frameworks such as Markov Logic Networks (MLNs) and Probabilistic Soft Logic (PSL) have successfully incorporated substantial domain knowledge.

**Markov Logic Networks**

A statistical relational learning framework that combineds first-order logic with Markov random fields for reasoning over uncertain relational data like knowledge graphs, where standard i.i.d. assumptions fail. MLNs use weighted first-order logic rules (e.g., Friends(A, B) ∧ VotesFor(A, P) → VotesFor(B, P) with a weight indicating confidence) to define relationships. These soft rules are converted into a Markov random field by grounding variables. The joint probability distribution is based on rule weights, favoring configurations satisfying more or higher-weighted rules. MLNs perform inference (predicting unknown relationships) and learning (adjusting rule weights from data).


https://link.springer.com/article/10.1007/s10994-006-5833-1

**Probabalistic Soft Logic** 

Probabilistic Soft Logic (PSL) models uncertain relational data by combining first-order logic with continuous probabilistic reasoning. It uses a hinge-loss Markov random field to optimize configurations that best satisfy weighted rules, which act as soft constraints penalized proportionally to violation. PSL works by defining rules with continuous truth values, assigning weights to indicate importance, modeling joint probability distributions, and inferring likely truth values while learning from data.

### Knowledge graph construction and inference
Knowledge graph construction (KGC) sees challenges due to uncertainty in named entity extraction and relationship identification. Probabilistic outputs from ML models are often converted to labels using set thresholds. Additionally, knowledge graphs built with NLP are frequently noisy and sparse. Knowledge graph identification (KGI) addresses the problem of selecting relevant data from these messy triples.

Knowledge graphs often contain errors like incorrect or missing links due to limitations in NLP and other extraction methods. Statistical relational learning (SRL) is a suitable framework for KGI because it can model relationships and manage uncertainty arising from noisy inputs such as incorrect triples. Incorporating domain knowledge, noise awareness, and system confidence is crucial. A specific SRL-based model utilizes joint reasoning over entity resolution, ontological constraints, and information extraction to refine a noisy KG into a more complete one by correcting errors, and removing incorrect links.

Extensive article on building KG: https://towardsdatascience.com/build-query-knowledge-graphs-with-llms/

### Referernces 

Kejriwal, Mayank, Craig A. Knoblock, and Pedro Szekely. 2021. Knowledge Graphs: Fundamentals, Techniques, and Applications. Cambridge, MA: MIT Press. [ISBN-13: 978-0262045094] Chapter 8 Instance Matching, pages 175–220, Chapter 9 Statistical Relational Learning, pages 221–240.

Richardson, Matthew, and Pedro Domingos. "Markov Logic Networks." Machine Learning 62, no. 1-2 (2006): 107-36. https://doi.org/10.1007/s10994-006-5833-1.

