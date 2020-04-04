+++
title = "Discrete-time signal processing basics"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time signal processing basics: overview"
  weight = 10

+++


The signal processing field deals with the analysis and manipulation of signals.
Signals that are observed in everyday life are continuous-time signals, which are not yet converted to the digital domain.
Understanding the basics that are related to the signal and system behavior in the continuous-time domain allows for a better understanding on how to process these signals in the digital domain. This module therefore covers the basics of signals and systems in the continuous-time domain.

The concepts covered in this discipline are:

1. <a href="../discretesignalprocessing_sampling_main">Basics of sampling and reconstruction</a> - Continuous-time signals are impractical to work with on computers. Therefore the conversion to the discrete-time domain is required in order to perform calculations on them. The conversion between the continuous- and discrete-time domain can have implications for the reconstructed signal.

2. <a href="../discretesignalprocessing_signals_main">Discrete-time signals</a> - There exist infinitely many signals. These signals can be characterized by certain properties that tell us something about the signal. Within the set of all possible signals, some elementary signals are used very often due to their simplicity and their descriptive power.

3. **Discrete-time systems** - When a discrete-time signal passes through a system it is interesting to know what the expected output signal will be. In order to make these predictions, it is desired to characterize a system and determine its properties.

4. **Discrete-time transforms** - Discrete-time signals are usually represented in the time-domain. However, for many applications it is usually more convenient to transform this signal first to another domain, such as the frequency domain, in order to perform calculations.
    - <a href="../discretesignalprocessing_transforms_ftd_main">Transforms I: Fourier transform for discrete-time signals (FTD)</a>
    - <a href="../discretesignalprocessing_transforms_dft_main">Transforms II: Discrete Fourier transform (DFT)</a>
    - <a href="../discretesignalprocessing_transforms_ztransform_main">Transforms IV: Z-transform</a>
<br></br>

5. **Transform analysis of discrete-time systems** - Similarly to discrete-time signals, also systems can be characterized in different domains. Usually this allows for better insight in the system and simplified calculations.
    - <a href="../discretesignalprocessing_analysis_fir_main">Analysis I: Frequency response FIR</a>
    - <a href="../discretesignalprocessing_analysis_lti_main">Analysis II: Frequency response LTI</a>
<br></br>

6. <a href="../discretesignalprocessing_multirate_main">Sampling, reconstruction and multirate signal processing</a> - The sample rate of a signal is a fixed characteristic of the measurement device. Sometimes it is desired to reduce or increase this rate after the measurement itself. This will lead to certain consequences.

7. **Filter structures** - Some filter structures behave in a very distinct way. Because of their characteristics and consequences it is worth discussing them.
    - <a href="../discretesignalprocessing_filters_fir_main">Filter stuctures I: Finite impulse response (FIR) filters</a>
<br></br>

8. **Filter design** (to be added) - The analysis of a filter gives insight into the operations of a filter. However, it is also important to use this knowledge in order to design a filter.

9. **Finite wordlength effects** (to be added) - Sampling signals is the process of converting a continuous-time signal into bits. More available bits allow for a higher resolution in the signal. This also means that there is an inevitable quantization error, which has an effect on the signal.
