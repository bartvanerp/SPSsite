+++
title = "Bias, Variance, Cramer-Rao Lower Bound"

# date = {{ .Date }}
lastmod = 2020-06-08

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "Bias, Variance, Cramer-Rao Lower Bound"
weight = 30
parent = "Estimation"

+++
## Introduction

Many different estimators can be formulated to estimate the controlling parameters $\theta$ of a signal model. In fact, many different signal models can be hypothesized as the source of the data, just as the noise can have different distributions. The question naturally arises: How can we know if an estimator is the best one possible? How accurately can we estimate the controlling parameters of a signal model? How can we even compare the performances of two estimators? In this module, we are going to devise the performance measures for estimators and come up with a performance bound that marks the best performance for a broad class of estimators.

---
<b>Example:</b> Consider the problem of estimating the voltage level $\theta$ from the data
\begin{equation}
x[n]=\theta+\omega[n].
\end{equation}
If we acquire N data points, we can come up with an estimator by following the intuition that the value we are looking for should be the average of the data samples:
\begin{equation}
\hat\theta=\frac{1}{N}\sum_{n=1}^{N}x[n].
\end{equation}
Consider another estimator:
\begin{equation}
\hat\theta=\frac{1}{N-1}\sum_{n=1}^{N}x[n].
\end{equation}
Which estimator is more accurate? Can we find a third estimator that is better than these two?

---

## Estimation Error
In the module on least squares, the goal was to fit a signal model to the collected data by minimizing the squared error between the data and the model output. If the same experiment is repeated, another data set is obtained. The data is modeled as
\begin{equation}
x[n]=s[n,\theta]+\omega[n],
\end{equation}
where the function $\omega[n]$ returns noise samples that are independent random variables with a probability distribution. Whenever the experiment is repeated to collect $N$ such samples of $x[n]$, the noise contribution to the data is different. The consequence of this difference is reflected in the variation of the estimate $\hat\theta$ from one experiment to the other. In fact, the estimate $\hat\theta$ is itself a random variable, even though the underlying parameter $\theta$ is deterministic (but unknown).

We consider the variation of the estimates for $\theta$ by stating that the squared estimation error is $(\hat\theta-\theta)^2$. The squared error is considered, because the deviation of $\hat\theta$ from $\theta$ is important rather than the sign of the deviation. To account for the randomness of the error the **mean squared error** is considered:
\begin{equation}
mse=E[(\hat\theta=\theta)^2].
\end{equation}

Obviously, we cannot calculate the error term, because the parameter $\theta$ is unknown. We can still look for ways to minimize the mean squared error term by solving the first derivative with respect to $\hat\theta$:
\begin{equation}
\frac{\partial}{\partial\hat\theta}E[(\hat\theta-\theta)^2]=\frac{\partial}{\partial\hat\theta}E[\hat\theta^2-2\theta\hat\theta+\theta^2].
\end{equation}
The problem with the expression above is the presence of the term that contains both $\theta$ and $\hat\theta$. After taking the derivative with respect to $\hat\theta$, the parameter $\theta$ still appears in the equation. However, it is possible to find a solution and minimize the mean squared error for a particular class of estimators.

## Minimum Variance Unbiased Estimator

To reveal the class of estimators that allow minimizing the mean squared error, we decompose the error term:
\begin{equation}
mse=E[\hat\theta^2-2\theta\hat\theta+\theta^2]=E[\hat\theta^2]-(E[\hat\theta])^2+(E[\hat\theta])^2-2\theta E[\hat\theta]+\theta^2,
\end{equation}
where we added and subtracted the term $(E[\hat\theta])^2$. This trick allows us to group the mse into two terms:
\begin{equation}
mse=\sigma^2_{\hat\theta}+(E[\hat\theta]-\theta)^2
\end{equation}
where $\sigma^2_{\hat\theta}=E[\hat\theta^2]-(E[\hat\theta])^2$ is the variance of the estimator and $E[\hat\theta]-\theta$ is the bias of the estimator. 

The class of estimators for which the mean squared error can be minimized is called **minimum variance unbiased estimators (MVUE)**. The mean error term contains the square of the bias, thus, to minimize the mse we need to have an **unbiased** estimator. The mse for an unbiased estimator is minimized if the variance term $\sigma^2_{\hat\theta}$ is minimized. Ideally, we would like to have a <b>consistent estimator</b>, which means the error term approaches to zero as the number of data points increases:
\begin{equation}
\underset{N\to\infty}{\lim}E[(\hat\theta-\theta)^2]=0.
\end{equation}

**refer to live scripts to explore further** 

## The Cramer-Rao Lower Bound and the MVUE

The derivation of the MVUE in the previous section does not provide a procedure to find a MVUE. However, under the assumption of zero bias, we can still calculate the minimum variance that can be attained by an estimator. The lower bound for the variance of an estimator is called **the Cramer Rao Lower Bound (CRLB)**. The CRLB connects the variability of the data $x$ with the variability of the estimate $\hat\theta$. This connection is established by the concepts of <a href="../estimation_maximumlikelihood/#the-likelihood-function">**likelihood**</a>, **score** and **Fisher information**.

Before exploring the concepts at the foundation of the CRLB, we will see the formal definition. To be able to derive the CRLB, for a scalar parameter $\theta$, the PDF of the data has to satisfy the regularity condition
\begin{equation}
E_x\Bigg(\frac{\partial\ln p(\mathbf{x};\theta)}{\partial\theta}\Bigg)=0 \quad for~ all~ \theta,
\end{equation}
where the expected value is taken with respect to $x$. When the regularity condition is satisfied, the variance of any unbiased estimator $\hat\theta$ is bounded by the Cramer-Rao lower bound
\begin{equation}
var(\hat\theta) > \frac{1}{\mathcal{I}(\theta)},
\end{equation}
where $\mathcal{I}(\theta)$ is the **Fisher information**:
\begin{equation}
\mathcal{I}(\theta)=-E_x\Bigg(\frac{\partial^2\ln p(\theta;\mathbf{x})}{\partial\theta^2}\Bigg).
\end{equation}

Only the MVUE achieves this bound, and an estimator $\hat\theta=f(\mathbf{x})$ is MVUE if and only if
\begin{equation}
\frac{\partial\ln p(\mathbf{x};\theta)}{\partial\theta}=\mathcal{I}(\theta)(f(\mathbf{x})-\theta).
\end{equation}

The result on the existence of MVUE will be used in the module on <a href="../estimation_mvue_linear">MVUE for Linear Models</a>.

The Cramer-Rao lower bound can be found for an estimator provided that the distribution for the data is available. This distribution, in turn, is based on the noise distribution and the signal model. Hence, to be able to come up with a measure of accuracy for our estimation, we need to know about the noise in the process. A Matlab live script that features the Cramer-Rao lower bound for the sinusoidal frequency estimation problem can be found in **INSERT LINK HERE**.

The rest of this section covers the fundamental concepts that give rise to the CRLB. The extension of the CRLB to vector parameter $\Theta$ is given at the end of this section.

### The Score

The score is found on the concept of the log-likelihood function. The likelihood function is essentially the probability density function (PDF) of the data, which is parametrized by the variable $\theta$ that controls the signal model $s[n;\theta]$. The log-likelihood function is simply the logarithm of the likelihood function. 


<b>Example:</b>

---

For additive white Gaussian noise (AWGN) with zero mean and $\sigma^2$ variance, the data is modeled as
\begin{equation}
\mathbf{x}=\mathbf{s}(\theta)+\mathbf{w},
\end{equation}
where $\mathbf{x}$ is the data vector, $\mathbf{w}$ is the noise vector, $\mathbf{s}(\theta)$ is the signal model and $\theta$ is the parameter that controls the signal model. The log-likelihood function for the data $\mathbf{x}$ is
\begin{equation}
\mathcal{l}(\mathbf{x};\theta)=\sum_{n=1}^N\ln p(x[n];\theta)=N\times\ln\frac{1}{\sqrt{2\pi\sigma^2}}-\sum_{n=1}^N\frac{(x[n]-s[n;\theta])^2}{2\sigma^2}.
\end{equation}
In terms of vectors, the log-likelihood function for the data with AWGN is
\begin{equation}
\mathcal{l}(\mathbf{x};\theta)=N\times\ln\frac{1}{\sqrt{2\pi\sigma^2}}-\frac{1}{2\sigma^2}(\mathbf{x}-\mathbf{s}(\theta))^T(\mathbf{x}-\mathbf{s}(\theta)).
\end{equation}

---

<a href="../estimation_maximumlikelihood">The maximum likelihood estimator (MLE)</a> is found by setting the first derivative of the likelihood or log-likelihood function to zero and solving for the parameter $\theta$. The first derivative of the log-likelihood function is called **the score**, so actually the MLE is found by setting the score equal to zero. The score attains a special form that is very useful in developing the Cramer-Rao lower bound:
\begin{equation}
g(\theta)=\frac{\partial}{\partial\theta}\ln \mathcal{L}(\theta;\mathbf{x})=\frac{1}{\mathcal{L}(\theta;\mathbf{x})}\frac{\partial}{\partial\theta}\mathcal{L}(\theta;\mathbf{x}),
\end{equation}
which is a direct consequence of the derivative identity regarding the natural logarithm function.

The usefulness of the score is revealed when considering its statistical properties. The expected value of the score is calculated as
\begin{equation}
E_x(g(\theta))=\int p(\mathbf{x};\theta)\frac{\partial}{\partial\theta}\ln \mathcal{L}(\theta;\mathbf{x})d\mathbf{x}
\end{equation}
If we apply the derivative and substitute the PDF in place of the likelihood (because they are actually the same function), we obtain
\begin{equation}
E_x(g(\theta))=\int\frac{\partial p(\mathbf{x};\theta)}{\partial\theta} d\mathbf{x}.
\end{equation}
The derivative with respect to $\theta$ and the integration with respect to $\mathbf{x}$ can switch order to yield
\begin{equation}
E_x(g(\theta))=\frac{\partial}{\partial\theta} \int p(\mathbf{x};\theta) d\mathbf{x},
\end{equation}
where the integral of the PDF over the sample space is equal to 1 and its derivative is equal to zero.  Thus, **the expected value of the score is equal to zero**. We should note that the switching of the order of the integral and the derivative is only possible if the PDF $p(\mathbf{x};\theta)$ satisfies the **regularity condition**:
<ul>
<li>The PDF $p(x;\theta)$ is non-zero for $x_1$ &lt $x$ &lt $x_2$, where $x_1$ and $x_2$ are independent of $\theta$,
<li>OR the PDF $p(x;\theta)$ is non-zero for all $x$, continuously differentiable and it's integral converges for all $\theta$.
 </ul>


<b>Example:</b>

---
For the data model $x[n]=\theta+\omega[n]$, if the noise has uniform distribution, i.e., $\omega[n]\sim U(\omega_1,\omega_2)$, then the data will be such that $\omega_1+\theta < x[n] < \omega_2+\theta$. In this case, the regularity condition is not satisfied. 

---

### The Fisher Information

The variance of the score is also called **the Fisher Information**. Because the expected value of the score is equal to zero, the variance of the score is
\begin{equation}
\mathcal{I}(\theta)=E_x(g^2(\theta))=\int p(\mathbf{x};\theta)\Big(\frac{\partial}{\partial\theta}\ln \mathcal{L}(\theta;\mathbf{x})\Big)^2d\mathbf{x}=E\Bigg(\Big(\frac{\partial}{\partial\theta}\ln \mathcal{L}(\theta;\mathbf{x})\Big)^2\Bigg).
\end{equation}

If the regularity conditions are satisfied and the log-likelihood function is twice differentiable with respect to $\theta$, then the Fisher information can also be written as
\begin{equation}
\mathcal{I}(\theta)=-E\Big(\frac{\partial^2}{\partial\theta^2}\ln \mathcal{L}(\theta;\mathbf{x})\Big).
\end{equation}

The meaning of the Fisher information deserves more contemplation. The role it plays in the CRLB stems from the derivation of the latter, which starts with the idea that an estimator is a function of the data, $\hat\theta=f(\mathbf{x})$, where the estimate is a random variable. The idea is to measure the information in the data we acquired over the parameter to be estimated. If the estimate is sensitive to the data, then slight changes in the data results in significant changes in the estimate. In other words, the log-likelihood function is *sharp*. This sharpness can be assessed through the second derivative of the log-likelihood function. 

Note, however, that the Fisher information is <i>the expected value</i> of the second derivative of the log-likelihood function. So, the intuition about the sharpness of the function gives only part of the picture. The actual relation that describes the information content of the data regarding the parameter to be estimated is the covariance of the estimate with the derivative of the log-likelihood function, which is the score.


### The Fisher Information Matrix

Note that the expression above concerns the scalar parameter $\theta$, which yields a single scalar term for the Fisher information. For the vector case, we have to consider the partial derivative with respect to each entry $\theta_k$ of the parameter vector $\Theta=[\theta_1 ~\theta_2 ~ ... ~ \theta_K]$. **The Fisher information matrix** consists of entries 
\begin{equation}
[\mathcal{I}(\Theta)]_{kl}=-E\Bigg(\frac{\partial^2 \ln\mathcal{L}(\Theta;\mathcal{x})}{\partial \theta_k \partial \theta_l}\Bigg),
\end{equation}
where $k$ is the row index and $l$ is the column index.


### The CRLB for Vector Parameters

The CRLB for scalar parameter $\theta$ is the lower bound for the variance of the estimate $\hat\theta$. For vector parameter $\Theta$, we need to consider the <a href="../mathematicalbackground_probability_vectors/#covariance">**covariance matrix**</a> for the estimate $\hat\Theta$. Consider the structure of the covariance matrix: The diagonal elements are the variances of the corresponding entries of $\hat\Theta$, and the off-diagonal elements show the correlation between the corresponding pairs of random variables. For a set of uncorrelated or independent random variables, the covariance matrix consists of non-zero entries only along its diagonal.

The CRLB for the covariance matrix is not a simple magnitude comparison anymore. The relation between the covariance matrix and the Fisher information matrix is
\begin{equation}
cov(\hat\Theta)-\mathcal(I)^{-1}(\Theta)\geq\mathbf{0}
\end{equation}
which should be understood as the result of the subtraction is a positive semi-definite matrix, i.e., for every non-zero column vector $\mathbf{z}$ of real numbers with the same dimension as $\Theta$,
\begin{equation}
\mathbf{z}^T[cov(\hat\Theta)-\mathcal(I)^{-1}(\Theta)]\mathbf{z}\geq 0.
\end{equation}
For $\Theta$ with independent entries, the relation above boils down to the scalar CRLB for each parameter.

As with the scalar case, only the MVUE achieves this bound, and an estimator $\hat\Theta=f(\mathbf{x})$ is MVUE if and only if
\begin{equation}
\frac{\partial\ln p(\mathbf{x};\Theta)}{\partial\Theta}=\mathcal{I}(\Theta)(f(\mathbf{x})-\Theta).
\end{equation}
While the expression is pretty much the same as in the scalar case, we should remember that the function $f(\mathbf{x})$ has as many dimensions as the size of the parameter vector $\Theta$ and $\mathcal{I}(\Theta)$ is the Fisher information matrix.

## Conclusion

The ability to analyze the bias and variance of an estimator gives us valuable insight on how to gauge the performance of estimators and find ways to improve. There are several properties we seek in an estimator, based on the tools developed in this module:

<ul>

<li><b>Efficient:</b> When an estimator is unbiased and attains the minimum possible variance for an estimator that is the CRLB, that estimator is called efficient.
<li><b>Asymptotically Efficient:</b> When the variance of an estimator decreases as the size of the data increases and reaches the minimum variance (CRLB) for infinitely long data, that estimator is called asymptotically efficient.
<li><b>Optimal:</b> When an estimator is unbiased and efficient, then that estimator is called optimal.
<li><b>Asymptotically Optimal:</b> When the bias of an estimator decreases as the size of the data increases and reaches zero for infinitely long data, that estimator is called asymptotically optimal.

</ul>

For example, the maximum likelihood estimator is asymptotically efficient and asymptotically optimal. Obviously, we cannot have infinitely long data sets. In such cases, the task is to determine the data size which gives acceptable performance, and while the best possible performance is determined through the theory explained in this module, what passes as <i>the acceptable performance</i> depends on the application. As long as new signal processing applications emerge (that is, for the forseeable future), methods to develop, analyze and improve estimators will remain indispensible.