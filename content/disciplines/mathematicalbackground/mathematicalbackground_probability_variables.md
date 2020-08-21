+++
title = "Random variables"

# date = {{ .Date }}
lastmod = 2019-12-30

draft = false       # Is this a draft? true/false
toc = true         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Random variables"
  parent = "Probability and random variables"
  weight = 52

+++

## Introduction

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/vu-3us2-370" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

<br></br>
In the field of probability theory, processes that involve uncertainty and therefore have a random outcome are called <i>random processes</i>. These processes have outcomes that can be both numerical as categorical. An example of a numerical outcome can be the voltage measured over a noisy circuit, whereas an example of a categorical outcome can be the suit of the card drawn from a card deck. The latter can produce a card of any of the four suits: spades ($\spadesuit$), clubs ($\clubsuit$), diamonds ($\diamondsuit$) and hearts ($\heartsuit$).

In order to perform calculations with these random processes, there is a need to introduce <i>random variables</i>. Random variables map all possible outcomes in the sample space $\mathcal{S}$ to numbers on the real line and are usually denoted by a capital letter.  While an event can be both numerical as categorical, random variables are always numerical. In the case of a numerical sample space, the mapping through a random variable usually happens directly. A random variable $X$ for the previous categorical example can be found by assigning four distinct numbers $\\{ 1,2,3,4\\}$ to the four suits of cards $s$. This random variable $X(s)$ can be defined as
\begin{equation}
    X(s) =
    \begin{cases}
        1, & \text{for } s=\spadesuit\newline
        2, & \text{for } s=\diamondsuit\newline
        3, & \text{for } s=\clubsuit\newline
        4, & \text{for } s=\heartsuit
    \end{cases}
\end{equation}
However, different definitions are also allowed.
A visualization of this mapping can be found in Fig. 1, where all elements in the sample space are mapped to the real line.

<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/random_variable_mapping.svg"
      alt="Visualization of the mapping of categorical elements (suits of cards) of a sample space $\mathcal{S}$ to numerical values."
    />
    <figcaption class="numbered">
      Visualization of the mapping of categorical elements (suits of cards) of a sample space $\mathcal{S}$ to numerical values.
    </figcaption>
  </figure>
</div>

This reader will first discuss the notation and properties of random variables, after which several measures will be introduced to characterize these random variables. The most common families of random variables will be introduced together with their respective properties. Finally the reader will discuss events that contain multiple random variables.


<br></br>

## Random variables

### Discrete and continuous random variables

The group of random variables can be split into two subgroups: discrete random variables and continuous random variables. Both subgroups share the property that their outcomes involve uncertainty. The difference between the two subgroups can be found in the allowed values of that random variable. A discrete random variable can take any value of a countable list of distinct values, whereas a continuous random variable can take any value on an interval.

The previous example of the playing cards is an example of a discrete random variable, because the random variable $X$ can only take values of the set $\\{1,2,3,4\\}$. Note that although the values that a discrete random variable can take on are usually integers, this is not always the case.

An example of a continuous random variable can be the measured voltage of a noisy circuit. Suppose that the noise has a lower and an upper limit of -5 and 5 mV, respectively, then any value within this interval can be measured. Thus, the measured voltage can be regarded as a continuous random variable.

### Definitions
As briefly mentioned before, random variables are denoted by a capital letter, such as $X(s)$. The argument $s$ can be any element on the <i>domain</i> of $X$, which is the sample space. The set of values or the interval to which the domain is mapped on the real line is called the <i>range</i> $S_X$ of $X$. A possible value of $X(s)$ on the real line can be denoted by a lowercase $x$ and is called a <i>realization</i> or an <i>observation</i>.

Random variables are described by probability distributions. Two distinct categories of probability distributions exist for both discrete as continuous random variables.

### Discrete random variables

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/t_sS2ycKrdg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


The probability that a discrete random variable $X$ takes on the value $x$ can be expressed by the <i>probability mass function</i> (PMF) as

\begin{equation}
    p_X(x) = \Pr[X=x].
\end{equation}
A lower case $p$ is used to indicate that it is the probability for a single realization. The subscript indicates the random variable that is considered and again $x$ resembles the value of the realization. This function immediately returns a probability of $x$.

Besides the probability mass function, the <i>cumulative distribution function</i> (CDF) of a discrete random variable can be defined (cumulative meaning summed/accumulated) as the probability of the discrete random variable $X$ having a value lower than or equal to $x$. This function is denoted by a capital $P$ as

\begin{equation}
    P_X(x) = \Pr[X\leq x] = \sum_{x_i\in \{X\leq x\} } \Pr[X=x_i].
\end{equation}
This function equals the sum of the probabilities of all values in the range of $X$ smaller than or equal to $x$.

### Continuous random variables

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/gxSDPh5PKjM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

<br></br>
Similarly for the continuous random variables the cumulative distribution function can be defined as

\begin{equation}
    P_X(x) = \Pr[X\leq x] = \int_{-\infty}^{x}p_X(x)\mathrm{d}x.
\end{equation}
The latter term differentiating the CDF of a continuous random variable from the CDF of a discrete random variable has purposely been rewritten, because the range of $X$ is now an interval and not a countable set. Therefore integration is required instead of a summation. In this context, the term $p_X(x)$ is the <i>probability density function</i> and denotes the probability density of an event $x$. This probability density function is defined as

\begin{equation}
    p_X(x) = \frac{\mathrm{d}P_X(x)}{\mathrm{d}x}.
\end{equation}

Please note the difference in meaning between the probability mass function and the probability density function. Where the probability mass function returns a true probability, the probability density function returns a probability density. This probability density can be integrated over an interval in order to find the total probability. Suppose a continuous random variable $X$ is uniformly distributed between 0 and 1 and we want to find the probability of $X$ being a single value (e.g. 0.5) on this interval. This probability equals 0, although this might seem counter-intuitive. The interval from 0 to 1 contains an infinite amount of distinct values. Although they have an infinitely small spacing between them, they are still distinct. If the probability would have been larger than 0, then all these values would have had this probability. Still it is required by the probability axioms to have a total probability of 1. Therefore it is not possible with an infinite amount of non-zero probabilities to satisfy the probability axiom, unless the probability is infinitely close to 0.

### Properties
From the definitions of the probability functions and the probability axioms, several consequences can be determined.
#### Cumulative distribution function
For the cumulative distribution function (CDF), the following properties can be determined from the probability axioms
<ol>
    <li style="margin-top:10px;"> $0\leq P_X(x) \leq 1$ for all $x$. </li>
    <li style="margin-top:10px;"> $P_X(-\infty) = 0$ and similarly $P_X(\infty) = 1$. </li>
    <li style="margin-top:10px;"> $P_X(x_2) \geq P_X(x_1)$ holds when $x_2\geq x_1$. </li>
    <li style="margin-top:10px;"> It holds that $P_X(x_2) - P_X(x_1) = \Pr[x_1 < X \leq x_2]$ for $x_2 > x_1$. </li>
</ol>
In short, the CDF is bounded between 0 and 1, because the total probability cannot be negative nor larger than 1 by the probability axioms. The range of $X$ that is upper-bounded by $-\infty$ is a null set and therefore the probability of an event in the null set is equal to 0. Additionally the range of $X$ that is upper-bounded by $\infty$ is the entire range and therefore the probability equals 1. The CDF is defined as the cumulative probability and is therefore never decreasing for consecutive numbers. Lastly, the CDF is defined over the interval from $-\infty$ to an upper-bound. Subtracting two cumulative distribution functions will result into the cumulative probability over an interval that is now also lower-bounded.


#### Probability mass function
For the probability function the following properties can be determined from the probability axioms
<ol>
    <li style="margin-top:10px;"> If $x$ is not in the range of $X$ then $p_X(x)=0$. </li>
    <li style="margin-top:10px;"> $0 \leq p_X(x) \leq 1$ for all $x$. </li>
    <li style="margin-top:10px;"> $\sum_x p_X(x) = 1$. </li>
</ol>
The first property states that the probability of observing an outcome that cannot be observed equals 0. The second and third property have already been defined by the probability axioms.


#### Probability density function
Similarly to the probability mass function, properties of the probability density function can be determined as
<ol>
    <li style="margin-top:10px;"> It holds that $p_X(x) \geq 0$ for all $x$. </li>
    <li style="margin-top:10px;"> By definition $P_X(x) = \int_{-\infty}^x p_X(x)\mathrm{d}x$. </li>
    <li style="margin-top:10px;"> It holds that $\int_{\infty}^\infty p_X(x)\mathrm{d}x = 1$. </li>
</ol>
The first and last properties are direct consequences of the probability axioms. Please note that now there is no upper-bound to the value of $p_X(x)$, since this function returns the probability density and not the true probability. The second property is just a repetition of the definition of the cumulative distribution function.


<br></br>

## Characteristics of random variables
### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/Lz3REvSebmc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>



A distribution of a random variable can be characterized in multiple ways. In order to explain these characteristics, an analogy is drawn with statistical properties.

### A statisticians approach
The statistics of a dataset are the characteristics of a set of observations, usually without knowing the underlying probabilistic model. Suppose a set of $m$ observations is defined as
\begin{equation}
    \mathcal{X} = \\{x_1, x_2, \ldots, x_m\\}.
\end{equation}

The <i>average</i> of this set can be determined by summing over all values and dividing by the amount of values through
\begin{equation}
    \text{average}(\mathcal{X}) = \frac{\sum\_{i=1}^{m}x_i}{m}.
\end{equation}

The <i>median</i> is another statistic to characterize a set of observations. The median is defined as the value in the middle of the ordered data set. After ordering the data set, left and right of the median there should be an equal amount of observation. In case that the data set has an even number of observations, usually the average of the two observations in the middle is taken.

The <i>mode</i> of a data set is the observation with the highest number of occurrences. If multiple observations occur both as often, then both observations are the mode of data set and the data set is then called multimodal.


#### Example
Suppose the students of the statistical signal processing course have made the final exam and the final course grades are available. A subset of all grades could consist of the following grades
\begin{equation}
    \\{ 8, 5, 6, 2, 7, 9, 10, 2, 7, 5, 6, 7\\}.
\end{equation}
From this set the average value can be computed as 6.17. The median can be determined after ordering the set as
\begin{equation}
    \\{ 2, 2, 5, 5, 6, \textbf{6}, \textbf{7}, 7, 7, 8, 9, 10\\}.
\end{equation}
The middle values are 6 and 7, because there are an even amount of observations. Therefore the median can be determined as 6.5. From this set the mode can be determined as 7, since this observation occurs 3 times, whereas all other grades occur only once or twice.

### Expected value
From this statistical approach, the summary statistics are determined from a set of realizations (observed data). Suppose now that the realizations are unknown, but the underlying distribution is known. From this it is still possible to determine its characteristics. However, they are called differently and require a different method to calculate them.

The <i>expected value</i> (or expectation) of a distribution can be regarded as the average value of the distribution for an infinite amount of observations, or as the center of gravity of a distribution. The expected value of a random variable is denoted by the $\mathbb{E}[\cdot]$ operator or by $\mu\_{\cdot}$ and is given for a discrete random variable $X$ as
\begin{equation}
    \mathbb{E}[X] = \mu\_{X} = \sum\_{x\in S\_X}x \cdot p\_{X}(x)
\end{equation}
and for a continuous random variable $X$ as
\begin{equation}
    \mathbb{E}[X] = \mu_{X} = \int\_{-\infty}^\infty x\cdot p_X(x) \mathrm{d}x.
\end{equation}
The expected value of a function $g(X)$ of a random variable $X$ can be determined as
\begin{equation}\label{eq:expected_function}
    \mathbb{E}[g(X)] =
    \begin{cases}
        \displaystyle \sum\_{x \in S\_X}g(x) \cdot p\_{X}(x), & \text{if $X$ is discrete}\newline
        \displaystyle \int\_{-\infty}^\infty g(x)\cdot p_X(x) \mathrm{d}x. & \text{if $X$ is continuous}
    \end{cases}
\end{equation}

### Variance
The variance of a distribution is a measure of the spread of the distribution. A large variance means that the distribution is spread out significantly, whereas a small variance means that the distribution is compact. This variance can be determined for a discrete random variable $X$ as
\begin{equation}
    \text{Var}[X] = \sigma_X^2 = \mathbb{E}[(X-\mu\_X)^2] = \sum\_{x\in S\_X}(x-\mu\_X)^2 \cdot p_{X}(x)
\end{equation}
and for a continuous random variable $X$ as
\begin{equation}
    \text{Var}[X] = \sigma_X^2 = \mathbb{E}[(X-\mu_X)^2] = \int\_{-\infty}^\infty (x-\mu_X)^2\cdot p_X(x) \mathrm{d}x.
\end{equation}

In some cases it is more convenient to rewrite the variance through
\begin{equation}\label{eq:var_rewrite}
    \begin{split}
        \text{Var}[X]
        &= \mathbb{E}[(X-\mu_X)^2] \newline
        &= \mathbb{E}[X^2 - 2\mu_X X + \mu_X^2] \newline
        &= \mathbb{E}[X^2] - 2\mu_X\mathbb{E}[X] + \mu_X^2 \newline
        &= \mathbb{E}[X^2] -2\mu_X^2 + \mu_X^2 \newline
        &= \mathbb{E}[X^2] - \mu_X^2
    \end{split}
\end{equation}
The calculation rules concerning the expectation operator will be described later on.

#### Standard deviation
The standard deviation is also a commonly used characteristic of a probability distribution and simply equals the square root of the variance as
\begin{equation}
    \text{Std}[X] = \sigma_X = \sqrt{\text{Var}[X]}.
\end{equation}

### Moments
As said before the expected value defines the center of gravity of a distribution and the variance is a measure of its spread. Besides these characteristics there are other characteristics such as the skewness (degree of asymmetry) and the kurtosis (how the tails of the distribution are shaped). The characteristics are represented in Fig. 2. The characteristics are a specific case of a more generalized concept called <i>moments</i>. The $m^{th}$ moment of a discrete and continuous random variable is defined as
\begin{equation}
    \mathbb{E}[X^m] =
    \begin{cases}
        \displaystyle \sum\_{x \in S_X} x^m p_X(x),             &\text{if $X$ is discrete} \newline
        \displaystyle \int\_{-\infty}^{\infty} x^m p_X(x) \mathrm{d}x.   &\text{if $X$ is continuous}
    \end{cases}
\end{equation}
It can be seen that the first order moment of a random variable is equal to its mean. Similarly, the <i>central moment</i> can be found by normalizing the random variables with their first order moments, i.e. by subtracting the mean, as
\begin{equation}
    \mathbb{E}[(X-\mu_X)^m] =
    \begin{cases}
        \displaystyle \sum\_{x \in S_X} (x-\mu_X)^m p_X(x),             &\text{if $X$ is discrete} \newline
        \displaystyle \int\_{-\infty}^{\infty} (x-\mu_X)^m p_X(x) \mathrm{d}x.   &\text{if $X$ is continuous}
    \end{cases}
\end{equation}
From this the variance can be found as the second order central moment. Finally the $m^{th}$ <i>normalized moment</i> is determined as the central moment divided by the $m^{th}$ order of the standard deviation as
\begin{equation}
    \frac{\mathbb{E}[(X-\mu_X)^m]}{\sigma^m} =
    \begin{cases}
        \displaystyle \frac{1}{\sigma^m}\sum\_{x \in S_X} (x-\mu_X)^m p_X(x),             &\text{if $X$ is discrete} \newline
        \displaystyle \frac{1}{\sigma^m}\int\_{-\infty}^{\infty} (x-\mu_X)^m p_X(x) \mathrm{d}x.   &\text{if $X$ is continuous}
    \end{cases}
\end{equation}
Skewness is defined as the third normalized moment and kurtosis as the fourth normalized moment.


<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/moments.svg"
      alt="Visualization of common distribution characteristics. The distribution in blue has a larger $m^{th}$ moment than the distribution in red."
    />
    <figcaption class="numbered">
      Visualization of common distribution characteristics. The distribution in blue has a larger $m^{th}$ moment than the distribution in red.
    </figcaption>
  </figure>
</div>
