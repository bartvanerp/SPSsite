+++
title = "Sampling, reconstruction and multirate signal processing"

# date = {{ .Date }}
lastmod = 2019-12-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling, reconstruction and multirate signal processing"
  weight = 80


+++

## Introduction
Sounds that reach our ears are signals in the form of air pressure. This air pressure is a continuous signal, i.e. it is defined for all time instances and can have any value on a reasonable domain. These kind of signals cannot be stored directly on a computer, which uses numbers to perform calculations. The signal first needs to be approximated in two ways in order to allow for computations on a computer and to limit the required memory.

## Module overview
The concepts covered in this module are:

1. <a href="../discretesignalprocessing_multirate_math">Mathematical description sampling process</a> [⯈] - The conversion of a sample frequency can give rise to several undesired artifacts. The correct filtering of the signal is therefore of crucial importance.
2. <a href="../discretesignalprocessing_multirate_blocks">Basic building blocks of multirate signal processing</a> [⯈] - In order to perform the sample conversion, several common filter architectures can be utilized, which will be discussed in this section.

## Summary

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px">
  A continuous-time signal $x_a(t)$ with frequencies not higher than $f_\text{max}$ can be reconstructed exactly from its samples $x[n] = x_a(t)|_{n \cdot T_s}$, if samples are taken at a rate $f_s=1/T_s$, that is larger than $2f_\text{max}$.
</div>
If the sampling frequency $f_s$ is lower than two times the highest frequency $f_{max}$ of the analog signal $x_a(t)$, an overlap of spectral components may occur and $x_a(t)$ cannot be recovered from its samples $x[n]$.
This overlap in frequency domain is called <b>aliasing</b>.

### C/D conversion
<i>Note: In practice analog LPF needed before input $x_a(t)$ to prevent frequencies $\omega > \frac{\pi}{T_s}$.</i>

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/CDconv.svg"
    />
  </figure>
</div>

\begin{equation}
X(e^{j\theta})= X_s(\omega)|_{\omega=\frac{\theta}{T_s}}=
\frac{1}{T_s} \sum_{k=- \infty}^{\infty} X_a(\frac{\theta}{T_s} - k \cdot \frac{2 \pi}{T_s})
\end{equation}

### D/C conversion
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/DAconv.svg"
    />
  </figure>
</div>

<i> Interpolation equations ideal LPF $H(\omega)$ </i>
\begin{equation}
h(t) = \frac{1}{2 \pi} \int_{-\pi/ T_s}^{\pi/ T_s} T_s e^{j\omega t} \mbox{d} \omega
= \frac{\sin(\frac{\pi}{T_s} t)}{\frac{\pi}{T_s} t}
\end{equation}
\begin{equation}
x_a(t) = x_s(t) \ast h(t) = \sum_{n=-\infty}^{\infty} x[n] \left ( \frac{\sin (\frac{\pi}{T_s} \cdot (t- n T_s))}{\frac{\pi}{T_s} \cdot (t - n T_s)} \right )
\end{equation}
\begin{equation}
X_a(\omega) =
\begin{cases}
T_s \cdot X(e^{j\theta})|_{\theta = \omega T_s} & |\omega| < \frac{\pi}{T_s} \newline
0 & \mbox{ otherwise}
\end{cases}
\end{equation}

<i> Practice D/C conversion: Ideal LPF $\Rightarrow$ Zero Order Hold filter:</i>
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/ZOHDAconv.svg"
    />
  </figure>
</div>

\begin{eqnarray}
h_0(t) =
\begin{cases}
1 & 0 \leq t < T_s \newline
0 & \mbox{otherwise}
\end{cases}
& \circ \hspace{-4px} - \hspace{-4px} \circ &
H_0(\omega) = \frac{\sin (\omega \frac{T_s}{2})}{\omega \frac{T_s}{2}} \cdot e^{-j\omega \frac{T_s}{2}}
\end{eqnarray}

### Relation analog vs discrete-time filter
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/DiscreteAnalogSystem.svg"
    />
  </figure>
</div>

<b> Bandlimited $x(t)$ and LPF in D/C </b>

\begin{equation}
H_a(\omega) =
\begin{cases}
H_d(e^{j\theta})|_{\theta= \omega \cdot T_s} & |\omega| < \frac{\pi}{T_s} \newline
0 & \mbox{otherwise}
\end{cases}
\end{equation}


\begin{equation}
H_d(e^{j\theta}) = H_a(\omega)|_{\omega= \frac{\theta}{T_s}} \mbox{ for } |\theta| < \pi
\end{equation}


### Sample Rate Conversion

#### SRD

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/decimator.svg"
    />
  </figure>
</div>

\begin{equation}
  y[n \cdot T_y] = x[ n \cdot (M \cdot T_x)]
\end{equation}

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/SRD.svg"
    />
  </figure>
</div>

\begin{equation}
Y(e^{j\theta})= \frac{1}{M} \sum_{p=0}^{M-1} X(e^{j(\theta - p \cdot 2 \pi)/M})$
\end{equation}

#### SRI

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/interpolator.svg"
    />
  </figure>
</div>

\begin{equation}
  y[n \cdot T_y] =
  \begin{cases}
  x[ n (T_x/L)] & n=0,\pm L, \cdots \newline
  0 & \mbox{otherwise}
  \end{cases}
\end{equation}

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/SRI.svg"
    />
  </figure>
</div>

\begin{equation}
  Y(e^{j\theta}) = X(e^{jn L  \theta})
\end{equation}
