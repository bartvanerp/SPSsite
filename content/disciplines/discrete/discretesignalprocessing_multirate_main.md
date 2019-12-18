+++
title = "Sampling, reconstruction and multirate signal processing"

# date = {{ .Date }}
lastmod = 2019-12-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling, reconstruction and multirate signal processing"
  weight = 80


+++

Discrete-time signals are often processed in the discrete time domain. However, many more of these domains exist, which offer more insight in the signals. One of the most famous domains is the frequency domain, where the signal is expressed in terms of its frequency components. As an example, high-pitched sounds have a strong frequency content in the high frequency range, whereas low bass tones populate the lower frequency range. This modules covers several continuous-time transforms, where the time domain signal is mapped to another domain.

The concepts covered in this module are:

1. <a href="../discretesignalprocessing_multirate_math">Mathematical description sampling process</a> (in progress) - In order to obtain full understanding of the theory

2. <a href="../discretesignalprocessing_multirate_blocks>Basic building blocks of multirate signal processing</a> (in progress) - The conversion of a sample frequency can give rise to several undesired artifacts. The correct filtering of the signal is therefore of crucial importance.

3. <a href="../discretesignalprocessing_multirate_tool">The DFT modulated Filterbank</a> (to be added)
