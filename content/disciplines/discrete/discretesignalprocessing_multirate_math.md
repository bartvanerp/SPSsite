+++
title = "Mathematical description sampling process"

# date = {{ .Date }}
lastmod = 2019-12-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Mathematical description sampling process [⯈]"
  weight = 81
  parent = "Sampling, reconstruction and multirate signal processing"


+++

## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/e-3TyTN_Tcg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br>

## Analog to digital conversion
Sounds that reach our ears are signals in the form of air pressure. This air pressure is a continuous signal, i.e. it is defined for all time instances and can have any value on a reasonable domain. These kind of signals cannot be stored directly on a computer, which uses numbers to perform calculations. The signal first needs to be approximated in two ways in order to allow for computations on a computer and to limit the required memory.

First, it is not possible to save the signal values of every time instance. The continuous time domain has an infinite amount of distinct time instances. In order to limit the number of values that we save in the memory, we only save the values of every $T_s$ seconds. This process is called sampling and is also know as continuous-time to discrete-time conversion, or C/D conversion.

Secondly, the values that we measure can have an infinite amount of distinct values. In order to bring down the infinite number of bits required to save these values, the measured values are rounded to a predefined set of values. This process is called quantization. After this quantization step, the values are encoded into bits.

The process of converting an analog to a digital signal is called analog-to-digital conversion or A/D conversion. An overview of this system is shown in Fig. 1. This conversion encompasses both the sampling as quantization of the analog signal. In this section we will be focusing on the sampling process.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/ADconv.svg"
      alt="An overview of analog-to-digital conversion with an encoding step. First the continuous-time signal is sampled in time in the C/D converter, then the signal is quantized to a predefined set of values and finally these values are encoded into bits."
    />
    <figcaption class="numbered">
      An overview of analog-to-digital conversion with an encoding step. First the continuous-time signal is sampled in time in the C/D converter, then the signal is quantized to a predefined set of values and finally these values are encoded into bits.
    </figcaption>
  </figure>
</div>

## C/D conversion
In the C/D conversion, the analog signal $x_a(t)$ is converted to a discrete-time signal with continuous values. Here the round brackets $(\cdot)$ indicate the continuous-time domain. The process of C/D conversion is presented in Fig. 2. This analog signal $x_a(t)$ is multiplied with a period pulse train $s_a(t)$ defined as
\begin{equation}
    s_a(t) = \sum_{n=-\infty}^\infty \delta(t - n \cdot T_s),
\end{equation}
which consists of a train of ideal delta pulses, uniformly spaced at a distance of $T_s$ seconds. Here $T_s$ represents the sampling period, with is the reciprocal of the sampling frequency $f_s$ as $T_s = 1/f_s$.
The resultant signal $x_s(t) = x_a(t) \cdot s_a(t)$ is a pulse train where the area under the delta pulse at time $t = n\cdot T_s$ represents the instantaneous value of $x_a(t)$. These values are then used to convert the signal to discrete-time signal samples $x[n]$, where the index $n$ is an integer and refers to the sample index. Please note that we now use square brackets $[\cdot]$ to denote the discrete-time domain.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/CDconv.svg"
      alt="The process of continuous-time to discrete-time conversion. First, the analog signal $x_a(t)$ is multiplied with a delta pulse train $s_a(t)$, yielding the continuous signal $x_s(t)$. These pulses are subsequently converted into samples by discretizing the time-domain."
    />
    <figcaption class="numbered">
      The process of continuous-time to discrete-time conversion. First, the analog signal $x_a(t)$ is multiplied with a delta pulse train $s_a(t)$, yielding the continuous signal $x_s(t)$. These pulses are subsequently converted into samples by discretizing the time-domain.
    </figcaption>
  </figure>
</div>

### Pulse train multiplication
Now we will investigate the consequences of sampling the analog signal for its frequency content, starting by the multiplication of the analog signal with the pulse train. We will do this by calculating the Fourier transform for continuous-time signals (FTC) for the resulting signal $x_s(t) = x_a(t)\cdot s_a(t)$.

Let us assume that the ideal frequency spectrum of $x_a(t)$ can be represented as $X_a(\omega)$, where $\omega$ denotes the angular frequency $\omega=2\pi f$. This gives us the Fourier pair
\begin{equation}
    x_a(t) \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad X_a(\omega)
\end{equation}
Similarly, the frequency spectrum $S_a(\omega)$ of the pulse train $s_a(t)$ is a basic Fourier pair, known to be
\begin{equation}\label{eq:Xs}
    s_a(t) = \sum_{n=-\infty}^\infty \delta(t - n \cdot T_s) \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad S_a(\omega) = \frac{2\pi}{T_s} \sum_{k=-\infty}^{\infty} \delta\left(\omega-k\cdot \frac{2\pi}{T_s}\right)
\end{equation}
Using the multiplication-convolution property of the FTC defined as
\begin{equation}
    x_s(t) = x_a(t) \cdot s_a(t) \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad X_s(\omega) = \frac{1}{2\pi} X_a(\omega) \ast S_a(\omega)
\end{equation}
we can obtain the frequency spectrum $X_s(\omega)$ of $x_s(t)$ as
\begin{equation}
    \begin{split}
        X_s(\omega)
        &= \frac{1}{T_s} \sum_{k=-\infty}^\infty X_a(\omega) \ast \delta\left( \omega - k\cdot \frac{2\pi}{T_s} \right), \newline
        &= \frac{1}{T_s} \sum_{k=-\infty}^\infty X_a\left(\omega - k\cdot \frac{2\pi}{T_s} \right).
    \end{split}\label{eq:Xsomega}
\end{equation}

From this description two consequences can be observed. First, the frequency spectrum gets scaled by a factor $1/T_s=f_s$. Secondly, the spectrum $X_s(\omega)$ resembles the spectrum $X_a(\omega)$, which repeats itself every $\frac{2\pi}{T_s}$ radians per second.

### Conversion to samples
Another way of determining the frequency spectrum $X_s(\omega)$ can be found by treating the signal $x_a(n\cdot T_s)$ as values and by using the shift property of the FTC for the delta pulses. From this we can obtain the Fourier pair
\begin{equation}\label{eq:fourier2}
    x_s(t) = \sum_{n=-\infty}^\infty x_a(n\cdot T_s)\delta(t-n\cdot T_s) \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad X_s(\omega) = \sum_{n=-\infty}^\infty x_a(n\cdot T_s)e^{-jn\omega T_s}
\end{equation}
This expression is similar to the expression of the Fourier transform for discrete-time signals (FTD), which is defined as
\begin{equation}\label{eq:FTD}
    X(e^{j\theta}) = \sum_{n=-\infty}^\infty x[n] e^{-jn\theta}
\end{equation}
By defining the discrete-time signal $x[n]$ as
\begin{equation}
    x[n] = x(t)|_{t=n \cdot T_s},
\end{equation}
we can observe equality of $X_s(\omega)$ in \eqref{eq:fourier2} and $X(e^{j\theta})$ in \eqref{eq:FTD} when
\begin{equation}
    \theta = \omega T_s = 2\pi \frac{f}{fs}
\end{equation}
holds. Here $\theta$ is known as the relative frequency.

From this equality and the expression in \eqref{eq:Xs} we can obtain the FTD of the sampled signal $x_s[n]$ as
\begin{equation}
    X_s(e^{j\theta}) = X_s(\omega)\mid_{\omega=\frac{\theta}{T_s}} = \frac{1}{T_s} \sum_{k=-\infty}^\infty X_a \left( \frac{\theta}{T_s} - k \frac{2\pi}{T_s} \right).
\end{equation}
As expected from our previously results, after sampling we obtain a spectrum that repeats every $\frac{2\pi}{T_s}$ radians per second. From the perspective of the relative frequency, we observe a periodic behaviour of the relative frequency every $2\pi$ and from the normal frequency, we observe a periodic behaviour of the frequency every $1/T_s=f_s$ Hz.

### Sampling theorem
Let us now consider the consequences of the spectral repetition in the frequency domain for a band-limited signal. With a band-limited signal we refer to a signal whose frequency content is restricted to a finite segment of the frequency domain. For simplicity we will assume that the spectrum of signal $x_a(t)$ is band-limited to the domain $f \in [-f_\text{max}, f_\text{max}]$.
If $f_\text{max}$ does not exceed the boundary frequency
$k\cdot f_s + f_s/2$, represented by the average center frequencies of two consecutive repetitions, the repetitions will be visible next to each other in the frequency domain. This is depicted on the left of Fig. 3. However, if this maximum frequency is larger than these boundaries, the repetitions will overlap each other in the frequency domain. This is called aliasing and is shown on the right of Fig. 3. Aliasing will lead to distortion at the frequency regions where the original frequency spectra overlap. Consequently, when sampling a signal, it is in general not possible to reconstruct the original signal from its samples when aliasing occurs, as we cannot undo the effect of this overlap.

In order to prevent aliasing and to make sure that we can reconstruct our original signal from our samples, we need to fulfill the following sampling theorem.
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px">
  A continuous-time signal $x_a(t)$ with frequencies not higher than $f_\text{max}$ can be reconstructed exactly from its samples $x[n] = x_a(t)|_{n \cdot T_s}$, if samples are taken at a rate $f_s=1/T_s$, that is larger than $2f_\text{max}$.
</div>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/aliasspectraFTCFTD.svg"
      alt="An illustrative example showing the concept of aliasing."
    />
    <figcaption class="numbered">
      An illustrative example showing the concept of aliasing.
    </figcaption>
  </figure>
</div>

In practice there are situations when it is not possible to satisfy this theorem, for example when you are measuring a high-frequency signal or when the computational power of the system is restricted. In these cases the distortion caused by aliasing can be prevent by cropping the frequency spectrum to the allowed domain. By doing so, we lose signal content and information, but we prevent distortion from taking place. This cropping can be performed by low-pass filtering the signal before sampling the signal. This process is depicted in Fig. 4.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/ADconvLPF.svg"
      alt="An overview of the system where the sampler is preceded by a low-pass filter to prevent aliasing from distorting the signal."
    />
    <figcaption class="numbered">
      An overview of the system where the sampler is preceded by a low-pass filter to prevent aliasing from distorting the signal.
    </figcaption>
  </figure>
</div>

<br>

## Digital to analog conversion
Now that we have considered the process of sampling the signal it is time to reconstruct the analog signal from its sampled values.

### Process overview
Consider the signal $x_s(t)$, which was a pulse train containing sampled values of the original analog signal $x_a(t)$ as shown on the left in equation \eqref{eq:fourier2}. This signal can be reconstructed relatively easily from the discrete-time signal samples $x[n]$. If we consider the spectrum $X_s(\omega)$ of $x_s(t)$ in \eqref{eq:Xsomega}, we can observe that the spectrum contains repetitions of the original spectrum. For the reconstruction of the original band-limited signal $x_a(t)$, we are only interested in the repetition for $k=0$, i.e. the repetition around 0 Hz. Through low-pass filtering the signal $x_s(t)$, all repetitions of the spectrum can be filtered out and only the original spectrum remains. By low-pass filtering we can reconstruct our signal. This process is shown in Fig. 5.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/DAconv.svg"
      alt="Process of digital to analog conversion, where a low-pass filter is used to reconstruct the original signal from the delta pulse train."
    />
    <figcaption class="numbered">
      Process of digital to analog conversion, where a low-pass filter is used to reconstruct the original signal from the delta pulse train.
    </figcaption>
  </figure>
</div>

### Time-domain interpolation
The process of converting the samples into a delta pulse train and of low-pass filtering the signal can also be represented mathematically. The process of converting the samples into delta pulses can be represented as
\begin{equation}
    x_s(t) = \sum_{n=-\infty}^\infty x[n]\delta(t - n\cdot T_s).
\end{equation}
The low-pass filter is assumed to be ideal with a cut-off radial frequency at $\pi/T_s$. This gives the frequency response of the low-pass filter $H_r(\omega)$ and the impulse response of the filter $h_r(t)$ as the Fourier pair
\begin{equation}
    H_r(\omega) =
    \begin{cases}
        T_s & |\omega| \leq \frac{\pi}{T_s} \newline
        0 & |\omega| > \frac{\pi}{T_s}
    \end{cases}
    \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad
    h_r(t) = \frac{\sin\left(\frac{\pi}{T_s}\cdot t\right)}{\frac{\pi}{T_s}\cdot t}
\end{equation}
In the frequency domain, the original spectrum is reconstructed through the multiplication of the repeating spectrum and the frequency response of the low-pass filter. In the time-domain this corresponds to the convolution of the signal with the impulse response of the low-pass filter as
\begin{equation}
    \begin{split}
        x_a(t)
        &= x_s(t) \ast h_r(t) \newline
        &= \left(\sum_{n=-\infty}^\infty x[n] \delta(t-nT_s)\right) \ast h_r(t) \newline
        &= \sum_{n=-\infty}^\infty x[n] (\delta(t-nT_s) \ast h_r(t)) \newline
        &= \sum_{n=-\infty}^\infty x[n] \cdot h_r(t-nT_s),
    \end{split}\label{eq:reconstruction}
\end{equation}
where the time-domain interpolation equation is determined as
\begin{equation}
\boxed{
    x_a(t) = \sum_{n=-\infty}^\infty x[n] \left(\frac{\sin\left(\frac{\pi}{T_s}\cdot (t-nT_s)\right)}{\frac{\pi}{T_s}\cdot (t-nT_s)}\right)
}
\end{equation}
This process is also known as sinc-interpolation as we are replacing all samples with scaled sinc-functions and summing over them. Fig. 6 shows the process of interpolating the signal samples with sinc functions.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/interpoltime.svg"
      alt="Process of signal reconstruction through sinc interpolation, where the signal samples are converted into scaled sinc functions over which is summed to reconstruct the original signal."
    />
    <figcaption class="numbered">
      Process of signal reconstruction through sinc interpolation, where the signal samples are converted into scaled sinc functions over which is summed to reconstruct the original signal.
    </figcaption>
  </figure>
</div>


### Frequency domain interpolation
From the description in the last line of \eqref{eq:reconstruction} the corresponding effects on the frequency spectrum can be determined by treating $x[n]$ again as values. This gives the Fourier pair
\begin{equation}
    x_a(t) = \sum_{n=-\infty}^\infty x[n]\cdot h_r(t-nT_s)
    \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad
    X_a(\omega) = \sum_{n=-\infty}^\infty x[n] H_r(\omega) e^{-jn\omega T_s}
\end{equation}
By shuffling around the terms on the right and by using the definition of the FTD we obtain the following expression for $X_a(\omega)$
\begin{equation}
    X_a(\omega)
    = H_r(\omega) \left( \sum_{n=-\infty}^\infty x[n] e^{-jn\omega T_s}\right)
    = H_r(\omega) X(e^{j\theta})\mid_{\theta=\omega T_s}.
\end{equation}
Using the definition of the frequency response of the low-pass filter, we end up with the frequency domain interpolation equation:
\begin{equation}
    \boxed{X_a(\omega) =
    \begin{cases}
        T_s \cdot X(e^{j\theta})\mid_{\theta=\omega T_S} & |\omega| \leq \frac{\pi}{T_s} \newline
        0 & \text{elsewhere}
    \end{cases}}
\end{equation}

### Reconstruction in practice
In practice an ideal low-pass filter cannot be implemented as it is non-causal, i.e. it requires future observations in the filtering process, and as the filter impulse response is infinitely long. It is more common to interpolate a signal through a zero-order hold operation. This operation outputs the same sample value for the entirety of the sampling period. In other words, it outputs the last sample value until a new sample appears. This operation creates a step-like signal. The impulse response $h_0(t)$ and frequency response $H_0(\omega)$ can be represented by the following Fourier pair:
\begin{equation}
    h_0(t) = \begin{cases}
        1 & 0 \leq t \leq T_s \newline
        0 & \text{elsewhere}
    \end{cases}
    \quad \overset{\mbox{FTC}}{\circ \hspace{-4px} - \hspace{-4px} \circ } \quad
    H_0(\omega) = \frac{\sin(\omega\frac{T_s}{2})}{\omega \frac{T_s}{2}} e^{-j\omega\frac{T_s}{2}}
\end{equation}
This process is visualized in Fig. 7. In order to compensate for the distortion caused by the zero-order hold operation, the signal is in practice passed through a so-called compensation filter, ideally represented by the frequency response
\begin{equation}
    H_c(\omega) =
    \begin{cases}
        \frac{\omega\frac{T_s}{2}}{\sin(\omega\frac{T_s}{2})}\cdot e^{j\omega \frac{T_s}{2}} & |\omega| \leq \frac{\pi}{T_s} \newline
        0 & |\omega| > \frac{\pi}{T_s}
    \end{cases}
\end{equation}
to compensate for the frequency response of the zero-order hold operation.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/ZOHDAconv.svg"
      alt="The zero-order hold operation and its effect for both the time-domain signal as the frequency spectrum."
    />
    <figcaption class="numbered">
      The zero-order hold operation and its effect for both the time-domain signal as the frequency spectrum.
    </figcaption>
  </figure>
</div>

### Continuous-time versus discrete-time processing
Consider the situation as depicted in Fig. 8, where a signal is processed in the continuous-time domain and in the discrete-time domain. Under two conditions, these operations are identical. The first condition is that the signal $x(t)$ is band-limited such that no aliasing occurs. This means that $X(\omega)=0$ needs to hold for $|\omega| > \frac{\pi}{T_s}$. Secondly, the low-pass filter used for the reconstruction of the signal needs to be ideal. Therefore also $H_r(\omega)=0$ needs to hold $|\omega| > \frac{\pi}{T_s}$.

If both of these conditions are satisfied the relationship between the analog filter $H_a(\omega)$ and the discrete-time filter $H_d(e^{j\theta})$ can be determined as
\begin{equation}
    \boxed{
        H_a(\omega) =
        \begin{cases}
            H_d(e^{j\theta})\mid_{\theta=\omega T_s} & |\omega| \leq \frac{\pi}{T_s} \newline
            0 & \text{elsewhere}
        \end{cases}
    }
\end{equation}


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/DiscreteAnalogSystem.svg"
      alt="Signal processing in the continuous- and discrete-time domain."
    />
    <figcaption class="numbered">
      Signal processing in the continuous- and discrete-time domain.
    </figcaption>
  </figure>
</div>
