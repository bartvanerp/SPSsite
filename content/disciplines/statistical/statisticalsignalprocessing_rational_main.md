+++
title = "Rational signal models"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-07-15

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Rational signal models"        # name of this item in that menu
  weight = 50                           # location in that menu

+++

## Introduction

In many applications, it is useful to generate random signals with desired properties or to obtain a representation of a random signal which captures a set of the signal characteristics. By the term *model* we indicate a mathematical description which provides a representation of certain properties of the signal. If we are able to construct a useful model of a random signal, then we can use this model for various applications. For example, to obtain a better understanding of the physical mechanism generating the signal, to detect changes in the signal for diagnostics purposes, to synthetize artificial signals similar to the natural ones, to extract parameters for pattern recognition and machine learning, to obtain a more efficient representation of the signal for data compression.

We often assume a model to be parametric, i. e., a function completely defined by a finite number of model parameter. In this module, we further restrict our attention to a particular class of models known as rational signal models, whose system function and power spectrum can be expressed as a ratio between polynomials in $z$ (or equivalently in $e^{j\omega}$ ). In this module, we will particularly on stochastic modeling, by which we describe a signal as the hypothetical output of some linear-time invariant system, the input of which is white noise.

<br></br>

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/9Cnb97vLxfg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module covers the following topics:

1. <a href="../statisticalsignalprocessing_rational_recap">Recap: LTI systems </a>- This section provides a brief review of fundamental concepts including linear time-invariant systems, stability, invertibility and minimum-phase.

3. <a href="../statisticalsignalprocessing_rational_spectral_factorization">Spectral factorization </a>- Can we obtain any random signal by simply filtering white noise? In this section, we describe how this can be achieved by the innovation representation.

2. <a href="../statisticalsignalprocessing_rational_arma">Auto-regressive moving-average (ARMA) signal models  </a>- This section describes an efficient representation of (stationary) random signals in terms of two polynomials, one accounting for the "autoregressive" part and the other for the "moving-average" part.



<br></br>
