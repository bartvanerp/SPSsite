+++
title = "Discrete-time transforms"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time transforms"
  weight = 50


+++

Discrete-time signals are often processed in the discrete time domain. However, many more of these domains exist, which offer more insight in the signals. One of the most famous domains is the frequency domain, where the signal is expressed in terms of its frequency components. As an example, high-pitched sounds have a strong frequency content in the high frequency range, whereas low bass tones populate the lower frequency range. This modules covers several continuous-time transforms, where the time domain signal is mapped to another domain.

The concepts covered in this module are:

1. <a href="../discretesignalprocessing_transforms_ftd">Fourier Transform for Discrete-time signals (FTD)</a> - The spectral representation of a discrete-time signal can be calculated with the Fourier Transform for Discrete-time signals.

2. <a href="../discretesignalprocessing_transforms_dft">Discrete Fourier Transform (DFT)</a> - The Fourier transform for discrete-time signals provides a continuous frequency spectrum, which cannot be saved in discrete bits. The discrete Fourier transform provides a sampled frequency spectrum.

3. **Fast Fourier Transform (FFT)** (to be added) - The DFT operation can be sped up significantly. This faster implementation is called the fast Fourier transform.

4. **Z-Transform** (to be added) - The Z-transform provides us with insight straight from the difference equation of the signal.

5. **Relation between different transforms** (to be added) - In order to fully grasp all the differences and similarities between the many different transforms, a good understanding of the relationships between them is crucial.
