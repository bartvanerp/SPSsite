+++
title = "FTC as limit of the FS"

# date = {{ .Date }}
lastmod = 2020-02-29

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "FTC as limit of the FS"
  weight = 1
  parent = "Transforms III: Fourier transform for continuous-time signals"

+++
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
<br></br>

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
<br></br>

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
