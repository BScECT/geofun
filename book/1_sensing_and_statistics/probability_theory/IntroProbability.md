(IntroP) =
# Introduction to probability

## Notation

| Description       | Notation | 
| :---------------- | :------------: | 
| Event            |   $A$   | 
| Complement of event $A$           |   $A^c$   | 
| Intersection of  $A$ and $B$    |  $A \cap B$   | 
| Union of  $A$ and $B$ | $A \cup B$|
| $A$ is subset of $B$ | $A \subset B$ |
| Set difference of  $A$ and $B$ | $A\setminus B$ |
| Probability of event $A$ | $\mathsf{P}(A)$ |
| Conditional probability of $A$ given $B$ | $\mathsf{P}(A\|B)$ |
| Sample space | $\Omega$|

## Learning objectives

After studying the Introduction probability theory you will be able to...
* explain why uncertainty needs to be accounted for in science and engineering
* define sample spaces and events
* execute set operations: perform and visualize (with Venn diagrams) unions ($A \cup B$), intersections ($A \cap B$), complements ($A^c$), and set differences 
* explain and apply Kolmogorov's Axioms of Probability
* explain the relation between relative frequency and probability

## Uncertainty

Uncertainty is part of every day life, but here we will focus on uncertainty that we have to deal with in science and engineering, with a focus on the field of Earth, Climate & Technology. Dealing with uncertainty is a necessity, since:

* We are observing phenomena with uncertainty - exact measurements do not exist! Hence we need to be able to separate the *signal of interest* we are trying to measure from the *noise* or *disturbances* that affect our observations. 
* We are building complex systems from components with uncertain lifetimes and in environments with uncertain conditions. Hence, we need to design systems taking into account reliability versus costs.
* We need to make decision in uncertain situations and hence need to minimize the risk of a wrong decision.

More specific examples from our field:

* To ensure energy security we need to be able to predict the available energy production of wind farms, for which we would need to know (amongst others) the wind speed. For longer term forecasts, we cannot rely on measurements, but need to use historical data and models, which both will not be perfect.
* Rising sea levels, more frequent extreme weather events and ground subsidence in The Netherlands require us to monitor our dikes and the surroundings. This is needed for instance in order to predict the impact of potential floodings, and inform the water boards about the need to increase the height of certain dikes. However, height measurements are not perfect, are not continuous, and have a limited spatial resolution (size of smallest unit in a map).
* Developing a geothermal well requires information about the subsurface to decide on drilling location, depth, orientation. However, knowledge about temperature, pressure, permeability, porosity, geological structures is again limited. At the same time, we need to minimize risks in terms of failures, maximize well productivity, and minimize environmental impact such as induced seismicity.

It is common to distinguish two types of uncertainty:

### Aleatoric uncertainty [in Latin *alea* is *rolling of dice*]
This is uncertainty due to natural variations, which are impossible to predict. A good example are certain weather phenomena, or variations in river flow. This type of uncertainty is irreducible.

### Epistemic uncertainty [in Greek *episteme* is *knowledge*]
This is uncertainty due to a lack of knowledge. This can be due to measurement errors, or due to limitations of the mathematical equations that are used to model a physical phenomenon. This type of uncertainty is reducible by taking more measurements or improving the models (for which generally also more data is needed).

In this course we will learn how probability distributions can be used to model both types of uncertainty.

## Fundamental concepts

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Terms and definitions}:$

- Sample space $\Omega$: all possible outcomes of an experiment
- Event $A$: subset of of the sample space
- Countable outcome: result of experiment can be assigned a distinct value
- Relative frequency: number of times that an event occurs divided by the total number of trials
</p>
</div>

So we need probability! But what is probability?

In situations where we have a *countable* number of outcomes (of an experiment) and each outcome is *equally likely*, it is rather straightforward to define probability. Let's take the well-known example of rolling dice. In this case we have 6 possible outcomes for each throw, hence we have sample space $\Omega = \{1,2,3,4,5,6\}$, and each outcome is equally likely in case of a fair die. We can then look at the probabilities of different *events*:

Probability that we throw
* a 1, denoted as event $A=\{1\}$: $\mathsf{P}(A)=\frac{1}{6}$
* an even number, i.e., event $A=\{2,4,6\}$: $\mathsf{P}(A)=\frac{3}{6}=\frac{1}{2}$
* smaller than 7, i.e., event $A=\{1,2,3,4,5,6\}$: $\mathsf{P}(A)=\frac{6}{6}=1$ (this is an example of a *sure event*)

Unfortunately, in many of our science and engineering problems it is not as simple as that. For instance wind speed is a *noncountable* parameter, and depending on location and time certain wind speeds will occur more frequently than others. One option then would be to collect wind speed measurements over a long time and create a histogram as shown in ({numref}`figure {number} <wind_histogram>`) , which shows the *relative frequencies* that the wind speed is in a certain interval.

````{figure} ../../figures/part-a_wind_histogram.png
---
name: wind_histogram
width: 95%
align: center
---
Histogram showing the relative frequency that wind speed in Delft is in a certain interval (based on data of one year).
````

Relative frequency in fact is only an estimate of the actual probability based on observed data and there is a dependency on the number of trials. A small number of trials will give a poor estimate. Gathering a large amount of data over a long timespan is not always possible, and sometimes those past data records simply do not exist. 

Is there then a definition of probability that can work? Kolmogorov came up with the following axiomatic definition, i.e., based on a set of rules.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Axiomatic definition of probability}:$

The probability of an event $A$ from sample space $\Omega$ is a number $\mathsf{P}(A)$ which satisfies three axioms:

1. $0 \leq \mathsf{P}(A) \leq 1$ (**non-negativity**)
2. $\mathsf{P}(\Omega)=1$ (**normalization**, probability of sure event)
3. $\mathsf{P}(A\cup B) = \mathsf{P}(A) + \mathsf{P}(B)$ if event $A$ and $B$ have no outcomes in common (**additivity**)
</div>

Looking at this definition, we can see that using relative frequency as an estimate of probability makes sense. Let $n$ be the total number of trials, and $n_A$ the number of times that event $A$ happens in an experiment. The relative frequency $\frac{n_A}{n}$ is then indeed always larger or equal than 0, and smaller than 1, since $0\leq n_A \leq n$. The sure event implies $n_A=n$, and the second axiom is also fulfilled. For two events that have no outcomes in common, we have that the number of times $n_{A\cup B}$ that $A$ or $B$ occurs is equal to $n_A + n_B$, which gives $\frac{n_{A\cup B}}{n}=\frac{n_A+n_B}{n}=\frac{n_A}{n}+\frac{n_B}{n}$, in line with the third axiom.

We can say that the axioms of probability are an abstraction of empirical evidence and can be used for defining a *probability model* for the problem at hand.

An important relation that can be derived from the second and thid axiom is that the probability that the complement $A^c$ of event $A$ occurs is:

<div style="background-color:#5f9c96 ; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Complement rule}:$

$
\mathsf{P}(A^c)=1-\mathsf{P}(A)
$
</div>

since $A^c \cup A = \Omega $ and hence $\mathsf{P}(A^c \cup A)=\mathsf{P}(A^c)+\mathsf{P}(A) = \mathsf{P}(\Omega)=1$. The second panel in ({numref}`figure {number} <venn_diagrams>`) illustrates the events in sample space $\Omega$.

````{figure} ../../figures/part-a_VennDiagrams.png
---
name: venn_diagrams
width: 95%
align: center
---
Venn diagrams illustrating set operations.
````

## Set theory

Set theory can used to derive more probability rules and relations. Sets are collections of elements, in our case outcomes. Hence, the sample space $\Omega$ is the set with all possible outcomes, and we can define events $A,B, \ldots$ as subsets of $\Omega$. Moreover, we can use operations like the union ($\cup$), intersection ($\cap$), complement $A^c$, and difference $A\setminus B$. If $A$ is a subset of $B$, this is denoted as $A\subset B$. Finally, the empty set is $\emptyset$.

The following set properties can be derived, where it can be useful to use Venn diagrams to visualize the set operations and relations.

* $A\cup \Omega = \Omega$ and  $A\cap \Omega = A$
* $A\cup \emptyset =A $ and  $A\cap \emptyset  = \emptyset $ 
* If $A\subset B$, then $A\cup B = B$ and $A\cap B = A$
* If $A\subset B$ and $B\subset C$, then $A\subset C$ (transitive property)
* $A\cup B=B\cup A$ and $A\cap B=B\cap A$ (commutative property)
* $(A\cup B)\cup C = A\cup (B\cup C)$ and $(A\cap B)\cap C = A\cap (B \cap C)$ (associative property)
* $(A\cup B)\cap C = (A\cap B) \cup (B \cap C)$ (distributive property)
*  $(A\cup B)^c=(A^c \cap B^c)$ and $(A\cap B)^c=(A^c \cup B^c)$ (DeMorgan's Laws)

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Rock example}$

We have a barrel with 20 rocks (equal in size and shape), 10 contain the rare earth element neodymium, 10 do not. If we randomly pick a rock from the barrel, it is thus equally likely that it contains neodymium or not. Picking a rock with neodymium is indicated as outcome $s$, picking a rock without noedymium as outcome $o$. If we pick two rocks with replacement (i.e., after picking the first it is put back) can then distinguish the following 16 events:

$\emptyset$

$\{so\}, \{os\}, \{ss\}, \{oo\}$

$\{so,os\}, \{so,ss\}, \{so,oo\}, \{os,ss\}, \{os,oo\}, \{ss,oo\}$

$\{so,os,oo\}, \{so,os,ss\}, \{so,ss,oo\}, \{os,ss,oo\}$

$\Omega = \{so,os,oo,ss\}$

For instance we can look at the events:

* $A=$  {one rock with neodymium and one without} $= \{so,os\}$, which means $\mathsf{P}(A)=\frac{2}{4}$
* $B=$ {second rock with neodymium} $= \{os,ss\}$, which means $\mathsf{P}(B)=\frac{2}{4}$
* $A\cap B =  \{os\}$, which means $\mathsf{P}(A\cap B)=\frac{1}{4}$
* $A\cup B =  \{so,os,ss\}$, which means $\mathsf{P}(A\cap B)=\frac{3}{4}$

We can observe thatin this case $\mathsf{P}(A\cap B) \neq \mathsf{P}(A) + \mathsf{P}(B)$. The reason is that $A$ and $B$ are not mutually exclusive: outcome $os$ is an element of both events, and if we would add up the probabilities of both events, this outcome would be counted twice. The common outcome is the same as the intersection  $A\cap B=\{os\}$. From this follows that 

$$
\begin{align*}
\mathsf{P}(A\cup B) &= \mathsf{P}(A) + \mathsf{P}(B)- \mathsf{P}(A\cap B)\\ &= \mathsf{P}(\{so,os\}) + \mathsf{P}(\{os,ss\})- \mathsf{P}(\{os\})=\frac{2}{4}+\frac{2}{4}-\frac{1}{4}=\frac{3}{4}
\end{align*}
$$

</div>

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Addition rule}:$

$\mathsf{P}(A\cup B) = \mathsf{P}(A) + \mathsf{P}(B)- \mathsf{P}(A\cap B)$
</div>

Note that this does not conflict with the third axiom we defined before, since if the events $A$ and $B$ are *disjoint* (i.e., have no outcomes in common), we have that $\mathsf{P}(A\cup B)=0$.

## What's next

In the following section we will look at conditional probabilities and independence, after which we will move on to the concept of *random variables* and probability distributions, which allows us to evaluate probabilities of events, both in case of countable and noncountable outcomes.

## Exercises

:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292824181516343687/embed" aria-label="Q01" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292824199861224337/embed" aria-label="Q02" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292824211660614697/embed" aria-label="Q03" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::

:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292824251734893837/embed" aria-label="Q04" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::