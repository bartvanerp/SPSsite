+++
title = "Power spectral density"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-05-19

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Power spectral density"        # name of this item in that menu
  weight = 3                           # location in that menu
  parent = "Stochastic processes and random signals"

+++


We previously saw that the auto-correlation function of a zero-mean white noise process was a Dirac delta pulse. The existence of the delta pulse can be proven by the fact that the noise is white, meaning that is uniformly distributed over its power spectrum. In order to make the link between the auto-correlation function and the power spectrum, first the Fourier transform for discrete-time signals needs to be introduced.

<br></br>
## The Fourier transform for discrete-time signals
First it is important to give a quick recap of the Fourier transform for discrete-time signals. A more detailed description of this transform can be found <a href="..\..\..\disciplines\discrete\discretesignalprocessing_transforms_ftd_main">here</a>.

The <i>Fourier transform for discrete-time signals</i> (FTD) is a mathematical operation to calculate the continuous spectrum of a discrete-time signal. This spectrum is periodic because of the uniqueness issue caused by the sampling procedure. Which reflects that we lose high-frequency spectral information due to a sampling rate that is below the Nyquist rate.

The Fourier transform for discrete-time signals is defined as
\begin{equation}
    X(e^{j\theta}) = \sum_{n=-\infty}^\infty x[n]e^{-jn\theta},
\end{equation}
where $x[n]$ is the discrete-time signal and $X(e^{j\theta})$ is the periodic spectrum. Similarly the <i>inverse Fourier transform for discrete-time signals</i> (IFTD) is defined as
\begin{equation}
    x[n] = \frac{1}{2\pi}\int_{-\pi}^\pi X(e^{j\theta})e^{jn\theta}\mathrm{d}\theta.
\end{equation}
In these equations $\theta$ is the normalized frequency defined as
\begin{equation}
    \theta = 2\pi\frac{f}{f_s},
\end{equation}
where $f$ is the signal frequency and $f_s$ the sampling frequency. $\theta$ is periodic with a period of $2\pi$. In practice the Fourier transform for discrete-time signals is often approximated with the fast Fourier transform (FFT), which is beyond the scope of this reader.

<br></br>
## Energy and power of signals
The energy $E_s$ of a signal is defined as the sum of all squared sample magnitudes as
\begin{equation}
    E_s = \sum_{n=-\infty}^\infty |x[n]|^2.
\end{equation}
The average signal power $P_s$ is the average signal energy per sample and is similarly defined as
\begin{equation}
    P_s = \lim_{N\rightarrow \infty} \frac{1}{N}\sum_{n=0}^{N-1} |x[n]|^2,
\end{equation}
where a total of $N$ samples are averaged over.

If an infinitely long signal has finite signal energy it is called an <i>energy signal</i>. Since the energy is finite and the time duration infinite, the average signal power is zero. An example of an energy signal is a short pulse that is transmitted only once.
An infinitely long signal that has a finite average signal power is called a <i>power signal</i>. Because of the finite power that the signal carries over an infinitely long time, the total signal energy is also infinity. Any non-zero bounded signal that is infinitely-long can be regarded as a power signal.

<br></br>
## Power spectral density
The average signal power yields a limited amount of information, because it is just a single number. Oftentimes it is desirable to know what frequencies are contributing the most to this signal power. This would for example allow for the detection of unwanted signals that cause interference. It is possible to calculate the <i>power spectral density</i> (PSD) of a signal from its Fourier transform of discrete-time signals, which represents the distribution of the signal power of the frequency spectrum. The power spectral density $P_X(e^{j\theta})$ is defined as the expected value of the squared Fourier transform of $x[n]$, normalized with the number of signal samples as
\begin{equation}\label{eq:psd}
    P_X(e^{j\theta}) = \lim_{N\rightarrow \infty} \frac{1}{2N+1} \mathrm{E}\left[\Big| \sum_{n=-N}^N x[n]e^{-jn\theta}\Big|^2\right].
\end{equation}
If the signal $x[n]$ is real-valued, then the power spectral density is symmetric around its DC component (i.e. $P_X(e^{j\theta}) = P_X(e^{-j\theta})$). Furthermore the power spectral density is always non-negative and periodic with a period of $2\pi$ similarly to $X(e^{j\theta})$. Averaging the area under the power spectral density function will return the average signal power as
\begin{equation}
    P_s = \frac{1}{2\pi} \int_{-\pi}^\pi P_X(e^{j\theta})\mathrm{d}\theta.
\end{equation}

<br></br>
## The power spectral density and the correlation function
What makes the power spectral density so important in the context of this reader, which is mainly about random processes and signals? The answer is given by the <i>Wiener-Khinchin theorem</i>, which states that the power spectral density of a wide-sense stationary signal is the Fourier transform of its auto-correlation function as
\begin{equation}\label{eq:psdcorr}
    P_X(e^{j\theta}) = \sum_{l=-\infty}^\infty r_X[l]e^{-jl\theta}.
\end{equation}
Similarly holds the opposite
\begin{equation}\label{eq:corrpsd}
    r_X[l] = \frac{1}{2\pi} \int_{-\pi}^\pi P_X(e^{j\theta})e^{jl\theta} \mathrm{d}\theta.
\end{equation}

### Example
Suppose we would like to calculate the power spectral density of a zero-mean wide-sense stationary random process $x[n]$, whose auto-correlation function is given as $r_X[l] = \alpha^{|l|}$ with $-1 <\alpha <1$.

Using the above equation the power spectral density can be determined as
\begin{equation}
    \begin{split}
        P_X(e^{j\theta})
        &= \sum_{l=-\infty}^\infty r_X[l]e^{-jl\theta}, \newline
        &= \sum_{l=-\infty}^0 r_X[l]e^{-jl\theta} + \sum_{l=0}^\infty r_X[l]e^{-jl\theta} - r_X[0]e^{-j0\theta}, \newline
        &= \sum_{p=0}^\infty r_X[-p]e^{jp\theta} + \sum_{l=0}^\infty r_X[l]e^{-jl\theta} - 1, \newline
        &= \sum_{p=0}^\infty \left(\alpha e^{j\theta}\right)^p + \sum_{l=0}^\infty \left(\alpha e^{-j\theta}\right)^l - 1, \newline
        &= \frac{1}{1-\alpha e^{j\theta}} + \frac{1}{1-\alpha e^{-j\theta}} - 1, \newline
        &= \frac{1-\alpha e^{-j\theta} + 1-\alpha e^{j\theta} - \left(1-\alpha e^{j\theta}\right)\left(1-\alpha e^{-j\theta}\right)}{\left(1-\alpha e^{j\theta}\right)\left(1-\alpha e^{-j\theta}\right)}, \newline
        &= \frac{1-\alpha^2}{1+\alpha^2 -2\alpha\cos(\theta)}.
    \end{split}
\end{equation}

<br></br>

<div class="example">
<h4> Exercise </h4>
<hr>
Given the following autocorrelation sequences. Find the PSD and verify that this function is real and nonnegative
<ol type="a">
	<li> $\rho[\tau]=3-|\tau|$ for $|\tau| \leq3$ and $\rho[\tau]=0$ elsewhere.</li>
	<li> $\rho[\tau]=2(-0.6)^{|\tau}|+\delta [\tau]$.</li>
</ol>
<button class="collapsible">Show solution</button>
<div class="content">
<ol type="a">
	<li>
  \begin{equation*}
\begin{split}
    P(\mbox{e}^{\mbox{j} \theta}) &= \sum_{\tau = - \infty}^{\infty} \rho[\tau ] \mbox{e}^{-\mbox{j} \tau \theta}\\
    &= \sum_{\tau = - 3}^{3} (3-|\tau|) \mbox{e}^{-\mbox{j} \tau \theta}\\
    &= \sum_{\tau = - 3}^{-1} (3+\tau) \mbox{e}^{-\mbox{j} \tau \theta} + \sum_{\tau = 1}^{3} (3-\tau) \mbox{e}^{-\mbox{j} \tau \theta} + (3-0)\mbox{e}^{-\mbox{j} 0 \theta}\\
    &= \mbox{e}^{\mbox{j} 2 \theta} + 2\mbox{e}^{\mbox{j} \theta} + 2\mbox{e}^{-\mbox{j} \theta} + \mbox{e}^{-\mbox{j} 2 \theta} + 3\\
    &=3 + 4 \cos (\theta) + 2 \cos ( 2\theta )\\
\end{split}
\end{equation*}</li>
	<li>
  \begin{equation*}
\begin{split}
    P(\mbox{e}^{\mbox{j} \theta}) &= \sum_{\tau = - \infty}^{\infty} \rho[\tau ] \mbox{e}^{-\mbox{j} \tau \theta}\\
    &= \sum_{\tau = - \infty}^{\infty} \delta[\tau] \mbox{e}^{-\mbox{j} \tau \theta} + 2\sum_{\tau = - \infty}^{\infty} (-0.6)^{|\tau|} \mbox{e}^{-\mbox{j} \tau \theta}\\
    &= 1 + 2\left( \sum_{\tau = - \infty}^{0} (-0.6)^{-\tau} \mbox{e}^{-\mbox{j} \tau \theta} + \sum_{\tau = 0}^{\infty} (-0.6)^{\tau} \mbox{e}^{-\mbox{j} \tau \theta} - 1 \right)\\
    &= 1 + 2\left( \sum_{\tau = 0}^{\infty} (-0.6)^{\tau} \mbox{e}^{\mbox{j} \tau \theta} + \sum_{\tau = 0}^{\infty} (-0.6)^{\tau} \mbox{e}^{-\mbox{j} \tau \theta} - 1 \right)\\
    &= 1 + 2\left( \frac{1}{1+0.6 \mbox{e}^{\mbox{j} \theta}} + \frac{1}{1+0.6 \mbox{e}^{\mbox{-j} \theta}} - 1\right)\\
    &= 1 + 2\left( \frac{0.64}{1.36 - 1.2 \cos (\theta)}\right) = 1 +  \frac{1.28}{1.36 - 1.2 \cos (\theta)}
\end{split}
\end{equation*}
Both functions of (a) and (b) are indeed real and $\geq 0$.</li>
</ol>
</div>
</div>

## Cross-power spectral density
The power spectral density as discussed up until now was just the auto power spectral density, since it corresponded with the auto-correlation function. Similarly the cross-power spectral density of two random processes can be defined, showing the relationship between two random processes in the frequency domain as
\begin{equation}
    P_{XY}(e^{j\theta}) = \sum_{l=-\infty}^\infty r_{XY}[l]e^{-jl\theta}\ \ \circ\hspace{-1.3mm} - \hspace{-1.3mm}\circ \ \ r_{XY}[l] = \frac{1}{2\pi}\int_{-\pi}^{\pi} P_{XY}(e^{j\theta})e^{jl\theta}\mathrm{d}\theta.
\end{equation}
Because of the complex conjugate symmetry property of the correlation function we may at the same time conclude that
\begin{equation}
    r_{XY}[l] = r_{YX}^\ast [-l] \ \ \circ\hspace{-1.3mm} - \hspace{-1.3mm}\circ \ \  P_{XY}(e^{j\theta}) = P_{YX}^\ast (e^{j\theta}).
\end{equation}

<br></br>
## Coherence functions
As was already discussed in the section on the correlation coefficient, the cross-correlation function depends a lot on the individual signal amplitudes. This is also the case for the cross-power spectral density function. In order to generalize the cross-power spectral density function for all types of signals, the coherence function is introduced as
\begin{equation}
    C_{XY}(e^{j\theta}) = \frac{P_{XY}(e^{j\theta})}{\sqrt{P_{X}(e^{j\theta})}\sqrt{P_{Y}(e^{j\theta})}}
\end{equation}
which normalizes the cross-power spectral density function. The absolute value of this function is bounded between 0 and 1, which reflects respectively no correlation and total correlation to the point where $x[n]=y[n]$.
