# A deeper dive into the normal distribution

The normal distribution deserves special attention as it is so crucial. Furthermore, we will see that we can evaluate probabilities of events even without the need for a computer.


## Properties of normal distribution

Recall that the pdf of a normally distributed random variable $X$ is given by:

$$
f_X(x)= \frac{1}{\sigma\sqrt{2 \pi}} \exp( -\frac{1}{2} \left( \frac{x-\mu}{\sigma} \right)^{2} ),~-\infty < x < \infty 
$$

with expectation $\mathbb{E}(X)=\mu$ and variance $Var(X)=\sigma^2$.

The pdf is symmetric at $\mu$, which means that the median and mode are all equal to $\mu$ as well.

The pdf has its points of inflection at $x = \mu \pm \sigma$: it is concave if $x\in [\mu - \sigma,\mu + \sigma]$, and is convex otherwise.

The normal pdf approaches the horizontal axis asymptotically, hence extends infinitely, in both directions.

````{figure} ../../figures/part-a_normalpdf.png
---
name: normal_pdf
width: 40%
align: center
---
Probability density function of $X\sim N(\mu,\sigma^2)$.
````

## Standard normal distribution

If the mean $\mu=0$ and variance $\sigma^2=1$ we obtain the so-called *standard* normal distribution with pdf:

$$
f(Z)(z)=\frac{1}{\sqrt{2 \pi}} \exp( -\frac{1}{2} z^{2} ),~-\infty < x < \infty 
$$

Hence, $Z\sim N(0,1)$. Note that $Z$ is specifically used for random variables with a standard normal distribution.

For $Z\sim N(0,1)$ we can use a tabulation to find the probabilities $\mathsf{P}(Z\geq k)=1-F_Z(k)$ (or vice versa, to find the $k$ for a given probability $\alpha$), see {numref}`figure {number} <normal_standard>` and [Table Standard Normal distribution](table_standardnormal).

````{figure} ../../figures/part-a_standardnormal.png
---
name: normal_standard
width: 40%
align: center
---
Probability density function of $Z\sim N(0,1)$ with $\mathsf{P}(Z\geq k)=\alpha$.
````

When using the table, it is good to see that:

* $\mathsf{P}(Z\leq -k)=\mathsf{P}(Z\geq k)$ (due to symmetry around 0)
*  $\mathsf{P}(a\leq Z\leq b)=\mathsf{P}(Z\leq b)-\mathsf{P}(Z\leq a) $
* $\mathsf{P}(Z\leq b) = 1 - \mathsf{P}(Z\geq b)$

Try yourself (tip: open the [Table Standard Normal distribution](table_standardnormal) in a new tab).

:::{card} Exercises (worked out solution at the end)

<iframe src="https://tudelft.h5p.com/content/1292832112006758507/embed" aria-label="standardnorm" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::

## Probability calculations by transforming to standard normal distribution

We know that we can calculate the probability to be in a certain interval $[a,b]$ as:

$$
\begin{align*}
\mathsf{P}(a\leq X \leq b)&= \int_a^b f_X(x)dx \\
&= \frac{1}{\sigma\sqrt{2 \pi}}\int_a^b\exp( -\frac{1}{2} \left( \frac{x-\mu}{\sigma} \right)^{2} )dx\\
& = \frac{1}{\sqrt{2 \pi}}\int_{\frac{a-\mu}{\sigma}}^{\frac{b-\mu}{\sigma}}\exp( -\frac{1}{2} z^{2} )dzd\\
&= \mathsf{P}(\frac{a-\mu}{\sigma} \leq Z \leq \frac{b-\mu}{\sigma})
\end{align*}
$$

where we applied the substitution $z=\frac{x-\mu}{\sigma}$, implying that $dx=\frac{1}{\sigma}dz$.

Since we can use [Table Standard Normal distribution](table_standardnormal) to calculate the probability $\mathsf{P}(\frac{a-\mu}{\sigma} \leq Z \leq \frac{b-\mu}{\sigma})$ this shows how we can use the transformation $Z=\frac{X-\mu}{\sigma}$ to calculate probabilities $\mathsf{P}(a\leq X \leq b)$ for any $X\sim N(\mu,\sigma^2)$.

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example ball bearings}$

The diameter of a ball bearing is an important component part, and for a certain instrument the specifications on the diameter are set to be $3.0 \pm 0.01$ cm. The implication is that no part falling outside these specifications will be accepted. 

It is known that in the process the diameter of a ball bearing has a normal distribution $X \sim {\rm N}(3.00, 0.005^{2})$. On the average, how many manufactured ball bearings will be scrapped? 

What is the percentage of ball bearing that will be accepted on average?


In order to determine this percentage, we need to compute $\mathsf{P}(2.99 < X < 3.01)$. 

Using the transformation $Z=(X-\mu)/\sigma$, it follows that 

$$
\begin{align*}
\mathsf{P}(2.99 < X < 3.01)&=\mathsf{P}(\frac{2.99-3.00}{0.005} < Z < \frac{2.99-3.00}{0.005})\\
&= 1-\mathsf{P}(Z\geq 2) - \mathsf{P}(Z\geq 2)\\
&= 1-2\cdot 0.0228 = 0.9544
\end{align*}
$$

which shows that we can expect 95.44\% of the ball bearingst to be accepted.

</div>

```{admonition} Solutions to exercises
:class: tip, dropdown

$\mathsf{P}(Z\leq 2)= 1- \mathsf{P}(Z\geq 2) = 1-0.0228$

$\mathsf{P}(-2.35 \leq Z\leq 3)= \mathsf{P}(Z\leq 3) - \mathsf{P}(Z\geq 2.35) = 1- \mathsf{P}(Z\geq 3) - \mathsf{P}(Z\geq 2.35)=1-0.0013-0.0094$

$\mathsf{P}(-2.35 \leq Z\leq -1.96)= \mathsf{P}(Z\geq 1.96) - \mathsf{P}(Z\geq 2.35) =0.0250-0.0094$

```

## Sum of independent normally distributed random variables

For two *independent* random variables $X_1\sim N(\mu_1,\sigma_1^2)$ and $X_2\sim N(\mu_2,\sigma_2^2)$ we have that:

$
Y= X_1 + X_2 \sim N(\mu_1+\mu_2,\sigma_1^2+\sigma_2^2)
$

This can be extended to the sum of $n$ independent normally distributed random variables:

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Sum of independent normally distributed random variables:}$

Let $X_i\sim N(\mu_i,\sigma_i^2)$ be independent, then their sum is normally distributed as:

$
Y= \sum_{i=1}^{n} X_i \sim N(\sum_{i=1}^{n}\mu_i,\sum_{i=1}^{n}\sigma_i^2)
$

</div>

Note that in case the mean and variance of all $X_i$ are identical, we get $Y\sim N(n\mu,n\sigma^2)$.


:::{card} Exercise

<iframe src="https://tudelft.h5p.com/content/1292831267040301097/embed" aria-label="Norm_solar" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::