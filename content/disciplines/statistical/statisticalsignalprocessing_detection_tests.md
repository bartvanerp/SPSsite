+++
title = "Statistical tests"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-01-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Statistical tests"        # name of this item in that menu
  weight = 83                          # location in that menu
  parent = "Detection theory"

+++

## Statistical hypothesis testing
Thus far we have discussed a rather ideal and simple situation, where everything about the environment was known. There were two hypotheses available to perform tests on and the distributions of these hypotheses were known. The decision of which hypothesis we regarded as true was determined by the likelihood ratio, which told us how likely our observations were for both hypotheses.

The ideality of the above approach is not only its strength, but also its weakness. In many applications this approach cannot be performed, because it might be the case that the signal distributions are unavailable. Therefore we need to resort to another method for performing the hypothesis testing.

<br></br>

## Problem statement
Suppose that we have a group of observation and we know that this group of observations can be modelled as a Gaussian distribution with mean $\mu_0$. At a certain point in time something happens to the observation generating process. Now is it unknown what the effect on the population is and how it influences our observations. If we would like to know whether the mean of the Gaussian distribution has changed then we could formulate hypotheses about it. When we expect that nothing has changed we could formulate the null hypotheses $\mathcal{H}_0$ as
\begin{equation}
    \mathcal{H}_0:\qquad \mu_0=\mu,
\end{equation}
which states that the new mean $\mu$ is simply equal to the previously determined mean $\mu_0$. Similarly the alternative hypothesis $\mathcal{H}_1$ can be defined as
\begin{equation}
    \mathcal{H}_1:\qquad \mu_0\neq\mu.
\end{equation}
This type of hypothesis test is called a <i>two-sided</i> test, since the new $\mu$ can both be significantly smaller or larger than $\mu$ in order to decide for the alternative hypothesis.

Now suppose that the above hypotheses are the only known facts that we have about the situation, except for the fact that the observations are always definitely Gaussian distributed. How do we make sense of all these uncertainties and when do we decide for one hypothesis over another?

<br></br>

## Student t-statistic
The answer was provided by William Sealy Gosset who performed research under the pseudonym "student". He came up with a random variable $t$ which was a measure for this dissimilarity. The <i>t-statistic</i> is defined as
\begin{equation}
    t = \frac{\bar{x}-\mu_0}{s/\sqrt{N}},
\end{equation}
where $\bar{x}$ is the sample mean, $\mu_0$ is the expected true mean under the null hypothesis, $s$ the square root of the unbiased variance estimator, of which a discussion will follow shortly, and $N$ is the amount of observed samples.

When observing $N$ new samples, the value calculated as $t$ provides us with information on how significantly the approximated mean value of the new samples deviates from the expected mean value under the null hypothesis.

<div class="video-container">
<iframe width="100%"; height="100%"; src="https://www.youtube.com/embed/sFd5d3j_3oo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"; allowfullscreen></iframe>
</div>

### Derivation of the t-statistic
Recall from the reader on random variables that it was possible to normalize a random variable $Y\sim\mathcal{N}(\mu_Y, \sigma_Y^2)$ to the random variable $X\sim\mathcal{N}(0,1)$ by the definition
\begin{equation}\label{eq:z}
    X = \frac{Y-\mu_Y}{\sigma_Y} = \frac{Y - \mathrm{E}[Y]}{\sqrt{\text{Var}[Y]}}.
\end{equation}
By performing this normalization, the probability density function does no longer depend on the mean or variance of the original random variable $Y$. Therefore the random variable $X$ is also called a <i>pivotal quantity</i>, which is a quantity whose distribution does not depend on its (unknown) parameters.

We can perform a similar operation when regarding the sample mean $\bar{x}$ as the random variable which we would like to normalize. Let us define the variable $t$ as the normalized random variable as
\begin{equation}
    t = \frac{\bar{x}-\mathrm{E}[\bar{x}]}{\sqrt{\text{Var}[\bar{x}]}}.
\end{equation}
In order to calculate $t$, the mean and variance of $\bar{x}$ need to be determined. The expected value of the sample mean $\bar{x}$, which is an estimate of the real mean defined as
\begin{equation}
    \bar{x} = \frac{1}{N}\sum_{i=1}^N x_i
\end{equation}
can be determined as
\begin{equation}
    \begin{split}
        \mathrm{E}[\bar{x}]
        &= \mathrm{E}\left[\frac{1}{N}\sum_{i=1}^N x_i\right],\newline
        &= \frac{1}{N}\sum_{i=1}^N \mathrm{E}\left[x_i\right],\newline
        &= \frac{1}{N}N\mu_0 = \mu_0.
    \end{split}
\end{equation}
And the corresponding variance can be determined as
\begin{equation}
    \begin{split}
        \text{Var}[\bar{x}]
        &= \text{Var}\left[\frac{1}{N}\sum_{i=1}^N x_i\right], \newline
        &= \frac{1}{N^2}\text{Var}\left[\sum_{i=1}^N x_i\right], \newline
        &= \frac{1}{N^2}\sum_{i=1}^N\text{Var}[x_i], \newline
        &=\frac{1}{N}\text{Var}[x_i],
    \end{split}
\end{equation}
where we use the assumption that the samples $x_i$ are uncorrelated from each other and therefore it holds that $\text{Var}[x_1 + x_2] = \text{Var}[x_1] + \text{Var}[x_2]$. This derivation, however, gives rise to the problem that the variance of $x_i$ is actually unknown. Therefore this variance is estimated using the unbiased sample variance estimator $s^2$ as $\text{Var}[x_i]\approx s^2$.

Using the derivations from above, the $t$-statistic can now be derived as
\begin{equation}\label{eq:t}
    t = \frac{\bar{x}-\mathrm{E}[\bar{x}]}{\sqrt{\text{Var}[\bar{x}]}} = \frac{\bar{x}-\mu_0}{s/\sqrt{N}}.
\end{equation}
The term $\bar{x}-\mu_0$ provides us with the absolute deviation from our estimated mean value to the expected mean value. The term $s/\sqrt{N}$ can be regarded as the estimated standard deviation of the estimated mean value. It is also known as the <i>standard error</i> of the mean. Although the variance of the individual samples is estimated, the $t$-statistic is still a pivotal quantity and can therefore be used to generalize every problem with a similar hypothesis.

### Unbiased sample variance estimator
So previously we have introduced the unbiased sample mean variance estimator $s^2$, which is defined as
\begin{equation}\label{eq:est_var_un}
    s^2 = \frac{1}{N-1} \sum_{i=1}^N (x_i-\bar{x})^2.
\end{equation}
One might wonder why there is a term $\frac{1}{N-1}$ in the definition, since normally it is $\frac{1}{N}$. The reason for this is that the variance estimator of the sample mean would be biased when using the factor $\frac{1}{N}$. In order to show this the biased sample variance estimator $\hat{\sigma}^2$ is defined as
\begin{equation}
    \hat{\sigma}^2 = \frac{1}{N}\sum_{i=1}^N (x_i-\bar{x})^2.
\end{equation}
If this estimator were to be unbiased then the expected value of this variance estimator would represent the true variance. When deriving the expected value of this biased variance estimator as
\begin{equation}
    \begin{split}
        \mathrm{E}[\hat{\sigma}^2]
        &= \mathrm{E}\left[\frac{1}{N}\sum_{i=1}^N(x_i-\bar{x})^2\right], \newline
        &= \frac{1}{N} \mathrm{E}\left[\sum_{i=1}^N \left((x_i-\mu_0)-(\bar{x}-\mu_0)\right)^2\right], \newline
        &= \frac{1}{N} \mathrm{E}\left[\sum_{i=1}^N \left((x_i-\mu_0)^2 -2(x_i-\mu_0)(\bar{x}-\mu_0) + (\bar{x}-\mu_0)^2\right)\right], \newline
        &= \frac{1}{N}\mathrm{E}\left[\sum_{i=1}^N\left(x_i-\mu_0\right)^2 -2(\bar{x}-\mu_0)\sum_{i=1}^N(x_i-\mu_0) + (\bar{x}-\mu_0)^2\sum_{i=1}^N1\right], \newline
        &= \frac{1}{N}\mathrm{E}\left[\sum_{i=1}^N\left(x_i-\mu_0\right)^2 -2(\bar{x}-\mu_0)N(\bar{x}-\mu_0) + N(\bar{x}-\mu_0)^2\right], \newline
        &= \frac{1}{N}\mathrm{E}\left[\sum_{i=1}^N\left(x_i-\mu_0\right)^2  -N(\bar{x}-\mu_0)^2\right], \newline
        &= \frac{1}{N}\left(\sum_{i=1}^N\mathrm{E}\left[\left(x_i-\mu_0\right)^2\right]  -N\mathrm{E}\left[(\bar{x}-\mu_0)^2\right]\right), \newline
        &= \frac{1}{N}\left(N\text{Var}[x_i]  -N\text{Var}[\bar{x}]\right), \newline
        &= \frac{1}{N}\left(N\text{Var}[x_i] - N\frac{1}{N}\text{Var}[x_i]\right), \newline
        &= \frac{N-1}{N}\text{Var}[x_i],
    \end{split}
\end{equation}
we have indeed proven that this estimator is biased. When the amount of samples increases, this bias will decrease, but still there is a bias present in this estimator. To solve this problem the estimator has to be multiplied with a factor $\frac{N}{N-1}$, which leads to the unbiased estimator.

<br></br>

## Student's t distribution
The $t$-statistic can be regarded as the normalized sample mean, where the variance is approximated with the unbiased sample variance estimator. Because of this approximation the probability density function of $t$ does not follow the standard normal $\mathcal{N}(0,1)$ distribution, but instead it follow the Student's $t$ distribution.

<div style="max-width: 900px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/information/detection/tdistribution.svg"
      alt="Visualisation of the concept of covariance."
    />
    <figcaption class="numbered">
      The Student's $t$ distribution plotted for several degrees of freedom $v$ in blue. In red the standard normal distribution is represented. It can be noted that for a large $v$ the Student's $t$ distribution approaches the standard normal distribution.
    </figcaption>
  </figure>
</div>

The probability density function of the newly defined variable $t$ can be determined as
\begin{equation}
    p(t|\nu) = \frac{\Gamma\left(\frac{\nu+1}{2}\right)}{\Gamma\left(\frac{\nu}{2}\right)}\frac{1}{\sqrt{\nu\pi}}\left(1+\frac{t^2}{\nu}\right)^{-\frac{\nu-1}{2}},
\end{equation}
where $v$ is the degrees of freedom, which is equal to $N-1$, and where $\Gamma$ is the gamma function. The proof of this probability density function is beyond the scope of this reader. This distribution returns the probability that a set of samples do not belong to the distribution with mean $\mu_0$ as formulated in the null hypothesis.

Fig. 1 shows the $t$ distribution for several degrees of freedom. It can be noted that as the amount of samples increases, our estimate of the variance improves. Therefore the approximation that was performed in the definition of $t$ becomes more valid and the distribution approaches the standard normal distribution. In the beginning one could say that there is still a large uncertainty about the variance of the distribution, which can be seen from Fig. 1 by its wider tails.

### Hypothesis testing
When testing the original hypothesis a certain threshold has to be placed on the probability of observing a significantly different mean. This probability $p$ can be translated to a $t$ value by using the definition of the $t$ distribution. Finally the $t$-statistic can be used to compare the actual situation with the $t$ threshold value(s) in order to make a statement about its significance.

As an example we have the same two-sided hypothesis test as described in the beginning of this section and we would like to know whether our observations are within the 95% confidence interval. This means that the null hypothesis is rejected when the observations are mapped onto the unlikeliest 5% of the probability density function. Since we are performing a two-sided test, this 5% is equally divided in the lowest segment where the total probability does not exceed 2.5% $P(x)<0.025$) and in the highest segment where the total probability does not exceed 2.5% ($P(x)>0.975$). This equal division is only allowed when dealing with symmetric probability density functions. In other words, we reject the null hypothesis when the observations are in the outer regions of the probability density function. These probabilities can be converted into a $t$ value depending on the degrees of freedom $v$ and this $t$ value can be used to compare the $t$ value with which is obtained from the measurements.

<br></br>

## Extension to multivariate case
The $t$ test can be extended to the case where we are dealing with linear models. Linear models are defined as
\begin{equation}
    {\bf{x}} = {\bf{H}}{\bf{\theta}} + {\bf{\epsilon}},
\end{equation}
where ${\bf{x}}$ are the observation samples, ${\bf{H}}$ is the deterministic observation matrix, which tells us what the original process might have been, ${\bf{\theta}}$ are the linear parameters of the model and where ${\bf{\epsilon}}$ are the noise samples.

For the null hypothesis it can be assumed that there is no correlation between ${\bf{H}}$ and ${\bf{x}}$ and that ${\bf{x}}$ therefore purely consist out of noise. This can be represented by the hypothesis ${\bf{\theta}} = {\bf{0}}$. For each of the individual parameters of the estimated $\hat{{\bf{\theta}}}$ we can calculate the $t$-statistic to verify whether there actually is no correlation present. In order to calculate this statistic the covariance matrix ${\bf{\Sigma}}$ of $\hat{{\bf{\theta}}}$ is required. The $t$ value for the $k^\text{th}$ element can be determined by
\begin{equation}
    t_k = \frac{{\bf{c}}\_k^\top \hat{{\bf{\theta}}}}{\sqrt{{\bf{c}}\_k^\top {\bf{\Sigma}}^{-1}_{\hat{{\bf{\theta}}}}{\bf{c}}_k^\top}},
\end{equation}
where ${\bf{c}}_k$ is a vector that can is used to select a single element of $\hat{{\bf{\theta}}}$. The vector only consists of zeros, except for a single 1 at the location of the desired element.
