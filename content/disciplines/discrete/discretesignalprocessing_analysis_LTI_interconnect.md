+++
title = "Interconnecting systems"

# date = {{ .Date }}
lastmod = 2020-05-18

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Interconnecting systems"
  weight = 3
  parent = "Analysis II: Frequency response LTI"
+++
In this section we will explore how systems will react when multiple systems are interconnected. Here we can distinguish two elementary situations, through which most situations can be explained. These two situations include two systems that are cascaded and two systems that are parallel to each other.

<br></br>
## Cascaded systems
Suppose that we have two systems, with frequency responses $H_1(\mathrm{e}^{j\theta})$ and $H_2(\mathrm{e}^{j\theta})$, whose operations can be described as
\begin{equation}
    Y_1(\mathrm{e}^{j\theta}) = H_1(\mathrm{e}^{j\theta}) X_1(\mathrm{e}^{j\theta})
\end{equation}
and as
\begin{equation}
    Y_2(\mathrm{e}^{j\theta}) = H_2(\mathrm{e}^{j\theta}) X_2(\mathrm{e}^{j\theta}),
\end{equation}
where $X_i(\mathrm{e}^{j\theta})$ and $Y_i(\mathrm{e}^{j\theta})$ denote the FTD pairs of the input and output of the $i$'th filter, respectively.
Cascading the two filter means that the output of the first filter is being connected to the input of the second filter, i.e. $Y_1(\mathrm{e}^{j\theta}) = X_2(\mathrm{e}^{j\theta})$. Fig. 1 shows a visualisation of this situation. Substitution of $Y_1(\mathrm{e}^{j\theta})$ into the input of the second filter $X_2(\mathrm{e}^{j\theta})$ in the above equations will lead to
\begin{equation}
    Y_2(\mathrm{e}^{j\theta}) = \underbrace{H_2(\mathrm{e}^{j\theta}) H_1(\mathrm{e}^{j\theta})}_{H(\mathrm{e}^{j\theta})} X_1(\mathrm{e}^{j\theta}).
\end{equation}
Here we can see that we can combine the two frequency responses $H_1(\mathrm{e}^{j\theta})$ and $H_2(\mathrm{e}^{j\theta})$ into an equivalent frequency response $H(\mathrm{e}^{j\theta})$. This means that the two filters can be combined into a single filter whose frequency response is the product of these filters. By using the convolution property, the impulse response of this equivalent system can be written as
\begin{equation}
    H(\mathrm{e}^{j\theta}) = H_1(\mathrm{e}^{j\theta}) \cdot H_2(\mathrm{e}^{j\theta}) \qquad \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ \qquad h[n] = h_1[n] \ast h_2[n].
\end{equation}

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/cascade.svg"
      alt="Two systems which are cascaded and their equivalent system."
    />
    <figcaption class="numbered">
      Two systems which are cascaded and their equivalent system.
    </figcaption>
  </figure>
</div>

<br></br>
## Systems in parallel
A second situation occurs when two systems are driven by the same input signal and whose outputs are added. This situation is visualized in Fig. 2. The total output $y_\text{tot} [n]$ is formed as the addition of the individual filter outputs as
\begin{equation}
    y[n] = y_1[n] + y_2[n].
\end{equation}
Through the definition of the individual filter outputs, $y_i[n] = h_i[n] \ast x[n]$, this equation can be rewritten as
\begin{equation}
    y[n] = h_1[n] \ast x[n] + h_2[n] \ast x[n] = (h_1[n] + h_2[n]) \ast x[n].
\end{equation}
This means that the impulse response of the equivalent system can be written as the sum of the individual impulse responses. Through the FTD pairs, this addition also holds for the frequency responses.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/analysis/LTI/parallel.svg"
      alt="Two systems which are placed in parallel and their equivalent system."
    />
    <figcaption class="numbered">
      Two systems which are placed in parallel and their equivalent system.
    </figcaption>
  </figure>
</div>
