+++
title = "Sampling theorem"

# date = {{ .Date }}
lastmod = 2019-06-23

draft = false  # Is this a draft? true/false
toc = false  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "Sampling theorem"
  weight = 25
  parent = "Sampling and reconstruction"

+++


From the previous section it follows that for a system as depicted in Fig. 1, with $f\_{s,in}=f\_{s,out}=f\_s$, the output $y(t)$ of the D-to-C convertor is equal to input $x(t)$ of the ideal C-to-D convertor if the continuous-time signal $x(t)$ contains no frequencies higher than $f_{max}$ and the sampling frequency $f_s$ is larger than $2 \cdot f\_{max}$. This results into the following important <b>sampling theorem</b>, which is usually assigned to Shannon, who introduced this theorem around 1940. Almost at the same time Kotelnikov did the same. However some years before the theoretical basis was created by E.T. and J.A. Whittaker. This theorem states:

<div style="border: 1px solid black; margin-top: 20px; margin-bottom: 20px"><i>A continuous-time signal $x(t)$ with frequencies no higher than $f_{max}$ can be reconstructed exactly from its samples $x[n]= x(t)\mid_{t=n \cdot T_s}$, if samples are taken at a rate $f_s=1/T_s$, that is greater than $2 f_{max}$.</i></div>
