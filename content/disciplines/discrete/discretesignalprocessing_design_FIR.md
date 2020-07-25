+++
title = "FIR filter design"

# date = {{ .Date }}
lastmod = 2020-06-13

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.discrete]
  name = "FIR filter design [⯈]"
  weight = 2
  parent = "Filter design"
+++


### Screencast video [⯈]
<div class="video-container">
<iframe width="100%" height="100%" src="https://www.youtube.com/embed/SNQGOLtoIVc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<br></br>
One of the most important advantages of FIR filters over IIR filters is that FIR filters can be easily constrained to have exact linear phase.
The frequency response of an $M$-th order causal FIR filter with linear phase is given by the following equation:
\begin{eqnarray*}
h[n]=\sum_{k=0}^{M-1} h_k \delta[n-k]
& \circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ & H(e^{j\theta}) = \sum_{k=0}^{M-1} h_k e^{-jk \theta}
= |H(e^{j\theta})| \cdot e^{j\varphi \\{ H(e^{j\theta}) \\}}\newline
&\mbox{ with }& \varphi \\{ H(e^{j\theta}) \\} = \color{red}{c} \cdot \theta + \color{blue}{\alpha} \cdot \frac{\pi}{2}
\end{eqnarray*}
Recall from the reader about filter structures that a linear phase characteristic simply corresponds to a time shift or delay and thus such linear phase filters can preserve the waveshape of the input signal. Furthermore linear phase can only be achieved with even or odd symmetric impulse responses with even or odd length, resulting into four different symmetries. The values of frequency responses at frequencies $\theta=0$ and $\theta=\pm \pi$ of these four different types are denoted in the following table:
<table style="width:100%">
  <tr>
    <th>Type</th>
    <th>Symmetry</th>
    <th>Length</th>
    <th>$\theta=0$</th>
    <th>$\theta=\pm \pi$</th>
  </tr>
  <tr>
    <td>I</td>
    <td>Even</td>
    <td>Odd</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>II</td>
    <td>Even</td>
    <td>Even</td>
    <td></td>
    <td>$H_{II}(\mbox{e}^{\pm j \pi})=0$</td>
  </tr>
  <tr>
    <td>III</td>
    <td>Odd</td>
    <td>Odd</td>
    <td>$H_{III}(e^{j0})=0$</td>
    <td>$H_{III}(\mbox{e}^{\pm j \pi})=0$</td>
  </tr>
  <tr>
    <td>IV</td>
    <td>Odd</td>
    <td>Even</td>
    <td>$H_{IV}(e^{j0})=0$</td>
    <td></td>
  </tr>
</table>

From this table it follows that the frequency response for a type II filter has the property that it is always zero for $\theta=\pm \pi$ , and is therefore not appropriate for a High Pass Filter. Similarly, filters of type III and IV introduce are always zero at $\theta=0$ which makes them
unsuitable for as Low Pass Filters. Additionally, the type III response is always zero at $\theta=\pm \pi$, making it only suitable as Band Pass Filter. The type I filter is the most versatile of the four.
These properties are summarized in the following table:

\begin{center}
\begin{tabular}{|c|c|c|c|}
\hline
Type & \multicolumn{2}{|c|}{Zero at} & Comment \\
& $\theta=0$ & $\theta=\pm \pi$ & \\ \hline \hline
I & -- & -- & --\\ \hline
II & -- & Yes & No HPF possible\\ \hline
III & Yes & Yes & Only Bandpass possible\\ \hline
IV & Yes & --& No LPF possible\\
\hline
\end{tabular}
\end{center}
<table style="width:100%">
  <tr>
    <th>Type</th>
    <th colspan="2">Zero at</th>
    <th>Comment</th>
  </tr>
  <tr>
    <th></th>
    <th>$\theta=0$</th>
    <th>$\theta=\pm \pi$</th>
    <th></th>
  </tr>
  <tr>
    <td>I</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>II</td>
    <td></td>
    <td>Yes</td>
    <td>No HPF possible</td>
  </tr>
  <tr>
    <td>III</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Only bandpass possible</td>
  </tr>
  <tr>
    <td>IV</td>
    <td>Yes</td>
    <td></td>
    <td>No LPF possible</td>
  </tr>
</table>
Because FIR filters are generally designed to have linear phase, we consider the following three design procedures:
<ol>
  <li>Based on the FTD and windowing,</li>
  <li>Based on equiripple filter design and</li>
  <li>Based on frequency sampling.</li>
</ol>

<br></br>
## Design based on FTD and windowing
The main steps of the design based on the FTD and windowing are depicted in Fig. 1 and are as follows:
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/FTDwindowing.svg"
      alt="Design steps based on FTD and wndowing."
    />
    <figcaption class="numbered">
      Design steps based on FTD and wndowing.
    </figcaption>
  </figure>
</div>

<ol>
  <li>Assume that the desired ideal Low Pass Filter response $H_d(e^{j\theta})$ with cutoff frequency $\theta_c$ is known as depicted in the figure.</li>
  <li>Using the inverse FTD we can determine the, infinite length, non-causal, desired impulse response $h_d[n]=\frac{\theta_c}{\pi} \cdot \frac{\sin(\theta_c n)}{\theta_c n}$.</li>
  <li>In the window method, a finite length FIR filter is obtained by multiplying this desired impulse response $h_d[n]$ with a finite length window $w[n]$.</li>
  <li>The result is a finite duration impulse response $h[n]$.</li>
  <li>The time domain window $w[n]$ can be represented in the frequency domain by $W(e^{j\theta})$, while the multiplication operation in the time domain is represented in the frequency domain by a convolution which results in the non-ideal frequency response $H(e^{j\theta})$ that is obtained as the convolution result of the ideal frequency response $H_d(e^{j\theta})$ with $W(e^{j\theta})$, which results in a smoothed version of the ideal frequency response. In the next subsection we will show that there are different types of windows that may be used in the window design method. We will also see that how well the non-ideal frequency response $H(e^{j\theta})$ approximates the desired ideal frequency response $H_d(e^{j\theta})$ is determined by the width of the main lobe of $W e^{j\theta})$ and its side-lobe peak. In the ideal case the main lobe width should be extremely narrow approaching a delta pulse.</li>
  <li>As a final step the finite length non-causal impulse response $h[n]$ can be made causal by shifting it in such a way that all impulse response indices are greater or equal than zero, represented by the causal impulse response $h_c[n]$.  This shift operation causes a linear phase change of all frequencies of the filter $H_d(e^{j\theta})$.</li>
</ol>


### Different window shapes
Some commonly used windows for filter design are depicted in Fig. 2.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/differentwindows.svg"
      alt="Four commonly used windows for design based on FTD and windowing."
    />
    <figcaption class="numbered">
      Four commonly used windows for design based on FTD and windowing.
    </figcaption>
  </figure>
</div>
The left hand side figures show the time domain representation $w[n]$ of four different windows all of length $M=32$ . The right hand plots show the frequency representations $W(e^{j\theta})$ of these windows in which the magnitude is denoted on dB scale. The analytical expressions of the time- domain representations of these four windows are given by the following equations:
<ul>
  <li> <b><u>Rectangular window</u></b> $$
  w[n]= \left \{
  \begin{array}{ll}
  1 & \mbox{for } 0 \leq n \leq M-1 \\
  0 & \mbox{otherwise}
  \end{array} \right .
  $$
  </li>
  <li> <b><u>Hanning window</u></b>
  $$
  w[n]= \left \{
  \begin{array}{ll}
  0.5 - 0.5 \cos (\frac{2 \pi}{M}n) & \mbox{for } 0 \leq n \leq M-1 \\
  0 & \mbox{otherwise}
  \end{array} \right .
  $$
  </li>

  <li> <b><u>Hamming window</u></b>
  $$
  w[n]= \left \{
  \begin{array}{ll}
  0.54 - 0.46 \cos (\frac{2 \pi}{M}n)  & \mbox{for } 0 \leq n \leq M-1 \\
  0 & \mbox{otherwise}
  \end{array} \right .
  $$
  </li>
  <li> <b><u>Blackman window</u></b>
  $$
  w[n]= \left \{
  \begin{array}{ll}
  0.42 - 0.5 \cos (\frac{2 \pi}{M}n) +0.08 \cos (\frac{4 \pi}{M}n) & \mbox{for } 0 \leq n \leq M-1 \\
  0 & \mbox{otherwise}
  \end{array} \right .
  $$
  </li>
</ul>

These analytical expressions can simply be used to calculate the coefficients $h[n]$ as the product of $h_d[n] \times w[n]$.

### Main window characteristics
The window design method is determined by the following two most important factors of the window: Its main lobe width $\Delta$  and the amplitude $A$ of the side-lobe peak, which are depicted in Fig. 3.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/window.svg"
      alt="Main window characteristics."
    />
    <figcaption class="numbered">
      Main window characteristics.
    </figcaption>
  </figure>
</div>
Ideally the main-lobe width $\Delta$ should be narrow, and the side-lobe amplitude $A$ should be small. Some general properties $W(e^{j\theta})$ are:
<ul>
  <li>The causal FIR filters that is obtained by truncating the impulse response coefficients of the ideal filters results in an fluctuating behavior of the magnitude response, which is more commonly referred to as the Gibbs phenomenon.</li>
  <li>The time- bandwidth product $M \cdot \Delta$ is constant. As a result, in practice, where we want to have a main lobe width $\Delta$ as narrow as possible, this can only be achieved by increasing the length $M$ of the FIR filter, which implies an increase of complexity.</li>
  <li>The side-lobe amplitude $A$ does not depend on the length $M$ but on the window shape. Usually a smaller side-lobe amplitude $A$ results in a wider main-lobe width $\Delta$.</li>
  <li>The main-lobe width $\Delta$ is directly related to the transition band.</li>
</ul>

The following table shows the main characteristics of the four windows:

<table style="width:100%">
  <tr>
    <th>Window</th>
    <th>$\color{blue}{A}$ [dB]</th>
    <th>Transition $\color{red}{\Delta}$</th>
    <th>Stopband [dB]</th>
  </tr>
  <tr>
    <td>Rectangular</td>
    <td>-13</td>
    <td>$1 \times (2 \pi/M)$</td>
    <td>-21</td>
  </tr>
  <tr>
    <td>Hanning</td>
    <td>-31</td>
    <td>$3.1 \times (2 \pi/M)$</td>
    <td>-44</td>
  </tr>
  <tr>
    <td>Hamming</td>
    <td>-41</td>
    <td>$3.3 \times (2 \pi/M)$</td>
    <td>-53</td>
  </tr>
  <tr>
    <td>Blackman</td>
    <td>-57</td>
    <td>$5.5 \times (2 \pi/M)$</td>
    <td>-74</td>
  </tr>
</table>

<div class="example">
<h4> Example </h4>
<hr>
Design an FIR linear phase filter according to the specifications as depicted in the following figure:
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example1.svg"
      alt="Main window characteristics."
    />
  </figure>
</div>
The cutoff frequency $\theta_c=0.2 \pi$, is in the middle of the Pass Band and Stop Band cutoff frequencies $\theta_p$ and $\theta_s$ respectively.
First derive an appropriate window and filter length. Than give an explicit equation of the impulse response weights $h[n]$.
Finally give plots that show the values of this impulse response and its magnitude response in dB scale.
<button class="collapsible">Show solution</button>
<div class="content">
For a Stop Band attenuation of 20 log(0.01)=-40 dB, we may use a {\color{brown}Hanning window} to window the impulse response weights.
Furthermore, because the specifications calls for a transition width of $\Delta=0.02 \pi$ it follows from the characteristics of a Hanning window that the required filter order should be $M=310$ samples long,  and thus the impulse response has to be delayed by {\color{red}155} samples to make it causal. From this it follows that the analytical expression for  the impulse response weights is as follows:
$$
h[n]= \frac{\sin(\color{blue}{0.2 \pi} (n - \color{red}{155}))}{(n-\color{red}{155}) \pi} \times
\left \{
\color{brown}{0.5 - 0.5 \cos (\frac{2 \pi}{310} \cdot n)}  \right \}
$$
Although we could also could have used a Hamming or a Blackman window, these windows would over design the filter and produce larger stop-band attenuation at the expense of an increase in the transition width.
The following plots show on top the values of this impulse response $h[n]$, in the middle figure the magnitude response in dB scale.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example1resulta.svg"
      alt="Main window characteristics."
    />
  </figure>
</div>
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example1resultb.svg"
      alt="Main window characteristics."
    />
  </figure>
</div>
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/example1resultc.svg"
      alt="Main window characteristics."
    />
  </figure>
</div>
The plot at the bottomside gives a more detailed zoom in of the Pass Band.
</div>
</div>



<br></br>
## Equiripple linear phase filter design
The design based on FTD and windowing is simple and generally results in a filter with relative good performance. However the result is in general not optimal in two respects:
<ol>
  <li>The pass band and stop band deviations $\delta_p$ and $\delta_s$ are approximately equal. In general the stop band deviation $\delta_s$ can be much smaller than the pass band deviation $\delta_p$. In the FTD and windowing approach these parameters cannot be independently controlled and therefore it is necessary to over design the filter pass band in order to satisfy the stricter requirements in the stop band.</li>
  <li>For most windows, the pass band and stop band ripple is not uniform.  In general the ripple decreases when moving away from the transition band. A smaller peak ripple could be produced when it would be possible to distribute the ripple more uniformly over the entire band would.</li>
</ol>

Parks and McClellan developed an iterative optimization algorithm with which these problems are solved. As a result this filter design approach results in a filter with less weights compared to the number of weights that are needed for the FTD and windowing approach.
The following equation gives a rough estimate of the filter length when using this approach:
\begin{equation}\label{Eq:LengthEquiripple}
M \approx \frac{-10 ^{10}\mbox{log}(\delta_p \cdot \delta_s)-13}{14.6 \cdot \frac{\Delta}{2\pi}}
\end{equation}
This Parks and McClellan equiripple design algorithm is implemented amongst others in the filter Designer programme of Matlab.

<div class="example">
<h4> Example </h4>
<hr>
When using the Parks and McClellan equiripple design algorithm calculate the filter length $M$ of the same filter of the previous exercise.
<button class="collapsible">Show solution</button>
<div class="content">
Using equation (\ref{Eq:LengthEquiripple}) to find the length of the filter results into the following:
$$
M = \frac{-10 ^{10}\mbox{log}(0.01 \times 0.01)-13}{14.6 \times (0.02 \pi/2 \pi)} \approx 185
$$
Thus for the same example as on the previous slide, this equiripple filter design approach leads to an FIR filter with $M=185$ weights, which is much less than the 310 weights that where needed for the FTD and windowing approach.</div>
</div>

<br></br>
## Design based on Frequency sampling filter
Another method for FIR filter design is the frequency sampling approach.
With frequency response $H(e^{j\theta})$, which is the FTD of the length $M$ FIR impulse response $h[n]$, and $H[k]$ the $M$ DFT coefficients, we have seen in the module about special filter structures that the frequency sampling filter parameterizes the desired frequency response $H(e^{j\theta})$ at $M$ uniformly spaced frequencies between $\theta=0$ and $\theta=2\pi$ by the $M$ DFT coefficients $H[k]$.
\begin{eqnarray*}
h[n] \mbox{ }\overset{\mbox{FTD}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}\mbox{ } H(e^{j\theta})
& \mbox{and} &
h[n] \mbox{ }\overset{\mbox{DFT}}{\circ  \hspace{-1.7mm} - \hspace{-1.7mm}  \circ}\mbox{ } \color{blue}{H[k]} \hspace{2mm} k=0,1, \cdots, M-1 \newline
\mbox{Frequency sampling} & \Rightarrow & H(e^{j\theta})|_{\theta = k \cdot \frac{2\pi}{M}} = \color{blue}{H[k]}
\end{eqnarray*}
As a result of the use of the DFT description, it is assumed in this approach that both the impulse response $h[n]$ and the DFT coefficients $H[k]$ are periodic sequences with period $M$.

In practice this approach is used to implement narrow band filters in which case most of the DFT coefficients are equal to zero. In such cases the filter is not implemented as transversal filter with $M$ weights but it can be implemented very efficiently as depicted in Fig. 4.
<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/Freqsampl.svg"
      alt="Frequency sampling structure."
    />
    <figcaption class="numbered">
      Frequency sampling structure.
    </figcaption>
  </figure>
</div>
This structure consists of the cascading of a filter, indicated by a red dotted box, with $M$ equally spaced zeros on the unit circle and a parallel structure, indicated by a blue dotted box, in which the weight $\alpha_l$ denote $M$ uniformly spaced poles on the unit circle. Only in those cases where the DFT weight $H[k]$ is not equal to zero, the pole cancels the zero at that particular frequency $\theta= k \cdot \frac{2\pi}{M}$. In the other cases, where $H[k]=0$, the frequency response is equal to zero at that particular frequency.

### Example design based on Frequency sampling filter
As an example we design a Low Pass Filter based on frequency sampling by predefining the frequency response $H(e^{j\theta})$ at $M=33$ uniformly spaced frequencies between $\theta=0$ and $\theta=2\pi$. Thus we use a $M=33$ point DFT  and we define the DFT coefficients $H[k]$
as follows:
\begin{equation}\label{Eq:HkFreqSamp}
H[k]=\left \\{
\begin{array}{ll}
1 & \mbox{for} \hspace{2mm} 0 \leq k \leq 8 \hspace{2mm} \mbox{and} \hspace{2mm} 25 \leq k \leq 32
\newline
0 & 9 \leq k \leq 24
\end{array}
\right .
\end{equation}
These DFT samples are depicted in Fig. 5 in black. The left hand plot side shows the DFT magnitudes samples $|H[k]|$ and the right hand plot shows the phase of the DFT samples.
<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/design/FreqSAbsHtheta.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/discrete/design/FreqSPhaseHtheta.svg"
    style="width:100%">
  </div>
</div>
<figcaption class="numbered">
  Magnitude and Phase response of frequency sampling filter according equation (\ref{Eq:HkFreqSamp}): The DFT samples are denoted in black. The red and blue drawn lines show the FTD result.
</figcaption>
</figure>
Remember that the frequency indices $k$ represent uniformly spaced frequencies between $\theta=0$ and $\theta=2\pi$. Thus, the cutoff frequency of the Low Pass Filter is in between the frequency index $k=8$ and $k=9$, which is approximately equal to $\theta_c \approx \frac{\pi}{2}$.

By applying the 33 point Inverse DFT f equation(\ref{Eq:HkFreqSamp}) we obtain the $M=33$ weights of the FIR impulse response $h[n]$ as depicted in Fig. 6.
<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/discrete/design/FreqSImphn.svg"
      alt="Impulse response obtained via the inverse DFT of equation(\ref{Eq:HkFreqSamp})."
    />
    <figcaption class="numbered">
      Impulse response obtained via the inverse DFT of equation(\ref{Eq:HkFreqSamp}).
    </figcaption>
  </figure>
</div>
A check how well the DFT weights approximate the frequency response can be obtained by applying the FTD to these $M=33$ weights of the impulse response $h[n]$. The red drawn line at the left hand side of Fig. 5 shows the magnitude response $|H(e^{j\theta})|$. The blue drawn line at the right hand side shows the phase response $\angle{H(e^{j\theta})}$. Both magnitude and phase response are depicted as a function of the continuous frequency $\theta$ in the range $\theta=0$ and $\theta=2\pi$.  From these figures it is clear that the frequency response $H(e^{j\theta})$ of the designed filter only equals the predefined values $H[k]$ at the $M=33$ uniformly spaced frequencies between $\theta=0$ and $\theta=2\pi$.  Furthermore it can be seen from the phase response, in blue, that the filter is not a linear phase filter, while this is a result from the fact that the impulse response $h[n]$, as depicted in Fig. 6, is not symmetric around the center point $n=16$.  By applying a phase shift to the DFT coefficients $H[k]$ the impulse response $h[n]$ can be made symmetric around the center point.

### Design based on frequency sampling: Procedure
Based on the design of the same causal low pass filter with cutoff frequency $\theta_c \approx \frac{\pi}{2}$, but now with linear phase, the design procedure of the frequency sampling approach contains the following basic steps:
<ol>
  <li>Define the frequency response $H(e^{j\theta})$ on $M$ uniformly distributed points between $\theta=0$ and $\theta=2\pi$ and take care of a phase shift in order to obtain a linear phase filter. For the example the DFT values are defined as follows:
  \begin{equation}\label{Eq:FreqLinPhase}
  H[k]=
  \begin{cases}
  e^{-j\color{red}{\bf{16}} \frac{2 \pi}{33} \cdot k} & 0 \leq k \leq 8 \\
  0 & 9 \leq k \leq 24 \\
  e^{-j\color{red}{\bf{16}} \frac{2 \pi}{33} \cdot k} & 25 \leq k \leq 32
  \end{cases}
  \end{equation}
  These DFT values are depicted in Fig. 7 in black, the left hand plot side show the DFT magnitudes samples $|H[k]|$ and the right hand plot shows the phase of the DFT samples.
  <figure>
  <div class="rowimg2">
    <div class="columnimg2">
      <img src="/../files/7.Images/discrete/design/FreqSampAbsHtheta.svg"
      style="width:100%">
    </div>
    <div class="columnimg2">
      <img src="/../files/7.Images/discrete/design/FreqSampPhaseHtheta.svg"
      style="width:100%">
    </div>
  </div>
  <figcaption class="numbered">
    Magnitude and Phase response of frequency sampling filter with linear phase according equation (\ref{Eq:FreqLinPhase}): DFT samples are denoted in black. The red and blue lines show the FTD results.
  </figcaption>
  </figure>
  </li>
  <li>To verify, the impulse response $h[n]$ of the FIR filter can be calculated via the Inverse DFT of equation (\ref{Eq:FreqLinPhase}), which results in a  symmetric function around the center point at $n=16$, as depicted in Fig. 8.
  <div style="max-width: 600px; margin: auto">
    <figure>
      <img
        src="/../files/7.Images/discrete/design/FreqSampImphn.svg"
        alt="Impulse response obtained via the inverse DFT of equation (\ref{Eq:FreqLinPhase})."
      />
      <figcaption class="numbered">
        Impulse response obtained via the inverse DFT of equation (\ref{Eq:FreqLinPhase}).
      </figcaption>
    </figure>
  </div>
  In this case and the shape of the impulse response represents a sampled Dirichlet, or sinc-like, function, which is indeed the inverse Fourier representation of a Low Pass Filter.

  The approximation of the frequency response can be evaluated by applying the FTD to these $M=33$ weights of the impulse response $h[n]$. The red drawn curve at the left hand side of Fig. 7 shows the magnitude response $|H(e^{j\theta})|$. The blue drawn curve at the right hand side shows the phase response $\angle{H(e^{j\theta})}$. Both as a functions are depicted as a function of the continuous frequency $\theta$ in the range $\theta=0$ and $\theta=2\pi$.
  </li>
  <li>Finally the filter can be implemented with the cascaded parallel structure as depicted in Fig. 4.</li>
</ol>

From this procedure it follows that this method only guarantees correct frequency response values at the points that were DFT weights are defined, thus at $M$ uniformly distributed frequencies $k \cdot \frac{2 \pi}{M}$. For this reason the design can be refined by pre defining the frequency response at more, uniformly spaced, frequencies especially to make the transition steps smaller.
