(CondP)=
# Conditional probability and independence

## Learning objectives

After studying Conditional probability and independence you will be able to explain and apply ...
* conditional probability
* the total probability rule
* Bayes' rule
* the concept of independence

## Conditional probability

Very often we are interested in probabilities of event $A$ occurring **given** that an event $B$ occurred. Examples are:

Probability that
* … it will rain today **given** that it is cloudy
* … email is spam **given** that subject contains the word ”free”
* … a person will conduct a crime **given** that they use hard drugs
* … an avalanche will occur **given** that a warning was issued
* … Northern light	will occur **given** that a solar flare was observed
* … GPS disruption	will occur **given** that a Northern light was observed
* … volcano eruption in next 5 years will occur **given** that the	volcano did not erupt for 50 years
* … a tsunami will occur **given** that a sub-sea earthquake with M>5.0 occurred
* … a storm surge will occur **given** a hurricane path
* … pixel is water	**given** that satellite spectral value is smaller than a certain threshold
 
 These are all examples of *conditional* probabilities, denoted as $\mathsf{P}(A|B)$.


<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Conditional probability } \mathsf{P}(A|B):$

This is the probability that event $A$ occurs given that event $B$ occurs:

$\mathsf{P}(A|B) = \frac{\mathsf{P}(A\cap B)}{\mathsf{P}(B)}$

</div>

The conditional probability is thus the probability of event $A$ in the 'reduced' sample space $B$. This may be easier to see if we look at relative frequencies: the conditional probability being the number of times that $A$ and $B$ occur ($n_{A\cap BS}$) divided by the number of times $B$ occurs, $n_B$, i.e., $n_{A\cap B}/n_B$.

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example throwing a fair die}$

The probability of throwing a 3 given that we throw uneven is:

$\mathsf{P}(A|B) = \frac{\mathsf{P}(A\cap B)}{\mathsf{P}(B)}= \frac{1/6}{3/6} =\frac{1}{3}$

This can also be seen by looking at the events $A=\{3\}$, $B=\{1,3,5\}$. If we consider $B$ as the 'reduced' sample space, it is easy to see that there is a probability of 1/3 that to get a $\{3\}$ ($=A\cap B$).

</div>

````{figure} ../../figures/part-a_Venn_CondP.png
---
name: venn_condP
width: 30%
align: center
---
Venn diagram to illustrate that for conditional probability $\mathsf{P}(A|B)$ we need to evaluate the probability of $A\cap B$ within the 'reduced' sample space $B$.
````

From the definition of conditional probability it follows that:

$$
\begin{align*}
\mathsf{P}(A\cap B) &= \mathsf{P}(A|B)\mathsf{P}(B)\\
&= \mathsf{P}(B|A)\mathsf{P}(A)\\
\end{align*}
$$

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example testing rocks}$

Two rocks are tested on the presence of neodymium. Result of a test is either 'detection', denoted as outcome $s$, or 'not detected', denoted as outcome $o$. The sample space is thus $\Omega = \{ss,so,os,oo\}$, and the following probabilities are given:

$\mathsf{P}(\{ss\})=0.5,\; \mathsf{P}(\{so\})=\mathsf{P}(\{os\})=0.2,\;\mathsf{P}(\{oo\})=0.1$.

What is the probability that testing the second rock results in 'not detected' given that for the first rock the outcome was 'not detected'.

We then have

$\mathsf{P}(A)=\mathsf{P}(\{\text{'not detected' for first rock}\})=\mathsf{P}(\{os\})+\mathsf{P}(\{oo\})=0.3$

$\mathsf{P}(A\cap B)=\mathsf{P}(\{\text{'not detected' for first and second rock}\})=\mathsf{P}(\{oo\})=0.1$

The asked for conditional probability is then:

$\mathsf{P}(B|A)=\frac{\mathsf{P}(A\cap B)}{\mathsf{P}(A)}= \frac{0.1}{0.3} = \frac{1}{3} $

</div>


## Total probability and Bayes' rule

Earlier we have seen that for disjoint sets $A$ and $B$ we have that $\mathsf{P}(A\cup B) = \mathsf{P}(A) + \mathsf{P}(B)$. Obviously, $A$ and $A^c$ are disjoint sets, and their union is equal to the sample space: $A\cup A^c = \Omega$. We can also look at a *partition* of the sample space comprising more than two sets.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Partition of sample space } \Omega:$

a collection of $n$ disjoint subsets $B_i$ with their union equal to the sample space

$\bigcup_{i=1}^n B_i = B_1 \cup B_2 \cup B_3 \ldots = \Omega$

</div>

This also implies that the third axiom of probability can be extended to $\mathsf{P}(\bigcup_{i=1}^n B_i) = \mathsf{P}(B_1) + \mathsf{P}(B_2) +\ldots + \mathsf{P}(B_n)$ for $n$ disjoint subsets $B_i$. 

An example with three disjoint subsets is shown in ({numref}`figure {number} <venn_part>`). In that figure, also a set $A$ is shown, for which we can see that:

$$A = (A\cap B_1)\cup(A\cap B_2)\cup(A\cap B_3)$$

````{figure} ../../figures/part-a_Venn_part.png
---
name: venn_part
width: 40%
align: center
---
Venn diagram with partition of three disjoint sets $B_i$, and intersections with set $A$.
````

Since the $B_i$ are disjoint, also the subsets $(A\cap B_i)$ are disjoint, and hence

$$
\begin{align*}
\mathsf{P}(A) &= \mathsf{P}(A\cap B_1)+\mathsf{P}(A\cap B_2)+\mathsf{P}(A\cap B_3)\\
&= \sum_{i=1}^3 \mathsf{P}(A\cap B_i)\\
&= \sum_{i=1}^3 \mathsf{P}(A|B_i)\mathsf{P}(B_i)
\end{align*}
$$

where the last equality follows from the definition of conditional probability.

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Total probability rule}:$

If events $B_i$ form a partition of sample space $\Omega$ then:

$\mathsf{P}(A) = \sum_{i=1}^n \mathsf{P}(A|B_i)\mathsf{P}(B_i)$

</div>

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example of total probability with rocks}$

We have a collection of rocks of which 70\% is igneous and 30\% is metamorphic. Among the igneous rocks 40\% contains neodymium, among the metamorphic rock that is 45\%.

What is the probability that a randomly picked rock contains neodymium?

Based on the given information we have
* event $B_1 =$ {igneous rock} with $\mathsf{P}(B_1)=0.7$
* event $B_2 =$ {metamorphic rock} with $\mathsf{P}(B_2)=0.3$
* event $A =$ {contains neodymium}
* $\mathsf{P}(A|B_1)=0.4$ and $\mathsf{P}(A|B_2)=0.45$

Application of the total probability rule gives:

$$
\begin{align*}
\mathsf{P}(A) &= \mathsf{P}(A|B_1)\mathsf{P}(B_1) + \mathsf{P}(A|B_2)\mathsf{P}(B_2)\\
&= 0.4 \cdot 0.7 + 0.45\cdot 0.3 \\&= 0.415
\end{align*}
$$

</div>

Recall that we have $\mathsf{P}(A\cap B_j)=\mathsf{P}(B_j|A)\mathsf{P}(A) = \mathsf{P}(A|B_j)\mathsf{P}(B_j) $. Using this together with the total probabiblity rule, we can derive Bayes' rule as follows:

$$
\mathsf{P}(B_j|A) = \frac{\mathsf{P}(A|B_j)\mathsf{P}(B_j)}{\mathsf{P}(A)}
=\frac{\mathsf{P}(A|B_j)\mathsf{P}(B_j)}{ \sum_{i=1}^n \mathsf{P}(A|B_i)\mathsf{P}(B_i)}
$$

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Bayes' rule}:$

If events $B_i$ form a partition of sample space $\Omega$ then for any event $B_j$ in the partition:

$\mathsf{P}(B_j|A) = \frac{\mathsf{P}(A|B_j)\mathsf{P}(B_j)}{ \sum_{i=1}^n \mathsf{P}(A|B_i)\mathsf{P}(B_i)}$

</div>

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example of total probability with rocks (continued)}$

Application of Bayes' rule allows to also find the conditional probability that a rock is igneous given that it contains neodymium:

$$
\begin{align*}
\mathsf{P}(B_1|A) &= \frac{\mathsf{P}(A|B_1)\mathsf{P}(B_1)} { \sum_{i=1}^2 \mathsf{P}(A|B_i)\mathsf{P}(B_i)}\\
&= \frac{0.4 \cdot 0.7} {0.4 \cdot 0.7 + 0.45\cdot 0.3}=0.675
\end{align*}
$$

</div>

(Indep)=
## Independence

<div style="background-color:#5f9c96; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Independence}:$

Two events $A$ and $B$ are mutually independent if $\mathsf{P}(B|A) = \mathsf{P}(B)$ and $\mathsf{P}(A|B) = \mathsf{P}(A)$

</div>

This can be generalized to $n$ independent events: the intersection of any number of subset of these events is equal to the product of the individual events in the subset. For instance with three independent events we have:

$$
\begin{align*}
\mathsf{P}(A_1\cap A_2) &= \mathsf{P}(A_1)\mathsf{P}(A_2)\\
\mathsf{P}(A_1\cap A_3) &= \mathsf{P}(A_1)\mathsf{P}(A_3)\\
\mathsf{P}(A_2\cap A_3) &= \mathsf{P}(A_2)\mathsf{P}(A_3)\\
\mathsf{P}(A_1\cap A_2\cap A_3) &= \mathsf{P}(A_1)\mathsf{P}(A_2)\mathsf{P}(A_3)
\end{align*}
$$

The concept of independence is very important, for instance in the context of repeated trials in an experiment, or for assessing system reliability.

<div style="background-color:#CAE7D3; color: black; width:95%; vertical-align: middle; padding:15px; margin: 10px; border-radius: 10px">
<p>

$\textbf{Example system reliability}$

System reliability depends on the reliability of each of its components. Hence, in order to determine the system reliability, or conversely the failure probability of the system, one needs to determine the failure probability of all components. Once all failure probabilities are known, it is possible to calculate the system reliability or failure probability of the complete system. For that purpose diagrams are used that show the relations and dependences of all components. 

Two basic relations are shown in FIGURE. On the left two parallel components are shown, which means that the system can operate as long as one of the components works properly. For instance, a satellite will have redundant power components to ensure it can still operate if one fails. The system will fail if \textbf{both} $A$ \textbf{and} $B$ occur. If failure of each of the components is independent, the failure probability $\mathsf{P}_F$ is equal to:

$$\mathsf{P}_F = P(A\cap B) = P(A)P(B)$$

If a third component would be added parellel to $A$ and $B$, with $C$ the event that it fails independent from the other components, the failure probability would becomes $\mathsf{P}_F = \mathsf{P}(A\cap B\cap C) = \mathsf{P}(A)\mathsf{P}(B)\mathsf{P}(C)$.
Since $P(C)$ will be smaller than 1, this shows that the failure probability decreases by adding more components in parallel. Alternatively, one can also say that the reliability $\mathsf{R} = 1-\mathsf{P}_F$ increases. 

FIGURE also shows two components in a series. For instance, the power system of a satellite only works if solar arrays and battery operate properly (and many more components). Hence, the system will fail if $A$ **or** $B$ occurs (or both). If $A$ and $B$ are again independent, the failure probability $\mathsf{P}_F$ is now equal to:

$$
\begin{align*} 
\mathsf{P}_F &= P(A\cup B) = P(A) + P(B) - P(A\cap B)\\
&= P(A) + P(B) - P(A)P(B)\\
&=1-(1-P(A))(1-P(B)) \\
&= 1 - P(A^c)P(B^c)
\end{align*}
$$

The system reliability is thus equal to $\mathsf{R}=\mathsf{P}(A^c)\mathsf{P}(B^c)$.

Adding a third component in a series, with $C$ the event that it fails independent from the other components, would make the failure probability become $\mathsf{P}_F = \mathsf{P}(A\cup B\cup C)=1-\mathsf{P}(A^c)\mathsf{P}(B^c)\mathsf{P}(C^c)$.
Hence, the failure probability increases by adding more components in a series, which is as expected since each component makes the system more susceptible to failure.

</div>

:::{card} Exercises

<iframe src="https://tudelft.h5p.com/content/1292827810544191377/embed" aria-label="Q05_Bayes" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292827823249190307/embed" aria-label="Q06_totalP" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292827827161330647/embed" aria-label="Q07" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292827839811357777/embed" aria-label="Q08_system" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

<iframe src="https://tudelft.h5p.com/content/1292827853278700257/embed" aria-label="Q09_condprob" width="1088" height="637" frameborder="0" allowfullscreen="allowfullscreen" allow="autoplay *; geolocation *; microphone *; camera *; midi *; encrypted-media *"></iframe><script src="https://tudelft.h5p.com/js/h5p-resizer.js" charset="UTF-8"></script>

:::