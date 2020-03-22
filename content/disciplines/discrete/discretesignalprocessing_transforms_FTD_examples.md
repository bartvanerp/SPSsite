+++
title = "FTD examples"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "FTD examples"
  weight = 2
  parent = "Transforms I: Fourier transform for discrete-time signals"

+++


<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/3yPFxOeVN9s" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

This section discusses some important examples of the FTD and IFTD.
To gain more skill with this transformation, it is useful to first elaborate some of these examples yourself.

## FTD and IFTD Delta function
One of the signals that is used most often is the discrete-time delta function $x[n]=\delta[n]$.
Because of the fact that this function is only 1 for index $n=0$ and zero for all other indices, the FTD results into 1 as shown in the following equation:
$$
X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta} = \sum\_{n=-\infty}^{\infty} \delta[n] e^{-jn \theta} = 1 \hspace{3mm} \forall \ \theta
$$
This implies that a delta function in time domain contains all frequencies $\theta$ in frequency domain. This effect is represented in the Fig. 1.

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
\sum\_{k=-\infty}^{\infty} 2 \pi \delta(\theta + k \cdot 2 \pi)$, which is denoted in Fig. 2.

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

## Discrete Phasor Property (DPP)
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

## FTD of discrete-time sinusoidal

<div class="example">
<h4> Example </h4>
<hr>
In this example we use the DPP property of the previous subsection to show that the FTD of a sinusoidal signal results in the following expression:
$$
x[n]=\cos(n \theta_0) \hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm}
\pi \delta(\theta - \theta_0) + \pi \delta(\theta + \theta_0)
$$
as depicted in Fig. 3.
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
\begin{eqnarray*}
\Rightarrow \text{ } \mathcal{F} \{ \cos(n \theta_0) \} &=&
\mathcal{F} \left\{ \frac{1}{2} e^{jn \theta_0} \right\} + \mathcal{F} \left\{ \frac{1}{2} e^{-jn \theta_0} \right\} \nonumber \\
&=& \pi \delta(\theta - \theta_0) + \pi \delta(\theta + \theta_0)
\end{eqnarray*}
which is represented in Fig. 3.</div>
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

## FTD of exponential decaying function
<div class="example">
<h4> Example </h4>
<hr>
In this example we will calculate the FTD $X(e^{j\theta})$ of a discrete time exponential decaying function $x[n]=a^n u[n]$, with $u[n]$ the unit step function. Furthermore we will sketch a plot of $|X(e^{j\theta})|$ in the Fundamental Interval (FI) for $0 < a < 1$ and $-1 < a < 0$ and give a reasoning for the difference between these two plots.
<button class="collapsible">Show solution</button>
<div class="content">
The FTD can be calculated as given in the following equations:
\begin{eqnarray*}
X(e^{j\theta}) &=& \sum_{n=-\infty}^{\infty} x[n] e^{-jn \theta}
= \sum_{n=-\infty}^{\infty} a^n {\color{red}u[n]} e^{-jn \theta}= \sum_{n={\color{red}0}}^{\infty} a^n  e^{-jn \theta} \nonumber \\
&=& \sum_{n=0}^{\infty} \left( a e^{-j\theta} \right) ^n
= \frac{1}{1 - a e^{-j\theta}} \hspace{3mm} |a| < 1
\end{eqnarray*}
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


## IFTD Block function
One of the filters which is used in many practical situations is a Low Pass Filter (LPF). Mathematically we can represent such an ideal LPF with a block function with a cut off frequency $\theta_c$. In the pass area the value of the frequency function is equal to 1, and in the attenuation area the value is zero. An example with $\theta_c=\frac{\pi}{2}$ is depicted at the right-hand side of Fig. 4.

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
With the ideal LPF as depicted at the right-hand side of Fig. 4, the integral of the IFTD equation reduces to an integral of a complex exponent within boundaries $\pm \theta_c$.
$$
x[n] = \frac{1}{2 \pi} \int_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \text{d} \theta
= \frac{1}{2 \pi} \int_{{\color{red}-\theta_c}}^{{\color{red}\theta_c}} {\color{red}1} e^{jn\theta} \text{d} \theta
$$
Changing the function variable $\theta$ of the integral into $j n \theta$ leads to the given equation:
$$
x[n] =\frac{1}{2 \pi j n } \int_{-\theta_c}^{\theta_c} e^{jn\theta} \text{d} (j n \theta)
$$
Using the boundaries and  combining the two phasors in the numerator as a sinusoidal, results in an expression  which is a so called Sinc-function:
\begin{eqnarray*}
x[n] &=& \frac{1}{2 \pi j n} e^{jn\theta}\mid_{- \theta_c}^{\theta_c}
= \frac{1}{2 \pi j n} \left( e^{jn\theta_c} - e^{-jn\theta_c} \right)
= \frac{\theta_c}{\pi} \cdot \frac{\sin(\theta_c n)}{\theta_c n}
\end{eqnarray*}
Such a Sinc-function is infinite long, which is caused by the fact that the frequency function $X(e^{j\theta})$ has infinite steep drops for $\theta= \pm \theta_c$.
For the case $\theta_c=\frac{\pi}{2}$ the IFTD result is depicted at the left-hand side of Fig. 4. For this case the samples are zero for all even values of the time index, except for $n=0$.
</div>
</div>

## FTD discrete-time Block function
When processing a signal it is often useful of even necessary to use or select only a part of the signal. This selection process is typically achieved by multiplying the signal with a window function. Although there are many different window functions, the most common one is the rectangular- or block- function. The left hand side of Fig. 5 gives an example of a discrete time block function of length $N=21$, which is equal to 1 for time index $n=0$ up to $n=20$.

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
A plot of both magnitude $|X(e^{j\theta})|$ and phase $\angle \{X(e^{j\theta}) \}$, for $\theta$ in the FI and $N=21$, is depicted in Fig. 5.
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
A plot of this function is a straight line as depicted at the right hand side plot of Fig. 5 for $N=21$.
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
