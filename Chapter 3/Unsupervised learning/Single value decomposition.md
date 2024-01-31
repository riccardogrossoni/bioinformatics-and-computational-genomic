also known as Principal Component Analysis can be used to reduce dimensionality of the data to summarize the most important components while also filtering out noise, after which a normal clustering algorithm is applied.
Lets consider a matrix mXn, with m the number of genes and n the number of experiments (samples). Each cell of the matrix has the expression level of the corresponding gene in the corresponding sample. The SVD of that matrix (which we'll call A) is defined as: $$A=U\Sigma V^T$$With U a mXr orthogonal matrix, V an nXr orthogonal matrix and $\Sigma$ an rXr diagonal matrix. r is the rank of A (number of linearly independent columns).
There's a close relationship between SVD and the **eigenvalue/eigenvector decomposition**:
- U is the set of eigenvectors of $AA^T$
- V is the set of eigenvectors of $A^TA$
- The  elements of Σ are (in non-increasing order) the square roots of the eigenvalues of $AA^T$ (or $A^TA$)
We now consider the submatrix obtained with the first $k<r$ columns of V and we obtain the following new k-dimensional features:
![[Single_value_decomposition.png]]We can use these new datasets in two ways:
- Use $A_k$ as input for a clustering algorithm
- Decide the number of clusters k and extract the first k columns of the matrix U. 