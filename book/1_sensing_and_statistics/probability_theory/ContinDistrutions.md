# Continuous probability distributions

Probability distributions of natural phenomena and experimental outcomes with a noncountable infinite number of outcomes can take an infinite number of forms, but in practice a few dozen specific continuous probability distribution are used to model them. Each of those distributions depends on certain parameters such that the number of possibilities to *shape* these distributions is still limitless. In this course, we will only look at a small subset of well known distributions that are frequently used for adequately describing the probabilistic properties of continuous random variables. Being able to understand and work with these distributions allows you to explore other distributions as well.

## Learning objectives

After studying *Continuous probability distributions* you will be able to ...
* identify and apply the uniform, normal, exponential and lognormal distributions apply in real-world contexts
* be able to explain dependence on parameters of these distributions


## Uniform distribution

We have already seen the uniform distribution of a discrete random variable. Likewise we can define the uniform distribution of a continuous random variable as follows.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Uniform distribution:}$

Random variable $X$ is uniformally distributed on the interval [$a,b$] if its probability density function is given as:

$f_X(x)=
\begin{cases} \frac{1}{b-a}& \text{for } a\leq x\leq b \\
0 & \text{otherwise}\end{cases}$

with $\mathbb{E}(X)=\frac{1}{2}(a+b)$ and $Var(X)=\frac{1}{12}(b-a)^2$.

Notation: $X\sim U(a,b)$

</div>

An example of the pdf and distibution function is shown in {numref}`figure {number} <uni_pdfcdf>`.

````{figure} ../../figures/part-a_uni_pdfcdf.png
---
name: uni_pdfcdf
width: 80%
align: center
---
Probability density function and distribution function of $X\sim U(-1,1)$.
````

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example signal transmission}$

A signal transmitted by a satellite arrives at time $t$ at a ground station. The received signal has a sinusoidal form:

$
Y(t) = a\sin(\omega t + X)
$

with amplitude $a$ and angular frequency $\omega$, and a random phase shift $X$. The phase shift has range $[0,2\pi]$ and each value in this interval has the same probability of occurrence, hence $X\sim U(0,2\pi)$.

</div>

:::{card} Exercise

Derive the distribution function $F_X(x)$ of $X\sim U(a,b)$.

*Solution at end of this page.*

:::

## Normal distribution

The famous bell-shaped probability density function that we have already seen in some examples before is the pdf of the *normal* distribution, also referred to as the Gaussian distribution. It describes many natural phenomena that occur in nature, think of the distribution of heights of persons, as well as the variability in the outcomes of experiments, think of repeated distance measurements.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Normal distribution:}$

Random variable $X$ is normally distributed if its probability density function is given as:

$f_X(x)=
\frac{1}{\sigma\sqrt{2 \pi}} \exp \{ -\frac{1}{2} \left( \frac{x-\mu}{\sigma} \right)^{2} \},~-\infty < x < \infty 
$

with $\mathbb{E}(X)=\mu$ and $Var(X)=\sigma^2$.

Notation: $X\sim N(\mu,\sigma^2)$

</div>

Examples of the pdf and distibution function are shown in {numref}`figure {number} <normal_pdfcdf>`. Note that the normal distribution is determined by the mean $\mu$ and variance $\sigma^2$ of the random variable.

````{figure} ../../figures/part-a_normal_pdfcdf.png
---
name: normal_pdfcdf
width: 80%
align: center
---
Probability density function and distribution function of $X\sim N(0,\sigma^2)$ for three values of $\sigma$.
````

## Exponential distribution

The exponential distribution is often concerned with the service times or the time between events. Examples: the time a computer part, GNSS receiver, or any other device lasts; the time between two earthquakes or tsunamis. 

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Exponential distribution:}$

Random variable $X$ is exponentially distributed if its probability density function is given as:

$f_X(x)=
\begin{cases} \lambda \exp(-\lambda x),& \text{for } x\geq 0 \\
0 & \text{otherwise}\end{cases}$
 

with parameter $\lambda>0$, $\mathbb{E}(X)=\frac{1}{\lambda}$ and $Var(X)=\frac{1}{\lambda^2}$.

Notation: $X\sim Exp(\lambda)$

</div>

The parameter $\lambda$ is called the decay parameter. In reliability engineering, the mean lifetime $1/\lambda$ is called the Mean Time To Failure or Mean Time Between Failures.

Examples of the pdf and distibution function are shown in {numref}`figure {number} <exp_pdfcdf>`. 

````{figure} ../../figures/part-a_exp_pdfcdf.png
---
name: exp_pdfcdf
width: 80%
align: center
---
Probability density function and distribution function of $X\sim Exp(\lambda)$ for three values of $\lambda$.
````

:::{card} Exercise

Derive the distribution function $F_X(x)$ of $X\sim Exp(\lambda)$.

*Solution at end of this page.*

:::


## Lognormal distribution

Growth processes in nature can often be modeled by a nonsymmetric distibution such as the lognormal distribution. Examples in our field are concentrations of particle matter in the atmosphere or river discharge volumes.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Lognormal distribution:}$

Random variable $X$ is lognormally distributed if its probability density function is given as:

$f_X(x)=
\frac{1}{x\sigma\sqrt{2 \pi}} \exp \{ -\frac{1}{2} \left( \frac{\ln x-\mu}{\sigma} \right)^{2} \},~-\infty < x < \infty 
$

with $\mathbb{E}(X)=\exp(\mu+\frac{\sigma^2}{2})$ and $Var(X)=(\exp \sigma ^{2}-1 )\exp( 2\mu +\sigma ^{2})$.

Notation: $X\sim Lognormal(\mu,\sigma^2)$

</div>

Note that $\ln X \sim N(\mu,\sigma^2)$.

Examples of the pdf and distibution function are shown in {numref}`figure {number} <lognormal_pdfcdf>`. Note that the lognormal distribution is determined by the mean $\mu$ and variance $\sigma^2$ of the random variable.

````{figure} ../../figures/part-a_lognormal_pdfcdf.png
---
name: lognormal_pdfcdf
width: 80%
align: center
---
Probability density function and distribution function of $X\sim Lognormal(0,\sigma^2)$ for three values of $\sigma$.
````

```{admonition} Solutions of exercises
:class: tip, dropdown

For the distribution function of $X\sim U(a,b)$ we have:

$
F_X(x)=\mathsf{P}(X\leq x) \begin{cases}
0 &\text{for } x<a\\
\frac{x-a}{b-a} & \text{for } a\leq x\leq b\\
1 & \text{for } x>b
\end{cases}
$

since if $a\leq x\leq b$ the probability $\mathsf{P}(X\leq x)$ is equal to the area below the pdf, which is $(x-a)\cdot f_X(x)= \frac{x-a}{b-a}$.

For the distribution function of $X\sim Exp(\lambda)$ we have:

$
F_X(x)=\int_{-\infty}^x \lambda \exp(-\lambda t)dt = 1-\exp(-\lambda x)
$

```

:::{card} Exercise

<iframe src="https://tudelft.h5p.com/content/1292831239836069137/embed" aria-label="U_quiz" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292831219009944247/embed" aria-label="norm_quiz" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>


<iframe src="https://tudelft.h5p.com/content/1292831231276417507/embed" aria-label="Exp_dist" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292831211736706777/embed" aria-label="Exp_Wind" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::





