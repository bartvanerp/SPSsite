+++
title = "Numerical Methods for Solving Estimators"

# date = {{ .Date }}
lastmod = 2020-06-08

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "2.6 Numerical Methods for Solving Estimators"
weight = 260


+++
## Introduction

For each estimator we investigate in this course, we introduce the formal description and demonstrate the derivation of a closed-form estimator when the signal model and noise distribution are suitable. However, the closed-form solution may not be available in many situations. Moreover, the data might be following a time-dependent distribution, which precludes using a single signal model for a data batch. In this module, we will see several solution methods to cover such situations. It can be said that a significant portion of the signal processing research focuses on devising solutions to problems that deviate from the standard methods described in this course. Thus, this module is far from a comprehensive investigation of all such methods. The goal of this module is to give insight into the practical side of the estimation problems.

<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/kf0seqVj_5U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


## The Gauss-Newton Method

In <a href="../estimation_leastsquares">the least-squares estimation module</a>, we consider the grid search to find the minimum of the squared error term. The tricky part of the grid search is the inability to determine the exact parameter value that corresponds to the minimum. Increasing the density of the grid points reduces the error in the parameter estimate asymptotically. Numerical methods that search for the extremum are utilized to obtain estimates with smaller error. The Gauss-Newton method is a numerical method that follows the gradient to reach the extremum.

The Gauss-Newton method is based on approximating a function by the first two terms of its Taylor series around a particular point. In other words, at a particular parameter value of interest, we replace the non-linear function by a line that has the same slope (i.e. the value for the first derivative) as the original function.

We demonstrate the Gauss-Newton method for the LSE by starting with the approximation of the non-linear signal model:
\begin{equation}
s[n,\theta]\approx s[n,\theta_0]+\frac{\partial s[n,\theta]}{\partial \theta}\Bigg|_{\theta=\theta_0}(\theta-\theta_0),
\end{equation}
where $s[n,\theta]$ is the signal model and $\theta_0$ is the parameter value for which we are calculating the approximation. This approximation for the scalar parameter $\theta$ is extended to vector parameter $\boldsymbol\theta$:
\begin{equation}
\mathbf{s}(\boldsymbol\theta)\approx \mathbf{s}(\boldsymbol\theta_0)+\mathbf{H}(\boldsymbol\theta_0)(\boldsymbol\theta-\boldsymbol\theta_0),
\end{equation}
where the observation matrix $\mathbf{H}(\boldsymbol\theta_0)$ consists of columns $\mathbf{h}_k$, i.e., $\mathbf{H}(\boldsymbol\theta_0)=[\mathbf{h}_1~ \mathbf{h}_2~...~\mathbf{h}_K]$,
\begin{equation}
\mathbf{h}_k=\frac{\partial \mathbf{s}(\boldsymbol\theta)}{\partial\theta_k}.
\end{equation}
Thus, the partial derivative of the signal model $\mathbf{s}(\boldsymbol\theta)$ with respect to an element $\theta_k$ of the parameter vector $\boldsymbol\theta$ is evaluated at $\boldsymbol\theta=\boldsymbol\theta_0$ and the values constitute the $k^{th}$ column of the observation matrix.

The approximation by Taylor series allows us to write the data as
\begin{equation}
\mathbf{x}\approx\mathbf{s}(\boldsymbol\theta_0)-\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta_0+\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta+\mathbf{w}.
\end{equation}
We can write the squared error term according to the linear data model given above, which allows deriving a closed form solution. Consider the squared error term:
\begin{equation}
J(\boldsymbol\theta) = \big(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_0)+\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta_0-\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta\big)^T\big(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_0)+\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta_0-\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta\big)
\end{equation}
To minimize this term, we take the partial derivative with respect to the parameter vector $\boldsymbol\theta$, which follows the derivative operation in linear algebraic form that is described in <a href="../estimation_leastsquares/#least-squares-estimator-for-vector-parameters">the least squares estimation (LSE)</a> module:
\begin{equation}
\frac{\partial J(\boldsymbol\theta)}{\partial\boldsymbol\theta}\Bigg|_{\boldsymbol\theta=\hat{\boldsymbol\theta}}=-2\mathbf{H}(\boldsymbol\theta_0)^T(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_0)+\mathbf{H}(\boldsymbol\theta_0)\boldsymbol\theta_0)+2\mathbf{H}(\boldsymbol\theta_0)^T\mathbf{H}(\boldsymbol\theta_0)\hat{\boldsymbol\theta}=\mathbf{0}
\end{equation}
The estimate $\hat{\boldsymbol\theta}$ is
\begin{equation}
\hat{\boldsymbol\theta}=\boldsymbol\theta_0+\big(\mathbf{H}(\boldsymbol\theta_0)^T \mathbf{H}(\boldsymbol\theta_0)\big)^{-1}\mathbf{H}(\boldsymbol\theta_0)^T\big(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_0)\big)
\end{equation}

We must note that the estimate $\hat{\boldsymbol\theta}$ depends on our choice of initial value $\boldsymbol\theta_0$. We can cast this approximate estimation into an iterative form, where the $m+1^{st}$ iteration step is:
\begin{equation}
\boldsymbol\theta_{m+1}=\boldsymbol\theta_m+\big(\mathbf{H}(\boldsymbol\theta_m)^T \mathbf{H}(\boldsymbol\theta_m)\big)^{-1}\mathbf{H}(\boldsymbol\theta_m)^T\big(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_m)\big)
\end{equation}
Starting from an initial value $\boldsymbol\theta_0$, the LSE can be iteratively calculated to converge to a minimum value. Of course, there has to be <i>criteria to stop the iterations</i>, such as limited change in the parameter estimate, i.e., $(\boldsymbol\theta_{m+1}-\boldsymbol\theta_m)^T(\boldsymbol\theta_{m+1}-\boldsymbol\theta_m)<\epsilon$, and reaching a maximum number of iterations. Selection of the initial parameter vector $\boldsymbol\theta_0$ can be based on a grid search over the squared error function to make sure the numerical solution begins close to the global maximum.


## The Newton-Raphson Method

The Newton-Raphson method searches for the zero of a function by measuring the gradient of that function. The idea is to approximate the behavior of the function at a particular point by a tangential line passing through that point. In other words, on a specific parameter value, the function is approximated by a line with the same slope as the function on that specific parameter value. For a generic function $f[n,\theta]$, the parameter value where the line approximating the function intercepts the parameter axis is found by
\begin{equation}
f(\theta_0)=(\theta_0-\theta)\frac{\partial f(\theta)}{\partial\theta}\Bigg|\_{\theta=\theta_0}
\end{equation}
Solving this equation, we obtain the parameter as
\begin{equation}
\theta=\theta_0-f(\theta_0)\Bigg(\frac{\partial f(\theta)}{\partial\theta}\Bigg|_{\theta=\theta_0}\Bigg)^{-1}
\end{equation}

While the solution to the equation above is closer to the actual zero of the function, there is still room for improvement. The approximation can be utilized again, this time the first derivative is evaluated on the new estimate. The iterative formulation is
\begin{equation}
\theta_{m+1}=\theta_m-f(\theta_m)\Bigg(\frac{\partial f(\theta)}{\partial\theta}\Bigg|_{\theta=\theta_m}\Bigg)^{-1}
\end{equation}

Same as the Gauss-Newton method, there has to be a criteria to stop the iterations and selection of the initial parameter value should allow converging to the global extremum.

We consider the Newton-Raphson method for <a href="../estimation_maximumlikelihood">the maximum likelihood estimation (MLE)</a>, where set the first derivative of the likelihood function to zero and solve it for the parameter vector $\boldsymbol\theta$. The Newton-Raphson method is used to numerically calculate the parameter value at which the derivative of the log-likelihood function is zero. Thus, we will be dealing with both the first and the second derivative of the log-likelihood function. The iterative MLE for the parameter vector $\boldsymbol\theta$ is
\begin{equation}
\boldsymbol\theta_{m+1}=\boldsymbol\theta_m-\frac{\partial \ln p(\mathbf{x};\boldsymbol\theta)}{\partial\boldsymbol\theta}\Bigg|_{\theta=\theta_m}\Bigg(\frac{\partial^2 \ln p(\mathbf{x};\boldsymbol\theta)}{\partial\boldsymbol\theta^2}\Bigg|_{\theta=\theta_m}\Bigg)^{-1}.
\end{equation}

### The Method of Scoring

An extension to the Newton-Raphson method for the MLE is the method of scoring. The idea is to replace the second derivative of the log-likelihood function with its expected value, negative of which is the Fisher information matrix. Thus, the method of scoring yields the iterative estimator
\begin{equation}
\boldsymbol\theta_{m+1}=\boldsymbol\theta_m+\mathcal{I}^{-1}(\boldsymbol\theta_m)\frac{\partial \ln p(\mathbf{x};\boldsymbol\theta)}{\partial\boldsymbol\theta}\Bigg|_{\theta=\theta_m}.
\end{equation}
The Fisher information does not depend on the data, while the second derivative of the log-likelihood function is data-dependent. It is possible to end up with an ill-conditioned second derivative expression that is almost singular. The iteration can become very unstable and unable to converge. The Fisher information alleviates this problem by eliminating the dependence on the data.


## Sequential Least Squares and Best Linear Unbiased Estimators


In some applications the data is streaming and parameter estimation needs to be updated in real time. Instead of running the estimator repeatedly with ever-increasing data size, it is useful to have an estimator that allows updating the estimate by using the latest data samples only. It is possible to formulate the LSE and BLUE in this manner. For LSE, we look for a relation between the estimates $\hat{\boldsymbol\theta}\_{N-1}$ and $\hat{\boldsymbol\theta}_{N}$, which represent the estimate with $N$ data points and $N+1$ data points, respectively. In LSE we do not have a noise model, however, if we know that the noise has zero mean with some known covariance, we can formulate a BLUE estimator that updates both the estimate and covariance for the estimate sequentially.

The starting point is the squared error function:
\begin{equation}
J(\boldsymbol\theta)=(\mathbf{x}-\mathbf{H}\boldsymbol\theta)^T\mathbf{C}^{-1}(\mathbf{x}-\mathbf{H}\boldsymbol\theta),
\end{equation}
where $\mathbf{C}$ is the noise covariance matrix. In this case, the inverse of the noise covariance matrix is used as the weight matrix in the weighted LSE. This means that when the noise variance is known for each data sample, those samples with higher variance can be assigned less weight to reduce their influence on the estimation. The LSE is found to be
\begin{equation}
\hat{\boldsymbol\theta}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}.
\end{equation}
Note that the LSE is actually the BLUE, so we can use the Gauss-Markov theorem to calculate the covariance for our estimate:
\begin{equation}
\mathbf{C}_{\hat{\boldsymbol\theta}}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}.
\end{equation}

The important condition to compute both the estimate $\hat{\boldsymbol\theta}$ and its covariance is the noise being uncorrelated, which corresponds to a diagonal noise covariance matrix. Under this condition, the sequential LSE/BLUE is
\begin{equation}
\hat{\boldsymbol\theta}\_{N}=\hat{\boldsymbol\theta}\_{N-1}+\mathbf{K}\_{N}\big(x[N]-\mathbf{h}^T[N]\hat{\boldsymbol\theta}\_{N-1}\big)
\end{equation}
where $\mathbf{h}^T[N]$ is the $N^\text{th}$ row of the observation matrix $\mathbf{H}$ when the corresponding data sample $x[N]$ is acquired. The term $x[N]-\mathbf{h}^T[N]\hat\Theta_{N-1}$ is the innovation, which is the difference between the data sample $x[N]$ and the estimate we have for that data sample, which is $\mathbf{h}^T[N]\hat{\boldsymbol\theta}\_{N-1}$. Based on our estimated parameter $\hat\Theta_{N-1}$ after the $N^\text{th}$ data sample, we come up with an estimate for the $N+1^\text{th}$ sample we acquire. For BLUE, the estimate is updated according to the innovation and a gain term $\mathbf{K}_{N}$, which is calculated as
\begin{equation}
\mathbf{K}_{N}=\frac{C_{N-1}\mathbf{h}[N]}{\sigma_{N}^2+\mathbf{h}^T[N]C_{N-1}\mathbf{h}[N]}
\end{equation}
For LSE, it is possible to lack information on the noise variance altogether. Thus, we need a gain term that does not depend on the noise covariance. It is obtained by replacing the noise covariance matrix $\mathbf{C}$ in the gain expression with the term $(\mathbf{H}^T\mathbf{H})^{-1}$ and replacing the sample variance term $\sigma_N^2$ by 1. The observation matrix $\mathbf{H}$ belongs to the signal model for the $N$ data samples preceding the current data sample $x[N]$.

Finally, for BLUE the covariance is updated as
\begin{eqnarray*}
\mathbf{C}_N=(\mathbf{I}-\mathbf{K}_N \mathbf{h}^T[N])\mathbf{C}_{N-1}
\end{eqnarray*}

The concepts of innovation, gain and sequential update for the estimate form the core of other recursive filtering techniques such as the Kalman filter. The gain term is actually quite intuitive: The weight of the innovation depends on the relation between the sample variance and the estimator variance. If the sample variance is higher than the estimator variance, then the denominator of the gain term is dominated by the noise variance and the gain is lower. For lower noise variance, the innovation term is considered more reliable and the gain is higher.

## Conclusion

When an estimation problem has no closed form, numerical solution methods are necessary to solve the estimator. There are many different iterative solution methods for various estimators and signal models. In this module, we saw two numerical solution methods that solve minimization/maximization problems by approximating the gradient of the functions. We also explored a sequential solution method, which updates the estimation as new data is obtained.
