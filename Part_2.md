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




### Knowledge graph construction and inference