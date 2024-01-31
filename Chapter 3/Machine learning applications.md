Lets see the basics of ML for biomedical applications.
First of all, in the case of microarray analysis the input will be a small set of microarray experiments which in turn will have many samples (genes).
A **feature vector** is formed by combining normalized expression values in the available samples. 
![[feature_vectors_example.png]]We can now apply different types of ML:
- **Unsupervised learning**: Such as clustering and class discovery, here the feature vectors are unlabeled and the (usual) goal is to attack to each gene a cluster label by grouping together genes with a similar expression behavior.
- **Supervised learning**: Such as classification or class prediction, feature vectors are labeled and the goal is to predict the label of a new unlabeled sample. If the class variable has continuous values (instead of discrete) we use regression analysis instead of classification.

## Definitions
- [[Features]]
- [[Distance]]
- [[Model]]

## Unsupervised learning
Known as clustering or class discovery, the idea is to determine how many groups are in the data and which variables seem to define the groupings. Basically clustering algorithms are methods to divide a set of n observations into g groups so that for each group the similarities of its elements are larger than the similarities with the other groups. The number of groups *g* is usually unknown and must be selected in some way, while implicitly both features and distance must have been already selected (due to the choice of clustering method).
There is no training sample and unlike classification there is no easy way to use cross validation.
## Hierarchical clustering
There are 2 types of hierarchical clustering:
- **[[Agglomerative hierarchical clustering]]**
- **Divisive**: the data is divided into g groups using some (re)allocation algorithm (this will not be covered)
both types must have defined the [[Distance]] between feature vectors and the [[distance]] between groups of feature vectors.
We will cover also [[K-means clustering]] and a method to reduce the input dimension ([[Single value decomposition]]).
## Supervised learning
Also known as **classification** or **Class Prediction**. The idea is to predict the class label of an input sample (called **Test sample**) given prior knowledge given by a set of labeled samples (called **Training samples**).
There are several techniques used in supervised learning:
- Linear classifiers
- [[K-Nearest Neighbors]]
- [[Support Vector Machines]]
- Artificial Neural Networks
Here the input feature vectors are usually the columns of the gene experiment matrix. The dimensionality is often huge since it depends on the number of genes of a single microarray and the **Sample size** is typically small since it depends on the number of experiments (microarrays). Many of these algorithms benefit of a pre-processing process to reduce dimensionality.

There are some key aspects to consider while working on supervised learning:
- **Overfitting vs Generalization**: We want our model to be able to generalize, but we can't always perform generalization well, so we call overfitting the cases where there is no generalization even though the performance on the training set is high.
- **Cross validation**: Is a "limiter" of overfitting, basically we divide the training samples into k groups called **folds** and we  iteratively consider k-1 folds for training and 1 for evaluation of the results (as validation set). Then we combine the k evaluations to define the parameter values that provide better performance overall. 
- **Testing data**: Proper evaluation of the learning algorithm **must** be performed on samples that have not been seen by the algorithm. 
