+++
title = "MVUE for Linear Models"

# date = {{ .Date }}
lastmod = 2020-06-08

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "2.4 MVUE for Linear Models"
weight = 240

+++
## Introduction

The performance of an estimator can be evaluated by calculating the bias and variance of the estimate. Minimum variance unbiased estimators (MVUE) are a special class of estimators with the minimum variance determined by the Cramer-Rao lower bound (CRLB). In the module that explains the MVUE and CRLB, it was stated that there is no method to find the MVUE, except for several special cases. This module concerns a special class of signal models for which a minimum variance unbiased estimator (MVUE) is available. There are two conditions that these signals satisfy:
<ul>
<li> The signal model is <b>linear</b>,
<li> The noise is <b>additive</b> and <b>Gaussian</b>.
</ul>
The module begins by introducing the linear signal model and derives the MVUE according to the Gaussian noise. To be able to handle a larger class of problems, the MVUE is extended to cover colored Gaussian noise. An interesting approach, when the information on noise distribution is not complete, is to approximate the noise as Gaussian by considering only the expected value and variance for the noise. Such estimators are called best linear unbiased estimators (BLUE), which are covered at the end of the module.


## Linear Signal Model

We model the data as the sum of the output from a data model and noise:
\begin{equation}
x[n]=s[n,\Theta]+\omega[n],
\end{equation}
where the data model $s[n,\Theta]$ is controlled by the parameter $\Theta$. When the model $s[n,\Theta]$ is linear, it can be expressed as
\begin{equation}
\mathbf{s}[\Theta]=\mathbf{H}\mathbf{\Theta},
\end{equation}
where $\mathbf{s}[\Theta]=[s[1]~ s[2]~ ...~ s[N]]^T$ is the vector composed of N samples of the model, $\mathbf{H}$ is called **the observation matrix** and $\Theta=[\theta_1, \theta_2, ..., \theta_K]^T$ is **the parameter vector**.

The complete signal model is written in vector form by introducing the noise vector $\mathbf{w}=[\omega[1]~ \omega[2]~ ... ~\omega[N]]^T:$
\begin{equation}
\mathbf{x}=\mathbf{H}\mathbf{\Theta}+\mathbf{w}.
\end{equation}
The equation tells that the data points are the result of a linear combination of controlling parameters with additive noise.


---
<b>Example:</b>

---

## MVUE for Additive White Gaussian Noise (AWGN)

In this section we will derive the MVUE for linear signal model with additive white Gaussian noise, which is 
\begin{equation}
\hat\Theta=(\mathbf{H}^T\mathbf{H})^{-1}\mathbf{H}^T\mathbf{x}.
\end{equation}
This result is the same as we obtained for the least squares estimator (LSE). In other words, LSE is the MVUE for linear signal model with additive white gaussian noise. The significance of this result is two-folds:
1. The least squares estimator has the best performance for a wide variety of applications where the signal model is linear and the white Gaussian noise model is applicable.
2. We can now assess the performance of the estimator directly by the covariance of the estimate.


The covariance of the estimate is 
\begin{equation}
\Gamma_\hat\Theta=\sigma^2(\mathbf{H}^T\mathbf{H})^{-1},
\end{equation}

where $\sigma^2$ is derived from the **covariance** of the **white Gaussian noise**. 

The derivation of the MVUE for linear signal model with additive white Gaussian noise (AWGN) is given below. The key properties are emphasized and links for detailed explanations are provided.

### Derivation of the MVUE for AWGN

By definition, the MVUE variance should be equal to the CRLB. There is one form for an estimator that guarantees the existence of MVUE. The estimator $\hat\Theta=g(\mathbf{x})$ is unbiased and minimum variance if
\begin{equation}
\frac{\partial \ln p(\mathbf{x};\Theta)}{\partial\Theta}=\mathcal{I}(\Theta)(g(\mathbf{x})-\Theta),
\end{equation}
where $\mathcal{I}(\Theta)$ is **the Fisher information matrix**.

This condition is satisfied when the noise is **white** and **Gaussian distributed**. In that case, the derivative of the log-likelihood function is obtained as
\begin{equation}
\frac{\partial \ln p(\mathbf{x};\Theta)}{\partial\Theta}=\frac{\partial}{\partial\Theta}\Big[-\ln(2\pi\sigma^2)-\frac{1}{2\sigma^2}(\mathbf{x}-\mathbf{H}\Theta)^T(\mathbf{x}-\mathbf{H}\Theta) \Big]=\frac{1}{\sigma^2}[\mathbf{H}^T\mathbf{x}-\mathbf{H}^T\mathbf{H}\Theta].
\end{equation}
To achieve the form of the condition for the existence of MVU, we need to isolate the $\Theta$ term. Multiplication by $(\mathbf{H}^T\mathbf{H})(\mathbf{H}^T\mathbf{H})^{-1}$ yields
\begin{equation}
\frac{\partial \ln p(\mathbf{x};\Theta)}{\partial\Theta}=\frac{\mathbf{H}^T\mathbf{H}}{\sigma^2}[(\mathbf{H}^T\mathbf{H})^{-1}\mathbf{H}^T\mathbf{x}-\Theta]
\end{equation}
which can be considered as consisting of the Fisher information matrix $\mathcal{I}(\Theta)$
\begin{equation}
\mathcal{I}(\Theta)=\frac{\mathbf{H}^T\mathbf{H}}{\sigma^2},
\end{equation}
and the estimator $\hat\Theta=g(\mathbf{x})$
\begin{equation}
g(\mathbf{x})=(\mathbf{H}^T\mathbf{H})^{-1}\mathbf{H}^T\mathbf{x}.
\end{equation}
Because the variance of the estimate $\hat\Theta$ is equal to the CRLB for MVUE, the **covariance** of the estimate $\hat\Theta$ is
\begin{equation}
\Gamma_\hat\Theta=\mathcal{I}^{-1}(\Theta)=\sigma^2(\mathbf{H}^T\mathbf{H})^{-1}.
\end{equation}

The derivation is also available as pencast in **INSERT LINK HERE**.


## MVUE for Colored Gaussian Noise
Rather than deriving the MVUE for colored Gaussian noise, we will adopt *whitening* by a filter such that
\begin{equation}
E[(\mathbf{Dw})(\mathbf{Dw})^T]=\mathbf{I},
\end{equation}
where $\mathbf{I}$ is the identity matrix of size $N\times N$, $N$ being the size of the noise vector. In other words, the covariance matrix for the whitened noise is equal to the identity matrix. The whitening filter $\mathbf{D}$ is found by considering the actual covariance matrix for the colored noise:
\begin{equation}
E[(\mathbf{Dw})(\mathbf{Dw})^T]=\mathbf{D}E[\mathbf{W}\mathbf{w}^T]\mathbf{D}=\mathbf{D}\Gamma\mathbf{D}^T=\mathbf{I}.
\end{equation}
Thus, the noise covariance matrix is decomposed such that
\begin{equation}
\Gamma^{-1}=\mathbf{D}^T\mathbf{D}.
\end{equation}

To obtain the estimator, the whitening is applied to the data,
\begin{equation}
\mathbf{x}'=\mathbf{D}\mathbf{x}=\mathbf{DH}\Theta+\mathbf{Dx},
\end{equation}
and processed using the MVUE for AWGN:
\begin{equation}
\hat\Theta=(\mathbf{H}^T\Gamma^{-1}\mathbf{H})^{-1}\mathbf{H}^T\Gamma^{-1}\mathbf{x}.
\end{equation}
The covariance of the MVUE after whitening is
\begin{equation}
\Gamma_\hat\Theta=(\mathbf{H}^T\Gamma^{-1}\mathbf{H})^{-1}.
\end{equation}

## Best Linear Unbiased Estimator (BLUE)

So far, we have derived the MVUE for linear signal model with AWGN. When there is limited information on the noise distribution, we can still use a linear estimator:
\begin{equation}
\hat\theta_k=\sum_{n=1}^N a_{k,n} x[n].
\end{equation}
In other words, we want to find the estimate $\hat\theta$ by a linear combination of our data. The obvious question at hand is how to determine the coefficients $a_n$ that yield an estimate with zero bias and minimum variance, also called <b>the best linear unbiased estimator (BLUE).</b>

To find the BLUE, we have to start from the assumptions at hand; that the estimator has zero bias and minimum variance. The zero bias condition is formulated as
\begin{equation}
E(\hat\theta_k)=\sum_{n=1}^Na_{k,n}E(x[n])=\mathbf{a_k}^TE(\mathbf{x})=\theta,
\end{equation}
or in matrix form
\begin{equation}
E(\hat\Theta)=\mathbf{A}E(\mathbf{x})=\Theta,
\end{equation}
where $\mathbf{A}$ is the K by N matrix that consists of the coefficients $a_{k,n}$.

The zero bias assumption leads to a linear relation between the parameter $\theta$ and the expected value of the data such that 
\begin{equation}
$E(\mathbf{x})=\mathbf{H}\Theta$.
\end{equation}
In other words, the expected value of the data is described by the linear signal model. In this case, the coefficient matrix $\mathbf{A}$ is related to the signal model as
\begin{equation}
\mathbf{A}\mathbf{H}=\mathbf{I}.
\end{equation}
where $\mathbf{I}$ is the K by K identity matrix.

The variance expression that needs to be minimized is
\begin{equation}
var(\hat\theta_k)=E[(\mathbf{a_k}^T\mathbf{x}-\mathbf{a_k}^TE(\mathbf{x}))^2]=E[(\mathbf{a_k}^T(\mathbf{x}-E(\mathbf{x})(\mathbf{x}-E(\mathbf{x}))^T\mathbf{a_k}]=\mathbf{a_k}^T\Gamma\mathbf{a_k},
\end{equation}
where $\Gamma$ is the covariance matrix for the data, which is equivalent to the covariance matrix for the zero-mean noise due to the linear signal model.

For each parameter $\theta_k$, the variance has to be minimized. We will not pursue the procedure to minimize the variance here, but present the resulting BLUE expression as stated in the <b>Gauss-Markov Theorem</b>:
\begin{equation}
\hat\Theta=(\mathbf{H}^T\Gamma^{-1}\mathbf{H})^{-1}\mathbf{H}^T\Gamma^{-1}\mathbf{x}.
\end{equation}
The covariance matrix for the estimate $\hat\Theta$ is
\begin{equation}
\Gamma_{\hat\Theta}=(\mathbf{H}^T\Gamma^{-1}\mathbf{H})^{-1}.
\end{equation}
Note that the BLUE indeed refers only to the covariance matrix of the noise, and it is actually the same expression as the MVUE for additive Gaussian noise. Thus, for Gaussian noise, the BLUE is also the MVUE.

## Conclusion

In this module we put into use the powerful concept of MVUE. The MVUE form given by the CRLB is applicable to linear signal models with Gaussian noise, which means we are able to attain the lowest possible variance in our estimates $\hat\theta$. Obviously, not all problems are linear, and the probability distribution of the data does not have to be Gaussian. However, certain transformations might cast the problem at hand into the linear form, and approximating the distribution of the data by using only the covariance can lead to solutions that are acceptable for some applications.