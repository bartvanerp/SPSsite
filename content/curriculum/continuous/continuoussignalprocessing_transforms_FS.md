+++
title = "Spectrum and Fourier series"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Spectrum and Fourier series"
  weight = 41
  parent = "Continuous-time transforms"

+++
## Overview
This submodule will cover one of the most fundamental transforms in signal processing, namely the Fourier series. In order to cover this topic first the spectrum of a signal is introduced. This submodule will finally conclude with some (MATLAB) exercises and a summary. Before you get into more detail on the subject matter, familiarize yourself with the topic by watching the introductory screencast video.

### Introductory video
<div>
<video controls preload>
  <source src="/../files/8.Screencast/Fourier/Continuous/FS/1FourierSeriesConcept.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>

## Spectrum
Many practical signals can be described as a set of sinusoidal signals. In this section we will first show how such a set can be rewritten as a set of weighted phasor components. From this description it follows that these weights represent the spectral information of the signal.

### Real signal as sum of phasors
Let us start with a general description of a signal $x(t)$, which consists of a DC component, with value $A_0$, and a sum of $N$ sinusoidal components, each with a different frequency $f_k$, amplitude $A_k$ and phase $\phi_k$, as

$$
x(t) = A_0 + \sum\_{k=1}^{N} A_k\cos \left( 2\pi  f_k t+ \phi_k \right).
$$

Now by using the <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler equations</a> we can write this equation as the following sum of
rotating <a href="../../mathematicalbackground/mathematicalbackground_complex_phasors">phasors</a>:

$$
\begin{split}
x(t) &= A_0 + \sum\_{k=1}^N \bigg\\{ \left(\frac{A_k}{2}e^{j\phi_k}\right)e^{j2\pi f_k t} + \left(\frac{A_k}{2}e^{-j\phi_k}\right)e^{-j2\pi f_k t}\bigg\\} \newline
&= X_0 + \sum\_{k=1}^N \bigg\\{ \frac{X_k}{2}e^{j2\pi f_k t} + \frac{X_k^\*}{2}e^{-j2\pi f_k t} \bigg\\},
\end{split}
$$

where $X_0 = A_0$ and $X_k = A_ke^{j\phi_k}$. From this description we can derive the following general property:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>For real signals the values of the complex weights of the phasors with negative frequencies are the complex conjugated versions of the complex weights of the phasors with positive frequencies.</i></div>

### Spectral plot
By ordering the frequencies from low to high we can represent the phasor description in a frequency spectrum plot. In such a plot we denote the frequencies on the horizontal axis. The frequency on this axis can either be denoted by the values of $f_k$ in [Hz] or by the values of $\omega_k = 2\pi f_k$ in [rad/sec]. For each of these frequencies $f_k$ we plot a bar, denoting the complex weights $\frac{X_k}{2}$ as described previously. Note that these complex weights are related to the amplitude and phase of the original sinusoidal signal.

<div class="example">
<h4> Example </h4>
<hr>

Find the complex weights of the phasor components of the signal
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right)$$
and make a spectral plot of the signal.

<button class="collapsible">Show solution</button>
<div class="content">

By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> the expression for $x(t)$ can be rewritten as

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

In a spectral plot, such as the one from the previous example, the phasor components of the signal are represented by bars and the corresponding weights are denoted by complex numbers above these bars. The amplitude or magnitude of the complex weights corresponds to the length of the bar. When denoting these complex weights in <a href="../../mathematicalbackground/mathematicalbackground_complex_notation">Polar notation</a> it becomes very easy to 'read from the spectral plot' and to convert the spectral plot back to the time-domain representation of the real signal $x(t)$.

From the spectral plot of the above example it can be noted that the spectrum is symmetric, indicating that we are dealing with a real signal. The spectrum consists of a DC term and two sinusoids. The DC term has a value of 10 and is by definition located at a frequency of $0$ [Hz]. The first sinusoid is located at $100$ [Hz] and has an amplitude of $2\times7 = 14$ and has a phase of $-\frac{\pi}{3}$, which is obtained from the right-hand side of the spectrum. The second sinusoid has an amplitude of $2\times4=8$ and has a phase of $\frac{\pi}{2}$. Keep in mind to read the phase of the sinusoid from the right-hand side of the spectrum, since the left-hand side contains the negated phase.
All together the spectral plot of the above example belongs to the following time-domain representation of signal $x(t)$:
$$ x(t) = 10 + 14 \cos\left(200\pi t -\frac{\pi}{3}\right) + 8\cos\left(500\pi t + \frac{\pi}{2}\right).$$

From the above interpretation of the spectral plot we can conclude

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>It is easiest to denote the complex weights corresponding to the individual phasor components in the spectral plot in Polar notation.</i></div>

### Product versus sum of frequencies
In the previous section we have seen that a spectral plot represents the spectral content of a signal. When a signal consists of a sum of sinusoids we have seen which spectral components belongs to which sinusoid. But what is the frequency content of a signal which consists of a multiplication of sinusoids? In practice this multiplication is commonly used when we apply ”Amplitude Modulation” (AM) to transmit a baseband signal, with relative low frequency content, over a long distance. In such a case the baseband signal is multiplied with a carrier signal which has a relative high carrier frequency $f_c$ [Hz].
So lets start our discussion by assuming that a signal $x(t)$ consists of the multiplication of two sinusoids, one with carrier frequency $f_c$ and the other with (baseband or message) frequency $f\_{\Delta}$ (typically with $f_c >> f\_{\Delta}$, i.e. the carrier frequency is way larger than the baseband frequency), as
$$ x(t) = 2\cos(2\pi f_c t) \cdot \cos(2\pi f\_\Delta t). $$

By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can rewrite this equation as

$$
\begin{split}
x(t)
&= 2\left(\frac{1}{2}e^{j2\pi f_c t}+ \frac{1}{2}e^{-j2\pi f_c t}\right) \cdot \left(\frac{1}{2}e^{j2\pi f\_\Delta t}+ \frac{1}{2}e^{-j2\pi f\_\Delta t}\right), \newline
&= \frac{1}{2} e^{j2\pi(f_c+f\_\Delta)t} + \frac{1}{2} e^{j2\pi(f_c-f\_\Delta)t} +\frac{1}{2} e^{-j2\pi(f_c-f\_\Delta)t} + \frac{1}{2} e^{-j2\pi(f_c+f\_\Delta)t}, \newline
&= \left(\frac{e^{j2\pi(f_c+f\_\Delta)t} + e^{-j2\pi(f_c+f\_\Delta)t}}{2}\right) + \left(\frac{e^{j2\pi(f_c-f\_\Delta)t} + e^{-j2\pi(f_c-f\_\Delta)t}}{2}\right), \newline
&= \cos(2\pi(f_c+f\_\Delta)t) + \cos(2\pi(f_c-f\_\Delta)t).
\end{split}
$$

From this expression we can conclude that

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The product of two sinusoidal signals with frequencies $f_c$ and $f_\Delta$ can be written as the sum of two sinusoidal signals with frequencies $f_c + f_\Delta$ and $f_c - f_\Delta$.</i></div>

Fig. 1 shows an example of what this multiplication now actually looks like in the time-domain. From the definition of $x(t)$ it can be understood as a sinusoid at a high carrier frequency, whose amplitude is slowly changing according to a baseband signal. In this case there is chosen for a carrier frequency $f_c$ of $200$ [Hz] and a baseband frequency $f\_\Delta$ of $20$ [Hz]. Fig. 2 shows what the new spectral plot of $x(t)$ looks like.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/modulation_time.svg"
      alt="Time-domain representation of modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Time-domain representation of modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/modulation_spectrum.svg"
      alt="Spectrum of modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>

One of the examples where we use this concept is when tuning a guitar or piano. With the previous example in mind: Assume a guitar string produces a, wrongly tuned, 180 [Hz] signal and we want it to be tuned at 220 [Hz]. Then by playing an external signal generator, which produces a 220 [Hz] pure tone, while playing the, wrongly tuned, 180 [Hz] guitar string, we will not hear a clear sound. The waveform of the sound (as a product) is shown in Fig. 1: The amplitude of the sound is not constant but it changes. This effect is called ”beat note”. Now we can tune the string by tightening it until the amplitude does not change anymore and we will hear one pure tone of 220 [Hz]. At that point our guitar string is tuned to 220 [Hz]. Another application of the previous concept is when transmitting a baseband signal, with relative low frequency content, over a long distance. An example of such a baseband signal is audio, e.g. speech or music, which has frequencies up to 20 [kHz]. It is impossible to transmit such an audio signal over a long distance in the air, because of attenuation. In such a case we can apply ”Amplitude modulation”: The baseband signal is multiplied with a carrier signal which has a relative high frequency $f_c$ [Hz] and the audio is then transmitted in the band around the less attenuating carrier frequency.

<div class="example">
<h4> Example </h4>
<hr>

Assume the baseband (message) signal $m(t)=4+2\cos(2\pi 6t-\frac{\pi}{4})$ is multiplied (modulated) with the carrier signal $c(t) = \cos(2\pi 1000t)$ to produce the Amplitude Modulated (AM) signal $x(t)=c(t)\cdot m(t)$. Determine the spectral plots of all three signals.

<button class="collapsible">Show solution</button>
<div class="content">

In order to create a spectral plot we first need to find the frequency components of all three signals. To do so, the signals are converted into <a href="../continuoussignalprocessing_transforms_fs/#real-signal-as-sum-of-phasors">phasor</a> notation. The message signal $m(t)$ can be written as
$$
\begin{split}
m(t)
&=4+2\cos(2\pi 6t-\frac{\pi}{4}),\newline
&= \left(4\right)e^{j2\pi 0 t} + \left(1e^{-j\frac{\pi}{4}}\right)e^{j2\pi 6 t} + \left(1e^{j\frac{\pi}{4}}\right)e^{-j2\pi 6 t}.
\end{split}$$

The carrier signal $c(t)$ can be written as
$$
\begin{split}
c(t)
&= \cos(2\pi 1000t), \newline
&= \left(\frac{1}{2}\right)e^{j2\pi 1000 t} + \left(\frac{1}{2}\right)e^{-j2\pi 1000 t}.
\end{split}
$$

Both these signals can already be represented in their spectral plots. In order to also be able to represent $x(t)$ in a spectral plot the signal also needs to be rewritten in <a href="../continuoussignalprocessing_transforms_fs/#real-signal-as-sum-of-phasors">phasor</a> notation as
$$
\begin{split}
x(t)
&= c(t)\cdot m(t), \newline
&= \bigg\{ \frac{1}{2}e^{j2\pi 1000 t} + \frac{1}{2}e^{-j2\pi 1000 t} \bigg\} \cdot \bigg\{ 4e^{j2\pi 0 t} + e^{-j\frac{\pi}{4}}e^{j2\pi 6 t} + e^{j\frac{\pi}{4}}e^{-j2\pi 6 t} \bigg\}, \newline
&= 2e^{j2\pi 1000 t} + \frac{1}{2}e^{-j\frac{\pi}{4}}e^{j2\pi (1000+6) t} + \frac{1}{2} e^{j\frac{\pi}{4}}e^{j2\pi (1000-6) t} \newline
&\qquad + 2e^{-j2\pi 1000 t} + \frac{1}{2}e^{-j\frac{\pi}{4}}e^{-j2\pi (1000-6) t} + \frac{1}{2} e^{j\frac{\pi}{4}}e^{-j2\pi (1000+6) t}.
\end{split}
$$

The spectral plots are shown in Fig. 3. From the spectral plots it follows that the whole spectral content of the message signal $m(t)$ has been 'shifted' (modulated) to the positive and negative carrier frequency components of the carrier signal $c(t)$.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/example2_spectrum.svg"
      alt="Spectrum of message signal $m(t)$, carrier signal $c(t)$ and modulated signal $x(t)$."
    />
    <figcaption class="numbered">
      Spectrum of message signal $m(t)$, carrier signal $c(t)$ and modulated signal $x(t)$.
    </figcaption>
  </figure>
</div>

</div>
</div>

From the previous example we may conclude that

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When a message signal $m(t)$ is modulated by a carrier signal $c(t)$ with frequency $f_c$, the whole spectral content of the message is moved to both the positive and negative frequency component of the carrier signal.</i></div>



## Fourier series
In the previous section we studied the spectral behavior of the sum of sinusoidal signals. In this section we will study signals which are composed of a sum of harmonic related sine waves.

### Periodic signals
In this subsection we will show that any periodic signal with a, so called, Fundamental period $T_0$ can be composed as the sum of sinusoidal signals from which each of these frequencies is related to the, so called, Fundamental frequency $F_0 = 1/T_0$ as an integer multiple. In order to show this Fig. 4 depicts a signal $y_2(t)$ which is composed of the sum of two sinusoidal signals $x_1(t)$ of frequency $f_1 = 6$ [Hz] and $x_2(t)$ of frequency $f_2 = 2$ [Hz]. From this figure it follows that $y_2(t)$ is periodic and we can measure that the period equals $T_0 = 1/F_0 = 0.5$ [sec]. The reason for this periodicity of signal $y_2(t)$ is that exactly three periods of $x_1(t)$ and one period of $x_2(t)$ fit into one period $T_0$ of signal $y_2(t)$. Thus after each $T_0 = 0.5$ [sec] the same composition of the signals $x_1(t)$ and $x_2(t)$ appears in the signal $y_2(t)$.

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

The figure also shows another signal $y_3(t)$ which is composed of the sum three sinusoidal signals. The same sinusoidal signals $x_1(t)$, $x_2(t)$ and a new sinusoidal signal $x_3(t)$, with frequency $f_3 = 1.2$ [Hz]. Again it follows from the figure that $y_3(t)$ is periodic but now we can measure that the period equals $T_0 = 1/F_0 = 2.5$ [sec]. This is because of the fact that exactly fifteen periods of $x_1(t)$, five periods of $x_2(t)$ and three periods of $x_3(t)$ fit into one period $T_0$ of signal $y_3(t)$. Mathematically we can calculate $F_0 = 1/T_0$ of $y_3(t)$ as the Greatest Common Divisor (gcd) of the frequencies from the individual sinusoidal components, since $F_0 = \text{gcd}\\{f_1, f_2, f_3\\} = \text{gcd}{6, 2, 1.2} = 0.4$ [Hz]. The greatest common divisor of a set of numbers is the largest number that all numbers of that set can be _fully_ divided by. From this it follows that the Fundamental period of $y_3(t)$ equals $T_0 = 1/F_0 = 2.5$ [sec]. This leads to the following general statement:

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

By using <a href="../../mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can write $x(t)$ as
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
The spectral plot of $x(t)$ is given in Fig. 5. The x-axis contains both the frequency as the integer values of $k$, which are the frequency divided by the Fundamental frequency.

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


### Fourier series synthesis
In the previous subsection we have seen that every periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, can be written as a sum of weighted harmonic related phasor components. In theory the summation can contain an infinite amount of components which leads to the following Fourier series expansion:

$$\bbox[5px,border:1px solid black]{
x(t) = \sum_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}.}
$$

Thus when the spectral weights, which are represented by the complex numbers $\alpha_k$, are known we can construct (synthesize) the periodic signal $x(t)$ according the above general expression.

### Fourier series analysis
In this subsection we will show the other way around: when we are given the waveform in the time-domain of a periodic signal $x(t)$, how can we derive the spectral weights $\alpha_k$? In order to do so we need the following basic property of a phasor function:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The integral over one period $T_0=1/F_0$ of a phasor with a harmonic related frequency $k \cdot F_0$ results always in zero except for the case $k=0$.</i></div>

Mathematically this can be shown as follows:
$$
\int_0^{T_0} e^{j2\pi k F_0 t} \mathrm{d}t = \left[\frac{e^{j2\pi kF_0 t}}{j2\pi F_0 k}\right]\_{t=0}^{T_0} = \frac{e^{j2\pi k}-1}{j2\pi F_0 k} = \frac{1-1}{j2\pi F_0 k} = 0.
$$
Furthermore the integral can be evaluated for $k=0$ as
$$
\int_0^{T_0} e^{j2\pi 0 F_0 t}\mathrm{d}t = \int_0^{T_0}1\mathrm{d}t = \left[t\right]\_0^{T_0} = T_0-0 = T_0.
$$
What do the above two equation now actually mean? If we integrate a sinusoidal signal over a number of periods, we are actually summing the areas under the sinusoid. Since the sinusoid has an equal area under as above the horizontal axis per period, the area will sum to zero. However, if $k=0$, which means that we are talking about a DC signal, the signal does not oscillate around the horizontal axis and therefore the integral will not become zero.

When we normalize and combine the previous two equations we obtain the basic property of phasors

$$\bbox[5px,border:1px solid black]{
\frac{1}{T_0}\int_0^{T_0}e^{j2\pi kF_0 t}\mathrm{d}t =
\begin{cases}
1,      &\text{for }k=0\newline
0.      &\text{for }k\neq 0
\end{cases}}
$$

Since we are sure that a periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, only consists of harmonic related frequencies we can use the above phasor property as follows to analyze which harmonic related frequencies are present in $x(t)$ and what are the complex values of the spectral weights. For this we evaluate the normalized integral over one period $T_0$ of $x(t)$ multiplied by a phasor with harmonic related frequency $l \cdot F_0$. Thus with both $k$ and $l$ integer we obtain

$$
\begin{split}
\frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi lF_0 t}\mathrm{d}t
&= \frac{1}{T_0}\int_0^{T_0}\left(\sum\_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}\right)e^{-j2\pi lF_0 t}\mathrm{d}t, \newline
&= \sum\_{k=-\infty}^{\infty} \alpha_k \left(\frac{1}{T_0} \int_0^{T_0} e^{j2\pi(k-l)F_0 t}\mathrm{d}t \right),
&= \alpha_l.
\end{split}
$$

In the last step we have used the phasor property to observe that the integral only becomes non-zero when $k=l$.

Thus when we are given a periodic signal $x(t)$ with period $T_0 = 1/F_0$ then we can find the spectral components $a_k$ by using the following Fourier series analysis equation
$$\bbox[5px,border:1px solid black]{
\alpha_k = \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j2\pi kF_0t}\mathrm{d}t}.
$$

In practical application it is impossible to evaluate $\alpha_k$ for $-\infty<k<\infty$. Therefore we can approximate a period signal $x(t)$ with only a limited amount of terms as

$$
\hat{x}(t) = \sum_{k=-N}^{N} \alpha_k e^{j2\pi kF_0 t}.
$$
It is obvious that the approximation becomes better and better for larger $N$.

<div class="example">
<h4> Example </h4>
Given the following periodic signal $x(t)$, evaluate the spectral weights $\alpha_k$. Furthermore, show the approximated periodic signal $x(t)$ when using only up to the first 5 terms.


  <figure style="max-width: 600px; margin: auto">
    <img
      src="/../files/7.Images/continuous/transforms/block_ideal.svg"
      alt="Ideal periodic block wave."
    />
    <figcaption>
      Ideal periodic block wave $x(t)$.
    </figcaption>
  </figure>


<button class="collapsible">Show solution</button>
<div class="content">

From the figure it follows that $x(t)$ is a periodic signal with period $T_0=1/F_0=4$ [sec]. In most cases it is convenient to evaluate first the DC component $\alpha_0$ of the periodic signal (which can be regarded as just the average value of the signal). The DC component can be calculated simply by averaging as
$$
\alpha_0 = \frac{1}{T_0}\int_0^{T_0} x(t)\mathrm{d}t = \frac{1}{4} \bigg\{ \int_0^2 2\mathrm{d}t + \int_2^4 0\mathrm{d}t\bigg\} = \frac{1}{4}\{ 4+0\} = 1.
$$

Furthermore with $\omega_0=2\pi F_0 = \frac{2\pi}{4} = \frac{\pi}{2}$, we obtain for $\alpha_k$

$$
\begin{split}
\alpha_k
&= \frac{1}{T_0}\int_0^{T_0}x(t)e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4}\int_0^{2}2e^{-j\omega_0 kt}\mathrm{d}t
= \frac{1}{4} \left[ \frac{2e^{-j\omega_0 kt}}{-j\omega_0 k}\right]\_0^2, \newline
&= \frac{j}{2\omega_0 k}\left(e^{-j2\omega_0 k}-1\right)
= \frac{j}{k\pi}(e^{-j\pi k}-1) = \frac{\left(e^{-j\pi}\right)^k -1}{k\pi}j
= \frac{(-1)^k -1}{k\pi}e^{j\frac{\pi}{2}}, \newline
&= \frac{1-(-1)^k}{k\pi}e^{-j\frac{\pi}{2}}.
\end{split}
$$

Thus except for $k=0$ all Fourier coefficients with even index $k$ are equal to zero. The Fourier coefficients with odd indices are:
$$
\alpha_1 = \alpha_{-1}^\ast = \frac{2}{\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_3 = \alpha_{-3}^\ast = \frac{2}{3\pi}e^{-j\frac{\pi}{2}},
\quad \alpha_5 = \alpha_{-5}^\ast = \frac{2}{5\pi}e^{-j\frac{\pi}{2}},
\quad \text{etc.}
$$

When approximating this periodic signal with the first $N$ terms we obtain

$$
\begin{split}
\hat{x}(t)
&= \alpha_0 + \sum_{k=1}^N \left(\alpha_k e^{jk\frac{\pi}{2} t} +\alpha_{-k} e^{-jk\frac{\pi}{2} t} \right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \cos\left(k\frac{\pi}{2}t - \frac{\pi}{2}\right), \newline
&= 1 + \frac{4}{k\pi}\sum_{k=1,3,5,\ldots}^N \sin\left(k\frac{\pi}{2}t\right).
\end{split}
$$

The figure below gives the approximation of the block wave for an increased number of Fourier coefficients, where $k$ is limited between $-N$ and $N$.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/block_approximate.gif"
      alt="Approximation of an ideal block wave."
    />
    <figcaption>
      Approximation of an ideal block wave, where the $k$ is limited between $-N$ and $N$. The value of $N$ is altered during the animation.
    </figcaption>
  </figure>
</div>

</div>
</div>

### Fourier series examples
The above example should give you some intuition on how the Fourier series works. For a better clarification of the subject matter the following screencast video will give some more examples

<div>
<video controls preload>
  <source src="/../files/8.Screencast/Fourier/Continuous/FS/2FourierSeriesExamples.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>

## Exercises
In this section several exercises are available, including their answers. The exercises marked in <span style="color:blue">*blue*</span> are explained by means of more extensive pencast videos.

### Exercise bundle
<object data="/../files/3.Exercises/2.SPAFS-StudentExercises.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/3.Exercises/2.SPAFS-StudentExercises.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/3.Exercises/2.SPAFS-StudentExercises.pdf">Download PDF</a>.</p>
    </embed>
</object>


### Answers
Download the answers <a href="/../files/3.Exercises/Answers/2.SPAFS-StudentAnswers.pdf">here</a>.

### Pencast videos
<script src='https://vjs.zencdn.net/7.4.1/video.js'></script>
<div class="grid-row reverse video-gallery">
 <input type="radio" value="1" name="video-list" id="video-1" checked="checked" /><label for="video-1">Exercise 4</label>
 <input type="radio" value="2" name="video-list" id="video-2" /><label for="video-2">Exercise 6</label>
 <input type="radio" value="3" name="video-list" id="video-3" /><label for="video-3">Exercise 12</label>


 <!-- videos -->
 <div class="video video-1">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SPAFS-4.mp4" type="video/mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-2">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SPAFS-6.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

 <div class="video video-3">
 <video width="500" height="240" controls>
   <source src="/../files/6.Pencast/SPAFS-12.mp4" type="video/mp4">
 Your browser does not support the video tag.
 </video>
 </div>

</div>

## MATLAB lab
Accompanied to this modules are some exercises in MATLAB, which will test your knowledge of the module and will help improve your MATLAB skills.

### Lab assignment
<object data="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf" width="100%" height="400px">
    <embed src="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf" type="application/pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="/../files/10.Matlab/Lab 3 - Fourier Transform.pdf">Download PDF</a>.</p>
    </embed>
</object>

### MATLAB demo
<div>
<video controls preload>
  <source src="/../files/10.Matlab/screencasts/SPAFS - MATLAB.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>

## Summary
<ul>
<li> Sum of DC and $N$ sinusoids written as sum of phasors:
$$
\begin{split}
x(t) &= A_0 + \sum_{k=1}^{N} A_k\cos \left( 2\pi  f_k t+ \phi_k \right),\newline
&= X_0 + \sum_{k=1}^N \bigg\{ \frac{X_k}{2}e^{j2\pi f_k t} + \frac{X_k^\ast}{2}e^{-j2\pi f_k t} \bigg\},
\end{split}
$$

where $X_0 = A_0$ and $X_k = A_ke^{j\phi_k}$.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>For real signals the values of the complex weights of the phasors with negative frequencies are the complex conjugated versions of the complex weights of the phasors with positive frequencies.</i></div>
</li>

<li>
By ordering the frequencies from low to high we can represent the phasor description in a frequency spectrum plot. In such a plot we denote the frequencies on the horizontal axis. The frequency on this axis can either be denoted by the values of $f_k$ in [Hz] or by the values of $\omega_k = 2\pi f_k$ in [rad/sec]. For each of these frequencies $f_k$ we plot a bar, denoting the complex weights $\frac{X_k}{2}$. These complex weights are related to the magnitude and phase of the original sinusoidal signal.

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>It is easiest to denote the complex numbers of the bars in the spectral plot in Polar notation.</i></div>
</li>

<li>
A product of sinusoids is related to a sum of sinusoids:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>We can write the <b>product</b> of two sinusoidal signals with frequencies $f_c$ and $f_\Delta$ as the <b>sum</b> of two sinusoidal signals with frequencies $f_c-f_\Delta$ and $f_c+f_\Delta$</i></div>
</li>

<li>
An Amplitude Modulated (AM) signal has the following property:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When a message signal $m(t)$ is modulated by a carrier signal $c(t)$ with frequency $f_c$, the whole spectral content of the message is moved to both the positive and negative frequency component of the carrier signal.</i></div>
</li>

<li>
A periodic signal has the following property:
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A real signal $x(t)$, which consists of a DC component and a sum of $N$ different frequencies $f_1, f_2,\ldots, f_N$, with $f_1 &lt f_2 &lt \ldots &lt f_N$, is a periodic signal with Fundamental period $T_0 = 1/F_0$ and has a Fundamental frequency $F_0 = \text{gcd}\{f_1,f_2,\ldots,f_N\} $.</i></div>
</li>

<li>
The integral over one period $T_0 = 1/F_0$ of a phasor with a harmonic related frequency $k \cdot F_0$ results always in zero except for the case $k = 0$.
Mathematically this can be written as follows:

$$\bbox[5px,border:1px solid black]{
\frac{1}{T_0}\int_0^{T_0}e^{j2\pi kF_0 t}\mathrm{d}t =
\begin{cases}
1      &\text{for }k=0\newline
0      &\text{for }k\neq 0
\end{cases}}
$$
</li>

<li>
Fourier analysis and synthesis equations for periodic signal $x(t)=x(t+T_0)$ with $T_0=1/F_0$:
$$\bbox[5px,border:1px solid black]{
\alpha_k = \frac{1}{T_0}\int_0^{T_0} x(t)e^{-j2\pi F_0 kt}\mathrm{d}t
\ \circ  \hspace{-1.7mm} - \hspace{-1.7mm} \circ \
x(t) = \sum_{k=-\infty}^\infty \alpha_k e^{j2\pi F_0 kt }\
}
$$
</li>

</ul>
