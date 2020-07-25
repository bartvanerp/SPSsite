+++
title = "IIR filter design"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "IIR filter design [⯈]"
  weight = 3
  parent = "Filter design"
+++


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/PHjR9Y-RgTY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
In contrast to FIR filters, IIR filters have besides zeros also poles and for this reason we have to take care about stability, since a stable filter requires all poles to be within the unit circle.  For FIR filters we have seen that filters with symmetric impulse responses lead to linear phase filters. However, for IIR filters it is not possible to realise linear phase filters or filters with a predefine phase characteristic.  There are powerful highly advanced design procedures that facilitate the design of analog filters.  For this reason a common design approach for IIR digital filters is to first design an analog IIR filter and then map it into an equivalent digital filter.  Here we will discuss the following 3 approaches:
<ol>
  <li>The impulse invariance approach, in which a digital filter is designed by sampling the impulse response of an analog filter.</li>
  <li>Mapping differential equation, which describes the input- output relation of an analog filter, into a difference equation, which describes the input- output relation of a digital filter.</li>
  <li>The bilinear transform, which maps the description of the analog filter in the complex $s$-plane into a description of the digital filter in the complex $z$-plane.</li>
</ol>

<br></br>
## Impulse invariant approach
The impulse invariant approach consists of the following steps:
<ol>
<li>Start with the impulse response $h_a(t)$ of an analog filter, or eventually with the frequency response $H_a(\omega)$, which is related to the impulse response via the Fourier Transform for Continuous time signals (FTC) and systems.</li>
<li>Then the discrete time impulse response $h_d[n]$ is created by sampling $h_a(t)$, with an inter sample distance of $T$ seconds.
$$
h_a(t)|_{t=n \cdot T} = h_d[n] \overset{\mbox{FTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} H_d(e^{j\theta})
=\color{brown}{
\frac{1}{T} \sum_{k=- \infty}^{\infty} H_a(\omega - k \cdot \frac{2 \pi}{T})|_{\omega=\frac{\theta}{T}}}
$$
The discrete time frequency response $H_d(e^{j\theta})$ follows from the FTD. From the module sampling and reconstruction we have seen that as a result of the sampling process  the discrete time frequency response can be constructed as an infinite sum of shifted and overlapped continuous time frequency responses $H_a(\omega)$, in which the shifts are inversely proportional to $1/T$.
The spectral overlap causes aliasing which is the price paid by using this design approach.
</li>
</ol>
As an example, assume the continuous time exponential decaying impulse response $h_a(t)$, with amplitude $A$ and decaying factor $B$.
\begin{eqnarray*}
h_a(t) = \left \{
\begin{array}{cl}
A \mbox{e}^{Bt} & t \geq 0 \\
0 & t<0
\end{array}
\right .
& \overset{\mbox{FTC}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} &
H_a(\omega) = \frac{A}{j \omega - B} \\
&\overset{\mbox{LT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}& H_a(s) = \frac{A}{s-B}
\end{eqnarray*}
The frequency response $H_a(\omega)$ is obtained via the Fourier Transform for Continuous time signals (FTC) and the system function $H_a(s)$ via the Laplace Transform (LT.
The expression for the discrete time impulse response $h_d[n]$ is constructed by sampling the continuous time impulse response $h_a(t)$,  which leads to the following expression for the discrete time frequency response $H_d(e^{j\theta})$:
\begin{eqnarray*}
h_d[n]=h_a(t)|_{T=nT} = A \mbox{e}^{BnT} u[n]
& \overset{\mbox{FTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} &
H_d(e^{j\theta})%= \sum_{n=-\infty}^{\infty} h_d[n] e^{-jn \theta}
=\frac{A}{1 - \mbox{e}^{BT} e^{-j\theta}}\\
& \overset{\mbox{ZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}&  H_d(z) = \frac{A}{1 - \mbox{e}^{BT} z^{-1}}
\end{eqnarray*}
With amplitude $A=2$ and decaying factor $B=-1$, this results in an IIR filter with one feedback loop which contains a multiplication factor of $e^{-T}$, from which the realisation is depicted in Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/realizationex5.svg"
      alt="Realisation of discrete-time filter via impulse variant approach."
    />
    <figcaption class="numbered">
      Realisation of discrete-time filter via impulse variant approach.
    </figcaption>
  </figure>
</div>
For $T=1$ [sec] the results are shown in Fig. 2. The figure shows two plots in black lines. The left hand plot is the continuous time impulse response $h_a(t)$.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example5T1.svg"
      alt="In black: Continuous-time impulse response $h_a(t)$ and its frequency response $|H_a(\omega)|$. In red: Discrete-time impulse response $h_d[n]$ obtained via impulse invariant approach of Fig. \ref{Fig:realizationex5} with $T=1$ [sec] and its frequency response $H_d(e^{j\theta})$."
    />
    <figcaption class="numbered">
      In black: Continuous-time impulse response $h_a(t)$ and its frequency response $|H_a(\omega)|$. In red: Discrete-time impulse response $h_d[n]$ obtained via impulse invariant approach of Fig. \ref{Fig:realizationex5} with $T=1$ [sec] and its frequency response $H_d(e^{j\theta})$.
    </figcaption>
  </figure>
</div>
The plot at the right hand side shows the frequency response $|H_a(\omega)|$, which is depicted as a function of the relative frequency $\theta$ for which we used the conversion $\theta = \omega \cdot T$. In other words the absolute frequency $\omega$ ranges, in this case, from $\omega=-2\pi$ until $\omega=2 \pi$.  The results of sampling the analog impulse response with an inter sample distance of $T=1$ [sec] are shown in red. The right hand plot shows the discrete time magnitude response $|H_d(e^{j\theta})|$. This plot shows two Fundamental Intervals, in which the relative frequency $\theta$ ranges from $-2\pi$ until $2 \pi$. From this plot we clearly see the mismatch with the analog magnitude response, as a result of aliasing.

When sampling with a 4 times finer inter-sample distance of $T=1/4$ [sec] the results are shown in Fig. 3.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example5T14.svg"
      alt="In black: Continuous-time impulse response $h_a(t)$ and its frequency response $|H_a(\omega)|$. In red: Discrete-time impulse response $h_d[n]$ obtained via impulse invariant approach of Fig. \ref{Fig:realizationex5} with $T=1/4$ [sec] and its frequency response $H_d(e^{j\theta})$."
    />
    <figcaption class="numbered">
      In black: Continuous-time impulse response $h_a(t)$ and its frequency response $|H_a(\omega)|$. In red: Discrete-time impulse response $h_d[n]$ obtained via impulse invariant approach of Fig. \ref{Fig:realizationex5} with $T=1/4$ [sec] and its frequency response $H_d(e^{j\theta})$.
    </figcaption>
  </figure>
</div>
From this result we clearly see that the mismatch with the analog magnitude response plot is reduced in comparison with the previous case for $T=1$ [sec]. Finally note that the shown absolute frequency axis now ranges from $\omega = -8\pi$ until $\omega=8 \pi$.

<br></br>
## Mapping differential- to difference-equations
The input output relation of a continuous time system can be described by a differential equation, as shown in the following equation:
$$
y_a(t) = \sum_{i=0}^{N} b_i \frac{d^i x_a(t)}{d t^i} + \sum_{i=0}^{M} a_i \frac{d^i y_a(t)}{d t^i}
\hspace{2mm} \overset{\mbox{LT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \hspace{2mm}
H_a(s)=\frac{\sum_{i=0}^{N} b_i s}{1 - \sum_{i=1}^{M} a_i s}
$$
This differential equation is related to the continuous time system function $H_a(s)$ via the Laplace Transform, abbreviated as LT.

### Approximate differential by backward difference
The first option of this second design approach is to approximate each continuous time differential by  the following backward difference equation in the discrete time domain:
$$
\color{red}{\frac{d y_a(t)}{d t} \approx }
\frac{y_a(nT) - y_a(nT-T)}{T} = \color{red}{\frac{y_d[n] - y_d[n-1]}{T} }
$$
By doing so the system functions in continuous time $H_a(s)$ and discrete time $H_d(z)$ can be related to each other by using the following steps:

First the Laplace Transform of a differential equation is simply a multiplication with the complex variable $s$ in the $S$ domain:
\begin{eqnarray*}
\frac{d y_a(t)}{d t} & \overset{\mbox{LT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} & {\color{brown} s} \cdot Y_a(s)
\end{eqnarray*}
Secondly the backward difference equation transforms via the $Z$ transform to following equation:
\begin{eqnarray*}
\frac{y_d[n] - y_d[n-1]}{T} & \overset{\mbox{ZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} & \frac{Y_d(z) - z^{-1} Y_d(z)}{T} =
\left ( \color{brown}{\frac{1 - z^{-1}}{T}} \right ) \cdot Y_d(z)
\end{eqnarray*}
By comparing these two equations it follows that  the complex variable $s$ is replaced by the complex variable $1-z^{-1}/T$ when approximating the differential by a backward difference or the other way around replace $z$ by $1/(1-sT)$:
\begin{eqnarray*}
s=\frac{1 - z^{-1}}{T} & \leftrightarrow & \color{red}{z = \frac{1}{1-s \cdot T}}
\end{eqnarray*}

### Approximate differential by forward difference
As an alternative we can approximate the differential by  a forward difference equation:
$$
\color{red}{\frac{d y_a(t)}{d t} \approx }
\frac{y_a(nT+T) - y_a(nT)}{T} = \color{red}{\frac{y_d[n+1] - y_d[n]}{T} }
$$
This leads to the result that in this case the complex variable $s$ is replaced by the complex variable $(z-1)/T$, or the other way around
$z$ is replaced by $1+sT$:
\begin{eqnarray*}
s=\frac{z-1}{T} & \leftrightarrow & \color{blue}{z = 1+s \cdot T}
\end{eqnarray*}

### Mapping of poles and zeros with backward and forward approximation
For stable systems it is important that stable poles of the analog system, which are at the left hand side in the complex $S$ plane, are mapped inside the unit circle in the $Z$ plane.  This is automatically the case where the differential is approximated by the backward difference equation.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/szdifferencemapping.svg"
      alt="Mapping between the S-plane to Z-plane for Backward difference and Forward difference approach."
    />
    <figcaption class="numbered">
      Mapping between the S-plane to Z-plane for Backward difference and Forward difference approach.
    </figcaption>
  </figure>
</div>
This is shown in Fig. 4 which shows the relation between the mappings of the $S$ plane to the $Z$ plane.  However, for the case where the differential is approximated by the forward difference  equation, the mapping of the $S$ plane to the $Z$ plane shows that a stable continuous time pole is not guaranteed mapped to a stable discrete time pole.


<div class="example">
<h4> Example </h4>
<hr>
Apply backward and forward difference with $T=1/2$ on the system with system function: $H_a(s) = (2 s+22)/((s+1)(s^2 + 4s + 13))$.
Are both approaches stable?
<button class="collapsible">Show solution</button>
<div class="content">
The system function $H_a(s)$ of this example can be written as follows:
$$
H_a(s) = \frac{2 s+22}{(s+1)(s^2 + 4s + 13)}
=\frac{2 s+22}{(s+1)\cdot (s+2 - 3j) \cdot (s+2 + 3j)}
$$
From this it follows that the system consists of one zero and three poles  which are all three located at the left hand side of the $S$ plane and so the continuous-time system is stable.

Using  the backward difference approach, with sampling rate $T=1/2$,  leads to the following expression:
\begin{eqnarray*}
s_{ba}=2 -2z^{-1}& \Rightarrow &
H_{d,ba}(z)=
\frac{ 26 - 4 z^{-1}}{(3 -2 z^{-1}) \cdot (4 - 3 j - 2 z^{-1}) \cdot (4 + 3 j - 2 z^{-1}) }
\end{eqnarray*}
From this it follows that all poles are inside the unit circle and thus the discrete time system is stable.  However when using the forward difference approach  the result is as follows:
\begin{eqnarray*}
s_{fo}=2z-2& \Rightarrow &
H_{d,fo}(z)=\frac{4z+18}{(2z-1)(2z+3j)(2z-3j)}
\end{eqnarray*}
From this it follows that there are two poles  which are located outside the unit circle and thus the system is not guaranteed to be stable. So we can not use this approach for this example.
</div>
</div>

<br></br>
## Bilinear transform
The third design approach uses the bilinear transform, which is a rational function that maps the left-half $S$ plane inside the unit circle and maps the imaginary axis of the $S$ plane in a one-to-one manner onto the unit circle in the $Z$ plane.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/szbilinear.svg"
      alt="Mapping between the S-plane to Z-plane for bilinear approach."
    />
    <figcaption class="numbered">
      Mapping between the S-plane to Z-plane for bilinear approach.
    </figcaption>
  </figure>
</div>
As depicted in Fig. 5, this is achieved by replacing the complex variable $s$ by the complex function $\frac{1-z^{-1}}{1+ z^{-1}}$ multiplied with $2/T$ or the other way around by replacing the complex variable $z$ by the complex function $\frac{2 + s \cdot T}{2 - s \cdot T}$:
\begin{eqnarray*}
\color{blue}{s=\frac{2}{T} \cdot \frac{1-z^{-1}}{1+ z^{-1}}} & \leftrightarrow & \color{red}{z = \frac{2 + s \cdot T}{2 - s \cdot T}}
\end{eqnarray*}
The figure also shows some important intermediate points of the mapping from the $S$ plane to the $Z$ plane.

The relation between the mapping of the imaginary axis in the $S$ plane onto the unit circle is highly non linear which can be shown as follows:

With $s= j \omega$ and $z=e^{j\theta}$ the transformation with $s= \frac{2}{T} \cdot \frac{1 - z^{-1}}{1+z^{-1}}$ becomes  as follows:
$$
j \cdot \left ( \omega \right )= \frac{2}{T} \cdot \frac{1-e^{-j\theta}}{1+ e^{-j\theta}}=
j \cdot \left ( \frac{2}{T} \frac{\sin (\theta/2)}{\cos (\theta/2)} \right )
= j \cdot \left ( \frac{2}{T} \tan (\theta/2) \right )
$$
From this result we can derive the so called frequency warping function:
$$
\theta = 2 \arctan (\omega T/2)
$$
The result of this non linear mapping is shown in Fig. 6.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/warpingresults.svg"
      alt="Non linear warping result of bilinear transform."
    />
    <figcaption class="numbered">
      Non-linear warping result of bilinear transform.
    </figcaption>
  </figure>
</div>
The figure in blue shows a sketch of a continuous time magnitude response $H_a(\omega)$ as a function of the continuous frequency $\omega$. This function is mapped via the frequency warping function $\theta = 2 \arctan (\omega T/2)$, depicted in black,  onto the discrete time magnitude response $H_d(e^{j\theta})$, which is depicted in red. Note that the continuous frequency axis $\omega$ from $\omega = -\infty$ until $\omega =+\infty$ is mapped onto the discrete frequency axis $\theta$ in the range $\theta=-\pi$ until $\theta =+\pi$, which results in the frequency warping which implies that both magnitude- and phase characteristics are warped  and there is no aliasing in the discrete domain.  Finally it is noted that there is no direct relation between the discrete-time and continuous-time impulse response.
