(meanvar)=
# Expectation (mean) and variance

Moments of a distribution are quantitative measures that describe the location and shape of a distribution. Here, we will only focus on the first two moments: *expectation* (location) and *variance* (spread).

## Expectation = mean
The expectation, also referred to as mean, is the first moment of a probability distribution and is defined as:

$$
\mathbb{E}(X) = \sum_{i=1}^n x_i p_X (x_i)
$$

for discrete distributions, where $p_X(x_i)$ are the probability masses for all possible outcomes $x_i$, $i=1,\ldots,n$. The expectation is thus the *weighted average* of all possible outcomes, and as such is equal to the center of mass of the pdf.

For continuous distributions the equivalent is:

$$
\mathbb{E}(X) = \int_{-\infty}^{\infty} x f_X (x)dx
$$

where $f_X (x)$ is the probability density function.

We will often use the notation $\mathbb{E}(X)=\mu_X$ (sometimes also without subscript if it is clear which random variable it concerns).

The empirical or sample mean based on $n$ outcomes (or: realizations) $x_i$ can be computed as:

$$
\hat{\mu}_X = \frac{1}{n}\sum_{i=1}^n x_i
$$

where we use the ^-symbol to indicate it is an *estimate* of the mean based on a number of realizations.

## Variance 

The outcomes or realizations of a random variable will by definition inhibit a certain spread; they will fluctuate around the mean. The variance  or dispersion  of a random variable  is a measure of these fluctuations around the mean, and is defined by:

$$
\begin{align*}
Var(X)&= \mathbb{E}((X-\mu_X)^2)\\
&= \sum_{i=1}^n (x_i-\mu_X)^2 p_X (x_i)
\end{align*}
$$

for discrete random variables, and 

$$
\begin{align*}
Var(X)&= \mathbb{E}((X-\mu_X)^2)\\
&= \int_{-\infty}^{\infty} (x-\mu_X)^2 f_X (x)dx
\end{align*}
$$

for continuous random variables.

Hence, the variance equals the expectation of the squared deviations from the mean value. The variance is the *second central moment*.

Based on the formula for the sample mean, we can also find an expression for the sample variance:

$$
Var(X) = \frac{1}{n}\sum_{i=1}^n (x_i-\hat{\mu}_X)^2
$$


We will often use the notation $Var(X)=\sigma^2_X$ (again sometimes without subscript).

The standard deviation $\sigma_X$ of random variable $X$ is given by the square root of its variance.

## Mean, median, mode, variance

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

Expectation = mean of a continuous random variable $X$:

$
\mathbb{E}(X) = \mu_X= \int_{-\infty}^{\infty} x f_X (x)dx
$

Median $x_{0.5}$ of a continuous random variable $X$ is the value for which:

$
F_X(x_{0.5}) = 0.5
$

Mode $x_{m}$ of a continuous random variable $X$ is the value for which:

$
f_X(x_{m}) = \max
$

Variance of a continuous random variable $X$:

$
Var(X)=\sigma^2_X = \mathbb{E}((X-\mu_X)^2)= \int_{-\infty}^{\infty} (x-\mu_X)^2 f_X (x)dx
$

</div>

## Mean and variance of $Y=rX+s$

A common example where we may be interested in a linear transformation of a random variable is a change of units. Let $X$ for instance be a temperature in $^oC$ (Celsius), which we would like to transform to $^oF$ (Fahrenheit). Then $Y = \frac{9}{5}X+32$.

If we would know the mean and variance of $X$, the question arises what the corresponding mean and variance of $Y$ will be.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Linear transformation } Y=rX+s$

$\mathbb{E}(Y)=r\mathbb{E}(X)+s$

$Var(Y)=r^2 Var(X)$

</div>

For the mean it may be easy to see that this relation holds by realizing that if we add the same value $s$ to all outcomes, the mean will be shifted accordingly. Similarly, mulitplying all values with the same $r$, means that also the mean will be multiplied with $r$. For the sample mean we have thus:

$$
\hat{\mu}_Y = \frac{1}{n}\sum_{i=1}^n y_i =\frac{1}{n}\sum_{i=1}^n (rx_i+s)=\frac{1}{n}\sum_{i=1}^n rx_i+\frac{1}{n}ns=r\hat{\mu}_X+s
$$

For the variance it is important to realize that adding $s$ to all outcomes does not influence the spread in the outcomes, since we are looking at the deviations of the mean, and both the outcomes and mean are shifted by $s$. Since the variance is the weighted average of the **squared** deviations, multiplying the outcomes with $r$ implies that the variance must be multiplied with $r^2$.