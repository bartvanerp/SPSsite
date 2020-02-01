+++
title = "Fourier transform for continuous-time signals"

# date = {{ .Date }}
lastmod = 2019-11-28

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Fourier transform for continuous-time signals"
  weight = 42
  parent = "Continuous-time transforms"

+++


## Introduction
The <a href="../continuoussignalprocessing_transforms_fourier">Fourier Series (FS)</a> representation is an extremely useful signal representation. Unfortunately, this signal representation can only be used for periodic signals.
That's why we will introduce a tool for representing non-periodic signals, known as the <b>F</b>ourier <b>T</b>ransform for <b>C</b>ontinuous time signals, abbreviated as FTC. One might wonder if we can somehow use the Fourier Series to develop a representation for non-periodic signals. As it turns out, this is possible. By viewing a non-periodic as a periodic signal with an infinitely large period, we can use the Fourier Series to develop a more general signal representation that can be used in the non-periodic case. By doing so we should realise that the development of the FTC is not completely rigorous. Instead it is plausible which suggests the correct form of the FTC equations and it provides a useful interpretation.

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/r1_Dotj41L4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Fourier Series (FS) recap
The development of the Fourier Series was based on the following General Phasor Integral (GPI-FS) property:
$$
\int_{-(T_0/2)}^{T_0/2} e^{j2 \pi  k \cdot F_0 t} \text{d} t
=\begin{cases}
\neq 0 & \text{ for } k = 0 \newline
0 & \text{ for } k \neq 0
\end{cases}
$$

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/continuous/transforms/FTC/GPIFS1.svg"
    style="width:100%">
    <figcaption>
      Upper bound intergral $U=3T_0/8$.
    </figcaption>
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/continuous/transforms/FTC/GPIFS2.svg"
    style="width:100%">
    <figcaption>
      Upper bound intergral $U=T_0/2$.
    </figcaption>
  </div>
</div>
<figcaption class="numbered">
  Different stages General Phasor Integral property (GPI-FS).
</figcaption>
</figure>

An example of the calculation of this integral is shown in Figure 1.
The figures show the projection of a phasor with frequency $2 \times F_0$, with $F_0=1/T_0=1$ [Hz], on both the real and imaginary axis. The result of the integral of this phasor is represented by a colored surface: blue for a positive and red for a negative surface.
The upper bound $U$ of the integral in the left hand figure equals $3 T_0/8$ and in the right hand figure $U=T_0/2$. From the right hand figure it follows that the total amount of red and blue area is the same. This implies that the total surface (or integral), over 2 rotations, is equal to zero. It is clear that this is true for any frequency which equals an integer multiple of $k$ times the fundamental frequency $F_0$. There is only one exception and that is when this multiple represents frequency 0 [Hz].

This GPI-FS property leads to the Fourier Series as given in the following equation:
$$
\boxed{
\begin{eqnarray}
\alpha\_{k} = \frac{1}{T_0} \int\_{-T\_0/2}^{T\_0/2} x\_p(t) e^{-j2 \pi  k F\_0 t} \text{d}t
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&
x\_p(t) = \sum\_{k=- \infty}^{\infty} \alpha\_k e^{j2 \pi k F\_0 t}
\end{eqnarray}}
$$
By multiplying a periodic signal $x_p(t)$ with a phasor with frequency $k \cdot F_0$ and taking the integral over one period $T_0$, the result of the GPI-FS property  is that only the frequency $k \cdot F_0$ of the periodic signal $x_p(t)$ is triggered. In case the frequency $k \cdot F_0$ is present, the integral results in a measure $\alpha_k$, representing the frequency content of the periodic signal $x_p(t)$ at frequency $k \cdot F_0$. When this particular frequency $k \cdot F_0$ is not present in the periodic signal $x_p(t)$ the value of $\alpha_k$ will result in zero.
This implies that a periodic signal can only have discrete (related) frequencies $k \cdot F_0$, which leads to the general expression of a periodic signal $x_p(t)$ which writes as a, possibly infinite, sum of weighted phasors.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FSsignal.svg"
      alt="Example periodic signal $x_p(t)$ and its Fourier Series representation."
    />
    <figcaption class="numbered">
      Example periodic signal $x_p(t)$ and its Fourier Series representation.
    </figcaption>
  </figure>
</div>

An example of a periodic signal $x_p(t)$, with fundamental period $T_0=1/F_0$, and its Fourier series representation is shown in Figure 2. The weights $\alpha_k$ represent the frequency content of the periodic signal $x_p(t)$.

<br></br>

## FTC as limit of FS

The FTC and Inverse FTC are defined as follows:
$$
\boxed{
\begin{eqnarray}
X(f)=\mathcal{F}\\{x(t)\\} = \int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) =\mathcal{F}^{-1}\\{X(f)\\}= \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f
\end{eqnarray}}
$$
In contrast to the Fourier Series the FTC equations are:
<ul>
<li> based on <b> non-periodic </b> signals, </li>
<li> based on <b> the entire </b> signal, </li>
<li> its frequencies $f$ are<b> continuous </b> and </li>
<li> $x(t)$ can be expressed as an <b> integral </b> of phasor components. </li>
</ul>
The correctness of the FTC equations can be shown by relating these equations with the Fourier series expressions. For this we assume a finite length non-periodic signal $x(t)$, with length $\Delta T = 1 / \Delta F$, as depicted in Figure 3. The right end side of the figure shows a sketch of its frequency distribution $X(f)$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCasFS.svg"
      alt="Non-periodic signal $x(t)$ and its frequency distribution $X(f)$."
    />
    <figcaption class="numbered">
      Non-periodic signal $x(t)$ and its frequency distribution $X(f)$.
    </figcaption>
  </figure>
</div>

On the one hand we can show that the non-periodic signal $x(t)$ can be approximated by an infinite sum of weighted phasors, which is similar to the general representation of a periodic signal.  In order to do so we write the non-periodic signal $x(t)$  as the Inverse FTC integral. By splitting the continuous frequency axis $f$ of $X(f)$ of a small width $\Delta F$ and replacing d$f$ of the integral with $\Delta F$, it is possible to think of the integral as an infinite sum as represented in the following equation:
$$
x(t)=\mathcal{F}^{-1}\\{X(f)\\} \overset{\text{def}}{=}
\int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f
\overset{\Delta F \rightarrow 0}{\approx}
\sum\_{k=-\infty}^{\infty} \left ( X(k \Delta F) \Delta F \right ) e^{j2 \pi k \Delta F t}
$$
As follows from Figure 3, the value of the product $X(k \Delta F) \Delta F$ (in blue) represents an approximation of the surface of the frequency distribution $X(f)$ at frequency $f= k \cdot \Delta F$.  When comparing the resulting infinite sum of weighted phasors to the Fourier Series expression of a periodic signal, it follows that the surface $X(k \Delta F) \Delta F$ represent the weight $\alpha\_k$ of the Fourier Series expression.
On the other hand, when using the Fourier Series expression for these weights, multiplied by $\Delta T$,  we obtain the Fourier Series integral within the boundaries $-\Delta T/2$ until $+\Delta T/2$ as given in the following equation:
\begin{eqnarray}
\left (X(k \Delta F) \Delta F\right ) \cdot \Delta T & \widehat{=} \ &\alpha\_k \cdot \Delta T
\overset{\text{FS}}{=} \int_{-\Delta T/2}^{\Delta T/2} x\_p(t) e^{-j2 \pi (k \Delta F) t} \text{d} t   \\
& \overset{k \Delta F \rightarrow f}{\approx} & \int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t} \text{d} t \overset{\text{def}}{=} X(f)
\end{eqnarray}
When the length $\Delta T$ goes to infinite, or equivalently when $\Delta F$ goes to zero and $k \Delta F$ becomes close to the continuous frequency $f$, the non-periodic signal $x(t)$ can be viewed as the limiting case of the periodic signal $x_p(t)$  and the result is FTC equation.

As mentioned before we should realise that the given development of the FTC equations is not completely rigorous. Instead it is plausible which suggests the correct form of the FTC equations and it provides a useful interpretation.

### Example rectangular signal

In order to further clarify the given insight we will evaluate the FTC, as an approximation of the Fourier Series, of the finite length non-periodic rectangular signal $x(t)$, which is depicted in Figure 4 and defined by the following equation:
$$
x(t) = \begin{cases}
1 & -\Delta T/2 < t < \Delta T/2 \newline
0 & \text{elsewhere}
\end{cases}\quad \text{and} \quad x\_p(t) = \sum\_{n=-\infty}^{\infty} x(t - n T\_0)
$$
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FSlimitsquare.svg"
      alt="Similarity $x(t)$ and $x_p(t)$ for different period lengths $T_0$."
    />
    <figcaption class="numbered">
      Similarity $x(t)$ and $x_p(t)$ for different period lengths $T_0$.
    </figcaption>
  </figure>
</div>
With $T_0 > \Delta T$, we can interpret the non-periodic signal $x(t)$ as <b>one</b> period of the periodic signal $x_p(t)$, with period $T_0$. The upper figure shows an example for $T_0 = 2 \Delta T$.  When increasing the period $\Delta T$, as depicted in the other figures,  it follows that the non-periodic signal $x(t)$ can be approximated by the periodic signal $x_p(t)$ when the period $T_0$  goes to infinity as follows:
$$
x(t) = \lim_{T_0 \rightarrow \infty} x_p(t)
$$
From this it follows that the FTC of the non-periodic signal $x(t)$ can be viewed as a reasonable approximation of the Fourier Series of the periodic signal $x_p(t)$. The weights $\alpha_k$ multiplied by $T_0$ of the periodic signal $x_p(t)$ can be evaluated via the following Fourier Series:
\begin{eqnarray}
\alpha_{k} = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} x_p(t) e^{-j2 \pi  k F_0 t} \text{d}t
&\overset{\text{FS}}{\quad\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ\quad}&
x_p(t) = \sum_{k=- \infty}^{\infty} \alpha_{k} e^{j2 \pi k F_0 t}
\end{eqnarray}
The block signal $x_p(t)$ equals 1 within the boundaries $-\Delta T/2$ and $+\Delta T/2$, which leads to the following result:
\begin{eqnarray}
\alpha_{k} \cdot T_0 &=& \int_{-\Delta T/2}^{\Delta T/2} 1 e^{-j2 \pi  k F_0 t} \text{d}t
 =
\frac{1}{-j 2 \pi k F_0}  e^{-j2 \pi k F_0 t} \Big|_{-\Delta T/2}^{\Delta T/2}
\newline
&=& \frac{e^{-j2 \pi k F_0 \Delta T/2}- e^{j2 \pi k F_0 \Delta T/2}}{-j 2 \pi k F_0} =
\Delta T \cdot \frac{\sin (\pi k F_0 \Delta T)}{\pi k F_0 \Delta T}
\end{eqnarray}
With $F_0=1/T_0$ and for the limiting case $F_0 \rightarrow 0$ and $k F_0 \rightarrow f$ we obtain:
$$
\Rightarrow \hspace{2mm}
\lim_{F_0 \rightarrow 0 }
\alpha_{k} \cdot T_0 \widehat{=} X(f) \rightarrow \Delta T \cdot \frac{\sin (\pi \color{blue}{f} \Delta T)}{\pi \color{blue}{f} \Delta T} \hspace{3mm} \left ( \widehat{=} \text{ Sinc} \right )
$$
A plot of this function for increasing values of $T_0$ is depicted in Fig. 5.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FS2FTC8DeltaT.svg"
      alt="Plot of $X(f)$ and $\alpha_{k} \cdot T_0$ for increasing $T_0$."
    />
    <figcaption class="numbered">
      Plot of $X(f)$ and $\alpha_{k} \cdot T_0$ for increasing $T_0$.
    </figcaption>
  </figure>
</div>

When increasing $T\_0$ we see that the values of the weights $\alpha\_k$ multiplied by $T_0$ get closer and closer together and eventually become dense and approach the continuous envelope sinc function.

Until now we have discussed the FTC equations as a function of frequency $f$ in [Hz]. In literature we also find the same FTC equations as a function of the radian frequency $\omega$ in [rad/sec] as defined in the following equation:
$$
\boxed{
\begin{eqnarray}
X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \text{d} \omega
\end{eqnarray}}
$$
With $\omega = 2 \pi f$, the replacement of the integral variable $f$ by $\omega$, in the Inverse FTC equation, results in the pre-multiplication factor of $1/ 2\pi$ in this case.

### Existence and convergence FTC

Not every function $x(t)$ has an FTC representation. So it would be helpful to be able to determine whether the FTC exists or not. As a simple condition for convergence of the FTC integral, we can check the magnitude $|X(f)|$. By first using the fact that the absolute value of an integral is smaller or equal than the integral of the absolute value and then that the absolute value of the given phasor equals one, we obtain the resulting integral.
\begin{eqnarray}
\left | X(f) \right | &=& \left |\int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t \right | \\
&\leq & \int\_{-\infty}^{\infty} \left | x(t) e^{-j2 \pi f t} \right |  \text{d} t
= \int\_{-\infty}^{\infty} \left | x(t) \right | \text{d} t
\end{eqnarray}

\begin{eqnarray}
\Rightarrow \hspace{3mm} \left | X(f) \right | < \infty & \leftrightarrow &
\int_{-\infty}^{\infty} \left | x(t) \right | \text{d} t < \infty
\end{eqnarray}

This implies that a sufficient, but not necessary, condition to check the existence of the FTC of a signal $x(t)$ is to evaluate the integral of the absolute value of $x(t)$ and verifying if the result is bounded.

<br></br>


## FTC Examples
In this section we will discuss the FTC of some basic signals. As such we will discuss the FTC and IFTC of a delta pulse, a block signal, a sinusoidal signal and finally a pulse train.

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/jWRR689o1zs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### (I)FTC delta pulse and General Phasor Integral (GPI)
The FTC of a delta pulse $\delta(t)$ can be found as follows:
$$
X(f) = \mathcal{F}\\{x(t)\\}=\mathcal{F}\\{\delta(t)\\}=\int\_{-\infty}^{\infty} \delta(t) e^{-j2 \pi f t} \text{d} t = 1
\hspace{2mm} \forall f
$$
This implies that all frequencies, from $-\infty$ to $+\infty$, are present in a delta pulse.

The other way around it follows, according the definition of a delta pulse, that the IFTC of a delta pulse $\delta(f)$ in frequency domain can be found as follows:
$$
x(t) = \mathcal{F}^{-1}\\{X(f)\\}=\mathcal{F}^{-1}\\{\delta(f)\\}=\int\_{-\infty}^{\infty} \delta(f) e^{-j2 \pi f t} \text{d} f = 1 \hspace{2mm} \forall t
$$
From this we can derive an important integral property which is basic for the development of the Fourier transform. This derivation goes as follows:
$$
\mathcal{F}^{-1}\\{\delta(f)\\} = 1
\quad \Leftrightarrow \quad \delta(f) = \mathcal{F}\\{ 1 \\} \quad \Leftrightarrow \quad \delta(f) = \int\_{-\infty}^{\infty} 1 \cdot e^{-j2 \pi f t} \text{d} t
$$
Thus a delta pulse $\delta(f)$ in frequency domain is the result of integrating a phasor with frequency $f$ for time $t$ from minus to plus infinity. In other words: The integral of a phasor is zero for all frequencies $f$ except for frequency $f=0$ (DC), then the result is infinite.
By replacing the frequency $f$ by $f \pm f\_0$ we obtain the following so called General Phasor Integral (GPI):
$$
\boxed{
\begin{eqnarray}
\int\_{-\infty}^{\infty}  e^{-j2 \pi (f \pm f\_0) t} \text{d} t
&\overset{\text{GPI}}{=}& \delta(f \pm f\_0)
\end{eqnarray}}
$$

### (I)FTC of block
Before we have approximated the FTC of a block signal by viewing it as an approximation of a periodic block signal. By doing so we could evaluate the FTC of a block signal as an approximation of the Fourier Series of a periodic block signal. The following derivations show that the result is the same by applying the FTC equation.

The block signal $x(t)$ is shown in Fig. 6 and defined as:
$$
x(t) =
\begin{cases}
1 & \text{for } |t| \leq T\_0/2 \newline
0 & \text{elsewhere}
\end{cases}
$$
Evaluating the FTC of this block signal results into the following:
\begin{eqnarray}
X(f) &=& \int\_{-\infty}^{\infty} x(t) \cdot e^{-j2 \pi f t} \text{d} t =
\int\_{-T\_0/2}^{T\_0/2} 1 \cdot e^{-j2 \pi f t} \text{d} t  \newline
&=&\frac{1}{-2j \pi f} e^{-j2 \pi f t} \left . \right |\_{-T\_0/2}^{T\_0/2} =
\frac{e^{-j2 \pi f T_0/2}- e^{j2 \pi f T\_0/2} }{-2j \pi f}  \newline
&=& T\_0 \frac{\sin(\pi f T\_0)}{\pi f T_0} = T\_0 \ \text{sinc}(\pi f T\_0)
\end{eqnarray}

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCBlock.svg"
      alt="FTC of time domain block results in sinc in frequency domain."
    />
    <figcaption class="numbered">
      FTC of time domain block results in sinc in frequency domain.
    </figcaption>
  </figure>
</div>

In other words: The FTC of a block-function in time domain is a sinc-function in frequency domain as depicted in Fig. 6.

By following similar steps we can evaluate the IFTC of a block signal $X(f)$ in the frequency domain, in which the block signal is defined as:
$$
X(f) =
\begin{cases}
1 & \text{for } |f| \leq F\_c \newline
0 & \text{elsewhere}
\end{cases}
$$
and depicted in Fig. 7.
The evaluation of the IFTC is as follows:
\begin{eqnarray}
x(t) &=& \int\_{-\infty}^{\infty} X(f) \cdot e^{j2 \pi f t} \text{d} f =
\int_{-F\_c}^{F\_c} 1 \cdot e^{j2 \pi f t \text{d} f}
= \frac{1}{2j \pi t} e^{j2 \pi f t} \left . \right |\_{-F\_c}^{F\_c}  \newline
&=& \frac{e^{j2 \pi F\_c t}- e^{-j2 \pi F\_c t} }{2j \pi t}
= 2 F\_c \frac{\sin(2\pi F\_c t)}{2\pi F\_c t} = 2 F\_c \ \text{sinc}(2\pi F\_c t)
\end{eqnarray}

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/IFTCBlock.svg"
      alt="IFTC of time domain block results in sinc in frequency domain."
    />
    <figcaption class="numbered">
      IFTC of time domain block results in sinc in frequency domain.
    </figcaption>
  </figure>
</div>

In other words: The IFTC of a block-function in frequency domain is a sinc-function in time domain as depicted in Fig. 7.

### FTC Sinusoidal
The following derivations describe the evaluation of the FTC of a sinuoidal function:
\begin{eqnarray}
&& x(t) = \cos (2 \pi F\_0 t)
= \frac{1}{2} e^{j2 \pi F\_0 t} + \frac{1}{2} e^{-j2 \pi F\_0 t} \newline
&& \mathcal{F}\\{e^{j2 \pi F_0 t}\\}
= \int\_{-\infty}^{\infty} e^{-j2 \pi (f-F\_0) t} \text{d} t \overset{\color{red}{\text{GPI}}}{=} \delta(f-F\_0) \newline
&& \mathcal{F}\\{e^{-j2 \pi F_0 t}\\}
= \int\_{-\infty}^{\infty} e^{-j2 \pi (f+F\_0) t} \text{d} t \overset{\color{red}{\text{GPI}}}{=} \delta(f+F\_0) \newline
\end{eqnarray}
$$
\Rightarrow \quad \mathcal{F}\\{\cos (2 \pi F\_0 t)\\}= \frac{1}{2} \delta(f-F\_0) + \frac{1}{2} \delta(f+F\_0)
$$
In the first step we use Euler to split the signal into phasors. Then we can use for each of these phasor the GPI property, which results in a sum of two delta pulses in the frequency domain.
In other words the frequency distribution of a sinusoidal signal, which runs from minus to plus infinity, is zero for all frequencies, except for the two frequencies of the phasor components of the sinusoidal signal the result is infinite. The result is depicted in Fig. 8.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCCos2Deltas.svg"
      alt="IFTC of frequency domain block results in sinc in time domain."
    />
    <figcaption class="numbered">
      IFTC of frequency domain block results in sinc in time domain.
    </figcaption>
  </figure>
</div>


#### Sufficient condition for existence of FTC
We have shown that a sufficient condition for the FTC to exist is that the integral of the absolute value of the signal $x(t)$ should be bounded, thus $\int\_{-\infty}^{\infty}|x(t)| \text{d}t < \infty$. However, when we take the integral of the absolute value of the previous sinusoidal signal, the result is not bounded. In other words since we have found a valid FTC result for the sinusoidal signal, it follows that the given condition for the existence of the FTC is a sufficient but not a necessary condition.

#### Comparison with FS Sinusoidal
When viewing the sinusoidal signal $x(t)$ as a periodic signal $x\_p(t)$, we can evaluate the frequency content by applying the Fourier Series of one period. The first steps of these derivations are as follows:
\begin{eqnarray}
\alpha\_{k} &=& \frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2} x\_p(t) e^{-j2 \pi k F\_0 t} \text{d}t  =
\frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2} \cos (2 \pi F\_0 t) e^{-j2 \pi k F\_0 t} \text{d}t  \newline
&=& \frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2}
\left ( \frac{1}{2} e^{j2 \pi F\_0 t} + \frac{1}{2} e^{-j2 \pi F\_0 t} \right )  e^{-j2 \pi k F\_0 t} \text{d}t  \newline
&=& \frac{1}{2 T\_0} \int\_{-T\_0/2}^{T\_0/2} e^{-j2 \pi (k-1) F\_0 t} \text{d}t +
\frac{1}{2 T\_0} \int\_{-T\_0/2}^{T\_0/2} e^{-j2 \pi (k+1) F\_0 t} \text{d}t
\end{eqnarray}
Using the General Phasor Integral Property for Fourier Series GPI-FS, it follows that the result is zero except for frequencies $\pm F\_0$. For these frequencies the result is finite, namely 1/2 as denoted in the following equation:
$$
\Rightarrow \quad \alpha\_{k} \overset{\text{GPI-FS}}{=}
\begin{cases}
\frac{1}{2} & \text{for } f= (\pm 1) \cdot F\_0 \newline
0 & \text{elsewhere}
\end{cases}
$$


This result is also depicted in Fig 9.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FSCos2Pulses.svg"
      alt="FS of sinusoidal signal."
    />
    <figcaption class="numbered">
      FS of sinusoidal signal.
    </figcaption>
  </figure>
</div>
From this result it follows that the main difference between the FTC and FS of a sinusoidal signal is the finiteness of the value at the phasor frequencies $\pm F_0$ of the sinusoidal signal. The main "mathematical" reason for this difference is the fact that the integral of the FS is taken of one period, while the integral of the FTC is calculated from $-\infty$ to $+\infty$.

### FTC Deltas
As a final example we will evaluate the FTC of an infinite train of delta pulses in time domain as depicted in Fig. 10.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/Deltas.svg"
      alt="FTC of infinite train of delta pulses."
    />
    <figcaption class="numbered">
      FTC of infinite train of delta pulses.
    </figcaption>
  </figure>
</div>

This result will be used for the explanation of the conversion from continuous to discrete time domain.

The first step in evaluating the FTC is to find an alternative representation for the infinite pulse train. For this we view the infinite pulse train as a periodic signal with period $T$, such that we can write this signal as an infinite sum of weighted phasors. The weights $\alpha\_n$ can be evaluated by the FS integral as follows:
$$
x(t)=\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T)
\overset{\text{FS}}{\widehat{=}} \sum\_{n=-\infty}^{\infty} \alpha\_n e^{j2 \pi \frac{1}{T} n t}
$$
$$
\text{with } \alpha\_n= \frac{1}{T} \int\_{-T/2}^{T/2} \delta(t) e^{-j2 \pi \frac{1}{T} n t} \text{d} t = \frac{1}{T} \hspace{2mm} \forall n
$$
From this it follows that we obtain the following alternative expression for the train of delta pulses:
$$
x(t)=\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T) \widehat{=} \frac{1}{T} \sum\_{n=-\infty}^{\infty} e^{j2 \pi \frac{1}{T} n t}
$$
In other words the FTC of the infinite train of delta pulses can be evaluated by applying the FTC of the infinite sum of phasors which results in the following derivation:
\begin{eqnarray}
\mathcal{F}\\{x(t)\\} &=&
\int\_{-\infty}^{\infty} \left ( \sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T)
\right ) e^{-j2 \pi f t} \text{d}t  \newline
&=& \int\_{-\infty}^{\infty} \left ( \frac{1}{T} \sum\_{n=-\infty}^{\infty} e^{j2 \pi \frac{1}{T} n t} \right ) e^{-j2 \pi f t} \text{d}t  \newline
&=& \frac{1}{T} \sum\_{n=-\infty}^{\infty} \left ( \int\_{-\infty}^{\infty}
e^{j2 \pi \frac{1}{T} n t} e^{-j2 \pi f t} \text{d}t \right )  \newline
&=& \frac{1}{T} \sum\_{n=-\infty}^{\infty} \left ( \int\_{-\infty}^{\infty}
e^{-j2 \pi (f - \frac{n}{T}) t} \text{d}t \right )
\overset{\text{GPI}}{=}
\frac{1}{T} \sum\_{n=-\infty}^{\infty} \delta (f - \frac{n}{T} )
\end{eqnarray}

First we changed the order of integration and summation and then we combined the two phasors. After that we used the GPI property which results in an infinite train of delta pulses in frequency domain as denoted in the following equation and depicted in Fig. 11.
$$
\boxed{
\begin{eqnarray}
\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T) & \overset{\text{FTC}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} &
\frac{1}{T} \sum\_{n=-\infty}^{\infty} \delta (f - \frac{n}{T} )
\end{eqnarray}}
$$
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCDeltasDeltas.svg"
      alt="FTC of a train of delta pulses."
    />
    <figcaption class="numbered">
      FTC of a train of delta pulses.
    </figcaption>
  </figure>
</div>
Note that the resulting train of delta pulses in frequency domain is scaled by the factor 1/T and that the inter-pulse-distance is inversely proportional to the inter-pulse-distance in time domain.
In other words, if we increase the period $T$ in the time domain, by taking less pulses per time unit, the repetitions of the pulses in frequency domain become spaced more closely.
This property is the basis for the so-called aliasing effect of an A-to-D convertor.

<br></br>


## FTC Properties
In this section we will discuss the main properties of the FTC.

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/rz5kJ13gMck" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Linearity
As a result of the fact that the integration operation of the FTC is a linear operation it follows that the FTC is linear.
\begin{eqnarray}
x(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ X(f) \quad\text{ and }\quad y(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ Y(f)
\end{eqnarray}
$$
\boxed{
\begin{eqnarray}
a \cdot x(t) + b \cdot y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
a \cdot X(f) + b \cdot Y(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of linearity property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
\begin{eqnarray}
  \mathcal{F}\{a \cdot x(t) + b \cdot y(t)\} &&=\int_{-\infty}^{\infty} \left ( a \cdot x(t) + b \cdot y(t) \right ) e^{-j2 \pi f t}  \text{d} t  \\
&&=  \int_{-\infty}^{\infty} \left ( a \cdot x(t) \right ) e^{-j2 \pi f t}  \text{d} t +
 \int_{-\infty}^{\infty} \left ( b \cdot y(t) \right ) e^{-j2 \pi f t}  \text{d} t  \\
&&= a \cdot \int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t +
 b \cdot \int_{-\infty}^{\infty} y(t) e^{-j2 \pi f t}  \text{d} t \\
&&= a \cdot X(f) + b \cdot Y(f)
\end{eqnarray}
The linearity property implies that of the sum of signals equals the sum of the FTC's of the signals.
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
As an example of this linear property we calculate the FTC of a sinusoidal signal.
By using Euler we can write the signal into two phasors.
Each of these phasors transforms into a delta pulse in frequency domain.
\begin{eqnarray}
\text{Euler } \rightarrow \text{ }\cos(2 \pi f_0 t) &=& \frac{1}{2} e^{j2 \pi f_0 t}+\frac{1}{2} e^{-j2 \pi f_0 t}  \\
e^{j2 \pi f_0 t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& \delta(f-f_0)  \\
e^{-j2 \pi f_0 t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& \delta(f+f_0)
\end{eqnarray}
By using the linearity property we can now write the FTC of the sum of phasors  as the sum of the FTC's of the two individual phasors.
\begin{eqnarray}
\Rightarrow \text{ } \mathcal{F}\{\cos(2 \pi f_0 t)\} &=& \mathcal{F}\{\frac{1}{2} e^{j2 \pi f_0 t}+\frac{1}{2} e^{-j2 \pi f_0 t}\}\\
&=& \frac{1}{2} \mathcal{F}\{e^{j2 \pi f_0 t}\}+\frac{1}{2} \mathcal{F}\{e^{-j2 \pi f_0 t}\}\\
&=& \frac{1}{2}\delta(f-f_0) + \frac{1}{2}\delta(f+f_0)
\end{eqnarray}
Thus the FTC of a cosine signal consists of  a sum of two delta pulses in the frequency domain.
</div>
</div>



### Conjugation
$$
\boxed{
\begin{eqnarray}
x^\ast(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  X^\ast(-f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of conjugation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the conjugation property  is to move the conjugation sign outside the integral.  Inside the brackets this results into an FTC from which the phasor has a positive sign, which writes as $X(-f)$.
\begin{eqnarray}
y(t) = x^\ast(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ
Y(f)&=&\int_{-\infty}^{\infty} x^\ast(t) e^{-j2 \pi f t} \text{d} t
= \left ( \int_{-\infty}^{\infty} x(t) e^{j2 \pi f t} \text{d} t \right )^*  \\
&=& \left ( X(-f) \right )^\ast=X^\ast(-f)
\end{eqnarray}
The final notation $X^\ast(-f)$  is just simpler way of the notation $(X(-f))^\ast$.
An important result of this conjugation property is that FTC $X(f)$ of a real signal $x(t)$, thus when $x(t)=x^\ast(t)$, has the following symmetry properties:
\\
The magnitude response is symmetric, while the phase response is anti-symmetric, thus:
$$
x(t) \text{ real } \Rightarrow \hspace{2mm} x(t)=x^\ast(t) \hspace{2mm} \Rightarrow  \hspace{2mm} X(f)=X^\ast(-f) \hspace{2mm} \Rightarrow
$$
\begin{eqnarray}
|X(f)| = |X(-f)| &:& \quad\textbf{Magnitude response symmetric}\\
\angle \{X(f)\} = - \angle \{X(f)\} &:& \quad\textbf{Phase response anti-symmetric}
\end{eqnarray}
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
A simple example of these symmetry properties can be found in the FTC of a shifted delta pulse. For this case the time domain signal is a real and the FTC results in a complex exponent as follows:
\begin{eqnarray}
x(t)=\delta(t-t_0) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ X(f)&= \int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t} \text{d} t  \\
&&= \int_{-\infty}^{\infty} \delta(t-t_0) e^{-j2 \pi f t} \text{d} t
= e^{-j2 \pi f t_0}
\end{eqnarray}
From this result it folows that the magnitude response equals 1, while the phase response equals $-2\pi t_0$.
\begin{eqnarray}
\textbf{Symmetric Magnitude response} &:& \quad |X(f)|=|e^{-j2 \pi f t_0}|=1  \\
\textbf{Anti-symmetric Phase response} &:& \quad \angle \{X(f)\} = -2 \pi t_0
\end{eqnarray}
A plot of this magnitude- and phase response is depicted in the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCshiftedDelta.svg"
      alt="Magnitude and phase response of shifted delta pulse."
    />
    <figcaption>
      Magnitude and phase response of shifted delta pulse.
    </figcaption>
  </figure>
</div>
From this plot the symmetry properties are clearly visible.
Note finally that for this case the angle of the phase response is directly related to the shift in time domain.
</div>
</div>

### Scaling
$$
\boxed{
\begin{eqnarray}
x(k \cdot t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{1}{|k|} X(f/k)
\hspace{3mm} \text{with } k \neq 0
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of scaling property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
$$
y(t) = x(k \cdot t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ Y(f) = \int_{-\infty}^{\infty} x(k \cdot t) e^{-j2 \pi f t}
$$
For the proof of the scaling property it is the easiest to split the proof into two cases.
For $k>0$ we substitute for the scaled variable $k \cdot t$ a new variable $\tau$ which leads straightforward to the following result:
$$
Y(f) \overset{\tau =k \cdot t}{=} \int_{-\infty}^{\infty} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \cdot \frac{1}{k} \text{d} \tau
= \frac{1}{k} X(\frac{f}{k})
$$
For $k<0$ we follow the same procedure. But now the boundaries of the integral are changed. Changing these boundaries causes an extra minus sign. As a last step we take the absolute value of $k$ which combines the negative sign together with the negative value of $k$.
\begin{eqnarray}
Y(f) &\overset{\tau =k \cdot t}{=}& \int_{{\color{red}+\infty}}^{{\color{red}-\infty}} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \cdot \frac{1}{k} \text{d} \tau  \\
&=& \frac{{\color{red}-1}}{k} \int_{{\color{red}-\infty}}^{{\color{red}+\infty}} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \text{d} \tau = \frac{1}{|k|} X(\frac{f}{k})
\end{eqnarray}
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
previously we have shown that the FTC of a block signal results in a sinc function, as given in the following equation and depicted in  the figure below.
$$
x(t)= \begin{cases}
1 & \text{for } -\frac{T_0}{2} < t < \frac{T_0}{2} \\
0 & \text{elsewhere}
\end{cases}
\hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm}
X(f) = T_0 \frac{\sin (\pi f T_0)}{\pi f T_0}
$$
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCscaledBlock.svg"
      alt="Result of scale operation applied to a block function."
    />
    <figcaption>
      Result of scale operation applied to a block function.
    </figcaption>
  </figure>
</div>
The figure shows an example in which applied a scale factor of 2: The time domain signal has shrunk by a factor of 2, while the frequency domain signal is stretched by a factor 2.
</div>
</div>
This leads to the following important "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Shrinking in one domain implies stretching in the other domain.</i></div>


### Shift properties

#### Time domain shift
$$
\boxed{
\begin{eqnarray}
x(t-t_0) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  e^{-j2 \pi f t_0} \cdot X(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of time shifting property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof is to change everywhere the variable $t$ by $t-t_0$.
\begin{eqnarray}
x(t-t_0) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \int_{-\infty}^{\infty} x(t-t_0) e^{-j2 \pi f t} \text{d} t \\
&=& \int_{-\infty}^{\infty} x(\color{red}{t-t_0}) e^{-j2 \pi f (\color{red}{t-t_0}+ \color{blue}{t_0})} \text{d} (\color{red}{t-t_0})
\end{eqnarray}
In the next step we take out the negative exponent with the term $t_0$ and substitute $t-t_0$ by $\tau$, which leads to the final result as follows:
\begin{eqnarray}
&\overset{\color{red}{\tau}=t-t_0}{=}&  e^{-j2 \pi f \color{blue}{t_0}} \cdot \int_{-\infty}^{\infty} x(\color{red}{\tau}) e^{-j2 \pi f \color{red}{\tau}} \text{d} {\color{red}\tau} \\
&=& e^{-j2 \pi f t_0} \cdot X(f)
\end{eqnarray}
</div>
</div>

#### Frequency domain shift
$$
\boxed{
\begin{eqnarray}
e^{j2 \pi f_0 t} \cdot x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &   X(f-f_0)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of frequency shifting property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The steps of this proof are similar to the previous ones and are as follows:
\begin{eqnarray}
\mathcal{F}^{-1}\{X(f-f_0)\} &=& \int_{-\infty}^{\infty} X(f-f_0) e^{j2 \pi f t} \text{d} f \\
&=& \int_{-\infty}^{\infty} X({\color{red}f-f_0}) e^{j2 \pi ({\color{red}f-f_0} + {\color{blue}f_0}) t} \text{d} ({\color{red}f-f_0}) \\
&\overset{{\color{red}\eta}=f-f_0}{=}&  e^{j2 \pi {\color{blue}f_0} t} \cdot \int_{-\infty}^{\infty} X({\color{red}\eta}) e^{j2 \pi {\color{red}\eta} t} \text{d} {\color{red}\eta}
= e^{j2 \pi f_0 t} \cdot x(t)
\end{eqnarray}
</div>
</div>


#### Modulation
A result of this frequency shift property is the following modulation property:
\begin{eqnarray}
e^{j2 \pi f_0 t} \cdot x(t) + e^{-j2 \pi f_0 t} \cdot x(t)
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&   X(f-f_0) + X(f+f_0)  \newline
\Leftrightarrow \hspace{3mm} 2 {\color{red}\cos (2 \pi f_0 t) \cdot } x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &   X(f-f_0) + X(f+f_0)
\end{eqnarray}
Thus when multiplying, or modulating, a signal $x(t)$ with a sinusoidal signal, the result in the frequency domain is a sum of two shifted versions of the FTC $X(f)$ of signal $x(t)$ which results into the following "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Modulation in one domain is shifting in the other domain..</i></div>


### Convolution

#### Time domain convolution
$$
\boxed{
\begin{eqnarray}
x(t) \star y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  X(f) \cdot Y(f)
\end{eqnarray}}
$$
<div class="example">
<h4> Proof of time domain convolution property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the time domain convolution property is to use the definition of the convolution integral into the FTC definition.
\begin{eqnarray}
\mathcal{F}\{\color{red}{x(t) \star y(t)}\} &=& \int_{t=-\infty}^{\infty} \left ( {\color{red}\int_{\tau= -\infty}^{\infty} x(\tau) y(t-\tau) \text{d} \tau }\right ) e^{-j2 \pi f t} \text{d} t
\end{eqnarray}
Then by interchanging the order of the integrals  and introducing in the second integral everywhere the variable $t-\tau$, this results in an extra phasor component $e^{-j2 \pi f \tau}$ in the first integral.
\begin{eqnarray}
\ldots
&=& \int_{\tau=-\infty}^{\infty} x(\tau) \left ( \int_{t=-\infty}^{\infty}  y(t-\tau)
e^{-j2 \pi f t} \text{d} t \right ) \text{d} \tau \\
&=& \int_{\tau=-\infty}^{\infty} x(\tau) e^{-j2 \pi f {\color{red}\tau}} \left ( \int_{t=-\infty}^{\infty}  y(t-\tau) e^{-j2 \pi f (t-{\color{red}\tau}) } \text{d} t \right ) \text{d} \tau
\end{eqnarray}
Finally by substituting $t-\tau$ by a new variable  $p$ we obtain the final result.
\begin{eqnarray}
\ldots &=& \left ( \int_{\tau=-\infty}^{\infty} x(\tau) e^{-j2 \pi f \tau} \text{d} \tau \right ) \cdot \left ( \int_{p=-\infty}^{\infty}  y(p) e^{-j2 \pi f p } \text{d} p \right ) \\
&=& X(f) \cdot Y(f)
\end{eqnarray}
</div>
</div>


#### Frequency domain convolution
$$
\boxed{
\begin{eqnarray}
x(t) \cdot y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(f) \star Y(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of frequency domain convolution property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the frequency domain convolution property is  to use the definition of Inverse FTC for the signal $x(t)$.
\begin{eqnarray}
\mathcal{F}\{x(t) \cdot y(t)\} &=& \int_{t=-\infty}^{\infty} \color{red}{x(t)} \cdot y(t) e^{-j2 \pi f t} \text{d} t\\
&=& \int_{t=-\infty}^{\infty} \left ( \color{red}
{\int_{\eta=-\infty}^{\infty} X(\eta) e^{j2 \pi \eta t} \text{d} \eta }
\right ) \cdot y(t) e^{-j2 \pi f t} \text{d} t
\end{eqnarray}
Then by interchanging the order of the integrals and  combining the two phasor components of the second integral we obtain (in red) the shifted FTC of the signal $y(t)$. The resulting integral is the convolution integral of $X(f)$ with $Y(f)$.
\begin{eqnarray}
\ldots&=& \int_{\eta=-\infty}^{\infty} X(\eta) \left (
\int_{t=-\infty}^{\infty} y(t) e^{j2 \pi \eta t} e^{-j2 \pi f t} \text{d} t
\right ) \text{d} \eta \\
&=& \int_{\eta=-\infty}^{\infty} X(\eta) \left ( \color{red}{
\int_{t=-\infty}^{\infty} y(t) e^{-j2 \pi (f- \eta) t} \text{d} t }
\right ) \text{d} \eta \\
&=& \int_{\eta=-\infty}^{\infty} X(\eta) \color{red}{Y(f-\eta)} \text{d} \eta
= X(f) \star Y(f)
\end{eqnarray}
</div>
</div>

This leads to the following important "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication in one domain results in convolution in the other domain.</i></div>

<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
As an example of the convolution property we will use the modulation property as discussed before. In this example signal $x(t)$ is a sinc function as depicted in the upper left side of the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCModulateSinc.svg"
      alt="Modulation in time domain results in frequency shifts of the spectrum."
    />
    <figcaption>
      Modulation in time domain results in frequency shifts of the spectrum.
    </figcaption>
  </figure>
</div>
Previously we have shown that the sinc function is the result of the IFTC of a frequency domain block function, as depicted on in the upper right side of the figure. Multiplying signal $x(t)$ with a sinusoidal signal with frequency $f_0$, which is a modulation operation, is according to the last "rule of thumb" equivalent to the convolution of the FTC $X(f)$ with the FTC of the sinusoidal. The FTC of the sinusoidal consists of two delta pulses, $\delta(f-f_0)$ and $\delta(f+f_0)$, as depicted in the middle part of the figure. Convolving $X(f)$ with a delta pulse results in a shift, which can be shown as follows:
\begin{eqnarray}
\delta(f \pm f_0) \star X(f) &=& \int_{\eta=-\infty}^{\infty} \delta(\eta \pm f_0) X(f-\eta) \text{d} \eta = X(f \pm f_0)
\end{eqnarray}
The result is shown in the lower part of the figure.
</div>
</div>





### Differentiation

#### Time domain differentiation
$$
\boxed{
\begin{eqnarray}
\frac{\text{d} }{\text{d} t} x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & j \omega X(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of time domain differentiation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
By using the IFTC definition of $x(t)$ and differentiating both sides with respect to $t$ we obtain:
$$
\frac{\text{d} }{\text{d} t} x(t) = \frac{\text{d} }{\text{d} t} \left (
\int_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f \right )
= \int_{-\infty}^{\infty} X(f) (j 2 \pi f) e^{j2 \pi f t} \text{d} f
= \mathcal{F}^{-1}\{j \omega X(f) \}
$$
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Find the FTC of the signal $x(t)= \frac{\text{d} }{\text{d} t} \delta(t)$.
<button class="collapsible">Show example</button>
<div class="content">
Taking the FTC of both sides gives:
$$
X(f)= \mathcal{F}\{\frac{\text{d} }{\text{d} t} \delta(t)\}  = j \omega \cdot \mathcal{F}\{ \delta(t) \} = j \omega \cdot 1 = j \omega
$$
</div>
</div>


#### Frequency domain differentiation
$$
\boxed{
\begin{eqnarray}
t x(t)  & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f)
\end{eqnarray}}
$$


<div class="example">
<h4> Proof of frequency domain differentiation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
Differentiation of both sides of the FTC difinition gives:
\begin{eqnarray*}
\frac{\text{d}}{\text{d} f} X(f) &=& \int_{-\infty}^{\infty} x(t) (-j 2 \pi t) e^{-j2 \pi f t}  \text{d} t = - j 2 \pi \int_{-\infty}^{\infty} t x(t)  e^{-j2 \pi f t}  \text{d} t = - j 2 \pi \mathcal{F}\\{t x(t)}
\end{eqnarray*}
Finally, multiplying both sides by the complex number $j$ results into:
$$
\frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f) = \mathcal{F}\\{t x(t)}
$$
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Find the FTC of $x(t) = t \cos(2 \pi F_0 t)$
<button class="collapsible">Show example</button>
<div class="content">
\begin{eqnarray}
X(f) &=& \mathcal{F}\{t \cos(2 \pi F_0 t)\} = \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f}
\left [\mathcal{F}\{ \cos(2 \pi F_0 t)\} \right ] \\
&=& \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} \left [
\frac{1}{2} \delta(f-F_0) + \frac{1}{2} \delta(f+F_0) \right ]
\end{eqnarray}
</div>
</div>



### Theorem Parseval
$$
\boxed{
\begin{eqnarray}
\int\_{-\infty}^{\infty} |x(t)|^2 \text{d} t &=& \int\_{-\infty}^{\infty} |X(f)|^2 \text{d}f
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of the Parseval theorem </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
In the first step of the proof we replace the complex conjugated version of $x(t)$ by the IFTC of the FTC of $x^\ast(t)$.
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t &=& \int_{-\infty}^{\infty} x(t) \color{red}{x^\ast(t)} \text{d} t
= \int_{-\infty}^{\infty} x(t) \mathcal{F}^{-1}\{ \color{red}{\mathcal{F} \{x^\ast(t)\}}\} \text{d} t
\end{eqnarray}
Using the FTC property of complex conjugation  and then applying the IFTC to this result gives:
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t
&=&\int_{-\infty}^{\infty} x(t) \mathcal{F}^{-1}\{\color{red}{ X^\ast(-f)}\} \text{d} t \\
&=& \int_{-\infty}^{\infty} x(t) \left (
\int_{-\infty}^{\infty} X^\ast(-f) e^{j2 \pi f t} \text{d} f \right ) \text{d} t
\end{eqnarray}
Finally interchanging the variable $-f$ by $f$ and then interchanging the order of the integrals and using the FTC definition leads to the final result.
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t
&=& \int_{-\infty}^{\infty} x(t) \left (
\int_{-\infty}^{\infty} X^\ast(f) e^{-j2 \pi f t} \text{d} f \right ) \text{d} t \\
&=& \int_{-\infty}^{\infty} X^\ast(f)  \left ( \color{red}{
\int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t} \text{d} t } \right ) \text{d} f \\
&=& \int_{-\infty}^{\infty} |X(f)|^2 \text{d} f
\end{eqnarray}
</div>
</div>

Concluding it follows that the theorem of Parseval states that the energy in time- and frequency-domain is the same. This implies that the FTC cannot introduce or lose energy, which leads to the following "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Energy in one domain is the same as energy in the other domain.</i></div>

<div class="example">
<h4> Example </h4>
<hr>
In this example the goal is to calculate the energy of a time domain sinc function as depicted on the left side of the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/IFTCBlock.svg"
      alt="IFTC of block."
    />
  </figure>
</div>
<br>
<button class="collapsible">Show example</button>
<div class="content">
When using the definition of a sinc function we can calculate the energy as follows:
\begin{eqnarray}
E &=& \int_{t=-\infty}^{\infty} |{\color{red}x(t)}|^2 \text{d} t
=\int_{t=-\infty}^{\infty} |2 F_c \text{sinc}(2 \pi F_c t)|^2 \text{d} t \\
&=&  \int_{t=-\infty}^{\infty} |2 F_c \frac{\sin(2 \pi F_c t)}{2 \pi F_c t}|^2 \text{d} t
\end{eqnarray}
The evaluation of this integral is not trivial. However, when using the theorem of Parseval we can find the same result by evaluating the energy in frequency domain. As shown before the FTC of a time domain sinc function is a block function in  frequency domain, as depicted on the right side of the figure above and the result is as follows:
\begin{eqnarray}
E &=& \int_{t=-\infty}^{\infty} |{\color{red}x(t)}|^2 \text{d} t \\
&\overset{\text{Parseval}}{=} & \int_{f=-\infty}^{\infty} |{\color{blue}X(f)}|^2 \text{d} f = \int_{f=-F_c}^{F_c} |1|^2 \text{d} f  = 2 F_c
\end{eqnarray}
</div>
</div>

<br></br>


## Summary

<b><u>Definition FTC and IFTC</u></b>

$$
\boxed{
\begin{eqnarray}
X(f)=\int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f
\end{eqnarray}}
$$

$$
\boxed{
\begin{eqnarray}
X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \text{d} \omega
\end{eqnarray}}
$$
<br>
<b><u>Existence and convergence FTC</u></b>
\begin{eqnarray}
\left | X(f) \right | < \infty & \leftrightarrow &
\int_{-\infty}^{\infty} \left | x(t) \right | \text{d} t < \infty
\end{eqnarray}

<br>
<b><u>General Phasor Integral property (GPI)</u></b>
\begin{eqnarray}
\int_{-\infty}^{\infty}  e^{-j2 \pi (f \pm f\_0) t} \text{d} t
&\overset{\text{GPI}}{=}& \delta(f \pm f\_0)
\end{eqnarray}

<br>
<b><u>Basic Fourier transform pairs</u></b>
\begin{eqnarray}
x(t)= \delta(t) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=1 \hspace{2mm} \forall f \newline
x(t)=1 \hspace{2mm} \forall t &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\delta(f) \newline
x(t) = \begin{cases}
1 & \text{for } |t| \leq T_0/2 \newline
0 & \text{elsewhere}
\end{cases}
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)= T_0 \frac{\sin(\pi f T_0)}{\pi f T_0} \newline
2 F_c \frac{\sin(2\pi F_c t)}{2\pi F_c t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&
X(f) = \begin{cases}
1 & \text{for } |f| \leq F_c \newline
0 & \text{elsewhere}
\end{cases}\newline
x(t) = \cos (2 \pi F_0 t) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\frac{1}{2} \delta(f-F_0) + \frac{1}{2} \delta(f+F_0) \newline
x(t)=\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\frac{1}{T} \sum\_{n=-\infty}^{\infty} \delta (f - \frac{n}{T} )
\end{eqnarray}

<br>
<b><u> Main properties </u></b>
<ul>
<li> Linearity: $a \cdot x(t) + b \cdot y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } a \cdot X(f) + b \cdot Y(f)$</li>
<li> Conjugation: $x^\ast(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ }  X^\ast(-f)$ </li>
<li> Scaling: $x(k \cdot t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } \frac{1}{|k|} X(f/k) \hspace{3mm}$ with $k \neq 0$ </li>
<li> Time domain shift: $x(t-t_0) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } e^{-j2 \pi f t_0} X(f)$ </li>
<li> Frequency domain shift: $e^{j2 \pi f_0 t} x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ
\text{ } X(f-f_0)$ </li>
<li> Modulation: $2 \cos(2 \pi f_0 t) \cdot x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f-f\_0) + X(f+f\_0)$ </li>
<li> Time domain convolution: $x(t) \star y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f) \cdot Y(f)$ </li>
<li> Frequency domain convolution: $x(t \cdot y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f) \star Y(f)$ </li>
<li> Time domain differentiation: $\frac{\text{d} }{\text{d} t} x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } j \omega X(f)$ </li>
<li> Frequency domain differentiation: $t x(t)  \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f)$ </li>
<li> Theorem of Parseval: $\int\_{-\infty}^{\infty} |x(t)|^2 \text{d} t = \int\_{-\infty}^{\infty} |X(f)|^2 \text{d}f$ </li>
</ul>

<br>
<b><u>Main "rules of thumb" </u></b>
\begin{eqnarray}
\text{Shrinking} &\leftrightarrow& \text{Stretching} \newline
\text{Multiplication} &\leftrightarrow& \text{Convolution}\newline
\text{Modulation} &\leftrightarrow& \text{Shifting}\newline
\text{Energy} &\leftrightarrow& \text{Energy}
\end{eqnarray}
