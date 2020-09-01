+++
title = "Families of random variables"

# date = {{ .Date }}
lastmod = 2019-12-30

draft = false       # Is this a draft? true/false
toc = true         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Families of random variables"
  parent = "Probability and random variables"
  weight = 54

+++

<!-- hide footnotes in plaintext, because they are added in the equations -->
<style>
  a.footnote-ref {display: none;}
  a.footnote-backref {display: none;}
</style>

The random processes which are generating observations under a certain probability distribution can be characterized in multiple ways as seen before. This section will discuss some common discrete and continuous probability distributions and explain in which context they are used. Their probability distributions are given together with their expected value and variance. The derivations of the cumulative distribution functions, expected values and variances are all provided. It is important to understand and follow the full derivations before blindly using the outcomes of these derivations.

In order to indicate that a random variable $X$ is distributed according to a certain distribution, e.g., univariate standard normal distribution, we may write $X \sim \mathcal{N}(0,1)$. By this notation, the letter  $\mathcal{N}$ indicates the normal distribution, while the numbers in parenthesis indicate the parameters controlling the distribution. In the case of a normal distribution, these are the mean and the variance. Thus, $X \sim \mathcal{N}(0,1)$  reads "the random variable $X$ is normally distributed with zero mean and unitary variance".

<br></br>

## Families of discrete random variables

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/v-ElE7vsXHU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>


/v-ElE7vsXHU
### The Bernoulli(p) distribution
The Bernoulli distribution is a discrete probability distribution that models an experiment where only 2 outcomes are possible. The probability distribution of flipping a coin is an example of a Bernoulli distribution. These outcomes are mapped to 0 and 1, whose probabilities are $1-p$ and $p$ respectively. The distribution is fully characterized by the parameter $p$, which is the probability of success ($\Pr[X = 1]$).

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_bernoulli_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_bernoulli_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the Bernoulli(p) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Bernoulli(p) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            1-p,     & \text{for } x=0 \newline
            p,       & \text{for } x=1 \newline
            0,       & \text{otherwise}
        \end{cases}
    \end{equation}
    where $p$ is in the range $ 0 < p < 1 $.
    <!---->
</div>

<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Bernoulli(p) distribution can be determined as
    \begin{equation*}
        \begin{split}
            P_X(x)
            &= \begin{cases}
                0,                  &\text{for } x<0 \\
                1-p,                &\text{for } x=0 \\
                1.                  &\text{for } x>0
            \end{cases}
        \end{split}
    \end{equation*}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{n=-\infty}^x p_X(n) \\
            &= \begin{cases}
                0,                  &\text{for } x<0 \\
                \displaystyle \sum_{n=-\infty}^0p_X(n), &\text{for } x=0 \\
                1,                  &\text{for } x>0
            \end{cases} \\
            &= \begin{cases}
                0,                  &\text{for } x<0 \\
                1-p,                &\text{for } x=0 \\
                1.                  &\text{for } x>0
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Bernoulli(p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= p.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{n=-\infty}^{\infty} n\cdot p_X(n), \\
            &= \sum_{n=0}^1 n\cdot p_X(n), \\
            &= 0\cdot (1-p) + 1\cdot p, \\
            &= p.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Bernoulli(p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= p(1-p)
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[(X-\mathbb{E}[X])^2], \\
            &= \mathbb{E}[X^2] - 2\mathbb{E}[X]\mathbb{E}[X] + \mathbb{E}[X]^2, \\
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= \sum_{n=-\infty}^{\infty} n^2\cdot p_X(n) - p^2, \\
            &= \sum_{n=0}^{1} n^2\cdot p_X(n) - p^2, \\
            &= 0^2\cdot(1-p) + 1^2\cdot p -p^2. \\
            &= p(1-p)
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<br></br>

### The Geometric(p) distribution
The Geometric distribution is a discrete probability distribution that models an experiment with probability of success $p$. The Geometric distribution gives the probability that the first success is observed at the $x^{th}$ independent trial. The distribution is fully characterized by the parameter $p$, which is the probability of success.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_geometric_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_geometric_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the Geometric(p) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Geometric(p) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            p(1-p)^{x-1},     & \text{for } x=1,2,\ldots \\
            0,                & \text{otherwise}
        \end{cases}
    \end{equation}
    where $p$ is in the range $ 0 < p < 1 $.
    <!---->
</div>

<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Geometric(p) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \begin{cases}
                0,                                  &\text{for } x < 1\\
                1-(1-p)^x.                          &\text{for } x\geq 1
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{n=-\infty}^x p_X(n), \\
            &= \begin{cases}
                0,                                  &\text{for } x < 1\\
                \sum_{n=1}^x p(1-p)^{n-1},          &\text{for } x\geq 1
            \end{cases} \\
            &= \begin{cases}
                0,                                  &\text{for } x < 1\\
                p\sum_{m=0}^{x-1} (1-p)^{m},        &\text{for } x\geq 1
            \end{cases} \\
            &\overset{\href{./#fn:1}{1}}{=} \begin{cases}
                0,                                  &\text{for } x < 1\\
                p\frac{1-(1-p)^x}{1-(1-p)},         &\text{for } x\geq 1
            \end{cases} \\
            &= \begin{cases}
                0,                                  &\text{for } x < 1\\
                1-(1-p)^x.                          &\text{for } x\geq 1
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^1]
[^1]: Sum of a geometric series: $$ \sum_{k=0}^{n-1}ar^k = a\left(\frac{1-r^n}{1-r}\right) \quad \text{for }|r|<1$$


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Geometric(p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \frac{1}{p}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{n=-\infty}^{\infty} n\cdot p_X(n), \\
            &= \sum_{n=1}^\infty n\cdot p(1-p)^{n-1}, \\
            &= p\sum_{n=1}^\infty n (1-p)^{n-1}, \\
            &\overset{\href{./#fn:2}{2}}{=} \frac{p}{(1-(1-p))^2} = \frac{1}{p}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^2]
[^2]: Derivative of the sum of a geometric series: $$ \sum_{k=1}^{\infty}kr^{k-1} = \frac{1}{(1-r)^2}\quad \text{for }|r|<1$$


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Geometric(p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \frac{1-p}{p^2}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation*}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[(X-\mathbb{E}[X])^2], \\
            &= \mathbb{E}[X^2] - 2\mathbb{E}[X]\mathbb{E}[X] + \mathbb{E}[X]^2, \\
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= \sum_{n=-\infty}^{\infty} n^2\cdot p(1-p)^{n-1} - \frac{1}{p^2}, \\
            &= p\sum_{n=1}^\infty n^2\cdot (1-p)^{n-1} - \frac{1}{p^2}, \\
            &\overset{\href{./#fn:3}{3}}{=}  -\frac{p((1-p)+1)}{((1-p)-1)^3} - \frac{1}{p^2}, \\
            &= \frac{2p-p^2}{p^3} -\frac{p}{p^3} = \frac{p-p^2}{p^3} = \frac{1-p}{p^2}.
        \end{split}
    \end{equation*}
    <!---->
  </div>
</div>

[^3]
[^3]: Second derivative of the sum of a geometric series: $$ \sum_{k=1}^{\infty}k^2r^{k-1} = -\frac{r+1}{(r-1)^3}\quad \text{for }|r|<1$$


<br></br>

### Binomial(n,p) distribution
The Binomial distribution is a discrete probability distribution that models an experiment with probability of success $p$. The Binomial distribution gives the probability of observing $x$ successes in $n$ independent trials. The distribution is fully characterized by the parameters $n$ and $p$. The parameter $n$ denotes the amount of independent trials and the parameter $p$ denotes the probability of observing a success per trial.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_binomial_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_binomial_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the Binomial(n,p) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Binomial(n,p) distribution is given as
    \begin{equation}
        p_X(x) \overset{\href{./#fn:4}{4}}{=} \begin{pmatrix} n \\ x\end{pmatrix}p^x(1-p)^{n-x},
    \end{equation}
    where $0 < p < 1$ and $n$ is an integer such that $n\geq 1$.
    <!---->
</div>

[^4]
[^4]: The binomial coefficient, which returns the total amount of possible unsorted combinations of $k$ distinct elements from a set of $n$ distinct elements, defined as: $$ \begin{pmatrix} n \\ k\end{pmatrix} = \frac{n!}{k!(n-k)!}, $$ where $!$ is the factorial operator (e.g. $4!=4\cdot 3\cdot 2\cdot 1$), which denotes the total amount of sorted permutations.


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Binomial(n,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{m=0}^x \begin{pmatrix} n \\ m\end{pmatrix}p^m(1-p)^{n-m}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{m=0}^x p_X(m), \\
            &= \sum_{m=0}^x \begin{pmatrix} n \\ m\end{pmatrix}p^m(1-p)^{n-m}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Binomial(n,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= np
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{m=-\infty}^{\infty}m\cdot p_X(m), \\
            &= \sum_{m=0}^n  m \cdot \begin{pmatrix} n \\ m\end{pmatrix}p^m(1-p)^{n-m}, \\
            &= \sum_{m=1}^n  m \cdot \binom{n}{m} p^m(1-p)^{n-m}, \\
            &\overset{\href{./#fn:5}{5}}{=} \sum_{m=1}^n  n\cdot\binom{n-1}{m-1} p^{m}(1-p)^{n-m}, \\
            &= np \sum_{m=1}^n  \binom{n-1}{m-1} p^{m-1}(1-p)^{(n-1)-(m-1)}, \\
            &\overset{\href{./#fn:6}{6}}{=} np \sum_{k=0}^{l}  \binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &\overset{\href{./#fn:7}{7}}{=} np \cdot (p + (1-p))^l = np
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


[^5][^6][^7]
[^5]: Factors of the binomial coefficient: $$ k \binom n k = k\frac{n!}{k!(n-k)!} = n\frac{(n-1)!}{(k-1)!((n-1)-(k-1))!} = n \binom {n - 1} {k - 1} $$
[^6]: Use substitutions $l = n-1$, $k=m-1$, $i=l-1$ and $j=k-1$.
[^7]: Binomial theorem: $$ (x+y)^n = \sum_{k = 0}^n \binom{n}{k} x^k y^{n - k} $$


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Binomial(n,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= np(1-p).
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[(X-\mathbb{E}[X])^2], \\
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= -(np)^2 + \sum_{m=-\infty}^{\infty}m^2\cdot p_X(m), \\
            &= -(np)^2 + \sum_{m=0}^n m^2\cdot\binom{n}{m} p^m(1-p)^{n-m}, \\
            &\overset{\href{./#fn:5}{5}}{=} -(np)^2 + \sum_{m=1}^n  nm\cdot\binom{n-1}{m-1} p^{m}(1-p)^{n-m}, \\
            &= -(np)^2 + np \sum_{m=1}^n  m \binom{n-1}{m-1} p^{m-1}(1-p)^{(n-1)-(m-1)}, \\
            &\overset{\href{./#fn:6}{6}}{=} -(np)^2 + np \sum_{k=0}^{l}  (k+1)\binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &= -(np)^2 + np \sum_{k=1}^{l}  k\binom{l}{k} p^{k}(1-p)^{l-k} + np \sum_{k=0}^{l}\binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &\overset{\href{./#fn:5}{5}}{=} -(np)^2 + np \sum_{k=1}^{l}  l\binom{l-1}{k-1} p^{k}(1-p)^{l-k} + np \sum_{k=0}^{l}\binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &= -(np)^2 + nlp^2 \sum_{k=1}^{l}  \binom{l-1}{k-1} p^{k-1}(1-p)^{(l-1)-(k-1)} + np \sum_{k=0}^{l}\binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &\overset{\href{./#fn:6}{6}}{=} -(np)^2 + nlp^2 \sum_{j=0}^{i}  \binom{i}{j} p^{j}(1-p)^{i-j} + np \sum_{k=0}^{l}\binom{l}{k} p^{k}(1-p)^{l-k}, \\
            &\overset{\href{./#fn:7}{7}}{=} -(np)^2 + nlp^2 (p+(1-p))^i + np (p+(1-p))^l, \\
            &\overset{\href{./#fn:6}{6}}{=} -n^2p^2 + n(n-1)p^2 + np = -np^2 + np = np(1-p).
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

<br></br>


### The Pascal(k,p) distribution
The Pascal distribution is a probability distribution that is also known as the negative Binomial distribution. The Pascal distribution gives the probability of observing the $k^{th}$ success at the $x^{th}$ trial. The distribution is fully characterized by the parameters $k$ and $p$. The parameter $k$ denotes the desired amount of successes and the parameter $p$ denotes the chance of success in an individual trial.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_pascal_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_pascal_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the Pascal(k,p) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Pascal(k,p) distribution is given as
    \begin{equation}
        p_X(x) = \begin{pmatrix} x-1 \\ k-1\end{pmatrix}p^k(1-p)^{x-k},
    \end{equation}
    where $0 < p < 1$ and $k$ is an integer such that $k\geq 1$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Pascal(k,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{n=-\infty}^x\begin{pmatrix} n-1 \\ k-1\end{pmatrix}p^k(1-p)^{n-k}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{n=-\infty}^x p_X(n), \\
            &= \sum_{n=-\infty}^x\begin{pmatrix} n-1 \\ k-1\end{pmatrix}p^k(1-p)^{n-k}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Pascal(k,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \frac{k}{p}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{n=-\infty}^\infty n \cdot p_X(n), \\
            &= \sum_{n=k}^{\infty} n\cdot \binom{n-1}{k-1}p^k(1-p)^{n-k}, \\
            &\overset{\href{./#fn:5}{5}}{=} \sum_{n=k}^\infty k\binom{n}{k} p^k(1-p)^{n-k}, \\
            &= \frac{kp^k}{(1-p)^k} \sum_{n=k}^\infty \binom{n}{k} (1-p)^{n}, \\
            &\overset{\href{./#fn:8}{8}}{=} \frac{kp^k}{(1-p)^k}\cdot \frac{(1-p)^k}{p^{k+1}}, \\
            &= \frac{k}{p}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^8]
[^8]: Ordinary generating function: $$ \sum_{n=k}^\infty \binom{n}{k}y^n = \frac{y^k}{(1-y)^{k+1}} $$


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Pascal(k,p) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \frac{k(1-p)}{p^2}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation*}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= -\frac{k^2}{p^2} + \sum_{n=-\infty}^\infty n^2 \cdot p_X(n), \\
            &= -\frac{k^2}{p^2} + \sum_{n=k}^{\infty} n^2\cdot \binom{n-1}{k-1}p^k(1-p)^{n-k}, \\
            &\overset{\href{./#fn:5}{5}}{=} -\frac{k^2}{p^2} + \sum_{n=k}^{\infty} nk\cdot \binom{n}{k}p^k(1-p)^{n-k}, \\
            &= -\frac{k^2}{p^2} + \frac{kp^k}{(1-p)^k}\sum_{n=k}^{\infty} n\cdot \binom{n}{k}(1-p)^{n}, \\
            &\overset{\href{./#fn:9}{9}}{=} -\frac{k^2}{p^2} + \frac{kp^k}{(1-p)^k}\left(\sum_{n=k}^{\infty} n\cdot \binom{n-1}{k-1}(1-p)^{n}+\sum_{n=k}^{\infty} n\cdot \binom{n-1}{k}(1-p)^{n}\right), \\
            &\overset{\href{./#fn:5}{5}\ \href{./#fn:10}{10}}{=} -\frac{k^2}{p^2} + \frac{kp^k}{(1-p)^k}\left(k\sum_{n=k}^{\infty} \binom{n}{k}(1-p)^{n}+(k+1)\sum_{n=k+1}^{\infty} \binom{n}{k+1}(1-p)^{n}\right), \\
            &\overset{\href{./#fn:8}{8}}{=} -\frac{k^2}{p^2} + \frac{kp^k}{(1-p)^k}\left(k\frac{(1-p)^k}{p^{k+1}}+(k+1)\frac{(1-p)^{k+1}}{p^{k+2}}\right), \\
            &= -\frac{k^2}{p^2} + \frac{kp^k}{(1-p)^k}\left(\frac{(1-p)^k}{p^{k+1}}\left(k + (k+1)\frac{1-p}{p}\right)\right), \\
            &= -\frac{k^2}{p^2} + \frac{k}{p}\left(\frac{k+1-p}{p}\right), \\
            &= -\frac{k^2}{p^2} + \frac{k^2+k-kp}{p^2} = \frac{k(1-p)}{p^2}.
        \end{split}
    \end{equation*}
    <!---->
  </div>
</div>

[^9][^10]
[^9]: Recurrence relationship: $$ \binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k} $$
[^10]:  Variation of the factors of the binomial coefficient: $$ n \binom{n-1}{k} = (k+1)\binom{n}{k+1} $$

<br></br>

### The discrete Uniform(k,l) distribution
The discrete uniform distribution is a discrete probability distribution that models an experiment where the outcomes are mapped only to discrete points on the interval from $k$ up to and including $l$. The distribution is fully characterized by the parameters $k$ and $l$, which are the discrete lower and upper bound of the interval respectively.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_uniform_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_uniform_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the discrete Uniform(k,l) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Uniform(k,l) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            \frac{1}{l-k+1},    &\text{for }x = k, k+1, k+2, \ldots,l\\
            0,                  &\text{otherwise}
        \end{cases}
    \end{equation}
    where $k$ and $l$ are integers such that $k < l$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Uniform(k,l) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x) =
            \begin{cases}
                0  &\text{for } x < k \\
                \frac{x-k+1}{l-k+1}  &\text{for } k \leq x < l \\
                1  &\text{for } x \geq l
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{m=-\infty}^x p_X(m), \\
            &=
            \begin{cases}
                0,  &\text{for } x < k \\
                \sum_{m=k}^x \frac{1}{l-k+1},  &\text{for } k \leq x < l \\
                1,  &\text{for } x \geq l
            \end{cases}\\
            &=
            \begin{cases}
                0,  &\text{for } x < k \\
                \frac{x-k+1}{l-k+1},  &\text{for } k \leq x < l \\
                1.  &\text{for } x \geq l
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Uniform(k,l) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \frac{k+l}{2}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{n=-\infty}^{\infty}n\cdot p_X(n), \\
            &= \sum_{n=k}^l n\cdot \frac{1}{l-k+1}, \\
            &= \frac{1}{l-k+1} \sum_{n=k}^l n, \\
            &= \frac{1}{l-k+1} \sum_{n=k}^l n, \\
            &\overset{\href{./#fn:11}{11}}{=} \frac{1}{l-k+1} \cdot \frac{1}{2} (k+l)(l-k+1), \\
            &= \frac{k+l}{2}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^11]
[^11]: Sum of consecutive integers: \begin{equation*} \begin{split}
    \sum_{n=k}^l n
    &= \frac{1}{2} \left[ \sum_{n=k}^l n + {\color{Gray} \sum_{n=k}^l n} \right] \newline
    &= \frac{1}{2}\left[k + (k+1) + \ldots + (l-1) + l + {\color{Gray} k + (k+1) + \ldots + (l-1) + l}\right] \newline
    &= \frac{1}{2} \underbrace{\left[ (k + {\color{Gray} l}) + (k + {\color{Gray} l}) + \ldots + (k + {\color{Gray} l}) + (k + {\color{Gray} l})  \right]}_{l-k+1 \text{ terms}} \newline
    &= \frac{1}{2} (k+l)(l-k+1)
\end{split}
\end{equation*}


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Uniform(k,l) distribution can be determined as
    \begin{equation*}
        \begin{split}
            \text{Var}[X]
            &= \frac{(l-k+1)^2-1}{12}
        \end{split}
    \end{equation*}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    The variance of the discrete Uniform(k,l) distribution can be determined as
    \begin{equation*}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= -\frac{(k+l)^2}{4} + \sum_{n=k}^l n^2\cdot \frac{1}{l-k+1}, \\
            &= -\frac{(k+l)^2}{4} + \frac{1}{l-k+1}\sum_{n=k}^l n^2, \\
            &\overset{\href{./#fn:12}{12}}{=} -\frac{(k+l)^2}{4} + \frac{1}{l-k+1}\sum_{m=1}^{l-k+1} (m+k-1)^2, \\
            &= -\frac{(k+l)^2}{4} + \frac{1}{l-k+1}\sum_{m=1}^{l-k+1}( m^2 + 2mk + k^2 + 1 - 2m -2k), \\
            &= -\frac{(k+l)^2}{4} + \frac{1}{l-k+1}\left(\sum_{m=1}^{l-k+1} m^2 + (2k-2)\sum_{m=1}^{l-k+1} m + (k^2 + 1 -2k)\sum_{m=1}^{l-k+1} 1\right), \\
            &\overset{\href{./#fn:11}{11}\ \href{./#fn:13}{13}}{=} -\frac{(k+l)^2}{4} + \frac{1}{l-k+1}\bigg(\frac{(l-k+1)(l-k+2)(2l-2k+3)}{6} \\&\qquad+ (2k-2)\frac{1}{2}(l-k+1)(l-k+2)+ (k^2 + 1 -2k)(l-k+1)\bigg), \\
            &= \frac{-3k^2 -3l^2 -6kl}{12} + \frac{4l^2 -4kl +6l -4kl +4k^2 -6k +8l -8k +12}{12} \\
            &\qquad + \frac{12kl - 12k^2 +24k -12l + 12k - 24}{12} + \frac{12k^2 + 12 -24k}{12}, \\
            &= \frac{k^2 + l^2 -2kl -2k +2l}{12}, \\
            &= \frac{(l-k+1)^2-1}{12}
        \end{split}
    \end{equation*}
    <!---->
  </div>
</div>

[^12][^13]
[^12]: Substitute $m = n-k+1$.
[^13]: Square pyramidal number or the sum of squared integers: $$ \sum_{n=1}^k n^2 = \frac{k(k+1)(2k+1)}{6}$$



<br></br>

### The Poisson($\alpha$) distribution
The Poisson distribution is a discrete probability distribution that models the number of events occurring within a certain interval of time, in which the events occur independently from each other at a constant rate. The exact moments at which the events occur are unknown, however, the average number of events occurring within the interval is known and is denoted by the parameter $\alpha$. An example of a process, where the number of events within an interval can be described as a Poisson distribution, is the number of phone calls over a network. For optimal allocation of resources, a service provider needs to know the chance that the allocated capacity is insufficient in order to limit the number of dropped calls. The inhabitants can be described as independent entities (i.e. everyone makes a phone call whenever it suits him or her), whilst they usually have their own habit of making phone calls.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_poisson_pmf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/discrete_poisson_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability mass function and (b) cumulative density function of the Poisson($\alpha$) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability mass function </h4>
    <!---->
    The probability mass function of the discrete Poisson($\alpha$) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            \frac{\alpha^xe^{-\alpha}}{x!},     &\text{for }x = 0,1,2,\ldots\\
            0,                          &\text{otherwise}
        \end{cases}
    \end{equation}
    where $\alpha$ is in the range $\alpha > 0$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the discrete Poisson($\alpha$) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &=
            \begin{cases}
                0,                                                      &\text{for } x<0 \\
               e^{-\alpha} \sum_{n=0}^x \frac{\alpha^n}{n!}.            &\text{for } x\geq 0
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \sum_{n=-\infty}^x p_X(n), \\
            &=
            \begin{cases}
                0,                                                      &\text{for } x<0 \\
                \sum_{n=0}^x \frac{\alpha^ne^{-\alpha}}{n!},            &\text{for } x\geq 0
            \end{cases}\\
            &=
            \begin{cases}
                0,                                                      &\text{for } x<0 \\
               e^{-\alpha} \sum_{n=0}^x \frac{\alpha^n}{n!}.            &\text{for } x\geq 0
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the discrete Poisson($\alpha$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X] = \alpha
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \sum_{n=-\infty}^{\infty}n\cdot p_X(n), \\
            &= \sum_{n=0}^\infty n\cdot \frac{\alpha^n e^{-\alpha}}{n!}, \\
            &= \sum_{n=1}^\infty n\cdot \frac{\alpha^n e^{-\alpha}}{n!}, \\
            &= \alpha \sum_{n=1}^\infty \frac{\alpha^{n-1} e^{-\alpha}}{(n-1)!}, \\
            &\overset{\href{./#fn:6}{6}}{=} \alpha \sum_{l=0}^\infty \frac{\alpha^{l} e^{-\alpha}}{l!}, \\
            &\overset{\href{./#fn:14}{14}}{=} \alpha
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^14]
[^14]: Definition of Poisson distribution and total probability axiom: $$ \sum_{n=-\infty}^{\infty} p_X(n) = 1 $$


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the discrete Poisson($\alpha$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \alpha
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    The variance of the discrete Poisson($\alpha$) distribution can be determined as
    \begin{equation*}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= -\alpha^2 + \sum_{n=-\infty}^{\infty}n^2\cdot p_X(n), \\
            &= -\alpha^2 + \sum_{n=0}^\infty n^2\cdot \frac{\alpha^n e^{-\alpha}}{n!}, \\
            &= -\alpha^2 + \sum_{n=1}^\infty n^2\cdot \frac{\alpha^n e^{-\alpha}}{n!}, \\
            &= -\alpha^2 + \alpha \sum_{n=1}^\infty n\cdot\frac{\alpha^{n-1} e^{-\alpha}}{(n-1)!}, \\
            &\overset{\href{./#fn:6}{6}}{=} -\alpha^2 + \alpha \sum_{l=0}^\infty (l+1)\cdot\frac{\alpha^{l} e^{-\alpha}}{l!}, \\
            &= -\alpha^2 + \alpha \sum_{l=0}^\infty \frac{\alpha^{l} e^{-\alpha}}{l!} + \alpha \sum_{l=0}^\infty l\cdot\frac{\alpha^{l} e^{-\alpha}}{l!}, \\
            &= -\alpha^2 + \alpha \sum_{l=0}^\infty \frac{\alpha^{l} e^{-\alpha}}{l!} + \alpha \sum_{l=1}^\infty l\cdot\frac{\alpha^{l} e^{-\alpha}}{l!}, \\
            &= -\alpha^2 + \alpha \sum_{l=0}^\infty \frac{\alpha^{l} e^{-\alpha}}{l!} + \alpha^2 \sum_{l=1}^\infty \frac{\alpha^{l-1} e^{-\alpha}}{(l-1)!}, \\
            &\overset{\href{./#fn:6}{6}}{=} -\alpha^2 + \alpha \sum_{l=0}^\infty \frac{\alpha^{l} e^{-\alpha}}{l!} + \alpha^2 \sum_{i=0}^\infty \frac{\alpha^{i} e^{-\alpha}}{i!}, \\
            &\overset{\href{./#fn:14}{14}}{=} -\alpha^2 + \alpha + \alpha^2 = \alpha
        \end{split}
    \end{equation*}
    <!---->
  </div>
</div>





<br></br>

## Families of continuous random variables

### Screencast video [⯈]
<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/mgHfvZgXTXI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>
<br></br>

### The Exponential($\lambda$) distribution
The exponential distribution is a continuous probability distribution that follow an exponential curve. The curve is fully characterized by the rate parameter $\lambda$.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_exponential_pdf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_exponential_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability density function and (b) cumulative density function of the Exponential($\lambda$) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability density function </h4>
    <!---->
    The probability density function of the continuous Exponential($\lambda$) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            \lambda e^{-\lambda x},       &\text{for }x\geq 0 \\
            0,                          &\text{for }x<0
        \end{cases}
    \end{equation}
    where $\lambda > 0$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the continuous Exponential($\lambda$) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &=
            \begin{cases}
                1-e^{-\lambda x}       &\text{for } x\geq 0\\
                0                                  &\text{for } x<0
            \end{cases}\\
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    The cumulative distribution function of the continuous Exponential($\lambda$) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \int_{-\infty}^{x} p_X(n) \mathrm{d}n, \\
            &=
            \begin{cases}
                \int_{0}^{x} \lambda e^{-\lambda n} \mathrm{d}n,       &\text{for } x\geq 0\\
                0,                                  &\text{for } x<0
            \end{cases}\\
            &=
            \begin{cases}
                \lambda \left[\frac{-1}{\lambda}e^{-\lambda n}\right]_{0}^x,       &\text{for } x\geq 0\\
                0,                                  &\text{for } x<0
            \end{cases}\\
            &=
            \begin{cases}
                \left[-e^{-\lambda n}\right]_{0}^x,       &\text{for } x\geq 0\\
                0,                                  &\text{for } x<0
            \end{cases}\\
            &=
            \begin{cases}
                1-e^{-\lambda x},       &\text{for } x\geq 0\\
                0                                  &\text{for } x<0
            \end{cases}\\
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the continuous Exponential($\lambda$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \frac{1}{\lambda}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \int_{-\infty}^{\infty} x \cdot p_X(x) \mathrm{d}x, \\
            &= \lambda \int_0^\infty xe^{-\lambda x} \mathrm{d}x, \\
            &\overset{\href{./#fn:15}{15}}{=} \lambda \left[ \frac{-1}{\lambda}xe^{-\lambda x}\right]_0^\infty - \lambda \int_0^\infty \frac{-1}{\lambda}e^{-\lambda x} \mathrm{d}x, \\
            &= -\left[ xe^{-\lambda x}\right]_0^\infty  -\frac{1}{\lambda}\left[ e^{-\lambda x}\right]_0^\infty, \\
            &\overset{\href{./#fn:16}{16}}{=} -(0-0) -\frac{1}{\lambda}(0-1) = \frac{1}{\lambda}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^15][^16]
[^15]: Integration by parts: $$ \int_a^b f(x)g'(x) \mathrm{d}x = \left[ f(x)g(x)\right]_a^b - \int_a^b f'(x)g(x) \mathrm{d}x$$
[^16]: Growth property of exponentials: $$ \lim_{x\to \infty} x^ae^{-x} = 0 $$


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the continuous Exponential($\lambda$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X] = \frac{1}{\lambda^2}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    The variance of the continuous Exponential($\lambda$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= \int_{-\infty}^{\infty} x^2 \cdot p_X(x) \mathrm{d}x -\frac{1}{\lambda^2}, \\
            &= -\frac{1}{\lambda^2} + \lambda\int_{0}^{\infty} x^2e^{-\lambda x} \mathrm{d}x, \\
            &\overset{\href{./#fn:15}{15}}{=} -\frac{1}{\lambda^2} + \lambda \left[ \frac{-1}{\lambda}x^2e^{-\lambda x}\right]_0^\infty - \lambda \int_0^\infty \frac{-2}{\lambda}xe^{-\lambda x} \mathrm{d}x, \\
            &= -\frac{1}{\lambda^2} -\left[ x^2e^{-\lambda x}\right]_0^\infty + 2\int_0^\infty xe^{-\lambda x} \mathrm{d}x, \\
            &\overset{\href{./#fn:15}{15}\ \href{./#fn:16}{16}}{=} -\frac{1}{\lambda^2} - (0-0) + 2\left[ \frac{-1}{\lambda}xe^{-\lambda x}\right]_0^\infty -  2\int_0^\infty \frac{-1}{\lambda}e^{-\lambda x} \mathrm{d}x, \\
            &= -\frac{1}{\lambda^2}  - \frac{2}{\lambda}\left[ xe^{-\lambda x}\right]_0^\infty + \frac{2}{\lambda} \int_0^\infty e^{-\lambda x} \mathrm{d}x, \\
            &\overset{\href{./#fn:16}{16}}{=} -\frac{1}{\lambda^2}  - \frac{2}{\lambda}(0-0) + \frac{2}{\lambda} \left[\frac{-1}{\lambda}e^{-\lambda x}\right]_0^\infty ,\\
            &= -\frac{1}{\lambda^2} - \frac{2}{\lambda^2}(0-1) = \frac{1}{\lambda^2}
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

<br></br>

### The Normal or Gaussian $\mathcal{N}(\mu, \sigma^2)$ distribution
The Normal or Gaussian distribution is probably the most commonly used continuous probability distribution. The distribution is bell-shaped and symmetric. The function is characterized by its mean $\mu$ and its variance $\sigma^2$.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_gaussian_pdf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_gaussian_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability density function and (b) cumulative density function of the Gaussian($\mu$, $\sigma^2$) distribution.
</figcaption>
</figure>

#### The Standard normal $\mathcal{N}(0,1)$ distribution
The Standard normal distribution is a specific case of the Normal or Gaussian distribution, where the mean equals $\mu = 0$ and the variance equals $\sigma^2=1$. This function can be regarded as the normalized Gaussian distribution. Any random variable $Y \sim \mathcal{N}(\mu_Y, \sigma_Y^2)$ can be transformed to a random variable $X$ under the Standard normal distribution by subtracting its mean and dividing by the standard deviation as $X = \frac{Y-\mu_Y}{\sigma_Y}$

#### The $Q$-function
The $Q$-function is a commonly used function in statistics, which calculates the probability of a Standard normal distributed random variable $X$ exceeding a certain threshold $x$. It is also known as the right-tail probability of the Gaussian distribution, since it is calculated by integrating the right side of the Gaussian PDF from the threshold $x$ up to $\infty$. The $Q$-function is defined as
\begin{equation}
    Q(x) = \Pr[X>x] = \frac{1}{\sqrt{2\pi}} \int_x^\infty e^{-\frac{u^2}{2}}\mathrm{d}u.
\end{equation}
The function can be used for all Gaussian distributed random variables, however, the random variable and the corresponding threshold should be normalized first. Additionally, through symmetry follows that $Q(x) = 1-Q(-x)$, where $Q(-x)$ is equal to the cumulative  density function $P_X(x)$.

<div class="example">
  <!---->
  <h4> Probability density function </h4>
    <!---->
    The probability density function of the continuous Gaussian $\mathcal{N}$($\mu, \sigma^2$) distribution is given as
    \begin{equation}
        p_X(x) = \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}},
    \end{equation}
    where $\sigma > 0$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the continuous Gaussian $\mathcal{N}$($\mu, \sigma^2$) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &= Q(-\frac{x-\mu}{\sigma})
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            P_X(x)
            &= \int_{-\infty}^{x} p_X(n) \mathrm{d}n, \\
            &= \frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{x} e^{-\frac{(n-\mu)^2}{2\sigma^2}} \mathrm{d}n, \\
            &= Q(-\frac{x-\mu}{\sigma})
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the continuous Gaussian $\mathcal{N}$($\mu, \sigma^2$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X] = \mu.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    The expected value of the continuous Gaussian $\mathcal{N}$($\mu, \sigma^2$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \int_{-\infty}^{\infty} x \cdot p_X(x) \mathrm{d}x, \\
            &= \frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} xe^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x, \\
            &=\frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} ((x-\mu)+\mu)e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x, \\
            &=\frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} (x-\mu)e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x + \mu\int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x, \\
            &= \frac{-\sigma^2}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} \frac{-2(x-\mu)}{2\sigma^2}e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x + \mu, \\
            &= \frac{-\sigma^2}{\sqrt{2\pi\sigma^2}} \left[ e^{-\frac{(x-\mu)^2}{2\sigma^2}}\right]_{-\infty}^\infty + \mu, \\
            &= \frac{-\sigma^2}{\sqrt{2\pi\sigma^2}}(0-0) + \mu = \mu.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the continuous Gaussian $\mathcal{N}$($\mu, \sigma^2$) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X] = \sigma^2.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[(X-\mu)^2], \\
            &=  \frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} (x-\mu)^2e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x, \\
            &\overset{\href{./#fn:17}{17}}{=} \frac{1}{\sqrt{2\pi\sigma^2}}\int_{-\infty}^{\infty} (x-\mu)^2e^{-\frac{(x-\mu)^2}{2\sigma^2}} \mathrm{d}x, \\
            &= \frac{\sigma^2}{\sqrt{\pi}}\int_{-\infty}^{\infty} w\cdot 2we^{-w^2} \mathrm{d}w, \\
            &\overset{\href{./#fn:15}{15}}{=} \frac{\sigma^2}{\sqrt{\pi}} \left[ -we^{-w^2}\right]_{-\infty}^\infty - \frac{\sigma^2}{\sqrt{\pi}} \int_{-\infty}^{\infty} -e^{-w^2} \mathrm{d}w, \\
            &\overset{\href{./#fn:16}{16}\ \href{./#fn:18}{18}}{=} \frac{\sigma^2}{\sqrt{\pi}} (0-0) + \frac{\sigma^2}{\sqrt{\pi}} \sqrt{\pi} = \sigma^2. \\
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>

[^17][^18]
[^17]: Substitute $w=\frac{x-\mu}{\sqrt{2\sigma^2}}$.
[^18]: Gaussian integral: $$ \int_{-\infty}^\infty e^{-x^2} \mathrm{d}x =\sqrt{\pi} $$


As is implicated by the <a href="../mathematicalbackground_probability_functions/#central-limit-theorem">central limit theorem</a>, the Gaussian distribution is extremely important. The Gaussian distribution is often used to model measurements in practice and, thanks to the CLT, its use can often be extended to other distributions. A Gaussian distribution is also often used to model the thermal noise of a band-limited system. This section will generalize the definition of the Gaussian distribution given in the previous reader and extend it to the multivariate case.

#### Univariate distribution
In the case of a single random variable $X$ that is generated according to a Gaussian distribution, defined by its mean $\mu$ and variance $\sigma^2$ where the subscript $\cdot_X$ is now omitted for simplification, the probability density function is defined as
\begin{equation}
    p_X(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}.
\end{equation}
The left side of the figure below shows an example of an univariate Gaussian distribution.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/gaussian.svg"
      alt="Example of an univariate and a multivariate Gaussian probability density function."
    />
    <figcaption>
      Example of an univariate and a multivariate Gaussian probability density function.
    </figcaption>
  </figure>
</div>

#### Multivariate distribution
The definition of the univariate Gaussian distribution can be extended to a multivariate distribution. In order to define the Gaussian distribution the position and its spread are required. These quantities are represented by the mean vector $\bf\mu$ and the covariance matrix $\bf\Sigma$. Whereas the covariance matrix is defined as $\bf\Gamma$ <a href="../mathematicalbackground_probability_vectors/#cross-covariance-matrix">in this section</a>, literature has adopted the $\bf\Sigma$ notation when discussing multivariate Gaussian distributions, as $\Sigma$ is the Greek capital letter of $\sigma$.

To indicate that a $k$-dimensional random vector $\bf{X}$ is Gaussian distributed, we can write ${\bf{X}} \sim \mathcal{N}\_k(\bf{\mu},\bf{\Sigma})$. The probability density function of such a multivariate Gaussian distribution is defined as
\begin{equation}
    p_{\bf{X}}({\bf{x}}) = \frac{1}{\sqrt{(2\pi)^k|\bf{\Sigma}|}}\exp \left\\{-\frac{1}{2} ({\bf{x}}-\bf{\mu})^\top \bf{\Sigma}^{-1}({\bf{x}}-\bf{\mu})\right\\},
\end{equation}
where $|\bf{\Sigma}|$ is the determinant of the covariance matrix. Please note the similarities between the univariate Gaussian distribution and the multivariate distribution. The inverse covariance matrix $\bf{\Sigma}^{-1}$ is often also called the <i>precision matrix</i> and is denoted by $\bf{\Lambda}$, because a low variance (i.e. low spread) relates to high precision and vice versa.

#### The covariance matrix of a multivariate Gaussian distribution
The probability density function of a Gaussian distribution is fully determined by its mean $\bf{\mu}$ and its covariance matrix $\bf{\Sigma}$. In order to give some intuition on how the mean and covariance matrix structure influence the final distribution, we jump forward to Fig. 2 in <a href="../mathematicalbackground_probability_vectors/#correlation-coefficient">the next section</a> where three multivariate distributions have been plotted. The covariance matrices that were used to plot these distributions in the figure are from left to right:
\begin{equation}
    \bf{\Sigma}\_1 = \begin{bmatrix}1 & -0.5 \newline -0.5 & 1\end{bmatrix} \qquad \bf{\Sigma}\_2 = \begin{bmatrix}1 & 0 \newline 0 & 1\end{bmatrix} \qquad \bf{\Sigma}\_3 = \begin{bmatrix}1 & 0.5 \newline 0.5 & 1\end{bmatrix}
\end{equation}
Please note how the off-diagonal entries, referring to Cov$[X_1,X_2]$ and Cov$[X_2,X_1]$ influence the shape of the distribution.

In order to understand how the covariance matrix is related to the tilt and the shape of the distribution, we need to first introduce the so-called rotation matrix and the eigenvalue decomposition. The rotation matrix $R_\theta$ rotates a coordinate counter-clockwise over an angle $\theta$ with respect to the origin. This rotation matrix is defined as
\begin{equation}\label{eq:rot_mat}
    R_\theta = \begin{bmatrix} \cos(\theta) & -\sin(\theta) \newline \sin(\theta) & \cos(\theta) \end{bmatrix}
\end{equation}
and a rotation of $\theta$ from the coordinates $(x,y)$ to the coordinates $(x', y')$ can be represented by
\begin{equation}
    \begin{bmatrix} x' \newline y' \end{bmatrix} = R_\theta \begin{bmatrix} x \newline y \end{bmatrix} = \begin{bmatrix} x\cos(\theta) - y\sin(\theta) \newline x\sin(\theta) + y\cos(\theta) \end{bmatrix}.
\end{equation}
One of the properties of a rotation matrix is that it is orthogonal. This means that $R_\theta R_\theta^\top = I$, where $I$ is the identity matrix. Using the fact that $R_\theta^{-1}= R_{-\theta} = R_\theta^\top$ from its definition, the orthogonality property makes complete sense, because rotating a coordinate with the angle $-\theta$ and $\theta$ respectively does not change anything.

Besides the rotation matrices, we need to introduce the eigenvalue decomposition in order to better understand the covariance matrix structure. The eigenvalue decomposition states that a square invertible symmetric matrix $A$ can be written as
\begin{equation}
    A = Q\Lambda Q^{-1},
\end{equation}
where the orthogonal matrix $Q$ contains the eigenvectors of $A$ and $\Lambda$ is a diagonal matrix containing the eigenvalues of $A$.

Now the general representation of the rotation matrix has been defined as well as the eigenvalue decomposition, we can show that <i>any covariance matrix can be written as the rotations of a diagonal covariance matrix</i>. This point is very important to understand. To start off, a diagonal covariance matrix can be represented as
\begin{equation}
    \bf{\Sigma}\_d = \begin{bmatrix} a & 0 \newline 0 & b \end{bmatrix}.
\end{equation}
The entries $a$ and $b$ correspond to the individual variances of $X_1$ and $X_2$ according to the definitions and are at the same time the eigenvalues of $\bf{\Sigma}\_d$. An example of a Gaussian distribution that corresponds to a diagonal covariance matrix where $a = 25$ and $b=4$ is shown on the left in the figure below. Please note that the ratio of $\sqrt{a}$ and $\sqrt{b}$ also represents the ratio of the length (the major axis) and the width (the minor axis) of the distribution.
\par
If we were to apply the eigenvalue decomposition to a covariance matrix $\bf{\Sigma}$, we would interestingly enough find that
\begin{equation}
    \bf{\Sigma} = R_\theta \bf{\Sigma}_d R_\theta^\top.
\end{equation}
The right of the figure below shows an example of a multivariate Gaussian distribution whose covariance matrix is a rotated version of the diagonal covariance matrix corresponding to the left side of the same figure. From this we can see that the ratio of eigenvalues of $\bf{\Sigma}$ corresponds to the ratio of the lengths of the major and minor axes. Furthermore, we can conclude that the matrix containing the eigenvectors of $\bf{\Sigma}$ is at the same time a rotation matrix, implicitly defining the rotation angle.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/gaussiandiag.svg"
      alt="Two multivariate Gaussian distribution, whose covariance matrices are related through the rotation matrices corresponding to a counter-clockwise rotation of $\pi/4$ radians."
    />
    <figcaption>
      Two multivariate Gaussian distribution, whose covariance matrices are related through the rotation matrices corresponding to a counter-clockwise rotation of $\pi/4$ radians.
    </figcaption>
  </figure>
</div>


<br></br>

### The continuous Uniform(a,b) distribution
The continuous Uniform distribution is a continuous probability distribution that models an experiment where the outcomes are mapped only to the interval from $a$ up to and including $b$, with the same probability all over this range. The distribution is fully characterized by the parameters $a$ and $b$, which are the continuous lower and upper bound of the interval respectively.

<figure>
<div class="rowimg2">
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_uniform_pdf.svg"
    style="width:100%">
  </div>
  <div class="columnimg2">
    <img src="/../files/7.Images/math/probability/continuous_uniform_cdf.svg"
    style="width:100%">
  </div>
</div>
<figcaption>
  Example plot of the (a) probability density function and (b) cumulative density function of the continuous Uniform(a,b) distribution.
</figcaption>
</figure>

<div class="example">
  <!---->
  <h4> Probability density function </h4>
    <!---->
    The probability density function of the continuous Uniform(a,b) distribution is given as
    \begin{equation}
        p_X(x) =
        \begin{cases}
            \frac{1}{b-a},  &\text{for }a \leq x \leq b \\
            0,              &\text{otherwise}
        \end{cases},
    \end{equation}
    where $b > a$.
    <!---->
</div>


<div class="example">
  <!---->
  <h4> Cumulative distribution function </h4>
    <!---->
    The cumulative distribution function of the continuous Uniform(a,b) distribution can be determined as
    \begin{equation}
        \begin{split}
            P_X(x)
            &=
            \begin{cases}
                0                  &\text{for } x\leq a \\
                \frac{x-a}{b-a}    &\text{for } a < x < b \\
                1                  &\text{for } x\geq b
            \end{cases}
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation*}
        \begin{split}
            P_X(x)
            &= \int_{-\infty}^{x} p_X(n) \mathrm{d}n, \\
            &=
            \begin{cases}
                0,                              &\text{for } x\leq a \\
                \int_{a}^{x} \frac{1}{b-a} \mathrm{d}n,  &\text{for } a < x < b \\
                1,                              &\text{for } x\geq b
            \end{cases} \\
            &=
            \begin{cases}
                0                  &\text{for } x\leq a \\
                \frac{x-a}{b-a}    &\text{for } a < x < b \\
                1                  &\text{for } x\geq b
            \end{cases}
        \end{split}
    \end{equation*}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Expected value </h4>
    <!---->
    The expected value of the continuous Uniform(a,b) distribution can be determined as
    \begin{equation}
        \begin{split}
            \mathbb{E}[X] = \frac{a+b}{2}.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \mathbb{E}[X]
            &= \int_{-\infty}^{\infty} x \cdot p_X(x) \mathrm{d}x, \\
            &= \int_a^b x\frac{1}{b-a} \mathrm{d}x, \\
            &= \frac{1}{b-a}\left[\frac{1}{2}x^2 \right]_a^b, \\
            &= \frac{1}{b-a} \cdot \left(\frac{1}{2}b^2 - \frac{1}{2}a^2\right) = \frac{(b-a)(b+a)}{2(b-a)} = \frac{a+b}{2}.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>


<div class="example">
  <!---->
  <h4> Variance </h4>
    <!---->
    The variance of the continuous Uniform(a,b) distribution can be determined as
    \begin{equation}
        \begin{split}
            \text{Var}[X]  = \frac{1}{12}(b-a)^2.
        \end{split}
    \end{equation}
    <!---->
  <button class="collapsible">Show proof</button>
  <!---->
  <div class="content">
    <!---->
    \begin{equation}
        \begin{split}
            \text{Var}[X]
            &= \mathbb{E}[X^2] - \mathbb{E}[X]^2, \\
            &= \int_{-\infty}^{\infty} x^2 \cdot p_X(x) \mathrm{d}x - \frac{(a+b)^2}{4}, \\
            &= \int_a^b x^2 \frac{1}{b-a} \mathrm{d}x - \frac{(a+b)^2}{4}, \\
            &= \frac{1}{b-a}\left[ \frac{1}{3}x^3\right]_a^b - \frac{(a+b)^2}{4}, \\
            &= \frac{1}{b-a}\left( \frac{1}{3}b^3 - \frac{1}{3}a^3\right) - \frac{(a+b)^2}{4}, \\
            &= \frac{b^3-a^3}{3(b-a)} - \frac{(a+b)^2}{4}, \\
            &= \frac{4b^3-4a^3}{12(b-a)} - \frac{3(a^2 + b^2 + 2ab)(b-a)}{12(b-a)}, \\
            &= \frac{4b^3 - 4a^3 - 3a^2b + 3a^3 -3b^3 +3b^2a -6ab^2 +6a^2b}{12(b-a)}, \\
            &= \frac{b^3 - a^3 + 3a^2b  -3ab^2 }{12(b-a)} = \frac{(b-a)^3}{12(b-a)} = \frac{1}{12}(b-a)^2.
        \end{split}
    \end{equation}
    <!---->
  </div>
</div>
