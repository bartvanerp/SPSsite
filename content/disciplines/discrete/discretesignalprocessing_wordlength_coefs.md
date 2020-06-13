+++
title = "Quantization of filter coefficients"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Quantization of filter coefficients"
  weight = 4
  parent ="Finite word length effects"

+++


For LTI filters,  when coefficients are quantized the system function
can be written as follows:
$$
\hat{H}(z) = \sum_{n} \left \\{ h[n] + \color{red}{ \Delta h[n] } \right \\} z^{-n} = H(z) + \color{red}{\Delta H(z)}
$$
which is depicted in Fig. 1.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/finitewordlength/QuantizedFIR.svg"
      alt="System function of quantized LTI filter."
    />
    <figcaption class="numbered">
      System function of quantized LTI filter.
    </figcaption>
  </figure>
</div>
Thus the quantization errors may be modeled as $H(z)$ in parallel with $\Delta H(z)$. As a conclusion it follows that quantization:
<ul>
  <li> Does not introduce non-linearity effects, </li>
  <li> Will influence the filter characteristics. </li>
</ul>
