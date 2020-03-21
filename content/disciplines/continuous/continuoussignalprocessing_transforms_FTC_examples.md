+++
title = "FTC examples"

# date = {{ .Date }}
lastmod = 2020-02-29

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "FTC examples"
  weight = 2
  parent = "Transforms III: Fourier transform for continuous-time signals"
+++

In this section we will discuss the FTC of some basic signals. As such we will discuss the FTC and IFTC of a delta pulse, a block signal, a sinusoidal signal and finally a pulse train.

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/jWRR689o1zs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## (I)FTC delta pulse and General Phasor Integral (GPI)
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
\begin{eqnarray*}
\int\_{-\infty}^{\infty}  e^{-j2 \pi (f \pm f\_0) t} \text{d} t
&\overset{\text{GPI}}{=}& \delta(f \pm f\_0)
\end{eqnarray*}}
$$

<br></br>

## (I)FTC of block
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
\begin{eqnarray*}
X(f) &=& \int\_{-\infty}^{\infty} x(t) \cdot e^{-j2 \pi f t} \text{d} t =
\int\_{-T\_0/2}^{T\_0/2} 1 \cdot e^{-j2 \pi f t} \text{d} t  \newline
&=&\frac{1}{-2j \pi f} e^{-j2 \pi f t} \left . \right |\_{-T\_0/2}^{T\_0/2} =
\frac{e^{-j2 \pi f T_0/2}- e^{j2 \pi f T\_0/2} }{-2j \pi f}  \newline
&=& T\_0 \frac{\sin(\pi f T\_0)}{\pi f T_0} = T\_0 \ \text{sinc}(\pi f T\_0)
\end{eqnarray*}

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
\begin{eqnarray*}
x(t) &=& \int\_{-\infty}^{\infty} X(f) \cdot e^{j2 \pi f t} \text{d} f =
\int_{-F\_c}^{F\_c} 1 \cdot e^{j2 \pi f t \text{d} f}
= \frac{1}{2j \pi t} e^{j2 \pi f t} \left . \right |\_{-F\_c}^{F\_c}  \newline
&=& \frac{e^{j2 \pi F\_c t}- e^{-j2 \pi F\_c t} }{2j \pi t}
= 2 F\_c \frac{\sin(2\pi F\_c t)}{2\pi F\_c t} = 2 F\_c \ \text{sinc}(2\pi F\_c t)
\end{eqnarray*}

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

<br></br>

## FTC Sinusoidal
The following derivations describe the evaluation of the FTC of a sinuoidal function:
\begin{eqnarray*}
&& x(t) = \cos (2 \pi F\_0 t)
= \frac{1}{2} e^{j2 \pi F\_0 t} + \frac{1}{2} e^{-j2 \pi F\_0 t} \newline
&& \mathcal{F}\\{e^{j2 \pi F_0 t}\\}
= \int\_{-\infty}^{\infty} e^{-j2 \pi (f-F\_0) t} \text{d} t \overset{\color{red}{\text{GPI}}}{=} \delta(f-F\_0) \newline
&& \mathcal{F}\\{e^{-j2 \pi F_0 t}\\}
= \int\_{-\infty}^{\infty} e^{-j2 \pi (f+F\_0) t} \text{d} t \overset{\color{red}{\text{GPI}}}{=} \delta(f+F\_0) \newline
\end{eqnarray*}
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


<br></br>

### Sufficient condition for existence of FTC
We have shown that a sufficient condition for the FTC to exist is that the integral of the absolute value of the signal $x(t)$ should be bounded, thus $\int\_{-\infty}^{\infty}|x(t)| \text{d}t < \infty$. However, when we take the integral of the absolute value of the previous sinusoidal signal, the result is not bounded. In other words since we have found a valid FTC result for the sinusoidal signal, it follows that the given condition for the existence of the FTC is a sufficient but not a necessary condition.

<br></br>

### Comparison with FS Sinusoidal
When viewing the sinusoidal signal $x(t)$ as a periodic signal $x\_p(t)$, we can evaluate the frequency content by applying the Fourier Series of one period. The first steps of these derivations are as follows:
\begin{eqnarray*}
\alpha\_{k} &=& \frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2} x\_p(t) e^{-j2 \pi k F\_0 t} \text{d}t  =
\frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2} \cos (2 \pi F\_0 t) e^{-j2 \pi k F\_0 t} \text{d}t  \newline
&=& \frac{1}{T\_0} \int\_{-T\_0/2}^{T\_0/2}
\left ( \frac{1}{2} e^{j2 \pi F\_0 t} + \frac{1}{2} e^{-j2 \pi F\_0 t} \right )  e^{-j2 \pi k F\_0 t} \text{d}t  \newline
&=& \frac{1}{2 T\_0} \int\_{-T\_0/2}^{T\_0/2} e^{-j2 \pi (k-1) F\_0 t} \text{d}t +
\frac{1}{2 T\_0} \int\_{-T\_0/2}^{T\_0/2} e^{-j2 \pi (k+1) F\_0 t} \text{d}t
\end{eqnarray*}
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

<br></br>

## FTC Deltas
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
\begin{eqnarray*}
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
\end{eqnarray*}

First we changed the order of integration and summation and then we combined the two phasors. After that we used the GPI property which results in an infinite train of delta pulses in frequency domain as denoted in the following equation and depicted in Fig. 11.
$$
\boxed{
\begin{eqnarray*}
\sum\_{n=-\infty}^{\infty} \delta(t - n \cdot T) & \overset{\text{FTC}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} &
\frac{1}{T} \sum\_{n=-\infty}^{\infty} \delta (f - \frac{n}{T} )
\end{eqnarray*}}
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
