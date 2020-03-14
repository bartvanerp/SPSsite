+++
title = "Approximate signal statistics"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-14

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Approximate signal statistics"        # name of this item in that menu
  weight = 2                           # location in that menu
  parent = "Stochastic or random signals"
+++

## Approximate mean
For ergodic random processes the signal statistics that are defined in the table of <a href="../statisticalsignalprocessing_signals_signals/#ideal-signal-statistics">the previous section</a> can be approximated by time-averaging. The expected value operator will then be replace by time-averaging over a sequence of length $N$ according to
\begin{equation}
    \mathrm{E}[\cdot] \quad \rightarrow \quad \frac{1}{N}\sum_{n=0}^{N-1}[\cdot].
\end{equation}
Please note that the averaging takes place over the individual realizations $x[n]$ and not over the random variables $X[n]$. Furthermore it would be better to denote the sequences of random numbers (bold capital letters) instead of the random processes itself (normal capital letters) in the subscripts of the signal statistics, because the approximation takes place over a finite length sequence and not the entire random process. However, because the processes are assumed to be stationary and ergodic these finite length sequences actually give a good approximation of the entire process. Therefore we can simplify our notation as for example $r_{\bf{XY}}[l] = r_{XY}[l]$.

By applying this time-averaging care should be taken for the calculation of the covariance and correlation functions. These functions need to be calculated for a certain lag $l$. When this lag $l$ reaches the length of the sequences $N$, then there is a very limited number of samples to average over. Therefore in the calculation of the covariance and correlation functions the lag $l$ is limited by a certain upper-lag $L$, which is significantly smaller than $N$.

The approximated signal statistics are denoted by a $\hat{\cdot}$ identifier. These approximate signal statistics are defined in the following table. It should be noted that the definitions of $\hat{r}$ and $\hat{\gamma}$ are biased, meaning that they are calculating by normalizing for $N$ values, whereas not always $N$ values are summed over, because of the effect of the lags.

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
## Approximate covariance and correlation matrices
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
