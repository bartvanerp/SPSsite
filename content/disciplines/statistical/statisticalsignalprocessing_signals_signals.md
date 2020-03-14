+++
title = "Random signals"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-14

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Random signals"        # name of this item in that menu
  weight = 1                           # location in that menu
  parent = "Stochastic or random signals"
+++

This section will provide you with the tools to put all theory into practice when dealing with random signals. The link between random variables and discrete-time signals is stated and all statistical characteristics of a signal are covered.

## Representation of a random signal
First it is important to elaborate on the definition of a random signal. Suppose there is a transmitter which transmits a signal $f(t)$. This signals is attenuated over the transmission path, leading to an attenuated signal at the receiver $s(t) = \alpha \cdot f(t)$, where $\alpha$ indicates the degree of attenuation and which is bounded by $0 \leq |\alpha| \leq 1$. Now at the output of the receiver, this received signal $s(t)$ will also be corrupted by noise from the electrical components in the receiver and from other unwanted signals that are received. Let us capture all this noise in a single term called $n(t)$. The signal at the output of the receiver $x(t)$ can now be written as
\begin{equation}
    x(t) = s(t) + n(t).
\end{equation}
The noise $n(t)$ can be regarded as a random signal, whose statistics are known but whose realization is unpredictable. The signal $s(t)$ is fully deterministic, meaning that we can calculate and predict each sample of this signal if we know what the transmitted signal $f(t)$ is. If the deterministic signal $s(t)$ and the noise $n(t)$ are added to form the received signal $x(t)$, we receive a signal which we can partially predict (the deterministic portion) and which is partially unpredictable (the random noise). Therefore also the signal $x(t)$ is called a random signal. Fig. 1 shows an example of a deterministic signal to which noise is added to create a random signal.


<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/signals/randomsignal.svg"
      alt="An example of a deterministic signal to which random noise is added to create a random signal."
    />
    <figcaption class="numbered">
      An example of a deterministic signal to which random noise is added to create a random signal.
    </figcaption>
  </figure>
</div>

### Additive white Gaussian noise
The random noise $n(t)$ that is part of the random signal $s(t)$ can be described by a probability density function. For simplicity it is often assumed that this noise is <i>additive white Gaussian noise</i> or AWGN noise. All adjectives correspond to certain characteristics of the noise. The noise is additive, meaning that it is added to the deterministic part of the signal. Noise can be regarded as white if it has an uniform power distribution over the relevant frequency spectrum. As an analogy, white light emits all frequencies uniformly across the visible spectrum. Furthermore it is assumed that the noise is Gaussian distributed as was a fair assumption given the central limit theorem. Oftentimes this Gaussian noise distribution has a zero mean and even if this is not the case and the noise actually has a DC-term, then this DC-term is often regarded as part of the deterministic signal. We may therefore write that $n(t) \sim \mathcal{N}(n(t) \mid 0,\sigma_n^2)$, or similarly that $x(t) \sim \mathcal{N}(x(t) \mid s(t), \sigma_n^2)$, meaning that the probability distribution is centered around the deterministic signal.

<br></br>
## Discrete-time stochastic processes
Suppose we would like to measure a random or stochastic signal. Using multiple identical receivers we will sample the received signal at the exact same time instances. We can denote each discrete-time signal sample as $x[n,\xi_k]$, where $n$ corresponds to the discrete-time index or sample number and where $\xi_k$ corresponds to the receiving element $k$. The noise that is present on the signal results in different sample values for each of the receiving elements.

### Ensemble
The <i>ensemble</i> is defined as the set of all possible sequences of $x[n,\xi_k]$, which defines the entire stochastic process. Each signal sample for each receiver is affected by the noise that is present on the deterministic signal. This ensemble is therefore defined by the deterministic signal and the probability distribution of the random noise component.

### Realization
Now we know that each sample is affected by random noise. If we have a look at the sampled signal that is produced by a single receiver (i.e. we fix $\xi$), we will see a noisy signal. This noisy signal is called a <i>realization</i> of the random process. This means that if we measure the signal again or with another receiver, we will measure different samples, because of the random noise that is present.

### Random variable
Suppose that we now do not look at the random signal produced by a single receiver, but at a fixed instance of time (i.e. we fix $n$) where we compare the samples received from all receivers. All these receivers should measure the exact same deterministic signal, but a different value of the noise. Each of the measured samples is therefore distributed around the value of the deterministic signal according to the probability distribution of the noise. Therefore we can regard the signal sample at a fixed time instance $n$ as a <i>random variable</i>.

### A random signal sequence as a random vector
Each individual sample can be regarded as a random variable. Let us denote the random variable corresponding to a specific time instance $n$ as $X[n]$. Using this notation the random signal which contains the $N$ samples at and before time instance $n$ can be captured in a random vector ${\bf{X}}[n]$ as
\begin{equation}
    {\bf{X}}[n] = [X[n], X[n-1], \ldots, X[n-N+1]]^\top.
\end{equation}
The corresponding realization can be written as
\begin{equation}
    {\bf{x}}[n] = [x[n], x[n-1], \ldots, x[n-N+1]]^\top.
\end{equation}
Because of the way that these column vectors are constructed, it is relatively easy to modify it for a newly received sample. The last element of the vector can be removed and the new sample can be appended to the front of the vector.

Please note the notation with respect to the other modules. Random variables for time series are accompanied with a time index (e.g. $X[n]$). The random processes that generate all these random variables are referred to by a single capital letter $X$. Time series sequences of these random variables displayed as random vectors are distinguished by bold capital letters, such as $\bf{X}$.

<br></br>
## Correlation in a time series
The random signals can be written as random vectors and therefore it is also possible to determine relationships between the individual random variables through its covariance and the correlation.

Two different types of relationships should be distinguished between. First there is the degree of dependence between individual signal samples, where relationships between the signal samples can be determined. These relationships are referred to as the auto-covariance and auto-correlation. Secondly there is the degree of dependence between two entire signal sequences, where similarities between the two can be determined. These relationships are referred to as the cross-covariance and cross-correlation.

<br></br>
## Ideal signal statistics
Given the random variables $X[n]$ and $Y[n]$ corresponding to individual samples of the random processes $X$ and $Y$, the statistical properties can be determined. An overview of all statistical properties is given in the following table. The random process is referred to by the subscript and the sample(s) at which the property is determined is given in between the square brackets $[\cdot]$.

<table>
    <tr>
        <th> Statistical property </th>
        <th style="text-align:center"> Definition </th>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Mean </td>
        <td> $$ \mu_X[n] = \mathrm{E}\Big[X[n]\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Variance </td>
        <td> $$ \sigma_X^2[n] = \mathrm{E}\Big[\big|X[n] - \mu_X[n]\big|^2\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Auto-covariance </td>
        <td> $$ \gamma_X[n_1,n_2] = \mathrm{E}\Big[\big(X[n_1] - \mu_X[n_1]\big)\big(X[n_2] - \mu_X[n_2]\big)^\ast\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Auto-correlation </td>
        <td> $$ r_X[n_1,n_2] = \mathrm{E}\Big[ X[n_1]\cdot X^\ast[n_2]\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Cross-covariance </td>
        <td> $$ \gamma_{XY}[n_1,n_2] = \mathrm{E}\Big[\big(X[n_1] - \mu_X[n_1]\big)\big(Y[n_2] - \mu_Y[n_2]\big)^\ast\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Cross-correlation </td>
        <td> $$ r_{XY}[n_1,n_2] = \mathrm{E}\Big[ X[n_1]\cdot Y^\ast[n_2]\Big] $$ </td>
    </tr>
    <tr>
        <td style="vertical-align:middle"> Correlation coefficient </td>
        <td> $$ \rho_{XY}[n_1,n_2] = \frac{\gamma_{XY}[n_1,n_2]}{\sigma_X[n_1]\sigma_Y[n_2]} $$ </td>
    </tr>
</table>

<br></br>
## Stationarity and ergodicity
Stationarity and ergodicity are characterizations of random signals. They allow for the simplification of calculations and provide powerful tools in signal processing.

### Stationarity
A random process is called stationary if its statistical properties do not change over time. This means that the signal statistics of random variable $X[n]$ should be identical to the signal statistics of random variable $X[n+k]$ for any value of $k$. For the underlying probability distribution then holds that
\begin{equation}
    p_{X[n]}(x) = p_{X[n+k]}(x) = p_{X}(x),
\end{equation}
where it is possible to drop the indexing if there is no effect on the distribution.

If a signal is not stationary, the signal usually may be approximated as stationary for windowed sequences of the signal. The provides the foundation for the short-time Fourier transform.

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

### Stationarity and the covariance and correlation functions
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

### Ergodicity
When a signal is stationary, the exact calculation of the expected value operators is usually still cumbersome, because it requires knowledge of the entire random process. In practices we usually only have a limited amount of sample of one realization of the random process. If a random process is ergodic then this means that the statistical properties of the entire random process can be inferred from just a limited amount of samples of a single realization. In order for a signal to be ergodic it has to be stationary. Ergodicity is usually a big assumption that cannot always be confirmed, however, without this assumption the signal statistics could not be approximated.



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

Now for all the other cases, we actually need to make use of the fact that the signal is white. However, the power spectrum is not yet introduced. Therefore an intuitive explanation is given, where the assumption is made that the noise is symmetrically distributed with zero-mean and is completely random. This means that each sample only depends on itself and has no dependence on the samples before of after it. If we were to introduce a certain lag $l$, each sample would be multiplied with another completely random sample at a distance $l$. This sample has a random sign and magnitude. Because of the zero-mean property we are half as likely to get a random number with a positive sign as a negative sign. The result  of the multiplication therefore is equally likely to result in a positive as negative contribution. Because of the random magnitudes that are symmetrically distributed around zero, in general we may intuitively understand that in total the total positive and negative contributions for the auto-correlation will cancel each other out, leading to a zero auto-correlation.
