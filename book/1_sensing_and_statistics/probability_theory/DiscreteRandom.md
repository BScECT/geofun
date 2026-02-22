# Discrete random variables

In science and engineering we are often dealing with events, processes or variables with an outcome that cannot be predicted with certainty. Hence, there is *randomness* involved due to aleatoric and/or epistemic uncertainty. Still, these *random* events, processes and variables may follow a long-term pattern which can be described by a probability distribution. In this section we will define what a random variable is, and focus on specifically *discrete* random variables. We will then introduce probability mass functions and distribution functions, which allow to evaluate the likelihood of certain outcomes. Finally, we will look at random variables that follow a specific distribution.

## Learning objectives

After studying Discrete random variables you will be able to ...
* define discrete random variables
* construct, visualize and interpret probability mass functions and distribution functions of discrete random variables
* identify when uniform, Bernouilli and binomial distributions apply in real-world contexts

## Random variables

In the previous sections we have seen examples of experiments or phenomena which had different types of outcomes, for instance:

* the number of eyes thrown with a die: {1,2,3,4,5,6}
* testing for presence of neodymium in a rock sample: {detection, no detection}
* measurement of a distance: {$\mathbb{R}^+$}
* wind speed at a certain location: {$\mathbb{R}^+$}

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Discrete random variable } X:$

A random variable $X$ is a function which maps the outcomes in sample space $\Omega$ to real numbers, $X:\Omega\rightarrow\mathbb{R}$.

A discrete random variable can take a (finite or infinite) set of distinct values $a_1,a_2,\ldots$

</div>

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example rock testing}$

Three rocks are tested on the presence of neodymium. Result of a test is either 'detection', denoted as outcome $s$, or 'not detected', denoted as outcome $o$. The sample space is shown on the left-side of {numref}`figure {number} <random_map>`. We now define the random variable $X$ as the number of 'detections', which then has four possible outcomes {0,1,2,3}. The figure illustrates how the outcomes in $\Omega$ are mapped to real numbers.

````{figure} ../../figures/part-a_rvmap.png
---
name: random_map
width: 40%
align: center
---
Mapping of outcomes in $\Omega$ to real numbers for testing 3 rock samples on presence of neodymium ($s$ is detection, $o$ no detection, $X$ number of detections.).
````

The probabilities $\mathsf{P}(X=a)$ are shown in the bar plot on the left in {numref}`figure {number} <pmf_Fx>`, assuming all outcomes in $\Omega$ are equally likely. The corresponding probabilities $\mathsf{P}(X\leq a)$ are shown on the right-hand side.

````{figure} ../../figures/part-a_pmf_Fx.png
---
name: pmf_Fx
width: 80%
align: center
---
Probability mass function (left) and distribution function for testing 3 rock samples on presence of neodymium with $X$ the number of detections.
````

</div>

The probabilities $\mathsf{P}(X=a)$ are referred to as *probability masses* and denoted as $p_X(a)$. Hence the *probability mass function* is defined as:

$$
p_X(a)= \mathsf{P}(X=a),\; -\infty < a < \infty
$$

Often we are interested in a probability that a random variable $X$ is in a certain interval, or smaller than or larger than a certain value. For instance for assessing the energy production of a wind farm, one may be interested in the probability that the wind speeds are below a certain threshold. The *distribution function* $F_X(a)$ provides the probabilities $\mathsf{P}(X\leq a)$:

$$
F_X(a)= \mathsf{P}(X\leq a),\; -\infty < a < \infty
$$

Vice versa, probability masses can be retrieved from the distribution fucnction, e.g., $\mathsf{P}(X= 3) = F_X(3)- F_X(2)$.

Note that both the probability mass function and distribution function contain all information to assess all types of probabilities. The distribution function can namely be expressed in terms of the individual probability masses of the distinct outcomes $a_1,a_2, \ldots$:

$$F_X(a_i)=\mathsf{P}(X\leq a_i)=p_X(a_1)+p_X(a_2)+\ldots +p_X(a_i)$$

Properties of a distribution function $F_X(a)$

* $0\leq F_X(a) \leq 1$ (since it is a probability), and

$$
\lim_{a\rightarrow -\infty}F_X(a)= 0, \;\lim_{a\rightarrow \infty}F_X(a)= 1
$$ 

* If $a\leq b$ then $F_X(a)\leq F_X(b)$ (since if $X\leq a$ then automatically $X\leq b$)
* $\mathsf{P}(X> a)=1- F_X(a)$ (since {$X>a$} is the complement of {$X\leq a$})

Discrete random variables can have many different distribution functions, but there are many cases for which one of the following discrete distributions apply.

## Discrete uniform distribution

An experiment with $n$ equally likely outcomes has a uniform distribution. An example is the outcome of throwing a die.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Discrete uniform distribution:}$

Random variable $X$ has probability mass function

$p_X(k)=\frac{1}{n},\;\; k=1,2,\ldots,n$

with $0\leq p \leq 1$

</div>

## Bernouilli distribution

This distribution is applicable for experiments with two possible outcomes: $X=1$ for "success" and $X=0$ for "failure".

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Bernouilli distribution:}$

Random variable $X$ has probability mass function

$p_X(1)=\mathsf{P}(X=1)=p\;\; \text{and};\;  p_X(0)=\mathsf{P}(X=0)=1-p$

with $0\leq p \leq 1$

Notation: $X\sim Ber(p)$

</div>

## Binomial distribution

This distribution is applicable in case of $n$ trials of an experiment with the following characteristics:
* each trial has two possible outcomes {1,0} (i.e., the outcome has Bernouilli distribution, therefore also called Bernouilli trial)
* each trial is independent
* probability $p$ is the same for each trial

The random variable $X$ is the number of times that a trial has outcome {1} (number of successes).

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Binomial distribution:}$

Random variable $X$ has probability mass function

$p_X(k)=\mathsf{P}(X=k)=\binom{n}{k}p^k (1-p)^{n-k},\;\; \text{for } k=0,1,\ldots,n$

with $0\leq p \leq 1$, and $n\geq 1$

Notation: $X\sim Bin(n,p)$

</div>

The binomial coefficient $\binom{n}{k}=\frac{n!}{k!(n-k)!}$ and is equal to the number of combinations that $k$ successes occur in $n$ trials.

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example rock testing}$

We will look again at the experiment where we test three rocks on the presence of neodymium. If we consider 'detection' as a "success", and 'not detected' as a "failure", we realize that the outcome of single trial follows the Bernouilli distribution. Let's now assume that the probability of success and failure are not equal, but $p$ and $1-p$, respectively.

If the 3 trials are independent this means that if $X$ is the number of successes that $X\sim Bin(3,p)$.

Let's see how we can find the probability $\mathsf{P}(X=2)$, i.e., the probability of 2 successes. First, we need to realize that there are 3 different combinations in which we have 2 successes: {sso,sos,oss}. Due to the independence of each trial we have

$$
\begin{align*}
\mathsf{P}(\{sso\}) &= \mathsf{P}(\{\text{first trial is success}\}\cap\{\text{second trial is success}\}\cap\{\text{third trial is failure}\})\\
&=\mathsf{P}(\{\text{first trial is success}\})\mathsf{P}(\{\text{second trial is success}\})\mathsf{P}(\{\text{third trial is failure}\}))\\
&= p\cdot p\cdot (1-p)= p^2 (1-p)
\end{align*}
$$

Check yourself that the probability for the other two outcomes is the same, such that:

$P(X=2) = \mathsf{P}(\{sso\})+\mathsf{P}(\{sos\})+\mathsf{P}(\{oss\}) = 3\cdot p^2 (1-p)$

and this is indeed equal to what you get using the expression for the probability mass function as defined above.

</div>

## Geometric distribution

The binomial distribution applies if we are interested in the number of successes in $n$ trials. If we are interested in the probability that the first success occurs in the $k^{\text{th}}$ trial, we need to use the geometric distribution.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Geometric distribution:}$

Random variable $X$ has probability mass function

$p_X(k)=\mathsf{P}(X=k)=p^k (1-p)^{n-k},\;\; \text{for } k=1,2,\ldots$

with $0\leq p \leq 1$

Notation: $X\sim Geo(p)$

</div>

## Poisson distribution

When dealing with random events that occur in time (or space), the occurrences of the events can often be modeled by a *Poisson process* if they happen independently and at a constant average rate of time (or space). Examples are energy emitted by radioactive particles, times at which electronic components fail, earthquakes, tsunamis, meteor strikes.

The random variable $X$ is now defined as the number of occurrences over a unit time interval.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Poisson distribution:}$

Random variable $X$ has probability mass function

$p_X(k)=\frac{\lambda^k}{k!}\exp\{-\lambda\},\;\; \text{for } k=0,1,\ldots,n$

with $\lambda >0$.

Notation: $X\sim Pois(\lambda)$

</div>

The Poisson distribution is an approximation of the binomial distribution in case $n$ is very large **and** $p$ is very small (i.e., the event is rare).

Parameter $\lambda$ is the *mean* number of occurrences in the given time interval.

## Summary of discrete distributions

In this section several discrete distributions have been introduced:

* Uniform distribution: $X$ has $n$ equally likely outcomes, each with probability mass $1/n$.
* Bernouilli distribution: $X$ has two outcomes with probabilities $p$ and $1-p$, respectively.
* Binomial distribution: $X$ is the number of successes in $n$ independent Bernouilli trials.
* Geometric distribution: $X$ is the number Bernouilli trials to get the first success.
* Poisson distribution: the number of occurrences of a rare event over a given time interval.

Other discrete distributions outside the scope of this course are:

* Negative binomial distribution: $X$ is the number of Bernouill trials to get $r$ successes. 
* Multinomial distribution: $X$ is the number of successes in $n$ independent Bernouilli trials, but now with $k$ possible outcomes per trial.
* Hypergeometric distribution: $X$ is the number of successes in $n$ independent Bernouilli trials, given that $K$ successes occur in a random subset of $N$ trials (useful in a factory if you only want to test a subset of all produced items).

Note: a discrete random variable does not always follow one of these distributions!

:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292829553002632237/embed" aria-label="Q03_pmf_Fx" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::


:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292827846291572497/embed" aria-label="Q01_binom" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::


:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292829530179315457/embed" aria-label="Q02_water" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::

