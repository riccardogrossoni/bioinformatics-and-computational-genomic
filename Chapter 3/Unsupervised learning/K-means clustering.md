With k-means we must first define a number of clusters *k*, then we have to designate a cluster center for each cluster.
Now we can start the procedure:
1) Assign each data point to the closest cluster center, now that data point is part of that cluster
2) calculate the new cluster center using the geometric average of all the members of the cluster
3) Calculate the sum of within-cluster sum-of-squares of distances of cluster elements from cluster centroid. With this value, if it has not changed significantly (over a certain threshold) for a certain number of iterations halt the process and return the resulting clusters, otherwise, if it has changed, repeat from step 1.
The main problem is that if the first partitions are not chosen carefully there's a chance that the algorithm halts at a local minimum and not at the global minimum.
To avoid this problem usually the algorithm is run multiple times with different starting positions, to see if the algorithm halts at the same minimum.
But this means that the actual computation is computationally expensive and time consuming.
