+++
title = "Finite word length effects"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Finite word length effects"
  weight = 100

+++

## Introduction
In implementing a discrete-time system in hardware or software, it is important to consider the finite word length effects.

For example, if a filter is to be implemented on a fixed point processor, both the signal samples and the filter coefficients must be quantized to a finite number of bits. This quantization introduces round-off noise and quantized filter coefficients will change the frequency response characteristics of the filter.

In this reader we first present the most common binary representations, quantization- and overflow- methods.
Then we analyze round-off noise. Finally we discuss how finite word length effects could influence filter coefficients and we show how this influences the filter characteristics and its sensitivity.

### A/D conversion
First let's take a closer look where finite word length effects play a role when converting an analog, or continuous time signal $x_a(t)$ to the digital domain. For this we refer to Fig. 1.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/ADconv.svg"
      alt="Finite word length effects in A/D conversion."
    />
    <figcaption class="numbered">
      Finite word length effects in A/D conversion.
    </figcaption>
  </figure>
</div>
Up to now we assumed an ideal C-to-D for this conversion, in which the resulting discrete-time samples $x[n]$ have infinite precision. These infinite precision samples are quantized with quantization step $q$ which results in a quantization error which is in the range $\pm \frac{q}{2}$. To overcome overflow, the quantization is limited up to a maximum and finally each quantized sample is encoded into $B$ bits.

In the following sections we will first discuss some binary representations, some quantization- and overflow- methods.
Then we will analyse round-off noise. Finally we will discuss how finite word length effects can influence filter coefficients and we will show how this influences the filter characteristics and its sensitivity.


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/zaPk3s25G3E" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_wordlength_binary">Binary representation of numbers</a> - As a start we will discuss the origin of the quantization errors, caused by the inevitable conversion of samples into bits.
2. <a href="../discretesignalprocessing_wordlength_quantization">Quantization and overflow</a> - Here we will discuss how sample values are processed into bits, taking into account the non-linear quantization and overflow characteristics.
3. <a href="../discretesignalprocessing_wordlength_roundoff">Analysis of round-off noise</a> - The consequences of the signal quantization will be discussed in this section.
4. <a href="../discretesignalprocessing_wordlength_coefs">Quantization of filter coefficients</a> - Filter coefficients also need to be quantized to allow for implementation in a digital systems. This quantization has an effect at the frequency response of the filter.
5. <a href="../discretesignalprocessing_wordlength_filter">Influence filter structure</a> - Finally, different filter structures are discussed with regards to the quantization of filter coefficients and the corresponding effects on the frequency response.

<br></br>

## Summary

### Binary representation of numbers

#### Fixed point representation
<ul>
  <li> <i> Sign Magnitude (SM): </i> $\color{red}{(-1)^{b_0}} \sum_{i=1}^{B-1} b_i 2^{B-1-i}$ </li>
  <li> <i> One's complement (1C): </i> Negative = $\overline{\mbox{positive}}$ </li>
  <li> <i> Two's complement (2C): </i> Negative = $\overline{\mbox{positive}} + 1$ </li>
</ul>

#### Floating point representation
$x=M \cdot 2^{E}$ with mantissa $M$ ($\frac{1}{2} \leq |M| < 1$) and exponent $E$, positive or negative integer.


### Quantization and overflow
<ul>
  <li> Three common quantization characteristics: Rounding, Value truncation and  Magnitude truncation. </li>
  <li> Three common overflow characteristics: Saturation,  Nulling and  Sawtooth overflow. </li>
</ul>

### Analysis of Round-off noise
$$
\frac{P_x}{P_e} = \frac{3}{16} 2^{2B} \hspace{2mm} \rightarrow \hspace{2mm}
10 \cdot ^{10}\text{log} \left ( \frac{P_x}{P_e} \right ) \hat{=}  \color{red}{6  B} \text{[dB]}
$$

#### Influence filtering of round-off noise
$$
\frac{P_x}{P_e} \neq \frac{P_v}{P_g} \hspace{3mm} \Leftrightarrow
\text{ SNR$_{in}$ $\neq$ SNR$_{out}$}
$$

#### Pairing and ordering
<ul>
  <li> Pair pole/zero couple which is closest to unit circle. </li>
  <li> Order according to closeness poles to unit circle. Increasing or decreasing ordering depends a.o. on shape output noise. </li>
</ul>

### Quantization of filter coefficients
<ul>
  <li> Does not introduce non-linearity effects. </li>
  <li> Will influence the filter characteristics. </li>
</ul>

### Influence filter structure
The accuracy with which the filter coefficients can be specified depends upon the word length of the processor, and the sensitivity of the filter to coefficient quantization depends on the structure of the filter, as well as on the locations of the poles and zeros.
