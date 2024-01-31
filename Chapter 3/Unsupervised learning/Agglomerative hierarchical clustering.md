The basics is to generate a hierarchy of clusters going from n clusters of 1 element each to 1 cluster of n elements
1) input: For each gene there's one feature vector;
2) Each cluster at the beginning consists of one gene;
3) The [[distance]] between each pair of clusters is computed;
4) The two clusters with the smallest distance are merged;
5) Repeat from step 2;
The output is a **Dendrogram** which is a tree-like structure with the genes at the bottom as leafs, and the joins represent the distance between the left an right branches.
![[Agglomerative_hierarchical_clustering.png]]
A threshold on the dendrogram levels will define the clustering (for example if we set the threshold at level 4 we will have 2 clusters, one containing "ab" the other containing "cde").

