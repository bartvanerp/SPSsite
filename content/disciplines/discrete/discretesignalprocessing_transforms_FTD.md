+++
title = "Fourier transform for discrete-time signals"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Fourier transform for discrete-time signals"
  weight = 51
  parent = "Discrete-time transforms"


+++

## From FTC to FTD


### Conceptual video
<iframe width="100%" height="450" src="https://www.youtube.com/embed/Av5_OuNjB4o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In <a href="../../continuous/continuoussignalprocessing_transforms_ftc">a previous module</a> we have seen how we can describe a continuous-time signal in frequency domain with the <a href="../../continuous/continuoussignalprocessing_transforms_ftc">Fourier Transform for Continuous-time signals (FTC)</a>. A similar approach is also possible for discrete-time signals if we take into account the specific property that such a signal is defined only at discrete instances of time and not in between.
The resulting description in frequency domain is the so called Fourier Transform for Discrete-time signals (FTD). Most of the derivations are not formal but have an intuitive character based on physical insight.

### Alternative expression pulse train
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

### FTD concept
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

### Inverse FTD
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

### Differences FTC and FTD
Both FTC and FTD have similarities but are different. That is why the most important aspects of both transformations are summarized here.

Based on absolute frequency $f$ in Hertz, the FTC and IFTC equations are:
$$
\begin{eqnarray}
{\bf FTC:} \quad X(f) = \int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \mathrm{d} t
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} & x(t) = \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \mathrm{d} f
\end{eqnarray}
$$
which alternatively can be expressed based on the absolute radian frequency $\omega$ in radians per second as follows:
$$
\begin{eqnarray}
{\bf FTC:} \quad X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \mathrm{d} t
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \mathrm{d} \omega
\end{eqnarray}
$$

Important aspects of these transforms are:
<ul>
<li>The continuous time signal $x(t)$ is not periodic, </li>
<li> The frequency representation $X(\omega)$ is a continuous function and not periodic, </li>
<li> Both FTC and IFTC are evaluated by an integral, </li>
<li> Finally we will use these notations for the FTC and IFTC:
$$\label{Eq:NotationFTC}
X(\omega)=\mathscr{F}\left\\{x(t)\right\\} \text{   and   } x(t)=\mathscr{F}^{-1} \left\\{ X(\omega)\right\\}
$$ </li>
</ul>

The FTD and IFTD equations are as follows:
$$
\begin{eqnarray}
{\bf FTD:} \quad X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
& \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} & x[n] = \frac{1}{2 \pi} \int\_{-\pi}^{\pi} X(e^{j\theta}) e^{jn \theta} \mathrm{d} \theta
\end{eqnarray}
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
X(e^{j\theta})=\mathcal{F}\left\\{x[n]\right\\} \text{   and   } x[n]=\mathcal{F}^{-1} \left\\{ X(e^{j\theta})\right\\}
$$</li>
</ul>

## FTD Examples

<iframe width="100%" height="450" src="https://www.youtube.com/embed/3yPFxOeVN9s" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This section discusses some important examples of the FTD and IFTD.
To gain more skill with this transformation, it is useful to first elaborate some of these examples yourself.

### FTD and IFTD Delta function
One of the signals that is used most often is the discrete-time delta function $x[n]=\delta[n]$.
Because of the fact that this function is only 1 for index $n=0$ and zero for all other indices, the FTD results into 1 as shown in the following equation:
$$
X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta} = \sum\_{n=-\infty}^{\infty} \delta[n] e^{-jn \theta} = 1 \hspace{3mm} \forall \ \theta
$$
This implies that a delta function in time domain contains all frequencies $\theta$ in frequency domain. This effect is represented in the Fig. 4.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDDelta.svg"
      alt="FTD of delta function $x[n]=\delta[n]$."
    />
    <figcaption class="numbered">
      FTD of delta function $x[n]=\delta[n]$.
    </figcaption>
  </figure>
</div>



On the other hand the IFTD of a frequency domain delta function $X(e^{j\theta})=2 \pi \delta(\theta)$ results also in a constant 1 for all integer values of the index $n$ as follows from the following equation:
$$
x[n] = \frac{1}{2 \pi} \int\_{-\pi}^{\pi} \left( 2 \pi \delta(\theta) \right) e^{jn\theta}
\mathrm{d} \theta = 1 \hspace{3mm} \forall \quad  n \quad \widehat{=} \sum\_{p=-\infty}^{\infty} \delta[n-p]
$$
In other words the result represents an infinite train of discrete time delta pulses $\sum\_{p=-\infty}^{\infty} \delta[n-p]$. Furthermore, because of the periodicity of the frequency representation $X(e^{j\theta})$, with period $2\pi$, we should realize that the delta function in frequency domain $2 \pi \delta(\theta)$ in fact consists of an infinite train of delta functions $
\sum\_{k=-\infty}^{\infty} 2 \pi \delta(\theta + k \cdot 2 \pi)$, which is denoted in Fig. 5.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/IFTDDelta.svg"
      alt="IFTD of delta function $X(e^{j\theta})=2 \pi \delta(\theta)$."
    />
    <figcaption class="numbered">
      IFTD of delta function $X(e^{j\theta})=2 \pi \delta(\theta)$.
    </figcaption>
  </figure>
</div>

Finally note the difference between a discrete-time delta pulse $\delta[n]$ and a continuous-time delta function $\delta(\theta)$. The first on $\delta[n]$ is a discrete function which is equal to 1 for index $n=0$, zero for all other indices and not defined for non-integer indices.  The second delta pulse $\delta(\theta)$ is a continuous function which defined as finite for $\theta=0$ and zero for all other values of the function variable $\delta(\theta)$.

Previously we have derived an alternative expression for an infinite train of continuous-time delta pulses which resulted in the expression
$$
s(t)=\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T_s) \hat{=} \frac{1}{T_s} \sum\_{k=-\infty}^{\infty} e^{j\frac{2 \pi }{T_s} k t}.
$$
Based on the result above we will derive in the following subsection the counterpart of such a continuous-time pulse train for the discrete-time case.

### Discrete Phasor Property (DPP)
From the result of the previous subsection it follows that the IFTD  of $2\pi \delta(\theta)$ results in an infinite train of discrete-time delta functions
$$
\mathcal{F}^{-1} \{ 2\pi \delta (\theta)\} = \sum\_{p=-\infty}^{\infty} \delta[n-p]
$$
The other way around: The function $2\pi \delta(\theta)$ can be obtained by the FTD of an infinite train of discrete time delta functions,  which writes as follows:
$$
2\pi \delta (\theta) = \mathcal{F} \{ \sum\_{p=-\infty}^{\infty} \delta[n-p] \}
=\sum\_{n=-\infty}^{\infty} \left( \sum\_{p=-\infty}^{\infty} \delta[n-p] \right) e^{-jn \theta}
$$
Because of linearity we may interchange the summations. The resulting inner summation, between brackets, is always zero except for the index $n=p$,  which results in a summation of discrete phasors:
$$
2\pi \delta (\theta) =
\sum\_{p=-\infty}^{\infty} \left(\sum\_{n=-\infty}^{\infty} \delta[n-p]
 e^{-jn \theta} \right) = \sum\_{p=-\infty}^{\infty} e^{-jp \theta}
 $$
As mentioned before, because of the periodic behavior of the frequency representation, the delta pulse $2\pi \delta(\theta)$ represents an infinite train of delta pulses. From this we obtain the following so called Discrete Phasor Property (DPP), which can be viewed as a counterpart of the pulse train.
$$
{\bf{\text{ DPP:}}} \hspace{5mm} \sum\_{p=-\infty}^{\infty} e^{-jp \theta} = \sum\_{k=-\infty}^{\infty} 2 \pi \delta(\theta + k \cdot 2 \pi)
$$
This DPP equation shows that we can express a non converging summation, at the left-hand side, into an infinite sum of delta pulses, at the right-hand side.

### FTD of discrete-time sinusoidal

<div class="example">
<h4> Example </h4>
<hr>

In this example we use the DPP property of the previous subsection to show that the FTD of a sinusoidal signal results in the following expression:
$$
x[n]=\cos(n \theta_0) \hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm}
\pi \delta(\theta - \theta_0) + \pi \delta(\theta + \theta_0)
$$
as depicted in Fig. 6.

<button class="collapsible">Show solution</button>
<div class="content">

The first step is to use Euler and write the function as a sum of two, discrete time phasors $\cos(n \theta_0) = \frac{1}{2} e^{jn \theta_0} + \frac{1}{2} e^{-jn \theta_0}$.
From the DPP property it follows that the FTD of the first phasor results in $2\pi$ times a delta pulse at $\theta=\theta_0$  and the second one in $2\pi$ times a delta pulse at $\theta=-\theta_0$:
\begin{eqnarray*}
\mathcal{F} \{ e^{jn \theta_0} \} &=& \sum_{n=-\infty}^{\infty} e^{jn \theta_0} e^{-jn \theta} =
\sum_{n=-\infty}^{\infty} e^{-jn(\theta -\theta_0)}
\overset{\text{DPP}}{=} 2 \pi \delta(\theta - \theta_0) \\
\mathcal{F} \{ e^{-jn \theta_0} \}&=&\sum_{n=-\infty}^{\infty} e^{-jn \theta_0} e^{-jn \theta} = \sum_{n=-\infty}^{\infty} e^{-jn(\theta +\theta_0)}
\overset{\text{DPP}}{=} 2 \pi \delta(\theta + \theta_0)
\end{eqnarray*}
From this it follows that the FTD of the sinusoidal function with frequency $\theta = \theta_0$  results in two delta functions at frequencies $\theta = \pm \theta_0$
\begin{eqnarray}
\Rightarrow \text{ } \mathcal{F} \{ \cos(n \theta_0) \} &=&
\mathcal{F} \left\{ \frac{1}{2} e^{jn \theta_0} \right\} + \mathcal{F} \left\{ \frac{1}{2} e^{-jn \theta_0} \right\} \nonumber \\
&=& \pi \delta(\theta - \theta_0) + \pi \delta(\theta + \theta_0)
\end{eqnarray}
which is represented in Fig. 6.</div>
</div>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDCos2Deltas.svg"
      alt="FTD of sinusoidal signal $\cos(n \theta_0)$."
    />
    <figcaption class="numbered">
      FTD of sinusoidal signal $\cos(n \theta_0)$.
    </figcaption>
  </figure>
</div>


### FTD of exponential decaying function
<div class="example">
<h4> Example </h4>
<hr>

In this example we will calculate the FTD $X(e^{j\theta})$ of a discrete time exponential decaying function $x[n]=a^n u[n]$, with $u[n]$ the unit step function. Furthermore we will sketch a plot of $|X(e^{j\theta})|$ in the Fundamental Interval (FI) for $0 < a < 1$ and $-1 < a < 0$ and give a reasoning for the difference between these two plots.

<button class="collapsible">Show solution</button>
<div class="content">


The FTD can be calculated as given in the following equations:
\begin{eqnarray}
X(e^{j\theta}) &=& \sum_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
= \sum_{n=-\infty}^{\infty} a^n {\color{red}u[n]} e^{-jn \theta}= \sum_{n={\color{red}0}}^{\infty} a^n  e^{-jn \theta} \nonumber \\
&=& \sum_{n=0}^{\infty} \left( a e^{-j\theta} \right) ^n
= \frac{1}{1 - a e^{-j\theta}} \hspace{3mm} |a| < 1
\end{eqnarray}
Because of the unit step function $u[n]$, the summation starts at index $n=0$.  Combining the parameter $a$ and the exponent results in the argument of a summation from which the running index $n$ ranges from zero to infinity. The argument of the summation is taken to a power of $n$. This is a well known geometric series which writes as  one divided by 1 minus the
argument of the summation.  The geometric series do only converge when the absolute value of the argument is smaller than 1. Otherwise the geometric series will diverge. Because of the fact that the amplitude of the complex exponent equals one, this implies that the absolute value of the parameter $a$ has to be smaller than 1.

A plot of a discrete time exponential decaying function $x[n]=a^n u[n]$, with $u[n]$ the unit step function and positive real parameter $a$ ($0 < a < 1$) is depicted at the left-hand side of the figure below.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDposexp.svg"
      alt="FTD of exponential decaying function with positive parameter $a$."
    />
    <figcaption>
      FTD of exponential decaying function with positive parameter $a$.
    </figcaption>
  </figure>
</div>


For positive values of $a$ smaller than 1, a plot of $|X(e^{j\theta})|$ is given at the right-hand side of the figure above.

For negative values of $a$ larger than -1,  a plot of the absolute value of the FTD is given in
the figure below. The speed of fluctuations in this second sequence of samples with negative parameter $a$ are higher in comparison to the first sequence of samples with positive parameter $a$. This effect is reflected in the FTD plots: The second FTD plot shows high frequency behavior, while the first FTD plot represents a low frequency behavior.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDnegexp.svg"
      alt="FTD of exponential decaying function with negative parameter $a$."
    />
    <figcaption>
      FTD of exponential decaying function with negative parameter $a$.
    </figcaption>
  </figure>
</div>

</div>
</div>


### IFTD Block function
One of the filters which is used in many practical situations is a Low Pass Filter (LPF). Mathematically we can represent such an ideal LPF with a block function with a cut off frequency $\theta_c$. In the pass area the value of the frequency function is equal to 1, and in the attenuation area the value is zero. An example with $\theta_c=\frac{\pi}{2}$ is depicted at the right-hand side of Fig. 7.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/IFTDBlock.svg"
      alt="IFTD of a block function with cutoff frequency $\theta_c=\frac{\pi}{2}$."
    />
    <figcaption class="numbered">
      IFTD of a block function with cutoff frequency $\theta_c=\frac{\pi}{2}$.
    </figcaption>
  </figure>
</div>


<div class="example">
<h4> Example </h4>
<hr>

In this example we will show that the IFTD of the LPF results in the following Sinc-function:
$$
x[n] = \frac{\theta_c}{\pi} \cdot \frac{\sin(\theta_c n)}{\theta_c n}
$$

<button class="collapsible">Show solution</button>
<div class="content">

With the ideal LPF as depicted at the right-hand side of Fig. 7, the integral of the IFTD equation reduces to an integral of a complex exponent within boundaries $\pm \theta_c$.
$$
x[n] = \frac{1}{2 \pi} \int_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \text{d} \theta
= \frac{1}{2 \pi} \int_{{\color{red}-\theta_c}}^{{\color{red}\theta_c}} {\color{red}1} e^{jn\theta} \text{d} \theta
$$
Changing the function variable $\theta$ of the integral into $j n \theta$ leads to the given equation:
$$
x[n] =\frac{1}{2 \pi j n } \int_{-\theta_c}^{\theta_c} e^{jn\theta} \text{d} (j n \theta)
$$
Using the boundaries and  combining the two phasors in the numerator as a sinusoidal, results in an expression  which is a so called Sinc-function:
\begin{eqnarray}
x[n] &=& \frac{1}{2 \pi j n} e^{jn\theta}\mid_{- \theta_c}^{\theta_c}
= \frac{1}{2 \pi j n} \left( e^{jn\theta_c} - e^{-jn\theta_c} \right)
= \frac{\theta_c}{\pi} \cdot \frac{\sin(\theta_c n)}{\theta_c n}
\end{eqnarray}
Such a Sinc-function is infinite long, which is caused by the fact that the frequency function $X(e^{j\theta})$ has infinite steep drops for $\theta= \pm \theta_c$.

For the case $\theta_c=\frac{\pi}{2}$ the IFTD result is depicted at the left-hand side of Fig. 7. For this case the samples are zero for all even values of the time index, except for $n=0$.

</div>
</div>

### FTD discrete-time Block function
When processing a signal it is often useful of even necessary to use or select only a part of the signal. This selection process is typically achieved by multiplying the signal with a window function. Although there are many different window functions, the most common one is the rectangular- or block- function. The left hand side of Fig. 8 gives an example of a discrete time block function of length $N=21$, which is equal to 1 for time index $n=0$ up to $n=20$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDBlock.svg"
      alt="FTD of a block function $u[n]- u[n-N]$ with $N=21$."
    />
    <figcaption class="numbered">
      FTD of a block function $u[n]- u[n-N]$ with $N=21$.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Example </h4>
<hr>


In this example we will show that the FTD of a block function of length $N$ results into the following so called Dirichlet function:
$$
X(e^{j\theta}) = e^{-j\frac{N-1}{2} \theta} \cdot \frac{\sin(N \frac{\theta}{2} )}{\sin(\frac{\theta}{2} )}
$$
A plot of both magnitude $|X(e^{j\theta})|$ and phase $\angle \{X(e^{j\theta}) \}$, for $\theta$ in the FI and $N=21$, is depicted in Fig. 8.
Furthermore we will explain the fact that the phase is a straight line, evaluate the zero crossings  and the value for $\theta=0$ of the magnitude $|X(e^{j\theta})|$.

<button class="collapsible">Show solution</button>
<div class="content">

In general we can describe a block function as the difference of two step functions $u[n]-u[n-N]$
and the result is a summation from which the index runs from $n=0$ until $N-1$:
$$
X(e^{j\theta}) =\sum_{n=-\infty}^{\infty} x[n]e^{-jn \theta}= \sum_{n=-\infty}^{\infty} (u[n]- u[n-N]) e^{-jn \theta} = \sum_{n=0}^{N-1} e^{-jn \theta}
$$
This expression is a known geometric series which can be written as:
$$
X(e^{j\theta}) = \frac{1 - e^{-jN \theta}}{1 - e^{-j\theta}}
$$
Now we take out half of the complex exponent in both numerator and denominator:
$$
X(e^{j\theta}) = \frac{e^{-j\frac{N}{2} \theta}}{e^{-j\frac{1}{2} \theta}} \cdot
\frac{e^{j\frac{N}{2} \theta} - e^{-j\frac{N}{2} \theta}}{e^{j\frac{1}{2} \theta} - e^{-j\frac{1}{2} \theta}}
$$
Combining the two complex exponents in front of the equation and dividing both numerator and denominator of the second part of the equation by $2 j$ simplifies the result into a complex exponent multiplied by a function which consists of  sinusoidal functions in both numerator and denominator:
$$
X(e^{j\theta}) = e^{-j\frac{N-1}{2} \theta} \cdot \frac{\sin(N \frac{\theta}{2} )}{\sin(\frac{\theta}{2} )}
$$
Since both sinusoidal terms are real, the phase is completely described by the parameter of the complex exponent:
$$
\angle \{X(e^{j\theta}) \} = - \frac{N-1}{2} \theta
$$
A plot of this function is a straight line as depicted at the right hand side plot of Fig. 8 for $N=21$.
The odd length $N$ block function $x[n]$ can be viewed as a shifted version of the symmetric block function $b[n]= u[n+ \frac{N-1}{2}]-u[n- \frac{N+1}{2}]$. Try to show yourself that the FTD of this function is given by:
$$
B(e^{j\theta})= \frac{\sin(N \frac{\theta}{2} )}{\sin(\frac{\theta}{2} )}
$$
which implies that the phase is zero, thus $\angle \{X(e^{j\theta}) \}=0$. In other words we can conclude that the angle indicates the amount of samples with which the symmetric block function is shifted. In case of the block function $x[n] = u[n] - u[n-N]$ this is indeed $\frac{N-1}{2}$ samples.

The magnitude  $|X(e^{j\theta})|$ is a periodic function which contains zero crossings. The zero crossings follow from the zeros of the numerator as follows:
$$
\sin(N \frac{\theta}{2} )=0 \hspace{3mm} \Rightarrow \hspace{3mm} \theta= k \cdot \frac{2\pi}{N}
$$
The periodicity of the function follows from the zero crossings of the denominator:
$$
\sin(\frac{\theta}{2} )=0 \hspace{3mm} \Rightarrow \hspace{3mm} \theta= k \cdot 2 \pi
$$
which is indeed the width of one Fundamental Interval (FI).
The value of $|X(e^{j\theta})|$ for $\theta=0$ can be evaluated by using the fact that
$\lim_{x \rightarrow 0} \sin(x) = x$, which leads to the following result:
$$
|X(e^{j\theta})| |_{\theta =0} = \lim_{\theta \rightarrow 0} \left \{
\frac{\sin(N \frac{\theta}{2} )}{\sin(\frac{\theta}{2} )} \right \} =
\frac{N \frac{\theta}{2}}{\frac{\theta}{2}} = N
$$

</div>
</div>



## FTD Properties
<iframe width="100%" height="450" src="https://www.youtube.com/embed/2kIrvAyID-o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As shown before the frequency representation $X(e^{j\theta})$ is periodic, which is denoted by representing the frequency variable $\theta$ in the exponent.
Furthermore because of the fact that integral in the FTD is a linear operator, it is straightforward to show that the FTD is also linear.
In this section we will show how conjugation and time reversal influence the frequency representation.  Furthermore we will prove that a shift in time domain results in modulation in frequency domain  and vice versa. Such duality also holds for convolution and multiplication: Convolution in time domain results in multiplication in frequency domain  and vice versa.  Finally we will show that the FTD preserves energy, which was shown by Parceval.

### Conjugation
In this subsection we will show the following conjugation property:
$$
\boxed{
x^\ast[n] \qquad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \qquad X^\ast(e^{-j\theta}) }
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A complex conjugation operation in time domain results in complex conjugation of the mirrored frequency representation.</i></div>

The proof of the conjugation property is straightforward. The first step is to use the conjugated version of $x[n]$ in the FTD definition and then taking out the conjugation operator of the resulting expression as follows:
$$
y[n]=x^\ast [n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} Y(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x^\ast [n] e^{-jn \theta} = \left( \sum\_{n=-\infty}^{\infty} x[n] e^{jn \theta} \right)^\ast
$$
The equation between brackets is equal to the FTD  $X(e^{-j\theta})$ in which $\theta$ is replaced by $- \theta$:
$$
\Rightarrow \hspace{3mm} Y(e^{j\theta}) = \left( X(e^{-j\theta}) \right)^* = X^\ast (e^{-j\theta})
$$
which finalizes the proof.

From this result it follows that for real signals the frequency representation has the following special symmetry properties:
$$
x[n] \text{ real } \Rightarrow \text{ } x[n]=x^\ast[n] \text{ } \Rightarrow \text{ }
X(e^{j\theta}) = X^\ast(e^{-j\theta})
$$

which results into a symmetric magnitude and an anti-symmetric phase response:
$$
\begin{eqnarray}
|X(e^{j\theta})|= |X(e^{-j\theta})| & \quad : \quad & \textbf{Magnitude response symmetric} \newline
\angle \{ X(e^{j\theta})\}=- \angle \{ X(e^{-j\theta})\}  & \quad : \quad & \textbf{Phase response anti-symmetric}
\end{eqnarray}
$$
This special property can be shown by the following simple example in which we calculate the FTD of a delta pulse which is shifted over two samples:
$$
\begin{eqnarray}
x[n] = \delta[n-2] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} \delta[n-2] e^{-jn \theta} = e^{-j2 \theta}
\end{eqnarray}
$$
Thus the FTD of a delta pulse at time index $n=2$ results in a complex exponential function $e^{-j2 \theta}$.  In other words the magnitude response is flat (a straight line), while the phase response has a negative angle $-2 \theta$. The symmetry and anti-symmetry properties are clearly shown as depicted at the right hand side of Fig. 9.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDshiftedDelta.svg"
      alt="Symmetry properties of the magnitude and phase FTD of a real signal."
    />
    <figcaption class="numbered">
      Symmetry properties of the magnitude and phase FTD of a real signal.
    </figcaption>
  </figure>
</div>

### Time reversal
In this subsection we will show the following time reversal property:
$$
\boxed{
\begin{eqnarray}
x[-n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{-j\theta})
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Reversing in time domain implies mirroring in the frequency domain.</i></div>


For the proof we first substitute the negative index $-n$  by a new index $p$ and reverse the summation which leads to the final result:
\begin{eqnarray}
y[n]=x[-n]  &\hspace{-2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \hspace{-2mm} Y(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[-n] e^{-jn\theta}
\overset{{\color{red}p=-n}}{=} \sum\_{p=-\infty}^{\infty} x[p] e^{jp \theta} = X(e^{-j\theta})
\end{eqnarray}
As an example we reverse the signal $x[n]=\delta[n-2]$ as discussed in the previous subsection. The resulting reversed signal $y[n]$ is a delta pulse at time index $n=-2$.
By applying the time reversal property it follows that the frequency representation is equal the complex exponential function $e^{j2 \theta}$.  The plots of the magnitude and phase response, as depicted at the right hand side of Fig. 10, show the effect of the time reversal in frequency domain.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDshiftednegDelta.svg"
      alt="Time reversal property FTD with $y[n]=\delta[n+2]$."
    />
    <figcaption class="numbered">
      Time reversal property FTD with $y[n]=\delta[n+2]$.
    </figcaption>
  </figure>
</div>

### Shifting
In this subsection we will show the following shift property:
$$
\boxed{
\begin{eqnarray}
x[n-n_0] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & e^{-jn_0 \theta} \cdot X(e^{j\theta})
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A shift in time domain results in a multiplication with a complex exponential function in frequency domain.</i></div>


In the first step  of the proof we make both indices of the signal and the exponent the same, namely $n-n_0$, which is achieved by a multiplication with $e^{jn_0 \theta}$.
$$
y[n]=x[n-n_0] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} Y(e^{j\theta})=\sum\_{n=-\infty}^{\infty} x[n-n_0] e^{-jn \theta}
=\sum\_{n=-\infty}^{\infty} x[n-n_0] e^{-j(n-{\color{red}n_0}) \theta} \cdot e^{j{\color{red}n_0} \theta}
$$
By substitution the index $n-n_0$ with a new index $p$ we obtain the final result:
$$
Y(e^{j\theta}) \overset{{\color{blue}p}=n-n_0}{=} \left( \sum\_{{\color{blue}p}=-\infty}^{\infty} x[{\color{blue}p}] e^{-j{\color{blue}p} \theta} \right) \cdot e^{jn_0 \theta}
= X(e^{j\theta}) \cdot e^{jn_0 \theta}
$$

### Modulation
In this subsection we will show the following modulation property:

$$
\boxed{
\begin{eqnarray}
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j(\theta - \theta_0)})
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication with a complex exponential function in time domain results in a shift in frequency domain.</i></div>

The proof is as follows:
$$
\begin{eqnarray}
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
\sum\_{n=-\infty}^{\infty} \left( e^{jn \theta_0} \cdot x[n] \right) e^{-jn \theta} \newline
&& = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn (\theta- \theta_0)} = X(e^{j(\theta - \theta_0)})
\end{eqnarray}
$$
When combining this property for a positive and negative exponent  it follows that the modulation of signal $x[n]$ with a sinusoidal frequency $\theta_0$ results in a frequency representation which consists of two shifted versions of the original frequency representation $X(e^{j\theta})$. This property can be shown as follows:
$$
\begin{eqnarray}
e^{jn \theta_0} \cdot x[n] + e^{-jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
X(e^{j(\theta - \theta_0)}) + X(e^{j(\theta + \theta_0)}) \nonumber \newline
\Rightarrow \text{ } \cos (n \theta_0) \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{1}{2} X(e^{j(\theta + \theta_0)}) + \frac{1}{2} X(e^{j(\theta - \theta_0)})
\end{eqnarray}
$$
In one of the following subsections we will give an example of this modulation property.

### Convolution
In this subsection we will show the following convolution property:

$$
\boxed{
\begin{eqnarray}
x[n] \ast y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \cdot Y(e^{j\theta})
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Convolution in time domain can be performed as a multiplication in frequency domain.</i></div>

The first step of the proof is to use the expression for the convolution sum between $x[n]$ and $y[n]$:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\} = \sum\_{n=-\infty}^{\infty} \left( \sum\_{p=-\infty}^{\infty} x[p] y[n-p] \right) e^{-jn \theta}
$$
Then we can interchange the two summations and multiply in the first summation the samples $x[p]$ with $e^{-jp \theta}$, which has to be compensated in the second summation by $e^{jp \theta}$:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\} =
\sum\_{p=-\infty}^{\infty} x[p] e^{-j{\color{red}p} \theta} \cdot \left( \sum\_{n=-\infty}^{\infty}y[n-p]  e^{-j(n{\color{red}-p}) \theta} \right)
$$
As a final step we substitute a new variable $m=n-p$ and since both variables $n$ and $p$ range from minus to plus infinity, this implies that the new variable also ranges from minus to plus infinity:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\}
\overset{{\color{blue}m}= n-p}{=} \sum\_{p=-\infty}^{\infty} x[p] e^{-jp \theta} \cdot \left( \sum\_{{\color{blue}m}=-\infty}^{\infty}y[m]  e^{-j{\color{blue}m} \theta} \right)
= X(e^{j\theta}) \cdot Y(e^{j\theta})
$$
which finalizes the proof.

### Multiplication
In this subsection we will show the dual property of the previous subsection:

$$
\boxed{
\begin{eqnarray}
x[n] \cdot y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \star Y(e^{j\theta}) =
\frac{1}{2 \pi} \int_{\psi = - \pi}^{\pi} X(e^{j\psi}) Y(e^{j(\theta - \psi)}) \text{d}\psi
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication in time domain can be performed by a convolution in frequency domain.</i></div>

In the first step of the proof  we replace $x[n]$ as the inverse of its frequency representation, which results in an equation with a summation and an integral:
$$
\begin{eqnarray}
\mathcal{F} \left\\{ x[n] \cdot y[n] \right\\} &=& \sum\_{n=-\infty}^{\infty}  x[n] \cdot y[n] e^{-jn \theta}
= \sum\_{n=-\infty}^{\infty} \left(
\mathcal{F}^{-1} \left\\{ X(e^{j\psi}) \right\\} \right) \cdot y[n] e^{-jn \theta} \newline
&=& \sum\_{n=-\infty}^{\infty}  \left( \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\psi}) e^{jn \psi} \text{d} \psi \right) \cdot y[n] e^{-jn \theta}
\end{eqnarray}
$$

Since both summation and integral operations are linear, we may interchange the order:

$$
\mathcal{F} \left\\{ x[n] \cdot y[n] \right\\} = \frac{1}{2\pi} \int\_{-\pi}^{\pi} X(e^{j\psi}) \left( \sum\_{n=-\infty}^{\infty} y[n] e^{-jn (\theta - \psi)} \right) \mathrm{d} \psi
$$
The equation between brackets represents the FTD of signal $y[n]$ from which the frequency $\theta$ is interchanged by $\theta - \psi$:
$$
\mathcal{F} \{ x[n] \cdot y[n] \} =
\frac{1}{2 \pi} \int_{\psi = - \pi}^{\pi} X(e^{j\psi}) Y(e^{j(\theta - \psi)}) \text{d}\psi
= X(e^{j\theta}) \star Y(e^{j\theta})
$$
This last equation represents the convolution integral between the two continuous frequency representations $X(e^{j\theta})$ and $Y(e^{j\theta})$, which is symbolically denoted by a star.
In the following subsections we will discuss some examples of this multiplication property.




#### Example multiplication property: Modulation
As a first example of the multiplication property we will show the previously discussed modulation property. In this example we choose for signal $x[n]$ a sinc function.
In the previous section we have shown that the FTD of a sinc function in time domain results in a block function in frequency domain. The top figure of Fig. 11 shows a sketch of this result.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDModulateSinc.svg"
      alt="Example multiplication property: Modulation."
    />
    <figcaption class="numbered">
      Example multiplication property: Modulation.
    </figcaption>
  </figure>
</div>

Furthermore we have shown in the previous section that the FTD of a sinusoidal  function with frequency $\theta_0$ consists of two delta pulses at frequencies $\pm \theta_0$, which is shown in the middle figure of Fig. 11. The lower part of Fig. 11
shows at the left hand side the result of the multiplication of the sinc function with the sinusoidal function in time domain. Multiplication in time domain results in convolution in frequency domain. Thus the block function in frequency domain has to be convolved with the two delta pulses at $\pm \theta_0$. Convolving a function with a delta pulse results in a shift of the original function to the position of the delta pulse. In this case the resulting frequency representation consists of two original frequency representations which are shifted over $\pm \theta_0$, which is shown at the right hand side of the lower figure of Fig. 11. This is exactly the result of the modulation property.

<!-- TODO: ADD MATLAB ANIMATION. -->


#### Example multiplication property: Finite length sinusoidal
In most cases we assume in theory that a signal is infinite long. In practice however this will never be true and we will work with a finite length signal. In this example we will show the implication of this effect in frequency domain for a sinusoidal signal.  The top figures of Fig. 12 shows at the left hand side an infinite long sinusoidal signal $s[n]$ of frequency $\theta_0$ and at the right hand side the FTD result $S(e^{j\theta})$, which consists of two delta functions at frequency $\pm \theta_0$.

<figure>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/signal.svg" />
  </div>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDsignal.svg" />
  </div>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/window.svg" />
  </div>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDwindow.svg" />
  </div>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/wsignal.svg" />
  </div>
  <div class="image-wrapper">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDwsignal.svg" />
  </div>
<figcaption class="numbered">
  FTD of an infinite and a finite length (windowed) sinusoidal signal.
</figcaption>
</figure>

A finite length sinusoidal $s_w[n]$ can be obtained by multiplication this infinite length sinusoidal $s[n]$ with a finite length window or block function $w[n]$.
The left hand side of the middle figure of Fig. 12 shows a rectangular block function $w[n]$ of length $N=32$ samples. The FTD $W(e^{j\theta})$ of this block function is depicted at the right hand side of the middle figure.
In the previous section we have shown that this is a Dirichlet function. The width of the main lobe of this Dirichlet function $W(e^{j\theta})$ equals $2 \times \frac{2\pi}{N}$, which follows from the first two zero crossings around this main lobe. This implies that the main lobe is inversely proportional with the length of the block function in time domain. In other words, a very long block function $w[n]$ will result in a very small main lobe $W(e^{j\theta})$ and the other way around.

Finally the figure at the left hand side of the lower figure in Fig. 12 shows the finite length sinusoidal signal $s_w[n]$, which is the result of the multiplication of
$s[n]$ with $w[n]$. The figure at the right hand side shows the FTD $S_w(e^{j\theta})$ of this finite length signal $s_w[n]$. The FTD $S_w(e^{j\theta})$ can be constructed by using the property: _"multiplication in time domain is equivalent to a convolution in frequency domain"_.
So in practice the two original, infinite small, delta pulses at frequencies $\pm \theta_0$ of the infinite long sinusoidal function are smeared out depending on the with of the main lobe of the Dirichlet function: The more samples $N$ we take, the smaller the two peaks will be and the result looks closely to the infinite length (theoretical) result. While on the other hand when using only a small number of samples $N$ of the sinusoidal functions will results into two peaks that are smeared out in frequency domain.

### Parceval: Preservation of energy
Parceval has shown following FTD property:

$$
\boxed{
\begin{eqnarray}
\sum\_{n=-\infty}^{\infty} |x[n]|^2 &=& \frac{1}{2 \pi} \int_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \text{d} \theta
\end{eqnarray}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The FTD preserves energy.</i></div>

The first step of the proof is to replace the complex conjugated version of $x[n]$ by the IFTD of the FTD of $x^\ast[n]$.
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 = \sum\_{n=-\infty}^{\infty} x[n] x^\ast[n]
=\sum\_{n=-\infty}^{\infty} x[n] \mathcal{F}^{-1} \left\\{ \mathcal{F} \left\\{ x^\ast[n] \right\\} \right\\}
$$
Then we apply the conjugation property and  write out the IFTD:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\sum\_{n=-\infty}^{\infty} x[n] \mathcal{F}^{-1} \left\\{ X^\ast(e^{-j\theta}) \right\\}
= \sum\_{n=-\infty}^{\infty} x[n] \left(
\frac{1}{2\pi} \int\_{-\pi}^{\pi}
X^\ast(\text{e}^{-j \theta}) \text{e}^{+ j n \theta}
\mathrm{d} \theta \right)
$$
Now we can replace $\theta$ by $-\theta$
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\sum\_{n=-\infty}^{\infty} x[n] \left(
\frac{1}{2\pi} \int\_{-\pi}^{\pi}
X^\ast(\text{e}^{{\color{red}+} j \theta}) \text{e}^{{\color{red}-} j n \theta}
\mathrm{d} \theta \right)
$$
and interchange the order of the summation and integral operations:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\frac{1}{2\pi} \int\_{-\pi}^{\pi} X^\ast(e^{j\theta}) \left(
\sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta} \right) \mathrm{d} \theta
$$
The term between brackets is the FTD definition of $x[n]$, which leads to the final result:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\frac{1}{2 \pi} \int\_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \text{d} \theta
$$

#### Example Parceval
In this example we will use Parceval to calculate the energy of the sinc function:
$$
x[n]= \frac{1}{2} \frac{\sin(\frac{\pi}{2} n)}{\frac{\pi}{2}}
$$
which is depicted at the left hand side of Fig. 7. For this we have to calculate the summation of the squared absolute values of the samples which may be a tough exercise.
On the other hand we have shown before that the frequency representation of the given sinc function is a block function with a cut off frequency $\theta_c=\frac{\pi}{2}$, as depicted at the right hand side of Fig. 7.
So by using the Parceval property it is easier to calculate the energy in frequency domain  which goes as follows:
$$
\begin{eqnarray}
E &=& \sum\_{n=-\infty}^{\infty} | x[n]|^2
= \sum\_{n=-\infty}^{\infty} \left | \frac{1}{2} \frac{\sin(\frac{\pi}{2} n)}{\frac{\pi}{2}}\right |^2 \nonumber \newline
&\overset{\text{Parceval}}{=}&
\frac{1}{2 \pi} \int\_{-\pi}^{\pi} \left |X(e^{j\theta}) \right |^2 \mathrm{d} \theta
= \frac{1}{2 \pi} \int\_{-\pi/2}^{\pi/2} \left | 1 \right |^2 \mathrm{d} \theta
= \frac{1}{2}
\end{eqnarray}
$$


## Summary
\\
$$
\boxed{
\begin{eqnarray}
X(e^{j\theta})
\overset{\mathcal{F}\left\\{x[n]\right\\}}{=\\! =}
\sum\_{n=- \infty}^{\infty} x[n] e^{-jn\theta}
&\\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  
x[n]
\overset{\mathcal{F}^{-1}\{X(e^{j\theta})\}}{=\\! =\\! =\\!}
\frac{1}{2 \pi} \int\_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \mathrm{d} \theta
\end{eqnarray}}
$$


\\
<b><u> Main differences with continuous-time Fourier transforms: </u></b>
<ul>
<li>  The signal samples $x[n]$ are discrete in time and not periodic, </li>
<li>  The normalized frequency $\theta = \omega \cdot T_s$, </li>
<li>  The Fundamental Interval is usually chosen as: $-\pi \leq \theta < \pi$, </li>
<li>  The frequency representation $X(e^{j\theta})$ is a continuous function and periodic, </li>
<li>  The FTD is evaluated over an infinite summation of samples $x[n]$, </li>
<li>  The IFTD is evaluated by an integral over one period of the frequency representation $X(e^{j\theta})$. </li>
</ul>


\\
<b><u> Discrete phasor property: </u></b>
$$
\textbf{DPP:} \qquad \sum\_{p=-\infty}^{\infty} e^{-jp \theta} = \sum\_{k=-\infty}^{\infty} 2 \pi \delta(\theta + k \cdot 2 \pi)
$$

\\
<b><u> Most important FTD pairs: </u></b>
<table style="width:100%">
  <tr>
    <th style="text-align:center"> $x[n]$  </th>
    <th style="text-align:center"> $X(e^{j\theta})$ </th>
  </tr>
  <tr>
    <td align=center> $\delta[n]$  </td>
    <td align=center> $1$ </td>
  </tr>
  <tr>
    <td align=center> $1$  </td>
    <td align=center> $2\pi\delta(\theta)$ </td>
  </tr>
  <tr>
    <td align=center> $\cos(n\theta_0)$  </td>
    <td align=center> $\pi\delta(\theta+\theta_0) + \pi\delta(\theta-\theta_0)$ </td>
  </tr>
  <tr>
    <td align=center> $a^nu[n], \ |a|<1$  </td>
    <td align=center> $\frac{1}{1-ae^{-j\theta}}$ </td>
  </tr>
  <tr>
    <td align=center> Sinc: $\frac{\theta_c}{\pi}\cdot \frac{\sin(\theta_c n)}{\theta_c n}$  </td>
    <td align=center> Block: $\begin{cases} 1 & |\theta|<\theta_c \newline 0 & \text{otherwise}\end{cases}$ </td>
  </tr>
  <tr>
    <td align=center> Block: $u[n]-u[n-N]$  </td>
    <td align=center> Dirichlet: $e^{-j\frac{N-1}{2}\theta}\frac{\sin(N\frac{\theta}{2})}{\sin(\frac{\theta}{2})}$ </td>
  </tr>
</table>



<b><u> Most important FTD properties:</u></b>
$$
\begin{eqnarray}
x^\ast[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X^\ast(e^{-j\theta}) \newline
x[-n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{-j\theta})\newline
x[n-n_0] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & e^{-jn_0 \theta} \cdot X(e^{j\theta})\newline
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j(\theta - \theta_0)})\newline
x[n] \star y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \cdot Y(e^{j\theta})\newline
x[n] \cdot y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \star Y(e^{j\theta}) \newline
\sum\_{n=-\infty}^{\infty} |x[n]|^2 &=& \frac{1}{2 \pi} \int\_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \mathrm{d} \theta
\end{eqnarray}
$$
