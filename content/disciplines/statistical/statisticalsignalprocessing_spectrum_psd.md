+++
title = "Spectral distributions"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Spectral distributions"        # name of this item in that menu
  weight = 3                      # location in that menu
  parent = "Spectral estimation"
+++

This section will describe the main methods used to calculate the energy and power spectrum of a discrete-time signal. Initially, we will assume that the signal is infinitely long, has zero-mean and is stationary. However, since this is usually not the case, we will later analyze the consequences of these non-ideal conditions.

{{% alert note %}}
**Reading&Watching guide**

The reader provides all the necessary information. The video "Energy and power spectral distribution" gives additional guidance on some derivations and provides a couple of examples of energy and power signals. The content in the video and the reader partially overlaps.
{{% /alert %}}

<br></br>

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/YSlmCHvJ0ek" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Energy signals
If an infinitely long signal has finite signal energy it is called an <i>energy signal</i>. Since the energy is finite and the time duration infinite, the average signal power is zero. An example of an energy signal is a short pulse that is transmitted only once. An energy signal can be characterized by its <i>energy spectral distribution</i> (ESD), which describes the energy distribution of the signal in the frequency domain. The ideal energy spectral density is denoted by $\mathcal{E}(e^{j\theta})$ and can be calculated using a direct or an indirect method.

As described in the reader on random processes and signals, the total energy $E_s$ of an energy signal $x[n]$ can be calculated as
\begin{equation}\label{eq:energy}
    E_s = \sum_{n=-\infty}^\infty | x[n] |^2,
\end{equation}
which is bounded between $0$ and $\infty$ by the definition of an energy signal.

<br></br>
## Energy spectral distribution: direct method
The energy spectral distribution of a discrete-time energy signal can be determined by squaring the magnitude spectrum of signal spectrum $X(e^{j\theta})$ as
\begin{equation}\label{eq:energy_direct}
    \mathcal{E}(e^{j\theta}) = \left| X(e^{j\theta})\right|^2 = \left| \sum_{n=-\infty}^\infty x[n]e^{-jn\theta}\right|^2,
\end{equation}
where the second equality results from the definition of the Fourier transform for discrete-time signals. In order to show that this definition is valid, we first need to make use of the <i>Parseval's theorem</i>, which states that the energy of a signal in the time-domain should be equal to the energy of the signal in the frequency-domain as

\begin{equation}\label{eq:parseval}
    \sum_{n=-\infty}^\infty |x[n]|^2 = \frac{1}{2\pi}\int_{-\pi}^\pi \left|X(e^{j\theta})\right|^2 \mathrm{d}\theta.
\end{equation}

Secondly, the intuitive definition of the total signal energy is required, which is the integral of the energy spectral distribution $\mathcal{E}(e^{j\theta})$ over all frequencies as
\begin{equation}\label{eq:energy_int}
    E_s = \frac{1}{2\pi}\int_{-\pi}^\pi \mathcal{E}(e^{j\theta})\mathrm{d}\theta.
\end{equation}

Combining (\ref{eq:energy}), (\ref{eq:parseval}) and (\ref{eq:energy_int}) leads to the desired direct calculation method as described by (\ref{eq:energy_direct}).

<br></br>
## Energy spectral distribution: indirect method
Using the definition of the Fourier transform for discrete-time signals, the direct method can be rewritten as
\begin{equation}
    \begin{split}
        \mathcal{E}(e^{j\theta})
        &= \left|X(e^{j\theta})\right|^2, \newline
        &= X(e^{j\theta})X^\ast (e^{j\theta}), \newline
        &= \left(\sum_{n=- \infty}^{\infty} x[n] e^{-jn\theta}\right)\left(\sum_{p=- \infty}^{\infty} x^\ast[p] e^{jp\theta}\right), \newline
        &= \sum_{p=- \infty}^{\infty}\sum_{n=- \infty}^{\infty}x[n]x^\ast[p]e^{-j(n-p)\theta}, \newline
        &\overset{p = n-l}{=} \sum_{l=- \infty}^{\infty}\left(\sum_{n=- \infty}^{\infty}x[n]x^\ast[n-l]e^{-jl\theta}\right), \newline
        &= \sum_{l=-\infty}^\infty r_x[l]e^{-jl\theta}
    \end{split}
\end{equation}
which is the Fourier transform for discrete-time signals of the ideal auto-correlation function $r_x[l]$, which is defined as
\begin{equation}
    r_x[l] = \mathrm{E}\left[x[n]x^\ast[n-l]\right] = \sum_{n=-\infty}^\infty x[n]x^\ast[n-l] = r_x^\ast[-l],
\end{equation}
where $l$ represents the lag between the signal $x[n]$ and its shifted version $x[n-l]$. As it is shown, the indirect method calculates the energy spectral distribution by calculating the Fourier transform for discrete-time signals of the auto-correlation function. This relation is described by the <i>Wiener-Khintchine theorem</i>. Fig. 1 graphically shows both the direct and indirect method for calculating the energy spectral density.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/energymethods.svg"
      alt="Graphical overview of the direct and indirect methods for calculating the energy spectral density of an energy signal."
    />
    <figcaption class="numbered">
      Graphical overview of the direct and indirect methods for calculating the energy spectral density of an energy signal.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Example </h4>
Given the signal $x[n] = a^n \cdot u[n]$, where $u[n]$ represents the unit step function and $|a|<1$, calculate the frequency spectrum, auto-correlation function, energy spectral density and signal energy of $x[n]$.
<button class="collapsible">Show solution</button>
<div class="content">
The frequency spectrum $X(e^{j\theta})$ can be calculated as
\begin{equation*}
    X(e^{j\theta}) = \sum_{n=-\infty}^\infty x[n]e^{-jn\theta} = \sum_{n=0}^\infty \left(ae^{-j\theta}\right)^n = \frac{1}{1-ae^{-j\theta}}.
\end{equation*}
The auto-correlation function can be determined as
\begin{equation*}
    \begin{split}
        r_x[l]
        &= \sum_{n=-\infty}^\infty x[n]x[n-l] \\
        &= \sum_{n=-\infty}^\infty a^nu[n]a^{n-l}u[n-l] \\
        &\overset{l\geq 0}{=} a^{-l}\sum_{n=l}^\infty a^{2n} \\
        &= a^{-l} \left(\sum_{n=0}^\infty a^{2n} - \sum_{n=0}^{l-1} a^{2n}\right) \\
        &= a^{-l} \left(\frac{1}{1-a^2} - \frac{1-a^{2l}}{1-a^2}\right) \\
        &= \frac{a^l}{1-a^2}.
    \end{split}
\end{equation*}
Here only the case where $l\geq 0$ is discussed. Because the signal $x[n]$ is a real signal (i.e. $x[n] = x^\ast[n]$) the auto-correlation function is symmetric around $l=0$ and is therefore fully given as
\begin{equation*}
    r_x[l] = \frac{a^{|l|}}{1-a^2}.
\end{equation*}
The energy spectral density can be determined as
\begin{equation*}
    \begin{split}
        \mathcal{E}(e^{j\theta})
        &= |X(e^{j\theta})|^2 = \sum_{l=-\infty}^\infty r_x[l] e^{-jl\theta} \\
        &= \frac{1}{1-ae^{-j\theta}}\frac{1}{1-ae^{j\theta}} = \frac{1}{(1+a^2) - 2a\cos(\theta)}.
    \end{split}
\end{equation*}
From this the total signal energy can be determined as
\begin{equation*}
    E_s = \frac{1}{2\pi}\int_{-\pi}^\pi \mathcal{E}(e^{j\theta}) \mathrm{d}\theta = \sum_{n=-\infty}^\infty |x[n] |^2 = \sum_{n=0}^\infty a^{2n} = \frac{1}{1-a^2}.
\end{equation*}
</div>
</div>


<br></br>
## Power signals
An infinitely long signal that has a finite average signal power is called a <i>power signal</i>. Because of the finite power that the signal carries over an infinitely long time, the total signal energy is infinite. Any non-zero bounded signal that is infinitely-long can be regarded as a power signal. A power signal can be characterized by its <i>power spectral distribution</i> (PSD), which describes the power distribution of the signal in the frequency domain. The power spectral density is denoted by $P(e^{j\theta})$ and it can be calculated using a direct and an indirect method, which are known as the <i>periodogram</i> and <i>correlogram</i> respectively.

Since the signal power is defined as the energy density over time, the average signal power $P_s$ of a windowed power signal $\tilde{x}[n]$ of length $N$ can be calculated as
\begin{equation}\label{eq:power_avg}
    P_s = \lim_{N\rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1} | \tilde{x}[n] |^2,
\end{equation}  
which is bounded between $0$ and $\infty$ by the definition of a power signal. The windowing operation is explained in detail later on in this reader.

<br></br>
## Power spectral distribution: direct method
Similarly to above, the average signal power can be intuitively understood as the integral of the power spectral distribution over frequencies as
\begin{equation}\label{eq:power_integral}
    P_s = \frac{1}{2\pi}\int_{-\pi}^\pi P(e^{j\theta})\mathrm{d}\theta =\lim_{N\rightarrow \infty} \frac{1}{2\pi}\int_{-\pi}^\pi P_N(e^{j\theta})\mathrm{d}\theta,
\end{equation}
where the subscript $N$ denotes the length of the windowed signal $\tilde{x}[n]$. The ideal power spectral distribution can be determined as
\begin{equation}
    P(e^{j\theta}) = \lim_{N\rightarrow \infty} P_N(e^{j\theta}).
\end{equation}
This definition cannot be evaluated directly since it requires an infinitely long signal window.
In order to define $P_N(e^{j\theta})$, first $X_N(e^{j\theta})$ has to be defined as the Fourier transform for discrete-time signals of the windowed signal $x[n]$ with length $N$ as
\begin{equation}\label{eq:power_Xn}
    X_N(e^{j\theta}) = \sum_{n=0}^{N-1} \tilde{x}[n]e^{-jn\theta}      \ \circ  \hspace{-1.5mm} - \hspace{-1.5mm} \circ \ \tilde{x}[n] = \frac{1}{2\pi} \int_{-\pi}^\pi X_N(e^{j\theta})e^{jn\theta}\mathrm{d}\theta.
\end{equation}

By rewriting (\ref{eq:power_avg}) using (\ref{eq:power_Xn}), the following expansion can be obtained
\begin{equation}
    \begin{split}
        P_s
        &= \lim_{N\rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1} | \tilde{x}[n] |^2, \newline
        &= \lim_{N\rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1}  \tilde{x}[n] \tilde{x}^\ast[n], \newline
        &= \lim_{N\rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1}  \tilde{x}[n] \left(\frac{1}{2\pi} \int_{-\pi}^\pi X_N^\ast(e^{j\theta})e^{-jn\theta}\mathrm{d}\theta\right), \newline
        &= \lim_{N\rightarrow \infty} \frac{1}{2\pi} \int_{-\pi}^\pi \frac{1}{N} \left(\sum_{n=0}^{N-1}  \tilde{x}[n] e^{-jn\theta}\right) X_N^\ast(e^{j\theta})\mathrm{d}\theta, \newline
        &= \lim_{N\rightarrow \infty} \frac{1}{2\pi} \int_{-\pi}^\pi \frac{1}{N} X_N(e^{j\theta}) X_N^\ast(e^{j\theta})\mathrm{d}\theta, \newline
        &= \lim_{N\rightarrow \infty} \frac{1}{2\pi} \int_{-\pi}^\pi \frac{1}{N}\left| X_N(e^{j\theta})\right|^2 \mathrm{d}\theta,
    \end{split}
\end{equation}
from which the direct method of calculating the the power spectral distribution follows by comparison with (\ref{eq:power_integral}) as
\begin{equation}\label{eq:pwer_dir}
    \hat{P}_N(e^{j\theta}) = \frac{1}{N}\left|X_N(e^{j\theta})\right|^2 =\frac{1}{N}\left|\sum_{n=0}^{N-1} \tilde{x}[n]e^{-jn\theta}\right|^2 .
\end{equation}
It should be noted that this definition is different from the energy spectral distribution as the spectrum is only calculated using a finite window of length $N$. In order to calculate the true power spectral density $N$ should approach $\infty$.

<br></br>
## Power spectral distribution: indirect method
By expanding the definition of $P_N(e^{j\theta})$, the indirect method of determining the power spectral distribution can be found as
\begin{equation}\label{eq:power_ind}
    \begin{split}
        \hat{P}_N(e^{j\theta})
        &= \frac{1}{N}\left|X_N(e^{j\theta})\right|^2, \newline
        &= \frac{1}{N}X_N(e^{j\theta})X_N^\ast (e^{j\theta}), \newline
        &= \frac{1}{N}\left(\sum\_{n=0}^{N-1} \tilde{x}[n] e^{-jn\theta}\right)\left(\sum\_{p=0}^{N-1} \tilde{x}^\ast [p] e^{jp\theta}\right), \newline
        &= \frac{1}{N}\sum\_{p=0}^{N-1}\sum\_{n=0}^{N-1}\tilde{x}[n]\tilde{x}^\ast[p]e^{-j(n-p)\theta}, \newline
        &\overset{p = n-l}{=} \sum\_{l=- (N-1)}^{N-1}\left(\frac{1}{N}\sum\_{n=0}^{N-1-|l|}\tilde{x}[n]\tilde{x}^\ast[n-|l|]e^{-jl\theta}\right), \newline
        &= \sum\_{l=-(N-1)}^{N-1} \hat{r}_x[l]e^{-jl\theta},
    \end{split}
\end{equation}
where $\hat{r}_x[l]$ is an estimate of the auto-correlation function of $x[n]$. As explained in the reader on random processes and signals, this can be obtained as
\begin{equation}\label{eq:autocorr}
    \hat{r}_x[l] = \frac{1}{N}\sum\_{n=0}^{N-1-|l|}\tilde{x}[n]\tilde{x}^\ast[n-|l|].
\end{equation}
Fig. 2 graphically shows the direct and indirect methods for calculating the power spectral density of a windowed power signal $\tilde{x}[n]$.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/powermethods.svg"
      alt="Graphical overview of the direct and indirect methods for calculating the power spectral density of a windowed power signal."
    />
    <figcaption class="numbered">
      Graphical overview of the direct and indirect methods for calculating the power spectral density of a windowed power signal.
    </figcaption>
  </figure>
</div>


<div class="example">
<h4> Example </h4>
Consider the power signal $x[n] = u[n]$. Calculate the frequency spectrum, auto-correlation function, power spectral density and average power of the windowed signal $x[n]$ for $0\leq n < N-1$.
<button class="collapsible">Show solution</button>
<div class="content">
The frequency spectrum can be calculated as
\begin{equation*}
    \begin{split}
        X_N(e^{j\theta})
        &= \sum_{n=-\infty}^\infty \tilde{x}[n]e^{-jn\theta}, \\
        &= \sum_{n=0}^{N-1} e^{-jn\theta}, \\
        &= \frac{1-e^{-jN\theta}}{1-e^{-j\theta}}, \\
        &= \frac{(e^{j\frac{N}{2}\theta} - e^{-j\frac{N}{2}\theta})e^{-j\frac{N}{2}\theta}}{(e^{j\frac{1}{2}\theta} - e^{-j\frac{1}{2}\theta})e^{-j\frac{1}{2}\theta}}, \\
        &= \frac{2j}{2j}\frac{\sin(\frac{N}{2}\theta)}{\sin(\frac{1}{2}\theta)}e^{-j\frac{N-1}{2}\theta}.
    \end{split}
\end{equation*}
The auto-correlation function for $|l| < N$ can be estimated as
\begin{equation*}
    \begin{split}
        \hat{r}_x[l]
        &= \frac{1}{N} \sum_{n=0}^{N-1-|l|} \tilde{x}[n]\tilde{x}[n-|l|], \\
        &= \frac{1}{N} \sum_{n=0}^{N-1-|l|} 1, \\
        &= \frac{N-|l|}{N}.
    \end{split}
\end{equation*}
The power spectral density can be calculated as
\begin{equation*}
    \hat{P}_N(e^{j\theta}) = \frac{1}{N} | X_N(e^{j\theta})|^2 = \frac{1}{N}\frac{\sin^2(\frac{N}{2}\theta)}{2\sin^2(\frac{1}{2}\theta)}.
\end{equation*}
The average signal power can be determined as
\begin{equation*}
    P_s = \hat{r}_x[0] = 1.
\end{equation*}
</div>
</div>



## Periodic power signals
When analyzing periodic signals, or when the signal is assumed to be periodic with period $N$, for which $x[n] = x[n+N]$ holds, the FTD operations can be replaced with the DFT operation. This allows for more efficient computations, with the consequence of discretizing the frequency domain. Similarly as in the previous subsections the power spectral distribution can be determined <i>directly</i> as
\begin{equation}
    \hat{P}[k] = \frac{1}{N}|X[k]|^2 = \frac{1}{N} \left| \sum_{n=0}^{N-1} \tilde{x}[n] e^{-j\frac{2\pi}{N} kn}\right|^2
\end{equation}
by interchanging the FTD operator with the DFT operator. Using the indirect method the power spectral distribution can be determined from the periodic auto-correlation function ($\hat{r}[l] = \hat{r}[l \mod N]$) as
\begin{equation}
    \hat{P}[k] = \sum_{l=0}^{N-1}\hat{r}[l]e^{-j\frac{2\pi}{N}kl}.
\end{equation}
