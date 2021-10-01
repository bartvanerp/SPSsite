+++
title = "Spectral estimation"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-21

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Spectral estimation"        # name of this item in that menu
  weight = 60                           # location in that menu

+++

## Introduction

Spectral estimation is concerned with estimating the power spectrum of a stochastic signal from a limited set of observations. The power spectrum describes how the power is distributed across frequencies and can thus provide important information about the signal itself. The distribution of the power of the signal across its frequency range can help in characterizing unwanted noise sources. Other purposes of spectral estimation include the detection of periodicities, signal compression and signal classification. Manipulation of the spectrum through filtering allows for the denoising, analysis, and classification of signals. The key underlying aspect of all these signal processing techniques in the frequency domain is a good understanding of the spectrum of a signal.

The simplest and most straightforward method for estimation of the signal spectrum is via the Fourier transform, which is often applied by using the Fast Fourier Transform (FFT) implementation, typically available in many computing environments, including MATLAB. However, careful understanding of the FFT operation and the analyzed signal are necessary in order to avoid inaccurate estimation and/or misinterpretation of the obtained results. An example of such a situation is represented in Fig. 1. Here a single discrete-time sinusoidal signal is plotted over time. Suppose that an ambitious student tries to determine the frequency of this sinusoid by simply applying the `fft()`-function. He or she would expect to find only 2 peaks at the positive and negative frequency of the sinusoid, but instead the right-hand plot in Fig. 1 is obtained. Here, there are multiple frequency components present, which seems to be unrelated to the original sinusoidal signal; moreover, the frequency axis does not immediately correspond to the actual frequency, but to some index $k$.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/spectrum/spectral_introduction.svg"
      alt="A sinusoidal discrete-time signal and the corresponding discrete-time Fourier transform."
    />
    <figcaption class="numbered">
      A sinusoidal discrete-time signal and the corresponding discrete-time Fourier transform.
    </figcaption>
  </figure>
</div>

After more careful studying, the student comes to the realization that the operation he performed just gave him an <i>estimate</i> of the frequency content. In this specific case, the student could easily have obtained the expected frequency spectrum. The student neglected the fact that the `fft()`-operation assumes a periodic signal. In this case the signal is <i>windowed</i>, meaning that the infinitely long signal is cropped to a finite length, which is no longer periodic, leading to potentially undesirable results in the frequency domain.

From this we can conclude that just calculating the spectrum of a signal, especially when it is comprised of multiple signals, is not as easy as it sounds. Since any real-world signal can be observed only for a limited amount of time, **all real-world signals are virtually windowed**. Another reason for windowing is to study non-stationary signals in short time segments, within which they can be considered stationary. Besides the effects of windowing, we cannot know in advance whether the signal is periodic or not. Because of these reasons, it is usually impossible to determine the exact spectrum of an observed random signal. Therefore we need to resort to estimation techniques for the calculation of the frequency spectrum of a finite random signal, a problem known as <i>spectral estimation</i>.
### Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/G0uywfC6BRE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

<br></br>
## Module overview
This module covers the following topics:

1. <a href="../../../courses/5cta0/statisticalsignalprocessing_spectrum_intro_distributions">Introduction to spectral estimation</a> In order to cover the topic of spectral estimation, it is important that to review topics such as the Fourier transform and calculation of the power spectrum for energy and power signals. In practice, however, all real-world signals are windowed, which leads to several consequences when calculating the power spectrum.
2. <a href="../../../courses/5cta0/statisticalsignalprocessing_spectrum_nonparametric">Non-parametric methods</a> - In order to improve the estimation of the spectral representation, several methods can be applied, such as combining several estimates of the spectrum.
3. <a href="../../../courses/5cta0/statisticalsignalprocessing_spectrum_parametric">Parametric methods</a> - Another methodology involves the modelling of the frequency spectrum through the use of several parameters. The parameters define the shape of the spectrum and by learning these parameters, the true spectrum can be estimated.


<br></br>
## Summary
This module should have given a relatively concise overview of the field of spectral estimation. Although this module could seem to be lengthy, the concepts introduced are only briefly touched upon.

First we have seen why it is important to analyze the spectrum of a signal. This usually provides us with more information about the signal and  enables better manipulation of the signal. Conventional methods using the Fourier transform and its many version provide the tools to estimate a spectrum and the power spectral density. However, the windowing involved when dealing with finite length signals reduces the spectral information through the inevitable smoothing and therefore new methods should be introduced to model the power spectral density. The first class of methods are non-parametric. They model the power spectral density by applying the Fourier transform in some kind of clever way, through clever windowing, overlap and averaging. Furthermore we have seen that the auto-correlation function of a signal is closely related to the power spectral density by the Wiener-Khinchin relation, denoting that we are dealing with Fourier pairs. This relationship introduced the topic of parametric spectral estimation, in which the signal is assumed to be modelled by an AR(p), MA(q) or ARMA(p,q) process. These processes have pre-determined auto-correlation functions and power spectral densities, parameterized by the process coefficients. By estimating these parameters through the comparison of the auto-correlation functions, the power spectral density can be modelled.
