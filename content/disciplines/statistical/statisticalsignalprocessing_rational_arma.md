+++
title = "Auto-regressive moving-average signal models "         # name of webpage

# date = {{ .Date }}
lastmod = 2020-07-14

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.

[menu.statistical]                       # name of menu section (main module)
  name = "ARMA signal models"        # name of this item in that menu
  weight = 2                           # location in that menu
  parent = "Rational signal models"

+++
A stochastic processes may be represented by a stochastic model with given order and parameters, which is able to generate a random signal characterized by well-defined spectral properties. In fact, although a stochastic model and process are in principle two different entities, they are sometimes used interchangeably.
Stochastic models are fundamental in many applied fields of science, including engineering, economics and medicine. Among stochastic models, a special class of models known as auto-regressive moving-average (ARMA) is widely used. In this section, we first explain how the statistical properties of a random signal are affected when filtering by LTI; then we discuss random signals with rational spectra and an important representation of a random signal known as the *innovation representation*; finally we provide a more detailed overview of ARMA models.

## LTI with random inputs

When a random signal is filtered by an LTI system, its statistical properties are changed. Focusing on the second-order statistics, here we show the transformation that a discrete random *power* signal undergoes when processed
by a discrete-time LTI system. The difference between *power* and *energy* signal is discussed in the section <a href="../statisticalsignalprocessing_signals_psd">Power Spectral Density</a>.

### Time-domain analysis
The input-output relationship of an LTI system is described using the following convolution
\begin{equation}
\begin{split}
    y[n] = \sum_{k=-\infty}^{\infty} h[k] x[n-k].
    \label{eq::1}
\end{split}
\end{equation}
Here $x[n]$ is a random stationary signal. Output $y[n]$ converges and is stationary if the system represented by the impulse response $h[k]$ is stable. The condition for stability is that $\sum_{-\infty}^{\infty}|h[k]|<\infty$.

The exact output $y[n]$ can not be calculated, since $y[n]$ is a stochastic process. However, certain statistical properties of $y[n]$ can be determined from knowledge of the statistical properties of the input and the characteristics of the system.

The **mean value** of output $y[n]$ can be determined by taking the expected value from both sides of equation (1) as
\begin{equation}
\begin{split}
    \mu_y = \sum_{k=-\infty}^{\infty}h[k]E\{{x[n-k]}\} = \mu_x \sum_{k=-\infty}^{\infty} h[k] = \mu_x H(e^{j0}).
\end{split}
\end{equation}
Note that the filter coefficients are deterministic, and thus $E\\{h[k]\\} = h[k]$.

The **input-output correlation** can also be calculated without knowing the exact output. The input-output correlation is defined as $r_{xy}[l] = E\\{ x[n+l]y^\ast[n]\\}$. Therefore, to calculate this correlation, we take the complex conjugate of (1) and multiply it with $x[n+l]$ before taking the expected value.

\begin{equation}
\begin{split}
    r_{xy}[l] &= E\{ x[n+l]y^\ast[n]\} = \sum_{k=-\infty}^{\infty} h^\ast[k] E\{x[n+l]x^\ast[n-k]\}\newline
    r_{xy}[l] &= \sum_{k=-\infty}^{\infty} h^\ast[k] r_{xx}[l+k] = \sum_{m=-\infty}^{\infty} h^\ast[-m] r_{xx}[l-m]\newline
    r_{xy}[l] &= h^\ast[-l]\star r_{xx}[l]\newline
    r_{yx}[l] &= h^\ast[l]\star r_{xx}[l].\newline
\end{split}
\end{equation}

The **output correlation** can be calculated by multiplying with $y^\ast[n-l]$ and taking the expectation.
\begin{equation}
\begin{split}
    r_{yy}[l] &= E\{y[n]y^\ast[n-l]\} = \sum_{k=-\infty}^{\infty} h[k]E\{x[n-l] y^\ast[n-l]\}\newline
    r_{yy}[l] &= \sum_{k=-\infty}^{\infty} h[k] r_{xy}[l-k] = h[l]\star r_{xy}[l].
\end{split}
\end{equation}

By combining this result with $r_{xy}[l] = h^\ast[-l]\star r_{xx}[l]$ we obtain
\begin{equation}
\begin{split}
    r_y[l] &= h[l]\star h^\ast[-l]\star r_x[l]\newline
    r_y[l] &= r_h[l]\star r_x[l].
\end{split}
\end{equation}

The **output signal power** is equal to $P_y=E\{|y[n]|^2\}=r_y[0]$, which can be calculated using the previous equations,
\begin{equation}
\begin{split}
    P_y&=E\{|y[n]|^2\}=r_y[0]\newline
    &=r_h[l]\star r_x[l=0] = \sum_{k=-\infty}^{\infty} h[k] h^\ast[-k] r_{x}[k],\newline
\end{split}
\end{equation}

where $r_h[l]$ is the autocorrelation of the LTI system with inmpulse response $h[n]$.

Figure 1 describes schematically what the input-output relationship of an LTI system in the time domain and in the "correlation" domain.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/signalmodels/scheme_LTI_AC.bmp"
      alt="LTI with random input"
    />
    <figcaption class="numbered">
     LTI with impulse response h[n], random input $x[n]$ and random output $y[n]$. Input-output relationship in the time and "correlation" domains.
    </figcaption>
  </figure>
</div>

### Transform-domain analysis

The relationships found above in the time domain can be easily transformed in the frequency- and z-domains. Let us first recall some properties of the z-transform.
Given a complex sequence $x[n]$, with z-transform $X(z)$, the following properties apply
\begin{equation}
\begin{split}
    x^\ast[n] \Longleftrightarrow & X^\ast(z^\ast) \newline
    x[n] \Longleftrightarrow & X(1/z) \newline
    x^\ast[-n] \Longleftrightarrow & X^\ast(1/z^\ast) \newline
\end{split}
\end{equation}

Since we are dealing with autocorrelation functions and power spectral densities of mostly real signals, it is also useful to recall that
<ul>
<li> if $x[n]$ is real, then
\begin{equation}
    x[n] = x^\ast[n] \Longleftrightarrow X(z) = X^\ast(z^\ast);  
\end{equation} </li>
<li> if $x[n]$ has even symmetry around the time origin, then
\begin{equation}
    x[n] = x[-n] \Longleftrightarrow X(z) = X(1/z);  
\end{equation}</li>
<li> if $x[n]$ is both real and even, then
\begin{equation}
    x[n] = x^\ast[-n] \Longleftrightarrow X(z) = X^\ast(z^\ast) = X(1/z) = X^\ast(1/z^\ast).  
\end{equation}</li>
</ul>

From the equation above, we can easily the input-output relationships for an LTI system  in the frequency and z-domain,  which are provided in the following table.

| Time Domain                    | Frequency domain                                            | z-domain                          |
|--------------------------------|-------------------------------------------------------------|-----------------------------------|
| $y[n]=h[n]\star x[n]$               | $Y(e^{j\theta})=H(e^{j\theta})X(e^{j\theta})$               | $Y(z)=H(z)X(z)$                   |
| $r_{yx}[l]=h[l]\star r_x[l]$        | $P_{yx}(e^{j\theta})=H(e^{j\theta})R_{x}(e^{j\theta})$      | $P_{yx}(z)=H(z)R_{x}(z)$          |
| $r_{xy}[l]=h^*[-l]\star r_x[l]$     | $P_{xy}(e^{j\theta})=H^*(e^{j\theta})R_{x}(e^{j\theta})$    | $P_{xy}(z)=H^*(1/z^*)P_{x}(z)$    |
| $r_{y}[l]=h[l]\star r_{xy}[l]$      | $P_{y}(e^{j\theta})=H(e^{j\theta})R_{xy}(e^{j\theta})$      | $P_{y}(z)=H(z)R_{xy}(z)$          |
| $r_{y}[l]=h[l]\star h^*[-l]\star r_x[l]$ | $P_{y}(e^{j\theta})=\|H(e^{j\theta})\|^2R_{x}(e^{j\theta})$ | $P_{y}(z)=H(z)H^*(1/z^*)R_{x}(z)$ |

## Innovation representation of a random signal

A rational spectrum is a ratio of two rational functions containing $e^{j\theta}$.
\begin{equation}
\begin{split}
    P(e^{j\theta}) = P(z) = \frac{\sum_{q=-Q}^{Q} r_x[n] e^{-j\theta q}}{\sum_{p=-P}^{P} r_y[n] e^{-j\theta p}}
\end{split}
\end{equation}

Here $r_x$ and $r_y$ are the auto-correlation sequences of two real signals. The rational spectrum is actually derived from the *Wold's decomposition* or *representation theorem*, a very general signal decomposition theorem, which states that every wide sense stationary (WSS) signal can be written as a sum of two components, one deterministic and one stochastic, as given below
\begin{equation}
\begin{split}
    x[n] = \sum_{k=0}^{\infty}h[k]i[n-k] + \hat{x}[n],
\end{split}
\end{equation}

where $h[k]$ represents a infinite-length sequence of weights; $i[n]$ is a white noise sequence, often referred to as *innovations*; $\hat{x}[n]$ is deterministic, thus exactly predictable from the past values. The deterministic part can be subtracted from this signal since it is exactly predictable. This will result in a purely random zero-mean WSS signal as
\begin{equation}
\begin{split}
    x[n] = \sum_{k=0}^{\infty}h[k] i[n-k] = \sum_{k=-\infty}^{n}h[n-k] i[k].
\end{split}
\end{equation}

From here it becomes clear that $x[n]$ can be considered as the outcome of filtering white noise by a stable LTI system, with a rational transfer function in the form of
\begin{equation}
\begin{split}
    H(z) = \frac{B(z)}{A(z)},
\end{split}
\end{equation}
with
\begin{equation}
\begin{split}\label{#eq:AB}
    A(z) = 1 + a_1z^{-1}+ ... + a_pz^{-p}x,\newline
    B(z) = 1 + b_1z^{-1}+ ... + b_qz^{-q}.
\end{split}
\end{equation}
In equation (15), we assume that $a_0 =  1$  and  $b_0 = 1$.

Combining equation (12) with the right-end side of equation (13), where we have reversed the summation, we can also rewrite (13) to obtain a "new" sample of the random signal $x[n]$ as

\begin{equation}
\begin{split}
    x[n+1] =  \underbrace{\sum_{k=-\infty}^{n}h[n+1-k] x[k]}\_{\color{red}{\begin{subarray}{c}\text{Predictable part: linear}\newline
    \text{combination of past information}\end{subarray}}} + \underbrace{i[n+1]}\_{\color{blue}{\begin{subarray}{c}\text{New information}\newline
    \text{(innovation)}\end{subarray}}}.
\end{split}
\end{equation}
The interpretation of  equation (16) is that any new sample of the random signal $x[n]$ is composed of a predictable part obtained by a linear combination of previous samples of $x[n]$ (filtering by LTI), and of an unpredictable  part, which is called innovation (Figure 2).

<div style="max-width: 750px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/signalmodels/innovation_representation.bmp"
      alt="LTI with random input"
    />
    <figcaption class="numbered">
    A random signal $x[n]$ can be described by the combination of a predictable part obtained by filtering previous samples and an unpredictable part, which is called innovation.
    </figcaption>
  </figure>
</div>

In summary, the power spectrum of a WSS random signal can be approximated by a rational polynomial; this is equivalent to describing the signal as the output of a LTI filter, whose input is a zero-mean white noise sequence. If the filter has transfer function $H(z) = B(z)/H(z)$, then the signal can be rewritten as
\begin{equation}
\begin{split}
    x[n] = -\sum_{p=1}^{p}a_p x[n-p] + \sum_{q=0}^{Q}b_q i[n-q].
\end{split}
\end{equation}
From the rational transfer function, the power spectrum of the random signal can be calculated as
\begin{equation}
\begin{split}
    P_{x}(e^{j\omega}) = \sigma_i \frac{|B(e^{j\omega})|^2}{|A(e^{j\omega})|^2} = \sigma_i |H(e^{j\omega})|^2,
\end{split}
\end{equation}
where
\begin{equation}
\begin{split}
    A(e^{j\omega}) = 1 + a_1e^{-j\omega} + ... + a_p e^{-j \omega p},  \newline
    B(e^{j\omega}) = 1 + b_1e^{-j\omega} + ... + b_q e^{-j \omega p}.
\end{split}
\end{equation}

As we shall see in the following section, this means viewing an observed random signal as a stochastic process modeled by an auto-regressive moving-average (ARMA) process, whose rational  spectrum contains the model parameters.

## Auto-regressive (AR) models
Jenkins in
1970 (see Box et al. 2008). The ARMA model was created as a tool for
• detecting, from a finite-length data record, the characteristics of the underlying
random process and thus understanding its nature by revealing something about
the mechanism that builds persistence into the series;
• forecasting future values of the series on the basis of past values;
• if desired, removing from the signal the imprint of some known process, so as to
get a more random residual signal to which statistical methods, such as methods
of spectral estimation, can be applied more pertinently (pre-whitening);
• finally, and more interestingly for our purposes, getting a kind of spectral estimate
derived directly from the stochastic model that best fits the signal, etc.
These goals are tackled exploiting and modeling the persistence exhibited by the
series. Autocorrelated process have memory, that can be long- or short-term, depending
on the rate at which absolute AC decreases as the lag between pairs of signal
samples increases, i.e., depending on the persistence of the AC.4
