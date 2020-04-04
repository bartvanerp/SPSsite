+++
title = "Fourier transform for continuous-time signals"

# date = {{ .Date }}
lastmod = 2019-11-28

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.continuous]
  name = "Transforms III: Fourier transform for continuous-time signals"
  weight = 42

+++


## Introduction
The <a href="../continuoussignalprocessing_transforms_fourier_main">Fourier Series (FS)</a> representation is an extremely useful signal representation. Unfortunately, this signal representation can only be used for periodic signals.
That's why we will introduce a tool for representing non-periodic signals, known as the <b>F</b>ourier <b>T</b>ransform for <b>C</b>ontinuous time signals, abbreviated as FTC. One might wonder if we can somehow use the Fourier Series to develop a representation for non-periodic signals. As it turns out, this is possible. By viewing a non-periodic as a periodic signal with an infinitely large period, we can use the Fourier Series to develop a more general signal representation that can be used in the non-periodic case. By doing so we should realise that the development of the FTC is not completely rigorous. Instead it is plausible which suggests the correct form of the FTC equations and it provides a useful interpretation.

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/r1_Dotj41L4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>

## Module overview
This module covers the following topics:

1. <a href="../continuoussignalprocessing_transforms_ftc_limit">FTC as limit of the FS</a> - We will show that the FTC is obtained as an extension of the Fourier series when the period goes to infinity.
2. <a href="../continuoussignalprocessing_transforms_ftc_examples">FTC examples</a> - Several examples are covered to get the reader acquainted with the FTC. The examples discussed are elementary signals and can therefore be used in combination with the properties of the FTC for more complex signals.
3. <a href="../continuoussignalprocessing_transforms_ftc_properties">FTC properties</a> - The definition of the FTC inherently leads to many different properties which can be used to simplify notations.

<br></br>

## Summary

<b><u>Definition FTC and IFTC</u></b>

$$
\boxed{
\begin{eqnarray*}
X(f)=\int\_{-\infty}^{\infty} x(t) e^{-j2 \pi f t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \int\_{-\infty}^{\infty} X(f) e^{j2 \pi f t} \text{d} f
\end{eqnarray*}}
$$

$$
\boxed{
\begin{eqnarray*}
X(\omega) = \int\_{-\infty}^{\infty} x(t) e^{-j\omega t}  \text{d} t
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &
x(t) = \frac{1}{2\pi} \int\_{-\infty}^{\infty} X(\omega) e^{j\omega t} \text{d} \omega
\end{eqnarray*}}
$$
<br>
<b><u>Existence and convergence FTC</u></b>
\begin{eqnarray*}
\left | X(f) \right | < \infty & \leftrightarrow &
\int_{-\infty}^{\infty} \left | x(t) \right | \text{d} t < \infty
\end{eqnarray*}

<br>
<b><u>General Phasor Integral property (GPI)</u></b>
\begin{eqnarray*}
\int_{-\infty}^{\infty}  e^{-j2 \pi (f \pm f_0) t} \text{d} t
&\overset{\text{GPI}}{=}& \delta(f \pm f_0)
\end{eqnarray*}

<br>
<b><u>Basic Fourier transform pairs</u></b>
\begin{eqnarray*}
x(t)= \delta(t) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=1 \hspace{2mm} \forall f \newline
x(t)=1 \hspace{2mm} \forall t &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\delta(f) \newline
x(t) = \begin{cases}
1 & \text{for } |t| \leq T_0/2 \newline
0 & \text{elsewhere}
\end{cases}
&\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)= T_0 \frac{\sin(\pi f T_0)}{\pi f T_0} \newline
2 F_c \frac{\sin(2\pi F_c t)}{2\pi F_c t} &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ&
X(f) = \begin{cases}
1 & \text{for } |f| \leq F_c \newline
0 & \text{elsewhere}
\end{cases}\newline
x(t) = \cos (2 \pi F_0 t) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\frac{1}{2} \delta(f-F_0) + \frac{1}{2} \delta(f+F_0) \newline
x(t)=\sum_{n=-\infty}^{\infty} \delta(t - n \cdot T) &\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ& X(f)=\frac{1}{T} \sum_{n=-\infty}^{\infty} \delta (f - \frac{n}{T} )
\end{eqnarray*}

<br>
<b><u> Main properties </u></b>
<ul>
<li> Linearity: $a \cdot x(t) + b \cdot y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } a \cdot X(f) + b \cdot Y(f)$</li>
<li> Conjugation: $x^\ast(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ }  X^\ast(-f)$ </li>
<li> Scaling: $x(k \cdot t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } \frac{1}{|k|} X(f/k) \hspace{3mm}$ with $k \neq 0$ </li>
<li> Time domain shift: $x(t-t_0) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } e^{-j2 \pi f t_0} X(f)$ </li>
<li> Frequency domain shift: $e^{j2 \pi f_0 t} x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ
\text{ } X(f-f_0)$ </li>
<li> Modulation: $2 \cos(2 \pi f_0 t) \cdot x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f-f_0) + X(f+f_0)$ </li>
<li> Time domain convolution: $x(t) \star y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f) \cdot Y(f)$ </li>
<li> Frequency domain convolution: $x(t) \cdot y(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } X(f) \star Y(f)$ </li>
<li> Time domain differentiation: $\frac{\text{d} }{\text{d} t} x(t) \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } j \omega X(f)$ </li>
<li> Frequency domain differentiation: $t x(t)  \text{ } \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \text{ } \frac{j}{2 \pi} \frac{\text{d}}{\text{d} f} X(f)$ </li>
<li> Theorem of Parseval: $\int_{-\infty}^{\infty} |x(t)|^2 \text{d} t = \int_{-\infty}^{\infty} |X(f)|^2 \text{d}f$ </li>
</ul>

<br>
<b><u>Main "rules of thumb" </u></b>
\begin{eqnarray*}
\text{Shrinking} &\leftrightarrow& \text{Stretching} \newline
\text{Multiplication} &\leftrightarrow& \text{Convolution}\newline
\text{Modulation} &\leftrightarrow& \text{Shifting}\newline
\text{Energy} &\leftrightarrow& \text{Energy}
\end{eqnarray*}
