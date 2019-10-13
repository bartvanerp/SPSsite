+++
title = "Discrete-time signal processing basics"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Overview"
  weight = 10

+++



The signal processing field deals with the analysis and manipulation of signals.
Signals that are observed in everyday life are continuous-time signals, which are not yet converted to the digital domain.
Understanding the basics that are related to the signal and system behavior in the continuous-time domain allows for a better understanding on how to process these signals in the digital domain. This module therefore covers the basics of signals and systems in the continuous-time domain.

The concepts covered in this module are:

1. <a href="../discretesignalprocessing_sampling_main">Sampling and reconstruction</a> - Continuous-time signals are impractical to work with on computers. Therefore the conversion to the discrete-time domain is required in order to perform calculations on them. The conversion between the continuous- and discrete-time domain can have implications for the reconstructed signal.

2. <a href="../discretesignalprocessing_signals_main">Discrete-time signals</a> (in progress) - There exist infinitely many signals. These signals can be characterized by certain properties that tell us something about the signal. Within the set of all possible signals, some elementary signals are used very often due to their simplicity and their descriptive power.

3. <a href="../discretesignalprocessing_systems_main">Discrete-time systems</a> (in progress) - When a discrete-time signal passes through a system it is interesting to know what the expected output signal will be. In order to make these predictions, it is desired to characterize a system and determine its properties.

4. <a href="../discretesignalprocessing_transforms_main">Discrete-time transforms</a> (in progress) - Discrete-time signals are usually represented in the time-domain. However, for many applications it is usually more convenient to transform this signal first to another domain, such as the frequency domain, in order to perform calculations.

5. <a href="../discretesignalprocessing_analysis_main">Transform analysis of discrete-time systems</a> (in progress) - Similarly to discrete-time signals, also systems can be characterized in different domains. Usually this allows for better insight in the system and simplified calculations.

6. **Special filter structures** (to be added) - Some filter structures behave in a very distinct way. Because of their characteristics and consequences it is worth discussing them.

7. **Multirate signal processing** (to be added) - The sample rate of a signal is a fixed characteristic of the measurement device. Sometimes it is desired to reduce or increase this rate after the measurement itself. This will lead to certain consequences.

8. **Additional topics** (to be added) - Besides the abovementioned topics, many more concepts exist that are relevant for discrete-time signal processing. These topics include: filter design techniques, finite word length effects and spectral estimation techniques.
