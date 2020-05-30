+++
title = "General filter structures"

# date = {{ .Date }}
lastmod = 2020-05-02

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Filter structures II: General filter structures"
  weight = 92

+++


## Introduction
A structural representation using interconnected basic building blocks is the first step in hardware or software implementation of an LTI filter. The structural representation provides the relation between some pertinent internal variables with the input and the output that in turn provide the keys to the implementation. There are various forms of the structural representation of filters. We review in this module structures for non-recursive and recursive systems. Then we will introduce the transposition theorem which is a general method of deriving from any given structure another structure from which the input- output properties remain unchanged. Finally, we will discuss several special filter structures.

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/2E2FUTjSFhM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Module overview
This module will cover the following topics:

1. <a href="../discretesignalprocessing_filters_general_nonrecursive">Structures of non-recursive systems</a> - First a general overview of a non-recursive system is explained.
2. <a href="../discretesignalprocessing_filters_general_recursive">Structures of recursive systems</a> - Afterwards this class of filters is extented to also include recursive filters.
3. <a href="../discretesignalprocessing_filters_general_transposition">Transposition theorem</a> - Here a method is discussed to change the structure of a filter.
4. <a href="../discretesignalprocessing_filters_general_special">Special structures</a> [⯈] - Finally the theory is put into practice and some very common examples of filter structures are discussed.

<br></br>
## Summary

### General difference equation and system function
\begin{eqnarray*}
y[n]&=&\sum_{k=0}^{M-1} b_k x[n-k] + \sum_{k=1}^{N-1} a_k y[n-k]\newline
H(z) &=& \frac{Y(z)}{X(z)}= \frac{\sum_{k=0}^{M-1}b_kz^{-k}}{1-\sum_{k=1}^{N-1}a_kz^{-k}}= \frac{\color{blue}{B(z)}}{\color{brown}{A(z)}}
\end{eqnarray*}

### Structures for Non Recursive systems
$$
\mbox{Impulse response: } h[n]=\sum_{k=0}^{M-1} h_k \delta[n-k] \hspace{2mm} \mbox{ with } \hspace{2mm} h_k=b_k
$$
\begin{eqnarray*}
\color{red}{\text{Direct form}} & : &
H(z) = \sum_{n=0}^{M-1} h_k z^{-k}
\end{eqnarray*}
\begin{eqnarray*}
\color{red}{\text{Cascadeform}} &:&
H(z) = C \prod_{k=1}^{M-1} \left (1 - \alpha_k z^{-1} \right ) \newline
& & H(z)= C \prod_{k=1}^{M_s} \left ( 1 + \beta_{1,k}z^{-1} + \beta_{2,k}z^{-2} \right )
\end{eqnarray*}

### Structures for Recursive systems

\begin{eqnarray*}
\color{red}{\text{Direct form I}} & : & H(z) = \color{blue}{B(z)} \cdot \color{brown}{\frac{1}{A(z)}} \newline
\color{red}{\text{Direct form II}} & : & H(z) = \color{brown}{\frac{1}{A(z)}} \cdot \color{blue}{B(z)} \newline
\color{red}{\text{Cascade}} & : & H(z)= C \prod_{k=1}^{\text{max} \\{ N-1,M-1\\}} \frac{1 - \beta_k z^{-1}}{1 - \alpha_k z^{-1}} \newline
\color{red}{\text{Parallel} (N>M, \alpha_i \neq \alpha_k)} & : & H(z)= \sum\_{k=1}^{N-1} \frac{C_k}{1 - \alpha_kz^{-1}}
\end{eqnarray*}

### Transposition theorem
<ol>
  <li> Reverse direction of all branches. </li>
  <li> Change branch points ($\color{blue}{\bullet}$)into summation  nodes ($\color{red}{\oplus}$)and vice versa. </li>
  <li> Interchange the input ($\color{green}{x[n]}$) and output ($y[n]$). </li>
</ol>

### Linear-phase filter
\begin{eqnarray*}
H(e^{j\theta}) &=&|H(e^{j\theta})| \cdot e^{j\varphi \\{ H(e^{j\theta}) \\}} \newline
\varphi \\{ H(e^{j\theta}) \\} &=& \color{red}{c} \cdot \theta + \color{blue}{\alpha} \cdot \frac{\pi}{2}\newline
\text{with constant } \color{red}{c } &\text{  and }& \color{blue}{\alpha} \in \\{ 0, \pm 1\\}.
\end{eqnarray*}
<ul>
  <li> Exact linear phase only with even/odd symmetry FIR. </li>
  <li> Only complex conjugated mirrored or on unit circle. </li>
</ul>

### All-pass filter
$$
| H_{ap}(e^{j\theta})| = 1 \hspace{3mm} \forall \theta
$$

### Minimum and maximum phase system
$H_{min}(z)$: All zeros inside unit circle

$H_{max}(z)$: All zeros outside unit circle

### Factoring: Product All pass and Minimum Phase filter
$$
H(z) = H_{ap}(z) \cdot H_{min}(z)
$$

### Comb filter
$$
G(z)=H(z^N)
$$

### Averaging filter
\begin{eqnarray*}
h[n]= \frac{1}{M} \sum_{k=0}^{M-1} \delta[n-k]
& \circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ &
H(e^{j\theta}) =
\frac{1}{M} \frac{\sin (\frac{M}{2} \theta)}{\sin (\frac{1}{2} \theta)} \cdot e^{-j\frac{M-1}{2}\theta}
\end{eqnarray*}
\begin{eqnarray*}
H(z)&=&
\color{red}{\frac{1}{M} \prod_{n=0}^{M-1} ( 1- \alpha_n z^{-1})} \cdot \color{blue}{\frac{1}{1 - z^{-1}}} \hspace{3mm} \text{with zeros } \color{red}{\alpha_n=e^{j n \frac{2\pi}{M}}}
\end{eqnarray*}

### Frequency sampling filter
\begin{eqnarray*}
h[n]= \sum_{k=0}^{M-1} h_k \delta[n-k]
&\overset{\text{IDFT}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} &
\frac{1}{M} \sum_{l=0}^{M-1} \color{blue}{H[l]} e^{j(2 \pi/M)l k}
\end{eqnarray*}
\begin{eqnarray*}
H(z)&=& \left \\{ \color{red}{\frac{1}{M} \cdot (1-z^{-M}) }\right \\} \cdot \left \\{ \color{blue}{\sum_{l=0}^{M-1}
\frac{H[l]}{\left ( 1-\alpha_l z^{-1} \right )}} \right \\}
\hspace{3mm} \text{with } \color{red}{\alpha_l=e^{jl \frac{2 \pi}{M}}}
\end{eqnarray*}

### Lattice filter
A lattice filter consists of a number of cascaded modules and each module has the same structure. The structure has low sensitivity to parameter quantization effects, and a simple criterion for ensuring filter stability.
