+++
title = "Detection theory"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-01-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.information]                       # name of menu section (main module)
  name = "Detection theory"        # name of this item in that menu
  weight = 20                           # location in that menu

+++

## Introduction

Noise makes it impossible to predict instantaneous values of received signals. Instead, we can define a probability density function that can tell us how likely it is that the received signal is within a certain interval. This probability density function is defined by the deterministic component of the stochastic signal, i.e. the noise-less signal, and the probability distribution of the noise signal. A discrete-time stochastic signal $x[n]$ can therefore be split into a deterministic signal $s[n]$ and a stochastic noise component $\epsilon[n]$ as
\begin{equation}
    x[n] = s[n] + \epsilon[n].
\end{equation}

Now imagine the case where the noise power is close to or larger than the signal power. This situation might occur if the received deterministic signal has suffered from significant attenuation in its transmission path. Fig. 1 shows three received signals where the deterministic component is a block-wave pulse. The noise power in all three cases is kept constant, whereas the signal power is consecutively decreased as a result of attenuation.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/detection_difficulties.svg"
      alt="Visualisation of the difficulties of signal detection."
    />
    <figcaption class="numbered">
      Three received signals are shown, where the received deterministic signal is plotted on top of the noisy received signal. The noise power is kept constant, whereas the deterministic signal power is decreased for each plot.
    </figcaption>
  </figure>
</div>

One would conclude from the left and middle plot of Fig. 1 that the deterministic block-wave pulse signal can visually be detected. However, this conclusion is not as apparent in the case presented by the right plot. We could even ask ourselves the question whether there actually is a deterministic signal present in the noise. The principles that focus on providing the answer to this question are the underlying foundation of <i>detection theory</i>.

### The detection problem
The importance of detection theory might become evident in the case of telecommunication, where we are interested in the transmitted signal. By being able to distinguish between transmitted bits (0's and 1's) the original message can be reconstructed leading to successful communication. However, the field of telecommunication is not the only field where detection plays an important role.

Another example of detection theory involves radar or sonar, where the goal is to identify flying or submerged objects. In the case of radar we might for example be interested in the detection of a hostile aircraft. The detection of such an aircraft is of vital importance, since an appropriate reaction needs to be taken in case it actually is present (i.e. the aircraft needs to be taken down). However, if an aircraft is detected by the system and there actually is not one, than the consequences of performing a military counter-operation might cause a disastrous international conflict.

The field of detection theory also extends to the field of medicine, where an example is provided by the detection of cancerous tissue. The early detection of malignant (Dutch: kwaadaardig) tissue proves to be of vital importance in the treatment process. Failing to detect such a malignant tissue might damage the chances of successful treatment. However, when a malignant tumor is detected, whereas the tumor is actually benign (Dutch: goedaardig), the patient will undergo unnecessary treatment that can be harmful to the health of the patient.

<br></br>

## Module overview
This module will cover the field of detection theory.

1. <a href="../../information/informationandcommunication_detection_hypothesis">Hypothesis testing</a> - This section will cover the decision theory concerning whether the a signal is measured or whether it is absent.
2. <a href="../../information/informationandcommunication_detection_matched">Matched filter</a> - When the decision criteria is established, a practical application can be created. The idealized filter for testing whether a signal is present is called a matched filter.
3. <a href="../../information/informationandcommunication_detection_tests">Statistical tests</a> - A single observation is usually not enough to accept or reject a hypothesis. Usually a decision is based on multiple observations to limit the effect of measurement noise. This section will discuss how decisions can be made when dealing with limited information.
