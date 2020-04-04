+++
title = "Transforms I: Fourier transform for discrete-time signals"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "From FTC to FTD"
  weight = 1
  parent = "Transforms I: Fourier transform for discrete-time signals"

+++

## Alternative expression pulse train
In the module sampling and reconstruction we have seen that the continuous time signal $x(t)$ can be represented by samples $x[n]$ when these samples are obtained by using an ideal <a href="../../discrete/discretesignalprocessing_sampling_samplingprocess">C-to-D convertor</a> which runs at a sampling frequency $f\_s$ which is larger than 2 times the maximum frequency $f_\text{max}$ of the continuous time signal $x(t)$. Here we will assume that this is the case, so there is no <a href="../../discrete/discretesignalprocessing_sampling_uniqueness">aliasing</a>.

In the development of the FTD we will use the model of an ideal <a href="../../discrete/discretesignalprocessing_sampling_samplingprocess">C-to-D convertor</a> as depicted in Fig. 1. In this model we first represent the discrete-time samples $x[n]$ by the continuous time signal $x_s(t)$, which is obtained by multiplying the continuous time signal $x(t)$ by a continuous-time signal $s(t)$ which is an infinite train of continuous-time delta pulses with an inter-pulse distance of $T_s=1/f_s$ seconds.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/CDconv.svg"
      alt="Model of an ideal C-to-D convertor."
    />
    <figcaption class="numbered">
      Model of an ideal C-to-D convertor.
    </figcaption>
  </figure>
</div>

Although this intermediate continuous-time signal $x_s(t)$ can never be realized in practice, it is very useful in the following conceptual derivation of the FTD.

In the module <a href="../../continuous/continuoussignalprocessing_transforms_ftc">Fourier Transform for Continuous-time signals</a> we have derived the following alternative expression for this infinite train of continuous-time delta pulses $s(t)$ as an infinite sum of phasors:
$$ s(t)=\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T_s) \hat{=} \frac{1}{T_s} \sum\_{k=-\infty}^{\infty} e^{j\frac{2 \pi }{T_s} k t} $$
The reasoning behind this equality can be shown by Fig. 2.
The figure at the left hand side indicates an example of the phasor terms of the summation for any continuous time variable $t$ which is not equal to $n \times T_s$.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/Phasors0.svg"
    style="width:100%">
    <figcaption>
      Distribution of delta pulses over the unit circle.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/Phasors1.svg"
    style="width:100%">
    <figcaption>
      Distribution of delta pulses on top of each other.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  Summation of an infinite train of continuous-time delta pulses.
</figcaption>
</figure>


In such cases, the phasors terms in the summation, which are unit length vectors, can have any angle. There will be an infinite amount of these unit length vectors with positive imaginary part, colored in blue, and with negative imaginary part, colored in red.
As a result of this infinite amount of vectors, for each blue vector there will be a red vector in opposite direction which cancel each other and the result is that the summation of all these phasors will add up to zero.
Only for values of the continuous-time variable $t \neq n \times T_s$, all phasor terms of the summation are equal to one and are all on top of each other. The result of the summation for this case is infinite, which is indicated at the right hand side of the figure.
Thus the infinite summation of phasors can indeed be represented by an infinite train of delta pulses with an inter distance of $T_s$ seconds, as depicted in the equation above.

In the following subsection we will use this equality in the derivation of the FTD.

## FTD concept
In this subsection we will derive the FTD by using frequency domain descriptions of signals $x(t), x_s(t)$ and $x[n]$, as indicated in Fig. 1 of the mathematical model of the ideal C-to-D convertor.

Assume we are given a continuous time signal $x(t)$ and its FTC $X(\omega)$. The maximum radian frequency of $x(t)$ is $\omega_m$, as depicted in the top figure Fig. 3.


<figure>
<div class="collumnimg3">
  <div class="rowimg3">
    <img src="/../files/7.Images/discrete/transforms/FTD/sampling0.svg"
    style="width:100%">
  </div>
  <div class="rowimg3">
    <img src="/../files/7.Images/discrete/transforms/FTD/sampling1bgreen.svg"
    style="width:100%">
  </div>
  <div class="rowimg3">
    <img src="/../files/7.Images/discrete/transforms/FTD/sampling2.svg"
    style="width:100%">
  </div>
</div>
<figcaption class="numbered">
  Spectra of the different steps of the C-to-D convertor.
</figcaption>
</figure>

As a result of the definition of an impulse train we can write the intermediate continuous-time signal $x_s(t)$ as follows:
$$
x_s(t)= x(t) \cdot \frac{1}{T_s} \sum\_{k=-\infty}^{\infty} e^{j\frac{2 \pi }{T_s} k t}
=\frac{1}{T_s} \sum\_{k=-\infty}^{\infty} x(t) \cdot e^{j\omega_s k t} \quad \text{with} \quad \omega_s =\frac{2 \pi }{T_s}
$$
This equation allows us to apply the frequency shift property to obtain the FTC of $x_s(t)$:
$$
X_s(\omega) = \frac{1}{T_s} \cdot \sum\_{k=-\infty}^{\infty} X(\omega - k \cdot \omega_s),
$$
which is a periodic function of $\omega$ with period $\omega_s = \frac{2 \pi}{T_s}$.
As depicted in the middle figure of Fig. 3, $X_s(\omega)$ (in green) gives the spectral representation of $x_s(t)$ in terms of shifted copies of $X(\omega)$, the FTC of the continuous-time signal $x(t)$.
On the other hand if we express $x_s(t)$ as an infinite train of continuous-time delta pulses $x_s(t)=x(t) \cdot \sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T_s)$ and using the delay property of the FTC, it follows that an equivalent relation for $X_s(\omega)$ can be given by the following equation:
$$
X_s(\omega) = \sum\_{n=-\infty}^{\infty} x(t)\Bigg | \_{t=nT_s} e^{-j\omega n T_s}
$$
which expresses $X_s(\omega)$ in terms of the sampled values $x(t)\mid\_{t=nT_s}$ of the continuous-time signal $x(t)$. Because of the exponential functions, as well as the description of $X_s(\omega)$ this form of $X_s(\omega)$ is periodic in $\omega$ with period $\omega_s = \frac{2 \pi}{T_s}$. Furthermore by representing the sampled values $x(t)\mid\_{t=nT_s}$ by the samples $x[n]$ and using the relative frequency $\theta = \omega \cdot T_s$ we can rewrite the above equation as:
$$
X(e^{j\theta})= \sum\_{n=-\infty}^{\infty} x[n] e^{-jn\theta}
$$
in which the periodicity of this function is denoted by expressing the continuous function variable $\theta$ as an exponent. This equation transforms the discrete-time samples $x[n]$ into a continuous periodic relative frequency domain function $X(e^{j\theta})$ and as such it represents the Fourier Transform of Discrete-time signals (FTD). From the equivalence of the spectra $X_s(\omega)$ and $X(e^{j\theta})$ it follows that the FTD can be viewed in terms of shifted copies of $X(\omega)$. Finally, as depicted in the lower figure of Fig. 3, it follows from $\theta = \omega \cdot T_s$ that the period of $X(e^{j\theta})$ is equal to $2\pi$. Only one period is necessary to represent $X(e^{j\theta})$, which is called the <a href="../../discrete/discretesignalprocessing_sampling_uniqueness/#the-fundamental-interval-fi">Fundamental Interval</a> (FI). In most cases we will use for the FI the period in between $-\pi$ and $+\pi$.

## Inverse FTD
By using the fact that $X(e^{j\theta})$ is a periodic function we can use the <a href="../../continuous/continuoussignalprocessing_transforms_fs/#fourier-series">Fourier Series</a> (FS) representation to find inverse of the FTD expression. For this reason we recall the FS definition which implies that any periodic function $x_p(t)$, with period $T_0=1/F_0$, can be represented as an infinite sum of weighted phasors while in the inverse case the weights $\alpha_k$ can be evaluated by an integral over one period, as denoted in the following equations:
$$
x\_p(t) = \sum\_{k=-\infty}^{\infty} \alpha\_k e^{j2 \pi k F\_0 t}
\hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} \alpha_k = \frac{1}{T_0} \int\_{-T\_0/2}^{T\_0/2} x\_p(t) e^{-j2 \pi k F\_0 t} \mathrm{d}t
$$

In our case we change time and frequency dimensions of the FS equations. Furthermore the periodic function is $X(e^{j\theta})$ with period $2\pi$ and the 'weights' are represented by the samples $x[n]$. Now by using the FS equation for the 'weights' $x[n]$ this results in the following expression for the Inverse FTD:
$$\label{Eq:IFTD}
x[n]=\frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \text{d} \theta
$$
Given the periodic expression $X(e^{j\theta})$ as a function of the continuous relative frequency $\theta$ this equation defines the way to compute the discrete-time samples $x[n]$.

## Differences FTC and FTD
Both FTC and FTD have similarities but are different. That is why the most important aspects of both transformations are summarized here.

Based on absolute frequency $f$ in Hertz, the FTC and IFTC equations are:
$$
\begin{eqnarray*}
{\bf FTC:} \quad X(f) = \int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \mathrm{d} t
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} & x(t) = \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \mathrm{d} f
\end{eqnarray*}
$$
which alternatively can be expressed based on the absolute radian frequency $\omega$ in radians per second as follows:
$$
\begin{eqnarray*}
{\bf FTC:} \quad X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \mathrm{d} t
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \mathrm{d} \omega
\end{eqnarray*}
$$

Important aspects of these transforms are:
<ul>
<li>The continuous time signal $x(t)$ is not periodic, </li>
<li> The frequency representation $X(\omega)$ is a continuous function and not periodic, </li>
<li> Both FTC and IFTC are evaluated by an integral, </li>
<li> Finally we will use these notations for the FTC and IFTC:
$$
X(\omega)=\mathscr{F}\left\{x(t)\right\} \text{   and   } x(t)=\mathscr{F}^{-1} \left\{ X(\omega)\right\}
$$ </li>
</ul>

The FTD and IFTD equations are as follows:
$$
\begin{eqnarray*}
{\bf FTD:} \quad X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} & x[n] = \frac{1}{2 \pi} \int\_{-\pi}^{\pi} X(e^{j\theta}) e^{jn \theta} \mathrm{d} \theta
\end{eqnarray*}
$$
Important aspects of these transforms, which differ from the FTC and IFTC equations, are:
<ul>
<li> The signal samples $x[n]$ are discrete in time and not periodic, </li>
<li> The normalized frequency $\theta = \omega \cdot T_s$,</li>
<li> The Fundamental Interval is usually chosen as: $-\pi \leq \theta < \pi$,</li>
<li> The frequency representation $X(e^{j\theta})$ is a continuous function and periodic,</li>
<li> The FTD is evaluated over an infinite summation of samples $x[n]$,</li>
<li> The IFTD is evaluated by an integral over one period of the frequency representation $X(e^{j\theta})$.</li>
<li> Finally, to make a clear distinction we will use the following notations for the FTD and IFTD:
$$
X(e^{j\theta})=\mathcal{F}\left\{x[n]\right\} \text{   and   } x[n]=\mathcal{F}^{-1} \left\{ X(e^{j\theta})\right\}
$$</li>
</ul>
