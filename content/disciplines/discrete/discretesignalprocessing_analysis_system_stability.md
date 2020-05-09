+++
title = "Stability and causality"

# date = {{ .Date }}
lastmod = 2020-05-09

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Stability and causality"
  weight = 2
  parent = "Analysis III: System function"
+++


In the module $Z$-transform we have discussed the importance of the Region Of Convergence (ROC).
Fig. 1 gives an impression of the Region Of Convergence of 4 different sequences, namely stable, non-stable, causal and non-causal sequences.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/ROCexamples.svg"
      alt="Impression of the Region Of Convergence (ROC) of stable, non-stable, causal and non-causal sequences."
    />
    <figcaption class="numbered">
      Impression of the Region Of Convergence (ROC) of stable, non-stable, causal and non-causal sequences.
    </figcaption>
  </figure>
</div>

<br></br>
## Bounded Input Bounded Output stability
In the module Systems we have seen that Bounded Input Bounded Output (BIBO) stability can very simply be tested by evaluating  the sum of absolute values of the impulse response weights as follows:
$$
\sum_{-\infty}^{\infty} |h[n]| < \infty
$$
Multiplying each value of the impulse response by $z^{-n}$ and evaluating the result around the unit circle does not change the test for BIBO stability:
$$
(\sum_{n=-\infty}^{\infty} |h[n]|z^{-n}) |\_{|z|=1} < \infty
\hspace{3mm} \Leftrightarrow \hspace{3mm} (H(z)) |\_{|z|=1} < \infty
$$
Thus BIBO stability implies that the evaluation of the system function $H(z)$ around the unit circle must result in a finite number. In other words:
$$\boxed{\color{red}{\text{ROC }H(z) \text{ must include }|z|=1}}$$
and as a result this excludes the upper right and lower left sequences out of the four possible sequences as depicted in Fig. 1.
Furthermore, it is obvious that no poles my lie inside the ROC:
$$\boxed{\color{red}{\text{No poles inside ROC}}}$$

<br></br>
## Causality
On the one hand in the module Systems we have seen that causality implies that the values of the impulse response $h[n]$ are zero for negative indices $n$. In other words the impulse response must be a right-sided sequence:
$$
h[n]=0 \text{ for } n < 0
$$
On the other hand from the module $Z$-transform we have seen that the $Z$-transform of such a right-sided sequence has a ROC which is outside a circle:
$$
\boxed{\color{red}{\text{ROC }H(z)\text{ exterior circle}}}
$$
which excludes the upper and lower right sequences out of the four possible sequences as depicted in Fig. 1.

<br></br>
## Realizability
A system can be realized in practice when the system is both stable and causal, which excludes the upper right
lower left and right sequences out of the four possible sequences as depicted in Fig. 1.
Thus all poles of a stable and causal LTI system $H(z)$ must lie inside the unit circle:

$$\boxed{\color{red}{\text{All poles must lie inside (or on) unit circle}}}$$
We will study the realizability in the following two examples: a first order and a second order system. These two systems are of special interest, because both first and second order systems are the basic building blocks for higher order systems.

### Realizability first order system
Fig. 2 shows a first order recursive filter with one feedback loop, which is weighted by the parameter $a$.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/example3.svg"
      alt="Example of a first order recursive system."
    />
    <figcaption class="numbered">
      Example of a first order recursive system.
    </figcaption>
  </figure>
</div>

Via the difference equation and its representation in the $Z$-domain,  we can find the system function $H(z)$  which has, besides a zero in $z=0$, one pole which is located at $z=a$.
$$
y[n] = x[n] + a y[n-1] \hspace{3mm} \circ  \hspace{-1.3mm} - \hspace{-1.3mm} \circ \hspace{3mm} Y(z) = X(z) + a z^{-1} Y(z)
$$
$$
H(z) = \frac{Y(z)}{X(z)}=\frac{1}{1 - a z^{-1}}
\hspace{5mm} \Rightarrow \text{ Pole @ } z=a
$$
According to the previous discussion, the system is both stable and causal, when the pole is within the unit circle. This implies that the absolute value of the feedback parameter $a$ of the given first order recursive system has to be smaller than 1:
$$
\Rightarrow \mbox{ System }\color{red}{\text{realizable}}\text{ for } |a| < 1
$$

#### Alternative view
An alternative view of the causal and stable properties of this first order system can be found as follows:
When the absolute value of the complex variable $z$ is larger than the absolute value of the feedback parameter $a$, the system function $H(z)$ can be expanded as the following geometric expression:
$$
H(z) = \frac{1}{1 - a z^{-1}}
\overset{|z| > |a|}{=} \sum_{k=0}^{\infty}  a^k z^{-k}
$$
Via the Inverse $Z$-transform this results in an exponential expression for the impulse response $h[n]$
$$
h[n]=\sum_{k=0}^{\infty} a^k \delta[n-k]
$$
From this expression it follows that the exponential function is a right sided and causal function, since the impulse response does not have negative indices and the first index is zero. Furthermore, when the absolute value of the feedback parameter $a$ smaller than 1, the exponential function is decaying and stable and indeed for $|a|<1$ the pole of the system is inside the unit circle and the unit circle is included in the ROC.

### Realizability second order system: Stability triangle
The system function of a second order feedback system, with the two feedback parameters $a_1$ and $a_2$, is as follows:
\begin{eqnarray*}
H(z) &=& \frac{1}{1 - a_1 z^{-1} - a_2 z^{-2}}
\end{eqnarray*}
The denominator can be spilt as a product of two first order systems with poles $\alpha_1$ and $\alpha_2$ as follows:
$$
H(z) = \frac{1}{(1 - \color{red}{\alpha_1} z^{-1})(1 - \color{red}{\alpha_2} z^{-1})}
$$
Combining these two expressions:
\begin{equation}\label{Eq:PolesHz}
H(z) = \frac{1}{1 - a_1 z^{-1} - a_2 z^{-2}}
= \frac{1}{1 - (\color{red}{\alpha_1} + \color{red}{\alpha_2}) z^{-1} + \color{red}{\alpha_1} \color{red}{\alpha_2} z^{-2}}
\end{equation}
leads to the following relations between the feedback parameters and the poles:
$$
a_1=\color{red}{\alpha_1} + \color{red}{\alpha_2} \mbox{ and } a_2=-\color{red}{\alpha_1} \color{red}{\alpha_2}
$$
Together with the fact that for a stable system both poles must lie inside the unit circle  this leads to the following restrictions for the feedback parameters:
$$
|a_2|<1 \hspace{2mm} \mbox{and} \hspace{2mm}
|a_1|< 1 - a_2
$$
These restriction can be represented in the so called 'stability triangle', as depicted in Fig. 3.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/StabTriangle.svg"
      alt="Stability triangle denoting the restriction of the feedback parameters of a second order system to be stable."
    />
    <figcaption class="numbered">
      Stability triangle denoting the restriction of the feedback parameters of a second order system to be stable.
    </figcaption>
  </figure>
</div>
Finally it is noted that the poles of equation (\ref{Eq:PolesHz}) can be found by the following expression:
$$
{\color{red}\alpha_{1,2}} = \frac{a_1}{2} \pm \frac{1}{2}\sqrt{a_1^2 + 4 a_2}
$$
From this it follows that the region for complex roots is defined by the area below the given parabola  $a_1^2 + 4 a_2=0$ as depicted in Fig. 3.

<div class="example">
<h4> Example </h4>
<hr>
Calculate the poles of the system as depicted in the following figure:
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/example4a.svg"
      alt="example4a."
    />
  </figure>
</div>
Furthermore calculate the system function $H(z)$ and the impulse response $h[n]$. Finally, what does the system represent.
<button class="collapsible">Show solution</button>
<div class="content">
The poles of the shown system can be found by first evaluating the system function:
\begin{eqnarray*}
H(z) &=& \frac{Y(z)}{X(z)}= \frac{z^{-1}}{1 - 2 \cos (\theta_0) z^{-1} + z^{-2}}
\end{eqnarray*}
By using the Euler expression for the $\cos (\theta_0)$ term  it follows that the system has two poles which are located on the unit circle at angles $\pm \theta_0$:
\begin{eqnarray*}
H(z) &=& \frac{z^{-1}}{1 - (e^{j\theta_0} + e^{-j\theta_0}) z^{-1} + z^{-2}} = \frac{z^{-1}}{(1 - e^{j\theta_0} z^{-1}) \cdot (1 - e^{-j\theta_0} z^{-1})}
\end{eqnarray*}
as depicted in the following Pole-Zero plot:
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/example4b.svg"
      alt="example4b."
    />
  </figure>
</div>
As discussed in the module about the $Z$-transform we can split this last expression for $H(z)$ into two first order terms
\begin{eqnarray*}
H(z) &=&\frac{1}{2 j \sin (\theta_0)} \left ( \frac{1}{1 - e^{j\theta_0} z^{-1}} + \frac{-1}{1 - e^{-j\theta_0} z^{-1}}\right )
\end{eqnarray*}
which leads via the Inverse $Z$ transform table to the following expression for the impulse response:
$$
h[n] = \color{blue}{c} \cdot \color{red}{\sin (n \cdot \theta_0)} u[n]
\hspace{3mm} \mbox{with constant} \hspace{3mm} \color{blue}{c=\frac{1}{\sin (\theta_0)}}
$$
The system represents a discrete oscillator: In other words,
when starting with an empty system and using a delta pulse as input, the system generates an output signal $y[n]$ which behaves as a sinusoidal signals with frequency $\theta_0$. The amplitude of this sinusoidal signal is equal to the contant $c$  which is equal to 1 divided by  $\sin(\theta_0)$
</div>
</div>
