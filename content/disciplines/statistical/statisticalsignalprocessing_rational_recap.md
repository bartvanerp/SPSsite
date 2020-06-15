+++
title = "Recap: LTI systems "         # name of webpage

# date = {{ .Date }}
lastmod = 2020-05-22

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.

[menu.statistical]                       # name of menu section (main module)
  name = "Recap: LTI systems"        # name of this item in that menu
  weight = 1                           # location in that menu
  parent = "Rational signal models"

+++

This section contains a selection of the material from the module on <a href="../../discrete/discretesignalprocessing_systems_main">discrete-time systems</a>, which provides a brief recap of the general form and properties of linear time-invariant systems.

<br></br>

## Linearity and time-invariance

A linear time-invariant system is a system having both the properties of linearity and time-invariance, which are described hereafter.

### Linearity

A system is regarded to be linear if it is both additive and homogeneous. Suppose that we have a system, which we provide separately with two distinct input signals $x_1[n]$ and $x_2[n]$. These signals are individually transformed by the system into two output signals, $y_1[n]$ and $y_2[n]$ respectively. This can be represented intuitively as
\begin{equation}
    x_1[n] \rightarrow y_1[n] \quad \text{and} \quad x_2[n] \rightarrow y_2[n].
\end{equation}

This system is called additive if and only if the output of this system equals the sum of the individual outputs when driven by the sum of the two distinct inputs. In other words, when the individual input signals are simultaneously applied to the system, the respective outputs are also observed simultaneously. This can be represented as
\begin{equation}
    \text{Additive:} \quad x_1[n] + x_2[n] \rightarrow y_1[n] + y_2[n].
\end{equation}

Furthermore, this system can be called homogeneous if and only if the output of this system contains a identically scaled output when driven by a scaled input. In other words, when the input signal is scaled with some scaling coefficient $c$, the output is also scaled with the same scaling coefficient. This can be represented as
\begin{equation}
    \text{Homogeneous:} \quad c \cdot x_1[n] \rightarrow c \cdot y_1[n].
\end{equation}

When a system is both additive and homogeneous, the system is linear. This is represented as
\begin{equation}
    \text{Linear:} \quad \alpha \cdot x_1[n] + \beta \cdot x_2[n] \rightarrow \alpha \cdot y_1[n] + \beta \cdot y_2[n],
\end{equation}
where $\alpha$ and $\beta$ are scaling coefficients.


### Time-invariance

Another system property is time invariance. This property concerns signal delays or temporal shifts. A system is called time invariant if a temporal shift in the input signal results in the same temporal shift in the respective output signal. This can be represented as
\begin{equation}
    \text{Time-invariance:} \quad x[n-n_0] \rightarrow y[n-n_0],
\end{equation}
where $n_0$ represents the temporal shift.

### System architecture

A general LTI system can be represented using a so-called signal flow diagram as in Fig. 1. The system is driven by an input signal $x[n]$ and outputs the signal $y[n]$. The output is obtained by the addition of two main branches. The upper branch, which is connected to the input signal, transforms the input and delayed inputs into an output. This branch is also called the moving-average part of the system. The lower branch, which is connected to the output signal, transforms delayed outputs into a new output. This branch is also called the auto-regressive part of the system. A more detailed explanation of the individual building blocks can be found <a href="../../discrete/discretesignalprocessing_systems_visualization">here</a>.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/flowdiagram.svg"
      alt="Signal flow diagram of an LTI system."
    />
    <figcaption class="numbered">
      Signal flow diagram of an LTI system.
    </figcaption>
  </figure>
</div>


<br></br>

## Difference equation

The operations of the system can be represented mathematically by the weighted sum of the current input and delayed versions of the input and delayed outputs. This mathematical description is called the difference equation. The output $y[n]$ at sample index $n$ can be calculated as
\begin{equation}\label{eq:DE}
    y[n] = \underbrace{\sum_{k=0}^{M-1} b_k x[n-k]}_\text{moving-average}  + \underbrace{\sum_{k=1}^{N-1} a_k y[n-k]}_\text{auto-regressive},
\end{equation}
where two distinct terms can be distinguished between. First is the moving-average part, which represents the upper branch of Fig. 1, and secondly follows the auto-regressive part, which represents the lower branch of Fig. 1. The weights are represented by the coefficients $a_k$ and $b_k$.

<br></br>

## Impulse response

Besides the difference equation, there is another way of describing the functioning of a system. This representation is called the impulse response and will prove useful in the following sections. The impulse response is the output, or response, of a system when driven by a short impulse $\delta[n]$ and is denoted by $h[n]$. This can be described intuitively as
\begin{equation}
    \delta[n] \rightarrow h[n],
\end{equation}
where $\delta[n]$ represents the Dirac delta pulse, which is defined as
\begin{equation}
    \delta[n] =
    \begin{cases}
        1, & \text{for } n=0, \newline
        0, & \text{elsewhere}.
    \end{cases}
\end{equation}
Another way of representing the definition of the impulse response is
\begin{equation}
    h[n] = y[n]\bigg\rvert_{x[n] = \delta[n]},
\end{equation}
which simply states that the impulse response is the output of a system when the input of that system is given by a Dirac delta pulse.

The impulse response can be metaphorically compared with a tuning fork. A tuning fork is used to tune an instrument. The fork is hit against another object, after which it will resonate at a specific frequency. This frequency is used as a guideline for the tuning of an instrument. This can be compared to the discussion of the impulse response. The system (the tuning fork) is excited with an impulse (hitting it against a solid object) and will output a signal, also called the impulse response (the sound signal at the resonant frequency).

<br></br>

## FIR and IIR filters

From the representation of the general LTI system, two different types of systems can be distinguished between. These two types are finite impulse response (FIR) filters and infinite impulse response (IIR) filters. As the name indicates, the distinction is based on the length of the impulse response.

FIR filters are discussed in more detail <a href="../../discrete/discretesignalprocessing_analysis_fir_main">here</a>. FIR filters are the class of filters in which all auto-regressive coefficients $a_k$ are equal to zero. These filters effectively only contain the upper branch of the signal flow diagram in Fig. 1. If this class of filters is excited by an impulse, this signal will pass through the upper branch and is delayed a total of $M-1$ times. Besides that, a weighted version of the signal is also directed to the output of the system. Mathematically, the impulse response of an FIR filter can be determined by substituting $\delta[n]$ for $x[n]$ in \eqref{eq:DE} and by setting all auto-regressive coefficients $a_k$ to zero as
\begin{equation}
    \begin{split}
        h[n]
        &=  \sum_{k=0}^{M-1} b_k \cdot \delta[n-k]  + \sum_{k=1}^{N-1} 0 \cdot y[n-k], \newline
        &= \sum_{k=0}^{M-1} b_k \cdot \delta[n-k] = b_n.
    \end{split}\label{eq:impulse_FIR}
\end{equation}
The last step in this equation can be understood by noting that $\delta[n-k]$ only equals $1$ when $n=k$ holds. From this it can be noted that the length of the impulse response depends on the number of moving-average weights $b_k$. The number of moving-average weights $b_k$ depends on the length of the upper branch of the filter, which should be finite to allow for a practical implementation. Therefore the number of moving-average weights is also finite, leading to finite impulse response given by \eqref{eq:impulse_FIR}.

IIR filters on the other hand, contain non-zero auto-regressive coefficients. Intuitively one could understand the consequence of this by paying close attention to the created feedback loop in the system, corresponding to the lower branch in the signal flow diagram in Fig. 1. Suppose an impulse is applied to the input of an IIR filter. This signal will propagate through the moving-average branch (or directly, when only $b_0$ is non-zero) to the output. Since at least one of the auto-regressive coefficients is non-zero, this output will pass through the auto-regressive branch back to the output and the signal will therefore keep propagating through the feedback loop and will keep generating outputs. By applying a single impulse at the input of the system, the system will keep generating outputs, leading to an infinitely long impulse response.

In the following example we will derive the impulse response of a simple system with a non-zero auto-regressive coefficient.


<div class="example">
<h4> Example </h4>
<hr>
Calculate the analytical impulse response of a first-order auto-regressive filter.
<br>
<button class="collapsible">Show solution</button>
<div class="content">
A first-order auto-regressive filter is defined as a system where the moving-average coefficients are all zero, except for $b_0$, which equals $1$, and where all auto-regressive coefficients are zero, except for $a_1$. Without the coefficient $b_0$, no signal would propagate to the output of the system and therefore there would be no influence of the auto-regressive portion. This definition gives rise to the corresponding difference equation
\begin{equation*}
    y[n] = x[n] + a_1 y[n-1].
\end{equation*}


Let us first calculate the first outputs of the system when driven by an input $x[n]$ to get some intuition of an auto-regressive process. If an arbitrary input signal $x[n]$ would be applied to the system, the first output of the system would be calculated as
\begin{equation*}
    y[0] = x[0] + a_1 y[-1] = x[0] + a_1 0 = x[0],
\end{equation*}
where the signal output is assumed to be $0$ for $n < 0$
From this first output of the system, the second output can be determined as
\begin{equation*}
    y[1] = x[1] + a_1 y[0] = x[1] + a_1  x[0]
\end{equation*}
and the third output as
\begin{equation*}
    y[2] = x[2] + a_1 y[1] = x[2] + a_1  \left( x[1] + a_1  x[0] \right) = x[2] + a_1x[1] + a_1^2 x[0].
\end{equation*}
Through these iterations the reader should be able to see some structure in the output signal. Using this structure an equation for the output $y[n]$ can be found as
\begin{equation}
    y[n] =
    \begin{cases}
        \displaystyle \sum^{n}_{k=0} a_1^k x[n-k], &\text{for } n\geq 0, \newline   
        0, & \text{for } n < 0.
    \end{cases}
\end{equation}
By using the definition of the unit step function $u[n]$, this can also be written as
\begin{equation*}
    y[n] = u[n]\sum^{n}_{k=0} a_1^k x[n-k].
\end{equation*}

Since the impulse response of the system is defined as the output of the system when driven by a Dirac delta pulse, i.e. $x[n] = \delta[n]$, the impulse response can be found as
\begin{equation}
    h[n] =
    u[n] \cdot a_1^n =
    \begin{cases}
        a_1^n,  &\text{for } n\geq 0, \newline
        0,      &\text{for } n<0.
    \end{cases}
\end{equation}
Based on the value of $a_1^n$ the impulse response will have a different shape. The figure below shows several examples of possible impulse response for different values of $a_1^n$.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/impulse_response_AR1.svg"
      alt="Different impulse responses for a first-order auto-regressive filter, depending on the value of the auto-regressive coefficient $a_1$."
    />
    <figcaption>
      Different impulse responses for a first-order auto-regressive filter, depending on the value of the auto-regressive coefficient $a_1$.
    </figcaption>
  </figure>
</div>

</div>
</div>

## System invertibility

A system $H(z)$ is invertible if the output $y[n] (n=(-\infty, \infty))$ can be used to uniquely define the input $x[n] (n=(-\infty, \infty))$. This is only possible if every unique value in $x[n]$ maps to a unique value in $y[n]$. This is called one-to-one mapping. Obtaining the inverse for any system is very difficult. However, if the system is linear time-invariant with an impulse response $h[n]$, the inverse $h_{inv}[n]$ can be defined as follows

\begin{equation*}
\begin{split}
    x[n] \ast h[n] &= y[n]\newline
    y[n] \ast h_{inv}[n] &= x[n]\newline
    x[n] &= (x[n]\ast h[n])\ast h_{inv}[n]
\end{split}
\end{equation*}
This can be simplified by utilizing the z-transform.
\begin{equation*}
\begin{split}
    X(z) H(z) &= Y(z)\newline
    Y(z) H_{inv}(z) &= X(z)\newline
    X(z) &= X(z) H(z) H_{inv}(z)\newline
    H_{inv}(z) &= \frac{1}{H(z)}
\end{split}
\end{equation*}
If the systems consists of poles and zeros, than it can be split into its denominator and numerator.
\begin{equation*}
\begin{split}
    H(z) = \frac{N(z)}{D(z)}\newline
    H_{inv}(z) = \frac{D(z)}{N(z)}
\end{split}
\end{equation*}

Thus, the poles of the system become zeros in its inverse and vice versa.
However the inverse is not always uniquely defined for every system, as shown by the following example.

<div class="example">
<h4> Example </h4>
Consider a system with the impulse response $h[n] = \delta[n]-\frac{1}{4}\delta[n-1]$. By performing the z-transform we end up with $H(z)=1-\frac{1}{4}z^{-1}$. Therefore, the inverse is equal to $H_{inv}(z)= \frac{1}{1-\frac{1}{4}z^{-1}}$, which has one pole at $z=\frac{1}{4}$.

If we choose the region of convergence (ROC) as $|z| > \frac{1}{4}$, the inverse system is causal and stable, and

\begin{equation*}
    h_{inv}[n] = (\frac{1}{4})^n u[n]
\end{equation*}
However, if we choose the ROC as $|z| < \frac{1}{4}$, the inverse system is noncausal and unstable
\begin{equation*}
    h_{inv}[n] = -(\frac{1}{4})^n u[-n-1]
\end{equation*}



</div>
</div>

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

## Minimum phase systems

The simple example above illustrates that the knowledge of the impulse response of a LTI system does not uniquely specify its inverse. Additional information such
as causality and stability would be helpful in many cases. This leads us to the concept of minimum-phase systems.

A minimum phase system is a system in which the system and its inverse are both stable and causal. To understand what this means we first need to know the conditions for stability and causality.

<ul>

<li style="margin-top:10px;"> <b>Stability</b>, in a stable system the ROC contains the unit circle. </li>

<li style="margin-top:10px;"> <b>Causal</b>, in a causal system the ROC is defined as going outward from a circle, with a radius larger than the largest pole in the system (excluding poles at infinity). </li>

<li style="margin-top:10px;"> <b>Anti-causal</b>, in an anti-causal system the ROC is defined as going inward from a circle, with a radius smaller than the smallest pole (excluding poles at zero). </li>

</ul>

Therefore, if a systems is minimum phase, its poles and zeros have the following properties. The ROC extends outwards from a circle with a radius larger than the largest pole, since the system needs to be causal. The system also needs to be stable. Therefore, the ROC includes the unit circle. Thus, the largest pole, and therefore all poles, need to be within the unit circle. The zeros need to be within the unit circle as well, since these rules also apply to the inverse.

Using these rules we can also define a maximum phase system in which the system and its inverse are stable and anti-causal. In this system all poles and zeros need to be outside of the unit circle.

### Minimum phase and all-pass decomposition

Now with the knowledge that we have about minimum phase and all-pass systems, we are able to show that you can decompose any causal poles and zeros system (without poles or zeros on the unit circle) using these two system types.  

Let $H(z)$ be a non-minimum phase system with one zero $z=\frac{1}{a}, |a|<1$, outside the unit circle and all other poles and zeros on the inside of the unit circle.
