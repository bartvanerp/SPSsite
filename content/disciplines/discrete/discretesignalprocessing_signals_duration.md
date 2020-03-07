+++
title = "Signal duration"

# date = {{ .Date }}
lastmod = 2020-03-07

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Signal duration"
  weight = 3
  parent = "Discrete-time signals"


+++

Discrete-time signals may be conveniently classified in terms of their duration or extent. For example, a discrete-time sequence is said to be a finite-length sequence if it is equal to zero for all values of the index $n$ outside a finite interval of indices. An example of such a finite signal, as depicted at the left hand side of Fig. 1, is $u[n+1]-u[n-1]$ which is zero for all indices $n$ except for $n=-1$, $n=0$ and $n=1$.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/signals/signalduration.svg"
      alt="Examples of finite and infinite length signals."
    />
    <figcaption class="numbered">
      Examples of finite and infinite length signals.
    </figcaption>
  </figure>
</div>
Signals that are not finite in length, such as the unit step and complex exponential function, are said to be infinite length sequences. Infinite length sequences may further be classified as either being right-sided, left-sided, or two-sided.
A right-sided sequence is any infinite length sequence that is equal to zero for all values of the index $n$ smaller than some integer $n_0$.  The unit step function delayed over 2 samples, as depicted in the middle of Fig. 1,
is an example of such a infinite length right-sided sequence.
Similarly an infinite-length sequence is said to be left-sided if, for some integer $n_0$ the signal is zero for all indices $n$ larger than $n_0$.  An example of such an infinite length left-sided sequence is $u[-n+2]$, which is depicted at the right hand side of Fig. 1.
Finally an infinite length signal that is neither right-sided nor left-sided is referred to as a two-sided sequence.
