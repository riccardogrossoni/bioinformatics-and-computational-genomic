method used to decide whether two samples are similar or not. There are many distance functions and it's important to choose the more appropriate one based on the experiment. 
## Metric distances
A distance measure between two vectors *i , j* must obey several rules:
- It must be positive and definite
- It must be symmetric
- It must respect the triangle inequality: when considering three objects, i, j and k, the distance from i to k is always less than or equal to the sum of the distance from *i* to *j* and the distance from j to k ($d_{ik} ≤ d_{ij} + d_{jk}$)
## Distance matrix
We can represent distances as matrices, here the value in a row *i* and column *j* is the distance between the sample *i* and the sample *j*. These matrices must be symmetric.
## Distance functions
- **Euclidian distance**: ![[Formula_euclidian_distance.png]]
- **Correlation distance**:![[formula_correlation_distance.png]]
- **Manhattan distance**: The distance between two points as the sum of the absolute difference of their coordinates$$d_{ij}^M=\sum_{k=1}^N|x_i^k-x_j^k|$$
## Distance between groups of feature vectors
- **Single linkage**:  With single linkage distance between two clusters is defined as the smallest distance between an element of the first cluster and an element of the second cluster. This method has a **Chaining issue** since it tends to "force" clusters together due to single entities being close regardless of the "average distance" of the two clusters.
- **Complete linkage**: With complete linkage distance between two clusters is defined as the maximum distance between an element of the first cluster and an element of the second cluster. This tends to not be used due to an expected huge amount of noise. This method also produces compact clusters, which can be useful if entities of the same cluster are expected to be far apart. 
- **Average linkage**:  With average linkage distance is defined as the average of all pairwise distances. Is more computationally expensive and is "half-way" between the other 2 distances, but there is no chaining issue and no "special favors" to outliers, so it's the most popular method used. It is also called **UPGMA** (unweighted pair group method using arithmetic averages).
## UPGMA
UPGMA is a distance measure used often to create phylogenic trees. The basic principle is to create a distance matrix between strings filling as cells the substitution distance (meaning a +1 each time 2 characters do not align) and grouping the 2 less distant ones.
![[UPGMA_step1.png]]
Here we can see that the 2 less distant strings are ATCC and ATGC, resulting in distance 1. We will group them together and recalculate the distance:
![[UPGMA_step2.png]]
Now the other 2 are the less distant, we now have only 2 stings (the two groups) and we can merge them together resulting in a phylogenic tree like this:
![[UPGMA_final_tree.png]]