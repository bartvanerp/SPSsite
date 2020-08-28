+++
title = "Auto-regressive moving-average models "         # name of webpage

# date = {{ .Date }}
lastmod = 2020-07-15

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.

[menu.statistical]                       # name of menu section (main module)
  name = "ARMA models"        # name of this item in that menu
  weight = 3                           # location in that menu
  parent = "Rational signal models"

+++
A stochastic process may be represented by a stochastic model with given order and parameters, which is able to generate a random signal characterized by well-defined spectral properties. In fact, although a stochastic model and process are in principle two different entities, they are sometimes used interchangeably.
Stochastic models are fundamental in many applied fields of science, including engineering, economics and medicine. Among stochastic models, a special class of models known as auto-regressive moving-average (ARMA) is widely used. In the section
<a href="../statisticalsignalprocessing_rational_spectral_factorization">Spectral factorization</a> we saw how any  wide-sense stationary random signal can be described as an LTI system driven by white noise. The system, also referred to as innovation filter, has a rational spectrum. It turns out that this is equivalent to modeling the random process generating the signal as an ARMA($p$, $q$) model, which provide a parsimonious description of a WSS stochastic process in terms of a rational polynomial. The numerator of order $q$ represents the moving-average part, while the denominator of order $p$ represents the auto-regressive part.

The ARMA model is based on the observation that stochastic time series often have a dependence on previous time points. This can be described by the auto-regressive part of an ARMA model, which permits modeling a "memory" that decades with time. The moving- average part takes into account the new information (innovation) by a linear combination of the present and previous samples.

Thanks to their ability to model a wide variety of stochastic processes, ARMA models are useful for:
<ul>
<li> understanding the nature of a stochastic process by detecting the mechanism that builds memory into the signal;</li>
<li> forecasting future values of a signal based on the past values;</li>
<li> removing from the signal the imprint of some known process, so as to
get a more random residual signal to be further analyzed and interpreted (pre-whitening);</li>
<li> finding a spectral estimate from a random signal. More on this in the section <a href="../statisticalsignalprocessing_spectrum_parametric">Parametric spectral estimation</a>. </li>
</ul>  

## Auto-regressive model, AR($p$)
An auto-regressive process is a special type of ARMA model for which $q= 0$.
The AR model is therefore an all-pole filter with the following transfer function
\begin{equation}
\begin{split}
    H(z) = \frac{1}{1+\sum_{p=1}^{P} a_p z^{-p}} = \frac{1}{A(z)}.
\end{split}
\end{equation}

The input to this system is white noise, thus an AR random process can be described by the following difference equation
\begin{equation}
    x[n] = i[n] - a_1 x[n-1] - a_2 x[n-2] - \ldots - a_p x[n-p].
\end{equation}

where $i[n]$ is the input white noise and $a_i$ are the filter coefficients. The order of the filter gives an indication on how many previous signal samples are used to form a new output.

<h3>Example</h3>
One of the first stochastic models was a AR model proposed by Yule in 1927 to describe the motion of a pendulum in a viscous medium. Yule expressed the amplitude $s[n]$ of the oscillation using the following homogeneous difference equation
\begin{equation}
\begin{split}
    s[n] + a_1 s[n-1] + a_2 s[n-2] = 0, \qquad n=0, 1, 2, ...
\end{split}
\end{equation}
However, the measured values of $s[n]$ are affected by noise. Therefore, Yule proposed to use noise as an external driving force determining the pendulum's behavior, resulting in
\begin{equation}
\begin{split}
    s[n] + a_1 s[n-1] + a_2 s[n-2] = i[n], \qquad n=0, 1, 2, ...,\newline
    s[n] = i[n] - a_1 s[n-1] - a_2 s[n-2], \qquad n=0, 1, 2, ...
\end{split}
\end{equation}
which is a 2$^{nd}$ order AR model.

### Autocorrelation of a AR($p$) process

The auto-correlation function of an AR process can be determined by the definition of the auto-correlation function
\begin{equation}
    r_x[l] = \mathrm{E}\left\\{x[n]x^\ast[n-l]\right\\},
\end{equation}
where we will make use of two properties. First the auto-correlation function of the independent white Gaussian input noise is defined as
\begin{equation}
    r_i[l] = \mathrm{E}\left\\{i[n]i^\ast[n-l]\right\\} = \sigma^2_i\delta[l]
\end{equation}
and secondly we use the fact that the signal is real, meaning that $x[n] = x^\ast[n]$. Before the auto-correlation function of $x[n]$ can be calculated, first the cross-correlation function between the white Gaussian noise input $i[n]$ and the AR-process $x[n]$ has to be determined as
\begin{equation}
    \begin{split}
        r_{ix}[l]
        &= \mathrm{E}\left\\{i[n]x^\ast[n-l]\right\\}, \newline
        &= \mathrm{E}\left\\{i[n]^\ast\left(i[n-l] - a_1 x^\ast[n-1-l]  - \ldots - a_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \mathrm{E}\left\\{i[n]i^\ast[n-l]\right\\} + \mathrm{E}\left\\{i[n]\left(- a_1 x^\ast[n-1-l] - \ldots - a_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \sigma_i^2\delta[l] -a_1\mathrm{E}\left\\{i[n] x^\ast[n-1-l]\right\\} - \ldots - a_p\mathrm{E}\left\\{i[n]x^\ast[n-p-l]\right\\}, \newline
        &= \sigma_i^2\delta[l]
    \end{split}
\end{equation}
where the simplification in the last line requires further clarification. Because the noise is independently distributed, only the expected value of two identically lagged signals $i[n]$ is non-zero. In the latter terms in the equation, the lagged signals $x[n-1-l],\ldots ,x[n-p-l]$ only depend on lagged values of the noise $i[n-1-l],\ldots ,i[n-p-l]$, which means that this always returns zero, because the white Gaussian noise signals are not calculated at the same lag.

Calculation of the auto-correlation function of the output $x[n]$ now gives
\begin{equation}
    \begin{split}
        r_x[l]
        &= \mathrm{E}\left\\{x[n]x^\ast[n-l]\right\\}, \newline
        &= \mathrm{E}\left\\{x[n]\left(i^\ast[n-l] - a_1 x^\ast[n-1-l] - \ldots - a_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \mathrm{E}\left\\{x[n]i^\ast[n-l]\right\\} - a_1 \mathrm{E}\left\\{x[n]x^\ast[n-1-l]\right\\} - \ldots - a_p \mathrm{E}\left\\{x[n]x^\ast[n-p-l]\right\\}, \newline
        &= r_{i,x}[l] - a_1 r_{x}[l-1] - \ldots - a_p r_{x}[l-p], \newline
        &= \sigma_i^2\delta[l] - a_1 r_{x}[l-1] - \ldots - a_p r_{x}[l-p],
    \end{split}
\end{equation}
which can rewritten as
\begin{equation}
    \sigma_i^2\delta[l] = \sum_{k=0}^p a_k r_x[l-k],
\end{equation}
where the newly introduced coefficient $a_0$ equals 1.

It is now possible to estimate the desired AR coefficients. When a windowed signal is observed and the auto-correlation function is estimated as $\hat{r}_x[l]$ the following relationship needs to be solved
\begin{equation}
     \hat{r}_x[l] + \hat{a}_1 \hat{r}_x[l-1] + \ldots + \hat{a}_p \hat{r}_x[l-p] = \hat{\sigma}_i^2\delta[l].
\end{equation}
In the equation above, we assume to know the correlation samples $  \hat{r}_x[l], ...,\hat{r}_x[l-p]$ (estimated from the observed signal), while the parameters $\hat{a}_1$,..., $\hat{a}_p$ and $\hat{\sigma}_i^2$ need to be estimated. This equality has $p+1$ unknowns, and thus we require $p+1$ equations to solve it. These $p+1$ equations can be obtained by evaluating the auto-correlation for different lags. The system of equations that follows from this approach is called the *Yule-Walker equations*, which can be written in matrix notation as
\begin{equation}
    \begin{bmatrix}
        \hat{r}_x[0]    & \hat{r}_x[1]      & \hat{r}_x[2]  & \cdots    & \hat{r}_x[p]      \newline
        \hat{r}_x[1]    & \hat{r}_x[0]      & \hat{r}_x[1]  & \cdots    & \hat{r}_x[p-1]    \newline
        \hat{r}_x[2]    & \hat{r}_x[1]      & \hat{r}_x[0]  & \cdots    & \hat{r}_x[p-2]    \newline
        \vdots          & \vdots            & \vdots        & \ddots    & \vdots            \newline
        \hat{r}_x[p]    & \hat{r}_x[p-1]    & \hat{r}_x[p-2]& \vdots    & \hat{r}_x[0]
    \end{bmatrix}
    \begin{bmatrix}
        1               \newline \hat{a}_1   \newline \hat{a}_2     \newline \vdots   \newline \hat{a}_p
    \end{bmatrix}
    =
    \begin{bmatrix}
        \hat{\sigma}_i^2      \newline 0                \newline 0            \newline \vdots    \newline 0
    \end{bmatrix}
\end{equation}

where the signal $x[n]$ is real, leading to a symmetric auto-correlation function which is shown as $\hat{r}_x[l] = \hat{r}_x[-l]$. Solving this system of equations, the unknown filter coefficient $\hat{a}_1, ..., \hat{a}_p$, and unknown variance of the input noise in the model,  $\hat{\sigma}_i^2$, can be estimated by least-square linear estimation.

<div class="example">
<h3> Example: AR(1) process </h3>
The output of an AR(1) process is given by the following difference equation
\begin{equation*}
    x[n] = i[n] - a_1 x[n-1].
\end{equation*}
Find the auto-correlation function.
<button class="collapsible">Show solution</button>
<div class="content">
The corresponding auto-correlation function can be found as
\begin{equation*}
    \begin{split}
        r_x[l]
        &= \mathrm{E}\left\{x[n]x^\ast[n-l]\right\}, \newline
        &= \mathrm{E}\left\{x[n]\left(i[n-l] - a_1 x[n-1-l]\right)\right\}, \newline
        &= \mathrm{E}\left\{ x[n]i[n-l]\right\} - a_1\mathrm{E}\left\{x[n]x[n-1-l]\right\}, \newline
        &= \sigma_i^2 \delta[l] - a_1 r_x[l+1].
    \end{split}
\end{equation*}
Evaluating the equation for the lags $0$ and $1$ gives
\begin{equation*}
    r_x[0] = \sigma_i^2 - a_1 r_x[1]
\end{equation*}
and
\begin{equation*}
    r_x[1] = r_x[-1] = -a_1 r_x[0]
\end{equation*}
respectively, where the auto-correlation function is assumed to be symmetric. From these two equations, we can determine the unknown filter coefficient and the noise variance. This approach will show how the unknown auto-correlation function can be determined. By combining the equations by the substitution of $r_x[1]$ of the second equation into the first gives
\begin{equation*}
    r_x[0] = \sigma_i^2 - a_1(-a_1r_x[0]),
\end{equation*}
from which, rearranging the terms, the value of $r_x[0]$ can be determined as
\begin{equation*}
    r_x[0] = \frac{\sigma_i^2}{1-a_i^2}
\end{equation*}
and from this $r_x[1]$ can be determined as
\begin{equation*}
    r_x[1] = -a_1 \frac{\sigma_i^2}{1-a_i^2}.
\end{equation*}
This recursion can be extended to all lags, leading to the final description of the auto-correlation function as
\begin{equation*}
    r_x[l] = \frac{\sigma_i^2}{1-a_1^2}(-a_1)^{|l|}
\end{equation*}

Similarly the Yuke-Walker equations can be determined as
\begin{equation*}
    \begin{bmatrix}
        r_x[0]  & r_x[l] \newline
        r_x[1]  & r_x[0]
    \end{bmatrix}
    \begin{bmatrix}
        1 \newline a_1
    \end{bmatrix}
    =
    \begin{bmatrix}
        \sigma_i^2 \newline 0
    \end{bmatrix},
\end{equation*}
which is similar to the system of equations determined above.
</div>
</div>

It can be observed that the auto-correlation function of the AR process is recursive. This is caused by the fact that a noise signal that enters the filter will appear at the output and will in this way always be somehow involved in the filter. Because the filter also processes previous outputs, every noise input signal will always be present in this feedback loop.

### Power spectral density of an AR($p$) process
Suppose that we have succeeded in determining the most optimal parameters for the AR process and we want to find the power spectral density estimate of our signal. Filtering an input signal with a filter with transfer function $H(e^{j\theta})$ relates the input and output power spectral densities ($P_I(e^{j\theta})$ and $P_X(e^{j\theta})$, respectively) through
\begin{equation}\label{eq:psd_inout}
    P_X(e^{j\theta}) = |H(e^{j\theta})|^2 P_I(e^{j\theta}) = H(e^{j\theta})H^\ast(e^{j\theta}) P_I(e^{j\theta}).
\end{equation}
Note that the transfer function depends on the filter coefficients. This relationship can be determined by calculating the transfer function of the filter. The transfer function $H(e^{j\theta})$ of the filter can be determined by taking the Fourier transform of the equation as
\begin{equation}
    X(e^{j\theta}) = I(e^{j\theta}) - a_1X(e^{j\theta})e^{-j\theta}  - a_2 X(e^{j\theta})e^{-j2\theta} - \ldots - a_p X(e^{j\theta})e^{-jp\theta},
\end{equation}
where $X(e^{j\theta})$ and $I(e^{j\theta})$ are the Fourier transforms of the desired signal and the white Gaussian process respectively. The terms can be separated as
\begin{equation}
    I(e^{j\theta}) = X(e^{j\theta}) (1+a_1 e^{-j\theta}  + a_2 e^{-j2\theta} + \ldots + a_p e^{-jp\theta}).
\end{equation}
From this the transfer function of the system can be determined by the fraction of the output spectrum over the input spectrum as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = \frac{1}{1+a_1 e^{-j\theta}  + a_2 e^{-j2\theta} + \ldots + a_p e^{-jp\theta}}.
\end{equation}
If we combine the result of this derivation with the fact that the power spectral density of a white Gaussian processes with variance $\sigma_i^2$ is given as $P_I(e^{j\theta}) = \sigma_i^2$, we finally obtain using (\ref{eq:psd_inout}) that
\begin{equation}\label{eq:psd_AR}
    P_X(e^{j\theta}) =  \frac{\sigma_i^2}{|1+a_1 e^{-j\theta}  + a_2 e^{-j2\theta} + \ldots + a_p e^{-jp\theta}|^2}
\end{equation}

## Moving-average model, MA($q$)
A moving-average process is a special type of ARMA model for which $p= 0$.
The MA model is therefore an all-zero filter, with the following transfer function
\begin{equation}
\begin{split}
    H(z) = 1+\sum_{q=1}^{Q} b_q z^{-q} = B(z).
\end{split}
\end{equation}

The name moving average can be somewhat misleading. In fact, to actually perform a moving average the coefficient of the filters should be all positive and sum up to unity. However, none of these conditions are valid for a general MA model.

The difference equation of a $q^\text{th}$-order MA filter is given by
\begin{equation}
    x[n] = i[n] + b_1 i[n-1] + b_2 i[n-2] - \ldots - b_q i[n-q].
\end{equation}
where $i[n]$ is the input white noise and $b_i$ are the filter coefficients. The filter order determines how many noise samples are combined to form a new sample.

### Autocorrelation of a MA($q$) process
While the auto-correlation of the AR process is recursive, this is not the case for MA processes. Each sample of the input noise will only be memorized during the time that is present in the filter, determined by the filter length. Therefore, after a certain time, a noise sample will not be present anymore in the output signal. This also leads to the fact that the auto-correlation function will only be non-zero for a certain number of lags, which is a function of the filter length. There is no correlation for lags exceeding the length of the filter. In order to demonstrate this behavior, the auto-correlation function is calculated for several lags.

At $l=0$ it can be found that
\begin{equation}
    \begin{split}
        r_x[0]
        &= \mathrm{E}\left\\{(i[n] + b_1i[n-1] + b_2i[n-2] + \ldots + b_qi[n-q])^2\right\\}, \newline
        &= \mathrm{E}\left\\{i^2[n]\right\\} + \mathrm{E}\left\\{b_1^2 i^2[n-1]\right\\} + \mathrm{E}\left\\{b_2^2 i^2[n-2]\right\\} + \ldots + \mathrm{E}\left\\{b_q^2 i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (1 + b_1^2 + b_2^2 + \ldots + b_q^2) = \sigma_i^2 \sum_{k=0}^{q}b_k^2,
    \end{split}
\end{equation}
where the terms including the noise signal that were not identically lagged were not shown, because these are zero. Furthermore, the coefficient $b_0$ is defined as 1. Similarly at $l=1$ the auto-correlation function can be determined as
\begin{equation}
    \begin{split}
        r_x[1]
        &= \mathrm{E}\big\\{(i[n] + b_1i[n-1]  + \ldots + b_qi[n-q]) \newline
        &\qquad\qquad \cdot(i[n-1] + b_1i[n-2]  + \ldots + b_qi[n-q-1])\big\\}, \newline
        &= b_1\mathrm{E}\left\\{i^2[n-1]\right\\} + b_1b_2\mathrm{E}\left\\{ i^2[n-2]\right\\} + b_2b_3\mathrm{E}\left\\{i^2[n-3]\right\\} \newline
        &\qquad\qquad + \ldots + b_{q-1}b_{q}\mathrm{E}\left\\{ i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (b_1 + b_1b_2 + b_2b_3 + \ldots + b_{q-1}b_q) = \sigma_i^2 \sum\_{k=1}^{q}b_kb_{k-1},
    \end{split}
\end{equation}
Please note how the lag has affected the above terms. Furthermore, the number of terms has decreased. The auto-correlation for $l=2$ can be determined as
\begin{equation}
    \begin{split}
        r_x[2]
        &= \mathrm{E}\big\\{(i[n] + b_1i[n-1]  + \ldots + b_qi[n-q]) \newline
        &\qquad\qquad \cdot(i[n-2] + b_1i[n-3]  + \ldots + b_qi[n-q-2])\big\\}, \newline
        &= b_2\mathrm{E}\left\\{i^2[n-2]\right\\} + b_1b_3\mathrm{E}\left\\{ i^2[n-3]\right\\} + b_2b_4\mathrm{E}\left\\{i^2[n-4]\right\\} \newline
        &\qquad\qquad + \ldots + b_{q-2}b_{q}\mathrm{E}\left\\{ i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (b_2 + b_1b_3 + b_2b_4 + \ldots + b_{q-2}b_q) = \sigma_i^2 \sum\_{k=2}^{q}b_kb_{k-2}.
    \end{split}
\end{equation}

This methodology can be extended for multiple lags, but a pattern should become noticeable, revealing the mathematical structure of the auto-correlation function. The mathematical description of the auto-correlation function can therefore be described as
\begin{equation}\label{eq:MAac}
    r_x[l] =
    \begin{cases}
        \sigma_i^2 \sum\_{k=|l|}^q b_{k}b_{k-|l|},       & \text{for } 0\leq |l|  \leq q \newline
        0.                                                  & \text{otherwise}
    \end{cases}
\end{equation}

While the auto-correlation function for an AR process results in a set of linear equations which can be easily solved by a matrix  inversion, this is not the case for the MA process, as can be observed from equation (\ref{eq:MAac}).

### Power spectral density of an MA($q$) process

From the definition of the difference equation, the Fourier equivalent can be determined as
\begin{equation}
    X(e^{j\theta}) = I(e^{j\theta}) + b_1 I(e^{j\theta}) e^{-j\theta} + \ldots + b_q I(e^{j\theta})e^{-jq\theta},
\end{equation}
from which the transfer function can be determined as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = 1 + b_1 e^{-j\theta} + \ldots + b_q e^{-jq\theta}.
\end{equation}
Using a similar approach as in the derivation of the AR($p$) power spectral density, we can find that the power spectral density of an MA($q$) process is given as
\begin{equation}\label{eq:psd_MA}
    P_x(e^{j\theta}) = P_I(e^{j\theta})H(e^{j\theta})H^\ast(e^{j\theta}) = \sigma_i^2 |1 + b_1 e^{-j\theta} + \ldots + b_q e^{-jq\theta}|^2.
\end{equation}

## Auto-regressive moving-average model, ARMA($p,q$)
The  general ARMA model is a mixture of a AR($p$) and a MA($q$) models, and therefore has both poles and zeros. The resulting transfer function is given by
\begin{equation}
\begin{split}
    H(z) = \frac{1+\sum_{q=1}^{Q} b_q z^{-q}}{1+\sum_{p=1}^{P} a_p z^{-p}} = \frac{B(z)}{A(z)}.
\end{split}
\end{equation}

The input to this system is white noise, thus an ARMA random process can be described by the following difference equation
\begin{equation}
\begin{split}
    x[n] = i[n] + b_1 i[n-1] + b_2 i[n-2] + \ldots + b_q i[n-q]&\newline
    - a_1 x[n-1] - a_2 x[n-2] - \ldots - a_p x[n-p]&.
    \end{split}
\end{equation}
where $i[n]$ is the input white noise, $a_i$ are the filter coefficients for the AR part, and $b_i$ are the filter coefficients for the MA part.

<div class="example">
<h3>Example: ARMA(1,1) process</h3>
Suppose you have been hired by Signify to manage lightbulb production. You are asked to estimate each month how many light bulbs to produce next month. Last month the estimation was $l[m-1] = 2500$ and the number of lightbulbs left in stock were $\epsilon[m-1] = 310$. Modeling the production as an ARMA(1,1), and knowing that you  would like to produce 10% more of the needed lightbulbs to avoid running out of stock, provide an estimate $\hat{l}[m]$ of the lightbulb to be produced for this month.
<button class="collapsible">Show solution</button>
<div class="content">
The lightbulb production can be modeled use the following ARMA(1,1) process
\begin{equation*}
        l[m] =  \underbrace{a_0+ a_1 l[m-1]}_{\text{AR}(1)} + \underbrace{b_1 \epsilon[m-1] + \epsilon[m]}_{\text{MA}(1)}.
\end{equation*}
In this model, the AR(1) part is a function of the previous month, while the MA(1) incorporates the error to make a new prediction. For both parts, we only look at data from this month and last month's production because we chose order $p=1$ and $q=1$.

Since the error for this month cannot be known in advance, we can estimate the number of lightbulb needed this month as
\begin{equation*}
        \hat{l}[m] =  a_0 + a_1 l[m-1] + b_1 \epsilon[m-1].
\end{equation*}
To estimate the parameters $a_0, a_1, b_1$, we can use information we have from previous month, and the fact that we want to produce 10% more of the needed light bulb. With this information in mind, we can write
\begin{equation*}
        a_0 + a_1 l[m-1] + b_1 \epsilon[m-1] = 1.1(l[m-1] - \epsilon[m-1]).
\end{equation*}
Although the solution is not unique, equating the coefficients on the left and right  hand sides of the above equation leads to $a_0=0$, $a_1 = 1.1$, and  $b_1 = - 1.1$, from which we obtain
\begin{equation*}
        \hat{l}[m] = 1.1 \cdot 2500 - 1.1\cdot 310 = 2409.
\end{equation*}
</div>

### The auto-correlation function of an ARMA($p,q$) process

As we have seen so far, the ARMA process is a combination of a AR and MA process. This also becomes apparent in the auto-correlation function. The derivation is lengthy and will not be shown, but an intuitive description is given.
The general form of the Yule-walker equations can be used to express the relationship between the parameters of the transfer function and the auto-correlation function of an ARMA($p,q$) process

\begin{equation}
    r_x[l] =
    \begin{cases}
        \sigma_i^2 \sum_{k=|l|}^q b_{k}b_{k-|l|} - \sum_{k=1}^p a_k r_x[|l|-k],  &\text{for }0 \leq |l| \leq q \newline
        - \sum_{k=1}^p a_k r_x[|l|-k].  &\text{for }|l| > q \\
    \end{cases}
\end{equation}

This expression may seem complicated, but it is easily explained by comparison with the auto-correlation function of the AR and MA process. The value of the auto-correlation function is a combination of both AR and MA auto-correlation functions. As with the AR process, the auto-correlation function has a recursive structure as can be seen from the terms with the $a_i$ coefficients. For smaller lags, there is not only an effect of an AR process, but there is also the effect of the MA process. In other words, the ARMA process and its auto-correlation function can be interpreted as the super-imposition of the AR and MA processes. For lags larger than $q$, the MA part does not contribute anymore to the autocorrelation function and thus only the AR part is present.

### Power spectral density of an ARMA($p,q$) process
From the definition of the difference equation the Fourier equivalent can be determined as

\begin{equation}
    \begin{split}
        X(e^{j\theta}) = I(e^{j\theta}) + b_1 I(e^{j\theta})  e^{-j\theta}+ \ldots + b_q I(e^{j\theta})e^{-jq\theta} &\newline  - a_1X(e^{j\theta})e^{-j\theta}  - \ldots - a_p X(e^{j\theta})e^{-jp\theta}&,
    \end{split}
\end{equation}
from which the transfer function can be determined as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = \frac{1 + b_1 e^{-j\theta} + \ldots + b_q e^{-jq\theta}}{1 + a_1e^{-j\theta}  + \ldots + a_p e^{-jp\theta}}.
\end{equation}

Using a similar approach as in the derivation of the AR(p) and MA(q) power spectral density functions, we can find that the power spectral density function of an ARMA(p,q) process is given as
\begin{equation}\label{eq:psd_ARMA}
    P_x(e^{j\theta}) = P_I(e^{j\theta})H(e^{j\theta})H^\ast(e^{j\theta}) = \sigma_i^2 \frac{|1 + b_1 e^{-j\theta} + \ldots + b_q e^{-jq\theta}|^2}{|1 + a_1e^{-j\theta}  + \ldots + a_p e^{-jp\theta}|^2}.
\end{equation}
