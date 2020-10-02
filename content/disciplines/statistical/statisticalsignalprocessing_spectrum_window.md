+++
title = "Windowing"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Windowing"        # name of this item in that menu
  weight = 3                      # location in that menu
  parent = "Spectral estimation"
+++


## Causes and issues of windowing
The methods presented in the previous section for the calculation of the power spectrum ideally require an infinitely-long signal for the most accurate estimation. However, in practice, all real-world signals are <i>windowed</i>, which means that only a finite portion of the signal is considered, instead of the entire signal. Windowing can result from many different causes. First, it is highly unlikely that an infinite number of signal samples are available for analysis and therefore it is inherently windowed by the limited observation time. Secondly, windowing makes an algorithm less computationally expensive. There are operations, such as matrix inversion, whose computational costs do not scale linearly with the number of samples. Therefore it is important to use a limited number of samples. Finally, there are cases in which the signal is not stationary, but most analysis methods assume stationarity. In these cases, the signal is windowed such that it can be assumed to be locally stationary.

Calculating the spectrum of signal $x[n]$ when only the windowed signal $\tilde{x}[n]$ is available leads to several issues. First of all, in most practical cases the spectrum will be calculated through the N-point discrete-time Fourier transform (DFT), which is actually a sampled version of the Fourier transform for discrete-time signals (FTD). Therefore, it is possible that important signal characteristics will get lost. Secondly, windowing causes <i>spectral leakage</i>, which means that single frequency components will be spread throughout the frequency spectrum. Finally, windowing leads to loss of <i>resolution</i>, which relates to the ability of distinguishing between different spectral components.

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/Woi2HemfAvI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

<br></br>
## A rectangular window
To illustrate the consequences of windowing, we will show the case of the simplest window: the rectangular window. The rectangular window $w[n]$ can be defined as
\begin{equation}
    w[n] =
    \begin{cases}
        1,      &\text{for }n = 0,1,\ldots, N-1 \newline
        0,      &\text{otherwise}
    \end{cases}
\end{equation}
where $N$ is the length of the window. The windowed signal $\tilde{x}[n]$ is obtained by multiplying the original signal $x[n]$ with the window in the time domain:
\begin{equation}
    \tilde{x}[n] = w[n]x[n].
\end{equation}
For a rectangular window this operation can be regarded as taking only a finite set of samples into account.

Suppose that we know that the Fourier transform of discrete-time signals of $x[n]$ is ideally $X(e^{j\theta})$ and we would like to see the effect of windowing on the estimated spectrum. Recall that a convolution in the time-domain results in a multiplication in the frequency domain. It can be shown that the opposite relation holds as well: a multiplication in the time domain will result in a periodic convolution in the frequency domain. This relationship leads to the following frequency response of the windowed signal $\tilde{X}(e^{j\theta})$ as
\begin{equation}
    \tilde{X}(e^{j\theta}) = X(e^{j\theta}) \ast W(e^{j\theta}),
\end{equation}
where $W(e^{j\theta})$ is the frequency response of the window. So the frequency response of the window determines how the original spectrum is influenced by windowing. From the definition of the Fourier transform for discrete-time signals, the spectrum of the rectangular window can be determined as
\begin{equation}
    \begin{split}
        W(e^{j\theta})
        &= \sum_{n=- \infty}^{\infty} w[n] e^{-jn\theta} , \newline
        &= \sum_{n=0}^{N-1} e^{-jn\theta}, \newline
        &= \frac{1-e^{-jN\theta}}{1-e^{j\theta}}, \newline
        &= \frac{\left(e^{j\frac{N}{2}\theta} - e^{-j\frac{N}{2}\theta}\right)e^{-j\frac{N}{2}\theta}}{\left(e^{j\frac{1}{2}\theta} - e^{-j\frac{1}{2}\theta}\right)e^{-j\frac{1}{2}\theta}}, \newline
        &= \frac{\frac{1}{2j}\left(e^{j\frac{N}{2}\theta} - e^{-j\frac{N}{2}\theta}\right)}{\frac{1}{2j}\left(e^{j\frac{1}{2}\theta} - e^{-j\frac{1}{2}\theta}\right)}e^{-j\frac{N-1}{2}\theta}, \newline
        &= \frac{\sin(N\theta/2)}{\sin(\theta/2)}e^{-j\frac{N-1}{2}\theta},
    \end{split}
\end{equation}
where the ratio $\frac{\sin(N\theta/2)}{\sin(\theta/2)}$ is the <i>Dirichlet</i> or <i>periodic and aliased sinc</i> function. This function is convoluted with the true spectrum $ X(e^{j\theta}) $ to obtain the estimated spectrum $\tilde{X}(e^{j\theta})$ from the windowed signal $\tilde{x}[n]$. The frequency response of the rectangular window is also a function of the window length $N$. Fig. 1 shows three rectangular windows with their respective normalized magnitude responses on the logarithmic scale for increasing $N$. The magnitude response is usually normalized to the peak at 0 dB for comparison. It can be noted that an increase of $N$ results in a better <i>resolution</i> of the estimated spectrum, which means that the width of the main lobe is smaller. However, the height of the side lobe does not change with $N$. This has important consequences for spectral leakage, as will be discussed hereafter.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/window_N.svg"
      alt="The normalized magnitude response of a rectangular window for increasing window lengths $N$. From the figure it can be noted that the resolution increases for an increasing $N$. The side lobe level is identical in all three cases."
    />
    <figcaption class="numbered">
      The normalized magnitude response of a rectangular window for increasing window lengths $N$. From the figure it can be noted that the resolution increases for an increasing $N$. The side lobe level is identical in all three cases.
    </figcaption>
  </figure>
</div>
<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/window_nomenclature.svg"
      alt="Nomenclature of the normalized magnitude response of a window function, where the 3 dB bandwidth and the side lob level are indicated."
    />
    <figcaption class="numbered">
      Nomenclature of the normalized magnitude response of a window function, where the 3 dB bandwidth and the side lob level are indicated.
    </figcaption>
  </figure>
</div>


From Fig. 2 it can be noted that the frequency response always consists of several <i>lobes</i>. The largest lobe is called the <i>main lobe</i> and the peak of this lobe is usually normalized to 1, which is 0 dB. This lobe should be as narrow as possible in order to get an accurate approximation of the real frequency spectrum. Its width can be described by the so-called <i>-3 dB bandwidth</i>, which is the size of the frequency interval on which the spectral power is reduced by less than a factor 2. In other words, the -3 dB bandwidth includes all frequencies whose power is still larger than half its original value. It turns out that the -3 dB bandwidth can be approximately calculated as we will show shortly.

The smaller lobes in Fig. 2 are called <i>side lobes</i> and they lead to <i>spectral leakage</i>. When convolving the original spectrum with the magnitude response of the window, the side lobes spread the amplitude of the frequency spectrum at the locations of the side lobes, thus creating additional (non-existing) frequency components. In order to limit the spectral leakage, it is desirable to have side lobes as low as possible compared to the main lobe. The difference in gain between the main lobe and the most significant side lobes is also known as the <i>side lobe level</i>. The height of the first side lobe does not depend $N$ for the rectangular window. This has to do with the fact that no matter how large N, there is always a sharp change from 1 to  0  at  the borders of the window. Thus, the only way to reduce spectral leakage is to change window.

<br></br>
## Different types of windows
The rectangular window is used in most cases because of its high resolution. However, the relatively high side lobe level can cause problems when small frequency components are to be detected. Changing the shape of the window can result in different frequency characteristics, such as a different resolution or side lobe level. Numerous different windows have been proposed over the years and Fig. 3 shows three of them: the rectangular, triangular and Hanning window for the same window length. In the corresponding normalized frequency spectra, it can be seen that there is a clear trade-off between the -3 dB bandwidth and the side lobe levels. This means that you can only improve either the resolution or the spectral leakage when estimating a spectrum using windowing.

As said before, the -3 dB bandwidth is dependent on the length of the window and it can be analytically approximated. The side lobe level is dependent on the type of window that is chosen. It is not influenced by the length of the window. The table belows shows the -3 dB bandwidth and the side lobe levels for various windowing functions. From this it can be noted that the selection of the type of window is performed firstly by meeting the desired specifications of the spectral leakage and then selecting a window length for sufficient resolution.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/window_types.svg"
      alt="Three types of windows, including the rectangular window, the triangular window and the Hanning window, with their respective normalized frequency spectra."
    />
    <figcaption class="numbered">
      Three types of windows, including the rectangular window, the triangular window and the Hanning window, with their respective normalized frequency spectra.
    </figcaption>
  </figure>
</div>

<table>
    <tr>
        <th style="text-align:center"> Window </th>
        <th style="text-align:center"> -3 dB bandwidth </th>
        <th style="text-align:center"> Side lobe level </th>
    </tr>
    <tr>
        <td style="text-align:center"> Rectangular </td>
        <td style="text-align:center"> $\approx 0.89\frac{2\pi}{N}$ </td>
        <td style="text-align:center"> -13 dB </td>
    </tr>
    <tr>
        <td style="text-align:center"> Triangular </td>
        <td style="text-align:center"> $\approx 1.28\frac{2\pi}{N}$ </td>
        <td style="text-align:center"> -27 dB </td>
    </tr>
    <tr>
        <td style="text-align:center"> Hanning </td>
        <td style="text-align:center"> $\approx 1.44\frac{2\pi}{N}$ </td>
        <td style="text-align:center"> -32 dB </td>
    </tr>
</table>


<br></br>
## Loss of resolution
 The resolution is an important characteristic of a spectral estimation method. When windowing, the resolution depends on the width of the main lobe of the window spectrum. We show this with a practical example. In Fig. 4, an ideal frequency spectrum of a periodic signal is given. The approximations of this signal due to windowing are shown in all the other plots. Several types and lengths of windows have been used and several observations can be made. First, when two frequency components are close together they may not be distinguishable if the resolution of the window is too low. Secondly, the spectral peak widths are dependent on both the window type and window length. Finally the influence of the spectral leakage can also be noted. It creates additional <i>spurious peaks</i>, which might overshadow smaller frequency components.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/resolution.svg"
      alt="A signal with three frequency components is windowed by several windows, differing in type and length, and the final estimated normalized frequency spectrum is determined. It can be seen how the length of the filter and the type of window influence the resolution, i.e. the ability to distinguish between spectral components, and the spectral leakage, i.e. the appearance of spurious peaks."
    />
    <figcaption class="numbered">
      A signal with three frequency components is windowed by several windows, differing in type and length, and the final estimated normalized frequency spectrum is determined. It can be seen how the length of the filter and the type of window influence the resolution, i.e. the ability to distinguish between spectral components, and the spectral leakage, i.e. the appearance of spurious peaks.
    </figcaption>
  </figure>
</div>

<br></br>
## Zero-padding
If we would like to calculate the spectrum of an infinitely long signal using only a finite number of samples then we will need to window our signal in some way. These windows influence the frequency spectrum that we approximate. The approximated frequency spectra discussed so far were continuous frequency spectra obtained by the Fourier transform for discrete-time signals (FTD). However, in practice this Fourier transform is not suitable to compute, therefore usually the discrete-time Fourier transform (DFT) is used, which is commonly implemented as the fast Fourier transform. In short, the discrete-time Fourier transform does not return a continuous frequency spectrum, but it returns samples of the continuous spectrum.

Thus, besides the consequences of windowing, the estimated spectrum is also a sampled version of the true continuous spectrum. When the estimated continuous spectrum is represented by $\hat{X}(e^{j\theta})$, the sampled spectrum is denoted by $X[k]$, where $k$ is the sample index, ranging from $0$ to $N-1$, where $N$ is the window length. Instead of enlarging the window length in order to obtain more samples, it is also possible to <i>zero-pad</i> the signal. Suppose that a windowed signal $\tilde{x}[n]$ of length $N$ is observed and the spectrum is calculated using the DFT. This DFT samples the FTD of the windowed signal. The number of samples simply equals the length of the windowed signal, thus $N$. To decrease the step at which we "walk" on the continuous spectrum, the signal can be extended with $L-N$ zeros, such that the signal, as well as the obtained spectrum, have now length $L>N$. This operation is known as zero-padding. To understand how this work, recall the definition of the DFT, by which the sampled spectrum $\hat{X}[k]$ can be determined as
\begin{equation}
    \hat{X}[k] = \sum_{n=0}^{N-1} \tilde{x}[n] e^{-j\frac{2 \pi}{N} k n}. \qquad \text{for }k=0,1,\ldots, N-1
\end{equation}
If the signal is now zero-padded to length $L$, the range of $k$ changes and so does the factor in the complex exponential, which determines the sampling interval. This can be seen by
\begin{equation}
    \begin{split}
        \hat{X}[k]
        &= \sum_{n=0}^{L-1} \tilde{x}[n] e^{-j\frac{2 \pi}{L} k n}, \qquad \text{for }k=0,1,\ldots, L-1 \newline
        &= \sum_{n=0}^{N-1} \tilde{x}[n] e^{-j\frac{2 \pi}{L} k n}. \qquad \text{for }k=0,1,\ldots, L-1
    \end{split}
\end{equation}
The sampling distance in the frequency domain is now decreased, but the summation is still from $n=0$ up to $N-1$, because for larger values of $n$ the signal $\tilde{x}[n]$ is simply zero.
Fig. 5 shows the approximated continuous spectrum of a windowed signal of length $N$. Besides this the DFT of the windowed signal is calculated, leading to the sampling of the continuous spectrum. Furthermore the signal is zero-padded up to several lengths $L$, which change the number of samples and the sampling intervals of the DFT. Depending on the length of the signal and the length of the zero-padding, some interesting phenomena can be observed, because in some cases the values at the sampling locations might give an unrealistic view of the frequency spectrum.

Let us go briefly through Fig.  5. The ideal spectrum $X(e^{j\theta})$ is plotted in blue. This could be obtained only from an infinite-length signal. In red, we see the estimated FTD of the signal after applying a window of N=30. This function is continuous and it is calculated analytically by knowledge of the $x[n]$ before windowing and by knowledge of the window function $w[n]$. However, in practice,  we do not know $x[n]$ before windowing, so we calculate the FFT from the windowed signal $\tilde{x}[n]$, obtained a discrete function $\tilde{X}[k]$. If we only use N=30 samples to calculate the FFT (no zero padding), we obtain the function in green, by which we would probably  misinterpret the signal as composed of two frequency peaks. If we apply a zero padding of 90 samples, then we obtain the discrete function in pink, from which we can correctly see the main peak. By applying zero padding we have increased the step at which we walk on the underlying red function, which is the approximated $\tilde{X}(e^{j\theta})$ obtained from the windowed signal. However, although our understanding of the original signal might improve by virtually increasing the number of samples on which we calculate the FFT, we can never recover the true spectrum (in blue) after windowing.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/zeropad.svg"
      alt="Comparison between an ideal frequency spectrum of a sinusoidal signal with frequency $\theta_0=\pi/2$, an approximated frequency spectrum using a rectangular window of length $N$, where $N=30$, and the DFT of the zero-padded signal for different lengths $L$. Keep in mind that this is a single-sided spectrum and therefore the number of sample points is half of the length of the zero-padded signal."
    />
    <figcaption class="numbered">
      Comparison between an ideal frequency spectrum of a sinusoidal signal with frequency $\theta_0=\pi/2$, an approximated frequency spectrum using a rectangular window of length $N$, where $N=30$, and the DFT of the zero-padded signal for different lengths $L$. Keep in mind that this is a single-sided spectrum and therefore the number of sample points is half of the length of the zero-padded signal.
    </figcaption>
  </figure>
</div>

It is important to keep in mind that zero-padding does not improve the resolution of the estimated frequency spectrum, as this is only determined by the window type and length. The zero-padding only influences the sampling interval of the DFT. In other words, it determines the step at which we walk on the underlying continuous spectrum. Moreover, since windowing causes loss of information (it is equivalent to setting to zero all the samples outside the window), the continuous spectrum is an approximated version of the real spectrum. To summarize, in practice, we can only compute a sampled, approximated version of the frequency spectrum.

In order to relate this section to the topic of power spectral density estimation, it should be noted that there is a direct relation between the spectrum of a signal and the power spectral density. Since the FTD is usually difficult to compute analytically, it is usually approximated by the sampled version of the spectrum determined by the DFT, which can be calculated numerically through the fast Fourier transform. As a direct consequence, the power spectral density is also a sampled, approximated version of the real power spectrum.

<br></br>
## Short-time Fourier transform
The short-time Fourier transform is a technique commonly used to calculate the Fourier spectrum when the frequency, amplitude or phase are varying over time. The short-time Fourier transform is defined as
\begin{equation}
    X(e^{j\theta}, n) = \sum_{p=-\infty}^{\infty} x[n-p]\cdot w[p] e^{-jp\theta},
\end{equation}
where $w[p]$ indicates a windowing function that selects a segment of the total signal. By extracting this finite segment, the spectral characteristics can be approximated to be stationary over the segment duration. In practice, the signal is split into multiple (overlapping) segments of which the short-time Fourier spectrum is calculated. By doing so, a time-varying frequency spectrum can be obtained, showing the frequency spectrum over time.

Using the DFT the short-time Fourier distribution of a signal of length $N$, zero-padded to length $L$, can be calculated as
\begin{equation}
    X_\text{STFT}[k,n] = X(e^{j\theta})\mid_{\theta=k\frac{2\pi}{L}} = \sum_{p=0}^{N-1}x[n-p]w[p]e^{-jpk\frac{2\pi}{L}}.
\end{equation}
