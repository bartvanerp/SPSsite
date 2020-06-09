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
  parent = "Stochastic processes and random signals"
+++

This section will provide you with the tools to put all theory into practice when dealing with random signals. The link between random variables and discrete-time signals is stated and all statistical characteristics of a signal are covered.

<br></br>
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


