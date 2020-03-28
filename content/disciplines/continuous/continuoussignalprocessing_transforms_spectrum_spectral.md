+++
title = "Spectral plot"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Spectral plot"
  weight = 2
  parent = "Transforms I: Spectrum of sinusoidal signals"
+++

By ordering the frequencies from low to high we can represent the phasor description in a frequency spectrum plot. In such a plot we denote the frequencies on the horizontal axis. The frequency on this axis can either be denoted by the values of $f_k$ in [Hz] or by the values of $\omega_k = 2\pi f_k$ in [rad/sec]. For each of these frequencies $f_k$ we plot a bar, denoting the complex weights $\frac{X_k}{2}$ as described previously. Note that these complex weights are related to the amplitude and phase of the original sinusoidal signal.

<div class="example">
<h4> Example </h4>
<hr>
Find the complex weights of the phasor components of the signal
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right)$$
and make a spectral plot of the signal.
<button class="collapsible">Show solution</button>
<div class="content">
By using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> the expression for $x(t)$ can be rewritten as
$$
\begin{split}
x(t)
&= 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right), \newline
&= 10\cdot 1 + 14\bigg\{ \frac{e^{j\left(200\pi t - \frac{\pi}{3}\right)} + e^{-j\left(200\pi t -\frac{\pi}{3}\right)}}{2}\bigg\} + 8\bigg\{ \frac{e^{j\left(500\pi t + \frac{\pi}{2}\right)} + e^{-j\left(500\pi t -\frac{\pi}{2}\right)}}{2}\bigg\}, \newline
&= \left(10\right) \cdot e^{j2\pi \cdot 0 \cdot t} + \left(7e^{-j\frac{\pi}{3}}\right) \cdot e^{j2\pi \cdot 100 \cdot t} + \left(7e^{j\frac{\pi}{3}}\right) \cdot e^{-j2\pi \cdot 100 \cdot t} \newline
&\qquad + \left(4e^{j\frac{\pi}{2}}\right) \cdot e^{j2\pi \cdot 250 \cdot t} + \left(4e^{-j\frac{\pi}{2}}\right) \cdot e^{-j2\pi \cdot 250 \cdot t}.
\end{split}
$$
From this it can be seen that the signal contains frequency components at the frequencies $f_0 = 0$, $f_1 = 100$, $-f_1 = -100$, $f_2 = 250$ and $-f_2 = -250$ [Hz], where each phasor is multiplied with its own complex weight, indicating the amplitude and phase of that respective phasor. These complex weights are given by
$$
X_0=10, \quad \frac{X_1}{2} = 7e^{-j\frac{\pi}{3}}, \quad  \frac{X_1^\ast}{2} = 7e^{j\frac{\pi}{3}}, \quad \frac{X_2}{2} = 4e^{j\frac{\pi}{2}}, \quad \frac{X_2^\ast}{2} = 4e^{-j\frac{\pi}{2}}.
$$
The spectral plot of the signal $x(t)$ is shown in Fig. 1.
<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example1_spectrum.svg"
      alt="Spectrum of $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of $x(t)$.
    </figcaption>
  </figure>
</div>  
</div>
</div>

In a spectral plot, such as the one from the previous example, the phasor components of the signal are represented by bars and the corresponding weights are denoted by complex numbers above these bars. The amplitude or magnitude of the complex weights corresponds to the length of the bar. When denoting these complex weights in <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_notation">Polar notation</a> it becomes very easy to 'read from the spectral plot' and to convert the spectral plot back to the time-domain representation of the real signal $x(t)$.

From the spectral plot of the above example it can be noted that the spectrum is symmetric, indicating that we are dealing with a real signal. The spectrum consists of a DC term and two sinusoids. The DC term has a value of 10 and is by definition located at a frequency of $0$ [Hz]. The first sinusoid is located at $100$ [Hz] and has an amplitude of $2\times7 = 14$ and has a phase of $-\frac{\pi}{3}$, which is obtained from the right-hand side of the spectrum. The second sinusoid has an amplitude of $2\times4=8$ and has a phase of $\frac{\pi}{2}$. Keep in mind to read the phase of the sinusoid from the right-hand side of the spectrum, since the left-hand side contains the negated phase.
All together the spectral plot of the above example belongs to the following time-domain representation of signal $x(t)$:
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right).$$

From the above interpretation of the spectral plot we can conclude

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>It is easiest to denote the complex weights corresponding to the individual phasor components in the spectral plot in Polar notation.</i></div>
