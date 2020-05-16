+++
title = "Frequency response LTI systems"

# date = {{ .Date }}
lastmod = 2020-05-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Analysis II: Frequency response LTI"
  weight = 62

+++

## Introduction
Filters are vital for proper signal processing. They can be used for a variety of different purposes. These purposes include, but are definitely not limited to, the removal of disturbing frequency components in biomedical recordings, speech denoising in audio processing algorithms, stock predictions and even for signal modelling in the field of parametric spectral estimation.

Because of the many applications for discrete-time systems, it is of vital importance that a thorough understanding of the filter is obtained. This module will start by describing the basic concept of Linear Time-Invariant (LTI) systems, by describing their system architecture and by describing how they process an incoming signal. After a general understanding of LTI systems has been established, this module will investigate how sinusoidal signals with different frequencies are affected by the filter. This frequency dependence will be described by the frequency response of the filter. Next up, the situation will be discussed in which multiple filters are interconnected, by cascading the filters or by placing the filters in parallel, and finally some special cases are discussed, which are commonly used in practice.

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/Oqmj3fHpsYQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module covers the following topics:

1. <a href="../discretesignalprocessing_analysis_lti_lti">LTI systems</a> - This section contains a selection of the material from the module on <a href="../discretesignalprocessing_systems_main">discrete-time systems</a>. This section will describe the general form of the LTI system and will describe 2 ways of characterizing such a system, but first the meaning of an linear time-invariant system will be briefly recapped.
2. <a href="../discretesignalprocessing_analysis_lti_freq">Frequency response LTI</a> - This section will derive the frequency response of an LTI system.
3. <a href="../discretesignalprocessing_analysis_lti_interconnect">Interconnecting systems</a> - In this section we will explore how systems will react when multiple systems are interconnected. Here we can distinguish two elementary situations, through which most situations can be explained. These two situations include two systems that are cascaded and two systems that are parallel to each other.
4. <a href="../discretesignalprocessing_analysis_lti_special">Special cases</a> - This section will discuss two special cases which commonly occur in real-time applications. These special cases include an averaging filter and a low-pass filter.

<br></br>
## Summary

### LTI systems
LTI systems are Linear-Time-Invariant. The difference equation of such systems is given as
\begin{equation}\label{eq:DE}
    y[n] = \underbrace{\sum_{k=0}^{M-1} b_k x[n-k]}_\text{moving-average}  + \underbrace{\sum_{k=1}^{N-1} a_k y[n-k]}_\text{auto-regressive},
\end{equation}

### Frequency response
The frequency response of an LTI system can be found as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = \frac{Y(\mathrm{e}^{j\theta})}{X(\mathrm{e}^{j\theta})} = \frac{\sum_{k=0}^{M-1}b_k  \mathrm{e}^{-jk\theta}}{1-\sum_{k=1}^{N-1}a_k\mathrm{e}^{-jk\theta}} = \frac{B(\mathrm{e}^{j\theta})}{A(\mathrm{e}^{j\theta})}.
\end{equation}

### Interconnecting systems
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When cascading two different LTI systems, one with frequency response $H_1(e^{j\theta})$ and the other with frequency response $H_2(e^{j\theta})$, we may combine these two systems into one LTI system of which the frequency response is given by the product of the individual frequency responses: $H(e^{j\theta})= H_1(e^{j\theta}) \cdot H_2(e^{j\theta})$.
</i></div>

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>When placing two different LTI systems in parallel, one with frequency response $H_1(e^{j\theta})$ and the other with frequency response $H_2(e^{j\theta})$, we may combine these two systems to one LTI system of which the frequency response is given by the sum of the individual frequency responses: $H(e^{j\theta})= H_1(e^{j\theta}) + H_2(e^{j\theta})$.
</i></div>

### Special cases
The difference equation of an $N$-point averaging filter is defined as
\begin{equation}
    y[n] = \sum_{k=0}^{N-1} b_k x[n-k] = \sum_{k=0}^{N-1} x[n-k].
\end{equation}
and its frequency response can be determined as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = \frac{\sin\left(\frac{N}{2}\theta\right)}{\sin\left(\frac{1}{2}\theta\right)} \mathrm{e}^{-j\left(\frac{N-1}{2}\right)\theta}.
\end{equation}

The frequency response of an ideal low-pass filter is given as
\begin{equation}
    H(e^{j\theta}) =
    \begin{cases}
        1, & \text{for } \vert \theta \vert \leq \theta_c, \newline
        0, & \text{otherwise},
    \end{cases}
\end{equation}
and the corresponding impulse response can be found as
\begin{equation}
    h[n] = \frac{\theta_c}{\pi}\left( \frac{\sin(\theta_c n)}{\theta_c n} \right).
\end{equation}
This representation is, however, not feasible to implement in practice and therefore some adjustments need to be made, deviating from the ideal frequency response of the low-pass filter.
