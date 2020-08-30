+++
title = "Maximum Likelihood Estimator"

# date = {{ .Date }}
lastmod = 2020-06-08

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "2.2 Maximum Likelihood Estimator"
weight = 220


+++

## Introduction

The maximum likelihood estimation (MLE) is a popular approach to estimation problems. Many of its properties are appreciated once the other estimation methods are investigated. However, the MLE is a natural extension of the concept of <i>likelihood</i>, which has to be understood well to derive the <a href="../estimation_CRLB">Cramer-Rao lower bound (CRLB) in the follow-up module</a>. Thus, we first introduce the likelihood and then show how the MLE is obtained.

<div class="video-container">
<iframe width="100%"; height="100%"; rc="https://www.youtube.com/embed/y4v4Y9uvK7c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

This module establishes a new paradigm over the least squares estimation (LSE): We are now taking into account the noise and its effect on the data. In the LSE we were aware of the stochastic nature of the data, in MLE we analyze this stochastic nature and include it in our estimation. This is the paradigm for all estimators except the LSE.

## Formal Description of the Maximum Likelihood Estimator

Even before investigating the fundamental concepts underlying the maximum likelihood estimator (MLE), we can write the formal description of the MLE and discover how the estimator is used. The starting point is the understanding that our data is stochastic, and its behavior can be modeled by a probability density function (PDF) such as $p(x[n];\theta)$. This representation describes a PDF for the random variable $x[n]$, which is also a function of the controlling parameter $\theta$ that is deterministic but unknown.

After collecting the data points $\mathbf{x}=[x[1] x[2] ... x[N]]$, we can view the PDF under a new light: We can search for the value of $\theta$ that maximizes the probability of acquiring the data points $\mathbf{x}$ at hand. This gives the formal description of the MLE:
\begin{equation}
\hat\theta=\underset{\theta}{arg \max}p(\mathbf{x};\theta)
\end{equation}

There is one link to identify before putting the MLE to use: How is the PDF for the data $x[n]$ or the data set $\mathbf{x}$ obtained? For this, the data model we adopt throughout this course is utilized. The data is modeled as the sum of a deterministic signal and the noise:
\begin{equation}
x[n]= s[n;\theta] + \omega[n].
\end{equation}

The PDF for the data $\mathbf{x}$ as a function of $\theta$ is obtained by
\begin{equation}
p(x[n];\theta)=p_{\omega}(x[n]-s[n;\theta]),
\end{equation}
where $p_\omega(X)$ is the PDF for the noise $\omega[n]$. Thus, the PDF of the noise is used to model the stochastic behavior of the data.

At this point, it is possible to start working on examples. A pencast describing the MLE for additive white Gaussian noise is available. 

<div class="video-container">
<iframe width="100%"; height="100%"; rc="https://www.youtube.com/embed/WQRoIfvZ5MA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

However, the MLE is in general not available as a closed form equation that accepts the data $\mathbf{x}$ and gives a solution $\hat\theta$. Numerical solution methods are explained in a separate module for both MLE and least squares estimation.

The remainder of this module explains fundamental concepts from which the MLE is derived. These concepts are also essential for understanding the Cramer-Rao lower bound and the binary hypothesis testing that is covered in the third part of the course.

## The Likelihood Function

The likelihood function concept is based on the data model we adopt throughout this course, which assumes the data is the sum of a deterministic signal and the noise. In this setting, we shall consider the probability of acquiring the data points at hand. The observations are modeled as random variables that depend on the parameters to be estimated and the noise:
\begin{equation}
p(x[n];\theta)=p_{\omega}(x[n]-s[n;\theta])
\end{equation}

The term $p_\omega(x[n]-s[n;\theta])$ corresponds to the probability density function (PDF) of the noise term $\omega[n]$. This equation tells us that the difference between the data $x[n]$ and the signal model $s[n;\theta]$ is a stochastic process with the same PDF as the noise. It is obvious that the difference $x[n]-s[n;\theta]$ depends on the parameter $\theta$, which also means the PDF $p(x[n];\theta)$ depends on $\theta$.

This dependence is established by the **likelihood function**, which is still the same function as the PFD $p(x[n];\theta)$ with one significant distinction: The likelihood function is a function of $\theta$. For a set of data points $\mathbf{x}=[x[1] x[2] ... x[N]]$, the value of the likelihood function $p(x[n];\theta)$ can be calculated.

### The Log-Likelihood Function

Rather than the likelihood function itself, the **log-likelihood function** is considered in most applications, which is simply the natural logarithm of the likelihood function. A reason for preferring the log-likelihood is the multiplicative nature of the probability. Consider the PDF for the set of data points $\mathbf{x}$:
\begin{equation}
p(\mathbf{x};\theta)=\prod_{n=1}^N p(x[n];\theta).
\end{equation}
The multiplication is simplified to an addition when the natural logarithm of the likelihood function is considered:
\begin{equation}
\ln p(\mathbf{x};\theta)=\sum_{n=1}^N \ln p(x[n];\theta).
\end{equation}

A PDF has to be strictly non-negative, which allows using the natural logarithm of the PDF. The logarithm function is monotonically increasing, which means for real numbers $0\leq A < B$, $\ln A < \ln B$. This means that the MLE formulation is valid also for the log-likelihood function.

In many references the likelihood function is written as $\mathcal{L}(\theta;\mathbf{X})$ and the log-likelihood function is written as $\mathcal{l}(\theta;\mathbf{x})=\ln \mathcal{L}(\theta;\mathbf{x})$.

## The Maximum Likelihood Estimator for AWGN

The maximum likelihood estimator is in general not in closed form, which means in most cases the MLE is not an equation that takes in the data and gives out the estimation. Numerical solution methods are an important part of the MLE. However, for the linear signal models with AWGN with known noise variance $\sigma^2$, the MLE yields a closed form solution. In this section we derive the MLE for AWGN, and obtain the closed form solution for the linear data.

### MLE for the Normal Distribution

The first step of deriving the maximum likelihood estimator is deriving the log-likelihood function. The reason for adopting the log-likelihood function instead of the likelihood function will become clear during this derivation. <a href="../estimation_maximumlikelihood/#the-likelihood-function">The likelihood function</a> is obtained from the PDF of the noise term. For the AWGN the noise samples are independent and have the normal distribution $\omega[n]\sim\mathcal{N}(0,\sigma)$. Accordingly, the PDF for the noise samples is
\begin{equation}
p(\omega[n])=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(\omega[n])^2}{2\sigma^2}}.
\end{equation}
If we have an accurate model $s[n;\theta]$ with the correct parameter $\theta$, the difference between the data $x[n]$ and the signal model $s[n;\theta]$ is equal to noise; $\omega[n]=x[n]-s[n\theta]$. Based on this relation, we obtain the likelihood function for a sample of data:
\begin{equation}
p(x[n];\theta)=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x[n]-s[n\theta])^2}{2\sigma^2}}.
\end{equation}
The likelihood function for the single sample is an exponential function, and we can obviously benefit from adopting the logarithm of this exponential function. But we also may want to combine multiple samples of the data in our estimator. The reason for using multiple data samples for estimation will become clear when we investigate <a href="../estimation_crlb">the bias, variance and Cramer-Rao lower bound</a> of estimators.

When the data samples $x[n]$ are independent identically distributed, the PDF of a set of data samples is obtained by multiplying the PDF of individual samples:
\begin{equation}
\mathcal{L}(\mathbf{x};\theta)=p(\mathbf{x};\theta)=\prod_{n=1}^Np(x[n];\theta)=\frac{1}{(2\pi\sigma^2)^{N/2}}\prod_{n=1}^Ne^{-\frac{(x[n]-s[n\theta])^2}{2\sigma^2}}.
\end{equation}
The log-likelihood function is obtained by taking the logarithm of the likelihood function:
\begin{equation}
\mathcal{l}(\mathbf{x};\theta)=\sum_{n=1}^N\ln p(x[n];\theta)=N\times\ln\frac{1}{\sqrt{2\pi\sigma^2}}-\sum_{n=1}^N\frac{(x[n]-s[n;\theta])^2}{2\sigma^2}.
\end{equation}
The MLE is found by taking the derivative of the log-likelihood function with respect to the parameter $\theta$ and setting it equal to zero. The value of $\theta=\hat\theta$ that sets the derivative of the log-likelihood function to zero is the MLE:
\begin{equation}
\frac{\partial\mathcal{L}(\mathbf{x};\theta)}{\partial\theta}\Bigg|_\hat\theta=\frac{1}{\sigma^2}\sum_{n=1}^N\frac{\partial s[n;\theta]}{\partial\theta}(x[n]-s[n;\theta])\Bigg|_\hat\theta=0.
\end{equation}

### MLE for a Vector Parameter

The derivation of MLE for normal distribution assumes a scalar parameter $\theta$. In this section we generalize the MLE to a vector parameter $\Theta=[\theta_1~ \theta_2~ ...~ \theta_K]^T$, which is a column vector. In other words, the signal model is controlled by $K$ parameters, which are treated as a parameter vector. Without making any assumptions over the form of the signal model $\mathbf{s}[\Theta]$, the PDF for the data is actually the same as that for the scalar parameter. However, the derivative with respect to the parameter vector $\Theta$ yields $K$ different equations that have to be solved together to find the MLE.

If the data is generated by a linear model such that $\mathbf{x}=\mathbf{H}\Theta+\mathbf{w}$, we can capitalize on the matrix algebraic methods to find the MLE. In this setting, the matrix $\mathbf{H}$ is called **the observation matrix**. The log-likelihood function is written as a vector multiplication according to
\begin{equation}
\sum_{n=1}^N\frac{(x[n]-s[n;\theta])^2}{2\sigma^2}=\frac{1}{2\sigma^2}[\mathbf{x}-\mathbf{s}(\Theta)]^T[\mathbf{x}-\mathbf{s}(\Theta)].
\end{equation}
The log-likelihood function is minimized by minimizing this vector multiplication, which is achieved by setting the derivative with respect to the parameter vector $\Theta$ to zero. The derivative in matrix algebra yields
\begin{equation}
\frac{\partial\mathcal{L}(\mathbf{x};\Theta)}{\partial\Theta}=-2\mathbf{H}^T\mathbf{x}+2\mathbf{H}^T\mathbf{H}\Theta=0,
\end{equation}
which yields the MLE for $\Theta$ as
\begin{equation}
\hat\Theta=(\mathbf{H}^T\mathbf{H})^{-1}\mathbf{H}^T\mathbf{x}.
\end{equation}
This result is significant, because <b>the MLE estimator for linear data model with AWGN and noise variance $\sigma^2$ turns out to be identical to the least squares (LS) estimator</b>. The missing piece in the LSE is the ability to assess the performance of the estimator. For MLE, we have not yet seen the analysis of the estimation performance. However, we now have the paradigm necessary to make the analysis, which is the stochastic nature of the data $\mathbf{x}$ arising from the noise and its connection to the stochastic nature of our estimate $\hat\theta$. 

## Conclusion

The MLE is a very useful estimation method that capitalizes on the **likelihood** concept. This module focuses on the likelihood and log-likelihood functions and demonstrates how the MLE is obtained once the likelihood function is available. The properties of MLE will be appreciated fully once we cover the module on <a href="../estimation_CRLB">Cramer-Rao lower bound (CRLB)</a>, which introduces the tools to assess the performance of estimators and determines their theoretical performance bounds based on the likelihood concept.
