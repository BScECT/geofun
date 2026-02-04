# From data to insights

## Why learning statistics?

In his New York Times' article [*For Today’s Graduate, Just One Word: Statistics*](https://www.nytimes.com/2009/08/06/technology/06stats.html), Steve Lohr transcribes the essence of statistics:

  > Yet data is merely the raw material of knowledge. "We’re rapidly entering a world where everything can be monitored and measured," said Erik Brynjolfsson, an economist and director of the Massachusetts Institute of Technology’s Center for Digital Business. "But the big problem is going to be the ability of humans to use, analyze and make sense of the data."

So one reason to learn statistics is vocational: data are invaluable for decision making, but that requires first to know how to manipulate and analyze them. This is especially true in the Earth sciences, where processes happen over spatial and temporal scales so large that observing them is difficult.

Another reason is more general: statistics are used in all aspects of our society, from medicine to the economy. In her essay *Marx, Marshall, and Keynes*, The economist Joan Robinson says:

  > The purpose of studying economics is not to acquire a set of ready-made answers to economic questions, but to learn how to avoid being deceived by economists.

And the same applies to statistics.

## What lies behind statistics?

### Probability theory

Probability theory provides a formal framework to reason under uncertainty. Uncertainty is often divided into two types:

  * *Aleatoric uncertainty*, which is an inherent ambiguity in the data (due to measurement noise for instance), so it is irreducible and would persist even with infinite data (unless we introduce new variables).
  * *Epistemic uncertainty*, which is a lack of knowledge (due to multiple models matching the data equally well for instance), so it is reducible and would vanish with infinite data (or potentially with a refined model).

Probability theory results from a long history, starting in the 17th century with a [correspondence between Blaise Pascal and Pierre de Fermat](https://www.aps.org/apsnews/2009/07/pascal-letters-fermat-points) on gambling problems and continuing today with [Daphne Koller’s research](https://www.technologyreview.com/technology/bayesian-machine-learning/) on making predictions based on incomplete knowledge of the world.

### Statistics

Statistics supports the quantitative analysis and interpretation of data. It is often divided into two main branches:

  * *Descriptive statistics*, which aims at analyzing and summarizing the available data by measuring central tendency and variability and by plotting.
  * *Inferential statistics*, which aims at generalizing beyond the data themselves by testing hypotheses and by making predictions.

While some of its concepts can be traced back to the [8th century](https://en.wikipedia.org/wiki/Founders_of_statistics), statistics was formalized as a discipline with applications behind science during the 19th and 20th centuries, especially under the impulsion of British figures such as [Francis Galton](https://doi.org/10.1111/j.1740-9713.2019.01275.x) and [Florence Nightingale](https://www.scientificamerican.com/article/how-florence-nightingale-changed-data-visualization-forever)

### Data science

Data science focuses on building data-driven models to make predictions. It is deeply linked to two concepts:

  * *Big data*, which refers to large, sometimes rapidly growing, datasets made of diverse data that traditional data-processing tools struggle to handle.
  * *Machine learning*, which focuses on developing algorithms that learn to perform tasks from data directly, so without explicit, hard-coded instructions.

Data science emerged in the late 20th century from two perspectives: one sought to integrate the advances in programming and high-performance computing that scientists like [Frances Allen](https://amturing.acm.org/award_winners/allen_1012327.cfm) had enabled into statistical analysis; the other, as advocated by [Leo Breiman](https://senate.universityofcalifornia.edu/_files/inmemoriam/html/leobreiman.htm), sought to respond to the growing gap between theoretical statistics and practical data needs across disciplines (like geoscience, biology, and medicine).

## How to put statistics into practice?

The data-to-insight workflow formalizes the different steps to extract insights from data ({numref}`figure {number} <data-to-insight_workflow>`), which can be grouped into four main parts:

  * Formulating a problem, usually as a question to answer ({numref}`figure {number} <data-to-insight_workflow>`, 1), e.g., *how to guarantee that there will be enough safe and clean drinking water in country X within the next Y years?*.
  * Determining what kind of data are needed to answer the question and where to get it from ({numref}`figure {number} <data-to-insight_workflow>`, 2 & 3), e.g., is it already available online or does it need to be acquired?
  * Processing and analyzing the data then evaluating the results ({numref}`figure {number} <data-to-insight_workflow>`, 4, 5, & 6), e.g., are the data clean, do they need to be transformed, how reliable are the results?
  * Interpreting the results and communicating them to colleagues and stakeholders ({numref}`figure {number} <data-to-insight_workflow>`, 7), e.g., what are our conclusions and how to best present them?

````{figure} ../../figures/part-a_data-to-insight_workflow.svg
---
name: data-to-insight_workflow
width: 60%
align: center
---
Overview of the data-to-insight workflow.
````

This workflow is iterative by nature at two levels:

  * At the level of the entire workflow, because the conclusion could be that more or different data are required to answer a given question reliably.
  * At the level of the processing, analysis, and evaluation, because this step usually involves some form of statistical modeling, and it is always better to start from the simplest model possible and only add complexity if required.

## What does it look like?

Here are four examples of how probability theory, statistics, and data science are used in practice. Note that some of those examples use methods that you will only see later in the bachelor and master programs.

### Example 1: tracking subsidence

Data acquisition and analysis has played a big role into quantifying and communicating about subsidence in Central Valley (CA, USA). You can find an overview of the problem and of the data gathered to map it [here](https://www.usgs.gov/tools/central-valley-drought-indicators). This subsidence is due to the over-exploitation of the aquifers in the subsurface, with groundwater withdrawal leading to compaction. And it is worsening because of changes of land use combined with longer and more intense droughts under climate change.

### Example 2: climate change attribution

Climate simulations and probabilities are cornerstones to climate attribution, i.e., quantifying whether climate change made extreme events more likely or more severe. You can find more explanations about how it works [here](https://www.climate.gov/news-features/understanding-climate/extreme-event-attribution-climate-versus-weather-blame-game). This also helps us to plan for the future, for instance to manage the use of groundwater between different sectors and avoid depleting aquifers entirely.

### Example 3: predicting at depth

Statistics also plays a major role in predicting the physical properties of the subsurface, which gives us an important tool to manage subsurface resources like groundwater. You can find a 3D model of sediment distributions for the Central Valley [here](https://ca.water.usgs.gov/projects/central-valley/cvhm-texture-model.html). It was built using specific methods from geostatistics, a branch of statistics focusing on spatial or spatio-temporal datasets, which you will study in the second year.

### Example 4: building AI systems

Artifical intelligence (AI) focuses on developing computer systems that perform tasks typically associated with human intelligence, such as learning, reasoning, and planning. Machine learning is a subfield of AI that plays a big role in modern systems like ChatGPT. ChatGPT itself is a large language model (LLM) that learns statistical relationships between words from huge text datasets to then generate (seemingly) new texts. You can find more information about how those LLMs work [here](https://ig.ft.com/generative-ai).
