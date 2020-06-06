+++
title = "Discrete-time systems"

# date = {{ .Date }}
lastmod = 2020-04-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Discrete-time systems"
  weight = 40

+++
## Introduction
This module introduces the concept of processing a discrete-time signal by a discrete-time system and the classification of such systems.

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/-iMgcYyi7gM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_systems_properties">System properties</a> - Systems can be characterized in multiple ways. These properties will be discussed in this section.
2. <a href="../discretesignalprocessing_systems_visualization">System visualization</a> - This section will introduce the basic building blocks of a discrete-time systems.
3. <a href="../discretesignalprocessing_systems_impulse">Impulse response</a> - A system can be characterized by its impulse response, which represents the output of the first when a short pulse is applied to its input.
4. <a href="../discretesignalprocessing_systems_convolution">Convolution</a> - The operation performed by the filter can be denoted mathematically using the convolution operation.
5. <a href="../discretesignalprocessing_systems_cascading">Cascading systems</a> - When a signal is passed through multiple systems, these signals may be combined, such that the signal is passing to another single filter.
6. <a href="../discretesignalprocessing_systems_special">Special convolutions</a> [⯈] - When dealing with real-time signals or when having limited memory, the convolution operation might not be ideal, therefore some special convolution operations are introduced that solve these problems.

<br></br>
## Summary

### Most important system properties
$$
x[n] \mapsto y[n] \text{ ; } x_1[n] \mapsto y_1[n] \text{ ; } x_2[n] \mapsto y_2[n]
$$

\begin{eqnarray*}
\color{blue}{\textit{Memoryless}} &:& \text{Output at $n=n_0$ depends only on input at $n=n_0$}\newline
\color{blue}{\textit{Causality}} &:& \text{Response at $n_0$ depends on input up to $n=n_0$}\newline
\color{blue}{\textit{Invertibility}} &:& \text{Input may be }\color{red}{\text{uniquely}}\text{ determined from output}\newline
\color{blue}{\textit{Additivity}} &:& x[n]=x_1[n]+x_2[n] \mapsto y[n]=y_1[n]+y_2[n]\newline
\color{blue}{\textit{Homogeneity}} &:& c \cdot x[n] \mapsto c \cdot y[n]\newline
\color{blue}{\textit{Impulse response}} &:& \text{Response to } \delta[n]  \hspace{2mm} \Rightarrow \delta[n] \mapsto h[n] \newline
\color{blue}{\textit{(BIBO) Stability}} &:& \text{For } A,B < \infty \text{,} \hspace{3mm} |x[n]| < A \hspace{2mm} \Rightarrow \hspace{2mm} |y[n]| < B \text{ } \overset{\color{red}{\text{LTI}}}{\Leftrightarrow} \text{ }
\sum_{n=-\infty}^{\infty} |h[n]| < \infty \newline
\color{blue}{\textit{Linearity}} &:& x[n]= \alpha x_1[n] + \beta x_2[n] \mapsto y[n] = \alpha y_1[n] + \beta y_2[n] \newline
\color{blue}{\textit{Time-Invariance}} &:& x[n-n_0 \mapsto y[n-n_0]\newline
\color{red}{\textit{LTI}} &:& \color{red}{\text{Linear Time-Invariance}}
\end{eqnarray*}

### Basic building blocks
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/basicbuildingblocks.svg"
      alt="Basic building blocks."
    />
  </figure>
</div>

### Realization scheme
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/flowdiagram.svg"
      alt="Flow diagram."
    />
  </figure>
</div>

### Difference Equation
$$
y[n] = \sum_{k=0}^{M-1} b_k x[n-k] + \sum_{k=1}^{N-1} a_k y[n-k]
$$

### Impulse response properties LTI
\begin{eqnarray*}
\textbf{BIBO stablility} & : & \sum_{n=-\infty}^{\infty} |h[n]| < \infty \newline
\textbf{Causalilty} & : & h[n]=0 \text{ for } n<0
\end{eqnarray*}

### Convolution sum
$$
y[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k]= x[n] \star h[n]
$$

<u><b>Convolution sum procedure:</b></u>
<ol>
  <li> Plot both input $x$ and impulse response $h$ as function of index $k$ </li>
  <li> Mirror (reverse) $h[k]$ $\Rightarrow$ $h[-k]$ </li>
  <li> For each new index $n$:
    <ol>
      <li> Shift mirrored $h[-k]$ to index $n$ $\Rightarrow$ $h[n-k]$. </li>
      <li> Output $y[n]$ is equal to the result of the sum of element by element multiplications of $x[k]$ and $h[n-k]$. </li>
    </ol>
  </li>
</ol>
<i>When the length of an input sequence of signal samples is $N$ and the length of the sequence of impulse response values is $M$, then the convolution sum procedure results in a sequence of length $N+M-1$ output signal samples $y[n]$.</i>

### Convolution sum properties
\begin{eqnarray*}
\text{Commutative} &:& h[n] \star x[n] = x[n] \star h[n] \newline
\text{Associative} &:& \\{ x[n] \ast h_1[n] \\} \ast h_2[n] = x[n] \ast \\{ h_1[n] \ast h_2[n] \\} \newline
\text{Distributive} &:& x[n] \ast h_1[n] + x[n] \ast h_2[n] = x[n] \ast \\{ h_1[n] + h_2[n] \\}
\end{eqnarray*}

### Cascade equivalence properties LTI system
<ul>
  <li> The cascading of two LTI systems, one with impulse response $h_1[n]$ and the other one with impulse response $h_2[n]$, can be combined to one LTI system with impulse response $h[n]=h_1[n] \star h_2[n]$. </li>
  <li> The order of two LTI systems, one with impulse response $h_1[n]$ and the other one with $h_2[n]$, can be interchanged. </li>
</ul>


<!--
### Special convolutions
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/overlapadd.svg"
      alt="Overlap-add procedure."
    />
  </figure>
</div>

<i>Notes overlap-add:</i>
<ol>
  <li> Based on complete convolution of non-overlapping blocks. </li>
  <li> Mainly used for fixed filters. </li>
</ol>

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/systems/overlapsave.svg"
      alt="Overlap-save procedure."
    />
  </figure>
</div>

<i> Notes overlap-save: </i>
<ol>
  <li> Based on partial convolution of overlapping blocks. </li>
  <li> Mainly used for adaptive filters. </li>
</ol>
-->
