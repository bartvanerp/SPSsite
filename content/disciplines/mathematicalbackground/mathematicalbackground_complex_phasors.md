+++
title = "Phasors"

# date = {{ .Date }}
lastmod = 2019-06-04

draft = false       # Is this a draft? true/false
toc = true          # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Phasors"
  parent = "Complex numbers and phasors"
  weight = 14

+++
## ⯈ Screencast video
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/IS3LOzP5cqk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br></br>

## Introduction to phasors
Many real world signals can be described by a time depending sinusoidal signals such as:
$$ x(t) = A \cos (\omega_o t +\phi) $$
In this equation is $A$ represents the amplitude, from which the dimension is equal to the dimension of the signal $x(t)$, $\omega_0$ [rad/sec] the radian (or angular) frequency and $\phi$ [rad] the phase.

<div style="max-width: 400px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/phasor.svg"
      alt="Visualisation of a phasor."
    />
    <figcaption class="numbered">
      Visualisation of a phasor.
    </figcaption>
  </figure>
</div>

By using the  <a href="../mathematicalbackground_complex_euler">Euler equations</a> and replacing $\theta$ by $\omega_o t +\phi$ we obtain the following **time depending** complex exponential function $z(t)$:
$$ z(t) = A e^{j(\omega_o t +\phi)} = A \cos (\omega_o t +\phi) + j A \sin (\omega_o t +\phi) $$

Such time depending complex exponential, which is depicted as a time depending complex vector in Fig. 1, is called a **phasor**.
The projection of the phasor on the real axis behaves like a cosine signal, while the projection on the imaginary axis behaves like a sine function.
In other words we can generalize a time depending sinusoidal signal by a phasor, since it describes both a sine and cosine function at the same time.
Alternatively we write the cosine and sine function in phasor notation as follows using the <a href="../mathematicalbackground_complex_euler">Euler equations</a>:
$$ \begin{eqnarray*}
&& A \cos (\omega_o t +\phi) = \Re e \\{ A  e^{j(\omega_o t +\phi)} \\} = \frac{A e^{j(\omega_o t +\phi)} + A e^{-j(\omega_o t +\phi)}}{2}  \newline
&& A \sin (\omega_o t +\phi) = \Im m \\{ A e^{j(\omega_o t +\phi)} \\} = \frac{A e^{j(\omega_o t +\phi)} - A e^{-j(\omega_o t +\phi)}}{2 j}
\end{eqnarray*} $$

<br></br>

## Phasor addition rule
We can write a phasor as the following product:
$$ A e^{j(\omega_o t +\phi)} = A e^{j\phi} \cdot e^{j\omega_0 t} $$

The second part $e^{j\omega_0 t}$ is the phasor component, containing the radian frequency $\omega_0$. The first part $A e^{j\phi}$ is a complex number, in which $A$ represents the amplitude and $\phi$ the phase of the phasor.
By using this fact it becomes obvious that the addition of two phasors,
$A_1 e^{j(\omega_0 t + \phi_1)}$ and $A_2 e^{j(\omega_0 t + \phi_2)}$,
with the same radial frequency $\omega_0$ result in one new phasor
$A e^{j(\omega_0 t + \phi)}$ having the same frequency $\omega_0$.
This can be shown as follows:
$$ A_1 e^{j(\omega_0 t + \phi_1)} + A_2 e^{j(\omega_0 t + \phi_2)} =
A_1 e^{j\phi_1} \cdot e^{j\omega_0} + A_2 e^{j\phi_2} \cdot e^{j\omega_0}
= \left ( A_1 e^{j\phi_1} + A_2 e^{j\phi_2} \right ) \cdot e^{j\omega_0}$$

The amplitude $A$ and phase $\phi$ of the resulting phasor $A e^{j(\omega_0 t + \phi)}$ can be calculated by using the complex addition rule for the complex numbers $A_1 e^{j\phi_1}$ and $A_2 e^{j\phi_2}$ of the individual phasors as follows:
$$ A e^{j\phi} = A_1 e^{j\phi_1} + A_2 e^{j\phi_2}$$

This phasor addition example is depicted in Fig. 2.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/phasor_addition.svg"
      alt="The addition of phasors."
    />
    <figcaption class="numbered">
      Visualisation of the addition operation on phasors with equal frequencies.
    </figcaption>
  </figure>
</div>

We can use this property when a signal $x(t)$ consists of the sum of two sinusoidal signals, both with the same frequency $\omega_0$, which goes as follows:

$$ \begin{eqnarray*}
x(t) &=& A_1 \cos (\omega_0 t + \phi_1) + A_2 \cos (\omega_0 t + \phi_2) \newline
&=& \left ( \frac{A_1}{2} e^{j\phi_1} + \frac{A_2}{2} e^{j\phi_2} \right ) \cdot e^{j\omega_0 t} + \left( \frac{A_1}{2} e^{-j\phi_1} + \frac{A_2}{2} e^{-j\phi_2} \right ) \cdot e^{-j\omega_0 t}
\end{eqnarray*}$$

By defining
$$ A e^{j\phi} = A_1 e^{j\phi_1} + A_2 e^{j\phi_2} $$
we obtain:
$$\begin{eqnarray*}
x(t) &=& \left ( \frac{A}{2} e^{j\phi} \right )  \cdot e^{j\omega_0 t} +
\left ( \frac{A}{2} e^{-j\phi} \right )  \cdot e^{-j\omega_0 t} = A \cos (\omega_0 t + \phi)
\end{eqnarray*}$$

Thus the amplitude $A$ and phase $\phi$ of the resulting sinusoidal signal $x(t)$ are found by complex addition of the amplitude and phase of the individual sinusoidal components.
\\
This example can be extended to the addition of $N$ sinusoidal signals, all with the same radian frequency $\omega_0$, resulting in one sinusoidal signal with the same radian frequency $\omega_0$ as follows:

$$ \bbox[5px,border:1px solid black]{x(t) = \sum_{k=1}^{N} A_k \cos (\omega_0 t + \phi_k)= A \cos (\omega_0 t + \phi)} $$

in which the amplitude $A$ and phase $\phi$ can be calculated by using complex addition rules as follows:
$$ \bbox[5px,border:1px solid black]{A e^{j\phi} = \sum_{k=1}^N A_k e^{j\phi_k}} $$

In words this results in the so called phasor addition rule:

***The sum of original sinusoidal signals, all with the same radian frequency $\omega_0$, results in one sinusoidal signal with the same radian frequency $\omega_0$. Amplitude and phase of this resulting signal can be found by adding the complex representation of amplitude and phase of the individual original sinusoidal signals.***

<div class="example">
<h4> Example </h4>
<hr>
The function $x(t)$ consists of the sum of the following 3 sinusoidal signals:
$$
x(t) = 5 \cos\left(\omega_0 t + \frac{3}{2}\pi\right) + 4 \cos\left(\omega_0 t + \frac{2}{3}\pi\right) + 4 \cos\left(\omega_0 t + \frac{1}{3}\pi\right)
$$
Express $x(t)$ in the form $x(t) = A\cos(\omega_0 t + \phi)$ by finding the numerical values of $A$ and $\phi$.
<button class="collapsible">Show solution</button>
<div class="content">
The different cosine functions can be written as the real part of phasors.
$$ x(t) = \Re e \{5 e^{j(\omega_0 t + \frac{3}{2}\pi)} \}+\Re e \{4 e^{j(\omega_0 t + \frac{2}{3}\pi)} \} + 4\Re e \{ e^{j(\omega_0 t + \frac{1}{3}\pi)} \} $$
The phasor component ($e^{j\omega_0 t}$) can be separated:
$$ x(t) = \Re e \{ e^{j\omega_0 t} \cdot \left ( 5e^{j\frac{3\pi}{2}}+4e^{j\frac{2\pi}		{3}}+4e^{j\frac{\pi}{3}} \right ) \}$$
The complex numbers, containing the amplitude and phase of the 3 individual sinusoidal signals, can be added together by using complex addition rules. Since we have to add complex numbers it is easiest to rewrite these complex numbers in Cartesian notation:
$$\begin{eqnarray*}
x(t)&=& \Re e \{ e^{j\omega_0 t} \cdot \left(- j 5 + 4 (- \frac{1}{2} + j \frac{1}{2} \sqrt{3}) + 4 (\frac{1}{2} + j \frac{1}{2} \sqrt{3}) \right) \newline
&=& \Re e \{ e^{j\omega_0 t} \cdot \left ( (4 \sqrt{3} -5) j \right ) \} =  \Re e \{ e^{j\omega_0 t} \cdot \left ( (4 \sqrt{3} -5) e^{j\frac{\pi}{2}} \right ) \} \newline
&=& \Re e \{ (4 \sqrt{3} -5) e^{j\omega_0 t + \frac{\pi}{2}} \}
\end{eqnarray*}$$
Now this answer can be written as the final answer:
$$ x(t) = (4\sqrt{3}-5)\cos\left(\omega_0 t +\frac{\pi}{2}\right)$$
</div>
</div>
