+++
title = "Spectral factorization and innovation representation "         # name of webpage

# date = {{ .Date }}
lastmod = 2020-06-17

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.

[menu.statistical]                       # name of menu section (main module)
  name = "Spectral factorization"        # name of this item in that menu
  weight = 2                           # location in that menu
  parent = "Rational signal models"

+++

Signal modeling is closely related to *spectral factorization* which states that most random processes with a continuous power spectral density (PSD) can be generated as the output of a causal filter driven by white noise, the so-called innovation representation of the random process.

In the module Power spectral density, we have seen that the PSD and the AC of a random signals are Fourier pairs. Consider a system depicted in Fig., with input $x[n]$ and output $y[n]$. Can we determine $H(z)$ by knowledge of $r_y[l]$ (or equivalently $P_y(e^{j\theta})$), and that the input is white noise with given $\sigma_x^2$? Unfortunately, there is no unique answer to this question. In fact, knowledge of $P_y(e^{j\theta})$ provides us only with the magnitude response of the system, i.e. $|H(z)|$, since we know that $P_y(e^{j\theta})$ = $\sigma_x^2$  $|H(z)|^2$ . This can be show by the following example.

\begin{equation*}
\begin{split}
    P_y(e^{j\theta}) &=& \sigma_i^2|H(e^{j\theta})|^2 = \frac{5}{4}-cos(\theta)\newline
    \sigma_i^2|H(z)|^2 &=& \sigma_i^2H(z)H(z^{-1}) = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
    \\
    H(z) &=& 1-\frac{1}{2}z^{-1} \quad \text{with} \quad \sigma_i^2=1\newline
    \sigma_i^2 H(z)H(z^{-1})&=& (1-\frac{1}{2}z^{-1})(1-\frac{1}{2}z)\newline
    & =& 1-\frac{z+z^{-1}}{2}+\frac{1}{4} = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
    H(z) &=& 1-2z^{-1} \quad \text{with} \quad \sigma_i^2=\frac{1}{4}\newline
    \sigma_i^2 H(z)H(z^{-1})&=& \frac{1}{4}(1-2z^{-1})(1-2z)\newline
    & = &\frac{1}{4}-\frac{z+z^{-1}}{2}+1 = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
\end{split}
\end{equation*}
Consequently more constraints are needed to uniquely define $H(z)$ for either $r_y[l]$ or $R_y(e^{j\theta})$. Therefore, spectral factorization is define as the determination of a minimum-phase system from its magnitude response or from its auto correlation function. In the previous example this would have been $H(z) = 1-\frac{1}{2}z^{-1}$.
Thus, if $P(z)$ is rational is can be factorized in the following form $\sigma_i^2 L(z)L(z-1)$. In which $L(z)$ is minimum-phase, and $\sigma^2_i$ is chosen such that $l[0]=1$.
