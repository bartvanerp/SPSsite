+++
title = "Structures of non-recursive systems"

# date = {{ .Date }}
lastmod = 2020-05-02

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Structures of non-recursive systems"
  weight = 1
  parent = "Filter structures II: General filter structures"
+++


We first consider different structures for non recursive systems, that is systems without a feedback loop.

## Direct form
The most common form of a non recursive filter is the so called transversal filter or tapped delay line as depicted in the Fig. 1, from which the difference equation is described by the following difference equation:
$$
y[n]=\sum_{k=0}^{M-1} b_k x[n-k]
$$
and the system function is described by the following  numerator polynomial:
$$
H(z) = \sum_{k=0}^{M-1} b_k z^{-k}
$$

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/directform.svg"
      alt="Transversalfilter or tapped delay line."
    />
    <figcaption class="numbered">
      Transversalfilter or tapped delay line.   
    </figcaption>
  </figure>
</div>

In a previous module we have seen that this filter has the following properties:
<ul>
  <li> The filter is causal since  the output signal $y[n]$ depends only on current and previous values of the input signal $x[n]$. </li>
  <li> The coefficients of the length $M$ impulse response $h[n]= \sum_{k=0}^{M-1} h_k \delta[n-k]$ are the same as the filter coefficients, namely with $h_k=b_k$. </li>
  <li> The system function $H(z)$ contains only zeros (and $M-1$ poles in $z=0$). </li>
  <li> The realization of the filter requires $M$ multiplications and $M-1$ additions. </li>
  <li> The filter structure is always stable, since there are no poles outside the unit circle. </li>
</ul>

<br></br>
## Cascade form
The system function $H(z)$ of the non recursive structure may be factored into a product of first order factors as follows:
$$
H(z) = \sum_{k=0}^{M-1} h_k z^{-k}=C \prod_{k=1}^{M-1} \left (1 - \alpha_k z^{-1} \right )
$$
where $\alpha_k$ for $k=1, \cdots , M-1$ are the zeros of the system function $H(z)$.
In case the complex roots of the system function $H(z)$ occur in complex conjugate pairs, these conjugate pairs may be combined to form second order factors with real coefficients as shown in the following equation:
$$
(1-\alpha z^{-1}) (1-\alpha^* z^{-1})
= 1 - \color{red}{2 \Re e \\{ \alpha \\}} z^{-1} + \color{red}{| \alpha|^2} z^{-2}
$$

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/cascade2.svg"
      alt="Cascaded non-recursive structure with real coefficients."
    />
    <figcaption class="numbered">
      Cascaded non-recursive structure with real coefficients.
    </figcaption>
  </figure>
</div>

When writing $H(z)$ in this form, the filter can be implemented as a cascade of the following second order non recursive structures:
$$
H(z)= C \prod_{k=1}^{M_s} \left ( 1 + \beta_{1,k}z^{-1} + \beta_{2,k}z^{-2} \right )
$$
as illustrated in the Fig. 2.
