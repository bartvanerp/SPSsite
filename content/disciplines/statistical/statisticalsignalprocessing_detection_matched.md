+++
title = "Matched filter"         # name of webpage

# date = {{ .Date }}
lastmod = 2020-01-04

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.statistical]                       # name of menu section (main module)
  name = "Matched filter"        # name of this item in that menu
  weight = 82                           # location in that menu
  parent = "Detection theory"

+++


## From signal samples to signals
So previously the main concepts discussed were about the detection of a signal sample in noise. In this case the detection was performed for each individual sample and for each individual sample a different hypothesis was valid. This was denoted by the indexing $[n]$.

This section discusses a more realistic situation, where we would like to know whether we have received a deterministic signal consisting of multiple samples. The deterministic signal of length $N$ is denoted using a bold identifier as the vector
\begin{equation}
    {\bf{s}} = \left[s[0], s[1], \ldots, s[N-1]\right]^\top,
\end{equation}
where it would be more suitable to also index $\bf{s}$, but where it is omitted for simplicity. Similarly the received signal and the noise signal can be described as
\begin{equation}
    {\bf{x}} = \left[x[0], x[1], \ldots, x[N-1]\right]^\top,
\end{equation}
and
\begin{equation}
    {\bf{\epsilon}} = \left[\epsilon[0], \epsilon[1], \ldots, \epsilon[N-1]\right]^\top.
\end{equation}
It is now also assumed that the hypotheses are valid for the entire signal duration instead of for just a single sample. This is denoted by the boldface ${\bf{\mathcal{H}}}_i$. So as an example this notation allows us to write the probability of receiving the signal $\bf{x}$ when a deterministic signal is actually present as $p(\bf{x}\mid\bf{\mathcal{H}}_1)$.

<br></br>

## Likelihood ratio model
The extension from random samples to random signals is a rather straightforward step for real world applications. So now the question arises how we can perform the hypothesis testing for random vectors, where the probability density functions are now multivariate?

The answer to this question has already been presented in the section on <a href="../../information/informationandcommunication_detection_hypothesis/">hypotesis testing</a>, where this likelihood ratio for binary hypothesis testing can be extended to multivariate probability density functions. Deciding for a detection, meaning that $\bf{\mathcal{H}}_1$ is regarded to be true, occurs when
\begin{equation}\label{eq:prob_ratio_multi}
    L(\bf{x}) = \frac{p(\bf{x}\mid\bf{\mathcal{H}}_1)}{p(\bf{x}\mid\bf{\mathcal{H}}_0)} > \gamma
\end{equation}
holds. The corresponding decision boundary can be represented by a line for the bivariate case as shown in Fig. 4 of <a href="../../information/informationandcommunication_detection_hypothesis/">the previous section</a> or an $N$-dimensional surface for random vectors of length $N$.

Let us now model these multivariate probability density functions. In order to do so, multiple assumptions about the noise components have to be made.

### Zero-mean Gaussian noise
First we assume that each individual sample has a zero-mean Gaussian noise component, which is supported by the central limit theorem. Secondly it is assumed that each noise sample has the identical variance $\sigma^2$ and there is no correlation between the noise samples. This results in a simplified diagonal covariance matrix $\bf{\Sigma} = \sigma^2I_N$, where $I_N$ is the identity matrix of size $N\times N$. These assumptions lead to the probability density functions of each individual sample defined as
\begin{equation}\label{eq:pdf_gauss1}
    p(x[n]\mid\mathcal{H}_0[n]) = \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x[n])^2}{2\sigma^2}}
\end{equation}
for the case when no deterministic signal is present and
\begin{equation}\label{eq:pdf_gauss2}
    p(x[n]\mid\mathcal{H}_1[n]) = \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x[n]-s[n])^2}{2\sigma^2}}
\end{equation}
for the case when a deterministic signal is present.

### Chain rule of probability
Before determining $p(\bf{x}|\bf{\mathcal{H}}_i)$ formally, the chain rule of probability has to be introduced. This is mere a expansion of the definition of joint and conditional probabilities, which was generally defined as
\begin{equation}\label{eq:cond_prob}
    \Pr[A,B] = \Pr[A \mid B] \cdot \Pr[B].
\end{equation}
The chain rule of probability allows for the factorization of multivariate probability density functions. An example will demonstrate its use. Consider the received signal $\bf{x} = [x_1, x_2, x_3, x_4]^\top$. Using the previous equation the multivariate probability density function $p(\bf{x})$ can be factored as
\begin{equation}
    \begin{split}
        p(\bf{x})
        &= p(x_1,x_2,x_3,x_4), \newline
        &= p(x_1\mid x_2,x_3,x_4)p(x_2,x_3,x_4), \newline
        &= p(x_1\mid x_2,x_3,x_4)p(x_2\mid x_3,x_4)p(x_3,x_4), \newline
        &= p(x_1\mid x_2,x_3,x_4)p(x_2\mid x_3,x_4)p(x_3\mid x_4)p(x_4).
    \end{split}
\end{equation}



### Independent noise samples

The reason of introducing the chain rule of probability is to show that multivariate probability density functions can become increasingly complex when the dimensionality increases. This dimensionality is equal to the length of the signal vector. Oftentimes the conditional probabilities of the noise are unknown, making it virtually impossible to calculate the exact value of $p(\bf{x}\mid\bf{\mathcal{H}}_i)$.

To simplify the calculation we resort to a third assumption stating that the samples are independently distributed. This means that a sample does not depend on previous samples, simplifying the definition of a joint probability as
\begin{equation}
    \Pr[A,B] = \Pr[A]\cdot \Pr[B].
\end{equation}
Using this assumption, the joint multivariate probability density function $p(\bf{x}\mid\bf{\mathcal{H}}\_i)$ can now be written as
\begin{equation}\label{eq:prob_fact}
    \begin{split}
        p(\bf{x}\mid\bf{\mathcal{H}}\_i)
        &= p(x[0]\mid {\bf{\mathcal{H}}}\_i) \cdot p(x[1]\mid {\bf{\mathcal{H}}}\_i) \cdot \ldots \cdot p(x[N-1]\mid \bf{\mathcal{H}}\_i), \newline
        &= \prod_{k=0}^{N-1}p(x[k]\mid\bf{\mathcal{H}}\_i),
  \end{split}
\end{equation}
where $\prod\cdot$ denotes the product operator, which is the multiplication variant of the summation operator $\sum\cdot$.

### Multivariate probability density function
Now that assumptions have been made about the signal, it is time to define $p(\bf{x}\mid\bf{\mathcal{H}}\_0)$ and $p(\bf{x}\mid\bf{\mathcal{H}}\_1)$. Using the probability density function of the signal samples and the factorization above the probability density function $p(\bf{x}\mid\bf{\mathcal{H}}\_0)$ can be written as
\begin{equation}
    p({\bf{x}}\mid{\bf{\mathcal{H}}}\_0) = \prod_{k=0}^{N-1} \frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x[k])^2}{2\sigma^2}} = (2\pi\sigma^2)^{-\frac{N}{2}}\prod_{k=0}^{N-1} e^{-\frac{(x[k])^2}{2\sigma^2}}.
\end{equation}
Using the mathematical identity $e^a\cdot e^b = e^{a+b}$, the final probability density functions of $p({\bf{x}}\mid{\bf{\mathcal{H}}}\_0)$ and $p({\bf{x}}\mid{\bf{\mathcal{H}}}\_1)$ can be written as
\begin{equation}\label{eq:pdf_final1}
    p({\bf{x}}\mid{\bf{\mathcal{H}}}\_0) = (2\pi\sigma^2)^{-\frac{N}{2}} \exp\left\\{-\frac{1}{2\sigma^2}\sum_{k=0}^{N-1}(x[k])^2\right\\}
\end{equation}
and
\begin{equation}\label{eq:pdf_final2}
    p({\bf{x}}\mid{\bf{\mathcal{H}}}\_1) = (2\pi\sigma^2)^{-\frac{N}{2}} \exp\left\\{-\frac{1}{2\sigma^2}\sum_{k=0}^{N-1}(x[k]-s[k])^2\right\\}
\end{equation}
respectively.

### Likelihood ratio
Now finally the probability density functions have been defined we can return to the previously defined likelihood ratio. Using above equations this ratio now simplifies to
\begin{equation}\label{eq:prob_ratio_match}
    \begin{split}
        L({\bf{x}})
        &= \frac{p({\bf{x}}\mid{\bf{\mathcal{H}}}\_1)}{p({\bf{x}}\mid{\bf{\mathcal{H}}}\_0)}, \newline
        &= \frac{\exp\left\\{-\frac{1}{2\sigma^2}\sum_{k=0}^{N-1}(x[k]-s[k])^2\right\\}}{\exp\left\\{-\frac{1}{2\sigma^2}\sum_{k=0}^{N-1}(x[k])^2\right\\}}, \newline
        &= \exp\left\\{-\frac{1}{2\sigma^2}\left(\sum_{k=0}^{N-1}(x[k]-s[k])^2-\sum_{k=0}^{N-1}(x[k])^2\right)\right\\} > \gamma.
    \end{split}
\end{equation}
In order to simplify the notation, we introduce $l({\bf{x}})$ which is the natural logarithm of $L({\bf{x}})$ and we decide for $\bf{\mathcal{H}}\_1$ if
\begin{equation}
    l({\bf{x}}) = \ln\left(L({\bf{x}})\right) = -\frac{1}{2\sigma^2}\left(\sum_{k=0}^{N-1}(x[k]-s[k])^2-\sum_{k=0}^{N-1}(x[k])^2\right) > \ln(\gamma)
\end{equation}
holds. After getting rid of the brackets, the following expression can be obtained as
\begin{equation}
    \frac{1}{2\sigma^2}\sum_{k=0}^{N-1}2x[k]s[k] -\frac{1}{2\sigma^2}\sum_{k=0}^{N-1}(s[k])^2 > \ln(\gamma).
\end{equation}
Rearranging the terms provides us with a more insightful decision criterion for $\bf{\mathcal{H}}_1$. So we should decide for $\bf{\mathcal{H}}_1$ if
\begin{equation}\label{eq:match}
    \underbrace{\sum_{k=0}^{N-1}x[k]s[k]}_{\substack{\text{unnormalized}\newline \text{cross-correlation}}} > \sigma^2\ln(\gamma) + \frac{1}{2}\underbrace{\sum_{k=0}^{N-1}(s[k])^2}_{\substack{\text{unnormalized}\newline \text{auto-correlation} \newline \text{or} \newline \text{signal energy for} \newline \text{real-valued signals}}}=\gamma'
\end{equation}
holds. From this equation we can observed two things. Firstly, the right-hand side of the equation can be determined before receiving any signal, since it does not depend on $\bf{x}$. Therefore this corresponds to a fixed value $\gamma'$ if $\bf{s}$ does not change over time. The parameter $\gamma'$ is called <i>the modified threshold of the Neyman-Pearson detector</i>. Secondly, the left-hand side has to be calculated during the reception of a signal. This value has to be calculated for each new signal sample received and is also known as the <i>test statistic</i>. The value that needs to be calculated for each new sample indexed by $n$ can be described as
\begin{equation}\label{eq:output}
    y[n] = \sum_{k=0}^{N-1}x[k+n]s[k]
\end{equation}
Luckily the operation is relatively inexpensive, because the unnormalized cross-correlation can be implemented in an FIR-filter as a convolution. If an arbitrary FIR filter has an impulse response $h[k]$, its output $y[k]$ can be determined as
\begin{equation}\label{eq:conv}
    y[n] = x[n] \ast h[n] = \sum_{k=0}^{N-1} h[k]x[n-k] = \sum_{k=0}^{N-1} x[k]h[n-k].
\end{equation}
Now the only design decision that we have to make is how we should define our impulse response $h[n]$. Comparison of both equations provides us with equations for $h[n]$ that give the optimal solution, namely
\begin{equation}
    h[n] = s[N-1-n],
\end{equation}
which corresponds to an impulse response that is the temporally mirrored deterministic signal. Filters designed with this specific impulse response and which are operated in the way described above are called <i>matched filters</i>.

<br></br>

## Performance of matched filters
So previously we have extended the probability ratio as described by the Neyman-Pearson theorem to the multivariate case and after several assumptions, we derived the decision criterion of a matched filter. This matched filter convolves the received signal $\bf{x}$ with a temporally mirrored version of the known deterministic signal $\bf{s}$ in order to determine how well they match and compares it with a modified threshold. This threshold consists of half the deterministic signal power $E_s$ and a user-determined constant.

The perceived optimality of the matched filter requires further analysis in order to determine its performance. Suppose we have a filter creating the output of the unnormalized correlation between the received signal and the expected deterministic signal, then this filter its output can be described as
\begin{equation}
    y({\bf{x}}) = \sum_{k=0}^{N-1} x[k]s[k] =
    \begin{cases}
        \displaystyle \sum_{k=0}^{N-1} \epsilon[k]s[k],       &\text{under }{\bf{\mathcal{H}}}_0 \newline
        \displaystyle \sum_{k=0}^{N-1} (s[k]+\epsilon[k])s[k],    &\text{under }{\bf{\mathcal{H}}}_1
    \end{cases}
\end{equation}
where a distinction is made for both hypotheses. From this expression it can be noted that the output is a sum of modulated Gaussian distributed samples. Therefore $y(\bf{x})$ must also be Gaussian distributed. So because $y(\bf{x})$ follows two Gaussian distributions depending on which hypothesis is true and because this term is consecutively compared with $\gamma'$, its performance can be evaluated similarly as here.

In order to relate the value of $\gamma'$ with the performance probabilities, the Gaussian probability density functions of $y(\bf{x})$ need to be determined. Using the zero-mean assumption of the noise, the expected value of the output can be determined under both hypotheses as
\begin{equation}
    \mathrm{E}\left[y({\bf{x}})\mid {\bf{\mathcal{H}}}\_0\right] = \mathrm{E}\left[\sum_{k=0}^{N-1} \epsilon[k]s[k]\right] = \sum_{k=0}^{N-1} s[k]\mathrm{E}\left[\epsilon[k]\right] = 0
\end{equation}
and as
\begin{equation}
    \begin{split}
        \mathrm{E}\left[y({\bf{x}})\mid {\bf{\mathcal{H}}}_1\right]
        &= \mathrm{E}\left[\sum_{k=0}^{N-1} \left(\epsilon[k]+s[k]\right)s[k]\right], \newline
        &= \sum_{k=0}^{N-1}\left(s[k]\right)^2 + \sum_{k=0}^{N-1} s[k]\mathrm{E}\left[\epsilon[k]\right], \newline
        &= \sum_{k=0}^{N-1}\left(s[k]\right)^2 = E_s,
    \end{split}
\end{equation}
where $E_s$ is the signal energy. Now let us determine the variance of $y(\bf{x})$ in a similar fashion as
\begin{equation}
    \begin{split}
        \text{Var}\left[y({\bf{x}})\mid{\bf{\mathcal{H}}}_0\right]
        &= \mathrm{E}\left[\left(y({\bf{x}})\right)^2\mid{\bf{\mathcal{H}}}_0\right] - \left(\mathrm{E}\left[y({\bf{x}})\mid{\bf{\mathcal{H}}}_0\right]\right)^2, \newline
        &= \mathrm{E}\left[\left(\sum_{k=0}^{N-1} \epsilon[k]s[k]\right)^2 \right], \newline
        &=\mathrm{E}\left[\left(\sum_{k=0}^{N-1} \epsilon[k]s[k]\right)\left(\sum_{l=0}^{N-1} \epsilon[l]s[l]\right) \right], \newline
        &=\mathrm{E}\left[\sum_{k=0}^{N-1} \sum_{l=0}^{N-1}\epsilon[k]\epsilon[l] s[k]s[l] \right], \newline
        &=\sum_{k=0}^{N-1} \sum_{l=0}^{N-1}s[k]s[l]\mathrm{E}\left[\epsilon[k]\epsilon[l]  \right], \newline
        &= \sum_{k=0}^{N-1} \sum_{l=0}^{N-1}s[k]s[l] \sigma^2\delta(k-l), \newline
        &= \sigma^2 \sum_{k=0}^{N-1} s[k]s[k] = \sigma^2 E_s
    \end{split}
\end{equation}
and by noting that the variance of $y({\bf{x}})$ under $\bf{\mathcal{H}}_1$ has in the calculation just an extra deterministic constant, the variance under $\bf{\mathcal{H}}_1$ can be calculated as
\begin{equation}
\begin{split}
    \text{Var}\left[y({\bf{x}})\mid{\bf{\mathcal{H}}}_1\right]
    &= \text{Var}\left[ \sum_{k=0}^{N-1}\left(s[k]\right)^2 + \sum_{k=0}^{N-1} s[k][\epsilon[k]] \right], \newline
    &= \text{Var}\left[ \sum_{k=0}^{N-1} s[k][\epsilon[k]] \right], \newline
    &= \text{Var}\left[y({\bf{x}})\mid{\bf{\mathcal{H}}}_0\right] = \sigma^2E_s.
\end{split}
\end{equation}

The probability density functions of the output of the filter $y({\bf{x}})$ can now be represented as
\begin{equation}
    p(y({\bf{x}})) =
    \begin{cases}
        \mathcal{N}(0, \sigma^2E_s), &\text{under }{\bf{\mathcal{H}}}_0 \newline
        \mathcal{N}(E_s, \sigma^2E_s). &\text{under }{\bf{\mathcal{H}}}_1
    \end{cases}
\end{equation}

### Probabilities of detection and false alarm
The values of $\text{P}\_D$ and $\text{P}\_{FA}$ can in this case be determined respectively as
\begin{equation} \label{eq:multi_PD}
    \text{P}\_D = \int_{\gamma'}^\infty p(y({\bf{x}})\mid \mathcal{H}_1[n]) \mathrm{d}y = Q\left(\frac{\gamma'-E_s}{\sqrt{\sigma^2E_s}}\right) = Q\left(\frac{\gamma'}{\sqrt{\sigma^2E_s}} - \sqrt{\frac{E_s}{\sigma^2}}\right)
\end{equation}
and
\begin{equation} \label{eq:multi_PFA}
    \text{P}\_{FA} = \int_{\gamma'}^\infty p(y({\bf{x}})\mid \mathcal{H}_0[n]) \mathrm{d}y = Q\left(\frac{\gamma'}{\sqrt{\sigma^2E_s}}\right).
\end{equation}
So now we might ask ourselves what does our performance actually depend on? If we consider again a fixed false alarm rate, so $\text{P}\_{FA}$ is a constant, then the ratio $\frac{\gamma'}{\sqrt{\sigma^2E_s}}$ is also fixed through the previous equation. If this ratio is fixed, then it becomes clear that the term $E_s/\sigma^2$ has an influence on our probability of detection. If we now consider the fact that $\sigma^2$ is equal to the noise energy $E_\epsilon$ for white Gaussian noise, then the ratio $E_s/\sigma^2$ represent the signal-to-noise ratio (SNR). So we can conclude that our performance depends on the signal-to-noise ratio of our received signal. The noise energy solely depends on the noise variance and the signal energy depends on the deterministic signal amplitude and the length of the signal.

<br></br>

## Generalized matched filters
In the previous section the matched filter was discussed. In order to derive its performance three assumptions were made: noise is zero-mean Gaussian distributed; each noise sample has variance $\sigma^2$ and no correlation between the noise components exists; and the received samples are independent from each other.

The first assumption can be supported by the central limit theorem and the third is necessary to perform tractable calculations. The second assumption might, however, be generalized for the matched filter to make the derivation more applicable in other cases. So up until now we have discussed a very specific covariance matrix, which simplifies calculations a lot. This covariance matrix was denoted as ${\bf{\Sigma}} = \sigma^2 I_N$. In order to make the matched filter more general, this assumption is discarded and the most important consequences will be discussed in this subsection.

In this generalized case the likelihood ratio can be determined as
\begin{equation}
    L({\bf{x}}) = \frac{p({\bf{x}}\mid {\bf{\mathcal{H}}}_1)}{p({\bf{x}}\mid {\bf{\mathcal{H}}}_0)} = \frac{\exp\left\\{-\frac{1}{2}\left[\left({\bf{x}}-{\bf{s}}\right)^\top{\bf{\Sigma}}^{-1}\left({\bf{x}}-{\bf{s}}\right)\right]\right\\}}{\exp\left\\{-\frac{1}{2}\left[{\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{x}}\right]\right\\}} > \gamma
\end{equation}
and the natural logarithm of the likelihood ratio then becomes
\begin{equation}
    \begin{split}
        l({\bf{x}})
        &= \ln(L({\bf{x}})), \newline
        &= -\frac{1}{2}\left[\left({\bf{x}}-{\bf{s}}\right)^\top{\bf{\Sigma}}^{-1}\left({\bf{x}}-{\bf{s}}\right)\right] + \frac{1}{2}\left[{\bf{x}}^\top{\bf{\Sigma}}^{-1}\bf{x}\right], \newline
        &= -\frac{1}{2}\left[ {\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{x}} -2{\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{s}}  + {\bf{s}}^\top{\bf{\Sigma}}^{-1}{\bf{s}}- {\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{x}}\right], \newline
        &={\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{s}} - \frac{1}{2}{\bf{s}}^\top{\bf{\Sigma}}^{-1}{\bf{s}}>\ln(\gamma).
    \end{split}
\end{equation}
So now we can decide for ${\bf{\mathcal{H}}}_1$ if
\begin{equation}
    y({\bf{x}}) = {\bf{x}}^\top{\bf{\Sigma}}^{-1}{\bf{s}} > \ln(\gamma) + \frac{1}{2}{\bf{s}}^\top{\bf{\Sigma}}^{-1}{\bf{s}} = \gamma'
\end{equation}
holds. Keep in mind that $\gamma'$ is not the same as the one defined previously.

### Signal-to-noise ratio maximization behaviour
Suppose that a signal is again passed through an FIR-filter with filter coefficients $\bf{h}$ where for simplicity the convolution operation on the input signal $\bf{x}$ is performed by calculating the scalar output $y(\bf{x})$ as
\begin{equation}\label{eq:vec_y}
    y({\bf{x}}) = {\bf{h}}^\top {\bf{x}}.
\end{equation}
The signal-to-noise ratio of this output signal can be calculated as the squared expected amplitude of the output signal divided by the variance left on the signal due to noise as
\begin{equation}
    \begin{split}
        \text{SNR}
        &= \frac{\mathrm{E}\left[y({\bf{x}})\mid {\bf{\mathcal{H}}}_1\right]^2}{\text{Var}\left[y({\bf{x}})\mid {\bf{\mathcal{H}}}_0\right]}, \newline
        &= \frac{\mathrm{E}\left[{\bf{h}}^\top({\bf{s}}+{\bf{\epsilon}})\right]^2}{\text{Var}\left[{\bf{h}}^\top{\bf{\epsilon}}\right]}, \newline
        &= \frac{\left({\bf{h}}^\top{\bf{s}} + {\bf{h}}^\top\mathrm{E}\left[{\bf{\epsilon}}\right]\right)^2}{\mathrm{E}\left[\left({\bf{h}}^\top{\bf{\epsilon}}\right)^2\right]-\mathrm{E}\left[{\bf{h}}^\top{\bf{\epsilon}}\right]^2}, \newline
        &= \frac{\left({\bf{h}}^\top{\bf{s}} + {\bf{h}}^\top{\bf{0}}\right)^2}{{\bf{h}}^\top\mathrm{E}\left[{\bf{\epsilon}}{\bf{\epsilon}}^\top\right]{\bf{h}}-\left({\bf{h}}^\top\mathrm{E}\left[{\bf{\epsilon}}\right]\right)^2}, \newline
        &= \frac{\left({\bf{h}}^\top{\bf{s}}\right)^2}{{\bf{h}}^\top\bf{\Sigma}{\bf{h}}-\left({\bf{h}}^\top{\bf{0}}\right)^2} = \frac{\left({\bf{h}}^\top{\bf{s}}\right)^2}{{\bf{h}}^\top{\bf{\Sigma}\bf{h}}}.
    \end{split}
\end{equation}
Here we used the fact that the noise was distributed with zero mean in determining the covariance matrix as $\bf{\Sigma}=\mathrm{E}\left[\bf{\epsilon\epsilon}^\top\right]$.

In order to show how we can maximize the SNR, we need to make use of the Cauchy-Schwarz inequality. The theory of this inequality is beyond the scope of this reader, however, in order to provide some intuition on how it works, an example is provided. An application of this inequality is the triangle inequality, which states that for an triangle with sides that are spanned by the vectors $x$, $y$, and $x+y$ the following holds:
\begin{equation}
    \|x+y\| \leq \|x\| + \|y\|,
\end{equation}
where $\|\cdot\|$ denotes the length of the vector. This inequality simply means that the length of the longest side of the triangle is always less or equal than the combined length of the two minor sides. Equality only occurs if the vectors $x$ and $y$ point in the exact same direction.

The application of the Cauchy-Schwarz inequality for our case states that
\begin{equation}
    \left(\bf{h}^\top\bf{s}\right)^2 \leq \left(\bf{h}^\top \bf{h}\right)\left(\bf{s}^\top\bf{s}\right)
\end{equation}
holds. Since this term is in the numerator of the SNR, equality of the Cauchy-Schwarz inequality would maximize it. This equality only occurs if $\bf{h}=c\bf{s}$, where $c$ is a constant. Because of the definition of $y$, which calculated the unnormalized correlation, this results is expected.
