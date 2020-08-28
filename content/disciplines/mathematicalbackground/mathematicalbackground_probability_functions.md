+++
title = "Functions and pairs of random variables"

# date = {{ .Date }}
lastmod = 2019-12-30

draft = false       # Is this a draft? true/false
toc = true         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Functions and pairs of random variables"
  parent = "Probability and random variables"
  weight = 53

+++

<!-- hide footnotes in plaintext, because they are added in the equations -->
<style>
  a.footnote-ref {display: none;}
  a.footnote-backref {display: none;}
</style>

## Functions of random variables
It can be possible that a signal is generated under a certain probability distribution, after which the signal is manipulated. The probability distribution that follows from this transformation is usually difficult to determine, however, the expected value and variance are usually easier to compute.

### Linear combinations of random variables
One common category of these transformation consists of the linear combinations of a continuous random variable $X$, with mean $\mu_X$ and variance $\sigma_X^2$. Suppose that the random variable $Y$ is a linear combination of $X$ defined by
\begin{equation}
    Y = aX+b.
\end{equation}
The mean of the random variable $Y$ can be determined as
\begin{equation}
    \begin{split}
        \mathbb{E}[Y]
        &= \mathbb{E}[aX + b] \newline
        &= \int\_{-\infty}^{\infty}(ax+b)\cdot p_X(x)\mathrm{d}x \newline
        &= a \int\_{-\infty}^{\infty} x\cdot p_X(x) \mathrm{d}x + b \int\_{-\infty}^{\infty}p_X(x)\mathrm{d}x \newline
        &= a\cdot \mathbb{E}[X] + b = a\cdot \mu_X + b
    \end{split}
\end{equation}
From this we have now obtained the rules that allowed us to rewrite the variance in an earlier subsection.
Similarly the variance of $Y$ can be determined using the previous result as
\begin{equation}
    \begin{split}
        \text{Var}[Y]
        &= \mathbb{E}[(Y-\mu\_Y)^2] \newline
        &= \mathbb{E}[(aX+b - (a\cdot \mu\_X + b))^2] \newline
        &= \mathbb{E}[a^2 (X-\mu_X)^2] \newline
        &= \int\_{-\infty}^{\infty}a^2(x-\mu\_X)^2\cdot p_X(x)\mathrm{d}x \newline
        &= a^2\int\_{-\infty}^{\infty}(x-\mu\_X)^2\cdot p_X(x)\mathrm{d}x \newline
        &= a^2 \text{Var}[X]
    \end{split}
\end{equation}
A very similar derivation also holds for discrete random variables. Please note that the variable $b$ did not have an effect on the variance of $Y$. Intuitively this makes sense since the variance is a measure of the spread of a variable. By adding a constant the spread of the probability distribution will not change.


### Continuous elementary functions
Sometimes it can be useful to more flexibly define probability distributions in the continuous domain. Up until now we were limited by the given families of distributions, but one might for example want to alter these distributions slightly according to the situation. Suppose there is a random variable $X$ that behaves as a uniform distribution for $X<0$ and an exponential distribution for $X\geq0$. How can we describe this distribution mathematically? For this the delta pulse function and the unit step function need to be introduced.  

#### Dirac delta pulse function
The Dirac delta pulse function is a function that only exists for one single value on its domain. The value at this point is undefined, but it guarantees that the integral over its domain equals 1. The dirac delta pulse is therefore defined as
\begin{equation}
    \delta(x) =
    \begin{cases}
        +\infty, &\text{for $x=0$} \newline
        0, &\text{for $x\neq 0$}
    \end{cases}
\end{equation}
under the constraint
\begin{equation}
    \int\_{-\infty}^{\infty}\delta(x)\mathrm{d}x = \int\_{0^-}^{0^+}\delta(x)\mathrm{d}x = 1,
\end{equation}
where $0^-$ and $0^+$ are the limits towards $0$ from below and above respectively.

#### Sifting property
The definition of the Dirac delta pulse function allows us to extract values from a function by simply multiplying with the delta pulse and integrating over the domain. This delta pulse can be shifted on its domain, allowing for the extraction at any point on the function. This process can be regarded as sampling. This is known as the sifting property and is defined as
\begin{equation}
    \int\_{-\infty}^{\infty}g(x)\delta(x-x_0)\mathrm{d}x = \int\_{x_0^-}^{x_0^+}g(x)\delta(x-x_0)\mathrm{d}x = g(x_0).
\end{equation}


#### Discrete to continuous probability functions
With the introduction of the Dirac delta pulse, we are now also capable of transforming a discrete probability mass function into a continuous probability density distribution. Each of the values of the probability mass function can be represented as a delta pulse multiplied with the corresponding value. As an example, the probability mass function of the discrete Bernoulli(p) distribution can be written as a probability density function as
\begin{equation}
    p_X(x) = (1-p)\cdot \delta(x) + p\cdot \delta(x-1).
\end{equation}
Similarly all other discrete probability mass functions can be rewritten as continuous probability density functions. For more details about the Bernoulli distribution, check the section  <a href="../mathematicalbackground_probability_families">Families of random variables</a>.

#### Unit step function
It is also possible that a probability density function is zero up to a threshold $x_0$, after which it nicely follows a known distribution $p_X(x)$. The mathematical description of this piece-wise probability density function can be determined using the unit step function, which is defined as
\begin{equation}
    u(x) =
    \begin{cases}
    1,      &\text{for } x\geq 0 \newline
    0.      &\text{for } x < 0
    \end{cases}
\end{equation}
This function allows us to put a known probability density function $p\_X(x)$ to zero up to a certain threshold $x\_0$, whilst retaining the other part of the function. A generalization of such a new probability density function $p\_{X1}(x)$ can be written as
\begin{equation}
    p\_{X1}(x) = c\cdot p\_X(x)\cdot u(x-x\_0),
\end{equation}
where $c$ is a constant that is required to satisfy the total probability axiom ($\int\_{-\infty}^{\infty} p\_{X1}(x)\mathrm{d}x = 1$).

### Mixed random variables
When the probability density function of a random variable consists of a combination of both delta pulses as probability density functions, it can be regarded as a mixed random variable. An example of a random variable is given in the following example.

#### Example
Suppose we are monitoring the duration of phone calls. The measured duration $x$ in minutes can be regarded as a continuous random variable $X$, which is distributed as an exponential random variable with rate parameter $\lambda=1$. This can be written as $X\sim \text{Exp}(\lambda=1)$ with probability density function
\begin{equation}
    p_X(x) =
    \begin{cases}
        e^{-x},     &\text{for } x\geq 0 \newline
        0.          &\text{for } x < 0
    \end{cases}
\end{equation}
The service provider decides for simplicity to round all phone calls lasting less than 60 seconds to exactly 1 minute. This administrative duration $y$ in minutes can be represented by a mixed random variable $Y$. The administrative duration can be mathematically determined as
\begin{equation}
    y =
    \begin{cases}
        1,          & \text{for }x < 1 \newline
        x.          & \text{for }x \geq 1
    \end{cases}
\end{equation}
Let us now derive the probability density function of $Y$. In order to do so, the derivation is split for the cases $Y<1$, $Y=1$ and $Y>1$.

We can easily see that $p_Y(y) = 0$ for $y<1$, because the duration is always rounded to at least 1 minute.

For $Y=1$ a <i>true probability</i> is involved, since there is a non-zero probability that the administrative duration is exactly 1 minute. Because the integral of the probability density function should return a non-zero value at $y=1$ when integrating $\int\_{1^-}^{1^+}p\_Y(y)\mathrm{d}y$, a Dirac delta pulse should be located at $y=1$ in order to make sure that the integral returns the true probability. This delta pulse should be multiplied with the probability of the occurrence of this event. This probability can be determined as
\begin{equation}
    \Pr[Y=1] = \Pr[X<1] = \int_{-\infty}^{1}p_X(x)\mathrm{d}x = \int_0^{1}e^{-x}\mathrm{d}x = \left[ -e^{-x}\right]^1_0 = 1-e^{-1}.
\end{equation}
For $Y>1$ the probability density function of $Y$ simply follows the exponential distribution of $X$. In order to cope with this partial domain, $p_X(x)$ needs to be multiplied with the shifted unit step function.

So to conclude the probability density function of $Y$ can be written as
\begin{equation}
    p\_Y(y) = (1-e^{-1})\cdot\delta(y-1) + e^{-y}\cdot u(y-1).
\end{equation}



<br></br>

## Pairs of random variables

So far this module has only focused on events that produce a single outcome and therefore can only have a single random variable. However, it is also possible for an event to return multiple random variables.
<br></br>

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%"; height="100%";  src="https://www.youtube.com/embed/cijeXJYNttM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>
<br></br>


#### Example
Suppose we have an experiment in which we throw 2 dices consecutively and we collect the total amount of eyes after the first and second dice are thrown. Assuming normal dices, the total amount of eyes observed after the first throw should be an integer between 1 and 6. But how can we now describe the total amount of eyes after throwing the second dice? It will be clear that this second observation will be between 2 and 12 eyes. However, we do need to keep in mind that the second observation depends greatly on the first observation. It is for example impossible to first observe a total of 5 eyes after throwing the first dice and then to observe a total of 4 eyes after throwing the second dice.

### Joint random variables
Through the previous example it is clear that there is a need to combine multiple random variables into a single function in order to draw conclusions about observations and their probabilities. Multiple random variables that are all associated with an event are called <i>joint random variables</i>. These random variables are usually denoted with different capital letters (e.g. $X$ and $Y$). The theory that follows, holds for every number of joint random variables, however, for simplicity this reader will only discuss events that produce 2 joint random variables.

#### Joint cumulative distribution function
In order to describe the probabilities that are associated with the observations ($x$, $y$), we will introduce the <i>joint cumulative distribution function</i>, which is a variant of the cumulative distribution function. This joint cumulative distribution function is defined for the random variables $X$ and $Y$ as
\begin{equation}
    P_{X,Y}(x,y) = \Pr[X\leq x, Y\leq y],
\end{equation}
where the comma in the probability operator indicates that <i>both</i> conditions need to hold.

#### Joint probability axioms
Similarly to the single random variable case, axioms can be determined for the joint cumulative distribution function. These axioms include
<ol>
    <li style="margin-top:10px;"> It holds that $0\leq P_{X,Y}(x,y)\leq 1$. </li>
    <li style="margin-top:10px;"> It holds that $P_{X,Y}(\infty, \infty) = 1$ and that $P_{X,Y}(x, -\infty) = P_{X,Y}(-\infty, y) = 0$. </li>
    <li style="margin-top:10px;"> It holds that $P_X(x) = P_{X,Y}(x,\infty)$ and similarly $P_Y(y) = P_{X,Y}(\infty,y)$. </li>
    <li style="margin-top:10px;"> The function is non-decreasing (i.e. for $x\leq x_0$ and $y \leq y_0$ it holds $P_{X,Y}(x,y)\leq P_{X,Y}(x_0, y_0)$). </li>
</ol>
The first axiom is a consequence of the total probability axiom, where a probability cannot be negative nor larger than 1.

A total probability of 1 only occurs when both $X\leq x$ and $Y\leq y$ are always satisfied, which is the case for $P_{X,Y}(\infty, \infty)$. Similarly, there is by definition no event where $x\leq -\infty$ or $y\leq -\infty$ and therefore this (cumulative) probability is always 0.

When one of the conditions $X\leq x$ and $Y\leq y$ is always satisfied, the cumulative distribution does not depend on that variable anymore and therefore that variable can be removed from the equation, leaving a distribution that now depends on one single random variable. This process is called marginalization and will be discussed later on.

Finally as seen previously the cumulative distribution is a sum or integral over an ever-increasing domain with non-negative values, leading to a non-decreasing function.

#### Joint probability density function
The previous definition of the joint cumulative distribution function both holds for continuous as discrete random variables. For the continuous random variables the <i>joint probability density function</i> can be defined through the relationship
\begin{equation}
    \int\_{-\infty}^{x}\int_{-\infty}^{y} p\_{X,Y}(u,v)\ \mathrm{d}u\ \mathrm{d}v = P\_{X,Y}(x,y)
\end{equation}
and can be calculated from the joint cumulative distribution function as
\begin{equation}
    p\_{X,Y}(x,y) = \frac{\partial^2 P\_{X,Y}(x,y)}{\partial x \partial y}.
\end{equation}

#### Joint probability mass function
In the case of discrete random variables, the <i>joint probability mass function</i> can be defined explicitly as
\begin{equation}
    p\_{X,Y}(x,y) = \Pr[X=x, Y=y],
\end{equation}
because the values that the function returns are true probabilities.

#### Expected value
The expected value of the joint random variables can be determined similarly to the single variable case. Given a new random variable $W$, which is an arbitrary function of the random variable $X$ and $Y$ through $W=g(X,Y)$, the expected value of $W$ can be determined as
\begin{equation}
    \mathbb{E}[W] = \sum\_{x\in S_X}\sum\_{y\in S_Y}g(x,y)\cdot p\_{X,Y}(x,y)
\end{equation}
in the case of discrete random variables and as
\begin{equation}
    \mathbb{E}[W] = \int\_{-\infty}^\infty \int\_{-\infty}^{\infty} g(x,y)\cdot p\_{X,Y}(x,y) \ \mathrm{d}x\ \mathrm{d}y
\end{equation}
in the case of continuous random variables.


### Marginalization
In many engineering problems you are only interested in the outcome of one random variable. When a joint probability function is available it is possible to <i>marginalize</i> over all other random variables except for the one random variable in which you are interested, leaving you with the probability function of just that random variable. This marginalization is performed for discrete random variables through
\begin{equation}
    p_X(x) = \sum\_{y\in S_Y} p\_{X,Y}(x,y)
\end{equation}
and for continuous random variables through
\begin{equation}
    p_X(x) = \int\_{-\infty}^\infty p\_{X,Y}(x,y) \mathrm{d} y.
\end{equation}
This operation can be understood when viewing the summation or integration as "taking all possibilities of all other random variables into account". The proof for the continuous random variables follows
\begin{equation}
    \begin{split}
        p\_X(x)
        &= \frac{\partial P\_{X}(x)}{\partial x}, \newline
        &= \frac{\partial}{\partial x} \Pr[X\leq x], \newline
        &= \frac{\partial}{\partial x} \Pr[X\leq x, Y\leq \infty], \newline
        &= \frac{\partial}{\partial x} \int\_{-\infty}^{x}\left(\int\_{-\infty}^{\infty}p\_{X,Y}(v,u)\mathrm{d}u\right)\mathrm{d}v, \newline
        &= \int\_{-\infty}^\infty p\_{X,Y}(u,v) \mathrm{d} v.
    \end{split}
\end{equation}
A similar proof can be found for the marginalization of discrete random variables.

### Conditional probabilities
When considering events with multiple outcomes we might be able to deduce one outcome from another. Take the example of the two dices. If we know that the first dice rolls 5 eyes then we automatically know that the total amount of eyes after the second throw is 6 up to 11 with equal probability. Similarly we may deduce with 100% certainty that the first throw should have given 6 eyes, when 12 eyes are observed after the second throw.

This line of reasoning is an example of <i>conditional probability</i>. Conditional probability involves the probability of some event when another event is observed. In the reader on probability theory, the definition of conditional probability was given and explained. If this definition is combined with random variables, two separate cases can be identified.

First, it is possible to determine the conditional probability function, which is the probability mass function or probability density function of observing outcomes $(x,y)$, when it is known that the outcomes can be found somewhere in an event set $B$, which is a subset of the sample space $\mathcal{S}$. When the initial joint probability function is given by $p\_{X,Y}(x,y)$, the conditional probability function of $X$ and $Y$ given $B$ (i.e. $X,Y|B$) can be determined as
\begin{equation}
    p\_{X,Y|B}(x,y) =
    \begin{cases}
        \frac{p\_{X,Y}(x,y)}{\Pr[B]},          &\text{when } (x,y)\in B \newline
        0.                  &\text{otherwise}
    \end{cases}
\end{equation}
This operation can be regarded as assigning all outcomes outside set $B$ to zero and normalizing the remaining function to satisfy the total probability axiom.

Secondly it is also possible that one outcome is observed and we would like to find the probability function of the other random variables. Let us now suppose that the random variable $Y$ is observed as $y$ and we are interested in finding the conditional probability function of $X$, which is $p\_{X|Y}(x|y)$. For discrete random variables this conditional probability mass function can be determined as
\begin{equation}
    p\_{X|Y}(x|y) = \Pr[X=x|Y=y] = \frac{\Pr[X=x, Y=y]}{\Pr[Y=y]} = \frac{p\_{X,Y}(x,y)}{p\_Y(y)}.
\end{equation}
Keep in mind that the marginalized probability mass function $p_Y(y)$ can be calculated using marginalization. Similarly to the derivation for the discrete random variables, the conditional probability density function of continuous random variables can be determined as
\begin{equation}
    p\_{X|Y}(x|y) = \frac{p\_{X,Y}(x,y)}{p\_Y(y)} = \frac{p\_{X,Y}(x,y)}{\int\_{-\infty}^{\infty} p\_{X,Y}(x,y) \mathrm{d}x}
\end{equation}

#### Example
Suppose we are given the joint probability density function
\begin{equation}
    p\_{X,Y}(x,y) =
    \begin{cases}
        Ce^{-x},        &\text{for } x\geq 0 \text{ and } -x\geq y \geq x \newline
        0,              &\text{otherwise}
    \end{cases}
\end{equation}
where $C$ is a constant to be determined. Let us now derive the value of $C$, the marginal probability density functions $p\_X(x)$ and $p\_Y(y)$ and the conditional probability density function $p\_{Y|X}(y|x)$.

In order to calculate $C$ we need to make use of the total probability axiom, which is given as
\begin{equation}
    \int\_{-\infty}^\infty \int\_{-\infty}^\infty p\_{X,Y}(x,y)\ \mathrm{d}x\ \mathrm{d}y = 1
\end{equation}
for the joint random variables case. If we substitute the given joint probability density function with the given constraints we find
\begin{equation}
    \begin{split}
        \int\_0^\infty \int\_{-x}^x Ce^{-x} \ \mathrm{d}y\ \mathrm{d}x
        &= C \int\_0^\infty e^{-x}\int\_{-x}^x  1\ \mathrm{d}y\ \mathrm{d}x
        = C \int\_0^\infty e^{-x}\left[y\right]\_{-x}^x \ \mathrm{d}x, \newline
        &= 2C \int\_0^\infty x e^{-x}\ \mathrm{d}x
        \overset{\href{./#fn:1}{1}}{=} 2C\left[ -xe^{-x}\right]\_0^\infty - 2C\int_0^\infty -e^{- x} \mathrm{d}x, \newline
        &= -2C\left[ xe^{- x}\right]\_0^\infty  -2C\left[ e^{- x}\right]\_0^\infty, \newline
        &\overset{\href{./#fn:2}{2}}{=} -2C(0-0) -2C(0-1) = 2C = 1.
    \end{split}
\end{equation}
From this follows that $C=\frac{1}{2}$.


[^1][^2]
[^1]: Integration by parts: $$ \int_a^b f(x)g'(x) \mathrm{d}x = \left[ f(x)g(x)\right]\_a^b - \int\_a^b f'(x)g(x) \mathrm{d}x$$
[^2]: Growth property of exponentials: $$ \lim_{x\to \infty} x^ae^{-x} = 0 $$

In order to calculate $p\_X(x)$ we will marginalize $p\_{X,Y}(x,y)$ over $Y$ as
\begin{equation}
    \begin{split}
        \int\_{-\infty}^\infty p\_{X,Y}(x,y)\mathrm{d}y
        &= \int\_{-x}^x Ce^{-x} \mathrm{d}{y}
        = Ce^{-x}\int\_{-x}^x1\mathrm{d}y = 2Cxe^{-x}.
    \end{split}
\end{equation}
When substituting the value of $C$ and considering that the function only exists for $x\geq 0$, the marginal probability density function can be determined as
\begin{equation}
    p\_X(x) =
    \begin{cases}
        xe^{-x},        &\text{for }x\geq 0 \newline
        0.              &\text{otherwise}
    \end{cases}
\end{equation}

Similarly we can find the marginal probability density function $p_Y(y)$. One might say that the marginalization integral has a lower-bound for $x$, namely $x\geq 0$. However, this is not entirely correct. When rewriting the constraint $-x\geq y \geq x$ as $x\geq |y|$ it becomes clear that $x$ is not bounded by $0$, but by $|y|$. The marginal probability density function is not bounded on $y$ by a constant and can therefore be written as
\begin{equation}
    \begin{split}
        p\_Y(y)
        &= \int\_{|y|}^\infty Ce^{-x} \mathrm{d}x
        = C [-e^{-x}]\_{|y|}^\infty
        = C(-0+e^{-|y|}) = \frac{1}{2}e^{-|y|}.
    \end{split}
\end{equation}

Now finally we can use our previous results in order to determine the conditional probability density function as
\begin{equation}
    \begin{split}
        p\_{Y|X}(y|x)
        &= \frac{p\_{X,Y}(x,y)}{p\_X(x)} \newline
        &=
        \begin{cases}
            \frac{\frac{1}{2}e^{-x}}{xe^{-x}},      &\text{for } x\geq 0 \text{ and } -x\geq y \geq x \newline
            0,                                      &\text{otherwise}
        \end{cases}\newline
        &=
        \begin{cases}
            \frac{1}{2x},       &\text{for } x\geq 0 \text{ and } -x\geq y \geq x \newline
            0.                  &\text{otherwise}
        \end{cases}
    \end{split}
\end{equation}
One could apply the axiom of total probability to all marginalized and conditional probability density functions over their domain and should note that the axiom is satisfied.

<br></br>

## Central limit theorem

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%"; height="100%";  src="https://www.youtube.com/embed/3KASsi7eyYE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


<br></br>



We have briefly discussed what happens with the signal statistics, especially the mean and variance, when a random variable is linearly transformed.
Now let us focus on the specific situation where we take the sum of $N$ independent continuous random variables. We will define a random variable $Y$ as
\begin{equation}
    Y = \frac{X_1 + X_2 + \ldots + X_N}{N}
\end{equation}
and have a look at what the probability density function of $Y$ looks like.

In Fig. 1,  100000 samples are generated  from three different probability distributions and the resulting histograms are plotted. This is repeated for an increasing number $N$, and the histograms are plotted after averaging $N$ similarly generated sets of data. It can be noted that after averaging multiple realizations of a random variable generated from the same (arbitrary) distribution, the distribution of the averaged random variables converges to a Gaussian distribution. This result is known as the <i>central limit theorem (CLT)</i>.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/centrallimittheorem.svg"
      alt="Visualisation of the central limit theorem."
    />
    <figcaption class="numbered">
      Demonstration of the CLT for three different probability distributions, i.e. $\mathcal{U}(0,5)$, $\mathcal{U}(-10,10)$ and Exp$(\lambda = 1)$, where $N$ sets of 100000 realizations are averaged and the new distributions of the averaged 100000 samples are shown for different values of $N$. A Gaussian function is fitted over the distributions and it can be seen that after averaging over more realizations, the new distribution will converge to the Gaussian distribution.
    </figcaption>
  </figure>
</div>

 The formal definition is given as:

{{% alert note %}}
Let $X_1,X_2,...,X_n$ be a set of $N$ independent identically-distributed (i.i.d) random variables and each $X_i$ has an arbitrary probability distribution $p(x_1,x_2, ..., x_n)$ with finite mean $\mu_i=\mu$ and finite standard deviation $\sigma_i=\sigma$. If the sample size $N$ is “sufficiently large”, then the CDF of the sum converges to a Gaussian CDF.
{{% /alert %}}

In simple words, the CLT states that the normalized sum of a sufficient number of i.i.d. random variables tends to a Gaussian distribution. It is also possible to predict the mean and the variance of the Gaussian probability density function after a sufficiently large set of $N$ random variables has been summed. The minimum value of $N$ for the CLT approximation to be valid depends on the distribution of the individual random variables.

Under certain conditions, the CLT can be extended for the sum of random variables that are independent but not necessarily identically distributed (i.e., Lyapunov condition). In both cases, the mean or expected value of the approximate Gaussian probability density function can be determined as
\begin{equation}
    \mathrm{E}[Y] = \frac{1}{N} \sum_{i=1}^N \mathrm{E}[X_i],
\end{equation}
which is simply the average value of all individual expected values. Similarly the variance can be determined as
\begin{equation}
    \text{Var}[Y] = \sigma_Y^2 = \frac{1}{N^2} \sum_{i=1}^N \sigma^2_{X_i} = \frac{1}{N^2} \sum_{i=1}^N \text{Var}[X_i].
\end{equation}

Similarly the random variable $Z$, which is the sum over normalized random variables, can be defined as
\begin{equation}
    Z = \frac{1}{N}\sum_{i=1}^N \frac{X_i-\mathrm{E}[X_i]}{\sigma_{X_i}}.
\end{equation}
Through the central limit theorem it follows that the probability density function of the random variable $Z$ converges to the normalized Gaussian distribution $\mathcal{N}(0,1)$.
