# Formula sheet

This formula sheet will be provided on the exam.

## Probability formulas

| Description      | Formula | 
| :---------------- | :------------------------------------------------ | 
| Addition rule            |   $\mathsf{P}(A\cup B) = \mathsf{P}(A) + \mathsf{P}(B)- \mathsf{P}(A\cap B)$  | 
| Conditional probability       |   $\mathsf{P}(A\mid B) = \frac{\mathsf{P}(A\cap B)}{\mathsf{P}(B)}$   | 
| Total probability rule*          |   $\mathsf{P}(A) = \sum_{i=1}^n \mathsf{P}(A\mid B_i)\mathsf{P}(B_i)$  | 
| Bayes' rule          |   $\mathsf{P}(B_j\mid A) = \frac{\mathsf{P}(A\mid B_j)\mathsf{P}(B_j)}{\mathsf{P}(A)}$  | 
| Independence | $\mathsf{P}(A\mid B) = \mathsf{P}(A)$ and $\mathsf{P}(B\mid A) = \mathsf{P}(B)$ |
| Central limit theorem (sum) | $\sum_{i=1}^n X_i \overset{d}{\sim}N(n\mu,n\sigma^2)$, ($X_i$ i.i.d.)  |
| Central limit theorem (mean) | $\bar{X}_n \overset{d}{\sim}N(\mu,\frac{\sigma^2}{n})$  |

*where the $B_i$ form a partition of the sample space.



## Discrete distributions

The probability mass function, expectation and variance of a selection of probability distributions is given.

### Discrete uniform distribution, $X\sim U(a,b)$

$p_X(k)=\frac{1}{n},\;\; k=1,2,\ldots,n$ with $0\leq p \leq 1$

$\mathbb{E}(X)=\frac{a+b}{2},\;Var(X)=\frac{(b-a+1)^2-1}{12}$

### Bernoulli distribution, $X\sim Ber(p)$

$p_X(1)=p,\;  p_X(0)=1-p$, with $0\leq p \leq 1$

$\mathbb{E}(X)=p,\;Var(X)=p(1-p)$

### Binomial distribution, $X\sim Bin(n,p)$

$p_X(k)=\binom{n}{k}p^k (1-p)^{n-k},\;\; \text{for } k=0,1,\ldots,n$, with $0\leq p \leq 1$, and $n\geq 1$

$\mathbb{E}(X)=np,\;Var(X)=np(1-p)$

### Geometric distribution, $X\sim Geo(p)$

$p_X(k)=p^k (1-p)^{n-k},\;\; \text{for } k=1,2,\ldots$, with $0\leq p \leq 1$

$\mathbb{E}(X)=\frac{1}{p},\;Var(X)=\frac{1-p}{p^2}$

### Poisson distribution, $X\sim Pois(\lambda)$

$p_X(k)=\frac{\lambda^k}{k!}\exp\{-\lambda\},\;\; \text{for } k=0,1,\ldots,n$, with $\lambda >0$.

$\mathbb{E}(X)=\lambda,\;Var(X)=\lambda$


## Continuous distributions

The probability density function, expectation and variance of a selection of probability distributions is given. 

### Continuous uniform distribution, $X\sim U(a,b)$

$f_X(x)=
\begin{cases} \frac{1}{b-a}& \text{for } a\leq x\leq b \\
0 & \text{otherwise}\end{cases}$

$\mathbb{E}(X)=\frac{1}{2}(a+b)$, $Var(X)=\frac{1}{12}(b-a)^2$.

### Normal distribution, $X\sim N(\mu,\sigma^2)$

$f_X(x)=
\frac{1}{\sigma\sqrt{2 \pi}} \exp \{ -\frac{1}{2} \left( \frac{x-\mu}{\sigma} \right)^{2} \},~-\infty < x < \infty 
$

$\mathbb{E}(X)=\mu$, $Var(X)=\sigma^2$.

### Exponential distribution, $X\sim Exp(\lambda)$

$f_X(x)=
\begin{cases} \lambda \exp\{-\lambda x\},& \text{for } x\geq 0 \\
0 & \text{otherwise}\end{cases}$, with parameter $\lambda>0$, 

$\mathbb{E}(X)=\frac{1}{\lambda}$,  $Var(X)=\frac{1}{\lambda^2}$.

### Lognormal distribution, $X\sim Lognormal(\mu,\sigma^2)$

$f_X(x)=
\frac{1}{x\sigma\sqrt{2 \pi}} \exp \{ -\frac{1}{2} \left( \frac{\ln x-\mu}{\sigma} \right)^{2} \},~-\infty < x < \infty 
$

$\mathbb{E}(X)=\exp\{\mu+\frac{\sigma^2}{2}\}$, $Var(X)=(\exp \sigma ^{2}-1 )\exp\{ 2\mu +\sigma ^{2}\}$.

## Table standard normal distribution, $Z\sim N(0,1)$

The table shows one-sided (**right-hand**) probabilities $\alpha$ as function of the value
$k_\alpha$, i.e. $\alpha = P(Z\geq k_\alpha)$.

```{csv-table} Standard Normal Distribution, Upper-Right Tail
   :file: normal_right.csv
   :widths: 30, 30, 30, 30, 30, 30, 30, 30, 30, 30, 30
   :header-rows: 1
   :align: center
```