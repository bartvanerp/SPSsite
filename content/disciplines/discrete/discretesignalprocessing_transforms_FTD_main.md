+++
title = "Transforms I: Fourier transform for discrete-time signals"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Transforms I: Fourier transform for discrete-time signals"
  weight = 51


+++

## Summary

$$
\boxed{
\begin{eqnarray}
X(e^{j\theta})
\overset{\mathcal{F}\left\\{x[n]\right\\}}{=\\! =}
\sum\_{n=- \infty}^{\infty} x[n] e^{-jn\theta}
&\\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ &  
x[n]
\overset{\mathcal{F}^{-1}\\{X(e^{j\theta})\\}}{=\\! =\\! =\\! =\\! =\\!}
\frac{1}{2 \pi} \int\_{-\pi}^{\pi} X(e^{j\theta}) e^{jn\theta} \mathrm{d} \theta
\end{eqnarray}}
$$

<b><u> Main differences with continuous-time Fourier transforms: </u></b>
<ul>
<li>  The signal samples $x[n]$ are discrete in time and not periodic, </li>
<li>  The normalized frequency $\theta = \omega \cdot T_s$, </li>
<li>  The Fundamental Interval is usually chosen as: $-\pi \leq \theta < \pi$, </li>
<li>  The frequency representation $X(e^{j\theta})$ is a continuous function and periodic, </li>
<li>  The FTD is evaluated over an infinite summation of samples $x[n]$, </li>
<li>  The IFTD is evaluated by an integral over one period of the frequency representation $X(e^{j\theta})$. </li>
</ul>


<b><u> Discrete phasor property: </u></b>
$$
\textbf{DPP:} \qquad \sum\_{p=-\infty}^{\infty} e^{-jp \theta} = \sum\_{k=-\infty}^{\infty} 2 \pi \delta(\theta + k \cdot 2 \pi)
$$

<b><u> Most important FTD pairs: </u></b>
<table style="width:100%">
  <tr>
    <th style="text-align:center"> $x[n]$  </th>
    <th style="text-align:center"> $X(e^{j\theta})$ </th>
  </tr>
  <tr>
    <td align=center> $\delta[n]$  </td>
    <td align=center> $1$ </td>
  </tr>
  <tr>
    <td align=center> $1$  </td>
    <td align=center> $2\pi\delta(\theta)$ </td>
  </tr>
  <tr>
    <td align=center> $\cos(n\theta_0)$  </td>
    <td align=center> $\pi\delta(\theta+\theta_0) + \pi\delta(\theta-\theta_0)$ </td>
  </tr>
  <tr>
    <td align=center> $a^nu[n], \ |a|<1$  </td>
    <td align=center> $\frac{1}{1-ae^{-j\theta}}$ </td>
  </tr>
  <tr>
    <td align=center> Sinc: $\frac{\theta_c}{\pi}\cdot \frac{\sin(\theta_c n)}{\theta_c n}$  </td>
    <td align=center> Block: $\begin{cases} 1 & |\theta|<\theta_c \newline 0 & \text{otherwise}\end{cases}$ </td>
  </tr>
  <tr>
    <td align=center> Block: $u[n]-u[n-N]$  </td>
    <td align=center> Dirichlet: $e^{-j\frac{N-1}{2}\theta}\frac{\sin(N\frac{\theta}{2})}{\sin(\frac{\theta}{2})}$ </td>
  </tr>
</table>



<b><u> Most important FTD properties:</u></b>
$$
\begin{eqnarray}
x^\ast[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X^\ast(e^{-j\theta}) \newline
x[-n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{-j\theta})\newline
x[n-n_0] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & e^{-jn_0 \theta} \cdot X(e^{j\theta})\newline
e^{jn \theta_0} \cdot x[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j(\theta - \theta_0)})\newline
x[n] \star y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \cdot Y(e^{j\theta})\newline
x[n] \cdot y[n] & \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & X(e^{j\theta}) \star Y(e^{j\theta}) \newline
\sum\_{n=-\infty}^{\infty} |x[n]|^2 &=& \frac{1}{2 \pi} \int\_{\theta = - \pi}^{\pi} |X(e^{j\theta}) |^2 \mathrm{d} \theta
\end{eqnarray}
$$