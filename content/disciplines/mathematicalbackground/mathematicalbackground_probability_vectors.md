+++
title = "Random vectors"            # Title of page as displayed on page

# date = {{ .Date }}
lastmod = 2020-01-04                # Last modification date

draft = false                       # Is this a draft? true/false
toc = true                          # Show table of contents? true/false
type = "docs"                       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]       # Do not modify
  name = "Random vectors"           
  parent = "Probability and random variables"
  weight = 55

+++

<style>
  a.footnote-ref {display: none;}
  a.footnote-backref {display: none;}
</style>

## Introduction
Previously we saw how we could grasp this notion of uncertainty in probability functions and we saw what happened when our outcome was conditioned. Finally, a brief discussion was provided for the case when multiple random variables were involved. In these examples, only the situation where we had 2 random variables was discussed. This module will generalize this theory for multiple random variables. In this case an outcome of an experiment comprises $N$ observed quantities. An example of such an observation is a noisy electroencephalography (EEG) measurement, which resembles the electrical activity of the brain and is measured over several channels.

<br></br>

### Screencast video [⯈]

<div class="video-container">
<iframe width="100%"; height="100%";  src="https://www.youtube.com/embed/7WYMXxwwMPg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


<br></br>

## Multivariate joint probability distributions
Let us denote each of these measured quantities by the random variable $X_n$, where $n$ ranges from $1$ up to $N$. Using this definition, the <i>multivariate</i> (meaning that multiple variables are involved) joint probability functions can be introduced. For notation purposes, all random variables $X_n$ can be grouped in a <i>random vector</i> ${\bf{X}} = [X_1, X_2,\ldots, X_N]^\top$, where the $\cdot^\top$ operator denotes the transpose, turning this row vector into a column vector. The bold capital letter distinguishes the random vector containing multiple random variables from a single random variable. Similarly, a specific realization of this random vector can be written in lower-case as ${\bf{x}} = [x_1, x_2, \ldots, x_N]^\top$.

<h3> Multivariate joint cumulative distribution function </h3>
The <i>multivariate joint cumulative distribution function</i> of the random vector $\bf{X}$ containing random variables $X_1, X_2, \ldots, X_N$ is defined as
\begin{equation}
    P_{\bf{X}}({\bf{x}})
    = P_{X_1,\ldots,X_N}(x_1, \ldots, x_N)
    = \Pr[X_1\leq x_1, \ldots, X_N\leq x_N].
\end{equation}
This definition holds for both discrete as continuous random variables.

<h3> Multivariate joint probability mass function </h3>
The <i>multivariate joint probability mass function</i> of the random vector $\bf{X}$ containing discrete random variables $X_1, X_2, \ldots, X_N$ is similarly defined as
\begin{equation}
    p_{\bf{X}}({\bf{x}})
    = p_{X_1,\ldots,X_N}(x_1, \ldots, x_N)
    = \Pr[X_1= x_1, \ldots, X_N= x_N].
\end{equation}

<h3> Multivariate joint probability density function </h3>
The <i>multivariate joint probability density function</i> of the random vector $\bf{X}$ containing continuous random variables $X_1, X_2, \ldots, X_N$ is defined from the multivariate joint cumulative distribution function as
\begin{equation}\label{eq:mjpdf}
    p_{\bf{X}}({\bf{x}})
    = p_{X_1,\ldots,X_N}(x_1, \ldots, x_N)
    = \frac{\partial^N P_{X_1,\ldots,X_N}(x_1, \ldots, x_N)}{\partial x_1 \ldots \partial x_N}.
\end{equation}


### Generalized probability axioms for multivariate joint distributions
From these definitions several multivariate joint probability axioms can be determined, which are similar to the case of two random variables as discussed in the last reader.

<ol>
    <li style="margin-top:10px;"> It holds that $p_{\bf{X}}({\bf{x}}) \geq 0$, where $\bf{X}$ is a continuous or discrete random vector. </li>
    <li style="margin-top:10px;"> From the multivariate joint probability density function it follows that $$P_{X_1,\ldots,X_N}(x_1,\ldots,x_N) = \int_{-\infty}^{x_1} \cdots \int_{-\infty}^{x_N} p_{X_1,\ldots,X_N}(x_1,\ldots, x_N)\ \mathrm{d}x_1\ldots \mathrm{d}x_N$$ holds for continuous random vectors. </li>
    <li style="margin-top:10px;"> Through the law of total probability it holds that
        <ol>
            <li> $$ \sum_{x_1\in S_{X_1}} \cdots \sum_{x_N \in S_{X_N}} p_{X_1, \ldots, X_N}(x_1, \ldots, x_N) = 1$$ for discrete random vectors and </li>
            <li> $$ \int_{-\infty}^\infty \cdots \int_{-\infty}^\infty p_{X_1, \ldots, X_N}(x_1, \ldots, x_N) \ \mathrm{d}x_N\ldots \mathrm{d}x_1= 1 $$ for continuous random vectors. </li>
        </ol> </li>
    <li style="margin-top:10px;"> The probability of an event $A$ can be determined as
        <ol>
            <li> $$\Pr[A] = \sum_{{\bf{X}}\in S} p_{X_1, \ldots, X_N}(x_1, \ldots, x_N) $$ for discrete random variables and </li>
            <li> $$\Pr[A] = \underset{A}{\int \cdots \int} p_{X_1, \ldots, X_N}(x_1, \ldots, x_N)\ \mathrm{d}x_1 \ldots \mathrm{d}x_N$$ for continuous random variables. </li>
        </ol> </li>
</ol>

Axiom 1 simply states that a probability (density) cannot be smaller than 0, since no negative probabilities exist by definition. The second axiom is a direct consequence of integrating both sides of the multivariate joint probability density function allowing us to determine the multivariate joint cumulative distribution function from the multivariate joint probability density function. The third axiom is a direct consequence of the law of total probability, where the probability of all events together equal 1. The final axiom tells us to sum or integrate over all possible outcomes of an event $A$ in order to calculate its probability.

<br></br>

## Probability distributions of multiple random vectors
The notation of a random vector allows us to easily include multiple random variables in a single vector. Suppose now that our random vector $\bf{Z}$ contains 2 different types of random variables, where for example each random variable corresponds to a different type of measurement. If we were to distinguish between these type of random variables using two generalized random variables $X_i$ and $Y_i$, the random vector $\bf{Z}$ could be written as ${\bf{Z}} = [X_1, X_2,\ldots, X_N, Y_1, Y_2, \ldots, Y_M]^\top$. If we now were to define the random vectors ${\bf{X}}=[X_1, X_2,\ldots,X_N]^\top$ and ${\bf{Y}}=[Y_1, Y_2,\ldots,Y_M]^\top$, it becomes evident that we could simplify the random vector $\bf{Z}$ as ${\bf{Z}} = [{\bf{X}}^\top, {\bf{Y}}^\top]^\top$.

This shows that it is also possible for joint probability distributions to depend on multiple random vectors, which each can be regarded as a subset of all random variables. This can prove useful in some cases when there is a clear distinction between the subsets and is purely for notation purposes. A probability distribution depending on multiple random vectors can be regarded in all aspects as a probability distribution depending on a single random vector (which is a concatenation of all different random variables). All calculations can be performed by regarding the probability distribution as if it depends on a single (concatenated) random vector. A probability distribution involving multiple random vectors can be written for example as $p_{{\bf{X}},{\bf{Y}}}({\bf{x}},{\bf{y}})$.

<br></br>

## Conditional probabilities
Similarly as in the previous reader, the conditional probability can be determined by normalizing the joint probability with the probability of the conditional event through

\begin{equation}
    p_{{\bf{X}}|B}({\bf{x}}) =
    \begin{cases}
        \frac{p_{{\bf{X}}}({\bf{x}})}{\Pr[B]},          &\text{when } {\bf{x}}\in B \newline
        0.                  &\text{otherwise}
    \end{cases}
\end{equation}

<br></br>

## Marginal probabilities
Because the notation of a random vector $\bf{X}$ is just a shorter notation for the set of random variables $X_1, X_2, \ldots, X_N$, it is possible to calculate the marginalized probability distribution of a subset of random variables. This subset can also just consist of a single random variable. Again this operation is performed through marginalization as discussed in the previous reader. For the case that we are given the probability distribution $p_{\bf{X}}({\bf{x}})$ and we would like to know the marginalized probability distribution $p_{X_2, X_3}(x_2,x_3)$ this can be calculated as
\begin{equation}
    p_{X_2, X_3}(x_2, x_3) = \int_{-\infty}^\infty \cdots \int_{-\infty}^\infty p_{\bf{X}}({\bf{x}}) \ \mathrm{d}x_1 \mathrm{d}x_4 \cdots \mathrm{d}x_N
\end{equation}
for continuous random variables and as
\begin{equation}
    p_{X_2,X_3} = \sum_{x_1\in S_{X_1}} \sum_{x_4\in S_{X_4}}\cdots \sum_{x_N\in S_{X_N}} p_{\bf{X}}({\bf{x}})
\end{equation}
for discrete random variables. Here we have integrated or summed over all possible values of all random variables except for the ones that we are interested in.

<br></br>

## Independence
Independence is a term in probability theory which reflects that the probability of an event $A$ is not changed after observing an event $B$, meaning that $\Pr[A|B] = \Pr[A]$. In other words, the occurrence of an event $B$ has no influence on the probability of an event $A$. Keep in mind that this does not mean that the physical occurrence of event $A$ and $B$ are unrelated, it just means that the probability of the occurrence of event $A$ is unrelated to whether event $B$ occurs or not.

### Independent random variables
This notion of independence can be extended to probability functions. The random variables $X_1,X_2,\ldots, X_N$ can be regarded as independent if and only if the following factorization holds
\begin{equation}
    p_{X_1,X_2,\ldots,X_N}(x_1,x_2,\ldots,x_N) = p_{X_1}(x_1)p_{X_2}(x_2)\ldots p_{X_N}(x_N).
\end{equation}
This equation represents that the total probability can be written a multiplication of the individual probabilities of the random variables. From a probability point of view (not a physical one) we can conclude that the random variables are independent, because the total probability solely depends on all the individual contributions of the random variables.
Random variables that satisfy the independence equation and are distributed under the same probability density function are regarded as <i>independent and identically distributed</i> (IID or iid) random variables. This notion will become important later on when discussing random signals.

### Independent random vectors
It is also possible to extend the definition of independence to random vectors. Two random vectors $\bf{X}$ and $\bf{Y}$ can be regarded as independent if and only if the probability function can be written as
\begin{equation}
    p_{{\bf{X}},{\bf{Y}}}({\bf{x}}, {\bf{y}}) = p_{\bf{X}}({\bf{x}})\ p_{\bf{Y}}({\bf{y}}) .
\end{equation}

<br></br>

## Statistical characterization of random vectors
In the previous reader on random variables, several characteristics were discussed for probability distributions depending on a single random variable, such as the mean, the variance and the moments of a random variable. This section will extend these characterization to random vectors.

### Expected value
The expected value of a random vector $\bf{X}$ is defined as the vector containing the expected values of the individual random variables $X_1, X_2, \ldots, X_N$ as
\begin{equation}
    \mathrm{E}[{\bf{X}}] = \mu_{\bf{X}} = [\mu_1, \mu_2, \ldots, \mu_N]^\top = \left[\mathrm{E}[X_1], \mathrm{E}[X_2],\ldots,\mathrm{E}[X_N]\right]^\top.
\end{equation}

<h4> Expected value of a function </h4>
When we are interested in the expected value of a certain function $g({\bf{X}})$, which accepts a random vector as argument and transforms it to a single value, this can be determined by multiplying the functions result with its corresponding probability and summing or integrating over all possible realizations of $\bf{X}$.
For a discrete random vector $\bf{X}$ consisting of random variables $X_1, X_2, \ldots, X_N$ the expected value of a function $g({\bf{X}})$ can be determined as
\begin{equation}
    \mathrm{E}[g({\bf{X}})] = \sum_{x_1\in S_{X_1}} \cdots \sum_{x_N \in S_{X_N}} g({\bf{x}})\cdot p_{\bf{X}}({\bf{x}})
\end{equation}
and for a continuous random vector as
\begin{equation}
    \mathrm{E}[g({\bf{X}})] = \int_{-\infty}^\infty \cdots \int_{-\infty}^\infty g({\bf{x}})\cdot p_{\bf{X}}({\bf{x}})\ \mathrm{d}x_1\ldots \mathrm{d}x_N.
\end{equation}

### Covariance
Previously, we have introduced the second centralized moment of a univariate random variable as the variance. While the variance denotes the spread in the univariate case, it has a different meaning in the multivariate case. Have a look at Fig. 1, where two contour plots are shown for two distinct multivariate Gaussian probability density functions. The exact mathematical description of a multivariate Gaussian probability density function is introduced <a href="../mathematicalbackground_probability_families/#the-normal-or-gaussian-mathcalnmu-sigma2-distribution">here</a>.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/covariance.svg"
      alt="Visualisation of the concept of covariance."
    />
    <figcaption class="numbered">
      This figure shows two different multivariate Gaussian probability density functions, under which each 10000 random two-dimensional samples are generated. The individual distributions of both the sample elements $x_1$ and $x_2$ are approximated using a histogram and a fitted Gaussian distribution. It can be seen that the variances of both $x_1$ and $x_2$ are identical, however, the initial multivariate distributions are definitely not identical. This phenomenon is caused by the covariance between $x_1$ and $x_2$.
    </figcaption>
  </figure>
</div>

It can be noted that the distributions in Fig. 1 are different, since the first contour plot shows clear circles and the second contour plot shows tilted ellipses. For both distributions, 10000 random realizations ${\bf{x}} = [x_1, x_2]^\top$ are generated and the marginal distributions of both $X_1$ and $X_2$ are shown using a histogram and a fitted Gaussian distribution. It can be seen that the individual distributions of $X_1$ and $X_2$ are exactly equal for both multivariate distributions, but still the multivariate distributions are different. This difference can be explained by the <i>covariance</i> between the random variables $X_1$ and $X_2$ of the random vector $\bf{X}$.

The covariance is a measure of the relationship between 2 random variables. The second distribution in Fig. 1 has a negative covariance between $X_1$ and $X_2$, because if $X_1$ increases $X_2$ decreases. No such thing can be said about the first distribution in Fig. 1, where $X_1$ and $X_2$ seem to have no relationship and behave independently from each other.

The formal definition of the covariance between two random variables $X_1$ and $X_2$ is given by
\begin{equation}
    \text{Cov}[X_1, X_2] = \mathrm{E}[(X_1-\mu_{X_1})(X_2-\mu_{X_2})],
\end{equation}
which is very similar to the definition of the variance, even to such an extent that it actually represents the variance if $X_1=X_2$. Intuitively, one might regard the covariance as the expected value of the multiplication of $X_1$ and $X_2$ from which the means are subtracted. If both the normalized $X_1$ and $X_2$ have the same sign, then their multiplication would be positive and if $X_1$ and $X_2$ have different signs, then their multiplication would be negative. The covariance may therefore be regarded as a measure to indicate how $X_2$ behaves if $X_1$ increases or decreases.

<br></br>
<div class="example">
<h4> Exercise </h4>
<hr>
Recalling the exercise from previous <a href="../mathematicalbackground_probability_functions/#conditional-probabilities">section</a>, let random variables $X$ and $Y$ have joint PDF
\begin{equation*}
    f_{X,Y}(x,y) =
	\begin{cases}
			5x^2/2 & -1 \leq x \leq 1; 0 \leq y \leq x^2, \\
			0 & \text{otherwise.}
	\end{cases}
\end{equation*}
In the previous section, we found that:
<ul>
<li> $\mathrm{E}[X] = 0$ and $\mathrm{Var}[X] = \frac{10}{14}$ </li>
<li> $\mathrm{E}[X] = \frac{5}{14}$ and $\mathrm{Var}[X] = 5/27 - (5/14)^2 = .0576$.</li>
</ul>
With this knowledge, can you compute Var[$X+Y$]?

</ol>
<button class="collapsible">Show solution</button>
<div class="content">

The variance of $X + Y$ is
\begin{equation*}
    \begin{split}
        \mathrm{Var}[X+Y] &\overset{\href{./#fn:1}{1}}{=}  \mathrm{Var}[X] + \mathrm{Var}[Y] + 2 \mathrm{E}[(X-\mu_X)(Y-\mu_Y)]\\
        &= 5/7 + 0.0576 = 0.7719
    \end{split}
\end{equation*}</li>

</div>
</div>

[^1]
[^1]: Proof that $\mathrm{Var}[X+Y] = \mathrm{Var}[X] + \mathrm{Var}[Y] + 2 \mathrm{E}[(X-\mu_X)(Y-\mu_Y)]$: \begin{equation}
    \begin{split}
        \mathrm{Var}[X+Y] &= \mathrm{E}[(X+Y-(\mu_X+\mu_Y))^2]\newline
        &= \mathrm{E}[((X-\mu_X)+(Y-\mu_Y))^2]\newline
        &= \mathrm{E}[(X-\mu_X)^2+2(X-\mu_X)(Y-\mu_Y)+(Y-\mu_Y))^2]
    \end{split}
\end{equation}

### Correlation
The definition of the covariance can be rewritten as
\begin{equation}
    \begin{split}
        \text{Cov}[X_1, X_2]
        &= \mathrm{E}[(X_1-\mu_{X_1})(X_2-\mu_{X_2})], \newline
        &= \mathrm{E}[X_1X_2 - \mu_{X_1}X_2 - \mu_{X_2}X_1 + \mu_{X_1}\mu_{X_2}], \newline
        &= \mathrm{E}[X_1X_2] - \mu_{X_1}\mathrm{E}[X_2] - \mu_{X_2}\mathrm{E}[X_1] + \mu_{X_1}\mu_{X_2}, \newline
        &= \mathrm{E}[X_1X_2] - \mu_{X_1}\mu_{X_2} -\mu_{X_1}\mu_{X_2} + \mu_{X_1}\mu_{X_2}, \newline
        &= \mathrm{E}[X_1X_2] - \mu_{X_1}\mu_{X_2}.
    \end{split}
\end{equation}
The term $\mathrm{E}[X_1X_2]$ is called the <i>correlation</i> $r_{X_1,X_2}$ of $X_1$ and $X_2$ and is defined as
\begin{equation}\label{eq:def_corr}
    r_{X_1,X_2} = \mathrm{E}[X_1X_2].
\end{equation}
This correlation can be regarded as a non-normalized version of the covariance. These two terms are related through
\begin{equation}\label{eq:cov_corr}
    \text{Cov}[X_1, X_2] = r_{X_1,X_2} - \mu_{X_1}\mu_{X_2}.
\end{equation}
It can be noted that the correlation and covariance of two random variables are equal if the mean values of both random variables are $0$.

#### Uncorrelated random variables
Two random variables are called <i>uncorrelated</i> if the covariance between both random variables equals $0$ as
\begin{equation}
    \text{Cov}[X_1, X_2] = 0.
\end{equation}
Although the term suggests that it is related to the correlation between two random variables, it is defined as a zero covariance. The former has a different definition.

#### Orthogonality
Two random variables are called <i>orthogonal</i> if the correlation between both random variables equals $0$ as
\begin{equation}
    r_{X_1, X_2} = 0.
\end{equation}

### Correlation coefficient
The value of the covariance depends significantly on the variance of both random variables and is therefore unbounded. In order to express the relationship between two random variables without having a dependence on the variances, it first has to be normalized. Therefore the  <i>correlation coefficient</i> is introduced as
\begin{equation} \label{eq:corr_coef}
    \rho_{X_1, X_2} = \frac{\text{Cov}[X_1, X_2]}{\sqrt{\text{Var}[X_1]\text{Var}[X_2]}} = \frac{\text{Cov}[X_1,X_2]}{\sigma_{X_1}\sigma_{X_2}}.
\end{equation}
Please note that this represents the normalized covariance and not the normalized correlation between two random variables, although the name suggests otherwise. Because of this normalization, the correlation coefficient has the property to be bounded between $-1$ and $1$ as
\begin{equation}
    -1 \leq \rho_{X_1, X_2} \leq 1.
\end{equation}
Fig. 2 shows realizations of three different probability distributions with negative, zero and positive correlation coefficients.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/correlation_coefficient.svg"
      alt="Visualisation of the concept of correlation coefficient."
    />
    <figcaption class="numbered">
      Scatter plots of random realizations of random variables $X_1$ and $X_2$ with negative, zero and positive correlation coefficients.
    </figcaption>
  </figure>
</div>

<div class="example">
<h4> Exercise </h4>
<hr>
$X$ and $Y$ are identically distributed random variables with $\mathrm{E}[X] = \mathrm{E}[Y] = 0$ and covariance $\mathrm{Cov}[X,Y] = 3$ and correlation coefficient $\rho_{X,Y} = 1/2$. For nonzero constants $a$ and $b$, $U=aX$ and $V=bY$.
<ol type="a">
    <li> Find $\mathrm{Cov}[U,V]$. </li>
    <li>Find the correlation coefficient $\rho_{U,V}$.</li>
    <li>Let $W = U + V$. For what values of $a$ and $b$ are $X$ and $W$ uncorrelated?</li>
</ol>
<button class="collapsible">Show solution</button>
<div class="content">
<ol type="a">
    <li> Since $X$ and $Y$ have zero expected value, $\mathrm{Cov}[X,Y] = \text{E}[XY] = 3$, $\text{E}[U] = a\text{E}[X]=0$ and $\text{E}[V] = b\text{E}[Y]=0$. It follows that
    \begin{equation*}
        \begin{split}
            \mathrm{Cov}[U,V] &= \mathrm{E}[UV]\\
            &=\mathrm{E}[abXY]\\
            &=ab\mathrm{E}[XY]=ab\mathrm{Cov}[X,Y]=3ab.
        \end{split}
    \end{equation*} </li>
    <li> We start by observing that $\text{Var}[U]=a^2 \text{Var}[X]$ and $\text{Var}[V]=b^2 \text{Var}[Y]$.
    It follows that
    \begin{equation*}
        \begin{split}
            \rho_{U,V} &= \frac{\mathrm{Cov}[U,V]}{\sqrt{\mathrm{Var}[U]\mathrm{Var}[V]}}\\
            &= \frac{ab\mathrm{Cov}[X,Y]}{\sqrt{a^2\mathrm{Var}[X]b^2\mathrm{Var}[Y]}} = \frac{ab}{\sqrt{a^2 b^2}}\rho_{X,Y} = \frac{1}{2} \frac{ab}{|ab|}.
        \end{split}
    \end{equation*}
    Not that $ab/|ab|$ is 1 if $a$ and $b$ have the same sign or is -1 if they have opposite signs.</li>
    <li>Since $\mathrm{E}[X] = 0$,
    \begin{equation*}
        \begin{split}
            \mathrm{Cov}[X,W] &= \mathrm{E}[XW]-\mathrm{E}[X]\mathrm{E}[U]\\
            &= \mathrm{E}[XW]\\
            &= \mathrm{E}[X(aX+bY)]\\
            &= a\mathrm{E}[X^2] + b\mathrm{E}[XY]\\
            &= a\mathrm{Var}[X] + b\mathrm{Cov}[X,Y].
        \end{split}
    \end{equation*}
    Since $X$ and $Y$ are identically distributed, $\mathrm{Var}[X] = \mathrm{Var}[Y]$ and
    \begin{equation*}
        \frac{1}{2} = \rho_{X,Y} = \frac{\mathrm{Cov}[X,Y]}{\sqrt{\mathrm{Var}[X]\mathrm{Var}[Y]}} = \frac{\mathrm{Cov}[X,Y]}{\mathrm{Var}[X]} = \frac{3}{\mathrm{Var}[X]}.
    \end{equation*}
    This implies $\mathrm{Var}[X] = 6$. From (3), $\mathrm{Cov}[X,W]=6a+3b=0$, or $b = -2a$.</li>
</ol>
</div>
</div>

### Cross-covariance matrix
We previously discussed how we could determine the covariance of two random variables. Let us turn now to the covariance of two random vectors ${\bf{X}} = [X_1, X_2,\ldots,X_N]^\top$ and ${\bf{Y}}=[Y_1,Y_2,\ldots,Y_N]^\top$. Intuitively, one might say that this covariance cannot be described by a single number, because there are more than one combinations of random variables of which we want to calculate the covariance. As an example, we could determine the covariances of $X_1$ and $Y_1$, $X_1$ and $Y_{23}$ and $X_N$ and $Y_1$. In order to facilitate for all these possible combinations, there is a need to introduce the <i>cross-covariance matrix</i> $\bf{\Gamma_{XY}}$, which contains the covariance of all the possible combinations of the random variables in random vectors $\bf{X}$ and $\bf{Y}$.

The covariance matrix is formally defined as
\begin{equation}\label{eq:cov_mat}
    {\bf{\Gamma_{XY}}} =
    \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{Y}}-\mu_{\bf{Y}})^\top] =
    \begin{bmatrix}
        \gamma_{11}     & \gamma_{12}       & \cdots    & \gamma_{1N} \newline
        \gamma_{21}     & \gamma_{22}       & \cdots    & \gamma_{2N} \newline
        \vdots          & \vdots            & \ddots    & \vdots \newline
        \gamma_{N1}     & \gamma_{N2}       & \cdots    & \gamma_{NN}
    \end{bmatrix},
\end{equation}
where the individual coefficients correspond to
\begin{equation}\label{eq:cov_entries}
    \gamma_{nm} = \text{Cov}[X_n, Y_m] = \mathrm{E}[(X_n - \mu_{X_n})(Y_m-\mu_{Y_m})].
\end{equation}
The transpose operator in the first equation creates a matrix from the two column vectors filled with the covariances of all possible combinations of random variables. For each of these covariances, the correlation coefficient $\rho_{nm}$ can be calculated similarly using the definition of the correlation coefficient. Two random vectors are called uncorrelated if ${\bf{\Gamma_{XY}}} = 0$.

<h4> Auto-covariance matrix of a random vector </h4>
For the special case that ${\bf{X}} = {\bf{Y}}$, the cross-covariance matrix is called the <i>auto-covariance matrix</i>, which calculates the covariances between all random variables in $\bf{X}$. The definition is the same as the definition of the covariance matrix, where $\bf{\Gamma_{XX}}$ is often simplified as $\bf{\Gamma_X}$.

<div class="example">
<h4> Exercise </h4>
<hr>
An $n$-dimensional Gaussian vector $\mathbf{W}$ has a block diagonal covariance matrix
\begin{equation}
    \mathbf{C_W} =
    \begin{bmatrix}
        \mathbf{C_X} & \mathbf{0}\\
        \mathbf{0} & \mathbf{C_Y}
    \end{bmatrix},
\end{equation}
where $\mathbf{C_X}$ is $m \times m$, $\mathbf{C_Y}$ is $(n-m) \times (n-m)$. Show that $\mathbf{W}$ can be written in terms of component vectors $\mathbf{X}$ and $\mathbf{Y}$ in the form
\begin{equation}
    \mathbf{W} =
    \begin{bmatrix}
        \mathbf{X} \\
        \mathbf{Y}
    \end{bmatrix},
\end{equation}
such that $\mathbf{X}$ and $\mathbf{Y}$ are independent Gaussian random vectors.
<button class="collapsible">Show solution</button>
<div class="content">
As given in the problem statement, we define the $m$-dimensional vector $\mathbf{X}$, the $n$-dimensional vector $\mathbf{Y}$ and $\mathbf{W} = \begin{bmatrix}
                    \mathbf{X'} \newline
                    \mathbf{Y'}
              \end{bmatrix}'
$. Note that $\mathbf{W}$ has expected value
\begin{equation*}
   \overline{\mu_W} = \mathrm{E}[\mathbf{W}] = \mathrm{E} \begin{bmatrix}
        \mathbf{X} \newline
        \mathbf{Y}
    \end{bmatrix}
    = \begin{bmatrix}
        \mathrm{E}[\mathbf{X}] \newline
        \mathrm{E}[\mathbf{Y}]
    \end{bmatrix}
    =\begin{bmatrix}
        \overline{\mu_X} \newline
        \overline{\mu_Y}
    \end{bmatrix}.
\end{equation*}
The covariance matrix of $\mathbf{W}$ is
\begin{equation*}
\begin{split}
        \mathbf{C_W} = &\mathrm{E}[(\mathbf{W}-\mu_W)(\mathbf{W}-\mu_W)']=\newline   
       			& = \mathrm{E}\left[
       			\begin{bmatrix}
       			\mathbf{X} - \overline{\mu_X} \newline \mathbf{Y}- \overline{\mu_Y}
       			\end{bmatrix}
			[ (\mathbf{X}-\overline{\mu_X})' \quad (\mathbf{Y}-\overline{\mu_Y})']\right]
			\newline
    &= \begin{bmatrix}
            \mathrm{E}[(\mathbf{X}-\overline{\mu_X})(\mathbf{X}-\overline{\mu_X})']   &\mathrm{E}[(\mathbf{X}-\overline{\mu_X})(\mathbf{Y}-\overline{\mu_Y})'] \newline
            \mathrm{E}[(\mathbf{Y}-\overline{\mu_Y})(\mathbf{X}-\overline{\mu_X})']  &\mathrm{E}[(\mathbf{Y}-\overline{\mu_Y})(\mathbf{Y}-\overline{\mu_Y})']
    \end{bmatrix}\newline
    &= \begin{bmatrix}
        \mathbf{C_X} & \mathbf{C_{XY}} \newline
        \mathbf{C_{YX}} & \mathbf{C_Y}
    \end{bmatrix}.
\end{split}
\end{equation*}
The assumption that $\mathbf{X}$ and $\mathbf{Y}$ are independent implies that
\begin{equation*}
    \mathbf{C_{XY}} = \mathrm{E}[(\mathbf{X}-\overline{\mu_X})(\mathbf{Y'}-\overline{\mu_Y}')] = \mathrm{E}[(\mathbf{X}-\overline{\mu_X})] \mathrm{E}[(\mathbf{Y}-\overline{\mu_Y})'] = \mathbf{0}.
\end{equation*}
This also implies that $\mathbf{C_{YX}} = \mathbf{C_{XY}'} = \mathbf{0}$. Thus
\begin{equation*}
    \mathbf{C_W} =
    \begin{bmatrix}
        \mathbf{C_X} & \mathbf{0}\\
        \mathbf{0} & \mathbf{C_Y}
    \end{bmatrix},
\end{equation*}
</div>
</div>


### Cross-correlation matrix
Similarly to the cross-covariance matrix, the <i>cross-correlation matrix</i> can be defined containing the correlations of all combinations between the random variables in $\bf{X}$ and $\bf{Y}$. The cross-correlation matrix of random vectors $\bf{X}$ and $\bf{Y}$ is denoted by $\bf{R_{XY}}$ and is defined as
\begin{equation}\label{eq:corr_mat}
    {\bf{R_{XY}}} =
    \mathrm{E}[{\bf{XY}}^\top] =
    \begin{bmatrix}
        r_{11}     & r_{12}       & \cdots    & r_{1N} \newline
        r_{21}     & r_{22}       & \cdots    & r_{2N} \newline
        \vdots     & \vdots       & \ddots    & \vdots \newline
        r_{N1}     & r_{N2}       & \cdots    & r_{NN}
    \end{bmatrix},
\end{equation}
where the individual coefficients correspond to the individual correlations
\begin{equation}
    r_{nm} = \mathrm{E}[X_nY_m].
\end{equation}
Two random vectors are called orthogonal if ${\bf{R_{XY}}} = 0$. Furthermore it can be proven that the cross-covariance matrix and the cross-covariance matrix are related through
\begin{equation}
    {\bf{\Gamma_{XY}}} = {\bf{R_{XY}}} - \mu_{\bf{X}}\mu_{\bf{Y}}^\top.
\end{equation}

<h4> Auto-correlation matrix of a random vector </h4>
For the special case that ${\bf{X}} = {\bf{Y}}$, the cross-correlation matrix is called the <i>auto-correlation matrix</i>, which calculates the correlations between all random variables in $\bf{X}$. The definition is the same as the definition of the cross-correlation matrix, where $\bf{R_{XX}}$ is often simplified as $\bf{R_X}$.


## Linear transformations of random vectors
In the previous reader some calculation rules were determined for the mean and variance of a linearly transformed random variable. This subsection will continue with this line of thought, but now for random vectors. We will define an invertible transformation matrix $\bf{A}$, with dimensions $(N\times N)$, which will linearly map a random vector $\bf{X}$ of length $N$ to a random vector $\bf{Y}$ again with length $N$ after adding an equally long column vector $\bf{b}$ through
\begin{equation}
    {\bf{Y}} = g({\bf{X}}) = {\bf{AX}} + {\bf{b}}.
\end{equation}

### Probability density function
From the initial multivariate probability density function of $\bf{X}$, $p_{\bf{X}}({\bf{x}})$, the new probability density function of $\bf{Y}$ can be determined as
\begin{equation}
    p_{\bf{Y}}({\bf{y}}) = \frac{p_{\bf{X}}(g^{-1}({\bf{y}}))}{|\det {\bf{A}}|} = \frac{p_{\bf{X}}({\bf{A}}^{-1}({\bf{y-b}}))}{|\det {\bf{A}}|},
\end{equation}
where $|\det {\bf{A}}|$ is the absolute value of the determinant of $\bf{A}$.

### Mean vector
The new mean vector of the random vector $\bf{Y}$ can be determined as
\begin{equation}
    \mu_{\bf{Y}} = \mathrm{E}[\bf{Y}] = \mathrm{E}[{\bf{AX}} + {\bf{b}}] = {\bf{A}}\mathrm{E}[{\bf{X}}] + {\bf{b}} = {\bf{A}}\mu_{\bf{X}} + {\bf{b}}.
\end{equation}

### Cross-covariance and cross-correlation matrix
By the definition of the cross-covariance matrix, the cross-covariance matrices $\bf{\Gamma_{XY}}$
and $\bf{\Gamma_{YX}}$ can be determined from the original auto-covariance matrix $\bf{\Gamma_X}$ of $\bf{X}$ through
\begin{equation}
\begin{split}
    {\bf{\Gamma_{XY}}}
    &= \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{Y}} - \mu_{\bf{Y}})^\top], \newline
    &= \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{AX+b}}-({\bf{A}}\mu_{\bf{X}} + {\bf{b}}))^\top], \newline
    &= \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{A}}({\bf{X}}-\mu_{\bf{X}}))^\top], \newline
    &= \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{X}}-\mu_{\bf{X}})^\top{\bf{A}}^\top], \newline
    &= \mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{X}}-\mu_{\bf{X}})^\top] {\bf{A}}^\top = {\bf{\Gamma_{X}A}}^\top
\end{split}
\end{equation}
and similarly we can find the result
\begin{equation}
    {\bf{\Gamma_{YX}}} = {\bf{A\Gamma_{X}}}.
\end{equation}
The new cross-correlation matrices $\bf{R_{XY}}$ and $\bf{R_{YX}}$ can be determined as
\begin{equation}
\begin{split}
    {\bf{R_{XY}}}
    &= \mathrm{E}[\bf{XY}^\top], \newline
    &= \mathrm{E}[{\bf{X}}({\bf{AX+b}})^\top], \newline
    &= \mathrm{E}[{\bf{X}}({\bf{AX}})^\top + {\bf{Xb}}^\top], \newline
    &= \mathrm{E}[{\bf{XX}}^\top{\bf{A}}^\top] + \mathrm{E}[{\bf{X}}]{\bf{b}}^\top, \newline
    &= {\bf{R_XA}}^\top + \mu_{\bf{X}}{\bf{b}}^\top
\end{split}
\end{equation}
and similarly as
\begin{equation}
    {\bf{R_{YX}}} = {\bf{AR_X}} + {\bf{b}}\mu_{\bf{X}}^\top.
\end{equation}

### Auto-covariance and auto-correlation matrix
The auto-covariance matrix of ${\bf{Y}}$ can be determined through
\begin{equation}
\begin{split}
    {\bf{\Gamma_{Y}}}
    &= \mathrm{E}[({\bf{Y}}-\mu_{\bf{Y}})({\bf{Y}} - \mu_{\bf{Y}})^\top], \newline
    &= \mathrm{E}[({\bf{AX+b}}-({\bf{A}}\mu_{\bf{X}} + {\bf{b}}))({\bf{AX+b}}-({\bf{A}}\mu_{\bf{X}} + {\bf{b}}))^\top], \newline
    &= \mathrm{E}[({\bf{A}}({\bf{X}}-\mu_{\bf{X}}))({\bf{A}}({\bf{X}}-\mu_{\bf{X}}))^\top], \newline
    &= \mathrm{E}[{\bf{A}}({\bf{X}}-\mu_{\bf{X}})({\bf{X}}-\mu_{\bf{X}})^\top{\bf{A}}^\top], \newline
    &= {\bf{A}}\mathrm{E}[({\bf{X}}-\mu_{\bf{X}})({\bf{X}}-\mu_{\bf{X}})^\top] {\bf{A}}^\top = {\bf{A\Gamma_{X}A}}^\top.
\end{split}
\end{equation}
In a similar fashion the new auto-correlation matrix of $\bf{Y}$ can be calculated as
\begin{equation}
    \begin{split}
        {\bf{R_Y}}
        &= \mathrm{E}[{\bf{YY}}^\top], \newline
        &= \mathrm{E}[({\bf{AX+b}})({\bf{AX+b}})^\top], \newline
        &= \mathrm{E}[({\bf{AX+b}})({\bf{X}}^\top {\bf{A}}^\top + {\bf{b}}^\top)], \newline
        &= \mathrm{E}[{\bf{AXX}}^\top{\bf{A}}^\top + {\bf{AXb}}^\top + {\bf{bX}}^\top{\bf{A}}^\top + {\bf{bb}}^\top], \newline
        &= {\bf{A}}\mathrm{E}[{\bf{XX}}^\top]{\bf{A}}^\top + {\bf{A}}\mathrm{E}[{\bf{X}}]{\bf{b}}^\top + {\bf{b}}\mathrm{E}[{\bf{X}}^\top]{\bf{A}}^\top + {\bf{bb}}^\top, \newline  
        &= {\bf{AR_{X}A}}^\top + {\bf{A}}\mu_{\bf{X}}{\bf{b}}^\top + {\bf{b}}\mu_{\bf{X}}^\top{\bf{A}}^\top + {\bf{bb}}^\top.
    \end{split}
\end{equation}
