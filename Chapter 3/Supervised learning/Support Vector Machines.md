We have 2 types of SVM:
- **Linear SVM**: it works for linearly separable samples, receive as input the original feature vectors and it finds the optimal hyperplane that separates the samples of the two classes
- **Non-linear SVM**: a non linear mapping, called a kernel function, is applied from the original feature space (called attribute space) to a higher dimensional target feature space (that can separate the data better in a linear way).

Lets see each one in more detail.
## Linear SVMs
the linear SVM finds the hyper-plane that maximize the margin (i.e. the distance of the decision boundaries (hyper-plane) from each sample).![[Linear_SVM.png]]
## Non linear SVMs
Here a loss factor is added to the cost function to account for misclassified samples. The need is due to the fact that data might not be linearly separable originally:![[Non-linear_SVM_1.png]]But when we go to a higher dimension we can maybe obtain a linearly separable result:![[Non-linear_SVM_2.png]]The function that elevate the dimensions of the data is called the **Kernel-function** and obviously there are various versions that focuses on different kind of dispersions.

