+++
title = "Recap: Fourier transforms"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Recap: Fourier transforms"        # name of this item in that menu
  weight = 2                          # location in that menu
  parent = "Spectral estimation"
+++

Before diving deeper into spectral estimation, a good understanding of the Fourier transform and its variants is desired. This section will describe the Fourier transforms starting with the analytically ideal transform and ending with its practical computational implementation.

The Fourier transform is the operation that converts a signal from the time-domain representation into the frequency-domain representation. The inverse transforms does the opposite. Many types of Fourier transforms exist, although the "main" Fourier transform usually refers to the Fourier transform for continuous-time signals. However, in practice, the fast Fourier transform is most commonly used, which is a computationally efficient variant of the discrete-time Fourier transform.

The summary below should point out the main differences between the different Fourier transforms. A more detailed explanation is beyond the scope of this module, but can be found in their respective modules as referenced below.

<br></br>
## Fourier series (FS)
> A full review of the Fourier series can be found <a href="../../continuous/continuoussignalprocessing_transforms_fourier_main">here</a>.

The Fourier series expansion is a method in which a continuous-time signal is decomposed in sinusoidal signals with harmonically related frequencies. The signal is split into complex phasors with frequency $f=kF_0$, where $k$ is an integer and $F_0$ is the fundamental frequency. The Fourier series coefficients $\alpha_k$ contain the amplitude and phase information of the $k^\text{th}$ harmonic. The Fourier series and the inverse operation are defined as:

\begin{equation}\label{eq:FS}
    \alpha_k = \frac{1}{T_0}\int_0^{T_0} x(t)e^{-j2\pi F_0 kt}\mathrm{d}t
    \ \circ  \hspace{-1.5mm} - \hspace{-1.5mm} \circ \
    x(t) = \sum_{k=-\infty}^\infty \alpha_k e^{j2\pi F_0 kt }
\end{equation}

<br></br>
## Fourier transform for continuous-time signals (FTC)
> A full review of the Fourier transform for continuous-time signals can be found <a href="../../continuous/continuoussignalprocessing_transforms_ftc_main">here</a>.

Whereas the Fourier series only calculates the coefficients of the sinusoidal signals at specific harmonically related frequencies, the Fourier transform for continuous-time signals (FTC) converts a continuous-time signal to a spectrum over all frequencies. The Fourier transform for continuous-time signals is defined as:

\begin{equation}\label{eq:FTC}
    X(f)=\int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \mathrm{d} t
    \ \circ  \hspace{-1.5mm} - \hspace{-1.5mm} \circ \
    x(t) = \int_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \mathrm{d} f
\end{equation}

<br></br>
## Fourier transform for discrete-time signals (FTD)
> A full review of the Fourier transform for discrete-time signals can be found <a href="../../discrete/discretesignalprocessing_transforms_ftc_main">here</a>.

The application of the Fourier Series for continuous-time signals is usually limited, since continuous-time signals cannot be directly recorded on a computer. Instead, these signals are sampled to the discrete-time domain. The Fourier transform that is capable of dealing with discrete-time signals is called the Fourier transform for discrete-time signals (FTD) and is defined as:

\begin{equation}
    X(e^{j\theta}) =
    \sum_{n=- \infty}^{\infty} x[n] e^{-jn\theta}
     \ \circ  \hspace{-1.5mm} - \hspace{-1.5mm}  \circ \
x[n] = \frac{1}{2 \pi} \int_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \mathrm{d} \theta
\end{equation}

<br></br>
## Discrete-time Fourier transform (DFT)
> A full review of the discrete-time Fourier transform can be found <a href="../../discrete/discretesignalprocessing_transforms_dft_main">here</a>.

Although the Fourier transform for discrete-time signals gives a very good representation of the frequency distribution of a signal, the continuous frequency domain variable $\theta$ is still impractical for computer-based operations. The discrete-time Fourier transform (DFT) calculates an equidistantly sampled version of the Fourier transform for discrete-time signals, based on a windowed signal. The discrete-time Fourier transform is defined as:

\begin{equation}
    X_p[k] = \sum_{n=0}^{N-1} x_p[n] e^{-j\frac{2 \pi}{N} k n}
\ \circ  \hspace{-1.5mm} - \hspace{-1.5mm}  \circ \
x_p[n] = \frac{1}{N} \sum_{k=0}^{N-1} X_p[k] e^{j\frac{2 \pi}{N} k n}  
\end{equation}

<br></br>
## Fast Fourier transform (FFT)
The fast Fourier transform is beyond the scope of this reader, but for now it can be regarded as a very efficient implementation of the discrete-time Fourier transform that is used in almost all software packages.
