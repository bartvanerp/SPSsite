+++
title = "Basic building blocks of multirate signal processing"

# date = {{ .Date }}
lastmod = 2019-12-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Basic building blocks of multirate signal processing [⯈]"
  weight = 82
  parent = "Sampling, reconstruction and multirate signal processing"


+++



## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/04YtOIj9zjY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>


<br>

## Introduction
So far we have seen that we require a sampling rate which is larger than twice our largest signal frequency in order to restore our signal correctly afterwards.
Humans can approximately hear frequencies from 20 Hz to 20 kHz. This requires a sampling frequency of at least 40 kHz. This also explains the sampling rate of CD's and MP3 files, which is set to 44.1 kHz.
Having all these samples has its benefits, but also makes real-time processing more difficult. Suppose that each sample is processed individually. This would only leave $1/f_s\approx 0.025$ ms for processing each sample. When performing complicated operations, this period might not be sufficient. Here a trade-off can be made between sampling rate and reconstruction performance. This section will describe the procedure and consequences of altering the sampling rate of a sampled signal.


## Sample rate conversion
Before we consider the effects of altering the sampling frequency, let us first explore the effects of sampling with different sampling frequencies. Fig. 1 shows the real continuous-time signal $x(t)$ with continuous symmetric spectrum $X(\omega)$. The spectrum is bounded up to radial frequency $2\pi f_h$. The figure shows the sampled signal, for 3 different sampling rates and their corresponding spectra.

When the sampling rate exceeds the Nyquist rate, as is the case in the second row in Fig. 1, the original spectrum is repeated, but with some spacing in between the spectra. Because the sampling rate is 2 times the Nyquist rate, the fundamental interval (the interval from $-\pi$ to $\pi$) is only occupied for $100\%/2 = 50\%$.

When the signal is sampled at exactly the Nyquist rate $f_s = 2f_h$, as shown in the third row of Fig. 1, the original spectrum is repeated and the boundaries of the original spectra are right next to each other. There is just no overlap.

Decreasing the sampling rate even further, as shown in the bottom row of Fig. 1, will create a spectrum whose components are repeated at a smaller distance from each other, leading to overlap. This overlap will mix the spectra and is called aliasing. From this aliased spectrum it is in general not possible to reconstruct the original spectrum $X(\omega)$ anymore. Similarly in general the original signal $x(t)$ can also not be reconstructed from this sampled signal.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/spectrarateconversion4.svg"
      alt="The effect of different sampling frequencies on its spectrum. When the sampling frequency does not satisfy the Nyquist criterion, aliasing will occur."
    />
    <figcaption class="numbered">
      The effect of different sampling frequencies on its spectrum. When the sampling frequency does not satisfy the Nyquist criterion, aliasing will occur.
    </figcaption>
  </figure>
</div>

<br>

## Sample rate conversion using D/C- and C/D-converters
A naive way of converting the sampling rate of a digital signal can be achieved using a two-step procedure. First the digital signal is converted to its corresponding continuous-time signal using a D/C-converter, under the assumption that that the initial sampling rate satisfies the Nyquist criterion. Secondly, the continuous-time signal is sampled again, but now with a different frequency using a C/D-converter.

Here we will discuss this procedure for the case when the new sampling frequency is larger than the original sampling frequency, i.e. sample rate increase, and the case when the new sampling frequency is smaller than the original sampling frequency, i.e. sample rate decrease.


### Increasing the sample rate
The sample rate increase procedure is visualized in Fig. 2. The sampled signal $x(n\cdot T_1)$ is assumed to have a spectrum $X(e^{j\theta})$, which fully occupies the fundamental interval. This signal is converted to a continuous-time signal with an absolute frequency spectrum bounded by $-f_{1}/2$ and $f_{1}/2$, corresponding to the boundaries of the fundamental interval.

This continuous-time signal is consecutively sampled with a sampling rate $f_{2}$, which is $L$ times higher than the original sampling rate $f_{1}$, thus $f_{2} = L \cdot f_{1}$. The maximum absolute signal frequency $f_{1}/2$ is now mapped to the relative frequency $\theta = 2\pi \frac{f_{1}/2}{f_{2}} = \pi \frac{f_{1}}{f_{2}}= \frac{\pi}{L}$. Where previously the signal occupied the entire fundamental interval, it now only occupies a portion of the fundamental interval which is specified by the ratio between the sampling frequencies. On one hand in view of relative frequencies, we can interpret this sample rate increase as a shrinkage of the frequency range on the fundamental interval. On the other hand in view of absolute frequencies, this sample rate increase results in a new fundamental interval which is not fully occupied.


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/InterpolatorviaDCCD.svg"
      alt="The ideal process of increasing the sample rate with factor $L=2$ using a D/C- and C/D-converter."
    />
    <figcaption class="numbered">
      The ideal process of increasing the sample rate with factor $L=2$ using a D/C- and C/D-converter.
    </figcaption>
  </figure>
</div>


### Decreasing the sample rate
Alternatively, the sample rate can also be decreased. Where previously the range of the relative frequency spectrum shrunk, we can now expect an expansion of the relative frequency range. This expansion can of course lead to problems, such as aliasing.

The sample rate decrease procedure is visualized in Fig. 3. The sampled signal $x(n\cdot T_1)$ is assumed to have a spectrum $X(e^{j\theta})$, which fully occupies the fundamental interval. This signal is converted to a continuous-time signal with an absolute frequency spectrum bounded by $-f_{1}/2$ and $f_{1}/2$, corresponding to the boundaries of the fundamental interval.

This continuous-time signal is consecutively sampled with a sampling rate $f_{2}$, which is $M$ times smaller than the original sampling rate $f_{1}$, thus $f_{2}=f_{1}/M$. The maximum signal frequency $f_{1}/2$ is now mapped to the relative frequency $\theta = 2\pi \frac{f_{1}/2}{f_{2}} = \pi\frac{f_{1}}{f_{2}}=\pi \cdot M$. Because $M$ is an integer factor which is larger than 1, this can result in a mapping of the maximum frequency outside of the fundamental interval. If the initial signal fully occupies the fundamental interval, this will lead to aliasing. However, if the initial signal does not fully occupy the fundamental interval, aliasing might not occur. This depends on the ratio $M$ of the sampling frequencies and the proportion of the fundamental interval that is initially being occupied. In view of relative frequencies, the ratio $M$ can be interpreted as an expansion factor which will stretch the spectrum horizontally. As long as the boundaries of the stretched spectrum is within the fundamental interval, no aliasing will occur.

In order to prevent aliasing, the continuous-time signal $x(t)$ should be filtered to remove the high-frequency content that would otherwise be mapped outside of the fundamental interval. An analog low-pass filter with cut-off frequency $f_{2}/2$ is required to prevent aliasing. Inevitably, information in the form of high-frequency content is lost by this filtering operation.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/DecimatorviaDCCD.svg"
      alt="The ideal process of decreasing the sample rate without aliasing with a factor $M=2$ using a D/C- and C/D-converter."
    />
    <figcaption class="numbered">
      The ideal process of decreasing the sample rate without aliasing with a factor $M=2$ using a D/C- and C/D-converter.
    </figcaption>
  </figure>
</div>


<br>

## Sample rate decrease (SRD)
Now we will consider changing the sampling frequency by manipulating the signal in the discrete-time domain, without the transformations to the continuous-time domain and back.

The sample rate decrease device decreases the original inter-sample distance $T_1$ by an integer factor $M$ to inter-sample distance $T_2 = M\cdot T_1$. Fig. 4 shows the sample rate decrease processing block. In practice it only outputs every $M$'th sample. Therefore the new output $y[n]$ can be related through the input $x[n]$ as
\begin{equation}
    y[n\cdot T_2] = x[n\cdot(M\cdot T_1)] \qquad \text{or} \qquad y[n] = x[n\cdot M].
\end{equation}
It should be noted that this sample rate decrease operation is not linear time-invariant. Analyzing this processing block therefore cannot use its impulse response. Therefore we will consider the frequency responses of the input and output signal for the characterization of this procedure.


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/SRD.svg"
      alt="Example of sample rate decrease (SRD) operation with $M=2$."
    />
    <figcaption class="numbered">
      Example of sample rate decrease (SRD) operation with $M=2$.
    </figcaption>
  </figure>
</div>


The FTD of the input signal can be written as
\begin{equation}
    X(e^{j\theta}) = \frac{1}{T_1}\sum_{k=-\infty}^{\infty} X_a\left(\frac{\theta}{T_1} - k \frac{2\pi}{T_1}\right)
\end{equation}
and the FTD of the output signal can be determined as
\begin{equation}
    Y(e^{j\theta}) = \frac{1}{T_2}\sum_{r=-\infty}^\infty X_a\left(\frac{\theta}{T_2} - r \frac{2\pi}{T_2}\right),
\end{equation}
where $k$ and $r$ are integers denoting the repetitions of the frequency domain and where $X_a$ denotes the analog frequency spectrum. This second equation can be rewritten by using the sample rate decrease relation $T_2 = M \cdot T_1$ as
\begin{equation}
    Y(e^{j\theta}) = \frac{1}{M}\frac{1}{T_1}\sum_{r=-\infty}^\infty X_a\left(\frac{1}{M}\frac{\theta}{T_1} - r \frac{1}{M}\frac{2\pi}{T_1}\right).
\end{equation}
The summation over $r$ can also be split into two summations by rewriting $r$ as $r=p+k\cdot M$. If we were to sum over $r$ from $-\infty$ to $\infty$, we could interpret this as summing over all spectral repetitions individually as $\sum_{r=-\infty}^\infty$. Another approach would be to divide all the spectral repetitions into $k$ groups of $M$ spectra. Now we can expand the summation by summing over the groups and consecutively over the repetitions inside these groups as $\sum_{k=-\infty}^\infty \sum_{p=0}^{M-1}$.

Thus, with $r=p+k \cdot M$ the previous equation can be rewritten as
\begin{equation}
    \begin{split}
        Y(e^{j\theta})
        &= \frac{1}{M}\frac{1}{T_1}\sum_{k=-\infty}^\infty \sum_{p=0}^{M-1} X_a\left(\frac{1}{M}\frac{\theta}{T_1} - (p+k\cdot M) \frac{1}{M}\frac{2\pi}{T_1}\right) \newline
        &= \frac{1}{M}\sum_{p=0}^{M-1} \frac{1}{T_1} \sum_{k=-\infty}^\infty X_a\left(\frac{1}{M}\frac{\theta}{T_1} - p\frac{1}{M}\frac{2\pi}{T_1} - k\frac{2\pi}{T_1}\right) \newline
        &= \frac{1}{M}\sum_{p=0}^{M-1} \frac{1}{T_1} \sum_{k=-\infty}^\infty X_a\left(\frac{\theta - p\cdot 2\pi}{M \cdot T_1} - k\frac{2\pi}{T_1}\right) \newline
        &= \frac{1}{M}\sum_{p=0}^{M-1} \frac{1}{T_1} \sum_{k=-\infty}^\infty X_a\left(\frac{\frac{\theta}{M} - p\cdot \frac{2\pi}{M}}{ T_1} - k\frac{2\pi}{T_1}\right) \newline
        &= \frac{1}{M}\sum_{p=0}^{M-1} X\left(e^{j\left(\frac{\theta}{M} - p\cdot \frac{2\pi}{M}\right)}\right).
    \end{split}
\end{equation}
In view of relative frequencies, this result can be interpreted as follows: The spectrum of the down-sampled signal $y[n]$ contains $M$ scaled and shifted repetitions of the frequency spectrum of the original signal $x[n]$.

### Example
Consider a factor $M=2$ sample rate decrease process, how will the frequency spectrum of the output signal look like as a function of the input spectrum and when will this process cause aliasing?

From our previously obtained results, we can observe that in view of relative frequencies the output spectrum can be defined as:
\begin{equation}
      Y(e^{j\theta}) = \frac{1}{2}\sum_{p=0}^{1} X\left(e^{j\left(\frac{\theta}{2} - p\cdot \frac{2\pi}{2}\right)}\right) =
      \frac{1}{2} X\left( e^{j\frac{1}{2}\theta}\right) + \frac{1}{2} X\left( e^{j\left(\frac{\theta}{2} - \pi \right)}\right).
\end{equation}
The first term is the original frequency spectrum, where the magnitude is halved and where the frequency content is scaled, expanded horizontally, by a factor of $M=2$  to occupy a frequency band which is twice as wide as it used to be. Fig. 5 shows an example of this scaled frequency band in blue. The second term can be interpreted as the original signal, where the magnitude is halved. The scaling and shifting can be interpreted in two ways. That is either by
$X\left( e^{j\left(\frac{\theta}{2} - \pi \right)}\right)$, which is
shifting the frequency content over $\pi$ and then expanded horizontally by a factor $M=2$. Alternatively we can write
$
X\left( e^{j\left(\frac{\theta}{2} - \pi \right)}\right) =
X\left( e^{j\left(\frac{\theta - 2 \pi}{2} \right)}\right)
$, thus first expand horizontally by a factor $M=2$ and then shift the frequency content over $2\pi$.
The second term is represented in red in Fig. 5. The summation of both spectra yields the frequency spectrum of the output signal.

In Fig. 5 no aliasing occurs, as the spectral repetitions do not overlap each other. However, in this illustrative case the frequency content of the original signal was band-limited from $-\pi/2$ to $\pi/2$. If the original signal was not band-limited to a part of the fundamental interval, but would occupy the entire fundamental interval, then the horizontal scaling of the spectrum would inevitably cause aliasing as the frequency content would spill out of the fundamental interval. So when does aliasing occur and when does it not? From our interpretation of the second term of the output spectrum, where we first expand the spectrum horizontally and then shift over $2\pi$, we can deduce that the expanded frequency spectrum should be band-limited to the fundamental interval. This would also mean that if the frequency spectrum gets expanded by a factor $M=2$, then no aliasing occurs when the original, symmetric and thus real, spectrum only occupies frequencies in the range $-\pi - \frac{\pi}{2}$ and $\frac{\pi}{2} - \pi$. Concluding it follows that the SRD operation can introduce aliasing depending on the frequency spectrum of the original signal.


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/SRDspectra5b.svg"
      alt="Example of the input and output spectrum of a factor $M=2$ sample rate decrease operation."
    />
    <figcaption class="numbered">
      Example of the input and output spectrum of a factor $M=2$ sample rate decrease operation.
    </figcaption>
  </figure>
</div>

<br>

## Decimator
By using a low-pass filter aliasing can be prevented. This system is called a decimator and its operations are shown in Fig. 6. The low-pass filter has a relative cut-off frequency at $\pi/M$, where $M$ denotes the sample rate decrease factor. This cut-off frequency is an inevitable result of the horizontal scaling caused by the sample rate decrease operation as we discussed in the previous example. By forcing the signal to be band-limited from $-\pi/M$ to $\pi/M$, the horizontally scaled frequency spectrum is guaranteed be stay within the fundamental interval. A downside of this low-pass filtering is that we might sacrifice signal information in the form of high-frequency content, as this is filtered out. Of course this loss depends on whether the original signal actually has frequency content outside of the boundaries set by the low-pass filter.


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/decimator.svg"
      alt="The operations performed by a decimator."
    />
    <figcaption class="numbered">
      The operations performed by a decimator.
    </figcaption>
  </figure>
</div>

<br>

## Sample rate increase (SRI)
Besides decreasing the sampling rate, we might also be interested in increasing the sampling rate. A practical use case is when a signal is observed and we are interested in the signal value in between two samples.
A sample rate increase device can increase the sampling rate by a factor $L$, i.e. $T_2 = T_1/L$. This sample rate increase device inserts zeros in between samples to construct the output signal.
Fig. 7 shows the operations of the sample rate increase device. Its operations can therefore be defined as
\begin{equation}
    y[n\cdot T_2] =
    \begin{cases}
        x\left(n \cdot \frac{T_1}{L}\right) & \text{for } n= k\cdot L \newline
        0 & \text{otherwise}
    \end{cases}
\end{equation}
or as
\begin{equation}
    y[n] =
    \begin{cases}
        x\left[n / {L}\right] & \text{for } n= k\cdot L \newline
        0 & \text{otherwise}
    \end{cases}
\end{equation}


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/SRI.svg"
      alt="Example of sample rate increase (SRI) operation with $L=2$."
    />
    <figcaption class="numbered">
      Example of sample rate increase (SRI) operation with $L=2$.
    </figcaption>
  </figure>
</div>


Again this operation is not linear time-invariant and therefore we will discuss the consequences of this operation by evaluating the frequency domain. The FTD of the input signal can be determined as
\begin{equation}
    X(e^{j\theta}) = \sum_{n=-\infty}^\infty x[n] e^{jn\theta}
\end{equation}
and of the output signal as
\begin{equation}
    Y(e^{j\theta}) = \sum_{n=-\infty}^\infty y[n] e^{jn\theta}.
\end{equation}
By substituting $n=m\cdot L$ and by noting that only every $L$'th sample of $y[n]$ is non-zero, the summation can be rewritten as
\begin{equation}
    Y(e^{j\theta}) = \sum_{m=-\infty}^\infty y[m\cdot L] e^{jmL\theta}.
\end{equation}
The term $y[m\cdot L]$ simply equals the samples $x[m]$ and therefore
\begin{equation}
    Y(e^{j\theta}) = \sum_{m=-\infty}^\infty x[m] e^{jmL\theta} = X(e^{jL\theta}).
\end{equation}
As $L$ is an integer value and in view of relative frequencies, the frequency spectrum is now shrunk horizontally by a factor $L$ and spectral repetitions from outside the fundamental interval move inside of the fundamental interval.



<br>
## Interpolator
These spectral repetitions are an undesired consequence of the sample rate increase operation. These repetitions allow the signal to be have these zeros in between the actual samples. In most applications these zeros are undesired and we would like to have signal values that better represents the signal. We would like to interpolate the signal with intermediate samples such that the resampled signal is smoother.

Fig. 8 visualizes the operations of an interpolator. This processing block removes the spectral repetitions in the frequency domain and therefore smooths the signal. The zero-valued samples then represent the true signal. The removal of these spectral repetitions is performed by low-pass filtering the upsampled signal, such that only one repetition of the original spectrum remains. The output samples can be determined analytically from the input samples through the interpolation equation
\begin{equation}
    \tilde{y}[n] = \sum_{m=-\infty}^\infty x[m] \cdot \frac{\sin\left(\frac{\pi}{L}(n-mL)\right)}{\frac{\pi}{L}(n-mL)}.
\end{equation}


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/interpolator.svg"
      alt="The operations performed by an interpolator."
    />
    <figcaption class="numbered">
      The operations performed by an interpolator.
    </figcaption>
  </figure>
</div>

<br>

## Oversampled A/D-converter
Another example of the application of a decimator is the so called oversampled A/D-convertor. Assume a continuous-time signal $x_a(t)$ with a wide FTC spectrum $X_a(\omega)$ from which we want to convert frequency components smaller or equal to $\pi=T_1$ into a discrete-time signal $x[n]$. This requires us to first low-pass filter the signal to prevent aliasing and to then sample the signal. Fig. 9 shows this procedure. The problem with this approach is that the design of the analog low-pass filter is relatively difficult as we desire a very small transition band. Alternatively, we could perform this filtering as shown in Fig. 10. Here the signal is oversampled and then filtered with an analog low-pass filter with less strict requirement as the transition band is wider. The signal is then sampled and no aliasing occurs in the frequency spectrum that we wish to capture. Then the signal is low-pass filtered using a digital filter, which is easier to design and can be altered later on in the design process. Finally the signal is decimated to stretch out the desired frequency range to occupy the fundamental interval. The complexity is moved to the digital domain.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/ADconvertor.svg"
      alt="Analog design approach to sampling a low-pass filtered signal."
    />
    <figcaption class="numbered">
      Analog design approach to sampling a low-pass filtered signal.
    </figcaption>
  </figure>
</div>


<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/multirate/oversampledAD.svg"
      alt="Digital design approach to sampling a low-pass filtered signal. The signal is oversampled and less strictly filtered in the analog domain and the complexity is moved to the digital domain instead."
    />
    <figcaption class="numbered">
      Digital design approach to sampling a low-pass filtered signal. The signal is oversampled and less strictly filtered in the analog domain and the complexity is moved to the digital domain instead.
    </figcaption>
  </figure>
</div>
