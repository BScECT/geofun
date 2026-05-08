## Estimation problems

Linear regression can be used to quantify relationships between physical parameters, and to predict outcomes of a certain process / property (dependent variables) based on observations of another variable (independent variable). Prediction based on linear regression is convenient when the dependent variables are *hard-to-measure*, whereas the independent variables can be easily measured. In the latter case, the idea is that based on a limited sample of observations of both the dependent and independent variables, we estimate the model parameters that describe their relationship. Once the model parameters are 'known', the dependent parameters can be predicted using **only** observations of the independent variables.


Examples are:

* magma eruption temperatures (dependent) based on $Si_2O$ content (independent)
* river run-off (dependent) based on rainfall amount (independent)
* tree-ring width (dependent) based on temperature and precipitation (independent)
* geothermal power production (dependent) based on brine temperature (independent)
* structural deformation (dependent) based on wind load (independent)

In Earth, Climate & Technology we are also looking at problems like estimating:

* positions using GNSS observations
* land subsidence as a function of time series of height measurements
* sea level change based on satellite altimetry or tide gauge measurement

For all these problems, least squares can be applied to *estimate* the unknown model parameters, that describe a linear relationship:

$$\boldsymbol{y} = \boldsymbol{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

where $\boldsymbol{X}$ is the design matrix and $\boldsymbol{\beta}$ the unknown vector with model parameters, and $\boldsymbol{\epsilon}$ the error vector.

The uncertainty in the estimation results depends on the errors $\boldsymbol{\epsilon}$ as well as on how well the assumed linear relationship represents the true relationship. Until now, it was assumed that the errors have a constant variance (homoscedasticity) and are independent. In this chapter we will also look at problems where this is not the case (heteroscedasticity) and how to deal with that by introducing *weighted* least squares. Furthermore, we will look into precision versus accuracy, show a practical example how the precision of observables can be estimated, and also which factors influence the precision and accuracy of our estimation results.

### Linear trend model for time series 
The unknown parameters are the intercept $\beta_0$ and rate of change (velocity) $\beta_1$. The observation equation of a single observation $y_i$ is:

$$
y_i= \beta_0 + \beta_1 t_i +\epsilon_i
$$

where the observation times, or epochs, $t_i$ are assumed to be known.

The linear functional model for $n$ observables becomes:

$$
\begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix} = \underset{\boldsymbol{X}}{\underbrace{\begin{bmatrix} 1 & t_1 \\ 1 & t_2  \\ \vdots & \vdots \\ 1 & t_n \end{bmatrix}}}\underset{\boldsymbol{\beta}}{\underbrace{\begin{bmatrix} \beta_0 \\ \beta_1 \end{bmatrix}}}+\boldsymbol{\epsilon}
$$

Examples where as a first guess the linear trend model could be applied (but might be too simplistic): subsidence of a point due to gas extraction, uplift of a point due to water injection, sea level rise at a location over the last 10 years.

:::{card} Exercise

What is the linear model if the observation equations are given by the quadratic function $y_i= \beta_0 + \beta_1 t_i +\beta_2 t_i^2 + \epsilon_i $. Is this a linear model?

```{admonition} Solution
:class: tip, dropdown

$$
\begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix} = \underset{\boldsymbol{X}}{\underbrace{\begin{bmatrix} 1 & t_1 & t_1^2\\ 1 & t_2 & t_2^2 \\ \vdots & \vdots \\ 1 & t_n & t_n^2 \end{bmatrix}}}\underset{\boldsymbol{\beta}}{\underbrace{\begin{bmatrix} \beta_0 \\ \beta_1 \\ \beta_2 \end{bmatrix}}}+\boldsymbol{\epsilon}
$$

This is model is linear in $\boldsymbol{\beta}$, therefore we refer to it as a linear model.
```
:::

### Step function
Consider a process with unknown parameter $\beta_0$ assumed to be constant up till time $t_{i-1}$, and a sudden change (step) at time $t_i$, after which the parameter remains constant at $\beta_1$. See {numref}`stepfun`.

```{figure} ../figures/part-b_stepfunction.png
---
height: 300px
name: stepfun
---
Observations with fitted step function.
```

The linear model can be written as:

$$
\begin{bmatrix} y_1 \\ \vdots \\ y_{i-1} \\ y_i \\ \vdots \\ y_m \end{bmatrix} = \underset{\boldsymbol{X}}{\underbrace{\begin{bmatrix} 1 & 0 \\ \vdots & \vdots \\ 1 & 0 \\ 0 & 1 \\ \vdots & \vdots \\ 0& 1 \end{bmatrix}}}\underset{\boldsymbol{\beta}}{\underbrace{\begin{bmatrix} \beta_0 \\ \beta_1 \end{bmatrix}}}+\boldsymbol{\epsilon}
$$

Such model may apply when considering deformation events in the subsurface, but can also be applicable in case of sensor replacement where one sensor has an offset with respect to the other (which would have to be calibrated).

:::{card} Exercise

The linear model of the step function can also be parameterized in terms of the initial value $\beta_0$ plus the step size $s=\beta_1-\beta_0$. Give the corresponding model.

```{admonition} Solution
:class: tip, dropdown

$$
\begin{bmatrix} y_1 \\ \vdots \\ y_{i-1} \\ y_i \\ \vdots \\ y_m \end{bmatrix} = \underset{\boldsymbol{X}}{\underbrace{\begin{bmatrix} 1 & 0 \\ \vdots & \vdots \\ 1 & 0 \\ 1 & 1 \\ \vdots & \vdots \\ 1& 1 \end{bmatrix}}}\underset{\boldsymbol{\beta}}{\underbrace{\begin{bmatrix} \beta_0 \\ s \end{bmatrix}}}+\boldsymbol{\epsilon}
$$

```
:::

:::{card} Exercise
<iframe src="https://tudelft.h5p.com/content/1292060588665722877/embed" aria-label="Quiz_subduction" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>
:::

(positioning)=
#### GNSS Positioning 
As a final example we will consider a non-linear functional model for estimating the unknown position and clock error $\boldsymbol{\beta}=\begin{bmatrix} x, y, z,b\end{bmatrix}^T$ of a Global Navigation Satellite System (GNSS) receiver on Earth. The observables are pseudoranges measured for $n \geq 4$ GNSS satellites with known positions $\begin{bmatrix} x_i, y_i, z_i\end{bmatrix}^T$.

```{figure} https://upload.wikimedia.org/wikipedia/commons/9/91/GDOP_good.svg
---
height: 200px
name: GNSS_GDOP
---
GNSS positioning: the position of the user is estimated from four GNSS satellites. Figure adapted from [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:GDOP_good.svg).
```

The functional model comprises $n$ non-linear functions of the unknown parameter vector $\boldsymbol{\beta}$:

$$
\begin{bmatrix} y_1 \\ y_2 \\\vdots \\ y_n \end{bmatrix} = \begin{bmatrix} \sqrt{(x_1-x)^2+(y_1-y)^2+(z_1-z)^2}+b\\ \sqrt{(x_2-x)^2+(y_2-y)^2+(z_2-z)^2} +b\\ \vdots \\ \sqrt{(x_n-x)^2+(y_n-y)^2+(z_n-z)^2}+b\end{bmatrix}+\boldsymbol{\epsilon}
$$

Where $y_i$ is the pseudorange measurement to satellite $i$. Note that the model is non-linear in $\boldsymbol{\beta}$, since three of the unknown parameters appear inside a square root. For such problems we would have to apply non-linear least squares, but this is outside the scope of this course.
