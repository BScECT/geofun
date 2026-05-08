## Heteroscedasticity and weighted least squares

Observations are never perfect, and we have to account for their uncertainty when evaluating our estimation results (and hence predictions). But not all observations have the same uncertainty. How to deal with this?

### Precision of observations

Assuming that the errors are a realization of a random variable, assumed to be normally distributed, we can describe the uncertainty or **precision** by their variance, $\sigma^2$.

Let's assume that we use the same instrument to collect $n$ *repeated* observations of the same variable (e.g., a fixed distance). The outcomes of these repeated measurements could look like those in {numref}`figure {number} <randome>`. Let's assume we know the true value $\mu$ (e.g., calibration distance); we can see that the repeated measurements fluctuate around $\mu$. The empirical mean will approximate $\mu$, especially if $n$ is large (law of large numbers). 

````{figure} ../figures/part-b_randomerrors.png
---
name: randome
width: 80%
align: center
---
Repeated measurements with mean $\mu$ (left) for which the errors are realizations from the normal distribution $\mathcal{N}(0,\sigma^2)$ (right).
````

The variance can be estimated as:

$$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^n (y_i-\mu)^2$$

Note that if $\mu$ would not be known, we would replace it by the empirical mean $\bar{y}$, and we should divide by $n-1$, see [Descriptive Statistics](1:descriptive_statistics).

With this approach, we can thus calibrate an instrument, and consider the estimated variance as the true variance, such that we can assess the precision of our estimation results.

### Heteroscedasticity (different variances)

The *ordinary* least squares method as introduced in [the previous chapter](2:regression) provides the *best* estimates in case all observation errors can be assumed to have the same variance and are independent. However, it may occur that this is not the case. Examples:

* measurements are taken with different sensors of different quality
* measurement precision may depend on environmental/weather conditions (this may for example lead to an increase in variance with distance)

Recall that the least squares principle is to minimize the sum of squared residuals, i.e.,

$$\min\sum_{i=1}^n r_i^2 =\min\boldsymbol{r}^T \boldsymbol{r} $$

with $ \boldsymbol{r} = \boldsymbol{y} - \boldsymbol{X}\boldsymbol{\hat{\beta}}$

Now, if we know that some of the observations are more precise than the others, it makes sense that we demand that the residuals (estimated errors) for those observations are smaller, since you expect the errors to be smaller. This can be accomplished by giving those observations more weight, which means the minimization problem becomes:

$$\min\sum_{i=1}^n w_ir_i^2 =\min\boldsymbol{r}^T \boldsymbol{Wr} $$

where $\boldsymbol{W}$ is the weight matrix with weights $w_i$ on the diagonal. 

:::{card} Looking at the minimization problem above: why does it make sense to assign larger weights to more precise observations?


 ```{admonition} Solution
:class: tip, dropdown 
It makes sense, since a larger weight $w_j$ should result in a smaller $r_j$ (and vice versa) in the minimization of the weighted sum of squared residuals, while in case of equal weights all residuals are expected to be equal.
```
:::

The weight matrix $\boldsymbol{W}$ must be a symmetric and invertible matrix. 

The *weighted* least squares solutions follows thus by miminiming:

$$
    \begin{align}
        S_{\text{res}}(\boldsymbol{\hat{\beta}}) &= \left(\boldsymbol{y} - \boldsymbol{X}\boldsymbol{\hat{\beta}}\right)^T \boldsymbol{W}\left(\boldsymbol{y} - \boldsymbol{X}\boldsymbol{\hat{\beta}}\right) \\
         &= \boldsymbol{y}^T \boldsymbol{W}\boldsymbol{y} - \boldsymbol{y}^T \boldsymbol{W}\boldsymbol{X}\boldsymbol{\hat{\beta}} - \boldsymbol{\hat{\beta}}^T \boldsymbol{X}^T \boldsymbol{W}\boldsymbol{y} + \boldsymbol{\hat{\beta}}^T \boldsymbol{X}^T \boldsymbol{W}\boldsymbol{X}\boldsymbol{\hat{\beta}} \\
    \end{align}
$$

which gives:

$$\boldsymbol{\hat{\beta}} = \left(\boldsymbol{X}^T \boldsymbol{W}\boldsymbol{X}\right)^{-1} \boldsymbol{X}^T \boldsymbol{W} \boldsymbol{y}$$

The question comes: how to choose the weights? If the errors of the different observations are independent, a sensible choice would be to choose the weight matrix as a diagonal matrix with the *inverse* variances of the individual observations as its diagonal elements:

$$\boldsymbol{W} =\begin{bmatrix} \frac{1}{\sigma_1^2}& & & 0 \\ &\frac{1}{\sigma_2^2}& &  
\\ && \ddots & 
\\ 0&&  & \frac{1}{\sigma_n^2} \end{bmatrix}$$

 A more precise observation will namely have a smaller variance, but should get a larger weight. In fact, this turns out to be a very good idea. If the errors of the different observations are indeed independent, in this way the weighted least squares solution provides the *best* estimates, i.e., you cannot find estimates with a better precision (smaller variance).

Note that in [Uncertainty in regression](uncertaintyreg) the confidence interval for linear regression was derived assuming that the variance of the observation errors is not known. For estimation problems where the variances can be assumed known (based on calibration), and the observation errors are normally distributed and independent, we have that the variance of the estimated parameters is equal to:

$$ \sigma_{\hat{\beta}_j}= \left(\boldsymbol{X}^T \boldsymbol{W}\boldsymbol{X}\right)^{-1}_{jj} $$

where $\boldsymbol{W}$ is the diagonal matrix with the inverse variances of the observation errors as diagonal elements.

The confidence interval then becomes

$$
    \hat{\beta}_j \pm z_{\alpha/2} \sigma_{\hat{\beta}_j}
$$




