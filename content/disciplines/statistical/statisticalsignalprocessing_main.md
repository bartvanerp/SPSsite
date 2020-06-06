+++
title = "Statistical signal processing"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-03-14

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Statistical signal processing: overview"        # name of this item in that menu
  weight = 10                           # location in that menu

+++

When processing and analyzing signals, the noise component makes it more difficult to draw meaningful conclusions on specific signal samples. In order to cope adequately with the uncertainty involved, deterministic signals can better be regarded as random signals, where the exact outcome in time is unknown, but where conclusions can be drawn from the statistical properties of the signal.

The concepts covered in this discipline are:

1. <a href="../statisticalsignalprocessing_signals_main">Stochastic processes and random signals</a> - In this module the deterministic signals as we are familiar with will be extended to contain a certain degree of uncertainty. Furthermore, tools will be provided to deal with this uncertainty.
2. **Optimal (Wiener) filtering** - When the observed signal contains uncertainty, how can it be filtered in an optimal way? This will be discussed in this module, where the Wiener filter will provide the solution to this question.
3. **Linear prediction** - Is it possible to foresee the future? This module will try to predict future observations from past observations.
4. <a href="../statisticalsignalprocessing_rational_main">Rational signal models</a> -  Can we create a signal with desired properties by just filtering noise? Representing a signal via model parameters opens up a variety of possibilities for signal compression, prediction, reconstruction and understanding.
5. **Estimation theory** - How do we estimate parameters from an observed signal when a random component is present? This modules presents different estimation frameworks which allow extracting information from a signal while dealing with uncertainty.
6. <a href="../statisticalsignalprocessing_spectrum_main">Spectrum estimation</a> - When only a portion of a signal is available, accuracy in the calculation of the Fourier transform will inevitably be lost, leading to noisy spectral estimates. This module will explore ways to estimate the frequency spectrum from a limited set of signal samples.
7. <a href="../statisticalsignalprocessing_detection_main">Detection theory</a> - Once we have extract information from a signal in the presence of uncertainty, how do we use this information to make decisions? This will be discussed in this module which deals with a field of statistical signal processing known as detection theory.
