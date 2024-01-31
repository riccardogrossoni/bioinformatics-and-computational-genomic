The basis of enrichment analysis is that with a list of genes that we found relevant in a studied condition we want to understand why they are (relevant). The goal is to *detect significant enrichments and/or depletions of annotation terms (e.g. Gene Ontology (GO) terms) within a target set of genes of interest, with respect to a master set (target-master scenario)*.
## Basis
Before starting this analysis we must:
- Know which are all the known features of such genes
- Evaluate which of such features (if any) make a gene having them likely belonging to such group of genes
For the first point we can retrieve all the information from known annotations of the gene (e.g. from[[ gene ontology]]) and then for the second point we consider their annotation terms and test which of them, if any, are significantly more/less annotated to the found genes w.r.t. all the studied genes.
## Problem statement
Input:
- Master set of $n_A$ genes or gene products
- Target set of $n_B$ genes or gene products
- Controlled vocabulary term $t_i$
- Annotation database where each gene or gene product is annotated to zero or more terms from the controlled vocabulary.
Output:
- Indication of over representation (called **enrichment**) or under-representation (called **depletion**) of the term $t_i$ in the target set
	- usually *p-value* is used as significance level
Note that no new annotation is generated with enrichment analysis.

We also define for each term $t_i$:
- $n_T$: number of master set genes or gene products annotated to $t_i$
- $k$: number of target set genes or gene products annotated to $t_i$
As we did in [[Chapter 3 - microarray data analysis]] we must develop an hypothesis framework:
- We define a null hypothesis and a null distribution
- We compute the significance (p-value in our case) of the observed data
- We compare the p-value to the significance level threshold we set

## Null hypothesis
- Under the null hypothesis belonging to target set (called B) is independent from being annotated with term t.
- The probability of observing k genes in the target set annotated to the term t is given by the hypergeometric distribution: $$P(N_{B\cap T}=k)={{n_T \choose k}{n_A - n_T\choose n_B -k}\over {n_A\choose n_B}}$$
The formula defines the probability of finding k genes annotated to *t* in the target set B under the null hypothesis. We want to find AT LEAST k genes, so we calculate: $$p=\sum_{k \geq n_{B\cap T}}P(N_{B\cap T}=k)$$
if p is greater than the threshold we set, then we accept the null hypothesis, otherwise we reject it, stating that the target set B is **dependent** from being annotated with the term *t* (term t significantly enriched).
## Biological interpretation
Annotation of genes (or gene products) to controlled vocabulary terms means that the annotated genes (or gene products) have the features described by the controlled terms. Terms statistically significantly enriched in a target set of genes represent the gene (gene product) features that make those genes (gene products) belonging to the target set. 
If we selected the target set as genes that are differentially expressed in a given biological condition, then the enriched terms represent the features that make those genes differentially expressed. Thus, they represent the significant features in the given biological condition.
## Multiple test correction
As in data analysis, the threshold controls the false positive rate (more lenient threshold means more false positives). This is true only when testing the enrichment of one annotation at a time. When using multiple annotation terms together (this is the usual case) multiple testing correction is needed. 
The methods remain the same as in chapter 3 (see [[Chapter 3 - microarray data analysis#Multiple testing correction]]).
## Ontology based analysis
Until now we have seen methods that assume that all the multiple tests are independent (the terms are independent), but when using ontological annotations we have an intrinsic dependency parent-child between annotation terms. 
## New approach (gene set enrichment analysis)
Let's consider 2 alternative conditions and the relevance of genes based on the ranking (e.g., based on differential expression between the two conditions).
Considering a gene characteristic, how does gene with that characteristic perform in the ranking?
Compute an enrichment score reflecting the degree to which the characteristic is overrepresented at the extremes (top or bottom) of the ranked gene list.
The characteristic can be any, including be part of a gene set (signature) know relevant for a biological condition (shift from single-gene to gene set evaluation, since cellular processes often affect gene sets acting in concert, rather single genes).

Gene set Enrichment Analysis ([[GSEA]]) is a computational method comparing a ranked list of genes L to gene sets/signatures defined based on prior biological knowledge, to determine whether the gene set shows statistically significant, concordant differences between two biological states (e.g. two phenotypes, normal or diseased conditions).

