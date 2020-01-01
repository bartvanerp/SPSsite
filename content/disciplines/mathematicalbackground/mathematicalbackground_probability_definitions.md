+++
title = "Definitions of probability"

# date = {{ .Date }}
lastmod = 2019-12-30

draft = false       # Is this a draft? true/false
toc = true         # Show table of contents? true/false
type = "docs"       # Do not modify.

# Add menu entry to sidebar.
[menu.mathematicalbackground]
  name = "Definitions of probability"
  parent = "Probability theory"
  weight = 51

+++

## Definitions

A set of important definitions in probability theory are given below.

<ul>

<li style="margin-top:10px;"> An <b>experiment</b> is a procedure that can be repeated infinitely many times with an underlying model that defines which outcomes will be likely to observed. </li>

<li style="margin-top:10px;"> An <b>observation</b> (or a <b>trial</b>) is one realization of the experiment. </li>

<li style="margin-top:10px;"> The <b>outcome</b> of the experiment is any possible observation of the experiment. </li>

<li style="margin-top:10px;"> The <b>sample space</b>, denoted by $\mathcal{S}$, is the set of all possible outcomes. </li>

<li style="margin-top:10px;"> An <b>event</b> is a set of outcomes of an experiment, which can be the sample space or a subset of the sample space. </li>

<li style="margin-top:10px;"> Two events are called <b>disjoint</b> or <b>mutually exclusive</b> if these sets of outcomes do not have common outcomes. </li>

<li style="margin-top:10px;"> If an event is an empty set of outcomes it is a <b>null event</b>, which is denoted by $\emptyset$. </li>

<li style="margin-top:10px;"> The <b>event space</b> is a set of disjoint events together forming the sample space. </li>

</ul>

In order to get some intuition about the practical meaning of these definitions we turn to the following example.

### Example

Suppose we are flipping two coins and observing which sides of the coins land on top. The <i>experiment</i> is in this case the flipping of the two coins, where the top side of both coins is observed. The underlying model behind the experiment is based on the fact that we assume fair coins, meaning that the probability of a coin landing heads is equal to the probability of a coin landing tails.

An <i>observation</i> or <i>trial</i> is flipping both coins just once, with <i>outcome</i> characterized by the top sides of the coins. Let us write this corresponding outcome using two letters indicating the top sides of both coins respectively, where we use $h$ to indicate heads and $t$ to indicate tails. A possible outcome of the trial is for example $ht$. On the contrary, $h$ or $hth$ are not possible outcomes of this experiment, which involves flipping two coins.

The <i>sample space</i> for this particular experiment is defined as
\begin{equation}
    \mathcal{S} = \\{ hh, ht, th, tt\\},
\end{equation}
which is written in the set notation as will be discussed shortly. Let us define an <i>event</i> $A$, which is the set of all possible outcomes where the first coin is heads, and an event $B$,  which is the set of all possible outcomes where the second coin is tails. Both events can be written in the set notation as $A = \\{hh, ht\\}$ and $B=\\{ ht, tt\\}$. The events $A$ and $B$ are not <i>disjoint</i>, because both share the outcome $ht$. An example of a <i>null set</i> for this experiment is the event when a coin lands with a blank side facing upwards. This face is not defined in our experiment and therefore this outcome cannot be observed, leading to an empty set. A possible event space is the set given by the events $A$ and $B$, where $A$ resembles the event that the first coin lands head and where $B$ resembles the event that the first coin lands tails. Both events do not contain similar outcomes, i.e. $A=\\{hh, ht\\}$ and $B=\\{tt, th\\}$, but together they form the entire sample space.

<br></br>

## Sets of outcomes

In the last section we already saw that we could write our events as sets of outcomes. A set can be regarded as a group or collection of elements. A set is denoted with curly brackets $\\{\cdot\\}$ which enclose all elements in that particular set. These sets can also be visually represented and their relationships are shown in the Venn diagrams as shown in Fig. 1. The sample space $\mathcal{S}$ containing all possible outcomes is represented by a square. The event $A$ represents a set of possible outcomes and is a subset of the sample space.

<div style="max-width: 700px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/event_sets.svg"
      alt="Venn diagrams showing the relations between different sets. The shaded areas represent the results of the different operations."
    />
    <figcaption class="numbered">
      Venn diagrams showing the relations between different sets. The shaded areas represent the results of the different operations.
    </figcaption>
  </figure>
</div>

Fig. 1 introduces several set operators. The <b>complement</b> of a set $A$ is denoted by $A^C$ and is a set containing all outcomes of the sample space excluding the outcomes in  $A$. The <b>intersection</b> operator $\cap$ denotes the intersection between two sets. In $A \cap B$ the intersection contains all outcomes that are both in set $A$ and $B$. The <b>union</b> operator $\cup$ denotes the union between two sets. In $A \cup B$ the union contains all outcomes that are in $A$, $B$ and both $A$ and $B$. A <b>subset</b>, which contains a part of a larger set, is denoted as $B \subset A$ (read $B$ is a subset of $A$). Lastly, as defined previously, two events are <b>disjoint</b> if these sets of outcomes do not have common outcomes.


<br></br>

## Definition of probability

### Probability and frequency
The concept of probability is related to chance. There are two main definitions of probability. The first definition of probability is the <i>frequentist</i> definition of probability, also known as <i>relative probability</i>, by which a probability is calculated based on how often an event occurs. The relative frequency of an event is given by

\begin{equation}
    f_A = \frac{\text{number of occurrences of event }A}{\text{total number of observations}} = \frac{\text{N}(A)}{\text{N}},
\end{equation}

where N($\cdot$) denotes the number of occurrences of a certain event and N the total number of observations. The relative frequency can be understood as how often event $A$ occurs relative to all observations. One can see that a low number of total observations does not give a good estimate of the true underlying probability of an event occurring. Therefore an infinitely large number of observations is needed to obtain the true probability. This leads to the frequentist definition of probability, given by

\begin{equation}
    \Pr [A] = \lim\_{\text{N}\to\infty}f_A =\lim\_{\text{N}\to\infty}\frac{\text{N}(A)}{\text{N}}.
\end{equation}

The second definition is the <i>Bayesian</i> interpretation. This interpretation does not rely on the relative frequency of an event, but reflects a certain degree of belief that an event occurs. This probability is associated with a state-of-knowledge, influenced by a prior probability, which reflects the belief before an event actually takes place. An example will clarify this difference.

### Example
Let us consider an extravagant example by calculating the probability of finding extraterrestrial life (aliens). From a frequentist perspective the probability of finding extraterrestrial life equals 0, because extraterrestrial life has not (yet) been observed. This provides us with a simple but limited answer to our question.

Now consider the Bayesian perspective. From scientific research we may conclude that extraterrestrial life is possible under the right circumstances. Combining this information with the immense number of planets, we could definitely argue for a non-zero probability of finding extraterrestrial life. This probability is regarded as the prior probability as it is determined without performing any observations. Even after performing many unsuccessful attempts at finding extraterrestrial life, there still is a (very small) probability of finding extraterrestrial life. The discrepancy in the probabilities is an example of the difference between both definitions.


### Probability axioms
From the definition of probability, three important probability axioms can be determined. Axioms are statements that are regarded as true and can therefore be used to prove other statements. These probability axioms include:
<ol>
    <li style="margin-top:10px;"> For any event $A$, it holds that $0\leq\Pr[A]\leq 1$. </li>
    <li style="margin-top:10px;"> It holds that $\Pr [\mathcal{S}]=1$. </li>
    <li style="margin-top:10px;"> For any countable collection of $M$ <i>disjoint</i> events it holds that  $\Pr[A_1\cup A_2\cup \ldots \cup A_M] = \Pr[A_1] + \Pr[A_2] + \ldots + \Pr[A_M]$ . </li>
</ol>

Let us now discuss these axioms one by one. The first axiom that a probability of an event is always between 0 and 1, where 0 means that there is no chance that the event will take place and 1 means that it will certainly happen. Negative probabilities do not exist, where we can take the definition of the relative probability as an example. In this equation it is not possible for an event to occur a negative amount of times and therefore a negative probability does not exist. Similarly, a probability larger than 1 would mean that a certain event would occur more often than all events together. Again this is not physically possible and therefore we are restricted to the probability bounds set by the first axiom.

The second axiom tells us that the probability of observing an outcome that is in our sample space $\mathcal{S}$ is always equal to 1. This axiom arises from the definition of the sample space. The sample space was defined previously as the set of <i>all</i> possible outcomes. Therefore we can conclude that an observation is always part of this set and thus the probability of observing an outcome that is part of the sample space equals 1.

The third axiom tells us that we may add the probabilities of separate events if we want to calculate the probability of the union of these events, under the constraint that the sets are disjoint to each other. Fig. 1 gives an intuitive explanation to why this holds. When the union is calculated of multiple disjoint events, there is no overlap (meaning no common outcomes) between these events. Therefore the total probability does not need to be compensated for overlap and we can simply add the probabilities of the separate events.

### Consequences of the probability axioms
From the previous axioms, several consequences can be determined. These include:
<ol>
    <li style="margin-top:10px;"> It holds that $\Pr [\emptyset] = 0$. </li>
    <li style="margin-top:10px;"> It holds that $\Pr [A^C] = 1 - \Pr [A]$. </li>
    <li style="margin-top:10px;"> For any events $A$ and $B$ it holds that $\Pr[A\cup B] = \Pr[A] + \Pr[B] -\Pr[A\cap B]$. </li>
    <li style="margin-top:10px;"> If $A \subset B$ it holds that $\Pr[A] \leq \Pr[B]$. </li>
    <li style="margin-top:10px;"> For any event $A$ and event space $\{B_1, B_2, \ldots, B_m\}$ it holds that  $\Pr[A] = \sum\_{i=1}^{m}\Pr[A\cap B_i] = \sum\_{i=1}^{m}\Pr[AB_i]$. </li>
</ol>

The first consequence is rather straightforward. The probability of observing an outcome that is in our null event equals 0, because it reflects the chance that we observe nothing. This is not the case, since our observations are inevitably in the sample space.

The second consequence can be understood again through Fig. 1, where the definition of the complement plays an important role. The complement of an event $A$ included all outcomes in the sample space excluding all outcomes of the event $A$. Since axiom 2 indicates that the probability of observing any outcome equals 1, the sets $A$ and $A^C$ together make up the entire sample space and therefore their probabilities together should be equal to one.

Consequence 3 is a generalization of axiom 3 and holds for all events, so not only for disjoint events. The axiom can be understood by analyzing Fig. 1. The union of two overlapping events can be written as their sum whilst compensating for the overlapping set of outcomes, denoted by the intersection of both events. Therefore in the axiom notation, the probability of the union of events $A$ and $B$ can be written as the sum of both individual probabilities minus the probability of the overlapping event. Axiom 3 is a special case of this axiom, where two events are disjoint and therefore the intersection between the two events equals 0.

The fourth consequence specifies that the probability of an event $A$ is smaller or equal to the probability of an event $B$ when $A$ is a subset of $B$. This is an immediate result of the definition of a subset, where the event $A$ contains a part of the outcomes of event $B$. Equality only occurs if the sets are equal.

The last consequence can be explained with the help of Fig. 2. The event $A$ can be split up in multiple subsets each in a separate region of the event space, denoted by the intersection between event $A$ and the subset $B_i$. Adding all different segments of $A$ gives the full event $A$, because the event space always covers the entire sample space and must therefore include the entire set of $A$.


<div style="max-width: 500px; margin: auto">
  <figure>
    <img
      src="/../files/7.Images/math/probability/event_space.svg"
      alt="Visualization of a sample space, separated in an event space $\{B_1, B_2, B_3, B_4\}$, with an event $A$ that can be split up in different segments."
    />
    <figcaption class="numbered">
      Visualization of a sample space, separated in an event space $\{B_1, B_2, B_3, B_4\}$, with an event $A$ that can be split up in different segments.
    </figcaption>
  </figure>
</div>

<br></br>

## Conditional probability
Conditional probabilities describe our knowledge about an event, given the knowledge that another event has happened. As an example we could compare two situations. Suppose it is sunny outside and we want to know the probability that it starts raining. This probability is relatively low, whereas this probability would be a lot higher if it were cloudy. From this example, we may conclude that our knowledge of the weather at this moment, influences our prediction of raining in the near future.

### A priori and a posteriori probability
The circumstances under which we would like to know the probability can be regarded as the observations of data. These observations provide us with insights about the circumstances and allow us to make a better estimate of the probability.
The probability of an event $A$ occurring without having made any observations is called the <i>a priori</i> probability (prior = before) and is denoted by $\Pr[A]$. The <i>a posteriori</i> probability (post = after) is the new probability after having obtained more information about the situation. This probability is denoted as $\Pr[A|B]$ and is read as " probability $A$ given $B$". As an example we have the probability of rain after clouds are observed.

This conditional probability $\Pr[A|B]$ can be calculated as
\begin{equation}
    \Pr[A|B] = \frac{\Pr[AB]}{\Pr[B]},
\end{equation}
where $\Pr[AB]$ is the probability of both events $A$ and $B$ occurring, which is equal to the probability of the intersection $\Pr[A\cap B]$. This equation scales the probability of observing an outcome in the intersection of $A$ and $B$ with the probability of $B$. From the visual notation of Fig. 1 this can be seen as the 'area' of the event $A\cap B$ normalized with the 'area' of $B$.

### Properties of conditional probability
From the definition of this conditional probability 3 properties can be deduced:
<ol>
    <li style="margin-top:10px;"> It holds that $\Pr[A|B] \geq 0$. </li>
    <li style="margin-top:10px;"> It holds that $\Pr[B|B] = 1$. </li>
    <li style="margin-top:10px;"> For a set of disjoint events $A = \{ A_1, A_2, \ldots, A_M\}$ it holds that $\Pr[A|B] = \Pr[A_1|B] + \Pr[A_2|B] + \ldots + \Pr[A_M|B]$. </li>
</ol>
The first and third property can be explained by the arguments as given in the Section with the probability axioms. The second property is not explicitly mentioned there, but this property confirms itself if you read it, since it simply reads as "The probability of having observed an event $B$ after having observed an event $B$ equals 1".

### Law of total probability
Similarly to the fifth consequence of the axioms of probability, a new expression can be determined using conditional probabilities. This is called the law of total probability and states that for an event space $\\{ B_1, B_2, \ldots, B_M \\}$ with $\Pr[B_i] > 0$ for all $i$, it holds that
\begin{equation}
    \Pr[A] = \sum\_{i=1}^{M}\Pr[A|B_i]\Pr[B_i].
\end{equation}
This law inevitably follows from substituting the definition of the conditional probability as $\Pr[AB_i] = \Pr[A|B_i]\Pr[B_i]$ in the fifth consequence of the probability axioms.

### Bayes' rule
One of the most important rules in probability theory is Bayes' rule, which is obtained from the definition of the conditional probability. This conditional probability can be rewritten as
\begin{equation}
    \Pr[A|B]\Pr[B] = \Pr[AB] = \Pr[BA] = \Pr[B|A]\Pr[A].
\end{equation}
Equality of the middle two terms is obtained because these terms represent the same probability. Rewriting the leftmost and rightmost expression gives Bayes' rule including the nomenclature of the separate terms as
\begin{equation}
    \underbrace{\Pr[B|A]}\_\text{posterior} = \frac{\overbrace{\Pr[A|B]}^\text{likelihood}\overbrace{\Pr[B]}^\text{prior}}{\underbrace{\Pr[A]}\_\text{evidence}}.
\end{equation}
Now why is this particular notation so useful? The answer requires you to think in a certain context. Think of a context where an observation of an event $A$ is related to a (non-observable) underlying event $B$. An example of this context is where $A$ resembles the observed data and $B$ the model parameters creating this data. In the signal processing field we would like to obtain the model parameters to draw conclusions about the underlying process (for example in medical diagnostics). We would like to estimate these parameters after observing some data. Therefore we are interested in the probability $\Pr[B|A]$. However, we cannot determine this immediately and therefore we need Bayes' rule. The initial (prior) probability of the model parameters is denoted by $\Pr[B]$ and is determined as an initial guess in terms of probability for the model parameters of the underlying process without having seen the data. The term $\Pr[A|B]$ represents the likelihood of the observed data <i>under the assumed model parameters</i>. Both these terms can be calculated relatively easily. The last term $\Pr[A]$ represents the evidence, which is the probability of observing some data. This last term is usually more difficult to calculate and is therefore usually calculated by using of the law of total probability.

### Example
A common example of Bayes' rule is positioned in the medical field. Suppose we have an event $A$, which indicates that a patient has a lung disease, and an underlying event $B$, which indicates that the patient smokes. Research has been conducted in a clinic and it has been found that among the patients with a lung disease 30% of the patients smoke. Furthermore, 20% of the people in the clinic smoke and only 10% of the people in the clinic have a lung disease. Let's suppose that we are interested in the probability that a patient who smokes actually has a lung disease.

If we convert the given information into mathematical notation we can find that the prior probability (a patient with a lung disease) is $\Pr[A]=0.1$. Furthermore the evidence (a patient who smokes) is $\Pr[B] = 0.2$. Lastly we find the likelihood (a patient with a lung disease smoking) as $\Pr[B|A] = 0.3$. From this we can determine the posterior $\Pr[A|B]$ (a patient who smokes having a lung disease) as
\begin{equation}
    \Pr[A|B] = \frac{\Pr[B|A]\Pr[A]}{\Pr[B]} = \frac{0.3\cdot 0.1}{0.2} = 0.15
\end{equation}
Please note that the order of $A$ and $B$ is the opposite of in the above equation, because $\Pr[B|A]$ is observed and therefore the nomenclature changes.

### Independence
Besides the definitions encountered throughout the reader, there is one other important definition in the field of probability theory called independence. Two events $A$ and $B$ are independent <i>if and only if</i> the following holds
\begin{equation}
    \Pr[AB] = \Pr[A]\Pr[B],
\end{equation}
which is equivalent to $\Pr[A|B] = \Pr[A]$ and $\Pr[B|A] = \Pr[B]$. These equalities simply mean that the probability of an event $A$ remains exactly the same after observing an event $B$, or vice versa. In other words, we do not get additional information through the occurrence of event $B$. Combining the previous two equations with the conditional probabilities gives rise to this independence condition.

Note that independent is not the same as disjoint! It can be possible that events are both disjoint as independent, but this does not have to be the case.

The definition of independence of two sets can be extended to multiple sets. Multiple sets $\\{A_1, A_2, \ldots, A_M\\}$ are independent if and only if the following two constraints hold

<ol>
    <li style="margin-top:10px;"> Every possible combination of two sets is independent. </li>
    <li style="margin-top:10px;"> It holds that $\Pr[A_1A_2\ldots A_M] = \Pr[A_1]\Pr[A_2]\ldots\Pr[A_M]$. </li>
</ol>

From this we may automatically conclude that pairwise independence (constraint 1) does not immediately lead to the independence of multiple events, since the second constraint still needs to be satisfied.
