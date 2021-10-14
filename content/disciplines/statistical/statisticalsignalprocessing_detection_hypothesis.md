+++
title = "Hypothesis testing"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-01-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Hypothesis testing"        # name of this item in that menu
  weight = 81                           # location in that menu
  parent = "Detection theory"

+++

## Introduction
We have seen that detection theory answers the question of whether something is present or not. This "something" can range from bits to aircraft to malignant tissue. In the most simple case, detection theory gives us two options: the presence or absence of a signal. This section will formalize this notion and will apply it to make decisions.

<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/bRZeH2GcwjE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

<br></br>

## A hypothesis
According to the Cambridge dictionary, a <i>hypothesis</i> is an idea or explanation for something that is based on known facts but has not yet been proved. It tells us what we expect about a situation. In detection theory, there usually are multiple hypotheses (e.g., a signal is present or not).

A decision is commonly based around a <i>null hypothesis</i>, denoted by $\mathcal{H}_0$, which is the hypothesis of a default situation where nothing new is happening. The situations where something new is actually happening can be represented by the <i>alternative hypotheses</i>, denoted by $\mathcal{H}_1$, $\mathcal{H}_2$ etc.

### Example
Let us consider a simplified example of binary phase-shift keying (BPSK), which is a transmission scheme used for telecommunication. This scheme relies on the fact that the transmitter only transmits block-wave pulses with an amplitude of $-1$ and $1$, representing a 0 bit and a 1 bit, respectively. An example of such a signal is shown in Fig. 1.

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/bpsk.svg"
      alt="An example of a binary phase-shift keying (BPSK) signal."
    />
    <figcaption class="numbered">
      An example of a binary phase-shift keying (BPSK) signal.
    </figcaption>
  </figure>
</div>

Suppose that we receive a noisy signal $x[n]$, and we know that there might be a BPSK-signal present. Assuming a noise-less case with no attenuation in the transmission path, we could receive three possible amplitudes: $0$ when no signal is present, $-1$ for a 0 bit, and $1$ for a 1 bit. We could formulate the null hypothesis for each sample $n$ as $\mathcal{H}_0[n]$: no signal is present. Similarly, the alternative hypotheses can be formulated as $\mathcal{H}_1[n]$: 0 bit detected, and $\mathcal{H}_2[n]$: 1 bit detected.

When assuming the noisy case without attenuation, the received signal $x[n]$ can be described mathematically as
\begin{equation}
    x[n] =
    \begin{cases}
        \epsilon[n],            &\text{under } \mathcal{H}_0[n] \newline
        -1 + \epsilon[n],       &\text{under } \mathcal{H}_1[n] \newline
        1 + \epsilon[n],        &\text{under } \mathcal{H}_2[n]
    \end{cases}
\end{equation}
where $\epsilon[n]$ represents the noise signal.

<br></br>

## Binary hypothesis testing
The simplest case of detection theory involves only two hypotheses. Suppose that a signal $x[n]$  is received and for each sample has to be decided whether a noisy deterministic signal $s[n]$ is present, or that the sample is just noise $\epsilon[n]$.

This gives rise to two hypotheses. We could formulate the null hypothesis $\mathcal{H}_0[n]$ being that no signal is present at sample $n$ and that the received signal is purely a stochastic noise signal $\epsilon[n]$. The alternative hypothesis $\mathcal{H}_1[n]$ will then be formulated as $x[n]$ being a noisy deterministic signal $s[n]$. Let us assume that the noise is additive and unrelated to the actual underlying signal and can therefore be described as the additive noise signal $\epsilon[n]$. Using this information the signal $x[n]$ can be described as
\begin{equation}\label{eq:xn_general}
    x[n] =
    \begin{cases}
        \epsilon[n],            &\text{under }\mathcal{H}_0[n] \newline
        s[n] + \epsilon[n].     &\text{under }\mathcal{H}_1[n]
    \end{cases}
\end{equation}

In the previous reader on random signals and processes, the random noise was modeled according to a probability distribution $p(\epsilon[n])$, because an accurate prediction of instantaneous values of the noise was impossible. As a common approximation, supported by the central limit theorem, the noise is assumed to be distributed according to a Gaussian distribution $\mathcal{N}(\mu, \sigma^2)$ with mean $\mu$ and variance $\sigma^2$. For the moment, let us assume that the distribution has zero mean ($\mu$ = 0) and variance $\sigma^2$. Under the null hypothesis $\mathcal{H}_0[n]$, the probability density function of the received signal $x[n]$ follows the probability distribution of the noise $\epsilon[n]$. Under the alternative hypothesis $\mathcal{H}_1[n]$, the received signal still follows the probability density function of the noise. However, it is offset by the value of the deterministic signal $s[n]$. In other words, the probability density function of the received signal has its mean at the value of the deterministic signal.

When discussing the probability density function of $x[n]$ under the assumption that the hypothesis $\mathcal{H}_i[n]$ is true, we can represent this probability density function as $p(x[n]\mid\mathcal{H}_i[n])$. For the general case, where the received signal can be described as in the introduction of this module and where the noise is Gaussian distributed with zero mean (i.e. $\epsilon[n] \sim \mathcal{N}(0, \sigma^2)$), the probability density function of the received signal $x[n]$ is given by
\begin{equation}
    p(x[n]) =
    \begin{cases}
        p(x[n]\mid\mathcal{H}_0[n]) = \mathcal{N}(0,\sigma^2),     &\text{under }\mathcal{H}_0[n] \newline
        p(x[n]\mid\mathcal{H}_1[n]) = \mathcal{N}(s[n],\sigma^2).     &\text{under }\mathcal{H}_1[n] \\
    \end{cases}
\end{equation}
A graphical representation of the probability distribution of $x[n]$ is given in Fig. 2. In this case, there are two possible distributions for $x[n]$, since it is unknown whether $\mathcal{H}_0[n]$ or $\mathcal{H}_1[n]$ is the correct hypothesis. It should be noted that both distributions do not occur simultaneously, since only a single hypothesis can be true per sample.

<div style="max-width: 800px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/binary_sn.svg"
      alt="Two distributions of the signal $x[n]$ for the cases when either $\mathcal{H}_0[n]$ or $\mathcal{H}_1[n]$ is true."
    />
    <figcaption class="numbered">
      Two distributions of the signal $x[n]$ for the cases when either $\mathcal{H}_0[n]$ or $\mathcal{H}_1[n]$ is true.
    </figcaption>
  </figure>
</div>

<br></br>

## Decision criterion
If we continue with the simple binary case presented above, we now know how the signal $x[n]$ can be distributed for both hypotheses, of which an example was shown in Fig. 2. So given this information, how do we know whether we are dealing with hypothesis $\mathcal{H}_0[n]$ or $\mathcal{H}_1[n]$ after receiving an individual signal sample $x[n]$?

The answer is that we cannot know this. However, we can determine the probability of receiving this random sample under the null hypothesis as $p(x[n]\mid\mathcal{H}_0[n])$ and under the alternative hypothesis as $p(x[n]\mid\mathcal{H}_1[n])$. A possible way to decide whether the signal is present ($\mathcal{H}_1[n]$) or not ($\mathcal{H}_0[n]$) is to compare the probabilities of the sample under both hypotheses. We could say that we regard $\mathcal{H}_0[n]$ as true if $p(x[n]\mid\mathcal{H}_0[n]) > p(x[n]\mid\mathcal{H}_1[n])$ and otherwise we regard $\mathcal{H}_1[n]$ as true. In other words, we can regard $\mathcal{H}_0[n]$ as true if it is more likely that the received sample $x[n]$ originated from the probability distribution of $\mathcal{H}_0[n]$ than of $\mathcal{H}_1[n]$.

In many cases, direct comparisons between the two signal sample probabilities might not be desired. In radar, for example, we would like to be especially certain about a detection in order to prevent the consequences of making a false detection. In this case, we could decide to use a different <i>decision criterion</i>, which tells us when we should decide that one hypothesis is true over another. An example is to decide for $\mathcal{H}_1$ when it is at least $\gamma$ times more likely than $\mathcal{H}_0$. So we can decide that we have detected a deterministic signal ($\mathcal{H}_1[n]$) when it holds that $p(x[n]\mid\mathcal{H}_1[n])>\gamma \cdot p(x[n]\mid\mathcal{H}_0[n])$.


Rearranging the above condition leads to the condition in terms of a likelihood ratio test as

\begin{equation} \label{eq:prob_ratio}
    \frac{p(x[n]\mid\mathcal{H}_1[n])}{p(x[n]\mid\mathcal{H}_0[n])} \lessgtr\_{\mathcal{H}_1[n]}^{\mathcal{H}_0[n]} \gamma.
\end{equation}
This reads as: decide $\mathcal{H}_1[n]$ if the ratio exceeds $\gamma$ and decide $\mathcal{H}_0[n]$ otherwise. The decision can also be evaluated graphically. The probability density function corresponding to $\mathcal{H}_0[n]$ should then be scaled vertically by a factor $\gamma$ and the (scaled) distribution with the highest value at the observed sample $x[n]$ is then regarded to be the true hypothesis.

<br></br>

## Decision boundary
At some points, the ratio above leads to equality. Let us consider the simple case when $\gamma=1$ for further discussion. The physical meaning of this equality is that the observed sample $x[n]$ is equally likely to occur under $\mathcal{H}_0[n]$ as $\mathcal{H}_1[n]$. Therefore the choice of the more likely hypothesis is arbitrary. The points at which this equality occurs create the <i>decision boundary</i> of the detection problem. In Fig. 2, this decision boundary, also known as the decision threshold, is located at $x\_{th}[n] = \frac{1}{2}s[n]$.


For some arbitrary univariate distributions, there may be multiple decision boundaries that separate different intervals, as shown in the left plot of Fig. 3. The decision boundary is represented by a line for the multivariate case, as shown in the right plot of Fig. 3.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/decision_boundary.svg"
      alt="This figure gives two example of decision boundaries. In (a) two univariate distributions have multiple decision boundary points and in (b) the decision boundary of the multivariate distributions is represented by a line."
    />
    <figcaption class="numbered">
      This figure gives two example of decision boundaries. In (a) two univariate distributions have multiple decision boundary points and in (b) the decision boundary of the multivariate distributions is represented by a line.
    </figcaption>
  </figure>
</div>

### Example: DC in noise
Consider the example where a noisy signal is received. The noise is distributed according to a zero-mean Gaussian distribution with unity variance, i.e., $\epsilon[n]\sim\mathcal{N}(0,1)$. Furthermore, a deterministic DC signal with amplitude $A$ might be present in the received signal. This information allows us to model the received signal $x[n]$ as
\begin{equation}
    x[n] =
    \begin{cases}
        \epsilon[n],        &\text{under }\mathcal{H}_0[n], \\
        A + \epsilon[n],    &\text{under }\mathcal{H}_1[n].
    \end{cases}
\end{equation}
The null hypothesis $\mathcal{H}_0[n]$ is chosen to be the case when the DC signal is not present, and the alternative hypothesis $\mathcal{H}_1[n]$ is chosen as the case when the signal is indeed present.

Using the above definition, the probability density function of our observation $x[n]$, also known as our likelihood function, can be determined as
\begin{equation}
    p(x[n]) =
    \begin{cases}
        \mathcal{N}(0,1),   &\text{under }\mathcal{H}_0 \newline
        \mathcal{N}(A,1).   &\text{under }\mathcal{H}_1
    \end{cases}
\end{equation}

For $\gamma=1$ the decision boundary can be determined by using symmetry arguments or analytically by solving
\begin{equation}
    \frac{p(x_{th}[n]\mid\mathcal{H}_0[n])}{p(x_{th}[n]\mid\mathcal{H}_1[n])} = 1
\end{equation}
for the decision threshold $x_{th}[n]$, which occurs when the probability ratio leads to equality. Separating the terms and substituting the definition of the Gaussian distributions gives us
\begin{equation}
    \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2}x_{th}^2 [n]}= \frac{1}{\sqrt{2\pi}} e^{-\frac{1}{2}(x_{th}[n]-A)^2}.
\end{equation}
Multiplying both sides with $\sqrt{2\pi}$ and consecutively calculating the natural logarithm ($\ln \left\\{\cdot\right\\}$) of both sides simplifies the equality to
\begin{equation}
    -\frac{1}{2}x^2_{th}[n] = -\frac{1}{2}(x_{th}[n]-A)^2,
\end{equation}
where both sides can be multiplied by $-2$ and the powers can be expanded as
\begin{equation}
    x_{th}^2[n] = x_{th}^2[n] -2Ax_{th}[n] + A^2.
\end{equation}
The last step is to solve this equation for $x_{th}[n]$, which can be obtained as
\begin{equation}
    x_{th}[n] = \frac{1}{2}A,
\end{equation}
which is the midway point in between the means of the possible distributions of $x[n]$. So when $x[n] < \frac{1}{2}A$ holds, $\mathcal{H}_0[n]$ is regarded as true and when $x[n] > \frac{1}{2}A$ holds, $\mathcal{H}_1[n]$ is regarded as true.

<br></br>

## Probability of detection and false alarm
Until now, we have seen using the decision criterion of the probability ratio that we can define a decision boundary that lets us estimate the correct hypothesis for each sample. However, this estimate is not guaranteed to be correct. In the example above, it might be possible that you decide that there is a DC signal present in the received signal when it is not present because the threshold is exceeded due to the noise component.

Since the probability distributions of both hypotheses are known, it is possible to calculate how often a wrong decision is made, which occurs when the random noise component exceeds the decision boundary. Fig. 4 shows the true situations as defined by the hypotheses and the regions in which is decided for a certain hypothesis. Two important probabilities can be determined from this figure. The <i>probability of detection</i>, denoted by $\text{P}\_D$, is the probability that a deterministic signal is correctly detected. The <i>probability of a false alarm</i>, denoted by $\text{P}\_{FA}$, is the probability that you decide that a deterministic signal is present in the situation when there actually only is noise. A false alarm is also known as a type I error, and a miss, which occurs when not detecting a deterministic signal, is called a type II error. In this case, the probabilities can easily be determined using the ${Q}(\cdot)$-function, because we are dealing with a Gaussian probability density function. The values of $\text{P}\_D$ and $\text{P}\_{FA}$ can, in this case, be determined respectively as
\begin{equation}
    \text{P}\_D = \int_{x_{th}}^\infty p(x\mid \mathcal{H}_1[n]) \mathrm{d}x = Q\left(\frac{x_{th}-s[n]}{\sigma}\right)
\end{equation}
and
\begin{equation}
    \text{P}\_{FA} = \int_{x_{th}}^\infty p(x\mid \mathcal{H}_0[n]) \mathrm{d}x = Q\left(\frac{x_{th}}{\sigma}\right).
\end{equation}

<div style="max-width: 600px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/detection_probabilities.svg"
      alt="Visual representation of the probability distribution for both hypotheses $\mathcal{H}_0$ and $\mathcal{H}_1$. In both cases the decision boundary is drawn with the corresponding choice of estimated hypothesis. The highlighted areas represent the probabilities of making a good or wrong decision and the conventional naming of these areas is given in the legends."
    />
    <figcaption class="numbered">
      Visual representation of the probability distribution for both hypotheses $\mathcal{H}_0$ and $\mathcal{H}_1$. In both cases the decision boundary is drawn with the corresponding choice of estimated hypothesis. The highlighted areas represent the probabilities of making a good or wrong decision and the conventional naming of these areas is given in the legends.
    </figcaption>
  </figure>
</div>

For an ideal receiver it is desired that the probability of detection is close to one and that the probability of a false alarm is close to zero. By shifting the decision boundary, different probabilities can be obtained. From Fig. 4 it can be seen that it is impossible to satisfy both requirements for an ideal receiver at once. Shifting the decision boundary either improves $\text{P}\_{D}$ and deteriorates $\text{P}\_{FA}$ or vice versa. This means that a compromise between the two performance metrics has to be found.

<br></br>

## Neyman-Pearson theorem
Previously we have introduced the parameter $\gamma$ in the probability ratio, which indirectly determined the location of the decision boundary. Now we have also seen that this decision boundary influences the probability of detection and false alarm. Therefore we may conclude that there is a relationship between $\text{P}\_D$, $\text{P}\_{FA}$, and $\gamma$ that is determined by the underlying probability density functions. Graphical visualizations that represent the relationship between both probabilities for a continuous range of $\gamma$ are called receiver operation characteristics (ROC) plots.

When designing a receiver, several approaches can be taken. The goal is to determine the decision boundaries in order to achieve a certain performance. By fixing $\text{P}\_D$ or $\text{P}\_{FA}$ to a desired value, the decision boundaries can be calculated. Because of the trade-off between the performance metrics, it is impossible to fix them both at the same time.

When considering a constant false alarm rate (CFAR), $\text{P}\_{FA}$ is fixed to the constant value $\alpha$, usually around $10^{-4}$ to $10^{-6}$ for radar-related problems. From this approach, the <i>Neyman-Pearson theorem</i> arises. This theorem states that in order to maximize $\text{P}\_{D}$ for a fixed $\text{P}\_{FA}=\alpha$, decide for the alternative hypothesis $\mathcal{H}\_1$ if
\begin{equation}\label{eq:prob_ratio2}
    L(x[n]) = \frac{p(x[n]\mid\mathcal{H}\_1[n])}{p(x[n]\mid\mathcal{H}\_0[n])} > \gamma,
\end{equation}
where the indirect decision threshold $\gamma$ is determined from solving
\begin{equation}\label{eq:neyman_pearson}
    \text{P}\_{FA} = \int_{\left\\{x[n]:L(x[n])=\gamma\right\\}}^\infty p(x[n]\mid\mathcal{H}_0[n])\mathrm{d}x=\alpha.
\end{equation}
This theorem boils down to the following: decide for the alternative hypothesis $\mathcal{H}_1[n]$ if the above ratio is satisfied, where the value of $\gamma$ can be found by solving the above equation. This integral is mere a formal definition of the probability of a false alarm determined from the area under the probability density function as depicted in Fig. 4. Here the lower bound is given by the decision boundary, which is determined by $\gamma$. Any detector where the detection is based on this theorem is called a <i>Neyman-Pearson detector</i>.

Fixing the probability of a false alarm determines the probability of detection from the probability density functions. So by fixing the false alarm rate, the probability of detection cannot be changed in the case of external signals. In some specific applications, where the received signal level can be controlled, it is possible to fix the probability of a false alarm and to improve the probability of detection. This can, for example, be intuitively improved by increasing the signal amplitude, which increases the distance between the two distributions from Fig. 4, leading to better performance.
