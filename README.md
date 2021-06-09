# Deep Clustering for Unsupervised Learning of Visual Features


## Project Objective
* To implement an end-to-end training of visual features on large scale dataset which requires little domain knowledge and no specific signal from the inputs.
* Deep Clustering is a clustering method that jointly learns the parameters of a neural network and the cluster assignments of the resulting features.

## Overview
* fθ the convnet mapping, where θ is the set of corresponding parameters.
* Given a training set X = {x1, x2, . . . , xN } of N images, we want to find a parameter θ∗ such that the mapping fθ∗ produces good general-purpose features.
* Traditionally,  each image xn is associated with a label yn in {0, 1}k 
* A parametrized classifier gW predicts the correct labels on top of the features fθ(xn). The parameters W of the classifier and the parameter θ of the mapping are then jointly learned by optimizing the following problem:

![Eqn 1](/images/eqn1.PNG)
where l is the multinomial logistic loss, also known as the negative log-softmax function. This cost function is minimized using mini-batch stochastic gradient descent and backpropagation to compute the gradient 

* A multilayer perceptron classifier on top of the last convolutional layer of a random AlexNet achieves 12% in accuracy on ImageNet while the chance is at 0.1%(convolutional structure gives a strong prior on the input signal)
* Will exploit this weak signal to bootstrap the discriminative power of a convnet.
Cluster the output of the convnet and use the subsequent cluster assignments as “pseudo-labels” to optimize the previous equation (iteratively learns the features and groups them).
* For clustering algorithm will use K-Means.
* K-Means jointly learns a d × k centroid matrix C and the cluster assignments yn of each image n by solving the following problem:

![Eqn 2](/images/eqn2.PNG)
Solving this problem provides a set of optimal assignments (yn*)n≤N and a centroid matrix C∗ . These assignments are then used as pseudo-labels; we make no use of the centroid matrix.

* In summary we alternates between clustering the features to produce pseudo-labels using Eq. (2) and updating the parameters of the convnet by predicting these pseudo-labels using Eq. (1).

![Model](/images/model.PNG)
