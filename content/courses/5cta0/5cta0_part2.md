+++
title = "Part 2: Estimation theory"

# date = {{ .Date }}
lastmod = 2020-08-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.5cta0]
name = "Part 2: Estimation Theory"
weight = 200

+++



## Introduction


<!-- Estimation theory is ubiquitous in our daily life and plays a fundamental role in many applications. The main objective of estimation theory is to infer the value of a parameter from some observation. Consider the following example. -->

<!-- ---
<b>Example:</b>

A mobile phone connects via a wireless link to a base station. The base station transmits information for a user on a specific carrier frequency.  Both the base station and mobile phone use local oscillators for modulation and demodulation. However, due to imperfection, the local oscillator frequencies do not match exactly. The frequency mismatch, if not compensated, results in an increased error rate. In the worst case, it can even lead to an interrupted connection. Thus, to maintain a good connection to a base station, a mobile phone must compensate for the frequency mismatch. We can model the impact of the frequency mismatch on the data as
$x[n] = c[n]e^{j2\pi \theta n} + w[n]$,
where $x[n]$ is the received complex symbol, $c[n]$ is the transmitted complex symbol, $\theta$ is the frequency mismatch, and $w[n]$ is some complex noise. The effect of the frequency mismatch is shown below.

<figure>
  <img
    src="/../files/7.Images/statistical/estimation/cfo_ex.jpg"
    alt="Received symbols without frequency mismatch (left) and with frequency mismatch (right). The frequency mismatch causes a rotation of the received symbols. If this mismatch is not compensated, it is virtually imposible to decode the symbols correctly."
  />
  <figcaption class="numbered">
      Received symbols without frequency mismatch (left) and with frequency mismatch (right). The frequency mismatch causes a rotation of the received symbols. If this mismatch is not compensated, it is virtually imposible to decode the symbols correctly.
  </figcaption>
</figure>


Typically, the base station sends a fixed and known training sequence of length $N$ at the beginning of a transmission. The task of a frequency offset estimator is now to determine the frequency mismatch based on the first N symbols. Note that noise impairs the signal. The noise itself is a random variable, and thus, each new observation of the training sequence will result in a different estimate.

<<<<<<< HEAD
--- -->

Estimation theory is ubiquitous in our daily life and plays a fundamental role in many applications. The main objective of estimation theory is to infer the value of a parameter $\theta$. from some observations, which are represented by a vector $\mathbf{x}$ . These observations are random variables whose PDF depends on the unknown parameter. Thus, we denote the PDF as $p(\mathbf{x}; \theta)$ to emphasize its dependency on the parameter $\theta$.



<!-- In general, we wish to determine an unknown parameter $\theta$. However, this parameter is not directly observable; instead, some observations are available, represented by a vector $\mathbf{x}$. These observations are random variables whose PDF depends on the unknown parameter. Thus, we denote the PDF as $p(\mathbf{x}; \theta)$ to emphasize its dependency on the parameter $\theta$. -->


---
<b>Example:</b>

Suppose we want to estimate a DC voltage $A$ which is embedded in noise. Our observation can be modeled as
\begin{equation}
x[n] = A + w[n],
\end{equation}
where $A$ is the unknown DC level, and w[n] is independent and identically distributed Gaussian noise with zero mean and known variance $\sigma^2$. The parametrized PDF of our observation is then
\begin{equation}
p(\mathbf{x};A) = \frac{1}{(2\pi\sigma^2)^{\frac{N}{2}}} \exp \\left[-\frac{1}{2\sigma^2}\sum_{0}^{N-1}(x[n]-A)^2\\right].
\end{equation}

---

 An estimator is now a function $g(\mathbf{x})$ that maps from the observations $\mathbf{x}$ to an estimate $\hat\theta$ of the unknown parameter, i.e.,
\begin{equation}
\hat{\theta} = g(\mathbf{x}).
\end{equation}
Note that different estimators can be defined. For the previous example, we can define, for example, the following three estimators:
\begin{align}
	\hat{A} &= \frac{1}{N} \sum_{n=0}^{N-1} x[n], \\\\\\
	\check{A} &= x[0], \\\\\\
	\tilde{A} &= \frac{1}{N-2}\\left( 2x[0]+\sum_{n=1}^{N-2}x[n]+2x[N-1]\\right).
\end{align}
The first estimator is the sample mean of the observation. The second estimator considers only the first observation, and the third estimator puts a higher weight on the first and the last observation. At this point, the question arises as to which of the estimators is the best. Furthermore, is there a better estimator? To answer these questions, we need first to define what we mean by best.

Since the observations $\mathbf{x}$ is a  random vector, the estimate $\hat\theta$ is also a random variable. Thus, we need to evaluate an estimator by its statistic. First of all, it is desirable that an estimator produced the true parameter on average, i.e.,
\begin{equation}
  \mathbb{E}\\left[\hat\theta\\right] = \theta
\end{equation}
for all $\theta$.

An estimator with this property is said to be **unbiased**. Estimators for which the expected value approaches the true value as the sample size increases are called **consistent** estimators. All three presented estimators possess this property. Although unbiasedness is a preferred property, it does not help us answer which presented estimator is better. A more suitable criterion for the performance evaluation of an estimator is the variance of the estimate. The variance of a random variable reflects its variability. Thus, an estimator whose variance is small is desirable.

Returning to the three estimators. The individual variances of the estimates are:
\begin{align}
\mathrm{Var}\\left[\hat{A}\\right] &= \frac{\sigma^2}{N},\\\\\\
\mathrm{Var}\\left[\check{A}\\right] &= \sigma^2,\\\\\\
\mathrm{Var}\\left[\tilde{A}\\right] &= \frac{(N+6)}{(N+2)^2}\sigma^2.
\end{align}

When comparing the different variances, we see that the first estimator has the lowest variance. When compared to the second estimator, we see that the variance is $N$-times smaller due to the noise averaging effect of the estimator. The variance of the last estimator converges to the variance of the first estimator as the sample size increases.

So far, we have seen that we can formulate different estimators, and we can compare their performance by means of their variance. It is logical now to ask if other estimators can have a lower variance or even a variance equal to zero. In this part of the lecture, we will answer this question and show that there exists a lower bound on the variance for unbiased estimators. Moreover, the bound provides an equality constraint which allows us to find an estimator with a variance equivalent to this bound. Such estimators are referred to as **efficient** estimators. In fact, the sample mean $\hat{A}$ in the above example is such an estimator. In general, efficient estimators only exist for special cases. Thus, we are interested in finding an estimator which has the lowest variance of all unbiased estimators. An estimator whose variance is lower then the variance of all other unbiased estimators for all values of $\theta$ is termed **minimum variance unbiased estimator**, or short MVUE. It should be noted that such an estimator must not necessarily exist and if it exits, it is unique.


## Outline
The topics covered in this part are

<ul>
<<<<<<< HEAD
<li><a href="../statisticalsignalprocessing_estimation_crlb/">The Cramer-Rao Lower Bound:</a> Just as the data is stochastic, so are the parameter estimations. When the noise properties are known, the lowest possible variance for the parameter estimations can be calculated for unbiased estimators.
<li><a href="../statisticalsignalprocessing_estimation_maximumlikelihood/">Maximum Likelihood Estimator:</a> The stochastic nature of the data due to the noise is modeled in terms of the probability density function of the noise. The parameter value that maximizes the probability of observing the data at hand is the maximum likelihood estimate.
<li><a href="../statisticalsignalprocessing_estimation_mvue_linear/">Minimum Variance Unbiased Estimator and Best Linear Unbiased Estimator:</a> The minimum variance unbiased estimator can be found for linear problems with Gaussian noise.
=======
<li><a href="../statisticalsignalprocessing_estimation_CRLB">The Cramer-Rao Lower Bound:</a> Just as the data is stochastic, so are the parameter estimations. When the noise properties are known, the lowest possible variance for the parameter estimations can be calculated for unbiased estimators.
<<<<<<< Updated upstream
<li><a href="../statisticalsignalprocessing_estimation_MaximumLikelihood">Maximum Likelihood Estimator:</a> The stochastic nature of the data due to the noise is be modeled in terms of the probability density function of the noise. The parameter value that maximizes the probability of observing the data at hand is the maximum likelihood estimate.
=======
<li><a href="../statisticalsignalprocessing_estimation_MaximumLikelihood">Maximum Likelihood Estimator:</a> The stochastic nature of the data due to the noise is modeled in terms of the probability density function of the noise. The parameter value that maximizes the probability of observing the data at hand is the maximum likelihood estimate.
>>>>>>> Stashed changes
<li><a href="../statisticalsignalprocessing_estimation_MVUE_linear">Minimum Variance Unbiased Estimator and Best Linear Unbiased Estimator:</a> The minimum variance unbiased estimator can be found for linear problems with Gaussian noise.
>>>>>>> Simona_20200519
<li><a href="../statisticalsignalprocessing_estimation_leastsquares">Least Squares Estimator:</a> This method fits the model to data by minimizing the sum of squared difference between the data and the model.
<li><a href="../statisticalsignalprocessing_estimation_bayes">Bayesian Estimators:</a> For all estimation techniques so far, the parameter to be estimated is assumed to be deterministic but unknown. Bayesian estimators consider the parameter also as a random variable and utilize the Bayes' Theorem to estimate it.
<li><a href="../statisticalsignalprocessing_estimation_numerical/">Numerical Solution Methods:</a> Not all estimators have closed forms; numerical methods that iteratively estimate the parameters are indispensable tools for implementing estimators.
