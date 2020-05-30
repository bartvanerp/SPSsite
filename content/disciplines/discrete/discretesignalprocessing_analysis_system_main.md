+++
title = "System function"

# date = {{ .Date }}
lastmod = 2020-05-09

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Analysis III: System function"
  weight = 63

+++

## Introduction
The system function $H(z)$ of an LTI system is defined as the $Z$-transform of the impulse response $h[n]$:
\begin{eqnarray}
h[n] & \overset{\color{red}{\bf ZT}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} &
H(z) = \sum_{n=-\infty}^{\infty} h[n] z^{-n}
\end{eqnarray}
The system function is very useful in the description and analysis of LTI systems. In this reader we will show how the system function can be derived from the signal flow graph in a very simple way, which also leads to an alternative simplified way to find the frequency response of such an LTI system. From this system function description it follows that the system function of a rational LTI system writes as a rational polynomial function from which both numerator and denominator polynomials can be split as a product of first order terms.
These first order terms define the poles and zeros of the system. We will see how stability and causality can be related to the poles and zeros of the system function. Finally we will discuss how the frequency response can be derived from the pole-zero plot of the system function.


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/kW52xCOTj70" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_analysis_system_lti">System function rational LTI</a> - Here the system function of a rational LTI system will be determined.
2. <a href="../discretesignalprocessing_analysis_system_stability">Stability and causality</a> - From the system function the system stability of the system can be determined. This is shown in this section.
3. <a href="../discretesignalprocessing_analysis_system_pz">Poles and zeros</a> - In this section the poles and zeros of the system function are determined.
4. <a href="../discretesignalprocessing_analysis_system_frequency">Frequency response from system function</a> - Here an alternative simplified way to find the frequency response of such an LTI system is discussed.

<br></br>
## Summary
\begin{eqnarray*}
\textbf{Systemfunction: }
h[n] & \overset{\color{red}{\bf ZT}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} &
H(z) = \sum_{n=-\infty}^{\infty} h[n] z^{-n}
\end{eqnarray*}

### System function rational LTI
\begin{eqnarray*}
Y(z) &=& \sum_{k=0}^{M-1} b_k z^{-k} X(z) + \sum_{k=1}^{N-1} a_k z^{-k} Y(z)\newline
\Rightarrow \mbox{ }
H(z) &=& \frac{ Y(z)}{X(z)} =
\frac{\sum_{k=0}^{M-1}b_k z^{-k}}{1 - \sum_{k=1}^{N-1}a_k z^{-k}} = b_0 \frac{\prod_{k=1}^{M} (1 - \color{blue}{\beta_k} z^{-1})}{\prod_{k=1}^{N} (1 - \color{magenta}{\alpha_k} z^{-1})}
\end{eqnarray*}
Alternative for frequency response:
$$
H(z) = \frac{Y(z)}{X(z)}
\text{ } \Rightarrow \text{ } H(e^{j\theta}) = H(z)|\_{z = e^{j\theta}}
$$

### Realizability: Stability and causality
$$
\boxed{\color{red}{\text{All poles must lie inside (or on) unit circle}}}
$$

### Frequency response from PZ-plot
\begin{eqnarray*}
|H(e^{j\theta})| &=&|b_0| \times
\left ( \prod_{k=1}^{M} \text{length}(e^{j\theta} - \color{blue}{\beta_k}) \right ) {\bf /} \left ( \prod_{k=1}^{N} \text{length}(e^{j\theta} - \color{magenta}{\alpha_k} ) \right )\newline
\varphi(e^{j\theta}) &=&(N-M) \cdot \theta + \sum_{k=1}^M \text{arg} (e^{j\theta} - \color{blue}{\beta_k}) -
\sum_{k=1}^N \text{arg} (e^{j\theta} - \color{magenta}{\alpha_k})
\end{eqnarray*}
