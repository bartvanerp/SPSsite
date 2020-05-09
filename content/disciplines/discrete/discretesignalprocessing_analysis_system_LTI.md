+++
title = "System function rational LTI"

# date = {{ .Date }}
lastmod = 2020-05-09

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "System function rational LTI"
  weight = 1
  parent = "Analysis III: System function"
+++

In this section we will derive the system function of a rational LTI function from the signal flow graph representation. This also leads to an alternative to find the frequency response of such an LTI system.

The signal flow graph of a rational LTI system is depicted in Fig. 1 and the Difference Equation is as follows:
\begin{eqnarray*}
 y[n] &=& \sum_{k=0}^{M-1} b_k x[n-k] + \sum_{k=1}^{N-1} a_k y[n-k]
\end{eqnarray*}
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/flowdiagram.svg"
      alt="Flow graph of a rational LTI system in time domain."
    />
    <figcaption class="numbered">
      Flow graph of a rational LTI system in time domain.
    </figcaption>
  </figure>
</div>
As a first step we describe the signal flow graph in the $Z$-domain. For this we use the following property:
$$
h[n]=\delta[n-1] \overset{ZT}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} H(z)= z^{-1}
$$
Thus for the description of the signal flow graph in $Z$-domain,
we interchange the time domain sequences $x[n]$ and $y[n]$ by their $Z$-transforms $X(z)$ and $Y(z)$ respectively and we use the symbol $z^{-1}$ to represent a delay. The result is depicted in Fig. 2.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/flowdiagramZ.svg"
      alt="Representation of flow graph of a rational LTI system in the $Z$-domain."
    />
    <figcaption class="numbered">
      Representation of flow graph of a rational LTI system in the $Z$-domain.
    </figcaption>
  </figure>
</div>
From this flow graph representation in the $Z$-domain we obtain the following algebraic equation between $X(z)$ and $Y(z)$:
\begin{equation}\label{Eq:RationalYZXZ}
Y(z) = \sum_{k=0}^{M-1} b_k z^{-k} X(z) + \sum_{k=1}^{N-1} a_k z^{-k} Y(z)
\end{equation}
Furthermore by using the property that a convolution sum in time domain transforms in $Z$-domain to a product:
$$
y[n]= x[n] \color{red}{\star } h[n] \overset{ZT}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} Y(z) = X(z) \color{red}{\cdot } H(z)
$$
it follows that we can find the system function $H(z)$ by dividing $Y(z)$ by $X(z)$. Thus from equation (\ref{Eq:RationalYZXZ}) we simply can derive the rational system function $H(z)$ of the LTI system as follows:
\begin{equation}\label{Eq:Hz}
H(z) = \frac{ Y(z)}{X(z)} =
\frac{\sum_{k=0}^{M-1}b_k z^{-k}}{1 - \sum_{k=1}^{N-1}a_k z^{-k}}
\end{equation}
Both numerator and denominator polynomials can be split as a product of first order terms:
\begin{eqnarray*}
H(z) &=& b_0 \frac{\prod_{k=1}^{M} (1 - \color{blue}{\beta_k} z^{-1})}{\prod_{k=1}^{N} (1 - \color{magenta}{\alpha_k} z^{-1})}
\end{eqnarray*}
Therefore, the system function $H(z)$ of an LTI system is defined, to within a scale factor $b_0$, by the location of the poles $\alpha_k$, and zeros $\beta_k$.

Finally the frequency response may be derived from the system function by evaluating the system function around the unit circle:
$$
H(e^{j\theta}) = H(z)|\_{z = e^{j\theta}}
$$
which leads to an alternative way to find the frequency response of an LTI system:
$$
H(z) = \frac{Y(z)}{X(z)}
\mbox{ } \Rightarrow \mbox{ } H(e^{j\theta}) = H(z)|\_{z = e^{j\theta}}
$$

<div class="example">
<h4> Example </h4>
<hr>
Given the following Difference Equation of an LTI system:
\begin{eqnarray*}
y[n] &=& b_0 x[n] + b_1 x[n-1] + b_2 x[n-2]+ a_1 y[n-1]+ a_2 y[n-2]
\end{eqnarray*}
Calculate the frequency response via the System function.
<button class="collapsible">Show solution</button>
<div class="content">
As a first step we describe the signal flow graph in the $Z$-domain. That is:  We interchange the time domain sequences $x[n]$ and $y[n]$ by their $Z$-transforms $X(z)$ and $Y(z)$ respectively and we use the symbol $z^{-1}$ to represent a delay.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/example1.svg"
      alt="example1."
    />
  </figure>
</div>
This signal flow graph representation in the $Z$-domain, results is a simple algebraic expression between input $X(z)$ and output $Y(z)$ as follows:
\begin{eqnarray*}
Y(z) &=& b_0 X(z) + b_1 z^{-1} X(z) + b_2 z^{-2} X(z)+ a_1 z^{-1} Y(z)+ a_2 z^{-2} Y(z)
\end{eqnarray*}
We can find the system function $H(z)$ as follows:
\begin{eqnarray*}
H(z)=\frac{Y(z)}{X(z)} &=&  \frac{b_0 +b_1 z^{-1} + b_2 z^{-2}}{1 -a_1 z^{-1} - a_2 z^{-2}}
\end{eqnarray*}
By evaluating this expression around the unit circle leads to an expression for the frequency response $H(e^{j\theta})$ of the given signal flow graph as follows:
\begin{eqnarray*}
H(e^{j\theta}) &=& H(z)|\_{z=e^{j\theta}} =
\frac{b_0 +b_1 e^{-j\theta} + b_2 e^{-j2\theta}}{1 -a_1 e^{-j\theta} -a_2 e^{-j2\theta}}
\end{eqnarray*}
</div>
</div>
