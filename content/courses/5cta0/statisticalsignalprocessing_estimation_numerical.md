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

## Grid Search
Closed-form solutions for estimators like the MLE or the LSE only exist for particular cases such as linear signal models. For all other cases, we have to resort to other methods to find the estimate. For the MSE, for example, we can evaluate the likelihood function numerically at equally spaced points for the parameter vector $\boldsymbol\theta$. If we choose the spacing between the points sufficiently small, we can find a value close to the real solution. This method is referred to as grid search. The application of the gird search, however, is restricted to simple problems. For example, if the range of possible values for the parameter is unbounded, the grid search becomes infeasible.

## The Newton-Raphson Method
The Newton-Raphson method is a method to approximate a function at a given point or to solve an equation. In maximum likelihood estimation, we want to solve the likelihood equation, and thus, we are interested in particular in the latter case application. The idea is to approximate the function's behavior at a particular point by a linear function. The derivative of the function determines the slope of the linear function at this point. Thus, the function is approximated as
\begin{equation}
f(x)=f(a)+f'(a)(x-a),
\label{eq:approx}
\end{equation}
where $f'(a)$ denotes the derivative of $f(x)$ evaluated at point $a$. In the particular case of solving the equation $f(x)=0$, we obtain
\begin{equation}
x = a - \frac{f(a)}{f'(a)}.
\end{equation}

While the solution to the equation above is closer to the actual zero of the function, there is still room for improvement. The approximation can be utilized again. This time the first derivative is evaluated on the new estimate. The iterative formulation is
\begin{equation}
x_{m+1}=x_m-\frac{f(x_m)}{f'(x_m)}
\end{equation}
A solution is found if $x_{m+1}=x_m$. Note that, depending on the starting point, the method may converge to a local minimum. Thus, to find a global minimum, the method should be initialized at different values.

### Newton-Raphson Method for Maximum Likelihood Estimation

We consider the Newton-Raphson method for the MLE, where it is used to numerically calculate the parameter value at which the derivative of the log-likelihood function is zero. Thus, we will be dealing with both the first and the second derivatives of the log-likelihood function. The iterative MLE for the parameter vector $\theta$ is
\begin{equation}
\theta_{m+1}=\theta_m-\\left(\frac{\partial^2 \ln p(\mathbf{x};\theta)}{\partial\theta^2}\Bigg|_{\theta=\theta_m}\\right)^{-1}\frac{\partial \ln p(\mathbf{x};\theta)}{\partial\theta}\Bigg|_{\theta=\theta_m}.
\end{equation}

### The Method of Scoring

An extension to the Newton-Raphson method for the MLE is the method of scoring. The idea is to replace the second derivative of the log-likelihood function with its expected value, negative of which is the Fisher information matrix. Thus, the method of scoring yields the iterative estimator
\begin{equation}
\theta_{m+1}=\theta_m+\mathcal{I}^{-1}(\theta_m)\frac{\partial \ln p(\mathbf{x};\theta)}{\partial\theta}\Bigg|_{\theta=\theta_m}.
\end{equation}
The Fisher information does not depend on the data, while the second derivative of the log-likelihood function is data-dependent. It is possible to end up with an ill-conditioned second derivative expression that is almost singular. The iteration can become very unstable and unable to converge. The Fisher information alleviates this problem by eliminating the dependence on the data.


### Extension to Vector Parameter
The Newton-Raphson method can be generalized to vector parameter $\boldsymbol\theta$ which gives following general iteration rule for the MLE:
\begin{equation}
  \boldsymbol\theta_{m+1} = \boldsymbol\theta_{m} - \\left(\mathbf{H}^{-1}(\boldsymbol\theta) \frac{\partial}{\partial\boldsymbol\theta}\ln p(\mathbf{x};\boldsymbol\theta)\\right)\bigg|_{\boldsymbol\theta = \boldsymbol\theta_m}
\end{equation}
where $\mathbf{H}$ is the Hessian matrix with elements
\begin{equation}
\mathbf{H}(\boldsymbol\theta)_{i,j} = \frac{\partial \ln(p(\mathbf{x};\boldsymbol\theta))}{\partial\theta_i\theta_j}.
\end{equation}

Equivalently, the scoring method becomes

\begin{equation}
  \boldsymbol\theta_{m+1} = \boldsymbol\theta_{m} + \mathbf{I}^{-1}(\boldsymbol\theta)\frac{\partial}{\partial\boldsymbol\theta}\ln p(\mathbf{x};\boldsymbol\theta)\bigg|_{\boldsymbol\theta = \boldsymbol\theta_m},
\end{equation}
where $\mathbf{I}(\boldsymbol\theta)$ is the Fisher information matrix.



## The Gauss-Newton Method for Least Squares
The above introduced Newton-Raphson method can also be applied to nonlinear least-squares problems. However, we can derive another method by using the linear approximation of a function. The cost function of the LSE is given as
\begin{equation}
J(\theta) = \sum_{n=0}^{N-1}(x[n]-s[n;\theta])^2.
\end{equation}
Using the approximation \eqref{eq:approx}, we obtain the following approximation of the cost function
\begin{align}
J(\theta) &\approx \sum_{n=0}^{N-1}\\left(x[n]-s[n;\theta_0]-\\left.\frac{\partial s[n;\theta]}{\partial\theta}\\right|_{\theta=\theta_0}(\theta-\theta_0)\\right)^2\\\\\\
          &= \sum_{n=0}^{N-1}\\left(x[n]-s[n;\theta_0]+\\left.\frac{\partial s[n;\theta]}{\partial\theta}\\right|_{\theta=\theta_0}\theta_0-\\left.\frac{\partial s[n;\theta]}{\partial\theta}\\right|_{\theta=\theta_0}\theta\\right)^2\\\\\\
          &=\\left(\mathbf{x}-\mathbf{s}(\theta_0)+\mathbf{h}(\theta_0)\theta_0-\mathbf{h}(\theta_0)\theta\\right)^T\\left(\mathbf{x}-\mathbf{s}(\theta_0)+\mathbf{h}(\theta_0)\theta_0-\mathbf{h}(\theta_0)\theta\\right),\label{eq:Gauss-Newton}
\end{align}
with
\begin{equation}
\mathbf{h}(\theta_0)= \\left.\begin{bmatrix}\frac{\partial s[0;\theta]}{\partial\theta} & \frac{\partial s[1;\theta]}{\partial\theta} &\dots & \frac{\partial s[N-1;\theta]}{\partial\theta} \end{bmatrix}^T\\right|_{\theta=\theta_0}.
\end{equation}
Note that the expression $\mathbf{x}-\mathbf{s}(\theta_0)+\mathbf{h}(\theta_0)\theta_0$ is known. To find the minimum, we equate the derivative of \eqref{eq:Gauss-Newton} with zero and solve for $\theta$ which yields
\begin{equation}
\hat\theta = \\left(\mathbf{h}^T(\theta_0)\mathbf{h}(\theta_0)\\right)^{-1}\mathbf{h}^T(\theta_0)\\left(\mathbf{x}-\mathbf{s}(\theta_0)+\mathbf{h}(\theta_0)\theta_0\\right).
\end{equation}
or, equivalently,
\begin{equation}
\hat\theta =\theta_0+ \\left(\mathbf{h}^T(\theta_0)\mathbf{h}(\theta_0)\\right)^{-1}\mathbf{h}^T(\theta_0)\\left(\mathbf{x}-\mathbf{s}(\theta_0)\\right).
\end{equation}
This method is the Gauss-Newton method.


To obtain a more accurate result, this procedure can be carried out iteratively using following iteration steps
\begin{equation}
\theta_{m+1} =\theta_{m}+ \\left(\mathbf{h}^T(\theta_m)\mathbf{h}(\theta_m)\\right)^{-1}\mathbf{h}^T(\theta_m)\\left(\mathbf{x}-\mathbf{s}(\theta_m)\\right).
\end{equation}


The presented method can be generalized for vector parameter. The corresponding iteration rule is
\begin{equation}
\boldsymbol\theta_{m+1} =\boldsymbol\theta_{m}+ \\left(\mathbf{H}^T(\boldsymbol\theta_m)\mathbf{H}(\boldsymbol\theta_m)\\right)^{-1}\mathbf{H}^T(\boldsymbol\theta_m)\\left(\mathbf{x}-\mathbf{s}(\boldsymbol\theta_m)\\right),
\end{equation}
where $\mathbf{H}(\boldsymbol\theta)$ is the Jacobian matrix with elements
\begin{equation}
    \mathbf{H}(\boldsymbol\theta)_{i,j} = \frac{\partial s[i;\boldsymbol\theta]}{\partial \theta_j }.
\end{equation}

Starting from an initial value $\boldsymbol\theta_0$, the LSE can be iteratively calculated to converge to a minimum value. Of course, there have to be <i>criteria to stop the iterations</i>, such as a limited change in the parameter estimate, i.e., $(\boldsymbol\theta_{m+1}-\boldsymbol\theta_m)^T(\boldsymbol\theta_{m+1}-\boldsymbol\theta_m)<\epsilon$, and reaching a maximum number of iterations. The selection of the initial parameter vector $\boldsymbol\theta_0$ can be based on a grid search over the squared error function to ensure the numerical solution begins close to the global maximum.


## Sequential Least Squares

In some applications, the data is sampled and processed in real-time. Instead of running the estimator repeatedly with ever-increasing data size, it is useful to have an estimator that allows updating the estimate using the latest data samples only. It is possible to formulate the LSE in this manner. For LSE, we look for a relation between estimates $\hat{\boldsymbol\theta}\_{N-1}$ and $\hat{\boldsymbol\theta}_{N}$, representing the estimate with $N-1$ data points and $N$ data points, respectively. If the noise has zero mean with some known covariance, we can formulate an estimator that sequentially updates both the estimate and covariance.

We consider the WLSE  with weights $\mathbf{C}^{-1}$, which is
\begin{equation}
\hat{\boldsymbol\theta}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}.
\end{equation}
From the Gauss-Markov theorem, we can calculate the covariance for our estimate:
\begin{equation}
\mathbf{C}_{\hat{\boldsymbol\theta}}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}.
\end{equation}

The important condition to compute the estimate $\hat{\boldsymbol\theta}$ and its covariance is uncorrelated noise, which corresponds to a diagonal noise covariance matrix. Under this condition, the sequential LSE is
\begin{equation}
\hat{\boldsymbol\theta}\_{N}=\hat{\boldsymbol\theta}\_{N-1}+\mathbf{K}\_{N}\big(x[N]-\mathbf{h}^T[N]\hat{\boldsymbol\theta}\_{N-1}\big)
\end{equation}
where $\mathbf{h}^T[N]$ is the $N^\text{th}$ row of the observation matrix $\mathbf{H}$ when the corresponding data sample $x[N]$ is acquired. The term $x[N]-\mathbf{h}^T[N]\hat{\boldsymbol\theta}\_{N-1}$ is the innovation, which is the difference between the data sample $x[N]$ and the estimate we have for that data sample, which is $\mathbf{h}^T[N]\hat{\boldsymbol\theta}\_{N-1}$. Based on our estimated parameter $\hat{\boldsymbol\theta}\_{N-1}$ after the $N^\text{th}$ data sample, we come up with an estimate for the $N+1^\text{th}$ sample we acquire. The estimate is updated according to the innovation and a gain term $\mathbf{K}\_{N}$, which is calculated as
\begin{equation}
\mathbf{K}\_{N}=\frac{\mathbf{C}\_{\hat{\theta},N-1}\mathbf{h}[N]}{\sigma_{N}^2+\mathbf{h}^T[N]C_{\hat{\theta},N-1}\mathbf{h}[N]}
\end{equation}


Finally, the covariance matrix is updated as
\begin{equation}
\mathbf{C}\_{\hat{\theta},N}=(\mathbf{I}-\mathbf{K}\_N \mathbf{h}^T[N])\mathbf{C}_{\hat{\theta},N-1}.
\end{equation}
