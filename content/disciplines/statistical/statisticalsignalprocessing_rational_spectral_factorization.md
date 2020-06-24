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

## Innovation representation

## Spectral factorization: problem
In the module <a href="../statisticalsignalprocessing_signals_psd">Power spectral density</a>, we have seen that the PSD and the AC of a random signals are Fourier pairs. Consider a system depicted in Fig., with input $x[n]$ and output $y[n]$.

Spectral factorization tackles the following questions: Can we determine $H(z)$ knowing that the input $x[n]$ is white noise, and given the second-order statistics ($r_y[l]$  or equivalently $P_y(e^{j\theta})$) of the output signal $y[n]$? In principle, there is no unique answer to this question. We can understand this by looking at the following example.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/signals/spectfact_1.bmp"
      alt="Spectral factorization"
    />
    <figcaption class="numbered">
     Spectral factorization problem: determining $H(z)$ knowing that the input $x[n]$ is white noise, and given the second-order statistics of the output signal $y[n]$.
    </figcaption>
  </figure>
</div>

Suppose we are given the PSD of $y[n]$. Since we know that $P_y(e^{j\theta})$ = $\sigma_x^2$  $|H(z)|^2$, we can write:
\begin{equation*}
\begin{split}
    P_y(e^{j\theta}) &=& \sigma_i^2|H(e^{j\theta})|^2 = \frac{5}{4}-cos(\theta)\newline
    \sigma_i^2|H(z)|^2 &=& \sigma_i^2H(z)H(z^{-1}) = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
\end{split}
\end{equation*}

Knowledge of $P_y(e^{j\theta})$ provides us with the magnitude response of the system, i.e. $|H(z)|$. However, there are two possible cases which provide the same magnitude response $|H(z)|^2$:
<ol>
<li> In the first case, we can define $H(z)$ and the input noise variance as:
\begin{equation*}
    H(z) = 1-\frac{1}{2}z^{-1}, \quad \text{with} \quad \sigma_x^2=1.
\end{equation*}
This choice gives as output $P_y(e^{j\theta})$, as proven below:
\begin{equation*}
\begin{split}
    \sigma_x^2 H(z)H(z^{-1})&=& (1-\frac{1}{2}z^{-1})(1-\frac{1}{2}z)\newline
    & =& 1-\frac{z+z^{-1}}{2}+\frac{1}{4} = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
\end{split}
\end{equation*}
</li>

<li> Alternatively, we can define $H(z)$ and the input noise variance as:
\begin{equation*}
  H(z) = 1-2z^{-1}, \quad \text{with} \quad \sigma_x^2=\frac{1}{4}.
\end{equation*}
This choice gives the same output $P_y(e^{j\theta})$, as proven below:
\begin{equation*}
\begin{split}
    \sigma_x^2 H(z)H(z^{-1})&=& \frac{1}{4}(1-2z^{-1})(1-2z)\newline
    & = &\frac{1}{4}-\frac{z+z^{-1}}{2}+1 = \frac{5}{4}-\frac{z+z^{-1}}{2}\newline
\end{split}
\end{equation*}
</li>
</ol>

Consequently more constraints are needed to uniquely define $H(z)$ which gives $r_y[l]$ or $P_y(e^{j\theta})$.

## Spectral factorization: definition
Spectral factorization is defined as the determination of a minimum-phase system from its magnitude response or from its auto correlation function. If $P(z)$ is rational, it can be factorized in the following form $\sigma_i^2 L(z)L(z^{-1})$, in which so-called "innovation filter" $L(z)$ is minimum-phase, and $\sigma^2_i$ is chosen such that $l[0]=1$.

One practical method to solve the spectral factorization problem is referred to as the *root method*. The basic principles are:
<ol>
<li> For every rational PSD, that is a PSD that can be expressed as a fraction between two polynomials in $e^{-j\omega}$ (or equivalently in $z$), there exist a unique minimum-phase factorization within a scale factor.  </li>
<li> For a PSD expressed as a rational polynomials, with a numerator of order Q and a denominator of order P, there are $2^{P+Q}$ possible rational systems which provide this PSD. </li>
<li> Not all possible rational systems are valid, since for a valid PSD the roots should appear in mirrored pairs, that is if $z_k$ is a root also $1/z^\ast_k$. </li>
<ol>
In the example above, we therefore need to choose $H(z) = 1-\frac{1}{2}z^{-1}$, as it is the minimum-phase choice.
