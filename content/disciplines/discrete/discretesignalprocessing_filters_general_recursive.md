+++
title = "Structures of recursive systems"

# date = {{ .Date }}
lastmod = 2020-05-02

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Structures of recursive systems"
  weight = 2
  parent = "Filter structures II: General filter structures"
+++

The following equation describes the difference equation of a recursive system:
$$
y[n]=\sum_{k=0}^{M-1} b_k x[n-k] + \sum_{k=1}^{N-1} a_k y[n-k]
$$
Its rational system function contains a numerator polynomial $B(z)$ and a denominator polynomial $A(z)$ as follows:
$$
H(z) = \frac{Y(z)}{X(z)}= \frac{\sum_{k=0}^{M-1}b_kz^{-k}}{1-\sum_{k=1}^{N-1}a_kz^{-k}}= \frac{\color{blue}{B(z)}}{\color{brown}{A(z)}}
$$
From this mathematical description we will derive in the following sub-sections the following recursive structures:
\begin{eqnarray*}
\color{red}{\text{Direct form I}} & : & H(z) = \color{blue}{B(z)} \cdot \color{brown}{\frac{1}{A(z)}} \newline
\color{red}{\text{Direct form II}} & : & H(z) = \color{brown}{\frac{1}{A(z)}} \cdot \color{blue}{B(z)} \newline
\color{red}{\text{Cascade}} & : & H(z)= C \prod_{k=1}^{\text{max} \\{ N-1,M-1\\}} \frac{1 - \beta_k z^{-1}}{1 - \alpha_k z^{-1}} \newline
\color{red}{\text{Parallel} (N>M, \alpha_i \neq \alpha_k)} & : & H(z)= \sum_{k=1}^{N-1} \frac{C_k}{1 - \alpha_kz^{-1}}
\end{eqnarray*}


## Direct and canonic forms
The direct form I structure is an implementation which follows from
the description of the system function $H(z)$ as the product of the non recursive part $B(z)$ with the recursive part $1/A(z)$ as shown in the upper part of figure of Fig. 1 and 2.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/directformI.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/directformII.svg"
    style="width:100%">
  </div>
</div>
<figcaption class="numbered">
  Different direct form recursive structures.
</figcaption>
</figure>

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/canonicdirectformII.svg"
      alt="Canonical direct form II filter structure."
    />
    <figcaption class="numbered">
      Canonical direct form II filter structure.  
    </figcaption>
  </figure>
</div>

The direct form II structure, which follows from the description of the system function $H(z)$ as a product, but now the other way around. Thus first the recursive part $1/A(z)$ and then the non recursive part  $B(z)$ as shown in the right part of Fig. 1.
From this direct form II structure it is obvious that we can combine delays, which results in the direct form II structure as shown in Fig. 2. This structure is canonic since it uses the minimum number of delays for the given system function $H(z)$.

<br></br>
## Cascade form
The cascade structure follows from factoring the numerator and denominator polynomials and using these factors to write the system function as a product $H(z)= C \prod_{k} H_k(z)$. The factorization corresponds to a cascade of first order filters, each having one pole and one zero. In general the coefficients $\alpha_k$ and $\beta_k$ will be complex.
\begin{eqnarray*}
\text{Complex } h[n] &:& H_k(z) =\frac{1 - \beta_k z^{-1}}{1 - \alpha_k z^{-1}}
\end{eqnarray*}
As mentioned before, when the impulse response $h[n]$ is real, the roots of the system function $H(z)$ will occur in complex conjugate pairs, and these complex conjugate factors may be combined to from second order factors with real coefficients.
\begin{eqnarray*}
\text{Real } h[n] &:&
H_k(z) =\frac{1 + \gamma_{1,k} z^{-1}+ \gamma_{2,k}z^{-2}}{1 +\rho_{1,k} z^{-1}+\rho_{2,k} z^{-2}}
\end{eqnarray*}

<div class="example">
<h4> Example </h4>
<hr>
  Factor the following system function as a cascade of a first order and a second order structure both with real coefficients:
  $$
  H(z)=\frac{1 -\frac{1}{4}z^{-1}+\frac{1}{4}z^{-2}+\frac{3}{8}z^{-3}}
  {1 +\frac{1}{4}z^{-1}-\frac{1}{4}z^{-2}-\frac{3}{8}z^{-3}}
  $$
  Finally give the pole-zero plot and a sketch of the magnitude and phase response.
<button class="collapsible">Show solution</button>
<div class="content">
  We can factor $H(z)$ as the following product of a first order recursive structure $H_1(z)$ (in red) and a second order recursive structure $H_2(z)$ (in blue):
  $$
  H(z) =
  \left ( \color{red}{\frac{1 +\frac{3}{4}z^{-1}}{1 -\frac{3}{4}z^{-1}}} \right ) \cdot
  \left ( \color{blue}{\frac{1 -z^{-1}+\frac{1}{2}z^{-2}}{1 +z^{-1}+\frac{1}{2}z^{-2}}} \right )
  $$
  Both filters have real coefficients and the realization scheme of this cascaded structure is depicted in the following figure:
  <div style="max-width: 800px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/filters/general/cascade.svg"
        alt="Cascaded filter structure."
      />
    </figure>
  </div>
  The pole-zero plot, which is depicted at the left hand side of the following figure, shows the real pole and zero of the first order system (in red) and the complex conjugated pairs of poles and zeros of the second order system in blue.
  <figure>
    <div class="rowimg2">
      <div class="columnimg2">
        <img src="/../files/7.Images/discrete/filters/general/cascadePZ.svg"
        style="width:100%">
      </div>
      <div class="columnimg2">
        <img src="/../files/7.Images/discrete/filters/general/cascadeAmplPhase.svg"
        style="width:100%">
      </div>
    </div>
  </figure>
  Finally, the magnitude and phase response plots are depicted at the right hand side of the figure.
</div>
</div>

<br></br>
## Parallel form
An alternative way to factoring the system function is to expand the system function using a partial fraction expansion and write the system function as $H(z)= \sum_{k} H_k(z)$. This corresponds to a sum of sub systems which can be realized by connecting these sub systems in parallel. Each of these sub systems may be first order filters with complex impulse response coefficients.
\begin{eqnarray*}
\text{Complex } h[n] &:& H_k(z) =\frac{C_k}{1 - \alpha_k z^{-1}}
\end{eqnarray*}
If the impulse response $h[n]$ has real coefficients, the poles of the system function $H(z)$ will occur in complex conjugate pairs which can be combined to from second order systems with real coefficients.
\begin{eqnarray*}
\text{Real } h[n] &:&
H_k(z) =\frac{\gamma_{0,k} + \gamma_{1,k} z^{-1}}{1 +\rho_{1,k} z^{-1}+ \rho_{2,k} z^{-2}}
\end{eqnarray*}



<div class="example">
<h4> Example </h4>
<hr>
Split the following second order recursive system function
$$
H(z)=\frac{4 -\frac{7}{4}z^{-1}+\frac{1}{4}z^{-2}}{1 -\frac{3}{4}z^{-1}+\frac{1}{8}z^{-2}}
$$
by using partial fraction expansion into a sum of three sub system functions which can be realized by connecting these sub systems in parallel.
<button class="collapsible">Show solution</button>
<div class="content">
  The system function can be split into the following 3 parallel sub systems:
  $$
  H(z)=\color{brown}{2}  \color{red}{+\frac{3}{1 -\frac{1}{2}z^{-1}}} \color{blue}{-\frac{1}{1 -\frac{1}{4}z^{-1}}}
  $$
  These 3 sub systems can be realized in parallel as depicted in the figure.
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/filters/general/example5.svg"
        alt="Cascaded filter structure."
      />
    </figure>
  </div>
</div>
</div>
