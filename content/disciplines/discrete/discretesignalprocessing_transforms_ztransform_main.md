+++
title = "Transforms IV: Z-transform"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Transforms IV: Z-transform"
  weight = 54


+++


## Summary
<ul>
  <li>
    Definition ZT:
    $$
    \boxed{X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n}} \label{eq:ZT}
    $$
  </li>
  <br></br>
  <li>
    <i>Region Of Convergence (ROC): All values of $z$ for which ZT converges.</i>
  </li>
  <br></br>
  <li>
    <i>FTD $\equiv$ ZT for $|z|=1$ only when the unit circle is in the ROC</i>
  </li>
  <br></br>
  <li>
    <i>The ZT $X(z)$ is only uniquely related to a sequence $x[n]$ if the ROC is known. Hence, the ZT must always be specified with its ROC.</i>
  </li>
  <br></br>
  <li>
  ROC's of divergent and convergent sequences:
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/transforms/Z/ROCexamplesx1x2.svg"
        alt="ROC's of divergent and convergent infinite length right- and left-sided sequences."
      />
    </figure>
  </div>
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/transforms/Z/ROCexamplesx3x4.svg"
        alt="ROC's of finite and infinite sequences."
      />
    </figure>
  </div>
  </li>
  <br></br>
  <li>
    <i>If rational $X(z)$ has poles with $R$ distinct magnitudes $\Rightarrow$ $R+1$ distinct sequences $x[n]$ having same rational $X(z)$.</i>
  </li>
  <br></br>
  <li>
    Linear property:
    $$
    w[n] = \alpha x[n] + \beta y[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad W(z) = \alpha X(z) + \beta Y(z)
    \text{ ROC } R_w=R_x \cap R_y
    $$
  </li>
  <br></br>
  <li>
    Shift property:
    $$
    x[n-n_0] \quad  \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad z^{-n_0} X(z)
    \text{ with ROC } R_x
    $$
  </li>
  <br></br>
  <li>
    Time reversal property:
    $$
    x[-n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X(z^{-1})
    \text{ with ROC } 1/R_x
    $$
  </li>
  <br></br>
  <li>
    Multiply by $a^n$:
    $$
    a^n x[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X(a^{-1} z) \text{ with ROC } R_y= |a|R_x
    $$
  </li>
  <br></br>
  <li>
    Convolution property:
    $$
    x[n] \star y[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X(z) \cdot Y(z)
    \hspace{3mm} \text{with } R_w=R_x \cap R_y
    $$
  </li>
  <br></br>
  <li>
    Conjugation property:
    $$
    x^\ast[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X^\ast(z^\ast) \text{ ; } R_x
    $$
  </li>
  <br></br>
  <li>
    Derivation property:
    $$
    n \cdot x[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad -z \frac{\text{d}}{\text{d} z} X(z) \text{ ; } R_x
    $$
  </li>
  <br></br>
  <li>
Initial value property:
$$
x[0] = \lim_{z \rightarrow \infty} \left \{ X(z) \right \}
$$
</li>
<br></br>
<li>
One sided ZT:
$$
\boxed{\tilde{X}(z)=\sum_{{\color{red}{n=0}}}^{\infty} x[n] z^{-n}}
$$
</li>
<br></br>
<li>
One sided ZT shift property:
$$
x[n-k] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad {\color{red}{\sum_{p=-k}^{-1} x[p] z^{-(p+k)}}} +  z^{-k} \cdot   \tilde{X}(z)
$$
</li>
<br></br>
<li>
IZT method 1: Table Lookup
</li>
<br></br>
<li>
IZT method 2: Long Tail Division

<u>Descending ordered polynomials:</u>
$$
X(z) = \frac{N(z)}{D(z)}=\sum_{k }^{} c_k z^{-k}
\hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm} x[n] = \sum_{k }^{} c_k \delta[n-k]
$$
<u>Ascending ordered polynomials:</u>
$$
X(z)=\frac{N(z)}{D(z)}=z^{M-N} \cdot \sum_{k=0}^{\infty} d_k z^{k} \quad\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad x[n] =\sum_{k=0}^{\infty} d_k \delta[n+(M-N)+k]
$$
</li>
<br></br>
<li>
IZT method 3: Partial Fraction; Single poles:
$$
X(z) =\frac{N(z)}{D(z)}
= \frac{\sum_{p=0}^{N} b_p z^{-p}}{\prod_{k=1}^{M} (1 - \alpha_k z^{-1})}
$$
<u>Case $M>N$:</u>
$$
X(z) =\sum_{k=1}^{M} \frac{A_k}{1 - \alpha_k z^{-1}}
\quad\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  \quad x[n] =\sum_{k=1}^{M} A_k (\alpha_k)^n u[n]
$$
$A_k$ via coefficient matching or residuals:
$$
A_k = \left [ (1 - \alpha_k z^{-1}) X(z) \right ] \mid_{z=\alpha_k}
$$
<u>Case $M \leq N$:</u>
$$
X(z) = \sum_{k=0}^{N-M}B_k z^{-k} + F(z)
\quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  \quad x[n] =\sum_{k=0}^{N-M}B_k \delta[n-k] +f[n]
$$
Order denominator $F(z)$ larger than order numerator. Coefficients $B_k$ via ascending ordered long tail division.
</li>
<br></br>
<li>
IZT method 3: Partial Fraction; Multiple order poles:
$$
X(z) = \frac{\sum_{p=0}^{N} b_p z^{-p}}{\left ( \prod_{k=1}^{M-K} (1 - \alpha_k z^{-1})\right ) \cdot \left ( 1 - \tilde{\alpha} z^{-1} \right )^K }
$$
$$
X(z) = \sum_{k=0}^{N-M}B_k z^{-k} +\sum_{k=1}^{M-K} \frac{A_k}{1 - \alpha_k z^{-1}}
+ \sum_{p=1}^{K} \frac{C_p}{(1 - \tilde{\alpha} z^{-1})^p}
$$
<u>General equation to compute residuals:</u>
$$
C_p  = \frac{1}{(K-p)! \cdot (-\tilde{\alpha})^{(K-p)}} \cdot
\frac{\text{d}^{K-p}}{\text{d} (z^{-1})^{K-p}}
\bigg[ (1-\tilde{\alpha} z^{-1})^K \cdot F(z) \bigg]
\mid_{z=\tilde{\alpha}}.
$$
</li>
<br></br>
<li>
Definition Inverse Z-Transform (IZT):
$$
\boxed{
x[n] = \frac{1}{2 \pi j} \oint_{{\color{red}{C}}} X(z) z^{n-1} \text{d} z }
$$
</li>
<br></br>
<li>
Cauchy's residu theorem:
$$
\frac{1}{2 \pi j} \oint_{C} F(z) \text{d} z =
\sum \left [ \text{Residues $F(z)$ @ poles inside $C$} \right ]
$$
</li>
<br></br>
<li>
General equation to compute the residu:
$$
\text{Res} \left [ F(z) \text{ @ } z=z_0 \right ] = \frac{1}{(K-1)!} \cdot
\frac{\text{d}^{K-1}}{\text{d} z^{K-1}} \left [ (z-z_0)^K \cdot F(z) \right ]
\mid_{z=z_0}
$$
</li>
<br></br>
<li>
Cauchy'integral theorem:
$$
\frac{1}{2 \pi j} \oint_{C}  z^{n-1} \text{d} z = \delta[n]
$$
</li>
</ul>
