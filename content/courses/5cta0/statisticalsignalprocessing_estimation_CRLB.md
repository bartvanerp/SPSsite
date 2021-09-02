+++
title = "Cramer-Rao Lower Bound"

# date = {{ .Date }}
lastmod = 2021-08-17

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "2.1 Cramer-Rao Lower Bound"
weight = 210


+++
## Introduction

Many different estimators can be formulated, as shown in the introduction. We also showed that the variance provides a tool to compare different estimators. In this module, we are going to devise a lower bound for the variance of an unbiased estimator, the so-called Cramer-Rao lower bound or short CRLB. The CRLB provides a lower bound for the variance of an estimate and provides conditions under which an estimator achieves this lower bound.


<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/zCr_1j0VeAg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


## CRLB for Single Parameter
The CRLB states that the variance of any unbiased estimator $g(\mathbf{x})$ is lower bounded by
\begin{equation}
  \mathrm{Var}[g(\mathbf{x})] \geq \\left(\mathbb{E}\\left[\\left(\frac{\partial \ln(p(\mathbf{x};\theta))}{\partial \\theta}\\right)^2\\right]\\right)^{-1}
  \label{eq:CR_1}
\end{equation}
or, equivalently, by
\begin{equation}
  \mathrm{Var}[g(\mathbf{x})] \geq \\left(-\mathbb{E}\\left[\frac{\partial^2 \ln(p(\mathbf{x};\theta))}{\partial \\theta^2}\\right]\\right)^{-1}.
  \label{eq:CR_Fisher}
\end{equation}
The inequalities are valid if the following regularity conditions hold:
\begin{equation}
 \frac{d}{d \theta}\int p(\mathbf{x};\theta) d\mathbf{x} = \int\frac{\partial}{\partial \theta} p(\mathbf{x};\theta)d\mathbf{x} = 0
\end{equation}
and
\begin{equation}
\frac{d}{d \theta}\int g(\mathbf{x}) p(\mathbf{x};\theta) d\mathbf{x} = \int g(\mathbf{x})\frac{\partial}{\partial \theta}d p(\mathbf{x};\theta)d\mathbf{x} = 0.
\end{equation}
The regularity conditions ensure that we can interchange the order of differentiation and integration. The conditions are violated, for example, when the domain of integration depends on the parameter $\theta$. The quantity
\begin{equation}
  \mathcal{I}(\theta) =\mathbb{E}\\left[\\left(\frac{\partial \ln(p(\mathbf{x};\theta))}{\partial \\theta}\\right)^2\\right]= -\mathbb{E}\\left[\frac{\partial^2 \ln(p(\mathbf{x};\theta))}{\partial \\theta^2}\\right]
\end{equation}
is the so-called Fisher information and tells how much information random variables carrier about an unknown parameter $\theta$.


<div class="example", style="background-color:LightGray;">
<details>
<summary>Proof</summary>

Since we assume that our estimator is unbiased, we have that
\begin{equation}
  \mathbb{E}\left[g(\mathbf{x})-\theta\right] = \int (g(\mathbf{x})-\theta) p(\mathbf{x};\theta)d\mathbf{x} = 0.
\end{equation}
Differentiating both sides with respect to $\theta$ and using the regularity conditions, we obtain
\begin{equation}
    \int (g(\mathbf{x})-\theta)\frac{\partial}{\partial\theta}p(\mathbf{x};\theta)d\mathbf{x}-1=0
\end{equation}
or, equivalently,
\begin{equation}
    \int (g(\mathbf{x})-\theta)\frac{\partial}{\partial\theta}p(\mathbf{x};\theta)d\mathbf{x}=1.
    \label{eq:CRLB_1}
\end{equation}
The partial derivative in \eqref{eq:CRLB_1} can be expressed as
\begin{equation}
  \frac{\partial}{\partial\theta}p(\mathbf{x};\theta) = p(\mathbf{x};\theta)\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta).
  \label{eq:partial_ln}
\end{equation}
Substituting \eqref{eq:partial_ln} in \eqref{eq:CRLB_1} yields
\begin{equation}
    \int (g(\mathbf{x})-\theta)p(\mathbf{x};\theta)\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)d\mathbf{x}=1.
    \label{eq:CRLB_2}
\end{equation}
We can rewrite the left-hand side of \eqref{eq:CRLB_2} as
\begin{equation}
    \int \left[(g(\mathbf{x})-\theta)\sqrt{p(\mathbf{x};\theta)}\right]\left[\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\sqrt{p(\mathbf{x};\theta)}\right]d\mathbf{x},
\end{equation}
which is an inner product between the two expression in the square brackets. The inner product is upper bounded by the Cauchy-Schwarz inequality given as
\begin{multline}
    \left(\int \left[(g(\mathbf{x})-\theta)\sqrt{p(\mathbf{x};\theta)}\right]\left[\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\sqrt{p(\mathbf{x};\theta)}\right]d\mathbf{x}\right)^2\\\\\\ \leq \int (g(\mathbf{x})-\theta)^2p(\mathbf{x};\theta)d\mathbf{x}  \int \left(\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\right)^2p(\mathbf{x};\theta)d\mathbf{x}. \qquad
    \label{eq:CSineq}
\end{multline}
The left hand side of \eqref{eq:CSineq} is 1. But
\begin{equation}
\int (g(\mathbf{x})-\theta)^2p(\mathbf{x};\theta)d\mathbf{x}  = \mathrm{Var}\left[g(\mathbf{x})\right]
\end{equation}
and
\begin{equation}
\int \left(\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\right)^2p(\mathbf{x};\theta)d\mathbf{x}=  \mathbb{E}\left[ \left(\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\right)^2 \right]
\end{equation}
so that we obtaine
\begin{equation}
\mathrm{Var}\left[g(\mathbf{x})\right] \geq \left(\mathbb{E}\left[ \left(\frac{\partial}{\partial\theta} \ln p(\mathbf{x};\theta)\right)^2 \right]\right)^{-1}.
\end{equation}
To obtain the equivalent expression \eqref{eq:CR_Fisher}, we integrate \eqref{eq:partial_ln}, which gives
\begin{equation}
  \int p(\mathbf{x};\theta)\frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)d\mathbf{x} = \int \frac{\partial}{\partial\theta} p(\mathbf{x};\theta)d\mathbf{x}=\frac{d}{d\theta} \int p(\mathbf{x};\theta)d\mathbf{x} = 0.
\end{equation}
Differentiating again with respect to $\theta$, we get
\begin{equation}
  \int \frac{\partial}{\partial\theta}p(\mathbf{x};\theta)\frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)d\mathbf{x}+\int p(\mathbf{x};\theta)\frac{\partial^2}{\partial\theta^2}\ln p(\mathbf{x};\theta)d\mathbf{x} = 0,
\end{equation}
where we substitue \eqref{eq:partial_ln} again into the first integral to obtain
\begin{equation}
  \int p(\mathbf{x};\theta)\left(\frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)\right)^2 d\mathbf{x}+\int p(\mathbf{x};\theta)\frac{\partial^2}{\partial\theta^2}\ln p(\mathbf{x};\theta)d\mathbf{x} = 0
\end{equation}
or
\begin{equation}
\mathbb{E}\left[\left(\frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)\right)^2\right] = -\mathbb{E}\left[\frac{\partial^2}{\partial\theta^2}\ln p(\mathbf{x};\theta)\right].
\end{equation}
</details>
</div>

### Efficient Estimator
An estimator that attains the lower bound is called **efficient**. In general, there is no guaranty that such an estimator exist at all. However, the Cauchy-Schwarz inequality not only provides an lower bound for the variance but also conditions for equality. If we can express  $\frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)$ in the form
\begin{equation}
 \frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)=\mathcal{I}(\theta)(g(\mathbf{x})-\theta),
 \label{eq:efficient_est}
\end{equation}
we can directly determine the expression to find the efficient estimator.

<div class="example", style="background-color:LightGray;">
<details>
<summary>Proof</summary>
  Equality in \eqref{eq:CSineq} holds if and only if
    \begin{equation}
     \frac{\partial}{\partial\theta}\ln p(\mathbf{x};\theta)=a(\theta)(g(\mathbf{x})-\theta).
    \end{equation}
    where $a(\theta)$ is an arbitrary function solely depending on $\theta$ and not on $\mathbf{x}$. To determine the function $a(\theta)$, we note that
    \begin{equation}
        \frac{\partial^2}{\partial\theta^2} \ln p(\mathbf{x};\theta) = \frac{\partial}{\partial\theta}\left(a(\theta)\right)(g(\mathbf{x})-\theta) - a(\theta).
    \end{equation}
    Taking the expectation and considering the unbiasedness assumption, we obtain
    \begin{equation}
      -\mathbb{E}\left[\frac{\partial^2}{\partial\theta^2}\ln p(\mathbf{x};\theta)\right] = a(\theta),
    \end{equation}
    i.e., the function $a(\theta)$ is the Fisher information $\mathcal{I}(\theta)$.

  </details>
</div>


---
<b>Example:</b>

Let us return to the example of estimating the DC voltage embedded in noise presented in the introduction module. We want to find the lowest attainable variance. Therefore, we start with the PDF of our observations given as
\begin{equation}
 p(\mathbf{x};A) = \frac{1}{(2\pi\sigma^2)^{N/2}}\exp\\left[-\frac{1}{2\sigma^2}\sum_{n=0}^{N-1}(x[n]-A)^2\\right].
\end{equation}
Taking the logarithm yields
\begin{equation}
  \ln p(\mathbf{x};A) = -\frac{N}{2}\ln(2\pi\sigma^2) -\frac{1}{2\sigma^2}\sum_{n=0}^{N-1}(x[n]-A)^2,
\end{equation}
and after differentiating with respect to $\theta$, we obtain
\begin{equation}
\frac{\partial}{\partial A} \ln p(\mathbf{x};A) = \frac{1}{\sigma^2}\sum_{n=0}^{N-1}(x[n]-A).
\label{eq:log_ll}
\end{equation}

The CRLB can now be found by either evaluating \eqref{eq:CR_1} or \eqref{eq:CR_Fisher}. For the sake of completeness, let us evaluate both expressions starting with\eqref{eq:CR_1}, which is
\begin{align}
  \mathbb{E}\\left[ \\left(\frac{\partial}{\partial A} \ln p(\mathbf{x};A) \\right)^2 \\right] &=  \frac{1}{\sigma^4} \mathbb{E}\\left[ \\left(\sum_{n=0}^{N-1}(x[n]-A)\\right) \\left(\sum_{m=0}^{N-1}(x[m]-A)\\right) \right] \\\\\\
  &=\frac{1}{\sigma^4} \mathbb{E}\\left[ \\left(\sum_{n=0}^{N-1}x[n]-NA\\right) \\left(\sum_{m=0}^{N-1}x[m]-NA\\right) \right]\\\\\\
  &=\frac{1}{\sigma^4} \mathbb{E}\\left[ \sum_{n=0}^{N-1}x[n]\sum_{m=0}^{N-1}x[m]\\right]\nonumber \\\\\\ & \qquad-NA\cdot\mathbb{E}\\left[\sum_{n=0}^{N-1}x[n]+\sum_{m=0}^{N-1}x[m] \right]+  (NA)^2 \\\\\\
  &=\frac{1}{\sigma^4} \mathbb{E}\\left[ \sum_{n=0}^{N-1}x^2[n]+\sum_{n=0}^{N-1}\sum_{\substack{m=0 \\\\\\ m\neq n}}^{N-1}x[n]x[m] \right] - \nonumber \\\\\\ &  \qquad 2(NA)^2 + (NA)^2\\\\\\
  &=\frac{1}{\sigma^4}  \\left(N\sigma^2+NA^2 + N(N-1)A^2-2(NA)^2+  (NA)^2 \\right)\\\\\\
  &=\frac{1}{\sigma^4} N\sigma^2\\\\\\
  &= \frac{N}{\sigma^2}. \label{eq:CR_mean}
\end{align}
Evaluating \eqref{eq:CR_Fisher}, we get
\begin{equation}
-\mathbb{E}\\left[\frac{\partial^2}{\partial A^2} \ln p(\mathbf{x},A)\\right] = -\mathbb{E}\\left[-\frac{N}{\sigma^2}\\right] = \frac{N}{\sigma^2},
\end{equation}
which is equivalent to \eqref{eq:CR_mean}, and thus, we have that
\begin{equation}
 \mathrm{Var}\\left[g(\mathbf{x})\\right] \geq \frac{\sigma^2}{N}.
\end{equation}
Note that this is the variance of the sample mean estimator presented in the introduction module. This result can also be verified by checking if we can express \eqref{eq:log_ll} in the form of \eqref{eq:efficient_est}. Rewriting \eqref{eq:log_ll} as
\begin{equation}
\frac{\partial}{\partial A} \ln p(\mathbf{x};A) =\underbrace{\frac{N}{\sigma^2}}\_{\mathcal{I}(\theta)}\\left(\underbrace{\frac{1}{N}\sum_{n=0}^{N-1}x[n]}\_{g(\mathbf{x})}-\underbrace{A}\_{\theta} \\right)
\label{eq:log_ll_eff}
\end{equation}
and comparing the single quantities in \eqref{eq:log_ll_eff} with \eqref{eq:efficient_est}, we recognize the expression
\begin{equation}
  g(\mathbf{x}) = \frac{1}{N} \sum_{n=0}^{N-1}x[n]
\end{equation}
as the efficient estimator for estimating the DC level embedded in white Gaussian noise.

---

### CRLB for IID Observations
The previous example highlighted another property of the CRLB in the case of IID observations. For IID observations, we have that the joint PDF factorizes as
\begin{equation}
  p(\mathbf{x};\theta) = \prod_{n=0}^{N-1} p(x[n];\theta),
\end{equation}
and since the logarithm of a product is the sum of the individual logarithms, we further have that
\begin{equation}
  \ln p(\mathbf{x};\theta) = \sum_{n=0}^{N-1}  \ln p(x[n];\theta).
\end{equation}
Taking the second derivative and the negative expectation over the observations $\mathbf{x}$, we get
\begin{equation}
-\mathbb{E} \\left[\frac{\partial^2}{\partial\theta^2}\ln p(\mathbf{x};\theta)\\right] = -\sum_{n=0}^{N-1}\mathbb{E}\\left[\frac{\partial^2}{\partial\theta^2}\ln p(x[n];\theta)\\right] = -N\mathbb{E}\\left[\frac{\partial^2}{\partial\theta^2}\ln p(x[n];\theta)\\right].
\end{equation}
Thus, the Fisher information for all $N$ observations is $N$-times the Fisher information of a single observation given as $-\mathbb{E}\\left[\ln p(x[n];\theta)\\right]$. Consequently, the CRLB decreases as the number of observations increases.

### General CRLB for Signals in White Gaussian Noise
In many engineering applications, we are confronted with signals corrupted by additive white Gaussian noise. In this case, we can model the observations as  
\begin{equation}
    x[n] = s[n;\theta] + w[n], \qquad n = 0,1,\dots,N-1,
\end{equation}
and the corresponding PDF as
\begin{equation}
 p(\mathbf{x};\theta) = \frac{1}{(2\pi\sigma^2)^{N/2}}\exp\\left[-\frac{1}{2\sigma^2}\sum_{n=0}^{N-1}(x[n]-s[n;\theta])^2\\right].
\end{equation}

Differentiating the logarithm of the PDF twice yields
\begin{equation}
      \frac{\partial^2}{\partial \theta^2} \ln  p(\mathbf{x};\theta) = \frac{1}{\sigma^2} \sum_{n=0}^{N-1} \\left\\{(x[n]-s[n;\theta])\frac{\partial^2}{\partial \theta^2}s[n;\theta]-\\left(\frac{\partial}{\partial \theta}s[n;\theta]\\right)^2\right\\}
\end{equation}
Calculating the negative expectation with respect to the observation $\mathbf{x}$ results in
\begin{equation}
  -\mathbb{E}\\left[ \frac{\partial^2}{\partial \theta^2} \ln  p(\mathbf{x};\theta) \\right] = \frac{1}{\sigma^2} \sum_{n=0}^{N-1}\\left(\frac{\partial}{\partial \theta}s[n;\theta]\\right)^2
\end{equation}
and the CRLB can be expressed as
\begin{equation}
  \mathrm{Var}\\left[g(\mathbf{x})\\right] \geq \frac{1}{\frac{1}{\sigma^2} \sum_{n=0}^{N-1}\\left(\frac{\partial}{\partial \theta}s[n;\theta]\\right)^2}.
  \label{eq:crlb_awgn}
\end{equation}
We can directly apply these result to the DC voltage estimation problem. The signal model is given by
\begin{equation}
 s[n;A] = A,
\end{equation}
and the partial derivative is simply
\begin{equation}
  \frac{\partial s[n,A]}{\partial A} = 1.
\end{equation}
Thus, \eqref{eq:crlb_awgn} becomes in this particular case
\begin{equation}
  \mathrm{Var}\\left[g(\mathbf{x})\\right] \geq \frac{1}{\frac{1}{\sigma^2} \sum_{n=0}^{N-1}1 }= \frac{\sigma^2}{N}.
\end{equation}

## CRLB for Vector Parameter
Let $\boldsymbol\theta = [\theta_0,\theta_1,\dots,\theta_{P-1}]^T$ be the vector holding the unknown parameters and let $\hat{\boldsymbol\theta}=g(\mathbf{x})$ be the estimate of the parameter vector. Then, for any unbiased estimator, the covariance matrix  $\mathbf{C}_{\hat{\boldsymbol\theta}}$ given as
\begin{equation}
\mathbf{C}_{\hat{\boldsymbol\theta}} = \mathbb{E}\begin{bmatrix}(g(\mathbf{x})-\boldsymbol\theta)(g(\mathbf{x})-\boldsymbol\theta)^T\end{bmatrix},
\end{equation}
is lower bounded by
\begin{equation}
\mathbf{C}_{\hat{\boldsymbol\theta}} \geq \mathbf{I}^{-1}(\boldsymbol\theta),
\label{eq:CRLB_vector}
\end{equation}
where $\mathbf{I}(\boldsymbol\theta)$ is the so-called Fisher information matrix
with entries
\begin{equation}
  \\left[\mathbf{I}(\boldsymbol\theta)\\right]_{i,j} = \mathbb{E}\\left[\\left(\frac{\partial}{\partial\theta_i}\ln p(\mathbf{x};\boldsymbol\theta) \\right)\\left(\frac{\partial}{\partial\theta_j}p(\mathbf{x};\boldsymbol\theta)\\right)\\right] = - \mathbb{E}\\left[\frac{\partial^2}{\partial\theta_i\partial\theta_j}\ln p( \mathbf{x};\boldsymbol\theta)\\right].
\end{equation}
The notation $\mathbf{C}_{\hat{\boldsymbol\theta}} \geq \mathbf{I}^{-1}(\boldsymbol\theta)$ in \eqref{eq:CRLB_vector} refers to the condition that the difference of the matrices is positive semi-definite, i.e., $\mathbf{a}^T(\mathbf{C}\_{\hat{\boldsymbol\theta}}-\mathbf{I}^{-1}(\boldsymbol\theta))\mathbf{a}\geq 0$ for arbitrary $\mathbf{a}\neq \mathbf{0}$.
Similar to the scalar case, equality holds if and only if
\begin{equation}
  \frac{\partial}{\partial\boldsymbol\theta} \ln p(\mathbf{x},\boldsymbol\theta) = \mathbf{I}(\boldsymbol\theta)(g(\mathbf{x})-\boldsymbol\theta).
\end{equation}

---
<b>Example:</b>

Suppose we want to estimate in addition to the DC voltage level of the previous example also the variance $\sigma^2$ of the noise. The required expressions are:
\begin{align}
\frac{\partial}{\partial A} \ln p(\mathbf{x};\boldsymbol\theta) &= \frac{1}{\sigma^2}\sum_{n=0}^{N-1}(x[n]-A)\\\\\\
\frac{\partial}{\partial \sigma^2} \ln p(\mathbf{x};\boldsymbol\theta) &= -\frac{N}{2\sigma^2}+\frac{1}{2\sigma^4}\sum_{n=0}^{N-1}(x[n]-A)^2\\\\\\
\frac{\partial^2}{\partial A^2} \ln p(\mathbf{x};\boldsymbol\theta) &= \frac{N}{\sigma^2}\\\\\\
\frac{\partial^2}{\partial (\sigma^2)^2} \ln p(\mathbf{x};\boldsymbol\theta) &= \frac{N}{2\sigma^4}-\frac{1}{\sigma^6}\sum_{n=0}^{N-1}(x[n]-A)^2\\\\\\
\frac{\partial^2}{\partial A \partial\sigma^2} \ln p(\mathbf{x};\boldsymbol\theta)&= \frac{\partial^2}{ \partial\sigma^2 \partial A} \ln p(\mathbf{x};A) = -\frac{1}{\sigma^4}\sum_{n=0}^{N-1}(x[n]-A)^2
\end{align}

The corresponding Fisher information matrix is
\begin{equation}
  \mathbf{I}(\boldsymbol\theta) = \begin{bmatrix} \frac{N}{\sigma^2} & 0, \\\\\\
  0 & \frac{N}{2\sigma^4}
  \end{bmatrix},
\end{equation}
and since it is a diagonal matrix we have that its inverse is simply the inverse of the main diagonal entries
\begin{equation}
  \mathbf{I}^{-1}(\boldsymbol\theta) = \begin{bmatrix} \frac{\sigma^2}{N} & 0 \\\\\\
  0 & \frac{2\sigma^4}{N}
  \end{bmatrix}.
\end{equation}
The individual variances are lower bounded by
\begin{equation}
  \mathrm{Var}[A] \geq   \frac{\sigma^2}{N},
\end{equation}
and
\begin{equation}
  \mathrm{Var}[\sigma^2] \geq   \frac{2\sigma^4}{N}.
\end{equation}

---

## Summary and Conclusion
In this module, we derived the CRLB for unbiased estimators. The CRLB provides a lower bound on the variance for any unbiased estimator. The derivation of the CRLB is based on the Cauchy-Schwarz inequality, which provides a constraint for equality. This equality constraint can be used to find an efficient estimator. If this constraint is not fulfilled, we have to find other tools ways to find an MVUE. A popular estimator closely related to the CRLB is the maximum likelihood estimator, the subject of the next module.
