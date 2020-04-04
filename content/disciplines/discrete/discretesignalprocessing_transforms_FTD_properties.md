+++
title = "FTD properties"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "FTD properties"
  weight = 3
  parent = "Transforms I: Fourier transform for discrete-time signals"

+++

## Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/2kIrvAyID-o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

As shown before the frequency representation $X(e^{j\theta})$ is periodic, which is denoted by representing the frequency variable $\theta$ in the exponent.
Furthermore because of the fact that integral in the FTD is a linear operator, it is straightforward to show that the FTD is also linear.
In this section we will show how conjugation and time reversal influence the frequency representation.  Furthermore we will prove that a shift in time domain results in modulation in frequency domain  and vice versa. Such duality also holds for convolution and multiplication: Convolution in time domain results in multiplication in frequency domain  and vice versa.  Finally we will show that the FTD preserves energy, which was shown by Parceval.

<br></br>
## Conjugation
In this subsection we will show the following conjugation property:
$$
\boxed{
x^\ast[n] \qquad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \qquad X^\ast(e^{-j\theta}) }
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A complex conjugation operation in time domain results in complex conjugation of the mirrored frequency representation.</i></div>

The proof of the conjugation property is straightforward. The first step is to use the conjugated version of $x[n]$ in the FTD definition and then taking out the conjugation operator of the resulting expression as follows:
$$
y[n]=x^\ast [n] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} Y(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x^\ast [n] e^{-jn \theta} = \left( \sum\_{n=-\infty}^{\infty} x[n] e^{jn \theta} \right)^\ast
$$
The equation between brackets is equal to the FTD  $X(e^{-j\theta})$ in which $\theta$ is replaced by $- \theta$:
$$
\Rightarrow \hspace{3mm} Y(e^{j\theta}) = \left( X(e^{-j\theta}) \right)^* = X^\ast (e^{-j\theta})
$$
which finalizes the proof.

From this result it follows that for real signals the frequency representation has the following special symmetry properties:
$$
x[n] \text{ real } \Rightarrow \text{ } x[n]=x^\ast[n] \text{ } \Rightarrow \text{ }
X(e^{j\theta}) = X^\ast(e^{-j\theta})
$$

which results into a symmetric magnitude and an anti-symmetric phase response:
$$
\begin{eqnarray*}
|X(e^{j\theta})|= |X(e^{-j\theta})| & \quad : \quad & \textbf{Magnitude response symmetric} \newline
\angle \{ X(e^{j\theta})\}=- \angle \{ X(e^{-j\theta})\}  & \quad : \quad & \textbf{Phase response anti-symmetric}
\end{eqnarray*}
$$
This special property can be shown by the following simple example in which we calculate the FTD of a delta pulse which is shifted over two samples:
$$
\begin{eqnarray*}
x[n] = \delta[n-2] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} \delta[n-2] e^{-jn \theta} = e^{-j2 \theta}
\end{eqnarray*}
$$
Thus the FTD of a delta pulse at time index $n=2$ results in a complex exponential function $e^{-j2 \theta}$.  In other words the magnitude response is flat (a straight line), while the phase response has a negative angle $-2 \theta$. The symmetry and anti-symmetry properties are clearly shown as depicted at the right hand side of Fig. 1.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDshiftedDelta.svg"
      alt="Symmetry properties of the magnitude and phase FTD of a real signal."
    />
    <figcaption class="numbered">
      Symmetry properties of the magnitude and phase FTD of a real signal.
    </figcaption>
  </figure>
</div>

## Time reversal
In this subsection we will show the following time reversal property:
$$
\boxed{
\begin{eqnarray*}
x[-n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{-j\theta})
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Reversing in time domain implies mirroring in the frequency domain.</i></div>


For the proof we first substitute the negative index $-n$  by a new index $p$ and reverse the summation which leads to the final result:
\begin{eqnarray*}
y[n]=x[-n]  &\hspace{-2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \hspace{-2mm} Y(e^{j\theta}) = \sum\_{n=-\infty}^{\infty} x[-n] e^{-jn\theta}
\overset{{\color{red}p=-n}}{=} \sum\_{p=-\infty}^{\infty} x[p] e^{jp \theta} = X(e^{-j\theta})
\end{eqnarray*}
As an example we reverse the signal $x[n]=\delta[n-2]$ as discussed in the previous subsection. The resulting reversed signal $y[n]$ is a delta pulse at time index $n=-2$.
By applying the time reversal property it follows that the frequency representation is equal the complex exponential function $e^{j2 \theta}$.  The plots of the magnitude and phase response, as depicted at the right hand side of Fig. 2, show the effect of the time reversal in frequency domain.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDshiftednegDelta.svg"
      alt="Time reversal property FTD with $y[n]=\delta[n+2]$."
    />
    <figcaption class="numbered">
      Time reversal property FTD with $y[n]=\delta[n+2]$.
    </figcaption>
  </figure>
</div>


<br></br>
## Shifting
In this subsection we will show the following shift property:
$$
\boxed{
\begin{eqnarray*}
x[n-n_0] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & e^{-jn_0 \theta} \cdot X(e^{j\theta})
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A shift in time domain results in a multiplication with a complex exponential function in frequency domain.</i></div>


In the first step  of the proof we make both indices of the signal and the exponent the same, namely $n-n_0$, which is achieved by a multiplication with $e^{jn_0 \theta}$.
$$
y[n]=x[n-n_0] \hspace{2mm} \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \hspace{2mm} Y(e^{j\theta})=\sum\_{n=-\infty}^{\infty} x[n-n_0] e^{-jn \theta}
=\sum\_{n=-\infty}^{\infty} x[n-n_0] e^{-j(n-{\color{red}n_0}) \theta} \cdot e^{j{\color{red}n_0} \theta}
$$
By substitution the index $n-n_0$ with a new index $p$ we obtain the final result:
$$
Y(e^{j\theta}) \overset{{\color{blue}p}=n-n_0}{=} \left( \sum\_{{\color{blue}p}=-\infty}^{\infty} x[{\color{blue}p}] e^{-j{\color{blue}p} \theta} \right) \cdot e^{jn_0 \theta}
= X(e^{j\theta}) \cdot e^{jn_0 \theta}
$$

## Modulation
In this subsection we will show the following modulation property:

$$
\boxed{
\begin{eqnarray*}
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j(\theta - \theta_0)})
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication with a complex exponential function in time domain results in a shift in frequency domain.</i></div>

The proof is as follows:
$$
\begin{eqnarray*}
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
\sum\_{n=-\infty}^{\infty} \left( e^{jn \theta_0} \cdot x[n] \right) e^{-jn \theta} \newline
&& = \sum\_{n=-\infty}^{\infty} x[n] e^{-jn (\theta- \theta_0)} = X(e^{j(\theta - \theta_0)})
\end{eqnarray*}
$$
When combining this property for a positive and negative exponent  it follows that the modulation of signal $x[n]$ with a sinusoidal frequency $\theta_0$ results in a frequency representation which consists of two shifted versions of the original frequency representation $X(e^{j\theta})$. This property can be shown as follows:
$$
\begin{eqnarray*}
e^{jn \theta_0} \cdot x[n] + e^{-jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
X(e^{j(\theta - \theta_0)}) + X(e^{j(\theta + \theta_0)}) \nonumber \newline
\Rightarrow \text{ } \cos (n \theta_0) \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & \frac{1}{2} X(e^{j(\theta + \theta_0)}) + \frac{1}{2} X(e^{j(\theta - \theta_0)})
\end{eqnarray*}
$$
In one of the following subsections we will give an example of this modulation property.


<br></br>
## Convolution
In this subsection we will show the following convolution property:

$$
\boxed{
\begin{eqnarray*}
x[n] \ast y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \cdot Y(e^{j\theta})
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Convolution in time domain can be performed as a multiplication in frequency domain.</i></div>

The first step of the proof is to use the expression for the convolution sum between $x[n]$ and $y[n]$:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\} = \sum\_{n=-\infty}^{\infty} \left( \sum\_{p=-\infty}^{\infty} x[p] y[n-p] \right) e^{-jn \theta}
$$
Then we can interchange the two summations and multiply in the first summation the samples $x[p]$ with $e^{-jp \theta}$, which has to be compensated in the second summation by $e^{jp \theta}$:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\} =
\sum\_{p=-\infty}^{\infty} x[p] e^{-j{\color{red}p} \theta} \cdot \left( \sum\_{n=-\infty}^{\infty}y[n-p]  e^{-j(n{\color{red}-p}) \theta} \right)
$$
As a final step we substitute a new variable $m=n-p$ and since both variables $n$ and $p$ range from minus to plus infinity, this implies that the new variable also ranges from minus to plus infinity:
$$
\mathcal{F} \left\\{ x[n] \ast y[n] \right\\}
\overset{{\color{blue}m}= n-p}{=} \sum\_{p=-\infty}^{\infty} x[p] e^{-jp \theta} \cdot \left( \sum\_{{\color{blue}m}=-\infty}^{\infty}y[m]  e^{-j{\color{blue}m} \theta} \right)
= X(e^{j\theta}) \cdot Y(e^{j\theta})
$$
which finalizes the proof.


<br></br>
## Multiplication
In this subsection we will show the dual property of the previous subsection:

$$
\boxed{
\begin{eqnarray*}
x[n] \cdot y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \star Y(e^{j\theta}) =
\frac{1}{2 \pi} \int_{\psi = - \pi}^{\pi} X(e^{j\psi}) Y(e^{j(\theta - \psi)}) \text{d}\psi
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>Multiplication in time domain can be performed by a convolution in frequency domain.</i></div>

In the first step of the proof  we replace $x[n]$ as the inverse of its frequency representation, which results in an equation with a summation and an integral:
$$
\begin{eqnarray*}
\mathcal{F} \left\\{ x[n] \cdot y[n] \right\\} &=& \sum\_{n=-\infty}^{\infty}  x[n] \cdot y[n] e^{-jn \theta}
= \sum\_{n=-\infty}^{\infty} \left(
\mathcal{F}^{-1} \left\\{ X(e^{j\psi}) \right\\} \right) \cdot y[n] e^{-jn \theta} \newline
&=& \sum\_{n=-\infty}^{\infty}  \left( \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{j\psi}) e^{jn \psi} \text{d} \psi \right) \cdot y[n] e^{-jn \theta}
\end{eqnarray*}
$$

Since both summation and integral operations are linear, we may interchange the order:

$$
\mathcal{F} \left\\{ x[n] \cdot y[n] \right\\} = \frac{1}{2\pi} \int\_{-\pi}^{\pi} X(e^{j\psi}) \left( \sum\_{n=-\infty}^{\infty} y[n] e^{-jn (\theta - \psi)} \right) \mathrm{d} \psi
$$
The equation between brackets represents the FTD of signal $y[n]$ from which the frequency $\theta$ is interchanged by $\theta - \psi$:
$$
\mathcal{F} \{ x[n] \cdot y[n] \} =
\frac{1}{2 \pi} \int_{\psi = - \pi}^{\pi} X(e^{j\psi}) Y(e^{j(\theta - \psi)}) \text{d}\psi
= X(e^{j\theta}) \star Y(e^{j\theta})
$$
This last equation represents the convolution integral between the two continuous frequency representations $X(e^{j\theta})$ and $Y(e^{j\theta})$, which is symbolically denoted by a star.
In the following subsections we will discuss some examples of this multiplication property.




### Example multiplication property: Modulation
As a first example of the multiplication property we will show the previously discussed modulation property. In this example we choose for signal $x[n]$ a sinc function.
In the previous section we have shown that the FTD of a sinc function in time domain results in a block function in frequency domain. The top figure of Fig. 3 shows a sketch of this result.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/FTDModulateSinc.svg"
      alt="Example multiplication property: Modulation."
    />
    <figcaption class="numbered">
      Example multiplication property: Modulation.
    </figcaption>
  </figure>
</div>

Furthermore we have shown in the previous section that the FTD of a sinusoidal  function with frequency $\theta_0$ consists of two delta pulses at frequencies $\pm \theta_0$, which is shown in the middle figure of Fig. 3. The lower part of Fig. 3
shows at the left hand side the result of the multiplication of the sinc function with the sinusoidal function in time domain. Multiplication in time domain results in convolution in frequency domain. Thus the block function in frequency domain has to be convolved with the two delta pulses at $\pm \theta_0$. Convolving a function with a delta pulse results in a shift of the original function to the position of the delta pulse. In this case the resulting frequency representation consists of two original frequency representations which are shifted over $\pm \theta_0$, which is shown at the right hand side of the lower figure of Fig. 3. This is exactly the result of the modulation property.

<!-- TODO: ADD MATLAB ANIMATION. -->


### Example multiplication property: Finite length sinusoidal
In most cases we assume in theory that a signal is infinite long. In practice however this will never be true and we will work with a finite length signal. In this example we will show the implication of this effect in frequency domain for a sinusoidal signal.  The top figures of Fig. 4 shows at the left hand side an infinite long sinusoidal signal $s[n]$ of frequency $\theta_0$ and at the right hand side the FTD result $S(e^{j\theta})$, which consists of two delta functions at frequency $\pm \theta_0$.


<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/signal.svg"
    style="width:90%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDsignal.svg"
    style="width:90%">
  </div>
</div>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/window.svg"
    style="width:90%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDwindow.svg"
    style="width:90%">
  </div>
</div>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/wsignal.svg"
    style="width:90%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/transforms/FTD/FTDwsignal.svg"
    style="width:90%">
  </div>
</div>
<figcaption class="numbered">
  FTD of an infinite and a finite length (windowed) sinusoidal signal.
</figcaption>
</figure>


A finite length sinusoidal $s_w[n]$ can be obtained by multiplication this infinite length sinusoidal $s[n]$ with a finite length window or block function $w[n]$.
The left hand side of the middle figure of Fig. 4 shows a rectangular block function $w[n]$ of length $N=32$ samples. The FTD $W(e^{j\theta})$ of this block function is depicted at the right hand side of the middle figure.
In the previous section we have shown that this is a Dirichlet function. The width of the main lobe of this Dirichlet function $W(e^{j\theta})$ equals $2 \times \frac{2\pi}{N}$, which follows from the first two zero crossings around this main lobe. This implies that the main lobe is inversely proportional with the length of the block function in time domain. In other words, a very long block function $w[n]$ will result in a very small main lobe $W(e^{j\theta})$ and the other way around.

Finally the figure at the left hand side of the lower figure in Fig. 4 shows the finite length sinusoidal signal $s_w[n]$, which is the result of the multiplication of
$s[n]$ with $w[n]$. The figure at the right hand side shows the FTD $S_w(e^{j\theta})$ of this finite length signal $s_w[n]$. The FTD $S_w(e^{j\theta})$ can be constructed by using the property: _"multiplication in time domain is equivalent to a convolution in frequency domain"_.
So in practice the two original, infinite small, delta pulses at frequencies $\pm \theta_0$ of the infinite long sinusoidal function are smeared out depending on the with of the main lobe of the Dirichlet function: The more samples $N$ we take, the smaller the two peaks will be and the result looks closely to the infinite length (theoretical) result. While on the other hand when using only a small number of samples $N$ of the sinusoidal functions will results into two peaks that are smeared out in frequency domain.


<br></br>
## Parceval: Preservation of energy
Parceval has shown following FTD property:

$$
\boxed{
\begin{eqnarray*}
\sum\_{n=-\infty}^{\infty} |x[n]|^2 &=& \frac{1}{2 \pi} \int_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \text{d} \theta
\end{eqnarray*}}
$$

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>The FTD preserves energy.</i></div>

The first step of the proof is to replace the complex conjugated version of $x[n]$ by the IFTD of the FTD of $x^\ast[n]$.
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 = \sum\_{n=-\infty}^{\infty} x[n] x^\ast[n]
=\sum\_{n=-\infty}^{\infty} x[n] \mathcal{F}^{-1} \left\\{ \mathcal{F} \left\\{ x^\ast[n] \right\\} \right\\}
$$
Then we apply the conjugation property and  write out the IFTD:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\sum\_{n=-\infty}^{\infty} x[n] \mathcal{F}^{-1} \left\\{ X^\ast(e^{-j\theta}) \right\\}
= \sum\_{n=-\infty}^{\infty} x[n] \left(
\frac{1}{2\pi} \int\_{-\pi}^{\pi}
X^\ast(\text{e}^{-j \theta}) \text{e}^{+ j n \theta}
\mathrm{d} \theta \right)
$$
Now we can replace $\theta$ by $-\theta$
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\sum\_{n=-\infty}^{\infty} x[n] \left(
\frac{1}{2\pi} \int\_{-\pi}^{\pi}
X^\ast(\text{e}^{{\color{red}+} j \theta}) \text{e}^{{\color{red}-} j n \theta}
\mathrm{d} \theta \right)
$$
and interchange the order of the summation and integral operations:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\frac{1}{2\pi} \int\_{-\pi}^{\pi} X^\ast(e^{j\theta}) \left(
\sum\_{n=-\infty}^{\infty} x[n] e^{-jn \theta} \right) \mathrm{d} \theta
$$
The term between brackets is the FTD definition of $x[n]$, which leads to the final result:
$$
\sum\_{n=-\infty}^{\infty} |x[n]|^2 =
\frac{1}{2 \pi} \int\_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \text{d} \theta
$$

### Example Parceval
In this example we will use Parceval to calculate the energy of the sinc function:
$$
x[n]= \frac{1}{2} \frac{\sin(\frac{\pi}{2} n)}{\frac{\pi}{2}}
$$
which is depicted at the left hand side of Fig. 5. For this we have to calculate the summation of the squared absolute values of the samples which may be a tough exercise.
On the other hand we have shown before that the frequency representation of the given sinc function is a block function with a cut off frequency $\theta_c=\frac{\pi}{2}$, as depicted at the right hand side of Fig. 5.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/transforms/FTD/IFTDBlock.svg"
      alt="IFTD of a block function with cutoff frequency $\theta_c=\frac{\pi}{2}$."
    />
    <figcaption class="numbered">
      IFTD of a block function with cutoff frequency $\theta_c=\frac{\pi}{2}$.
    </figcaption>
  </figure>
</div>

So by using the Parceval property it is easier to calculate the energy in frequency domain  which goes as follows:
$$
\begin{eqnarray*}
E &=& \sum\_{n=-\infty}^{\infty} | x[n]|^2
= \sum\_{n=-\infty}^{\infty} \left | \frac{1}{2} \frac{\sin(\frac{\pi}{2} n)}{\frac{\pi}{2}}\right |^2 \nonumber \newline
&\overset{\text{Parceval}}{=}&
\frac{1}{2 \pi} \int\_{-\pi}^{\pi} \left |X(e^{j\theta}) \right |^2 \mathrm{d} \theta
= \frac{1}{2 \pi} \int\_{-\pi/2}^{\pi/2} \left | 1 \right |^2 \mathrm{d} \theta
= \frac{1}{2}
\end{eqnarray*}
$$
