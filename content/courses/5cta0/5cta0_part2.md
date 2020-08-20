+++
title = "Part 2: Estimation theory"

# date = {{ .Date }}
lastmod = 2020-08-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Add menu entry to sidebar.
[menu.5cta0]
name = "Part 2: Estimation theory"
weight = 200

+++

To explain what is covered by the term estimation, at least in the scope of this course, consider an experiment. An <i> experiment </i>, in the context of probability theory, is a mechanism that generates outcomes according to a probability density function (or probability mass function if the outcomes have discrete values). For example, the experiment can consist of picking several batteries at random from a batch produced at a factory and measuring their output voltages by connecting them to a test circuit. Due to variability in the production processes, the measured voltage is expected to be different for each battery and for each repetition of the experiment. If there is a <i>model</i> that connects the distribution of measured voltages with <i>parameters</i> controlling the production processes, then these parameters can be <i> estimated </i> based on the measurements.

The concept of estimation is visualised in Fig. 1. This part of the course presents the fundamental toolset for solving estimation problems involving different signal models.

<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/statistical/estimation/estimation_model.svg"
      alt="."
    />
    <figcaption class="numbered">
      The data model describes the scope of the estimation methods covered in the Estimation part of the course.
    </figcaption>
  </figure>
</div>



The topics covered in this part are
<ul>
<li><a href="../estimation_leastsquares">Least Squares Estimator:</a> This method fits the model to data by minimizing the sum of squared difference between the data and the model.
<li><a href="../estimation_maximumlikelihood">Maximum Likelihood Estimator:</a> The stochastic nature of the data due to the noise is be modeled in terms of the probability density function of the noise. The parameter value that maximizes the probability of observing the data at hand is the maximum likelihood estimate.
<li><a href="../estimation_crlb">The Cramer-Rao Lower Bound:</a> Just as the data is stochastic, so are the parameter estimations. When the noise properties are known, the lowest possible variance for the parameter estimations can be calculated for unbiased estimators.
<li><a href="../estimation_mvue_linear">Minimum Variance Unbiased Estimator and Best Linear Unbiased Estimator:</a> The minimum variance unbiased estimator can be found for linear problems with Gaussian noise.
<li><a href="../estimation_bayes">Bayesian Estimators:</a> For all estimation techniques so far, the parameter to be estimated is assumed to be deterministic but unknown. Bayesian estimators consider the parameter also as a random variable and utilized the Bayes' Theorem to estimate it.
<li><a href="../estimation_numerical_methods">Numerical Solution Methods:</a> Not all estimators have closed forms; numerical methods that iteratively estimate the parameters are indispensible tools for implementing estimators.
<li><a href="../estimation_spectral_estimation">Spectral Estimation:</a>
The power spectrum provides important information on the stochastic process generating the data; in this module we discuss methods to estimate the power spectrum when only a short segment of a random signal is available.</ul>
