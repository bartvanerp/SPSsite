+++
title = "Stationarity and ergodicity"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-09-07

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Stationarity and ergodicity"        # name of this item in that menu
  weight = 2                           # location in that menu
  parent = "Stochastic processes and random signals"

+++

Stationarity and ergodicity are characterizations of random signals. They allow for the simplification of calculations and provide powerful tools in signal processing.

## Stationarity

A random process is called stationary if its statistical properties do not change over time. This means that the signal statistics of random variable $X[n]$ should be identical to the signal statistics of random variable $X[n+k]$ for any value of $k$. For the underlying probability distribution then holds that
\begin{equation}
    p_{X[n]}(x) = p_{X[n+k]}(x) = p_{X}(x),
\end{equation}
where it is possible to drop the indexing if there is no effect on the distribution.

If a signal is not stationary, the signal usually may be approximated as stationary for windowed sequences of the signal. This provides the foundation for the short-time Fourier transform.

### $N^\text{th}$-order stationarity

A signal is called an $N^\text{th}$-order stationary signal if the $N^\text{th}$-order signal statistics do not change over time. The order of the signal statistics is characterized by the largest multiplication chain of random variables in the signal statistics definition. As an example for the univariate case the mean can be regarded as a first-order signal statistic and the variance as a second-order signal statistic. Fig. 2 shows examples of random signals with first- and second-order stationarity.

### Strict-sense stationarity

When a random signal is fully stationary and absolutely none of its signals characteristics change over time, the signal can be regarded as <i>strict-sense stationary</i> (SSS). This also implies that the signal is a $N^\text{th}$-order stationary signal for $N=1,2,\ldots$.

### Wide-sense stationarity

<i>Wide-sense stationarity</i> (WSS) is a subset of strict-sense stationarity. Only signals that are both first- as second-order stationary are regarded as wide-sense stationary. The left plot in Fig. 2 can for example be regarded as wide-sense stationary. Because of the first- and second-order stationarity we may simplify the notation of its signal statistics as
\begin{equation}
    \mathrm{E}\Big[X[n]\Big] = \mu_X[n] = \mu_X
\end{equation}
and similarly
\begin{equation}
    \text{Var}\Big[X[n]\Big] = \sigma_X^2[n] = \sigma_X^2.
\end{equation}


<div style="max-width: 1100px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/signals/stationarity.svg"
      alt="Three types of random signals. The first signal is wide-sense stationary, meaning that its mean and variance do not change over time. The second signal is just first-order stationary, meaning that its mean is fixed, but its variance changes over time. The final signal is just second-order stationary, leading to a fixed variance, but a changing mean."
    />
    <figcaption class="numbered">
      Three types of random signals. The first signal is wide-sense stationary, meaning that its mean and variance do not change over time. The second signal is just first-order stationary, meaning that its mean is fixed, but its variance changes over time. The final signal is just second-order stationary, leading to a fixed variance, but a changing mean.
    </figcaption>
  </figure>
</div>


### Stationarity and second orders statistics

It is also important to consider the consequences of (wide-sense) stationarity for the covariance and correlation functions. From the definitions in the above table these properties depend on the two time indices $n_1$ and $n_2$. From the definition of the stationarity it can be concluded that for the example of the auto-covariance $\gamma_X[n_1,n_2] = \gamma_X[n_1+k, n_2+k]$ holds. This leads to the observation that the value of the covariance and correlation only depend on the difference between the two time indices. This time difference is called the <i>lag</i> and is defined as
\begin{equation}
    l = n_1-n_2.
\end{equation}
So for wide-sense stationary signals the notation of the correlation (and the covariance) may be simplified as
\begin{equation}
    r_X[n_1,n_2] = r_X[n_1-n_2] = r_X[l] = \mathrm{E}\Big[X[n_1]X^\ast[n_2]\Big] = \mathrm{E}\Big[X[n]X^\ast[n-l]\Big].
\end{equation}
Using this definition, the value of the auto-correlation function can be determined for $l=0$ as
\begin{equation}
    r_X[0]= \sigma_X^2 + |\mu_X|^2 \geq 0
\end{equation}
and it can be shown that this correlation value is (one of) the largest auto-correlation values since $r_X[0] \geq r_X[l] \ \ \forall \ \ l$. Furthermore it can be found that the auto-correlation function is a complex conjugate symmetric function of its lag
\begin{equation}\label{eq:corr_prop}
    r_X^\ast[-l] = r_X[l].
\end{equation}
When dealing with real-valued signals, this property can be simplified to $r_X[l] = r_X[-l]$.

<div class="example">
<h4> Exercise </h4>
<hr>
$X(t)$ and $Y(t)$ are independent wide sense stationary processes with expected values $\mu_X$ and $\mu_Y$ and auto-correlation functions $R_x(\tau)$ and $R_y(\tau)$, respectively. Let $W(t) = X(t)Y(t)$.
<ol type ="a">
    <li> Find $E[W(t)]$ and $R_W(t,\tau)$ and show that $W(t)$ is wide sense stationary. </li>
    <li> Are $W(t)$ and $X(t)$ jointly wide sense stationary?</li>
</ol>
<button class="collapsible">Show solution</button>
<div class="content">
<ol type ="a">
<li> Since $X(t)$ and $Y(t)$ are independent processes,
    \begin{equation*}
        E[W(t)] = E[X(t)Y(t)]=E[X(t)]E[Y(t)] = \mu_X \mu_Y.
    \end{equation*}
    In addition,
    \begin{equation*}
    \begin{split}
       R_W(t,\tau) = R_X(\tau)R_Y(\tau).
    \end{split}
    \end{equation*}   
    We can conclude that $W(t)$ is wide sense stationary. </li>
<li> To examine whether $W(t)$ and $X(t)$ are jointly wide sense stationary, we calculate
    \begin{equation*}
        R_{WX}(t,\tau) = E[W(t)X(t+\tau)] = E[X(t)Y(t)X(t+\tau)].
    \end{equation*}
    By independence of $X(t)$ and $Y(t)$,
    \begin{equation*}
        R_{WX}(t,\tau) = E[X(t)X(t+\tau)]E[Y(t)] = \mu_Y R_X(\tau).
    \end{equation*}
    Since $W(t)$ and $X(t)$ are both wide sense stationary and since $R_{WX}(t,\tau)$ depends only on the time difference $\tau$, we can conclude that $W(t)$ and $X(t)$ are jointly wide sense stationary.</li>
</ol>    
</div>
</div>


## Ergodicity

When a signal is stationary, the exact calculation of the expected value operators is usually still cumbersome, because it requires knowledge of the entire random process. In practice we usually only have a limited amount of sample of one realization of the random process. If a random process is ergodic then this means that the statistical properties of the entire random process can be inferred from just a limited amount of samples of a single realization. In order for a signal to be ergodic it has to be stationary. Ergodicity is usually a big assumption that cannot always be confirmed, however, without this assumption the signal statistics could not be approximated.


<br></br>

## Special case: zero-mean white noise

There is one really important case of the auto-correlation function that is often used in the field of signal processing. Namely the auto-correlation function of zero-mean white noise.
The auto-correlation function of a zero-mean white noise process can be determined as
\begin{equation} \label{eq:corr_white}
    r_X[l] = \mathrm{E}\Big[X[n]X^\ast[n-l]\Big] = \sigma_X^2\delta[l] =
    \begin{cases}
        \sigma_X^2,      & \text{for } l=0 \newline
        0.               & \text{otherwise}
    \end{cases}
\end{equation}

Let us break this definition down. So for a lag of $0$, the auto-correlation function reduces to the variance minus the squared mean. Since the mean is $0$, only the variance remains. Intuitively one could also regard the zero lag as multiplying each signal sample with itself, leading always to positive contributions, since the multiplication of equal signs always returns a positive number.

Now for all the other cases, we actually need to make use of the fact that the signal is white. However, the power spectrum is not yet introduced. Therefore an intuitive explanation is given, where the assumption is made that the noise is symmetrically distributed with zero-mean and is completely random. This means that each sample only depends on itself and has no dependence on the samples before or after it. If we were to introduce a certain lag $l$, each sample would be multiplied with another completely random sample at a distance $l$. This sample has a random sign and magnitude. Because of the zero-mean property we are half as likely to get a random number with a positive sign as a negative sign. The result of the multiplication therefore is equally likely to result in a positive or a negative contribution. Because of the random magnitudes that are symmetrically distributed around zero, in general we may intuitively understand that in total the total positive and negative contributions for the auto-correlation will cancel each other out, leading to a zero auto-correlation.

<div class="example">
<h4> Exercise </h4>
<hr>
Let $w[n]$ be a zero-mean, uncorrelated Gaussian random sequence with variance $\sigma^2[n]=1.$
<ol type="a">
<li> Characterize the random sequence  $w[n]$.</li>
<li> Define $x[n] = w[n] + w[n-1]$, $-\infty < n < \infty$. Determine the mean and autocorrelation of $x[n]$. Also characterize $x[n]$.</li>
</ol>
<button class="collapsible">Show solution</button>
<div class="content">
<ol type="a">
<li> Since uncorrelatedness implies independence for Gaussian random variables, $w[n]$ is an independent random sequence. Since its mean and variance are constants, it is at least stationary in the first order. Furthermore, we have
\begin{equation*}
r_x[n_1,n_2]=\sigma^2\delta[n_1-n_2]=\delta[n_1-n_2].
\end{equation*}
Hence $w[n]$ is also a WSS random process.</li>
<li> The mean of $x[n]$ is zero for all $n$ since $w[n]$ is a zero-mean process. Consider
\begin{equation*}
\begin{split}
r_x[n_1,n_2]&=E\{x[n_1]x[n_2]\}=E\{(w[n_1]+w[n_1-1])(w[n_2]+w[n_2-1])\}=\\
&=r_w[n_1,n_2]+r_w[n_1,n_2-1]+r_w[n_1-1,n_2]+r_w[n_1-1,n_2-1]\\
&=\sigma^2\delta[n_1-n_2]+\sigma^2\delta[n_1-n_2+1]+\sigma^2\delta[n_1-n_2-1]+\sigma^2\delta[n_1-1-n_2+1]\\
&=2\delta[n_1-n_2]+\delta[n_1-n_2+1]+\delta[n_1-n_2-1].\\
\end{split}
\end{equation*}
Clearly, $r_w[n_1,n_2]$ is a function of $n1-n2$. Hence
\begin{equation*}
\begin{split}
r_w[l]=2\delta[l]+\delta[l+1]+\delta[l-1].\\
\end{split}
\end{equation*}
Therefore, $x[n]$ is a WSS sequence. However, it is not an independent random sequence since both $x[n]$ and $x[n+1]$ depend on $w[n]$.</li>
</ol>
</div>
</div>

## Approximate statistics

For ergodic random processes the signal statistics that are defined in the table of <a href="../statisticalsignalprocessing_signals_signals/#ideal-signal-statistics">the previous section</a> can be approximated by time-averaging. The expected value operator will then be replaced by time-averaging over a sequence of length $N$ according to
\begin{equation}
    \mathrm{E}[\cdot] \quad \rightarrow \quad \frac{1}{N}\sum_{n=0}^{N-1}[\cdot].
\end{equation}
Please note that the averaging takes place over the individual realizations $x[n]$ and not over the random variables $X[n]$. Furthermore it would be better to denote the sequences of random numbers (bold capital letters) instead of the random processes itself (normal capital letters) in the subscripts of the signal statistics, because the approximation takes place over a finite length sequence and not the entire random process. However, because the processes are assumed to be stationary and ergodic these finite length sequences actually give a good approximation of the entire process. Therefore we can simplify our notation as for example $r_{\bf{XY}}[l] = r_{XY}[l]$.

By applying this time-averaging care should be taken for the calculation of the covariance and correlation functions. These functions need to be calculated for a certain lag $l$. When this lag $l$ reaches the length of the sequences $N$, then there is a very limited number of samples to average over. Therefore in the calculation of the covariance and correlation functions the lag $l$ is limited by a certain upper-lag $L$, which is significantly smaller than $N$.

The approximated signal statistics are denoted by a $\hat{\cdot}$ identifier. These approximate signal statistics are defined in the following table. It should be noted that the definitions of $\hat{r}$ and $\hat{\gamma}$ are biased, meaning that they are calculated by normalizing for $N$ values, whereas not always $N$ values are summed over, because of the effect of the lags.

<table>
    <tr>
        <th> Statistical property </th>
        <th style="text-align:center"> Definition </th>
        <th> Constraints </th>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Mean </td>
        <td> $$ \hat{\mu}_X = \frac{1}{N}\sum_{n=0}^{N-1} x[n] $$ </td>
        <td></td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Variance </td>
        <td> $$ \hat{\sigma}_X^2 = \frac{1}{N}\sum_{n=0}^{N-1} |x[n]-\hat{\mu}_X|^2 = \frac{1}{N}\sum_{n=0}^{N-1} |x[n]|^2 -|\hat{\mu}_X|^2 $$ </td>
        <td></td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Auto-covariance </td>
        <td> $$ \hat{\gamma}_X [l]= \frac{1}{N}\sum_{n=0}^{N-1-|l|} (x[n]-\hat{\mu}_X)(x[n-l]-\hat{\mu}_X)^\ast $$ </td>
        <td> $$ |l|\leq L-1 $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Auto-correlation </td>
        <td> $$ \hat{r}_X[l] = \frac{1}{N}\sum_{n=0}^{N-1-|l|} x[n]x^\ast[n-l] = \hat{\gamma}_X[l] + |\hat{\mu}_X|^2 $$ </td>
        <td> $$ |l|\leq L-1 $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Cross-covariance </td>
        <td> $$ \hat{\gamma}_{XY} [l]= \frac{1}{N}\sum_{n=0}^{N-1-|l|} (x[n]-\hat{\mu}_X)(y[n-l]-\hat{\mu}_Y)^\ast $$ </td>
        <td> $$ |l|\leq L-1 $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Cross-correlation </td>
        <td> $$ \hat{r}_{XY}[l] = \frac{1}{N}\sum_{n=0}^{N-1-|l|} x[n]y^\ast[n-l] = \hat{\gamma}_{XY}[l] + \hat{\mu}_X\cdot\hat{\mu}_Y^\ast $$ </td>
        <td> $$ 0\leq l\leq L-1 $$ </td>
    </tr>
    <tr>
        <td></td>
        <td> $$ \hat{r}_{XY}[l] = \frac{1}{N}\sum_{n=|l|}^{N-1} x[n]y^\ast[n-l] = \hat{\gamma}_{XY}[l] + \hat{\mu}_X\cdot\hat{\mu}_Y^\ast $$ </td>
        <td> $$ -(L-1)\leq l\leq 0 $$ </td>
    <tr>
        <td style="vertical-align:middle"> Correlation coefficient </td>
        <td> $$ \hat{\rho}_{XY}[l] = \frac{\hat{\gamma}_{XY}[l]}{\hat{\sigma}_X \cdot \hat{\sigma}_Y}  $$ </td>
        <td></td>
    </tr>
</table>

<br></br>

Before we saw that the value of the covariance and correlation only depends on the lag $l$ for stationary signals. For ergodic processes the covariances and correlations could be approximated from the time series by averaging. By approximating the definitions of the cross-covariance and cross-correlation matrices and by generalizing the definitions for the auto-covariance and -correlation matrices, the following approximated covariance and correlation matrices can be determined for the random signal sequences $\bf{X}$ and $\bf{Y}$ of length $N$. The approximated cross-covariance matrix can be defined using the definitions in the above table as


\begin{equation}
    \hat{\bf{\Gamma}}\_{XY} =
    \begin{bmatrix}
        \hat{\gamma}\_{XY}[0]   &   \hat{\gamma}\_{XY}[1]     &   \hat{\gamma}\_{XY}[2]    &   \cdots  & \hat{\gamma}\_{XY}[N-1] \newline
        \hat{\gamma}\_{XY}[-1]  &   \hat{\gamma}\_{XY}[0]     &   \hat{\gamma}\_{XY}[1]    &   \cdots  & \hat{\gamma}\_{XY}[N-2] \newline
        \hat{\gamma}\_{XY}[-2]  &   \hat{\gamma}\_{XY}[-1]    &   \hat{\gamma}\_{XY}[0]    &   \cdots  & \hat{\gamma}\_{XY}[N-3] \newline
        \vdots                  &   \vdots                    &   \vdots                   &   \ddots  & \vdots \newline
        \hat{\gamma}\_{XY}[1-N] &   \hat{\gamma}\_{XY}[2-N]   &   \hat{\gamma}\_{XY}[3-N]  &   \cdots  & \hat{\gamma}\_{XY}[0]
    \end{bmatrix}
\end{equation}

and the approximated cross-correlation matrix by

\begin{equation}
    \hat{\bf{R}}\_{XY} =
    \begin{bmatrix}
        \hat{r}\_{XY}[0]   &   \hat{r}\_{XY}[1]     &   \hat{r}\_{XY}[2]    &   \cdots  & \hat{r}\_{XY}[N-1] \newline
        \hat{r}\_{XY}[-1]  &   \hat{r}\_{XY}[0]     &   \hat{r}\_{XY}[1]    &   \cdots  & \hat{r}\_{XY}[N-2] \newline
        \hat{r}\_{XY}[-2]  &   \hat{r}\_{XY}[-1]    &   \hat{r}\_{XY}[0]    &   \cdots  & \hat{r}\_{XY}[N-3] \newline
        \vdots             &   \vdots               &   \vdots              &   \ddots  & \vdots \newline
        \hat{r}\_{XY}[1-N] &   \hat{r}\_{XY}[2-N]   &   \hat{r}\_{XY}[3-N]  &   \cdots  & \hat{r}\_{XY}[0]
    \end{bmatrix}.
\end{equation}
The approximated auto-covariance matrix can be defined by
\begin{equation}
    \hat{\bf{\Gamma}}\_{X} =
    \begin{bmatrix}
        \hat{\gamma}\_{X}[0]   &   \hat{\gamma}\_{X}[1]     &   \hat{\gamma}\_{X}[2]    &   \cdots  & \hat{\gamma}\_{X}[N-1] \newline
        \hat{\gamma}\_{X}[-1]  &   \hat{\gamma}\_{X}[0]     &   \hat{\gamma}\_{X}[1]    &   \cdots  & \hat{\gamma}\_{X}[N-2] \newline
        \hat{\gamma}\_{X}[-2]  &   \hat{\gamma}\_{X}[-1]    &   \hat{\gamma}\_{X}[0]    &   \cdots  & \hat{\gamma}\_{X}[N-3] \newline
        \vdots                 &   \vdots                   &   \vdots                  &   \ddots  & \vdots \newline
        \hat{\gamma}\_{X}[1-N] &   \hat{\gamma}\_{X}[2-N]   &   \hat{\gamma}\_{X}[3-N]  &   \cdots  & \hat{\gamma}\_{X}[0]
    \end{bmatrix}
\end{equation}
and the approximated auto-correlation matrix by
\begin{equation}
    \hat{\bf{R}}_{X} =
    \begin{bmatrix}
        \hat{r}\_{X}[0]   &   \hat{r}\_{X}[1]     &   \hat{r}\_{X}[2]    &   \cdots  & \hat{r}\_{X}[N-1] \newline
        \hat{r}\_{X}[-1]  &   \hat{r}\_{X}[0]     &   \hat{r}\_{X}[1]    &   \cdots  & \hat{r}\_{X}[N-2] \newline
        \hat{r}\_{X}[-2]  &   \hat{r}\_{X}[-1]    &   \hat{r}\_{X}[0]    &   \cdots  & \hat{r}\_{X}[N-3] \newline
        \vdots            &   \vdots              &   \vdots             &   \ddots  & \vdots \newline
        \hat{r}\_{X}[1-N] &   \hat{r}\_{X}[2-N]   &   \hat{r}\_{X}[3-N]  &   \cdots  & \hat{r}\_{X}[0]
    \end{bmatrix}.
\end{equation}

Especially the approximated auto-correlation matrix is in practice often used. When dealing with real-valued signals, this leads to a symmetric auto-correlation matrix (i.e. $\hat{\bf{R}}_X = \hat{\bf{R}}_X^\top$) and it turns out that this matrix is at the same time positive semi-definite (i.e. $\hat{\bf{R}} \succeq 0$).
