+++
title = "Stochastic processes and random signals"         # name of webpage

# date = {{ .Date }}
lastmod = 2019-05-20

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Stochastic processes and random signals"        # name of this item in that menu
  weight = 20                           # location in that menu

+++

## Introduction
When processing and analyzing signals, the noise component makes it more difficult to draw meaningful conclusions on specific signal samples. In order to cope adequately with the uncertainty involved, deterministic signals can better be regarded as random signals, where the exact outcome in time is unknown, but where conclusions can be drawn from the statistical properties of the signal.

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/yaZmrQy-wkA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module will cover the following topics:

1. <a href="../statisticalsignalprocessing_signals_signals">Random signals</a> - This section will discuss the concept of random signals. Several signal statistics are discussed and some properties are elaborated upon.
2. <a href="../statisticalsignalprocessing_signals_stationarity">Stationarity and ergodicitity</a> - In all practical applications, the exact signal statistics are unknown. These therefore need to be approximated based on a limited set of data. The assumptions of stationarity and ergodicity permit calculation of signal statistics a from a single observation of a random signal.
3. <a href="../statisticalsignalprocessing_signals_psd">Power spectral density</a> -  Analysis of the second order statistics, such as the auto-correlation and power spectral density, can provide important insights into a random signal. From the Wiener-Khinchin theorem it follows that the power spectral density of a random signal is given by the Fourier transform of the auto-correlation function.
