+++
title = "Discrete-time signals"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time signals"
  weight = 30

+++
## Introduction
### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/ijIeC5lSPRA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module will cover some very basic characteristics and examples of signals in the discrete-time domain.

1. <a href="../discretesignalprocessing_signals_sampling">Sampling process</a> - In the discrete domain the signals are represented as sequences of numbers called samples.
2. <a href="../discretesignalprocessing_signals_elementary">Elementary signals</a> - All discrete-time signals can be written as a set of elementary signals, therefore a good understanding of these elementary signals helps with the analysis of more complex signals.
3. <a href="../discretesignalprocessing_signals_duration">Signal duration</a> - Discrete-time signals may be conveniently classified in terms of their duration or extent.
4. <a href="../discretesignalprocessing_signals_periodicity">Periodicity</a> - A discrete-time signal may always be classified as either periodic or aperiodic, which refers to whether the signal repeats itself.
5. <a href="../discretesignalprocessing_signals_symmetry">Symmetry</a> - A discrete-time signal will often possess some form of symmetry that may be exploited in solving problems.
6. <a href="../discretesignalprocessing_signals_manipulations">Signal manipulations</a> - Signal manipulations are generally decomposed of a few basic transformations.

<br></br>
## Summary

### Elementary signals
<table style="width:100%">
  <tr>
    <th> Name </th>
    <th> Description </th>
    <th> Remark </th>
  </tr>
  <tr>
    <td> Delta pulse </td>
    <td> $$ \delta[n] = \begin{cases} 1 & \text{for } n=0 \newline 0 & \text{otherwise} \end{cases} $$ </td>
    <td> $$ u[n] - u[n-1] $$ </td>
  </tr>
  <tr>
    <td> Unit step </td>
    <td> $$ u[n] = \begin{cases} 1 & \text{for } n\geq 0 \newline 0 & \text{otherwise} \end{cases} $$ </td>
    <td> $$ \sum_{k=0}^\infty \delta[n-k] $$ </td>
  </tr>
  <tr>
    <td> Exponential decaying </td>
    <td> $$ a^n \cdot u[n] $$ </td>
    <td> $ a $ real or complex with $ |a| < 1 $ </td>
  </tr>
  <tr>
    <td> Complex </td>
    <td> $$ e^{jn\omega_0} $$ </td>
    <td> $$ \cos(n\omega_0) + j\sin(n\omega_0)$$ </td>
  </tr>
</table>

### Signal duration
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/signalduration.svg"
      alt="Examples of finite and infinite length signals."
    />
    <figcaption>
      Examples of finite and infinite length signals.
    </figcaption>
  </figure>
</div>

### Signal properties
\begin{eqnarray*}
\textit{Periodic} &:& x[n]=x[n+N] \newline
\textit{Even } \color{blue}{\textit{Conjugate-symmetric}} &:& x[n]=x[-n] \hspace{3mm} \color{blue}{x[n]=x^\ast[-n]}\newline
\textit{Odd } \color{blue}{\textit{Conjugate-antisymmetric}} &:& x[n]=-x[-n] \hspace{3mm} \color{blue}{x[n]=-x^\ast[-n]} \newline
\textit{General: } \hspace{3mm} x[n]&=&x_e[n]+x_o[n] \newline
\text{with } \hspace{3mm} x_e[n]&=&\frac{1}{2} \left ( x[n] + x[-n] \right ) \newline
\text{and } \hspace{3mm} x_o[n]&=&\frac{1}{2} \left ( x[n] - x[-n] \right )
\end{eqnarray*}

### Signal manipulations
Amplitude transformations:
\begin{eqnarray*}
\color{blue}{\textit{Addition}} &:& y[n]=x_1[n]+x_2[n] \newline
\color{blue}{\textit{Multiplication}} &:& y[n]=x_1[n] \cdot x_2[n] \newline
\color{blue}{\textit{Scaling}} &:& y[n] = c \cdot x[n]
\end{eqnarray*}

Transformation of independent variable $n$:

\begin{eqnarray*}
\textit{Time shifting (delay or advance)} &:& f[n]=n-n_0 \newline
\textit{Time reversal} &:& f[n]=-n \newline
\textit{Time scaling = Down- or Up- sampling} &:& f[n]=M \cdot n \text{ or } f[n]=n/M
\end{eqnarray*}
<i>Note:</i> Shifting, reversal, and time scaling operations are order dependent.
