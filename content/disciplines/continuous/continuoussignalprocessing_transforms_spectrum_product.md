+++
title = "Product versus sum of sinusoids"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Product versus sum of sinusoids"
  weight = 3
  parent = "Transforms I: Spectrum of sinusoidal signals"
+++

In the previous section we have seen that a spectral plot represents the spectral content of a signal. When a signal consists of a sum of sinusoids we have seen which spectral components belongs to which sinusoid. But what is the frequency content of a signal which consists of a multiplication of sinusoids? In practice this multiplication is commonly used when we apply ”Amplitude Modulation” (AM) to transmit a baseband signal, with relative low frequency content, over a long distance. In such a case the baseband signal is multiplied with a carrier signal which has a relative high carrier frequency $f_c$ [Hz].
So lets start our discussion by assuming that a signal $x(t)$ consists of the multiplication of two sinusoids, one with carrier frequency $f_c$ and the other with (baseband or message) frequency $f\_{\Delta}$ (typically with $f_c >> f\_{\Delta}$, i.e. the carrier frequency is way larger than the baseband frequency), as
$$ x(t) = 2\cos(2\pi f_c t) \cdot \cos(2\pi f\_\Delta t). $$

By using <a href="../../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler</a> we can rewrite this equation as

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
In order to create a spectral plot we first need to find the frequency components of all three signals. To do so, the signals are converted into <a href="./#real-signal-as-sum-of-phasors">phasor</a> notation. The message signal $m(t)$ can be written as
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
Both these signals can already be represented in their spectral plots. In order to also be able to represent $x(t)$ in a spectral plot the signal also needs to be rewritten in <a href="./#real-signal-as-sum-of-phasors">phasor</a> notation as
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
