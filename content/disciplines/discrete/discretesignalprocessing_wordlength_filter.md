+++
title = "Influence filter structure"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Influence filter structure"
  weight = 5
  parent ="Finite word length effects"

+++



In order to implement a filter on a digital processor, the filter coefficients must be converted with finite word length precision. This conversion leads to movements in the pole and zero locations and a change in the frequency response of the filter. To get any sense of quantization on the location of poles and zeros we consider the second order recursive IIR filter with two coefficients $a_1$ and $a_2$, as depicted in Fig. 1.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/example9.svg"
      alt="Second order recursive IIR filter with two coefficients $a_1$ and $a_2$."
    />
    <figcaption class="numbered">
      Second order recursive IIR filter with two coefficients $a_1$ and $a_2$.
    </figcaption>
  </figure>
</div>
When choosing the coefficients $a_1$ and $a_2$ as follows:
$$
a_1=2r \cos(\theta_0) \hspace{2mm} \mbox{ and } \hspace{2mm}  a_2 = -r^2
$$
the filter has two complex conjugated poles that are located at $z=r \mbox{e}^{\pm j \theta_0}$ and the system function can be written as follows:
\begin{eqnarray*}
H(z)&=& \frac{1}{1-a_1 z^{-1}-a_2 z^{-2}}
=\frac{1}{(1-r e^{j\theta_0} z^{-1}) \cdot (1-r e^{-j\theta_0} z^{-1})} \end{eqnarray*}
In case of infinite precision, by properly selecting the two parameters $a_1$ and $a_2$, we can realize any desired pair of complex conjugated poles. After quantization of $a_1$ and $a_2$, however, only a limited number of pole pairs can be realized, because $a_1$ and $a_2$, and therefore also $r$ and $\theta_0$, can only take a finite number of different values.  Fig. 2 shows an example of which poles can be realized within the unit circle in case the coefficients $a_1$ and $a_2$ are
decimal fractions that are quantized to 4 bits with 1 bit for the sign.
<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/example9sensitivity.svg"
      alt="Set of allowable pole positions (only at the crossings of the black lines and red circles) of second order IIR filter of Fig.\ref{Fig:example9} with coefficients that are quantized to 4 bits with 1 bit for the sign."
    />
    <figcaption class="numbered">
      Set of allowable pole positions (only at the crossings of the black lines and red circles) of second order IIR filter of Fig. 1 with coefficients that are quantized to 4 bits with 1 bit for the sign.
    </figcaption>
  </figure>
</div>
Because of symmetry, only one quadrant of the $Z$-plane is shown.
In this case the possible pole positions are at the crossings of the black vertical lines and red circles. From this figure we can see that the possible pole positions are not evenly distributed over the $Z$-plane. The largest deviation of the desired frequency response is in case where the possible pole positions are far from each other.

Fig. 3 shows an alternative realization of the second order recursive structure as discussed above. This alternative example shows that the sensitivity of the filter to coefficient quantization depends also on the structure of the filter.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/example9b.svg"
      alt="Alternative second order IIR filter."
    />
    <figcaption class="numbered">
      Alternative second order IIR filter.
    </figcaption>
  </figure>
</div>

Fig. 4 shows possible pole posities when both coefficients $a$ and $b$ are decimal fractions that are quantized to 4 bits, from which 1 bit represents the sign.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/example9bsensitivity.svg"
      alt="Set of allowable pole positions (only at the crossings of the black and red lines) of alternative second order IIR filter of Fig. 3 with coefficients that are quantized to 4 bits with 1 bit for the sign."
    />
    <figcaption class="numbered">
      Set of allowable pole positions (only at the crossings of the black and red lines) of alternative second order IIR filter of Fig. 3 with coefficients that are quantized to 4 bits with 1 bit for the sign.
    </figcaption>
  </figure>
</div>

From this figure it follows that the poles of this alternative second order structure are more evenly distributed over the $Z$-plane compared to the structure as depicted in Fig. 1.
As a conclusion it follows that in general the possible pole positions are strongly dependent on the filter structure.

As a final note we should realize that quantization of the coefficients  can also influence the stability of the second order filter structure, since the coefficients of a stable second order system have to be within the so called stability triangle, as discussed in the reader about system function of an LTI filter.
