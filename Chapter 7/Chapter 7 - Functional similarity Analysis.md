The goal of functional similarity analysis is to compute functional similarity between genes based on annotations describing their functions.
The traditional methods have been sequence similarity and analysis of correlation (co-expression) in a gene expression, using for example microarray experiments. The issue is that in the majority of co-functioning genes neither of them is sequence related, they do not encode proteins in the same family or pathway and they can be expressed at different time points.
We make an hypothesis: if two genes have similar functional annotation profiles, they should be functionally related.
We call the measure of functional similarity based on gene **Annotation profiles**. They are expressed via controlled vocabularies and ontologies (e.g. [[Gene Ontology]]).
## Computing similarity based on annotation profile
Typically with ontological annotations first we compute the ontological **term to term** similarity, then the gene to gene similarity based on annotation profile. There are some optional additional steps which are to compute gene similarity based on multiple ontologies and compute gene clustering based on functional similarity.
For the first step we can have different methods:
- Ontology topology based methods:
	- Compute the distance between two ontological terms by counting the number of arches between them within the ontology;
	- Shortest or average distance is used for multiple paths;
	- The issue is that it assumes that nodes and arches are distributed uniformly in an ontology, which is usually not true.
- Information theoretic methods (such as Singular Value Decomposition)
	- Are less sensitive to arch density variability.
## Term to term similarity
The most common method for computing term to term similarity requires 5 steps:
1) Firstly we compute the frequency of occurrence of a term in a corpus (a corpus is for example all gene annotations to the ontology terms) as $$Freq(c)=\sum\{occur(c_i)|c\in Ancestors (c_i)\}$$$$Prob(c)={Freq(c)\over maxFreq}$$
2) Compute the [[information content]] (IC) of a term (in a corpus) as $$IC(c)=-log(Prob(c))$$Generally, the more rare (specific) the term, the higher is its IC, the more common the lower it will be.
3) Find the common ancestors of two terms as $$CommonAnc(c_1, c_2)=Ancestors(c_1)\cap Ancestors(c_2)$$
4) Compute the shared information between two terms as $$Share(c_1,c_2)=max\{IC(a)|a\in CommonAnc(c_1,c_2)\}$$That is, the information content of the [[Lowest Common Ancestor (LCA)]]
5) Compute the similarity metrics between two terms. For this point there are various metrics available (see [[Similarity_metrics(term-to-term).png]])
## Gene to gene similarity
![[step_1_gene_to_gene_simil.png]]

We can then compute the similarity metrics similarly to what we did in the previous paragraph, and also in this case we have various methods that are available in [[Similarity_metrics_gene_to_gene.png]]
## Validation
To validate the functional similarity metrics we apply 3 approaches:
- Use structural information (sequence similarity)
- Use gene expression data (e.g. microarray experiments)
- Assessing the functional consistency of clustering
Each of these approaches have different limitations.

