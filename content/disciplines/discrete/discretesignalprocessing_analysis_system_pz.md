+++
title = "Poles and zeros of system function"

# date = {{ .Date }}
lastmod = 2020-05-09

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Poles and zeros"
  weight = 3
  parent = "Analysis III: System function"
+++

As discussed before the system function $H(z)$ of a rational LTI system has a numerator and a denominator polynomial.
\begin{eqnarray*}
H(z) = \frac{ Y(z)}{X(z)} =
\frac{\sum_{k=0}^{M}b_k z^{-k}}{1 - \sum_{k=1}^{N}a_k z^{-k}}
&=&
b_0 \frac{\prod_{k=1}^{M} (1 - \color{blue}{\beta_k} z^{-1})}{\prod_{k=1}^{N} (1 - \color{magenta}{\alpha_k} z^{-1})}
\end{eqnarray*}
Both numerator and denominator polynomials can be split as a product of first order terms. Therefore, the system function $H(z)$ of a rational LTI system is defined, to within a scale factor $b_0$, by the location of the poles $\alpha_k$, and zeros $\beta_k$.
Note that each term in the numerator $1-\beta_k z^{-1}$ contributes a zero to the system function at $z=\beta_k$ and a pole at $z=0$. Similarly, each term in the denominator $1- \alpha_k z^{-1}$ contributes a pole at $z=\alpha_k$ and a zero at $z=0$.  On the one hand, an FIR system consists, besides poles at $z=0$, of only zeros. On the other hand an IIR system consists of both poles and zeros.  If the impulse response $h[n]$ is real-valued, the system function $H(z)$ is a conjugate symmetric function of $z$, thus $H(z)=H^\ast(z^\ast)$ and the complex poles and zeros occur in conjugate symmetric pairs. Thus if there is a complex pole (zero) at $z=z_0$, there is also a pole (zero) at $z=z^\ast_0$.
