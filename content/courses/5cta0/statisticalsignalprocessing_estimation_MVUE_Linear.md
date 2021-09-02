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
name = "2.3 MVUE for Linear Models"
weight = 230

+++
## Introduction

The minimum variance unbiased estimator (MVUE) has the lowest variance among all unbiased estimators. In general, there is no method to find the MVUE; however, for a special class of estimation problems, we can find these estimators. This module concerns a special class of signal models for which a minimum variance unbiased estimator (MVUE) is available. This special class consists of estimation problems with linear signal models and additive Gaussian noise.

The module begins by introducing the linear signal model and derives the MVUE for colored Gaussian noise. Next, we assume white Gaussian noise, which can be considered a special case of colored noise. When the information on noise distribution is not complete, an interesting approach is to approximate the noise as Gaussian by considering only the expected value and variance for the noise. Such estimators are called best linear unbiased estimators (BLUE), covered at the end of the module.

<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/3I_6DN4M-R0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


## Linear Signal Model

A linear signal model is any model for which the signal s[n,θ] can be expressed as a linear combination of the weighted parameters, i.e.,
\begin{equation}
  s[n;\boldsymbol\theta] = \sum_{k=0}^{K-1} h_k[n]\theta_k.
\end{equation}
For multiple signal values, the model can be expressed as a matrix-vector product of the form
\begin{equation}
  \mathbf{s}(\boldsymbol\theta) = \mathbf{H}\boldsymbol\theta,
  \label{eq:ls_linear}
\end{equation}
where $\mathbf{s}(\boldsymbol\theta)$ is the signal vector of length $N$, $\mathbf{H}$ is the so-called <b>observation matrix</b> of size $N\times K$, and $\boldsymbol\theta$ is the parameter vector of length $K$.

---

<b>Example:</b>

Assume our signal model is a polynomial of degree $K-1$ with coefficients $\theta_0,\theta_1,\dots,\theta_{K-1}$, i.e.,
\begin{equation}
  s[n;\boldsymbol\theta] = \theta_{0}n^{0} + \theta_{1}n^{1}+ \dots + \theta_{K-1}n^{K-1},
\end{equation}
and suppose observations for $n=0,1,\dots,N-1$ are given. The corresponding observation matrix $\mathbf{H}$ is
\begin{equation}
  \mathbf{H} =
  \begin{bmatrix}
      1  & 0 & 0 &\cdots &0\newline
      1  & 1 & 1& & 1\newline
      1  & 2 & 2^2 & & 2^{K-1} \newline
      \vdots & & & \ddots\newline
      1 & N-1 & (N-1)^2 & \cdots & (N-1)^{K-1}
  \end{bmatrix}.
\end{equation}

---

## MVUE for Linear Models and Additive Gaussian Noise
To find the MVUE for linear signals in Gaussian noise, we will take advantage of the equality constraint of the CRLB. Therefore, we need to show that we can express the derivative of the log-likelihood function in the form
\begin{equation}
\frac{\partial}{\partial\boldsymbol\theta}l(\mathbf{x},\boldsymbol\theta) = \mathcal{I}(\boldsymbol\theta)(g(\mathbf{x})-\boldsymbol\theta),
\label{eq:equality}
\end{equation}
see module on the CRLB. To obtain the derivative of the log-likelihood function, we need first to determine the probability density function of the observations. For the linear signal model embedded in additive Gaussian noise, our observations are modeled as
\begin{equation}
 \mathbf{x} = \mathbf{H}\boldsymbol\theta  + \mathbf{w},
 \label{eq:linear_model}
\end{equation}
where $\mathbf{w}$ is zero mean noise with covariance matrix $\mathbf{C}$, i.e.,
$\mathbf{w} \sim \mathcal{N}(\mathbf{0},\mathbf{C})$. Thus, the PDF of the observation vector is
\begin{equation}
p(\mathbf{x},\boldsymbol\theta) = \frac{1}{|2\pi\mathbf{C}|^{\frac{1}{2}}}\exp\\left(-\frac{1}{2}(\mathbf{x-\mathbf{H}\boldsymbol\theta})^T\mathbf{C}^{-1}(\mathbf{x-\mathbf{H}\boldsymbol\theta})\\right).
\end{equation}

The corresponding log-likelihood function is
\begin{equation}
  l(\mathbf{x};\boldsymbol\theta) = -\frac{1}{2}\ln|2\pi \mathbf{C}|-\frac{1}{2}(\mathbf{x-\mathbf{H}\boldsymbol\theta})^T\mathbf{C}^{-1}(\mathbf{x-\mathbf{H}\boldsymbol\theta}),
\end{equation}
which after expanding the second term becomes
\begin{equation}
  l(\mathbf{x};\boldsymbol\theta)= -\frac{1}{2}\ln|2\pi \mathbf{C}|-\frac{1}{2}\\left(\mathbf{x}^T\mathbf{C}^{-1}\mathbf{x}-\mathbf{x}^T\mathbf{C}^{-1}\mathbf{H}\boldsymbol\theta -\boldsymbol\theta^T \mathbf{H}^T \mathbf{C}^{-1}\mathbf{x} + \boldsymbol\theta^T \mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}\boldsymbol\theta\\right).
\end{equation}

The gradient of the log-likelihood function is
\begin{equation}
\frac{\partial}{\partial\boldsymbol\theta}l(\mathbf{x};\boldsymbol\theta)=\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}-\mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}\boldsymbol\theta,
\label{eq:part_ll}
\end{equation}
and if $\mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}$ is invertible, we further have
\begin{equation}
\frac{\partial}{\partial\boldsymbol\theta}l(\mathbf{x};\boldsymbol\theta) =\mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}\\left(\\left(\mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}\\right)^{-1}\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}-\boldsymbol\theta\\right).
\label{eq:MLE_lin_col}
\end{equation}
By comparing \eqref{eq:MLE_lin_col} with \eqref{eq:equality}, we recognize the Fisher information matrix
\begin{equation}
\mathbf{I}(\boldsymbol\theta) = \mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}
\end{equation}
and the estimator
\begin{equation}
g(\mathbf{x})= \\left(\mathbf{H}^T \mathbf{C}^{-1}\mathbf{H}\\right)^{-1}\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}.
\end{equation}
We found an efficient estimator, and thus, an MVUE. In the module on the MLE, we also stated that if an efficient estimator exits, it is the MLE, which is easily verified by equating \eqref{eq:part_ll} with zero and solving for $\boldsymbol\theta$.

## MVUE for Linear Models in White Additive Gaussian Noise

So far, we have assumed that our noise is colored, i.e., that our noise sample are correlated. For the case of additive white Gaussian noise we can reuse the above result. Therefore, we assume that our individual noise samples are IID with zero mean and variance $\sigma^2$. In this case, the covariance matrix $\mathbf{C}$ is a diagonal matrix with elements $\sigma^2$ on the main diagonal, i.e.,
\begin{equation}
\mathbf{C} = \sigma^{2}\mathbf{I}
\label{eq:covariance}
\end{equation}
Substitung \eqref{eq:covariance} in \eqref{eq:MLE_lin_col} yields
\begin{equation}
\frac{\partial}{\partial\boldsymbol\theta}l(\mathbf{x};\boldsymbol\theta)=\frac{\mathbf{H}^T \mathbf{H}}{\sigma^2}\\left(\\left(\mathbf{H}^T\mathbf{H}\\right)^{-1}\mathbf{H}^T\mathbf{x}-\boldsymbol\theta\\right)
\end{equation}
where we recognize the estimator
\begin{equation}
g(\mathbf{x}) =(\mathbf{H}^T \mathbf{H}\boldsymbol)^{-1}\mathbf{H}^T\mathbf{x}
\end{equation}
and the Fisher information matrix
\begin{equation}
\mathbf{I}(\boldsymbol\theta)=\frac{\mathbf{H}^T \mathbf{H}}{\sigma^2}.
\end{equation}

---
<b>Example</b>

Assume we have a signal composed of $P$ sinusoidal signals embedded in white Gaussian noise with zero mean and variance $\sigma^2$, i.e.,
\begin{equation}
x[n] = \sum_{p=0}^{P-1} c_p \cos\\left(2\pi \frac{k_p}{N}n-\varphi_p\\right) + w[n],
\label{eq:signal_model_cos}
\end{equation}
where $c_p$ and $\varphi_p$
are the unknown amplitude and phase, respectively. The frequency parameters $k_0$ to $k_{(P-1)}$ are assumed to be known, different, and between $0$ and $N-1$. The signal is linear in the parameter $c_p$, but it is not linear in the unknown phase $\varphi_p$. However, we can use the trigonometric relations
\begin{equation}
\cos(\alpha)\cos(\beta) = \frac{1}{2}\\left(\cos(\alpha-\beta)+\cos(\alpha+\beta)\\right)
\end{equation}
and
\begin{equation}
\sin(\alpha)\sin(\beta) = \frac{1}{2}\\left(\cos(\alpha-\beta)-\cos(\alpha+\beta)\\right)
\end{equation}
to express \eqref{eq:signal_model_cos} as
\begin{equation}
x[n] = \sum_{p=0}^{P-1} \underbrace{c_p\cos(\varphi)}_{a_p} \cos\\left(2\pi \frac{k_p}{N}n\\right)+ \underbrace{c_p\sin(\varphi)}\_{b_p} \sin\\left(2\pi \frac{k_p}{N}n\\right) + w[n].
\label{eq:signal_model_cos_sin}
\end{equation}
The transformed model is now linear in the unknown parameters $a_p$ and $b_p$. Due to the invariance of the MLE, we can find the maximum likelihood estimate for the amplitudes $a_p$ and $b_p$ and obtain the maximum likelihood estimate for $c_p$ and $\varphi$ by using relations
\begin{equation}
  c_p = \sqrt{a_p^2+b_p^2}
\end{equation}
and
\begin{equation}
  \varphi_p = \arctan2(b_p,a_p).
\end{equation}
The signal model in \eqref{eq:signal_model_cos_sin} for multiple observation can be expressed as
\begin{equation}
\mathbf{x} = \mathbf{H}\boldsymbol\theta + \mathbf{w}.
\end{equation}
The observation matrix $\mathbf{H}$ is
\begin{equation}
  \mathbf{H} = \begin{bmatrix}
  \mathbf{c}\_{k_0} & \dots &\mathbf{c}\_{k_{(P-1)}} & \mathbf{s}\_{k_0} & \dots &\mathbf{s}\_{k_{(P-1)}}
  \end{bmatrix}
\end{equation}
with columns
\begin{equation}
\mathbf{c}\_{k_p} = \begin{bmatrix}
 \cos\\left(2\pi\frac{k_p}{N}0\\right) &
\cos\\left(2\pi\frac{k_p}{N}1\\right) &
\dots &
\cos\\left(2\pi\frac{k_p}{N}(N-1)\\right)
\end{bmatrix}^{T}
\end{equation}
and
\begin{equation}
\mathbf{s}\_{k_p} = \begin{bmatrix}
 \sin\\left(2\pi\frac{k_p}{N}0\\right) &
\sin\\left(2\pi\frac{k_p}{N}1\\right) &
\dots &
\sin\\left(2\pi\frac{k_p}{N}(N-1)\\right)
\end{bmatrix}^{T},
\end{equation}
respectively. The parameter vector $\theta$ for this model is
\begin{equation}
\boldsymbol\theta = \begin{bmatrix}a_0 & \dots &a_{(P-1)}& b_0 \dots b_{(P-1)}\end{bmatrix}
\end{equation}


Note that the frequencies $k_p$ are multiple of the fundamental frequency $1/N$, and thus, the columns of the observation matrix are orthogonal. The matrix $\mathbf{H}^T\mathbf{H}$ is
\begin{equation}
\mathbf{H}^T\mathbf{H} = \frac{N}{2}\mathbf{I},
\end{equation}
i.e., a diagonal matrix with entries $N/2$ on the main diagonal. The maximum likelihood estimate is
\begin{equation}
\hat{\boldsymbol\theta}\_{\text{ML}} =\\left(\mathbf{H}^T\mathbf{H}\\right)^{-1}\mathbf{H}\mathbf{x} = \begin{bmatrix}
\frac{2}{N}\mathbf{c}\_{k_0}^{T} \\\\\\\ \vdots \\\\\\ \frac{2}{N} \mathbf{c}\_{k_{(P-1)}}^{T} \\\\\\ \frac{2}{N}\mathbf{s}\_{k_0}^{T} \\\\\\\\ \vdots \\\\\\ \frac{2}{N}\mathbf{s}\_{k_{(P-1)}}^{T}
\end{bmatrix}\mathbf{x}
\end{equation}
The estimate of the parameter $a_p$ and $a_b$ are
\begin{equation}
\hat{a}\_p = \frac{2}{N} \sum_{n=0}^{N-1} x[n] \cos\\left(2\pi\frac{k_p}{N}n\\right)
\label{eq:cos}
\end{equation}
and
\begin{equation}
\hat{b}\_p = \frac{2}{N} \sum_{n=0}^{N-1} x[n] \sin\\left(2\pi\frac{k_p}{N}n\\right)
\label{eq:sin}
\end{equation}
Suppose that the frequency $k_p$ takes all values of from 0 to $N-1$, then \eqref{eq:cos} and \eqref{eq:sin} are the discrete Fourier transform for real signals.

---


## Best Linear Unbiased Estimator (BLUE)

So far, we have derived the MVUE for linear signal models with AWGN. In many applications, it is not possible to find an MVUE estimator using techniques presented up to this point. A popular choice is to restrict the estimator to be linear in the observation $\mathbf{x}$, i.e., of the form
\begin{equation}
\hat{\boldsymbol\theta} =\mathbf{Ax}.
\end{equation}
Here, we assume that $N$ observations are available and that we seek to estimate $K$ unknown parameter with $N>P$. Thus, $\mathbf{A}$ is of size $K\times N$. Depending on the choice of the $\mathbf{A}$'s coefficients, different estimators can be obtained. Among all linear estimators, we seek an estimator that is unbiased and has minimum variance. The estimator which fulfills these properties is called the <b>best linear unbiased estimator (BLUE)</b>. The BLUE, as we will see, is also applicable, if limited knowledge about the PDF of the observation is available.

To find the BLUE, we have to start from the assumptions at hand; that the estimator has zero bias and minimum variance. The zero bias condition is formulated as
\begin{equation}
\mathbb{E}\\left[\hat{\boldsymbol\theta}\\right]=\mathbb{E}\left[\mathbf{A}\mathbf{x}\\right]=\mathbf{A}\mathbb{E}[\mathbf{x}]=\boldsymbol\theta,
\label{eq:constraint}
\end{equation}
where $\mathbf{A}$ is the $K\times N$ matrix that consists of the coefficients $a_{k,n}$. The constraint of unbiasedness requires a linear relation between the parameter vector $\boldsymbol\theta$ and the expected value of the data such that
\begin{equation}
\mathbb{E}[\mathbf{x}]=\mathbf{H}\boldsymbol\theta.
\label{eq:linear}
\end{equation}
Substituting \eqref{eq:linear} in \eqref{eq:constraint} yields
\begin{equation}
  \mathbb{E}\\left[\hat{\boldsymbol\theta}\\right] = \mathbf{AH}\boldsymbol\theta.
\end{equation}

Thus, for the linear estimator to be unbiased, we require that
\begin{equation}
\mathbf{A}\mathbf{H}=\mathbf{I},
\end{equation}
where $\mathbf{I}$ is the $K\times K$ identity matrix.

The variance of the $k$th estimate $\hat\theta_k$ is
\begin{equation}
\mathrm{Var}\\left[\hat\theta_k\\right]=\mathbb{E}
\\left[(\mathbf{a}_k^T\mathbf{x}-\mathbb{E}[\mathbf{a}_k^T\mathbf{x}])^2\\right]
\end{equation}
where $\mathbf{a}_k^T$ is the $k$th row of $\mathbf{A}$. This can be equivalently expressed as
\begin{align}
\mathrm{Var}\\left[\hat\theta_k\\right]&=\mathbb{E}\\left[\\left(\mathbf{a}_k^T(\mathbf{x}-\mathbb{E}[\mathbf{x}])\\right)^2\\right]\\\\\\
&=\mathbb{E}\\left[(\mathbf{a}_k^T(\mathbf{x}-\mathbb{E}[\mathbf{x}])(\mathbf{x}-\mathbb{E}[\mathbf{x}])^T\mathbf{a}_k\\right]\\\\\\
&=\mathbf{a}_k^T\mathbf{C}\mathbf{a}_k.
\end{align}
Here, $\mathbf{C}$ is the covariance matrix for the data, which is equivalent to the covariance matrix for the zero-mean noise due to the linear signal model.

The BLUE is found by minimizing the variance for all estimates with the constraint $\mathbf{AH}=\mathbf{I}$. Thus, the optimization problem is
\begin{equation}
\min_{\mathbf{a}_k^T} \mathbf{a}_k^T\mathbf{C}\mathbf{a}_k, \quad \text{s.t. }  \mathbf{a}_k^T \mathbf{h}_l=\delta\_{k,l},
\end{equation}
where $\mathbf{h}_l$ is the $l$th column of $\mathbf{H}$. The minimum can be found using Lagrange multipliers, which results in
\begin{equation}
\hat{\boldsymbol\theta}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}\mathbf{H}^T\mathbf{C}^{-1}\mathbf{x}.
\end{equation}
The covariance matrix for the estimate $\hat{\boldsymbol\theta}$ is
\begin{equation}
\\mathbf{C}_{\hat{\boldsymbol\theta}}=(\mathbf{H}^T\mathbf{C}^{-1}\mathbf{H})^{-1}.
\end{equation}

Note that the BLUE is the MVUE for the linear model in \eqref{eq:linear_model}. This follows directly from the unbiased constraint
\begin{equation}
 \mathbb{E}[\mathbf{x}] = \mathbb{E}[\mathbf{H}\boldsymbol\theta  + \mathbf{w}] = \mathbf{H}\boldsymbol\theta.
\end{equation}
