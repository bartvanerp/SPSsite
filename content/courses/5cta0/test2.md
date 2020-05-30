+++
title = "test2"

# date = {{ .Date }}
lastmod = 2020-05-10

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

# Responsible teacher (email)
responsibleteacher = "StatisticalSignalProcessing@groups.tue.nl"

# Add menu entry to sidebar.
[menu.5cta0]
name = "test2"
weight = 99

+++

% This LaTeX was auto-generated from MATLAB code.
% To make changes, update the MATLAB code and export to LaTeX again.

\documentclass{article}

\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage{graphicx}
\usepackage{color}
\usepackage{listings}
\usepackage{hyperref}
\usepackage{amsmath}
\usepackage{amsfonts}
\usepackage{epstopdf}
\usepackage[table]{xcolor}
\usepackage{matlab}

\sloppy
\epstopdfsetup{outdir=./}
\graphicspath{ {./CLTdemo_images/} }

\begin{document}

\matlabtitle{\textbf{The Central Limit Theorem}}

\matlabheading{\textbf{Introduction}}

\begin{par}
\begin{flushleft}
The \textbf{central limit theorem (CLT)} is one of the most important results in probability theory. It states that, under certain conditions, the sum of a large number of random variables is approximately normal. Several versions of the CLT have been proposed, which differ according to the underlying assumptions on the sampling distribution and the criteria for convergence.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
In this demo, we begin by focusing on a version of the CLT that applies to indipendent identically distributed (i.i.d.) random variables, and then we show that, under specific assumptions, the CLT can be extended to independent, but non identically-distributed random variables.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
he learning objectives of the following simulations are:
\end{flushleft}
\end{par}

\begin{itemize}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} understand sampling of random variables \end{flushleft}}
   \item{\begin{flushleft} investigate how the sampling distribution infiuences convergence to the CLT \end{flushleft}}
   \item{\begin{flushleft} extend the CLT to independent, but not identically distribute random variables \end{flushleft}}
   \item{\begin{flushleft} understand the implications of the CLT for real-world applications \end{flushleft}}
\end{itemize}

\matlabheading{The CLT for i.i.d. random variables}

\begin{par}
\begin{flushleft}
The classic version of the CLT states:
\end{flushleft}
\end{par}


\begin{par}
\begin{flushleft}
Given $X_1, X_2, ..., X_N$\textbf{ i.i.d} random variables with expected value $E[X_i] = \mu < \infty$ and variance $Var [X_i] = \sigma^2 < \infty$, the random variable given by their \textbf{normalized sum}
\end{flushleft}
\end{par}

\begin{par}
$$\bar{X} = \frac{X_1, X_2, ..., X_N}{N}$$
\end{par}

\begin{par}
\begin{flushleft}
converges in distribution to the normal random variable for \textbf{N sufficiently large}. The mean and standard deviation of $\bar{X}$ are
\end{flushleft}
\end{par}

\begin{par}
$$E[\bar{X}] = \frac{NE[X_i]}{N} =  \mu$$                                                $$Var [\bar{X}] =\frac{\sigma^2}{N}$$
\end{par}


\vspace{1em}

\matlabheadingtwo{Sampling of i.i.d random variables}

\begin{par}
\begin{flushleft}
Let us now see how the CLT works in practice for i.i.d random variables\textit{. }
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
We start by simulating 30 uniformely distributed RVs with controlling parameters $a

$ and $b
$. Thus, the mean and standard deviation can be calculated as:
\end{flushleft}
\end{par}


\vspace{1em}
\begin{par}
$$\mu = \frac{b+a}{2}$$                       $$\sigma^2 = \frac{(b-a + 1)^2-1}{12}$$
\end{par}

\begin{matlabcode}
%parameters a and b from a uniform distribution
a = 2;
b = 10;
%number of samples drawn to form each random variables
M = 1000;
%number of simulated random variables
N = 100;
%Simulate 30 uniformly distributed RV wiht parameters a,b
X_iid = (b-a).*rand(N,M) + a;
%Visualize a few of the simulated random variables
my_subplots_of_X(X_iid, 3, 3)
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_0}
\end{center}


\begin{par}
\begin{flushleft}
\textbf{Assignement 1}
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
On Canvas, go on the discussion section and answer the following questions, in the thread entitled "Matlab demo on Central Limit theorem".
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
a) Change M to 100, 500, 1000, 20000. How does the histogram change as M increases? Discuss your observations.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
b) Write your own piece of code to calculate $\mu$ and $\sigma^2
$ for each $X_i$ and compare them with theoretical values for a uniform distribution. Repeat for different values of M and describe what you observe.
\end{flushleft}
\end{par}


\vspace{1em}
\begin{matlabcode}
%-------------------------------------------------------------------------------------------------------------------------------------
%Write below you code for question b)
%---------------------------------------------------------------------------------------------------------------------------------------
\end{matlabcode}


\matlabheadingtwo{The CLT in practice for i.i.d random variables}

\begin{par}
\begin{flushleft}
After simulating N random variables and storing them in matrix X, we now show what happens when we sum them and how the number of summed random variables influences the results.
\end{flushleft}
\end{par}

\begin{matlabcode}
% number of summed random variables
N_k = [2 5 10 30 50 100];
%initialize figure
figxsum = figure('units','normalized','outerposition',[0 0 1 0.8]);
for k = 1:length(N_k)
    X_sum = sum(X_iid(1:N_k(k),:)) / N_k(k);
    %plot the distribution of the sum of N random variables
    my_subplots_of_Xsum(X_sum, 2, 3, k, N_k(k), figxsum)

    %calculate mean and std of X_sum

    %theoretical mean and var from CLT

    mu_CLT = (b + a) / 2;
    var_CLT = (((b - a + 1)^2 - 1) / 12) / N_k(k);

    x = linspace(a, b, 100);

    %plot Gaussian distribution
end
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_1}
\end{center}


\begin{par}
\begin{flushleft}
\textbf{Assignement 2}
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
On Canvas, go on the discussion section and answer the following questions, in the thread entitled "Matlab demo on Central Limit theorem".
\end{flushleft}
\end{par}

\begin{enumerate}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} When is N sufficiently large for Xsum to converge to a normal distribution? \end{flushleft}}
   \item{\begin{flushleft} Plot the calculated mean and std and compare it with the theoretical value according to the CLT. Do your calculation support the answer given in question 2.1? Explain. \end{flushleft}}
   \item{\begin{flushleft} Change parameters a and b. Check also extreme values (very low a and very large b). Does the answer to question 2.1 changes? \end{flushleft}}
   \item{\begin{flushleft} Repeat the simulation for a skewed distribution of your choice (e.g., exponential, Poisson). Does your answer to question 2.1 changes? Attach a picture with the plots to your answer. \end{flushleft}}
\end{enumerate}



\vspace{1em}
\matlabheading{Extension of CLT to non indentically-distributed random variables}

\begin{par}
\begin{flushleft}
A variant of the CLT formulated by Aleksandr Lyapunov extends the results to independent random variables, which are not identically distributed. This Lyapunov CLT states:
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
Let $X_1, X_2, ..., X_N$ be a set of N\textbf{ independent} random variables, and each $X_i$ has an arbitrary probability distribution with expected value $E[X_i] = \mu_i < \infty$ and variance $Var [X_i] = \sigma^2_i < \infty$, the random variable given by their \textbf{normalized sum}
\end{flushleft}
\end{par}

\begin{par}
$$\bar{X} = \frac{X_1, X_2, ..., X_N}{N}$$
\end{par}

\begin{par}
\begin{flushleft}
converges in distribution to the normal random variable for \textbf{N sufficiently large}, if the \textbf{Lyapunov condition }is satisfied.
\end{flushleft}
\end{par}


\vspace{1em}
\begin{par}
\begin{flushleft}
The mean and standard deviation of $\bar{X}$ are
\end{flushleft}
\end{par}

\begin{par}
$$E[\bar{X}] = \frac{NE[X_i]}{N} =  \mu$$                                                $$Var [\bar{X}] =\frac{\sigma^2}{N}$$
\end{par}

\begin{par}
\begin{flushleft}
The Lyanpunov condition essentially sets a limit of the rate of growth of the moments of each $X_i$ \href{https://mathworld.wolfram.com/LyapunovCondition.html}{[1]}.
\end{flushleft}
\end{par}


\matlabheadingtwo{Sampling of independent random variables}

\begin{par}
\begin{flushleft}
Let us now see how the CLT works in practice for independent, but not identically-distributed random variables\textit{. }
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
To do this, we will start again by simulating N uniformely distributed random variables, but this time we will make also the controlling parameters a and b a random variable.
\end{flushleft}
\end{par}

\begin{matlabcode}
%number of samples drawn to form each random variables
M = 1000;
%number of simulated random variables
N = 100;
%parameters a and b from a uniform distribution
a_min = -8;
a_max = 5;
width_min = 1;
width_max = 100;
%Simulate N uniformly distributed RV with different controlling parameters
A = (a_max - a_min).*rand(N, 1) + a_min;
W = (width_max - width_min).*rand(N, 1) + width_min;
X = W.*rand(N, M) + A;
%Visualize a few of the simulated random variables
my_subplots_of_X(X, 3, 3)
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_2}
\end{center}

\begin{par}
\begin{flushleft}
It can be observed that know the variables have different controlling parameters a,b and therefore different mean and variance.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
Let's now observe what are the implications for the convergence of the CLT.
\end{flushleft}
\end{par}

\begin{matlabcode}
% number of summed random variables
N_k = [2 5 10 30 50 100];
%initialize figure
figxsum = figure('units','normalized','outerposition',[0 0 1 0.8]);
for k = 1:length(N_k)
    X_sum = sum(X(1:N_k(k),:))/N_k(k);
    %plot the distribution of the sum of N random variables
    my_subplots_of_Xsum(X_sum, 2, 3, k, N_k(k), figxsum)

    %calculate mean and std of X_sum

end
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_3}
\end{center}


\begin{par}
\begin{flushleft}
Finally, we extend the simulation to N independent random variables from different sampling distributions and different controlling parameters. In this example, we simulate random variables sampled from Uniform, Gaussian, Exponential, and Poisson distributions.
\end{flushleft}
\end{par}

\begin{matlabcode}
%number of samples drawn to form each random variables
M = 1000;
%Parameters uniform distribution
a_min = -8;
a_max = 5;
width_min = 1;
width_max = 100;
N_uni = 25;
%Simulate uniformely distributed RVs
A = (a_max - a_min).*rand(N_uni, 1) + a_min;
W = (width_max - width_min).*rand(N_uni, 1) + width_min;
X_uni = W.*rand(N_uni, M) + A;

%Parameters Gaussian distribution
mu_min = -10;
mu_max = 10;
sigma_min = 0.1;
sigma_max = 4;
N_norm = 25;
%Simulate Normal distributed RVs
MU = (mu_max - mu_min).*rand(N_norm, 1) + mu_min;
SIG = (sigma_max - sigma_min).*rand(N_norm, 1) + sigma_min;
X_norm = SIG.*randn(N_norm, M)+ MU;
%Parameters Poisson distribution
lambda_min = 1;
lambda_max = 10;
N_pois = 25;
%Simulate Poisson distributed RVs
LAMBDA = (lambda_max - lambda_min).*rand(N_pois, 1) + lambda_min;
X_pois= poissrnd(repmat(LAMBDA, [1 M]));
%Parameters Exponential distribution
gamma_min = 0.1;
gamma_max = 4;
N_exp = 25;
%Simulate exponentially distributed RVs
GAMMA = (gamma_max - gamma_min).*rand(N_exp, 1) + gamma_min;
X_exp = exprnd(repmat(GAMMA, [1 M]));
%Stack random variables interleaved
N = 100;
X_all = zeros(N, M);
X_all(1:4:end-3) = X_uni;
X_all(2:4:end-2) = X_norm;
X_all(3:4:end-1) = X_pois;
X_all(4:4:end) = X_exp;
%Visualize a few of the simulated random variables
my_subplots_of_X(X_all, 3, 3)
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_4}
\end{center}


\begin{par}
\begin{flushleft}
Let's take a look at the convergence to the CLT when we have an independent set of random variables, but drawn from differnent distributions with varying controlliing parameters.
\end{flushleft}
\end{par}

\begin{matlabcode}
% number of summed random variables
N_k = [2 5 10 30 50 100];
%initialize figure
figxsum = figure('units','normalized','outerposition',[0 0 1 0.8]);
for k = 1:length(N_k)
    X_sum = sum(X_all(1:N_k(k),:))/N_k(k);
    %plot the distribution of the sum of N random variables
    my_subplots_of_Xsum(X_sum, 2, 3, k, N_k(k), figxsum)

end
\end{matlabcode}
\begin{center}
\includegraphics[width=\maxwidth{102.86001003512293em}]{figure_5}
\end{center}


\begin{par}
\begin{flushleft}
\textbf{Assignement 3}
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
On Canvas, go on the discussion section and answer the following questions, in the thread entitled "Matlab demo on Central Limit theorem".
\end{flushleft}
\end{par}

\begin{enumerate}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} Write your own code to calculate the mean and standard deviation of the random variable obtained by summing n random variables draw from X\_all, with n ranging from 2 to 100. Compare the values obtained experimentally with the theoretical values from the CLT. Make a plot and give a rough estimation of how large n should be to converge to the CLT in this case. Attach your plot to your reply in the forum. \end{flushleft}}
\end{enumerate}


\matlabheading{DIscussion: Implications of the CLT}

\begin{par}
\begin{flushleft}
The importance of the central limit theorem lies on that, in many real-world examples, a certain random variable of interest is a sum of a large number of independent random variables. In these situations, the CLT justifys using the normal distribution to model our random variable of interest. We can find examples in almost every discipline:
\end{flushleft}
\end{par}

\begin{itemize}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} In statitstics, when applying random sampling to study a population, the resulting quantity is typically modeled as a normal random variable. \end{flushleft}}
   \item{\begin{flushleft} In laboratory measurements, where errors are usually modeled by normal random variables. \end{flushleft}}
   \item{\begin{flushleft} In communication and signal processing, where noise is the most frequently modeled as Gaussian. \end{flushleft}}
   \item{\begin{flushleft} In finance, where the percentage changes in the prices of some assets can be modeled by normal random variables. \end{flushleft}}
\end{itemize}

\begin{par}
\begin{flushleft}
The ability to model the variable of interest as a Gaussian random variable simplifies computations significantly. If you would like to actually compute the distribution of the sum of one thousand i.i.d. random variables, it might be extremely difficult, if not impossible. The CLT enables you to write the resulting distribution, by only knolwedge of the mean and variance of each random variable.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
As shown in this simulation, a question that comes to mind is how large \textit{n} should be so that we can use the normal approximation. We have shown that the answer generally depends on the distribution of the random variables. Nevertheless, as a rule of thumb it is often stated that if \textit{n} is larger than or equal to 30, then the normal approximation is very good.
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
\textbf{Assignement 4}
\end{flushleft}
\end{par}

\begin{par}
\begin{flushleft}
On Canvas, go on the discussion section and answer the following questions, in the thread entitled "Matlab demo on Central Limit theorem".
\end{flushleft}
\end{par}

\begin{enumerate}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} Provide a concrete real-world example where we can use the CLT. \end{flushleft}}
   \item{\begin{flushleft} Does the rule of thumb of n=30 seem appropriate for our simulations? Elaborate. \end{flushleft}}
\end{enumerate}


\matlabheading{Conclusions}

\begin{par}
\begin{flushleft}
In this simulation, we have formulated two different versions of the CLT and showed how they work in practice. We have also discussed what are the implicaitons of the CLT in real-world examples. By the end of this simulation, you should be able to:
\end{flushleft}
\end{par}

\begin{itemize}
\setlength{\itemsep}{-1ex}
   \item{\begin{flushleft} explain the CLT  \end{flushleft}}
   \item{\begin{flushleft} understand how the sampling conditions (i.i.d, independent non i.d.) influence convergence of the CLT \end{flushleft}}
   \item{\begin{flushleft} understand how the charachteristics of the sampling distribution influence convergence of the CLT \end{flushleft}}
   \item{\begin{flushleft} explain the implications of the CLT in real-world measurements \end{flushleft}}
\end{itemize}

\end{document}
