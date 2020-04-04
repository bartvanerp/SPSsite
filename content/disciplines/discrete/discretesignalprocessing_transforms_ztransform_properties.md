+++
title = "Properties of the Z-transform"

# date = {{ .Date }}
lastmod = 2020-02-16

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Properties"
  weight = 2
  parent = "Transforms IV: Z-transform"


+++


## Screencast video [⯈]

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/-PwKgv0qdsg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

This section first describes the main properties of the ZT.
Finally, the so called one-sides ZT will be introduce, which is useful for solving Difference Equations with initial conditions.

Assume the ZT of the sequences $x[n]$ and $y[n]$ are given by $X(z)$ and $Y(z)$ and their ROC by $R_x$ and $R_y$ respectively.

$$
\begin{eqnarray*}
x[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(z) \text{ with ROC } R_x & \quad\text{and} \quad&
y[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } Y(z) \text{ with ROC } R_y
\end{eqnarray*}
$$

<br></br>
## Property: Linearity
The ZT, as the FTD, is a linear operation:

$$
\boxed{w[n] = \alpha x[n] + \beta y[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad W(z) = \alpha X(z) + \beta Y(z)
\text{  with ROC  } R_w=R_x \cap R_y}
$$

The resulting ROC $R_w$ of the sequence $w[n]$ will include the intersection of $R_x$ and $R_y$.  However the ROC $R_w$ may be larger.

<div class="example">
  <h4> Example </h4>
  <hr>
  Compute the ROC of $w[n]=x[n]-y[n]$, with $x[n]=u[n]$ and $y[n]=u[n-1]$.
  <button class="collapsible">Show solution</button>
  <div class="content">
    Both ROC's $X(z)$ and $Y(z)$ are all values of $z$ outside the circle with radius 1. However, the ZT of $w[n]=x[n]-y[n]=\delta[n]$ is the entire $z$-plane.
  </div>
</div>

<br></br>
## Property: Shifting
Shifting a sequence, which can be delaying or advancing, multiplies the ZT by a power of $z$:

$$
\boxed{x[n-n_0] \quad  \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad z^{-n_0} X(z)
\text{ with ROC } R_x}
$$

Because shifting a sequence does not affect its absolute sumability, shifting does not change the ROC. Therefor, the ZT of $x[n]$ and $x[n-n_0]$ have the same ROC, with the possible exception of adding or deleting the points $z=0$ and $z=\infty$.

<br></br>
## Property: Time reversal
The ZT of the time reversed sequence $x[-n]$ is given by $X(z^{-1}$.

$$
\boxed{x[-n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X(z^{-1})
\text{ with ROC } 1/R_x}
$$

In case the ROC $R_x$ is given by the annulus in between $r_{-}$ and $r_{+}$, the ROC of the time reversed sequence is given by the annulus in between $\frac{1}{r_{+}}$ and $\frac{1}{r_{-}}$, which is denoted by $1/R_x$.

<br></br>
## Property: Multiply by $a^n$
$$
\boxed{a^n x[n] \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \quad X(a^{-1} z) \text{ with ROC } R_y= |a|R_x}
$$

The proof of this property is as follows:
If a sequence $x[n]$ is multiplied by a complex exponential $a^n$ the resulting ZT $Y(z)$ can be obtained by first combining the parameter $a^{-1}$ and the variable $z$  resulting in a scaled version of $X(z)$:

$$
\begin{eqnarray*}
y[n] = a^n x[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ
\text{ } &Y(z)&
= \sum_{n=-\infty}^{\infty} a^n x[n] z^{-n}
=\sum_{n=-\infty}^{\infty}  x[n] (a^{-1} \cdot z)^{-n}\newline
& & = X(a^{-1} z) \quad\text{ with ROC } R_y= |a|R_x
\end{eqnarray*}
$$

The resulting ROC is also scaled by the parameter $a$.

<div class="example">
  <h4> Example </h4>
  <hr>
  The ZT and ROC of the unit step function $x[n]=u[n]$ is as follows:
  $$
  \begin{eqnarray*}
  x[n]=u[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(z)= \sum_{n=0}^{\infty}  z^{-n}
  \overset{{\color{red}{|z|>1}}}{=} \frac{1}{1- z^{-1}} \hspace{2mm} \text{ } {\color{red}{{R_x: |z|>1}}}
  \end{eqnarray*}
  $$
  Calculate the ZT and its ROC of the scaled version $y[n]=a^n u[n]$ of the unit step function.
  <button class="collapsible">Show solution</button>
  <div class="content">
    Evaluating the ZT of the scaled version $y[n]$ via the property  leads to the following complex function $Y(z)$  from which the ROC is outside a circle with radius $a$.
    \begin{eqnarray*}
    y[n] = a^n x[n]  &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& Y(z) = X(a^{-1} z )
    = \frac{1}{1- (a^{-1} z)^{-1}} \\
    &&= \frac{1}{1- a z^{-1}}
    \text{ } {\color{red}{R_y: |z|>|a|}}
    \end{eqnarray*}
    Verifying this result by applying the ZT to the sequence $y[n]=a^n u[n]$ leads indeed to the same result $Y(z)$  with the same ROC as follows from the following equations:
    \begin{eqnarray*}
    \text{via ZT of } y[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& Y(z) =\sum_{n=0}^{\infty} a^n z^{-n}
    \overset{{\color{red}|z|>|a|}}{=} \frac{1}{1- a z^{-1}}
    \text{ } {\color{red}{R_y: |z|>|a|}}
    \end{eqnarray*}
    Finally, as a special case note that if $x[n]$ is multiplied by a complex exponent $e^{jn \theta_0}$:
    $$
    e^{jn \theta_0} x[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(e^{-j\theta_0} z)
    $$
    which corresponds to a rotation of the $z$-plane
  </div>
</div>

<br></br>
## Property: Convolution Theorem
Perhaps the most important ZT property is the convolution theorem, which states that convolution in time domain is mapped to multiplication in $z$ domain.

$$
\boxed{x[n] \star y[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(z) \cdot Y(z)
\hspace{3mm} \text{with } R_w=R_x \cap R_y}
$$

The proof of this property is shown in the following steps:
First write out the convolution sum and transform to the $z$-domain.

$$
\begin{eqnarray*}
w[n]= x[n] \ast y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & W(z) =
\sum_{n=-\infty}^{\infty}\left ( \sum_{p=-\infty}^{\infty} x[p] y[n-p] \right ) z^{-n}
\end{eqnarray*}
$$

In the next step change the order of the two summations  and then add an extra exponent $z^{-p}$ in the first summation  which has to be compensated this in the second summation:

$$
\begin{eqnarray*}
W(z) &=& \sum\_{p=-\infty}^{\infty} x[p] \left\\{ \sum\_{n=-\infty}^{\infty} y[n-p] z^{-n} \right\\} \newline
&=& \sum\_{p=-\infty}^{\infty} x[p] z^{-p} \cdot \left\\{
\sum\_{n=-\infty}^{\infty} y[n-p] z^{-(n-p)}  \right\\}
\end{eqnarray*}
$$

The first summation is the ZT of the sequence $x[n]$ and the second summation between large brackets is the ZT of the sequence $y[n]$ , which finalizes the proof.

$$
\begin{eqnarray*}
W(z)&=& X(z) \cdot Y(z) \hspace{3mm} \text{with } R_w=R_x \cap R_y
\end{eqnarray*}
$$

The ROC of the result $W(z)$ of the convolution property includes the intersection of the ROC's of $X(z)$ and $Y(z)$. However, the ROC $R_w$ may be larger, if there is a pole-zero cancellation in the product $X(z) \cdot Y(z)$.

<div class="example">
  <h4> Example </h4>
  <hr>
  Calculate the convolution result of the two finite length sequences:
  $$
  \begin{eqnarray*}
  x[n]= \delta[n] + 2 \delta[n-1] & \text{and} & y[n]=\delta[n] + \delta[n-1]
  \end{eqnarray*}
  $$
  Calculate first the result via the convolution procedure and verify this result via the convolution property of the ZT.
  <button class="collapsible">Show solution</button>
  <div class="content">
    Both $x$ and $y$ are finite length sequences  and the convolution result $w[n]$ is a finite length sequence which consists of 3 delta pulse with coefficients ${\bf 1}$, ${\color{red}{3}}$ and ${\color{green}{2}}$ respectively.
    $$
    \begin{eqnarray*}
    w[n]=x[n] \ast y[n] &=&= {\bf 1} \delta[n] + {\color{red}{{\bf 3}}} \delta[n-1] + {\color{green}{{\bf 2}}} \delta[n-3]
    \end{eqnarray*}
    $$
    The ZT of the two sequences is as follows:
    $$
    \begin{eqnarray*}
    x[n]= \delta[n] + 2 \delta[n-1] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(z) = 1 + 2z^{-1}\newline
    y[n]=\delta[n] + \delta[n-1] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& Y(z)=1 + z^{-1}
    \end{eqnarray*}
    $$
    Multiplying these two polynomials results in a finite length polynomial with
    coefficients ${\bf 1}$, ${\color{red}{3}}$ and ${\color{green}{2}}$, which is indeed the ZT of the convolution result $w[n]$.
    $$
    \begin{eqnarray*}
    W(z)=X(z) \cdot Y(z) &=&
    = (1 + 2z^{-1}) \cdot (1 + z^{-1})
    = {\bf 1} + {\color{red}{\bf 3}} z^{-1} + {\color{green}{\bf 2}} z^{-2}
    \end{eqnarray*}
    $$
    Finally the ROC of the result $W(z)$ of the convolution theorem includes the intersection of the ROC's of $X(z)$ and $Y(z)$.
  </div>
</div>

<div class="example">
  <h4> Example </h4>
  <hr>
  Calculate the ROC of $x[n] \star y[n]$ with $x[n]= a^n u[n]$ and $y[n]=\delta[n] - a \delta[n-1]$.
  <button class="collapsible">Show solution</button>
  <div class="content">
    $$
    \begin{eqnarray*}
    x[n]= a^n u[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(z) = \frac{1}{1 - a z^{-1}} \hspace{3mm} \text{with }R_x \text{ : }|z| > |a|\\
    y[n]=\delta[n] - a \delta[n-1] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& Y(z) = 1 - a z^{-1} \hspace{3mm} \text{with }R_y \text{ : }|z| > 0
    \end{eqnarray*}
    $$
    In this example the ZT $X(z)$ of the infinite length exponential decaying sequence $x[n]$ has one pole at $z=a$ and the ROC contains all complex variables $z$ outside a circle with radius $a$. The ZT $Y(z)$ of the finite length sequence $y[n]$ has one zero at $z=a$ and the ROC contains all complex variables $z$ except $z=0$.
    $$
    \begin{eqnarray*}
    W(z) = X(z) \cdot Y(z) = \frac{1}{1 - a z^{-1}} \cdot (1 - a z^{-1} ) = 1
    \hspace{3mm} \text{with }R_w \text{ : all } z
    \end{eqnarray*}
    $$
    The ZT of the convolution of $x[n]$ with $y[n]$ is $W(z)=X(z) \cdot Y(z)$, which, due to the pole-zero cancellation, has a ROC that is the entire $z$-plane.
  </div>
</div>

<br></br>
## Property: Conjugation
$$
\boxed{x^\ast[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X^\ast(z^\ast) \text{ ; } R_x}
$$
As a corollary, note that if $x[n]$ is real-valued, $y[n]=x^\ast[n]=x[n]$, then $X(z)=X^\ast(z^\ast)$ is such as case.

The proof of the conjugation property goes as follows:

The ZT  of the complex conjugate of the sequence $x[n]$  can be rewritten by taking the complex conjugation operation outside the brackets and interchange in the exponents of the variable $z$  which leads to the final result.
$$
\begin{eqnarray*}
y[n] = x^\ast[n]
\text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } & Y(z)& = \sum_{n=-\infty}^{\infty} x^\ast[n] z^{-n}
= \left ( \sum_{n=-\infty}^{\infty} x[n] \{z^{-n}\}^{\ast} \right )^\ast\newline
&&= \left ( \sum_{n=-\infty}^{\infty} x[n] \{z^{\ast}\}^{-n} \right )^\ast
= X^\ast(z^\ast) \text{ ; } R_y=R_x
\end{eqnarray*}
$$
The ROC is not influenced by the complex operation.

<div class="example">
  <h4> Example </h4>
  <hr>
  Calculate the ZT of the sequence $\left ( e^{-j\theta_0}\right )^n u[n]$.
  <button class="collapsible">Show solution</button>
  <div class="content">
    From the table with ZT-pairs it follows that $a^n u[n] \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ 1/(1-az^{-1})$ $\rightarrow$:
    $$
    \begin{eqnarray*}
    x[n]= \left ( e^{j\theta_0}\right )^n u[n]
    & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(z) = \frac{1}{1 - e^{j\theta_0} z^{-1} }
    \end{eqnarray*}
    $$
    With $y[n]=x^\ast[n]$ ,we can find the result $Y(z)$ by using the conjugation property as follows:
    $$
    \begin{eqnarray*}
    Y(z)=X^\ast(z^\ast)&=& \left \{ \frac{1}{1 - e^{j\theta_0} (z^\ast)^{-1} } \right \}^\ast
    =\left \{ \frac{1}{1 - e^{j\theta_0} (z^{-1})^{\ast} } \right \}^\ast \newline
    &=& \frac{1}{1 - e^{-j\theta_0} z^{-1} }
    \end{eqnarray*}
    $$
  </div>
</div>


<br></br>
## Property: Derivative
$$
\boxed{n \cdot x[n] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } -z \frac{\text{d}}{\text{d} z} X(z) \text{ ; } R_x}
$$

The proof of this property goes as follows:

The ZT  of the sequence $n \cdot x[n]$  can be pre-multiplied with $z$, which has to be compensated inside the summation:
$$
\begin{eqnarray*}
y[n] = n \cdot x[n] &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & Y(z)=\sum\_{n=-\infty}^{\infty} n \cdot x[n]  z^{-n}
=z \sum\_{n=-\infty}^{\infty} \left\\{ n \cdot x[n] z^{-n-1} \right\\}
\end{eqnarray*}
$$
The function in between brackets can be rewritten as a differentiation, which can be taken outside the summation, because of linearity, which leads to the final result:
$$
\begin{eqnarray*}
Y(z)& =&
=z  \sum_{n=-\infty}^{\infty}\left\\{ -\frac{\text{d}}{\text{d} z}  x[n] z^{-n} \right\\}
=-z \frac{\text{d}}{\text{d} z} \left( \sum_{n=-\infty}^{\infty}x[n] z^{-n} \right)
= -z \frac{\text{d}}{\text{d} z} X(z)
\end{eqnarray*}
$$
The ROC is not influenced.

<div class="example">
  <h4> Example </h4>
  <hr>
  Calculate the ZT of $y[n] = n a^n u[n]$.
  <button class="collapsible">Show solution</button>
  <div class="content">
    The sequence $y[n]$ is $n$ times the exponential decaying sequence $a^n u[n]$.  From the derivative property it follows that we can find the ZT $Y(z)$ of $y[n]$ as follows:
    $$
    \begin{eqnarray*}
    Y(z) & =& -z \frac{\text{d}}{\text{d} z} \left(
    \frac{1}{1-a z^{-1}}\right)
    = -z \left\{ \frac{- a z^{-2}}{(1-a z^{-1})^2} \right\}
    = \frac{a z^{-1}}{(1-a z^{-1})^2}
    \end{eqnarray*}
    $$
  </div>
</div>


## Property: Initial value
When the sequence $x[n]=0$ for $n<0$,  the initial value $x[0]$ may be found from the ZT $X(z)$  by taking the limit  for $z$ to infinity:
$$
\boxed{x[0] = \lim_{z \rightarrow \infty} \left \\{ X(z) \right \\}}
$$
The proof goes as follows with $x[n]=0$ for $n<0$:
$$
\begin{eqnarray*}
\lim_{z \rightarrow \infty} \left\\{ X(z) \right\\}
&=& \lim_{z \rightarrow \infty}  \left\\{ \sum\_{n=-\infty}^{\infty} x[n] z^{-n} \right\\} \newline
&=&\lim_{z \rightarrow \infty} \left\\{
\cdots x[-1] z  + x[0] + x[1] z^{-1} + \cdots \right\\}\newline
&=& \lim_{z \rightarrow \infty} \left\\{ 0 + x[0] + x[1] z^{-1} + \cdots \right\\} =x[0]
\end{eqnarray*}
$$
This initial value property can be shown in the following example:

<div class="example">
  <h4> Example </h4>
  <hr>
  Calculate the initial value $x[0]$ of the sequence  $x[n] = a^n u[n]$ via the initial value property of the ZT.
  <button class="collapsible">Show solution</button>
  <div class="content">
    The given ZT $X(z)$  is related to the exponential decaying function $x[n]$  from which it is clear that the initial value $x[0]=1$.
    $$
    \begin{eqnarray*}
    X(z) = \frac{1}{1-az^{-1}}
    & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x[n] = a^n u[n]
    \quad \rightarrow \quad x[0]=1
    \end{eqnarray*}
    $$
    The same result can be found via the initial value property as follows:
    $$
    \lim_{z \rightarrow \infty} \left\{ X(z) \right\}
    =\lim_{z \rightarrow \infty} \left\{ \frac{1}{1-az^{-1}} \right\} = 1
    $$
  </div>
</div>


## One sided Z-Transform
The ZT $X(z)$ of the sequence $x[n]$, as discussed before, is the two-sided ZT.  The one-sided ZT $\tilde{X}(z)$ is defined by the given equation in which the summation index $n$ does not start from $n=-\infty$ but from $n=0$.
\begin{equation*}
\boxed{\tilde{X}(z)=\sum_{{\color{red}{n=0}}}^{\infty} x[n] z^{-n}}
\end{equation*}
Most of the properties of the one-sided ZT are the same as the properties of the two-sided ZT. One that is different, however, is the shift property.
Specifically, if the sequence $x[n]$ has a one-sided ZT $\tilde{X}(z)$, the difference of the one-sided ZT of the shifted sequence $x[n-k]$ is represented in red in the following shift property of the one-sided ZT:
$$
\boxed{x[n-k] \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } {\color{red}{\sum_{p=-k}^{-1} x[p] z^{-(p+k)}}} +  z^{-k} \cdot   \tilde{X}(z)}
$$
For the proof of this property we apply the one-sided ZT to the shifted sequence $x[n-k]$ and then substitute a new variable $p$ for $n-k$, which finalizes the proof:
$$
\begin{eqnarray*}
x[n-k] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \sum_{n=0}^{\infty} x[n-k] z^{-n}
\overset{p=n-k}{=\\!=\\!=\\!=}
\sum_{p=-k}^{\infty} x[p] z^{-(p+k)} \newline
& & = {\color{red}{\sum_{p=-k}^{-1} x[p] z^{-(p+k)}}}  +  z^{-k} \cdot \left( \sum_{p=0}^{\infty} x[p] z^{-p} \right)
\end{eqnarray*}
$$
It is this shifting property that makes the one-sided ZT useful for solving Difference Equations with initial conditions, as can be shown by the following example.

<div class="example">
  <h4> Example </h4>
  <hr>
  Consider the linear constant Difference Equation $y[n]=\frac{1}{4} y[n-2] + x[n]$. Find the solution for this equation assuming $x[n]=\delta[n-1]$.
  First use the ZT for the case $y[n]=0$ for $n < 0$ and then use the one sided ZT shift property for the case $y[-2]=y[-1]=1$.  <button class="collapsible">Show solution</button>
  <div class="content">
    $\bullet \underline{{\color{blue}{\text{Case $y[n]=0$ for $n < 0$}}}} \rightarrow \textbf{ Use ZT}$:
    <p></p>
    In case the initial conditions are zero, we can use the usual ZT.  Together with the ZT  of $x[n]=\delta[n-1]$  this leads to the given fraction. This fraction can be expanded as a sum of two terms  which are related to the given sum of two exponential decaying sequences.
    $$
    \begin{eqnarray*}
    Y(z) &=& \frac{1}{4} z^{-2} \cdot Y(z) + X(z)
    \hspace{5mm} \text{ with} \hspace{5mm} X(z)=z^{-1} \quad \rightarrow
    \end{eqnarray*}
    $$
    $$
    \begin{eqnarray*}
    Y(z)= \frac{z^{-1}}{1 - \frac{1}{4} z^{-2}} =
    \frac{1}{1-\frac{1}{2} z^{-1}} - \frac{1}{1+\frac{1}{2} z^{-1}} &&\newline
    \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ }
    y[n]=  \left (\left ( \frac{1}{2} \right )^n - \left ( -\frac{1}{2} \right )^n \right ) \cdot u[n] &&
    \end{eqnarray*}
    $$
    <p></p>
    $\bullet \underline{{\color{blue}{\text{Case $y[-2]=y[-1]=1$}}}} \rightarrow \textbf{ Use one-sided ZT:}$
    <p></p>
    In case the initial conditions are nonzero, for example $y[-2]=y[-1]=1$ we have to use the one-sided ZT to solve the Difference Equation.  The one-sided ZT $\tilde{X}(z)$ of $x[n]=\delta[n-1]$ is the same as the ZT $X(z)$ which is equal to $Z^{-1}$.  Using this together with the shift property of the one-sided ZT  results in the given fraction,  which can be expanded as a sum of two terms which are related to the given sum of two weighted exponential decaying sequences.
    $$
    \begin{eqnarray*}
    \tilde{Y}(z) & =&  \frac{1}{4}\cdot \left ( {\color{red}y[-2] + y[-1] z^{-1}} + z^{-2} \cdot \tilde{Y}(z) \right ) + \tilde{X}(z)
    \end{eqnarray*}
    $$
    $$
    \begin{eqnarray*}
    \rightarrow \hspace{2mm}
    \tilde{Y}(z) &=& \frac{\frac{1}{4} + \frac{5}{4} z^{-1}}{1 - \frac{1}{4} z^{-2}}= \frac{\frac{11}{8}}{1-\frac{1}{2} z^{-1}} - \frac{\frac{9}{8}}{1+\frac{1}{2} z^{-1}} \newline
    \tilde{Y}(z)& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
    y[n]=  \left ( {\color{red}{\frac{11}{8}}} \left( \frac{1}{2} \right )^n - {\color{red}{\frac{9}{8}}} \left ( -\frac{1}{2} \right )^n \right ) \cdot u[n]
    \end{eqnarray*}
    $$
    The influence of the initial conditions is reflected by the two weights denoted in red.
  </div>
</div>
