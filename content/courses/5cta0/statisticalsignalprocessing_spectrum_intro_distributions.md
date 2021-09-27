+++
title = "3.1 Introduction to spectral estimation"         # name of webpage

# date = {{ .Date }}
lastmod = 2021-08-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.5cta0]                       # name of menu section (main module)
name = "3.1 Introduction to spectral estimation"        # name of this item in that menu
weight = 305                          # location in that menu

+++

## Introduction

One of the most common operation in statistical signal processing systems is the calculation, either implicitly or explicitly, of the signal's Fourier spectrum. Thus, a good understanding of the Fourier transform is a necessary prerequisite for spectral estimation. Distinguishing between (discrete-time) energy and power signals, we will see how the spectrum can be obtained directly from the Fourier transform of the signal, or indirectly from the autocorrelation function. In practice, real-world signals have a finite duration and thus are not ideal, infinetely-long signals; this implicit signal windowing has consequences on the maximum attainable spectral resolution, which is the the degree to which a spectral estimate can express spectral details.

## Module overview
This module covers the following topics:

1. <a href="../statisticalsignalprocessing_spectrum_recap">Recap: Fourier transforms</a> - A good understanding of the Fourier transform and its variants is a necessary pre-requisite for spectral estimation. Here, a recap from previous courses is offered.
2. <a href="../statisticalsignalprocessing_spectrum_psd">Spectral distributions</a> - The spectrum of discrete-time energy and power signals can be calculated directly from the signal samples in time, or inderictely from the autocorrelation function.
3. <a href="../statisticalsignalprocessing_spectrum_window">Windowing</a> - All real-world signals are windowed in time, either implicitly or explicitly. Different types of windows have different trade-offs in terms of spectral resolution and spectral leakage.
