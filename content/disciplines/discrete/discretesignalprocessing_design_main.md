+++
title = "Filter design"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Filter design"
  weight = 110

+++

## Introduction
In this reader we will provide some general background material of filter design techniques. In some applications the impulse response or unit step response may be specified, however, in most applications either the magnitude and/or the phase response has to be specified for the design of a digital filter.
Since the phase response of a designed filter can be corrected by cascading it with an all-pass section, in most cases the problem of interest is the development of a realizable approximation to a given magnitude response specification. For this reason we restrict our attention in this reader to the approximation of the magnitude response only.

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/3Z0r2vQuhJM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_design_overview">Overview filter design</a> - This module starts off by describing the most basic filter structures.
2. <a href="../discretesignalprocessing_design_fir">FIR filter design</a> - In this section a design procedure is outlined for finite impulse response filters.
3. <a href="../discretesignalprocessing_design_iir">IIR filter design</a> - Finally, the design procedure is extended to the topic of infinite impulse response filters.


<br></br>
## Summary


### Overview filter design
#### Four ideal frequency selective filters
<ul>
  <li> Low-pass filter </li>
  <li> High-pass filter </li>
  <li> Band-pass filter </li>
  <li> Band-stop filter </li>
</ul>

#### Methods to obtain High Pass filter via Low Pass Filter
<ul>
  <li> Spectral inversion </li>
  <li> Spectral reversal </li>
</ul>

#### From LPF and HPF to Band Stop
Subtract Low Pass Filter from All Pass filter

#### From LPF and HPF to Band Pass
Cascade Low Pass Filter and High Pass Filter

### Filter design process
<ol>
  <li> Filter specifications, </li>
  <li> Selection type (FIR or IIR) and filter order, </li>
  <li> Find set of filter coefficients, </li>
  <li> Implement filter in hard- or soft-ware, </li>
  <li> Check result and eventually repeat previous 3 steps. </li>
</ol>


#### Comparison FIR and IIR filters
<ul>
  <li> FIR has only zeros.  IIR filter can have both poles and zeros. </li>
  <li> Exact linear phase only with an FIR filter. All Pass only with  IIR. </li>
  <li> FIR always stable. IIR unstable when poles outside the unit circle. </li>
  <li> FIR filter has mainly transversal structure, or tapped delay line. IIR has recursive parts and in most cases build as cascaded or parallel set of first and second order sections. </li>
  <li> Complexity of FIR filter directly related to the filter length. To make highly selective filters cost usually less complexity when using IIR filters. </li>
  <li> Initial state influences behavior FIR maximal up to the filter length. Because of recursion of IIR filter this can take an infinite long time. </li>
  <li> Influence of quantization is limited for FIR filters, while poles can move outside the unit circle, which leads to instability. Moreover IIR filter quantization can lead to limit cycles and overflow oscillations. </li>
  <li> Design methods available for all kind of FIR frequency responses, while for IIR frequency response mainly available for LPF, HPF, Band Pass and Band Stop filters. </li>
  <li> FIR available design aids mainly iterative methods. IIR methods mainly consist of transformation of available analog filters to digital domain. </li>
</ul>


### Design procedures for Linear-phase FIR filters
<ul>
  <li> Design based on FTD and windowing </li>
  <li> Equiripple linear phase filter design </li>
  <li> Design based on Frequency sampling filter </li>
</ul>

### IIR filter design methods
<ul>
  <li> The impulse invariance approach </li>
  <li> Mapping differential- into difference-equation </li>
  <li> The bilinear transform </li>
</ul>
