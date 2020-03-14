+++
title = "Statistical signal processing"         # name of webpage

# date = {{ .Date }}
lastmod = 2019-05-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Statistical signal processing: overview"        # name of this item in that menu
  weight = 10                           # location in that menu

+++

When processing and analyzing signals, the noise component makes it more difficult to draw meaningful conclusions on specific signal samples. In order to cope adequately with the uncertainty involved, deterministic signals can better be regarded as random signals, where the exact outcome in time is unknown, but where conclusions can be drawn from the statistical properties of the signal.

The concepts covered in this module are:

1. <a href="../statisticalsignalprocessing_signals_main">Stochastic or random signals</a> - In this module the deterministic signals as we are familiar to will be extended to also contain a certain degree of uncertainty. Furthermore, tools will be provided to deal with this uncertainty.

2. **Optimal (Wiener) filtering** - When the observed signal contains uncertainty, how can it be filtered in an optimal way? This will be discussed in this module, where the Wiener filter will provide the solution to this question.

3. **Linear prediction** - Is it possible to foresee the future? This module will try to predict future observations from past observations.

4. <a href="../statisticalsignalprocessing_rational_main">Rational signal models</a> - With this notion of uncertainty, it is actually possible to create a signal with a desired frequency spectrum by just filtering noise.

5. <a href="../statisticalsignalprocessing_spectrum_main">Spectrum estimation</a> - With the approximations made in from the Fourier transform for continuous-time signals to the fast Fourier transform, accuracy will inevitably be lost, leading to noisy spectral estimates. This module will explore ways to model the frequency spectrum.
