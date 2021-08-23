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

The maximum likelihood estimator (MLE) is a popular approach to estimation problems. Firstly, if an efficient unbiased estimator exists, it is the MLE.  Secondly, even if no efficient estimator exists, the mean and the variance converges asymptotically to the real parameter and CRLB as the number of observation increases. Thus, the MLE is asymptotically unbiased and asymptotically efficient. The principle of the MLE is to maximize the so-called likelihood function, which is a known function. Another important function, in the context of the MLE, is the log-likelihood function. It reveals the fundamental connection of the MLE to the CRLB.
Finding the maximum can be achieved for simple problems analytically. However, for more complex estimation problems, we rely on numerical methods addressed in the module on numerical methods.


<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/FsIlTgFnK7w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Maximum Likelihood Estimation

Before defining the MLE, we define the likelihood function. The likelihood function is the PDF $p(\mathbf{x},\theta)$ for a given observation $\mathbf{x}$. Since we fix the observation $\mathbf{x}$, the PDF $p(\mathbf{x},\theta)$ depends only on the unknown parameter. The value of \theta that maximizes the likelihood function is the maximum likelihood estimate $\hat{\theta}\_{\text{ML}}$, i.e., \begin{equation}
	\hat\theta_{\text{ML}} = \underset{\theta}{\operatorname{argmax}} p(\mathbf{x};\theta).
\end{equation}
In other words, the maximum likelihood estimate is the value of theta that most likely caused the observation $\mathbf{x}$. Note that depending on the estimation problem, no maximum or multiple maxima exist.


---
<b>Example: </b>

Let $x[0],x[1],\dots,x[N-1]$ be iid and uniformly distributed random variables with PDF
\begin{equation}
  p(x[i];\theta)  = \begin{cases}
        \theta^{-1}, & 0 \leq x[i] \leq \theta,\\\\\\
        0 & \text{else}.
  \end{cases}
\end{equation}
The unknown parameter $\theta>0$ determines the length of the interval. Due to the iid assumption, we further have that
\begin{equation}
  p(\mathbf{x};\theta)  = \begin{cases}
        \theta^{-N}, & \text{if } 0 < x[i] < \theta \text{ for } 0\leq i \leq N-1 \\\\\\
        0, & \text{else}.
  \end{cases}
\end{equation}

The value of $\theta$ must be larger than or equal to the largest value in our observed data. Otherwise, we have zero probability of obtaining the data. Thus, we can equivalently express the PDF as
\begin{equation}
  p(\mathbf{x};\theta)  = \begin{cases}
        \theta^{-N}, & 0 < \max(x[0],x[1],\dots,x[N-1]) < \theta \\\\\\
        0 & \text{else}.
  \end{cases}
\end{equation}
The likelihood function is strictly monotonically decreasing function and is maximized by minimizing the value of $\theta$. However, since $\theta \geq \max(x[0],x[1],\dots,x[N-1]) $, we get
\begin{equation}
\hat\theta_{\text{ML}} = \max(x[0],x[1],\dots,x[N-1]).
\end{equation}

---

Instead of maximizing the likelihood function, we can also maximize the so-called **log-likelihood** function defined as
\begin{equation}
  l(\mathbf{x};\theta) = \ln p(\mathbf{x};\theta).
\end{equation}
Since the logarithm is a monotonically increasing function, $\ln p(\mathbf{x};\theta)$ and $p(\mathbf{x};\theta)$ have their maxima for the same value of $\theta$. If the log-likelihood function is differentiable and the maximum is at an interior point, we further have that the derivative is equal to zero a its maxima, i.e.,
\begin{equation}
\\left.\frac{\partial}{\partial \theta} l(\mathbf{x};\theta) \\right\rvert_{\theta = \hat\theta_{\text{ML}}} = 0.
\label{eq:log_ll_max}
\end{equation}
The above equation is referred to as the likelihood equation. We already encountered the log-likelihood function in the module on the CRLB, which indicates its fundamental importance in estimation theory. If the log-likelihood function is not differentiable, other techniques have to be applied.

We have shown that an efficient estimator can be obtained if the log-likelihood function can be expressed as
\begin{equation}
 \frac{\partial}{\partial\theta}l(\mathbf{x};\theta)=\mathcal{I}(\theta)(g(\mathbf{x})-\theta).
 \label{eq:efficient}
\end{equation}
Combining \eqref{eq:log_ll_max} and \eqref{eq:efficient} yields
\begin{equation}
\\left.\mathcal{I}(\theta)(g(\mathbf{x})-\theta) \\right\rvert_{\theta = \hat\theta_{\text{ML}}} = 0.
\label{eq:ml_efficient}
\end{equation}
Since the Fisher information is a strictly positive quantity $(\mathcal{I}(\theta)>0)$, we require that
\begin{equation}
    g(\mathbf{x})=\hat\theta_{\text{ML}}.
\end{equation}
Consequently, if an efficient estimator exists, then it is the MLE.

---
<b>Example:</b>

We have already seen that the sample mean is an efficient estimator for estimating the DC level in the presence of additive white Gaussian noise. Moreover, we have just shown that if an efficient estimator exists, it is the MLE, and thus the sample mean is also the MLE. We can verify this by looking at the partial derivative of the log-likelihood function, which is
\begin{equation}
  \frac{\partial}{\partial \theta} l(\mathbf{x};\theta) = \frac{1}{\sigma^2} \sum_{n=0}^{N-1}(x[n]-A).
\end{equation}
After equating with zero and solving for $A$, we have that
\begin{equation}
\hat{A}\_{\text{ML}} = \frac{1}{N}\sum_{n=0}^{N-1}x[n],
\end{equation}
which is the efficient estimator found in the module on the CRLB.

---

### Properties of the Maximum Likelihood Estimator

The MLE has many appealing properties for large sample sizes that can be summarized as follows:
\begin{align}
    \mathbb{E}\\left[\hat\theta_{\text{ML}}\\right] &\rightarrow \theta\\\\\\
    \mathrm{Var}\\left[\hat\theta_{\text{ML}}\\right]  &\rightarrow  \mathcal{I}^{-1}(\theta)
\end{align}
Moreover, $\hat\theta_{\text{ML}}$ is asymptotically normal. Combining these properties, we have for $N\rightarrow\infty$ that
\begin{equation}
  \hat\theta_{\text{ML}}\sim \mathcal{N}\\left(\theta,\mathcal{I}^{-1}(\theta)\\right),
\end{equation}
i.e., the MLE is asymptotically consistent and the maximum likelihood estimate is normal distributed.

For some specific problems, we are interest in finding a transformed parameter $\psi(\theta)$, i.e., a parameter which depends on $\theta$. If $\psi$ is a one-to-one mapping, then the maximum likelihood estimate of $\psi$ is
\begin{equation}
	\hat\psi_{\text{ML}} = \psi\\left(\hat\theta_{\text{ML}}\\right)
\end{equation}
which is known as the invariance property of the maximum likelihood estimator.


<!-- ---

<b>Example</b>

Suppose we observe $N$ samples from a signal given as
\begin{equation}
x[n] = A + w[n],
\end{equation}
where $w[n]$ is iid white Gaussian noise with zero mean and variance $A$, i.e.,
\begin{equation}
w[n] \sim \mathcal{N}(0,A).
\end{equation}
Compared to the problems studied in the CRLB module, here the unknown parameter $A$ is also reflected in the variance of the signal. Since the noise is additive, the likelihood function is given as
\begin{equation}
p(\mathbf{x};A) = \frac{1}{(2\pi A)^{\frac{N}{2}}} \exp\\left(-\frac{1}{2A}\sum_{n=0}^{N-1}(x[n]-A)^2\\right)
\end{equation}
The log-likelihood function is
\begin{equation}
\ln p(\mathbf{x};A)=-\frac{N}{2}\ln(2\pi A) - \frac{1}{2\pi A} \sum_{n=0}^{N-1}(x[n]-A)^2,
\end{equation}
and the partial derivative is
\begin{equation}
\frac{\partial}{\partial A} \ln p(\mathbf{x};A) = -\frac{N}{2A} + \frac{1}{A}\sum_{n=0}^{N-1}(x[n]-A) +  \frac{1}{2A^2}\sum_{n=0}^{N-1}(x[n]-A)^2.
\label{eq:log_ll_deriv}
\end{equation}
To evaluate the Fisher information and the CRLB, we evaluate the second derivative which yields

\begin{multline}
\frac{\partial^2}{\partial A^2} \ln p(\mathbf{x};A) = \frac{N}{2A^2} - \frac{1}{A^2}\sum_{n=0}^{N-1}(x[n]-A)-\frac{N}{A} \\\\\\ -  \frac{1}{A^3}\sum_{n=0}^{N-1}(x[n]-A)^2 -  \frac{1}{A^2}\sum_{n=0}^{N-1}(x[n]-A).\qquad\qquad
\end{multline}

Taking the negative expectation with respect to the observations, we get
\begin{align}
-\mathbb{E}\\left[\frac{\partial^2}{\partial A^2}\ln p(\mathbf{x};A)\\right] & = -\frac{N}{2A^2} + \frac{1}{A^2}\sum_{n=0}^{N-1}(A-A)+\frac{N}{A}\nonumber \\\\\\ &\quad + \frac{1}{A^3}\sum_{n=0}^{N-1}(A+A^2-2A^2+A^2) +  \frac{1}{A^2}\sum_{n=0}^{N-1}(A-A)\\\\\\
&= -\frac{N}{2A^2} +\frac{N}{A} +\frac{N}{A^2} \\\\\\
&=  \frac{N}{2A^2} +\frac{N}{A}\\\\
&=  \frac{N\\left(A+\frac{1}{2}\\right)}{A^2} = \mathcal{I}(A)
\end{align}

If an efficient estimator exists, we should be apple to express the derivative of the log-likelihood function \eqref{eq:log_ll_deriv} as
\begin{equation}
 \frac{\partial}{\partial A}\ln p(\mathbf{x};A)=\mathcal{I}(A)(g(\mathbf{x})-A),
\end{equation}
which is in this particular case not possible. However, we can still determine the maximum likelihood estimator by equating \eqref{eq:log_ll_deriv} to zero and solve for $A$ which yields
\begin{align}
 -\frac{N}{2A} + \frac{1}{A}\sum_{n=0}^{N-1}(x[n]-A) +  \frac{1}{2A^2}\sum_{n=0}^{N-1}(x[n]-A)^2 &= 0\\\\\\
  -\frac{N}{2A} - N + \frac{1}{2A^2} \sum_{n=0}^{N-1}x^2[n] +\frac{N}{2}&=0\\\\\\
  A^2 + NA - \frac{1}{N}\sum_{n=0}^{N-1}x^2[n] &=0
\end{align}

\begin{equation}
  \hat{A}\_{\text{ML}}=-\frac{1}{2}  \pm \sqrt{\frac{1}{N}\sum_{n=0}^{N-1}x^2[n]+\frac{1}{4}}
\end{equation}

Unfortunately, the estimator is biased since
\begin{equation}
\mathbb{E}\\left[-\frac{1}{2}  + \sqrt{\frac{1}{N}\sum_{n=0}^{N-1}x^2[n]+\frac{1}{4}}\\right] < -\frac{1}{2}  + \sqrt{\frac{1}{N}\sum_{n=0}^{N-1}\mathbb{E}\\left[x^2[n]\\right]+\frac{1}{4}} = A
\end{equation}
which follows from the Jensen's inequality. However, applying the law of large number, it follows that for large $N$
\begin{equation}
    \frac{1}{N}\sum_{n=0}^{N-1}x^2[n] \rightarrow A +A^2,
\end{equation}
and thus,
\begin{equation}
  \hat{A}\_{\text{ML}} \rightarrow A
\end{equation}


--- -->


## Maximum Likelihood Estimator for Vector Parameter
The concept of the MLE can also in estimating multiple parameters. If the maximum is interior and if the partial derivative with respect to all parameters exists, then a necessary condition for the maximum is
\begin{equation}
  \frac{\partial}{\partial\boldsymbol\theta} l(\mathbf{x};\boldsymbol\theta) = \mathbf{0}.
\end{equation}
Thus, the maximum can be found by equating the gradient of the log-likelihood function with zero.

### Properties of the Maximum Likelihood Estimator for Vector Parameter
The MLE for vector parameter possesses the same asymptotical properties as the MLE for scalar parameter. We summarize the properties as follows: For $N\rightarrow \infty$, the maximum likelihood estimate is
\begin{equation}
\hat{\boldsymbol\theta}_{\text{ML}} \sim \mathcal{N}\\left(\boldsymbol\theta,\mathbf{I}^{-1}(\boldsymbol\theta)\\right),
\end{equation}
where $\mathbf{I}(\boldsymbol\theta)$ is the Fisher information matrix evaluated at the true value of the unknown parameter.


---

<b>Example </b>

Consider the example of estimating the DC level and the noise variance presented in the module on the CRLB. There we already evaluated the expressions we need to evaluate the gradient given as
\begin{align}
\frac{\partial}{\partial A} l(\mathbf{x};\boldsymbol\theta) &= \frac{1}{\sigma^2}\sum_{n=0}^{N-1}(x[n]-A)\\\\\\
\frac{\partial}{\partial \sigma^2} l(\mathbf{x};\boldsymbol\theta) &= -\frac{N}{2\sigma^2}+\frac{1}{2\sigma^4}\sum_{n=0}^{N-1}(x[n]-A)^2 \label{eq:variance} \\\\\\
\end{align}

We already obtained the maximum likelihood estimate for the DC level which is the sample mean
\begin{equation}
\hat{A} = \bar{x} = \frac{1}{N}\sum_{n=0}^{N-1}.
\label{eq:samplemean}
\end{equation}
Equating \eqref{eq:variance} to zero and solving for $\sigma^2$ using $\bar{x}$ yields
\begin{equation}
  \frac{1}{N}\sum_{n=0}^{N-1}(x[n]-\bar{x})^2
\end{equation}

The sample mean $\bar{x}$ is a scaled sum of iid Gaussian random variables, and thus, Gaussian again with mean $A$ and variance $\sigma^2/N$, i.e.,
\begin{equation}
  \bar{x} \sim \mathcal{N}\\left(A,\frac{\sigma^2}{N}\\right)
\end{equation}

On the other hand, by the central limit theorem, it can be shown that
\begin{equation}
    \hat{\sigma^2} \sim \mathcal{N}\left(\frac{N-1}{N}\sigma^2, \frac{2(N-1)}{N^2}\sigma^4\right),
\end{equation}
which, for large $N$, can be approximated by
\begin{equation}
    \hat{\sigma^2} \sim \mathcal{N}\left(\sigma^2, \frac{2}{N}\sigma^4\right).
\end{equation}
Thus, we have that our estimates are asymptotically unbiased, and their variance approaches the CRLB.

---
