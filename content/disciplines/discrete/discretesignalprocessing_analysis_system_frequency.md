+++
title = "Frequency response from system function"

# date = {{ .Date }}
lastmod = 2020-05-09

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Frequency response from system function"
  weight = 4
  parent = "Analysis III: System function"
+++


In this section we will discuss how the frequency response can be derived in a geometrical way from the pole-zero plot of the system function.
As a first step we rewrite the factored form of the system function $H(z)$  by dividing both numerator and denominator by the terms $z^{-1}$.  
\begin{eqnarray}
H(z) &=& b_0 \cdot
\frac{\prod_{k=1}^{M} (1 - \color{blue}{\beta_k} z^{-1})}{\prod_{k=1}^{N} (1 - \color{magenta}{\alpha_k} z^{-1})}
= z^{N-M}\frac{\prod_{k=1}^{M} (z - \color{blue}{\beta_k})}{\prod_{k=1}^{N} (z - \color{magenta}{\alpha_k})} \label{Eq:ProdHz}
\end{eqnarray}
As mentioned before, the frequency response $H(e^{j\theta})$ may be found from the system function by evaluating $H(z)$ on the unit circle.
\begin{eqnarray*}
H(z)|\_{|z|=1}=H(e^{j\theta})= |H(e^{j\theta})| \cdot e^{j\varphi(e^{j\theta})}
\end{eqnarray*}
The procedure to calculate the frequency response at frequency $\theta_0$ in a geometrical way from the pole-zero of the system function $H(z)$ can be explained based on
Fig. 1. This figure represents one zero at $z=\beta_k$ and one pole at $z=\alpha_k$ of such a system and the location $z=e^{j\theta_0}$ on the unit circle.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/PZplot.svg"
      alt="Evaluation of frequency response $H(e^{j\theta})$
      at frequency $\theta_0$, based on the pole $\alpha_k$ and zero $\beta_k$.."
    />
  </figure>
  <figcaption class="numbered">
  Evaluation of frequency response $H(e^{j\theta})$
  at frequency $\theta_0$, based on the pole $\alpha_k$ and zero $\beta_k$.
  </figcaption>
</div>
From equation (\ref{Eq:ProdHz}) ir follows that the magnitude of the frequency response can be written as the following product:
\begin{eqnarray*}
|H(e^{j\theta})| &=& |b_0| \times
\left ( \prod_{k=1}^{M} |e^{j\theta} - \color{blue}{\beta_k}| \right ) {\bf /} \left ( \prod_{k=1}^{N} |e^{j\theta} - \color{magenta}{\alpha_k} | \right )
\end{eqnarray*}
Each absolute values of a term $e^{j\theta} - \beta_k$ is the length of the vector from the zero at $z=\beta_k$ to the unit circle at $z=e^{j\theta_0}$,  labeled $v_1$ in the Fig. 1.
Similarly each absolute value of a term in the denominator $e^{j\theta} - \alpha_k$ is the length of the vector from the pole at $z=\alpha_k$ to the unit circle at $z=e^{j\theta}$,  labeled $v_2$ in Fig. 1, thus:
\begin{eqnarray*}
|H(e^{j\theta})| &=&|b_0| \times
\left ( \prod_{k=1}^{M} \mbox{length}(e^{j\theta} - \color{blue}{\beta_k}) \right ) {\bf /} \left ( \prod_{k=1}^{N} \mbox{length}(e^{j\theta} - \color{magenta}{\alpha_k} ) \right )
\end{eqnarray*}
Besides a constant factor $|b_0|$, this implies that  the contribution of the zero at $z=\beta_k$ and the pole at $z=\alpha_k$ to the value of the magnitude of the frequency response at frequency $\theta_0$ is equal to:
$$
|H(e^{j\theta_0})|=\color{blue}{v_1}/\color{magenta}{v_2}
$$
Thus, when a pole is close to the unit circle, the magnitude of the frequency response becomes large because the length of the vector ($v_2$) from the pole to the unit circle becomes small. Similarly, if there is a zero close to the unit circle  the magnitude of the frequency response becomes small because the length of the vector ($v_1$) from the zero to the unit circle becomes small.

The analysis of the phase is similar. Assuming that the constant $b_0$ is a positive real number, the phase corresponding to the frequency response as a function of $\theta$ is given by the following equation:
\begin{eqnarray*}
\varphi(e^{j\theta}) &=&(N-M) \cdot \theta + \sum_{k=1}^M \mbox{arg} (e^{j\theta} - \color{blue}{\beta_k}) -
\sum_{k=1}^N \mbox{arg} (e^{j\theta} - \color{magenta}{\alpha_k})
\end{eqnarray*}
Besides the factor $(N-M) \times \theta$ the phase is equal to the sum of the phases associated with the terms $e^{j\theta} - \beta_k$, minus the sum of the phases of the terms $e^{j\theta}- \alpha_k$.
With $\phi_1$ the angle of the vector $v_1$ and with $\phi_2$ the angle of the vector $v_2$ (see Fig. 1) this implies that the contribution of the zero at $z=\beta_k$ and the pole at $z=\alpha_k$ to the value of the phase of the frequency response at frequency $\theta_0$ is:
$$
\Phi(e^{j\theta_0})={\color{blue} \phi_1}-{\color{magenta}\phi_2}
$$
%When a pole (zero) is close to the unit circle, the phase decreases (increases) rapidly as we move past the pole (zero). Because the group delay is the negative of the derivative of the phase, this implies that the group delay is large and positive close to a pole and large and negative when close to a zero.

### Example magnitude- and phase response from PZ-plot
The pole-zero plot of a second order system $H(z)$
\begin{eqnarray*}
H(z)&=&  \frac{1}{(1 - \alpha z^{-1}) \cdot (1 - \alpha^* z^{-1})}
\end{eqnarray*}
with two complex conjugated poles at $z=\alpha$ and $z=\alpha^\ast$, with $\alpha=r e^{j\frac{\pi}{4}}$, and two zeros at $z=0$ is depicted in Fig. 2.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/system/PZexample21.svg"
      alt="Example of second order system with two complex conjugated poles at $z=\alpha$ and $z=\alpha^\ast$, with $\alpha=r e^{j\frac{\pi}{4}}$."
    />
  </figure>
  <figcaption class="numbered">
  Example of second order system with two complex conjugated poles at $z=\alpha$ and $z=\alpha^\ast$, with $\alpha=r e^{j\frac{\pi}{4}}$.
  </figcaption>
</div>
Complex conjugated poles imply that the coefficients of the frequency response $H(e^{j\theta})$ are real, a indicated in the following equation:
$$
\Rightarrow \hspace{2mm} H(e^{j\theta}) = \frac{1}{1 -a_1 e^{-j\theta} - a_2 e^{-j2 \theta}}
\mbox{ with } a_1 = 2 \mbox{Re} \{ \alpha \} \mbox{ and } a_2 = - | \alpha|^2
$$
In this example will vary $r=|\alpha|$, which is an indication of the distance of the poles to the unit circle as indicated in the following table:

<table style="width:100%">
  <tr>
    <th></th>
    <th>$a_1$</th>
    <th>$a_2$</th>
    <th>$r=|\alpha|$</th>
  </tr>
  <tr>
    <td>$\color{black}{- -}$</td>
    <td>1.0</td>
    <td>-0.50</td>
    <td>0.7071</td>
  </tr>
  <tr>
    <td>$\color{red}{- -}$</td>
    <td>1.2</td>
    <td>-0.72</td>
    <td>0.8485</td>
  </tr>
  <tr>
    <td>$\color{blue}{- -}$</td>
    <td>1.4</td>
    <td>-0.98</td>
    <td>0.9899</td>
  </tr>
</table>

The magnitude and phase response plots are shown in Fig.
3.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/analysis/system/Amplexample2.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/analysis/system/Phaseexample2.svg"
    style="width:100%">
  </div>
  <figcaption class="numbered">
  Magnitude and phase response of second order system for different distances from poles to unit circle.
  </figcaption>
</div>
</figure>
From this it follows that when increasing $r=|\alpha|$, that is decreasing the distance of the poles to the unit circle, the peaks in the magnitude response plot at the frequencies $\pm \pi/4$ becomes higher and sharper and the phase change at these frequencies increases.
