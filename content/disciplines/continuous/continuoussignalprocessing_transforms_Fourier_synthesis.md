+++
title = "Fourier series synthesis"

# date = {{ .Date }}
lastmod = 2020-03-28

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Fourier series synthesis"
  weight = 2
  parent = "Transforms II: Fourier series"
+++

In the previous section we have seen that every periodic signal $x(t)$, with Fundamental period $T_0 = 1/F_0$, can be written as a sum of weighted harmonic related phasor components. In theory the summation can contain an infinite amount of components which leads to the following Fourier series expansion:

$$\bbox[5px,border:1px solid black]{
x(t) = \sum_{k=-\infty}^{\infty} \alpha_k e^{j2\pi kF_0 t}.}
$$

Thus when the spectral weights, which are represented by the complex numbers $\alpha_k$, are known we can construct (synthesize) the periodic signal $x(t)$ according the above general expression.
