+++
title = "Parameteric methods"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Parametric methods"        # name of this item in that menu
  weight = 5                      # location in that menu
  parent = "Spectral estimation"
+++


So far the non-parametric methods were based on two major assumptions. First of all, by the calculation of the Fourier transform it is assumed that our finite signal is periodic. The period in this case is fixed by the length of the signal $N$. Because the signal is unknown, it is highly unlikely that this assumption is actually valid. Secondly, the estimated auto-correlation function of the finite signal is zero for absolute lags larger than the signal length. Because the auto-correlation has now also a finite window, the indirect method cannot calculate the exact power spectral density, limiting the resolution of the estimate.

It would be nice to extrapolate the auto-correlation function for larger lags, because this would increase the resolution of the estimated power spectral density. With extrapolation we are referring to the process where additional values are estimated or predicted based on the already available information. In other words, the auto-correlation function can be extended or extrapolated by finding a pattern in the available auto-correlation function and by filling the unknown values with the expected values from this pattern.

This pattern or <i>signal model</i> requires us to have some prior information about the signal generating process, otherwise it is impossible to determine an accurate signal model that would correspond with the obtained auto-correlation function. After the signal model has been identified, it needs to be fitted to the available auto-correlation function. This means that the unknown parameters of the signal model are estimated according to the available auto-correlation function, and once the parameters are estimated, the signal model can be used to estimate the entire auto-correlation function.

This approach is very different from the non-parametric methods and it is usually refer to as <i>parametric method</i>, by which parameters of a signal model are estimated such that signal and auto-correlation function can be described by such a model. The parametric approach roughly consists out of three steps. First, a signal model needs to be defined. This step is usually the hardest since it would ideally require prior knowledge of the process. If this knowledge is not available, then several models can be fitted to the data after which the most optimal one is chosen. The definition of optimal depends on the evaluation criterion. Second, once the model is defined, the parameters can be estimated and the power spectral density can be obtained using the signal model.

<br></br>
## Signal models
The first step in estimating the power spectral density is finding a signal model. How do we define such a signal model? One way is to use spectral factorization, i.e., filtering a white Gaussian process $i[n]$ by a linear time-invariant (LTI) filter. A white Gaussian process has the characteristic that the power spectral density is constant. If we transform this constant spectrum by applying filters (low-pass, high-pass etc.) to this spectrum it is possible to shape the power spectral density. In other words a constant spectrum can be filtered such that the resulting spectrum provides us with a good estimate of the actual power spectral density. Of course, we cannot directly assess the accuracy of the resulting spectrum since this is unknown, but we can compare the estimated with the determined auto-correlation functions. Although in principle there is an infinite number of possibilities for the filter, we typically restrict the choice to finite impulse response (FIR) and infinite impulse response (IIR) filters.


### Auto-regressive (p) filters
One specific type of filters are auto-regressive (AR) filters. In these filters, the current output only depends on the current input and previous outputs. An output $y[n]$ of a p$^\text{th}$-order AR filter can be described by its difference equation as
\begin{equation}
    y[n] = x[n] - \alpha_1 y[n-1] - \alpha_2 y[n-2] - \ldots - \alpha_p y[n-p],
\end{equation}
where $x[n]$ is the input to the filter and $\alpha_i$ are the filter coefficients. The order of the filter gives an indication on how many previous output samples are used to form a new output.

### Moving-average (q) filters
Moving-average (MA) filters determine the output from the current input and previous inputs. Therefore the difference equation of a q$^\text{th}$-order MA filter is given by
\begin{equation}
    y[n] = x[n] + \beta_1 x[n-1] + \beta_2 x[n-2] + \ldots + \beta_q y[n-q],
\end{equation}
where $x[n]$ and $y[n]$ are the input and output of the filter, respectively, and the $\beta_i$ are the filter coefficients. The order of the filter gives an indication on how many previous input samples are used to form a new output.

### Auto-regressive moving-average (p,q) filters
A logical extension to the previous two filters is the filter which combines both. This filter is called the auto-regressive moving-average filter (ARMA). This filter combines weighted previous inputs and outputs and the current input into a new output value. The difference equation of such a filter with a p$^\text{th}$-order AR part and an q$^\text{th}$-order MA part is given by
\begin{equation}
\begin{split}
    y[n] = x[n] + \beta_1 x[n-1] + \beta_2 x[n-2] + \ldots + \beta_q y[n-q]&\newline
    - \alpha_1 y[n-1] - \alpha_2 y[n-2] - \ldots - \alpha_p y[n-p]&
    \end{split}
\end{equation}
where $x[n]$ and $y[n]$ are respectively the input and output of the filter and $\alpha_i$ and $\beta_i$ are the filter coefficients of the AR and MA part respectively. The order of the filter gives an indication on how many previous input and output samples are used to form a new output.

<br></br>
## AR(p) spectral estimation
Suppose that now we assume our signal $x[n]$ to be the result of filtering a white Gaussian process with an AR filter. This is equivalent to assuming that the spectrum that we are trying to estimate is a consequence of shaping the uniform spectrum of the white Gaussian process by the transfer function of the AR filter. If the input to the system is now represented by the white Gaussian noise process $i[n]$ and the output is now the signal $x[n]$ (not the input signal in contrary to the nomenclature in the difference equation) that we are trying to estimate, we have the following equality
\begin{equation}
    x[n] = i[n] - \alpha_1 x[n-1] - \alpha_2 x[n-2] - \ldots - \alpha_p x[n-p].
\end{equation}

### The auto-correlation function of an AR(p) process
The filter coefficients provide us with almost all the information about the appearance of the power spectral density of our signal. Only the variance white Gaussian noise will need to be determined to know exactly the power spectral density of $x[n]$ at any frequency. Solving the above equality for the filter coefficients is not possible, because the signal $i[n]$ is random and therefore we have no starting point. It is also not directly possible to compare the power spectral density of the AR process and of the signal, because the true power spectral density of the signal is unknown. The best way to calculate the filter coefficients is through the estimated auto-correlation function. Then the estimated model of the auto-correlation function can be used to extrapolate the auto-correlation (or equivalently the power spectral density) at any lag (frequency) using the determined filter coefficients. This results in a virtually infinite resolution.

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
        r_{i,x}[l]
        &= \mathrm{E}\left\\{i[n]x^\ast[n-l]\right\\}, \newline
        &= \mathrm{E}\left\\{i[n]^\ast\left(i[n-l] - \alpha_1 x^\ast[n-1-l]  - \ldots - \alpha_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \mathrm{E}\left\\{i[n]i^\ast[n-l]\right\\} + \mathrm{E}\left\\{i[n]\left(- \alpha_1 x^\ast[n-1-l] - \ldots - \alpha_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \sigma_i^2\delta[l] -\alpha_1\mathrm{E}\left\\{i[n] x^\ast[n-1-l]\right\\} - \ldots - \alpha_p\mathrm{E}\left\\{i[n]x^\ast[n-p-l]\right\\}, \newline
        &= \sigma_i^2\delta[l]
    \end{split}
\end{equation}
where the simplification in the last line requires further clarification. Because the noise is independently distributed, only the expected value of two identically lagged signals $i[n]$ is non-zero. In the latter terms in the equation, the lagged signals $x[n-1-l],\ldots ,x[n-p-l]$ only depend on lagged values of the noise $i[n-1-l],\ldots ,i[n-p-l]$, which means that this always returns zero, because the white Gaussian noise signals are not calculated at the same lag.

Calculation of the auto-correlation function of the output $x[n]$ now gives
\begin{equation}
    \begin{split}
        r_x[l]
        &= \mathrm{E}\left\\{x[n]x^\ast[n-l]\right\\}, \newline
        &= \mathrm{E}\left\\{x[n]\left(i^\ast[n-l] - \alpha_1 x^\ast[n-1-l] - \ldots - \alpha_p x^\ast[n-p-l]\right)\right\\}, \newline
        &= \mathrm{E}\left\\{x[n]i^\ast[n-l]\right\\} - \alpha_1 \mathrm{E}\left\\{x[n]x^\ast[n-1-l]\right\\} - \ldots - \alpha_p \mathrm{E}\left\\{x[n]x^\ast[n-p-l]\right\\}, \newline
        &= r_{i,x}[l] - \alpha_1 r_{x}[l-1] - \ldots - \alpha_p r_{x}[l-p], \newline
        &= \sigma_i^2\delta[l] - \alpha_1 r_{x}[l-1] - \ldots - \alpha_p r_{x}[l-p],
    \end{split}
\end{equation}
which can rewritten as
\begin{equation}
    \sigma_i^2\delta[l] = \sum_{k=0}^p \alpha_k r_x[l-k],
\end{equation}
where the newly introduced coefficient $\alpha_0$ equals 1.

It is now possible to estimate the desired AR coefficients. When a windowed signal is observed and the auto-correlation function is estimated as $\hat{r}_x[l]$ the following relationship needs to be solved
\begin{equation}
     \hat{r}_x[l] + \hat{\alpha}_1 \hat{r}_x[l-1] + \ldots + \hat{\alpha}_p \hat{r}_x[l-p] = \hat{\sigma}_i^2\delta[l].
\end{equation}
The parameters $\hat{\alpha}_1$ up to $\hat{\alpha}_p$ and $\hat{\sigma}_i^2$ need to be estimated, using auto-correlation estimated from the data at lags $0,1, ..., p$. This equality has $p+1$ unknowns, and thus we require $p+1$ equations to solve this. These $p+1$ equation can be obtained by evaluating the auto-correlation for different lags. The system of equations that follows from this approach is called the \textit{Yule-Walker equations}, which can be written in matrix notation as
\begin{equation}
    \begin{bmatrix}
        \hat{r}_x[0]    & \hat{r}_x[1]      & \hat{r}_x[2]  & \cdots    & \hat{r}_x[p]      \newline
        \hat{r}_x[1]    & \hat{r}_x[0]      & \hat{r}_x[1]  & \cdots    & \hat{r}_x[p-1]    \newline
        \hat{r}_x[2]    & \hat{r}_x[1]      & \hat{r}_x[0]  & \cdots    & \hat{r}_x[p-2]    \newline
        \vdots          & \vdots            & \vdots        & \ddots    & \vdots            \newline
        \hat{r}_x[p]    & \hat{r}_x[p-1]    & \hat{r}_x[p-2]& \vdots    & \hat{r}_x[0]
    \end{bmatrix}
    \begin{bmatrix}
        1               \newline \hat{\alpha}_1   \newline \hat{\alpha}_2     \newline \vdots   \newline \hat{\alpha}_p
    \end{bmatrix}
    =
    \begin{bmatrix}
        \hat{\sigma}_i^2      \newline 0                \newline 0            \newline \vdots    \newline 0
    \end{bmatrix}
\end{equation}
where the signal $x[n]$ is real, leading to a symmetric auto-correlation function which is shown as $\hat{r}_x[l] = \hat{r}_x[-l]$. Solving this system of equations, the unknown filter coefficient $\hat{\alpha}_1, ..., \hat{\alpha}_p$, and unknown variance of the input noise in the model,  $\hat{\sigma}_i^2$, can be estimated by least-square linear estimation.

<h3> Example: AR(1) process </h3>
The output of an AR(1) process is given by the following difference equation
\begin{equation}
    x[n] = i[n] - \alpha_1 x[n-1].
\end{equation}
The corresponding auto-correlation function can be found as
\begin{equation}
    \begin{split}
        r_x[l]
        &= \mathrm{E}\left\{x[n]x^\ast[n-l]\right\}, \newline
        &= \mathrm{E}\left\{x[n]\left(i[n-l] - \alpha_1 x[n-1-l]\right)\right\}, \newline
        &= \mathrm{E}\left\{ x[n]i[n-l]\right\} - \alpha_1\mathrm{E}\left\{x[n]x[n-1-l]\right\}, \newline
        &= \sigma_i^2 \delta[l] - \alpha_1 r_x[l+1].
    \end{split}
\end{equation}
Evaluating the equation for the lags $0$ and $1$ gives
\begin{equation}
    r_x[0] = \sigma_i^2 - \alpha_1 r_x[1]
\end{equation}
and
\begin{equation}
    r_x[1] = r_x[-1] = -\alpha_1 r_x[0]
\end{equation}
respectively, where the auto-correlation function is assumed to be symmetric. From these two equations, we can determine the unknown filter coefficient and the noise variance. This approach will show how the unknown auto-correlation function can be determined. By combining the equations by the substitution of $r_x[1]$ of the second equation into the first gives
\begin{equation}
    r_x[0] = \sigma_i^2 - \alpha_1(-\alpha_1r_x[0]),
\end{equation}
from which, rearranging the terms, the value of $r_x[0]$ can be determined as
\begin{equation}
    r_x[0] = \frac{\sigma_i^2}{1-\alpha_i^2}
\end{equation}
and from this $r_x[1]$ can be determined as
\begin{equation}
    r_x[1] = -\alpha_1 \frac{\sigma_i^2}{1-\alpha_i^2}.
\end{equation}
This recursion can be extended to all lags, leading to the final description of the auto-correlation function as
\begin{equation}
    r_x[l] = \frac{\sigma_i^2}{1-\alpha_1^2}(-\alpha_1)^{|l|}
\end{equation}

Similarly the Yuke-Walker equations can be determined as
\begin{equation}
    \begin{bmatrix}
        r_x[0]  & r_x[l] \newline
        r_x[1]  & r_x[0]
    \end{bmatrix}
    \begin{bmatrix}
        1 \newline \alpha_1
    \end{bmatrix}
    =
    \begin{bmatrix}
        \sigma_i^2 \newline 0
    \end{bmatrix},
\end{equation}
which is similar to the system of equations determined above.

### The power spectral density of an AR(p) process
Suppose that we have succeeded in determining the most optimal parameters for the AR process and we want to find the power spectral density estimate of our signal. Filtering an input signal with a filter with transfer function $H(e^{j\theta})$ relates the input and output power spectral densities ($P_I(e^{j\theta})$ and $P_X(e^{j\theta})$ respectively) through
\begin{equation}\label{eq:psd_inout}
    P_X(e^{j\theta}) = |H(e^{j\theta})|^2 P_I(e^{j\theta}) = H(e^{j\theta})H^\ast(e^{j\theta}) P_I(e^{j\theta}).
\end{equation}
Note that the transfer function depends on the filter coefficients. This relationship can be determined by calculating the transfer function of the filter. The transfer function $H(e^{j\theta})$ of the filter can be determined by taking the Fourier transform of the equation as
\begin{equation}
    X(e^{j\theta}) = I(e^{j\theta}) - \alpha_1X(e^{j\theta})e^{-j\theta}  - \alpha_2 X(e^{j\theta})e^{-j2\theta} - \ldots - \alpha_p X(e^{j\theta})e^{-jp\theta},
\end{equation}
where $X(e^{j\theta})$ and $I(e^{j\theta})$ are the Fourier transforms of the desired signal and the white Gaussian process respectively. The terms can be separated as
\begin{equation}
    I(e^{j\theta}) = X(e^{j\theta}) (1+\alpha_1 e^{-j\theta}  + \alpha_2 e^{-j2\theta} + \ldots + \alpha_p e^{-jp\theta}).
\end{equation}
From this the transfer function of the system can be determined by the fraction of the output spectrum over the input spectrum as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = \frac{1}{1+\alpha_1 e^{-j\theta}  + \alpha_2 e^{-j2\theta} + \ldots + \alpha_p e^{-jp\theta}}.
\end{equation}
If we combine the result of this derivation with the fact that the power spectral density of a white Gaussian processes with variance $\sigma_i^2$ is given as $P_I(e^{j\theta}) = \sigma_i^2$, we finally obtain using (\ref{eq:psd_inout}) that
\begin{equation}\label{eq:psd_AR}
    P_X(e^{j\theta}) =  \frac{\sigma_i^2}{|1+\alpha_1 e^{-j\theta}  + \alpha_2 e^{-j2\theta} + \ldots + \alpha_p e^{-jp\theta}|^2}
\end{equation}

### Calculation procedure of an AR(p) spectrum
In order to estimate the spectrum of an AR(p) process the first step is to write down the Yule-Walker equation for a certain model order $p$. This model order can be freely chosen, but its performance can be measured using the metrics that will be discussed later on. For this Yule-Walker equation first the auto-correlation function of the signal should be estimated for lags $|l| \leq p$. Once the Yule-Walker equation has been established, the AR coefficients $\hat{\alpha}_i$ and the innovation variance $\hat{\sigma}^2_i$ can be calculated. With these parameters the analytical AR power spectral density can be estimated using (\ref{eq:psd_AR}). For practical implementations, however, the power spectral density is calculated using the DFT, zero-padded to length $L$, through
\begin{equation}
    \hat{P}[k] = \frac{\hat{\sigma}_i^2}{\left| \sum\_{i=0}^p \hat{\alpha}_ie^{-jik\frac{2\pi}{L}}\right|^2}.
\end{equation}


<br></br>
## MA(q) spectral estimation
Let us now assume that the signal $x[n]$ is the result of filtering a white Gaussian process with an MA filter. If the input to the system is now represented by the white Gaussian noise process $i[n]$ and the output is now the signal $x[n]$ (not the input signal in contrary to the nomenclature in the difference equation) that we are trying to estimate, we have the following equality
\begin{equation}
    x[n] = i[n] + \beta_1 i[n-1] + \beta_2 i[n-2] - \ldots - \beta_q i[n-q].
\end{equation}

### The auto-correlation function of an MA(q) process
The auto-correlation function of the AR process was recursive as we have seen before. This is caused by the fact that a noise signal that enters the filter will appear at the output and will in this way always be somehow involved in the filter. Because the filter also processes previous outputs, every noise input signal will always be present in this feedback loop. With MA processes this is not the case. Each sample of the input noise will only be memorized during the time that is present in the filter, determined by the filter length. Therefore, after a certain time, a noise sample will not be present anymore in the output signal. This also leads to the fact that the auto-correlation function will only be non-zero for several lags. There is no correlation for lags exceeding the length of the filter. In order to demonstrate this behaviour, the auto-correlation function is calculated for several lags.
At $l=0$ it can be found that
\begin{equation}
    \begin{split}
        r_x[0]
        &= \mathrm{E}\left\\{(i[n] + \beta_1i[n-1] + \beta_2i[n-2] + \ldots + \beta_qi[n-q])^2\right\\}, \newline
        &= \mathrm{E}\left\\{i^2[n]\right\\} + \mathrm{E}\left\\{\beta_1^2 i^2[n-1]\right\\} + \mathrm{E}\left\\{\beta_2^2 i^2[n-2]\right\\} + \ldots + \mathrm{E}\left\\{\beta_q^2 i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (1 + \beta_1^2 + \beta_2^2 + \ldots + \beta_q^2) = \sigma_i^2 \sum_{k=0}^{q}\beta_k^2,
    \end{split}
\end{equation}
where the terms including the noise signal that were not identically lagged were not shown, because these are zero. Furthermore, the coefficient $\beta_0$ is defined as 1. Similarly at $l=1$ the auto-correlation function can be determined as
\begin{equation}
    \begin{split}
        r_x[1]
        &= \mathrm{E}\big\\{(i[n] + \beta_1i[n-1]  + \ldots + \beta_qi[n-q]) \newline
        &\qquad\qquad \cdot(i[n-1] + \beta_1i[n-2]  + \ldots + \beta_qi[n-q-1])\big\\}, \newline
        &= \beta_1\mathrm{E}\left\\{i^2[n-1]\right\\} + \beta_1\beta_2\mathrm{E}\left\\{ i^2[n-2]\right\\} + \beta_2\beta_3\mathrm{E}\left\\{i^2[n-3]\right\\} \newline
        &\qquad\qquad + \ldots + \beta_{q-1}\beta_{q}\mathrm{E}\left\\{ i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (\beta_1 + \beta_1\beta_2 + \beta_2\beta_3 + \ldots + \beta_{q-1}\beta_q) = \sigma_i^2 \sum\_{k=1}^{q}\beta_k\beta_{k-1},
    \end{split}
\end{equation}
Please note how the lag has affected the above terms. Furthermore, the number of terms has decreased. The auto-correlation for $l=2$ can be determined as
\begin{equation}
    \begin{split}
        r_x[2]
        &= \mathrm{E}\big\\{(i[n] + \beta_1i[n-1]  + \ldots + \beta_qi[n-q]) \newline
        &\qquad\qquad \cdot(i[n-2] + \beta_1i[n-3]  + \ldots + \beta_qi[n-q-2])\big\\}, \newline
        &= \beta_2\mathrm{E}\left\\{i^2[n-2]\right\\} + \beta_1\beta_3\mathrm{E}\left\\{ i^2[n-3]\right\\} + \beta_2\beta_4\mathrm{E}\left\\{i^2[n-4]\right\\} \newline
        &\qquad\qquad + \ldots + \beta_{q-2}\beta_{q}\mathrm{E}\left\\{ i^2[n-q]\right\\}, \newline
        &= \sigma_i^2 (\beta_2 + \beta_1\beta_3 + \beta_2\beta_4 + \ldots + \beta_{q-2}\beta_q) = \sigma_i^2 \sum\_{k=2}^{q}\beta_k\beta_{k-2}.
    \end{split}
\end{equation}

This methodology can be extended for multiple lags, but a pattern should become noticeable, revealing the mathematical structure of the auto-correlation function. The mathematical description of the auto-correlation function can therefore be described as
\begin{equation}
    r_x[l] =
    \begin{cases}
        \sigma_i^2 \sum\_{k=|l|}^q \beta_{k}\beta_{k-|l|},       & \text{for } 0\leq |l|  \leq q \newline
        0.                                                  & \text{otherwise}
    \end{cases}
\end{equation}

### The power spectral density of an MA(q) process
From the definition of the difference equation, the Fourier equivalent can be determined as
\begin{equation}
    X(e^{j\theta}) = I(e^{j\theta}) + \beta_1 I(e^{j\theta}) e^{-j\theta} + \ldots + \beta_q I(e^{j\theta})e^{-jq\theta},
\end{equation}
from which the transfer function can be determined as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = 1 + \beta_1 e^{-j\theta} + \ldots + \beta_q e^{-jq\theta}.
\end{equation}
Using a similar approach as in the derivation of the AR(p) power spectral density function, we can find that the power spectral density function of an MA(q) process is given as
\begin{equation}\label{eq:psd_MA}
    P_x(e^{j\theta}) = P_I(e^{j\theta})H(e^{j\theta})H^\ast(e^{j\theta}) = \sigma_i^2 |1 + \beta_1 e^{-j\theta} + \ldots + \beta_q e^{-jq\theta}|^2.
\end{equation}


### Calculation procedure of an MA(q) spectrum
In order to estimate the spectrum of an MA(q) process three methods exist.

First, the windowed estimated auto-correlation function can be used to estimate the power spectral density directly using the Wiener-Khinchin relationship. It is known that the analytical auto-correlation function is non-zero for lags $|l| < q$ where $q$ denotes the process order. Using this fact, the auto-correlation function can be approximated by windowing the estimated auto-correlation function to the expected non-zero lags. From this the power spectral density can be estimated as
\begin{equation}
    \hat{P}(e^{j\theta}) = \sum_{l=-q}^q \hat{r}[l] e^{jl\theta}.
\end{equation}
This description can be compared with the Blackman-Tukey method of the previous section using a rectangular window of length $2q+1$. It should also be noted that care should be taken whilst performing this estimation, because model mismatch can lead to a negative power spectral density at some relative frequencies, which should not be possible by the definition of the power spectral density.

Secondly, from the estimated auto-correlation function of the signal, it is also possible to estimate the model parameters $\hat{\beta}_i$ and the innovation variance $\hat{\sigma}_i^2$. This estimation is a non-linear estimation problem. However, once the parameters have been obtained and the power spectral density is calculated using (\ref{eq:psd_MA}), the power spectral density is guaranteed to be non-negative.

A third approach is aimed more specifically at the practical implementation of the above mentioned methods. Here the analytical description of the power spectral density is approximated using (a zero-padded version of) the DFT or FFT.

<br></br>
## ARMA(p,q) spectral estimation
Let us now assume that the signal $x[n]$ is the result of filtering a white Gaussian process with an ARMA filter. Then, we have the following equality
\begin{equation}
\begin{split}
    x[n] = i[n] + \beta_1 i[n-1] + \beta_2 i[n-2] + \ldots + \beta_q i[n-q]&\newline
    - \alpha_1 x[n-1] - \alpha_2 x[n-2] - \ldots - \alpha_p x[n-p]&.
    \end{split}
\end{equation}


### The auto-correlation function of an ARMA(p,q) process
As we have seen so far, the ARMA process is a combination of a AR and MA process. This also becomes apparent in the auto-correlation function. The derivation is lengthy and will not be shown, but an intuitive description is given. The auto-correlation function of an ARMA(p,q) process is given as
\begin{equation}
    r_x[l] =
    \begin{cases}
        \sigma_i^2 \sum_{k=|l|}^q \beta_{k}\beta_{k-|l|} - \sum_{k=1}^p \alpha_k r_x[|l|-k],  &\text{for }0 \leq |l| \leq q \newline
        - \sum_{k=1}^p \alpha_k r_x[|l|-k].  &\text{for }|l| > q \\
    \end{cases}
\end{equation}
This expression seems complicated, but it is easily explained by comparison with the auto-correlation function of the AR and MA process. The value of the auto-correlation function is a combination of both AR and MA auto-correlation functions. As with the AR process, the auto-correlation function has a recursive structure as can be seen from the terms with the $\alpha_i$ coefficients. For smaller lags, there is not only an effect of an AR process, but there is also the effect of the MA process. In other words, the ARMA process and its auto-correlation function can be interpreted as the super-imposition of the AR and MA processes.

### The power spectral density of an ARMA(p,q) process
From the definition of the difference equation the Fourier equivalent can be determined as
\begin{equation}
    \begin{split}
        X(e^{j\theta}) = I(e^{j\theta}) + \beta_1 I(e^{j\theta})  e^{-j\theta}+ \ldots + \beta_q I(e^{j\theta})e^{-jq\theta} &\newline  - \alpha_1X(e^{j\theta})e^{-j\theta}  - \ldots - \alpha_p X(e^{j\theta})e^{-jp\theta}&,
    \end{split}
\end{equation}
from which the transfer function can be determined as
\begin{equation}
    H(e^{j\theta}) = \frac{X(e^{j\theta})}{I(e^{j\theta})} = \frac{1 + \beta_1 e^{-j\theta} + \ldots + \beta_q e^{-jq\theta}}{1 + \alpha_1e^{-j\theta}  + \ldots + \alpha_p e^{-jp\theta}}.
\end{equation}
Using a similar approach as in the derivation of the AR(p) and MA(q) power spectral density functions, we can find that the power spectral density function of an ARMA(p,q) process is given as
\begin{equation}\label{eq:psd_ARMA}
    P_x(e^{j\theta}) = P_I(e^{j\theta})H(e^{j\theta})H^\ast(e^{j\theta}) = \sigma_i^2 \frac{|1 + \beta_1 e^{-j\theta} + \ldots + \beta_q e^{-jq\theta}|^2}{|1 + \alpha_1e^{-j\theta}  + \ldots + \alpha_p e^{-jp\theta}|^2}.
\end{equation}

### Calculation procedure of an ARMA(p,q) spectrum
The ARMA process is a combination of the AR(p) and MA(q) process. The ARMA coefficients can be estimated as follows.

First, the AR coefficients are estimated. The auto-correlation function of the ARMA process consists of the AR(p) auto-correlation function added to the MA(q) auto-correlation function. The former spans over all lags whereas the influence of the latter is bounded by its model order $|l| \geq q$. For lags $|l| > q$ only the influence of the AR(p) process is visible and from this region in the auto-correlation function the AR coefficients can be determined using the methods as described previously.

Secondly, the goal is to remove the influence of the AR(p) process such that only the MA(q) process remains. Several methods exist to perform this inverse filtering and are often denoted as deconvolution or spectral subtraction, however, this is beyond the scope of this reader.

Once the MA(q) process has been separated, the MA parameters can be determined using the methods as described earlier. After this, both the AR and MA parameters have been estimated and the analytical power spectral density can be determined using (\ref{eq:psd_ARMA}) or by approximating it with the DFT or FFT.


<br></br>
## Model selection
As mentioned in the beginning of this section, choosing the right model is the hardest design choice in parametric estimation. There is an infinite number of options to explore each with a different complexity. But how can we know which model is actually the best? As an analogy we present a well-known regression example, where the goal is to describe a set of points as good as possible using a function. Fig. 1 shows three lines that were fitted to some data. Intuitively, the middle plot seems to represent the best fit; the left plot does not capture the essence of the samples (large error, while the right plot tunes to the specific data points, and hence might tune to the noise rather than the actual model generating the data. If there would be new data, which is similarly distributed as the already present data, then the fit of the right plot would be inadequate. Thus, when choosing a model it can either be too simplistic or too complex. These phenomena are respectively called <i>underfitting</i> and <i>overfitting</i>.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/model_selection.svg"
      alt="Three different fits of data using a polynomial, differentiating between the underfitting, overfitting and having an appropriate fit."
    />
    <figcaption class="numbered">
      Three different fits of data using a polynomial, differentiating between the underfitting, overfitting and having an appropriate fit.
    </figcaption>
  </figure>
</div>

In machine learning, underfitting and overfitting are major problems. Nonetheless, several methodologies have been developed in order to limit this undesired behaviour. One of these includes a more realistic optimization scheme. Instead of optimizing only the fit of the function, now the complexity is also considered. This is called <i>regularization</i>. The optimization algorithm needs to find a balance between a very complex model with a perfect fit and a very simple model with a bad fit.

With the spectral estimation techniques presented above, similar reasoning is used. As the performance criterion of the best model, not only the error should be considered, but also the model complexity. This criterion can be implemented in several ways as will be seen.

### Residual error
The most basic model selection criterion is the residual error $\hat{\sigma}_r^2$. This error is the variance of the residual signal, defined as $\hat{x} - x$, which is the difference between the estimated and true signal. By the definition of the variance, this is also commonly known as the mean-squared error.

A performance metric which is commonly used in the field of statistics and which uses the residual error is the coefficient of determination, denoted by $R^2$. This coefficient is defined as
\begin{equation}
    R^2 = 1-\frac{\sum_i(x_i - \mu_x)^2}{\sum_i (x_i - \hat{x}_i)^2}.
\end{equation}
The coefficient can be understood as one minus the ratio between the variance of the data and the variance of the residual error. This coefficient is upper-bounded by the value of $1$ since the variance cannot be negative. For perfect models the variance of the error equals $0$ and therefore the coefficient of determination attains its upper bound. A lower value of $R^2$ denotes a more worse model fit. Although the coefficient of determination is denoted using the square operator, it should be noted that its value can actually be negative, denoting a very poor fit of the model.

### Final prediction error
The final prediction error (FPE) is a metric which adds an additional factor to the variance of the residual error $\hat{\sigma}_P^2$. This additional factor depends on the signal length $N$ and the number of parameters in the model $P$. For example, for an AR model $P=p+1$, where $p$ is the AR model order and 1 is given by the input noise variance. The FPE provides some compensation between the error (which decreases as the model order increases) and the number of model parameters, by applying a penalty for the increasing P. The final prediction error is defined as
\begin{equation}
    \text{FPE}(P) = \frac{N+P}{N-P} \hat{\sigma}^2_P.
\end{equation}
The best model is chosen as the one that yields the lowest FPE.

### Akaike's information criterion
Another model selection criterion is the Akaike's information criterion (AIC). This criterion is based on the Kullback-Leibler divergence and is defined as
\begin{equation}
    \text{AIC}(P) = N\cdot \ln(\hat{\sigma}_P^2) + 2P.
\end{equation}
This criterion, however, is very likely to lead to overfitting when the number of samples is limited. Therefore a corrected version of the Akaike's information criterion is introduced as
\begin{equation}
    \text{AICc}(P) = N\cdot \ln (\hat{\sigma}_P^2) + 2P + \frac{2P(P+1)}{N-P-1}.
\end{equation}
The best model order is chosen as the one that yields the lowest AIC (or AICc).

Although these criteria are useful to compare similar models of the different orders, they are not suited to compare different model structure. This a much more complex task that is beyond the scope of this reader.

### Example
Given some data that can ideally be modelled as
\begin{equation}
    y[n] = ax^2[n] + bx[n] + c + w[n],
\end{equation}
where $a$, $b$ and $c$ denote the true model parameters and $w[n]$ is Gaussian distributed noise. Fig. 2 shows the observed data, the true underlying model and estimates of the underlying model. These estimates correspond to linear equations where the order equals the largest power of the input signal in the model. Order $0$ corresponds to only a constant signal. The following table shows several performance metrics for different model orders. The residual error and the coefficient of determination do not take the number of parameters into account and therefore prefer the most complex models. All other performance metrics actually correct for the number of parameters and also prefer the order of the true underlying model.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/modelcomparison.svg"
      alt="Observed data with the true underlying data generation model. Furthermore several orders of polynomials are plotted that try to fit the data."
    />
    <figcaption class="numbered">
      Observed data with the true underlying data generation model. Furthermore several orders of polynomials are plotted that try to fit the data.
    </figcaption>
  </figure>
</div>

<table>
    <tr>
        <th style="text-align:center"> Order </th>
        <th style="text-align:center"> P </th>
        <th style="text-align:center"> $\hat{\sigma}^2_P$ </th>
        <th style="text-align:center"> $R^2$ </th>
        <th style="text-align:center"> $FPE(P)$ </th>
        <th style="text-align:center"> $AIC(P)$ </th>
        <th style="text-align:center"> $AICc(P)$ </th>
    </tr>
    <tr>
        <td style="text-align:center"> 0 </td>
        <td style="text-align:center"> 1 </td>
        <td style="text-align:center"> 7321 </td>
        <td style="text-align:center"> 0 </td>
        <td style="text-align:center"> 7808 </td>
        <td style="text-align:center"> 277.9 </td>
        <td style="text-align:center"> 278.0 </td>
    </tr>
    <tr>
        <td style="text-align:center"> 1 </td>
        <td style="text-align:center"> 2 </td>
        <td style="text-align:center"> 791 </td>
        <td style="text-align:center"> 0.8919 </td>
        <td style="text-align:center"> 900 </td>
        <td style="text-align:center"> 210.9 </td>
        <td style="text-align:center"> 211.3 </td>
    </tr>
    <tr>
        <td style="text-align:center"> 2 </td>
        <td style="text-align:center"> 3 </td>
        <td style="text-align:center"> 64.1 </td>
        <td style="text-align:center"> 0.9912 </td>
        <td style="text-align:center"> $\bf{77.9}$ </td>
        <td style="text-align:center"> $\bf{135.0}$ </td>
        <td style="text-align:center"> $\bf{135.8}$ </td>
    </tr>
    <tr>
        <td style="text-align:center"> 3 </td>
        <td style="text-align:center"> 4 </td>
        <td style="text-align:center"> $\bf{62.7}$ </td>
        <td style="text-align:center"> $\bf{0.9914}$ </td>
        <td style="text-align:center"> 81.2 </td>
        <td style="text-align:center"> 136.3 </td>
        <td style="text-align:center"> 137.7 </td>
    </tr>
</table>
