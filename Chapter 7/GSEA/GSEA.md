## Basis
Genes from an expression dataset are ordered in a ranked list called **L** based (usually) on their differential expression between two classes. 
We then take a previously defined gene set **S** and GSEA determines whether members of S are randomly distributed throughout L or occur primarily toward the top or bottom of the list. 
An enrichment score indicates if the genes in set S are clustered towards the beginning or end of the ranked list L and if that is the case, the gene set is correlated with the class distinction.
## STEP 1
GSEA begins with the calculation of the enrichment score $ES(S)$: This value reflects the degree a set S is overrepresented at the extremes of the ranked list L. The score is calculated by walking down the list L, increasing a running sum statistic when a gene S is met or decreasing it when genes NOT in S are met. The magnitude of the increment depends on the correlation of the gene with the phenotype/class. The enrichment score is the maximum deviation from zero in the random walk.
For a randomly distributed S, ES(S) will be relatively small, but if it is non randomly concentrated at the top or bottom of the list, ES(S) will be correspondingly high.
## STEP 2
The step 2 consists in the **estimation of significance level of ES**. To do so we use a permutation test: 
- We first randomly assign original phenotype labels to samples, we then reorder genes and re-compute ES(S)
- We repeat this previous step to perform 1000 permutations to generate a null distribution and create a histogram of the corresponding enrichment scores ESNULL
- We estimate empirically the significance observed ES(S) relative to null distribution ESNULL scores, using the positive or negative portion of the distribution based on sign of observed ES(S)
## STEP 3 
Consists in the **adjustment for multiple hypothesis setting**. When an entire collection of gene sets is evaluated, any estimated significance level must be adjusted to account for multiple hypothesis testing:
- For each gene set S' we compute ES(S')
- For each S’, take 1000 fixed permutations π of phenotype labels, reorder the genes in L and determine ES(S’, π)
- We normalize the observed ES(S') and the ES(S', $\pi$) to account for size of S', separately rescaling the positive and negative scores dividing by the mean of ES(S, π), to yield normalized enrichment scores NES(S’) and NES(S’, π).
- We compute the false discovery rate FDR of each NES by comparing the tails of the observed and null distributions for the NES, separately for negative and positive scores