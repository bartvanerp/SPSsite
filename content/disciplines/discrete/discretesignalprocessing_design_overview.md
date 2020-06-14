+++
title = "Overview filter design"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Overview filter design"
  weight = 1
  parent = "Filter design"
+++


## Four ideal frequency selective filters
Fig. 1 shows the magnitude responses of four basic types of ideal frequency selective filters:
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/filters4.svg"
      alt="Four ideal frequency selective filters."
    />
    <figcaption class="numbered">
      Four ideal frequency selective filters.
    </figcaption>
  </figure>
</div>
A Low Pass Filter (LPF),  a High Pass Filter (HPF), a Band Pass Filter and a Band Stop Filter. The purpose of these filters is to allow some frequencies to pass unaltered, while completely blocking other frequencies. The pass band refers to those frequencies that are passed, while the stop band contains those frequencies that are blocked.

We should note here that these ideal filters are not realizable because the impulse response corresponding to each of these ideal filters is noncausal and of infinite length.

<br></br>
## From LPF to HPF
High Pass, Band Pass and Band Stop filters are designed by starting with a Low Pass Filter, and then converting it into the desired response. For this reason, most discussions on filter design only give examples of Low Pass Filters. Roughly, there are two methods for the Low Pass Filter to High Pass Filter conversion: Spectral inversion and Spectral reversal. Both methods are equally useful.

### Spectral inversion
In general, with spectral inversion the frequency response is inverted or flipped, that is changing pass bands into stop bands, and vice versa.
In other words, spectral inversion changes a filter from low pass to high pass, from high pass to low pass, from band pass to band stop, or from band stop to band pass.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/spectralinversion.svg"
      alt="Principle of spectral inversion."
    />
    <figcaption class="numbered">
      Principle of spectral inversion.
    </figcaption>
  </figure>
</div>
The left hand side of Fig. 2 shows the principle of spectral inversion: The input signal $x[n]$ is applied to two systems in parallel. One of these systems is a Low Pass Filter, with an impulse response given by $h[n]$. The other system is an All Pass (AP) filter. In the ideal case this All Pass filter does nothing to the signal, and therefore it has an impulse response that is a delta function $\delta[n]$. The overall output $y[n]$ is equal to the output of the All Pass filter minus the output of the Low Pass Filter. Since the low frequency components are subtracted from the original signal, only the high frequency components appear in the output. Thus, a High Pass Filter is formed.

As show at the right hand side of Fig. 2 these two parallel filters with added outputs can be combined into a single filter by adding their impulse responses.

For this technique to work, the low-frequency components exiting the Low Pass Filter must have the same phase as the low-frequency components exiting the All Pass filter, otherwise a complete subtraction cannot take place. This places two restrictions on this method: First, the original filter must have left-right symmetry. That is the filter must have a linear phase. Second, the impulse must be added at the center of symmetry.

### Spectral reversal
The second method for LPF to HPF conversion is depicted in Fig. 3.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/spectralreversal.svg"
      alt="Principle of spectral reversal."
    />
    <figcaption class="numbered">
      Principle of spectral reversal.
    </figcaption>
  </figure>
</div>
This method uses the modulation property that a multiplication in time domain with a complex exponential function results in a shift in frequency domain. In other words, when changing the sign of every other sample of the impulse response $h[n]$, the frequency response shifts by $\pi$:
$$
e^{j\theta_0 n}h[n] \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ H(e^{j\theta-\theta_0})
\hspace{3mm} \Rightarrow \hspace{3mm} (-1)^n h[n] \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  H(e^{j\theta-\pi})
$$
Thus the HPF impulse response is formed by changing the sign of every other sample of the impulse response $h[n]$ of the LPF, as depicted at the right hand side of Fig. 3.


<br></br>
## From LPF and HPF to Band Pass and Band Stop Filters
Fig. 4 shows how Low Pass and High Pass Filters can
be combined to form Band Stop filter.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/BandStop.svg"
      alt="Band Stop filter from LPF and HPF."
    />
    <figcaption class="numbered">
      Band Stop filter from LPF and HPF.
    </figcaption>
  </figure>
</div>
These parallel filters can be combined to one filter as depicted at the right hand side of the figure.

A Band Pass filter can be designed  by cascading a Low Pass Filter and a High Pass Filter, as depicted in Fig. 5.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/BandPass.svg"
      alt="Band Pass filter from LPF and HPF."
    />
    <figcaption class="numbered">
      Band Pass filter from LPF and HPF.
    </figcaption>
  </figure>
</div>
These parallel filters can be combined to one filter as depicted at the right hand side of the figure.

<br></br>
## Filter design process
As discussed before, we restrict our attention in this reader to the design of the magnitude response of a Low Pass filter. The design process of a digital filter involves the following stapes:
<ol>
  <li>Before a filter can be designed, a set of filter specifications must be defined. Because the ideal LPF is unrealizable, it is necessary to relax the ideal constraints on the magnitude response and allow some deviation from the ideal response. Fig. 6 shows the general design specifications of magnitude response.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/filterspec.svg"
      alt="General design specifications of magnitude response."
    />
    <figcaption class="numbered">
      General design specifications of magnitude response.
    </figcaption>
  </figure>
</div>
The pass band, with pass-band cutoff frequency $\theta_p$, refers to those frequencies that are passed while the stop band, with stop-band cutoff frequency $\theta_s$, contains those frequencies that are blocked. The transition band is between $\theta_p$ and $\theta_s$. The cutoff frequency $\theta_c$ is usually in the middle of this transition band. The pass-band deviation is denoted as $\pm \delta_p$, and the stop-band deviation as $\delta_s$. </li>
<li> The second step is the selection of the filter type, i.e. whether an FIR or an IIR filter is to be employed and the filter order. </li>
<li> Once the specifications have been defined the next step is to find a set of filter coefficients that produce an acceptable filter. </li>
<li> After the filter has been designed to implement the system in hardware or software, an appropriate filter structure is chosen ans if necessary the filter coefficients are quantized. </li>
<li> As a final step check the resulting filter and eventually repeat the previous 3 steps. </li>
</ol>

<br></br>
## Comparison FIR and IIR filters
Choosing between FIR and IIR is critical since it determines the characteristics of the filter and the available design methods.
The most important characteristics of FIR and IIR filters are:
<ul>
<li> An FIR filter has only zeros, while an IIR filter can have both poles and zeros. </li>
<li> Exact linear phase can be realized with an FIR filter and not with an IIR filter while an all-pass filter can be realized with IIR and not with FIR, except for a filter which consists of delays. </li>
<li> An FIR filter is always stable. An IIR filter is unstable when there are poles outside the unit circle. </li>
<li> The most important FIR filter is the transversal structure, or tapped delay line. The IIR has recursive parts and in most cases it is build as a cascaded or parallel set of first and second order sections. </li>
<li> The complexity of an FIR filter is, in most cases, directly related to the filter length. To make highly selective filters cost usually less complexity when using IIR filters. </li>
<li> The initial state influences the behavior of an FIR maximal up to the filter length. Because of the recursion of an IIR filter this can take in theory an infinite long time. </li>
<li> The influence of quantization is limited for FIR filters, while poles can move outside the unit circle, which leads to instability. Moreover for IIR filters quantization can lead to limit cycles and overflow oscillations. </li>
<li> Design methods are available for all kind of FIR frequency responses, while design methods for IIR frequency response are mainly available for LPF, HPF, Band Pass and Band Stop filters. </li>
<li> The FIR available design aids are mainly iterative methods, while the IIR methods mainly consist of the transformation of available analog filters to the digital domain. </li>
</ul>
