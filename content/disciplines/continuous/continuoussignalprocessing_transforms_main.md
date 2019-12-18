+++
title = "Continuous-time transforms"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Continuous-time transforms"
  weight = 40

+++

Continuous-time signals are often processed in the time domain. However, many more of these domains exist, which offer more insight in the signals. One of the most famous domains is the frequency domain, where the signal is expressed in terms of its frequency components. As an example, high-pitched sounds have a strong frequency content in the high frequency range, whereas low bass tones populate the lower frequency range. This modules covers several continuous-time transforms, where the time domain signal is mapped to another domain.

The concepts covered in this module are:

1. <a href="../continuoussignalprocessing_transforms_spectrum">Spectrum of sinusoidal signals</a> - A time-domain signal can be converted to the frequency domain. The frequency representation of a signal is called its frequency spectrum.

2. <a href="../continuoussignalprocessing_transforms_fourier">Fourier Series (FS)</a> - The frequency spectrum of periodic signals can be represented as the sum of harmonically related sinusoidal signals.

3. <a href="../continuoussignalprocessing_transforms_ftc">Fourier Transform of Continuous-time signals (FTC)</a> - The transformation from the time-domain to the frequency domain and vice versa. The Fourier Transform of Continuous-time signals is a frequency analysis tool for continuous-time signals.

4. **Laplace transform** (to be added) - Whereas the Fourier transform is a complex function of the *it* real frequency. The Laplace transformation calculates a complex function of a *complex* variable.
