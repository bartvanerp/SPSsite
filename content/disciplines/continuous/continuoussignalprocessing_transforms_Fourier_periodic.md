+++
title = "Periodic signals"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Periodic signals"
  weight = 1
  parent = "Transforms II: Fourier series"
+++


In this section we will show that any periodic signal with a, so called, Fundamental period $T_0$ can be composed as the sum of sinusoidal signals from which each of these frequencies is related to the, so called, Fundamental frequency $F_0 = 1/T_0$ as an integer multiple. In order to show this Fig. 1 depicts a signal $y_2(t)$ which is composed of the sum of two sinusoidal signals $x_1(t)$ of frequency $f_1 = 6$ [Hz] and $x_2(t)$ of frequency $f_2 = 2$ [Hz]. From this figure it follows that $y_2(t)$ is periodic and we can measure that the period equals $T_0 = 1/F_0 = 0.5$ [sec]. The reason for this periodicity of signal $y_2(t)$ is that exactly three periods of $x_1(t)$ and one period of $x_2(t)$ fit into one period $T_0$ of signal $y_2(t)$. Thus after each $T_0 = 0.5$ [sec] the same composition of the signals $x_1(t)$ and $x_2(t)$ appears in the signal $y_2(t)$.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/fundamental_frequency.svg"
      alt="Signals of various frequencies with there cumulative signals."
    />
    <figcaption class="numbered">
      Signals of various frequencies with there cumulative signals.
    </figcaption>
  </figure>
</div>

The figure also shows another signal $y_3(t)$ which is composed of the sum three sinusoidal signals. The same sinusoidal signals $x_1(t)$, $x_2(t)$ and a new sinusoidal signal $x_3(t)$, with frequency $f_3 = 1.2$ [Hz]. Again it follows from the figure that $y_3(t)$ is periodic but now we can measure that the period equals $T_0 = 1/F_0 = 2.5$ [sec]. This is because of the fact that exactly fifteen periods of $x_1(t)$, five periods of $x_2(t)$ and three periods of $x_3(t)$ fit into one period $T_0$ of signal $y_3(t)$. Mathematically we can calculate $F_0 = 1/T_0$ of $y_3(t)$ as the Greatest Common Divisor (gcd) of the frequencies from the individual sinusoidal components, since $F_0 = \text{gcd}\\{f_1, f_2, f_3\\} = \text{gcd}\\{6, 2, 1.2\\} = 0.4$ [Hz]. The greatest common divisor of a set of numbers is the largest number that all numbers of that set can be _fully_ divided by. From this it follows that the Fundamental period of $y_3(t)$ equals $T_0 = 1/F_0 = 2.5$ [sec]. This leads to the following general statement:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A real signal $x(t)$, which consists of a DC component and a sum of $N$ different frequencies $f_1, f_2,\ldots, f_N$, with $f_1 &lt f_2 &lt \ldots &lt f_N$, is a periodic signal with Fundamental period $T_0 = 1/F_0$ and has a Fundamental frequency $F_0 = \text{gcd}\{f_1,f_2,\ldots,f_N\} $.</i></div>

In the case that this general statement is true, all $N$ different frequencies of signal $x(t)$ are related by an integer number times the Fundamental frequency $F\_0$. Thus we can define the largest frequency by $f\_N = M\cdot F\_0$ with integer $M \geq N$. With this definition we can write such a periodic signal $x_(t)$ as a weighted sum of phasor components as
$$
x(t) = \sum\_{k=-M}^{M} \alpha_k e^{j2\pi kF_0 t},
$$
in which the complex weights $\alpha_k$ represent the amplitude and phase of the frequency components at frequency $k \cdot F_0$. Finally note that possible $\alpha_0$ and definitely only $N$ out of $M$ complex weights $\alpha_k$ are not equal to zero.


<div class="example">
<h4> Example </h4>
$$
x(t) = 2+2\cos\left(102\pi t-\frac{\pi}{8}\right) - \sin\left(238\pi t +\frac{\pi}{3}\right) + 3\cos\left(340\pi t+\frac{\pi}{2}\right)
$$
Determine if the above signal is periodic and if so calculate the Fundamental frequency $F_0=1/T_0$ and give the general expression for $x(t)$ as in the above equation and make a spectral plot of $x(t)$.
<button class="collapsible">Show solution</button>
<div class="content">
The signal consists out of a DC component and a sum of 3 sinusoids with frequencies $f_1=51$, $f_2=119$ and $f_3=170$ [Hz]. The Fundamental frequency can be determined as $F_0 = \text{gcd}\{ 51, 119, 170\} = 17$ [Hz]. Therefore $x(t)$ is a periodic signal with Fundamental period $T_0=1/F_0=1/17$ [sec]. The relationships between the three frequencies and the Fundamental frequencies are $f_1=51=3\cdot F_0$, $f_2=119=7\cdot F_0$ and $f_3=170=10\cdot F_0$ [Hz].
The highest frequency contains $10$ times the Fundamental frequency and therefore $x(t)$ can be written as
$$
x(t) = \sum_{k=-10}^{10} \alpha_k e^{j2\pi kF_0 t}.
$$
By using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can write $x(t)$ as
$$
\begin{split}
x(t)
&= \frac{3}{2}e^{-j\frac{\pi}{2}}e^{-j2\pi 170t} + \frac{1}{2j}e^{-j\frac{\pi}{3}}e^{-j2\pi 119t} + e^{j\frac{\pi}{8}}e^{-j2\pi 51t} + 2 \newline
&\qquad + e^{-j\frac{\pi}{8}}e^{j2\pi 51t} + \frac{-1}{2j}e^{j\frac{\pi}{3}}e^{j2\pi 119t}  + \frac{3}{2}e^{j\frac{\pi}{2}}e^{j2\pi 170t}.
\end{split}
$$
When comparing the above two equations, the values of $\alpha_k$ can be determined as
$$
\alpha_k =
\begin{cases}
\frac{3}{2}e^{j\frac{\pi}{2}},        &\text{for }k=10\\
\frac{-1}{2j}e^{j\frac{\pi}{3}},      &\text{for }k=7\\
e^{-j\frac{\pi}{8}},                &\text{for }k=3\\
2,      &\text{for }k=0\\
e^{j\frac{\pi}{8}}=\alpha_3^\ast,   &\text{for }k=-3\\
\frac{1}{2j}e^{-j\frac{\pi}{3}}= \alpha_7^\ast,         &\text{for }k=-7\\
\frac{3}{2}e^{-j\frac{\pi}{2}} =\alpha_{10}^\ast,        &\text{for }k=-10\\
0.      &\text{otherwise}
\end{cases}
$$
The spectral plot of $x(t)$ is given in Fig. 2. The x-axis contains both the frequency as the integer values of $k$, which are the frequency divided by the Fundamental frequency.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example3_spectrum.svg"
      alt="Spectral plot of the given function $x(t)$."
    />
    <figcaption class="numbered">
      Spectral plot of the given function $x(t)$.
    </figcaption>
  </figure>
</div>
</div>
</div>
