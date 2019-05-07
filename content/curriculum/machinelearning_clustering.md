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

## Unsupervised learning
When dealing with large sets of data manual inspection and characterization is cumbersome. Good understanding of the data can reveal _hidden structures_ within the data, which might allow us to draw conclusions from this data. In the medical field we could for example use these hidden structures to classify a tumor as benign or malignant. Similarly these hidden structures could allow us to classify images of handwritten digits. \
The field of **unsupervised learning** involves the characterization of data when the desired output is unavailable (i.e. the hidden features inside the data are unknown). **Clustering** is a field of unsupervised learning, which involves the discovery of hidden groups or *clusters* in a set of data. When returning to the case of handwritten digits these groups could indicate which digit is written down.

<figure>
<img
    src="/../files/7.Images/clusters.svg"
    alt="A 2-dimensional plot in which 3 hidden clusters can be observed."
/>
<figcaption>
This figures shows a set of 2-dimensional data points, which seem to be separable in 3 distinct clusters.
</figcaption>
</figure>


## K-means clustering


## Expected maximization algorithm

$$ \textbf{EM}:\, \theta^{(m+1)} := \underbrace{\arg \max\_\theta}\_{M-step}\underbrace{\sum\_{z} \overbrace{p(z|x,\theta^{(m)})}^{q^{(m+1)}(z)}\log p(x,z|\theta)}\_{E-step}$$
