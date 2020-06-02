+++
title = "Special structures"

# date = {{ .Date }}
lastmod = 2020-05-02

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Special structures [⯈]"
  weight = 4
  parent = "Filter structures II: General filter structures"
+++


## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/9QmeyU-sv5w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
## Linear-phase filter
The most important property of a linear phase filter is that its phase response is linear proportional with the relative frequency $\theta$ plus a possible offset, as shown in the following equation:
\begin{eqnarray*}
H(e^{j\theta}) &=&|H(e^{j\theta})| \cdot e^{j\varphi \\{ H(e^{j\theta}) \\}} \newline
\varphi \\{ H(e^{j\theta}) \\} &=& \color{red}{c} \cdot \theta + \color{blue}{\alpha} \cdot \frac{\pi}{2}\newline
\text{with constant } \color{red}{c } &\text{  and  }& \color{blue}{\alpha} \in \\{ 0, \pm 1\\}.
\end{eqnarray*}
A linear phase filter will preserve the waveform of the signal or component of the input signal to the extent that's possible, given that some frequencies will be changed in amplitude by the action of the filter. This could be important in several domains: For example
in radar signal processing, where the wave shape of a returned radar signal might contain important information about the target's properties. It is also important in coherent signal processing and demodulation, where the wave shape is important because a thresholding decision must be made on the wave shape (possibly in quadrature space, and with many thresholds, e.g. 128 QAM modulation), in order to decide whether a received signal represented a "1" or "0". Therefore, preserving or recovering the originally transmitted wave shape is of utmost importance, else wrong thresholding decisions will be made, which would represent a bit error in the communications system. Another example where linear phase is important is audio processing, where some believe (although many dispute the importance) that "time aligning" the different components of a complex wave shape is important for reproducing or maintaining subtle qualities of the listening experience (like the "stereo image", and the like).

In the following subsections we will show the following properties of a linear phase filters:
<ul>
  <li> <b><u>$\color{blue}{\text{Exact linear phase only with even/odd symmetry FIR:}}$</u></b> <br>
  In order for a causal system with a rational system function to have linear phase, exact linear phase can only be achieved with FIR filters. For an FIR filter with a real valued impulse response a sufficient condition for this filter to have linear phase is that the impulse response is either even-symmetric or odd-symmetric.</li>
  <li> <b><u>$\color{blue}{\text{Only complex conjugated mirrored or on unit circle:}}$</u></b> <br>
  As a result of the symmetry property of the FIR filter, it follows that the zeros of the system function appear in complex conjugated mirrored pairs or complex conjugated on the unit circle. </li>
</ul>


### Four different symmetries
In order for a causal system with rational system function to have linear phase, the impulse response must be finite in length. Therefore, IIR filters cannot have exact linear phase.

Assume the length $M$ FIR filter from which $h[n]$ is real valued and $h[0]$ is the first nonzero value of $h[n]$.
A sufficient condition for this FIR filter to have a linear phase is that the impulse response is even-symmetric or odd-symmetric.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/linearphases.svg"
      alt="Four different types of linear-phase filters."
    />
    <figcaption class="numbered">
      Four different types of linear-phase filters.
    </figcaption>
  </figure>
</div>

This implies that linear phase filters may be classified into four types depending on whether the impulse response is even- or odd-symmetric and whether the length $M$ is even or odd. For even-symmetry  filters Type I has odd length and type II has even length filters, while for odd-symmetric filters type III has odd length and type IV has even length filters.
A visual impression of the impulse responses of these four types is depicted in Fig. 1.

### Frequency response of linear phase filters
In general the frequency response of a length $M$ FIR filter is given by the following equation:
\begin{eqnarray*}
h[n] = \sum_{k=0}^{M-1} h_k \delta[n-k] &\overset{\text{FTD}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} & H(e^{j\theta})= \sum_{k=0}^{M-1} h_k e^{-jk \theta}
\end{eqnarray*}
The frequency response expressions for each of the four linear filter types is as follows:

<b> Even symmetry $h_k=h_{M-1-k}$; Odd $M$ $\Rightarrow$ $L=\frac{M-1}{2}$: </b>
\begin{eqnarray*}
\color{red}{\textit{Type I}}  &:&
H_{I}(e^{j\theta}) =\left (h_L +  2\sum_{i=1}^{L} h_{L-i} \cos(i \cdot \theta) \right ) \cdot e^{-jL \cdot \theta}
\end{eqnarray*}
<b>Even symmetry $h[=h_{M-1-k}$; Even $M$ $\Rightarrow$ $L=\frac{M}{2}$:</b>
\begin{eqnarray*}
\color{red}{\textit{Type II}}  &:&
H_{II}(e^{j\theta}) =\left ( 2\sum_{i=1}^{L} h_{L-i} \cos((i - \frac{1}{2}) \cdot \theta) \right ) \cdot e^{-j(L- \frac{1}{2}) \cdot \theta}
\end{eqnarray*}
<b>Odd symmetry $hk=-h-{M-1-k}$; Odd $M$ $\Rightarrow$ $L=\frac{M-1}{2}$:</b>
\begin{eqnarray*}
\color{red}{\textit{Type III}}  &:&
H_{III}(e^{j\theta}) =\left (2\sum_{i=1}^{L} h_{L-i} \sin(i \cdot \theta) \right ) \cdot e^{-j(L \cdot \theta - \frac{\pi}{2}) }
\end{eqnarray*}
<b>Odd symmetry $h_k=-h-{M-1-k}$; Even $M$ $\Rightarrow$ $L=\frac{M}{2}$:</b>
\begin{eqnarray*}
\color{red}{\textit{Type IV}}  &:&
H_{IV}(e^{j\theta}) =\left ( 2 \sum_{i=1}^{L} h_{L-i} \sin((i-\frac{1}{2})\theta)  \right ) \cdot e^{-j((L - \frac{1}{2}) \cdot \theta - \frac{\pi}{2})}
\end{eqnarray*}
Finally we have the following general expressions for the FIR frequency response $H(e^{j\theta})=\sum_{k=0}^{M-1} h_k e^{-jk \theta}$ evaluated at $\theta=0$ and $\theta=\pm \pi$
$$
H(e^{j0})=\sum_{k=0}^{M-1} h_k
\hspace{2mm} \text{and} \hspace{2mm}
H(e^{j\pm \pi})= \sum_{k=0}^{M-1} (-1)^k h_k
$$
The frequencies $\theta=0$ and $\theta=\pm \pi$ deserve special attention. For example evaluating the Type III frequency response $H_{III}(e^{j\theta})$ for $\theta=0$ results in:
\begin{eqnarray*}
H_{III}(e^{j\theta})\vert_{\theta=0} &=& \sum_{k=0}^{M-1} h_k \overset{\text{odd } M}{=}0
\end{eqnarray*}
In a similar way we can derive the following results:
<table style="width:100%; text-align:center">
  <tr>
    <th>Type</th>
    <th>$\theta=0$</th>
    <th>$\theta=\pm \pi$</th>
  </tr>
  <tr>
    <td>I</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td>II</td>
    <td>-</td>
    <td>$H_{II}(\text{e}^{\pm j \pi})=0$</td>
  </tr>
  <tr>
    <td>III</td>
    <td>$H_{III}(e^{j0})=0$</td>
    <td>$H_{III}(\text{e}^{\pm j \pi})=0$</td>
  </tr>
  <tr>
    <td>IV</td>
    <td>$H_{IV}(e^{j0})=0$</td>
    <td>-</td>
  </tr>
</table>

In a follow up video we will use these zero crossings, or phase jumps of $\pi$, of the linear phase filters to design certain specific filter characteristics as denoted in the following table:

<table style="width:100%; text-align:center">
  <tr>
    <th>Type</th>
    <th colspan=2>Phase jump of $\pi$ at</th>
    <th>Comment</th>
  </tr>
  <tr>
    <td></td>
    <td>$\theta=0$</td>
    <td>$\theta=\pm \pi$</td>
    <td></td>
  </tr>
  <tr>
    <td>I</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
  </tr>
  <tr>
    <td>II</td>
    <td>-</td>
    <td>Yes</td>
    <td>No HPF possible</td>
  </tr>
  <tr>
    <td>III</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Only Bandpass possible</td>
  </tr>
  <tr>
    <td>IV</td>
    <td>Yes</td>
    <td>-</td>
    <td>No LPF possible</td>
  </tr>
</table>

### $Z$-transform of linear phase filters
In general the system function of a length $M$ FIR filter is given by the following equation:
\begin{eqnarray*}
h[n] = \sum_{k=0}^{M-1} h_k \delta[n-k]
&\overset{\text{ZT}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} & H(z)= \sum_{k=0}^{M-1} h_k z^{-k}
\end{eqnarray*}
The symmetry in the coefficients of the impulse response of a linear phase FIR filter impose constraints on the system function $H(z)$. For even-symmetric Type I and Type II filters, thus with $h_k=h_{M-1-k}$, we have:
\begin{eqnarray*}
z^{-(M-1)}H(z^{-1})&=& z^{-(M-1)} \sum_{k=0}^{M-1}h_k z^{k}
=\sum_{k=0}^{M-1} h_k z^{k-(M-1)}\newline
&\overset{l=-k+M-1}{=} &
\sum_{l=M-1}^{0} h_{M-1-l} z^{-l} \newline &\overset{h_{M-1-l}=h_l}{=}& \sum_{l=0}^{M-1} h_l z^{-l} = H(z).
\end{eqnarray*}
Thus for even-symmetric Type I and Type II filters we have the following property:
\begin{equation}\label{Eq:Sym1}
H(z)=z^{-(M-1)}H(z^{-1})
\end{equation}
Similarly, for odd-symmetric filters Type III and Type IV filters, thus with $h_k=-h_{M-1-k}$, we have:
\begin{equation}\label{Eq:Sym2}
H(z)=-z^{-(M-1)}H(z^{-1})
\end{equation}
From both equations (\ref{Eq:Sym1}) and (\ref{Eq:Sym2}) it follows that if the system function $H(z)$ of a linear phase filter is equal to zero for $z=z_0$, $H(z)$ must also be zero for $z=1/z_0$. Therefor the zeros occur in reciprocal pairs. Furthermore, in case of real coefficients, if $H(z)$ is equal to zero for $z=z_0$, $H(z)$ will also have a zero at $z=z^\ast_0$. Thus in general the zeros of the linear phase system $H(z)$ will appear in groups of four zeros in conjugate reciprocal pairs, $z_0, 1/z_0, z^\ast_0, 1/z^\ast_0$, as illustrated in Fig. 2.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/mirroring.svg"
      alt="Groups of zeros of a linear phase system."
    />
    <figcaption class="numbered">
      Groups of zeros of a linear phase system.
    </figcaption>
  </figure>
</div>
This figure also shows some special cases when the zeros coincide: $H(z)$ may have complex conjugate zeros on the unit circle at $z=\color{red}{z_1}$ and $z=\color{red}{z^\ast_1}$. Or $H(z)$ may have one or more zeros at $z=\color{yellow}{1}$ or $z=\color{green}{-1}$. Finally $H(z)$ may have reciprocal zeros on the real axis at $z=\color{blue}{z_2}$ and $z=\color{blue}{1/z_2}$.


Another consequence of equations (\ref{Eq:Sym1}) and (\ref{Eq:Sym2}) is that the cases $z=1$ and $z=-1$ deserve special attention. For example evaluating the Type II system function $H_{II}(z)$ for $z=-1$ results in:
\begin{eqnarray*}
H_{II}(z)\vert_{z=-1} &=& \left \\{ z^{-(M-1)} H_{II}(z^{-1}) \right \\} \bigg\vert_{z=-1} \newline
H_{II}(-1) &=& (-1)^{-(M-1)} H_{II}(-1) \overset{\text{even } M}{=}
-H_{II}(-1) \text{ } \Rightarrow \text{ } H_{II}(-1)=0
\end{eqnarray*}
In a similar we can derive the following results:
<table style="width:100%">
  <tr>
    <th>Type</th>
    <th>$z=1$</th>
    <th>$z=-1$</th>
  </tr>
  <tr>
    <td>I</td>
    <td>--</td>
    <td>--</td>
  </tr>
  <tr>
    <td>II</td>
    <td>--</td>
    <td>$H_{II}(-1)=0$</td>
  </tr>
  <tr>
    <td>III</td>
    <td>$H_{III}(1)=0$</td>
    <td>$H_{III}(-1)=0$</td>
  </tr>
  <tr>
    <td>IV</td>
    <td>$H_{IV}(1)=0$</td>
    <td>--</td>
  </tr>
</table>
From the fact that $z=1$ coincides with $\theta=0$ and $z=-1$ with $\theta=\pm \pi$, it follows that these results are a generalized representation of the results as found in the previous subsection.

### Examples of linear phase filters
In order to show the validity of the linear phase properties try to solve the following two odd length 5 FIR filter examples: The first example is an FIR filter with a even-symmetric impulse response and the second one with an odd-symmetric impulse response.

<div class="example">
<h4> Example </h4>
<hr>
The equation shows the mathematical expression of the frequency response of an odd length 5 FIR filter with impulse response $h_I[n]$:
$$
H_I(e^{j\theta})= h_0 + h_1 e^{-j\theta} + h_2 e^{-j2\theta} + h_3 e^{-j3\theta} + h_4 e^{-j4\theta}
$$
Assume the impulse response is even-symmetric around the center coefficient $h_2$ with coefficients $\color{red}{h_4=h_0=1}$ and $\color{blue}{h_3=h_1=-3}$ and $h_2=\frac{9}{2}$. Show that this system has linear phase and make a sketch of the magnitude- and phase response and the pole-zero-plot.
<button class="collapsible">Show solution</button>
<div class="content">
We can use the fact that the impulse response is even-symmetric as follows:
First bring the complex exponent $e^{-j\theta}$, which belongs to the centre coefficient,  outside brackets. The result is that inside brackets each component which contains a negative exponent is weighted with the same number as the component which contains a positive exponent.
\begin{eqnarray*}
H_I(e^{j\theta}) &=& \color{red}{h_0} + \color{blue}{h_1} e^{-j\theta} + h_2 e^{-j2\theta} + \color{blue}{h_1} e^{-j3\theta}+ \color{red}{h_0} e^{-j4\theta} \\
&=& \left ( \color{red}{h_0} e^{j2 \theta} + \color{blue}{h_1} e^{j\theta} + h_2 +\color{blue}{h_1} e^{-j\theta} + \color{red}{h_0} e^{-j2 \theta} \right ) \cdot e^{-j2 \theta}
\end{eqnarray*}
In this example the weights of $e^{j2\theta}$ and $e^{-j2\theta}$ have the same value $\color{red}{h_0}$ and also the weights of $e^{j\theta}$ and $e^{-j\theta}$ have the same value ${\color{blue}h_1}$.
For this reason we can combine the different complex exponents which results into an expression with only real components, namely an offset and a sum of cosine shapes.
\begin{eqnarray*}
H_I(e^{j\theta})
&=& \Big( 2 \cdot \Big( \color{red}{h_0} \cos(2 \theta) +  \color{blue}{h_1} \cos(\theta) \Big) + h_2  \Big) \cdot e^{-j2 \theta}
\end{eqnarray*}
In other words the phase is completely described by the complex exponent $e^{-j2\theta}$ outside the brackets, from which it follows that the phase response is equal to $-2 \theta$, which is indeed linear proportional with the relative frequency $\theta$.
The given values of the coefficients results in the following expression for the frequency response.
\begin{eqnarray*}
H_I(e^{j\theta}) &=&
\left ( 2 \cdot \Big( \cos (2 \theta) - 3 \cos (\theta) \Big) + \frac{9}{2} \right ) \cdot e^{-j2 \theta}
\end{eqnarray*}
From the following plots of the magnitude and phase response it is clearly visible that the phase response has a linear behavior.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/MagPhaseTypeI.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/PZplotTypeI.svg"
    style="width:100%">
  </div>
</div>
</figure>
The system function writes as follows:
\begin{eqnarray*}
H_I(z)&=& \color{red}{1} \color{blue}{-3} z^{-1} + \frac{9}{2} z^{-2} \color{blue}{-3} z^{-3}\color{red}{+} z^{-4} \newline
&=&
(1- z_1 z^{-1}) \cdot (1- z^\ast_1 z^{-1}) \cdot (1- (1/z_1) z^{-1}) \cdot(1- (1/z^\ast_1) z^{-1})
\end{eqnarray*}
with  $z_1 = (\sqrt{2}/2) e^{j\pi/4}$. From this equation it follows that the odd length FIR filter with even-symmetric impulse response results into a system function  that can be expressed as a polynomial function from which the zeros appear as complex conjugated and mirrored pairs as depicted in the pole zero plot.
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
The equation shows the mathematical expression of the frequency response of an odd length 5 FIR filter with impulse response $h[n]$:
$$
H_{III}(e^{j\theta})= h_0 + h_1 e^{-j\theta} + h_2 e^{-j2\theta} + h_3 e^{-j3\theta} + h_4 e^{-j4\theta}
$$
Assume the impulse response is odd-symmetric around the center coefficient $h_2$ with coefficients $\color{red}{h_4=-h_0=-1}$; $\color{blue}{h_3=-h_1=1}$ and $h_2=-h_2$ $\Rightarrow$ $h_2=0$.  Show that this system has linear phase and make a sketch of the magnitude- and phase response and the pole-zero-plot.
<button class="collapsible">Show solution</button>
<div class="content">
Now the combination of the different complex exponents results into an expression with only real sinus components, as follows from the following derivation:
\begin{eqnarray*}
H_{III}(e^{j\theta})&=& \color{red}{h_0} + \color{blue}{h_1} e^{-j\theta} - \color{blue}{h_1} e^{-j3\theta}- \color{red}{h_0} e^{-j4\theta}\newline
&=& \left ( \color{red}{h_0} e^{j2 \theta} +\color{blue}{h_1} e^{j\theta} -\color{blue}{h_1} e^{-j\theta} -  \color{red}{h_0} e^{-j2 \theta} \right ) \cdot e^{-j2 \theta}\newline
&=&2 \color{green}{j}  \cdot \Big(  \color{red}{h_0} \sin(2 \theta) + \color{blue}{h_1} \sin(\theta)\Big) \cdot e^{-j2 \theta}\newline
&=& 2 \cdot \Big( \color{red}{h_0} \sin(2 \theta)+\color{blue}{h_1} \sin(\theta)  \Big) \cdot e^{-j(2 \theta \color{green}{- \frac{\pi}{2}})}\newline
&=&2 \cdot \Big(\sin(2\theta) - \sin(\theta) \Big) \cdot e^{-j(2\theta \color{green}{- \frac{\pi}{2}})}
\end{eqnarray*}
The plots of the magnitude and phase response are depicted in the figure.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/MagPhaseTypeIII.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/PZplotTypeIII.svg"
    style="width:100%">
  </div>
</div>
</figure>
The system function writes as:
\begin{eqnarray*}
H_{III}(z) &=&
\color{red}{1} \color{blue}{-} z^{-1} \color{blue}{+} z^{-3} \color{red}{-} z^{-4} \newline
&=&  (1- z^{-1}) \cdot (1+z^{-1}) \cdot (1- e^{j\pi/3} z^{-1}) \cdot(1- e^{-j\pi/3}z^{-1})
\end{eqnarray*}
From this equation it follows that the odd length FIR filter with odd-symmetric impulse response results into a system function  that can be expressed as a polynomial function from which the zeros appear as complex conjugated and mirrored pairs as depicted in the pole zero plot.
</div>
</div>


### Reduced complexity
The symmetry of the impulse response coefficients of a linear-phase FIR filter can be exploited to reduce the complexity of the realization of such a structure.

<div class="example">
<h4> Example </h4>
<hr>
Give a realization scheme of the type II even length $M$ even-symmetric linear-phase filter, thus $h[M-1-n]=h[n]$ with a reduction of the number of multiplications with 50 %.
<button class="collapsible">Show solution</button>
<div class="content">
As an example of a type II linear phase filter the number of multiplications can be reduced by 50 \% by forming the sums of the samples $x[n-k] + x[n-M+k]$ prior to multiplying by $h_k$.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/evensymmetry.svg"
      alt="Even symmetry system"
    />
  </figure>
</div>
A similar approach holds for the other types of linear-phase symmetries.
</div>
</div>

<br></br>
## All-pass filter
An all-pass filter passes all frequency with the same magnification factor, that is the magnitude of the frequency response is  constant
$$
| H_{ap}(e^{j\theta})| = 1 \hspace{3mm} \forall \theta
$$
This unit magnitude constraint constrains poles and zeros of a rational system function to occur in mirrored pairs. Thus if $H(z)$ has a pole $z=\alpha_k$, $H(z)$ must also have a zero at the mirrored location $z=1/\alpha^\ast_k$.
\begin{eqnarray*}
\text{Complex } h[n] &:& H_{ap}(z) = \prod_{k=1}^{p} \frac{z^{-1}-\alpha_k^\ast}{1 - \alpha_k z^{-1}} \newline
\text{Real } h[n] &:& H_{ap}(z) = \prod_{k=1}^{N_s}
\frac{|\alpha_{k}|^2 - 2 \Re e \\{ \alpha_k \\} z^{-1}+  z^{-2}}{1 - 2 \Re e \\{ \alpha_k \\} z^{-1}+ |\alpha_{k}|^2 z^{-2}}
\end{eqnarray*}
The poles of a stable and causal all pass filter $H(z)$ lie inside the unit circle, that is all $|\alpha_k|<1$.
If the impulse response $h[n]$ is real-valued, the complex roots occur in conjugate pairs, and these conjugate pairs can be combined to form second-order factors from which all coefficients are real, as shown in the equation.

<div class="example">
<h4> Example </h4>
<hr>
Show that the following system is all pass:
$$
H(e^{j\theta})=\frac{\frac{1}{2} - e^{-j\theta} + e^{-j2 \theta}}{1 - e^{-j\theta} + \frac{1}{2} e^{-j2\theta}}
$$
Give the pole zero plot and a rough sketch of the magnitude and phase response plots.
<button class="collapsible">Show solution</button>
<div class="content">
By replacing $e^{-j\theta}$ with the complex variable $z^{-1}$ we obtain the following system function:
$$
H(z)= \frac{\frac{1}{2} - z^{-1} + z^{-2}}{1 - z^{-1} + \frac{1}{2} z^{-2}}
$$
Because of the special structure of this equation, the absolute value results in:
\begin{eqnarray*}
|H(z)| &=&\sqrt{H(z) \cdot (H(z))^*}= \sqrt{H(z) \cdot H^*(z^{-1})}\\
&=& \sqrt{
\left ( \frac{\frac{1}{2} - z^{-1} + z^{-2}}{1 - z^{-1} + \frac{1}{2} z^{-2}} \right ) \cdot
\left ( \frac{\frac{1}{2} - z + z^{2}}{1 - z + \frac{1}{2} z^{2}} \right )} \\
&=& \sqrt{\left ( \frac{z^{-2} \left ( \frac{1}{2}z^2 - z + 1 \right )}{z^{-2} \left ( z^2 - z + \frac{1}{2} \right )} \right ) \cdot
\left ( \frac{\frac{1}{2} - z + z^{2}}{1 - z + \frac{1}{2} z^{2}} \right )} = 1 \\
\Rightarrow & & |H(e^{j\theta})| = \vert H(z)\vert_{|z|=1} =1
\end{eqnarray*}
The pole and zeros are:
$$
H(z) = \frac{(\frac{1}{2} \sqrt{2}- e^{j\frac{\pi}{4}}z^{-1}) (\frac{1}{2} \sqrt{2}- e^{-j\frac{\pi}{4}}z^{-1})}{(1- \frac{1}{2} \sqrt{2} e^{j\frac{\pi}{4}}z^{-1})(1- \frac{1}{2} \sqrt{2} e^{j\frac{\pi}{4}}z^{-1})}
$$
as shown at the left hand side of the following plot:
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/AllpassPZ.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/AllpassAmplPhase.svg"
    style="width:100%">
  </div>
</div>
</figure>
A sketch of the magnitude and phase response is depicted at the right hand side of the figure.
</div>
</div>


<br></br>
## Minimum and maximum phase system
A stable and causal LTI system has all its poles inside the unit circle. The zeros, however may lie anywhere in the $z$-plane. In some applications, it is necessary to constraint a system $H(z)$ so that its inverse $G(z)=1/H(z)$ is also stable and causal. This requires that the zeros of $H(z)$ lie also inside the unit circle.
A stable and causal filter that has a stable and causal inverse is said to have minimum phase and so a minimum phase system has all of its poles and zeros inside the unit circle, as shown in Fig. 3.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/pzminphase.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/magphaseminphase.svg"
    style="width:100%">
  </div>
  <figcaption class="numbered">
    Pole-zero plot and magnitude- and phase-response of minimum phase system.
  </figcaption>
</div>
</figure>
The magnitude and phase response of a minimum phase system with three zeros inside the unit circle is depicted in Fig. 3.

When mirroring all zeros of a stable and causal minimum phase system we obtain a maximum phase system and so a maximum phase system has all of its poles inside and its zeros outside the unit circle, as shown in Fig. 4.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/pzmaxphase.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/magphasemaxphase.svg"
    style="width:100%">
  </div>
  <figcaption class="numbered">
    Pole-zero plot and magnitude- and phase-response of maximum phase system.
  </figcaption>
</div>
</figure>
The magnitude and phase response of a minimum phase system with three zeros inside the unit circle is depicted in Fig. 4.
The plots show the magnitude and phase response of a maximum phase system with three zeros outside the unit circle as depicted in the pole zero plot. These zeros are obtained by mirroring all three zeros of the previous minimum phase system.


{{% alert note %}}
<ul>
  <li> Mirroring a zero with respect to the unit circle does not change the shape of the magnitude response. Thus both minimum and maximum phase systems have, besides a constant factor, the same shape of the magnitude response characteristic. </li>
  <li> The phase of a minimum phase system has less variations compared to the phase variations of a maximum phase system. </li>
  <li> The group delay is defined as:
  $$
  \tau (\theta) = - \frac{\text{d} \varphi \{ H(e^{j\theta}) \}}{\text{d} \theta},
  $$
  The group delay of a minimum phase system is minimal. </li>
</ul>
{{% /alert %}}


<br></br>
## Factoring: Product All pass and Minimum Phase filter
Stable causal filter with system function $H(z)$, can always be factored as a product of a minimum phase filter and an all-pass filter. The procedure is as follows:
<ol>
  <li> First mirror the zeros which are outside $|z|=1$ into new zeros inside $|z|=1$. </li>
  <li> Then cancel the new zeros by new poles. </li>
  <li> Combine the old and new zeros that are inside $|z|=1$ and the old poles together which results in a minimum phase system. </li>
  <li> The combination of the old zeros that are outside $|z|=1$ and the new poles results in an all pass system. </li>
</ol>

<div class="example">
<h4> Example </h4>
<hr>
Factor the following system function as the product of a minimum phase system and an all-pass system:
$$
H(z) = \frac{1 - 2 z^{-1}}{1 - 0.9 z^{-1}}
$$
<button class="collapsible">Show solution</button>
<div class="content">
This can be shown as follows:
\begin{eqnarray*}
H(z) &=& \frac{1 - \color{green}{2} z^{-1}}{1 - 0.9 z^{-1}}
\cdot \frac{1 - \color{red}{\frac{1}{2} z^{-1}}}{1 - \color{blue}{\frac{1}{2} z^{-1}}}
= \frac{1 - \color{red}{\frac{1}{2}} z^{-1}}{1 - 0.9 z^{-1}}  \cdot
\frac{1 - \color{green}{2} z^{-1}}{1 - \color{blue}{\frac{1}{2}} z^{-1}} \newline
&=& H_{min}(z) \cdot H_{ap}(z)
\end{eqnarray*}
First create a zero by we mirroring the zero, which results in a new zero at $z=0.5$. This new zero has to be compensated by a new pole at the same position $z=0.5$. Then rearrange all old and new poles and zeros of $H(z)$ into two factors. The first factor contains the old pole and the new zero, which are both inside the unit circle and so this factor is minimum phase. The second factor contains the old zero and new pole which are each others mirrored versions and so this factor is all pass.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/ExampleFact.svg"
      alt="Example fortorization."
    />
  </figure>
</div>
These steps can be applied to any filter $H(z)$
</div>
</div>


<br></br>
## Comb filter
A comb filter is obtained by replacing each delay of an original filter structure by $N$ delays in a new filter structure. In terms of the system function, the function variable $z$ of the original system function $H(z)$ is replaced by $z^N$ in the new system function $G(z)$:
$$
G(z)=H(z^N)
$$
<div class="example">
<h4> Example </h4>
<hr>
Given the system function $H(z)=1 -z^{-1}$ and its pole zero plot and magnitude and phase plots:
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/PZCombN1.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/AmplPhasCombN1.svg"
    style="width:100%">
  </div>
</div>
</figure>
Make a pole zero plot of the comb filter $G(z)=H(z^5)$. Give also a rough sketch of the magnitude and phase response plots of $G(z)$.
<button class="collapsible">Show solution</button>
<div class="content">
The system function becomes:
$$
G(z)=H(z^5)=1-z^{-5}
=\prod_{n=0}^{4} ( 1- \alpha_n z^{-1})
\hspace{3mm} \text{with } \alpha_n=e^{jn \frac{2\pi}{5}}
$$
The plots are as follows:
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/PZCombN5.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/AmplPhasCombN5.svg"
    style="width:100%">
  </div>
</div>
</figure>
When replacing the function variable $z$ by $z^5$ we obtain a new system function $G(z) = 1 - z^{-5}$ which can be expanded as a product of 5 first order terms, each having a zero at $z=\alpha_n = e^{jn \frac{2\pi}{5}}$ and a pole at $z=0$. The pole zero plot shows the distributed zeros over the unit circle and the magnitude and phase response plots show clearly the 5 repetitions of the original magnitude and phase response. The name 'comb filter' arrives from the 'comb-like' shape of these plots.
</div>
</div>


<br></br>
## Averaging filter
An $M$ point averaging filter can be realized with the following non recursive direct form I structure as a transversal FIR with unit weights as depicted in Fig. 5.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/averagefilFIR.svg"
      alt="$M$ point averaging FIR filter."
    />
  </figure>
  <figcaption class="numbered">
    $M$ point averaging FIR filter.
  </figcaption>
</div>
In a previous module we have seen that the frequency response of this $N$ point averaging filter can be described by the following Dirichlet function
\begin{eqnarray*}
h[n]= \frac{1}{M} \sum_{k=0}^{M-1} \delta[n-k]
& \circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ &
H(e^{j\theta}) =
\frac{1}{M} \frac{\sin (\frac{M}{2} \theta)}{\sin (\frac{1}{2} \theta)} \cdot e^{-j\frac{M-1}{2}\theta}
\end{eqnarray*}
from which the magnitude response has its main lobe around frequency zero and the phase response is linear as shown in Fig. 6.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/DirichletM21.svg"
      alt="Dirichlet function: Magnitude- and Phase- response of $M=21$ averaging filter."
    />
  </figure>
  <figcaption class="numbered">
    Dirichlet function: Magnitude- and Phase- response of $M=21$ averaging filter.
  </figcaption>
</div>
An alternative recursive structure can be found by rewriting the system function as a rational function that can be interpreted as the cascading of the non recursive structure of the numerator (in red) and the recursive structure of the denominator (in blue).
\begin{eqnarray*}
H(z)&=&\frac{1}{M} \sum_{k=0}^{M-1} z^{-k} =
\frac{1}{M} \cdot \frac{1 - z^{-M}}{1 - z^{-1}}
=\color{red}{\frac{1}{M} \cdot (1 -z^{-M})} \cdot \color{blue}{
\frac{1}{1-z^{-1}}}\newline
&=& \color{red}{\frac{1}{M} \prod_{n=0}^{M-1} ( 1- \alpha_n z^{-1})} \cdot \color{blue}{\frac{1}{1 - z^{-1}}} \hspace{3mm} \text{with zeros } \color{red}{\alpha_n=e^{jn \frac{2\pi}{M}}}
\end{eqnarray*}
The non recursive structure of the numerator can be expanded as the product of $M$ first order terms, each with one zero at $z=\alpha_n=e^{jn \frac{2\pi}{M}}$ and one pole in $z=0$. The recursive structure of the denominator has one pole in $z=1$ and one zero in $z=0$. Concluding it follows that the pole zero plot of the $M$ point averaging filter contains, except poles at $z=0$, $M$ zeros that are equally distributed over the unit circle and one pole at $z=1$, which cancels the zero at $z=1$.

<div class="example">
<h4> Example </h4>
<hr>
Give the realization scheme of an averaging filter with $M=5$ as the cascading of a fifth order non recursive structure filter and a first order recursive structure. Also give the pole zero plot and a sketch of the magnitude response.
<button class="collapsible">Show solution</button>
<div class="content">
$$
H(z) = \frac{1}{5} \sum_{k=0}^{4} z^{-k}
= \color{red}{\frac{1}{5}} \cdot \frac{\color{red}{1 - z^{-5}}}{\color{blue}{1 - z^{-1}}}
= \color{red}{\frac{1}{5} \prod_{n=0}^{4} ( 1- \alpha_n z^{-1})} \cdot \color{blue}{\frac{1}{1 - z^{-1}}}
$$
with zeros $\color{red}{\alpha_n=e^{jn \frac{2\pi}{5}}}$.
The figure shows an example of the cascaded structure of an averaging filter with $N=5$.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/averagefilCasc.svg"
      alt="Cascaded averaging filter."
    />
  </figure>
</div>
Expanding the numerator as a product of 5 first order terms results in the pole zero plot, which shows the 5 equally distributed zeros over the unit circle from which the zero at $z=1$ is cancelled by the pole at $z=1$ which is also reflected in the magnitude plot.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/pzplotaverageN5.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/AmplDirichletN5.svg"
    style="width:100%">
  </div>
</div>
</figure>
</div>
</div>


<br></br>
## Frequency sampling filter
The previously discussed philosophy of the averaging filter
can be extended to an $M$ point transversal FIR filter with weights $h_k$ as shown in Fig. 7
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/averagefilCasc.svg"
      alt="$M$ point transversal FIR filter."
    />
  </figure>
  <figcaption class="numbered">
    $M$ point transversal FIR filter.
  </figcaption>
</div>
This results in the so called frequency sampling filter which is a filter structure from which the system function $H(z)$, or equivalently its frequency response $H(e^{j\theta})$, can be parameterized in terms of the $M$ DFT weights $H[l]$ of the impulse response $h[n]$.

Starting with the system function $H(z)$ of non recursive $M$ point transversal FIR filter with weights $h_k$, the derivation of the frequency sampling structure goes as follows:
With the $M$-point Inverse DFT relation
\begin{eqnarray*}
h[n]= \sum_{k=0}^{M-1} h_k \delta[n-k]
&\overset{\text{IDFT}}{\circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ} &
\frac{1}{M} \sum_{l=0}^{M-1} \color{blue}{H[l]} e^{j(2 \pi/M)l k}
\end{eqnarray*}
we can substitute this IDFT equation for the impulse response weights.
\begin{eqnarray*}
H(z)&=& \sum_{k=0}^{M-1} h_k z^{-k}
= \sum_{k=0}^{M-1}
\left \\{ \frac{1}{M} \sum_{l=0}^{M-1} \color{blue}{H[l]} e^{j(2 \pi/M)l k} \right \\} z^{-k}
\end{eqnarray*}
Then change the order of the summations and write the internal summation as a rational function.
\begin{eqnarray*}
H(z)&=& \frac{1}{M} \sum_{l=0}^{M-1} \color{blue}{H[l]}
\left \\{ \sum_{k=0}^{M-1} \left ( e^{j(2 \pi/M)l } z^{-1} \right )^{k} \right \\}\newline
&=& \frac{1}{M} \sum_{l=0}^{M-1} \color{blue}{H[l]} \cdot
\left \\{ \frac{1-\color{green}{e^{j(2 \pi/M)l M }} z^{-M}}{1-e^{j(2 \pi /M)l } z^{-1}} \right \\}
\end{eqnarray*}
The exponent (in green) of the numerator polynomial is equal to 1.
\begin{eqnarray*}
H(z)&=& \frac{1}{M} \sum_{l=0}^{M-1} {\color{blue}H[l]} \cdot
\left \\{ \frac{1-z^{-M}}{1-e^{j(2 \pi /M)l } z^{-1}} \right \\}
\end{eqnarray*}
As a last step  the system function can be written as a product (cascading) of a non recursive structure of the numerator (in red) and the recursive structure of the denominator (in blue), representing the $M$ parallel first order terms.
\begin{eqnarray*}
H(z)&=& \left \\{ \color{red}{\frac{1}{M} \cdot (1-z^{-M}) }\right \\} \cdot \left \\{ \color{blue}{\sum_{l=0}^{M-1}
\frac{H[l]}{\left ( 1-\alpha_l z^{-1} \right )}} \right \\}
\hspace{3mm} \text{with } \color{red}{\alpha_l=e^{jl \frac{2 \pi}{M}}}
\end{eqnarray*}
A realization scheme of this frequency sampling filter structure is depicted in Fig. 8.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/Freqsampl.svg"
      alt="Structure Frequency sampling filter."
    />
  </figure>
  <figcaption class="numbered">
    Structure Frequency sampling filter.
  </figcaption>
</div>
The recursive part consists of $M$ parallel weighted first order terms, each with a pole at $z=\alpha_l=e^{jl \frac{2\pi}{M}}$, a zero at $z=0$ and weight $H[l]$. These $M$ poles cancel the $M$ equally distributed zeros of the non recursive part (in red) and the value of the frequency response at each of these $M$ equally distributed frequencies is equal to the $M$ different values of the $M$-point DFT weights $H[l]$ of the $M$ point impulse response $h[n]$.

In a follow up module, we will see that the frequency sampling filter structure is typically used for the realization of narrow band filters. In such a case most weights of the parallel terms are equal to zero and need not to be implemented, which results in a very efficient structure.


<div class="example">
<h4> Example </h4>
<hr>
Design a frequency sampling filter from which the frequency response is defined for the following frequencies:
$$
H(e^{j\theta}) =
\left \{
\begin{array}{cl}
0 & \text{for } \theta = 0, \pm 2 \cdot \frac{2\pi}{5} \\
3 & \text{for } \theta = \pm \frac{2\pi}{5}
\end{array}
\right .
$$
Derive the realization scheme of the structure as the cascading of a non recursive structure and parallel first order recursive structures. Give also a realization scheme in which the parallel structure has real coefficients. Finally give the pole zero plot and a sketch of the magnitude response $|H(e^{j\theta})|$.
<button class="collapsible">Show solution</button>
<div class="content">
We need to design a frequency filter with the following parameters:
$N=5$ and DFT weights: $H[k]=0$ except $H[1]=H[4]=3$.
The following equation shows the system function description of a 5-th order frequency sampling filter with all DFT weights equal to zero, except the first and the last weight which are equal to 3:
\begin{equation*}
H(z) = \left \{ \color{red}{\frac{1}{5} \cdot (1-z^{-5})} \right \}
\cdot \left \{ \color{blue}{ \left ( \frac{3}{1 -z^{-1} \alpha_1} \right )+\left ( \frac{3}{1 -z^{-1} \alpha_1^\ast} \right ) }
\right \}
\end{equation*}
with $\alpha_1=e^{j\frac{2\pi}{5}}$. This structure can be realized with the cascaded structure as depicted in the following figure.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/Freqsampl1.svg"
      alt="Structure Frequency sampling filter."
    />
  </figure>
</div>
The complex roots $\alpha_1$ and $\alpha^\ast_1$ occur each other conjugate versions and can be combined to form a second-order factor from which all coefficients are real, as shown in the following equation:
\begin{eqnarray*}
H(z)&=&
\left \{ \color{red}{\frac{1}{5} \cdot (1-z^{-5})} \right \}
\cdot \left \{ \color{blue}{
\frac{b_0 + b_1 z^{-1}}{1 - a_1 z^{-1} - a_2 z^{-2}}}
\right \}\newline
\text{with} && b_0=6 \text{ ; } b_1=-6\cos(\alpha_1)\text{ ; }a_1=2\cos(\alpha_1) \text{ ; } a_2=-1
\end{eqnarray*}
The realization scheme of this structure is depicted in the figure.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/Freqsampl2.svg"
      alt="Structure Frequency sampling filter."
    />
  </figure>
</div>
The zero of the resulting numerator polynomial is at $z=-\frac{b_1}{b_0} = \cos (\frac{2\pi}{5}) \approx 0.3$. Furthermore the pole zero plot shows the 5 equally distributed zeros over the unit circle, while the two poles at $e^{j\frac{2\pi}{5}}$ and $e^{-j\frac{2\pi}{5}}$ cancel the zeros.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/PZFreqsamplN5.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/filters/general/FreqsamplN5.svg"
    style="width:100%">
  </div>
</div>
</figure>
The magnitude response shows
the values of $5$ equally distributed frequencies $\theta = l \cdot \frac{2\pi}{5}$ are defined by the $5$ DFT weights $H[0]$ until $H[4]$.
</div>
</div>


<br></br>
## Lattice filter
A lattice filter has a modular structure. That means that a lattice consists of a number of cascaded modules and each module has the same structure. For example, the top of Fig. 9 shows a typical module of a lattice filter, which is a two port, with two inputs, two outputs, one delay and two multipliers with a factor $\Gamma_k$.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/LatticeFIR.svg"
      alt="Lattice FIR filter."
    />
  </figure>
  <figcaption class="numbered">
    Lattice FIR filter.
  </figcaption>
</div>
In most literature these parameters are denoted by reflection coefficients.
Since the module does not contain a feedback path the cascading of $p$ of such modules represent a $p^{th}$ order FIR filter, as shown at the bottom of Fig. 9.

In a similar way lattice filters can be used to implement All pole structures or structures with poles and zeros, as depicted in Fig. 10.
<figure>
<div class="rowimg2">
  <div class="rowimg2">
    <img src="/../files/7.Images/discrete/filters/general/LatticeAP.svg"
    style="width:100%">
  </div>
  <p></p>
  <div class="rowimg2">
    <img src="/../files/7.Images/discrete/filters/general/LatticeIIR.svg"
    style="width:100%">
  </div>
  <figcaption class="numbered">
    Lattice All Pole (top) and IIR filter (bottom).
  </figcaption>
</div>
</figure>
Lattice filters have a number of interesting and important properties that make them popular in a number of different applications. Besides the modularity property, the structure has low sensitivity to parameter quantization effects, and a simple criterion for ensuring filter stability.

### Example Lattice FIR filter
The following equations show the, coupled, difference equation of section $k$ of a lattice FIR filter:
\begin{eqnarray*}
f_k[n] &=& f_{k-1}[n] + \Gamma_k g_{k-1}[n-1] \newline
g_k[n] &=& g_{k-1}[n-1] + \Gamma_k f_{k-1}[n]
\end{eqnarray*}
When connecting the input $x[n]$ to both inputs of the first module, thus $F_0(z)=G_0(z)=X(z)$, the system function $A_k(z)$ relates the input $x[n]$ to the intermediate output $f_k[n]$. With $A_0(z)=1$, the system function $A_k(z)$ may be solved the given recurrence equation:
$$
F_k(z) = A_k(z) \cdot X(z) \hspace{3mm} \text{with }
A_k(z)= A_{k-1}(z) + \Gamma_k z^{-k} A_{k-1}(z^{-1})
$$
As an example of the second order Lattice FIR filter with reflection coefficients $\Gamma_1= \frac{1}{2}$ and $\Gamma_1= \frac{1}{4}$. The system function relating $x[n]$ to $f_1[n]$ is $A_1(z)$ and the second order system function relating $x[n]$ to $f_2[n]$ is  $A_2(z)$:
\begin{eqnarray*}
A_1(z) &=& A_0(z) + \Gamma_1 z^{-1} A_0(z^{-1}) = 1 + \frac{1}{2} z^{-1} \newline
A_2(z) &=& A_1(z) + \Gamma_2 z^{-2} A_1(z^{-1}) = 1 + \frac{5}{5} z^{-1} + \frac{1}{4} z^{-2}
\end{eqnarray*}
which represents the  non recursive second order transversal structure as depicted in Fig. 11.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/filters/general/LatticeExample.svg"
      alt="Example of Lattice structure of a non recursive second order transversal filter."
    />
  </figure>
  <figcaption class="numbered">
    Example of Lattice structure of a non recursive second order transversal filter.
  </figcaption>
</div>
