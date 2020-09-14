+++
title = "Least Squares Estimation"

# date = {{ .Date }}
lastmod = 2020-08-27

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "2.1 Least Squares Estimation"
weight = 210


+++
## Introduction

This first module of the Estimation part concerns an intuitive approach to fitting a model to the data at hand. Consider the problem of setting up a budget for the energy expenditure of an electric car. We can estimate the car's energy consumption per kilometer using the data from our charging station, where we fully recharge the car at the end of the day, and the distance travelled before recharging.

<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/DXyKPf_ehvs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

The module starts by introducing the squared error term, which is the <i>cost function</i> that measures the goodness of fit between the model parameter and the data at hand. The least squares estimator is derived based on this cost function. In many applications the model has multiple parameters, which can be organized into vectors. Solving such problems requires extending the least squares estimation to vector parameters. There are also cases where the underlying model changes over time. Estimating the model parameters at a time instance requires putting more emphasis on the data points around that time instance while reducing the weight of the earlier and later data points. Weighted least squares estimation aims to solve such problems. This module stops short of non-linear least squares estimation problems, which are handled separately in another module concerning numerical solution methods.

## The Squared Error Term
As for all estimation methods covered in this course, the least squares estimator concerns data $x[n]$, which is assumed to be generated according to a model $s[n;\theta]$. The intuition behind the least squares estimator is to find the value of the controlling parameter $\theta$ that minimizes the difference between the data and the model output. The error term between the data and the model at each sample $n$ is
\begin{equation}
e[n;\theta] = x[n]-s[n;\theta].
\end{equation}
Just as the model $s[n;\theta]$ depends on the parameter $\theta$, so does the error term $e[n;\theta]$. By changing $\theta$, the error for any sample can be reduced to zero. However, the goal is to reduce the error term globally. In other words, the total error has to be minimized. For this reason, the cumulative error that is the sum of the error terms $e[n,\theta]$ over all samples $n\in\{0,...,N-1\}$ is considered. Since each error term $e[n,\theta]$ can be either positive or negative, they may cancel out in the cumulative error. For this reason, the squared error term is considered as the measure of fit between the model and the data. The <i> cost function</i> that describes the goodness of fit is
\begin{equation}
J(\theta) = \sum_{n=0}^{N-1}(x[n]-s[n;\theta])^2,
\end{equation}
which is a function of $\theta$.

<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/estimation/LS_Fig2.svg"
    />
	<img
      src="/../files/7.Images/statistical/estimation/LS_Fig3.svg"
    />
    <figcaption class="numbered">
      Visualization of the line fitted over the data and the error terms.
    </figcaption>
  </figure>
</div>

## The Least Squares Estimator
<i>The least squares estimate</i> $\hat\theta_{LS}$ is the value that minimizes the cost function $J(\theta)$, which is formally expressed as
\begin{equation}
\hat{\theta}_{LS}=\underset{\theta}{\mathrm{argmin}}J(\theta).
\end{equation}

The minimum (or maximum) of a function can be found by taking the derivative of the function and equating it to zero. Thus, to find $\hat\theta_{LS}$, the following equation has to be solved:
\begin{equation}
\frac{\partial J(\theta)}{\partial\theta}=0
\end{equation}
Taking the derivative yields
\begin{equation}
\sum_{n=0}^{N-1}2(x[n]-s[n;\theta])\frac{\partial s[n;\theta]}{\partial\theta}=0
\end{equation}
Solving the equation above yields the least squares estimate $\hat\theta_{LS}$.


## Least Squares Estimator for Vector Parameters

Estimation problems in general deal with models that are controlled by multiple parameters. Consider a line fitting example where the model is
\begin{equation}
s[n,\Theta]=An+B,
\end{equation} 
where the east squares estimation for both parameters $A$ and $B$ have to be found. In other words, $\Theta=[A B]^T$. This means there are two minimization problems to be solved:
\begin{equation}
\frac{\partial}{\partial A}\sum_{n=0}^{N-1}(x[n]-An-B)^2=0
\end{equation}
\begin{equation}
\frac{\partial}{\partial B}\sum_{n=0}^{N-1}(x[n]-An-B)^2=0
\end{equation}
Both minimization problems can be combined into a single expression that can be solved using linear algebra methods. The first step is to write the model in linear algebraic form:
\begin{equation}
s[n;\Theta]=\mathbf{H\Theta}
\end{equation}
where $\mathbf{H}$ is called <b>the observation matrix</b>. 

The cost function that is the sum of squared error terms becomes
\begin{equation}
J(\Theta)=(\mathbf{x}-\mathbf{H}\Theta)^T(\mathbf{x}-\mathbf{H}\Theta)
\end{equation}

The derivative operation in linear algebraic form is
\begin{equation}
\frac{\partial}{\partial\Theta}[(\mathbf{x}-\mathbf{H}\Theta)^T(\mathbf{x}-\mathbf{H}\Theta)]=-2\mathbf{H}^T\mathbf{x}+2\mathbf{H}^T\mathbf{H}\Theta=0
\end{equation}
The least squares estimation formulation is obtained as
\begin{equation}
\hat\Theta_{LS}=(\mathbf{H}^T\mathbf{H})^{-1}\mathbf{H}^T\mathbf{x}.
\end{equation}

### Weighted Least Squares Estimation

For some estimation problems, we might want to reduce the influence of a portion of the data on our final estimate. For example, consider again the problem of setting up a budget for the energy expenditure of an electric car. It is possible that the energy consumption per kilometer for driving in the city is different from driving a long distance on a highway. So, we may want to derive two separate estimations for the energy consumption to reflect on the difference. Weighted least squares estimation serves this purpose by introducing a weight $\gamma_n$ to the squared error term:
\begin{equation}
J(\Theta) = \sum_{n=0}^{N-1}\gamma_n(x[n]-s[n;\Theta])^2.
\end{equation}
The squared error term expression can be written in linear algebraic form:
\begin{equation}
J(\Theta)=(\mathbf{x}-\mathbf{H}\Theta)^T\Gamma(\mathbf{x}-\mathbf{H}\Theta)
\end{equation}
where $\Gamma$ is a diagonal matrix such that $\Gamma_{nn}=\gamma_n$ is the entry on the $n^{th}$ row and column.

The weighted least squares estimator is obtained by setting the derivative of the squared error term to zero, which yields
\begin{equation}
\hat\Theta_{LS}=(\mathbf{H}^T\Gamma\mathbf{H})^{-1}\mathbf{H}^T\Gamma\mathbf{x}.
\end{equation}

## Nonlinear Least Squares Estimation

Until now, we focused our attention on signal models that are a linear function of the controlling parameter $\theta$. We were able to derive a closed form expression for the LSE that operates on the data $\mathbf{x}$ with the observation mtrix $\mathbf{H}$. Not all problems can be cast into a linear LSE. In this section, we will investigate several ways of dealing with nonlinear LSE. Numerical solution methods are covered at the end of the Estimation Theory part of the course.

### Transforming a Nonlinear Problem to a Linear Problem

The first method of dealing with nonlinear problems can be described as finding our way back to the linear LS problem by applying an invertible transformation to the parameters to be estimated. If we can find a transformation
\begin{equation}
\alpha=f(\theta)
\end{equation}
such that
\begin{equation}
\mathbf{s}(theta)=\mathbf{s}(f^{-1}(\alpha))=\mathbf{H}\alpha
\end{equation}
then we can simply use the linear LS formulations we derived so far and find the parameter $\theta$ through the inverse transform.

<b>Example:</b>

---
The relation between the phase of a sinusoidal signal and the data samples from that signal is nonlinear:
\begin{equation}
s[n,\theta] = \sin(2\pi fn + \theta).
\end{equation}
It is possible to transform the signal such that the signal model is in a linear relation with a function of the phase term $\theta$. Consider the trigonometric identity:
\begin{equation}
\sin(A+B)=\sin(A)\cos(B)+\cos(A)\sin(B).
\end{equation}
Then the signal model can be rewritten as
\begin{equation}
s[n,\theta]=\sin(2\pi fn)\cos(\theta) + cos(2\pi fn)\sin(\theta).
\end{equation}
To implement least squares estimation, we substitute the phase $\theta$ with two other parameters, $\alpha_1=\cos(\theta)$ and $\alpha_2=\sin(\theta)$. The signal model in vector form becomes
\begin{equation}
\mathbf{s}(\theta) = \mathbf{s}(f^{-1}(\alpha))=\mathbf{H}\alpha
\end{equation}
where $\mathbf{H}=[\mathbf{S}~~\mathbf{C}]$ is the observation matrix consisting of two columns, 
\begin{equation}
\mathbf{S}=\big[0 ~ \sin(2\pi f) ~ \sin(2\pi 2f) ~ ... ~ \sin(2\pi Nf)\big]^T,
\end{equation}
\begin{equation}
\mathbf{C}=\big[1 ~ \cos(2\pi f) ~ \cos(2\pi 2f) ~ ... ~ \cos(2\pi Nf)\big]^T,
\end{equation}
and the parameter vector is $\alpha=[\alpha_1 ~~ \alpha_2]^T$

---

### Separating the Nonlinear and Linear Parts of a Problem

The second method of dealing with nonlinear problems consist of dividing the problem into linear and non-linear parts. The parameters to be estimated are dividen into two sets such that $\Theta=[\Theta_a~\Theta_b]^T$, where
\begin{equation}
\mathbf{s}(\Theta)=\mathbf{H}(\Theta_a)\Theta_b.
\end{equation}
In other words, we write the signal model such that some of the parameters to be estimated, $\Theta_a$, are left inside the observation matrix, which is in a linear relation with the remaining parameters $\Theta_b$. We can still use the linear LSE for estimating the parameters $\Theta_b$, after finding the parameters $\Theta_a$.


<b>Example:</b>

---
Consider a capacitor-resistor circuit where the capacitor is charged up to a voltage level $V_b$ and then left to discharge over the resistor. The measured voltage between the capacitor's contact points is given by
\begin{equation}
x[n]=V_b e^{-\frac{nT_s}{RC}},
\end{equation}
where $T_s$ is the sampling period, $R$ is the resistance value and $C$ is the capacitance value. To estimate the value of $RC$ and $V_b$ from a set of $N$ samples, we separate the problem into non-linear and linear parts:
\begin{equation}
\mathbf{x}=\mathbf{H}(RC)V_b,
\end{equation}  
where $\mathbf{H}(RC)=[h~ h^2~ ...~ h^N]^T$ is the observation matrix and
\begin{equation}
h=e^{-\frac{T_s}{RC}}.
\end{equation}
The solution to $V_b$ can be found by
\begin{equation}
\hat{V}_b=\big(\mathbf{H}^T(RC)\mathbf{H}(RC)\big)^{-1}\mathbf{H}^T(RC)\mathbf{x},
\end{equation}
if the value for RC can be found by another method.

---

### The Grid Search

The closed form solution to the LSE gives the parameter value that minimizes the squared error function. Another method to locate the minimum of the squared error function is to sample that function on possible values of the parameter $\theta$ and pick the one that leads to the smallest squared error value. For a parameter vector $\Theta$, each dimension has to be sampled in search for the minimum of the error function. We can imagine the sampling points constituting a grid in the two dimensional case, hence, the name <i>grid search</i>.

The grid search is computationally expensive, especially when the parameter vector $\Theta$ has more than a few dimensions. Eventually, the grid search corresponds to evaluating the squared error for each sample in the parameter space. Thus, we have to limit the number of samples by limiting the search range and keeping the sample granularity coarse.


## Conclusion

The least squares estimation is an intuitive estimation technique that measures the goodness of fit between the data and the signal model through the squared error term. It is applicable to a variety of problems and finds frequent use in linear regression. A caveat regarding the LSE is the possibility of over-fitting. It is possible to come up with a signal model with enough number of parameters to reduce the squared error to zero for a data set. Failure of such models become evident only when the squared error is calculated for a new data set. 

There is no criteria that tells how much residual error has to remain after a model is fitted. Such criteria requires more information on the noise, which is not considered in the LSE. We will see in the remaining modules the paradigm shift required to take the noise properties into consideration when designing estimators. LSE can be augmented with information on noise properties; we will revisit the LSE later to see an example of such augmentation.



