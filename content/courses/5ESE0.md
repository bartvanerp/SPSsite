+++
title = "5ESE0 - Signal processing basics"

# date = {{ .Date }}
lastmod = 2019-08-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.courses]
  name = "5ESE0 - Signal processing basics"
  weight = 10

+++

## Learning goals

This course will teach the most fundamental principles in signal processing. The main topics covered include:

Module 1 (Introduction) and 2 (Complex numbers and phasors): Basic properties of a sinusoidal signal, The relation between time- and phase-shift of a sinusoidal signal, The concept of complex exponentials and phasors, The Polar and Cartesian representation of a phasor, The phasor addition and multiplication rules, The rotating phasor interpretation, Both the Euler and Inverse Euler formulas, The interpretation of complex exponential signals.

Chapter 3 (Spectrum and Fourier series): The spectrum of a sum of sinusoids and its graphical interpretation, The result of multiplication and addition of sinusoidal signals and its relation with the concepts of beat notes and amplitude modulation, The concept of periodic and non-periodic waveforms, Derive the Fourier series expansion equations, both analysis and synthesis, The orthogonality property, The spectrum of the Fourier series, The Fourier analysis of a periodic signal, The concept of time-frequency spectrum, The concept of frequency modulation.

Chapter 4 (Sampling and Aliasing): The concept of sampling a continuous-time sinusoidal signal, The concept of discrete-time sinusoidal signal, The concept of normalized discrete-time frequency, The spectrum of a discrete-time signal, The sampling theorem, The ideal reconstruction of an analog signal from its discrete-time samples, The spectrum view interpretation of sampling and reconstruction, The concept and results of over-sampling, The concept and results of under-sampling, such as aliasing and folding of spectra, The concept of Discrete-to-Continuous conversion: Interpolation with Pulses, Zero order hold and Linear interpolation, The concept of ideal band-limited interpolation.

Chapter 5 (FIR Filters): The concept of a discrete-time system, The general Finite Impulse Response (FIR) filter, The concept of Impulse response of a filter, The concept of unit impulse or delta function, The concept of convolution, How to implement an FIR filter with basic building blocks like unit delays, multipliers and adders, The concept of Linear Time-Invariant (LTI) system, How to compute the convolution result of an LTI system, Basic properties of an LTI system, The result of cascading LTI systems.

Chapter 6 (Frequency Response of FIR Filters): The concept of frequency response of an FIR system, The concept of super position and the frequency response, The steady state and transition response, The relation of frequency response to impulse response and difference equation, Basic properties of the frequency response, The graphical representation of the frequency response, The result in the frequency domain of cascading LTI systems, The result of filtering sampled continuous-time signals in the discrete-time domain.


## Study material

The corresponding sections on this website are:

<ul>
  <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_main">Complex numbers and phasors</a> </li>
  <ul>  
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_numbersets">Number sets</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_euler">Euler equations</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_notation">Complex numbers</a> </li>
    <li>  <a href="../../disciplines/mathematicalbackground/mathematicalbackground_complex_phasors">Phasors</a>  </li>
  </ul>
  <li>  <a href="../../disciplines/continuous/continuoussignalprocessing_transforms_fs">Spectrum and Fourier series</a> </li>
  <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_main">Sampling and reconstruction</a> </li>
  <ul>  
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_samplingprocess">Sampling process of C-to-D converter</a> </li>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_frequency">Absolute and relative frequency</a> </li>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_uniqueness">Uniqueness issue</a> </li>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_reconstruction">Reconstruction of D-to-C converter</a>  </li>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_sampling_samplingtheorem">Sampling theorem</a>  </li>
  </ul>
  <li>  <a href="../../disciplines/discrete/discretesignalprocessing_signals_main">Discrete-time signals</a> </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_signals_basics">Elementary signals</a> </li>
  </ul>  
  <li>  <a href="../../disciplines/discrete/discretesignalprocessing_systems_main">Discrete-time systems</a> </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_systems_fir">Finite impulse response filters</a> </li>
  </ul>
  <li>  <a href="../../disciplines/discrete/discretesignalprocessing_analysis_main">Transform analysis of discrete-time systems</a> </li>
  <ul>
    <li>  <a href="../../disciplines/discrete/discretesignalprocessing_analysis_frequency">Frequency response of finite impulse response filters</a> </li>
  </ul>
</ul>
