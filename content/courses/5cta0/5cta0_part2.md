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

Estimation theory is ubiquitous in our daily life and plays a fundamental role in many applications. The main objective of estimation theory is to infer the value of a parameter from some observation.

---
<b>Example:</b>

Consider, for example, your mobile phone. The mobile phone connects via a wireless link to a base station. The base station transmits information for a user on a specific carrier frequency.  Both the base station and mobile phone use local oscillators for modulation and demodulation. However, due to imperfection, the local oscillator frequencies do not match exactly. The frequency mismatch, if not compensated, results in an increased error rate. In the worst case, it can even lead to an interrupted connection. Thus, to maintain a good connection to a base station, a mobile phone must compensate for the frequency mismatch. We can model the impact of the frequency mismatch on the data as
$x[n] = c[n]e^{j2\pi \theta n} + w[n]$,
where $x[n]$ is the received symbol, $c[n]$ is the transmitted symbol, $\theta$ is the frequency mismatch, and $w[n]$ is some noise. The effect of the frequency mismatch is shown below.

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

---


The above example can be generalized as follows. An estimator is a function that determines a parameter $\theta$ from an N-point dataset $\\{x[0],x[1],...,x[N-1]\\}$, i.e.,
\begin{equation}
\hat{\theta} = g(x[0],x[1],...,x[N-1])
\end{equation}
where $g$ is some function and $\hat{\theta}$ is the estimate. The focus of estimation theory is to find estimators "good" estimators. In this context, good means optimal under certain conditions, which we will address later.

To find estimators, we need to model our observations. In general, the parameters of interest are not observed directly. Instead, the observations are related to these parameters through a known function. For instance, measuring non-electrical quantities is typically carried out by converting them to electrical quantities like voltage or current using physical relations between these quantities. The voltage or the current can then be determined by using volt- or amperemeters. In most cases, noise or model inaccuracies impair our observations. Thus, each experiment will result in different observations. Hence, we need to describe our observations by a probability density function.  The unknown parameters parametrize the probability density function (pdf), and thus, we denote the pdf as
\begin{equation}
p(\mathbf{x}; \boldsymbol\theta),
\end{equation}
where $\mathbf{x}$ is the vector of observation and $\boldsymbol\theta$ is the vector of parameters that we wish to determine.

---
<b>Example:</b>

Suppose we want to estimate the DC voltage embedded in noise. Our observation can be modeled as
\begin{equation}
x[n] = A + w[n]
\end{equation}
where $A$ is the unknown DC level, and w[n] is i.i.d. Gaussian noise with zero mean and known variance $\sigma^2$. The parametrized pdf of our observation is then
\begin{equation}
p(\mathbf{x},\theta) = \frac{1}{(2\pi\sigma^2)^{\frac{N}{2}}} \exp \\left[-\frac{1}{2\sigma^2}\sum_{0}^{N-1}(x[n]-A)^2\\right].
\end{equation}

---

For the previous example, we can define different estimators. Consider the following three estimators:
\begin{align}
	\hat{A} &= \frac{1}{N} \sum_{n=0}^{N-1} x[n], \\\\\\
	\check{A} &= x[0], \\\\\\
	\tilde{A} &= \frac{1}{N-2}\\left( 2x[0]+\sum_{n=1}^{N-2}x[n]+2x[N-1]\\right).
\end{align}
The first estimator is the arithmetic mean of the observation, while the second estimator considers only the first observation. The third puts a different weight on the first and the last observation. At this point, the question arises as to which of the estimators is the best. Furthermore, is there a better estimator? To answer these questions, we need first to define what we mean by best.

The estimator is a function with random variables as an input. Thus, also the estimate is a random variable. We, therefore, describe the estimator by its statistic. First of all, it is desirable that an estimator produced the true parameter on average, i.e.,
\begin{equation}
  \mathbb{E}[\hat\theta] = \theta
\end{equation}
for all $\theta$.

An estimator with this property is said to be unbiased. All three presented estimators possess this property. Even unbiasedness is a preferred property; it does not help us answer which presented estimator is better. A more suitable criterion for the performance evaluation of an estimator is the variance of the estimate. The variance of a random variable reflects its variability. Therefore, an estimator whose estimate is small is desirable.
Moreover, as we will show, the variance is lower bounded. Thus, we can not only compare different estimators with each other but also with this lower bound. Under certain conditions, this lower bound even allows us to find estimators which achieve this bound.

Returning to the three estimators. It can be shown that the indivdual variances of the estimates are:
\begin{align}
\mathrm{Var}[\hat{A}] &= \frac{\sigma^2}{N},\\\\\\
\mathrm{Var}[\check{A}] &= \sigma^2,\\\\\\
\mathrm{Var}[\tilde{A}] &= \frac{(N+6)}{(N+2)^2}\sigma^2.
\end{align}

When comparing the different variances, we see that the first estimator has the lowest variance. When compared to the second estimator, we see that the variance is N-times smaller due to the noise averaging effect of the estimator. In fact, the variance of the first estimator is the lowest possible variance attainable for this specific estimation problem.

## Outline
The topics covered in this part are

<ul>
<li><a href="../statisticalsignalprocessing_estimation_leastsquares">Least Squares Estimator:</a> This method fits the model to data by minimizing the sum of squared difference between the data and the model.
<li><a href="../statisticalsignalprocessing_estimation_MaximumLikelihood">Maximum Likelihood Estimator:</a> The stochastic nature of the data due to the noise is be modeled in terms of the probability density function of the noise. The parameter value that maximizes the probability of observing the data at hand is the maximum likelihood estimate.
<li><a href="../statisticalsignalprocessing_estimation_CRLB">The Cramer-Rao Lower Bound:</a> Just as the data is stochastic, so are the parameter estimations. When the noise properties are known, the lowest possible variance for the parameter estimations can be calculated for unbiased estimators.
<li><a href="../statisticalsignalprocessing_estimation_MVUE_linear">Minimum Variance Unbiased Estimator and Best Linear Unbiased Estimator:</a> The minimum variance unbiased estimator can be found for linear problems with Gaussian noise.
<li><a href="../statisticalsignalprocessing_estimation_Bayes">Bayesian Estimators:</a> For all estimation techniques so far, the parameter to be estimated is assumed to be deterministic but unknown. Bayesian estimators consider the parameter also as a random variable and utilize the Bayes' Theorem to estimate it.
<li><a href="../statisticalsignalprocessing_estimation_numerical_methods">Numerical Solution Methods:</a> Not all estimators have closed forms; numerical methods that iteratively estimate the parameters are indispensible tools for implementing estimators.
<li><a href="../statisticalsignalprocessing_spectrum_main">Spectral Estimation:</a>
The power spectrum provides important information on the stochastic process generating the data; in this module we discuss methods to estimate the power spectrum when only a short segment of a random signal is available.</ul>
