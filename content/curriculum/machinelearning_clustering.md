+++
title = "Clustering"

# date = {{ .Date }}
lastmod = 2019-05-07

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.curriculum]
  name = "Clustering"
  parent = "Machine learning"
  weight = 1

+++

## Groups of data: clusters
Suppose we are dealing with the data set as shown in Fig. 1, where we have taken several measurements of different types of fruits. For several pieces of fruit we have measured the size of the fruit and the roughness of the fruit. From the figure we can see that in this case we are dealing with 3 specific types of fruit: grapes, watermelons and kiwis. It is clear that each type of fruit can be characterized by a certain size and roughness and clear distinctions between the fruits can be noted. From the visualization the data could be divided in 3 different groups or **clusters**. Clusters can be defined as groups of data sharing similar (unknown) features. In this example the similar feature is the type of fruit.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/clusters_fruit_annotated.svg"
      alt="A data set containing measurements of the size and roughness of 3 types of fruit: grapes, watermelons and kiwis."
    />
    <figcaption class="numbered">
      A data set containing measurements of the size and roughness of 3 types of fruit: grapes, watermelons and kiwis.
    </figcaption>
  </figure>
</div>

## Supervised learning
Suppose that we would now measure the characteristics of an _unknown_ fruit and we were asked to characterize the unknown fruit as either a grape, a watermelon or a kiwi. This type of task is an example of a **classification task**, where the goal is to predict a hidden feature (the type of fruit) from observed features (size and roughness) after having observed several examples. Classification is a type of **supervised learning**, because the prediction is based on a set of data in which the currently hidden feature was known.

## Unsupervised learning
**Unsupervised learning** is the opposite of supervised learning in the sense that there is no _known_ feature to predict. The goal of unsupervised learning is to detect hidden structures in data in order to gain understanding from the data. **Clustering** is a field of unsupervised learning, which involves the discovery of hidden groups or *clusters* in a set of data.

When returning to the previous example with the different types of fruit, lets now suppose that we have access to a similar set of data, but now the features characterizing the clusters are unknown. Fig. 2 shows a data set which consists of multiple entries, each with two observed features. From the figure it is clearly visible that there is some _hidden structure_ present in the data. This _could_ (does not have to be!) provide us with information of a hidden or **latent** feature, which affects the observed features.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/clusters_general.svg"
      alt="A data set containing measurements of two features."
    />
    <figcaption class="numbered">
      A data set containing measurements of two features.
    </figcaption>
  </figure>
</div>

The goal of clustering is to discover hidden groups in the data. Two common algorithms used are the K-means algorithm and the expected maximization algorithm. The most important difference between the algorithms is the way in which the algorithms assigns data points to clusters.

Both cases suffer from 2 drawbacks:

1. **The amount of clusters is unknown** - _Before both algorithms can start, they require an user-defined number of clusters. Therefore a critical assumption has to be made in order to be able to detect clusters at all. This number of clusters is not guaranteed to give the best representation of the hidden structure in the data. Algorithms exist to find an optimal number of clusters with respect to some metric, however, these still do not guarantee to provide the correct amount of clusters describing the underlying structure of the data._
2. **Convergence depends on initialization** - _The convergence of the algorithm (i.e. the final assignment of data points to clusters) depends on the initialization of the clusters. In practice usually both algorithms are run several times with different initial conditions, after which the best result, with respect to some metric, is chosen as the optimal solution._



## K-means clustering


## Expected maximization algorithm

$$ \textbf{EM}:\, \theta^{(m+1)} := \underbrace{\arg \max\_\theta}\_\text{M-step}\underbrace{\sum\_{z} \overbrace{p(z|x,\theta^{(m)})}^{q^{(m+1)}(z)}\log p(x,z|\theta)}\_\text{E-step}$$
