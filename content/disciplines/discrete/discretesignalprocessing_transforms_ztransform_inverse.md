+++
title = "The inverse Z-transform"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Inverse Z-transform"
  weight = 3
  parent = "Transforms IV: Z-transform"


+++


## Inverse Z-Transform
The ZT is a useful tool in linear signals and systems analysis. However, just as important as techniques for finding the ZT of a sequence are methods that may be used to invert the ZT.

Before deriving an expression of the formal definition of the Inverse Z-Transform (abbreviated by IZT), we will first describe three possible methods for its computation.



## IZT Method 1: Table Lookup
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/yId3JnwpgyQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

The first method to calculate the IZT of a sequence is by using a table with known ZT pairs. An example of such a table with most common ZT pairs is as follows:

<table style="width:100%">
  <tr>
    <th> Sequence </th>
    <th> $Z$-transform </th>
    <th> ROC </th>
  </tr>
  <tr>
    <td> $\delta[n]$ </td>
    <td> 1 </td>
    <td> all $z$ </td>
  </tr>
  <tr>
    <td> $\delta[n-i]$ </td>
    <td> $z^{-i}$ </td>
    <td> $z \neq 0, \infty$ </td>
  </tr>
  <tr>
    <td> $a^n u[n]$ </td>
    <td> $\frac{1}{1 - a z^{-1}}$ </td>
    <td> $|z| > |a|$ </td>
  </tr>
  <tr>
    <td> $-a^n u[-n-1]$ </td>
    <td> $\frac{1}{1 - a z^{-1}}$ </td>
    <td> $|z| < |a|$ </td>
  </tr>
  <tr>
    <td> $n a^n u[n]$ </td>
    <td> $\frac{a z^{-1}}{(1 - a z^{-1})^2}$ </td>
    <td> $|z| > |a|$ </td>
  </tr>
  <tr>
    <td> $-n a^n u[-n-1]$ </td>
    <td> $\frac{a z^{-1}}{(1 - a z^{-1})^2}$ </td>
    <td> $|z| < |a|$ </td>
  </tr>
  <tr>
    <td> $a^n \cos (n \theta_0 ) u[n]$ </td>
    <td> $\frac{1 - a z^{-1} \cos (\theta_0)}{1 - 2 a z^{-1} \cos (\theta_0) + a^2 z^{-2}}$ </td>
    <td> $|z| > |a|$ </td>
  </tr>
  <tr>
    <td> $a^n \sin (n \theta_0 ) u[n]$ </td>
    <td> $\frac{a z^{-1} \sin (\theta_0)}{1 - 2 a z^{-1} \cos (\theta_0) + a^2 z^{-2}}$ </td>
    <td> $|z| > |a|$ </td>
  </tr>
  <tr>
    <td> $a^n \sin (n \theta_0 + \phi) u[n]$ </td>
    <td> $\frac{\sin (\phi)+ a z^{-1} \sin (\theta_0 - \phi)}{1 - 2 a z^{-1} \cos (\theta_0) + a^2 z^{-2}}$ </td>
    <td> $|z| > |a|$ </td>
  </tr>
</table>

Together with these ZT pairs and ZT properties, most IZT of interest may easily be calculated.


<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT of $X_0(z)=\sum_{i=-N}^{N} z^{-i}$
  <button class="collapsible">Show solution</button>
  <div class="content">
    From the table it follows that the IZT of a term $z^{-i}$ is a shifted delta function $\delta[n-i]$ in time domain. Applying this for each term of $X_0(z)$ results in the non-causal sequence $x_0[n]$.
    $$
    X_0(z)=\sum_{i=-N}^{N} z^{-i} \quad \overset{\text{IZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \quad x_0[n] = \sum_{i=-N}^{N} \delta[n-i]
    $$
  </div>
</div>

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT of
  $$
  X_1(z)= \frac{1}{(1+ \frac{1}{3}z^{-1})^2} \hspace{5mm} \text{ROC }|z| > \frac{1}{3}
  $$
  From the table we find the following pair $X(z)$ and $x[n]$ in which the expression of $X(z)$ looks almost the same as $X_1(z)$:
  $$\begin{eqnarray*}
  X(z)=\frac{a z^{-1}}{(1 - a z^{-1})^2} & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x[n]=n a^n u[n] \hspace{5mm} \text{ ROC } |z| > |a|
  \end{eqnarray*}$$
  The equivalence becomes better when scaling $X(z)$ with $\frac{1}{a}$ and pre-multiplying with $z$.
  $$\begin{eqnarray*}
  \frac{1}{a} z  X(z)  & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{1}{a} \cdot x[n+1]= \frac{1}{a} \cdot (n+1) a^{(n+1)} u[n+1]\\
  &&=(n+1) a^n u[n+1] =(n+1) a^n u[n]
  \end{eqnarray*}$$
  The scaling factor in time domain is the same as in $z$-domain, while pre-multiplying the function $X(z)$ with $z$ results in a shift by $+1$ sample. Furthermore, the factor $\frac{1}{a}$ can be combined with $a^{n+1}$  Finally, the unit step function $u[n+1]$ starts at index $n=-1$, but for $n=-1$ the term $(n+1)$ is equal to zero.  Thus the unit step function can start with index $n=0$, which is represented by $u[n]$.  With parameter $a=-\frac{1}{3}$ we find the IZT of the function $X_1(z)$ resulting in the sequence $x_1[n]$:
  $$
  X_1(z)
  \quad \overset{\text{IZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \quad x_1[n] = (n+1) \left ( - \frac{1}{3} \right ) ^n u[n]
  $$
  </div>
</div>

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT of
  $$
  X_2(z) = \frac{1 + \frac{2}{3}z^{-1}}{1 - \frac{2}{3} z^{-1} + \frac{4}{9}z^{-2}}\hspace{5mm} \text{ROC }|z| > \frac{2}{3}
  $$
  <button class="collapsible">Show solution</button>
  <div class="content">
  From the table we find the following ZT pair, which looks similar to $X_2(z)$. With ROC $|z| > |a|$:
  $$\begin{eqnarray*}
  \frac{A \sin (\phi)+ A \cdot a z^{-1} \sin (\theta_0 - \phi)}{1 - 2 a z^{-1} \cos (\theta_0) + a^2 z^{-2}}
  & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & A \cdot a^n \sin (n \theta_0 + \phi) u[n]
  \end{eqnarray*}$$
  Comparing $X_2(z)$ with this expression results in the following set of 4 equations with 4 unknown parameters:
  $$
  \begin{array}{lcl}
  A \sin (\phi) &=&1 \\
  A \cdot a \sin (\theta_0 - \phi)&=& \frac{2}{3}\\
  2 a \cos (\theta_0) &=& \frac{2}{3}\\
  a^2 &=& \frac{4}{9}
  \end{array}
  \quad  \Rightarrow \quad
  \begin{array}{lcl}
  a &=& \frac{2}{3} \newline
  \theta_0 &=& \frac{\pi}{3}\\
  A &=& 2\\
  \phi &=& \frac{\pi}{6}
  \end{array}
  $$
  which can be solved resulting in the given numbers. Using these numbers results in the following expression for the sequence $x_2[n]$ which is the IZT of $X_2(z)$:
  $$\begin{eqnarray*}
  X_2(z) = \frac{1 + \frac{2}{3}z^{-1}}{1 - \frac{2}{3} z^{-1} + \frac{4}{9}z^{-2}}&
  \overset{\text{IZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} &
  x_2[n]= 2 \left ( \frac{2}{3} \right ) ^n  \sin(n \frac{\pi}{3} + \frac{\pi}{6}) u[n]
  \end{eqnarray*}$$
  </div>
</div>

## IZT Method 2: Long tail division
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/hjX3bM6khdA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

The second method to calculate the IZT of a sequence is by using
long tail division. In many practical cases $X(z)$ is rational, with numerator polynomial $N(z)$ and denominator polynomial $D(z)$,  both polynomials are nonzero, and usually the first coefficient $a_0$ is chosen as 1.
$$\begin{eqnarray*}
X(z) &=& \frac{N(z)}{D(z)} = \frac{\sum_{p=0}^{N} b_p z^{-p}}{
\sum_{p=0}^{M} a_p z^{-p}}=  \frac{\sum_{p=0}^{N} b_p z^{-p}}{
1+ \sum_{p=1}^{M} a_p z^{-p}}
\end{eqnarray*}$$
$$\begin{eqnarray*}
N \geq 0 &:& b_N \neq 0 \newline
M \geq 0 &:& M=0 \quad \Rightarrow \quad D(z)=a_0
\text{ usually } a_0=1 \newline
& & M>0 \quad\Rightarrow \quad a_M \neq 0
\end{eqnarray*}$$
In the long tail division method we write the rational expression of $X(z)$ as a power series expansion.  In general, this can be achieved by applying long tail division which results in, a possible infinite length, polynomial expression in powers of $z$ with coefficients $c_k$.
$$
X(z) = \frac{N(z)}{D(z)}
\overset{\textit{Long tail division}}{=\\!=\\!=\\!=\\!=\\!=\\!=}
\sum_{k }^{} c_k z^{-k}
$$
Since $z^{-k}$ $\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ$ $\delta[n-k]$, the coefficient $c_k$ multiplying the term $z^{-k}$ is the $k^{th}$ sample of the sequence $x[n]$:
$$
X(z) = \sum_{k }^{} c_k z^{-k}
\hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm} x[n] = \sum_{k }^{} c_k \delta[n-k]
$$
The IZT $x[n]$ is a, possible infinite length, sequence of samples with weights $c_k$.


<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT of $X_2(z)$ with long tail division and compare the result with the result obtained by using the Table Lookup method
  <button class="collapsible">Show solution</button>
  <div class="content">
    Applying long tail division to the rational function $X_2(z)$ results in an infinite long polynomial expression with powers of $z$. All powers of $z$ are smaller or equal than zero.
    $$
    X_2(z) = \frac{1 + \frac{2}{3}z^{-1}}{1 - \frac{2}{3} z^{-1} + \frac{4}{9}z^{-2}}
    = 1 + {\bf \frac{4}{3}} z^{-1} + {\color{red}{\frac{4}{9}}} z^{-2}- {\color{green}{\frac{8}{27}}} z^{-3}- {\color{blue}{\frac{32}{81}}} z^{-4} + \cdots
    $$
    From the, infinite length, polynomial expression of $X_2(z)$, we can simply obtain the time domain sequence, which is denoted by $\tilde{x}_2[n]$.
    $$
    X_2(z) \quad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  \quad\hspace{2mm} \tilde{x}_2[n]= 1 + {\bf \frac{4}{3}} \delta[n-1] + {\color{red}{\frac{4}{9}}} \delta[n-2] - {\color{green}{\frac{8}{27}}} \delta[n-3] - {\color{blue}{\frac{32}{81}}} \delta[n-4]  + \cdots
    $$
    Each coefficient of the term $\delta[n-p]$ is the same as the weight of the term $z^{-p}$ of the polynomial expression of $X_2(z)$.
    <br></br>
    <i> Notes:</i>
    <p></p>
    It can be shown that for $p > 1$, the weight of the $p^{th}$ element $z^{-p}$ equals
    $\pm (\frac{2}{3})^p$.  This implies that all terms of the polynomial $X_2(z)$ will converge for all values of $|z| > \frac{2}{3}$. In other words the ROC is outside a circle with radius $\frac{2}{3}$.  Thus the unit circle is inside the ROC of $X_2(z)$, and so the FTD of the, infinite long, sequence $\tilde{x}_2[n]$ exist. Finally, although the expression for $x_2[n]$, as found by the Table Lookup method, and the sequence $\tilde{x}_2[n]$ look different, they both represent the same, infinite length, right sided causal sequence of samples, thus $\tilde{x}_2[n]=x_2[n]$, $\forall$ $n$
  </div>
</div>


### Long tail division: Both $N(z),D(z)$ descending order
The long tail division can be performed in different ways, resulting in different polynomial expressions.  In this first approach both numerator and denominator polynomials are represented in descending order:
$$\begin{eqnarray*}
X(z) &=& (b_0 + b_1 z^{-1} + \cdots + b_N z^{-N}) \cdot \left ( \frac{1}{a_0 + a_1 z^{-1} + \cdots + a_M z^{-M}}\right ) \newline
&=&\left ( \sum_{p=0}^{N} b_p z^{-p} \right ) \cdot \left (\frac{1}{\sum_{p=0}^{M} a_p z^{-p}}\right )
\end{eqnarray*}$$
Applying long tail division to the second term results in an infinite long polynomial from which all powers of the variable $z$ are negative or zero.  The weights of these terms are denoted by $\tilde{a}_k$.
$$\begin{eqnarray*}
X(z) &=&\left ( \sum_{p=0}^{N} b_p z^{-p} \right )
\cdot \left ( \sum_{k=0}^{\infty} \tilde{a}_k z^{-k} \right )
= \sum_{k=0}^{\infty} c_k z^{-k}
\end{eqnarray*}$$
Multiplying this infinite long polynomial  with the numerator polynomial results in an infinite long polynomial with powers of the variable $z$ which are all smaller or equal to zero, from which the weights are denoted by $c_k$. From the fact that the resulting polynomial contains only negative powers of $z$, the ROC is outside a circle with radius $r$. It can be shown that this radius $r$ depends on the values of $\tilde{a}_k$.

The IZT of the rational function $X(z)$ results in the sequence $x[n]$, which is a right sided causal sequence  from which the FTD exist when the value of radius $r$ is smaller than one.
$$\begin{eqnarray*}
X(z)=\frac{N(z)}{D(z)}=\sum_{k=0}^{\infty} c_k z^{-k} & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x[n] =\sum_{k=0}^{\infty} c_k \delta[n-k]
\end{eqnarray*}$$

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT and the ROC of $X_3(z)= \frac{1}{1-\frac{1}{3}z^{-1}}$ via the descending ordered long tail division method.
  <button class="collapsible">Show solution</button>
  <div class="content">
    The long tail division results in an infinite length
    summation, which is convergent when the argument $\frac{1}{3} z^{-1}$ is smaller than 1.
    $$\begin{eqnarray*}
    X_3(z)= \frac{1}{1-\frac{1}{3}z^{-1}}
    &\overset{\color{red}{\text{ROC}}}{\underset{\color{red}{|z| > \frac{1}{3}}}{===}}& \sum_{p=0}^{\infty} \left ( \frac{1}{3} z^{-1}\right )^p
    =\sum_{p=0}^{\infty} \left ( \frac{1}{3} \right )^p z^{-p}
    \newline
    & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  x_3[n]= \sum_{p=0}^{\infty} \left ( \frac{1}{3} \right )^p \delta[n-p]
    \end{eqnarray*}$$
    This implies that the ROC is outside a circle with radius $\frac{1}{3}$.  Writing this expression as an infinite length polynomial with powers of $z$ that are zero or negative, it follows that the IZT is given by $x_3[n]$  which is a right-sided causal sequence from which the FTD exist.
  </div>
</div>

### Long tail division: Both $N(z),D(z)$ ascending order

When representing both numerator and denominator polynomials in ascending order,  which writes in short hand notation as the given product,  we first divide the numerator by $z^{-N}$ and the denominator by $z^{-M}$ .
$$\begin{eqnarray*}
X(z) &=& (b_N z^{-N} + \cdots + b_1 z^{-1} + b_0) \cdot \left ( \frac{1}{a_M z^{-M} + \cdots + a_1 z^{-1} + a_0}\right )\newline
&=& \left ( \sum_{q=0}^{N} b_{N-q} z^{-N+q} \right ) \cdot \left (\frac{1}{\sum_{q=0}^{M} a_{M-q} z^{-M+q}}\right )\newline
&=& \left ( z^{-N} \cdot \sum_{q=0}^{N} b_{N-q} z^{q} \right ) \cdot \left ( z^{M} \cdot \frac{1}{\sum_{q=0}^{M} a_{M-q} z^{q}}\right )
\end{eqnarray*}$$
These two components  can be combined into a term $z^{M-N}$ and  the first summation can be copied.  Applying long tail division to the second term, results in an infinite long polynomial containing powers of $z$ which are all greater or equal to zero, from which the weights are denoted by $\hat{a}_k$ as follows:
$$\begin{eqnarray*}
X(z) &=& z^{M-N}
\cdot \left ( \sum_{q=0}^{N} b_{N-q} z^{q} \right )
 \cdot \left (\sum_{k=0}^{\infty} \hat{a}_k z^{k} \right )
= z^{M-N} \cdot \sum_{k=0}^{\infty} d_k z^k
\end{eqnarray*}$$
The resulting polynomial writes as an infinite length  polynomial in $z$ with exponents that are greater or equal than zero. The weights of this polynomial are denoted by $d_k$ and it is pre-multiplied with $z^{M-N}$.  From the fact that the resulting polynomial contains only positive powers of $z$, it follows that the ROC is inside a circle with radius $r$. It can be shown that this radius $r$ depends on the values of the weights $\hat{a}_k$.
$$\begin{eqnarray*}
X(z)=\frac{N(z)}{D(z)}=z^{M-N} \cdot \sum_{k=0}^{\infty} d_k z^{k} & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x[n] =\sum_{k=0}^{\infty} d_k \delta[n+(M-N)+k]
\end{eqnarray*}$$
The IZT now results in the sequence $x[n]$,  which is a left sided sequence which is partially causal. The sequence $x[n]$ has a causal part when the order $N$ of the numerator is larger than the order $M$ of the denominator. Finally, depending on the value of the radius $r$, the FTD  exist.

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT and the ROC of $X_4(z)= \frac{1}{-3z^{-1}+1}$ via the ascending ordered long tail division method.
  <button class="collapsible">Show solution</button>
  <div class="content">
    In order to obtain only positive powers of $z$ we first divide the denominator by $-3z^{-1}$:
    $$\begin{eqnarray*}
    X_4(z)&=& \frac{1}{-3z^{-1}+1}= \frac{1}{ -3z^{-1} } \cdot \frac{1}{1 - \frac{1}{3} z}
    \end{eqnarray*}$$
    Applying long tail division to 1 divided by $1-\frac{1}{3} z$ results in an infinite convergent series for all $z$ within a circle of radius smaller than 3:
    $$\begin{eqnarray*}
    X_4(z)
    &\overset{\color{red}{\text{ROC}}}{\underset{\color{red}{|z| < \frac{1}{3}}}{===}}&
    \left ( - \frac{1}{3} z \right ) \cdot \sum_{p=0}^{\infty} \left (\frac{1}{3}z \right )^{p}
    \end{eqnarray*}$$
    The two terms can be combined
    $$\begin{eqnarray*}
    X_4(z)&= & - \sum_{{\bf {\color{red}{p=1}}}}^{\infty} \left ( \frac{1}{3} \right )^k z^p
    \end{eqnarray*}$$
    The IZT results in the infinite length $x_4[n]$  which is a left sided non causal sequence  from which the FTD exist:
    $$\begin{eqnarray*}
    X_4(z)
    & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x_4[n] = - \sum_{{\bf {\color{red}{p=1}}}}^{\infty} \left ( \frac{1}{3}\right )^{p} \delta[n+p]
    \end{eqnarray*}$$
  </div>
</div>

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT and the ROC of $X_5(z) = \frac{-z^{-2}+1}{- 2 z^{-1}+1}$ via the ascending ordered long tail division method.
  <button class="collapsible">Show solution</button>
  <div class="content">
    All intermediate steps are as follows:
    $$\begin{eqnarray*}
    X_5(z) &=& \frac{-z^{-2}+1}{- 2 z^{-1}+1}
    =\frac{-z^{-2}+1}{- 2 z^{-1}( 1 - \frac{1}{2} z)}\\
    &=&
    \left ( -z^{-2}+1 \right ) \cdot \left ( -\frac{1}{2} z  \cdot \frac{1}{1 - \frac{1}{2} z}\right )\\
    &\overset{{\color{red}{|z|< 2}}}{=}&
    \left ( -z^{-2}+1 \right ) \cdot \left ( - \sum_{{\bf {\color{red}{p=1}}}}^{\infty} \left ( \frac{1}{2} \right )^p z^p \right ) \\
    &=& \frac{1}{2} z^{-1} + \frac{1}{4} - \frac{3}{4} \sum_{{\bf {\color{red}{p=1}}}}^{\infty} \left ( \frac{1}{2} \right )^p z^p
    \end{eqnarray*}$$
    Since the ROC ($|z|<2$) includes the unit circle this results in the following left sided partially causal sequence $x_5[n]$ from which the FTD exist:
    $$\begin{eqnarray*}
    \Rightarrow \quad x_5[n] &=& -\frac{1}{2} \delta[n-1] + \frac{1}{4} \delta[n] - \frac{3}{4} \sum_{{\bf {\color{red}{p=1}}}}^{\infty} \left ( \frac{1}{2} \right )^p \delta[n+p]
    \end{eqnarray*}$$
  </div>
</div>


## IZT Method 3: Partial fraction
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/ZkFAgD2aGIs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

The third method to calculate the IZT of a sequence is by using
the partial fraction method. This makes use of the fundamental algebraic property that  the order $M$ polynomial of the denominator can be written as a product of $M$ first order polynomials. The roots of the denominator are called the poles of $X(z)$ and in first instance we assume simple first order poles.
$$\begin{eqnarray*}
X(z) &=& \frac{N(z)}{D(z)} = \frac{\sum_{p=0}^{N} b_p z^{-p}}{1+ \sum_{p=1}^{M} a_p z^{-p}}
= \frac{\sum_{p=0}^{N} b_p z^{-p}}{\prod_{k=1}^{M} (1 - \alpha_k z^{-1})}
\end{eqnarray*}$$
In case the order $M$ of the denominator polynomial is larger than the order $N$ of the nominator polynomial, $X(z)$ can be written as the following sum of $M$ first order terms, each weighted by scalars $A_k$.

### Case $M>N$
$$\begin{eqnarray*}
X(z) =\sum_{k=1}^{M} \frac{A_k}{1 - \alpha_k z^{-1}}
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  & x[n] =\sum_{k=1}^{M} A_k (\alpha_k)^n u[n]
\end{eqnarray*}$$
From the table with known ZT pairs it follows that the IZT of each individual first order term is an exponential decaying sequence. The sequence $x[n]$ consists of a summation of $M$ of such terms.
The weights $A_k$ can be obtained by either coefficient matching or via the so called residual approach:
$$
A_k = \left [ (1 - \alpha_k z^{-1}) X(z) \right ] \vert_{z=\alpha_k}
$$

We will show both approaches by computing the IZT of the following rational function:
$$
X_6(z) = \frac{1 + 2 z^{-1}}{1 + 0.4 z^{-1} - 0.12 z^{-2}}
$$

#### Example using coefficient matching

The first step is to spilt the second order polynomial of $X_6(z)$ into two first order polynomials.
$$\begin{eqnarray*}
X_6(z) &=&  \frac{{\color{red}{1}} + {\color{blue}{2}} z^{-1}}{(1 - 0.2 z^{-1})(1 + 0.6 z^{-1})}
\end{eqnarray*}$$
For the coefficient matching approach, we assume that $X_6(z)$ can be written as the sum of two terms, each weighted by an unknown weight $A_1$ and $A_2$ respectively.
$$\begin{eqnarray*}
X_6(z)&=& \frac{A_1}{1 - 0.2 z^{-1}} + \frac{A_2}{1 + 0.6 z^{-1}}
= \frac{{\color{red}{(A_1 + A_2)}} + {\color{blue}{( 0.6 A_1 - 0.2 A_2)}} z^{-1}}{(1 - 0.2 z^{-1})(1 + 0.6 z^{-1})}
\end{eqnarray*}$$
These two terms can be combined again into one expression, as denoted at the right hand side of the equation, which contains the unknown parameters in the numerator polynomial.
When comparing (matching) the coefficients of all terms with the original numerator polynomial results in this case in two equations with two unknowns $A_1$ and $A_2$,  which can be solved as follows:
$$
\begin{array}{lcl}
{\color{red}{A_1 + A_2}} &=& {\color{red}{1}} \newline
{\color{blue}{0.6 A_1 -0.2 A_2}} &=& {\color{blue}{2}}
\end{array}
\hspace{3mm} \Rightarrow \hspace{3mm} A_1=2.7 \text{ ; } A_2=-1.75
$$
These results can be used in the original expression of $X_6(z)$
$$\begin{eqnarray*}
X_6(z) &=&\frac{1 + 2 z^{-1}}{1 + 0.4 z^{-1} - 0.12 z^{-2}}
=  \frac{2.75}{1 - 0.2 z^{-1}} + \frac{-1.75}{1 + 0.6 z^{-1}}
\end{eqnarray*}$$
from which the IZT results into the following expression for the sequence $x_6[n]$:
$$\begin{eqnarray*}
X_6(z) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & x_6[n] = 2.75 (0.2)^n u[n] - 1.75 (-0.6)^n u[n]
\end{eqnarray*}$$

#### Example using residuals

The left hand side of the equation represents the original expression from which the denominator is split in first order terms.
$$\begin{eqnarray*}
\frac{1 + 2 z^{-1}}{(1 - 0.2 z^{-1})(1 + 0.6 z^{-1})}
&=&\frac{A_1}{1 - 0.2 z^{-1}} + \frac{A_2}{1 + 0.6 z^{-1}}
\end{eqnarray*}$$
The right hand side of the equal sign represents the two first order terms with unknown weights which can be solved via the so called residual approach:
$$
A_k = \left [ (1 - \alpha_k z^{-1}) X(z) \right ] \vert_{z=\alpha_k}
$$
This approach can be explained as follows:

From the right hand side of the representation of $X_6(z)$ it follows that the weight $A_1$ can obtained by  multiplying the right hand side  with $1-0.2 z^{-1}$ and then evaluating this result at $z=0.2$. Thus
$$\begin{eqnarray*}
\left ( 1 - 0.2 z^{-1} \right ) \cdot \left ( \frac{A_1}{1 - 0.2 z^{-1}} + \frac{A_2}{1 + 0.6 z^{-1}} \right ) =
A_1 + \frac{A_2 \cdot (1 - 0.2 z^{-1})}{1 + 0.6 z^{-1}}
\overset{z=0.2}{=} A_1
\end{eqnarray*}$$
Applying the same procedure to the left hand side of the representation of $X_6(z)$, that is first multiply with $1-0.2 z^{-1}$  and evaluating the result at $z=0.2$  leads to the value of the weight $A_1$:
$$\begin{eqnarray*}
A_1 &=& (1 - 0.2 z^{-1}) X_6(z)|_{z=0.2}
= \frac{1 + 2 z^{-1}}{1 + 0.6 z^{-1}}|_{z=0.2}
=2.75
\end{eqnarray*}$$
Applying the same procedure results in the value of the weight $A_2$:
$$\begin{eqnarray*}
A_2 &=& (1 + 0.6 z^{-1}) X_6(z)|_{z=-0.6}
= \frac{1 + 2 z^{-1}}{1 - 0.2 z^{-1}}|_{z=-0.6}
=-1.75
\end{eqnarray*}$$
Thus $X_6(z)$ can be split in two first order terms  from which the IZT lead to the same resulting sequence $x_6[n]$ as before.

### Case $M \leq N$
In case of simple poles the IZT procedure of the partial fraction method needs one extra step when the order of the denominator $M$ is smaller or equal than the order $N$ of the nominator. First split $X(z)$ by using long tail division and stop this long division procedure when the resulting rational polynomial function $F(z)$ is such that the order of the denominator is larger than the order of the nominator.
$$\begin{eqnarray*}
X(z) = \sum_{k=0}^{N-M}B_k z^{-k} + F(z)
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ  & x[n] =\sum_{k=0}^{N-M}B_k \delta[n-k] +f[n]
\end{eqnarray*}$$
The coefficients $B_k$ are calculated via the first steps of the ascended ordered long tail division method,  while the partial fraction method can be applied to the rational polynomial function $F(z)$.  The IZT results in a sequence $x[n]$ which consists of two parts: The first part is a sequence of delayed delta pulses with weights $B_k$ and the second part $f[n]$ is the IZT of $F(z)$.

<div class="example">
  <h4> Example </h4>
  <hr>
  Find the IZT of
  $$\begin{eqnarray*}
  X_7(z)&=& \frac{6 + \frac{15}{4}z^{-1} - \frac{5}{4}z^{-2} - \frac{1}{2}z^{-3}}{1 - \frac{1}{4}z^{-1} - \frac{1}{8}z^{-2}}
  \end{eqnarray*}$$
  <button class="collapsible">Show solution</button>
  <div class="content">
    In the first step we split $X_7(z)$ into two parts:
    $$\begin{eqnarray*}
    X_7(z)&=& {\color{red}{4 z^{-1} + 2}} + {\color{blue}{F(z)}}
    \hspace{3mm} \text{with } \hspace{3mm}
    {\color{blue}{F(z)}}= {\color{blue}{\frac{4 + \frac{1}{4} z^{-1}}{1 - \frac{1}{4}z^{-1} - \frac{1}{8}z^{-2}}}}
    \end{eqnarray*}$$
    The first part (in red) is obtained by applying ascending ordered long tail division. This long division procedure is stopped when the resulting rational polynomial function $F(z)$ (in blue) is such that the order of the denominator, which is 2, is larger than the order of the nominator.  In the second step we apply the partial fraction method to $F(z)$. In this case write $F(z)$ as a sum of two first order denominator polynomials and calculate the weights $A_1$ and $A_2$ via the coefficient matching or residual method  which leads to the following result:
    $$\begin{eqnarray*}
    {\color{blue}{F(z)}}&=& {\color{blue}{\frac{4 + \frac{1}{4} z^{-1}}{(1 - \frac{1}{2} z^{-1}) (1 + \frac{1}{4} z^{-1})}}} = {\color{blue}{\frac{A_1}{1 - \frac{1}{2} z^{-1}} + \frac{A_2}{1 + \frac{1}{4} z^{-1}}}}\\
    &=& {\color{blue}{\frac{3}{1 - \frac{1}{2} z^{-1}} + \frac{1}{1 + \frac{1}{4} z^{-1}}}}
    \end{eqnarray*}$$
    The sequence $x_7[n]$ consists of two parts:
    $$
    x_7[n] = {\color{red}{4\delta[n-1] + 2 \delta[n]}} + {\color{blue}{3 \left (\frac{1}{2}\right )^n u[n] + \left (-\frac{1}{4} \right )^n u[n]}}
    $$
    The first part (in red) is a sum of two delta pulses, which is clearly the IZT of the first part of $X_7(z)$. The second part (in blue)is the sum of two exponential decaying sequences which is clearly the IZT of the two first order denominator polynomials of $F(z)$.
  </div>
</div>


### Modification for multiple-order poles
Finally the partial fraction method needs to be adjusted in case of multiple order poles.
$$
X(z) = \frac{\sum_{p=0}^{N} b_p z^{-p}}{\left ( \prod_{k=1}^{M-K} (1 - \alpha_k z^{-1})\right ) \cdot \left ( 1 - \tilde{\alpha} z^{-1} \right )^K }
$$
The equation shows an example of a rational polynomial $X(z)$ in which there are $M-K$ simple poles $\alpha_k$ and one $K$ fold pole denoted by $\tilde{\alpha}$.  Depending on the order $M$ in relation to the order $N$ we can split $X(z)$ into three different parts:
$$
\boxed{X(z) = \sum_{k=0}^{N-M}B_k z^{-k} +\sum_{k=1}^{M-K} \frac{A_k}{1 - \alpha_k z^{-1}}+ \sum_{p=1}^{K} \frac{C_p}{(1 - \tilde{\alpha} z^{-1})^p}}
$$
When the order $M$ is smaller or equal to the order $N$ the first part is obtained by (ascending ordered) long tail division.  The second part, which belongs to the $M-K$ simple poles, can be written as a sum of $M-K$ first order polynomials by using coefficient matching or residuals as discussed before.  The third term consists of $K$ higher order polynomials from which the weights can be found by coefficient matching or via the given generalized equation for residuals:
$$
\boxed{
C_p  = \frac{1}{(K-p)!\cdot (-\tilde{\alpha})^{(K-p)}} \cdot
\frac{\text{d}^{K-p}}{\text{d} (z^{-1})^{K-p}}
\left [ (1-\tilde{\alpha} z^{-1})^K \cdot F(z) \right ]
\bigg\vert_{z=\tilde{\alpha}}  }
$$
This procedure will be explained by finding the IZT of the following function with one simple pole $z=\alpha_1=\frac{1}{2}$ and one second-order pole $z=\tilde{\alpha}= - \frac{1}{3}$:
$$
X_8(z) = \frac{3 + \frac{8}{3} z^{-1}}{(1-\frac{1}{2} z^{-1})(1 + \frac{1}{3} z^{-1})^2}
$$

#### Example using coefficient matching

The first step is to split the function $X_8(z)$ into the following three terms with unknown coefficients $A$, $C_1$ and $C_2$ respectively:
$$
X_8(z) =  \frac{A}{1-\frac{1}{2} z^{-1}} + \frac{C_1}{1 + \frac{1}{3} z^{-1}} + \frac{C_2}{(1 + \frac{1}{3} z^{-1})^2}
$$
Coefficient matching of the numerator results in the following three equations:
$$
3 + \frac{8}{3} z^{-1} = \left ( A + C_1 + C_2\right ) +
\left ( \frac{2}{3} A - \frac{1}{6} C_1 - \frac{1}{2} C_2 \right ) z^{-1}+
\left (  \frac{1}{9} A - \frac{1}{6} C_1\right ) z^{-2}
$$
which lead to the values for $A$, $C_1$ and $C_2$.
$$
\begin{array}{lcl}
A + C_1 + C_2 &=& 3 \newline
\frac{2}{3} A - \frac{1}{6} C_1 - \frac{1}{2} C_2  &=& \frac{8}{3} \newline
\frac{1}{9} A - \frac{1}{6} C_1 &=& 0
\end{array}
\hspace{3mm} \Rightarrow \hspace{3mm} A=3 \text{ ; } C_1=2 \text{ ; } C_2=-2
$$
The IZT of the three terms of $X_8(z)$ result  in the following sequence $x_8[n]$:
$$\begin{eqnarray*}
&&X_8(z) =\frac{3}{1-\frac{1}{2} z^{-1}} + \frac{2}{1 + \frac{1}{3} z^{-1}} - \frac{2}{(1 + \frac{1}{3} z^{-1})^2}\newline
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \hspace{2mm} x_8[n] = 3 \left ( \frac{1}{2} \right )^n u[n] + 2 \left ( -\frac{1}{3} \right )^n u[n] -2 (n+1) \left ( - \frac{1}{3} \right ) ^n u[n]
\end{eqnarray*}$$
from which the last two parts are found by using the table of ZT pairs.

#### Example using residuals

The values for $A$, $C_1$ and $C_2$ can also be found by using the general expression for the residuals.
For the first simple pole the general residual expression reduces to the expression as discussed before:
$$\begin{eqnarray*}
A &=& (1-\frac{1}{2} z^{-1}) \cdot X_8(z) \vert_{z = \frac{1}{2}}=3
\end{eqnarray*}$$
For the second order pole the general residual expression leads to the following two equations:
$$\begin{eqnarray*}
C_1 &=& \frac{1}{1/3} \cdot \frac{\text{d}}{\text{d} (z^{-1})} \left [
(1 + \frac{1}{3} z^{-1})^2 \cdot X_8(z)\right ] \vert_{z=-\frac{1}{3}} = 2 \newline
C_2 &=& (1 + \frac{1}{3} z^{-1})^2 \cdot X_8(z) \vert_{z=-\frac{1}{3}} = -2
\end{eqnarray*}$$
which leads to the same result as with the coefficient matching approach as discussed above.


## IZT Formal method
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/XJ8iA4y29yg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

In this section we will derive the formal definition of the Inverse $Z$-transform (IZT). For this let's see if we intuitively can derive the IZT from the IFTD, which is defined by the following integral:
$$\begin{eqnarray*}
\text{IFTD: } x[n] &=& \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\theta}) e^{jn \theta} \text{d} \theta
\end{eqnarray*}$$
For this intuitive derivation we replace in the IFTD definition the exponent $e^{j\theta}$ by the complex variable $z$. Differentiating the variable $z$ to the variable $\theta$ now leads to the following expression for d$\theta$:
$$
\frac{\text{d} }{\text{d} \theta } \{ z \} = j e^{j\theta} \hspace{3mm}
\Rightarrow \hspace{3mm} \text{d} \theta = \frac{1}{j} z^{-1} \text{d} z
$$
Furthermore, the integral over variable $\theta$ has to be replaced by an integral in the z plane over a closed contour on the unit circle, denoted by $|z|=1$, thus:
$$
\int_{-\pi}^{\pi}\hspace{3mm} \Rightarrow \hspace{3mm} \text{encircle unit circle counterclockwise: } \oint_{|z|=1}
$$
Using these two steps the IFTD integral can be generalized,  which can be rewritten as the following equation:
$$\begin{eqnarray*}
x[n] &=& \frac{1}{2\pi} \oint_{|z|=1} X(z) z^{n} \cdot \frac{1}{j} z^{-1} \text{d} z
= \frac{1}{2 \pi j} \oint_{{\color{red}{|z|=1}}} X(z) z^{n-1} \text{d} z
\end{eqnarray*}$$
The formal definition of the IZT is almost the same.
$$
\boxed{
x[n] = \frac{1}{2 \pi j} \oint_{{\color{red}{C}}} X(z) z^{n-1} \text{d} z }
$$
This equation represents an integral in the z plane
over a counterclockwise closed contour $C$ inside the ROC of $X(z)$ encircling the origin $z=0$.  The IZT is equivalent to the IFTD, when the IZT is evaluated on the unit circle.

In the following subsections we will derive the IZT in a more formal way, via the so called Cauchy residue theorem.

### IZT via Cauchy's residue theorem
Cauchy's residue theorem states that for a rational function $F(z)$ the integral in the $z$-plane of the function $F(z)$ over a counterclockwise closed contour $C$ can be calculated as a sum of the residues of $F(z)$ at all poles of $F(z)$ inside the closed contour $C$:
$$
\boxed{
\frac{1}{2 \pi j} \oint_{C} F(z) \text{d} z =
\sum \left [ \text{Residues $F(z)$ @} {\color{red}{\text{poles inside } C}} \right ]}
$$

The procedure to calculate the residue of $F(z)$ is as follows:
In case of a single pole at $z=z_0$ inside $C$, the residue can be found by first cancelling the pole of $F(z)$ at $z=z_0$ with a zero at $z=z_0$, that is multiply $F(z)$ with $z-z_0$, and then evaluating the result at the $z=z_0$.
$$\begin{eqnarray*}
\text{Res} \left [ F(z) \text{ @ } z=z_0 \right ] &=&  \left\\{ (z-z_0) \cdot F(z) \right\\}  \bigg\vert_{z=z_0}
\end{eqnarray*}$$
In case of a two-fold pole at $z=z_0$ inside $C$: First cancel the two-fold pole by a two-fold zero at $z=z_0$, that is multiply $F(z)$ with $(z-z_0)^2$. Then differentiate to the variable $z$ and evaluate the result at $z=z_0$.
$$\begin{eqnarray*}
\text{Res} \left [ F(z) \text{ @ } z=z_0 \right ] &=&  \frac{\text{d}}{\text{d} z} \left\\{ (z-z_0)^2 \cdot F(z) \right\\} \bigg\vert_{z=z_0}
\end{eqnarray*}$$
In general in case of a $K$-fold pole inside $C$, the procedure to calculate the residue of $F(z)$ is as follows: First cancel the $K$-fold pole by a $K$-fold zero at $z=z_0$, that is multiply $F(z)$ with $(z-z_0)^K$. Then take the $K-1$$^{th}$ differentiate and divide by $K-1$-faculty. Evaluate this result at $z=z_0$.
$$
\boxed{
\text{Res} \left [ F(z) \text{ @ } z=z_0 \right ] = \frac{1}{(K-1)!} \cdot
\frac{\text{d}^{K-1}}{\text{d} z^{K-1}} \left [ (z-z_0)^K \cdot F(z) \right ]
\bigg \vert_{z=z_0}  }
$$

#### Example

In this example we will calculate the IZT of the function $X(z)=1$ by using Cauchy's residue theorem. Applying the IZT definition to the function $X(z)=1$ leads to an integral in the $z$-plane over a counterclockwise closed contour $C$ of the function $z^{n-1}$.
$$\begin{eqnarray*}
X(z)=1 \quad \overset{\text{IZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \quad x[n] &=&
\frac{1}{2 \pi j} \oint_{C} X(z) z^{n-1} \text{d} z
=\frac{1}{2 \pi j} \oint_{C} z^{n-1} \text{d} z
\end{eqnarray*}$$
This integral can be computed for the following different cases:

When the index $n$ is larger or equal than 1 the function $z^{n-1}$ has no poles inside any closed contour $C$ and thus from Cauchy's residue theorem it follows that the result $x[n]=0$ for all indices $n \geq 1$.

<u>$\color{blue}{n = 0}$</u>:
For index $n=0$ the function $z^{n-1}$ has one poles at $z=0$. From the procedure of Cauchy's residue theorem it follows that in this case the integral results into the value 1 and thus $x[n]=1$ for index $n=0$.
$$\begin{eqnarray*}
x[n] &=& (z-0) \cdot z^{-1} \vert_{z=0} =1 \text{ for } n=0
\end{eqnarray*}$$

<u>$\color{blue}{n = -1}$</u>:
For index $n=-1$ the function $z^{n-1}$ has two poles at $z=0$.
Applying Cauchy's residue theorem  results in the value 0 and thus $x[n]=0$ for index $n=-1$.
$$\begin{eqnarray*}
x[n] &=& \frac{\text{d}}{\text{d} z} \left [ (z-0)^2 \cdot z^{-2} \right ] \vert_{z=0}
=\frac{\text{d}}{\text{d} z} \left [ 1 \right ] \vert_{z=0}  =0 \text{ for } n=-1
\end{eqnarray*}$$.

<u>$\color{blue}{n \leq -1}$</u>:
 This result can be generalized to  all indices $n \leq -1$. With $r=-n$ the function $z^{-r-1}$ has $r+1$ poles at $z=0$.  Cauchy's residual theorem results in the value 0 for this case.
$$\begin{eqnarray*}
x[n] &=&
\frac{1}{r!} \cdot
\frac{\text{d}^{r}}{\text{d} z^{r}} \left [ (z-0)^{r+1} \cdot z^{-r-1}  \right ]
\bigg \vert_{z=0}
= \frac{\text{d}^{r}}{\text{d} z^{r}} \left [ 1 \right ]
\bigg\vert_{z=0}  =0 \text{ for } n \leq -1
\end{eqnarray*}$$
Combining the results for all indices $n$ implies that $x[n]$ is always 0, except for index $n=0$.
Concluding it follows that the IZT of the function $X(z)=1$ is equal to the delta pulse $x[n]=\delta[n]$, which is known as the following so called ${\color{red}{\text{Cauchy's integral theorem}}}$:
$$
\boxed{\frac{1}{2 \pi j} \oint_{C}  z^{n-1} \text{d} z = \delta[n]}
$$
This theorem is the counterpart of the Fourier integral which states that the IFTD of the function 1 is equal to $\delta[n]$. Intuitively this can be shown by substituting for the complex variable $z$ the complex exponent $e^{j\theta}$ and evaluating the integral on the unit circle $|z|=1$  which indeed leads to the following result:
$$
\frac{1}{2 \pi j} \oint_{|z|=1}  z^{n-1} \text{d} z \quad \Rightarrow \quad
\frac{1}{2 \pi j} \int_{-\pi}^{\pi} \left ( e^{j\theta} \right )^{n-1} j e^{j\theta} \text{d} \theta =
\frac{1}{2\pi} \int_{-\pi}^{\pi} e^{jn \theta} \text{d} \theta
\overset{\color{red}{\text{IFTD}}}{=} \delta[n]
$$

### Proof IZT via Cauchy's integral theorem
In this subsection we will use Cauchy's integral theorem to derive a more formal proof  of the IZT equation.
First we replace the function $X(z)$ by its ZT definition and than interchange the summation with the integral:
$$\begin{eqnarray*}
\frac{1}{2 \pi } \oint_{C} X(z) z^{n-1} \text{d} z
&=& \frac{1}{2 \pi j} \oint_{C} \left ( \sum_{p=-\infty}^{\infty} x[p] z^{-p} \right ) z^{n-1} \text{d} z \\
&=& \sum_{p=-\infty}^{\infty} x[p] \left\\{ {\color{red}{\frac{1}{2 \pi j} \oint_{C}  z^{n-1-p} \text{d} z }} \right\\}
\end{eqnarray*}$$
The integral (in red) can be evaluated by using Cauchy's integral theorem,  which leads to the function $\delta[n-p]$, which is only 1 when index $p$ is equal to $n$:
$$\begin{eqnarray*}
\frac{1}{2 \pi j} \oint_{C} X(z) z^{n-1} \text{d} z
&=& \sum_{p=-\infty}^{\infty} x[p] \left\\{ {\color{red}{\delta[n-p]}} \right\\} = x[n]
\end{eqnarray*}$$
In other words the result is $x[n]$ which finalized the proof of the derivation of the IZT equation.

#### Example

In this example we will compute the following ZT-pair:
$$
X(z)= \frac{1}{1 - a z^{-1}} \hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm}
x[n]=a^n u[n]
$$
with Cauchy's Residual theorem for the case $|a|<1$.
Applying the formal definition the IZT results in the following equation:
$$\begin{eqnarray*}
X(z) = \frac{1}{1-a z^{-1}} \quad \overset{\text{IZT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \quad x[n] &=&
\frac{1}{2 \pi j} \oint_{C} \left ( \frac{1}{1-a z^{-1}} \right ) z^{n-1} \text{d} z
=\frac{1}{2 \pi j} \oint_{C} \frac{z^n}{z-a}\text{d} z
\end{eqnarray*}$$
When using the unit circle for contour $C$, the result of the IZT is equivalent to the result of the IFTD:
$$\begin{eqnarray*}
X(z) \overset{\text{IZT=IFTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ} \quad x[n] &=&
=\frac{1}{2 \pi j} \oint_{{\color{red}{|z|=1}}} \frac{z^n}{z-a}\text{d} z
\end{eqnarray*}$$
The derivation for the case that the absolute value of the parameter $a$ is smaller than 1 goes in the following steps:

<u>Case $\color{blue}{n \geq 0}$:</u>
<p></p>
For index $n \geq 0$ the function $\frac{z^n}{z-a}$ has only one pole inside the unit circle, which is located at $z=a$.  The resulting residue for $z=a$ leads to  the expression $a^n$.
$$\begin{eqnarray*}
x[n]&=& \text{Res} \left [\frac{z^n}{z-a} \text{ @ } z=a \right ]
=(z - a) \cdot  \frac{z^n}{z-a} \bigg\vert_{z=a}
= a^n
\end{eqnarray*}$$


<u>Case $\color{blue}{n < 0}$:</u>
<p></p>
For $n <0$, with $r=-n$ the function $\frac{z^n}{z-a}$ has an $r$-fold pole at $z=0$ plus one pole at $z=a$.
On the one hand the residua for the $r$-fold pole at $z=0$  results in $-a^n$.
On the other hand the residua for the single pole at $z=a$  results in $+a^n$. Thus for negative indices $n$ the sum of the residuals at $z=0$ and $z=a$ results in 0.
$$\begin{eqnarray*}
\text{Res} \left[\frac{z^{-r}}{z-a} \text{ @ } z=0 \right]
&=&\frac{1}{(r-1) ! } \cdot
\frac{\text{d}^{r-1}}{\text{d} z^{r-1}} \left\{ z^{r} \cdot \frac{z^{-r}}{z-a}  \right\}
\bigg\vert_{z=0}
\overset{r=-n}{=}  -a^n
\end{eqnarray*}$$
Combining this with the result for $n \geq 0$ indeed leads to the sequence $x[n]=a^n u[n]$.



<div class="example">
  <h4> Example </h4>
  <hr>
  Use Chauchy's residue theorem to show that the IZT of $X(z) = \frac{1}{1-a z^{-1}}$, with $|a| >1$,
  results in the non-causal sequence $x[n]=- a^n u[-n-1]$.
  <button class="collapsible">Show solution</button>
  <div class="content">
  For the case $|a|>1$ Cauchy's residue theorem can be computed in the following steps:
  <p></p>
  <u>$\color{blue}{n \geq 0}$</u>: When index $n$ is larger or equal than 0, the function $\frac{z^n}{z-a}$ has no poles within the unit circle, which implies that the residu is zero and thus the sequence $x[n]=0$ for all indices $n \geq 0$.
  <p></p>
  <u>$\color{blue}{n < 0}$</u>
  For negative values of the index $n$ and with $r=-n$ the function $\frac{z^{-r}}{z-a}$ has one $r$-fold poles at $z=0$ within the unit circle. The residu at this $r$-fold pole  results in $-a^n$.
  $$\begin{eqnarray*}
  \text{Res} \left [ \frac{z^{-r}}{z-a} \text{ @ } z=0 \right ] &=&
  \frac{1}{(r-1)!} \cdot
  \frac{\text{d}^{r-1}}{\text{d} z^{r-1}} \left [ z^{r} \cdot \frac{z^{-r}}{z-a}  \right ]
  \bigg \vert_{z=0}
  \overset{r=-n}{=}  -a^n
  \end{eqnarray*}$$
  Combining the result for all indices,  indeed leads to the non-causal sequence $x[n]=-a^n u[-n-1]$.
  </div>
</div>


<div class="example">
  <h4> Example </h4>
  <hr>
  For $|a|<1$ calculate the IZT of the function
  $$
  X(z) = \frac{az^{-1}}{(1 - az^{-1})^2}
  $$
  <button class="collapsible">Show solution</button>
  <div class="content">
  This example needs some more intermediate steps to calculate the IZT. These steps are as follows:
  First we write $X(z)$ as a function of positive powers of $z$.
  Then the IZT can be calculated via the given integral, which leads to the same result as the IFTD when the contour $C$ is on the unit circle.
  $$\begin{eqnarray*}
  X(z) = \frac{az^{-1}}{(1 - az^{-1})^2}
  = \frac{az}{(z-a)^2}
  &\overset{\text{IZT=IFTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}&
  \end{eqnarray*}$$
  $$\begin{eqnarray*}
  x[n]= \frac{1}{2 \pi j} \oint_{{\color{red}{|z|=1}}} \frac{az}{(z-a)^2} \cdot z^{n-1} \text{d} z
  =\frac{1}{2 \pi j} \oint_{{\color{red}{|z|=1}}} \frac{a z^n}{(z-a)^2}\text{d} z
  \end{eqnarray*}$$
  By using Cauchy's residu theorem we have to calculate the given integral of the function $\frac{a z^n}{(z-a)^2}$.  First we split the resulting sequence $x[n]$ into two parts: One part for indices $n$ larger or equal than 0, denoted by $x_{+}[n]$, and the other part for indices $n$ smaller than 0, denoted by $x_{-}[n]$.

  <u>Results for $\color{blue}{n \geq 0}$:</u>
   For the first part the function $\frac{a z^n}{(z-a)^2}$ has one two-fold pole at $z=a$ within the unit circle.  Applying Cauchy's residu theorem  results in  the expression $n \cdot a^n$.
  $$\begin{eqnarray*}
  x_{+}[n] &=& \frac{\text{d}}{\text{d} z} \left [ (z-a)^2 \cdot \frac{a z^n}{(z-a)^2} \right ]
  \bigg\vert_{z=a}
  = a \cdot n \cdot z^{n-1}\bigg\vert_{z=a}
  = n \cdot a^n
  \end{eqnarray*}$$

  <u>Results for $\color{blue}{n < 0}$:</u>

  $x_{-}[n] = x_1[n] + x_2[n]$
  For indices $n<0$ the function $\frac{a z^n}{(z-a)^2}$ has one two-fold pole at $z=a$ and one $r=-n$-fold pole at $z=0$. For this reason we split $x_{-}[n]$ into $x_1[n]$ and $x_2[n]$, in which $x_1[n]$ is the result of the residue at the two-fold pole at $z=a$ and $x_2[n]$ the result of the residue of the $r=-n$-fold pole at $z=0$.
  $$\begin{eqnarray*}
  x_1[n] &=& \frac{\text{d}}{\text{d} z} \left [ (z-a)^2 \cdot \frac{a z^n}{(z-a)^2} \right ]
  \bigg \vert_{z=a}
  = a \cdot n \cdot z^{n-1}\left \vert_{z=a} \right .
  = n \cdot a^n
  \end{eqnarray*}$$
  The result of the residue at the two-fold pole at $z=a$  is equal to  $n \cdot a^n$.
  The result of the residue of the $r=-n$-fold pole at $z=0$  is calculated by the following steps:
  $$\begin{eqnarray*}
  x_2[n] &=& \frac{1}{(r-1)!} \frac{\text{d}^{r-1}}{\text{d} z^{r-1}}
  \left [ z^r \cdot \frac{a z^{-r}}{(z-a)^2} \right ] \bigg \vert_{z=0}  \newline
  &=&\frac{(-2)(-3) \cdots (-r)}{(r-1)!} a (z-a)^{-r-1}\bigg \vert_{z=0}  \newline
  &=& \frac{(-1)^{r-1} r!}{(r-1)!} (-1)^{-r-1} a^{-r}
  = r a^{-r} \overset{r=-n}{=} -n \cdot a^{n}
  \end{eqnarray*}$$
  Thus for negative indices the result $x_{-}[n]$ is equal to the sum of $x_1[n]+x_2[n]$, which results in 0 and  the final results leads to the expression $x[n]=n a^n u[n]$:
  $$\begin{eqnarray*}
  X(z) = \frac{az^{-1}}{(1 - az^{-1})^2} &\overset{\text{IZT=IFTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}&
  x[n]= x_{{\color{red}{+}}}[n] + x_{-}[n] = n a^n {\color{red}{u[n]}}
  \end{eqnarray*}$$
  </div>
</div>
