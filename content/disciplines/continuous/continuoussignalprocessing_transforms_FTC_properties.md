+++
title = "FTC properties"

# date = {{ .Date }}
lastmod = 2020-02-29

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "FTC properties"
  weight = 3
  parent = "Transforms III: Fourier transform for continuous-time signals"
+++

In this section we will discuss the main properties of the FTC.

<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/rz5kJ13gMck" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Linearity
As a result of the fact that the integration operation of the FTC is a linear operation it follows that the FTC is linear.
\begin{eqnarray}
x(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ X(f) \quad\text{ and }\quad y(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ Y(f)
\end{eqnarray}
$$
\boxed{
\begin{eqnarray}
a \cdot x(t) + b \cdot y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
a \cdot X(f) + b \cdot Y(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of linearity property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
\begin{eqnarray}
  \mathcal{F}\{a \cdot x(t) + b \cdot y(t)\} &&=\int_{-\infty}^{\infty} \left ( a \cdot x(t) + b \cdot y(t) \right ) e^{-j2 \pi f t}  \text{d} t  \\
&&=  \int_{-\infty}^{\infty} \left ( a \cdot x(t) \right ) e^{-j2 \pi f t}  \text{d} t +
 \int_{-\infty}^{\infty} \left ( b \cdot y(t) \right ) e^{-j2 \pi f t}  \text{d} t  \\
&&= a \cdot \int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t +
 b \cdot \int_{-\infty}^{\infty} y(t) e^{-j2 \pi f t}  \text{d} t \\
&&= a \cdot X(f) + b \cdot Y(f)
\end{eqnarray}
The linearity property implies that of the sum of signals equals the sum of the FTC's of the signals.
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
As an example of this linear property we calculate the FTC of a sinusoidal signal.
By using Euler we can write the signal into two phasors.
Each of these phasors transforms into a delta pulse in frequency domain.
\begin{eqnarray}
\text{Euler } \rightarrow \text{ }\cos(2 \pi f_0 t) &=& \frac{1}{2} e^{j2 \pi f_0 t}+\frac{1}{2} e^{-j2 \pi f_0 t}  \\
e^{j2 \pi f_0 t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& \delta(f-f_0)  \\
e^{-j2 \pi f_0 t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& \delta(f+f_0)
\end{eqnarray}
By using the linearity property we can now write the FTC of the sum of phasors  as the sum of the FTC's of the two individual phasors.
\begin{eqnarray}
\Rightarrow \text{ } \mathcal{F}\{\cos(2 \pi f_0 t)\} &=& \mathcal{F}\{\frac{1}{2} e^{j2 \pi f_0 t}+\frac{1}{2} e^{-j2 \pi f_0 t}\}\\
&=& \frac{1}{2} \mathcal{F}\{e^{j2 \pi f_0 t}\}+\frac{1}{2} \mathcal{F}\{e^{-j2 \pi f_0 t}\}\\
&=& \frac{1}{2}\delta(f-f_0) + \frac{1}{2}\delta(f+f_0)
\end{eqnarray}
Thus the FTC of a cosine signal consists of  a sum of two delta pulses in the frequency domain.
</div>
</div>


<br></br>

## Conjugation
$$
\boxed{
\begin{eqnarray}
x^\ast(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  X^\ast(-f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of conjugation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the conjugation property  is to move the conjugation sign outside the integral.  Inside the brackets this results into an FTC from which the phasor has a positive sign, which writes as $X(-f)$.
\begin{eqnarray}
y(t) = x^\ast(t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ
Y(f)&=&\int_{-\infty}^{\infty} x^\ast(t) e^{-j2 \pi f t} \text{d} t
= \left ( \int_{-\infty}^{\infty} x(t) e^{j2 \pi f t} \text{d} t \right )^*  \\
&=& \left ( X(-f) \right )^\ast=X^\ast(-f)
\end{eqnarray}
The final notation $X^\ast(-f)$  is just simpler way of the notation $(X(-f))^\ast$.
An important result of this conjugation property is that FTC $X(f)$ of a real signal $x(t)$, thus when $x(t)=x^\ast(t)$, has the following symmetry properties:
\\
The magnitude response is symmetric, while the phase response is anti-symmetric, thus:
$$
x(t) \text{ real } \Rightarrow \hspace{2mm} x(t)=x^\ast(t) \hspace{2mm} \Rightarrow  \hspace{2mm} X(f)=X^\ast(-f) \hspace{2mm} \Rightarrow
$$
\begin{eqnarray}
|X(f)| = |X(-f)| &:& \quad\textbf{Magnitude response symmetric}\\
\angle \{X(f)\} = - \angle \{X(f)\} &:& \quad\textbf{Phase response anti-symmetric}
\end{eqnarray}
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
A simple example of these symmetry properties can be found in the FTC of a shifted delta pulse. For this case the time domain signal is a real and the FTC results in a complex exponent as follows:
\begin{eqnarray}
x(t)=\delta(t-t_0) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ X(f)&= \int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t} \text{d} t  \\
&&= \int_{-\infty}^{\infty} \delta(t-t_0) e^{-j2 \pi f t} \text{d} t
= e^{-j2 \pi f t_0}
\end{eqnarray}
From this result it folows that the magnitude response equals 1, while the phase response equals $-2\pi t_0$.
\begin{eqnarray}
\textbf{Symmetric Magnitude response} &:& \quad |X(f)|=|e^{-j2 \pi f t_0}|=1  \\
\textbf{Anti-symmetric Phase response} &:& \quad \angle \{X(f)\} = -2 \pi t_0
\end{eqnarray}
A plot of this magnitude- and phase response is depicted in the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCshiftedDelta.svg"
      alt="Magnitude and phase response of shifted delta pulse."
    />
    <figcaption>
      Magnitude and phase response of shifted delta pulse.
    </figcaption>
  </figure>
</div>
From this plot the symmetry properties are clearly visible.
Note finally that for this case the angle of the phase response is directly related to the shift in time domain.
</div>
</div>

## Scaling
$$
\boxed{
\begin{eqnarray}
x(k \cdot t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{1}{|k|} X(f/k)
\hspace{3mm} \text{with } k \neq 0
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of scaling property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
$$
y(t) = x(k \cdot t) \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ Y(f) = \int_{-\infty}^{\infty} x(k \cdot t) e^{-j2 \pi f t}
$$
For the proof of the scaling property it is the easiest to split the proof into two cases.
For $k>0$ we substitute for the scaled variable $k \cdot t$ a new variable $\tau$ which leads straightforward to the following result:
$$
Y(f) \overset{\tau =k \cdot t}{=} \int_{-\infty}^{\infty} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \cdot \frac{1}{k} \text{d} \tau
= \frac{1}{k} X(\frac{f}{k})
$$
For $k<0$ we follow the same procedure. But now the boundaries of the integral are changed. Changing these boundaries causes an extra minus sign. As a last step we take the absolute value of $k$ which combines the negative sign together with the negative value of $k$.
\begin{eqnarray}
Y(f) &\overset{\tau =k \cdot t}{=}& \int_{{\color{red}+\infty}}^{{\color{red}-\infty}} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \cdot \frac{1}{k} \text{d} \tau  \\
&=& \frac{{\color{red}-1}}{k} \int_{{\color{red}-\infty}}^{{\color{red}+\infty}} x(\tau) e^{-j2\pi f \frac{1}{k} \tau} \text{d} \tau = \frac{1}{|k|} X(\frac{f}{k})
\end{eqnarray}
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
previously we have shown that the FTC of a block signal results in a sinc function, as given in the following equation and depicted in  the figure below.
$$
x(t)= \begin{cases}
1 & \text{for } -\frac{T_0}{2} < t < \frac{T_0}{2} \\
0 & \text{elsewhere}
\end{cases}
\hspace{3mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{3mm}
X(f) = T_0 \frac{\sin (\pi f T_0)}{\pi f T_0}
$$
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCscaledBlock.svg"
      alt="Result of scale operation applied to a block function."
    />
    <figcaption>
      Result of scale operation applied to a block function.
    </figcaption>
  </figure>
</div>
The figure shows an example in which applied a scale factor of 2: The time domain signal has shrunk by a factor of 2, while the frequency domain signal is stretched by a factor 2.
</div>
</div>
This leads to the following important "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Shrinking in one domain implies stretching in the other domain.</i></div>

<br></br>

## Shift properties

### Time domain shift
$$
\boxed{
\begin{eqnarray}
x(t-t_0) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  e^{-j2 \pi f t_0} \cdot X(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of time shifting property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof is to change everywhere the variable $t$ by $t-t_0$.
\begin{eqnarray}
x(t-t_0) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \int_{-\infty}^{\infty} x(t-t_0) e^{-j2 \pi f t} \text{d} t \\
&=& \int_{-\infty}^{\infty} x(\color{red}{t-t_0}) e^{-j2 \pi f (\color{red}{t-t_0}+ \color{blue}{t_0})} \text{d} (\color{red}{t-t_0})
\end{eqnarray}
In the next step we take out the negative exponent with the term $t_0$ and substitute $t-t_0$ by $\tau$, which leads to the final result as follows:
\begin{eqnarray}
&\overset{\color{red}{\tau}=t-t_0}{=}&  e^{-j2 \pi f \color{blue}{t_0}} \cdot \int_{-\infty}^{\infty} x(\color{red}{\tau}) e^{-j2 \pi f \color{red}{\tau}} \text{d} {\color{red}\tau} \\
&=& e^{-j2 \pi f t_0} \cdot X(f)
\end{eqnarray}
</div>
</div>

### Frequency domain shift
$$
\boxed{
\begin{eqnarray}
e^{j2 \pi f_0 t} \cdot x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &   X(f-f_0)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of frequency shifting property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The steps of this proof are similar to the previous ones and are as follows:
\begin{eqnarray}
\mathcal{F}^{-1}\{X(f-f_0)\} &=& \int_{-\infty}^{\infty} X(f-f_0) e^{j2 \pi f t} \text{d} f \\
&=& \int_{-\infty}^{\infty} X({\color{red}f-f_0}) e^{j2 \pi ({\color{red}f-f_0} + {\color{blue}f_0}) t} \text{d} ({\color{red}f-f_0}) \\
&\overset{{\color{red}\eta}=f-f_0}{=}&  e^{j2 \pi {\color{blue}f_0} t} \cdot \int_{-\infty}^{\infty} X({\color{red}\eta}) e^{j2 \pi {\color{red}\eta} t} \text{d} {\color{red}\eta}
= e^{j2 \pi f_0 t} \cdot x(t)
\end{eqnarray}
</div>
</div>


### Modulation
A result of this frequency shift property is the following modulation property:
\begin{eqnarray}
e^{j2 \pi f_0 t} \cdot x(t) + e^{-j2 \pi f_0 t} \cdot x(t)
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&   X(f-f_0) + X(f+f_0)  \newline
\Leftrightarrow \hspace{3mm} 2 {\color{red}\cos (2 \pi f_0 t) \cdot } x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &   X(f-f_0) + X(f+f_0)
\end{eqnarray}
Thus when multiplying, or modulating, a signal $x(t)$ with a sinusoidal signal, the result in the frequency domain is a sum of two shifted versions of the FTC $X(f)$ of signal $x(t)$ which results into the following "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Modulation in one domain is shifting in the other domain..</i></div>

<br></br>

## Convolution

### Time domain convolution
$$
\boxed{
\begin{eqnarray}
x(t) \star y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  X(f) \cdot Y(f)
\end{eqnarray}}
$$
<div class="example">
<h4> Proof of time domain convolution property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the time domain convolution property is to use the definition of the convolution integral into the FTC definition.
\begin{eqnarray}
\mathcal{F}\{\color{red}{x(t) \star y(t)}\} &=& \int_{t=-\infty}^{\infty} \left ( {\color{red}\int_{\tau= -\infty}^{\infty} x(\tau) y(t-\tau) \text{d} \tau }\right ) e^{-j2 \pi f t} \text{d} t
\end{eqnarray}
Then by interchanging the order of the integrals  and introducing in the second integral everywhere the variable $t-\tau$, this results in an extra phasor component $e^{-j2 \pi f \tau}$ in the first integral.
\begin{eqnarray}
\ldots
&=& \int_{\tau=-\infty}^{\infty} x(\tau) \left ( \int_{t=-\infty}^{\infty}  y(t-\tau)
e^{-j2 \pi f t} \text{d} t \right ) \text{d} \tau \\
&=& \int_{\tau=-\infty}^{\infty} x(\tau) e^{-j2 \pi f {\color{red}\tau}} \left ( \int_{t=-\infty}^{\infty}  y(t-\tau) e^{-j2 \pi f (t-{\color{red}\tau}) } \text{d} t \right ) \text{d} \tau
\end{eqnarray}
Finally by substituting $t-\tau$ by a new variable  $p$ we obtain the final result.
\begin{eqnarray}
\ldots &=& \left ( \int_{\tau=-\infty}^{\infty} x(\tau) e^{-j2 \pi f \tau} \text{d} \tau \right ) \cdot \left ( \int_{p=-\infty}^{\infty}  y(p) e^{-j2 \pi f p } \text{d} p \right ) \\
&=& X(f) \cdot Y(f)
\end{eqnarray}
</div>
</div>


### Frequency domain convolution
$$
\boxed{
\begin{eqnarray}
x(t) \cdot y(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(f) \star Y(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of frequency domain convolution property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
The first step of the proof of the frequency domain convolution property is  to use the definition of Inverse FTC for the signal $x(t)$.
\begin{eqnarray}
\mathcal{F}\{x(t) \cdot y(t)\} &=& \int_{t=-\infty}^{\infty} \color{red}{x(t)} \cdot y(t) e^{-j2 \pi f t} \text{d} t\\
&=& \int_{t=-\infty}^{\infty} \left ( \color{red}
{\int_{\eta=-\infty}^{\infty} X(\eta) e^{j2 \pi \eta t} \text{d} \eta }
\right ) \cdot y(t) e^{-j2 \pi f t} \text{d} t
\end{eqnarray}
Then by interchanging the order of the integrals and  combining the two phasor components of the second integral we obtain (in red) the shifted FTC of the signal $y(t)$. The resulting integral is the convolution integral of $X(f)$ with $Y(f)$.
\begin{eqnarray}
\ldots&=& \int_{\eta=-\infty}^{\infty} X(\eta) \left (
\int_{t=-\infty}^{\infty} y(t) e^{j2 \pi \eta t} e^{-j2 \pi f t} \text{d} t
\right ) \text{d} \eta \\
&=& \int_{\eta=-\infty}^{\infty} X(\eta) \left ( \color{red}{
\int_{t=-\infty}^{\infty} y(t) e^{-j2 \pi (f- \eta) t} \text{d} t }
\right ) \text{d} \eta \\
&=& \int_{\eta=-\infty}^{\infty} X(\eta) \color{red}{Y(f-\eta)} \text{d} \eta
= X(f) \star Y(f)
\end{eqnarray}
</div>
</div>

This leads to the following important "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication in one domain results in convolution in the other domain.</i></div>

<div class="example">
<h4> Example </h4>
<hr>
<button class="collapsible">Show example</button>
<div class="content">
As an example of the convolution property we will use the modulation property as discussed before. In this example signal $x(t)$ is a sinc function as depicted in the upper left side of the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/FTCModulateSinc.svg"
      alt="Modulation in time domain results in frequency shifts of the spectrum."
    />
    <figcaption>
      Modulation in time domain results in frequency shifts of the spectrum.
    </figcaption>
  </figure>
</div>
Previously we have shown that the sinc function is the result of the IFTC of a frequency domain block function, as depicted on in the upper right side of the figure. Multiplying signal $x(t)$ with a sinusoidal signal with frequency $f_0$, which is a modulation operation, is according to the last "rule of thumb" equivalent to the convolution of the FTC $X(f)$ with the FTC of the sinusoidal. The FTC of the sinusoidal consists of two delta pulses, $\delta(f-f_0)$ and $\delta(f+f_0)$, as depicted in the middle part of the figure. Convolving $X(f)$ with a delta pulse results in a shift, which can be shown as follows:
\begin{eqnarray}
\delta(f \pm f_0) \star X(f) &=& \int_{\eta=-\infty}^{\infty} \delta(\eta \pm f_0) X(f-\eta) \text{d} \eta = X(f \pm f_0)
\end{eqnarray}
The result is shown in the lower part of the figure.
</div>
</div>




<br></br>

## Differentiation

### Time domain differentiation
$$
\boxed{
\begin{eqnarray}
\frac{\text{d} }{\text{d} t} x(t) & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & j \omega X(f)
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of time domain differentiation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
By using the IFTC definition of $x(t)$ and differentiating both sides with respect to $t$ we obtain:
$$
\frac{\text{d} }{\text{d} t} x(t) = \frac{\text{d} }{\text{d} t} \left (
\int_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f \right )
= \int_{-\infty}^{\infty} X(f) (j 2 \pi f) e^{j2 \pi f t} \text{d} f
= \mathcal{F}^{-1}\{j \omega X(f) \}
$$
</div>
</div>

<div class="example">
<h4> Example </h4>
<hr>
Find the FTC of the signal $x(t)= \frac{\text{d} }{\text{d} t} \delta(t)$.
<button class="collapsible">Show example</button>
<div class="content">
Taking the FTC of both sides gives:
$$
X(f)= \mathcal{F}\{\frac{\text{d} }{\text{d} t} \delta(t)\}  = j \omega \cdot \mathcal{F}\{ \delta(t) \} = j \omega \cdot 1 = j \omega
$$
</div>
</div>


### Frequency domain differentiation
$$
\boxed{
\begin{eqnarray}
t x(t)  & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f)
\end{eqnarray}}
$$


<div class="example">
<h4> Proof of frequency domain differentiation property </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
Differentiation of both sides of the FTC difinition gives:
\begin{eqnarray*}
\frac{\text{d}}{\text{d} f} X(f) &=& \int_{-\infty}^{\infty} x(t) (-j 2 \pi t) e^{-j2 \pi f t}  \text{d} t = - j 2 \pi \int_{-\infty}^{\infty} t x(t)  e^{-j2 \pi f t}  \text{d} t = - j 2 \pi \mathcal{F}\\{t x(t)}
\end{eqnarray*}
Finally, multiplying both sides by the complex number $j$ results into:
$$
\frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f) = \mathcal{F}\\{t x(t)}
$$
</div>
</div>


<div class="example">
<h4> Example </h4>
<hr>
Find the FTC of $x(t) = t \cos(2 \pi F_0 t)$
<button class="collapsible">Show example</button>
<div class="content">
\begin{eqnarray}
X(f) &=& \mathcal{F}\{t \cos(2 \pi F_0 t)\} = \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f}
\left [\mathcal{F}\{ \cos(2 \pi F_0 t)\} \right ] \\
&=& \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} \left [
\frac{1}{2} \delta(f-F_0) + \frac{1}{2} \delta(f+F_0) \right ]
\end{eqnarray}
</div>
</div>


<br></br>

## Theorem Parseval
$$
\boxed{
\begin{eqnarray}
\int\_{-\infty}^{\infty} |x(t)|^2 \text{d} t &=& \int\_{-\infty}^{\infty} |X(f)|^2 \text{d}f
\end{eqnarray}}
$$

<div class="example">
<h4> Proof of the Parseval theorem </h4>
<hr>
<button class="collapsible">Show proof</button>
<div class="content">
In the first step of the proof we replace the complex conjugated version of $x(t)$ by the IFTC of the FTC of $x^\ast(t)$.
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t &=& \int_{-\infty}^{\infty} x(t) \color{red}{x^\ast(t)} \text{d} t
= \int_{-\infty}^{\infty} x(t) \mathcal{F}^{-1}\{ \color{red}{\mathcal{F} \{x^\ast(t)\}}\} \text{d} t
\end{eqnarray}
Using the FTC property of complex conjugation  and then applying the IFTC to this result gives:
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t
&=&\int_{-\infty}^{\infty} x(t) \mathcal{F}^{-1}\{\color{red}{ X^\ast(-f)}\} \text{d} t \\
&=& \int_{-\infty}^{\infty} x(t) \left (
\int_{-\infty}^{\infty} X^\ast(-f) e^{j2 \pi f t} \text{d} f \right ) \text{d} t
\end{eqnarray}
Finally interchanging the variable $-f$ by $f$ and then interchanging the order of the integrals and using the FTC definition leads to the final result.
\begin{eqnarray}
\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t
&=& \int_{-\infty}^{\infty} x(t) \left (
\int_{-\infty}^{\infty} X^\ast(f) e^{-j2 \pi f t} \text{d} f \right ) \text{d} t \\
&=& \int_{-\infty}^{\infty} X^\ast(f)  \left ( \color{red}{
\int_{-\infty}^{\infty} x(t) e^{-j2 \pi f t} \text{d} t } \right ) \text{d} f \\
&=& \int_{-\infty}^{\infty} |X(f)|^2 \text{d} f
\end{eqnarray}
</div>
</div>

Concluding it follows that the theorem of Parseval states that the energy in time- and frequency-domain is the same. This implies that the FTC cannot introduce or lose energy, which leads to the following "rule of thumb":
<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Energy in one domain is the same as energy in the other domain.</i></div>

<div class="example">
<h4> Example </h4>
<hr>
In this example the goal is to calculate the energy of a time domain sinc function as depicted on the left side of the figure below.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/continuous/transforms/FTC/IFTCBlock.svg"
      alt="IFTC of block."
    />
  </figure>
</div>
<br>
<button class="collapsible">Show example</button>
<div class="content">
When using the definition of a sinc function we can calculate the energy as follows:
\begin{eqnarray}
E &=& \int_{t=-\infty}^{\infty} |{\color{red}x(t)}|^2 \text{d} t
=\int_{t=-\infty}^{\infty} |2 F_c \text{sinc}(2 \pi F_c t)|^2 \text{d} t \\
&=&  \int_{t=-\infty}^{\infty} |2 F_c \frac{\sin(2 \pi F_c t)}{2 \pi F_c t}|^2 \text{d} t
\end{eqnarray}
The evaluation of this integral is not trivial. However, when using the theorem of Parseval we can find the same result by evaluating the energy in frequency domain. As shown before the FTC of a time domain sinc function is a block function in  frequency domain, as depicted on the right side of the figure above and the result is as follows:
\begin{eqnarray}
E &=& \int_{t=-\infty}^{\infty} |{\color{red}x(t)}|^2 \text{d} t \\
&\overset{\text{Parseval}}{=} & \int_{f=-\infty}^{\infty} |{\color{blue}X(f)}|^2 \text{d} f = \int_{f=-F_c}^{F_c} |1|^2 \text{d} f  = 2 F_c
\end{eqnarray}
</div>
</div>
